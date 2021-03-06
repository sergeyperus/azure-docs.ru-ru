---
title: Учебник. Интеграция Azure Active Directory с Skillport | Документы Майкрософт
description: Узнайте, как настроить единый вход Azure Active Directory в приложении Skillport.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 03/25/2019
ms.author: jeedes
ms.openlocfilehash: ed71311125229a7575c675dd3338b4908ea1be95
ms.sourcegitcommit: 59f506857abb1ed3328fda34d37800b55159c91d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2020
ms.locfileid: "92518438"
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a>Руководство по интеграции Azure Active Directory с Skillport

В этом руководстве описано, как интегрировать Skillport с Azure Active Directory (Azure AD).
Интеграция Azure AD с приложением Skillport обеспечивает следующие преимущества.

* В Azure AD вы можете контролировать доступ к Skillport.
* Вы можете включить автоматический вход пользователей в приложение Skillport (единый вход) с помощью учетных записей Azure AD.
* Вы можете управлять учетными записями централизованно на портале Azure.

Дополнительные сведения об интеграции приложений SaaS с Azure AD см. в статье [Единый вход в приложениях в Azure Active Directory](../manage-apps/what-is-single-sign-on.md).
Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.

## <a name="prerequisites"></a>предварительные требования

Чтобы настроить интеграцию Azure AD с Skillport, вам потребуется:

* подписка Azure AD; (если у вас нет среды Azure AD, вы можете получить [бесплатную учетную запись](https://azure.microsoft.com/free/));
* Подписка на Skillport с возможностью единого входа

## <a name="scenario-description"></a>Описание сценария

В рамках этого руководства вы настроите и проверите единый вход Azure AD в тестовой среде.

* Skillport поддерживает единый вход, инициированный **пакетом обновления**

## <a name="adding-skillport-from-the-gallery"></a>Добавление Skillport из коллекции

Чтобы настроить интеграцию приложения Skillport с Azure AD, вам нужно добавить Skillport из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Skillport из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory** .

    ![Кнопка Azure Active Directory](common/select-azuread.png)

2. Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения** .

    ![Колонка "Корпоративные приложения"](common/enterprise-applications.png)

3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение** .

    ![Кнопка "Создать приложение"](common/add-new-app.png)

4. В поле поиска введите **Skillport** , на панели результатов выберите **Skillport** и нажмите на кнопку **Добавить** , чтобы добавить это приложение.

    ![Skillport в списке результатов](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описаны настройка и проверка единого входа Azure AD в Skillport с помощью тестового пользователя **Britta Simon** .
Для обеспечения работы единого входа необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Skillport.

Чтобы настроить и проверить единый вход Azure AD в Skillport, вам потребуется выполнить действия в следующих стандартных блоках.

1. **[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Настройка единого входа Skillport](#configure-skillport-single-sign-on)** необходима, чтобы конфигурировать параметры единого входа на стороне приложения.
3. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
4. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы разрешить пользователю Britta Simon использовать единый вход Azure AD.
5. **[Создание тестового пользователя Skillport](#create-skillport-test-user)** требуется для того, чтобы в Skillport также существовал пользователь Britta Simon, связанный с представлением этого же пользователя в Azure AD.
6. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы проверить работу конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе описано включение единого входа Azure AD на портале Azure.

Чтобы настроить единый вход Azure AD в Skillport, выполните следующие действия.

1. На [портале Azure](https://portal.azure.com/) на странице интеграции с приложением **Skillport** щелкните **Единый вход** .

    ![Ссылка "Настройка единого входа"](common/select-sso.png)

2. В диалоговом окне **Выбрать метод единого входа** выберите режим **SAML/WS-Fed** , чтобы включить единый вход.

    ![Режим выбора единого входа](common/select-saml-option.png)

3. На странице **Настройка единого входа с помощью SAML** щелкните **Изменить** , чтобы открыть диалоговое окно **Базовая конфигурация SAML** .

    ![Правка базовой конфигурации SAML](common/edit-urls.png)

4. В разделе **Базовая конфигурация SAML** выполните приведенные ниже действия.

    ![Сведения о домене и URL-адресах единого входа приложения Skillport](common/sp-identifier-reply.png)

    а. В текстовом поле **URL-адрес входа** введите URL-адрес:

    Центр обработки данных в ЕС: `https://adfs.skillport.eu`

    Центр обработки данных в США: `https://sso.skillport.com`

    b. В поле **Идентификатор** введите URL-адрес:

    Центр обработки данных в ЕС: `http://adfs.skillport.eu/adfs/services/trust`

    Центр обработки данных в США: `https://sso.skillport.com`

    c. В текстовом поле **URL-адрес ответа** введите URL-адрес:

    Центр обработки данных в ЕС: `https://adfs.skillport.eu/adfs/ls/`

      Центр обработки данных в США: `https://sso.skillport.com/sp/ACS.saml2`

5. На странице **Настройка единого входа с помощью SAML** в разделе **Сертификат подписи SAML** щелкните **Скачать** , чтобы скачать нужный вам **XML метаданных федерации** , и сохраните его на компьютере.

    ![Ссылка для скачивания сертификата](common/metadataxml.png)

6. Скопируйте нужные URL-адреса в разделе **Настройка Skillport** .

    ![Копирование URL-адресов настройки](common/copy-configuration-urls.png)

    а. URL-адрес входа.

    b. Идентификатор Azure AD

    c. URL-адрес выхода.

### <a name="configure-skillport-single-sign-on"></a>Настройка единого входа в Skillport

Чтобы настроить единый вход со стороны **Skillport** , нужно отправить в [группу поддержки Skillport](https://www.skillsoft.com/about/contact-us) скачанный **XML-файл метаданных федерации** и соответствующие URL-адреса, скопированные на портале Azure. Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

1. На портале Azure в области слева выберите **Azure Active Directory** , **Пользователи** , а затем — **Все пользователи** .

    ![Ссылки "Пользователи и группы" и "Все пользователи"](common/users.png)

2. В верхней части экрана выберите **Новый пользователь** .

    ![Кнопка "Новый пользователь"](common/new-user.png)

3. В разделе свойств пользователя сделайте следующее:

    ![Диалоговое окно "Пользователь"](common/user-properties.png)

    а. В поле **Имя** введите **BrittaSimon** .
  
    b. В поле **Имя пользователя** введите `brittasimon@yourcompanydomain.extension`.  
    Например BrittaSimon@contoso.com.

    c. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле "Пароль".

    d. Нажмите кнопку **Создать** .

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Skillport.

1. На портале Azure выберите **Корпоративные приложения** , **Все приложения** , а затем **Skillport** .

    ![Колонка "Корпоративные приложения"](common/enterprise-applications.png)

2. В списке приложений выберите **Skillport** .

    ![Ссылка на Skillport в списке приложений](common/all-applications.png)

3. В меню слева выберите **Пользователи и группы** .

    ![Ссылка "Пользователи и группы"](common/users-groups-blade.png)

4. Нажмите кнопку **Добавить пользователя** , а затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы** .

    ![Область "Добавление назначения"](common/add-assign-user.png)

5. В диалоговом окне **Пользователи и группы** из списка пользователей выберите **Britta Simon** , а затем в верхней части экрана нажмите кнопку **Выбрать** .

6. Если ожидается, что в утверждении SAML будет получено какое-либо значение роли, то в диалоговом окне **Выбор ролей** нужно выбрать соответствующую роль для пользователя из списка и затем нажать кнопку **Выбрать** , расположенную в нижней части экрана.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить** .

### <a name="create-skillport-test-user"></a>Создание тестового пользователя Skillport

Чтобы создать тестового пользователя Skillport, обратитесь в [службу поддержки Skillport](https://www.skillsoft.com/about/contact-us), так как они поддерживают различные бизнес-сценарии в соответствии с требованиями пользователей. Специалисты выполнят настройку после обсуждения с пользователями.

### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув плитку Skillport на Панели доступа, вы автоматически войдете в приложение Skillport, для которого настроили единый вход. См. дополнительные сведения о [панели доступа](../user-help/my-apps-portal-end-user-access.md)

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Список учебников по интеграции приложений SaaS с Azure Active Directory](./tutorial-list.md)

- [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

- [Что представляет собой условный доступ в Azure Active Directory?](../conditional-access/overview.md)