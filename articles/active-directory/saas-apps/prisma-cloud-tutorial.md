---
title: Руководство по Интеграция единого входа Azure Active Directory с Prisma Cloud SSO | Документация Майкрософт
description: Узнайте, как настроить единый вход между Azure Active Directory и Prisma Cloud SSO.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 02/07/2020
ms.author: jeedes
ms.openlocfilehash: 0a5caf3a52f388bceeec76c411b0bda21669baf2
ms.sourcegitcommit: 59f506857abb1ed3328fda34d37800b55159c91d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92515277"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-prisma-cloud-sso"></a>Руководство по Интеграция единого входа Azure Active Directory с Prisma Cloud SSO

В этом руководстве описано, как интегрировать Prisma Cloud SSO с Azure Active Directory (Azure AD). Интеграция Prisma Cloud SSO с Azure AD обеспечивает приведенные ниже возможности.

* Контроль доступа к Prisma Cloud SSO с помощью Azure AD.
* Включение автоматического входа пользователей в Prisma Cloud SSO с помощью учетных записей Azure AD.
* Централизованное управление учетными записями через портал Azure.

Чтобы узнать больше об интеграции приложений SaaS с Azure AD, прочитайте статью [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

## <a name="prerequisites"></a>Предварительные требования

Чтобы приступить к работе, потребуется следующее.

* Подписка Azure AD. Если у вас нет подписки, вы можете получить [бесплатную учетную запись](https://azure.microsoft.com/free/).
* Подписка Prisma Cloud SSO с поддержкой единого входа.

## <a name="scenario-description"></a>Описание сценария

В рамках этого руководства вы настроите и проверите единый вход Azure AD в тестовой среде.

* Prisma Cloud SSO поддерживает единый вход, инициированный **IDP**

* Prisma Cloud SSO поддерживает **JIT** -подготовку пользователей

* После настройки Prisma Cloud SSO можно применять элементы управления сеансами, которые защищают от хищения и несанкционированного доступа к конфиденциальным данным вашей организации в режиме реального времени. Элементы управления сеансом являются расширением функции условного доступа. [Узнайте, как применять управление сеансами с помощью Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-any-app).

## <a name="adding-prisma-cloud-sso-from-the-gallery"></a>Добавление Prisma Cloud SSO из коллекции

Чтобы настроить интеграцию Prisma Cloud SSO с Azure AD, необходимо добавить Prisma Cloud SSO из коллекции в список управляемых приложений SaaS.

1. Войдите на [портал Azure](https://portal.azure.com) с помощью личной учетной записи Майкрософт либо рабочей или учебной учетной записи.
1. В области навигации слева выберите службу **Azure Active Directory** .
1. Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения** .
1. Чтобы добавить новое приложение, выберите **Новое приложение** .
1. В разделе **Добавление из коллекции** в поле поиска введите **Prisma Cloud SSO** .
1. Выберите **Prisma Cloud SSO** в области результатов и добавьте это приложение. Подождите несколько секунд, пока приложение не будет добавлено в ваш клиент.

## <a name="configure-and-test-azure-ad-single-sign-on-for-prisma-cloud-sso"></a>Настройка и проверка единого входа Azure AD для Prisma Cloud SSO

Настройте и проверьте единый вход Azure AD в Prisma Cloud SSO с помощью тестового пользователя **B.Simon** . Для обеспечения работы единого входа необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Prisma Cloud SSO.

Чтобы настроить и проверить единый вход Azure AD в Prisma Cloud SSO, выполните действия в следующих стандартных блоках:

1. **[Настройка единого входа Azure AD](#configure-azure-ad-sso)** необходима, чтобы пользователи могли использовать эту функцию.
    1. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD с помощью пользователя B.Simon.
    1. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить пользователю B.Simon использовать единый вход Azure AD.
1. **[Настройка единого входа в Prisma Cloud](#configure-prisma-cloud-sso)** необходима, чтобы настроить параметры единого входа на стороне приложения.
    1. **[Создание тестового пользователя Prisma Cloud SSO](#create-prisma-cloud-sso-test-user)** требуется для того, чтобы в Prisma Cloud SSO существовал пользователь B.Simon, связанный с одноименным пользователем в Azure AD.
1. **[Проверка единого входа](#test-sso)** позволяет убедиться в правильности конфигурации.

## <a name="configure-azure-ad-sso"></a>Настройка единого входа Azure AD

Выполните следующие действия, чтобы включить единый вход Azure AD на портале Azure.

1. На [портале Azure](https://portal.azure.com/) на странице интеграции с приложением **Prisma Cloud SSO** найдите раздел **Управление** и выберите **Единый вход** .
1. На странице **Выбрать метод единого входа** выберите **SAML** .
1. На странице **Настройка единого входа с помощью SAML** щелкните значок "Изменить" (значок пера), чтобы открыть диалоговое окно **Базовая конфигурация SAML** и изменить параметры.

   ![Изменение базовой конфигурации SAML](common/edit-urls.png)

1. На странице **Настройка единого входа с помощью SAML** введите значения для следующих полей:

    а. В текстовом поле **Идентификатор** введите URL-адрес в формате `https://app2.prismacloud.io/customer/<CUSTOMERID>`.

    b. Значения **URL-адрес ответа** на портале Azure являются фиксированными и предварительно заполненными. Вам необходимо выбрать соответствующий URL-адрес согласно требованиям.

    > [!NOTE]
    > Значение идентификатора приведено для примера и не является реальным. Вместо него нужно указать фактический идентификатор. Чтобы получить это значение, [обратитесь в службу поддержки клиентов Prisma Cloud SSO](mailto:support@paloaltonetworks.com). Можно также посмотреть шаблоны в разделе **Базовая конфигурация SAML** на портале Azure.

1. На странице **Настройка единого входа с помощью SAML** в разделе **Сертификат подписи SAML** найдите пункт **Сертификат (Base64)** и щелкните **Скачать** , чтобы скачать сертификат. Сохраните этот сертификат на компьютере.

    ![Ссылка для скачивания сертификата](common/certificatebase64.png)

1. Скопируйте требуемый URL-адрес из раздела **Настройка Prisma Cloud SSO** .

    ![Копирование URL-адресов настройки](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

В этом разделе описано, как на портале Azure создать тестового пользователя с именем B.Simon.

1. На портале Azure в области слева выберите **Azure Active Directory** , **Пользователи** , а затем — **Все пользователи** .
1. В верхней части экрана выберите **Новый пользователь** .
1. В разделе **Свойства пользователя** выполните следующие действия.
   1. В поле **Имя** введите `B.Simon`.  
   1. В поле **Имя пользователя** введите username@companydomain.extension. Например, `B.Simon@contoso.com`.
   1. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль** .
   1. Нажмите кнопку **Создать** .

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как включить единый вход в Azure для пользователя B.Simon, предоставив этому пользователю доступ к Prisma Cloud SSO.

1. На портале Azure выберите **Корпоративные приложения** , а затем — **Все приложения** .
1. Из списка приложений выберите **Prisma Cloud SSO** .
1. На странице "Обзор" приложения найдите раздел **Управление** и выберите **Пользователи и группы** .

   ![Ссылка "Пользователи и группы"](common/users-groups-blade.png)

1. Выберите **Добавить пользователя** , а в диалоговом окне **Добавление назначения**  выберите **Пользователи и группы** .

    ![Ссылка "Добавить пользователя"](common/add-assign-user.png)

1. В диалоговом окне **Пользователи и группы** выберите **B.Simon** в списке пользователей, а затем в нижней части экрана нажмите кнопку **Выбрать** .
1. Если ожидается, что в утверждении SAML будет получено какое-либо значение роли, то в диалоговом окне **Выбор роли** нужно выбрать соответствующую роль для пользователя из списка и затем нажать кнопку **Выбрать** , расположенную в нижней части экрана.
1. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить** .

## <a name="configure-prisma-cloud-sso"></a>Настройка единого входа Prisma Cloud

Чтобы настроить единый вход на стороне **Prisma Cloud SSO** , нужно отправить скачанный **сертификат (Base64)** и соответствующие URL-адреса, скопированные на портале Azure в [группу поддержки Prisma Cloud SSO](mailto:support@paloaltonetworks.com). Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.

### <a name="create-prisma-cloud-sso-test-user"></a>Создание тестового пользователя Prisma Cloud SSO

В этом разделе описано, как в приложении Prisma Cloud SSO создать пользователя B.Simon. Приложение Prisma Cloud SSO поддерживает JIT-подготовку. Эта функция включена по умолчанию. В этом разделе никакие действия с вашей стороны не требуются. Если пользователь еще не существует в Prisma Cloud SSO, он создается при попытке доступа к приложению Prisma Cloud SSO.

## <a name="test-sso"></a>Проверка единого входа 

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув на плитку Prisma Cloud SSO на панели доступа, вы автоматически войдете в приложение Prisma Cloud SSO, для которого настроили единый вход. См. дополнительные сведения о [панели доступа](../user-help/my-apps-portal-end-user-access.md)

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Список учебников по интеграции приложений SaaS с Azure Active Directory](./tutorial-list.md)

- [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

- [Что представляет собой условный доступ в Azure Active Directory?](../conditional-access/overview.md)

- [Что такое управление сеансами в Microsoft Cloud App Security?](/cloud-app-security/proxy-intro-aad)

- [Пробное использование Prisma Cloud SSO с Azure AD](https://aad.portal.azure.com/)