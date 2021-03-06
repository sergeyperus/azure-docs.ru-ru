---
title: включить файл
description: включить файл
services: cognitive-services
manager: nitinme
ms.service: cognitive-services
ms.topic: include
ms.custom: include file
ms.date: 04/16/2020
ms.openlocfilehash: 78b93c05621754ae499e4ae8ca6b66c5bbfaad1b
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "96025502"
---
Cognitive Services предоставляет две службы обработки естественных языков, [Language Understanding](../luis/what-is-luis.md) и [QnA Maker](../qnamaker/overview/overview.md), каждая из которых имеет разные цели. Узнайте, когда следует использовать каждую службу и как они дополняют друг друга.

Обработка на естественном языке (NLP) позволяет клиентскому приложению, например роботу чата, работать с пользователями с помощью естественного языка. Пользователь вводит предложение или фразу. Текст пользователя может содержать некачественную грамматику, орфографию и знаки препинания. Служба автопросмотра может работать с предложением пользователя, возвращая информацию, которую должен помочь пользователю.

## <a name="cognitive-services-with-nlp"></a>Cognitive Services с NLP

Language Understanding (LUIS) и QnA Maker предоставляют NLP. Клиентское приложение отправляет текст на естественном языке. Служба принимает текст, обрабатывает его и возвращает результат.

## <a name="when-to-use-each-service"></a>Когда следует использовать каждую службу

Language Understanding (LUIS) и QnA Maker решают различные проблемы. LUIS определяет намерение текста пользователя (известного как utterance), а QnA Maker определяет ответ на текст пользователя (называемый запросом).

Чтобы выбрать нужную службу, необходимо понять текст пользователя, поступающий из клиентского приложения, а также сведения, необходимые клиентскому приложению для получения от переданной службы.

Если программа-робот чата получает текст `How do I get to the Human Resources building on the Seattle North campus?` , используйте приведенную ниже диаграмму, чтобы понять, как работает каждая служба с текстом.

|Служба|Клиентское приложение определяет|
|--|--|
|LUIS|**Определяет намерение пользователя** текста. служба не возвращает ответ на вопрос. Например, этот текст классифицируется как совпадение с `FindLocation` намерением.<br>|
|QnA Maker|**Возвращает ответ на вопрос** из пользовательской базы знаний. Например, этот текст определяется как вопрос с ответом на статический текст  `Get on the #9 bus and get off at Franklin street` .|
|||

> [!div class="mx-imgBorder"]
> ![Инфографика определить, когда следует использовать LUIS и когда использовать QnA Maker](./luis-qna-maker-together-decision.png)

## <a name="when-do-you-use-luis"></a>Когда вы используете LUIS?

Используйте LUIS, если вам нужно знать намерение речевого фрагмента в рамках процесса чат-бота. Продолжим пример текста `How do I get to the Human Resources building on the Seattle North campus?` . После того, как пользователь знает намерение найти расположение, вы можете передать сведения о utterance (извлеченные с сущностями) в другую службу, например транспортный сервер, чтобы получить ответ.

Для определения намерения не нужно объединять LUIS и QnA Maker.

Вы можете объединить две службы для этого utterance, если Bot в чате должен обработать текст на основе намерения и сущностей (с помощью LUIS), а также найти конкретный ответ на статический текст (с помощью QnA Maker).

## <a name="when-do-you-use-qna-maker"></a>Когда вы используете QnA Maker?

Используйте QnA Maker, если у вас статическая база знаний с ответами. Такую базу знаний, сформированную из документов PDF и URL-адресов, можно настроить в соответствии со своими требованиями.

Продолжая работу с примером utterance, `How do I get to the Human Resources building on the Seattle North campus?` отправьте текст в качестве запроса в опубликованную службу QnA Maker и получите наилучший ответ.

Вам не нужно объединять LUIS и QnA Maker, чтобы определить ответ на вопрос.

Вы можете объединить две службы для этого utterance, если Bot в чате должен обработать текст на основе намерения и сущностей (с помощью LUIS), а также найти ответ (с помощью QnA Maker).

## <a name="use-both-services-when-your-knowledge-base-is-incomplete"></a>Использовать обе службы, если база знаний неполна

Если вы создаете базу знаний QnA Maker, но помните, что домен субъекта изменяется (например, своевременная информация), можно сочетать службы LUIS и QnA Maker. Это позволяет использовать информацию в базе знаний, а также использовать LUIS для определения намерения пользователя. После того, как клиентское приложение преднамерено, оно может запросить релевантную информацию из другого источника.

Клиентское приложение должно отслеживать LUIS и QnA Maker ответы для оценки. Если оценка от QnA Maker находится ниже какого-либо произвольного порогового значения, используйте сведения о намерении и сущности, возвращенные из LUIS, для передачи информации в службу стороннего производителя.

Продолжим пример текста, `How do I get to the Human Resources building on the Seattle North campus?` Предположим, что QnA Maker Возвращает оценку низкой достоверности. Используйте намерение, возвращенное из LUIS, `FindLocation` и все извлеченные сущности, такие как `Human Resources building` и `Seattle North campus` , чтобы отправить эту информацию в службу сопоставления или поиска для другого ответа.

Вы можете предоставить этот ответ сторонним пользователям для проверки. После утверждения пользователя можно вернуться к QnA Maker, чтобы добавить сведения, чтобы расширить свои знания.

## <a name="use-both-services-when-your-chat-bot-needs-more-information"></a>Используйте обе службы, когда программе Chat Bot требуется дополнительная информация

Если программе-роботу для разговора требуется больше информации, чем любая служба, то для продолжения работы с деревом принятия решений используйте обе службы и обрабатывайте оба ответа в клиентском приложении.

Используйте средство CLI для **[диспетчеризации](https://github.com/Microsoft/botbuilder-tools/tree/master/packages/Dispatch)** инфраструктуры, чтобы создать процесс для работы с обеими службами. Это средство создает наиболее LUISное приложение для целей, которые переправляются между LUIS и QnA Maker как дочерние приложения. Дополнительные [сведения](/azure/bot-service/bot-builder-tutorial-dispatch?tabs=cs&view=azure-bot-service-4.0) об интеграции с LUIS, QnA Maker и Bot Framework.

Используйте образец программы Bot Builder, **NLP с Dispatch**, в [C#](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/14.nlp-with-dispatch) или [Node.js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/14.nlp-with-dispatch), чтобы реализовать этот тип робота Chat.

## <a name="best-practices"></a>Рекомендации

Реализуйте рекомендации для каждой службы:

* Рекомендации по [Luis](../luis/luis-concept-best-practices.md)
* Рекомендации по [QnA Maker](../qnamaker/concepts/best-practices.md)

## <a name="see-also"></a>См. также

* [Распознавание речи (LUIS)](../luis/what-is-luis.md)
* [QnA Maker](../qnamaker/overview/overview.md)
* [Диспетчер CLI](https://github.com/Microsoft/botbuilder-tools/tree/master/packages/Dispatch)
* [Примеры для платформы Bot](https://github.com/Microsoft/BotBuilder-Samples)
* [Служба Azure Bot](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)
* [Эмулятор Azure Bot](https://github.com/Microsoft/BotFramework-Emulator)
* [Веб-чат для платформы Bot](https://github.com/microsoft/BotFramework-WebChat)