---
title: O que é o Azure Data Explorer?
description: O Azure Data Explorer é um serviço de exploração de dados rápido e altamente dimensionável para dados telemétricos e de registo.
author: orspod
ms.author: orspodek
ms.reviewer: mblythe
ms.service: data-explorer
ms.topic: overview
ms.date: 09/24/2018
ms.openlocfilehash: 02b239922f481240341225ea68d8d0ee7492c48b
ms.sourcegitcommit: 8313d5bf28fb32e8531cdd4a3054065fa7315bfd
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/05/2019
ms.locfileid: "59044179"
---
# <a name="what-is-azure-data-explorer"></a>O que é o Azure Data Explorer?

O Azure Data Explorer é um serviço de exploração de dados rápido e altamente dimensionável para dados telemétricos e de registo. Ajuda-o a processar os vários fluxos de dados emitidos por software moderno para que possa recolher, armazenar e analisar dados. O Azure Data Explorer é ideal para analisar grandes volumes de dados diversificados provenientes de qualquer origem de dados, como sites, aplicações, dispositivos IoT e muito mais. Estes dados são utilizados para diagnóstico, monitorização, relatórios, aprendizagem automática e capacidades de análise adicionais. O Explorador de dados do Azure simplifica a ingestão de dados e permite-lhe executar consultas ad hoc complexas nos dados em segundos.

## <a name="what-makes-azure-data-explorer-unique"></a>O que torna o Azure Data Explorer único?

- Dimensiona rapidamente para terabytes de dados, em minutos, permitindo rápidas iterações de exploração de dados para descobrir informações relevantes.

- Oferece uma linguagem de consulta inovadora, otimizada para análise de dados de elevado desempenho.

- Suporta a análise de grandes volumes de dados heterogéneos (estruturados e não estruturados).

- Fornece a capacidade de compilar e implementar exatamente aquilo de que precisa, através da conjunção com outros serviços para fornecer uma solução de análise de dados abrangente, poderosa e interativa.

## <a name="data-warehousing-workflow"></a>Fluxo de trabalho de armazenamento de dados

O Azure Data Explorer integra-se noutros serviços principais para fornecer uma solução ponto a ponto que inclui recolha de dados, ingestão, armazenamento, indexação, consulta e visualização. Desempenha um papel fundamental no fluxo de armazenamento de dados, ao executar o passo **EXPLORAR** do fluxo em terabytes de diferentes dados não processados.

![Diagrama de armazém de dados](media/data-explorer-overview/data-warehouse.png)

O Azure Data Explorer suporta vários métodos de ingestão, incluindo os conectores para serviços comuns, como o Hub de Eventos, ingestão programática através de SDKs, como o .NET e Python, e acesso direto ao motor para fins de exploração. O Azure Data Explorer integra-se nos serviços de análise e modelação para análises adicionais e visualização de dados.

## <a name="azure-data-explorer-flow"></a>Fluxo do Azure Data Explorer

O diagrama seguinte mostra os diferentes aspetos do trabalho no Azure Data Explorer.

![Fluxo do Azure Data Explorer](media/data-explorer-overview/workflow.png)

Em geral, o trabalho no Azure Data Explorer segue este padrão:

1. **Crie base de dados:** Criar uma *cluster* e, em seguida, criar um ou mais *bases de dados* desse cluster. [Início rápido: Criar um cluster do Explorador de dados do Azure e a base de dados](create-cluster-database-portal.md)

1. **Ingestão de dados:** Carregar dados para tabelas de base de dados para que pode executar consultas em relação a ele. [Início rápido: Ingerir dados de Hub de eventos no Explorador de dados do Azure](ingest-data-event-hub.md)

1. **Consultar a base de dados:** Utilize o nosso aplicativo web para executar, reveja e partilhar consultas e os resultados. Está disponível no portal do Azure e como uma aplicação autónoma. Além disso, pode enviar consultas por meio de programação (com um SDK) ou para um ponto de final de API REST. [Início rápido: Consultar dados no Explorador de dados do Azure](web-query-data.md)

## <a name="query-experience"></a>Experiência de consulta

Uma consulta no Azure Data Explorer é um pedido só de leitura para processar os dados e devolver os resultados deste processo, sem modificar os dados ou metadados. Continue a refinar as consultas até concluir a análise. O Explorador de dados do Azure facilita este processo devido à sua experiência de consulta muito rápida ad hoc.

O Azure Data Explorer processa grandes quantidades de dados estruturados, semiestruturados (tipos aninhados semelhantes a JSON) e não estruturados (texto livre) igualmente bem. Permite procurar termos específicos de texto, localizar eventos em particular e realizar cálculos de estilo métrico em dados estruturados. O Azure Data Explorer liga os mundos de registos de texto não estruturado e números e dimensões estruturados, ao extrair valores no runtime de campos de texto de forma livre. A exploração de dados é simplificada através de operações rápidas de indexação de texto, arquivo de colunas e séries de tempo.

Capacidades do Explorador de dados do Azure são estendidas por outros serviços criados na sua linguagem de consulta poderosa, incluindo [registos do Azure Monitor](/azure/log-analytics/), [Application Insights](/azure/application-insights/), [Time Series Insights ](/azure/time-series-insights/), e [proteção avançada contra ameaças do Windows Defender](/windows/security/threat-protection/windows-defender-atp/windows-defender-advanced-threat-protection/).

## <a name="feedback"></a>Comentários

Gostaríamos de receber os seus comentários relativos ao Azure Data Explorer e à respetiva linguagem de consulta em:

- Faça perguntas
  - [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-data-explorer)
  - [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Data-Explorer/bd-p/Kusto)
  - [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureKusto)
- [Faça sugestões de produtos em voz do utilizador](https://aka.ms/AzureDataExplorer.UserVoice)

## <a name="next-steps"></a>Passos Seguintes

[Início rápido: Criar um cluster do Explorador de dados do Azure e a base de dados](create-cluster-database-portal.md)

[Início rápido: Ingerir dados de Hub de eventos no Explorador de dados do Azure](ingest-data-event-hub.md)

[Início rápido: Consultar dados no Explorador de dados do Azure](web-query-data.md)
