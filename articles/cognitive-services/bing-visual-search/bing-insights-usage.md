---
title: Примеры аналитических сведений Bing — Визуальный поиск Bing
titleSuffix: Azure Cognitive Services
description: В этой статье содержатся примеры того, как Визуальный поиск Bing может использовать и показывать аналитику изображений в Bing.com.
services: cognitive-services
author: swhite-msft
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-visual-search
ms.topic: conceptual
ms.date: 04/03/2019
ms.author: scottwhi
ms.openlocfilehash: 3d4e9bf67aa1d3df815c674fdc1e2019f68b4a60
ms.sourcegitcommit: 3bdeb546890a740384a8ef383cf915e84bd7e91e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93086709"
---
# <a name="examples-of-bing-insights-usage"></a>Примеры использования аналитических сведений Bing

> [!WARNING]
> API-интерфейсы поиска Bing перемещаются из Cognitive Services в Поиск Bing службы. Начиная с **30 октября 2020** , все новые экземпляры Поиск Bing должны быть подготовлены, следуя описанному [здесь](https://aka.ms/cogsvcs/bingmove)процессу.
> API-интерфейсы поиска Bing, подготовленные с помощью Cognitive Services, будут поддерживаться в течение следующих трех лет или до конца Соглашение Enterprise, в зависимости от того, что происходит раньше.
> Инструкции по миграции см. в разделе [Поиск Bing Services](https://aka.ms/cogsvcs/bingmigration).

В этой статье содержатся примеры того, как служба Bing может использовать и отображать аналитические сведения на Bing.com.

## <a name="pagesincluding-insight-example"></a>Пример аналитических сведений PagesIncluding

Ниже показана ссылка на первую веб-страницу и позволяет пользователю развернуть и свернуть список других веб-страниц, содержащих изображение:

![Развернутые страницы, содержащие изображение](./media/pages-including.PNG)

## <a name="shoppingsources-insight-example"></a>Пример аналитических сведений ShoppingSources

Ниже показано, как Bing может отображать источники покупок для продуктов, показанных на изображении:

![Ресурсы покупок](./media/shopping-sources.PNG)

## <a name="visualsearch-insight-example"></a>Пример аналитических сведений VisualSearch

Ниже показано, как Bing может отображать визуально схожие изображения (см. **связанные изображения** в примере):

![Визуально похожие изображения](./media/similar-images.PNG)

## <a name="recipes-insight-example"></a>Пример аналитических сведений рецептов

Ниже показано, как служба Bing может отображать рецепты еды, идентифицированной на изображении. В этом примере пользователю сообщается о доступных рецептах:

![Рецепты и страницы, содержащие изображение](./media/recipes-pages-including.PNG)

 И предоставляет ссылку на рецепты, когда пользователь развертывает список:

![Развернутые страницы с рецептами, содержащие изображение](./media/expanded-recipes-pages-including.PNG)

## <a name="relatedsearches-insight-example"></a>Пример аналитических сведений RelatedSearches

Ниже показано, как служба Bing может отображать связанные поисковые запросы изображений, сделанные другими пользователями. Если пользователь щелкнет изображение, то он будет перенаправлен на страницу результатов поиска Bing.com/images для соответствующего связанного запроса.

![Связанные поисковые запросы для изображений](./media/bordered-related-searches.PNG)

## <a name="entity-insight-example"></a>Пример аналитических сведений сущностей

Ниже показано, как служба Bing может отображать сведения о сущности (человеке, месте или вещи), идентифицированной на изображении. Если пользователь щелкнет ссылку на сущность, он перейдет на страницу результатов поиска Bing.com для сущности:

![Сущность, идентифицированная на изображении](./media/entity.PNG)

## <a name="displaying-other-insights-that-the-user-might-explore"></a>Отображение других аналитических сведений, доступных пользователю

Ниже показано, как служба Bing может отображать другие сведения об изображении, доступные пользователю.

![Просмотр других аналитических сведений изображения](./media/apple-pie-more-tags.PNG)

## <a name="bounding-boxes-and-hot-spots"></a>Ограничивающие прямоугольники и гиперобъекты

Теги не по умолчанию включают в себя ограничивающий прямоугольник, определяющий интересующую вас область изображения, к которой применяется тег. Если ограничивающий прямоугольник не идентифицирует изображение целиком, то создайте на изображении гиперобъект, используя ограничивающий прямоугольник. Пользователь может щелкнуть такой гиперобъект, чтобы просмотреть сведения, связанные с содержимым, найденным в зоне этого гиперобъекта (или прямоугольника). Например, если изображение является высокопроизводительным, результаты могут содержать теги (и ограничивающие прямоугольники) для аксессуаров, показанных на изображении, например роняет, ювелирный, скарфс и т. д. В следующем примере показан прямоугольник с активной областью для своему солнцезащитных очков, показанного на изображении:

![Ограничивающий прямоугольник и гиперобъект](./media/click-to-search.PNG)

## <a name="next-steps"></a>Дальнейшие действия

Чтобы начать работу с первым запросом, ознакомьтесь с краткими руководствами:

* [C#](quickstarts/csharp.md)

* [Java](quickstarts/java.md)

* [Node.js](quickstarts/nodejs.md)

* [Python](quickstarts/python.md)





