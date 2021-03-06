---
title: Configuração de serviço-QnA Maker
description: Entenda como e onde configurar os recursos.
ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: reference
ms.date: 11/9/2020
ms.openlocfilehash: eac930971cab041fbf398da1ac5f8a055412832d
ms.sourcegitcommit: 051908e18ce42b3b5d09822f8cfcac094e1f93c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94376852"
---
# <a name="service-configuration"></a>Configuração de serviço

Cada versão do QnA Maker usa um conjunto diferente de recursos do Azure (serviços). Este artigo descreve as personalizações com suporte para esses serviços. 

## <a name="app-service"></a>Serviço de Aplicativo

# <a name="qna-maker-ga-stable-release"></a>[QnA Maker GA (versão estável)](#tab/v1)

QnA Maker usa o serviço de aplicativo para fornecer o tempo de execução de consulta usado pela [API generateAnswer](https://docs.microsoft.com/rest/api/cognitiveservices/qnamakerruntime/runtime/generateanswer).

Essas configurações estão disponíveis no portal do Azure, para o serviço de aplicativo. As configurações estão disponíveis selecionando **configurações** e, em seguida, **configuração**.

Você pode definir uma configuração individual por meio da lista de configurações do aplicativo ou modificar várias configurações selecionando **edição avançada**.

|Recurso|Configuração|
|--|--|
|AzureSearchAdminKey|Pesquisa Cognitiva-usado para o armazenamento e o classificador do QnA Pair #1|
|AzureSearchName|Pesquisa Cognitiva-usado para o armazenamento e o classificador do QnA Pair #1|
|Defaultanswer|Texto de resposta quando nenhuma correspondência for encontrada|
|UserAppInsightsAppId|Log de chat e telemetria|
|UserAppInsightsKey|Log de chat e telemetria|
|UserAppInsightsName|Log de chat e telemetria|

Você precisa **reiniciar** o serviço na página **visão geral** do portal do Azure, quando terminar de fazer alterações.

# <a name="qna-maker-managed-preview-release"></a>[Gerenciado QnA Maker (versão de visualização)](#tab/v2)

As personalizações do serviço de aplicativo não se aplicam ao QnA Maker gerenciado (versão prévia).

---

## <a name="qna-maker-service"></a>Serviço QnA Maker

O serviço de QnA Maker fornece configuração para que os usuários a seguir colaborem em um único serviço de QnA Maker e todas as suas bases de dados de conhecimento.

Saiba [como adicionar colaboradores](./how-to/collaborate-knowledge-base.md) ao seu serviço.

## <a name="change-azure-cognitive-search"></a>Alterar Pesquisa Cognitiva do Azure

Saiba [como alterar o serviço de pesquisa cognitiva](./how-to/set-up-qnamaker-service-azure.md#configure-qna-maker-to-use-different-cognitive-search-resource) vinculado ao serviço de QnA Maker.

## <a name="change-default-answer"></a>Alterar a resposta padrão

Saiba [como alterar o texto de suas respostas padrão](How-To/change-default-answer.md). 

## <a name="telemetry"></a>Telemetria

# <a name="qna-maker-ga-stable-release"></a>[QnA Maker GA (versão estável)](#tab/v1)

Application Insights é usado para monitorar a telemetria com QnA Maker GA. Não há definições de configuração específicas para QnA Maker.

# <a name="qna-maker-managed-preview-release"></a>[Gerenciado QnA Maker (versão de visualização)](#tab/v2)

Saiba [como adicionar telemetria ao seu serviço QnA Maker gerenciado (versão prévia)](How-To/get-analytics-knowledge-base.md). 

---

## <a name="app-service-plan"></a>Plano do Serviço de Aplicativo

# <a name="qnamaker-ga-stable-release"></a>[QnAMaker GA (versão estável)](#tab/v1)

O plano do serviço de aplicativo não tem definições de configuração específicas para QnA Maker.

# <a name="qnamaker-managed-preview-release"></a>[Gerenciado por QnAMaker (versão de visualização)](#tab/v2)

O plano do serviço de aplicativo não é usado com QnA Maker gerenciado (versão prévia).

---

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre [formatos](reference-document-format-guidelines.md) de documentos e URLs que você deseja importar para uma base de dados de conhecimento.