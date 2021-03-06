---
title: Como e onde implementar modelos
titleSuffix: Azure Machine Learning service
description: 'Saiba como e onde implementar os seus modelos de serviço do Azure Machine Learning, incluindo: Matrizes de porta do Container Instances, serviço Kubernetes do Azure, Azure IoT Edge e campos programáveis do Azure.'
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: conceptual
ms.author: aashishb
author: aashishb
ms.reviewer: larryfr
ms.date: 04/02/2019
ms.custom: seoapril2019
ms.openlocfilehash: a6ef53d56fa293791658b37b16cbaff94aee6ef3
ms.sourcegitcommit: 62d3a040280e83946d1a9548f352da83ef852085
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59280898"
---
# <a name="deploy-models-with-the-azure-machine-learning-service"></a>Implementar modelos com o serviço Azure Machine Learning

Neste documento, saiba como implementar o seu modelo como um serviço web na cloud do Azure ou para dispositivos do IoT Edge. 

## <a name="compute-targets-for-deployment"></a>Destinos de computação para a implementação

Utilize o SDK do Azure Machine Learning para implementar o modelo preparado nas seguintes localizações:

| Destino de computação | Tipo de implementação | Descrição |
| ----- | ----- | ----- |
| [Serviço de Kubernetes do Azure (AKS)](#aks) | Inferência de tipos em tempo real | Ideal para implementações de produção de grande escala. Fornece o dimensionamento automático e tempos de resposta rápidos. |
| [Azure computação do Machine Learning (amlcompute)](#azuremlcompute) | Inferência de tipos do batch | Execute a predição de batch de computação sem servidor. Suporta VMs normais e de baixa prioridade. |
| [Azure Container Instances (ACI)](#aci) | Testes | Bom para desenvolvimento ou teste. **Não é adequado para cargas de trabalho de produção.** |
| [Azure IoT Edge](#iotedge) | (Pré-visualização) Módulo de IoT | Implemente modelos em dispositivos IoT. Inferência acontece no dispositivo. |
| [Matriz de porta de campos programáveis (FPGA)](#fpga) | (Pré-visualização) Serviço Web | Latência ultrabaixa para inferência em tempo real. |

## <a name="deployment-workflow"></a>Fluxo de trabalho de implantação

O processo de implantação de um modelo é semelhante para todos os destinos de computação:

1. Dar formação e registar um modelo.
1. Configurar e registar uma imagem que utiliza o modelo.
1. Implantar a imagem num destino de computação.
1. Testar a implementação

O vídeo seguinte demonstra a implementar no Azure Container Instances:

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2Kwk3]


Para obter mais informações sobre os conceitos envolvidos no fluxo de trabalho de implantação, consulte [gerir, implementar e monitorizar os modelos de serviço do Azure Machine Learning](concept-model-management-and-deployment.md).

## <a name="prerequisites-for-deployment"></a>Pré-requisitos para implementação

[!INCLUDE [aml-prereq](../../../includes/aml-prereq.md)]

- Um modelo preparado. Se não tiver um modelo preparado, utilize os passos no [formar modelos](tutorial-train-models-with-aml.md) tutorial para treinar e registar um com o serviço Azure Machine Learning.

    > [!NOTE]
    > Embora o serviço Azure Machine Learning pode funcionar com qualquer modelo genérico que pode ser carregado no Python 3, os exemplos neste documento demonstram o uso de um modelo armazenado no formato de pickle do Python.
    >
    > Para obter mais informações sobre como utilizar modelos ONNX, consulte a [ONNX e o Azure Machine Learning](how-to-build-deploy-onnx.md) documento.

## <a id="registermodel"></a> Registe-se de um modelo preparado

O registro de modelo é uma forma de armazenar e organizar seus modelos ensinados na cloud do Azure. Modelos são registrados na sua área de trabalho do serviço do Azure Machine Learning. O modelo pode ser treinado com o Azure Machine Learning ou outro serviço. O código a seguir demonstra como registar um modelo de ficheiro, defina um nome e uma descrição etiquetas:

```python
from azureml.core.model import Model

model = Model.register(model_path = "outputs/sklearn_mnist_model.pkl",
                       model_name = "sklearn_mnist",
                       tags = {"key": "0.1"},
                       description = "test",
                       workspace = ws)
```

**Estimativa de tempo**: Aproximadamente 10 segundos.

Para obter um exemplo de um modelo de registo, consulte [treinar um classificador de imagem](tutorial-train-models-with-aml.md).

Para obter mais informações, consulte a documentação de referência para o [classe de modelo](https://docs.microsoft.com/python/api/azureml-core/azureml.core.model.model?view=azure-ml-py).

## <a id="configureimage"></a> Criar e registrar uma imagem

Modelos implementados são empacotados como uma imagem. A imagem contém as dependências necessárias para executar o modelo.

Para **instância de contentor do Azure**, **Azure Kubernetes Service**, e **Azure IoT Edge** implementações, a [azureml.core.image.ContainerImage](https://docs.microsoft.com/python/api/azureml-core/azureml.core.image.containerimage?view=azure-ml-py) classe é utilizada para criar uma configuração de imagem. A configuração de imagem, em seguida, é utilizada para criar uma nova imagem do Docker.

Ao criar a configuração de imagem, pode utilizar um __imagem predefinida__ fornecido pelo serviço Azure Machine Learning ou uma __imagem personalizada__ fornecidas por si.

O código a seguir demonstra como criar uma nova configuração de imagem:

```python
from azureml.core.image import ContainerImage

# Image configuration
image_config = ContainerImage.image_configuration(execution_script = "score.py",
                                                 runtime = "python",
                                                 conda_file = "myenv.yml"}
                                                 )
```

**Estimativa de tempo**: Aproximadamente 10 segundos.

Os parâmetros importantes neste exemplo descrito na tabela a seguir:

| Parâmetro | Descrição |
| ----- | ----- |
| `execution_script` | Especifica um script de Python que é utilizado para receber pedidos submetidos para o serviço. Neste exemplo, o script está contido no `score.py` ficheiro. Para obter mais informações, consulte a [script de execução](#script) secção. |
| `runtime` | Indica que a imagem utiliza o Python. A outra opção é `spark-py`, que utiliza o Python com o Apache Spark. |
| `conda_file` | Utilizado para fornecer um ficheiro de ambiente de conda. Esse arquivo define o ambiente de conda para o modelo implementado. Para obter mais informações sobre como criar este ficheiro, consulte [criar um ficheiro de ambiente (myenv.yml)](tutorial-deploy-models-with-aml.md#create-environment-file). |

Para obter um exemplo de criação de uma configuração de imagem, veja [implementar um classificador de imagem](tutorial-deploy-models-with-aml.md).

Para obter mais informações, consulte a documentação de referência para [ContainerImage classe](https://docs.microsoft.com/python/api/azureml-core/azureml.core.image.containerimage?view=azure-ml-py)

### <a id="customimage"></a> Utilizar uma imagem personalizada

Quando utilizar uma imagem personalizada, a imagem tem de cumprir os seguintes requisitos:

* Ubuntu 16.04 ou superior.
* Conda 4.5. # ou superior.
* Python 3.5. # ou 3.6. #.

Para utilizar uma imagem personalizada, defina o `base_image` propriedade da configuração da imagem para o endereço da imagem. O exemplo seguinte demonstra como utilizar uma imagem do tanto um público e privado Azure Container Registry:

```python
# use an image available in public Container Registry without authentication
image_config.base_image = "mcr.microsoft.com/azureml/o16n-sample-user-base/ubuntu-miniconda"

# or, use an image available in a private Container Registry
image_config.base_image = "myregistry.azurecr.io/mycustomimage:1.0"
image_config.base_image_registry.address = "myregistry.azurecr.io"
image_config.base_image_registry.username = "username"
image_config.base_image_registry.password = "password"
```

Para obter mais informações sobre o carregamento de imagens para o Azure Container Registry, veja [enviar a sua primeira imagem para um registo de contentor do Docker privado](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-docker-cli).

Se é preparado o modelo na computação do Azure Machine Learning, utilizando __versão 1.0.22 ou superior__ do SDK do Azure Machine Learning, uma imagem é criada durante o treinamento. O exemplo seguinte demonstra como utilizar esta imagem:

```python
# Use an image built during training with SDK 1.0.22 or greater
image_config.base_image = run.properties["AzureML.DerivedImageName"]
```

### <a id="script"></a> Script de execução

O script de execução recebe dados enviados para uma imagem implementada e passa-o para o modelo. Em seguida, usa a resposta devolvida pelo modelo e retorna que para o cliente. **O script é específico ao seu modelo**; tem de compreender os dados que o modelo de espera e retorna. Para um script de exemplo que funciona com um modelo de classificação de imagens, consulte [implementar um classificador de imagem](tutorial-deploy-models-with-aml.md).

O script contém duas funções que carregar e executam o modelo:

* `init()`: Normalmente, esta função carrega o modelo de um objeto global. Esta função só é executada uma vez, quando o contentor do Docker é iniciado.

* `run(input_data)`: Essa função usa o modelo para prever um valor com base nos dados de entrada. Entradas e saídas para a execução normalmente usam JSON para a serialização e desserialização. Também pode trabalhar com dados binários não processados. Pode transformar os dados antes de enviar para o modelo ou antes de o devolver ao cliente.

#### <a name="working-with-json-data"></a>Trabalhar com dados JSON

O seguinte script de exemplo aceita e devolve dados JSON. O `run` função transforma os dados JSON num formato que o modelo de espera e, em seguida, transforma a resposta para JSON antes de o devolver:

```python
%%writefile score.py
import json
import numpy as np
import os
import pickle
from sklearn.externals import joblib
from sklearn.linear_model import LogisticRegression
from azureml.core.model import Model

# load the model
def init():
    global model
    # retrieve the path to the model file using the model name
    model_path = Model.get_model_path('sklearn_mnist')
    model = joblib.load(model_path)

# Passes data to the model and returns the prediction
def run(raw_data):
    data = np.array(json.loads(raw_data)['data'])
    # make prediction
    y_hat = model.predict(data)
    return json.dumps(y_hat.tolist())
```

#### <a name="working-with-binary-data"></a>Trabalhar com dados binários

Se o seu modelo aceita __dados binários__, utilize `AMLRequest`, `AMLResponse`, e `rawhttp`. O seguinte script de exemplo aceita dados binários e devolve os bytes revertidos em solicitações POST. Para solicitações GET, ele retorna o URL completo no corpo da resposta:

```python
from azureml.contrib.services.aml_request  import AMLRequest, rawhttp
from azureml.contrib.services.aml_response import AMLResponse

def init():
    print("This is init()")

# Accept and return binary data
@rawhttp
def run(request):
    print("This is run()")
    print("Request: [{0}]".format(request))
    # handle GET requests
    if request.method == 'GET':
        respBody = str.encode(request.full_path)
        return AMLResponse(respBody, 200)
    # handle POST requests
    elif request.method == 'POST':
        reqBody = request.get_data(False)
        respBody = bytearray(reqBody)
        respBody.reverse()
        respBody = bytes(respBody)
        return AMLResponse(respBody, 200)
    else:
        return AMLResponse("bad request", 500)
```

> [!IMPORTANT]
> O `azureml.contrib` espaço de nomes são alterados com frequência, pois estamos a trabalhar para melhorar o serviço. Como tal, qualquer coisa neste espaço de nomes deve ser considerada como uma pré-visualização e não totalmente suportada pela Microsoft.
>
> Se precisar de teste em seu ambiente de desenvolvimento local, pode instalar os componentes no `contrib` espaço de nomes utilizando o seguinte comando:
> ```shell
> pip install azureml-contrib-services
> ```

### <a id="createimage"></a> Registre-se a imagem

Depois de criar a configuração de imagem, pode usá-lo para se registar uma imagem. Esta imagem é armazenada no registo de contentor para a área de trabalho. Depois de criado, pode implementar a mesma imagem em vários serviços.

```python
# Register the image from the image configuration
image = ContainerImage.create(name = "myimage",
                              models = [model], #this is the model object
                              image_config = image_config,
                              workspace = ws
                              )
```

**Estimativa de tempo**: Aproximadamente 3 minutos.

As imagens são automaticamente com a versão ao registar várias imagens com o mesmo nome. Por exemplo, a primeira imagem registado como `myimage` é atribuído um ID de `myimage:1`. Da próxima vez que Registre-se uma imagem como `myimage`, o ID da nova imagem é `myimage:2`.

Para obter mais informações, consulte a documentação de referência [ContainerImage classe](https://docs.microsoft.com/python/api/azureml-core/azureml.core.image.containerimage?view=azure-ml-py).

## <a id="deploy"></a> Implementar como um serviço web

Quando chegar à implementação, o processo é ligeiramente diferente consoante o destino de computação que implementar. Utilize as informações nas secções seguintes para aprender a implementar em:

| Destino de computação | Tipo de implementação | Descrição |
| ----- | ----- | ----- |
| [Serviço de Kubernetes do Azure (AKS)](#aks) | Serviço Web (inferência de tipos em tempo real)| Ideal para implementações de produção de grande escala. Fornece o dimensionamento automático e tempos de resposta rápidos. |
| [Computação do Azure ML](#azuremlcompute) | Serviço Web (inferência de tipos do Batch)| Execute a predição de batch de computação sem servidor. Suporta VMs normais e de baixa prioridade. |
| [Azure Container Instances (ACI)](#aci) | Serviço Web (Dev/test)| Bom para desenvolvimento ou teste. **Não é adequado para cargas de trabalho de produção.** |
| [Azure IoT Edge](#iotedge) | (Pré-visualização) Módulo de IoT | Implemente modelos em dispositivos IoT. Inferência acontece no dispositivo. |
| [Matriz de porta de campos programáveis (FPGA)](#fpga) | (Pré-visualização) Serviço Web | Latência ultrabaixa para inferência em tempo real. |

> [!IMPORTANT]
> Recursos de várias origens (CORS) de partilha não é atualmente suportado quando implementar um modelo como um serviço web.

Os exemplos nesta secção utilizam [deploy_from_image](https://docs.microsoft.com/en-us/python/api/azureml-core/azureml.core.webservice(class)?view=azure-ml-py#deploy-from-model-workspace--name--models--image-config--deployment-config-none--deployment-target-none-), que requer que se Registre o modelo e a imagem antes de fazer uma implantação. Para obter mais informações sobre outros métodos de implantação, consulte [implementar](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice(class)?view=azure-ml-py#deploy-workspace--name--model-paths--image-config--deployment-config-none--deployment-target-none-) e [deploy_from_model](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice(class)?view=azure-ml-py#deploy-from-model-workspace--name--models--image-config--deployment-config-none--deployment-target-none-).

### <a id="aci"></a> Implementar no Azure Container Instances (Dev/Test)

Utilização do Azure Container Instances para implementar os seus modelos como um serviço da web se um ou mais das seguintes condições for verdadeiro:

- Precisa implementar e validar o seu modelo rapidamente. Conclusão da implementação do ACI em menos de 5 minutos.
- Está a testar um modelo que está em desenvolvimento. Para ver a disponibilidade de região e quota para o ACI, consulte a [Quotas e disponibilidade das regiões do Azure Container Instances](https://docs.microsoft.com/azure/container-instances/container-instances-quotas) documento.

Para implementar no Azure Container Instances, utilize os seguintes passos:

1. Defina a configuração de implementação. Esta configuração depende dos requisitos do seu modelo. O exemplo seguinte define uma configuração que utiliza um núcleo de CPU e 1 GB de memória:

    [!code-python[](~/aml-sdk-samples/ignore/doc-qa/how-to-deploy-to-aci/how-to-deploy-to-aci.py?name=configAci)]

2. Para implementar a imagem criada no [criar a imagem](#createimage) secção deste documento, utilize o seguinte código:

    [!code-python[](~/aml-sdk-samples/ignore/doc-qa/how-to-deploy-to-aci/how-to-deploy-to-aci.py?name=option3Deploy)]

    **Estimativa de tempo**: Cerca de cinco minutos.

Para obter mais informações, consulte a documentação de referência para o [AciWebservice](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice.aciwebservice?view=azure-ml-py) e [Webservice](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice.webservice?view=azure-ml-py) classes.

### <a id="aks"></a> Implementar no serviço Kubernetes do Azure (produção)

Para implementar o seu modelo como um serviço da web de produção de grande escala, utilize o Azure Kubernetes Service (AKS). Pode utilizar um cluster do AKS existente ou crie um novo com o SDK do Azure Machine Learning, a CLI ou o portal do Azure.

Criar um cluster do AKS é um processo de tempo para a área de trabalho. Pode reutilizar este cluster para várias implementações.

> [!IMPORTANT]
> Se eliminar o cluster, em seguida, tem de criar um novo cluster da próxima vez que precisa implantar.

Serviço Kubernetes do Azure fornece as seguintes capacidades:

* Dimensionamento automático
* Registo
* Recolha de dados do modelo
* Tempos de resposta rápidos para os seus serviços web
* Terminação de TLS
* Authentication

#### <a name="autoscaling"></a>Dimensionamento automático

Dimensionamento automático pode ser controlado através da definição `autoscale_target_utilization`, `autoscale_min_replicas`, e `autoscale_max_replicas` para o AKS de serviço web. O exemplo seguinte demonstra como ativar o dimensionamento automático:

```python
aks_config = AksWebservice.deploy_configuration(autoscale_enabled=True,
                                                autoscale_target_utilization=30,
                                                autoscale_min_replicas=1,
                                                autoscale_max_replicas=4)
```

Decisões para aumentar/reduzir verticalmente baseia-se fora de utilização de réplicas de contentor atual. O número de réplicas que estejam lotadas (um pedido de processamento) dividido pelo total número de réplicas atuais é a utilização atual. Se este número excede a utilização de destino, em seguida, são criadas mais réplicas. Se ela for menor, em seguida, as réplicas são reduzidas. Por predefinição, a utilização de destino é de 70%.

Decisões para adicionar réplicas são feitas e rapidamente implementadas (cerca de 1 segundo). Decisões para remover as réplicas demoram mais tempo (cerca de 1 minuto). Este comportamento mantém réplicas Inativas em torno durante um minuto, no caso de chegarem novos pedidos que pode processar.

Pode calcular as réplicas necessárias, utilizando o seguinte código:

```python
from math import ceil
# target requests per second
targetRps = 20
# time to process the request (in seconds)
reqTime = 10
# Maximum requests per container
maxReqPerContainer = 1
# target_utilization. 70% in this example
targetUtilization = .7

concurrentRequests = targetRps * reqTime / targetUtilization

# Number of container replicas
replicas = ceil(concurrentRequests / maxReqPerContainer)
```

Para obter mais informações sobre a definição `autoscale_target_utilization`, `autoscale_max_replicas`, e `autoscale_min_replicas`, consulte o [AksWebservice.deploy_configuration](https://docs.microsoft.com/en-us/python/api/azureml-core/azureml.core.webservice.akswebservice?view=azure-ml-py#deploy-configuration-autoscale-enabled-none--autoscale-min-replicas-none--autoscale-max-replicas-none--autoscale-refresh-seconds-none--autoscale-target-utilization-none--collect-model-data-none--auth-enabled-none--cpu-cores-none--memory-gb-none--enable-app-insights-none--scoring-timeout-ms-none--replica-max-concurrent-requests-none--max-request-wait-time-none--num-replicas-none--primary-key-none--secondary-key-none--tags-none--properties-none--description-none-) referência.

#### <a name="create-a-new-cluster"></a>Criar um novo cluster

Para criar um novo cluster do serviço Kubernetes do Azure, utilize o seguinte código:

> [!IMPORTANT]
> Criar o cluster do AKS é um processo de tempo para a área de trabalho. Depois de criado, pode reutilizar este cluster para várias implementações. Se eliminar o cluster ou o grupo de recursos que o contém, em seguida, tem de criar um novo cluster da próxima vez que precisa implantar.
> Para [ `provisioning_configuration()` ](https://docs.microsoft.com/python/api/azureml-core/azureml.core.compute.akscompute?view=azure-ml-py), se escolher valores personalizados para agent_count e vm_size, tem de certificar-se de que agent_count multiplicado por vm_size é maior que ou igual a 12 CPUs virtuais. Por exemplo, se usar um vm_size de "Standard_D3_v2", que tem 4 CPUs virtuais, em seguida, deve escolher um agent_count 3 ou superior.

```python
from azureml.core.compute import AksCompute, ComputeTarget

# Use the default configuration (you can also provide parameters to customize this)
prov_config = AksCompute.provisioning_configuration()

aks_name = 'aml-aks-1'
# Create the cluster
aks_target = ComputeTarget.create(workspace = ws,
                                    name = aks_name,
                                    provisioning_configuration = prov_config)

# Wait for the create process to complete
aks_target.wait_for_completion(show_output = True)
print(aks_target.provisioning_state)
print(aks_target.provisioning_errors)
```

**Estimativa de tempo**: Cerca de 20 minutos.

#### <a name="use-an-existing-cluster"></a>Utilizar um cluster existente

Se já tiver um cluster do AKS na sua subscrição do Azure e é a versão 1.12. # # e tem, pelo menos, 12 CPUs virtuais, pode usá-lo para implementar a imagem. O código a seguir demonstra como anexar um 1.12 existente do AKS. # # cluster para a área de trabalho:

```python
from azureml.core.compute import AksCompute, ComputeTarget
# Set the resource group that contains the AKS cluster and the cluster name
resource_group = 'myresourcegroup'
cluster_name = 'mycluster'

# Attach the cluster to your workgroup
attach_config = AksCompute.attach_configuration(resource_group = resource_group,
                                         cluster_name = cluster_name)
aks_target = ComputeTarget.attach(ws, 'mycompute', attach_config)

# Wait for the operation to complete
aks_target.wait_for_completion(True)
```

**Estimativa de tempo**: Aproximadamente 3 minutos.

Para obter mais informações sobre como criar um cluster do AKS fora do SDK do Azure Machine Learning, consulte os artigos seguintes:

* [Criar um cluster do AKS (Create an AKS cluster)](https://docs.microsoft.com/cli/azure/aks?toc=%2Fen-us%2Fazure%2Faks%2FTOC.json&bc=%2Fen-us%2Fazure%2Fbread%2Ftoc.json&view=azure-cli-latest#az-aks-create)
* [Criar um cluster do AKS (portal)](https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal?view=azure-cli-latest)

#### <a name="deploy-the-image"></a>Implementar a imagem

Para implementar a imagem criada no [criar a imagem](#createimage) secção deste documento para o cluster de servidor de Kubernetes do Azure, utilize o seguinte código:

```python
from azureml.core.webservice import Webservice, AksWebservice

# Set configuration and service name
aks_config = AksWebservice.deploy_configuration()
aks_service_name ='aks-service-1'
# Deploy from image
service = Webservice.deploy_from_image(workspace = ws,
                                            name = aks_service_name,
                                            image = image,
                                            deployment_config = aks_config,
                                            deployment_target = aks_target)
# Wait for the deployment to complete
service.wait_for_deployment(show_output = True)
print(service.state)
```

**Estimativa de tempo**: Aproximadamente 3 minutos.

Para obter mais informações, consulte a documentação de referência para o [AksWebservice](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice.akswebservice?view=azure-ml-py) e [Webservice](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice.webservice.webservice?view=azure-ml-py) classes.

### <a id="azuremlcompute"></a> Inferência de tipos com a computação do Azure ML

Destinos de computação do Azure ML são criados e geridos pelo serviço Azure Machine Learning. Eles podem ser usados para predição de batch de Pipelines do Azure ML.

Para obter instruções de inferência de tipos do batch com a computação do Azure ML, leia os [como executar o Batch previsões](how-to-run-batch-predictions.md) documento.


### <a id="fpga"></a> Implementar a matrizes de porta de campos programáveis (FPGA)

Project Brainwave torna possível alcançar a latência ultrabaixa para pedidos de inferência em tempo real. Project Brainwave acelera redes neurais profundas (DNN) implementadas nas matrizes de porta de campos programáveis na cloud do Azure. Normalmente utilizado o DNNs estão disponíveis como featurizers para aprendizagem de transferência ou personalizável com pesos preparado a partir de seus próprios dados.

Para obter instruções de implantação de um modelo com o Project Brainwave, consulte a [implementar para um FPGA](how-to-deploy-fpga-web-service.md) documento.

## <a name="define-schema"></a>Definir esquema

Decoradores personalizados podem ser utilizados para [OpenAPI](https://swagger.io/docs/specification/about/) entrada e de geração de especificação escreva manipulação quando implementar o serviço web. Na `score.py` arquivo, é fornecer um exemplo da entrada e/ou saída no construtor para um dos objetos de tipo definido, e o tipo e o exemplo são utilizados para criar automaticamente o esquema. Atualmente são suportados os seguintes tipos:

* `pandas`
* `numpy`
* `pyspark`
* standard Python

Certifique-se primeiro as dependências necessárias para o `inference-schema` pacote estão incluídos no seu `env.yml` conda ficheiro de ambiente. Este exemplo utiliza a `numpy` parâmetro escreva para o esquema, por isso, o pip extra `[numpy-support]` também é instalado.

```python
%%writefile myenv.yml
name: project_environment
dependencies:
  - python=3.6.2
  - pip:
    - azureml-defaults
    - scikit-learn
    - inference-schema[numpy-support]
```

Em seguida, modifique o `score.py` ficheiro a importar o `inference-schema` pacotes. Definir a entrada e saída de formatos de exemplo no `input_sample` e `output_sample` variáveis, que representam os formatos de solicitação e resposta para o serviço web. Utilize estes exemplos na entrada e saída decoradores de função no `run()` função.

```python
%%writefile score.py
import json
import numpy as np
import os
import pickle
from sklearn.externals import joblib
from sklearn.linear_model import LogisticRegression
from azureml.core.model import Model

from inference_schema.schema_decorators import input_schema, output_schema
from inference_schema.parameter_types.numpy_parameter_type import NumpyParameterType


def init():
    global model
    model_path = Model.get_model_path('sklearn_mnist')
    model = joblib.load(model_path)


input_sample = np.array([[1.8]])
output_sample = np.array([43638.88])

@input_schema('data', NumpyParameterType(input_sample))
@output_schema(NumpyParameterType(output_sample))
def run(raw_data):
    data = np.array(json.loads(raw_data)['data'])
    y_hat = model.predict(data)
    return json.dumps(y_hat.tolist())
```

Depois de seguir a imagem normal web e de registo de serviço processo de implantação com a atualização `score.py` de ficheiros, obter o uri de Swagger do serviço. Pedir este uri irá devolver o `swagger.json` ficheiro.

```python
service.wait_for_deployment(show_output=True)
print(service.swagger_uri)
```



Quando cria uma nova imagem, tem de atualizar manualmente cada serviço que pretende utilizar a nova imagem. Para atualizar o serviço web, utilize o `update` método. O código a seguir demonstra como atualizar o serviço web para utilizar uma nova imagem:

```python
from azureml.core.webservice import Webservice
from azureml.core.image import Image

service_name = 'aci-mnist-3'
# Retrieve existing service
service = Webservice(name = service_name, workspace = ws)

# point to a different image
new_image = Image(workspace = ws, id="myimage2:1")

# Update the image used by the service
service.update(image = new_image)
print(service.state)
```

Para obter mais informações, consulte a documentação de referência para o [Webservice](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice(class)?view=azure-ml-py) classe.

## <a name="test-web-service-deployments"></a>Implementações de serviços web de teste

Para testar uma implementação do serviço web, pode usar o `run` método do objeto de serviço Web. No exemplo a seguir, um documento JSON está definido como um serviço da web e o resultado é exibido. Os dados enviados tem de corresponder ao que o modelo de espera. Neste exemplo, o formato de dados corresponde a entrada esperada pelo modelo diabetes.

```python
import json

test_sample = json.dumps({'data': [
    [1,2,3,4,5,6,7,8,9,10],
    [10,9,8,7,6,5,4,3,2,1]
]})
test_sample = bytes(test_sample,encoding = 'utf8')

prediction = service.run(input_data = test_sample)
print(prediction)
```

O serviço Web é uma API REST, para que possa criar aplicações cliente numa variedade de linguagens de programação. Para obter mais informações, consulte [criar cliente aplicações para consumir webservices](how-to-consume-web-service.md).

## <a id="update"></a> Atualizar o serviço web

Quando cria uma nova imagem, tem de atualizar manualmente cada serviço que pretende utilizar a nova imagem. Para atualizar o serviço web, utilize o `update` método. O código a seguir demonstra como atualizar o serviço web para utilizar uma nova imagem:

```python
from azureml.core.webservice import Webservice
from azureml.core.image import Image

service_name = 'aci-mnist-3'
# Retrieve existing service
service = Webservice(name = service_name, workspace = ws)

# point to a different image
new_image = Image(workspace = ws, id="myimage2:1")

# Update the image used by the service
service.update(image = new_image)
print(service.state)
```

Para obter mais informações, consulte a documentação de referência para o [Webservice](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice(class)?view=azure-ml-py) classe.

## <a id="iotedge"></a> Implementar o Azure IoT Edge

Um dispositivo Azure IoT Edge é um Linux ou um dispositivo baseado em Windows que executa o tempo de execução do Azure IoT Edge. Utilizar o IoT Hub do Azure, pode implementar modelos de aprendizagem automática para estes dispositivos como módulos do IoT Edge. Implementar um modelo para um dispositivo IoT Edge permite ao dispositivo utilizar o modelo diretamente, em vez de precisar enviar dados para a cloud para processamento. Obtém os tempos de resposta mais rápidos e menos transferência de dados.

Módulos do IoT Edge do Azure são implementados para o seu dispositivo a partir de um registo de contentor. Quando cria uma imagem do seu modelo, são armazenado no registo de contentor para a área de trabalho.

> [!IMPORTANT]
> As informações nesta secção assume que já está familiarizado com os módulos do IoT Hub do Azure e Azure IoT Edge. Embora algumas das informações nesta secção é específico do serviço Azure Machine Learning, ocorre a maior parte do processo de implantar num dispositivo do edge no serviço do Azure IoT.
>
> Se não estiver familiarizado com o Azure IoT, veja [Noções básicas do IoT do Azure](https://docs.microsoft.com/azure/iot-fundamentals/) e [Azure IoT Edge](https://docs.microsoft.com/azure/iot-edge/) para obter informações básicas. Em seguida, utilize as outras ligações nesta secção para saber mais sobre operações específicas.

### <a name="set-up-your-environment"></a>Configurar o ambiente

* Um ambiente de desenvolvimento. Para obter mais informações, consulte a [como configurar um ambiente de desenvolvimento](how-to-configure-environment.md) documento.

* Uma [IoT Hub do Azure](../../iot-hub/iot-hub-create-through-portal.md) na sua subscrição do Azure.

* Um modelo preparado. Para obter um exemplo de como preparar um modelo, consulte a [preparar um modelo de classificação de imagem com o Azure Machine Learning](tutorial-train-models-with-aml.md) documento. Um modelo com formação prévia está disponível na [ferramentas de ia para o repositório do GitHub do Azure IoT Edge](https://github.com/Azure/ai-toolkit-iot-edge/tree/master/IoT%20Edge%20anomaly%20detection%20tutorial).

### <a id="getcontainer"></a> Obter as credenciais do registo de contentor

Para implementar um módulo do IoT Edge para o seu dispositivo, o IoT do Azure tem as credenciais para que o serviço Azure Machine Learning armazena imagens do docker no registo de contentor.

Pode obter as credenciais de duas formas:

+ **No portal do Azure**:

  1. Inicie sessão no [portal do Azure](https://portal.azure.com/signin/index).

  1. Aceda à sua área de trabalho do serviço do Azure Machine Learning e selecione __descrição geral__. Para ir para as definições de registo de contentor, selecione o __Registro__ ligação.

     ![Uma imagem da entrada de registo de contentor](./media/how-to-deploy-and-where/findregisteredcontainer.png)

  1. Uma vez no registo de contentor, selecione **chaves de acesso** e, em seguida, ative o utilizador de administrador.

     ![Uma imagem do ecrã de chaves de acesso](./media/how-to-deploy-and-where/findaccesskey.png)

  1. Guarde os valores para **servidor de início de sessão**, **nome de utilizador**, e **palavra-passe**.

+ **Com um script de Python**:

  1. Utilize o seguinte script de Python depois do código que executou acima para criar um contentor:

     ```python
     # Getting your container details
     container_reg = ws.get_details()["containerRegistry"]
     reg_name=container_reg.split("/")[-1]
     container_url = "\"" + image.image_location + "\","
     subscription_id = ws.subscription_id
     from azure.mgmt.containerregistry import ContainerRegistryManagementClient
     from azure.mgmt import containerregistry
     client = ContainerRegistryManagementClient(ws._auth,subscription_id)
     result= client.registries.list_credentials(resource_group_name, reg_name, custom_headers=None, raw=False)
     username = result.username
     password = result.passwords[0].value
     print('ContainerURL{}'.format(image.image_location))
     print('Servername: {}'.format(reg_name))
     print('Username: {}'.format(username))
     print('Password: {}'.format(password))
     ```
  1. Guarde os valores para os objetos ContainerURL, servername, nome de utilizador e palavra-passe.

     Estas credenciais são necessárias para fornecer o IoT Edge acesso de dispositivo a imagens no seu registo de contentor privado.

### <a name="prepare-the-iot-device"></a>Preparar o dispositivo de IoT

Registar o seu dispositivo hub IoT do Azure e, em seguida, instale o runtime do IoT Edge no dispositivo. Se não estiver familiarizado com esse processo, consulte o artigo [início rápido: Implementar o seu primeiro módulo do IoT Edge num dispositivo de Linux x64](../../iot-edge/quickstart-linux.md).

Outros métodos de registo de um dispositivo são:

* [Portal do Azure](https://docs.microsoft.com/azure/iot-edge/how-to-register-device-portal)
* [CLI do Azure](https://docs.microsoft.com/azure/iot-edge/how-to-register-device-cli)
* [Visual Studio Code](https://docs.microsoft.com/azure/iot-edge/how-to-register-device-vscode)

### <a name="deploy-the-model-to-the-device"></a>Implementar o modelo para o dispositivo

Para implementar o modelo para o dispositivo, utilize as informações de registo coletadas a [obter as credenciais do registo de contentor](#getcontainer) seção com a implementação do módulo de passos para módulos do IoT Edge. Por exemplo, quando [módulos de implementar o Azure IoT Edge do portal do Azure](../../iot-edge/how-to-deploy-modules-portal.md), tem de configurar o __definições de registo__ para o dispositivo. Utilize o __servidor de início de sessão__, __nome de utilizador__, e __palavra-passe__ para o seu registo de contentor de área de trabalho.

Também pode implementar utilizando [CLI do Azure](https://docs.microsoft.com/azure/iot-edge/how-to-deploy-modules-cli) e [Visual Studio Code](https://docs.microsoft.com/azure/iot-edge/how-to-deploy-modules-vscode).

## <a name="clean-up"></a>Limpeza

Para eliminar um serviço web implementado, utilize `service.delete()`.

Para eliminar uma imagem, utilize `image.delete()`.

Para eliminar um modelo registado, utilize `model.delete()`.

Para obter mais informações, consulte a documentação de referência [WebService.delete()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.webservice(class)?view=azure-ml-py#delete--), [Image.delete()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.image.image(class)?view=azure-ml-py#delete--), e [Model.delete()](https://docs.microsoft.com/python/api/azureml-core/azureml.core.model.model?view=azure-ml-py#delete--).

## <a name="next-steps"></a>Passos Seguintes

* [Resolução de problemas de implementação](how-to-troubleshoot-deployment.md)
* [Proteger serviços da web do Azure Machine Learning com SSL](how-to-secure-web-service.md)
* [Consumir um modelo de ML implementado como um serviço web](how-to-consume-web-service.md)
* [Como executar previsões de batch](how-to-run-batch-predictions.md)
* [Monitorizar os seus modelos do Azure Machine Learning com o Application Insights](how-to-enable-app-insights.md)
* [Recolher dados para modelos em produção](how-to-enable-data-collection.md)
* [Serviço de Machine Learning do Azure SDK](https://docs.microsoft.com/python/api/overview/azure/ml/intro?view=azure-ml-py)
* [Utilizar o serviço Azure Machine Learning com redes virtuais do Azure](how-to-enable-virtual-network.md)
* [Melhores práticas para criar sistemas de recomendação](https://github.com/Microsoft/Recommenders)
* [Criar uma API de recomendação em tempo real no Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/ai/real-time-recommendation)
