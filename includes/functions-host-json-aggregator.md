---
title: incluir ficheiro
description: incluir ficheiro
services: functions
author: ggailey777
manager: jeconnoc
ms.service: functions
ms.topic: include
ms.date: 10/19/2018
ms.author: glenga
ms.custom: include file
ms.openlocfilehash: da0cbab59d9c801419ac4b3704fee3275f337fd9
ms.sourcegitcommit: 1d3353b95e0de04d4aec2d0d6f84ec45deaaf6ae
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/30/2018
ms.locfileid: "50251275"
---
Especifica quantos invocações de função são agregados quando [calcular métricas para o Application Insights](../articles/azure-functions/functions-monitoring.md#configure-the-aggregator). 

```json
{
    "aggregator": {
        "batchSize": 1000,
        "flushTimeout": "00:00:30"
    }
}
```

|Propriedade |Predefinição  | Descrição |
|---------|---------|---------| 
|batchSize|1000|Número máximo de pedidos a agregar.| 
|flushTimeout|00:00:30|Tempo máximo de período a agregar.| 

Invocações de função são agregadas quando o primeiro dos dois limites são atingidos.