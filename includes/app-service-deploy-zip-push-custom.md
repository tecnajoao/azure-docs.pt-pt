---
author: cephalin
ms.service: app-service
ms.topic: include
ms.date: 11/03/2016
ms.author: cephalin
ms.openlocfilehash: 79fb8517ec6880e8a3eae0e74275567a24644b87
ms.sourcegitcommit: 9d7391e11d69af521a112ca886488caff5808ad6
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/25/2018
ms.locfileid: "50133530"
---
## <a name="deployment-customization"></a>Personalização da implementação

O processo de implantação parte do princípio de que o ficheiro. zip que enviar contém uma aplicação de prontos para executar. Por predefinição, são executadas sem personalizações. Para ativar os mesmos processos de compilação que obtém com a integração contínua, adicione o seguinte para as definições da aplicação:

    SCM_DO_BUILD_DURING_DEPLOYMENT=true 

Quando usa a implementação de push. zip, esta definição é **false** por predefinição. A predefinição é **true** para implementações de integração contínua. Quando definido como **true**, as definições relacionadas com a implementação são utilizadas durante a implementação. Pode configurar estas definições, como definições da aplicação ou num ficheiro de configuração. Deployment que está localizado na raiz do seu ficheiro. zip. Para obter mais informações, consulte [repositório e definições relacionadas com a implementação](https://github.com/projectkudu/kudu/wiki/Configurable-settings#repository-and-deployment-related-settings) na referência de implementação.