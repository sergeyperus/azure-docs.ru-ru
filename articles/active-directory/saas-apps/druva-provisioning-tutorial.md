---
title: Руководство по настройке Druva для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт
description: Сведения о настройке Azure Active Directory для автоматической подготовки и отзыва учетных записей пользователей в Druva.
services: active-directory
author: zchia
writer: zchia
manager: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 07/26/2019
ms.author: zhchia
ms.openlocfilehash: 5579a9d96828caa1453547e7c2e11b8f0d717d2a
ms.sourcegitcommit: 0b9fe9e23dfebf60faa9b451498951b970758103
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2020
ms.locfileid: "94359312"
---
# <a name="tutorial-configure-druva-for-automatic-user-provisioning"></a>Руководство по настройке Druva для автоматической подготовки пользователей

В этом учебнике описаны шаги, которые нужно выполнить в Druva и Azure Active Directory (Azure AD), чтобы настроить Azure AD для автоматической подготовки и отзыва пользователей и (или) групп в Druva.

> [!NOTE]
> В этом руководстве рассматривается соединитель, созданный на базе службы подготовки пользователей Azure AD. Подробные сведения о том, что делает эта служба, как она работает, и часто задаваемые вопросы см. в статье [Автоматическая подготовка пользователей и ее отзыв для приложений SaaS в Azure Active Directory](../app-provisioning/user-provisioning.md).
>
> Сейчас этот соединитель предоставляется в общедоступной предварительной версии. Дополнительные сведения об общих условиях использования продуктов в предварительной версии см. в документе [Дополнительные условия использования Предварительных версий Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="prerequisites"></a>Предварительные требования

В сценарии, описанном в этом руководстве, предполагается, что у вас уже имеется:

* Клиент Azure AD.
* [клиент Druva;](https://www.druva.com/products/pricing-plans/).
* учетная запись пользователя в Druva с разрешениями администратора.

## <a name="assigning-users-to-druva"></a>Назначение пользователей в Druva

В Azure Active Directory для определения того, какие пользователи должны получать доступ к выбранным приложениям, используется концепция, называемая *назначением*. В контексте автоматической подготовки синхронизируются только те пользователи и (или) группы, которые были назначены конкретному приложению в Azure AD.

Перед настройкой и включением автоматической подготовки пользователей нужно решить, какие пользователи и (или) группы в Azure AD должны иметь доступ к Druva. Когда данный вопрос будет решен, этих пользователей и (или) группы можно будет назначить приложению Druva, следуя инструкциям:
* [Назначение корпоративному приложению пользователя или группы](../manage-apps/assign-user-or-group-access-portal.md)

## <a name="important-tips-for-assigning-users-to-druva"></a>Важные рекомендации по назначению пользователей в Druva

* Рекомендуется назначить одного пользователя Azure AD в Druva для тестирования конфигурации автоматической подготовки пользователей. Дополнительные пользователи и/или группы можно назначить позднее.

* При назначении пользователя в Druva в диалоговом окне назначения необходимо выбрать действительную роль для конкретного приложения (если доступно). Пользователи с ролью **Доступ по умолчанию** исключаются из подготовки.

## <a name="setup-druva-for-provisioning"></a>Настройка Druva для подготовки

Перед настройкой Druva для автоматической подготовки пользователей с помощью Azure AD необходимо включить подготовку SCIM в Druva.

1. Войдите в [консоль администрирования Druva](https://console.druva.com). Выберите **Druva > inSync (Синхронизация)** .

    ![Консоль администрирования Druva](media/druva-provisioning-tutorial/menubar.png)

2. Выберите **Manage (Управление)**  > **Deployments (Развертывания)**  > **Users (Пользователи)** .

    :::image type="content" source="media/druva-provisioning-tutorial/manage.png" alt-text="Снимок экрана консоли администрирования Druva. Выделен элемент Manage (Управление), отображается меню Manage (Управление). В этом меню в разделе &quot;Развертывания&quot; выделен пункт &quot;Пользователи&quot;." border="false":::

3.  Выберите **Settings** (Параметры). Щелкните **Generate Token** (Создать токен).

    :::image type="content" source="media/druva-provisioning-tutorial/settings.png" alt-text="Снимок экрана: страница в консоли администрирования Druva. Выделен элемент Settings (Параметры), вкладка Settings (Параметры) открыта. Выделена кнопка Generate token (Создать токен)." border="false":::

4.  Скопируйте значение параметра **Auth token** (Токен проверки подлинности). Его нужно будет ввести в поле **Секретный токен** на вкладке "Подготовка" для приложения Druva на портале Azure.
    
    :::image type="content" source="media/druva-provisioning-tutorial/auth.png" alt-text="Снимок экрана: страница Create token (Создание токена) в консоли администрирования Druva. Ссылка с подписью Copy Token (Копировать токен) доступна для копирования значения токена проверки подлинности." border="false":::

## <a name="add-druva-from-the-gallery"></a>Добавление Druva из коллекции

Чтобы настроить Druva для автоматической подготовки пользователей в Azure AD, необходимо добавить Druva из коллекции приложений Azure AD в список управляемых приложений SaaS.

**Чтобы добавить Druva из коллекции приложений Azure AD, сделайте следующее:**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева выберите элемент **Azure Active Directory**.

    ![Кнопка Azure Active Directory](common/select-azuread.png)

2. Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.

    ![Колонка "Корпоративные приложения"](common/enterprise-applications.png)

3. Чтобы добавить новое приложение, в области сверху нажмите кнопку **Новое приложение**.

    ![Кнопка "Создать приложение"](common/add-new-app.png)

4. В поле поиска введите **Druva**, выберите **Druva** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Druva в списке результатов](common/search-new-app.png)

## <a name="configuring-automatic-user-provisioning-to-druva"></a>Настройка автоматической подготовки пользователей в Druva 

В этом разделе описывается, как настроить службу подготовки Azure AD для создания, обновления и отключения пользователей и (или) групп в Druva на основе их назначений в Azure AD.

> [!TIP]
> Для Druva также можно включить единый вход на основе SAML. Для этого следуйте инструкциям, приведенным в [учебнике по единому входу в Druva](druva-tutorial.md). Единый вход можно настроить независимо от автоматической подготовки пользователей, хотя эти две возможности дополняют друг друга.

### <a name="to-configure-automatic-user-provisioning-for-druva-in-azure-ad"></a>Чтобы настроить автоматическую подготовку пользователей в Druva, сделайте следующее:

1. Войдите на [портал Azure](https://portal.azure.com). Выберите **Корпоративные приложения**, а затем **Все приложения**.

    ![Колонка "Корпоративные приложения"](common/enterprise-applications.png)

2. В списке приложений выберите **Druva**.

    ![Ссылка на Druva в списке "Приложения"](common/all-applications.png)

3. Выберите вкладку **Подготовка**.

    ![Снимок экрана: раздел "Управление" с выделенным параметром "Подготовка".](common/provisioning.png)

4. Для параметра **Режим подготовки к работе** выберите значение **Automatic** (Автоматически).

    ![Снимок экрана: раскрывающийся список "Режим подготовки" с выделенным параметром "Автоматически".](common/provisioning-automatic.png)

5.  В разделе "Учетные данные администратора" введите значение `https://apis.druva.com/insync/scim` в поле **URL-адрес клиента**. Введите значение **токена проверки подлинности** в поле **Секретный токен**. Щелкните **Проверить подключение**, чтобы убедиться, что Azure AD может подключиться к Druva. Если установить подключение не удалось, убедитесь, что у учетной записи Druva есть разрешения администратора, и повторите попытку.

    ![URL-адрес клиента + токен](common/provisioning-testconnection-tenanturltoken.png)

6. В поле **Почтовое уведомление** введите адрес электронной почты пользователя или группы, которые должны получать уведомления об ошибках подготовки, а также установите флажок **Отправить уведомление по электронной почте при сбое**.

    ![Почтовое уведомление](common/provisioning-notification-email.png)

7. Выберите команду **Сохранить**.

8. В разделе **Сопоставления** выберите **Synchronize Azure Active Directory Users to Druva** (Синхронизировать пользователей Azure Active Directory с Druva).

    ![Сопоставления пользователей Druva](media/druva-provisioning-tutorial/usermapping.png)

9. В разделе **Сопоставление атрибутов** просмотрите атрибуты пользователей, синхронизированные из Azure AD в Druva. Атрибуты, выбранные как свойства **сопоставления**, используются для сопоставления учетных записей пользователей в Druva для операций обновления. Нажмите кнопку **Сохранить**, чтобы зафиксировать все изменения.

    ![Атрибуты пользователя Druva](media/druva-provisioning-tutorial/userattribute.png)


10. Чтобы настроить фильтры области, ознакомьтесь со следующими инструкциями, предоставленными в [руководстве по фильтрам области](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md).

11. Чтобы включить службу подготовки Azure AD для Druva, в разделе **Параметры** измените значение параметра **Состояние подготовки** на **Включено**.

    ![Состояние подготовки "Включено"](common/provisioning-toggle-on.png)

12. Определите пользователей и (или) группы для подготовки в Druva, выбрав нужные значения в поле **Область** в разделе **Параметры**.

    ![Область действия подготовки](common/provisioning-scope.png)

13. Когда будете готовы выполнить подготовку, нажмите кнопку **Сохранить**.

    ![Сохранение конфигурации подготовки](common/provisioning-configuration-save.png)

    После этого начнется начальная синхронизация пользователей и (или) групп, определенных в поле **Область** раздела **Параметры**. Начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Если служба запущена, они выполняются примерно каждые 40 минут. В разделе **Сведения о синхронизации** можно отслеживать ход выполнения и переходить по ссылкам для просмотра отчетов о подготовке, в которых зафиксированы все действия, выполняемые службой подготовки Azure AD с приложением Druva.

    Дополнительные сведения о чтении журналов подготовки Azure AD см. в руководстве по [отчетам об автоматической подготовке учетных записей](../app-provisioning/check-status-user-account-provisioning.md).
    
## <a name="connector-limitations"></a>Ограничения соединителя

* В Druva атрибут **email** должен быть обязательным. 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](../app-provisioning/configure-automatic-user-provisioning-portal.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a>Дальнейшие действия

* [Сведения о просмотре журналов и получении отчетов о действиях по подготовке](../app-provisioning/check-status-user-account-provisioning.md).
