---
title: Recursos para o desenvolvimento de um pool SQL dedicado no Azure Synapse Analytics
description: Conceitos de desenvolvimento, decisões de design, recomendações e técnicas de codificação para um pool SQL dedicado no Azure Synapse Analytics.
services: synapse-analytics
author: XiaoyuMSFT
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql-dw
ms.date: 08/29/2018
ms.author: xiaoyul
ms.reviewer: igorstan
ms.openlocfilehash: f158655cd7aeba647480325966c7f0cfcf65b13c
ms.sourcegitcommit: 96918333d87f4029d4d6af7ac44635c833abb3da
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2020
ms.locfileid: "93322147"
---
# <a name="design-decisions-and-coding-techniques-for-a-dedicated-sql-pool-in-azure-synapse-analytics"></a>Decisões de design e técnicas de codificação para um pool SQL dedicado no Azure Synapse Analytics 

 Neste artigo, você encontrará recursos adicionais para ajudá-lo a entender melhor as principais decisões de design, recomendações e técnicas de codificação para um pool SQL dedicado no Azure Synapse.

## <a name="key-design-decisions"></a>Principais decisões de design

Os artigos a seguir destacam os conceitos e as decisões de design para o desenvolvimento de um data warehouse distribuído usando o recurso de pool dedicado do SQL no Azure Synapse:

* [conexões](../sql/connect-overview.md)
* [concurrency](resource-classes-for-workload-management.md)
* [transações](sql-data-warehouse-develop-transactions.md)
* [esquemas definidos pelo usuário](sql-data-warehouse-develop-user-defined-schemas.md)
* [distribuição de tabela](sql-data-warehouse-tables-distribute.md)
* [índices de tabela](sql-data-warehouse-tables-index.md)
* [partições de tabela](sql-data-warehouse-tables-partition.md)
* [CTAS](sql-data-warehouse-develop-ctas.md)
* [estatística](sql-data-warehouse-tables-statistics.md)

## <a name="development-recommendations-and-coding-techniques"></a>Recomendações para o desenvolvimento e técnicas de codificação

Os artigos a seguir apresentam técnicas de codificação específicas, dicas e recomendações para o desenvolvimento de um pool SQL dedicado:

* [procedimentos armazenados](sql-data-warehouse-develop-stored-procedures.md)
* [las](sql-data-warehouse-develop-label.md)
* [modos de exibição](performance-tuning-materialized-views.md)
* [tabelas temporárias](sql-data-warehouse-tables-temporary.md)
* [SQL dinâmico](sql-data-warehouse-develop-dynamic-sql.md)
* [loop](sql-data-warehouse-develop-loops.md)
* [Agrupar por opções](sql-data-warehouse-develop-group-by-options.md)
* [atribuição de variável](sql-data-warehouse-develop-variable-assignment.md)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações de referência, consulte [instruções T-SQL](sql-data-warehouse-reference-tsql-statements.md).
