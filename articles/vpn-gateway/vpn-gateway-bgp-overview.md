---
title: Descrição geral de gateways de VPN do Azure e BGP | Documentos da Microsoft
description: Este artigo fornece uma descrição geral do BGP com Gateways de VPN do Azure.
services: vpn-gateway
author: yushwang
manager: rossort
ms.service: vpn-gateway
ms.topic: article
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: 91e9fe1eb6b3df0b64d05f2b1e300403a9e01db9
ms.sourcegitcommit: 70471c4febc7835e643207420e515b6436235d29
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/15/2019
ms.locfileid: "54306527"
---
# <a name="about-bgp-with-azure-vpn-gateway"></a>Sobre o BGP com o Gateway VPN do Azure
Este artigo fornece uma visão geral do suporte BGP (Border Gateway Protocol) no Gateway de VPN do Azure.

O BGP é o protocolo de encaminhamento padrão utilizado normalmente na Internet para trocar informações de encaminhamento e acessibilidade entre duas ou mais redes. Quando utilizado no contexto das Redes Virtuais do Azure,o BGP permite que os Gateways de VPN do Azure e os seus dispositivos VPN no local, conhecidos como elementos de rede ou vizinhos BGP, troquem “rotas” que informarão ambos os gateways da disponibilidade e acessibilidade para esses prefixos percorrerem os gateways ou routers envolvidos. O BGP também pode permitir o encaminhamento de tráfego entre várias redes ao propagar rotas para todos os outros elementos de rede BGP, que um gateway BGP aprende de um elemento de rede BGP. 

## <a name="why"></a>Porquê utilizar o BGP?
O BGP é uma funcionalidade opcional que pode utilizar com os gateways de VPN do Azure Baseados na Rota. Antes de ativar esta funcionalidade, deve verificar se os seus dispositivos VPN no local suportam o BGP. Pode continuar a utilizar os gateways de VPN do Azure e os seus dispositivos VPN no local sem o BGP. É o equivalente a utilizar rotas estáticas (sem BGP) *vs.* utilizar encaminhamento dinâmico com BGP entre as suas redes e o Azure.

O BGP possui várias vantagens e novas capacidades:

### <a name="prefix"></a>Suporte a atualizações de prefixos automáticas e flexíveis
Com o BGP, só tem de declarar um prefixo mínimo para um elemento de rede BGP específico no túnel VPN S2S de IPsec. Pode ser tão pequeno como um prefixo de anfitrião (/32) do endereço IP do elemento de rede BGP do seu dispositivo VPN no local. Pode controlar que prefixos da rede no local pretende anunciar no Azure, para permitir o acesso da sua Rede Virtual do Azure.

Também pode anunciar prefixos maiores, que podem incluir alguns dos seus prefixos de endereço VNet, como um grande privado espaço de endereços IP (por exemplo, 10.0.0.0/8). Tenha em atenção que os prefixos não podem ser idênticos a nenhum dos seus prefixos VNet. As rotas idênticas aos prefixos VNet serão rejeitadas.

### <a name="multitunnel"></a>Suporte de vários túneis entre uma VNet e um site no local com ativação pós-falha automática baseada no BGP
Pode estabelecer várias ligações na mesma localização entre a VNet do Azure e os dispositivos VPN no local. Esta capacidade proporciona vários túneis (caminhos) entre as duas redes numa configuração no modo ativo-ativo. Se um dos túneis for desconectado, as rotas correspondentes serão retiradas através do BGP e o tráfego passa automaticamente para os restantes túneis.

O diagrama seguinte mostra um exemplo simples desta configuração de elevada disponibilidade:

![Vários caminhos ativos](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="transitrouting"></a>Suporte de encaminhamento do tráfego entre as redes no local e várias VNets do Azure
O BGP permite que vários gateways aprendam e propaguem os prefixos a partir de redes diferentes, quer estejam direta ou indiretamente ligadas. Esta opção pode ativar o encaminhamento de tráfego com os gateways de VPN do Azure entre os sites no local ou entre várias Redes Virtuais do Azure.

O diagrama seguinte mostra um exemplo de uma topologia multi-hop com vários caminhos em que o tráfego pode transitar entre as duas redes no local através de gateways de VPN do Azure dentro de Redes da Microsoft:

![Tráfego multi-hop](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="faq"></a>FAQ DE BGP
[!INCLUDE [vpn-gateway-faq-bgp-include](../../includes/vpn-gateway-faq-bgp-include.md)]

## <a name="next-steps"></a>Passos Seguintes
Veja [Introdução ao BGP nos gateways de VPN do Azure](vpn-gateway-bgp-resource-manager-ps.md) para obter os passos para configurar o BGP para as ligações em vários locais e VNet a VNet.

