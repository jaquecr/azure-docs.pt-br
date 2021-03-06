---
author: rothja
ms.service: app-service
ms.topic: include
ms.date: 03/04/2020
ms.author: jroth
ms.openlocfilehash: 800dc50f82fa47228f1a88a143c5b515168812a6
ms.sourcegitcommit: 3e8058f0c075f8ce34a6da8db92ae006cc64151a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92755777"
---
| Recurso | Grátis | Compartilhado | Basic | Standard | Premium (v3) | Isolado </th> |
| --- | --- | --- | --- | --- | --- | --- |
| [Aplicativos Web, móveis ou de API](https://azure.microsoft.com/services/app-service/) por [plano do Serviço de Aplicativo do Azure](../articles/app-service/overview-hosting-plans.md)<sup>1</sup> |10 |100 |Ilimitado<sup>2</sup> |Ilimitado<sup>2</sup> |Ilimitado<sup>2</sup> |Ilimitado<sup>2</sup>|
| [Plano do Serviço de Aplicativo](../articles/app-service/overview-hosting-plans.md) |10 por região |10 por grupo de recursos |100 por grupo de recursos |100 por grupo de recursos |100 por grupo de recursos |100 por grupo de recursos|
| Tipo de instância de computação |Compartilhado |Compartilhado |Dedicado<sup>3</sup> |Dedicado<sup>3</sup> |Dedicado<sup>3</sup></p> |Dedicado<sup>3</sup>|
| [Aumentar](../articles/app-service/manage-scale-up.md) (máximo de instâncias) |1 compartilhada |1 compartilhada |3 dedicados<sup>3</sup> |10 dedicados<sup>3</sup> |30 dedicados<sup>3</sup>|100 dedicados<sup>4</sup>|
| Armazenamento<sup>5</sup> |1 GB<sup>5</sup> |1 GB<sup>5</sup> |10 GB<sup>5</sup> |50 GB<sup>5</sup> |250 GB<sup>5</sup> <br/><br/> Para mais de 250 GB, envie uma solicitação de suporte. |1 TB<sup>5</sup> <br/><br/> A cota de armazenamento disponível é de 999 GB. |
| Tempo de CPU (5 minutos)<sup>6</sup> |3 minutos |3 minutos |Ilimitado, pagamento das [tarifas](https://azure.microsoft.com/pricing/details/app-service/)</a> padrão |Ilimitado, pagamento das [tarifas](https://azure.microsoft.com/pricing/details/app-service/)</a> padrão |Ilimitado, pagamento das [tarifas](https://azure.microsoft.com/pricing/details/app-service/)</a> padrão |Ilimitado, pagamento das [tarifas](https://azure.microsoft.com/pricing/details/app-service/)</a> padrão|
| Tempo de CPU (dia)<sup>6</sup> |60 minutos |240 minutos |Ilimitado, pagamento das [tarifas](https://azure.microsoft.com/pricing/details/app-service/)</a> padrão |Ilimitado, pagamento das [tarifas](https://azure.microsoft.com/pricing/details/app-service/)</a> padrão |Ilimitado, pagamento das [tarifas](https://azure.microsoft.com/pricing/details/app-service/)</a> padrão |Ilimitado, pagamento das [tarifas](https://azure.microsoft.com/pricing/details/app-service/)</a> padrão |
| Memória (1 hora) |1\.024 MB por plano do Serviço de Aplicativo |1\.024 MB por aplicativo |N/D |N/D |N/D |N/D |
| Largura de banda |165 MB |Ilimitada, aplicam-se [taxas de transferência de dados](https://azure.microsoft.com/pricing/details/data-transfers/) |Ilimitada, aplicam-se [taxas de transferência de dados](https://azure.microsoft.com/pricing/details/data-transfers/) |Ilimitada, aplicam-se [taxas de transferência de dados](https://azure.microsoft.com/pricing/details/data-transfers/) |Ilimitada, aplicam-se [taxas de transferência de dados](https://azure.microsoft.com/pricing/details/data-transfers/) |Ilimitada, aplicam-se [taxas de transferência de dados](https://azure.microsoft.com/pricing/details/data-transfers/) |
| Arquitetura do aplicativo |32 bits |32 bits |32 bits/64 bits |32 bits/64 bits |32 bits/64 bits |32 bits/64 bits |
| Soquetes da Web por instância<sup>7</sup> |5 |35 |350 |Ilimitado |Ilimitado |Ilimitado |
| Conexões IP | 600 | 600 | Depende do tamanho da instância<sup>8</sup> | Depende do tamanho da instância<sup>8</sup> | Depende do tamanho da instância<sup>8</sup> | 16.000 |
| [Conexões do depurador](../articles/app-service/troubleshoot-dotnet-visual-studio.md) simultâneas por aplicativo |1 |1 |1 |5 |5 |5 |
| Certificados do Serviço de Aplicativo por assinatura<sup>9</sup>| Sem suporte | Sem suporte |10 |10 |10 |10 |
| Domínios personalizados por aplicativo</a> |0 (somente subdomínio do azurewebsites.net)|500 |500 |500 |500 |500 |
| domínio personalizado [Suporte a SSL](../articles/app-service/configure-ssl-certificate.md) |Não compatível, certificado curinga para \*.azurewebsites.net disponível por padrão|Não compatível, certificado curinga para \*.azurewebsites.net disponível por padrão|Conexões SSL de SNI ilimitadas |Conexões SSL de SNI ilimitadas e IP SSL incluídas |Conexões SSL de SNI ilimitadas e IP SSL incluídas | Conexões SSL de SNI ilimitadas e IP SSL incluídas|
| Conexões Híbridas | | | 5 por plano | 25 por plano | 200 por aplicativo | 200 por aplicativo |
| [Integração de Rede Virtual](../articles/app-service/web-sites-integrate-with-vnet.md) | | |   |  X |  X  |  X  |
| Balanceador de carga integrado | |X |X |X |X |X<sup>10</sup> |
| [Restrições de acesso](../articles/app-service/networking-features.md#access-restrictions) | 512 regras por aplicativo | 512 regras por aplicativo | 512 regras por aplicativo | 512 regras por aplicativo | 512 regras por aplicativo | 512 regras por aplicativo |
| [Always On](../articles/app-service/configure-common.md) | | |X |X |X |X |
| [Backups agendados](../articles/app-service/manage-backup.md) | | | | Backups agendados a cada 2 horas, máximo de 12 backups por dia (manuais + agendados) | Backups agendados a cada hora, máximo de 50 backups por dia (manuais + agendados) | Backups agendados a cada hora, máximo de 50 backups por dia (manuais + agendados) |
| [Autoescala](../articles/app-service/manage-scale-up.md) | | | |X |X |X |
| [WebJobs](../articles/app-service/webjobs-create.md)<sup>11</sup> |X |X |X |X |X |X |
| [Monitoramento do ponto de extremidade](../articles/app-service/web-sites-monitor.md) | | |X |X |X |X |
| [Slots de preparo](../articles/app-service/deploy-staging-slots.md) por aplicativo| | | |5 |20 |20 |
| [Teste em produção](../articles/app-service/deploy-staging-slots.md#route-traffic)| | | |X |X |X |
| [Logs de Diagnóstico](../articles/app-service/troubleshoot-diagnostic-logs.md) | X | X | X | X | X | X |
| Kudu | X | X | X | X | X | X |
| [Autenticação e autorização](../articles/app-service/overview-authentication-authorization.md) | X | X | X | X | X | X |
| [Certificados Gerenciados do Serviço de Aplicativo (Versão Prévia Pública)](https://azure.microsoft.com/updates/secure-your-custom-domains-at-no-cost-with-app-service-managed-certificates-preview/)<sup>12</sup> | |  | X | X | X | X |
| Contrato de Nível de Serviço | |  |99,95%|99,95%|99,95%|99,95%|  

<sup>1</sup>Aplicativos e cotas de armazenamento são oferecidos por plano de Serviço de Aplicativo, a menos que haja indicação contrária.  
<sup>2</sup>O número real de aplicativos que podem ser hospedados nesses computadores depende da atividade dos aplicativos, do tamanho das instâncias do computador e da utilização do recurso correspondente.  
<sup>3</sup>As instâncias dedicadas podem ter tamanhos diferentes. Para saber mais, veja [Preços do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/).  
<sup>4</sup>Uma quantidade maior é permitida sob solicitação.  
<sup>5</sup>O limite de armazenamento é o tamanho total do conteúdo em todos os aplicativos no mesmo Plano do Serviço de Aplicativo. O tamanho total do conteúdo de todos os aplicativos em todos os Planos do Serviço de Aplicativo em um único grupo de recursos e em uma única região não pode exceder 500 GB.  
<sup>6</sup>Esses recursos são limitados pelos recursos físicos nas instâncias dedicadas (o tamanho de instância e o número de instâncias).  
<sup>7</sup>Ao escalar um aplicativo na camada Basic para duas instâncias, você tem 350 conexões simultâneas para cada uma das duas instâncias. Para o nível Standard e superior, não há limites teóricos para os soquetes da Web, mas outros fatores podem limitar o número de soquetes da Web. Por exemplo, o máximo de solicitações simultâneas permitidas (definidas por `maxConcurrentRequestsPerCpu`) é: 7.500 por VM pequena, 15.000 por VM média (7.500 x 2 núcleos) e 75.000 por VM grande (18.750 x 4 núcleos).  
<sup>8</sup>O número máximo de conexões IP é por instância e depende do tamanho da instância: 1.920 por instância B1/S1/P1V3, 3.968 por instância B2/S2/P2V3, 8.064 por instância B3/S3/P3V3.  
<sup>9</sup>O limite de cota do Certificado do Serviço de Aplicativo por assinatura pode ser aumentado por meio de uma solicitação de suporte para um limite máximo de 200.  
<sup>10</sup>Os SKUs do Serviço do Aplicativo Isolado podem ter balanceamento de carga interno (ILB) com o Azure Load Balancer, portanto não há conectividade pública da Internet. Como resultado, alguns recursos do Serviço de Aplicativo Isolado de ILB devem ser usados de computadores com acesso direto ao ponto de extremidade de rede de ILB.  
<sup>11</sup>Execute scripts e/ou executáveis personalizados sob demanda, em um agendamento ou continuamente, como uma tarefa em segundo plano em sua instância do Serviço de Aplicativo. Para a execução contínua de Trabalhos Web, a opção Sempre Ativado é obrigatória. Não há nenhum limite predefinido no número de WebJobs que podem ser executados em uma instância do Serviço de Aplicativo. Há limites práticos que dependem do que o código do aplicativo está tentando fazer.

<sup>12</sup>Não há suporte para domínios raiz. Emissão somente de certificados padrão (certificados curinga não estão disponíveis). Limitado a apenas um certificado gratuito por domínio personalizado.
