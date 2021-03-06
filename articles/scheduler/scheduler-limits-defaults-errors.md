---
title: Limites, quotas e limites no agendador do Azure
description: Saiba mais sobre os limites, quotas, valores padrão e limiares de limitação do Azure Scheduler
services: scheduler
ms.service: scheduler
author: derek1ee
ms.author: deli
ms.reviewer: klam
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.topic: article
ms.date: 08/18/2016
ms.openlocfilehash: 0c1e704a3bdec239c87d879ae1ef95e6e76d27fc
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/24/2018
ms.locfileid: "46966919"
---
# <a name="limits-quotas-and-throttle-thresholds-in-azure-scheduler"></a>Limites, quotas e limites de limitação no agendador do Azure

> [!IMPORTANT]
> [O Azure Logic Apps](../logic-apps/logic-apps-overview.md) está a substituir o Azure Scheduler, que está a ser descontinuado. Para agendar tarefas, [Experimente o Azure Logic Apps antes](../scheduler/migrate-from-scheduler-to-logic-apps.md). 

## <a name="limits-quotas-and-thresholds"></a>Limites, quotas e limites

[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="x-ms-request-id-header"></a>cabeçalho x-ms-request-id

Cada pedido efetuado para o serviço de agendador retorna um cabeçalho de resposta denominado **x-ms-request-id**. Este cabeçalho contém um valor indefinido, que identifica exclusivamente o pedido. Então, se um pedido de forma consistente de falha, e confirmar a solicitação está formatada corretamente, pode reportar o erro para a Microsoft, fornecendo a **x-ms-request-id** valor do cabeçalho de resposta e estes detalhes, incluindo: 

* O **x-ms-request-id** valor
* O tempo aproximado quando o pedido foi efectuado 
* Os identificadores para a subscrição do Azure, a coleção de tarefas e a tarefa 
* O tipo de operação tentado o pedido

## <a name="see-also"></a>Consulte também

* [O que é o agendador do Azure?](scheduler-intro.md)
* [Conceitos, terminologia e hierarquia de entidades do Azure Scheduler](scheduler-concepts-terms.md)
