---
title: Exemplo da CLI - criar uma base de dados SQL do Azure | Microsoft Docs
description: Utilize este script de exemplo da CLI do Azure para criar uma base de dados SQL.
services: sql-database
ms.service: sql-database
ms.subservice: single-database
ms.custom: ''
ms.devlang: azurecli
ms.topic: sample
author: CarlRabeler
manager: craigg
ms.author: carlrab
ms.reviewer: ''
ms.date: 02/08/2019
ms.openlocfilehash: 9ed1512053c06108178275b0523beede470325a5
ms.sourcegitcommit: 43b85f28abcacf30c59ae64725eecaa3b7eb561a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/09/2019
ms.locfileid: "59361429"
---
# <a name="use-cli-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a>Utilizar a CLI para criar uma base de dados SQL do Azure única e configurar uma regra de firewall

Este exemplo de script da CLI do Azure cria uma base de dados SQL do Azure e configura uma regra de firewall ao nível do servidor. Assim que o script tiver sido executado com êxito, a Base de Dados SQL pode ser acedida a partir de todos os serviços do Azure e do endereço IP configurado.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se optar por instalar e usar a CLI localmente, este tópico requer a execução da versão 2.0 ou posterior da CLI do Azure. Executar `az --version` para localizar a versão. Se precisar de instalar ou atualizar, veja [Instalar a CLI do Azure]( /cli/azure/install-azure-cli).

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a>Limpar a implementação

Utilize o seguinte comando para remover o grupo de recursos e todos os recursos associados à mesma.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação do script

Este script utiliza os seguintes comandos. Cada comando na tabela liga à documentação específica do comando.

| Comando | Notas |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az sql server create](/cli/azure/sql/server#az-sql-server-create) | Cria um servidor de base de dados SQL que aloja uma base de dados individual ou um conjunto elástico. |
| [az sql server firewall create](/cli/azure/sql/server/firewall-rule#az-sql-server-firewall-rule-create) | Cria uma regra de firewall para permitir o acesso a todas as bases de dados únicas, conjuntos de um elásticos no servidor de base de dados SQL do intervalo de endereços IP introduzido. |
| [az sql db create](/cli/azure/sql/db#az-sql-db-create) | Cria uma base de dados individual ou um conjunto elástico. |
| [eliminação do grupo de AZ](/cli/azure/resource#az-resource-delete) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos Seguintes

Para obter mais informações sobre a CLI do Azure, veja [Documentação da CLI do Azure](https://docs.microsoft.com/cli/azure).

Pode ver exemplos do script da CLI da Base de Dados SQL adicionais na [Documentação da Base de Dados SQL do Azure](../sql-database-cli-samples.md).