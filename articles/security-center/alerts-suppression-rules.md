---
title: Uso de regras de supressão de alertas para suprimir falsos positivos ou outros alertas de segurança indesejados na Central de Segurança do Azure.
description: Este artigo explica como usar as regras de supressão da central de segurança do Azure para ocultar alertas indesejados do Azure defender
author: memildin
manager: rkarlin
services: security-center
ms.author: memildin
ms.date: 09/10/2020
ms.service: security-center
ms.topic: how-to
ms.openlocfilehash: b954d6ed29074aa9261611f0d1bb79b5917d03f2
ms.sourcegitcommit: 65d518d1ccdbb7b7e1b1de1c387c382edf037850
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94372652"
---
# <a name="suppress-alerts-from-azure-defender"></a>Suprimir alertas do Azure Defender

Esta página explica como você pode usar as regras de supressão de alertas para suprimir falsos positivos ou outros alertas de segurança indesejados do Azure defender.

## <a name="availability"></a>Disponibilidade

|Aspecto|Detalhes|
|----|:----|
|Estado da versão:|Versão Prévia<br>[!INCLUDE [Legalese](../../includes/security-center-preview-legal-text.md)] |
|Preço:|Gratuita<br>(A maioria dos alertas de segurança só está disponível com o Azure defender)|
|Funções e permissões necessárias:|**Administrador de segurança** e **proprietário** podem criar/excluir regras.<br>O **Leitor de segurança** e o **Leitor** podem exibir regras.|
|Nuvens:|![Sim](./media/icons/yes-icon.png) Nuvens comerciais<br>![Sim](./media/icons/yes-icon.png) Nacionais/soberanas (US Gov, China Gov, outros Gov)|
|||


## <a name="what-are-suppression-rules"></a>O que são regras de supressão?

Os vários planos do Azure defender detectam ameaças em qualquer área do seu ambiente e geram alertas de segurança.

Quando um único alerta não é interessante ou relevante, você pode descartá-lo manualmente. Como alternativa, use o recurso de regras de supressão para ignorar automaticamente alertas semelhantes no futuro. Normalmente, você usaria uma regra de supressão para:

- Suprimir alertas que você identificou como falsos positivos

- Suprimir alertas que estão sendo disparados com muita frequência para serem úteis

As regras de supressão definem os critérios para os quais os alertas devem ser automaticamente ignorados.

> [!CAUTION]
> Suprimir alertas de segurança reduz a eficácia da proteção contra ameaças do Azure defender. Você deve verificar cuidadosamente o possível impacto das regras de supressão e monitorá-lo ao longo do tempo.

:::image type="content" source="./media/alerts-suppression-rules/create-suppression-rule.gif" alt-text="Criar regra de supressão de alerta":::

## <a name="create-a-suppression-rule"></a>Criar regra de supressão

Há algumas maneiras de criar regras para suprimir alertas de segurança indesejados:

- Para suprimir alertas no nível de grupo de gerenciamento, use o Azure Policy
- Para suprimir alertas no nível de assinatura, você pode usar o portal do Azure ou a API REST, conforme explicado abaixo

As regras de supressão só podem ignorar alertas que já foram acionados nas assinaturas selecionadas.

Para criar uma regra diretamente no portal do Azure:

1. Na página de alertas de segurança da Central de Segurança:

    - Localize o alerta específico que você não deseja mais ver e, no menu de reticências (...) do alerta, selecione **Criar regra de supressão** :

        [![Opção **Criar regra de supressão**](media/alerts-suppression-rules/auto-dismiss-future-option.png)](media/alerts-suppression-rules/auto-dismiss-future-option.png#lightbox)

    - Ou então, selecione o link **regras de supressão** na parte superior da página e, na página de regras de supressão, selecione **Criar nova regra de supressão** :

        ![Botão Criar nova regra de supressão**](media/alerts-suppression-rules/create-new-suppression-rule.png)

1. No painel Nova regra de supressão, insira os detalhes da nova regra.
    - A regra pode ignorar o alerta em **todos os recursos** para que você não receba alertas como este no futuro.     
    - A regra pode ignorar o alerta **em critérios específicos** - quando está relacionado especificamente a um endereço IP, um nome do processo, uma conta de usuário, um recurso do Azure ou um local.

    > [!TIP]
    > Se você abriu a página da nova regra em um alerta específico, o alerta e a assinatura serão configurados automaticamente na nova regra. Se você usou o link **Criar nova regra de supressão** , as assinaturas selecionadas corresponderão ao filtro atual no portal.

    [![Painel de criação de regras de supressão](media/alerts-suppression-rules/new-suppression-rule-pane.png)](media/alerts-suppression-rules/new-suppression-rule-pane.png#lightbox)
1. Insira os detalhes da regra:
    - **Nome** - um nome para a regra. Os nomes de regra precisam começar com uma letra ou um número, ter entre 2 e 50 caracteres e só podem conter os símbolos de traço (-) ou sublinhado (_). 
    - **Estado** - habilitado ou desabilitado.
    - **Motivo** - selecione um dos motivos integrados ou "outros", se eles não atenderem às suas necessidades.
    - **Data de validade** - uma data e hora de término para a regra. As regras podem ser executadas por até seis meses.
1. Como opção, teste a regra usando o botão **Simular** para ver quantos alertas teriam sido ignorados se essa regra estivesse ativa.
1. Salve a regra. 


## <a name="edit-a-suppression-rules"></a>Editar regras de supressão

Para editar as regras que você criou, use a página regras de supressão.

1. Na página de alertas de segurança da Central de Segurança, selecione o link **regras de supressão** na parte superior da página.
1. A página regras de supressão é aberta com todas as regras para as assinaturas selecionadas.

    [![Lista de regras de supressão](media/alerts-suppression-rules/suppression-rules-page.png)](media/alerts-suppression-rules/suppression-rules-page.png#lightbox)

1. Para editar uma única regra, abra o menu de reticências (...) da regra e selecione **Editar**.
1. Faça as alterações necessárias e selecione **Aplicar**. 

## <a name="delete-a-suppression-rule"></a>Excluir uma regra de supressão

Para excluir uma ou mais regras que você criou, use a página de regras de supressão.

1. Na página de alertas de segurança da Central de Segurança, selecione o link **regras de supressão** na parte superior da página.
1. A página regras de supressão é aberta com todas as regras para as assinaturas selecionadas.
1. Para excluir uma única regra, abra o menu de reticências (...) da regra e selecione **Excluir**.
1. Para excluir várias regras, marque as caixas de seleção das regras a serem excluídas e selecione **Excluir**.
    ![Exclusão de uma ou mais regras de supressão](media/alerts-suppression-rules/delete-multiple-alerts.png)

## <a name="view-suppressed-alerts"></a>Exibir alertas suprimidos

Os alertas que corresponderem às regras de supressão habilitadas ainda serão gerados, mas o estado deles será definido como **ignorado**. Você poderá ver o estado no portal do Azure ou de qualquer outra maneira que você acessar os alertas de segurança da Central de Segurança. 

> [!TIP]
> O [Azure Sentinel](https://azure.microsoft.com/services/azure-sentinel/) não criará incidentes para alertas suprimidos. Para outros SIEMs, você pode filtrar os alertas suprimidos usando o estado dos alertas ("ignorado").

Use o filtro da Central de Segurança para exibir os alertas que foram ignorados pelas regras.

* Na página de alertas de segurança da Central de Segurança, abra as opções de filtro e selecione **Ignorado**.  

   [![Exibição dos alertas ignorados](media/alerts-suppression-rules/view-dismissed-alerts.png)](media/alerts-suppression-rules/view-dismissed-alerts.png#lightbox)


## <a name="create-and-manage-suppression-rules-with-the-api"></a>Criar e gerenciar regras de supressão com a API

Você pode criar, exibir ou excluir regras de supressão de alerta por meio da API REST da Central de Segurança. 

Os métodos HTTP relevantes para regras de supressão na API REST são:

- **PUT** : Para criar ou atualizar uma regra de supressão em uma assinatura especificada.

- **GET** :

    - Para listar todas as regras configuradas para uma assinatura especificada. Esse método retorna uma matriz das regras aplicáveis.

    - Para obter os detalhes de uma regra específica em uma assinatura especificada. Esse método retorna uma regra de supressão.

    - Para simular o impacto de uma regra de supressão ainda na fase de design. Essa chamada identifica qual dos alertas existentes teria sido ignorado, se a regra estivesse ativa.

- **DELETE** : Exclui uma regra existente (mas não altera o status dos alertas já ignorados por ela).

Para obter os detalhes completos e exemplos de uso, confira a [documentação da API](/rest/api/securitycenter/). 


## <a name="next-steps"></a>Próximas etapas

Este artigo descreveu as regras de supressão na Central de Segurança do Azure que ignoraram automaticamente os alertas indesejados.

Para obter mais informações sobre os alertas de segurança do Azure defender, consulte as seguintes páginas:

- [Alertas de segurança e a intenção de Kill Chain](alerts-reference.md) -um guia de referência para os alertas de segurança que você pode obter do Azure defender.