---
title: Como responder a alertas do Azure defender para Key Vault
description: Saiba mais sobre as etapas necessárias para responder a alertas do Azure defender para Key Vault.
author: memildin
ms.author: memildin
ms.date: 9/22/2020
ms.topic: how-to
ms.service: security-center
manager: rkarlin
ms.openlocfilehash: 6a40ffab652a6ae8671d6cd1c0dd9336764ce2c4
ms.sourcegitcommit: 400f473e8aa6301539179d4b320ffbe7dfae42fe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92791929"
---
# <a name="respond-to-azure-defender-for-key-vault-alerts"></a>Responder a alertas do Azure Defender para Key Vault
Quando você recebe um alerta do Azure defender para Key Vault, recomendamos investigar e responder ao alerta conforme descrito abaixo. O Azure defender para Key Vault protege aplicativos e credenciais, portanto, mesmo que você esteja familiarizado com o aplicativo ou o usuário que disparou o alerta, é importante verificar a situação em torno de cada alerta.  

Todos os alertas do Azure defender para Key Vault, inclui os seguintes elementos:

- ID de objeto
- Nome principal do usuário ou endereço IP do recurso suspeito

> [!TIP]
> Com base no *tipo* de acesso que ocorreu, alguns campos podem não estar disponíveis. Por exemplo, se o cofre de chaves foi acessado por um aplicativo, você não verá um nome principal de usuário associado. Se o tráfego foi originado de fora do Azure, você não verá uma ID de objeto.

## <a name="step-1-contact"></a>Etapa 1. Contact

1. Verifique se o tráfego foi originado de dentro de seu locatário do Azure. Se o Firewall do cofre de chaves estiver habilitado, é provável que você tenha fornecido acesso ao usuário ou ao aplicativo que disparou esse alerta.
1. Se você não conseguir verificar a origem do tráfego, continue para a [etapa 2. Mitigação imediata](#step-2-immediate-mitigation).
1. Se você puder identificar a origem do tráfego em seu locatário, entre em contato com o usuário ou o proprietário do aplicativo. 

> [!CAUTION]
> O Azure defender para Key Vault foi projetado para ajudar a identificar atividades suspeitas causadas por credenciais roubadas. **Não** ignore o alerta simplesmente porque você reconhece o usuário ou o aplicativo. Contate o proprietário do aplicativo ou o usuário e verifique se a atividade foi legítima. Você pode criar uma regra de supressão para eliminar o ruído, se necessário. Saiba mais em [suprimir alertas do Azure defender](alerts-suppression-rules.md).


## <a name="step-2-immediate-mitigation"></a>Etapa 2. Mitigação imediata 
Se você não reconhece o usuário ou o aplicativo, ou se você acredita que o acesso não deveria ter sido autorizado:

- Se o tráfego vier de um endereço IP não reconhecido:
    1. Habilite o firewall Azure Key Vault conforme descrito em [configurar Azure Key Vault firewalls e redes virtuais](../key-vault/general/network-security.md).
    1. Configure o firewall com recursos e redes virtuais confiáveis.

- Se a origem do alerta fosse um aplicativo não autorizado ou um usuário suspeito:
    1. Abra as configurações de política de acesso do cofre de chaves.
    1. Remova a entidade de segurança correspondente ou restrinja as operações que a entidade de segurança pode executar.  

- Se a origem do alerta tiver uma função de Azure Active Directory em seu locatário:
    1. Contate o administrador.
    1. Determine se há a necessidade de reduzir ou revogar as permissões de Azure Active Directory.

## <a name="step-3-identify-impact"></a>Etapa 3. Identificar o impacto 
Quando o impacto for mitigado, investigue os segredos no cofre de chaves que foram afetados:
1. Abra a página "segurança" no Azure Key Vault e exiba o alerta disparado.
1. Selecione o alerta específico que foi disparado.
    Examine a lista de segredos que foram acessados e o carimbo de data/hora.
1. Opcionalmente, se você tiver os logs de diagnóstico do Key Vault habilitados, examine as operações anteriores para o IP do chamador correspondente, a entidade de usuário ou a ID de objeto.  

## <a name="step-4-take-action"></a>Etapa 4. Executar ação 
Quando você compilou sua lista de segredos, chaves e certificados que foram acessados pelo usuário ou aplicativo suspeito, você deve girar esses objetos imediatamente.

1. Os segredos afetados devem ser desabilitados ou excluídos do cofre de chaves.
1. Se as credenciais foram usadas para um aplicativo específico:
    1. Entre em contato com o administrador do aplicativo e peça para auditar seu ambiente para qualquer uso das credenciais comprometidas desde que elas foram comprometidas.
    1. Se as credenciais comprometidas foram usadas, o proprietário do aplicativo deverá identificar as informações que foram acessadas e atenuar o impacto.


## <a name="next-steps"></a>Próximas etapas

Esta página explicou o processo de responder a um alerta do Azure defender para Key Vault. Para obter informações relacionadas, consulte as seguintes páginas:

- [Introdução ao Azure Defender para Key Vault](defender-for-key-vault-introduction.md)
- [Suprimir alertas do Azure Defender](alerts-suppression-rules.md)
- [Exportar continuamente os dados da central de segurança](continuous-export.md)