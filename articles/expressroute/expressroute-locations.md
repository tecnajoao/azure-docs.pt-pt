---
title: 'Localizações e fornecedores de conectividade: O Azure ExpressRoute | Documentos da Microsoft'
description: Este artigo fornece uma descrição geral detalhada das localizações onde os serviços são oferecidos e como ligar a regiões do Azure. Ordenado pelo fornecedor de conectividade.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
ms.assetid: c878513a-d594-42ad-8b0e-403efd0c4b25
ms.service: expressroute
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/05/2019
ms.author: pareshmu
ms.openlocfilehash: a30280339b2172860fa8c859de569c2de1c68e17
ms.sourcegitcommit: 62d3a040280e83946d1a9548f352da83ef852085
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59267451"
---
# <a name="expressroute-partners-and-peering-locations"></a>Parceiros e localizações de peering do ExpressRoute 

> [!div class="op_single_selector"]
> * [Localizações por fornecedor](expressroute-locations.md)
> * [Fornecedores por localização](expressroute-locations-providers.md)


As tabelas neste artigo fornecem informações sobre fornecedores de conectividade ExpressRoute, cobertura geográfica ExpressRoute, serviços em nuvem da Microsoft suportados no ExpressRoute e integradores de sistema ExpressRoute (SIs).

## <a name="partners"></a>Fornecedores de conectividade do ExpressRoute
O ExpressRoute é suportado em todas as regiões e localizações do Azure. O mapa seguinte fornece uma lista de regiões do Azure e localizações do ExpressRoute. As localizações do ExpressRoute mencionam os locais onde a Microsoft se junta a vários fornecedores de serviços.

![Mapa de localização][0]

Terá acesso aos serviços do Azure em todas as regiões numa região geopolítica se estiver ligado a, pelo menos, uma localização do ExpressRoute numa região geopolítica.

### <a name="azure-regions-to-expressroute-locations-within-a-geopolitical-region"></a>Regiões do Azure para localizações do ExpressRoute numa região geopolítica.
A tabela seguinte fornece um mapa de regiões do Azure para localizações do ExpressRoute numa região geopolítica.

| **Região geopolítica** | **Zona** | **Regiões do Azure** | **Localizações do ExpressRoute** |
| --- | --- | --- | --- |
| **Governo da Austrália** | 1 | Austrália Central, Austrália Central 2 |Camberra, Camberra2 |
| **Europa** | 1 |França Central, Sul de França, Europa do Norte, Europa Ocidental, Oeste do Reino Unido, Sul do Reino Unido |Amesterdão, Amsterdam2, Dublin, Londres, London2, Marselha, Newport(Wales), Paris, Zurique |
| **América do Norte** | 1 |E.U.A. Leste, E.U.A. Oeste, E.U.A. Leste 2, E.U.A. Oeste 2, E.U.A. Central, E.U.A. Centro-Sul, E.U.A. Centro-Norte, E.U.A. Centro-Oeste, Canadá Central, Canadá Leste |Atlanta, Chicago, Dallas, Denver, Las Vegas, Los Angeles, Miami, Nova Iorque, San Antonio, Seattle, Silicon Valley, Washington DC, Washington DC2, Montreal, cidade do Quebeque, Toronto |
| **Ásia** | 2 |Ásia Oriental, Sudeste Asiático |Hong Kong, Kuala Lumpur, Singapore, Singapore2, Taipei |
| **Austrália** | 2 |Sudeste da Austrália, Leste da Austrália |Melbourne, Perth, Sydney | 
| **Índia** | 2 |Oeste da Índia, Índia Central, Sul da Índia |Chennai, Chennai2, Mumbai, Mumbai2 |
| **Japão** | 2 |Oeste do Japão, Leste do Japão |Osaka, Tóquio |
| **Coreia do Sul** | 2 |Centro da Coreia, Sul da Coreia do Sul |Busan, Seul|
| **EMIRADOS ÁRABES UNIDOS** | 2 | EAU Central, Norte dos eau | Dubai |
| **África do Sul** | 3 |África do Sul Ocidental, Norte da África do Sul |Cidade do Cabo, Joanesburgo |
| **América do Sul** | 3 |Sul do Brasil |São Paulo |


### <a name="regions-and-geopolitical-boundaries-for-national-clouds"></a>Regiões e limites geopolíticos para nuvens nacionais
A tabela abaixo fornece informações sobre regiões e limites geopolíticos para nuvens nacionais.

| **Região geopolítica** | **Regiões do Azure** | **Localizações do ExpressRoute** |
| --- | --- | --- |
| **Nuvem do Governo dos EUA** |US Gov Arizona, US Gov - Iowa, US Gov Texas, Gov (US) - Virginia, US DoD Central, US DoD East  |Chicago, Dallas, Nova Iorque, Phoenix, San Antonio, Seattle, Silicon Valley, Washington DC |
| **Leste da China** |Leste da China, Leste da China 2 |Shanghai, Shanghai2 |
| **Norte da China** |Norte da China, Norte da China 2 |Pequim, Beijing2 |
| **Alemanha** |Alemanha Central, Leste da Alemanha |Berlim, Frankfurt |

A conectividade em regiões geopolíticas não é suportada no SKU do ExpressRoute standard. Terá de ativar o suplemento ExpressRoute Premium para suportar a conetividade global. A conectividade com ambientes em nuvem nacionais não é suportada. Pode trabalhar com o seu fornecedor de conectividade, se tal for necessário.

## <a name="locations"></a>Localizações dos fornecedores de conectividade

A tabela seguinte mostra as localizações por fornecedor de serviços. Se quiser ver os fornecedores disponíveis por localização, veja [Fornecedores de serviços por localização](expressroute-locations-providers.md#locations).


### <a name="production-azure"></a>Azure de Produção

| **Fornecedor de serviços** | **Microsoft Azure** | **Office 365 e Dynamics 365** | **Localizações** |
| --- | --- | --- | --- |
| **[AARNet](https://www.aarnet.edu.au/network-and-services/cloud-services-applications/azure-expressroute/)** |Suportadas |Suportado |Melbourne, Sydney |
| **[Airtel](https://www.airtel.in/creatingsmiles/)** | Suportadas | Suportadas | Chennai2, Mumbai2 |
| **[Redes Aryaka](https://www.aryaka.com/)** |Suportadas |Suportadas |Amesterdão, Chicago, Dallas, Hong Kong, São Paulo, Seattle, Silicon Valley, Singapura, Tóquio, Washington D.C. |
| **[Ascenty Data Centers](https://ascenty.com/servicos/cloud-connect/microsoft-expressroute/)** |Suportadas |Suportado |São Paulo |
| **[AT & T NetBond](https://www.synaptic.att.com/clouduser/html/productdetail/ATT_NetBond.htm)** |Suportadas |Suportado |Amesterdão, Chicago, Dallas, Londres, Silicon Valley, Singapura, Sydney, Tóquio, Toronto, Washington D.C. |
| **[Bell Canada](https://business.bell.ca/shop/enterprise/cloud-connect-access-to-cloud-partner-services)** |Suportadas |Suportado |Montreal, Toronto, Cidade do Quebeque |
| **[British Telecom](https://www.globalservices.bt.com/en/solutions/products/bt-compute-for-microsoft-azure)** |Suportadas |Suportadas |Amesterdão, RAE de Hong Kong, Londres, Newport(Wales), são Paulo, Silicon Valley, Singapura, Sydney, Tóquio, Washington D.C. |
| **C3ntro** |Brevemente |Brevemente |Miami |
| **CDC** | Suportadas | Suportadas | Camberra, Camberra2 |
| **[CenturyLink Cloud Connect](https://www.centurylink.com/cloudconnect)** |Suportadas |Suportadas |Las Vegas, Nova Iorque, San Antonio, Silicon Valley, Tóquio, Toronto |
| **Diretor de telecomunicações** |Suportadas |Suportadas |Taipé |
| **China Telecom Global** |Suportadas |Não suportado |Hong Kong |
| **[Cologix](https://www.cologix.com/solutions/cloud-connect/public-clouds/microsoft-cloud/)** |Suportadas |Suportadas |Chicago, Dallas, Montreal, Toronto, Washington D.C. |
| **[Colt](https://www.colt.net/uk/en/news/colt-announces-dedicated-cloud-access-for-microsoft-azure-services-en.htm)** |Suportadas |Suportadas |Amesterdão, Dublin, Londres, Paris, singapura2, Tóquio |
| **[Comcast](https://business.comcast.com/landingpage/microsoft-azure)** |Suportadas |Suportado |Chicago, Silicon Valley, Washington D.C. |
| **[CoreSite](https://www.coresite.com/solutions/cloud-services/public-cloud-providers/microsoft-azure-expressroute)** |Suportadas |Suportadas |Chicago, Denver, Los Angeles, Nova Iorque, Silicon Valley, Washington DC, Washington DC2 |
| **DE-CIX** | Suportadas |Suportadas |Amsterdam2|
| **eir** |Suportadas |Suportado |Dublin|
| **Comunicações globais de épsilon** |Suportadas |Suportado |Singapura, Singapura2 |
| **[Equinix](https://www.equinix.com/partners/microsoft-azure/)** |Suportadas |Suportadas |Amesterdão, Atlanta, Chicago, Dallas, Dublin, Hong Kong, Londres, London2, Los Angeles, Melbourne, Miami, Nova Iorque, Osaka, Paris, são Paulo, Seattle, Silicon Valley, Singapura, Sydney, Tóquio, Toronto, Washington D.C. |
| **UAE Etisalat** |Suportadas |Suportadas |Dubai|
| **euNetworks** |Suportadas |Suportado |Amesterdão, Dublin, Londres |
| **GÉANT** |Suportadas |Suportado |Amesterdão |
| **[Global Cloud Xchange (GCX)](https://globalcloudxchange.com/cloud-platform/cloud-x-fusion/)** | Suportadas| Suportado | Chennai, Mumbai |
| **[InterCloud](https://www.intercloud.com/)** |Suportadas |Suportadas |Amesterdão, Chicago, Londres, Nova Iorque, Paris, Silicon Valley, Singapura, Washington D.C. |
| **Internet2** |Suportadas |Suportadas |Chicago, Dallas, Washington D.C. |
| **[Internet Initiative Japan Inc. – IIJ](https://www.iij.ad.jp/en/news/pressrelease/2015/1216-2.html)** |Suportadas |Suportado |Osaka, Tóquio |
| **[Internet Solutions – Cloud Connect](https://www.is.co.za/solution/cloud-connect/)** |Suportadas |Suportadas |Cidade do Cabo, Joanesburgo, Londres |
| **[Interxion](https://www.interxion.com/why-interxion/colocate-with-the-clouds/Microsoft-Azure/)** |Suportadas |Suportadas |Amesterdão, Amsterdam2, Dublin, Londres, Marselha, Paris, Zurique |
| **[IX Reach](https://www.ixreach.com/partners/cloud-partners/microsoft-azure/)**|Suportadas |Suportadas | Amesterdão, London2, Silicon Valley, Toronto |
| **Jisc** |Suportadas |Suportado |Londres |
| **[KINX](https://www.kinx.net/service/network/cloudhub/ms-expressroute/?lang=en)** |Suportadas |Suportado |Seul |
| **[Kordia](https://www.kordia.co.nz/cloudconnect)** | Suportadas |Suportadas |Sydney |
| **[KPN](https://www.kpn.com/zakelijk/cloud/connect.htm)** | Suportadas | Suportado | Amesterdão | 
| **[Comunicações de nível 3](http://your.level3.com/LP=882?WT.tsrc=02192014LP882AzureVanityAzureText)** |Suportadas |Suportadas |Amesterdão, Chicago, Dallas, Londres, Newport (Gales), são Paulo, Seattle, Silicon Valley, Singapura, Washington D.C. |
| **LG CNS** |Suportadas |Suportado |Busan, Seul |
| **[Telecomunicações líquidas](https://www.liquidtelecom.com/products-and-services/cloud.html)** |Suportadas |Suportadas |Cidade do Cabo, Joanesburgo |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |Suportadas |Suportadas |Amesterdão, Atlanta, Chicago, Dallas, Denver, Dublin, Hong Kong, Las Vegas, Londres, Los Angeles, Melbourne, Miami, Nova Iorque, Perth, cidade do Quebeque, San Antonio, Seattle, Silicon Valley, Singapura, singapura2, Sydney, Toronto, Washington D.C. |
| **[MTN](https://www.mtnbusiness.com/en/enterprise/Pages/microsoft-express-route.aspx)** |Suportadas |Suportado |Londres |
| **[Redes de Neutrona](http://www.neutrona.com/index.php/azure-expressroute/)** |Suportadas |Suportadas |Dallas, Los Angeles, Miami, são Paulo |
| **[Next Generation Data](http://www.nextgenerationdata.co.uk/ngd-cloud-gateway/)** |Suportadas |Suportado |Newport (País de Gales) |
| **[NEXTDC](https://www.nextdc.com/services/axon-ethernet/microsoft-expressroute)** |Suportadas |Suportadas |Melbourne, Perth, Sydney |
| **[Comunicações NTT](https://www.ntt.com/en/services/network/virtual-private-network.html)** |Suportadas |Suportado |Amesterdão, RAE de Hong Kong, Londres, Los Angeles, Osaka, Singapura, Sydney, Tóquio, Washington D.C. |
| **[NTT EAST](https://flets.com/cloudgateway/crossconnect/)** |Suportadas |Suportadas |Tóquio |
| **[NTT SmartConnect](https://cloud.nttsmc.com/cxc/azure.html)** |Suportadas |Suportado |Osaka |
| **[Optus](https://www.optus.com.au/enterprise/networking/network-connectivity/express-link)** |Suportadas |Suportado |Melbourne, Sydney |
| **[Laranja](https://www.orange-business.com/en/products/business-vpn-galerie)** |Suportadas |Suportadas |Amesterdão, RAE de Hong Kong, Londres, Paris, são Paulo, Silicon Valley, Singapura, Sydney, Tóquio, Washington D.C. |
| **[PacketFabric](https://www.packetfabric.com/packetcor/microsoft-azure/)** |Suportadas |Suportado |Chicago, Silicon Valley, Washington D.C. |
| **[PCCW Global Limited](https://consoleconnect.com/clouds/#azureRegions)** |Suportadas |Suportadas |Chicago, RAE de Hong Kong, Londres |
| **[Sejong Telecom](https://www.sejongtelecom.net/en/pages/service/cloud_ms)** |Suportadas |Suportado |Seul |
| **[SIFY](http://telecom.sify.com/azure-expressroute.html)** |Suportadas |Suportadas |Chennai, Mumbai2 |
| **[SingTel](http://info.singtel.com/about-us/news-releases/singtel-provide-secure-private-access-microsoft-azure-public-cloud)** |Suportadas |Suportado |Singapura, Singapura2 |
| **[Softbank](https://www.softbank.jp/biz/cloud/cloud_access/direct_access_for_az/)** |Suportadas |Suportado |Osaka, Tóquio |
| **[Sprint](https://business.sprint.com/solutions/cloud-networking/)** |Suportadas |Suportado |Chicago, Silicon Valley, Washington D.C. |
| **[Tata Communications](https://www.tatacommunications.com/lp/izo/azure/azure_index.html)** |Suportadas |Suportadas |Amesterdão, Chennai, RAE de Hong Kong, Londres, Mumbai, São Paulo, Silicon Valley, Singapura, Washington D.C. |
| **Telecity Group** |Suportadas |Suportado |Amesterdão |
| **[Telefonica](https://www.business-solutions.telefonica.com/es/enterprise/solutions/efficient-infrastructure/managed-voice-data-connectivity/)** |Suportadas |Suportado |Amesterdão, São Paulo |
| **[Telehouse - KDDI](https://www.telehouse.net/solutions/cloud-services/cloud-link)** |Suportadas |Suportado |Londres |
| **Telenor** |Suportadas |Suportado |Amesterdão, Londres |
| **[Operadora de Telia](https://teliacarrier.com/our-services/connectivity/cloud-connect.html?title=Cloud%20Connect)** | Suportadas | Suportadas |Amesterdão, Chicago, Dallas, Londres, Washington D.C. |
| **Telmex Uninet**| Suportadas | Suportadas | Dallas |
| **[Telstra Corporation](https://www.telstra.com.au/business-enterprise/network-services/networks/cloud-direct-connect/)** |Suportadas |Suportadas |Melbourne, Singapura, Sydney |
| **[Telus](https://www.telus.com)** |Suportadas |Suportado |Montreal, Toronto |
| **[Teraco](https://www.teraco.co.za/services/africa-cloud-exchange/)** |Suportadas |Suportadas |Cidade do Cabo, Joanesburgo |
| **[TIME dotCom](https://www.time.com.my/enterprise/connectivity/cloud-interconnect)** | Suportadas | Suportadas | Kuala Lumpur |
| **[UOLDIVEO](https://www.uoldiveo.com.br/)** |Suportadas |Suportado |São Paulo |
| **[Verizon](https://enterprise.verizon.com/products/network/application-enablement/secure-cloud-interconnect/)** |Suportadas |Suportado |Amesterdão, Chicago, Dallas, Hong Kong, Londres, Silicon Valley, Singapura, Sydney, Tóquio, Washington D.C |
| **[Vodafone](https://www.vodafone.com/business/global-enterprise/global-connectivity/vodafone-ip-vpn-cloud-connect)** |Suportadas |Não suportado |Londres, Singapura |
| **Vodafone Idea** | Suportadas | Suportadas | Mumbai, Mumbai2 |
| **[Zayo](http://www.zayo.com/solutions/industries/cloud-connectivity/microsoft-expressroute)** |Suportadas |Suportadas |Amesterdão, Chicago, Dallas, Denver, Londres, Los Angeles, Montreal, Nova Iorque, Paris, Seattle, Silicon Valley, Toronto, Washington D.C. |

 **+** brevemente disponível

### <a name="national-cloud-environment"></a>Ambientes em nuvens nacionais

### <a name="us-government-cloud"></a>Nuvem do Governo dos EUA

| **Fornecedor de serviços** | **Microsoft Azure** | **Office 365** | **Localizações** |
| --- | --- | --- | --- |
| **[AT & T NetBond](https://www.synaptic.att.com/clouduser/html/productdetail/ATT_NetBond.htm)** |Suportadas |Suportadas |Chicago, Phoenix,  Washington DC |
| **[CenturyLink Cloud Connect](https://www.centurylink.com/cloudconnect)** |Suportadas |Suportadas |Nova Iorque, Phoenix |
| **[Equinix](https://www.equinix.com/partners/microsoft-azure/)** |Suportadas |Suportado |Chicago, Dallas, Nova Iorque, Seattle, Silicon Valley, Washington DC |
| **[Comunicações de nível 3](http://your.level3.com/LP=882?WT.tsrc=02192014LP882AzureVanityAzureText)** |Suportadas |Suportado |Chicago, Silicon Valley, Washington D.C. |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |Suportadas | Suportadas | Chicago, Dallas, San Antonio, Seattle |
| **[Verizon](http://news.verizonenterprise.com/2014/04/secure-cloud-interconnect-solutions-enterprise/)** |Suportadas |Suportadas |Chicago, Dallas, Nova Iorque, Silicon Valley, Washington DC |

### <a name="china"></a>China

| **Fornecedor de serviços** | **Microsoft Azure** | **Office 365** | **Localizações** |
| --- | --- | --- | --- |
| **China Telecom** |Suportadas |Não suportado |Pequim, Xangai |
| **[GDS](http://en.gds-services.com/news_detail/newsId=21.html)** |Suportadas |Não suportado |Beijing2, Shanghai2 |

Para saber mais, veja [ExpressRoute na China](http://www.windowsazure.cn/home/features/expressroute/).

### <a name="germany"></a>Alemanha

| **Fornecedor de serviços** | **Microsoft Azure** | **Office 365** | **Localizações** |
| --- | --- | --- | --- |
| **[Colt](https://www.colt.net/uk/en/news/colt-announces-dedicated-cloud-access-for-microsoft-azure-services-en.htm)** |Suportadas |Não suportado |Frankfurt |
| **[Equinix](https://www.equinix.com/partners/microsoft-azure/)** |Suportadas |Não suportado |Frankfurt |
| **[e-shelter](https://www.e-shelter.de/en/microsoft-expressroutetm)** |Suportadas |Não suportado |Berlim |
| **Interxion** |Suportadas |Não suportado |Frankfurt |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |Suportadas  | Não suportado | Berlim |
| **T-Systems** |Suportadas |Não suportado |Berlim |

## <a name="connectivity-through-exchange-providers"></a>Conectividade Através de Fornecedores do Exchange

Se o seu fornecedor de conectividade não está listado nas secções anteriores, pode criar na mesma uma ligação.

* Consulte o seu fornecedor de conectividade para saber se este está ligado a alguma das trocas na tabela acima. Pode verificar as ligações seguintes para recolher mais informações sobre os serviços disponibilizados pelos fornecedores de troca. Vários fornecedores de conectividade já estão ligados às trocas de Ethernet.
  * [Cologix](https://www.cologix.com/)
  * [CoreSite](https://www.coresite.com/)
  * [Nuvem Equinix Exchange](https://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [Interxion](https://www.interxion.com/products/interconnection/cloud-connect/)
  * [IX Reach](https://www.ixreach.com/partners/cloud-partners/microsoft-azure/)
  * [Megaport](https://www.megaport.com/services/microsoft-expressroute/)
  * [NextDC](https://www.nextdc.com/)
  * [PacketFabric](https://www.packetfabric.com/packetcor/microsoft-azure/) 
* Solicite ao seu fornecedor de conectividade para expandir a sua rede para a localização de peering que pretende.
  * Certifique-se de que o fornecedor de conectividade expande a sua conectividade para um estado de elevada disponibilidade, de forma a não existirem pontos únicos de falha.
* Organize um circuito ExpressRoute com a troca como o seu fornecedor de conectividade para se ligar à Microsoft.
  * Siga os passos em [Criar um circuito ExpressRoute](expressroute-howto-circuit-classic.md) para configurar a conectividade.

## <a name="connectivity-through-additional-service-providers"></a>Conectividade Através de Fornecedores de Serviços Adicionais

| **Fornecedor de conectividade** | **Troca** | **Localizações** |
| --- | --- | --- |
| **[1CLOUDSTAR](https://www.1cloudstar.com/service/cloudconnect-azure-expressroute/)** |Equinix |Singapura |
| **[Airgate Technologies, Inc.](https://www.airgate.ca/expressroute)** | Equinix, Cologix | Toronto, Montreal |
| **[Alaska Communications](https://www.alaskacommunications.com/For-Your-Business/Direct-Cloud-Service)** |Equinix |Seattle |
| **[Altice comercial](https://golightpath.com/transport)** |Equinix |Nova Iorque, Washington D.C. |
| **[Arteria Networks Corporation](https://www.arteria-net.com/business/service/cloud/sca/)** |Equinix |Tóquio |
| **[Axtel](https://alestra.mx/landing/expressrouteazure/)** |Equinix |Dallas|
| **[Bezeq International Ltd.](https://www.bezeqint.net/english)** | euNetworks | Londres |
| **[BICS](https://bics.com/bics-solutions-suite/cloud-connect/)** | Equinix | Amesterdão, Frankfurt, Londres, Singapura, Washington D.C. |
| **[BroadBand Tower, Inc.](https://www.bbtower.co.jp/product-service/data-center/network/dcconnect-for-azure/)** | Equinix | Tóquio |
| **[C3ntro Telecom](https://www.c3ntro.com/data/express-route)** | Equinix, Megaport | Dallas |
| **[Chief](https://www.chief.com.tw/dispPageBox/ct.aspx?ddsPageID=ENCLOUDSERVICE&dbid=4852937342)** | Equinix | Hong Kong |
| **[Cinia](https://www.cinia.fi/en/services/connectivity-services/direct-public-cloud-connection.html)** | Equinix, Megaport | Frankfurt, Hamburgo |
| **[CloudXpress](https://www2.telenet.be/fr/business/produits-services/internet/cloudxpress/)** | Equinix | Amesterdão | 
| **[Cogeco mesmo nível 1](https://www.cogecopeer1.com/en/)**| Equinix | Montreal, Toronto |
| **[CoreAzure](http://coreazure.com/expressroute)**| Equinix | Londres |
| **[Cox Business](https://www.cox.com/business/networking/cloud-connectivity.html)** | Equinix | Dallas, Silicon Valley, Washington DC | 
| **[Dados Foundry](https://www.datafoundry.com/services/cloud-connect)** | Megaport | Dallas |
| **[Épsilon limitado de telecomunicações](http://www.epsilontel.com/data-connectivity/cloud-access/)** | Equinix | Londres, Singapura, Washington DC |
| **[Eurofiber](https://eurofiber.nl/microsoft-azure/)** | Equinix | Amesterdão |
| **[Exponential E](https://www.exponential-e.com/services/connectivity-services/cloud-connect-exchange)** | Equinix | Londres |
| **[Fastweb S.p.A](https://www.fastweb.it/grandi-aziende/connessione-voce-e-wifi/scheda-prodotto/rete-privata-virtuale/)** | Equinix | Amesterdão |
| **[Fibrenoire](https://www.fibrenoire.ca/en/cloudextn)** | Megaport | Cidade do Quebeque |
| **[GTt comunicações Inc](https://www.gtt.net)** |Equinix | Washington, D.C. |
| **[Bridge de longa distância internacional](https://www.gbiinc.com/microsoft-azure-expressroute/)** | Equinix | Amesterdão |
| **[HSO](https://www.hso.co.uk/products/cloud-direct)** |Equinix | Londres, Slough |
| **[IVedha Inc](http://www.ivedha.com/cloud/manage-azure-cloud/express-route-4/)**| Equinix | Toronto |
| **LGA Telecom** |Equinix |Singapura|
| **[Lightower](http://www.lightower.com/network-solutions/cloud-connect/#microsoft-azure)** |Equinix | Chicago, Nova Iorque, Washington D.C. |
| **[Macroview Telecom](http://www.macroview.com/en/scripts/catitem.php?catid=solution&sectionid=expressroute)** |Equinix |Hong Kong |
| **[Macquarie Telecom Group](https://macquariegovernment.com/secure-cloud/secure-cloud-exchange/)** | Megaport | Sydney |
| **[MainOne](https://www.mainone.net/services/connectivity/cloud-connect/)** |Equinix | Amesterdão |
| **[Masergy](https://www.masergy.com/solutions/hybrid-networking/cloud-marketplace/microsoft-azure)** | Equinix | Washington, D.C. |
| **[MTN](https://www.mtnbusiness.com/en/enterprise/Pages/microsoft-express-route.aspx)** | Teraco | Cidade do Cabo, Joanesburgo |
| **[Redes de NexGen](https://www.nexgen-net.com/nexgen-networks-direct-connect-microsoft-azure-expressroute.html)** | Interxion | Londres |
| **[Nianet](https://nianet.dk/produkter/internet/microsoft-expressroute)** |Telecity | Amesterdão, Frankfurt |
| **[Publicar](https://www.teralinksolutions.com/cloud-connectivity/cloudbridge-to-azure-expressroute/)**|Equinix | Amesterdão |
| **[Proximus](https://www.proximus.be/en/id_b_cl_proximus_external_cloud_connect/companies-and-public-sector/discover/magazines/expert-blog/proximus-external-cloud-connect.html)**|Equinix | Amesterdão, Dublin, Londres, Paris |
| **[QSC AG](https://www.qsc.de/de/produkte-loesungen/cloud-services-und-it-outsourcing/pure-enterprise-cloud/multi-cloud-management/azure-expressroute/)** |Interxion | Frankfurt |  
| **Rogers** | Cologix, Equinix | Montreal, Toronto |
| **[Tamares Telecom](http://www.tamarestelecom.com/our-services/#Connectivity)** | Telecity | Londres | 
| **[TDC Erhverv](https://tdc.dk/Produkter/cloudaccessplus)** | Equinix | Amesterdão | 
| **[Telecomunicações Itália Sparkle](https://www.tisparkle.com/our-platform/corporate-platform/sparkle-cloud-connect#catalogue)**| Equinix | Amesterdão |
| **[Telia](https://www.telia.se/foretag/losningar/produkter-tjanster/datanet)** | Equinix | Amesterdão |
| **[ThinkTel](https://www.thinktel.ca/services/agile-ix-data/expressroute/)** | Equinix | Toronto | 
| **[Transtelco](http://www.transtelco.net/tcloud/microsoft)** |Equinix | Dallas, Los Angeles |
| **[Unidos de informações de autoestrada (UIH)](https://www.uih.co.th/en/internet-solution/cloud-direct/uih-cloud-direct-for-microsoft-azure-expressroute)**| Equinix | Singapura |
| **[Venha Pra Nuvem](https://venhapranuvem.com.br/)** | Equinix | São Paulo |
| **[Webair](https://www.webair.com/microsoft-express-route-partnership/)**| Megaport | Nova Iorque |
| **[Windstream](https://www.windstreambusiness.com/solutions/cloud-services/cloud-and-managed-hosting-services)**| Equinix | Chicago, Silicon Valley, Washington D.C. |
| **Zain** |Equinix |Londres|
| **[Zertia](https://www.zertia.es)**| Level 3 | Madrid |
| **[Zirro](https://zirro.com/services/)**| Equinix | Montreal, Toronto |

## <a name="connectivity-through-datacenter-providers"></a>Conectividade Através de Fornecedores de Datacenters

| **Fornecedor** | **Exchange** |
| --- | --- |
| **[Cyrus um](https://cyrusone.com/enterprise-data-center-services/connectivity-and-interconnection/cloud-connectivity-reaching-amazon-microsoft-google-and-more/microsoft-azure-expressroute/?doing_wp_cron=1498512235.6733090877532958984375)** | Megaport |
| **[Cyxtera](https://www.cyxtera.com/data-center-services/interconnection)** | Megaport |
| **[Digital Realty](https://www.digitalrealty.com/services/interconnection/service-exchange/)** | Megaport |
| **[EdgeConnex](http://www.edgeconnex.com/services/edge-data-centers-proximity-matters/)** | Megaport |
| **[Centros de dados de RagingWire](https://www.ragingwire.com/wholesale/wholesale-data-centers-worldwide-nexcenters)** | IX Reach |
| **[T5 centros de dados](https://t5datacenters.com/network-cloud-connect/)** | IX Reach |

## <a name="connectivity-through-national-research-and-education-networks-nren"></a>Conectividade Através de National Research and Education Networks (NREN, Redes de Investigação e Ensino Nacionais)

| **Fornecedor**|
| --- |
| **AARNET**| 
| **DeIC, através da GÉANT**|
| **GARR, através da GÉANT**|
| **GÉANT**|
| **HEAnet, através da GÉANT**|
| **Internet2**|
| **JISC**|
| **RedIRIS, através da GÉANT**|
| **SINET**|
| **Surfnet, através da GÉANT**|

* Se o seu fornecedor de conectividade não estiver listado aqui, verifique se está ligado a algum dos Parceiros do Exchange do ExpressRoute apresentados acima.

## <a name="expressroute-system-integrators"></a>Integradores de sistemas ExpressRoute
A ativação da conectividade privada para atender as suas necessidades pode ser um desafio, com base na escala da sua rede. Pode trabalhar com qualquer um dos integradores de sistemas listados na seguinte tabela para ajudá-lo com a integração do ExpressRoute.

| **Integrador de sistema** | **Continente** |
| --- | --- |
| **[Altogee](https://altogee.be/diensten/express-route/)** | Europa |
| **[Avanade Inc.](https://www.avanade.com/)** | Ásia, Europa, América do Norte, América do Sul |
| **[Bright Skies GmbH](http://bskies.io/expressroute)** | Europa
| **[Ensyst](https://www.ensyst.com.au)** | Ásia
| **[Serviços Profissionais Equinix](https://www.equinix.com/services/consulting/)** | América do Norte |
| **[FlexManage](https://www.flexmanage.com/cloud)** | América do Norte |
| **[Lightstream](https://www.lightstream.tech/partners/microsoft-azure/)** | América do Norte |
| **[O grupo de consultoria de TI](https://itconsult.com.au/)** | Austrália |
| **[MOQdigital](https://www.moqdigital.com.au/insights/technical/network-connectivity-options-for-azure)** | Austrália |
| **[Serviços de mensagem](https://www.msg-services.de/it-services/managed-services/cloud-outsourcing/)** | Europa (Alemanha) |
| **[Nelite](https://www.nelite.com/offres-services/)** | Europa |
| **[New Signature](https://newsignature.com/technologies/express-route/)** | Europa |
| **[OneAs1a](https://www.oneas1a.com/connectivity.html)** | Ásia |
| **[Redes de cor de laranja](https://orange-networks.com/blog/88-azureexpressroute)** | Europa |
| **[Perficient](https://www.perficient.com/Partners/Microsoft/Cloud/Azure-ExpressRoute)** | América do Norte |
| **[Presidio](https://info.presidio.com/microsoft-azure-expressroute)** | América do Norte |
| **[sol-tec](https://www.sol-tec.com/services)** | Europa |
| **[Venha Pra Nuvem](https://venhapranuvem.com.br/)** | América do Sul |
| **[Vigilant.IT](https://vigilant.it/expressroute)** | Austrália |

## <a name="next-steps"></a>Passos seguintes
* Para obter mais informações acerca do ExpressRoute, veja as [FAQs do ExpressRoute](expressroute-faqs.md).
* Confirme que todos os pré-requisitos são cumpridos. Veja os [Pré-requisitos do ExpressRoute](expressroute-prerequisites.md).

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "Mapa de localização"
