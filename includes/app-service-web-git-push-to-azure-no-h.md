---
title: incluir ficheiro
description: incluir ficheiro
services: app-service
author: cephalin
ms.service: app-service
ms.topic: include
ms.date: 02/02/2018
ms.author: cephalin
ms.custom: include file
ms.openlocfilehash: aa6f18d4f667862687083c5db3679ce9d8e188cd
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56213152"
---
Regresse à _janela de terminal local_ e adicione um remoto do Azure ao seu repositório Git local. Substitua _&lt;deploymentLocalGitUrl-from-create-step>_ pelo URL do Git remoto que guardou em [Criar uma aplicação Web](#create-a-web-app).

```bash
git remote add azure <deploymentLocalGitUrl-from-create-step>
```

Envie para o remoto do Azure para implementar a sua aplicação com o comando seguinte. Quando lhe forem pedidas credenciais pelo Gestor de credenciais do Git, certifique-se de que introduz as credenciais que criou em configurar um utilizador de implementação, não as credenciais de que utiliza para iniciar sessão no portal do Azure.

```bash
git push azure master
```

Este comando pode demorar alguns minutos a ser executado. Ao executar, apresenta informações semelhantes ao exemplo seguinte:
