---
title: Atribuir variáveis com Synapse SQL
description: Neste artigo, você encontrará dicas para atribuir variáveis T-SQL com Synapse SQL.
services: synapse-analytics
author: azaricstefan
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql
ms.date: 04/15/2020
ms.author: v-stazar
ms.reviewer: jrasnick
ms.openlocfilehash: abc0a9f6fa6baefc7cc4b29c84ff179f0851dc30
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "90028909"
---
# <a name="assign-variables-with-synapse-sql"></a>Atribuir variáveis com Synapse SQL

Neste artigo, você encontrará dicas para atribuir variáveis T-SQL com Synapse SQL.

## <a name="set-variables-with-declare"></a>Definir variáveis com DECLARE

Variáveis em Synapse SQL são definidas usando a `DECLARE` instrução ou a `SET` instrução. Inicializar variáveis com DECLARE é uma das maneiras mais flexíveis de definir um valor de variável em Synapse SQL.

```sql
DECLARE @v  int = 0
;
```

Você também pode usar DECLARE para definir mais de uma variável por vez. Você não pode usar SELECT ou UPDATE para fazer o seguinte:

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

Você não pode inicializar e usar uma variável na mesma instrução DECLARE. Para ilustrar, o exemplo a seguir não é permitido, pois * \@ P1* é inicializado e usado na mesma instrução Declare. O exemplo a seguir apresenta um erro.

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="set-values-with-set"></a>Definir valores com SET

SET é um método comum para definir uma única variável.

As instruções a seguir sempre são maneiras válidas de definir uma variável com SET:

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

Você só pode definir uma variável por vez com SET. No entanto, os operadores compostos são permitidos.

## <a name="limitations"></a>Limitações

Você não pode usar UPDATE para atribuição de variável.

## <a name="next-steps"></a>Próximas etapas

Para obter mais dicas de desenvolvimento, consulte o artigo [visão geral do desenvolvimento do Synapse SQL](develop-overview.md) .
