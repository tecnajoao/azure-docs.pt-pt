---
title: Conceitos de servidor na base de dados do Azure para PostgreSQL
description: Este artigo fornece considerações e diretrizes para configurar e gerir a base de dados do Azure para servidores PostgreSQL.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 11/07/2018
ms.openlocfilehash: a5b6db9f4bfbe9a11119270e9236580b41fae8c7
ms.sourcegitcommit: 71ee622bdba6e24db4d7ce92107b1ef1a4fa2600
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/17/2018
ms.locfileid: "53540867"
---
# <a name="azure-database-for-postgresql-servers"></a>Base de Dados do Azure para servidores PostgreSQL
Este artigo fornece considerações e diretrizes para trabalhar com a base de dados do Azure para servidores PostgreSQL.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>O que é uma base de dados do Azure para o servidor PostgreSQL?
Uma base de dados do Azure para o servidor PostgreSQL é um ponto administrativo central para várias bases de dados. É a construção de servidor PostgreSQL mesmo que talvez esteja familiarizado com o mundo no local. Especificamente, o serviço PostgreSQL é gerenciado, fornece garantias de desempenho, expõe o acesso e funcionalidades ao nível do servidor.

Uma base de dados do Azure para o servidor PostgreSQL:

- É criado dentro de uma subscrição do Azure.
- É o recurso principal para bases de dados.
- Fornece um espaço de nomes para bases de dados.
- É um contentor com semântica de duração forte - elimine um servidor e elimina as bases de dados contidas.
- Coloca recursos numa região.
- Fornece um ponto final de ligação para o servidor e acesso de base de dados 
- Fornece o âmbito para políticas de gestão que se aplicam às respetivas bases de dados: início de sessão, firewall, os utilizadores, funções, configurações, etc.
- Está disponível em várias versões. Para obter mais informações, consulte [versões de base de dados do PostgreSQL suportadas](concepts-supported-versions.md).
- É extensível por utilizadores. Para obter mais informações, consulte [extensões do PostgreSQL](concepts-extensions.md).

Dentro de uma base de dados do Azure para o servidor PostgreSQL, pode criar uma ou várias bases de dados. Pode optar por criar uma base de dados por servidor para utilizar todos os recursos ou criar várias bases de dados para partilhar os recursos. O preço é estruturado por servidor, com base na configuração do armazenamento (GB), vCores e escalão de preço. Para obter mais informações, consulte [escalões de preço](./concepts-pricing-tiers.md).

## <a name="how-do-i-connect-and-authenticate-to-an-azure-database-for-postgresql-server"></a>Como ligar e autenticar-se para uma base de dados do Azure para o servidor PostgreSQL?
Os seguintes elementos ajudar a garantir um acesso seguro à sua base de dados:

|||
|:--|:--|
| **Autenticação e autorização** | Base de dados do Azure para PostgreSQL server suporta a autenticação de PostgreSQL nativa. Pode ligar e autenticar-se ao servidor com o início de sessão de administrador do servidor. |
| **Protocolo** | O serviço suporta um protocolo baseada em mensagens usado pelo PostgreSQL. |
| **TCP/IP** | O protocolo é suportado por TCP/IP e do protocolo de sockets de domínio Unix. |
| **Firewall** | Para ajudar a proteger os seus dados, uma regra de firewall impede que todos os acessos ao seu servidor e às respetivas bases de dados, até que especifica que computadores têm permissão. Ver [base de dados do Azure para as regras de firewall do servidor PostgreSQL](concepts-firewall-rules.md). |

## <a name="managing-your-server"></a>Gerir o seu servidor
Pode gerir a base de dados do Azure para servidores PostgreSQL utilizando o [portal do Azure](https://portal.azure.com) ou o [CLI do Azure](/cli/azure/postgres).

Ao criar um servidor, defina as credenciais para o seu utilizador de administrador. O utilizador de administrador é o utilizador de privilégio mais alto que tem no servidor. Pertence a azure_pg_admin a função. Esta função não tem permissões de Superutilizador completa. 

O atributo de Superutilizador do PostgreSQL está atribuído a azure_superuser, o qual pertence o serviço gerido. Não tem acesso a esta função.

Uma base de dados do Azure para o servidor PostgreSQL tem bases de dados predefinido: 
- **postgres** -criar uma base de dados padrão pode ligar a vez no seu servidor.
- **azure_maintenance** -esta base de dados é utilizado para separar os processos que fornecem o serviço gerido de ações do usuário. Não tem acesso a esta base de dados.
- **azure_sys** -uma base de dados para o Store de consulta. Esta base de dados não acumulam dados quando a consulta Store está desativado; Esta é a predefinição. Para obter mais informações, consulte a [descrição geral de consulta Store](concepts-query-store.md).


## <a name="server-parameters"></a>Parâmetros do servidor
Os parâmetros do servidor PostgreSQL determinam a configuração do servidor. Na base de dados do Azure para PostgreSQL, a lista de parâmetros pode ser visualizada e editados através do portal do Azure ou a CLI do Azure. 

Como um serviço gerido para Postgres, os parâmetros configuráveis na base de dados do Azure para PostgreSQL são um subconjunto dos parâmetros numa instância de Postgres local (para obter mais informações sobre os parâmetros de Postgres, consulte o [documentação do PostgreSQL](https://www.postgresql.org/docs/9.6/static/runtime-config.html)). A base de dados do Azure para o servidor PostgreSQL está ativado com valores predefinidos para cada parâmetro após a criação. Alguns parâmetros que necessitem de um servidor reiniciar ou acesso de Superutilizador para que as alterações entrem em vigor não pode ser configurado pelo utilizador.


## <a name="next-steps"></a>Passos Seguintes
- Para uma descrição geral do serviço, consulte [base de dados do Azure para PostgreSQL descrição-geral](overview.md).
- Para obter informações sobre recursos específicos quotas e limitações com base no seu **escalão de serviço**, consulte [escalões de serviço](concepts-pricing-tiers.md).
- Para obter informações sobre como ligar ao serviço, consulte [bibliotecas de ligação para base de dados do Azure para PostgreSQL](concepts-connection-libraries.md).
- Ver e editar os parâmetros do servidor por meio [portal do Azure](howto-configure-server-parameters-using-portal.md) ou [CLI do Azure](howto-configure-server-parameters-using-cli.md).
