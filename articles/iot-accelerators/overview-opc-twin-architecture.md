---
title: Arquitetura de OPC duplo - Azure | Documentos da Microsoft
description: Arquitetura de OPC duplo
author: dominicbetts
ms.author: dobett
ms.date: 11/26/2018
ms.topic: overview
ms.service: iot-industrialiot
services: iot-industrialiot
manager: philmea
ms.openlocfilehash: d1c10e056de1bc61b5365550bf2543d2cdf61229
ms.sourcegitcommit: 1a19a5845ae5d9f5752b4c905a43bf959a60eb9d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/11/2019
ms.locfileid: "59495025"
---
# <a name="opc-twin-architecture"></a>Arquitetura de OPC duplo

Os diagramas seguintes mostram a arquitetura de OPC duplo.

## <a name="discover-and-activate"></a>Detectar e ativar

1. O operador ativa de análise no módulo de rede ou faz com que uma deteção única através de um URL de deteção. Os pontos de extremidade detetados e as informações de aplicativo são enviadas através de telemetria para o agente de integração para processamento.  O agente de integração de dispositivo OPC UA processa os eventos de deteção de servidores OPC UA enviados pelo módulo do IoT Edge do OPC duplo no modo de deteção ou análise. O resultado de eventos de deteção no registo de aplicação e as atualizações do registo do dispositivo de OPC UA.

   ![Como funciona o OPC duplo](media/overview-opc-twin-architecture/opc-twin1.png)

1. O operador inspeciona o certificado do ponto de extremidade detetado e ativa o duplo de ponto de extremidade registrados para o acesso. 

   ![Como funciona o OPC duplo](media/overview-opc-twin-architecture/opc-twin2.png)

## <a name="browse-and-monitor"></a>Procurar e monitor

1. Depois de ativado, o operador pode utilizar o REST API do serviço de duplo para procurar ou inspecionar o modelo de informações do servidor, variáveis de objeto de leitura/escrita e chamar métodos.  O utilizador utiliza uma API simplificada de UA de OPC totalmente expresso em HTTP e JSON.

   ![Como funciona o OPC duplo](media/overview-opc-twin-architecture/opc-twin3.png)

1. A interface REST do serviço de duplo também pode ser utilizada para criar itens monitorizados e subscrições no publicador OPC. O publicador de OPC permite que a telemetria ser enviados a partir de sistemas de servidor OPC UA para o IoT Hub. Para obter mais informações sobre o publicador OPC, consulte a [o publicador OPC](https://github.com/Azure/iot-edge-opc-publisher) repositório no GitHub.

   ![Como funciona o OPC duplo](media/overview-opc-twin-architecture/opc-twin4.png)