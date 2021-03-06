---
title: Конфигурация приложений Azure REST API — управление версиями
description: Справочные страницы по управлением версиями с помощью REST API конфигурации приложений Azure
author: lisaguthrie
ms.author: lcozzens
ms.service: azure-app-configuration
ms.topic: reference
ms.date: 08/17/2020
ms.openlocfilehash: 3a7f50b26d59501d2be3a0147fe89919819b50e6
ms.sourcegitcommit: 30906a33111621bc7b9b245a9a2ab2e33310f33f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/22/2020
ms.locfileid: "95246373"
---
# <a name="versioning"></a>Управление версиями

Каждый клиентский запрос должен предоставлять явную версию API в качестве параметра строки запроса. Например, так: `https://{myconfig}.azconfig.io/kv?api-version=1.0`.

`api-version` выражается в формате SemVer (основной. дополнительный). Согласование диапазона или версии не поддерживается.

Эта статья относится к API версии 1,0.

Ниже приведена сводка возможных сообщений об ошибках, возвращаемых сервером, если запрашиваемая версия API не может быть сопоставлена.

## <a name="api-version-unspecified"></a>Версия API не указана

Эта ошибка возникает, когда клиент выполняет запрос без предоставления версии API.

```http
HTTP/1.1 400 Bad Request
Content-Type: application/problem+json; charset=utf-8
{
  "type": "https://azconfig.io/errors/invalid-argument",
  "title": "API version is not specified",
  "name": "api-version",
  "detail": "An API version is required, but was not specified.",
  "status": 400
}
```

## <a name="unsupported-api-version"></a>Неподдерживаемая версия API

Эта ошибка возникает, когда запрошенная версия API клиента не соответствует ни одной из поддерживаемых версий API на сервере.

```http
HTTP/1.1 400 Bad Request
Content-Type: application/problem+json; charset=utf-8
{
  "type": "https://azconfig.io/errors/invalid-argument",
  "title": "Unsupported API version",
  "name": "api-version",
  "detail": "The HTTP resource that matches the request URI '{request uri}' does not support the API version '{api-version}'.",
  "status": 400
}
```

## <a name="invalid-api-version"></a>Недопустимая версия API

Эта ошибка возникает, когда клиент выполняет запрос с версией API, но значение имеет неправильный формат или не может быть проанализировано сервером.

```http
HTTP/1.1 400 Bad Request
Content-Type: application/problem+json; charset=utf-8  
{
  "type": "https://azconfig.io/errors/invalid-argument",
  "title": "Invalid API version",
  "name": "api-version",
  "detail": "The HTTP resource that matches the request URI '{request uri}' does not support the API version '{api-version}'.",
  "status": 400
}
```

## <a name="ambiguous-api-version"></a>Неоднозначная версия API

Эта ошибка возникает, когда клиент запрашивает версию API, неоднозначность для сервера (например, несколько различных значений).

```http
HTTP/1.1 400 Bad Request
Content-Type: application/problem+json; charset=utf-8
{
  "type": "https://azconfig.io/errors/invalid-argument",
  "title": "Ambiguous API version",
  "name": "api-version",
  "detail": "The following API versions were requested: {comma separated api versions}. At most, only a single API version may be specified. Please update the intended API version and retry the request.",
  "status": 400
}
```
