---
title: Exemplo - uso aprovado sub-rede para interfaces de rede VM
description: Esta definição de política de exemplo requer que as interfaces de rede utilizam uma sub-rede aprovada.
author: DCtheGeek
manager: carmonm
ms.service: azure-policy
ms.topic: sample
ms.date: 01/23/2019
ms.author: dacoulte
ms.openlocfilehash: b4b6b2293952103bdcaccf11e8f7d528b33cbc46
ms.sourcegitcommit: 62d3a040280e83946d1a9548f352da83ef852085
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59270035"
---
# <a name="sample---use-approved-subnet-for-vm-network-interfaces"></a>Exemplo - uso aprovado sub-rede para interfaces de rede VM

Esta política requer que as interfaces de rede utilizem uma sub-rede aprovada. Especifica o ID da sub-rede aprovada.

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a>Modelo de exemplo

[!code-json[main](../../../../policy-templates/samples/Network/vm-creation-in-approved-subnet/azurepolicy.json "Use approved subnet for VM network interfaces")]

Pode implementar este modelo através do [portal do Azure](#deploy-with-the-portal), do [PowerShell](#deploy-with-powershell) ou da [CLI do Azure](#deploy-with-azure-cli).

## <a name="deploy-with-the-portal"></a>Implementar com o portal

[![Deploy o exemplo de política para o Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fvm-creation-in-approved-subnet%2Fazurepolicy.json)

## <a name="deploy-with-powershell"></a>Implementar com o PowerShell

[!INCLUDE [sample-powershell-install](../../../../includes/sample-powershell-install-no-ssh-az.md)]

```azurepowershell-interactive
$definition = New-AzPolicyDefinition -Name "vm-creation-in-approved-subnet" -DisplayName "Use approved subnet for VM network interfaces" -description "This policy enforces VM network interfaces to use subnet" -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/vm-creation-in-approved-subnet/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/vm-creation-in-approved-subnet/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzPolicyAssignment -Name <assignmentname> -Scope <scope>  -subnetId <Subnet Id> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a>Limpar a implementação do PowerShell

Execute o seguinte comando para remover o grupo de recursos, a VM e todos os recursos relacionados.

```azurepowershell-interactive
Remove-AzResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a>Implementar com a CLI do Azure

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'vm-creation-in-approved-subnet' --display-name 'Use approved subnet for VM network interfaces' --description 'This policy enforces VM network interfaces to use subnet' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/vm-creation-in-approved-subnet/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/vm-creation-in-approved-subnet/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "vm-creation-in-approved-subnet"
```

### <a name="clean-up-azure-cli-deployment"></a>Limpar a implementação da CLI do Azure

Execute o seguinte comando para remover o grupo de recursos, a VM e todos os recursos relacionados.

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a>Passos Seguintes

- Veja mais exemplos na página [Exemplos do Azure Policy](index.md)