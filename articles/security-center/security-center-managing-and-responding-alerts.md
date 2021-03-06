---
title: Gerenciar alertas de segurança na Central de Segurança do Azure | Microsoft Docs
description: Este documento ajuda você a usar recursos da Central de segurança do Azure para gerenciar e responder a alertas de segurança.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: how-to
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2020
ms.author: memildin
ms.openlocfilehash: 75ca0438336825bf8d4bbdc6e08eca109f430fde
ms.sourcegitcommit: 400f473e8aa6301539179d4b320ffbe7dfae42fe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92785911"
---
# <a name="manage-and-respond-to-security-alerts-in-azure-security-center"></a>Gerencie e responda a alertas de segurança na Central de Segurança do Azure

Este tópico mostra como exibir e processar os alertas que você recebeu para proteger seus recursos. 

* Para saber mais sobre os diferentes tipos de alertas, consulte [tipos de alertas de segurança](alerts-reference.md).
* Para obter uma visão geral de como a central de segurança gera alertas, consulte [como a central de segurança do Azure detecta e responde às ameaças](security-center-alerts-overview.md).

> [!NOTE]
> Para habilitar as detecções avançadas, habilite o Azure defender. Há uma avaliação gratuita disponível. Para atualizar, selecione tipo de preço na [política de segurança](tutorial-security-policy.md). Consulte [Preços da Central de Segurança do Azure](security-center-pricing.md) para saber mais.

## <a name="what-are-security-alerts"></a>O que são alertas de segurança?
A Central de segurança coleta, analisa e integra automaticamente os dados de registro de seus recursos do Azure, da rede e das soluções de parceiros conectados, como firewall e soluções de proteção de ponto de extremidade, a fim de detectar ameaças reais e reduzir os falsos positivos. Uma lista priorizada de alertas de segurança é exibida na Central de Segurança, junto com as informações necessárias para investigar rapidamente o problema, e recomendações sobre como corrigir um ataque.

> [!NOTE]
> Para obter mais informações sobre como funcionam os recursos de detecção da central de segurança, consulte [como a central de segurança do Azure detecta e responde às ameaças](security-center-alerts-overview.md#detect-threats).

## <a name="manage-your-security-alerts"></a>Gerenciar seus alertas de segurança

1. No painel da central de segurança, consulte o bloco  **proteção contra ameaças** para exibir e visão geral dos alertas.

    ![Bloco Alertas de segurança na Central de Segurança](./media/security-center-managing-and-responding-alerts/security-center-dashboard-alert.png)

1. Para ver mais detalhes sobre os alertas, clique no bloco.

   ![Os Alertas de segurança na Central de Segurança](./media/security-center-managing-and-responding-alerts/security-center-manage-alerts.png)

1. Para filtrar os alertas mostrados, clique em **Filtrar** e, na folha **filtro** que é aberta, selecione as opções de filtro que você deseja aplicar. A lista é atualizada de acordo com o filtro selecionado. A filtragem pode ser muito útil. Por exemplo, convém lidar com os alertas de segurança que ocorreram nas últimas 24 horas, pois você está investigando uma possível falha no sistema.

    ![Filtragem de alertas na Central de Segurança](./media/security-center-managing-and-responding-alerts/security-center-filter-alerts.png)

## <a name="respond-to-security-alerts"></a>Responder a alertas de segurança

1. Na lista **alertas de segurança** , clique em um alerta de segurança. Os recursos envolvidos e as etapas que precisam ser tomadas para corrigir um ataque são mostrados.

    ![Responder a alertas de segurança](./media/security-center-managing-and-responding-alerts/security-center-alert.png)

1. Depois de revisar as informações, clique em um recurso que foi atacado.

    O painel esquerdo da página alerta de segurança mostra informações de alto nível sobre o alerta de segurança: título, severidade, status, tempo de atividade, descrição da atividade suspeita e o recurso afetado. Junto com o recurso afetado estão as marcas do Azure relevantes para o recurso. Use-os para inferir o contexto organizacional do recurso ao investigar o alerta.

    O painel direito inclui a guia **detalhes do alerta** que contém mais detalhes do alerta para ajudá-lo a investigar o problema: endereços IP, arquivos, processos e muito mais.
     
    ![Sugestões sobre o que fazer sobre alertas de segurança](./media/security-center-managing-and-responding-alerts/security-center-alert-remediate.png)

    Também no painel direito está a guia **executar ação** . Use esta guia para executar mais ações em relação ao alerta de segurança. Ações como:
    - *Atenuar a ameaça* -fornece etapas de correção manual para este alerta de segurança
    - *Evitar ataques futuros* – fornece recomendações de segurança para ajudar a reduzir a superfície de ataque, aumentar a postura de segurança e, portanto, evitar ataques futuros
    - *Disparar resposta automatizada* – fornece a opção para disparar um aplicativo lógico como uma resposta a este alerta de segurança
    - *Suprimir alertas semelhantes* – fornece a opção de suprimir alertas futuros com características semelhantes se o alerta não for relevante para sua organização

    ![Executar a guia ação](./media/security-center-managing-and-responding-alerts/alert-take-action.png)




## <a name="see-also"></a>Veja também

Neste documento, você aprendeu a exibir alertas de segurança. Consulte as páginas a seguir para obter material relacionado:

- [Configurar regras de supressão de alerta](alerts-suppression-rules.md)
- [Automatizar respostas para gatilhos da central de segurança](workflow-automation.md)
