---
title: Idioma de consulta
titleSuffix: Azure Digital Twins
description: Entenda os conceitos básicos da linguagem de consulta do Azure digital gêmeos.
author: baanders
ms.author: baanders
ms.date: 3/26/2020
ms.topic: conceptual
ms.service: digital-twins
ms.openlocfilehash: d656f19f6f4030025ff1393c3e5017466b3333fd
ms.sourcegitcommit: 2e72661f4853cd42bb4f0b2ded4271b22dc10a52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92044387"
---
# <a name="about-the-query-language-for-azure-digital-twins"></a>Sobre a linguagem de consulta para o gêmeos digital do Azure

Lembre-se de que o centro do Azure digital gêmeos é o [**gráfico de entrelaçamento**](concepts-twins-graph.md), construído de gêmeos e **relações** **digitais** . Esse grafo pode ser consultado para obter informações sobre o gêmeos digital e as relações que ele contém. Essas consultas são escritas em uma linguagem de consulta do tipo SQL personalizada, conhecida como a **linguagem de consulta do Azure digital gêmeos**.

Para enviar uma consulta ao serviço de um aplicativo cliente, você usará a [**API de consulta**](/dotnet/api/azure.digitaltwins.core.digitaltwinsclient.query?view=azure-dotnet-preview)do gêmeos digital do Azure. Isso permite que os desenvolvedores gravem consultas e apliquem filtros para localizar conjuntos de gêmeos digitais no grafo de entrelaçamento e outras informações sobre o cenário do gêmeos digital do Azure.

[!INCLUDE [digital-twins-query-operations.md](../../includes/digital-twins-query-operations.md)]

## <a name="next-steps"></a>Próximas etapas

Saiba como escrever consultas e ver exemplos de código de cliente em [*como: consultar o grafo de entrelaçamento*](how-to-query-graph.md).