---
title: Suporte HTTP/2 na CDN do Azure | Microsoft Docs
description: Saiba mais sobre o suporte HTTP/2 e CDN.
services: cdn
documentationcenter: ''
author: lichard
manager: erikre
editor: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: b4751320af82a29fb13dc6012c1b197ebc2b1f9b
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2018
ms.locfileid: "33764847"
---
# <a name="http2-support-in-azure-cdn"></a>Suporte HTTP/2 na CDN do Azure

HTTP/2 é uma revisão principal ao HTTP/1.1\. Fornece mais rapidamente do desempenho da web, tempo de resposta reduzida e melhorada experiência do utilizador, enquanto mantém o métodos de HTTP familiares, códigos de estado e semântica. Apesar de HTTP/2 foi concebida para funcionar com HTTP e HTTPS, muitos browsers do cliente suportam apenas HTTP/2 sobre TLS.

### <a name="http2-benefits"></a>Vantagens HTTP/2

Os benefícios de HTTP/2 incluem:

*   **Multiplexação e simultaneidade**

    Utilizar HTTP 1.1, tornar vários pedidos de recursos requer várias ligações TCP e cada ligação tem uma tolerância de desempenho associada ao mesmo. HTTP/2 permite vários recursos de pedido numa única ligação TCP.

*   **Compressão de cabeçalho**

    Através da compressão de cabeçalhos de HTTP servidos recursos, hora da transmissão é significativamente reduzida.

*   **Dependências de sequência**

    Dependências de sequência permitem ao cliente indicar ao servidor que recursos tem prioridade.


## <a name="http2-browser-support"></a>Suporte de browsers HTTP/2

Todos os browsers principais tem implementada HTTP/2 suporte das respetivas versões atuais. Não suportado browsers automaticamente contingência para HTTP/1.1.

|Browser|Versão mínima|
|-------------|------------|
|Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

## <a name="enabling-http2-support-in-azure-cdn"></a>Ativar o suporte HTTP/2 na CDN do Azure

Atualmente, o suporte HTTP/2 está ativo para todos os perfis da CDN do Azure. Nenhuma ação adicional é necessária de clientes.

## <a name="next-steps"></a>Próximos Passos

Para ver as vantagens de HTTP/2 em ação, consulte [esta demonstração da Akamai](https://http2.akamai.com/demo).

Para saber mais sobre o HTTP/2, consulte os seguintes recursos:

*   [Home page de especificação de HTTP/2](https://http2.github.io/)
*   [Oficial HTTP/2 FAQ](https://http2.github.io/faq/)
*   [Informações da Akamai HTTP/2](https://http2.akamai.com/)

Para saber mais sobre as funcionalidades disponíveis da CDN do Azure, consulte o [descrição geral da CDN do Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).