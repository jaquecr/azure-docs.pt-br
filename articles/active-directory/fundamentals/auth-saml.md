---
title: Autenticação SAML com Azure Active Directory
description: Diretrizes arquitetônicas sobre a obtenção de autenticação SAML com Azure Active Directory
services: active-directory
author: BarbaraSelden
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.subservice: fundamentals
ms.topic: conceptual
ms.date: 10/10/2020
ms.author: baselden
ms.reviewer: ajburnle
ms.custom: it-pro, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ab14413de1f999747e5b3fb58b505e0a9258a55
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92441208"
---
# <a name="saml-authentication-with-azure-active-directory"></a>Autenticação SAML com Azure Active Directory

Security Assertion Markup Language (SAML) é um padrão aberto para a troca de dados de autenticação e autorização entre um provedor de identidade e um provedor de serviços. SAML é uma linguagem de marcação baseada em XML para asserções de segurança, que são instruções que os provedores de serviços usam para tomar decisões de controle de acesso. 

A especificação SAML define três funções:

* A entidade de segurança, geralmente um usuário
* O IdP (provedor de identidade)
* O provedor de serviços (SP)


## <a name="use-when"></a>Usar quando

Há a necessidade de fornecer uma experiência de SSO (logon único) para um aplicativo SAML corporativo.

Embora seja um dos casos de uso mais importantes que os endereços SAML são SSO, especialmente ao estender o SSO entre domínios de segurança, também há outros casos de uso (chamados perfis). 

![diagrama arquitetônico para SAML](./media/authentication-patterns/saml-auth.png)

## <a name="components-of-system"></a>Componentes do sistema

* **Usuário**: solicita um serviço do aplicativo.

* **Navegador da Web**: o componente com o qual o usuário interage.

* **Aplicativo Web**: aplicativo empresarial que dá suporte ao SAML e usa o Azure ad como IDP.

* **Token**: uma Asserção SAML (também conhecida como tokens SAML) que transporta conjuntos de declarações feitas pelo IDP sobre o princípio (usuário). Ele contém informações de autenticação, atributos e instruções de decisão de autorização.

* **Azure ad**: IDP do Enterprise Cloud que fornece SSO e autenticação multifator para aplicativos SAML. Ele sincroniza, mantém e gerencia informações de identidade para os usuários ao mesmo tempo em que fornece serviços de autenticação para aplicativos de confiança. 

## <a name="implement-saml-authentication-with-azure-ad"></a>Implementar a autenticação SAML com o Azure AD

* [Tutoriais para integração de aplicativos SaaS usando o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/saas-apps/tutorial-list) 

* [Configurando o logon único baseado em SAML para aplicativos que não são da Galeria](https://docs.microsoft.com/azure/active-directory/manage-apps/add-non-gallery-app) 

* [Como o Azure AD usa o protocolo SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)
