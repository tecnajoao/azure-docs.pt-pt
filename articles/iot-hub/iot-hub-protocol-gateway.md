---
title: Gateway de protocolo do IoT do Azure | Documentos da Microsoft
description: Como utilizar um gateway de protocolo do IoT do Azure para expandir o seu IoT Hub recursos e suporte de protocolo para permitir que os dispositivos para ligar ao seu hub utilizando protocolos não suportados nativamente pelo IoT Hub.
author: robinsh
manager: philmea
ms.author: robinsh
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 07/11/2017
ms.openlocfilehash: 9dbb7905c2a0fed65ede610577e0fa11a1deef92
ms.sourcegitcommit: 62d3a040280e83946d1a9548f352da83ef852085
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59276240"
---
# <a name="support-additional-protocols-for-iot-hub"></a>Suporte para protocolos adicionais para o IoT Hub

O IoT Hub do Azure suporta nativamente comunicação pelos protocolos MQTT, AMQP e HTTPS. Em alguns casos, dispositivos ou gateways de campo podem não ser capazes de usar um desses protocolos padrão e exigem adaptação de protocolo. Nesses casos, pode utilizar um gateway personalizado. Um gateway de personalizado permite a adaptação de protocolo para pontos finais do IoT Hub preenchendo o tráfego de e para o IoT Hub. Pode utilizar o [gateway de protocolo do IoT do Azure](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) como um gateway personalizado para ativar a adaptação de protocolo para o IoT Hub.

## <a name="azure-iot-protocol-gateway"></a>Gateway de protocolo do Azure IoT

O gateway de protocolo do IoT do Azure é uma estrutura para adaptação de protocolo que foi concebida para elevado escalamento, bidirecionais de comunicação de dispositivos com o IoT Hub. O gateway de protocolo é um componente de pass-through que aceita ligações de dispositivos através de um protocolo específico. Ele liga o tráfego para o IoT Hub através de AMQP 1.0.

Pode implementar o gateway de protocolo no Azure de forma altamente dimensionável com o Azure Service Fabric, funções de trabalho de serviços Cloud do Azure ou as máquinas virtuais do Windows. Além disso, o gateway de protocolo pode ser implementado em ambientes no local, como gateways de campo.

O gateway de protocolo do IoT do Azure inclui um adaptador de protocolo MQTT que permite-lhe personalizar o comportamento de protocolo MQTT se necessário. Uma vez que o IoT Hub fornece suporte interno para o protocolo do MQTT v3.1.1, deve considerar apenas usando o adaptador do protocolo MQTT se são necessários as personalizações de protocolo ou requisitos específicos para uma funcionalidade adicional.

O adaptador MQTT também demonstra o modelo de programação para a criação de adaptadores de protocolo para outros protocolos. Além disso, o modelo de programação de gateway de protocolo do Azure IoT permite-lhe de plug-in componentes personalizados para processamento especializado, como autenticação personalizada, transformações de mensagens, compactação/descompactação ou encriptação/desencriptação de tráfego entre os dispositivos e IoT Hub.

Para flexibilidade, o gateway de protocolo do IoT do Azure e a implementação de MQTT são fornecidos num projeto de software open-source. Pode utilizar o projeto de código-fonte aberto para adicionar suporte para vários protocolos e as versões de protocolo, ou personalizar a implementação para o seu cenário. 

## <a name="next-steps"></a>Passos Seguintes

Para saber mais sobre o gateway de protocolo do IoT do Azure e como utilizar e implementá-la como parte da sua solução de IoT, veja:

* [Repositório de gateway do IoT protocolo do Azure no GitHub](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)

* [Guia do Programador de gateway de protocolo do Azure IoT](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

Para saber mais sobre o planeamento da implementação do IoT Hub, veja:

* [Compare com os Hubs de Eventos](iot-hub-compare-event-hubs.md)

* [Dimensionamento, elevada disponibilidade e recuperação após desastre](iot-hub-scaling.md)

* [Guia do programador do IoT Hub](iot-hub-devguide.md)