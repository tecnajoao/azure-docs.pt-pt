---
title: Utilizar bases de dados fornecidos pela RP de adaptador MySQL no AzureStack | Documentos da Microsoft
description: Como criar e gerir bases de dados MySQL aprovisionados com o fornecedor de recursos do adaptador de MySQL
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2019
ms.author: jeffgilb
ms.reviewer: quying
ms.lastreviewed: 10/16/2018
ms.openlocfilehash: 6eaba728b794c0102ec4e28791b218efa28b51b5
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/13/2019
ms.locfileid: "56160769"
---
# <a name="create-mysql-databases"></a>Criar bases de dados MySQL
Um utilizador do Azure Stack, subscrever uma oferta que inclui o serviço de base de dados do MySQL, pode criar e gerir Self-serviços bases de dados MySQL no portal de utilizador.

## <a name="create-a-mysql-database"></a>Criar uma base de dados MySQL

1. Inicie sessão no portal de utilizador do Azure Stack.
2. Selecione **+ criar um recurso** > **dados + armazenamento** > **base de dados MySQL** > **adicionar**.
3. Sob **criar a base de dados do MySQL**, introduza o nome de base de dados e configure as outras definições conforme necessário para o seu ambiente.

    ![Criar um teste de base de dados MySQL](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. Sob **Create Database**, selecione **SKU**. Sob **selecionar um SKU MySQL**, escolha o SKU da base de dados.

    ![Selecionar um SKU de MySQL](./media/azure-stack-mysql-rp-deploy/mysql-select-sku.png)

    >[!Note]
    >Servidores de alojamento são adicionadas ao Azure Stack, que lhes foram atribuídas um SKU. Bases de dados são criadas no conjunto de servidores num SKU de hospedagem.

5. Sob **início de sessão**, selecione ***configurar definições necessárias***.
6. Sob **selecionar um início de sessão**, pode escolher um início de sessão existente ou selecione **+ criar um novo início de sessão** para configurar um novo início de sessão.  Introduza um **início de sessão da base de dados** nome e **palavra-passe**e, em seguida, selecione **OK**.

    ![Criar um novo início de sessão de banco de dados](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    >[!NOTE]
    >O comprimento do nome de início de sessão da base de dados não pode exceder 32 carateres no MySQL 5.7. Nas edições anteriores, ele não pode exceder os 16 carateres.

7. Selecione **criar** para concluir a configuração da base de dados.

Depois da base de dados é implementado, anote o **cadeia de ligação** sob **Essentials**. Pode usar essa cadeia de caracteres em qualquer aplicativo que precise acessar o banco de dados MySQL.

![Obter a cadeia de ligação para a base de dados MySQL](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

## <a name="update-the-administrative-password"></a>Atualizar a palavra-passe administrativa

É possível modificar a palavra-passe ao alterá-la na instância do servidor MySQL.

1. Selecione **recursos administrativos** > **MySQL alojar servidores**. Selecione o servidor de alojamento.
2. Sob **configurações**, selecione **palavra-passe**.
3. Sob **palavra-passe**, introduza a palavra-passe nova e, em seguida, selecione **guardar**.

![Atualizar a palavra-passe de administrador](./media/azure-stack-mysql-rp-deploy/mysql-update-password.png)

## <a name="next-steps"></a>Passos Seguintes

[Update the MySQL resource provider](azure-stack-mysql-resource-provider-update.md) (Atualizar o fornecedor de recursos do MySQL)
