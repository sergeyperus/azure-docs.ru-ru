---
title: Проверка экземпляра контейнера работоспособности
titleSuffix: Azure Cognitive Services
description: Узнайте, как проверить экземпляр контейнера работоспособности.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: text-analytics
ms.topic: include
ms.date: 07/07/2020
ms.author: aahi
ms.openlocfilehash: 83a9eeb7644d107a808494ad06a8bef91d471fe1
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "96009873"
---
### <a name="verify-that-a-container-is-running"></a>Проверка выполнения контейнера

1. Перейдите на вкладку **Обзор** и скопируйте IP-адрес.
1. Откройте новую вкладку браузера и введите IP-адрес. Например, введите `http://<IP-address>:5000 (http://55.55.55.55:5000` ). Откроется домашняя страница контейнера, в которой вы узнаете, что контейнер выполняется.

    ![Просмотрите домашнюю страницу контейнера, чтобы убедиться, что она запущена](../media/how-tos/container-instance/swagger-docs-on-container.png)

1. Выберите ссылку **API службы Description** , чтобы открыть страницу Swagger контейнера.

1. Выберите любой из API-интерфейсов **POST** и нажмите кнопку **попробовать**. Отображаются параметры, включая пример входных данных.

Существует несколько URL-адресов, которые можно также использовать для проверки того, что контейнер работает.

|Запрос|Назначение|
|--|--|
|`http://localhost:5000/`|Контейнер предоставляет домашнюю страницу.|
|`http://localhost:5000/ready`|Запрашивается с помощью GET, это обеспечивает проверку готовности контейнера к принятию запроса к модели. Этот запрос может использоваться для [проб активности и готовности](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) Kubernetes.|
|`http://localhost:5000/status`|Запрос с помощью GET, как и конечная точка/РЕАДИ, проверяет, что контейнер выполняется без выполнения запроса к модели. Этот запрос может использоваться для [проб активности и готовности](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) Kubernetes.|
|`http://localhost:5000/swagger`|С помощью этого URL-адреса контейнер предоставляет полный набор документации по конечным точкам и `Try it now` функции. Эта функция позволяет ввести параметры в веб-форму HTML и создать запрос без необходимости писать код. После возвращения результатов запроса предоставляется пример команды CURL с примером требуемого формата HTTP-заголовков и текста. |
|`http://localhost:5000/demo`| Этот компонент, запрошенный через браузер, предоставляет интерактивную визуализацию результатов из запросов примеров входного текста или предоставленного вами.  |

Используйте этот URL-адрес запроса, `http://localhost:5000/text/analytics/v3.2-preview.1/entities/health` чтобы отправить запрос в контейнер.
