---
title: Azure Monitor Application Insights Java
description: Monitoramento do desempenho de aplicativos para aplicativos Java em execução em qualquer ambiente sem a necessidade de modificação de código. Rastreamento distribuído e mapa de aplicativos.
ms.topic: conceptual
ms.date: 03/29/2020
ms.openlocfilehash: 2459f80746d95234701319bbb5142c8e540890d3
ms.sourcegitcommit: 8a1ba1ebc76635b643b6634cc64e137f74a1e4da
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94379762"
---
# <a name="java-codeless-application-monitoring-azure-monitor-application-insights"></a>Azure Monitor de monitoramento de aplicativos com código Java Application Insights

O monitoramento de aplicativos sem código Java é bastante simples – não há alterações de código e o agente Java pode ser habilitado com apenas algumas alterações de configuração.

 O agente do Java funciona em qualquer ambiente e permite que você monitore todos os seus aplicativos Java. Em outras palavras, se você estiver executando seus aplicativos Java em VMs, no local, no AKS, no Windows, no Linux, você deve nomeá-lo, o agente do Java 3,0 monitorará seu aplicativo.

Adicionar o SDK do Java Application Insights ao seu aplicativo não é mais necessário, pois o agente 3,0 coleta automaticamente solicitações, dependências e logs por conta própria.

Você ainda pode enviar telemetria personalizada do seu aplicativo. O agente 3,0 irá rastreá-lo e correlacioná-lo junto com toda a telemetria concolhida.

O agente 3,0 dá suporte a Java 8 e superior.

## <a name="quickstart"></a>Início Rápido

**1. baixar o agente**

> [!WARNING]
> **Se você estiver atualizando da versão prévia do 3,0**
>
> Examine todas as [Opções de configuração](./java-standalone-config.md) com cuidado, pois a estrutura JSON foi completamente alterada, além do próprio nome de arquivo, que ficou com todas as letras minúsculas.

Baixar [applicationinsights-Agent-3.0.0. jar](https://github.com/microsoft/ApplicationInsights-Java/releases/download/3.0.0/applicationinsights-agent-3.0.0.jar)

**2. aponte a JVM para o agente**

Adicionar `-javaagent:path/to/applicationinsights-agent-3.0.0.jar` aos argumentos JVM de seu aplicativo

Os argumentos de JVM típicos incluem `-Xmx512m` e `-XX:+UseG1GC` . Portanto, se você souber onde adicioná-los, já saberá onde adicioná-los.

Para obter ajuda adicional sobre como configurar os argumentos JVM de seu aplicativo, consulte [dicas para atualizar seus argumentos JVM](./java-standalone-arguments.md).

**3. aponte o agente para o recurso de Application Insights**

Se você ainda não tiver um recurso de Application Insights, poderá criar um novo seguindo as etapas no guia de criação de [recursos](./create-new-resource.md).

Aponte o agente para o recurso de Application Insights, definindo uma variável de ambiente:

```
APPLICATIONINSIGHTS_CONNECTION_STRING=InstrumentationKey=...
```

Ou criando um arquivo de configuração chamado `applicationinsights.json` e colocando-o no mesmo diretório que `applicationinsights-agent-3.0.0.jar` o, com o seguinte conteúdo:

```json
{
  "instrumentationSettings": {
    "connectionString": "InstrumentationKey=..."
  }
}
```

Você pode encontrar a cadeia de conexão em seu recurso de Application Insights:

:::image type="content" source="media/java-ipa/connection-string.png" alt-text="Application Insights cadeia de conexão":::

**4. isso é tudo!**

Agora, inicie seu aplicativo e vá para o recurso de Application Insights no portal do Azure para ver os dados de monitoramento.

> [!NOTE]
> Pode levar alguns minutos para que os dados de monitoramento sejam exibidos no Portal.


## <a name="configuration-options"></a>Opções de configuração

No `applicationinsights.json` arquivo, você também pode configurar:

* Nome da função de nuvem
* Instância de função de nuvem
* amostragem
* Métricas JMX
* Dimensões personalizadas
* Processadores de telemetria
* Registro em log coletado automaticamente
* Métricas de micrometer coletadas automaticamente (incluindo as métricas do acionador do Spring boot)
* Pulsação
* Proxy HTTP
* Autodiagnóstico

Consulte [Opções de configuração](./java-standalone-config.md) para obter detalhes completos.

## <a name="autocollected-requests-dependencies-logs-and-metrics"></a>Solicitações, dependências, logs e métricas concolhidas.

### <a name="requests"></a>Requests

* Consumidores JMS
* Consumidores de Kafka
* De sub-rede/webfluxo
* Servlets
* Agendamento Spring

### <a name="dependencies-with-distributed-trace-propagation"></a>Dependências com propagação de rastreamento distribuído

* Apache HttpClient e HttpAsyncClient
* gRPC
* Java. net. HttpURLConnection
* JMS
* Kafka
* Cliente de sub-rede
* OkHttp

### <a name="other-dependencies"></a>Outras dependências

* Cassandra
* JDBC
* MongoDB (assíncrono e sincronizado)
* Redis (lettuce e Jedis)

### <a name="logs"></a>Logs

* Java. util. Logging
* Log4J (incluindo propriedades MDC)
* SLF4J/Logback (incluindo propriedades MDC)

### <a name="metrics"></a>Métricas

* Micrometer (incluindo as métricas do acionador do Spring boot)
* Métricas JMX

## <a name="sending-custom-telemetry-from-your-application"></a>Enviando telemetria personalizada do seu aplicativo

Nossa meta no 3.0 + é permitir que você envie sua telemetria personalizada usando APIs padrão.

Damos suporte ao micrometer, à API OpenTelemetry e às estruturas de log populares. Application Insights Java 3,0 capturará automaticamente a telemetria e a correlacionará junto com toda a telemetria coletada automaticamente.

### <a name="supported-custom-telemetry"></a>Telemetria personalizada com suporte

A tabela a seguir representa os tipos de telemetria personalizados com suporte no momento que você pode habilitar para complementar o agente do Java 3,0. Para resumir, há suporte para métricas personalizadas por meio de micrometer, exceções e rastreamentos personalizados podem ser habilitados por meio de estruturas de log e qualquer tipo de telemetria personalizada tem suporte por meio do [SDK Application insights Java 2. x](#sending-custom-telemetry-using-application-insights-java-sdk-2x). 

|                     | Micrometer | Log4J, logback, JUL | SDK 2. x |
|---------------------|------------|---------------------|---------|
| **Eventos personalizados**   |            |                     |  Sim    |
| **Métricas personalizadas**  |  Sim       |                     |  Sim    |
| **Dependências**    |            |                     |  Sim    |
| **Exceções**      |            |  Sim                |  Sim    |
| **Visualizações de página**      |            |                     |  Sim    |
| **Solicitações**        |            |                     |  Sim    |
| **Rastreamentos**          |            |  Sim                |  Sim    |

Não estamos planejando lançar um SDK com o Application Insights 3,0 no momento.

Application Insights Java 3,0 já está escutando a telemetria que é enviada para o Application Insights SDK 2. x do Java. Essa funcionalidade é uma parte importante da história de atualização para usuários existentes de 2. x e preenche uma lacuna importante em nosso suporte de telemetria personalizado até que a API OpenTelemetry seja GA.

## <a name="sending-custom-telemetry-using-application-insights-java-sdk-2x"></a>Enviando telemetria personalizada usando Application Insights SDK do Java 2. x

Adicione `applicationinsights-core-2.6.0.jar` ao seu aplicativo (todas as versões 2. x têm suporte pelo Application insights Java 3,0, mas vale a pena usar a mais recente se você tiver uma opção):

```xml
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-core</artifactId>
    <version>2.6.0</version>
  </dependency>
```

Criar um TelemetryClient:

  ```java
private static final TelemetryClient telemetryClient = new TelemetryClient();
```

e usá-lo para enviar telemetria personalizada.

### <a name="events"></a>Eventos

  ```java
telemetryClient.trackEvent("WinGame");
```
### <a name="metrics"></a>Métricas

Você pode enviar telemetria de métricas via [micrometer](https://micrometer.io):

```java
  Counter counter = Metrics.counter("test_counter");
  counter.increment();
```

Ou você também pode usar Application Insights Java SDK 2. x:

```java
  telemetryClient.trackMetric("queueLength", 42.0);
```

### <a name="dependencies"></a>Dependências

```java
  boolean success = false;
  long startTime = System.currentTimeMillis();
  try {
      success = dependency.call();
  } finally {
      long endTime = System.currentTimeMillis();
      RemoteDependencyTelemetry telemetry = new RemoteDependencyTelemetry();
      telemetry.setTimestamp(new Date(startTime));
      telemetry.setDuration(new Duration(endTime - startTime));
      telemetryClient.trackDependency(telemetry);
  }
```

### <a name="logs"></a>Logs
Você pode enviar telemetria de log personalizada por meio de sua estrutura de registro em log favorita.

Ou você também pode usar Application Insights Java SDK 2. x:

```java
  telemetryClient.trackTrace(message, SeverityLevel.Warning, properties);
```

### <a name="exceptions"></a>Exceções
Você pode enviar telemetria de exceção personalizada por meio de sua estrutura de registro em log favorita.

Ou você também pode usar Application Insights Java SDK 2. x:

```java
  try {
      ...
  } catch (Exception e) {
      telemetryClient.trackException(e);
  }
```

## <a name="upgrading-from-application-insights-java-sdk-2x"></a>Atualizando do SDK do Java do Application Insights 2. x

Se você já estiver usando Application Insights Java SDK 2. x em seu aplicativo, não será necessário removê-lo.
O agente do Java 3,0 o detectará e irá capturar e correlacionar qualquer telemetria personalizada que você estiver enviando por meio do SDK do Java 2. x, ao mesmo tempo em que suprimirá qualquer coleção automática executada pelo SDK do Java 2. x para evitar a telemetria duplicada.

Se você estiver usando o agente Application Insights 2. x, será necessário remover o `-javaagent:` ARG JVM que estava apontando para o agente 2. x.

> [!NOTE]
> O Java SDK 2. x TelemetryInitializers e o TelemetryProcessors não serão executados ao usar o agente 3,0.
> Muitos dos casos de uso exigidos anteriormente podem ser resolvidos em 3,0 Configurando [dimensões personalizadas](./java-standalone-config.md#custom-dimensions) ou configurando [processadores de telemetria](./java-standalone-telemetry-processors.md).

> [!NOTE]
> 3,0 não oferece suporte a várias chaves de instrumentação em uma única JVM ainda.
