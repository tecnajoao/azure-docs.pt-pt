---
title: 'Início rápido: Sintetizar a conversão de voz, C++ (Linux) - serviços de voz'
titleSuffix: Azure Cognitive Services
description: Saiba como sintetizar voz em C++ no Linux com o SDK de voz
services: cognitive-services
author: yinhew
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: quickstart
ms.date: 4/03/2019
ms.author: yinhew
ms.openlocfilehash: c0981ec993f3717f3ec3d3da987a5977b212fb9f
ms.sourcegitcommit: e43ea344c52b3a99235660960c1e747b9d6c990e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/04/2019
ms.locfileid: "59012235"
---
# <a name="quickstart-synthesize-speech-in-c-on-linux-by-using-the-speech-sdk"></a>Início rápido: Sintetizar voz em C++ no Linux com o SDK de voz

Neste artigo, vai criar uma aplicação de consola C++ para o Ubuntu 16.04 de Linux ou 18.04. Utiliza os serviços cognitivos [SDK de voz](speech-sdk.md) sintetizar a voz do texto em tempo real e reproduzir a conversão de voz no orador do seu PC. A aplicação é criada com o [SDK de Voz para Linux](https://aka.ms/csspeech/linuxbinary) e o compilador de C++ da sua distribuição Linux (por exemplo, `g++`).

## <a name="prerequisites"></a>Pré-requisitos

Precisa de uma chave de subscrição de serviços de voz para concluir este início rápido. Pode obter uma gratuitamente. Ver [experimentar gratuitamente os serviços de voz](get-started.md) para obter detalhes.

## <a name="install-speech-sdk"></a>Instalar o SDK de Voz

[!INCLUDE [License Notice](../../../includes/cognitive-services-speech-service-license-notice.md)]

A versão atual do SDK de Voz dos Serviços Cognitivos é `1.4.0`.

O SDK de Voz para Linux pode ser utilizado para criar aplicações de 64 e 32 bits. As bibliotecas necessárias e os arquivos de cabeçalho podem ser baixados como um ficheiro de destino da https://aka.ms/csspeech/linuxbinary.

Transfira e instale o SDK da seguinte forma:

1. Certifique-se de que as dependências do SDK estão instaladas.

   ```sh
   sudo apt-get update
   sudo apt-get install build-essential libssl1.0.0 libasound2 wget
   ```

1. Escolha um diretório para o qual os ficheiros do SDK de Voz serão extraídos e defina a variável de ambiente `SPEECHSDK_ROOT` para apontar para esse diretório. Esta variável facilita a referência ao diretório em comandos futuros. Por exemplo, se pretender utilizar o diretório `speechsdk` no diretório-raiz, utilize um comando semelhante ao seguinte:

   ```sh
   export SPEECHSDK_ROOT="$HOME/speechsdk"
   ```

1. Crie o diretório se este ainda não existir.

   ```sh
   mkdir -p "$SPEECHSDK_ROOT"
   ```

1. Transfira e extraia o arquivo `.tar.gz` que contém os binários do SDK de Voz:

   ```sh
   wget -O SpeechSDK-Linux.tar.gz https://aka.ms/csspeech/linuxbinary
   tar --strip 1 -xzf SpeechSDK-Linux.tar.gz -C "$SPEECHSDK_ROOT"
   ```

1. Valide os conteúdos do diretório de nível superior do pacote extraído:

   ```sh
   ls -l "$SPEECHSDK_ROOT"
   ```

   A lista de diretórios deve conter o aviso de terceiros e os ficheiros de licença, bem como um diretório `include` com ficheiros de cabeçalho (`.h`) e um diretório `lib` com as bibliotecas.

   [!INCLUDE [Linux Binary Archive Content](../../../includes/cognitive-services-speech-service-linuxbinary-content.md)]

## <a name="add-sample-code"></a>Adicionar código de exemplo

1. Crie um ficheiro de origem C++ com o nome `helloworld.cpp` e cole o código seguinte no mesmo.

   [!code-cpp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/text-to-speech/cpp-linux/helloworld.cpp#code)]

1. Neste novo ficheiro, substitua a cadeia de caracteres `YourSubscriptionKey` com a sua chave de subscrição de serviços de voz.

1. Substitua a cadeia de carateres `YourServiceRegion` pela [região](regions.md) associada à subscrição (por exemplo, `westus` para a subscrição de avaliação gratuita).

## <a name="build-the-app"></a>Criar a aplicação

> [!NOTE]
> Certifique-se de introduz os comandos abaixo como uma _única linha de comandos_. A maneira mais fácil de o fazer é copiar o comando com o botão **Copiar** junto a cada comando e, em seguida, colá-lo na sua linha de comandos da shell.

* Num sistema **x64** (64 bits), execute o comando seguinte para criar a aplicação.

  ```sh
  g++ helloworld.cpp -o helloworld -I "$SPEECHSDK_ROOT/include/cxx_api" -I "$SPEECHSDK_ROOT/include/c_api" --std=c++14 -lpthread -lMicrosoft.CognitiveServices.Speech.core -L "$SPEECHSDK_ROOT/lib/x64" -l:libssl.so.1.0.0 -l:libasound.so.2
  ```

* Num sistema **x86** (32 bits), execute o comando seguinte para criar a aplicação.

  ```sh
  g++ helloworld.cpp -o helloworld -I "$SPEECHSDK_ROOT/include/cxx_api" -I "$SPEECHSDK_ROOT/include/c_api" --std=c++14 -lpthread -lMicrosoft.CognitiveServices.Speech.core -L "$SPEECHSDK_ROOT/lib/x86" -l:libssl.so.1.0.0 -l:libasound.so.2
  ```

## <a name="run-the-app"></a>Executar a aplicação

1. Configure o caminho da biblioteca do carregador para apontar para a biblioteca do SDK de Voz.

   * Num sistema **x64** (64 bits), introduza o comando seguinte.

     ```sh
     export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:$SPEECHSDK_ROOT/lib/x64"
     ```

   * Num sistema **x86** (32 bits), introduza o comando seguinte.

     ```sh
     export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:$SPEECHSDK_ROOT/lib/x86"
     ```

1. Execute a aplicação.

   ```sh
   ./helloworld
   ```

1. Na janela do console, um aviso é exibido, solicitando que introduza algum texto. Escreva algumas palavras ou uma frase. O texto que introduziu é transmitido para os serviços de voz e sintetizado para conversão de voz, que desempenha na sua orador.

   ```text
   Type some text that you want to speak...
   > hello
   Speech synthesized to speaker for text [hello]
   Press enter to exit...
   ```

## <a name="next-steps"></a>Passos Seguintes

> [!div class="nextstepaction"]
> [Explore exemplos de C++ no GitHub](https://aka.ms/csspeech/samples)

## <a name="see-also"></a>Consulte também

- [Personalizar tipos de voz](how-to-customize-voice-font.md)
- [Gravar amostras de voz](record-custom-voice-samples.md)
