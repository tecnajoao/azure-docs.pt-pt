---
title: Aceder ao Cofre de chaves protegido por uma firewall - Azure Key Vault | Documentos da Microsoft
description: Saiba como aceder ao Azure Key Vault a partir de uma aplicação protegida por uma firewall
services: key-vault
documentationcenter: ''
author: amitbapat
manager: barbkess
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 01/07/2019
ms.author: ambapat
ms.openlocfilehash: 36b431d07ad517d495316963fd6710dafab6c297
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56108641"
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>Aceder ao Cofre de Chaves do Azure protegido por firewall

## <a name="what-ports-hosts-or-ip-addresses-should-i-open-to-enable-my-key-vault-client-application-behind-a-firewall-to-access-key-vault"></a>Que portas, anfitriões ou endereços IP devo abrir para ativar a minha aplicação de cliente do Cofre de chaves protegido por uma firewall aceder ao Cofre de chaves?

Para aceder a um cofre de chaves, a sua aplicação cliente do cofre de chaves tem de aceder a vários pontos finais para várias funcionalidades:

* Autenticação através do Azure Active Directory (Azure AD).
* Gestão do Cofre de Chaves do Azure. Isto inclui criar, ler, atualizar, eliminar e definir políticas de acesso através do Azure Resource Manager.
* Aceder e gerir objetos (chaves e segredos) armazenados no próprio Key Vault, através do ponto final específico do Key Vault (por exemplo, [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

Dependendo da configuração e do ambiente, existem algumas variações.

## <a name="ports"></a>Portas

Todo o tráfego para um cofre de chaves para as três funções (autenticação, gestão e acesso ao plano de dados) é feito por HTTPS: porta 443. No entanto, existirá ocasionalmente tráfego HTTP (porta 80) para CRL. Os clientes que suportam o OCSP não devem alcançar o CRL, mas podem, ocasionalmente, alcançar [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl).  

## <a name="authentication"></a>Authentication

As aplicações cliente do Cofre de Chaves terão de aceder a pontos finais do Azure Active Directory para autenticação. O ponto final utilizado depende da configuração do inquilino do Azure AD, do tipo de principal (principal de utilizador ou principal de serviço) e do tipo de conta - por exemplo, uma conta Microsoft ou uma conta escolar ou profissional.  

| Tipo de principal | Ponto final:porta |
| --- | --- |
| Utilizador com conta Microsoft<br> (por exemplo, user@hotmail.com) |**Global:**<br> login.microsoftonline.com:443<br><br> **Azure China:**<br> login.chinacloudapi.cn:443<br><br>**Azure US Government:**<br> login.microsoftonline.us:443<br><br>**Azure Alemanha:**<br> login.microsoftonline.de:443<br><br> e <br>login.live.com:443 |
| Principal de utilizador ou serviço com uma conta escolar ou profissional com o Azure AD (por exemplo, user@contoso.com) |**Global:**<br> login.microsoftonline.com:443<br><br> **Azure China:**<br> login.chinacloudapi.cn:443<br><br>**Azure US Government:**<br> login.microsoftonline.us:443<br><br>**Azure Alemanha:**<br> login.microsoftonline.de:443 |
| Principal de utilizador ou serviço com uma conta escolar ou profissional, mais Serviços de Federação do Active Directory (AD FS) ou outro ponto final federado (por exemplo, user@contoso.com) |Todos os pontos finais para uma conta escolar ou profissional, mais AD FS ou outros pontos finais federados |

Existem outros cenários possíveis complexos. Consulte [Fluxo de Autenticação do Azure Active Directory](../active-directory/develop/authentication-scenarios.md), [Integrar Aplicações com o Azure Active Directory](../active-directory/develop/active-directory-how-to-integrate.md) e [Protocolos de Autenticação do Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) para obter informações adicionais.  

## <a name="key-vault-management"></a>Gestão do Cofre de Chaves

Para a gestão do Cofre de Chaves (CRUD e definição da política de acesso), a aplicação cliente do cofre de chaves tem de aceder a um ponto final do Azure Resource Manager.  

| Tipo de operação | Ponto final:porta |
| --- | --- |
| Operações do painel de controlo do Cofre de Chaves<br> através do Azure Resource Manager |**Global:**<br> management.azure.com:443<br><br> **Azure China:**<br> management.chinacloudapi.cn:443<br><br> **Azure US Government:**<br> management.usgovcloudapi.net:443<br><br> **Azure Alemanha:**<br> management.microsoftazure.de:443 |
| Graph API do Azure Active Directory |**Global:**<br> graph.windows.net:443<br><br> **Azure China:**<br> graph.chinacloudapi.cn:443<br><br> **Azure US Government:**<br> graph.windows.net:443<br><br> **Azure Alemanha:**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Operações do Cofre de Chaves

Para todas as operações criptográficas e de gestão de objetos do cofre de chaves (chaves e segredos), o cliente do cofre de chaves precisa de aceder ao ponto final do cofre de chaves. O sufixo DNS do ponto final varia consoante a localização do seu cofre de chaves. O ponto final do cofre de chaves tem o formato *vault-name*.*region-specific-dns-suffix*, tal como descrito na tabela seguinte.  

| Tipo de operação | Ponto final:porta |
| --- | --- |
| Operações, incluindo operações criptográficas em chaves; criar, ler, atualizar e eliminar chaves e segredos; definir ou obter etiquetas e outros atributos de objetos de cofre de chaves (chaves ou segredos) |**Global:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure China:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure US Government:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Alemanha:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>Intervalos de endereços IP

O serviço Cofre de Chaves utiliza outros recursos do Azure, como a infraestrutura PaaS. Por isso, não é possível fornecer um intervalo de endereços IP específico que os pontos finais do serviço Cofre de Chaves terão num determinado momento. Se a sua firewall só suporta intervalos de endereço IP, consulte o documento [Intervalos IP do Microsoft Azure Datacenter](https://www.microsoft.com/download/details.aspx?id=41653). A Autenticação e Identidade (Azure Active Directory) é um serviço global e pode efetuar a ativação pós-falha noutras regiões ou mover tráfego sem aviso prévio. Neste cenário, todos os intervalos de IP listados em [Endereços IP de Identidade e Autenticação](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity_ip) devem ser adicionados à firewall.

## <a name="next-steps"></a>Passos Seguintes

Se tiver perguntas sobre o Cofre de Chaves, visite os [Fóruns do Cofre de Chaves do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).
