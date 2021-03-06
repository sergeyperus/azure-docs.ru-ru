---
title: Автоматическая переадресация сущностей обмена сообщениями служебной шины Azure
description: В этой статье описывается, как связать очередь или подписку служебной шины Azure с другой очередью или разделом.
ms.topic: article
ms.date: 06/23/2020
ms.custom: devx-track-csharp
ms.openlocfilehash: 8f5f93f65871c0b9658a75264ab959dbae7fefe7
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2020
ms.locfileid: "91819581"
---
# <a name="chaining-service-bus-entities-with-autoforwarding"></a>Объединение в цепочки сущностей служебной шины с помощью автоматической переадресации

Функция *автоматической переадресации* служебной шины позволяет привязать очередь или подписку к другой очереди или разделу, которые являются частью одного и того же пространства имен. Если включена автоматическая переадресация, служебная шина автоматически удаляет сообщения, помещенные в первую очередь или подписку (источник), и помещает их во вторую очередь или раздел (место назначения). При этом сохраняется возможность отправить сообщение в конечную сущность напрямую.

## <a name="using-autoforwarding"></a>Использование автоматической переадресации

Автоматическую переадресацию можно включить, задав свойства [QueueDescription.ForwardTo][QueueDescription.ForwardTo] или [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] объектов источника [QueueDescription][QueueDescription] или [SubscriptionDescription][SubscriptionDescription], как показано в следующем примере:

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

Конечная сущность должна существовать на момент создания исходной сущности. Если конечной сущности не существует, служебная шина возвращает исключение при попытке создать исходную сущность.

С помощью автоматической переадресации можно выполнить масштабирование отдельного раздела. Служебная шина ограничивает [количество подписок на определенный раздел](service-bus-quotas.md) до 2000. Создав разделы второго уровня, можно разместить дополнительные подписки. Даже при отсутствии ограничения служебной шины на количество подписок, добавление разделов второго уровня может повысить общую пропускную способность раздела.

![Схема сценария перенаправления, показывающего сообщение, обработанное с помощью раздела Orders, который может создать ветвь для любого из трех разделов заказов второго уровня.][0]

С помощью автоматической переадресации также можно разделить отправителей и получателей сообщений. Например, рассмотрим систему ERP, состоящую из трех модулей: обработки заказов, управления запасами и управления отношениями с клиентами. Каждый из этих модулей создает сообщения, передаваемые в очередь в соответствующем разделе. Алиса и Роберт — торговые представители, которых интересуют все сообщения, относящиеся к своим клиентам. Для получения этих сообщений Алиса и Боб создают персональные очереди и подписки в каждом из разделов ERP, которые автоматически пересылают все сообщения в их очереди.

![Схема сценария перемотки, показывающий три модуля обработки, отправляющих сообщения через три соответствующих раздела в две отдельные очереди.][1]

Если Алиса уйдет в отпуск, то заполнится ее личная очередь, а не очередь раздела ERP. В этом сценарии ни один из разделов ERP не достигнет выделенной квоты, так как торговый представитель не получил ни одного сообщения.

> [!NOTE]
> При установке автоматической пересылки значение для AutoDeleteOnIdle в **источнике и месте назначения** автоматически устанавливается равным максимальному значению типа данных.
> 
>   - На стороне источника пересылка действует как операция получения. Таким образом, источник, в котором настроена автопереадресация, никогда не является "бездействующим".
>   - На стороне назначения это делается для того, чтобы гарантировать, что для пересылки сообщения всегда существует назначение.

## <a name="autoforwarding-considerations"></a>Рекомендации по автоматической переадресации

Если целевая сущность накапливает слишком много сообщений и превышает квоту или целевая сущность отключена, то исходная сущность добавляет сообщения в [очередь недоставленных сообщений](service-bus-dead-letter-queues.md) до тех пор, пока в целевой сущности не появится место (или пока целевая сущность не будет снова включена). Эти сообщения будут находиться в очереди недоставленных сообщений, поэтому необходимо явным образом получать и обрабатывать их из этой очереди.

При объединении в цепочку отдельных разделов для получения составного раздела с несколькими подписками рекомендуется сократить количество подписок на раздел первого уровня до умеренного и увеличить количество подписок на разделы второго уровня. Например, раздел первого уровня с 20 подписками, каждая из которых объединена в цепочку с разделом второго уровня с 200 подписками, позволяет получить более высокую пропускную способность по сравнению с разделом первого уровня с 200 подписками, каждая из которых объединена в цепочку с разделом второго уровня с 20 подписками.

Служебная шина тарифицирует каждое перенаправленное сообщение как одну операцию. Например, отправка сообщения в раздел с 20 подписками, каждая из которых настроена на автоматическую переадресацию сообщений в другую очередь или раздел, тарифицируется как 21 операция, если все подписки первого уровня получили копию сообщения.

Для создания подписки, связанной с другой очередью или разделом, создатель подписки должен иметь разрешения на **Управление** как исходной, так и целевой сущности. Для отправки сообщений в исходный раздел требуется только разрешение на **отправку** для исходного раздела.

Не создавайте цепочку, которая превышает 4 прыжка. Сообщения, размер которых превышает 4 прыжка, недоставлены.

## <a name="next-steps"></a>Дальнейшие шаги

Подробные сведения об автоматической переадресации см. в следующих разделах:

* [Отправить][QueueDescription.ForwardTo]
* [QueueDescription][QueueDescription]
* [SubscriptionDescription][SubscriptionDescription]

Дополнительные сведения об улучшении производительности служебной шины см. в статье 

* [Рекомендации по повышению производительности с помощью обмена сообщениями через служебную шину](service-bus-performance-improvements.md)
* [Секционированные сущности обмена сообщениями][Partitioned messaging entities].

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
