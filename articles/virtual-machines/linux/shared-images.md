---
title: Criar imagens VM partilhadas com a CLI do Azure | Documentos da Microsoft
description: Neste artigo, saiba como utilizar a CLI do Azure para criar uma imagem partilhada de uma VM no Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: axayjo
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/19/2018
ms.author: akjosh; cynthn
ms.custom: ''
ms.openlocfilehash: 08c7e84a27a4c8e9527083360dbd08296bd86775
ms.sourcegitcommit: 63b996e9dc7cade181e83e13046a5006b275638d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/10/2019
ms.locfileid: "54190094"
---
# <a name="preview-create-a-shared-image-gallery-with-the-azure-cli"></a>Pré-visualização: Criar uma galeria de imagem partilhada com a CLI do Azure

R [Galeria de imagens de partilhado](shared-image-galleries.md) simplifica a imagem personalizada de partilha na sua organização. As imagens personalizadas são como imagens do marketplace, mas são criadas por si. As imagens personalizadas podem ser utilizadas para configurações do programa de arranque do sistema, como o pré-carregamento de aplicações, configurações de aplicação e outras configurações do SO. 

A Galeria de imagens partilhado permite que Compartilhe suas imagens VM personalizadas com outras pessoas na sua organização, numa ou em regiões, dentro de um inquilino do AAD. Escolha quais imagens que pretende partilhar, quais são as regiões que pretende tornar disponível no mesmos e a quem pretende partilhá-los com. Pode criar várias galerias, para que pode agrupar logicamente Imagens partilhadas. 

A galeria é um recurso de nível superior que fornece controlo de acesso completa baseada em funções (RBAC). Imagens podem ser atualizadas, e pode optar por replicar cada versão de imagem para um conjunto diferente de regiões do Azure. A Galeria só funciona com imagens gerenciadas pelo.

O recurso da Galeria de imagens de partilhado tem vários tipos de recursos. Podemos será a utilizar ou criar neste artigo:

| Recurso | Descrição|
|----------|------------|
| **Imagem gerida** | Esta é uma imagem básica que pode ser usada sozinha ou utilizada para criar uma **versão da imagem** na Galeria de imagens. Imagens geridas são criadas a partir de VMs generalizadas. Uma imagem gerida é um tipo especial de VHD que pode ser utilizado para fazer várias VMs e pode agora ser utilizado para criar versões de imagem partilhada. |
| **Galeria de imagens** | Como o Azure Marketplace, um **Galeria de imagens** é um repositório de gerenciamento e compartilhamento de imagens, mas controlar quem tem acesso. |
| **Definição de imagem** | As imagens são definidas dentro de uma galeria e transportar informações sobre a imagem e os requisitos para utilizá-lo internamente. Isto inclui se a imagem é Windows ou Linux, notas de versão e os requisitos de memória mínimos e máximos. É uma definição de um tipo de imagem. |
| **Versão da imagem** | Uma **versão da imagem** é o que utiliza para criar uma VM ao utilizar uma galeria. Pode ter várias versões de uma imagem, conforme necessário para o seu ambiente. Como uma imagem gerida, quando utiliza um **versão da imagem** para criar uma VM, a versão da imagem é usada para criar novos discos para a VM. Versões de imagem podem ser utilizadas várias vezes. |



[!INCLUDE [virtual-machines-common-shared-images-cli](../../../includes/virtual-machines-common-shared-images-cli.md)]

## <a name="create-a-vm"></a>Criar uma VM

Criar uma VM a partir da versão de imagem com [az vm criar](/cli/azure/vm#az-vm-create).

```azurecli-interactive 
az vm create\
   -g myGalleryRG \
   -n myVM \
   --image "/subscriptions/<subscription-ID>/resourceGroups/myGalleryRG/providers/Microsoft.Compute/galleries/myGallery/images/myImageDefinition/versions/1.0.0" \
   --generate-ssh-keys
```

[!INCLUDE [virtual-machines-common-gallery-list-cli](../../../includes/virtual-machines-common-gallery-list-cli.md)]



## <a name="next-steps"></a>Passos Seguintes
Também pode criar recursos de Galeria de imagens de partilhado através de modelos. Vários modelos de início rápido do Azure estão disponíveis: 

- [Criar uma galeria de imagem partilhada](https://azure.microsoft.com/resources/templates/101-sig-create/)
- [Criar uma definição de imagem numa galeria de imagem partilhada](https://azure.microsoft.com/resources/templates/101-sig-image-definition-create/)
- [Criar uma versão de imagem numa galeria de imagem partilhada](https://azure.microsoft.com/resources/templates/101-sig-image-version-create/)
- [Criar uma VM a partir da versão de imagem](https://azure.microsoft.com/resources/templates/101-vm-from-sig/)

Para obter mais informações sobre as galerias de imagem de partilhado, consulte a [descrição geral](shared-image-galleries.md). Caso se depare com problemas, consulte [resolução de problemas partilhado galerias de imagem](troubleshooting-shared-images.md).
