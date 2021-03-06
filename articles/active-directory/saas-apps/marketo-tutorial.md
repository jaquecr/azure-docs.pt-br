---
title: 'Tutorial: Integração do Azure Active Directory ao Marketo | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Marketo.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 02/19/2019
ms.author: jeedes
ms.openlocfilehash: 493e34ff60383ce31d185bddd684e72ff6aee3af
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92458276"
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>Tutorial: Integração do Azure Active Directory com o Marketo

Neste tutorial, você aprenderá a integrar o Marketo ao Azure AD (Azure Active Directory).
A integração do Marketo ao Azure AD oferece os seguintes benefícios:

* No Azure AD, você pode controlar quem tem acesso ao Marketo.
* Você pode permitir que os usuários sejam conectados automaticamente ao Marketo (logon único) com suas contas do Azure AD.
* Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](../manage-apps/what-is-single-sign-on.md).
Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Prerequisites

Para configurar a integração do Azure AD com o Marketo, você precisará dos seguintes itens:

* Uma assinatura do Azure AD. Se não tiver um ambiente do Azure AD, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/)
* Assinatura habilitada para logon único do Marketo

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, você configurará e testará o logon único do Azure AD em um ambiente de teste.

* O Marketo dá suporte ao SSO iniciado por **IDP**

## <a name="adding-marketo-from-the-gallery"></a>Adicionar o Marketo da galeria

Para configurar a integração do Marketo ao Azure AD, você precisará adicionar o Marketo da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Marketo da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)** , no painel navegação à esquerda, clique no ícone **Azure Active Directory** .

    ![O botão Azure Active Directory](common/select-azuread.png)

2. Navegue até **Aplicativos Empresariais** e, em seguida, selecione a opção **Todos os Aplicativos** .

    ![A folha Aplicativos empresariais](common/enterprise-applications.png)

3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo](common/add-new-app.png)

4. Na caixa de pesquisa, digite **Marketo** , selecione **Marketo** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

     ![Marketo na lista de resultados](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Marketo, com base em um usuário de teste chamado **Brenda Fernandes** .
Para que o logon único funcione, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Marketo.

Para configurar e testar o logon único do Azure AD com o Marketo, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Configurar o logon único do Marketo](#configure-marketo-single-sign-on)** – para definir as configurações de logon único no lado do aplicativo.
3. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Criar um usuário de teste do Marketo](#create-marketo-test-user)** – para ter um equivalente de Brenda Fernandes no Marketo que esteja vinculado à representação de usuário do Azure AD.
6. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no portal do Azure.

Para configurar o logon único do Azure AD com o Marketo, execute as seguintes etapas:

1. No [portal do Azure](https://portal.azure.com/), na página de integração de aplicativos do **Marketo** , selecione **Logon único** .

    ![Link Configurar logon único](common/select-sso.png)

2. Na caixa de diálogo **Selecionar um método de logon único** , selecione o modo **SAML/WS-Fed** para habilitar o logon único.

    ![Modo de seleção de logon único](common/select-saml-option.png)

3. Na página **Definir logon único com SAML** , clique no ícone **Editar** para abrir a caixa de diálogo **Configuração básica do SAML** .

    ![Editar a Configuração Básica de SAML](common/edit-urls.png)

4. Na página **Configurar Logon Único com SAML** , execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do Marketo](common/idp-intiated.png)

    a. No **identificador** caixa de texto, digite uma URL usando o seguinte padrão: `https://saml.marketo.com/sp`

    b. No **URL de resposta** caixa de texto, digite uma URL usando o seguinte padrão: `https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE]
    > Esses valores não são reais. Atualize esses valores com o Identificador e a URL de Resposta reais. Contate a [equipe de suporte ao cliente do Marketo](https://investors.marketo.com/contactus.cfm) para obter esses valores. Você também pode consultar os padrões exibidos na seção **Configuração Básica de SAML** no portal do Azure.

5. Na página **Configurar logon único com SAML** , na seção **Certificado de Autenticação SAML** , clique em **Fazer o download** para fazer o download do **Certificado (Base64)** usando as opções fornecidas de acordo com seus requisitos e salve-o no computador.

    ![O link de download do Certificado](common/certificatebase64.png)

6. Na seção **Configurar o Marketo** , copie as URLs apropriadas de acordo com suas necessidades.

    ![Copiar URLs de configuração](common/copy-configuration-urls.png)

    a. URL de logon

    b. Identificador do Azure AD

    c. URL de logoff

### <a name="configure-marketo-single-sign-on"></a>Configurar o logon único do Marketo

1. Para obter a Id do Munchkin do aplicativo, faça logon no Marketo usando credenciais de administrador e execute as seguintes ações:
   
    a. Faça logon usando credenciais de administrador de aplicativo do Marketo.
   
    b. Clique no botão **Admin** no painel de navegação superior.
   
    ![A captura de tela mostra Administrador selecionado no painel de navegação.](./media/marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navegue até o menu Integração e clique no link do **Munchkin** .
   
    ![A captura de tela mostra o Munchkin selecionado em Integração.](./media/marketo-tutorial/tutorial_marketo_11.png)
   
    d. Copie a identificação do Munchkin mostrada na tela e conclua sua URL de resposta no assistente de configuração do Azure AD.
   
    ![A captura de tela mostra a página Munchkin em que você pode copiar a ID da Conta.](./media/marketo-tutorial/tutorial_marketo_12.png) 

2. Para configurar o SSO no aplicativo, siga estas etapas:
   
    a. Faça logon usando credenciais de administrador de aplicativo do Marketo.
   
    b. Clique no botão **Admin** no painel de navegação superior.
   
    ![A captura de tela mostra Administrador selecionado no painel de navegação.](./media/marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navegue até o menu Integração e clique em **Logon Único** .
   
    ![A captura de tela mostra o Logon Único selecionado em Integração.](./media/marketo-tutorial/tutorial_marketo_07.png) 
   
    d. Para habilitar as configurações de SAML, clique no botão **Editar** .
   
    ![A captura de tela mostra as Configurações de SSO em que você pode selecionar EDITAR.](./media/marketo-tutorial/tutorial_marketo_08.png) 
   
    e. Configurações de logon único **habilitadas** .
   
    f. Cole o **Identificador do Azure AD** na caixa de texto **ID do Emissor** .
   
    g. Na caixa de texto **ID da Entidade** , insira a URL como `http://saml.marketo.com/sp`.
   
    h. Selecione o local da ID de usuário como **elemento do Identificador de Nome** .
   
    ![A captura de tela mostra Editar Configurações do SAML em que você pode inserir os valores descritos.](./media/marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > Se o identificador de usuário não for um valor de UPN, altere o valor na guia Atributo.
   
    i. Carregue o certificado que você baixou do assistente de configuração do Azure AD. **Salve** as configurações.
   
    j. Edite as configurações de redirecionamento de páginas.
   
    k. Cole a **URL de Logon** na caixa de texto **URL de Logon** .
   
    l. Cole a **URL de Logoff** na caixa de texto **URL de Logoff** .
   
    m. Na **URL de erro** , copie a **URL da instância do Marketo** e clique no botão **Salvar** para salvar as configurações.
   
    ![A captura de tela mostra a caixa de diálogo Editar Páginas de Redirecionamento em que você pode inserir os valores descritos.](./media/marketo-tutorial/tutorial_marketo_10.png)

3. Para habilitar o SSO para usuários, conclua as seguintes ações:
   
    a. Faça logon usando credenciais de administrador de aplicativo do Marketo.
   
    b. Clique no botão **Admin** no painel de navegação superior.
   
    ![A captura de tela mostra Administrador selecionado no painel de navegação.](./media/marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navegue até o menu **Segurança** e clique em **Configurações de Logon** .
   
    ![A captura de tela mostra a opção Configurações de Logon selecionada em Segurança.](./media/marketo-tutorial/tutorial_marketo_13.png)
   
    d. Marque a opção **Exigir SSO** e **salve** as configurações.
   
    ![A captura de tela mostra as Configurações de Força de Senha em que você pode selecionar Exigir SSO.](./media/marketo-tutorial/tutorial_marketo_14.png)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD 

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

1. No Portal do Azure, no painel esquerdo, selecione **Azure Active Directory** , selecione **Usuários** e, em seguida, **Todos os usuários** .

    ![Os links “Usuários e grupos” e “Todos os usuários”](common/users.png)

2. Selecione **Novo usuário** na parte superior da tela.

    ![Botão Novo usuário](common/new-user.png)

3. Nas Propriedades do usuário, execute as etapas a seguir.

    ![A caixa de diálogo Usuário](common/user-properties.png)

    a. No campo **Nome** , insira **BrendaFernandes** .
  
    b. No campo **Nome de usuário** , digite **brendafernandes\@dominiodaempresa.extensao**  
    Por exemplo, BrittaSimon@contoso.com

    c. Marque a caixa de seleção **Mostrar senha** e, em seguida, anote o valor exibido na caixa Senha.

    d. Clique em **Criar** .

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao Marketo.

1. No portal do Azure, selecione **Aplicativos Empresariais** , **Todos os aplicativos** e, em seguida, **Marketo** .

    ![Folha de aplicativos empresariais](common/enterprise-applications.png)

2. Na lista de aplicativos, selecione **Marketo** .

    ![O link do Marketo na lista Aplicativos](common/all-applications.png)

3. No menu à esquerda, selecione **Usuários e grupos** .

    ![O link “Usuários e grupos”](common/users-groups-blade.png)

4. Escolha o botão **Adicionar usuário** e, em seguida, escolha **Usuários e grupos** na caixa de diálogo **Adicionar Atribuição** .

    ![O painel Adicionar Atribuição](common/add-assign-user.png)

5. Na caixa de diálogo **Usuários e grupos** , escolha **Brenda Fernandes** na lista Usuários e clique no botão **Selecionar** na parte inferior da tela.

6. Se você estiver esperando um valor de função na declaração SAML, na caixa de diálogo **Selecionar função** , escolha a função de usuário apropriada na lista e clique no botão **Selecionar** na parte inferior da tela.

7. Na caixa de diálogo **Adicionar atribuição** , clique no botão **Atribuir** .

### <a name="create-marketo-test-user"></a>Criar um usuário de teste do Marketo

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Marketo. siga estas etapas para criar um usuário na plataforma do Marketo.

1. Faça logon usando credenciais de administrador de aplicativo do Marketo.

2. Clique no botão **Admin** no painel de navegação superior.
   
    ![A captura de tela mostra Administrador selecionado no painel de navegação.](./media/marketo-tutorial/tutorial_marketo_06.png) 

3. Navegue até o menu **Segurança** e clique em **Usuários e Funções**
   
    ![A captura de tela mostra a opção Usuários e Funções selecionada em Segurança.](./media/marketo-tutorial/tutorial_marketo_19.png)  

4. Clique no link **Convidar Novo Usuário** na guia Usuários
   
    ![A captura de tela mostra Convidar Novo Usuário na guia Usuários.](./media/marketo-tutorial/tutorial_marketo_15.png) 

5. No assistente para Convidar Novo Usuário, preencha as informações a seguir
   
    a. Insira o endereço de **Email** do usuário na caixa de texto
   
    ![A captura de tela mostra a primeira etapa do assistente Convidar Novo Usuário em que você insere as informações do usuário.](./media/marketo-tutorial/tutorial_marketo_16.png)
   
    b. Insira o **Nome** na caixa de texto
   
    c. Insira o **Sobrenome** na caixa de texto
   
    d. Clique em **Avançar** .

6. Na guia **Permissões** , selecione **userRoles** e clique em **Avançar**
   
    ![A captura de tela mostra a primeira etapa do assistente Convidar Novo Usuário em que você insere permissões.](./media/marketo-tutorial/tutorial_marketo_17.png)
7. Clique no botão **Enviar** para enviar o convite de usuário
   
    ![A captura de tela mostra a primeira etapa do assistente Convidar Novo Usuário em que você insere sua mensagem.](./media/marketo-tutorial/tutorial_marketo_18.png)

8. Os usuários receberão a notificação de email e precisarão clicar no link e alterar a senha para ativar a conta. 

### <a name="test-single-sign-on"></a>Testar logon único 

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Marketo no Painel de Acesso, você deverá ser conectado automaticamente ao Marketo, para o qual você configurou o SSO. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Recursos adicionais

- [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](./tutorial-list.md)

- [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

- [O que é o acesso condicional no Azure Active Directory?](../conditional-access/overview.md)