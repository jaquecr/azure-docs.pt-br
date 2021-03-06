---
title: Visão geral da política de TLS para Aplicativo Azure gateway
description: Saiba como configurar a política de TLS para Aplicativo Azure gateway e reduzir a sobrecarga de criptografia e descriptografia de um farm de servidores back-end.
services: application gateway
author: amsriva
ms.service: application-gateway
ms.topic: conceptual
ms.date: 11/16/2019
ms.author: amsriva
ms.openlocfilehash: 16c6dd28d47573c2ad5b0d5a331b0dc48e7aacef
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "85253623"
---
# <a name="application-gateway-tls-policy-overview"></a>Visão geral da política TLS do gateway de aplicativo

Você pode usar Aplicativo Azure gateway para centralizar o gerenciamento de certificados TLS/SSL e reduzir a sobrecarga de criptografia e descriptografia de um farm de servidores back-end. Essa manipulação de TLS centralizado também permite que você especifique uma política TLS central adequada aos seus requisitos de segurança organizacional. Isso ajuda a atender aos requisitos de conformidade, bem como às diretrizes de segurança e às práticas recomendadas.

A política TLS inclui o controle da versão do protocolo TLS, bem como os conjuntos de codificação e a ordem em que as codificações são usadas durante um handshake TLS. O gateway de aplicativo oferece dois mecanismos para controlar a política TLS. Você pode usar uma política predefinida ou uma política personalizada.

## <a name="predefined-tls-policy"></a>Política TLS predefinida

O Gateway de Aplicativo tem três políticas de segurança predefinidos. Você pode configurar o gateway com alguma dessas políticas para obter o nível adequado de segurança. Os nomes de política são anotados pelo ano e mês no qual eles foram configurados. Cada política oferece versões de protocolo TLS e conjuntos de codificação diferentes. Recomendamos que você use as políticas de TLS mais recentes para garantir a melhor segurança de TLS.

### <a name="appgwsslpolicy20150501"></a>AppGwSslPolicy20150501

|Propriedade  |Valor  |
|---|---|
|Nome     | AppGwSslPolicy20150501        |
|MinProtocolVersion     | TLSv1_0        |
|Padrão| True (se nenhuma política predefinida é especificada) |
|CipherSuites     |TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_DHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_DHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_3DES_EDE_CBC_SHA<br>TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA |
  
### <a name="appgwsslpolicy20170401"></a>AppGwSslPolicy20170401
  
|Propriedade  |Valor  |
|   ---      |  ---       |
|Nome     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_1        |
|Padrão| Falso |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA |
  
### <a name="appgwsslpolicy20170401s"></a>AppGwSslPolicy20170401S

|Propriedade  |Valor  |
|---|---|
|Nome     | AppGwSslPolicy20170401S        |
|MinProtocolVersion     | TLSv1_2        |
|Padrão| Falso |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 <br>    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 <br>    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br> |

## <a name="custom-tls-policy"></a>Política TLS personalizada

Se uma política TLS predefinida precisar ser configurada para seus requisitos, você deverá definir sua própria política TLS personalizada. Com uma política TLS personalizada, você tem controle total sobre a versão mínima do protocolo TLS para oferecer suporte, bem como os conjuntos de criptografia com suporte e sua ordem de prioridade.
 
### <a name="tlsssl-protocol-versions"></a>Versões do protocolo TLS/SSL

* SSL 2.0 e 3.0 são desabilitados por padrão para todos os gateways do aplicativo. Essas versões de protocolo não são configuráveis.
* Uma política TLS personalizada oferece a opção de selecionar qualquer um dos três protocolos a seguir como a versão mínima do protocolo TLS para seu gateway: TLSv1_0, TLSv1_1 e TLSv1_2.
* Se nenhuma política de TLS for definida, todos os três protocolos (TLSv1_0, TLSv1_1 e TLSv1_2) serão habilitados.

### <a name="cipher-suites"></a>Conjuntos de criptografia

O Gateway de Aplicativo dá suporte aos seguintes conjuntos de criptografia dos quais a política personalizada pode ser escolhida. A ordenação dos conjuntos de codificação determina a ordem de prioridade durante a negociação de TLS.


- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

> [!NOTE]
> Os conjuntos de criptografia TLS usados para a conexão também são baseados no tipo de certificado que está sendo usado. No cliente para conexões de gateway de aplicativo, os conjuntos de codificação usados são baseados no tipo de certificados de servidor no ouvinte do gateway de aplicativo. No gateway de aplicativo para conexões de pool de back-end, os conjuntos de codificação usados são baseados no tipo de certificados de servidor nos servidores do pool de back-end.

## <a name="known-issue"></a>Problema conhecido
Atualmente, o gateway de aplicativo v2 não oferece suporte às seguintes codificações:
- DHE-RSA-AES128-GCM-SHA256
- DHE-RSA-AES128-SHA
- DHE-RSA-AES256-GCM-SHA384
- DHE-RSA-AES256-SHA
- DHE-DSS-AES128-SHA256
- DHE-DSS-AES128-SHA
- DHE-DSS-AES256-SHA256
- DHE-DSS-AES256-SHA

## <a name="next-steps"></a>Próximas etapas

Se você quiser aprender a configurar uma política de TLS, consulte [Configurar versões de política de TLS e conjuntos de codificação no gateway de aplicativo](application-gateway-configure-ssl-policy-powershell.md).
