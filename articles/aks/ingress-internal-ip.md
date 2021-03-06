---
title: Criar um controlador de entrada para uma rede interna no Azure Kubernetes Service (AKS)
description: Saiba como instalar e configurar um controlador de entradas NGINX para uma rede interna, privada num cluster do Azure Kubernetes Service (AKS).
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 08/30/2018
ms.author: iainfou
ms.openlocfilehash: 56e7f9a7760fc270df40dd4524f70b5ddce57198
ms.sourcegitcommit: 8115c7fa126ce9bf3e16415f275680f4486192c1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54847446"
---
# <a name="create-an-ingress-controller-to-an-internal-virtual-network-in-azure-kubernetes-service-aks"></a>Criar um controlador de entrada para uma rede virtual interna no Azure Kubernetes Service (AKS)

Um controlador de entrada é uma parte do software que fornece o proxy inverso, encaminhamento de tráfego configurável e terminação de TLS para serviços do Kubernetes. Recursos de entrada do Kubernetes são utilizados para configurar as regras de entrada e as rotas para serviços individuais do Kubernetes. Utilizar um controlador de entrada e de regras de entrada, um único endereço IP pode servir-se para encaminhar o tráfego para vários serviços num cluster do Kubernetes.

Este artigo mostra-lhe como implementar o [controlador de entradas NGINX] [ nginx-ingress] num cluster do Azure Kubernetes Service (AKS). O controlador de entrada está configurado numa rede virtual interna, privada e o endereço IP. Sem acesso externo é permitido. Dois aplicativos, em seguida, são executados no cluster do AKS, cada um deles está acessível através do endereço IP único.

Também pode:

- [Criar um controlador de entrada básico com conectividade de rede externa][aks-ingress-basic]
- [Ativar o suplemento de encaminhamento de aplicação de HTTP][aks-http-app-routing]
- [Criar um controlador de entrada que utiliza os seus próprios certificados TLS][aks-ingress-own-tls]
- Criar um controlador de entrada que utiliza a encriptar vamos para gerar automaticamente certificados TLS [com um endereço IP público dinâmico] [ aks-ingress-tls] ou [com um endereço IP público estático][aks-ingress-static-tls]

## <a name="before-you-begin"></a>Antes de começar

Este artigo utiliza o Helm para instalar o controlador de entrada do NGINX, o Gestor de certificado e um exemplo de aplicação web. Tem de ter o Helm inicializado no seu cluster do AKS e utilizar uma conta de serviço para Tiller. Para obter mais informações sobre como configurar e utilizar o Helm, consulte [instalar aplicações com Helm no Azure Kubernetes Service (AKS)][use-helm].

Este artigo também requer a execução da versão 2.0.41 da CLI do Azure ou posterior. Executar `az --version` para localizar a versão. Se precisar de instalar ou atualizar, veja [Install Azure CLI (Instalar o Azure CLI)][azure-cli-install].

## <a name="create-an-ingress-controller"></a>Criar um controlador de entrada

Por predefinição, um controlador de entrada do NGINX é criado com uma atribuição de endereço IP pública dinâmica. Um requisito de configuração comum é utilizar uma rede interna, privada e o endereço IP. Esta abordagem permite-lhe restringir o acesso aos seus serviços para utilizadores internos, sem acesso externo.

Crie um ficheiro denominado *interno ingress.yaml* usando o arquivo de manifesto de exemplo seguinte. Este exemplo atribui *10.240.0.42* para o *loadBalancerIP* recursos. Fornece seu próprio endereço IP para utilização com o controlador de entrada. Certifique-se de que este endereço IP não já está em utilização na sua rede virtual.

```yaml
controller:
  service:
    loadBalancerIP: 10.240.0.42
    annotations:
      service.beta.kubernetes.io/azure-load-balancer-internal: "true"
```

Implementar o *nginx entrada* gráfico com Helm. Para utilizar o ficheiro de manifesto criado no passo anterior, adicione o `-f internal-ingress.yaml` parâmetro. Para maior redundância, as duas réplicas dos controladores de entrada de NGINX são implementadas com o `--set controller.replicaCount` parâmetro. Para beneficiar totalmente a execução de réplicas do controlador de entrada, certificar-se de que há mais de um nó no cluster do AKS.

> [!TIP]
> O exemplo seguinte instala o controlador de entrada no `kube-system` espaço de nomes. Pode especificar um espaço de nomes diferente para o seu próprio ambiente, se assim o desejar. Se o cluster do AKS não RBAC ativado, adicione `--set rbac.create=false` para os comandos.

```console
helm install stable/nginx-ingress \
    --namespace kube-system \
    -f internal-ingress.yaml \
    --set controller.replicaCount=2
```

Quando o serviço de Balanceador de carga do Kubernetes é criado para o controlador de entrada do NGINX, o endereço IP é atribuído, conforme mostrado no seguinte exemplo:

```
$ kubectl get service -l app=nginx-ingress --namespace kube-system

NAME                                              TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)                      AGE
alternating-coral-nginx-ingress-controller        LoadBalancer   10.0.97.109   10.240.0.42   80:31507/TCP,443:30707/TCP   1m
alternating-coral-nginx-ingress-default-backend   ClusterIP      10.0.134.66   <none>        80/TCP                       1m
```

Não existem regras de entrada foram criadas no entanto, para que a página 404 do controlador de entrada NGINX predefinida é apresentada se navegar até o endereço IP interno. Regras de entrada estão configuradas nos passos seguintes.

## <a name="run-demo-applications"></a>Executar aplicações de demonstração

Para ver o controlador de entrada em ação, vamos executar duas aplicações de demonstração no cluster do AKS. Neste exemplo, o Helm é utilizada para implementar duas instâncias de um aplicativo "Hello world" simples.

Antes de instalar os gráficos do Helm de exemplo, adicione o repositório de exemplos do Azure para o seu ambiente do Helm da seguinte forma:

```console
helm repo add azure-samples https://azure-samples.github.io/helm-charts/
```

Crie a primeira aplicação de demonstração de um gráfico Helm com o seguinte comando:

```console
helm install azure-samples/aks-helloworld
```

Agora a instalar uma segunda instância do aplicativo de demonstração. Para a segunda instância, especifique um novo título para que as duas aplicações são visualmente distintas. Também especificar um nome de serviço único:

```console
helm install azure-samples/aks-helloworld --set title="AKS Ingress Demo" --set serviceName="ingress-demo"
```

## <a name="create-an-ingress-route"></a>Criar uma rota de entrada

Ambas as aplicações estão agora em execução no seu cluster de Kubernetes. Para encaminhar o tráfego para cada aplicativo, crie um recurso de entrada do Kubernetes. O recurso de entrada configura as regras que encaminham o tráfego para uma das duas aplicações.

No exemplo a seguir, o tráfego para o endereço `http://10.240.0.42/` é encaminhado para o serviço com o nome `aks-helloworld`. O tráfego para o endereço `http://10.240.0.42/hello-world-two` é encaminhado para o `ingress-demo` serviço.

Crie um ficheiro denominado `hello-world-ingress.yaml` e copie o exemplo seguinte YAML.

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: hello-world-ingress
  annotations:
    kubernetes.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /
        backend:
          serviceName: aks-helloworld
          servicePort: 80
      - path: /hello-world-two
        backend:
          serviceName: ingress-demo
          servicePort: 80
```

Crie o recurso de entrada com o `kubectl apply -f hello-world-ingress.yaml` comando.

```
$ kubectl apply -f hello-world-ingress.yaml

ingress.extensions/hello-world-ingress created
```

## <a name="test-the-ingress-controller"></a>Testar o controlador de entrada

Para testar as rotas para o controlador de entrada, navegue para as duas aplicações com um cliente web. Se for necessário, pode testar rapidamente a esta funcionalidade apenas internos de um pod no cluster do AKS. Criar um pod de teste e anexar uma sessão de terminal a ele:

```console
kubectl run -it --rm aks-ingress-test --image=debian
```

Instale `curl` no pod com `apt-get`:

```console
apt-get update && apt-get install -y curl
```

Agora, acessar o endereço da sua utilização de controlador de entrada do Kubernetes `curl`, tal como *http://10.240.0.42*. Fornece que seu próprio endereço IP especificado ao implementar o controlador de entrada no primeiro passo deste artigo.

```console
curl -L http://10.240.0.42
```

Nenhum caminho adicional foi fornecido com o endereço, portanto, o controlador de entrada é predefinido para o */* rota. A primeira aplicação de demonstração é retornada, conforme mostrado no seguinte exemplo condensado:

```
$ curl -L 10.240.0.42

<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <link rel="stylesheet" type="text/css" href="/static/default.css">
    <title>Welcome to Azure Kubernetes Service (AKS)</title>
[...]
```

Agora, adicione */hello-world-two* caminho para o endereço, tal como *http://10.240.0.42/hello-world-two*. O segundo aplicativo de demonstração com o título personalizado for retornado, conforme mostrado no seguinte exemplo condensado:

```
$ curl -L -k http://10.240.0.42/hello-world-two

<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <link rel="stylesheet" type="text/css" href="/static/default.css">
    <title>AKS Ingress Demo</title>
[...]
```

## <a name="clean-up-resources"></a>Limpar recursos

Este artigo usou o Helm para instalar os componentes de entrada e aplicações de exemplo. Quando implementa um gráfico Helm, um número de recursos do Kubernetes é criado. Estes recursos incluem pods, implementações e serviços. Para limpar estes recursos, lista as versões do Helm com a `helm list` comando. Procure gráficos chamados *entrada de nginx* e *aks-helloworld*, conforme mostrado no seguinte exemplo:

```
$ helm list

NAME                REVISION    UPDATED                     STATUS      CHART                   APP VERSION NAMESPACE
kissing-ferret      1           Tue Oct 16 17:13:39 2018    DEPLOYED    nginx-ingress-0.22.1    0.15.0      kube-system
intended-lemur      1           Tue Oct 16 17:20:59 2018    DEPLOYED    aks-helloworld-0.1.0                default
pioneering-wombat   1           Tue Oct 16 17:21:05 2018    DEPLOYED    aks-helloworld-0.1.0                default
```

Eliminar as versões com a `helm delete` comando. O exemplo seguinte elimina a implementação de entrada do NGINX e as dois exemplos AKS Olá mundo de aplicações.

```
$ helm delete kissing-ferret intended-lemur pioneering-wombat

release "kissing-ferret" deleted
release "intended-lemur" deleted
release "pioneering-wombat" deleted
```

Em seguida, remova o repositório Helm para a aplicação hello world do AKS:

```console
helm repo remove azure-samples
```

Por fim, remova a rota de entrada que eram direcionadas para o tráfego para as aplicações de exemplo:

```console
kubectl delete -f hello-world-ingress.yaml
```

## <a name="next-steps"></a>Passos Seguintes

Este artigo inclui alguns componentes externos ao AKS. Para saber mais sobre estes componentes, consulte as seguintes páginas do projeto:

- [Helm CLI][helm-cli]
- [Controlador de entradas do NGINX][nginx-ingress]

Também pode:

- [Criar um controlador de entrada básico com conectividade de rede externa][aks-ingress-basic]
- [Ativar o suplemento de encaminhamento de aplicação de HTTP][aks-http-app-routing]
- [Criar um controlador de entrada com um IP público dinâmico e configurar a encriptar vamos para gerar automaticamente certificados TLS][aks-ingress-tls]
- [Criar um controlador de entrada com um endereço IP público estático e configurar a encriptar vamos para gerar automaticamente certificados TLS][aks-ingress-static-tls]

<!-- LINKS - external -->
[helm-cli]: https://docs.microsoft.com/azure/aks/kubernetes-helm
[nginx-ingress]: https://github.com/kubernetes/ingress-nginx

<!-- LINKS - internal -->
[use-helm]: kubernetes-helm.md
[azure-cli-install]: /cli/azure/install-azure-cli
[aks-ingress-basic]: ingress-basic.md
[aks-ingress-tls]: ingress-tls.md
[aks-ingress-static-tls]: ingress-static-ip.md
[aks-http-app-routing]: http-application-routing.md
[aks-ingress-own-tls]: ingress-own-tls.md
