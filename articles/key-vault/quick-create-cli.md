---
title: Início Rápido do Azure - Definir e obter um segredo do Key Vault com a CLI do Azure | Microsoft Docs
description: Início Rápido que mostra como definir e obter um segredo do Azure Key Vault com a CLI do Azure
services: key-vault
author: barclayn
manager: barbkess
tags: azure-resource-manager
ms.assetid: 4acc894f-fee0-4c2f-988e-bc0eceea5eda
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: quickstart
ms.custom: mvc
ms.date: 01/08/2019
ms.author: barclayn
ms.openlocfilehash: 8065f670da6614db8c3524fd351a31ad095f8257
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56113044"
---
# <a name="quickstart-set-and-retrieve-a-secret-from-azure-key-vault-using-azure-cli"></a>Início rápido: Definir e obter um segredo a partir do Azure Key Vault com a CLI do Azure

O Azure Key Vault é um serviço cloud que funciona como um arquivo de segredos seguro. Pode armazenar chaves, palavras-passe, certificados e outros segredos em segurança. Para obter mais informações sobre o Key Vault, pode ver a [Descrição Geral](key-vault-overview.md). A CLI do Azure é utilizada para criar e gerir recursos do Azure através de comandos ou scripts. Neste início rápido, vai criar um cofre de chaves. Depois de concluir este passo, irá armazenar um segredo.

Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-try-it.md)]

Se optar por instalar e utilizar a CLI localmente, este início rápido requer a versão 2.0.4 ou posterior da CLI do Azure. Executar `az --version` para localizar a versão. Se precisar de instalar ou atualizar, veja [Instalar a CLI do Azure]( /cli/azure/install-azure-cli).

Para iniciar sessão no Azure com a CLI, pode escrever:

```azurecli
az login
```

Para obter mais informações sobre as opções de início de sessão através da CLI dar uma olhada [iniciar sessão com a CLI do Azure](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest)

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Um grupo de recursos é um contentor lógico no qual os recursos do Azure são implementados e geridos. O exemplo seguinte cria um grupo de recursos com o nome *ContosoResourceGroup* na localização *eastus*.

```azurecli
az group create --name "ContosoResourceGroup" --location eastus
```

## <a name="create-a-key-vault"></a>Criar um Key Vault

A seguir, vai criar um Key Vault no grupo de recursos criado no passo anterior. Terá de fornecer algumas informações:

- Para este início rápido, utilizamos **Contoso-vault2**. Tem de fornecer um nome exclusivo no teste.
- **ContosoResourceGroup** como o nome do grupo de recursos.
- **E.U.A. Leste** como a localização.

```azurecli
az keyvault create --name "Contoso-Vault2" --resource-group "ContosoResourceGroup" --location eastus
```

O resultado deste cmdlet mostra as propriedades do Key Vault recém-criado. Tome nota das duas propriedades listadas abaixo:

- **Nome do cofre**: No exemplo, isto é **Contoso-Vault2**. Irá utilizar este nome para outros comandos do Key Vault.
- **URI do cofre**: No exemplo, isto é https://contoso-vault2.vault.azure.net/. As aplicações que utilizam o cofre através da respetiva API têm de utilizar este URI.

Nesta altura, a sua conta do Azure é a única autorizada a realizar quaisquer operações neste novo cofre.

## <a name="add-a-secret-to-key-vault"></a>Adicionar um segredo ao Key Vault

Para adicionar um segredo ao cofre, apenas tem de efetuar alguns passos adicionais. Esta palavra-passe pode ser utilizada por uma aplicação. A palavra-passe será chamada **ExamplePassword** e irá armazenar o valor de **hVFkk965BuUv** nela.

Escreva os comandos abaixo para criar um segredo no Key Vault denominado **ExamplePassword** que irá armazenar o valor **hVFkk965BuUv** :

```azurecli
az keyvault secret set --vault-name "Contoso-Vault2" --name "ExamplePassword" --value "hVFkk965BuUv"
```

Agora, pode referenciar esta palavra-passe que adicionou ao Azure Key Vault com o respetivo URI. Utilize **https://ContosoVault.vault.azure.net/secrets/ExamplePassword** para obter a versão atual. 

Para ver o valor contido no segredo como texto simples:

```azurecli
az keyvault secret show --name "ExamplePassword" --vault-name "Contoso-Vault2"
```

Agora, criou um Key Vault, armazenou um segredo e obteve-o.

## <a name="clean-up-resources"></a>Limpar recursos

Outros inícios rápidos e tutoriais desta coleção têm por base este início rápido. Se quiser continuar a trabalhar com os inícios rápidos e tutoriais subsequentes, pode manter estes recursos.
Quando já não forem necessários, pode utilizar o comando [az group delete](/cli/azure/group) para remover o grupo de recursos e todos os recursos relacionados. Pode eliminar os recursos da seguinte forma:

```azurecli
az group delete --name ContosoResourceGroup
```

## <a name="next-steps"></a>Passos Seguintes

Neste início rápido, criou um Key Vault e armazenou um segredo. Para saber mais sobre o Key Vault e como utilizá-lo com as suas aplicações, avance para o tutorial referente às aplicações Web que funcionam com o Key Vault.

> [!div class="nextstepaction"]
> Para saber como ler um segredo a partir do Key Vault através de uma aplicação Web com identidades geridas para recursos do Azure, avance para o tutorial[Configurar uma aplicação Web do Azure para ler um segredo a partir do Key Vault](quick-create-net.md)
