---
title: Criar uma entrada de trabalho dos Serviços de Mídia do Azure com base em uma URL HTTPS | Microsoft Docs
description: Este tópico demonstra como criar uma entrada de trabalho dos serviços de mídia do Azure de uma URL HTTPS.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: how-to
ms.date: 08/31/2020
ms.author: inhenkel
ms.openlocfilehash: e440e4393065d2bc1cad1a96b4f8c975624faa11
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "89295505"
---
# <a name="create-a-job-input-from-an-https-url"></a>Criar uma entrada de trabalho de uma URL HTTPS

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Nos Serviços de Mídia v3, ao enviar Trabalhos para processar seus vídeos, você precisa informar os Serviços de Mídia onde encontrar o vídeo de entrada. Uma das opções é especificar uma URL HTTPS como um trabalho de entrada (conforme mostrado neste exemplo). Observe que, no momento, o AMS v3 não dá suporte à codificação de transferência em partes sobre URLs HTTPS. Para obter um exemplo completo, confira esta [amostra do GitHub](https://github.com/Azure-Samples/media-services-v3-dotnet-quickstarts/blob/master/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs).

> [!TIP]
> Antes de começar a desenvolver, examine o [desenvolvimento com as APIs dos serviços de mídia v3](media-services-apis-overview.md) (inclui informações sobre como acessar APIs, convenções de nomenclatura, etc.)

## <a name="net-sample"></a>Exemplo de .NET

O código a seguir mostra como criar um trabalho com uma entrada de URL HTTPS.

[!code-csharp[Main](../../../media-services-v3-dotnet-quickstarts/AMSV3Quickstarts/EncodeAndStreamFiles/Program.cs#SubmitJob)]

## <a name="job-error-codes"></a>Códigos de erro do trabalho

Confira [Códigos de erro](/rest/api/media/jobs/get#joberrorcode).

## <a name="next-steps"></a>Próximas etapas

[Crie uma entrada de trabalho de um arquivo local](job-input-from-local-file-how-to.md).
