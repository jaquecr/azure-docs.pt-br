---
title: 'Tutorial: integração do Azure Active Directory ao Degreed | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Degreed.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 08/27/2020
ms.author: jeedes
ms.openlocfilehash: 96f2c96e7770ec7acc690a1d057fef16db5b88ed
ms.sourcegitcommit: 4cb89d880be26a2a4531fedcc59317471fe729cd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92675967"
---
# <a name="tutorial-azure-active-directory-integration-with-degreed"></a>Tutorial: integração do Azure Active Directory com o Degreed

Neste tutorial, você aprende a integrar o Degreed ao Azure AD (Azure Active Directory).
A integração do Degreed ao Azure AD oferece os seguintes benefícios:

* No Azure AD, é possível controlar quem tem acesso ao Degreed.
* Você pode permitir que seus usuários entrem automaticamente no Degreed (logon único) com suas contas do Azure AD.
* Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](../manage-apps/what-is-single-sign-on.md).
Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Prerequisites

Para configurar a integração do Azure AD com o Degreed, você precisa dos seguintes itens:

* Uma assinatura do Azure AD. Se não tiver um ambiente do Azure AD, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/)
* Assinatura do Degreed habilitada para logon único

> [!NOTE]
> Essa integração também está disponível para uso do ambiente de Nuvem do Governo dos EUA do Azure AD. Encontre esse aplicativo na Galeria de Aplicativos de Nuvem do Governo dos EUA do Azure AD e configure-o da mesma forma que na nuvem pública.

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, você configurará e testará o logon único do Azure AD em um ambiente de teste.

* O Degreed dá suporte ao SSO iniciado por **SP**

* O Degreed dá suporte ao provisionamento de usuário **Just-In-Time**

* Depois de configurar o Degreed, você poderá impor o Controle de sessão, que protege contra a exfiltração e a infiltração de dados confidenciais da sua organização em tempo real. O controle da sessão é estendido do acesso condicional. [Saiba como impor o controle de sessão com o Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-aad)

## <a name="adding-degreed-from-the-gallery"></a>Adição do Degreed a partir da galeria

Para configurar a integração do Degreed ao Azure AD, você precisa adicionar o Degreed por meio da galeria à sua lista de aplicativos SaaS gerenciados.

1. Entre no [portal do Azure](https://portal.azure.com) usando uma conta corporativa ou de estudante ou uma conta pessoal da Microsoft.
1. No painel de navegação esquerdo, escolha o serviço **Azure Active Directory** .
1. Navegue até **Aplicativos Empresariais** e, em seguida, escolha **Todos os Aplicativos** .
1. Para adicionar um novo aplicativo, escolha **Novo aplicativo** .
1. Na seção **Adicionar por meio da galeria** , digite **Degreed** na caixa de pesquisa.
1. Selecione **Degreed** no painel de resultados e, em seguida, adicione o aplicativo. Aguarde alguns segundos enquanto o aplicativo é adicionado ao seu locatário.

## <a name="configure-and-test-azure-ad-sso"></a>Configurar e testar o SSO do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Degreed com base em um usuário de teste chamado **Brenda Fernandes** .
Para que o logon único funcione, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Degreed.

Para configurar e testar o logon único do Azure AD com o Degreed, você precisará concluir os seguintes blocos de construção:

1. **[Configurar o SSO do Azure AD](#configure-azure-ad-sso)** – para permitir que os usuários usem esse recurso.
    * **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
    * **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
2. **[Configurar o SSO do Degreed](#configure-degreed-sso)** – para definir as configurações de Logon Único no lado do aplicativo.
    * **[Criar um usuário de teste do Degreed](#create-degreed-test-user)** – para ter um equivalente de Brenda Fernandes no Degreed que esteja vinculado à representação de usuário do Azure AD.
3. **[Testar o SSO](#test-sso)** – para verificar se a configuração funciona.

## <a name="configure-azure-ad-sso"></a>Configurar o SSO do Azure AD

Siga estas etapas para habilitar o SSO do Azure AD no portal do Azure.

1. No [portal do Azure](https://portal.azure.com/), na página de integração de aplicativos do **Degreed** , localize a seção **Gerenciar** e selecione **logon único** .
1. Na página **Selecionar um método de logon único** , escolha **SAML** .
1. Na página **Configurar o logon único com o SAML** , clique no ícone de edição/caneta da **Configuração Básica do SAML** para editar as configurações.

   ![Editar a Configuração Básica de SAML](common/edit-urls.png)

4. Na seção **Configuração básica de SAML** , realize as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do Degreed](common/sp-identifier.png)

    a. Na caixa de texto **URL de Logon** , digite uma URL usando o seguinte padrão: `https://degreed.com/?orgsso=<company code>`

    b. Na caixa de texto **Identificador (ID da Entidade)** , digite uma URL usando o seguinte padrão: `https://degreed.com/<instancename>`

    c. No **URL de resposta** caixa de texto, digite uma URL usando o seguinte padrão: `https://degreed.com/SAML/<instancename>`
    
    > [!NOTE]
    > Esses valores não são reais. Você precisa atualizar esses valores com a URL de Logon, o Identificador e a URL de Resposta reais. Contate a [equipe de suporte ao cliente do Degreed](mailto:admin@degreed.com) para obter esses valores. Você também pode consultar os padrões exibidos na seção **Configuração Básica de SAML** no portal do Azure.

5. Na página **Configurar Logon Único com SAML** , na seção **Certificado de Autenticação SAML** , clique em **Baixar** para baixar o **XML de Metadados de Federação** usando as opções fornecidas de acordo com seus requisitos e salve-o no computador.

    ![O link de download do Certificado](common/metadataxml.png)

6. Na seção **Configurar o Degreed** , copie a URL apropriada de acordo com seus requisitos.

    ![Copiar URLs de configuração](common/copy-configuration-urls.png)

    a. URL de logon

    b. Identificador do Azure Ad

    c. URL de logoff

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD 

Nesta seção, você criará uma usuária de teste no portal do Azure chamada B.Fernandes.

1. No painel esquerdo no portal do Azure, selecione **Azure Active Directory** , selecione **Usuários** e, em seguida, **Todos os usuários** .
1. Na parte superior da tela, selecione **Novo usuário** .
1. Nas propriedades do **Usuário** , siga estas etapas:
   1. No campo **Nome** , insira **B.Fernandes** .  
   1. No campo **Nome de usuário** , insira `<username>@<companydomain>.<extension>`. Por exemplo: `B.Simon@contoso.com`.
   1. Marque a caixa de seleção **Mostrar senha** e, em seguida, anote o valor exibido na caixa **Senha** .
   1. Selecione **Criar** .

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que B.Fernandes use o logon único do Azure permitindo o acesso ao Degreed.

1. No portal do Azure, selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos** .
1. Na lista de aplicativos, selecione **Degreed** .
1. Na página de visão geral do aplicativo, localize a seção **Gerenciar** e escolha **Usuários e grupos** .

   ![O link “Usuários e grupos”](common/users-groups-blade.png)

1. Escolha **Adicionar usuário** e, em seguida, **Usuários e grupos** na caixa de diálogo **Adicionar Atribuição** .

    ![O link Adicionar Usuário](common/add-assign-user.png)

1. Na caixa de diálogo **Usuários e grupos** , selecione **B.Fernandes** na lista Usuários e clique no botão **Selecionar** na parte inferior da tela.
1. Se você estiver esperando um valor de função na declaração SAML, na caixa de diálogo **Selecionar Função** , escolha a função apropriada para o usuário da lista e, em seguida, clique no botão **Escolher** na parte inferior da tela.
1. Na caixa de diálogo **Adicionar atribuição** , clique no botão **Atribuir** .

### <a name="configure-degreed-sso"></a>Configurar o SSO do Degreed

Para configurar o logon único no lado do **Degreed** , é necessário enviar o **XML de metadados de federação** baixado e as URLs apropriadas copiadas do portal do Azure para a [equipe de suporte do Degreed](mailto:sso@degreed.com). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

### <a name="create-degreed-test-user"></a>Criar um usuário de teste do Degreed

O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Degreed. O Degreed dá suporte ao provisionamento just-in-time, que está habilitado por padrão.

Não há itens de ação para você nesta seção. Um novo usuário será criado durante uma tentativa de acessar o Degreed, caso ele ainda não exista.

> [!NOTE]
> Se você precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do Degreed](mailto:sso@degreed.com).


## <a name="test-sso"></a>Testar o SSO

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Degreed no Painel de Acesso, você deve ser conectado automaticamente ao Degreed para o qual você configurou o SSO. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Recursos adicionais

- [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](./tutorial-list.md)

- [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

- [O que é o Acesso Condicional no Azure Active Directory?](../conditional-access/overview.md)
