---
title: Copiar uma base de dados SQL do Azure | Documentos da Microsoft
description: Crie uma cópia transacional consistente da base de dados SQL do Azure existente no mesmo servidor ou um servidor diferente.
services: sql-database
ms.service: sql-database
ms.subservice: data-movement
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: CarlRabeler
ms.author: sahsan
ms.reviewer: carlrab
manager: craigg
ms.date: 04/11/2019
ms.openlocfilehash: 47aa88040b6010aeca4aeed696310505d1e17df9
ms.sourcegitcommit: 031e4165a1767c00bb5365ce9b2a189c8b69d4c0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/13/2019
ms.locfileid: "59549700"
---
# <a name="copy-a-transactionally-consistent-copy-of-an-azure-sql-database"></a>Copiar uma cópia transacional consistente de uma base de dados SQL do Azure

Base de dados SQL do Azure fornece vários métodos para criar uma cópia transacional consistente da base de dados SQL do Azure existente no mesmo servidor ou um servidor diferente. Pode copiar uma base de dados SQL utilizando o portal do Azure, o PowerShell ou o T-SQL. 

## <a name="overview"></a>Descrição geral

Uma cópia da base de dados é um instantâneo da base de dados de origem no momento do pedido de cópia. Pode selecionar o mesmo servidor ou um servidor diferente, o escalão de serviço e o tamanho de computação ou um tamanho de computação diferentes dentro da mesma camada de serviço (edição). Depois da cópia estiver concluída, torna-se uma base de dados totalmente funcional e independente. Neste momento, pode atualizar ou mudar a versão para todas as edições. Os inícios de sessão, utilizadores e permissões podem ser geridas de forma independente.  

> [!NOTE]
> [Cópias de segurança da base de dados automatizadas](sql-database-automated-backups.md) são utilizadas quando cria uma cópia da base de dados.

## <a name="logins-in-the-database-copy"></a>A cópia da base de dados de inícios de sessão

Quando copiar uma base de dados para o mesmo servidor de base de dados SQL, inícios de sessão mesmo podem ser utilizados em ambas as bases de dados. O principal de que usar para copiar a base de dados de segurança se torna o proprietário da base de dados na base de dados nova. Todos os utilizadores de base de dados, as respetivas permissões e seus identificadores de segurança (SIDs) são copiados para a cópia da base de dados.  

Quando copiar uma base de dados para um servidor de base de dados SQL diferente, o principal no novo servidor de segurança se torna o proprietário da base de dados na base de dados nova. Se usar [utilizadores de base de dados contidos](sql-database-manage-logins.md) para acesso a dados, certifique-se de que as bases de dados primários e secundários têm sempre as mesmas credenciais de utilizador, para que quando a cópia estiver concluída pode imediatamente acessá-lo com as mesmas credenciais . 

Se usar [do Azure Active Directory](../active-directory/fundamentals/active-directory-whatis.md), pode eliminar completamente a necessidade de gerir as credenciais na cópia. No entanto, quando copiar a base de dados para um novo servidor, o acesso com base no início de sessão poderão não funcionar, porque os inícios de sessão não existe no novo servidor. Para saber mais sobre a gestão de inícios de sessão quando copiar uma base de dados para um servidor diferente da base de dados SQL, veja [como gerir a segurança de base de dados SQL do Azure após a recuperação após desastre](sql-database-geo-replication-security-config.md). 

Depois da cópia for concluída com êxito e antes de outros utilizadores são remapeados, apenas o início de sessão que iniciou a cópia, o proprietário da base de dados, pode iniciar sessão para a nova base de dados. Para resolver os inícios de sessão depois de concluída a operação de cópia, veja [resolver inícios de sessão](#resolve-logins).

## <a name="copy-a-database-by-using-the-azure-portal"></a>Copiar uma base de dados com o portal do Azure

Para copiar uma base de dados com o portal do Azure, abra a página da base de dados e, em seguida, clique em **cópia**. 

   ![Cópia da base de dados](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>Copiar uma base de dados com o PowerShell

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]
> [!IMPORTANT]
> O módulo do PowerShell do Azure Resource Manager ainda é suportado pelo SQL Database do Azure, mas todo o desenvolvimento futuro é para o módulo de Az.Sql. Para estes cmdlets, consulte [azurerm. SQL](https://docs.microsoft.com/powershell/module/AzureRM.Sql/). Os argumentos para os comandos no módulo Az e nos módulos AzureRm são substancialmente idênticos.

Para copiar uma base de dados com o PowerShell, utilize o [New-AzSqlDatabaseCopy](/powershell/module/az.sql/new-azsqldatabasecopy) cmdlet. 

```powershell
New-AzSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

Para obter um script de exemplo completo, consulte [copiar uma base de dados para um novo servidor](scripts/sql-database-copy-database-to-new-server-powershell.md).

## <a name="copy-a-database-by-using-transact-sql"></a>Copiar uma base de dados com o Transact-SQL

Inicie sessão na base de dados mestra com o início de sessão principal ao nível do servidor ou o início de sessão que criou a base de dados que pretende copiar. Para a base de dados a copiar para ter êxito, inícios de sessão que não são o principal ao nível do servidor tem de ser membros da função dbmanager. Para obter mais informações sobre os inícios de sessão e ligar ao servidor, consulte [gerir inícios de sessão](sql-database-manage-logins.md).

Comece a copiar a base de dados de origem com o [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) instrução. Executando esta instrução inicia o processo de copiar a base de dados. Como copiar uma base de dados é um processo assíncrono, a instrução CREATE DATABASE devolve antes da cópia da base de dados está concluída.

### <a name="copy-a-sql-database-to-the-same-server"></a>Copiar uma base de dados SQL para o mesmo servidor

Inicie sessão na base de dados mestra com o início de sessão principal ao nível do servidor ou o início de sessão que criou a base de dados que pretende copiar. Para a base de dados a copiar para ter êxito, inícios de sessão que não são o principal ao nível do servidor tem de ser membros da função dbmanager.

Este comando copia Database1 para uma nova base de dados com o nome base de dados2 no mesmo servidor. Dependendo do tamanho da base de dados, a operação de cópia pode demorar algum tempo a concluir.

    -- Execute on the master database.
    -- Start copying.
    CREATE DATABASE Database2 AS COPY OF Database1;

### <a name="copy-a-sql-database-to-a-different-server"></a>Copiar uma base de dados SQL para um servidor diferente

Inicie sessão na base de dados mestra do servidor de destino, o servidor de base de dados SQL onde a nova base de dados está a ser criada. Utilize um início de sessão que tenha o mesmo nome e palavra-passe como o proprietário da base de dados da base de dados de origem no servidor de base de dados SQL de origem. O início de sessão no servidor de destino também tem de ser um membro da função dbmanager ou ser o início de sessão principal ao nível do servidor.

Este comando copia Database1 no servidor1 para uma nova base de dados com o nome base de dados2 no Servidor2. Dependendo do tamanho da base de dados, a operação de cópia pode demorar algum tempo a concluir.

    -- Execute on the master database of the target server (server2)
    -- Start copying from Server1 to Server2
    CREATE DATABASE Database2 AS COPY OF server1.Database1;
    
> [!IMPORTANT]
> Firewalls de ambos os servidores tem de ser configurados para permitir a ligação de entrada de IP do cliente de emissão do comando de cópia de T-SQL.

### <a name="copy-a-sql-database-to-a-different-subscription"></a>Copiar uma base de dados SQL para uma subscrição diferente

Pode utilizar o descrbed passos na secção anterior para copiar a base de dados para um servidor de base de dados SQL numa subscrição diferente. Certifique-se de utilizar um início de sessão que tenha o mesmo nome e palavra-passe como o proprietário da base de dados da base de dados de origem e é um membro da função dbmanager ou é o início de sessão principal ao nível do servidor. 

> [!NOTE]
> O [portal do Azure](https://portal.azure.com) não suporta copiar para uma subscrição diferente porque Portal chama a API de ARM e utiliza os certificados de assinatura para aceder a ambos os servidores envolvidos na replicação geográfica.  

### <a name="monitor-the-progress-of-the-copying-operation"></a>Monitorizar o progresso da operação de cópia

Monitorize o processo de copiar ao consultar as exibições sys. Databases e sys.dm_database_copies. Enquanto a cópia estiver em curso, o **state_desc** coluna da vista sys. Databases para a nova base de dados está definida como **COPYING**.

* Se a cópia falhar, o **state_desc** coluna da vista sys. Databases para a nova base de dados está definida como **SUSPEITAR**. Execute a declaração de SOLTAR na base de dados novo e tente novamente mais tarde.
* Se a cópia for bem-sucedida, o **state_desc** coluna da vista sys. Databases para a nova base de dados está definida como **ONLINE**. A cópia estiver concluída e a nova base de dados é uma base de dados regular que pode ser alterada independente da base de dados de origem.

> [!NOTE]
> Se optar por cancelar a cópia enquanto ele estiver em curso, executar o [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) instrução na base de dados nova. Em alternativa, a instrução DROP DATABASE em execução na base de dados de origem também cancela o processo de cópia.

## <a name="resolve-logins"></a>Resolver inícios de sessão

Depois da nova base de dados está online no servidor de destino, utilize o [alterar utilizador](https://msdn.microsoft.com/library/ms176060.aspx) instrução para remapear os utilizadores da base de dados novos inícios de sessão no servidor de destino. Para resolver utilizadores órfãos, veja [resolver problemas relacionados com utilizadores órfãos](https://msdn.microsoft.com/library/ms175475.aspx). Consulte também [como gerir a segurança de base de dados SQL do Azure após a recuperação após desastre](sql-database-geo-replication-security-config.md).

Todos os utilizadores na nova base de dados retém as permissões que eles tinham no banco de dados de origem. O utilizador que iniciou a cópia da base de dados torna-se o proprietário da base de dados da base de dados novo e é atribuído um novo identificador de segurança (SID). Depois da cópia for concluída com êxito e antes de outros utilizadores são remapeados, apenas o início de sessão que iniciou a cópia, o proprietário da base de dados, pode iniciar sessão para a nova base de dados.

Para saber mais sobre a gestão de utilizadores e inícios de sessão quando copiar uma base de dados para um servidor diferente da base de dados SQL, veja [como gerir a segurança de base de dados SQL do Azure após a recuperação após desastre](sql-database-geo-replication-security-config.md).

## <a name="next-steps"></a>Passos Seguintes

* Para obter informações sobre inícios de sessão, consulte [gerir inícios de sessão](sql-database-manage-logins.md) e [como gerir a segurança de base de dados SQL do Azure após a recuperação após desastre](sql-database-geo-replication-security-config.md).
* Para exportar uma base de dados, consulte [exportar a base de dados para um BACPAC](sql-database-export.md).
