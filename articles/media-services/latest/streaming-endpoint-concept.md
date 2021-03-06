---
title: Transmissão em fluxo de pontos de extremidade nos serviços de multimédia do Azure | Documentos da Microsoft
description: Este artigo fornece uma explicação sobre o que são pontos finais de transmissão em fluxo e como elas são usadas pelos serviços de multimédia do Azure.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 04/01/2019
ms.author: juliako
ms.openlocfilehash: 2e715e5280794172451a333624a954340a1a60fe
ms.sourcegitcommit: a60a55278f645f5d6cda95bcf9895441ade04629
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/03/2019
ms.locfileid: "58881023"
---
# <a name="streaming-endpoints"></a>Pontos Finais de Transmissão em fluxo

No Microsoft Azure Media Services (AMS), o [pontos finais de transmissão em fluxo](https://docs.microsoft.com/rest/api/media/streamingendpoints) entidade representa um serviço de transmissão em fluxo que pode entregar conteúdo diretamente a uma aplicação de leitor cliente ou para uma rede de entrega de conteúdo (CDN) para obter mais distribuição. O fluxo de saída de um **ponto final de transmissão em fluxo** serviço pode ser uma transmissão em direto ou um elemento de vídeo a pedido na sua conta de Media Services. Quando cria uma conta de Media Services, um **predefinição** ponto final de transmissão em fluxo é criado por si no estado parado. Não é possível eliminar a **predefinição** ponto final de transmissão em fluxo. Pontos finais de transmissão em fluxo adicionais podem ser criados sob a conta. 

> [!NOTE]
> Para começar a transmissão em fluxo de vídeos, precisa para começar a **ponto final de transmissão em fluxo** partir da qual quer transmitir o vídeo. 
>  
> É-lhe cobrada apenas quando o ponto final de transmissão em fluxo está no estado de execução.

## <a name="naming-convention"></a>Convenção de nomenclatura

Para o ponto final predefinido: `{AccountName}-{DatacenterAbbreviation}.streaming.media.azure.net`

Para pontos finais adicionais: `{EndpointName}-{AccountName}-{DatacenterAbbreviation}.streaming.media.azure.net`

## <a name="types"></a>Tipos  

Existem dois tipos de **Ponto Final de Transmissão em Fluxo**: **Standard** e **Premium**. O tipo é definido pelo número de unidades de escala (`scaleUnits`) alocar para o ponto final de transmissão em fluxo. 

A tabela descreve os tipos:  

|Type|Unidades de escala|Descrição|
|--------|--------|--------|  
|**Ponto Final de Transmissão em Fluxo Standard** (recomendado)|0|A predefinição é o ponto final de transmissão em fluxo uma **padrão** tipo, mas pode ser alterada para o tipo Premium.<br/> O tipo de padrão é a opção recomendada para praticamente todos os cenários de transmissão em fluxo e tamanhos de audiência. O tipo **Standard** dimensiona a largura de banda de saída automaticamente. O débito deste tipo de ponto final de transmissão em fluxo é até 600 Mbps. Fragmentos de vídeo colocado em cache no CDN, não utilize a largura de banda do ponto final de transmissão em fluxo.<br/>Para clientes com requisitos extremamente exigentes, os Serviços de Multimédia oferecem pontos finais de transmissão em fluxo **Premium**, que podem ser utilizados para ampliar a capacidade para as maiores audiências de internet. Se espera grandes públicos e visualizadores em simultâneo, contacte-nos em amsstreaming\@microsoft.com para obter orientações sobre a necessidade de mover para o **Premium** tipo. |
|**Ponto final de transmissão em fluxo Premium**|>0|Os pontos finais de transmissão em fluxo **Premium** são adequadas para cargas de trabalho avançadas, ao fornecer uma capacidade de largura de banda dimensionável e dedicada. Mover para uma **Premium** tipo ao ajustar `scaleUnits`. `scaleUnits` Fornece capacidade de saída dedicada que pode ser comprada em incrementos de 200 Mbps. Ao utilizar o tipo **Premium**, cada unidade ativada fornece capacidade de largura de banda adicional à aplicação. |
 
## <a name="comparing-streaming-types"></a>Comparar tipos de transmissão em fluxo

### <a name="features"></a>Funcionalidades

Funcionalidade|Standard|Premium
---|---|---
Gratuitos primeiros 15 dias| Sim |Não
Débito |Até 600 Mbps quando não for utilizada o CDN do Azure. Dimensiona com CDN.|200 Mbps por unidade (SU) de transmissão em fluxo. Dimensiona com CDN.
SLA | 99.9|99,9 (200 Mbps por SU).
CDN|A CDN do Azure, terceiros CDN ou não CDN.|A CDN do Azure, terceiros CDN ou não CDN.
A faturação é calculada| Diariamente|Diariamente
Encriptação dinâmica|Sim|Sim
Empacotamento dinâmico|Sim|Sim
Escala|Automática se aumentar verticalmente para a taxa de transferência de destino.|Unidades de transmissão em fluxo adicionais
Anfitrião de filtragem/G20/personalizado IP <sup>1</sup>|Sim|Sim
Transferência progressiva|Sim|Sim
Uso recomendado |Recomendado para a grande maioria dos cenários de transmissão em fluxo.|Utilização profissional.<br/>Se acha que podem ter necessidades além padrão. Contacte-nos (amsstreaming@microsoft.com) se espera que um tamanho de audiência em simultâneo maior do que 50.000 visualizadores.

<sup>1</sup> usado diretamente no ponto final de transmissão em fluxo apenas quando a CDN não estiver ativada no ponto final.

## <a name="properties"></a>Propriedades 

Esta secção fornece detalhes sobre algumas das propriedades de transmissão em fluxo do ponto de extremidade. Para obter exemplos de como criar um novo ponto de final de transmissão em fluxo e as descrições de todas as propriedades, consulte [ponto final de transmissão em fluxo](https://docs.microsoft.com/rest/api/media/streamingendpoints/create). 

- `accessControl` -Utilizado para configurar as seguintes definições de segurança para este ponto final de transmissão em fluxo: Chaves de autenticação de cabeçalho de assinatura de Akamai e endereços IP que estão autorizados a ligar a este ponto final.<br />Só pode ser definida esta propriedade quando `cdnEnabled` é definido como false.
- `cdnEnabled` -Indica se é ou não a integração da CDN do Azure para este ponto final de transmissão em fluxo ativado (desativado por predefinição). Se definir `cdnEnabled` como true, as seguintes configurações obterem desativadas: `customHostNames` e `accessControl`.
  
    Nem todos os centros de dados suportam a integração da CDN do Azure. Para verificar se tem ou não seu centro de dados a integração da CDN do Azure disponível, faça o seguinte:
 
  - Tente definir o `cdnEnabled` como true.
  - Verificar o resultado retornado para um `HTTP Error Code 412` (PreconditionFailed) com uma mensagem de "Propriedade CdnEnabled de ponto final de transmissão em fluxo não pode ser definido como true, conforme a capacidade CDN não está disponível na região atual." 

    Se obtiver este erro, o Centro de dados não o suporta. Deve tentar outro centro de dados.
- `cdnProfile` -Quando `cdnEnabled` está definido como true, também é possível passar `cdnProfile` valores. `cdnProfile` é o nome do perfil da CDN de onde será criado o ponto de ponto final CDN. Pode fornecer um cdnProfile existente ou utilizar um novo. Se o valor é NULL e `cdnEnabled` é true, o valor predefinido "AzureMediaStreamingPlatformCdnProfile" é utilizado. Se o fornecido `cdnProfile` já existir, é criado um ponto final sob a mesma. Se o perfil não existir, é criado um novo perfil automaticamente.
- `cdnProvider` -Quando a CDN estiver ativada, pode também passar `cdnProvider` valores. `cdnProvider` controla qual o fornecedor será utilizado. Atualmente, são suportados os três valores: "StandardVerizon", "PremiumVerizon" e "StandardAkamai". Se não for fornecido nenhum valor e `cdnEnabled` for VERDADEIRO, "StandardVerizon" é utilizado (ou seja, o valor predefinido).
- `crossSiteAccessPolicies` -Utilizado para especificar políticas de acesso entre sites para vários clientes. Para obter mais informações, consulte [especificação de ficheiro de política entre domínios](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html) e [fazendo um serviço disponível em domínio limites](https://msdn.microsoft.com/library/cc197955\(v=vs.95\).aspx).<br/>As definições só se aplicam a transmissão em fluxo uniforme.
- `customHostNames` -Utilizado para configurar um ponto final de transmissão em fluxo para aceitar o tráfego direcionado para um nome de anfitrião personalizado.  Esta propriedade é válida para o Standard e os pontos finais de transmissão em fluxo Premium e pode ser definida quando `cdnEnabled`: FALSO.
    
    A propriedade de nome de domínio tem de ser confirmada pelos serviços de multimédia. Serviços de multimédia verifica a propriedade de nome de domínio, exigindo que um `CName` registo que contém o ID de conta de Media Services como um componente ser adicionado ao domínio em utilização. Por exemplo, para "sports.contoso.com" ser utilizado como um nome de anfitrião personalizado para o ponto final de transmissão, um registo para `<accountId>.contoso.com` deve ser configurado para apontar para um dos nomes de anfitrião de verificação de serviços de multimédia. O nome de anfitrião de verificação é composta por verifydns. \<zona de dns de mediaservices >. 

    Seguem-se as zonas DNS esperadas a ser utilizado no registo de verificar para diferentes regiões do Azure.
  
  - América do Norte, Europa, Singapura, Hong Kong, Japão:
      
    - `media.azure.net`
    - `verifydns.media.azure.net`
      
  - China:
        
    - `mediaservices.chinacloudapi.cn`
    - `verifydns.mediaservices.chinacloudapi.cn`
        
    Por exemplo, um `CName` registo que mapeia "945a4c4e-28ea-45 cd-8ccb-a519f6b700ad.contoso.com" para "verifydns.media.azure.net" comprova que 945a4c4e-28ea-45cd-8ccb-a519f6b700ad o ID de serviços de suporte de dados tem a propriedade do domínio contoso.com, assim, permitir que qualquer nome em contoso.com para ser utilizado como um nome de anfitrião personalizado para um ponto final de transmissão em fluxo nessa conta. Para encontrar o valor de ID de serviço de suporte de dados, vá para o [portal do Azure](https://portal.azure.com/) e selecione a sua conta de serviço de multimédia. O **ID da conta** aparece no canto superior direito da página.
        
    Se houver uma tentativa para definir um nome de anfitrião personalizado sem uma verificação adequada do `CName` registo, a resposta DNS falhará e, em seguida, ser colocados em cache durante algum tempo. Depois de um registo adequado estiver em vigor, poderá demorar algum tempo até que a resposta em cache é revalidar. Dependendo do fornecedor DNS para o domínio personalizado, pode demorar em qualquer lugar de alguns minutos para uma hora para revalide o registo.
        
    Para além da `CName` que mapeia `<accountId>.<parent domain>` para `verifydns.<mediaservices-dns-zone>`, tem de criar outro `CName` que mapeia o nome de anfitrião personalizado (por exemplo, `sports.contoso.com`) para o nome de anfitrião do seu suporte de dados dos serviços de transmissão em fluxo do ponto de extremidade (por exemplo, `amstest-usea.streaming.media.azure.net`).
 
    > [!NOTE]
    > Localizado no mesmo centro de dados, de pontos finais de transmissão em fluxo não é possível partilhar o mesmo nome de anfitrião personalizado.

    Atualmente, os serviços de multimédia não suporta SSL com domínios personalizados. 
    
- `maxCacheAge` -Substituições o cache HTTP de idade máxima de padrão controlar cabeçalho definido pelo ponto de final de transmissão em fluxo em fragmentos de suporte de dados e manifestos de sob demanda. O valor é definido em segundos.
- `resourceState` -

    - Parado – o estado inicial de um ponto final de transmissão em fluxo após a criação
    - A iniciar - é fazer a transição para o estado de execução
    - Em execução - é capaz de transmitir conteúdos para clientes
    - Dimensionamento - dimensionamento unidades estão a ser aumenta ou diminui
    - A parar - é fazer a transição para o estado de paragem
    - A eliminar - está a ser eliminada
    
- `scaleUnits` -Fornece capacidade de saída dedicada que pode ser comprada em incrementos de 200 Mbps. Se precisar de mover para uma **Premium** escreva, ajuste `scaleUnits`.

## <a name="working-with-cdn"></a>Trabalhar com CDN

Na maioria dos casos, deve ter a CDN ativada. No entanto, se estiver a prever uma simultaneidade máxima inferior a 500 visualizadores, recomendamos que desative a CDN, uma vez que a CDN dimensiona melhor com simultaneidade.

### <a name="considerations"></a>Considerações

* O ponto final de transmissão em fluxo `hostname` e o URL de transmissão em fluxo permanece o mesmo se ou não ativar a CDN.
* Se tiver a capacidade de testar o seu conteúdo com ou sem CDN, pode criar outro Endpoint de transmissão em fluxo que não seja CDN ativada.

### <a name="detailed-explanation-of-how-caching-works"></a>Explicação detalhada de como o cache funciona

Não existe nenhum valor de largura de banda específica quando adicionar a CDN, porque a quantidade de largura de banda que é necessária para uma CDN ativado o ponto final de transmissão em fluxo varia. Muito depende do tipo de conteúdo, quão popular é, velocidades de transmissão e os protocolos. A CDN é apenas a colocação em cache o que está a ser requerido. Isso significa que será fornecido popular conteúdo diretamente a partir da CDN – desde que o fragmento de vídeo é colocado em cache. Conteúdo em direto é provável que sejam armazenados em cache porque, normalmente, tem muitas pessoas exatamente a mesma coisa a observar. Conteúdo sob demanda pode ser um pouco mais complicado, porque poderia ter algum conteúdo que é popular e algumas que não é. Se tiver de milhões de recursos de vídeo em que nenhuma delas é populares (apenas 1 ou 2 visualizadores por semana), tem milhares de pessoas ver vídeos todos diferentes, mas, a CDN se torna muito menos eficaz. Com esta cache erros, aumenta a carga no ponto de final de transmissão em fluxo.
 
Terá também de considerar como adaptável funciona de transmissão em fluxo. Cada fragmento de vídeo individual é colocado em cache, pois é a própria entidade. Por exemplo, se a primeira vez que um determinado vídeo é observado, a pessoa ignora em torno de apenas alguns segundos a observar aqui e Ali apenas os fragmentos de vídeos associados com o que a pessoa assistiu obterem armazenados em cache no CDN. Com a transmissão em fluxo adaptável, normalmente tem 5 a 7 diferentes velocidades de transmissão de vídeo. Se uma pessoa está a observar uma velocidade de transmissão e a outra pessoa está a observar uma velocidade de transmissão diferente, em seguida, eles são cada colocadas em cache separadamente na CDN. Mesmo se duas pessoas estão observando a mesma velocidade de transmissão eles poderiam ser de transmissão em fluxo através de protocolos diferentes. Cada protocolo (HLS, MPEG-DASH, Smooth Streaming) é armazenado em cache separadamente. Portanto, cada velocidade de transmissão e o protocolo são colocadas em cache em separado e são armazenados em cache apenas esses fragmentos de vídeo que foram solicitados.

### <a name="enable-azure-cdn-integration"></a>Ativar a integração da CDN do Azure

Depois de um ponto final de transmissão em fluxo é aprovisionado com o CDN ativada aqui é um tempo de espera definido nos serviços de suporte de dados antes de atualização de DNS é feita para mapear o ponto final de transmissão em fluxo para o ponto final da CDN.

Se pretender mais tarde desativar/ativar a CDN, o ponto final de transmissão em fluxo tem de estar no **parado** estado. Pode demorar até duas horas para que a integração da CDN do Azure obter ativada e as alterações de ser o Active Directory em todos os POP de CDN. No entanto, pode iniciar o seu ponto final de transmissão em fluxo e fluxo sem interrupções a partir do ponto final de transmissão em fluxo e assim que a integração foi concluída, a transmissão é entregue da CDN. Durante o período de aprovisionamento, o ponto final de transmissão em fluxo vai estar num **a partir de** estado e poderá observar degradação do desempenho.

Quando o ponto de final de transmissão em fluxo Standard é criado, ele é configurado por predefinição com Standard da Verizon. Pode configurar fornecedores de Premium da Verizon ou Standard da Akamai com REST APIs. 

Integração da CDN está ativada em todos os centros de dados do Azure, exceto a China e Governo Federal regiões.

> [!IMPORTANT]
> Integração de serviços de multimédia do Azure com a CDN do Azure é implementada em **CDN do Azure da Verizon** para padrão de transmissão em fluxo em pontos de extremidade. Pontos finais de transmissão em fluxo Premium pode ser configurada com todos os **CDN do Azure, fornecedores e escalões de preços**. Para obter mais informações sobre as funcionalidades de CDN do Azure, consulte a [descrição geral da CDN](../../cdn/cdn-overview.md).

### <a name="determine-if-dns-change-has-been-made"></a>Determinar se foi efetuada qualquer alteração DNS

Pode determinar se a alteração de DNS foi efetuada num ponto final de transmissão em fluxo (o tráfego estiver sendo direcionado para a CDN do Azure) utilizando https://www.digwebinterface.com. Se os resultados tem nomes de domínio azureedge.net nos resultados, o tráfego é agora que está sendo apontado para a CDN.

## <a name="next-steps"></a>Passos Seguintes

O exemplo [neste repositório](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs) mostra como iniciar o transmissão em fluxo ponto final com o .NET de predefinido.

