---
title: Coletar fontes de dados de log de eventos do Windows com Log Analytics Agent no Azure Monitor
description: Descreve como configurar a coleta de logs de Eventos do Windows pelo Azure Monitor e detalhes dos registros criados.
ms.subservice: logs
ms.topic: conceptual
author: bwren
ms.author: bwren
ms.date: 10/21/2020
ms.openlocfilehash: 109e96f862ec2f3ddf879bccba114c44aecfe3c8
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92440596"
---
# <a name="collect-windows-event-log-data-sources-with-log-analytics-agent"></a>Coletar fontes de dados de log de eventos do Windows com o agente de Log Analytics
Os logs de eventos do Windows são uma das [fontes de dados](agent-data-sources.md) mais comuns para agentes de log Analytics em máquinas virtuais do Windows, já que muitos aplicativos gravam no log de eventos do Windows.  Você pode coletar eventos de logs padrão como do sistema e aplicativo além de especificar todos os logs personalizados criados por aplicativos que você precisa monitorar.

> [!IMPORTANT]
> Este artigo aborda a coleta de eventos do Windows com o [agente de log Analytics](log-analytics-agent.md) , que é um dos agentes usados pelo Azure monitor. Outros agentes coletam dados diferentes e são configurados de forma diferente. Consulte [visão geral dos agentes de Azure monitor](agents-overview.md) para obter uma lista dos agentes disponíveis e os dados que eles podem coletar.

![Eventos do Windows](media/data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Configurando os logs de eventos do Windows
Configure logs de eventos do Windows no [menu dados em configurações avançadas](agent-data-sources.md#configuring-data-sources) para o espaço de trabalho log Analytics.

O Azure Monitor coleta apenas os eventos dos logs de eventos do Windows especificados nas configurações.  Você pode adicionar um log de eventos digitando o nome do log e clicando em **+** .  Para cada log, somente eventos com as severidades selecionadas são coletados.  Marque as severidades para o log específico que você deseja coletar.  Você não pode fornecer quaisquer critérios adicionais para filtrar eventos.

Conforme você digita o nome de um log de eventos, o Azure Monitor fornece sugestões de nomes comuns de log de eventos. Se o log que você deseja adicionar não aparecer na lista, você ainda poderá adicioná-lo digitando o nome completo do log. Você pode encontrar o nome completo do log usando o visualizador de eventos. No visualizador de eventos, abra a página *Propriedades* para o log e copie a cadeia de caracteres do campo *Nome Completo*.

![Configurar eventos do Windows](media/data-sources-windows-events/configure.png)

> [!NOTE]
> Os eventos críticos do log de eventos do Windows terão uma severidade de "erro" nos logs de Azure Monitor.

## <a name="data-collection"></a>Coleta de dados
O Azure Monitor coleta cada evento que corresponde a uma severidade selecionada de um log de eventos monitorado, conforme o evento é criado.  O agente registra seu lugar em cada log de eventos do qual ele realiza a coleta.  Se o agente ficar offline por um período, ele coletará os eventos de onde ele parou, mesmo se os eventos foram criados enquanto o agente estava offline.  Há a probabilidade de que os eventos não sejam coletados se o log de eventos é encapsulado com eventos não coletados sendo substituídos enquanto o agente estiver offline.

>[!NOTE]
>O Azure Monitor não coleta eventos de auditoria criados pelo SQL Server do *MSSQLSERVER* de origem com a ID de evento 18453 que contenham as palavras-chave *Clássico* ou *Êxito de Auditoria* e a palavra-chave *0xa0000000000000*.
>

## <a name="windows-event-records-properties"></a>Propriedades de registros de eventos do Windows
Os registros de eventos do Windows têm um tipo de **evento** e têm as propriedades na tabela a seguir:

| Propriedade | Descrição |
|:--- |:--- |
| Computador |Nome do computador do qual o evento foi coletado. |
| EventCategory |Categoria do evento. |
| EventData |Todos os dados de evento em formato bruto. |
| EventID |Número do evento. |
| EventLevel |Severidade do evento em formato numérico. |
| EventLevelName |Severidade do evento em formato de texto. |
| EventLog |Nome do log de eventos do qual o evento foi coletado. |
| ParameterXml |Valores de parâmetro de evento em formato XML. |
| ManagementGroupName |Nome do grupo de gerenciamento para agentes do System Center Operations Manager.  Para outros agentes, esse valor é `AOI-<workspace ID>` |
| RenderedDescription |Descrição do evento com valores de parâmetro |
| Fonte |Origem do evento. |
| SourceSystem |Tipo de agente do qual o evento foi coletado. <br> OpsManager - agente do Windows: conexão direta ou Operations Manager gerenciado <br>  Linux: todos os agentes do Linux  <br>  AzureStorage: Diagnóstico do Azure |
| TimeGenerated |Data e hora em que o evento foi criado no Windows. |
| UserName |Nome de usuário da conta que registrou o evento. |

## <a name="log-queries-with-windows-events"></a>Consultas de log com Eventos do Windows
A tabela a seguir fornece diferentes exemplos de consultas de log que recuperam registros de Eventos do Windows.

| Consulta | Descrição |
|:---|:---|
| Evento |Todos os eventos do Windows. |
| Event &#124; where EventLevelName == "error" |Todos os eventos do Windows com severidade de erro. |
| Event &#124; summarize count() by Source |Contagem de eventos do Windows por fonte. |
| Event &#124; where EventLevelName == "error" &#124; summarize count() by Source |Contagem de eventos de erro do Windows por fonte. |


## <a name="next-steps"></a>Próximas etapas
* Configure o Log Analytics para coletar outras [fontes de dados](agent-data-sources.md) para análise.
* Saiba mais sobre [registrar consultas](../log-query/log-query-overview.md) para analisar os dados coletados de fontes de dados e soluções.  
* Configure a [coleta de contadores de desempenho](data-sources-performance-counters.md) de seus agentes do Windows.
