---
title: Reinicie a base de dados do Azure para o servidor de MariaDB com a CLI do Azure
description: Este artigo descreve como pode reiniciar uma base de dados do Azure para o servidor de MariaDB com a CLI do Azure.
author: ajlam
ms.author: andrela
ms.service: mariadb
ms.topic: conceptual
ms.date: 3/28/2019
ms.openlocfilehash: a6e0509d941d9bfdfe6db7a8b93ee49c5bece1a6
ms.sourcegitcommit: f8c592ebaad4a5fc45710dadc0e5c4480d122d6f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58623082"
---
# <a name="restart-azure-database-for-mariadb-server-using-the-azure-cli"></a>Reinicie a base de dados do Azure para o servidor de MariaDB com a CLI do Azure
Este tópico descreve como pode reiniciar uma base de dados do Azure para MariaDB server. Terá de reiniciar o servidor por motivos de manutenção, o que faz com que uma interrupção curta como o servidor executa a operação.

O reinício do servidor será bloqueado se o serviço está ocupado. Por exemplo, o serviço poderá estar a processar uma operação de pedido anteriormente, como o dimensionamento vCores.

O tempo necessário para concluir um reinício depende do processo de recuperação MariaDB. Para diminuir o tempo de reinício, recomendamos que estará a minimizar a quantidade de atividade ocorrida no servidor antes do reinício.

## <a name="prerequisites"></a>Pré-requisitos
Para concluir este guia de procedimentos, terá de:
- Um [base de dados do Azure para o servidor de MariaDB](quickstart-create-mariadb-server-database-using-azure-cli.md)

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

> [!IMPORTANT]
> Este guia de procedimentos é necessário utilizar a CLI do Azure versão 2.0 ou posterior. Para confirmar a versão, no prompt de comando da CLI do Azure, introduza `az --version`. Para instalar ou atualizar, veja [instalar a CLI do Azure]( /cli/azure/install-azure-cli).


## <a name="restart-the-server"></a>Reinicie o servidor

Reinicie o servidor com o seguinte comando:

```azurecli-interactive
az mariadb server restart --name mydemoserver --resource-group myresourcegroup
```

## <a name="next-steps"></a>Passos Seguintes

Saiba mais sobre [como definir parâmetros na base de dados do Azure para MariaDB](howto-configure-server-parameters-cli.md)