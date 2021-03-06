---
title: Anexar um disco de dados geridos para uma VM do Windows - Azure | Documentos da Microsoft
description: Como anexar um disco de dados geridos para uma VM do Windows com o portal do Azure.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/08/2018
ms.author: cynthn
ms.subservice: disks
ms.openlocfilehash: 81fbf650597813baaf6618f82ef55a937f1870d9
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/31/2019
ms.locfileid: "55476031"
---
# <a name="attach-a-managed-data-disk-to-a-windows-vm-by-using-the-azure-portal"></a>Anexar um disco de dados geridos para uma VM do Windows com o portal do Azure

Este artigo mostra-lhe como anexar um novo disco de dados geridos para uma máquina virtual de Windows (VM) com o portal do Azure. O tamanho da VM determina quantos discos de dados, pode anexar. Para obter mais informações, consulte [tamanhos de máquinas virtuais](sizes.md).


## <a name="add-a-data-disk"></a>Adicionar um disco de dados

1. Na [portal do Azure](https://portal.azure.com), no menu à esquerda, selecione **máquinas virtuais**.
2. Selecione uma máquina virtual a partir da lista.
3. Sobre o **Máquina Virtual** página, selecione **discos**.
4. Sobre o **discos** página, selecione **adicionar disco de dados**.
5. Na lista pendente para o novo disco, selecione **criar disco**.
6. Na **disco gerido de criar** página, escreva um nome para o disco e ajustar as outras definições conforme necessário. Quando terminar, selecione **Criar**.
7. Na **discos** página, selecione **guardar** para guardar a nova configuração de disco para a VM.
8. Depois do Azure cria o disco e anexa-o para a máquina virtual, o novo disco está listado nas definições de disco da máquina virtual em **discos de dados**.


## <a name="initialize-a-new-data-disk"></a>Inicializar um novo disco de dados

1. Ligue à VM.
1. Selecione o Windows **começar** menu no interior da VM em execução e introduza **Diskmgmt. msc** na caixa de pesquisa. O **gestão de discos** consola é aberta.
2. Gestão de discos reconhece que tem um disco novo, não inicializado e o **Inicializar disco** é apresentada a janela.
3. Certifique-se de que o novo disco está selecionado e, em seguida, selecione **OK** para inicializá-la.
4. O novo disco aparece como **não alocado**. Com o botão direito em qualquer lugar no disco e selecione **novo volume simples**. O **Assistente de novo Volume simples** é aberta a janela.
5. Avance no assistente, manter todos os padrões, e quando terminar, selecione **concluir**.
6. Fechar **gestão de discos**.
7. É apresentada uma janela de pop-up a notificá-lo de que precisa de formatar o disco novo antes de poder utilizá-lo. Selecione **formatar disco**.
8. Na **Formatar novo disco** janela, verifique as definições e, em seguida, selecione **iniciar**.
9. É apresentado um aviso a informar de que os discos de formatação apague todos os dados. Selecione **OK**.
10. Quando a formatação estiver concluída, selecione **OK**.

## <a name="next-steps"></a>Passos Seguintes

- Também pode [anexar um disco de dados com o PowerShell](attach-disk-ps.md).
- Se a sua aplicação precisa de utilizar o *D:* unidade para armazenar dados, pode [alterar a letra de unidade do disco temporário Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
