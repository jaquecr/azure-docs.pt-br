---
title: 'Tutorial: integração do SSO (logon único) do Azure Active Directory com o IntSights | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o IntSights.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 08/06/2020
ms.author: jeedes
ms.openlocfilehash: 5f8995e9473e8f0cbcf9bd15441ab164e2d6f755
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92459893"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-intsights"></a>Tutorial: integração do SSO (logon único) do Azure Active Directory ao IntSights

Neste tutorial, você aprenderá a integrar o IntSights ao Azure AD (Azure Active Directory). Ao integrar o IntSights ao Azure AD, você poderá:

* Controlar no Azure AD quem tem acesso ao IntSights.
* Permitir que os usuários entrem automaticamente no IntSights com suas contas do Azure AD.
* Gerenciar suas contas em um local central: o portal do Azure.

Para saber mais sobre a integração de aplicativos SaaS ao Azure AD, confira [O que é o acesso de aplicativos e o logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para começar, você precisará dos seguintes itens:

* Uma assinatura do Azure AD. Caso você não tenha uma assinatura, obtenha uma [conta gratuita](https://azure.microsoft.com/free/).
* Uma assinatura do IntSights habilitada para SSO (logon único).

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, você configurará e testará o SSO do Azure AD em um ambiente de teste.

* O IntSights dá suporte ao SSO iniciado por **IDP**

* O IntSights dá suporte ao provisionamento de usuário **Just-In-Time**

* Depois de configurar o IntSights, você poderá impor controles de sessão, que protegem contra exfiltração e infiltração de dados confidenciais da sua organização em tempo real. O controle da sessão é estendido do acesso condicional. [Saiba como impor o controle de sessão com o Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-any-app).

## <a name="adding-intsights-from-the-gallery"></a>Adicionar o IntSights da galeria

Para configurar a integração do IntSights ao Azure AD, você precisa adicionar o IntSights por meio da galeria à sua lista de aplicativos SaaS gerenciados.

1. Entre no [portal do Azure](https://portal.azure.com) usando uma conta corporativa ou de estudante ou uma conta pessoal da Microsoft.
1. No painel de navegação esquerdo, escolha o serviço **Azure Active Directory** .
1. Navegue até **Aplicativos Empresariais** e, em seguida, escolha **Todos os Aplicativos** .
1. Para adicionar um novo aplicativo, escolha **Novo aplicativo** .
1. Na seção **Adicionar da galeria** , digite **IntSights** na caixa de pesquisa.
1. Selecione **IntSights** no painel de resultados e adicione o aplicativo. Aguarde alguns segundos enquanto o aplicativo é adicionado ao seu locatário.


## <a name="configure-and-test-azure-ad-sso-for-intsights"></a>Configurar e testar o SSO do Azure AD com o IntSights

Configure e teste o SSO do Azure AD com o IntSights usando um usuário de teste chamado **B.Fernandes** . Para que o SSO funcione, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do IntSights.

Para configurar e testar o SSO do Azure AD com o IntSights, conclua os seguintes blocos de construção:

1. **[Configurar o SSO do Azure AD](#configure-azure-ad-sso)** – para permitir que os usuários usem esse recurso.
    1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** para testar o logon único do Azure AD com B.Fernandes.
    1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que B.Fernandes use o logon único do Azure AD.
1. **[Configurar o SSO do IntSights](#configure-intsights-sso)** – para definir as configurações de logon único no lado do aplicativo.
    1. **[Criar um usuário de teste do IntSights](#create-intsights-test-user)** – para ter um equivalente de B.Fernandes no IntSights que esteja vinculado à representação de usuário do Azure AD.
1. **[Testar o SSO](#test-sso)** – para verificar se a configuração funciona.

## <a name="configure-azure-ad-sso"></a>Configurar o SSO do Azure AD

Siga estas etapas para habilitar o SSO do Azure AD no portal do Azure.

1. No [portal do Azure](https://portal.azure.com/), na página de integração de aplicativos do **IntSights** , localize a seção **Gerenciar** e escolha **logon único** .
1. Na página **Selecionar um método de logon único** , escolha **SAML** .
1. Na página **Configurar o logon único com o SAML** , clique no ícone de edição/caneta da **Configuração Básica do SAML** para editar as configurações.

   ![Editar a Configuração Básica de SAML](common/edit-urls.png)

1. Na página **Configurar logon único com SAML** , insira os valores para os seguintes campos:

    a. No **identificador** caixa de texto, digite uma URL usando o seguinte padrão: `https://<SUBDOMAIN>.intsights.com/auth/saml-callback/azure`

    b. No **URL de resposta** caixa de texto, digite uma URL usando o seguinte padrão: `https://<SUBDOMAIN>.intsights.com/auth/saml-callback/azure`

    > [!NOTE]
    > Esses valores não são reais. Atualize esses valores com o Identificador e a URL de Resposta reais. Contate a [equipe de suporte ao cliente do IntSights](mailto:supportteam@intsights.com) para obter esses valores. Você também pode consultar os padrões exibidos na seção **Configuração Básica de SAML** no portal do Azure.

1. O aplicativo IntSights espera as declarações do SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizados de acordo com a sua configuração de atributos do token SAML. A captura de tela a seguir mostra a lista de atributos padrão.

    ![image](common/default-attributes.png)

1. Além do indicado acima, o aplicativo IntSights espera que mais alguns atributos sejam passados novamente na resposta SAML, que são mostrados abaixo. Esses atributos também são pré-populados, mas você pode examiná-los de acordo com seus requisitos.
    
    | Nome | Atributo de Origem |
    | -----| ---------------- |
    | firstName | user.givenname |
    | lastName | user.surname |
    | intsightsAccountId | < intsightsAccountId > |
    | intsightsRole | < intsightsRole > |

    > [!NOTE]
    > **intsightsAccountId** e **intsightsRole** são declarações opcionais que não são adicionadas por padrão e devem ser adicionadas manualmente somente quando o provisionamento de usuário **Just In Time** está habilitado.

1. Na página **Configurar o logon único com o SAML** , na seção **Certificado de Autenticação SAML** , localize **Certificado (Base64)** e selecione **Baixar** para baixar o certificado e salvá-lo no computador.

    ![O link de download do Certificado](common/certificatebase64.png)

1. Na seção **Configurar o IntSights** , copie as URLs apropriadas de acordo com suas necessidades.

    ![Copiar URLs de configuração](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Nesta seção, você criará um usuário de teste no portal do Azure chamado B.Fernandes.

1. No painel esquerdo do portal do Azure, escolha **Azure Active Directory** , **Usuários** e, em seguida, **Todos os usuários** .
1. Selecione **Novo usuário** na parte superior da tela.
1. Nas propriedades do **Usuário** , siga estas etapas:
   1. No campo **Nome** , insira `B.Simon`.  
   1. No campo **Nome de usuário** , insira username@companydomain.extension. Por exemplo, `B.Simon@contoso.com`.
   1. Marque a caixa de seleção **Mostrar senha** e, em seguida, anote o valor exibido na caixa **Senha** .
   1. Clique em **Criar** .

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que B.Fernandes use o logon único do Azure concedendo a ela acesso ao IntSights.

1. No portal do Azure, selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos** .
1. Na lista de aplicativos, selecione **IntSights** .
1. Na página de visão geral do aplicativo, localize a seção **Gerenciar** e escolha **Usuários e grupos** .

   ![O link “Usuários e grupos”](common/users-groups-blade.png)

1. Escolha **Adicionar usuário** e, em seguida, **Usuários e grupos** na caixa de diálogo **Adicionar Atribuição** .

    ![O link Adicionar Usuário](common/add-assign-user.png)

1. Na caixa de diálogo **Usuários e grupos** , selecione **B.Fernandes** na lista Usuários e clique no botão **Selecionar** na parte inferior da tela.
1. Se você estiver esperando um valor de função na declaração SAML, na caixa de diálogo **Selecionar Função** , escolha a função apropriada para o usuário da lista e, em seguida, clique no botão **Escolher** na parte inferior da tela.
1. Na caixa de diálogo **Adicionar atribuição** , clique no botão **Atribuir** .

## <a name="configure-intsights-sso"></a>Configurar o SSO do IntSights

Para configurar o logon único no lado do **IntSights** , é necessário enviar o **Certificado (Base64)** baixado e as URLs apropriadas copiadas do portal do Azure para a [equipe de suporte do IntSights](mailto:supportteam@intsights.com). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

### <a name="create-intsights-test-user"></a>Criar usuário de teste do IntSights

Nesta seção, um usuário chamado B.Fernandes será criado no IntSights. O IntSights é compatível com o provisionamento de usuário just-in-time, que está habilitado por padrão. Não há itens de ação para você nesta seção. Se ainda não existir um usuário no IntSights, ele será criado após a autenticação.

## <a name="test-sso"></a>Testar o SSO 

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco IntSights no Painel de Acesso, você deverá ser conectado automaticamente ao IntSights para o qual configurou o SSO. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Recursos adicionais

- [ Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure ](./tutorial-list.md)

- [O que é o acesso a aplicativos e logon único com o Azure Active Directory? ](../manage-apps/what-is-single-sign-on.md)

- [O que é o acesso condicional no Azure Active Directory?](../conditional-access/overview.md)

- [Experimentar o IntSights com o Azure AD](https://aad.portal.azure.com/)

- [O que é controle de sessão no Microsoft Cloud App Security?](/cloud-app-security/proxy-intro-aad)

- [Como proteger o IntSights com visibilidade e controles avançados](/cloud-app-security/proxy-intro-aad)