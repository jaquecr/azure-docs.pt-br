---
title: Controle de acesso de pastas de trabalho Azure Monitor
description: Simplifique relatórios complexos com pastas de trabalho parametrizadas predefinidas e personalizadas com controle de acesso baseado em função
services: azure-monitor
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.topic: conceptual
ms.date: 10/23/2019
ms.openlocfilehash: 92ac1887aca8f30c551419ef9149073d79f333a5
ms.sourcegitcommit: dbe434f45f9d0f9d298076bf8c08672ceca416c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92143829"
---
# <a name="access-control"></a>Controle de acesso

O controle de acesso em pastas de trabalho refere-se a duas coisas:

* Acesso necessário para ler dados em uma pasta de trabalho. Esse acesso é controlado pelas [funções padrão do Azure](../../role-based-access-control/overview.md) nos recursos usados na pasta de trabalho. As pastas de trabalho não especificam ou configuram o acesso a esses recursos. Normalmente, os usuários terão esse acesso a esses recursos usando a função [leitor de monitoramento](../../role-based-access-control/built-in-roles.md#monitoring-reader) nesses recursos.

* Acesso necessário para salvar pastas de trabalho

    - Salvar `("My")` pastas de trabalho particulares não requer privilégios adicionais. Todos os usuários podem salvar pastas de trabalho particulares e apenas podem ver essas pastas de trabalho.
    - Salvar pastas de trabalho compartilhadas requer privilégios de gravação em um grupo de recursos para salvar a pasta de trabalho. Esses privilégios geralmente são especificados pela função de [colaborador de monitoramento](../../role-based-access-control/built-in-roles.md#monitoring-contributor) , mas também podem ser definidos por meio da função colaborador de pastas de *trabalho* .
    
## <a name="standard-roles-with-workbook-related-privileges"></a>Funções padrão com privilégios relacionados à pasta de trabalho

O [leitor de monitoramento](../../role-based-access-control/built-in-roles.md#monitoring-reader) inclui privilégios de/Read padrão que seriam usados por ferramentas de monitoramento (incluindo pastas de trabalho) para ler dados de recursos.

O [colaborador de monitoramento](../../role-based-access-control/built-in-roles.md#monitoring-contributor) inclui privilégios gerais `/write` usados por várias ferramentas de monitoramento para salvar itens (incluindo `workbooks/write` privilégios para salvar pastas de trabalho compartilhadas).
"Colaborador de pastas de trabalho" adiciona privilégios de "pastas de trabalho/gravação" a um objeto para salvar pastas de trabalho compartilhadas.
Nenhum privilégio especial é necessário para que os usuários salvem pastas de trabalho particulares que só possam ver.

Para controle de acesso baseado em função personalizado:

Adicionar `microsoft.insights/workbooks/write` para salvar pastas de trabalho compartilhadas. Para obter mais detalhes, consulte a função [colaborador da pasta de trabalho](../../role-based-access-control/built-in-roles.md#monitoring-contributor) .

## <a name="next-steps"></a>Próximas etapas

* [Comece a aprender mais](./workbooks-overview.md#visualizations) sobre pastas de trabalho muitas opções de visualizações ricas.