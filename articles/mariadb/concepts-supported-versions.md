---
title: Versões suportadas na base de dados do Azure para MariaDB
description: Descreve as versões suportadas na base de dados do Azure para MariaDB.
author: ajlam
ms.author: andrela
ms.service: mariadb
ms.topic: conceptual
ms.date: 09/24/2018
ms.openlocfilehash: 69330e9d5a05fbcc892889f70a04f5eb4a4a2fb9
ms.sourcegitcommit: 71ee622bdba6e24db4d7ce92107b1ef1a4fa2600
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/17/2018
ms.locfileid: "53541426"
---
# <a name="supported-azure-database-for-mariadb-server-versions"></a>Suporte base de dados do Azure para MariaDB versões de servidor
Base de dados do Azure para MariaDB foi desenvolvido a partir de open source [MariaDB servidor](https://downloads.mariadb.org/), usando o mecanismo de InnoDB. Atualmente, a base de dados do Azure para MariaDB suporta a versão seguinte:

## <a name="mariadb-version-10217"></a>Versão de MariaDB 10.2.17
Consulte a [MariaDB documentação](https://downloads.mariadb.org/mariadb/10.2.17/) para obter mais informações sobre melhorias e correções MariaDB 10.2.17.

> [!NOTE]
> No serviço, um gateway é utilizado para redirecionar as ligações para instâncias de servidor. Depois da ligação é estabelecida, o cliente do MySQL apresenta a versão do MariaDB definida no gateway, não a versão real em execução na sua instância de servidor MariaDB. Para determinar a versão da sua instância de servidor MariaDB, utilize o `SELECT VERSION();` comando na linha de comandos MySQL.

## <a name="managing-updates-and-upgrades"></a>Gerenciando atualizações e atualizações
O serviço gere automaticamente a aplicação de patches para as atualizações de versão secundária.

## <a name="next-steps"></a>Passos Seguintes
Para obter informações sobre recursos específicos quotas e limitações com base no seu **escalão de serviço**, consulte [escalões de serviço](./concepts-pricing-tiers.md)
