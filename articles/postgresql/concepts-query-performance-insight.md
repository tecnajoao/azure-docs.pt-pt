---
title: Informações de desempenho de consulta na base de dados do Azure para PostgreSQL
description: Este artigo descreve a funcionalidade de informações de desempenho de consulta na base de dados do Azure para PostgreSQL.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 03/28/2019
ms.openlocfilehash: 56abdd819e78312e64209078c3966826385df7bc
ms.sourcegitcommit: f8c592ebaad4a5fc45710dadc0e5c4480d122d6f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58620738"
---
# <a name="query-performance-insight"></a>Query Performance Insight 

**Aplica-se a:** Base de dados do Azure para PostgreSQL 9.6 e 10

O Query Performance Insight ajuda-o a identificar rapidamente quais são suas consultas de maior duração, como são alterados ao longo do tempo e esperas de que estão a afetá-los.

## <a name="permissions"></a>Permissões
As permissões **Proprietário**ou **Contribuidor** necessárias para ver o texto das consultas no Query Performance Insight. O **Leitor** pode ver gráficos e tabelas, mas não o texto da consulta.

## <a name="prerequisites"></a>Pré-requisitos
Para o Query Performance Insight para a função, dados tem de existir na [Query Store](concepts-query-store.md).

## <a name="viewing-performance-insights"></a>Ver informações de desempenho
A vista [Query Performance Insight](concepts-query-performance-insight.md) no portal do Azure vai apresentar visualizações sobre informações importantes do Arquivo de Consultas. 

Na página do portal da sua base de dados do Azure para o servidor PostgreSQL, selecione **informações de desempenho de consultas** sob a **desempenho inteligente** secção da barra de menus.

![O Query Performance Insight consultas de execução longa](./media/concepts-query-performance-insight/query-performance-insight-landing-page.png)

O **consultas de longa execução** separador mostra as consultas de cinco por duração média por execução, agregados em intervalos de 15 minutos. Pode ver mais consultas ao selecionar no menu pendente **Número de Consultas**. Ao fazer isso, as cores do gráfico podem ser alteradas para um ID de Consulta específico.

Pode clicar e arrastar no gráfico para restringir a uma janela de tempo específica. Em alternativa, utilize o zoom os ícones para ver um menor ou maior do período de tempo, respetivamente.

A tabela abaixo o gráfico fornece mais detalhes sobre as consultas de longa execução nessa janela de tempo.

Selecione o separador **Estatísticas de Espera** para ver as visualizações correspondentes sobre esperas no servidor.

![Estatísticas de espera o Query Performance Insight](./media/concepts-query-performance-insight/query-performance-insight-wait-statistics.png)

## <a name="next-steps"></a>Passos Seguintes
- Saber mais sobre [monitorização e otimização](concepts-monitoring.md) na Base de Dados do Azure para PostgreSQL.


