---
title: Модели потребления автомобиля для маршрутизации | Карты Microsoft Azure
description: 'Сведения о моделях потребления, которые Azure Maps поддерживает: комбустион и электрический. Узнайте, какие параметры использует каждая модель, и просмотрите ограничения параметров.'
author: subbarayudukamma
ms.author: skamma
ms.date: 05/08/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.openlocfilehash: b44186d783a249192a8c13ee97063034ee319df7
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "96013145"
---
# <a name="consumption-model"></a>Модель потребления

Служба маршрутизации предоставляет набор параметров для подробного описания модели потребления, зависящей от автомобиля.
В зависимости от значения параметра **vehicleEngineType** (тип двигателя транспортного средства) поддерживаются две основные модели потребления: _Combustion_ (для двигателя внутреннего сгорания) и _Electric_ (для электродвигателя). Неверно указывать параметры, принадлежащие разным моделям в одном запросе. Кроме того, параметры модели потребления нельзя использовать со следующими значениями **травелмоде** : _велосипед_ и _пешеход_.

## <a name="parameter-constraints-for-consumption-model"></a>Ограничения параметров для модели потребления

В обеих моделях потребления существуют зависимости при указании параметров. Это означает, что, явно указывая некоторые параметры, может потребоваться указать некоторые другие параметры. Ниже приведены эти зависимости, которые следует учитывать:

* Все параметры требуют указания параметра **constantSpeedConsumption** (потребление постоянной скорости) пользователем. Указание любого другого параметра модели потребления, если **константспидконсумптион** не задано, является ошибкой. Параметр **вехиклевеигхт** является исключением для этого требования.
* **акцелератионеффиЦиенци** и **децелератионеффиЦиенци** должны быть указаны в виде пары (т. е. одновременно или нет).
* Если параметры **accelerationEfficiency** и **decelerationEfficiency** указаны, сумма их значений не должна превышать 1 (для предотвращения вечного движения).
* **уфиллеффиЦиенци** и **довнхиллеффиЦиенци** должны быть заданы как пара (то есть обе, или нет).
* Если **uphillEfficiency** и **downhillEfficiency** указаны, сумма их значений не должна превышать 1 (для предотвращения вечного движения).
* Если пользователь указал параметры \*__эффективности__, должен быть указан и **вес транспортного средства**. Если параметр **vehicleEngineType** имеет значение _combustion_, параметр **fuelEnergyDensityInMJoulesPerLiter** (энергетическая плотность топлива в джоулях на литр) также должен быть указан.
* **максчаржеинквх** и **куррентчаржеинквх** должны быть указаны в виде пары (т. е. одновременно или нет).

> [!NOTE]
> Если **постоянное потребление скорости** указано, то другие аспекты потребления, такие как уклоны и ускорение транспорта, не учитываются для вычислений потребления.

## <a name="combustion-consumption-model"></a>Модель потребления для двигателя внутреннего сгорания

Модель потребления для двигателя внутреннего сгорания используется, если для параметра **vehicleEngineType** задано значение _combustion_.
Ниже приведен список параметров, относящихся к этой модели. Подробное описание см. в разделе "Параметры".

* constantSpeedConsumptionInLitersPerHundredkm (постоянная скорость в литрах на 100 км).
* vehicleWeight (вес транспортного средства).
* currentFuelInLiters (расход топлива в литрах).
* auxiliaryPowerInLitersPerHour (вспомогательная мощность в литрах в час).
* fuelEnergyDensityInMJoulesPerLiter (энергетическая плотность топлива в джоулях на литр).
* accelerationEfficiency (эффективность ускорения).
* decelerationEfficiency (эффективность замедления).
* uphillEfficiency (эффективность подъема).
* downhillEfficiency (эффективность спуска).

## <a name="electric-consumption-model"></a>Модель потребления для электродвигателя

Модель потребления для электродвигателя используется, если для параметра **vehicleEngineType** задано значение _electric_.
Ниже приведен список параметров, относящихся к этой модели. Подробное описание см. в разделе "Параметры".

* constantSpeedConsumptionInkWhPerHundredkm (постоянная скорость в кВт/ч на 100 км).
* vehicleWeight (вес транспортного средства).
* currentChargeInkWh (текущий заряд в кВт/ч).
* maxChargeInkWh (максимальный заряд в кВт/ч).
* auxiliaryPowerInkW (вспомогательная мощность в кВт).
* accelerationEfficiency (эффективность ускорения).
* decelerationEfficiency (эффективность замедления).
* uphillEfficiency (эффективность подъема).
* downhillEfficiency (эффективность спуска).

## <a name="sensible-values-of-consumption-parameters"></a>Чувствительные значения параметров потребления

Определенный набор параметров потребления можно отклонять, даже если набор может удовлетворить все явные требования. Это происходит, когда значение определенного параметра или сочетание значений нескольких параметров считаются неоправданными величинами значений потребления. В этом случае, вероятнее всего, появится ошибка ввода, так как принимаются соответствующие меры, чтобы применить все чувствительные значения параметров потребления. Если определенный набор параметров потребления отклоняется, в сопутствующем сообщении об ошибке будет содержаться текстовое описание причин.
В подробном описании параметров есть примеры чувствительных значений для обеих моделей.
