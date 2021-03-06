---
title: Exemplo do Script da CLI do Azure – Encriptar uma VM do Linux | Microsoft Docs
description: Exemplo do Script da CLI do Azure – Encriptar uma VM do Linux
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 8f3e032d6723faf149faad039e3c3faff3e6d83a
ms.sourcegitcommit: 3aa0fbfdde618656d66edf7e469e543c2aa29a57
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/05/2019
ms.locfileid: "55731500"
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a>Encriptar uma máquina virtual do Linux no Azure

Este script cria um Azure Key Vault seguro, as chaves de encriptação, o principal do serviço Azure Active Directory e uma máquina virtual (VM) do Linux. A VM é encriptada com a chave de encriptação a partir do Key Vault e das credenciais do principal do serviço.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute o seguinte comando para remover o grupo de recursos, a VM e todos os recursos relacionados.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação do script

Este script utiliza os seguintes comandos para criar um grupo de recursos, o Azure Key Vault, o principal do serviço, uma máquina virtual e todos os recursos relacionados. Cada comando na tabela liga à documentação específica do comando.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault) | Cria um Azure Key Vault para armazenar dados seguros, tais como chaves de encriptação. |
| [az keyvault key create](https://docs.microsoft.com/cli/azure/keyvault/key) | Cria uma chave de encriptação no Key Vault. |
| [az ad sp create-for-rbac](https://docs.microsoft.com/cli/azure/ad/sp) | Cria um principal do serviço Azure Active Directory para autenticar e controlar o acesso às chaves de encriptação de forma segura. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault) | Define as permissões no Key Vault para conceder ao principal do serviço acesso às chaves de encriptação. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm) | Cria a máquina virtual e liga-a à placa de rede, à rede virtual, à sub-rede e ao NSG. Este comando também especifica a imagem da máquina virtual a ser utilizada e as credenciais administrativas.  |
| [az vm encryption enable](https://docs.microsoft.com/cli/azure/vm/encryption) | Ativa a encriptação numa VM com as credenciais do principal do serviço e a chave de encriptação. |
| [az vm encryption show](https://docs.microsoft.com/cli/azure/vm/encryption) | Mostra o estado do processo de encriptação da VM. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos Seguintes

Para obter mais informações sobre a CLI do Azure, veja [Documentação da CLI do Azure](https://docs.microsoft.com/cli/azure).

Pode ver exemplos do script da CLI da máquina virtual adicionais na [Documentação da VM Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
