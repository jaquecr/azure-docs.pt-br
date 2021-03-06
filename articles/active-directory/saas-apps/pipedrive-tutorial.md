---
title: 'Tutorial: Integração do SSO (logon único) do Azure Active Directory ao Pipedrive | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Pipedrive.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 03/06/2020
ms.author: jeedes
ms.openlocfilehash: f85cb97406e8b6cbb4811268696fc36f47ec3adb
ms.sourcegitcommit: 4064234b1b4be79c411ef677569f29ae73e78731
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92896524"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-pipedrive"></a>Tutorial: Integração do SSO (logon único) do Azure Active Directory ao Pipedrive

Neste tutorial, você aprenderá como integrar o Pipedrive ao Azure AD (Azure Active Directory). Com a integração do Pipedrive ao Azure AD, você poderá:

* Controlar no Azure AD quem tem acesso ao Pipedrive.
* Permitir que seus usuários entrem automaticamente no Pipedrive com suas contas do Azure AD.
* Gerenciar suas contas em um local central: o portal do Azure.

Para saber mais sobre a integração de aplicativos SaaS ao Azure AD, confira [O que é o acesso de aplicativos e o logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para começar, você precisará dos seguintes itens:

* Uma assinatura do Azure AD. Caso você não tenha uma assinatura, obtenha uma [conta gratuita](https://azure.microsoft.com/free/).
* Uma assinatura do Pipedrive com SSO (logon único) habilitado.

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, você configurará e testará o SSO do Azure AD em um ambiente de teste.

* O Pipedrive dá suporte ao SSO iniciado por **SP e IDP**
* Depois de configurar o SSO do Pipedrive, você poderá impor um controle de sessão, que fornece proteção contra exfiltração e infiltração dos dados confidenciais da sua organização em tempo real. O controle da sessão é estendido do acesso condicional. [Saiba como impor o controle de sessão com o Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-any-app).


## <a name="adding-pipedrive-from-the-gallery"></a>Como adicionar o Pipedrive por meio da galeria

Para configurar a integração do Pipedrive ao Azure AD, você precisará adicionar o Pipedrive por meio da galeria à lista de aplicativos SaaS gerenciados.

1. Entre no [portal do Azure](https://portal.azure.com) usando uma conta corporativa ou de estudante ou uma conta pessoal da Microsoft.
1. No painel de navegação esquerdo, escolha o serviço **Azure Active Directory**.
1. Navegue até **Aplicativos Empresariais** e, em seguida, escolha **Todos os Aplicativos**.
1. Para adicionar um novo aplicativo, escolha **Novo aplicativo**.
1. Na seção **Adicionar por meio da galeria** , digite **Pipedrive** na caixa de pesquisa.
1. Selecione **Pipedrive** no painel de resultados e, em seguida, adicione o aplicativo. Aguarde alguns segundos enquanto o aplicativo é adicionado ao seu locatário.

## <a name="configure-and-test-azure-ad-single-sign-on-for-pipedrive"></a>Configurar e testar logon único do Azure AD para o Pipedrive

Configure e teste o SSO do Azure AD com o Pipedrive usando um usuário de teste chamado **B. Fernandes**. Para que o SSO funcione, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Pipedrive.

Para configurar e testar o SSO do Azure AD com o Pipedrive, conclua os seguintes blocos de construção:

1. **[Configurar o SSO do Azure AD](#configure-azure-ad-sso)** – para permitir que os usuários usem esse recurso.
    * **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** para testar o logon único do Azure AD com B.Fernandes.
    * **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que B.Fernandes use o logon único do Azure AD.
1. **[Configurar o SSO do Pipedrive](#configure-pipedrive-sso)** – para definir as configurações de logon único no lado do aplicativo.
    * **[Criar usuário de teste do Pipedrive](#create-pipedrive-test-user)** – para ter um equivalente de B. Fernandes no Pipedrive que esteja vinculado à representação do usuário no Azure AD.
1. **[Testar o SSO](#test-sso)** – para verificar se a configuração funciona.

## <a name="configure-azure-ad-sso"></a>Configurar o SSO do Azure AD

Siga estas etapas para habilitar o SSO do Azure AD no portal do Azure.

1. No [portal do Azure](https://portal.azure.com/), na página de integração de aplicativos do **Pipedrive** , localize a seção **Gerenciar** e selecione **Logon único**.
1. Na página **Selecionar um método de logon único** , escolha **SAML**.
1. Na página **Configurar o logon único com o SAML** , clique no ícone de edição/caneta da **Configuração Básica do SAML** para editar as configurações.

   ![Editar a Configuração Básica de SAML](common/edit-urls.png)

1. Na seção **Configuração Básica do SAML** , caso deseje configurar o aplicativo no modo iniciado por **IDP** , digite os valores dos seguintes campos:

    a. No **identificador** caixa de texto, digite uma URL usando o seguinte padrão: `https://<COMPANY-NAME>.pipedrive.com/sso/auth/samlp/metadata.xml`

    b. No **URL de resposta** caixa de texto, digite uma URL usando o seguinte padrão: `https://<COMPANY-NAME>.pipedrive.com/sso/auth/samlp`

1. Clique em **Definir URLs adicionais** e execute o passo seguinte se quiser configurar a aplicação no modo **SP** iniciado:

    Na caixa de texto **URL de logon** , digite um URL usando o seguinte padrão: `https://<COMPANY-NAME>.pipedrive.com/`

    > [!NOTE]
    > Esses valores não são reais. Atualize esses valores com o Identificador, a URL de Resposta e a URL de Logon reais. Contate a [equipe de suporte do Cliente do Pipedrive](mailto:support@pipedrive.com) para obter esses valores. Você também pode consultar os padrões exibidos na seção **Configuração Básica de SAML** no portal do Azure.

1. O aplicativo Pipedrive espera as declarações do SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizados de acordo com a sua configuração de atributos do token SAML. A captura de tela a seguir mostra a lista de atributos padrão.

    ![image](common/default-attributes.png)

1. Além do indicado acima, o aplicativo Pipedrive espera que mais alguns atributos sejam passados novamente na resposta SAML, que são mostrados abaixo. Esses atributos também são pré-populados, mas você pode examiná-los de acordo com seus requisitos.

    | Nome | Atributo de Origem|
    | ------------ | --------- |
    | email | user.mail |

1. Na página **Configurar o logon único com o SAML** , na seção **Certificado de Autenticação SAML** , localize **Certificado (Base64)** e selecione **Baixar** para baixar o certificado e salvá-lo no computador. Copie também **URL de Metadados de Federação de Aplicativo** e salve-o em seu computador.

    ![O link de download do Certificado](./media/pipedrive-tutorial/certificate-data.png)

1. Na seção **Configurar o Pipedrive** , copie as URLs apropriadas com base em seus requisitos.

    ![Copiar URLs de configuração](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Nesta seção, você criará um usuário de teste no portal do Azure chamado B.Fernandes.

1. No painel esquerdo do portal do Azure, escolha **Azure Active Directory** , **Usuários** e, em seguida, **Todos os usuários**.
1. Selecione **Novo usuário** na parte superior da tela.
1. Nas propriedades do **Usuário** , siga estas etapas:
   1. No campo **Nome** , insira `B.Simon`.  
   1. No campo **Nome de usuário** , insira username@companydomain.extension. Por exemplo, `B.Simon@contoso.com`.
   1. Marque a caixa de seleção **Mostrar senha** e, em seguida, anote o valor exibido na caixa **Senha**.
   1. Clique em **Criar**.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que B. Fernandes use o logon único do Azure permitindo a ela acesso ao Pipedrive.

1. No portal do Azure, selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.
1. Na lista de aplicativos, selecione **Pipedrive**.
1. Na página de visão geral do aplicativo, localize a seção **Gerenciar** e escolha **Usuários e grupos**.

   ![O link “Usuários e grupos”](common/users-groups-blade.png)

1. Escolha **Adicionar usuário** e, em seguida, **Usuários e grupos** na caixa de diálogo **Adicionar Atribuição**.

    ![O link Adicionar Usuário](common/add-assign-user.png)

1. Na caixa de diálogo **Usuários e grupos** , selecione **B.Fernandes** na lista Usuários e clique no botão **Selecionar** na parte inferior da tela.
1. Se você estiver esperando um valor de função na declaração SAML, na caixa de diálogo **Selecionar Função** , escolha a função apropriada para o usuário da lista e, em seguida, clique no botão **Escolher** na parte inferior da tela.
1. Na caixa de diálogo **Adicionar atribuição** , clique no botão **Atribuir**.

## <a name="configure-pipedrive-sso"></a>Configurar o SSO do Pipedrive

1. Em outra janela do navegador, entre no site do Pipedrive como administrador.

1. Clique em **Perfil do Usuário** e selecione **Configurações**.

    ![Captura de tela que mostra a opção "Configurações" selecionada no menu "Perfil do Usuário".](./media/pipedrive-tutorial/configure1.png)

1. Role para baixo até a central de segurança e selecione **Logon único**.

    ![Captura de tela que mostra a opção "Logon único" selecionada na "Central de Segurança".](./media/pipedrive-tutorial/configure2.png)

1. Na seção **Configuração SAML para Pipedrive** , execute as seguintes etapas:

    ![Captura de tela que mostra a seção "Configuração do SAML para Pipedrive" com todas as caixas de texto realçadas.](./media/pipedrive-tutorial/configure3.png)

    a. Na caixa de texto **Emissor** , cole o valor da **URL de Metadados de Federação do Aplicativo** que você copiou do portal do Azure.

    b. Na caixa de texto **URL de SSO (Logon Único)** , cole o valor da **URL de Logon** que você copiou do portal do Azure.

    c. Na caixa de texto **URL de SLO (Logoff Único)** , cole o valor da **URL de Logout** copiado do portal do Azure.

    d. Na caixa de texto **certificado x.509** , abra o arquivo **Certificado (Base64)** baixado do portal do Azure no Bloco de notas, copie o conteúdo dele e cole-o na caixa de texto **certificado x.509** e salve as alterações.

### <a name="create-pipedrive-test-user"></a>Criar usuário de teste do Pipedrive

1. Em outra janela do navegador, entre no site do Pipedrive como administrador.

1. Role para baixo até empresa e selecione **gerenciar usuários**.

    ![Captura de tela que mostra a opção "Gerenciar usuários" selecionada no menu "Empresa".](./media/pipedrive-tutorial/user1.png)

1. Clique em **Adicionar usuários**.
    
    ![Captura de tela que mostra a página "Gerenciar usuários" com o botão "Adicionar usuários" selecionado no lado direito.](./media/pipedrive-tutorial/user2.png)

1. Na seção **Gerenciar usuários** , realize as seguintes etapas:

    ![Configuração do Pipedrive](./media/pipedrive-tutorial/user3.png)

    a. Na caixa de texto **Email** , digite o endereço de email do usuário, como `B.Simon@contoso.com`.

    b. Na caixa de texto **Nome** , insira o nome do usuário.

    c. Na caixa de texto **Sobrenome** , insira o sobrenome do usuário.

    d. Clique em **Confirmar e convidar usuários**.

## <a name="test-sso"></a>Testar o SSO 

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Pipedrive no Painel de Acesso, você será conectado automaticamente ao aplicativo Pipedrive para o qual configurou o SSO. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Recursos adicionais

- [ Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure ](./tutorial-list.md)

- [O que é o acesso a aplicativos e logon único com o Azure Active Directory? ](../manage-apps/what-is-single-sign-on.md)

- [O que é o acesso condicional no Azure Active Directory?](../conditional-access/overview.md)

- [Experimentar o Pipedrive com o Azure AD](https://aad.portal.azure.com/)

- [O que é controle de sessão no Microsoft Cloud App Security?](/cloud-app-security/proxy-intro-aad)