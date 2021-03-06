---
title: Utilização de relatórios infraestrutura para fornecedores de serviços Cloud para o Azure Stack | Documentos da Microsoft
description: O Azure Stack inclui a infra-estrutura necessária para controlar a utilização dos inquilinos servidos por um fornecedor de serviços Cloud (CSP) conforme ele ocorre e encaminha-o para o Azure.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2019
ms.author: sethm
ms.reviewer: alfredop
ms.lastreviewed: 01/05/2019
ms.openlocfilehash: 1b8b83491211ae26493a6bb41c7f0f219f47f620
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/30/2019
ms.locfileid: "55241309"
---
# <a name="usage-reporting-infrastructure-for-cloud-service-providers"></a>Utilização de infraestrutura de criação de relatórios para fornecedores de serviços Cloud

O Azure Stack inclui a infra-estrutura necessária para controlar a utilização como ele ocorre e encaminha-o para o Azure. No Azure, Azure Commerce processa os dados de utilização e custos de utilização para as subscrições do Azure adequadas. Isso ocorre da mesma forma que o controlo de utilização é monitorizada na cloud do Azure global.

Deve observar que alguns conceitos são consistentes entre o global Azure e do Azure Stack. O Azure Stack tem subscrições locais, que cumpram uma função semelhante a uma subscrição do Azure. Subscrições locais localmente só são válidas. Subscrições locais são mapeadas para as subscrições do Azure quando a utilização é reencaminhada para o Azure.

O Azure Stack tem os medidores de utilização local. Uso local é mapeado para os medidores utilizados no comércio do Azure. No entanto, os IDs de medidor são diferentes. Há mais de medidores disponíveis localmente que a Microsoft utiliza para faturação.

Existem algumas diferenças entre como serviços são calculados os preços no Azure Stack e o Azure. Por exemplo, no Azure Stack, o custo das VMs é apenas base/horas de vcore, com a mesma tarifa para todas as séries VM, ao contrário do Azure. O motivo é que, no global Azure, os preços diferentes refletem um hardware diferente. No Azure Stack, o cliente fornece o hardware, portanto, não há nenhuma razão para cobrança de taxas diferentes para diferentes classes VM.

Pode obter informações sobre os medidores do Azure Stack usados em comércio e seus preços no Centro de parceiros, da mesma forma, tal como faria para serviços do Azure:

1. No Centro de parceiros, vá para o **menu do Dashboard** > **preços e ofertas**.
2. Sob **serviços baseados em utilização**, selecione **atual**.
3. Abra o **do Azure na lista de preços do Global CSP** folha de cálculo.
4. Filtre **região do Azure Stack de =**.

## <a name="usage-and-billing-error-codes"></a>Utilização e faturação códigos de erro

As mensagens de erro seguinte podem ser encontradas durante a adição de inquilinos para um registo.

| Erro                           | Detalhes                                                                                                                                                                                                                                                                                                                           | Comentários                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **RegistrationNotFound**            | O registo fornecido não foi encontrado. Certifique-se de que as seguintes informações foi fornecidas corretamente:<br>1. Identificador de subscrição (valor fornecido: _identificador de subscrição_),<br>2. Grupo de recursos (valor fornecido: _grupo de recursos_),<br>3. Nome do registo (valor fornecido: _do registo-nome_).                             | Este erro ocorre normalmente quando as informações que aponta para o registo inicial não estão corretas. Se precisar de verificar o grupo de recursos e o nome do seu registo, pode encontrá-lo no portal do Azure, liste todos os recursos. Se encontrar mais do que um recurso de registro, consulte a **CloudDeploymentID** de propriedades e selecione o registo cujo **CloudDeploymentID** corresponde da sua cloud. Para localizar os **CloudDeploymentID**, pode usar este PowerShell na pilha do Azure:<br>`$azureStackStampInfo = Invoke-Command -Session $session -ScriptBlock { Get-AzureStackStampInformation }` |
| **BadCustomerSubscriptionId**       | Fornecido _identificador de subscrição de cliente_ e o _nome do registo_ identificador de subscrição não pertencem ao mesmo fornecedor de serviços de Cloud de Microsoft. Verifique se o identificador de subscrição de cliente está correto. Se o problema persistir, contacte o suporte. | Este erro ocorre quando a subscrição do cliente é uma subscrição do CSP, mas ele agrega a um parceiro CSP diferente ao qual a subscrição utilizada no registo inicial agrega. Esta verificação é executada para impedir que uma situação que poderia resultar numa faturação de parceiro CSP que não é responsável pelo Azure Stack utilizado.                                                                                                                                                                                                                                                                          |
| **InvalidCustomerSubscriptionId**   | O '_identificador de subscrição de cliente_' não é válido. Certifique-se de que uma subscrição do Azure válida é fornecida.                                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| **CustomerSubscriptionNotFound**    | _Identificador de subscrição de cliente_ não foi encontrado em nome de _registration. Certificar-se de que está a ser utilizada uma subscrição do Azure válida e se o identificador de subscrição foi adicionado ao registo usando a operação PUT.                                                   | Este erro ocorre quando tentar vidade de incompatibilidade que um inquilino tenha sido adicionado a uma subscrição e a subscrição do cliente não está a ser associado com o registo. O cliente não foi adicionado para o registo ou o ID de subscrição tenha sido escrito incorretamente.                                                                                                                                                                                                                                                                                                                                |
| **UnauthorizedCspRegistration**     | Fornecido _do registo-nome_ não está aprovada para utilizar vários inquilinos. Envie um e-mail para azstCSP@microsoft.com e incluir o seu nome de registo, grupo de recursos e o identificador de subscrição utilizado no registo.                                                                                    | Um registo tem de ser aprovado para vários inquilinos pela Microsoft antes de começar a adicionar os inquilinos ao mesmo.                                                                                                                                                                                                                                                                                                                                                                                             |
| **CustomerSubscriptionsNotAllowed** | Operações de subscrição de cliente não são suportadas para os clientes desligados. Para utilizar esta funcionalidade, volte a registar com o licenciamento de pagar enquanto utiliza.                                                                                                                                                                    | O registo para o qual está a tentar adicionar inquilinos é um registo de capacidade; ou seja, quando o registo foi criado, o parâmetro `BillingModel Capacity` foi utilizado. Pagar apenas pelo que utiliza registos estão autorizados a adicionar os inquilinos. É necessário registrar novamente utilizando o parâmetro `BillingModel PayAsYouUse`.                                                                                                                                                                                                                                                                                          |
| **InvalidCSPSubscription**          | Fornecido _identificador de subscrição de cliente_ não é uma subscrição do CSP válida. Certifique-se de que uma subscrição do Azure válida é fornecida.                                                                                                                                                        | Este é provavelmente porque a subscrição do cliente que está a ser escrito incorretamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| **MetadataResolverBadGatewayError** | Um dos servidores a montante devolveu um erro inesperado. Tente novamente mais tarde. Se o problema persistir, contacte o suporte.                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

## <a name="terms-used-for-billing-and-usage"></a>Termos utilizados para faturação e utilização

Os seguintes termos e conceitos são utilizados para utilização e faturação no Azure Stack:

| Termo | Definição |
| --- | --- |
| Qualidade de parceiro CSP direta | Um parceiro direta do fornecedor de soluções Cloud (CSP) recebe uma nota fiscal diretamente da Microsoft para utilização do Azure e o Azure Stack e os clientes de faturas diretamente. |
| CSP indireto | Os revendedores indiretos de colaborar com um fornecedor de indireto (também conhecido como um distribuidor). Os revendedores recruta clientes finais; o fornecedor indireto contém a relação de faturação com a Microsoft, gerencia a cobrança aos clientes e oferece serviços adicionais, como o suporte do produto. |
| Cliente final | Os clientes do fim são as empresas e agências do governo que possuem as aplicações e outras cargas de trabalho que são executadas no Azure Stack. |

## <a name="next-steps"></a>Passos Seguintes

- Para saber mais sobre o programa CSP, veja [programa Cloud Solution Provider](https://partner.microsoft.com/solutions/microsoft-cloud-solutions).
- Para saber mais sobre como recuperar informações de utilização de recursos do Azure Stack, veja [utilização e faturação no Azure Stack](azure-stack-billing-and-chargeback.md).
