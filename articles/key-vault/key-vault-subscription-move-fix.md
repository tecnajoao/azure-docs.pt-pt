---
title: Alterar o ID de inquilino do Cofre de chaves após a movimentação de uma subscrição - Azure Key Vault | Documentos da Microsoft
description: Saiba como mudar o ID do inquilino para um cofre de chaves depois de mover uma subscrição para um inquilino diferente
services: key-vault
documentationcenter: ''
author: amitbapat
manager: barbkess
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 01/07/2019
ms.author: ambapat
ms.openlocfilehash: a83bff5a494ce338f43b6e967df5fe67cacfab01
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56112194"
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a>Alterar um ID do inquilino do cofre de chaves após a movimentação de uma subscrição

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

## <a name="q-my-subscription-was-moved-from-tenant-a-to-tenant-b-how-do-i-change-the-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a>P: A minha subscrição foi movida do inquilino A para o inquilino B. Como altero o ID do inquilino para o meu cofre de chaves existente e defino os ACLs corretos para os principais no inquilino B?

Ao criar um novo cofre de chaves numa subscrição, é automaticamente associado ao ID de inquilino do Azure Active Directory predefinido nessa subscrição. Todas as entradas de política de acesso também estão associadas a este ID de inquilino. Ao mover a sua subscrição do Azure do inquilino A para o inquilino B, os seus cofres de chaves existentes estão inacessíveis pelos principais (utilizadores e aplicações) no inquilino B. Para corrigir este problema, tem de:

* Alterar o ID de inquilino associado a todos os cofres de chaves existentes nesta subscrição para o inquilino B.
* Remover todas as entradas de política de acesso existentes.
* Adicionar novas entradas de política de acesso que estão associadas ao inquilino B.

Por exemplo, se tiver o cofre de chaves "myvault" numa subscrição que tenha sido movida do inquilino A para o B, saiba como alterar o ID de inquilino para este cofre de chaves e remover as políticas de acesso antigas.

<pre>
Select-AzSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzKeyVault -VaultName myvault).ResourceId
$vault = Get-AzResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

Uma vez que este cofre estava no inquilino A antes da movimentação, o valor original do **$vault. Properties.TenantId** é o inquilino A, while **(Get-AzContext). Tenant.TenantId** é inquilino B.

Agora que o Cofre está associado com o ID de inquilino correto e as entradas de política de acesso antigas foram removidas, defina as novas acesso entradas de política com [Set-AzKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/az.keyvault/Set-azKeyVaultAccessPolicy).

## <a name="next-steps"></a>Passos Seguintes

Se tiver perguntas sobre o Cofre de Chaves do Azure, visite os [Fóruns do Cofre de Chaves do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).
