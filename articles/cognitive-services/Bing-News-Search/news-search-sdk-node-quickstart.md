---
title: 'Início rápido: Efetua uma pesquisa de notícias - SDK de pesquisa de notícias do Bing para node. js'
titleSuffix: Azure Cognitive Services
description: Utilize este guia de introdução para pesquisar notícias utilizando o SDK de pesquisa de notícias do Bing para node. js e processar a resposta.
services: cognitive-services
author: mikedodaro
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-news-search
ms.topic: quickstart
ms.date: 01/10/2019
ms.author: v-gedod
ms.custom: seodec2018
ms.openlocfilehash: 1930ef761b4be9d8085fd6e1785e78146c6b5547
ms.sourcegitcommit: 2d0fb4f3fc8086d61e2d8e506d5c2b930ba525a7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/18/2019
ms.locfileid: "58109172"
---
# <a name="quickstart-perform-a-news-search-with-the-bing-news-search-sdk-for-nodejs"></a>Início rápido: Efetua uma pesquisa de notícias com o SDK de pesquisa de notícias do Bing para node. js

Utilize este guia de introdução para a pesquisa de notícias com o SDK de pesquisa de notícias do Bing para node. js. Embora a pesquisa do Bing notícias tenha uma API de REST compatível com a maioria das linguagens de programação, o SDK fornece uma forma fácil de integrar o serviço aos seus aplicativos. O código-fonte para este exemplo pode ser encontrado no [GitHub](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/newsSearch.js).

## <a name="prerequisites"></a>Pré-requisitos

* [Node.js](https://nodejs.org/en/)

Para configurar uma aplicação de consola com o SDK de pesquisa de notícias do Bing:
1. Executar `npm install ms-rest-azure` no seu ambiente de desenvolvimento.
2. Executar `npm install azure-cognitiveservices-newssearch` no seu ambiente de desenvolvimento.


[!INCLUDE [cognitive-services-bing-news-search-signup-requirements](../../../includes/cognitive-services-bing-news-search-signup-requirements.md)]

## <a name="create-and-initialize-the-application"></a>Criar e inicializar a aplicação

1. Crie uma instância de `CognitiveServicesCredentials`. Crie variáveis para a chave de subscrição e um termo de pesquisa.

    ```javascript
    const CognitiveServicesCredentials = require('ms-rest-azure').CognitiveServicesCredentials;
    let credentials = new CognitiveServicesCredentials('YOUR-ACCESS-KEY');
    let search_term = 'Winter Olympics'
    ```

2. Criar uma instância do cliente:
    
    ```javascript
    const NewsSearchAPIClient = require('azure-cognitiveservices-newssearch');
    let client = new NewsSearchAPIClient(credentials);
    ```

## <a name="send-a-search-query"></a>Enviar uma consulta de pesquisa

1. Utilize o cliente para pesquisar com um termo de consulta, neste caso, "Jogos Olímpicos de Inverno":
    
    ```javascript
    client.newsOperations.search(search_term).then((result) => {
        console.log(result.value);
    }).catch((err) => {
        throw err;
    });
    ```

O código imprime `result.value` itens na consola sem analisar o texto. Os resultados, se existirem por categoria, incluirão:

- `_type: 'NewsArticle'`
- `_type: 'WebPage'`
- `_type: 'VideoObject'`
- `_type: 'ImageObject'`

## <a name="next-steps"></a>Passos Seguintes

> [!div class="nextstepaction"]
> [Criar uma aplicação Web de página única](tutorial-bing-news-search-single-page-app.md)
