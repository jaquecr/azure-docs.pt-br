---
title: Desempenho insatisfatório em consultas Apache Hive LLAP no Azure HDInsight
description: As consultas no Apache Hive LLAP estão sendo executadas mais lentamente do que o esperado no Azure HDInsight.
ms.service: hdinsight
ms.topic: troubleshooting
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.date: 07/30/2019
ms.openlocfilehash: ee7ce401f889dd9c06b14860f4fc9674c5350b52
ms.sourcegitcommit: 7863fcea618b0342b7c91ae345aa099114205b03
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93288874"
---
# <a name="scenario-poor-performance-in-apache-hive-llap-queries-in-azure-hdinsight"></a>Cenário: desempenho insatisfatório em consultas de Apache Hive LLAP no Azure HDInsight

Este artigo descreve as etapas de solução de problemas e as possíveis resoluções para problemas ao usar componentes de consulta interativa em clusters do Azure HDInsight.

## <a name="issue"></a>Problema

As configurações de cluster padrão não estão suficientemente ajustadas para sua carga de trabalho. As consultas no hive LLAP estão sendo executadas mais lentamente do que o esperado.

## <a name="cause"></a>Causa

Isso pode ocorrer por vários motivos.

## <a name="resolution"></a>Resolução

LLAP é otimizado para consultas que envolvem junções e agregações. Consultas como as seguintes não têm um bom desempenho em um cluster de Hive interativo:

```
select * from table where column = "columnvalue"
```

Para melhorar o desempenho de consulta de ponto no hive LLAP, defina as seguintes configurações:

```
hive.llap.io.enabled=false; (disable LLAP IO)
hive.optimize.index.filter=false; (disable ORC row index)
hive.exec.orc.split.strategy=BI; (to avoid recombining splits)
```

Você também pode aumentar o uso do cache LLAP para melhorar o desempenho com a seguinte alteração de configuração:

```
hive.fetch.task.conversion=none
```

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [troubleshooting next steps](../../../includes/hdinsight-troubleshooting-next-steps.md)]