---
title: API REST de configuração de Azure App-bloqueios
description: Páginas de referência para trabalhar com bloqueios de chave-valor usando a API REST de configuração de Azure App
author: lisaguthrie
ms.author: lcozzens
ms.service: azure-app-configuration
ms.topic: reference
ms.date: 08/17/2020
ms.openlocfilehash: 4949db646c54d75f60d29d3c631d0f4ee8d7c26e
ms.sourcegitcommit: 7cc10b9c3c12c97a2903d01293e42e442f8ac751
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2020
ms.locfileid: "93423908"
---
# <a name="locks"></a>Locks

versão da API: 1,0

Essa API fornece semântica de bloqueio/desbloqueio para o recurso chave-valor. Ele dá suporte às seguintes operações:

- Local de bloqueio
- Remover bloqueio

Se presente, `label` deve ser um valor de rótulo explícito ( **não** um curinga). Para todas as operações, é um parâmetro opcional. Se omitido, ele não implica nenhum rótulo.

## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE [azure-app-configuration-create](../../includes/azure-app-configuration-rest-api-prereqs.md)]

## <a name="lock-key-value"></a>Key-Value de bloqueio

- **Necessário:** ``{key}`` , ``{api-version}``  
- *Opcional:*``label``

```http
PUT /locks/{key}?label={label}&api-version={api-version} HTTP/1.1
```

**Response**

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.microsoft.appconfig.kv+json; charset=utf-8"
```

```json
{
  "etag": "4f6dd610dd5e4deebc7fbaef685fb903",
  "key": "{key}",
  "label": "{label}",
  "content_type": null,
  "value": "example value",
  "created": "2017-12-05T02:41:26.4874615+00:00",
  "locked": true,
  "tags": []
}
```

Se o valor de chave não existir, a seguinte resposta será retornada:

```http
HTTP/1.1 404 Not Found
```

## <a name="unlock-key-value"></a>Desbloquear Key-Value

- **Necessário:** ``{key}`` , ``{api-version}``  
- *Opcional:*``label``

```http
DELETE /locks/{key}?label={label}?api-version={api-version} HTTP/1.1
```

**Response**

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.microsoft.appconfig.kv+json; charset=utf-8"
```

```json
{
  "etag": "4f6dd610dd5e4deebc7fbaef685fb903",
  "key": "{key}",
  "label": "{label}",
  "content_type": null,
  "value": "example value",
  "created": "2017-12-05T02:41:26.4874615+00:00",
  "locked": true,
  "tags": []
}
```

Se o valor de chave não existir, a seguinte resposta será retornada:

```http
HTTP/1.1 404 Not Found
```

## <a name="conditional-lockunlock"></a>Bloqueio/desbloqueio condicional

Para evitar condições de corrida, use `If-Match` ou `If-None-Match` cabeçalhos de solicitação. O `etag` argumento faz parte da representação de chave. Se `If-Match` ou `If-None-Match` forem omitidos, a operação será incondicional.

A solicitação a seguir aplica a operação somente se a representação de chave-valor atual corresponder à especificada `etag` :

```http
PUT|DELETE /locks/{key}?label={label}&api-version={api-version} HTTP/1.1
If-Match: "4f6dd610dd5e4deebc7fbaef685fb903"
```

A solicitação a seguir aplica a operação somente se a representação de chave-valor atual existir, mas não corresponder ao especificado `etag` :

```http
PUT|DELETE /kv/{key}?label={label}&api-version={api-version} HTTP/1.1
If-None-Match: "4f6dd610dd5e4deebc7fbaef685fb903"
```
