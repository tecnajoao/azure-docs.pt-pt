---
author: mgoedtel
ms.service: log-analytics
ms.topic: include
ms.date: 11/09/2018
ms.author: magoedte
ms.openlocfilehash: 6890c71ac7c265d46cc77751786fea4d0b228588
ms.sourcegitcommit: f24fdd1ab23927c73595c960d8a26a74e1d12f5d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58505755"
---
### <a name="troubleshoot-azure-diagnostics"></a>Resolver Problemas do Diagnóstico do Azure

Se receber a seguinte mensagem de erro, o fornecedor de recursos Microsoft.insights não está registado:

`Failed to update diagnostics for 'resource'. {"code":"Forbidden","message":"Please register the subscription 'subscription id' with Microsoft.Insights."}`

Para registar o fornecedor de recursos, execute os seguintes passos no portal do Azure:

1.  No painel de navegação à esquerda, clique em *Subscrições*
2.  Selecione a subscrição identificada na mensagem de erro
3.  Clique em *Fornecedores de Recursos*
4.  Encontre o fornecedor *Microsoft.insights*
5.  Clique na ligação *Registar*

![Registe o fornecedor de recursos do microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

Assim que o fornecedor de recursos do *Microsoft.insights* estiver registado, repita o diagnóstico de configuração.


No PowerShell, se receber a seguinte mensagem de erro, terá de atualizar a versão do PowerShell:

`Set-AzDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

Atualizar a versão do Azure PowerShell, siga as instruções no [instalar o Azure PowerShell](/powershell/azure/install-az-ps) artigo.
