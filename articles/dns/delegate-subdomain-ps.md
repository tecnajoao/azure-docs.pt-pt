---
title: Delegar um subdomínio de DNS do Azure com o Azure PowerShell
description: Aprenda a delegar um subdomínio de DNS do Azure com o Azure PowerShell.
services: dns
author: vhorne
ms.service: dns
ms.topic: article
ms.date: 2/7/2019
ms.author: victorh
ms.openlocfilehash: 40b2a4d98e6269d9740856ba44c1043af75ce1b8
ms.sourcegitcommit: e51e940e1a0d4f6c3439ebe6674a7d0e92cdc152
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/08/2019
ms.locfileid: "55896730"
---
# <a name="delegate-an-azure-dns-subdomain-using-azure-powershell"></a>Delegar um subdomínio de DNS do Azure com o Azure PowerShell

Pode utilizar o Azure PowerShell para delegar um subdomínio DNS. Por exemplo, se for o proprietário do domínio contoso.com, pode delegar um subdomínio chamado *engenharia* à zona de outro e separada que pode administrar em separado da zona contoso.com.

Se preferir, pode delegar um subdomínio utilizando o [Portal do Azure](delegate-subdomain.md).

> [!NOTE]
> Contoso.com é utilizado como um exemplo no decorrer deste artigo. Substitua o seu nome de domínio por contoso.com.

Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

## <a name="prerequisites"></a>Pré-requisitos

Delegar um subdomínio de DNS do Azure, primeiro tem de delegar o seu domínio público ao DNS do Azure. Ver [delegar um domínio ao DNS do Azure](./dns-delegate-domain-azure-dns.md) para obter instruções sobre como configurar os servidores de nome para a delegação. Assim que o seu domínio é delegado à sua zona DNS do Azure, pode delegar o seu subdomínio.

## <a name="create-a-zone-for-your-subdomain"></a>Criar uma zona para o subdomínio

Em primeiro lugar, crie a zona para o **engenharia** subdomínio.

`New-AzDnsZone -ResourceGroupName <resource group name> -Name engineering.contoso.com`

## <a name="note-the-name-servers"></a>Tenha em atenção os servidores de nomes

Em seguida, tenha em atenção os quatro servidores de nomes para o subdomínio de engenharia.

`Get-AzDnsRecordSet -ZoneName engineering.contoso.com -ResourceGroupName <resource group name> -RecordType NS`

## <a name="create-a-test-record"></a>Criar um registo de teste

Criar uma **A** registos na zona de engenharia para utilizar em testes.

   `New-AzDnsRecordSet -ZoneName engineering.contoso.com -ResourceGroupName <resource group name> -Name www -RecordType A -ttl 3600 -DnsRecords (New-AzDnsRecordConfig -IPv4Address 10.10.10.10)`.

## <a name="create-an-ns-record"></a>Criar um registo NS

Em seguida, crie um registo de servidor (NS) de nome para o **engenharia** zona na zona contoso.com.

```azurepowershell
$Records = @()
$Records += New-AzDnsRecordConfig -Nsdname <name server 1 noted previously>
$Records += New-AzDnsRecordConfig -Nsdname <name server 2 noted previously>
$Records += New-AzDnsRecordConfig -Nsdname <name server 3 noted previously>
$Records += New-AzDnsRecordConfig -Nsdname <name server 4 noted previously>
$RecordSet = New-AzDnsRecordSet -Name engineering -RecordType NS -ResourceGroupName <resource group name> -TTL 3600 -ZoneName contoso.com -DnsRecords $Records
```

## <a name="test-the-delegation"></a>Testar a delegação

Use o nslookup para testar a delegação.

1. Abra uma janela do PowerShell.
2. No prompt de comando, digite `nslookup www.engineering.contoso.com.`
3. Deverá receber uma resposta não autoritativa, que mostra o endereço **10.10.10.10**.

## <a name="next-steps"></a>Passos Seguintes

Saiba como [configurar DNS inverso para os serviços alojados no Azure](dns-reverse-dns-for-azure-services.md).