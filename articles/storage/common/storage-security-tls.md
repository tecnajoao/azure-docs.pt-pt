---
title: Ativar o TLS segura para o cliente de armazenamento do Azure | Documentos da Microsoft
description: Saiba como ativar o TLS 1.2 no cliente do armazenamento do Azure.
services: storage
author: fhryo-msft
ms.service: storage
ms.topic: article
ms.date: 06/25/2018
ms.author: fryu
ms.subservice: common
ms.openlocfilehash: 4af86b570dfb24f990f1d8b4ff501d1a222bd21d
ms.sourcegitcommit: 5978d82c619762ac05b19668379a37a40ba5755b
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/31/2019
ms.locfileid: "55494294"
---
# <a name="enable-secure-tls-for-azure-storage-client"></a>Ativar o TLS seguro para o cliente do Armazenamento do Azure

Transport Layer Security (TLS) e o Secure Sockets Layer (SSL) são protocolos de criptografia que fornecem segurança de comunicações através de uma rede de computador. Foram encontrados SSL 1.0, 2.0 e 3.0 vulneráveis. Eles têm sido proibidos por RFC. TLS 1.0 torna-se inseguro para usar o bloco cifrado inseguro (DES CBC e RC2 CBC) e cifras de Stream (RC4). Conselho PCI sugeridas, também, a migração para versões do TLS superiores. Para obter mais detalhes, pode ver [Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security#SSL_1.0.2C_2.0_and_3.0).

O armazenamento do Azure foi parado o SSL 3.0 desde 2015 e utiliza o TLS 1.2 no pontos finais públicos do HTTPs, mas o TLS 1.0 e TLS 1.1 ainda são suportados para compatibilidade com versões anteriores.

Para garantir uma ligação segura e em conformidade para o armazenamento do Azure, terá de ativar o TLS 1.2 ou uma versão mais recente no lado do cliente antes de enviar pedidos para operar o serviço de armazenamento do Azure.

## <a name="enable-tls-12-in-net-client"></a>Ativar o TLS 1.2 no cliente do .NET

Para o cliente negociar o TLS 1.2, o sistema operacional e o .NET Framework versão ambos tem oferecer suporte a TLS 1.2. Veja mais detalhes no [suporte para TLS 1.2](https://docs.microsoft.com/dotnet/framework/network-programming/tls#support-for-tls-12).

O exemplo a seguir mostra como ativar o TLS 1.2 no cliente .NET.

```csharp

    static void EnableTls12()
    {
        // Enable TLS 1.2 before connecting to Azure Storage
        System.Net.ServicePointManager.SecurityProtocol = System.Net.SecurityProtocolType.Tls12;

        // Connect to Azure Storage
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName={yourstorageaccount};AccountKey={yourstorageaccountkey};EndpointSuffix=core.windows.net");
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        CloudBlobContainer container = blobClient.GetContainerReference("foo");
        container.CreateIfNotExists();
    }

```

## <a name="enable-tls-12-in-powershell-client"></a>Ativar o TLS 1.2 no cliente do PowerShell

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)] 

O exemplo a seguir mostra como ativar o TLS 1.2 no cliente PowerShell.

```powershell
# Enable TLS 1.2 before connecting to Azure Storage
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12;

$resourceGroup = "{YourResourceGroupName}"
$storageAccountName = "{YourStorageAccountNme}"
$prefix = "foo"

# Connect to Azure Storage
$storageAccount = Get-AzStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccountName
$ctx = $storageAccount.Context
$listOfContainers = Get-AzStorageContainer -Context $ctx -Prefix $prefix
$listOfContainers
```

## <a name="verify-tls-12-connection"></a>Verificar a ligação de TLS 1.2

Para verificar se o TLS 1.2 é usado, na verdade, pode usar o Fiddler. Abra o Fiddler para começar a capturar o tráfego de rede do cliente, em seguida, executar acima de exemplo. Em seguida, pode encontrar a versão do TLS na ligação que o exemplo faz.

Captura de ecrã seguinte é um exemplo para a verificação.

![captura de ecrã de verificação da versão do TLS no Fiddler](./media/storage-security-tls/storage-security-tls-verify-in-fiddler.png)

## <a name="see-also"></a>Consulte também

* [Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security#SSL_1.0.2C_2.0_and_3.0)
* [Conformidade com PCI no TLS](https://blog.pcisecuritystandards.org/migrating-from-ssl-and-early-tls)
* [Ativar o TLS no cliente de Java](https://www.java.com/en/configure_crypto.html)
