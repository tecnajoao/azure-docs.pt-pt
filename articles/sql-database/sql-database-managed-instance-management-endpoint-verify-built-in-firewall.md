---
title: Detetar o firewall interno da instância gerida da base de dados SQL do Azure | Documentos da Microsoft
description: Saiba como verificar a proteção de firewall interno na instância gerida da base de dados SQL do Azure.
services: sql-database
ms.service: sql-database
ms.subservice: managed-instance
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: srdan-bozovic-msft
ms.author: srbozovi
ms.reviewer: sstein, carlrab
manager: craigg
ms.date: 12/04/2018
ms.openlocfilehash: 774455a2901782ef52b213c6a13c17636e28b1a4
ms.sourcegitcommit: 43b85f28abcacf30c59ae64725eecaa3b7eb561a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/09/2019
ms.locfileid: "59356696"
---
# <a name="verifying-the-managed-instance-built-in-firewall"></a>A verificar o firewall interno da instância gerida

A instância gerida [regras de segurança de entrada obrigatória](sql-database-managed-instance-connectivity-architecture.md#mandatory-inbound-security-rules) precisa de portas de gestão 9000, 9003, 1438, 1440, 1452 ser abrir a partir do **qualquer origem** em segurança de rede grupo (NSG) que protege a gerida Instância. Embora estas portas estão abertas no nível do NSG, estão protegidos ao nível da rede, o firewall interno.

## <a name="verify-firewall"></a>Certifique-se a firewall

Para verificar se estas portas, utilize qualquer ferramenta de scanner de segurança para testar estas portas. Captura de ecrã seguinte mostra como usar uma dessas ferramentas.

![Verificar o firewall interno](./media/sql-database-managed-instance-management-endpoint/03_verify_firewall.png)

## <a name="next-steps"></a>Passos Seguintes

Para obter mais informações sobre as instâncias geridas e a conectividade, consulte [arquitetura de conectividade de instância de geridas da base de dados do SQL Azure](sql-database-managed-instance-connectivity-architecture.md).