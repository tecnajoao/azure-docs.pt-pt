---
title: Armazenamento de disco do Azure geridos descrição geral do disco para VMs do Windows | Documentos da Microsoft
description: Descrição geral do Azure os discos geridos, que processa as contas de armazenamento por si ao utilizar VMs do Windows Azure
services: virtual-machines-windows,storage
author: roygara
ms.service: virtual-machines-windows
ms.workload: storage
ms.tgt_pltfrm: vm-windows
ms.topic: article
ms.date: 02/11/2019
ms.author: rogarana
ms.subservice: disks
ms.openlocfilehash: 85b2dcb73024ce786b78436b7070ad2e9a96e1d4
ms.sourcegitcommit: d2329d88f5ecabbe3e6da8a820faba9b26cb8a02
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/16/2019
ms.locfileid: "56328475"
---
# <a name="introduction-to-azure-managed-disks"></a>Introdução ao Azure para os discos geridos

Do Azure gerido disco é um disco rígido virtual (VHD). Pode considerá-lo como um disco físico num servidor no local, mas, virtualizados. Managed disks do Azure são armazenados como blobs de páginas, que são um objeto de armazenamento de e/s aleatório no Azure. Chamamos um disco gerido "gerido" porque é uma abstração sobre contas de armazenamento do Azure, contentores de BLOBs e blobs de páginas. Com discos geridos, tudo o que precisa fazer é aprovisionar o disco e Azure trata do resto.

Quando seleciona a utilização do Azure geridos discos com cargas de trabalho, o Azure cria e gere o disco por si. Os tipos de discos disponíveis são Ultra unidades (SSD, Solid State) (pré-visualização), Premium SSD, Standard SSD e unidades de disco rígido Standard (HDD). Para obter mais informações sobre cada tipo de disco individual, veja [selecionar um tipo de disco para IaaS VMs](disks-types.md).

[!INCLUDE [virtual-machines-managed-disks-overview.md](../../../includes/virtual-machines-managed-disks-overview.md)]

> [!div class="nextstepaction"]
> [Selecione um tipo de disco para IaaS VMs](disks-types.md)