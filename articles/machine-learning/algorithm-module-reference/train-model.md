---
title: 'Обучение модели: Справочник по модулям'
titleSuffix: Azure Machine Learning
description: Узнайте, как использовать модуль **обучение модели** в машинное обучение Azure для обучения модели классификации или регрессии.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: reference
author: likebupt
ms.author: keli19
ms.date: 11/25/2020
ms.openlocfilehash: f9a7623fd27178e8b9c213a1759bb09863d16c72
ms.sourcegitcommit: 2e9643d74eb9e1357bc7c6b2bca14dbdd9faa436
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "96030702"
---
# <a name="train-model-module"></a>Модуль "Обучение модели"

В этой статье описывается модуль в конструкторе Машинное обучение Azure.

Используйте этот модуль для обучения модели классификации или регрессии. Обучение выполняется после определения модели и установки ее параметров и требует наличия данных с тегами. Можно также использовать **обучение модели** для переобучения существующей модели новыми данными. 

## <a name="how-the-training-process-works"></a>Принцип работы процесса обучения

В Машинное обучение Azure создание и использование модели машинного обучения обычно выполняется в три этапа. 

1. Модель настраивается путем выбора определенного типа алгоритма и определения его параметров или параметров. Выберите любой из следующих типов моделей: 

    + Модели **классификации** , основанные на нейронных сетях, деревьях принятия решений, лесах принятия решений и других алгоритмах.
    + Модели **регрессии** , которые могут включать стандартную линейную регрессию или использовать другие алгоритмы, включая нейронные сети и Байеса регрессию.  

2. Предоставьте набор данных с меткой и совместимый с алгоритмом. Подключите данные и модель для **обучения модели**.

    В каком формате создается конкретный двоичный формат, iLearner, который инкапсулирует статистические шаблоны, полученные из данных. Вы не можете напрямую изменять или читать этот формат. Однако другие модули могут использовать эту обученную модель. 
    
    Также можно просмотреть свойства модели. Дополнительные сведения см. в разделе "результаты".

3. После завершения обучения используйте обученную модель с одним из [модулей оценки](./score-model.md), чтобы создать прогнозы по новым данным.

## <a name="how-to-use-train-model"></a>Использование модели обучения 
    
1. Добавьте модуль **обучение модели** в конвейер.  Этот модуль можно найти в категории **машинное обучение** . Разверните узел **обучение**, а затем перетащите модуль **обучение модели** в конвейер.
  
1.  В левой части входных данных присоедините обученный режим. Прикрепите набор данных для обучения к правому входу **обучение модели**.

    Набор данных для обучения должен содержать столбец меток. Все строки без меток игнорируются.
  
1.  В поле **столбец метки** щелкните **изменить столбец** в правой панели окна модуль и выберите один столбец, содержащий результаты, которые модель может использовать для обучения.
  
    - Для проблем классификации столбец меток должен содержать либо значения **категорий** , либо **дискретные** значения. Некоторые примеры могут быть "да/нет", кодом или именем классификации по болезни или группой доходов.  При выборе неупорядоченного столбца модуль будет возвращать ошибку во время обучения.
  
    -   Для проблем регрессии столбец меток должен содержать **числовые** данные, представляющие переменную ответа. В идеале числовые данные представляют непрерывное масштабирование. 
    
    Примерами могут быть оценки кредитного риска, предполагаемое время сбоя жесткого диска или прогнозирование количества вызовов к центру обработки звонков в указанный день или время.  Если не выбрать числовой столбец, может появиться сообщение об ошибке.
  
    -   Если не указан используемый столбец метки, машинное обучение Azure попытается определить подходящий столбец метки с помощью метаданных набора данных. При выборе неправильного столбца используйте селектор столбцов, чтобы исправить его.
  
    > [!TIP] 
    > Если при использовании селектора столбцов возникают проблемы, см. советы [в статье Выбор столбцов в наборе данных](./select-columns-in-dataset.md) . В нем описываются некоторые распространенные сценарии и советы по использованию параметров **with Rules** и **Name** .
  
1.  Отправьте конвейер. Если у вас много данных, это может занять некоторое время.

    > [!IMPORTANT] 
    > Если у вас есть столбец ИДЕНТИФИКАТОРов, который является ИДЕНТИФИКАТОРом каждой строки, то при **обучении модели** может возникнуть ошибка, например "число уникальных значений в столбце:" {column_name} "больше допустимого значения". Это обусловлено тем, что столбец ID достиг порогового значения уникальных значений и может привести к нехватке памяти. Обычно столбец ИДЕНТИФИКАТОРов не имеет смысла во время обучения. Можно использовать функцию [изменить метаданные](edit-metadata.md) , чтобы пометить столбец как **четкий** , и он не будет использоваться в обучении. Дополнительные сведения об ошибке см. в разделе [код ошибки конструктора](././designer-error-codes.md) .

## <a name="results"></a>Результаты

После обучения модели:


+ Чтобы использовать модель в других конвейерах, выберите модуль и щелкните значок **зарегистрировать набор данных** на вкладке **выходные данные** на правой панели. Доступ к сохраненным моделям можно получить в палитре модулей в разделе **наборы данных**.

+ Чтобы использовать модель в прогнозе новых значений, подключите ее к модулю « [Оценка модели](./score-model.md) » вместе с новыми входными данными.


## <a name="next-steps"></a>Дальнейшие действия

Ознакомьтесь с [набором доступных модулей](module-reference.md) в службе Машинного обучения Azure. 