---
title: Como configurar a base de dados SQL do Azure | Documentos da Microsoft
description: Saiba como configurar e gerir a base de dados do Azure SQL.
services: sql-database
ms.service: sql-database
ms.subservice: service
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: sstein
manager: craigg
ms.date: 01/25/2019
ms.openlocfilehash: 7db9c6400ac7d235153a59965e34e30d9b809a81
ms.sourcegitcommit: 43b85f28abcacf30c59ae64725eecaa3b7eb561a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/09/2019
ms.locfileid: "59359707"
---
# <a name="how-to-use-azure-sql-database"></a>Como utilizar a base de dados do Azure SQL

Nesta seção encontrará várias guias, scripts e explicações que podem ajudar a gerir e configurar a sua base de dados do SQL do Azure. Também encontrará guias de procedimentos específicos para [base de dados individual](sql-database-howto-single-database.md) e [instância gerida](sql-database-howto-managed-instance.md).

## <a name="load-data"></a>Carregar dados

- [Copiar uma base de dados individual ou bases de dados agrupadas no Azure](sql-database-copy.md)
- [Importar uma BD de um BACPAC](sql-database-import.md)
- [Exportar uma BD de um BACPAC](sql-database-export.md)
- [Carregar dados com o BCP](sql-database-load-from-csv-with-bcp.md)
- [Carregar dados com o ADF](../data-factory/connector-azure-sql-database.md?toc=/azure/sql-database/toc.json)

### <a name="data-sync"></a>Sincronização de dados

- [Sincronização de Dados SQL](sql-database-sync-data.md)
- [Agente de Sincronização de Dados](sql-database-data-sync-agent.md)
- [Replicar as alterações do esquema](sql-database-update-sync-schema.md)
- [Monitorizar com o OMS](sql-database-sync-monitor-oms.md)
- [Melhores práticas para a Sincronização de Dados](sql-database-best-practices-data-sync.md)
- [Resolver problemas de Sincronização de Dados](sql-database-troubleshoot-data-sync.md)

## <a name="monitoring-and-tuning"></a>Monitorização e otimização

- [Ajuste manual](sql-database-performance-guidance.md)
- [Utilizar DMVs para monitorizar o desempenho](sql-database-monitoring-with-dmvs.md)
- [Utilizar o Arquivo de consultas para monitorizar o desempenho](sql-database-operate-query-store.md)
- [Resolução de problemas de desempenho com o Intelligent Insights](sql-database-intelligent-insights-troubleshoot-performance.md)
- [Utilizar registo de diagnóstico do Intelligent Insights](sql-database-intelligent-insights-use-diagnostics-log.md)
- [Monitorizar o espaço OLTP dentro da memória](sql-database-in-memory-oltp-monitoring.md)

### <a name="extended-events"></a>Eventos expandidos

- [Eventos expandidos](sql-database-xevent-db-diff-from-svr.md)
- [Store eventos expandidos no arquivo de eventos](sql-database-xevent-code-event-file.md)
- [Eventos expandidos de Store em memória intermédia em anel](sql-database-xevent-code-ring-buffer.md)

## <a name="configure-features"></a>Configurar funcionalidades

- [Configurar a autenticação do Azure AD](sql-database-aad-authentication-configure.md)
- [Configurar o acesso condicional](sql-database-conditional-access.md)
- [Autenticação multifator do AAD](sql-database-ssms-mfa-authentication.md)
- [Configurar a autenticação multifator](sql-database-ssms-mfa-authentication-configure.md)
- [Configurar a política de retenção temporal](sql-database-temporal-tables-retention-policy.md)
- [Configurar o TDE com o BYOK](transparent-data-encryption-byok-azure-sql-configure.md)
- [Rodar chaves BYOK de TDE](transparent-data-encryption-byok-azure-sql-key-rotation.md)
- [Remover o protetor de TDE](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)
- [Configurar o OLTP dentro da memória](sql-database-in-memory-oltp-migration.md)
- [Configurar a Automatização do Azure](sql-database-manage-automation.md)

## <a name="develop-applications"></a>Programar aplicações

- [Conectividade](sql-database-libraries.md)
- [Utilizar o Conector do Spark](sql-database-spark-connector.md)
- [Autenticar aplicação](sql-database-client-id-keys.md)
- [Mensagens de erro](sql-database-develop-error-messages.md)
- [Utilize a criação de batches para um melhor desempenho](sql-database-use-batching-to-improve-performance.md)
- [Orientações para conectividade](sql-database-connectivity-issues.md)
- [Aliases DNS](dns-alias-overview.md)
- [Configurar o alias PowerShell de DNS](dns-alias-powershell.md)
- [Portas - ADO.NET](sql-database-develop-direct-route-ports-adonet-v12.md)
- [C e C ++](sql-database-develop-cplusplus-simple.md)
- [Excel](sql-database-connect-excel.md)

## <a name="design-applications"></a>Conceber aplicações

- [Conceber para a recuperação após desastre](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
- [Conceção para conjuntos elásticos](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)
- [Conceber para atualizações da aplicação](sql-database-manage-application-rolling-upgrade.md)

### <a name="design-multi-tenant-saas-applications"></a>Criar aplicações SaaS de multi-inquilino

- [Padrões de design de SaaS](saas-tenancy-app-design-patterns.md)
- [Indexador de vídeos de SaaS](saas-tenancy-video-index-wingtip-brk3120-20171011.md)
- [Segurança de aplicação SaaS](saas-tenancy-elastic-tools-multi-tenant-row-level-security.md)

## <a name="next-steps"></a>Passos Seguintes

- Saiba mais sobre [guias de procedimentos para instâncias geridas](sql-database-howto-managed-instance.md).
- Saiba mais sobre [guias de procedimentos para bases de dados individuais](sql-database-howto-single-database.md).
