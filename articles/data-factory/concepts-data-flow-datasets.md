---
title: Mapeamento de conjuntos de dados de fluxo de dados de fábrica de dados do Azure
description: O Azure Data Factory mapeamento de fluxo de dados tem a compatibilidade do conjunto de dados específico
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.date: 02/14/2019
ms.openlocfilehash: efb82c57a5620ef3eace8b39f6f27f2286202f84
ms.sourcegitcommit: 6da4959d3a1ffcd8a781b709578668471ec6bf1b
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58521844"
---
# <a name="mapping-data-flow-datasets"></a>Conjuntos de dados de fluxo de dados de mapeamento

[!INCLUDE [notes](../../includes/data-factory-data-flow-preview.md)]

Conjuntos de dados são uma construção de fábrica de dados que definem a forma dos dados que está a trabalhar no seu pipeline. No fluxo de dados, os dados de nível de coluna e linha requerem uma definição de conjunto de dados escalados refinado. Conjuntos de dados utilizados em pipelines de fluxo de controle não exigem a mesma profundidade de compreensão de dados.

Conjuntos de dados no fluxo de dados são utilizados nas transformações de origem e Sink. São utilizados para definir os esquemas de dados básicos. Se não tiver esquema nos seus dados, pode definir os Descompassos de esquema para a sua origem e Sink. Com o esquema definido do conjunto de dados, terá os tipos de dados relacionados, formatos de dados, localização do ficheiro e informações de ligação do serviço ligado associados. Os metadados de conjuntos de dados irão aparecer na sua transformação de origem como a origem "Projeção". O esquema do conjunto de dados representa o tipo de dados físico e de forma enquanto a projeção na transformação de origem representa a representação de fluxo de dados dos dados com nomes predefinidos e de tipos.

## <a name="dataset-types"></a>Tipos de conjunto de dados

Atualmente no fluxo de dados, encontrará quatro tipos de conjunto de dados:

* BD SQL do Azure
* Azure SQL DW
* Parquet (a partir do ADLS e BLOBs)
* Texto delimitado (a partir do ADLS e BLOBs)

Datasets de fluxo de dados separado a *tipo de origem* partir a *tipo de ligação de serviço ligado*. Normalmente, no Data Factory, selecione o tipo de ligação (Blob, ADLS, etc.) e, em seguida, definir o tipo de ficheiro no conjunto de dados. Dentro do fluxo de dados, escolhe os tipos de origem, o que podem ser associados com diferentes tipos de ligação de serviço ligado.

![Opções de transformação de origem](media/data-flow/dataset1.png "origens")

## <a name="data-flow-compatible-datasets"></a>Conjuntos de dados compatíveis do fluxo de dados

Ao criar um novo conjunto de dados, há uma caixa de seleção rotulada como "Dados de fluxo compatível" no canto superior direito do painel. Ao clicar nesse botão irá filtrar apenas os conjuntos de dados que podem ser utilizados com fluxos de dados. 

## <a name="import-schemas"></a>Importar esquemas

Ao importar o esquema de conjuntos de dados de fluxo de dados, verá um botão importar esquema. Ao clicar nesse botão irá apresentar-lhe duas opções: Importar da origem ou importar a partir de um ficheiro local. Na maioria dos casos, irá importar o esquema diretamente da fonte. No entanto, se tiver um ficheiro de esquema existente (ficheiro Parquet ou CSV com cabeçalhos), pode apontar para ficheiro local e o Data Factory irão definir o esquema com base nesse ficheiro de esquema.

## <a name="create-new-table"></a>Criar nova tabela

No fluxo de dados, pode pedir o ADF para criar uma nova definição de tabela na base de dados de destino através da definição de um conjunto de dados na transformação de Sink, que tem um novo nome de tabela. No conjunto de dados SQL, clique em "Editar" abaixo o nome da tabela e introduza um novo nome de tabela. Em seguida, na transformação de Sink, ative "Permitir Descompassos de esquema". Seth a definição de "Importar esquema" como None.

![Esquema de transformação de origem](media/data-flow/dataset2.png "esquema SQL")

## <a name="choose-your-type-of-data-first"></a>Escolher o tipo de dados pela primeira vez

### <a name="delimited-text"></a>Texto delimitado

O conjunto de dados de texto delimitado, definirá o delimitador para lidar com qualquer um dos delimitadores únicos ("\t"para TSV,',' para CSV, "|"...) ou utilizar vários carateres para o delimitador. Defina o Seletor de linha de cabeçalho e, em seguida, vá para a transformação de origem para detetar automaticamente tipos de dados. Se estiver a utilizar um conjunto de dados de texto delimitado por para mover dados num coletor, basta Selecione uma pasta de destino. Nas definições de Sink, pode definir o nome dos ficheiros de saída.

### <a name="parquet"></a>Parquet

Utilize o Parquet como o tipo de conjunto de dados de teste preferido nos fluxos de dados do ADF. Parquet armazenará o esquema de metadados sofisticados juntamente com os dados.

### <a name="database-types"></a>Tipos de base de dados

Pode selecionar a BD SQL do Azure ou o Azure SQL DW.

Para os outros ADF conjunto de dados tipos, utilize a atividade de cópia para testar os seus dados. Existe um modelo do ADF na Galeria de modelos para ajudar a criar este padrão.

![Copie a transição](media/data-flow/templatedf.png "copiar teste")

## <a name="choose-your-connection-type"></a>Escolher o tipo de ligação

Se estiver a utilizar o Parquet ou de texto delimitado por conjuntos de dados, em seguida, pode selecionar a localização para os seus dados: ADLS ou Blob.

## <a name="next-steps"></a>Passos Seguintes

Comece por [criar um novo fluxo de dados](data-flow-create.md) e adicione uma transformação de origem. Em seguida, configure o conjunto de dados para a sua origem.

Utilize o [atividade de cópia](copy-activity-overview.md) para importar dados a partir de qualquer ADF origem de dados e testá-los no ADLS ou BLOBs para acesso por fluxo de dados.

