---
title: Criar um espaço de desenvolvimento de Kubernetes na cloud com o código VS e .NET Core
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
author: zr-msft
ms.author: zarhoads
ms.date: 09/26/2018
ms.topic: tutorial
description: Desenvolvimento rápido da Kubernetes com contentores e microsserviços no Azure
keywords: Docker, o Kubernetes, o Azure, o AKS, o serviço Kubernetes do Azure, contentores, Helm, a malha de serviço, roteamento de malha do serviço, kubectl, k8s
ms.openlocfilehash: 4c759462d603a35e738f76a505abd04b832afc3f
ms.sourcegitcommit: ef20235daa0eb98a468576899b590c0bc1a38394
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/09/2019
ms.locfileid: "59426346"
---
# <a name="get-started-on-azure-dev-spaces-with-net-core"></a>Começar a trabalhar com espaços de desenvolvimento do Azure com .NET Core

Neste guia, vai aprender a:

- Criar um ambiente baseado no Kubernetes no Azure otimizado para o desenvolvimento - um _espaço de programação_.
- Utilizar o VS Code e a linha de comandos para desenvolver iterativamente código em contentores.
- Desenvolver e testar de forma produtiva o seu código num ambiente de equipa.

> [!Note]
> **Se tiver problemas** em qualquer altura, consulte a [resolução de problemas](troubleshooting.md) secção.

## <a name="install-the-azure-cli"></a>Instalar a CLI do Azure
O Azure Dev Spaces só precisa de configuração mínima do computador local. A maior parte da configuração do espaço de desenvolvimento é armazenada na cloud e é partilhável com outros utilizadores. Comece por transferir e executar a [CLI do Azure](/cli/azure/install-azure-cli?view=azure-cli-latest).

### <a name="sign-in-to-azure-cli"></a>Iniciar sessão na CLI do Azure
Inicie sessão no Azure. Escreva o seguinte comando numa janela de terminal:

```cmd
az login
```

> [!Note]
> Se não tiver uma subscrição do Azure, pode [criar uma conta gratuita](https://azure.microsoft.com/free).

#### <a name="if-you-have-multiple-azure-subscriptions"></a>Se tiver várias subscrições do Azure...
Pode ver as suas subscrições ao executar: 

```cmd
az account list
```
Localize a subscrição que tem `isDefault: true` na saída do JSON.
Se esta não for a subscrição que pretende utilizar, pode alterar a subscrição predefinida:

```cmd
az account set --subscription <subscription ID>
```

## <a name="create-a-kubernetes-cluster-enabled-for-azure-dev-spaces"></a>Criar um cluster do Kubernetes ativado para os Espaços de Programador do Azure

No prompt de comando, criar o grupo de recursos num [região que suporte do Azure Dev espaços](https://docs.microsoft.com/azure/dev-spaces/#a-rapid,-iterative-kubernetes-development-experience-for-teams).

```cmd
az group create --name MyResourceGroup --location <region>
```

Crie um cluster do Kubernetes com o seguinte comando:

```cmd
az aks create -g MyResourceGroup -n MyAKS --location <region> --generate-ssh-keys
```

A criação do cluster demora alguns minutos.

### <a name="configure-your-aks-cluster-to-use-azure-dev-spaces"></a>Configurar o seu cluster do AKS para utilizar os espaços de desenvolvimento do Azure

Introduza o seguinte comando da CLI do Azure com o grupo de recursos que contém o cluster do AKS e o nome do cluster do AKS. O comando configura o seu cluster com suporte para espaços de desenvolvimento do Azure.

   ```cmd
   az aks use-dev-spaces -g MyResourceGroup -n MyAKS
   ```
   
> [!IMPORTANT]
> O processo de configuração de espaços de desenvolvimento do Azure irá remover o `azds` espaço de nomes do cluster, se existir.

## <a name="get-kubernetes-debugging-for-vs-code"></a>Depurar o Kubernetes para o VS Code
Estão disponíveis funcionalidades avançadas, como a depuração do Kubernetes, para programadores de .NET Core e o Node.js com o VS Code.

1. Se não tiver, instale o [VS Code](https://code.visualstudio.com/Download).
1. Transfira e instale a [extensão do Azure Dev Spaces do VS](https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds). Clique em Instalar uma vez na página do Marketplace da extensão e, novamente, no VS Code. 

## <a name="create-a-web-app-running-in-a-container"></a>Criar uma aplicação Web em execução num contentor

Nesta secção, irá criar uma aplicação web ASP.NET Core e executá-lo num contentor no Kubernetes.

### <a name="create-an-aspnet-core-web-app"></a>Criar uma aplicação Web ASP.NET Core
Clonar ou transferir os [aplicação de exemplo do Azure Dev espaços](https://github.com/Azure/dev-spaces). Este artigo usa o código na *amostras/dotnetcore/obter-iniciada/webfrontend* diretório.

## <a name="preparing-code-for-docker-and-kubernetes-development"></a>Preparar o código para implementação do Docker e Kubernetes
Neste momento, tem uma aplicação Web básica que pode ser executada localmente. Agora, irá colocá-la em contentor ao criar recursos que definem o contentor da aplicação e como esta será implementada no Kubernetes. É fácil executar esta tarefa com o Azure Dev Spaces: 

1. Inicie o VS Code e abra a pasta `webfrontend`. (Pode ignorar os pedidos predefinidos para adicionar recursos de erro ou restaurar o projeto.)
1. Abra o Terminal Integrado no VS Code (através do menu **Ver > Terminal Integrado**).
1. Execute este comando (certifique-se de que **webfrontend** é a sua pasta atual):

    ```cmd
    azds prep --public
    ```

O comando `azds prep` da CLI do Azure gera recursos do Docker e Kubernetes com as predefinições:
* `./Dockerfile` Descreve a aplicação imagem de contentor e como o código-fonte é criado e é executado dentro do contentor.
* Um [gráfico Helm](https://docs.helm.sh) em `./charts/webfrontend` descreve como implementar o contentor no Kubernetes.

Por enquanto, não é necessário entender o conteúdo completo desses ficheiros. No entanto, importa realçar que **os mesmos recursos de configuração como código do Kubernetes e do Docker podem ser utilizados do desenvolvimento à produção, dando maior consistência em diferentes ambientes.**
 
É também geral um ficheiro com o nome `./azds.yaml` pelo comando `prep`, que é o ficheiro de configuração do Azure Dev Spaces. Este complementa os artefactos do Docker e do Kubernetes com uma configuração adicional que permite uma experiência de desenvolvimento iterativa no Azure.

## <a name="build-and-run-code-in-kubernetes"></a>Criar e executar códigos no Kubernetes
Vamos executar o nosso código! Na janela do terminal, execute este comando a partir da **pasta de código raiz**, webfrontend:

```cmd
azds up
```

Fique de olho no resultado do comando, vai reparar em várias coisas à medida que progride:
- O código fonte é sincronizado com o espaço de programação no Azure.
- É criada uma imagem de contentor no Azure, conforme especificado pelos ativos do Docker na sua pasta de códigos.
- São criados objetos do Kubernetes que utilizam a imagem do contentor, conforme especificado pelo gráfico Helm na sua pasta de códigos.
- São apresentadas as informações sobre o(s) ponto(s) final(ais) do contentor. No nosso caso, contamos com um URL HTTP público.
- Assumindo que os estágios acima sejam concluídos com sucesso, deve começar a ver o resultado `stdout` (e `stderr`), à medida que o contentor é iniciado.

> [!Note]
> Estes passos vão demorar mais tempo quando o comando `up` é executado pela primeira vez, mas as execuções seguintes deverão ser mais rápidas.

### <a name="test-the-web-app"></a>Testar a aplicação Web
Analise o resultado da consola para obter informações sobre o URL público que foi criado pelo comando `up`. Estará na forma: 

```
(pending registration) Service 'webfrontend' port 'http' will be available at <url>
Service 'webfrontend' port 80 (TCP) is available at 'http://localhost:<port>'
```

Abra este URL numa janela do browser e deve ver o carregamento da aplicação Web. À medida que o contentor é executado, os resultados `stdout` e `stderr` são transmitidos para a janela do terminal.

> [!Note]
> Na primeira execução, pode demorar alguns minutos para que o DNS público esteja pronto. Se não resolver o URL público, pode utilizar a alternativa `http://localhost:<portnumber>` URL que é apresentado na saída da consola. Se utilizar o URL de anfitrião local, poderá parecer que o contentor está a ser executado localmente, contudo, está a ser executado no AKS. Para sua comodidade e para facilitar a interação com o serviço da sua máquina local, os Espaços de Programador do Azure criam um túnel SSH temporário para o contentor em execução no Azure. Pode voltar atrás e tentar o URL público mais tarde, quando o registo DNS estiver pronto.

### <a name="update-a-content-file"></a>Atualizar um ficheiro de conteúdo
O Azure Dev Spaces não se limita apenas a pôr o código em execução no Kubernetes. Tem que ver com permitir-lhe ver, de forma rápida e iterativa, as alterações ao código serem aplicadas num ambiente do Kubernetes na cloud.

1. Localize o ficheiro `./Views/Home/Index.cshtml` e faça uma edição ao HTML. Por exemplo, altere a linha 70, que lê `<h2>Application uses</h2>` para algo como: `<h2>Hello k8s in Azure!</h2>`
1. Guarde o ficheiro. Pouco depois, na janela do terminal, verá uma mensagem que diz que um ficheiro no contentor em execução foi atualizado.
1. Aceda ao seu browser e atualize a página. Deverá ver a página Web mostrar o código HTML atualizado.

O que aconteceu? As edições aos ficheiros de conteúdos, como HTML e CSS, não requerem a recompilação numa aplicação Web .NET Core, pelo que um comando `azds up` ativo sincroniza automaticamente qualquer ficheiro de conteúdos modificado com o contentor em execução no Azure, de modo a que possa ver as edições aos conteúdos de imediato.

### <a name="update-a-code-file"></a>Atualizar um ficheiro de código
A atualização de ficheiros de código exige mais algum trabalho, porque a aplicação .NET Core tem de ser recompilada e produzir binários de aplicação atualizados.

1. Na janela de terminal, prima `Ctrl+C` (para parar `azds up`).
1. Abra o ficheiro de código com o nome `Controllers/HomeController.cs`e editar a mensagem que será apresentada a página About: `ViewData["Message"] = "Your application description page.";`
1. Guarde o ficheiro.
1. Execute `azds up` na janela de terminal. 

Este comando recria a imagem do contentor e reimplementa o gráfico Helm. Para ver as alterações ao código entrarem em vigor na aplicação em execução, aceda ao menu About (Sobre) na aplicação Web.


Mas existe um *método ainda mais rápido* para programar código, que vai explorar na próxima secção. 

## <a name="debug-a-container-in-kubernetes"></a>Depurar um contentor no Kubernetes

Nesta secção, ai utilizar o VS Code para depurar diretamente o nosso contentor em execução no Azure. Também vai aprender como obter um ciclo de edição-execução-teste mais rápido.

![](media/common/edit-refresh-see.png)

> [!Note]
> **Se ficar bloqueado** em qualquer altura, veja a secção [Resolução de problemas](troubleshooting.md) ou publique um comentário nesta página.

### <a name="initialize-debug-assets-with-the-vs-code-extension"></a>Inicializar ativos de depuração com a extensão do VS Code
Primeiro tem de configurar o seu projeto de código para que o VS Code comunique com o nosso espaço de programação no Azure. A extensão do VS Code para Espaços de Programação do Azure oferece um comando auxiliar para contribuir para a configuração da depuração. 

Abra a **Paleta de Comandos** (através do menu **Ver | Paleta de Comandos**), e utilize o preenchimento automático para escrever e selecione este comando: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`. 

Esta ação adiciona a configuração de depuração para os Espaços de Programação do Azure na pasta `.vscode`. Este comando não deve ser confundido com o comando `azds prep`, que configura o projeto para implementação.

![](media/common/command-palette.png)


### <a name="select-the-azds-debug-configuration"></a>Selecionar a configuração de depuração do AZDS
1. Para abrir a vista Debug (Depuração), clique no ícone Debug em **Activity Bar** (Barra de Atividades), no lado do VS Code.
1. Selecione **.NET Core Launch (AZDS)** (Iniciar .NET Core [AZDS]) como a configuração de depuração ativa.

![](media/get-started-netcore/debug-configuration.png)

> [!Note]
> Se não vir nenhum comando do Azure Dev Spaces em Command Palette (Paleta de Comandos), confirme que tem instalada a extensão do VS Code para o Azure Dev Spaces. Lembre-se de que a área de trabalho que abriu no VS Code é a pasta que contém azds.yaml.


### <a name="debug-the-container-in-kubernetes"></a>Depurar o contentor no Kubernetes
Prima **F5** para depurar o código no Kubernetes.

Tal como sucede com o comando `up`, o código é sincronizado com o espaço de programador e é criado e implementado um contentor no Kubernetes. Desta vez, obviamente, o depurador está ligado ao contentor remoto.

> [!Tip]
> A barra de estado do VS Code apresentará um URL clicável.

![](media/common/vscode-status-bar-url.png)

Defina um ponto de interrupção num ficheiro de código do lado do servidor, como, por exemplo, a função `Index()` no ficheiro de origem `Controllers/HomeController.cs`. Atualizar a página do browser faz com que o ponto de interrupção seja atingido.

Tem acesso total às informações da depuração, tal como aconteceria se o código estivesse a ser executado localmente, como, por exemplo, a pilha de chamadas, as variáveis locais, as informações de exceção, etc.

### <a name="edit-code-and-refresh"></a>Editar o código e atualizar
Com o depurador ativo, faça uma edição ao código. Por exemplo, modifique a mensagem da página About (Sobre), em `Controllers/HomeController.cs`. 

```csharp
public IActionResult About()
{
    ViewData["Message"] = "My custom message in the About page.";
    return View();
}
```

Guarde o ficheiro e, no **painel Debug actions** (Ações de depuração), clique no botão **Refresh** (Atualizar). 

![](media/get-started-netcore/debug-action-refresh.png)

Em vez de reconstruir e reimplementar uma imagem de contentor nova sempre que forem feitas edições ao código, o que, muitas vezes, irá demorar um tempo considerável, o Azure Dev Spaces recompilará incrementalmente o código dentro do contentor existente para proporcionar um ciclo de edição/depuração mais rápido.

Atualize a aplicação Web no browser e aceda à página About (Sobre). Deverá ver a mensagem personalizada apresentada na IU.

**Agora tem um método para iteração no código e depuração diretamente no Kubernetes rapidamente!** Em seguida, irá ver como pode criar e chamar um segundo contentor.

## <a name="next-steps"></a>Passos Seguintes

> [!div class="nextstepaction"]
> [Aprenda sobre o desenvolvimento de múltiplos serviço](multi-service-netcore.md)
