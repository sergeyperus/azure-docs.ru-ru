---
title: Руководство по интеграции единого входа Azure Active Directory с VPN SSL FortiGate | Документация Майкрософт
description: Сведения о шагах, которые необходимо выполнить для интеграции FortiGate SSL VPN с Azure Active Directory (Azure AD).
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 18a3d9d5-d81c-478c-be7e-ef38b574cb88
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: tutorial
ms.date: 08/11/2020
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: acb08d5430f13ad9a339b2cdd072fce9c196d05f
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2020
ms.locfileid: "92451491"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-fortigate-ssl-vpn"></a>Руководство по интеграции единого входа Azure Active Directory с VPN SSL FortiGate

В этом руководстве описано, как интегрировать VPN SSL FortiGate с Azure Active Directory (Azure AD). Интеграция VPN SSL FortiGate с Azure AD обеспечивает следующие возможности.

* Контроль доступа к SSL VPN FortiGate с помощью Azure AD.
* Автоматический вход пользователей в SSL VPN FortiGate с помощью учетных записей Azure AD.
* Централизованное управление учетными записями через портал Azure.

Чтобы узнать больше об интеграции приложений SaaS с Azure AD, прочитайте статью [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

## <a name="prerequisites"></a>Предварительные требования

Чтобы приступить к работе, потребуется следующее.

* Подписка Azure AD. Если у вас нет подписки, вы можете получить [бесплатную учетную запись](https://azure.microsoft.com/free/).
* Подписка SSL VPN FortiGate с поддержкой единого входа.

## <a name="tutorial-description"></a>Описание учебника

В рамках этого учебника вы настроите и проверите единый вход Azure AD в тестовой среде.

SSL VPN FortiGate поддерживает единый вход, инициированный поставщиком услуг.

После настройки SSL VPN FortiGate вы можете применить функцию управления сеансом, которая защищает от хищения конфиденциальных данных вашей организации и несанкционированного доступа к ним в реальном времени. Управление сеансом является расширением функции условного доступа. [Узнайте, как применять управление сеансами с помощью Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-any-app).

## <a name="add-fortigate-ssl-vpn-from-the-gallery"></a>Добавление SSL VPN FortiGate из коллекции

Чтобы настроить интеграцию SSL VPN FortiGate с Azure AD, необходимо добавить SSL VPN FortiGate из коллекции в список управляемых приложений SaaS:

1. Войдите на [портал Azure](https://portal.azure.com) с помощью личной учетной записи Майкрософт либо рабочей или учебной учетной записи.
1. В области слева выберите **Azure Active Directory**.
1. Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.
1. Чтобы добавить приложение, выберите **Новое приложение**.
1. В разделе **Добавление из коллекции** в поле поиска введите **SSL VPN FortiGate**.
1. В области результатов выберите **SSL VPN FortiGate** и добавьте это приложение. Подождите несколько секунд, пока приложение не будет добавлено в ваш клиент.

## <a name="configure-and-test-azure-ad-sso-for-fortigate-ssl-vpn"></a>Настройка и проверка единого входа Azure AD для VPN SSL FortiGate

Настройте и проверьте единый вход Azure AD в SSL VPN FortiGate с помощью тестового пользователя B. Simon. Чтобы обеспечить работу единого входа, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SSL VPN FortiGate.

Чтобы настроить и проверить единый вход Azure AD в SSL VPN FortiGate, вам потребуется выполнить приведенные ниже пошаговые действия.

1. **[Настройка единого входа Azure AD](#configure-azure-ad-sso)**  — чтобы ваши пользователи могли использовать эту функцию.
    1. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD.
    1. **[Предоставление тестовому пользователю доступа](#grant-access-to-the-test-user)** необходимо, чтобы разрешить пользователю использовать единый вход Azure AD.
1. **[Настройте единый вход в SSL VPN FortiGate](#configure-fortigate-ssl-vpn-sso)** на стороне приложения.
    1. **Создание тестового пользователя SSL VPN FortiGate** , связанного с одноименным пользователем в Azure AD.
1. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configure-azure-ad-sso"></a>Настройка единого входа Azure AD

Выполните следующие действия, чтобы включить единый вход Azure AD на портале Azure:

1. На [портале Azure](https://portal.azure.com/) на странице интеграции с приложением **SSL VPN FortiGate** в разделе **Управление** выберите **Единый вход**.
1. На странице **Выбрать метод единого входа** выберите **SAML**.
1. На странице **Настройка единого входа с помощью SAML** щелкните значок карандаша, чтобы открыть диалоговое окно **Базовая конфигурация SAML** и изменить эти параметры:

   ![Снимок экрана, на котором показана кнопка карандаша для изменения базовой конфигурации SAML.](common/edit-urls.png)

1. На странице **Настройка единого входа с помощью SAML** введите следующие значения:

    а. В поле **URL-адрес для входа** введите URL-адрес в формате `https://<FQDN>/remote/login`.

    b. В поле **Идентификатор** введите URL-адрес в формате `https://<FQDN>/remote/saml/metadata`.

    c. В поле **URL-адрес ответа** введите URL-адрес в формате `https://<FQDN>/remote/saml/login`.

    d. В поле **URL-адрес выхода** введите URL-адрес в формате `https://<FQDN>/remote/saml/logout`.

    > [!NOTE]
    > Эти значения — шаблоны. Вместо них нужно указать фактический **URL-адрес для входа** , **Идентификатор** , **URL-адрес ответа** и **URL-адрес для выхода**. Чтобы получить их, обратитесь в [группу поддержки клиентов SSL VPN FortiGate](mailto:tac_amer@fortinet.com). Можно также посмотреть шаблоны в разделе **Базовая конфигурация SAML** на портале Azure.

1. Приложение FortiGate SSL VPN ожидает проверочные утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию. На следующем снимке экрана показан список атрибутов по умолчанию.

    ![Снимок экрана, на котором показаны атрибуты по умолчанию.](common/default-attributes.png)

1. В таблице ниже приведены два дополнительных утверждения, требуемые FortiGate SSL VPN. Имена этих утверждений должны соответствовать именам, используемым в разделе **Выполнение настройки командной строки FortiGate** этого руководства. 

   | Имя |  Атрибут источника|
   | ------------ | --------- |
   | username | user.userprincipalname |
   | group | user.groups |
   
   Чтобы создать такие дополнительные утверждения, выполните следующие действия:
   
   1. Рядом с заголовком **Атрибуты и утверждения пользователя** , выберите **Изменить**.
   1. Выберите **Добавить новое утверждение**.
   1. Для параметра **Имя** введите значение **username**.
   1. Для параметра **Исходный атрибут** выберите **user.userprincipalname**.
   1. Щелкните **Сохранить**.
   1. Выберите **Добавить утверждение о группе**.
   1. Выберите **Все группы**.
   1. Установите флажок **Изменить имя утверждения группы**.
   1. Для параметра **Имя** введите значение **group**.
   1. Щелкните **Сохранить**.   

1. На странице **Настройка единого входа с помощью SAML** в разделе **Сертификат подписи SAML** найдите элемент **Сертификат (Base64)** и щелкните **Загрузить** , чтобы загрузить сертификат. Сохраните этот сертификат на компьютере:

    ![Снимок экрана ссылки для загрузки сертификата.](common/certificatebase64.png)

1. Требуемый URL-адрес или URL-адреса вы можете скопировать в разделе **Настройка SSL VPN FortiGate** :

    ![Снимок экрана с URL-адресами конфигурации.](common/copy-configuration-urls.png)

#### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

В этом разделе описано, как создать на портале Azure тестового пользователя с именем B.Simon.

1. На портале Azure в области слева щелкните **Azure Active Directory**. Щелкните **Пользователи** , а затем **Все пользователи**.
1. В верхней части экрана выберите **Новый пользователь**.
1. В свойствах **пользователя** выполните следующие действия:
   1. В поле **Имя** введите **B.Simon**.  
   1. В поле **Имя пользователя** введите \<username>@\<companydomain>.\<extension> Например, `B.Simon@contoso.com`.
   1. Выберите **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.
   1. Нажмите кнопку **создания**.

#### <a name="grant-access-to-the-test-user"></a>Предоставление доступа тестовому пользователю

В этом разделе описано, как включить единый вход Azure для пользователя B. Simon, предоставив этому пользователю доступ к SSL VPN FortiGate.

1. На портале Azure выберите **Корпоративные приложения** , а затем — **Все приложения**.
1. В списке приложений выберите **VPN SSL FortiGate**.
1. В разделе **Управление** на странице сводных данных о приложении выберите **Пользователи и группы** :

   ![Снимок экрана с параметром "Пользователи и группы".](common/users-groups-blade.png)

1. Выберите **Добавить пользователя** , а затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Снимок экрана с кнопкой "Добавить пользователя".](common/add-assign-user.png)

1. В диалоговом окне **Пользователи и группы** выберите **B. Simon** в списке **Пользователи** , а затем в нижней части экрана нажмите кнопку **Выбрать**.
1. Если вы хотите получить значение роли в утверждении SAML, выберите в диалоговом окне **Выбор роли** подходящую роль для пользователя в предложенном списке. В нижней части экрана нажмите кнопку **Выбрать**.
1. В диалоговом окне **Добавление назначения** выберите **Назначить**.

#### <a name="create-a-security-group-for-the-test-user"></a>Создание группы безопасности для тестового пользователя

В этом разделе вы создадите группу безопасности в Azure Active Directory для тестового пользователя. FortiGate будет использовать группу безопасности для предоставления пользователю сетевого доступа через VPN.

1. На портале Azure в области слева щелкните **Azure Active Directory**. Затем выберите **Группы**.
1. В верхней части экрана щелкните **Новый пользователь**.
1. В разделе свойств **Новая группа** выполните следующее.
   1. В списке **Тип группы** выберите **Безопасность**.
   1. В поле **Имя группы** введите **FortiGateAccess**.
   1. В поле **Описание группы** введите **Group for granting FortiGate VPN access** (Группа для предоставления доступа через VPN FortiGate).
   1. Установите для параметра **Azure AD roles can be assigned to the group (Preview)** (Роли Azure AD можно назначить группе (предварительная версия)) значение **Нет**.
   1. В поле **Тип членства** выберите **Назначено**.
   1. В разделе **Участники** выберите **Нет выбранных участников**.
   1. В диалоговом окне **Пользователи и группы** выберите **B. Simon** в списке **Пользователи** , а затем в нижней части экрана нажмите кнопку **Выбрать**.
   1. Нажмите кнопку **создания**.
1. После возвращения в раздел **Группы** в Azure Active Directory найдите группу **Доступ к FortiGate** и обратите внимание на **идентификатор объекта**. Он понадобится вам позднее.

### <a name="configure-fortigate-ssl-vpn-sso"></a>Настройка единого входа в VPN SSL FortiGate

#### <a name="upload-the-base64-saml-certificate-to-the-fortigate-appliance"></a>Загрузка сертификата SAML в кодировке Base64 в приложение FortiGate

После завершения настройки SAML приложения FortiGate в клиенте будет скачан сертификат SAML в кодировке Base64. Необходимо передать этот сертификат на устройство FortiGate:

1. Откройте портал управления приложения FortiGate.
1. В левой области щелкните **Система**.
1. В разделе **Система** выберите **Сертификаты**.
1. Выберите **Импорт** > **Remote Certificate** (Удаленный сертификат).
1. Перейдите к сертификату, загруженному из развертывания приложения FortiGate в клиенте Azure, выберите его и нажмите кнопку **ОК**.

После отправки сертификата запишите его имя в разделе **Система** > **Сертификаты** > **Remote Certificate** (Удаленный сертификат). Имя по умолчанию — REMOTE_Cert_ *N* , где *N*  — это целое значение.

#### <a name="complete-fortigate-command-line-configuration"></a>Завершение настройки из командной строки FortiGate

Для выполнения следующих действий необходимо настроить URL-адрес выхода Azure. Этот URL-адрес содержит символ вопросительного знака (?). Чтобы успешно отправить символ, необходимо выполнить определенные действия. Вы не можете выполнить эти действия из консоли CLI FortiGate. Вместо этого установите сеанс SSH для приложения FortiGate с помощью средства PuTTY. Если приложение FortiGate является виртуальной машиной Azure, вы можете выполнить указанные ниже действия в последовательной консоли виртуальной машины Azure.

Для выполнения этих действий потребуются записанные ранее значения:

- Идентификатор сущности
- URL-адрес ответа
- URL-адрес выхода.
- URL-адрес входа Azure
- Идентификатор Azure AD
- URL-адрес выхода Azure
- Имя сертификата SAML в кодировке Base64 (REMOTE_Cert_ *N* )

1. Установите сеанс SSH для приложения FortiGate и выполните вход с помощью учетной записи администратора FortiGate.
1. Выполните следующие команды:

   ```console
    config user saml
    edit azure
    set entity-id <Entity ID>
    set single-sign-on-url <Reply URL>
    set single-logout-url <Logout URL>
    set idp-single-sign-on-url <Azure Login URL>
    set idp-entity-id <Azure AD Identifier>
    set idp-single-logout-url <Azure Logout URL>
    set idp-cert <Base64 SAML Certificate Name>
    set user-name username
    set group-name group
    end

   ```

   > [!NOTE]
   > URL-адрес выхода Azure содержит знак `?`. Чтобы правильно указать этот URL-адрес в последовательной консоли FortiGate, необходимо нажать правильную последовательность клавиш. Обычно URL-адресом является `https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0`.
   >
   > Чтобы ввести URL-адрес выхода Azure в последовательной консоли, введите `set idp-single-logout-url https://login.microsoftonline.com/common/wsfederation`.
   > 
   > Затем нажмите клавиши CTRL+V и вставьте остальную часть URL-адреса, чтобы завершить строку: `set idp-single-logout-url https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0`.

#### <a name="configure-fortigate-for-group-matching"></a>Настройка FortiGate для сопоставления групп

В этом разделе вы настроите FortiGate для распознавания идентификатора объекта группы безопасности, которая содержит тестового пользователя. Настройка позволит FortiGate принимать решения о доступе на основе членства в группе.

Для выполнения этих действий потребуется идентификатор объекта группы безопасности FortiGateAccess, созданной ранее при прохождении руководства.

1. Установите сеанс SSH для приложения FortiGate и выполните вход с помощью учетной записи администратора FortiGate.
1. Выполните следующие команды:

   ```
    config user group
    edit FortiGateAccess
    set member azure
    config match
    edit 1
    set server-name azure
    set group-name <Object Id>
    next
    end
    next
    end
   ```

#### <a name="create-a-fortigate-vpn-portals-and-firewall-policy"></a>Создание VPN-порталов и политики брандмауэра FortiGate

В этом разделе вы настроите VPN-порталы и политики брандмауэра FortiGate, предоставляющие доступ к группе безопасности FortiGateAccess, созданной ранее при прохождении руководства.

Обратитесь к [группе поддержки FortiGate](mailto:tac_amer@fortinet.com), чтобы добавить VPN-порталы и политику брандмауэра на VPN-платформу FortiGate. Перед использованием единого входа выполните этот шаг.

### <a name="test-single-sign-on"></a>Проверка единого входа 

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью Панели доступа.

Выбрав плитку SSL VPN FortiGate на Панели доступа, вы автоматически войдете в приложение SSL VPN FortiGate, для которого настроили единый вход. Дополнительные сведения о панели доступа см. в [этой статье](../user-help/my-apps-portal-end-user-access.md).

Чтобы обеспечить лучшее взаимодействие с пользователем, корпорация Майкрософт и FortiGate рекомендуют использовать VPN-клиент Fortinet и FortiClient.

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Учебники по интеграции приложений SaaS с Azure Active Directory](./tutorial-list.md).

- [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

- [Что представляет собой условный доступ в Azure Active Directory?](../conditional-access/overview.md)

- [Попробуйте использовать VPN SSL FortiGate с Azure AD](https://aad.portal.azure.com/)

- [Что такое управление сеансами в Microsoft Cloud App Security?](/cloud-app-security/proxy-intro-aad)