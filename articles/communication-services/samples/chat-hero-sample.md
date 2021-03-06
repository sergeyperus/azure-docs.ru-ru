---
title: Главный пример функции группового чата
titleSuffix: An Azure Communication Services sample overview
description: Обзор главного примера функции чата с использованием Служб коммуникации Azure, который предоставит разработчикам дополнительные сведения о том, как работает этот пример, и о том, как его изменить.
author: ddematheu2
manager: nimag
services: azure-communication-services
ms.author: dademath
ms.date: 07/20/2020
ms.topic: overview
ms.service: azure-communication-services
ms.openlocfilehash: fc757e1310369c48de24c0cc9253c668ca27495c
ms.sourcegitcommit: 230d5656b525a2c6a6717525b68a10135c568d67
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/19/2020
ms.locfileid: "94888578"
---
# <a name="get-started-with-the-group-chat-hero-sample"></a>Начало работы с главным примером функции чата

[!INCLUDE [Public Preview Notice](../includes/public-preview-include.md)]

<!----
> [!WARNING]
> links to our Hero Sample repo need to be updated when the sample is publicly available.
---->

> [!IMPORTANT]
> [Этот пример можно найти на сайте GitHub.](https://github.com/Azure-Samples/communication-services-web-chat-hero)


В **главном примере функции чата** Служб коммуникации Azure показано, как можно использовать библиотеку веб-клиента чата Служб коммуникации для создания группового вызова.

Из краткого руководства мы узнаем, как работает пример и запустим его на локальном компьютере. Затем мы развернем пример в Azure с помощью собственных ресурсов Служб коммуникации Azure.


## <a name="overview"></a>Обзор

Пример содержит клиентское и серверное приложения. **Клиентское приложение** — это веб-приложение React/Redux, использующее платформу пользовательского интерфейса Fluent от Майкрософт. Это приложение отправляет запросы в **серверное приложение** ASP.NET Core, которое помогает клиентскому приложению подключаться к Azure. 

Вот как выглядит этот пример:

:::image type="content" source="./media/chat/landing-page.png" alt-text="Снимок экрана, на котором показана целевая страница примера приложения.":::

При нажатии кнопки "Начать чат" веб-приложение получает маркер доступа пользователя из приложения на стороне сервера. Затем этот маркер используется для подключения клиентского приложения к Службам коммуникации Azure. После получения маркера вам будет предложено указать имя и эмодзи, которые будут представлять вас в чате. 

:::image type="content" source="./media/chat/pre-chat.png" alt-text="Снимок экрана: экран приложения перед созданием чата.":::

После настройки отображаемого имени и эмодзи вы можете присоединиться к сеансу чата. Теперь вы увидите основной холст чата, где находятся основные возможности чата.

:::image type="content" source="./media/chat/main-app.png" alt-text="Снимок экрана: главный экран примера приложения.":::

Компоненты главного экрана чата:

- **Основная область чата**: это основные возможности чата, с помощью которых пользователи могут отправлять и получать сообщения. Для отправки сообщений можно использовать область ввода и нажать клавишу "ВВОД" (или использовать кнопку "Отправить"). Полученные сообщения в чате классифицируются по отправителю с правильными именами и эмодзи. В области чата вы увидите два типа уведомлений: 1) уведомления о вводе, когда пользователь печатает, и 2) уведомления об отправке и прочтении сообщений.
- **Заголовок**: здесь пользователь увидит заголовок потока чата и элементы управления для переключения между боковыми панелями участников и параметров, а также кнопку "Выйти" для выхода из сеанса чата.
- **Боковая панель**: здесь отображаются участники и сведения о параметрах при переключении с помощью элементов управления в заголовке. Боковая панель участников содержит список участников в чате и ссылку для приглашения участников в сеанс чата. Боковая панель параметров позволяет настроить заголовок потока чата. 

Ниже вы найдете дополнительные сведения о предварительных требованиях и шагах по настройке примера.

## <a name="prerequisites"></a>Предварительные требования

- Создайте учетную запись Azure с активной подпиской. Дополнительные сведения см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Node.js (8.11.2 и более поздние версии)](https://nodejs.org/en/download/)
- [Visual Studio 2017 и более поздние версии](https://visualstudio.microsoft.com/vs/)
- [.NET Core 3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1) (установите 32- или 64-разрядную версию в соответствии с версией экземпляра Visual Studio).
- Создайте ресурс Служб коммуникации Azure. Дополнительные сведения см. в статье [Краткое руководство по созданию ресурсов Служб коммуникации и управлению ими](../quickstarts/create-communication-resource.md). Для работы с этим кратким руководством необходимо записать **строку подключения** к ресурсу.

## <a name="locally-deploying-the-service--client-app"></a>Локальное развертывание приложения службы и клиентского приложения

Пример чата с использованием одного потока — это по сути два приложения — клиентское и серверное приложение.

Откройте Visual Studio в chat.csproj и запустите в режиме отладки, после чего запустится служба внешнего интерфейса чата. При посещении серверного приложения из браузера оно перенаправляет трафик в локально развернутую службу внешнего интерфейса чата.

Вы можете проверить пример локально, открыв несколько сеансов браузера с URL-адресом чата, чтобы имитировать чат для нескольких пользователей.

## <a name="before-running-the-sample-for-the-first-time"></a>Перед первым запуском примера

1. Откройте экземпляр PowerShell, Терминал Windows, командную строку или эквивалент и перейдите в каталог, в который вы хотите клонировать пример.
2. `git clone https://github.com/Azure-Samples/communication-services-web-chat-hero.git`
3. Получите `Connection String` с помощью портала Azure. Дополнительные сведения о строках подключения см. в статье [Создание ресурсов Служб коммуникации Azure и управление ими](../quickstarts/create-communication-resource.md).
4. После получения `Connection String` добавьте строку подключения в файл **Chat/appsettings.json**, расположенный в папке Chat. Сохраните строку подключения в переменную: `ResourceConnectionString`.

### <a name="local-run"></a>Локальный запуск

1. Перейдите в папку Chat и откройте решение `Chat.csproj` в Visual Studio.
2. Запустите проект. Браузер откроет страницу по адресу localhost:5000.

#### <a name="troubleshooting"></a>Диагностика

- Решение не выполняет сборку, оно выдает ошибки во время установки или выполнения сборки NPM.

   Очистите и перестройте решение C#.

## <a name="publish-the-sample-to-azure"></a>Публикация примера в Azure

1. Щелкните правой кнопкой мыши проект `Chat` и выберите команду "Опубликовать".
2. Создайте профиль публикации и выберите подписку Azure.
3. Перед публикацией добавьте строку подключения с `Edit App Service Settings`, а затем укажите `ResourceConnectionString` в качестве ключа и строку подключения (скопированную из appsettings.json) в качестве значения.

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы хотите очистить и удалить подписку на Службы коммуникации, вы можете удалить ресурс или группу ресурсов. При этом удаляются все ресурсы, связанные с ней. См. сведения об [очистке ресурсов](../quickstarts/create-communication-resource.md#clean-up-resources).

## <a name="next-steps"></a>Дальнейшие действия

>[!div class="nextstepaction"] 
>[Скачайте пример с GitHub.](https://github.com/Azure-Samples/communication-services-web-chat-hero)

Дополнительные сведения см. в следующих статьях:

- Сведения о [концепциях чата](../concepts/chat/concepts.md)
- Ознакомьтесь с нашей [клиентской библиотекой чата](../concepts/chat/sdk-features.md)

## <a name="additional-reading"></a>Дополнительные материалы

- [Службы коммуникации Azure (GitHub)](https://github.com/Azure/communication) — дополнительные примеры и сведения на официальной странице GitHub
- [Redux](https://redux.js.org/) — управление состоянием на стороне клиента
- [FluentUI](https://aka.ms/fluent-ui) — библиотека пользовательского интерфейса, поддерживаемая корпорацией Майкрософт
- [React](https://reactjs.org/) — библиотека для создания пользовательских интерфейсов
- [ASP.NET Core](/aspnet/core/introduction-to-aspnet-core?preserve-view=true&view=aspnetcore-3.1) — платформа для создания веб-приложений