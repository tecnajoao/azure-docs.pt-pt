---
title: incluir ficheiro
description: incluir ficheiro
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 857d29f407c9939143fbb8263be40dadb040efdc
ms.sourcegitcommit: c2e61b62f218830dd9076d9abc1bbcb42180b3a8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53439241"
---
[!INCLUDE [P2S FAQ All](vpn-gateway-faq-p2s-all-include.md)]

### <a name="is-radius-authentication-supported-on-all-azure-vpn-gateway-skus"></a>A autenticação RADIUS é suportada em todos os SKUs de Gateway de VPN do Azure?

A autenticação RADIUS é suportada para SKUs de VpnGw1, VpnGw2 e VpnGw3. Se estiver a utilizar SKUs legados, a autenticação RADIUS é suportada em SKUs Standard e de Elevado Desempenho. Não é suportada no SKU de Gateway Básico. 
 
### <a name="is-radius-authentication-supported-for-the-classic-deployment-model"></a>A autenticação RADIUS é suportada para o modelo de implementação clássica?
 
Não. A autenticação RADIUS não é suportada para o modelo de implementação clássica.
 
### <a name="are-3rd-party-radius-servers-supported"></a>Os servidores RADIUS de terceiros são suportados?

Sim, os servidores RADIUS de terceiros são suportados.
 
### <a name="what-are-the-connectivity-requirements-to-ensure-that-the-azure-gateway-is-able-to-reach-an-on-premises-radius-server"></a>Quais são os requisitos de conectividade necessários para garantir que o gateway do Azure é capaz de alcançar um servidor RADIUS no local?

É necessária uma ligação de rede de VPNs ao site no local com as rotas adequadas configuradas.  
 
### <a name="can-traffic-to-an-on-premises-radius-server-from-the-azure-vpn-gateway-be-routed-over-an-expressroute-connection"></a>O tráfego para um servidor RADIUS no local (a partir do gateway de VPN do Azure) pode ser encaminhado através de uma ligação do ExpressRoute?

Não. O tráfego só pode ser encaminhado através de uma ligação de rede de VPNs.
 
### <a name="is-there-a-change-in-the-number-of-sstp-connections-supported-with-radius-authentication-what-is-the-maximum-number-of-sstp-and-ikev2-connections-supported"></a>Existe uma alteração no número de ligações SSTP suportadas com a autenticação RADIUS? Qual é o número máximo de ligações SSTP e IKEv2 suportadas?

Não existe qualquer alteração no número máximo de ligações SSTP suportadas num gateway com a autenticação RADIUS. Ele continua a ser 128 para SSTP, mas depende do SKU de gateway para IKEv2. Para obter mais informações sobre o número de ligações suportadas, consulte [SKUs de Gateway](../articles/vpn-gateway/vpn-gateway-about-vpngateways.md#gwsku).
 
### <a name="what-is-the-difference-between-doing-certificate-authentication-using-a-radius-server-vs-using-azure-native-certificate-authentication-by-uploading-a-trustedcertificate-to-azure"></a>Qual é a diferença entre fazer a autenticação de certificados com um servidor RADIUS relativamente a utilizar a autenticação de certificados nativa do Azure (através do carregamento de um certificado fidedigno para o Azure).

Na autenticação de certificados RADIUS, o pedido de autenticação é reencaminhado para um servidor RADIUS que processa a validação de certificados. Esta opção é útil caso queira integrar numa infraestrutura de autenticação de certificados que já tenha através de RADIUS.
  
Ao utilizar o Azure para a autenticação de certificados, o gateway de VPN do Azure realiza a validação do certificado. Tem de carregar a chave pública do certificado para o gateway. Também pode especificar uma lista de certificados revogados que não devem ter permissão para estabelecer ligação.

### <a name="does-radius-authentication-work-with-both-ikev2-and-sstp-vpn"></a>A autenticação RADIUS funciona com as VPN IKEv2 e SSTP?

Sim, a autenticação RADIUS funciona com as VPNs IKEv2 e SSTP. 
