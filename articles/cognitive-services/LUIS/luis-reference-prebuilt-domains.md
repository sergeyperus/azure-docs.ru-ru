---
title: Предварительно созданная ссылка на домен — LUIS
titleSuffix: Azure Cognitive Services
description: Справочник по предварительно созданным доменам, которые представляют собой предварительно собранные коллекции намерений и сущностей из Интеллектуальных служб распознавания речи (LUIS).
services: cognitive-services
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: reference
ms.date: 09/27/2019
ms.openlocfilehash: 73b279f98011181b329cdb010041022ab0da57f0
ms.sourcegitcommit: 10d00006fec1f4b69289ce18fdd0452c3458eca5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2020
ms.locfileid: "95018639"
---
# <a name="prebuilt-domain-reference-for-your-luis-app"></a>Справочник по предварительно созданным доменам для приложения LUIS
В этом справочнике представлены сведения о [предварительно созданных доменах](./howto-add-prebuilt-models.md), которые представляют собой предварительно созданные коллекции намерений и сущностей, предлагаемые приложением LUIS.

[Пользовательские домены](luis-how-to-start-new-app.md), напротив, сначала не имеют намерений и моделей. Вы можете добавить любые намерения и сущности предварительно созданных доменов в пользовательскую модель.

## <a name="prebuilt-domains-per-language"></a>Предварительно созданные домены для каждого языка

В таблице ниже перечислены поддерживаемые в настоящее время домены. Поддержка английского языка обычно более полная, чем другие.

| Тип сущности       | EN-US      | ZH-CN   | DE    | СВ     | ES    | ИТ-отдел      | PT-BR |  JP  |      KO |        NL |    TR |
|:-----------------:|:-------:|:-------:|:-----:|:------:|:-----:|:-------:| :-------:| :-------:| :-------:| :-------:|  :-------:|
| Календарь  | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
|Связь  | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Электронная почта     | ✓    | ✓       | ✓   | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| HomeAutomation          | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Примечания     | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Размещает   | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| RestaurantReservation  | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Столбце     | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Служебные программы      | ✓    | ✓        | ✓    | ✓      | ✓     | ✓       | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Погода        | ✓    | ✓        | ✓    | ✓      | ✓     | ✓       | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Интернет    | ✓    | ✓        | ✓    | ✓      | ✓     | ✓       | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |

Предварительно созданные домены **не поддерживаются** в:

* Французский (Канада)
* Хинди
* Испанский (Мексика)

## <a name="next-steps"></a>Дальнейшие действия

Изучите [простую сущность](reference-entity-simple.md).