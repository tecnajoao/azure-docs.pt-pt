---
title: Exemplo do script da CLI do Azure - encaminhar o tráfego de elevada disponibilidade de aplicativos | Documentos da Microsoft
description: Exemplo do script da CLI do Azure - encaminhar o tráfego de elevada disponibilidade de aplicações
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: jeconnoc
editor: tysonn
tags: azure-infrastructure
ms.assetid: ''
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 04/26/2018
ms.author: kumud
ms.openlocfilehash: 6c610a1cddb0854878d4c2bd5531f88a1cf2ec51
ms.sourcegitcommit: e43ea344c52b3a99235660960c1e747b9d6c990e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/04/2019
ms.locfileid: "59009109"
---
# <a name="route-traffic-for-high-availability-of-applications-using-azure-cli"></a>Encaminhar o tráfego de elevada disponibilidade de aplicações através da CLI do Azure

Este script cria um grupo de recursos, dois planos de serviço de aplicações, duas aplicações web, um perfil do Gestor de tráfego e dois pontos de extremidade de Gestor de tráfego. O Gestor de tráfego direciona o tráfego para a aplicação numa única região, como a região primária e para a região secundária quando a aplicação na região primária estiver indisponível. Antes de executar o script, tem de alterar os valores de MyWebApp, MyWebAppL1 e MyWebAppL2 para valores exclusivos em todo o Azure. Depois de executar o script, pode acessar a aplicação na região primária com o mywebapp.trafficmanager.net de URL.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a>Limpar a implementação 

Depois de executar o script de exemplo, pode ser utilizado o comando de seguir para remover o grupo de recursos, a aplicação de serviço de aplicações e todos os recursos relacionados.

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a>Explicação do script

Este script utiliza os seguintes comandos para criar um grupo de recursos, uma aplicação Web, um perfil do gestor de tráfego e todos os recursos relacionados. Cada comando na tabela liga à documentação específica do comando.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan) | Cria um plano do Serviço de Aplicações. É como um farm de servidores para a sua aplicação web do Azure. |
| [criar web do AZ webapp](https://docs.microsoft.com/cli/azure/webapp#az-webapp-create) | Cria uma aplicação web do Azure no plano do serviço de aplicações. |
| [Criar perfil do Gestor de tráfego de rede de AZ](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile) | Cria um perfil do Gestor de Tráfego do Azure. |
| [criar o ponto final do Gestor de tráfego de rede AZ](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint) | Adiciona um ponto final a um Perfil do Gestor de Tráfego do Azure. |

## <a name="next-steps"></a>Passos Seguintes

Para obter mais informações sobre a CLI do Azure, veja [Documentação da CLI do Azure](https://docs.microsoft.com/cli/azure).

Exemplos do script da CLI do serviço de aplicações adicionais podem ser encontrados no [documentação de redes do Azure](../cli-samples.md).
