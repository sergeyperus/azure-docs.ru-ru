---
title: Статистика в режиме реального времени в Azure CDN | Документация Майкрософт
description: Статистика в реальном времени предоставляет актуальные данные о производительности сети Azure CDN при доставке содержимого клиентам.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: azure-cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 3af2e849aa6658e539b0b5bdbda4428cc28e5ce5
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2020
ms.locfileid: "84887227"
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a>Статистика в реальном времени в сети CDN Microsoft Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Обзор
В этом документе содержатся сведения о статистике в реальном времени в сети CDN Microsoft Azure.  Эта функция предоставляет данные в реальном времени, например о пропускной способности, состоянии кэша и числе одновременных подключений к профилю сети CDN, при доставке содержимого клиентам. Благодаря этому обеспечивается постоянный мониторинг работоспособности службы, в том числе событий запуска.

Доступны следующие диаграммы:

* [Пропускная способность](#bandwidth)
* [Коды состояний](#status-codes)
* [Состояния кэша](#cache-statuses)
* [Соединения](#connections)

## <a name="accessing-real-time-stats"></a>Доступ к статистике в реальном времени
1. На [портале Azure](https://portal.azure.com)перейдите к профилю CDN.
   
    ![Колонка профиля сети CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. В колонке профиля сети CDN нажмите кнопку **Управление** .
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    Откроется портал управления CDN.
3. Наведите указатель на вкладку **Аналитика**, а затем на всплывающее окно **Real-Time Stats** (Статистика в реальном времени).  Щелкните **Большой HTTP-объект**.
   
    ![Портал управления CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    Отобразятся диаграммы статистических данных в реальном времени.

На каждой диаграмме отображается статистика в реальном времени за определенный период. Они запускаются при загрузке страницы  Они запускаются при загрузке страницы и автоматически обновляются каждые несколько секунд.  Кнопка **Refresh Graph** (Обновить диаграмму), если она присутствует, позволяет очистить данные на диаграмме, после чего отобразятся только выбранные данные.

## <a name="bandwidth"></a>Пропускная способность
![Диаграмма "Пропускная способность"](./media/cdn-real-time-stats/cdn-bandwidth.png)

На диаграмме **Пропускная способность** отображается объем пропускной способности, использовавшийся для текущей платформы за выбранный период времени. На затененной части диаграммы показано использование пропускной способности. Точный объем пропускной способности, используемой в данный момент, отображается непосредственно под линейной диаграммой.

## <a name="status-codes"></a>Коды состояний
![Диаграмма "Код состояния"](./media/cdn-real-time-stats/cdn-status-codes.png)

На диаграмме **Коды состояний** показана частота возникновения определенных кодов HTTP-ответов за выбранный период времени.

> [!TIP]
> Описание каждого параметра кода состояния HTTP см. в разделе [Azure CDN HTTP Status Codes](/previous-versions/azure/mt759238(v=azure.100)) (Коды состояний HTTP в сети Azure CDN).
> 
> 

Список кодов состояний HTTP находится непосредственно над диаграммой. В списке приводится каждый код состояния, который может быть включен в линейную диаграмму, и текущее количество вхождений в секунду этого кода состояния. По умолчанию отображается строка для каждого кода состояния в диаграмме. Однако можно отслеживать только те коды состояний, которые имеют особое значение для конфигурации сети CDN. Для этого проверьте требуемые коды состояний и очистите все другие параметры, а затем нажмите кнопку **Refresh Graph**(Обновить диаграмму). 

Можно временно скрыть данные журнала для определенного кода состояния.  В условных обозначениях непосредственно под диаграммой щелкните код состояния, который нужно скрыть. Код состояния сразу же пропадет из диаграммы. Если щелкнуть этот код состояния еще раз, он снова появится на диаграмме.

## <a name="cache-statuses"></a>Состояния кэша
![Диаграмма "Состояния кэша"](./media/cdn-real-time-stats/cdn-cache-status.png)

На диаграмме **Состояния кэша** показана частота возникновения определенных типов состояний кэша за выбранный период времени. 

> [!TIP]
> Описание каждого параметра кода состояния кэша см. в разделе [Azure CDN Cache Status Codes](/previous-versions/azure/mt759237(v=azure.100)) (Коды состояний кэша в сети Azure CDN).
> 
> 

Список кодов состояний кэша находится непосредственно над диаграммой. В списке приводится каждый код состояния, который может быть включен в линейную диаграмму, и текущее количество вхождений в секунду этого кода состояния. По умолчанию отображается строка для каждого кода состояния в диаграмме. Однако можно отслеживать только те коды состояний, которые имеют особое значение для конфигурации сети CDN. Для этого проверьте требуемые коды состояний и очистите все другие параметры, а затем нажмите кнопку **Refresh Graph**(Обновить диаграмму). 

Можно временно скрыть данные журнала для определенного кода состояния.  В условных обозначениях непосредственно под диаграммой щелкните код состояния, который нужно скрыть. Код состояния сразу же пропадет из диаграммы. Если щелкнуть этот код состояния еще раз, он снова появится на диаграмме.

## <a name="connections"></a>Соединения
![Диаграмма "Подключения"](./media/cdn-real-time-stats/cdn-connections.png)

На этой диаграмме показано количество подключений, установленных с пограничными серверами. Подключение устанавливается при каждом запросе к ресурсу, который проходит через сеть CDN.

## <a name="next-steps"></a>Next Steps
* Получение уведомлений с помощью [оповещения в режиме реального времени в Azure CDN](cdn-real-time-alerts.md)
* Дополнительные сведения о [расширенных HTTP-отчетах](cdn-advanced-http-reports.md).
* Анализ [закономерностей использования](cdn-analyze-usage-patterns.md)

