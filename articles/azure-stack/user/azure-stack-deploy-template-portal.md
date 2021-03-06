---
title: Implementar modelos com o portal no Azure Stack | Documentos da Microsoft
description: Saiba como utilizar o portal do Azure Stack para implementar modelos.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: eafa60f2-16c9-4ef1-b724-47709e9ea29e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2019
ms.author: sethm
ms.reviewer: unknown
ms.lastreviewed: 01/05/2019
ms.openlocfilehash: b9adac3f2f56093c3559570aab4e905eb047ccd2
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/30/2019
ms.locfileid: "55247090"
---
# <a name="deploy-templates-using-the-azure-stack-portal"></a>Implementar modelos com o portal do Azure Stack

*Aplica-se a: Integrados do Azure Stack, sistemas e o Kit de desenvolvimento do Azure Stack*

Pode utilizar o portal para implementar os modelos Azure Resource Manager para o Azure Stack.

## <a name="to-deploy-a-template"></a>Para implementar um modelo

1. Inicie sessão no portal, selecione **+ criar um recurso**e, em seguida, selecione **personalizado**.
2. Selecione **Implementação de modelo**.
3. Selecione **Editar modelo**e, em seguida, cole o código de modelo JSON para a janela de código. Selecione **Guardar**.
4. Selecione **Editar parâmetros**, forneça valores para os parâmetros que são apresentados e, em seguida, selecionam **OK**.
5. Selecione **subscrição**. Escolha a subscrição que pretende utilizar e, em seguida, selecione **OK**.
6. Selecione **grupo de recursos**. Escolha um grupo de recursos existente ou crie um novo e, em seguida, selecione **OK**.
7. Selecione **Criar**. Um novo mosaico no dashboard controla o progresso da implementação do modelo.

## <a name="next-steps"></a>Passos Seguintes

Para saber mais sobre a implementação de modelos, consulte o artigo seguinte:

- [Implementar modelos com o PowerShell](azure-stack-deploy-template-powershell.md)
