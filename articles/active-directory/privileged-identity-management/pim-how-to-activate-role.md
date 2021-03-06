---
title: Ativar minhas funções do Azure AD no PIM-Azure Active Directory | Microsoft Docs
description: Saiba como ativar as funções do Azure AD no Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: how-to
ms.workload: identity
ms.subservice: pim
ms.date: 07/06/2020
ms.author: curtand
ms.custom: pim
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38992c15c23216aa81cda566a333d8e45f90b17e
ms.sourcegitcommit: 28c5fdc3828316f45f7c20fc4de4b2c05a1c5548
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92369838"
---
# <a name="activate-my-azure-ad-roles-in-pim"></a>Ativar minhas funções do Azure AD no PIM

O Azure Active Directory (Azure AD) Privileged Identity Management (PIM) simplifica o modo como as empresas gerenciam o acesso privilegiado a recursos no Azure AD e outros serviços online da Microsoft, como Microsoft 365 ou Microsoft Intune.  

Se você tiver se tornado qualificado para uma função administrativa, deverá ativar a atribuição de função quando precisar executar ações privilegiadas. Por exemplo, se você ocasionalmente gerencia Microsoft 365 recursos, os administradores de função com privilégios de sua organização podem não torná-lo um administrador global permanente, pois essa função também afeta outros serviços. Em vez disso, eles o tornam qualificado para funções do Azure AD, como Administrador do Exchange Online. Você pode solicitar a ativação da função quando precisar de seus privilégios e terá controle de administrador por um período predeterminado.

Este artigo é para os administradores que precisam ativar sua função do Azure AD no Privileged Identity Management.

## <a name="determine-your-version-of-pim"></a>Determinar sua versão do PIM

A partir de novembro de 2019, a parte das funções do Azure AD da Privileged Identity Management está sendo atualizada para uma nova versão que corresponde às experiências de funções de recurso do Azure. Isso cria recursos adicionais, bem como [as alterações na API existente](azure-ad-roles-features.md#api-changes). Enquanto a nova versão está sendo distribuída, os procedimentos que você seguir neste artigo dependem da versão do Privileged Identity Management que você tem atualmente. Siga as etapas nesta seção para determinar qual versão do Privileged Identity Management você tem. Depois de saber sua versão do Privileged Identity Management, você pode selecionar os procedimentos neste artigo que correspondem a essa versão.

1. Entre no [portal do Azure](https://portal.azure.com/) com a função de [administrador de função com privilégios](../roles/permissions-reference.md#privileged-role-administrator) .
1. Abra **Azure ad Privileged Identity Management**. Se você tiver uma faixa na parte superior da página Visão geral, siga as instruções na **nova guia versão** deste artigo. Caso contrário, siga as instruções na guia **versão anterior** .

    [![Selecione Azure AD > Privileged Identity Management.](media/pim-how-to-add-role-to-user/pim-new-version.png)](media/pim-how-to-add-role-to-user/pim-new-version.png#lightbox)

# <a name="new-version"></a>[Nova versão](#tab/new)

## <a name="activate-a-role-for-new-version"></a>Ativar uma função para a nova versão

Quando você precisar assumir uma função do Azure AD, poderá solicitar a ativação abrindo **minhas funções** no Privileged Identity Management.

1. Entre no [portal do Azure](https://portal.azure.com/).

1. Abra **Azure ad Privileged Identity Management**. Para obter informações sobre como adicionar o bloco Privileged Identity Management ao seu painel, consulte [começar a usar o Privileged Identity Management](pim-getting-started.md).

1. Selecione **minhas funções**e, em seguida, selecione **funções do Azure ad** para ver uma lista de suas funções qualificadas do Azure AD.

    ![Minha página de funções mostrando funções que você pode ativar](./media/pim-how-to-activate-role/my-roles.png)

1. Na lista **funções do Azure ad** , localize a função que você deseja ativar.

    ![Funções do Azure AD – minha lista de funções qualificadas](./media/pim-how-to-activate-role/activate-link.png)

1. Selecione **Ativar** para abrir a página ativar.

    ![Funções do Azure AD – a página ativação contém a duração e o escopo](./media/pim-how-to-activate-role/activate-page.png)

1. Se sua função exigir autenticação multifator, selecione **Verificar sua identidade antes de prosseguir**. Você só precisa se autenticar uma vez por sessão.

    ![Verificar minha identidade com MFA antes da ativação de função](./media/pim-resource-roles-activate-your-roles/resources-my-roles-mfa.png)

1. Selecione **verificar minha identidade** e siga as instruções para fornecer verificação de segurança adicional.

    ![Tela para fornecer verificação de segurança, como um código PIN](./media/pim-resource-roles-activate-your-roles/resources-mfa-enter-code.png)

1. Se você quiser especificar um escopo reduzido, selecione **escopo** para abrir o painel de filtro. No painel filtro, você pode especificar os recursos do Azure AD aos quais você precisa acessar. É uma prática recomendada solicitar acesso apenas aos recursos de que você precisa.

1. Se necessário, especifique uma hora de início de ativação personalizada. A função do Azure AD seria ativada após a hora selecionada.

1. Na caixa **Motivo**, insira o motivo da solicitação de ativação.

1. Selecione **Ativar**.

    Se a [função exigir aprovação](pim-resource-roles-approval-workflow.md) para ser ativada, uma notificação será exibida no canto superior direito do seu navegador informando que a solicitação está com a aprovação pendente.

    ![Notificação de aprovação pendente da solicitação de ativação](./media/pim-resource-roles-activate-your-roles/resources-my-roles-activate-notification.png)

## <a name="view-the-status-of-your-requests-for-new-version"></a>Exibir o status de suas solicitações para a nova versão

Você pode exibir o status das suas solicitações pendentes a serem ativadas.

1. Abra o Azure AD Privileged Identity Management.

1. Selecione **minhas solicitações** para ver uma lista de suas funções do Azure AD e das solicitações de função de recurso do Azure.

    ![Minhas solicitações – página do Azure AD mostrando suas solicitações pendentes](./media/pim-how-to-activate-role/my-requests-page.png)

1. Role para a direita para exibir o **Status da solicitação** coluna.

## <a name="cancel-a-pending-request-for-new-version"></a>Cancelar uma solicitação pendente para a nova versão

Caso não precise da ativação de uma função que requer aprovação, você pode cancelar uma solicitação pendente a qualquer momento.

1. Abra o Azure AD Privileged Identity Management.

1. Selecione **minhas solicitações**.

1. Para a função que você deseja cancelar, selecione o link **Cancelar** .

    Quando você selecionar cancelar, a solicitação será cancelada. Para ativar a função novamente, você precisará enviar uma nova solicitação de ativação.

   ![Minha lista de solicitações com a ação cancelar realçada](./media/pim-resource-roles-activate-your-roles/resources-my-requests-cancel.png)

## <a name="troubleshoot-for-new-version"></a>Solucionar problemas da nova versão

### <a name="permissions-are-not-granted-after-activating-a-role"></a>As permissões não são concedidas depois de ativar uma função

Quando você ativa uma função no Privileged Identity Management, a ativação pode não ser propagada instantaneamente para todos os portais que exigem a função privilegiada. Às vezes, mesmo quando a alteração é propagada, o cache da web em um portal pode fazer com que a alteração não entre em vigor de imediato. Se a ativação estiver atrasada, aqui está o que você deve fazer.

1. Saia do portal do Azure e entre novamente.

1. Em Privileged Identity Management, verifique se você está listado como o membro da função.

# <a name="previous-version"></a>[Versão anterior](#tab/previous)

## <a name="activate-a-role-previous-version"></a>Ativar uma função (versão anterior)

Quando precisar tomar uma função do Azure AD, você poderá solicitar a ativação usando a opção de navegação **minhas funções** no Privileged Identity Management.

1. Entre no [portal do Azure](https://portal.azure.com/).

1. Abra **Azure ad Privileged Identity Management**. Para obter informações sobre como adicionar o bloco Privileged Identity Management ao seu painel, consulte [começar a usar o Privileged Identity Management](pim-getting-started.md).

1. Clique em **funções do Microsoft Azure Active Directory**.

1. Clique em **minhas funções** para ver uma lista de suas funções qualificadas do Azure AD.

    ![Funções do Azure AD – minhas funções mostrando a lista de funções qualificadas ou ativas](./media/pim-how-to-activate-role/directory-roles-my-roles.png)

1. Localize uma função que você deseja ativar.

    ![Funções do Azure AD – minha lista de funções qualificadas mostrando o link ativar](./media/pim-how-to-activate-role/directory-roles-my-roles-activate.png)

1. Clique em **Ativar** para abrir o painel Detalhes de ativação de função.

1. Se sua função exigir a MFA (autenticação multifator), clique em **Verificar sua identidade antes de prosseguir**. Você só precisa se autenticar uma vez por sessão.

    ![Verificar meu painel de identidade com MFA antes da ativação de função](./media/pim-how-to-activate-role/directory-roles-my-roles-mfa.png)

1. Clique em **Verificar minha identidade** e siga as instruções para fornecer a verificação de segurança adicional.

    ![Página de verificação de segurança adicional perguntando como entrar em contato com você](./media/pim-how-to-activate-role/additional-security-verification.png)

1. Clique em **Ativar** para abrir o painel Ativação.

    ![Painel ativação para especificar a hora de início, a duração, o tíquete e o motivo](./media/pim-how-to-activate-role/directory-roles-activate.png)

1. Se necessário, especifique uma hora de início de ativação personalizada.

1. Especifique a duração da ativação.

1. Na caixa **Motivo da ativação**, insira o motivo para a solicitação de ativação. Algumas funções exigem que você forneça um número de tíquete de problema.

    ![O painel de ativação foi concluído com uma hora de início personalizada, a duração, o tíquete e o motivo](./media/pim-how-to-activate-role/directory-roles-activation-pane.png)

1. Clique em **Ativar**.

    Se a função não exigir aprovação, um painel **status de ativação** será exibido exibindo o status da ativação.

    ![Página status da ativação mostrando os três estágios da ativação](./media/pim-how-to-activate-role/activation-status.png)

    Depois que todos os estágios forem concluídos, clique **no link sair para sair do** portal do Azure. Quando você entra novamente no portal, agora você pode usar a função.

    Se a [função exigir aprovação](./azure-ad-pim-approval-workflow.md) para ativar, uma notificação do Azure será exibida no canto superior direito do seu navegador informando que a solicitação está com aprovação pendente.

## <a name="view-the-status-of-your-requests-previous-version"></a>Exibir o status de suas solicitações (versão anterior)

Você pode exibir o status das suas solicitações pendentes a serem ativadas.

1. Abra o Azure AD Privileged Identity Management.

1. Clique em **funções do Microsoft Azure Active Directory**.

1. Clique em **Minhas solicitações** para ver uma lista das suas solicitações.

    ![Funções do Azure AD – lista de minhas solicitações](./media/pim-how-to-activate-role/directory-roles-my-requests.png)

## <a name="deactivate-a-role-previous-version"></a>Desativar uma função (versão anterior)

Após uma função ter sido ativada, ela será desativada automaticamente quando limite de tempo (duração qualificada) for atingido.

Se concluir suas tarefas de administrador antes, você também poderá desativar uma função manualmente no Azure AD Privileged Identity Management.

1. Abra o Azure AD Privileged Identity Management.

1. Clique em **funções do Microsoft Azure Active Directory**.

1. Clique em **Minhas funções**.

1. Clique em **Funções ativas** para ver a lista de funções ativas.

1. Localize a função que você terminou de usar e clique em **Destivar**.

## <a name="cancel-a-pending-request-previous-version"></a>Cancelar uma solicitação pendente (versão anterior)

Caso não precise da ativação de uma função que requer aprovação, você pode cancelar uma solicitação pendente a qualquer momento.

1. Abra o Azure AD Privileged Identity Management.

1. Clique em **funções do Microsoft Azure Active Directory**.

1. Clique em **Minhas solicitações**.

1. Para a função que você deseja cancelar, clique no botão **Cancelar**.

    Quando você clicar em cancelar, a solicitação será cancelada. Para ativar a função novamente, você precisará enviar uma nova solicitação de ativação.

   ![Minha lista de solicitações com o botão Cancelar realçado](./media/pim-how-to-activate-role/directory-role-cancel.png)

## <a name="troubleshoot-previous-version"></a>Solução de problemas (versão anterior)

### <a name="permissions-are-not-granted-after-activating-a-role"></a>As permissões não são concedidas depois de ativar uma função

Quando você ativa uma função no Privileged Identity Management, a ativação pode não ser propagada instantaneamente para todos os portais que exigem a função privilegiada. Às vezes, mesmo quando a alteração é propagada, o cache da web em um portal pode fazer com que a alteração não entre em vigor de imediato. Se a ativação estiver atrasada, aqui está o que você deve fazer.

1. Saia do portal do Azure e entre novamente.

    Quando você ativar uma função do Azure AD, verá os estágios da ativação. Quando todas as fases forem concluídas, você verá um link **Sair**. Você pode usar este link para sair. Isso irá resolver a maioria dos casos de atraso de ativação.

1. Em Privileged Identity Management, verifique se você está listado como o membro da função.

 ---

## <a name="next-steps"></a>Próximas etapas

- [Ativar minhas funções do Azure AD no Privileged Identity Management](pim-how-to-activate-role.md)
