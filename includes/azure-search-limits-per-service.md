---
title: incluir ficheiro
description: incluir ficheiro
services: search
author: HeidiSteen
ms.service: search
ms.topic: include
ms.date: 04/04/2018
ms.author: heidist
ms.custom: include file
ms.openlocfilehash: 30c6fc189ebcd497a214828f65213a55cefdf03f
ms.sourcegitcommit: f8c592ebaad4a5fc45710dadc0e5c4480d122d6f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58632770"
---
Armazenamento é limitado pelo espaço em disco ou por um limite restritivo no *número máximo* de índices, documento ou outros recursos de alto nível, o que ocorrer primeiro. A tabela seguinte documenta os limites de armazenamento. Para obter limites máximos em índices, documentos e outros objetos, consulte [limites por recurso](../articles/search/search-limits-quotas-capacity.md#index-limits).

| Recurso | Gratuito | Básico<sup>1</sup> | S1 | S2 | S3 | S3&nbsp;HD<sup>2</sup> | L1 | ERROS DE L2 |
| -------- | --- | --- | --- | --- | --- | --- | --- | --- |
| (SLA) de contrato de nível de serviço<sup>3</sup>  |Não |Sim |Sim |Sim |Sim |Sim |Sim |Sim |
| Armazenamento por partição |50 MB |2GB |25 GB |100 GB |200 GB |200 GB |1 TB |2 TB |
| Partições por serviço |N/A |1 |12 |12 |12 |3 |12 |12 |
| Tamanho da partição |N/A |2 GB |25 GB |100 GB |200 GB |200 GB |1 TB |2 TB |
| Réplicas |N/A |3 |12 |12 |12 |12 |12 |12 |

<sup>1</sup> basic possui uma partição fixa. Nesta camada de unidades de pesquisa adicionais são utilizadas para alocar mais réplicas para cargas de trabalho de consulta maior.

<sup>2</sup> S3 HD tem um limite rígido de três partições, que é menor do que o limite de partição para S3. O limite de partição inferior é imposto porque a contagem de índice do S3 HD é significativamente mais elevada. Dado que existem limites de serviço para recursos informáticos (processamento e armazenamento) e conteúdo (índices e documentos), o limite de conteúdo é atingido primeiro.

<sup>3</sup> contratos de nível de serviço estão disponíveis para os serviços faturáveis em recursos dedicados. Recursos de serviços e pré-visualização gratuitos não tem nenhum SLA. Para os serviços faturáveis, SLAs em vigor quando Aprovisiona redundância suficiente para o seu serviço. Duas ou mais réplicas são necessárias para SLAs de consulta (ler). Três ou mais réplicas são necessárias para consulta e indexação de SLAs (leitura / escrita). O número de partições não é uma consideração de SLA. 