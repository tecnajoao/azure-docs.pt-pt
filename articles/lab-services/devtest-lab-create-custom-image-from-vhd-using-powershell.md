---
title: Criar uma imagem personalizada do Azure DevTest Labs de um ficheiro VHD com o PowerShell | Documentos da Microsoft
description: Automatizar a criação de uma imagem personalizada no Azure DevTest Labs, de um ficheiro VHD com o PowerShell
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/05/2018
ms.author: spelluru
ms.openlocfilehash: dc6e218fe048e1781f53c53935308eb193fcd094
ms.sourcegitcommit: 0dd053b447e171bc99f3bad89a75ca12cd748e9c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/26/2019
ms.locfileid: "58487163"
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a>Criar uma imagem personalizada a partir de um ficheiro VHD com o PowerShell

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

## <a name="step-by-step-instructions"></a>Instruções passo a passo

Os seguintes passos guiá-lo através da criação de uma imagem personalizada de um ficheiro VHD com o PowerShell:

1. Na linha de comandos do PowerShell, inicie sessão na sua conta do Azure com a chamada seguinte para o **Connect-AzAccount** cmdlet.  
    
    ```powershell
    Connect-AzAccount
    ```

1.  Selecione a subscrição do Azure pretendida ao chamar o **AzSubscription selecione** cmdlet. Substitua o marcador de posição seguinte para o **$subscriptionId** variável com um ID de subscrição do Azure válida. 

    ```powershell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzSubscription -SubscriptionId $subscriptionId
    ```

1.  Obtenha o objeto de laboratório ao chamar o **Get-AzResource** cmdlet. Substitua os marcadores de posição seguintes para o **$labRg** e **$labName** variáveis com os valores adequados para o seu ambiente. 

    ```powershell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  Obtenha o laboratório de armazenamento conta e laboratório armazenamento conta valores de chave do objeto de laboratório. 

    ```powershell
    $labStorageAccount = Get-AzResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  Substitua o marcador de posição seguinte para o **$vhdUri** variável com o URI para o ficheiro VHD carregado. Pode obter o URI do ficheiro VHD do painel de blob da conta de armazenamento no portal do Azure.

    ```powershell
    $vhdUri = '<Specify the VHD URI here>'
    ```

1.  Crie a imagem personalizada com o **New-AzResourceGroupDeployment** cmdlet. Substitua os marcadores de posição seguintes para o **$customImageName** e **$customImageDescription** variáveis para nomes significativos para o seu ambiente.

    ```powershell
    $customImageName = '<Specify the custom image name>'
    $customImageDescription = '<Specify the custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-to-create-a-custom-image-from-a-vhd-file"></a>Script do PowerShell para criar uma imagem personalizada a partir de um ficheiro VHD

O seguinte script do PowerShell pode ser utilizado para criar uma imagem personalizada de um ficheiro VHD. Substitua os marcadores de posição (começando e terminando com colchetes angulares) com os valores adequados para as suas necessidades. 

```powershell
# Log in to your Azure account.  
Connect-AzAccount

# Select the desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzSubscription -SubscriptionId $subscriptionId

# Get the lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get the lab storage account and lab storage account key values.
$labStorageAccount = Get-AzResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set the URI of the VHD file.  
$vhdUri = '<Specify the VHD URI here>'

# Set the custom image name and description values.
$customImageName = '<Specify the custom image name>'
$customImageDescription = '<Specify the custom image description>'

# Set up the parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create the custom image. 
New-AzResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a>Postagens de blogs relacionados

- [Imagens personalizadas ou fórmulas?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copiar imagens personalizadas entre o Azure DevTest Labs](https://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

## <a name="next-steps"></a>Passos Seguintes

- [Adicionar uma VM para o laboratório](devtest-lab-add-vm.md)
