---
title: O Azure AD v2 Windows Desktop introdução iniciada - Config | Documentos da Microsoft
description: Como uma aplicação .NET de Desktop do Windows (XAML) pode obter um token de acesso e chamar uma API protegida pelo ponto de final do Azure Active Directory v2.
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.collection: M365-identity-device-management
ms.openlocfilehash: dc9b5cbc4904c6b2238e56742381feb4d2811437
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/13/2019
ms.locfileid: "56195826"
---
# <a name="add-the-applications-registration-information-to-your-app"></a>Adicionar informações de registo da aplicação à sua aplicação
Neste passo, terá de adicionar o Id da aplicação ao seu projeto.

1.  Open `App.xaml.cs` e substitua a linha que contém o `ClientId` com:

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a>O que é o seguinte

[!INCLUDE [Test and Validate](../../../../includes/active-directory-develop-guidedsetup-windesktop-test.md)]
