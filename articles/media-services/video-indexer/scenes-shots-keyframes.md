---
title: Nos bastidores, capturas e quadros-chave - Azure indexador vídeo
titlesuffix: Azure Media Services
description: Este tópico apresenta uma visão geral do plano indexador de vídeos, capturas e quadros-chave.
services: media-services
author: Juliako
manager: femila
ms.service: media-services
ms.topic: article
ms.date: 04/01/2019
ms.author: juliako
ms.openlocfilehash: dfa41dc695cf6ab357a9cd4cdbd32454b6dd107d
ms.sourcegitcommit: 0a3efe5dcf56498010f4733a1600c8fe51eb7701
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/03/2019
ms.locfileid: "58896557"
---
# <a name="scenes-shots-and-keyframes"></a>Nos bastidores, capturas e quadros-chave

O Video Indexer suporta segmentar vídeos em unidades temporais com base nas propriedades de estruturais e semânticas. Esta capacidade permite aos clientes procurar, gerir e editar o conteúdo de vídeo com base nas granularidades variadas facilmente. Por exemplo, com base em segundo plano, capturas e quadros-chave, descritas neste tópico. O **deteção de cena** funcionalidade está atualmente em pré-visualização.   

![Nos bastidores, capturas e quadros-chave](./media/scenes-shots-keyframes/scenes-shots-keyframes.png)

## <a name="scene-detection-preview"></a>Deteção de cena (pré-visualização)

O Video Indexer determina quando uma cena altera em vídeo com base no indicações visuais. Uma cena descreve um único evento e é composta por uma série de capturas consecutivas, que é semanticamente estão relacionados. Uma miniatura de cena é o primeiro quadro-chave da respetiva captura subjacente. O Video indexer segmenta um vídeo em plano com base em coerência de cor em capturas de consecutivas e recupera o início e hora de fim de cada cena. Deteção de cena é considerada uma tarefa desafiadora, pois envolve a quantificação aspectos semânticos de vídeos.

> [!NOTE]
> Aplicável a vídeos que contêm pelo menos 3 plano.

## <a name="shot-detection"></a>Deteção de captura

O Video Indexer determina quando uma captura alterações no vídeo com base em indicações visuais, ao controlar as transições de reinicialização abrupta e graduais no esquema de cores de quadros adjacentes. Metadados de captura incluem um início e hora de fim, bem como a lista de quadros-chave incluída no que captura. As capturas de são consecutivos quadros obtidos a partir da câmera mesmo ao mesmo tempo.

## <a name="keyframe-detection"></a>Deteção de Keyframe

Seleciona o frame(s) que melhor representa a captura. Quadros-chave é os quadros representativos selecionados do vídeo todo com base nas propriedades estética (por exemplo, contraste e stableness). O Video Indexer obtém uma lista de IDs de quadro-chave como parte dos metadados de captura, com base no qual os clientes podem extrair a miniatura do quadro-chave. 

Quadros-chave está associados com capturas de JSON de saída. 

## <a name="next-steps"></a>Passos Seguintes

[Examine a saída do indexador de vídeo produzida pela API](video-indexer-output-json-v2.md#scenes)