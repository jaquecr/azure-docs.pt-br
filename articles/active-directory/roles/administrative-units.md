---
title: Unidades administrativas no Azure Active Directory | Microsoft Docs
description: Use unidades administrativas para delegação mais granular de permissões no Azure Active Directory.
services: active-directory
documentationcenter: ''
author: curtand
manager: daveba
ms.service: active-directory
ms.topic: overview
ms.subservice: users-groups-roles
ms.workload: identity
ms.date: 09/22/2020
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0fb24d0cd2714969b5a888b1036f524c4c062d76
ms.sourcegitcommit: daab0491bbc05c43035a3693a96a451845ff193b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2020
ms.locfileid: "93027611"
---
# <a name="administrative-units-in-azure-active-directory"></a>Unidades administrativas no Azure Active Directory

Este artigo descreve como criar unidades administrativas no Azure AD (Azure Active Directory). Uma unidade administrativa é um recurso do Azure AD que pode ser um contêiner para outros recursos do Azure AD. Uma unidade administrativa pode conter apenas usuários e grupos.

Usando unidades administrativas, você pode conceder permissões de administrador restritas a um departamento, uma região ou outro segmento de sua organização que você define. Você pode usar unidades administrativas para delegar permissões a administradores regionais ou definir uma política em um nível granular. Por exemplo, um administrador de conta de usuário poderia atualizar as informações do perfil, redefinir senhas e atribuir licenças para usuários apenas na unidade administrativa dele.

Por exemplo, você pode delegar a especialistas de suporte regional a função [Administrador da Assistência Técnica](permissions-reference.md#helpdesk-administrator), restrita ao gerenciamento de apenas usuários na região à qual eles dão suporte.

## <a name="deployment-scenario"></a>Cenário de implantação

Pode ser útil restringir o escopo administrativo usando unidades administrativas em organizações compostas por divisões independentes de qualquer tipo. Considere o exemplo de uma grande universidade composta por muitas escolas autônomas (Escola de Negócios, Escola de Engenharia e assim por diante). Cada escola tem uma equipe de administradores de TI que controlam o acesso, gerenciam usuários e definem políticas para a escola deles. 

Um administrador central poderia:

- Criar uma função com permissões administrativas somente para usuários do Azure AD na unidade administrativa da escola de negócios.
- Criar uma unidade administrativa para a Escola de Negócios.
- Popular a unidade administrativa com apenas os alunos e os funcionários da escola de negócios.
- Adicionar a equipe de TI da escola de negócios à função, juntamente com o escopo dela.

## <a name="license-requirements"></a>Requisitos de licença

Para usar unidades administrativas, é necessária uma licença do Azure Active Directory Premium para cada administrador da unidade administrativa e licenças do Azure Active Directory Gratuito para membros da unidade administrativa. Para saber mais, consulte [Introdução ao AD Premium do Azure](../fundamentals/active-directory-get-started-premium.md).

## <a name="manage-administrative-units"></a>Gerenciar unidades administrativas

Você pode gerenciar unidades administrativas usando o portal do Azure, os cmdlets e scripts do PowerShell ou o Microsoft Graph. Para obter mais informações, consulte:

- [Criar, remover, popular e adicionar funções a unidades administrativas](admin-units-manage.md): inclui procedimentos detalhados completos.
- [Trabalhar com unidades administrativas](/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0&preserve-view=true): aborda como trabalhar com unidades administrativas usando o PowerShell.
- [Suporte ao Graph da unidade administrativa](/graph/api/resources/administrativeunit?view=graph-rest-1.0&preserve-view=true): fornece uma documentação detalhada no Microsoft Graph para unidades administrativas.

### <a name="plan-your-administrative-units"></a>Planejar suas unidades administrativas

Você pode usar unidades administrativas para agrupar logicamente os recursos do Azure AD. Por exemplo, para uma organização cujo departamento de TI está globalmente disperso, pode fazer sentido criar unidades administrativas que definem esses limites geográficos. Em outro cenário, em que uma organização multinacional tem varias *suborganizações* , semiautônomas nas operações delas, uma unidade administrativa pode representar cada suborganização.

Os critérios em que as unidades administrativas são criadas são guiados pelos requisitos exclusivos de uma organização. As unidades administrativas são uma forma comum de definir a estrutura nos serviços Microsoft 365. Recomendamos que você prepare suas unidades administrativas considerando o uso delas nos serviços Microsoft 365. Você pode obter o valor máximo das unidades administrativas quando pode associar recursos comuns no Microsoft 365 em uma unidade administrativa.

Você pode esperar que a criação de unidades administrativas na organização passe pelas seguintes fases:

1. **Adoção inicial** : sua organização começará a criar unidades administrativas com base em critérios iniciais e o número de unidades administrativas aumentará à medida que os critérios forem refinados.
1. **Remoção** : depois que os critérios estiverem bem definidos, as unidades administrativas que não forem mais necessárias serão excluídas.
1. **Estabilização** : sua estrutura organizacional está bem definida e o número de unidades administrativas não será alterado significativamente em curto prazo.

## <a name="currently-supported-scenarios"></a>Cenários com suporte no momento

Como Administrador Global ou Administrador de Funções com Privilégios, você pode usar o portal do Azure AD para criar unidades administrativas, adicionar usuários como membros de unidades administrativas e atribuir a equipe de TI a funções de administrador no escopo da unidade administrativa. Os administradores no escopo da unidade administrativa podem usar o Centro de administração do Microsoft 365 para o gerenciamento básico de usuários nas unidades administrativas deles.

Além disso, você pode adicionar grupos como membros de uma unidade administrativa. Um administrador de grupo no escopo da unidade administrativa pode gerenciá-los usando o PowerShell, o Microsoft Graph e o portal do Azure AD.

As seguintes tabelas descrevem o suporte atual para cenários de unidades administrativas:

### <a name="administrative-unit-management"></a>Gerenciamento de unidades administrativas

| Permissões |   Grafo/PowerShell   | Portal do Azure AD | Centro de administração do Microsoft 365 | 
| -- | -- | -- | -- |
| Criar e excluir unidades administrativas   |    Com suporte    |   Com suporte   |    Sem suporte | 
| Adicionar e remover membros de unidades administrativas individualmente    |   Com suporte    |   Com suporte   |    Sem suporte | 
| Adicionar e remover membros de unidades administrativas em massa usando arquivos CSV   |    Sem suporte     |  Com suporte   |    Nenhum plano para dar suporte | 
| Atribuir administradores no escopo da unidade administrativa  |     Com suporte    |   Com suporte    |   Sem suporte | 
| Adicionar e remover membros da unidade administrativa dinamicamente com base em atributos | Sem suporte | Sem suporte | Sem suporte 

### <a name="user-management"></a>Gerenciamento de Usuários

| Permissões |   Grafo/PowerShell   | Portal do Azure AD | Centro de administração do Microsoft 365 |
| -- | -- | -- | -- |
| Gerenciamento de propriedades do usuário, senhas e licenças no escopo da unidade administrativa   |    Com suporte     |  Com suporte   |   Com suporte |
| Bloqueio e desbloqueio de entradas de usuário no escopo da unidade administrativa    |   Com suporte   |    Com suporte   |    Com suporte |
| Gerenciamento de credenciais de autenticação multifator do usuário no escopo da unidade administrativa   |    Com suporte   |   Com suporte   |   Sem suporte |

### <a name="group-management"></a>Gerenciamento de grupos

| Permissões |   Grafo/PowerShell   | Portal do Azure AD | Centro de administração do Microsoft 365 |
| -- | -- | -- | -- |
| Gerenciamento de membros e propriedades do grupo no escopo da unidade administrativa     |  Com suporte   |    Com suporte    |  Sem suporte |
| Gerenciamento de licenciamento de grupo no escopo da unidade administrativa   |    Com suporte  |    Com suporte   |   Sem suporte |


As unidades administrativas aplicam o escopo somente às permissões de gerenciamento. Elas não impedem os membros ou administradores de usar as [permissões de usuário padrão](../fundamentals/users-default-permissions.md) para procurar outros usuários, grupos ou recursos fora da unidade administrativa. No centro de administração do Microsoft 365, os usuários fora de uma unidade administrativa do administrador com escopo são filtrados. Mas você pode procurar outros usuários no portal do Azure AD, no PowerShell e em outros serviços da Microsoft.

## <a name="next-steps"></a>Próximas etapas

- [Gerenciar unidades administrativas](admin-units-manage.md)
- [Gerenciar usuários em unidades administrativas](admin-units-add-manage-users.md)
- [Gerenciar grupos em unidades administrativas](admin-units-add-manage-groups.md)
- [Atribuir funções a uma unidade administrativa](admin-units-assign-roles.md)
