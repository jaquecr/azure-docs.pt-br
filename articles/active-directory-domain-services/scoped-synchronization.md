---
title: Sincronização com escopo para Azure AD Domain Services | Microsoft Docs
description: Saiba como usar o portal do Azure para configurar a sincronização com escopo do Azure AD para um Azure Active Directory Domain Services domínio gerenciado
services: active-directory-ds
author: MicrosoftGuyJFlo
manager: daveba
ms.assetid: 9389cf0f-0036-4b17-95da-80838edd2225
ms.service: active-directory
ms.subservice: domain-services
ms.workload: identity
ms.topic: how-to
ms.date: 07/24/2020
ms.author: joflore
ms.custom: devx-track-azurepowershell
ms.openlocfilehash: 514932726d9283af0c3fb404f787a10057ce8842
ms.sourcegitcommit: d103a93e7ef2dde1298f04e307920378a87e982a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91967844"
---
# <a name="configure-scoped-synchronization-from-azure-ad-to-azure-active-directory-domain-services-using-the-azure-portal"></a>Configurar a sincronização com escopo do Azure AD para Azure Active Directory Domain Services usando o portal do Azure

Para fornecer serviços de autenticação, Azure Active Directory Domain Services (Azure AD DS) sincroniza usuários e grupos do Azure AD. Em um ambiente híbrido, os usuários e grupos de um ambiente de Active Directory Domain Services local (AD DS) podem ser sincronizados primeiro com o Azure AD usando Azure AD Connect e, em seguida, sincronizados com um domínio gerenciado do Azure AD DS.

Por padrão, todos os usuários e grupos de um diretório do Azure AD são sincronizados com um domínio gerenciado. Se você tiver necessidades específicas, poderá optar por sincronizar apenas um conjunto definido de usuários.

Este artigo mostra como configurar a sincronização com escopo e, em seguida, alterar ou desabilitar o conjunto de usuários com escopo usando o portal do Azure. Você também pode [concluir essas etapas usando o PowerShell][scoped-sync-powershell].

## <a name="before-you-begin"></a>Antes de começar

Para concluir este artigo, você precisará dos seguintes recursos e privilégios:

* Uma assinatura ativa do Azure.
    * Caso não tenha uma assinatura do Azure, [crie uma conta](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
* Um locatário do Azure Active Directory associado com a assinatura, sincronizado com um diretório local ou somente em nuvem.
    * Se necessário, [crie um locatário do Azure Active Directory][create-azure-ad-tenant] ou [associe uma assinatura do Azure à sua conta][associate-azure-ad-tenant].
* Um domínio gerenciado do Azure Active Directory Domain Services habilitado e configurado no locatário do Azure AD.
    * Se necessário, conclua o tutorial para [criar e configurar um Azure Active Directory Domain Services domínio gerenciado][tutorial-create-instance].
* Você precisa de privilégios de *administrador global* em seu locatário do Azure ad para alterar o escopo de sincronização de AD DS do Azure.

## <a name="scoped-synchronization-overview"></a>Visão geral da sincronização com escopo

Por padrão, todos os usuários e grupos de um diretório do Azure AD são sincronizados com um domínio gerenciado. Se apenas alguns usuários precisarem acessar o domínio gerenciado, você poderá sincronizar somente as contas de usuário. Essa sincronização com escopo é baseada em grupo. Quando você configura a sincronização com escopo baseado em grupo, somente as contas de usuário que pertencem aos grupos que você especifica são sincronizadas com o domínio gerenciado. Grupos aninhados não são sincronizados, somente os grupos específicos que você selecionar.

Você pode alterar o escopo de sincronização ao criar o domínio gerenciado ou depois de ele ser implantado. Agora, você também pode alterar o escopo da sincronização em um domínio gerenciado existente sem precisar recriá-lo.

Para saber mais sobre o processo de sincronização, consulte [entender a sincronização no Azure AD Domain Services][concepts-sync].

> [!WARNING]
> Alterar o escopo da sincronização faz com que o domínio gerenciado sincronize novamente todos os dados. As seguintes considerações se aplicam:
>
>  * Quando você altera o escopo de sincronização para um domínio gerenciado, ocorre uma ressincronização completa.
>  * Os objetos que não são mais necessários no domínio gerenciado são excluídos. Novos objetos são criados no domínio gerenciado.

## <a name="enable-scoped-synchronization"></a>Habilitar sincronização com escopo

Para habilitar a sincronização com escopo no portal do Azure, conclua as seguintes etapas:

1. No portal do Azure, pesquise e selecione **Azure AD Domain Services**. Escolha o domínio gerenciado, como *aaddscontoso.com*.
1. Selecione **sincronização** no menu do lado esquerdo.
1. Para o *tipo de sincronização*, selecione com **escopo**.
1. Escolha **Selecionar grupos**, procure e escolha os grupos a serem adicionados.
1. Quando todas as alterações forem feitas, selecione **salvar escopo de sincronização**.

Alterar o escopo da sincronização faz com que o domínio gerenciado sincronize novamente todos os dados. Os objetos que não são mais necessários no domínio gerenciado são excluídos e a ressincronização pode levar algum tempo para ser concluída.

## <a name="modify-scoped-synchronization"></a>Modificar sincronização com escopo

Para modificar a lista de grupos cujos usuários devem ser sincronizados com o domínio gerenciado, conclua as seguintes etapas:

1. No portal do Azure, pesquise e selecione **Azure AD Domain Services**. Escolha o domínio gerenciado, como *aaddscontoso.com*.
1. Selecione **sincronização** no menu do lado esquerdo.
1. Para adicionar um grupo, escolha **+ Selecionar grupos** na parte superior e, em seguida, escolha os grupos a serem adicionados.
1. Para remover um grupo do escopo de sincronização, selecione-o na lista de grupos sincronizados no momento e escolha **remover grupos**.
1. Quando todas as alterações forem feitas, selecione **salvar escopo de sincronização**.

Alterar o escopo da sincronização faz com que o domínio gerenciado sincronize novamente todos os dados. Os objetos que não são mais necessários no domínio gerenciado são excluídos e a ressincronização pode levar algum tempo para ser concluída.

## <a name="disable-scoped-synchronization"></a>Desabilitar sincronização com escopo

Para desabilitar a sincronização com escopo baseado em grupo para um domínio gerenciado, conclua as seguintes etapas:

1. No portal do Azure, pesquise e selecione **Azure AD Domain Services**. Escolha o domínio gerenciado, como *aaddscontoso.com*.
1. Selecione **sincronização** no menu do lado esquerdo.
1. Altere o *tipo de sincronização* de **escopo** para **todos**e selecione **salvar escopo de sincronização**.

Alterar o escopo da sincronização faz com que o domínio gerenciado sincronize novamente todos os dados. Os objetos que não são mais necessários no domínio gerenciado são excluídos e a ressincronização pode levar algum tempo para ser concluída.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o processo de sincronização, consulte [entender a sincronização no Azure AD Domain Services][concepts-sync].

<!-- INTERNAL LINKS -->
[scoped-sync-powershell]: powershell-scoped-synchronization.md
[concepts-sync]: synchronization.md
[tutorial-create-instance]: tutorial-create-instance.md
[create-azure-ad-tenant]: ../active-directory/fundamentals/sign-up-organization.md
[associate-azure-ad-tenant]: ../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md
