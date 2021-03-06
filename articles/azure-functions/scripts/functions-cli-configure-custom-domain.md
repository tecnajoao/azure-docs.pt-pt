---
title: Exemplo do Script da CLI do Azure – Mapear um domínio personalizado para uma aplicação de funções | Microsoft Docs
description: Exemplo do Script da CLI do Azure – Mapear um domínio personalizado para uma aplicação de funções no Azure.
services: functions
documentationcenter: ''
author: ggailey777
manager: jeconnoc
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: azure-functions
ms.devlang: azurecli
ms.topic: sample
ms.date: 07/04/2018
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 5299675656ea23b85f78b3dbfdc02814ab332a8b
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/24/2018
ms.locfileid: "46979054"
---
# <a name="map-a-custom-domain-to-a-function-app"></a>Mapear um domínio personalizado para uma aplicação de funções

Este script de exemplo cria uma aplicação de funções num plano do Serviço de Aplicações e, em seguida, mapeia-a para o domínio personalizado que indicar. Quando a sua aplicação de funções estiver alojada num [plano do Serviço de Aplicações](../functions-scale.md#app-service-plan), pode mapear um domínio personalizado com um CNAME ou um registo A. Para aplicações de funções num [Plano de consumo](../functions-scale.md#consumption-plan), é suportada apenas a opção CNAME. Este exemplo cria um plano do Serviço de Aplicações e requer um registo A para mapear o domínio. 

Para executar este script de exemplo, tem de já ter configurado um registo A no seu domínio personalizado que aponte para o nome de domínio predefinido da sua aplicação Web. Para obter mais informações, consulte as [Instruções do mapa do domínio personalizado para o Serviço de Aplicações do Azure](https://aka.ms/appservicecustomdns). 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se optar por instalar e utilizar a CLI localmente, tem de utilizar a versão 2.0 ou uma versão posterior da CLI do Azure. Para localizar a versão, execute `az --version`. Se precisar de instalar ou atualizar, veja [Instalar a CLI do Azure]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação do script

Este script utiliza os seguintes comandos: cada comando na tabela está ligado a documentação específica do comando.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az-group-create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#az-storage-account-create) | Cria uma conta de armazenamento necessária para a aplicação de funções. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#az-appservice-plan-create) | Cria um plano do Serviço de Aplicações necessário para mapear um domínio personalizado. |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#az-functionapp-create) | Cria uma aplicação de funções no plano do Serviço de Aplicações. |
| [az functionapp config hostname add](https://docs.microsoft.com/cli/azure/functionapp/config/hostname#az-functionapp-config-hostname-add) | Mapeia um domínio personalizado para uma aplicação de funções. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre a CLI do Azure, veja [Documentação da CLI do Azure](https://docs.microsoft.com/cli/azure).

Pode ver exemplos do script da CLI das Funções adicionais na [Documentação das Funções do Azure](../functions-cli-samples.md).
