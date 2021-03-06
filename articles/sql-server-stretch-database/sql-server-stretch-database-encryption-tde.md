---
title: Ativar a encriptação de dados transparente para o Stretch Database - Azure | Documentos da Microsoft
description: Ativar a encriptação de dados transparente (TDE) para SQL Server Stretch Database, no Azure
services: sql-server-stretch-database
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1e40e3d9eb1231666acda89c752ebc8f517e8fc6
ms.sourcegitcommit: 21466e845ceab74aff3ebfd541e020e0313e43d9
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/21/2018
ms.locfileid: "53741543"
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Ativar a encriptação de dados transparente (TDE) para Stretch Database no Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Encriptação de dados transparente (TDE) ajuda a proteger contra ameaças de atividades maliciosas através de encriptação em tempo real e a desencriptação da base de dados, cópias de segurança associadas e ficheiros de registo de transação em repouso sem a necessidade de alterações à aplicação.

TDE criptografa o armazenamento de uma base de dados completa com uma chave simétrica denominada a chave de encriptação da base de dados. A chave de encriptação da base de dados está protegida por um certificado de servidor interno. O certificado de servidor interno é exclusivo para cada servidor do Azure. Microsoft gira automaticamente estes certificados, pelo menos a cada 90 dias. Para obter uma descrição geral de TDE, consulte [encriptação de dados transparente (TDE)].

## <a name="enabling-encryption"></a>Ativar a encriptação
Para ativar a TDE para um Azure, base de dados que está armazenando os dados migrados de uma base de dados do SQL Server com a Stretch ativada, efetue os seguintes procedimentos:

1. Abrir a base de dados no [portal do Azure](https://portal.azure.com)
2. No painel da base de dados, clique nas **definições** botão
3. Selecione o **encriptação de dados transparente** opção ![][1]
4. Selecione o **nos** definição e, em seguida, selecione **guardar**
   ![][2]

## <a name="disabling-encryption"></a>A desativação da encriptação
Para desativar a TDE para um Azure base de dados que está armazenando os dados migrados de uma base de dados do SQL Server com a Stretch ativada, efetue os seguintes procedimentos:

1. Abrir a base de dados no [portal do Azure](https://portal.azure.com)
2. No painel da base de dados, clique nas **definições** botão
3. Selecione o **encriptação de dados transparente** opção
4. Selecione o **Off** definição e, em seguida, selecione **guardar**

<!--Anchors-->
[Encriptação de dados transparente (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
