---
title: Удаление организации Azure AD (клиента) — Azure Active Directory | Документация Microsoft
description: Объясняется, как подготовить организацию Azure AD (клиента) для удаления, включая организации самообслуживания.
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 11/15/2020
ms.author: curtand
ms.reviewer: addimitu
ms.custom: it-pro
ms.collection: M365-identity-device-management
ms.openlocfilehash: be40a3cea5aa7abfa257c4e5a2db61c514892dd5
ms.sourcegitcommit: b8eba4e733ace4eb6d33cc2c59456f550218b234
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/23/2020
ms.locfileid: "95503631"
---
# <a name="delete-a-tenant-in-azure-active-directory"></a>Удаление клиента в Azure Active Directory

При удалении организации Azure AD (клиента) также удаляются все ресурсы, содержащиеся в этой организации. Необходимо подготовить организацию, сведя к минимуму связанные ресурсы, прежде чем выполнять удаление. Только глобальный администратор Azure Active Directory (Azure AD) может удалить организацию Azure AD с портала.

## <a name="prepare-the-organization"></a>Подготовка организации

Вы не можете удалить организацию в Azure AD, пока она не пройдет несколько проверок. Эти проверки снижают риск того, что удаление Организации Azure AD негативно влияет на доступ пользователей, например на возможность входа в Microsoft 365 или доступ к ресурсам в Azure. Например, если организация, связанная с подпиской, будет случайно удалена, пользователи не смогут получить доступ к ресурсам Azure для этой подписки. Проверяются следующие условия.

* В организации Azure AD (клиенте) не должно быть пользователей, за исключением одного глобального администратора, который должен удалить организацию. Всех других пользователей следует удалить перед удалением организации. Если данные пользователей синхронизируются из локальной среды, синхронизацию необходимо отключить, а пользователей сначала удалить из облачной организации с помощью портала Azure или командлетов Azure PowerShell.
* В организации не должно быть ни одного приложения. Все приложения должны быть удалены перед удалением организации.
* С организацией не могут быть связаны поставщики многофакторной проверки подлинности.
* Для таких служб Microsoft Online Services, как Microsoft Azure, Microsoft 365 или Azure AD Premium, связанных с Организацией, не может быть ни одной подписки. Например, если организация Azure AD по умолчанию создана в Azure, ее невозможно удалить, если ваша подписка Azure по-прежнему использует ее для проверки подлинности. Точно так же нельзя удалить организацию, если у другого пользователя есть связанная с ней подписка.

## <a name="delete-the-organization"></a>Удаление организации

1. Войдите в [центр администрирования Azure AD](https://aad.portal.azure.com) с помощью учетной записи глобального администратора организации.

2. Выберите **Azure Active Directory**.

3. Переключитесь на организацию, которую нужно удалить.
  
   ![Подтверждение организации перед удалением](./media/directory-delete-howto/delete-directory-command.png)

4. Выберите **Удалить клиент**.
  
   ![выберите команду для удаления организации](./media/directory-delete-howto/delete-directory-list.png)

5. Если организация не проходит одну или несколько проверок, вы получите ссылку с дополнительной информацией о том, как пройти проверки. Когда клиент пройдет все проверки, нажмите **Удалить** для завершения процесса.

## <a name="if-you-cant-delete-the-organization"></a>Невозможно удалить организацию

При настройке организации Azure AD вы также могли активировать подписки на основе лицензий для вашей организации, например Azure AD Premium P2, Microsoft 365 бизнес Standard или Enterprise Mobility + Security. Во избежание случайной потери данных невозможно удалить организацию до тех пор, пока не будут полностью удалены подписки. Подписки должны находиться в состоянии **Отозвано**, чтобы можно было удалить организацию. Подписка в состоянии **Просрочено** или **Отменено** перемещается в состояние **Отключено**, а затем — **Отозвано**.

Если срок действия пробной подписки Microsoft 365 истекает (не включая платного партнера/CSP, Соглашение Enterprise или корпоративного лицензирования), см. следующую таблицу. Дополнительные сведения о Microsoft 365 сроках хранения данных и подписки см. в статье [что происходит с моими данными и доступ к ним при завершении подписки Microsoft 365 для бизнеса?](https://support.office.com/article/what-happens-to-my-data-and-access-when-my-office-365-for-business-subscription-ends-4436582f-211a-45ec-b72e-33647f97d8a3). 

Состояние подписки | Данные | Доступ к данным
----- | ----- | -----
Активно (пробная версия — 30 дней) | Данные доступны для всех | Пользователи имеют стандартный доступ к файлам Microsoft 365 или приложениям<br>Администраторы имеют обычный доступ к центру администрирования и ресурсам Microsoft 365 
Просрочено (30 дней) | Данные доступны для всех| Пользователи имеют стандартный доступ к файлам Microsoft 365 или приложениям<br>Администраторы имеют обычный доступ к центру администрирования и ресурсам Microsoft 365
Отключено (30 дней) | Данные доступны только для администратора | Пользователи не могут получить доступ к файлам Microsoft 365 или приложениям<br>Администраторы имеют доступ к центру администрирования Microsoft 365, но не могут назначать лицензии или обновлять пользователей
Отозвано (через 30 дней после отключения) | Данные удаляются (автоматически, если другие службы не используются) | Пользователи не могут получить доступ к файлам Microsoft 365 или приложениям<br>Администраторы имеют доступ к центру администрирования Microsoft 365 для покупки и управления другими подписками

## <a name="delete-a-subscription"></a>Удаление подписки

Вы можете поместить подписку в состояние **Отозвано**, чтобы удалить ее через три дня с помощью центра администрирования Microsoft 365.

1. Войдите в [центр администрирования Microsoft 365](https://admin.microsoft.com) с помощью учетной записи глобального администратора организации. Если вы пытаетесь удалить организацию Contoso с начальным доменом по умолчанию contoso.onmicrosoft.com, войдите с именем участника-пользователя, например admin@contoso.onmicrosoft.com.

2. Для использования предварительной версии нового центра администрирования Microsoft 365 нужно убедиться, что включен переключатель **Опробовать новый центр администрирования**.

   ![Использование предварительной версии нового центра администрирования M365](./media/directory-delete-howto/preview-toggle.png)

3. После включения нового центра администрирования необходимо отменить подписку. Только после этого ее можно будет удалить. Выберите **Выставление счетов** и **Продукты и услуги**, а затем — **Отменить подписку** напротив отменяемой подписки. Откроется страница обратной связи.

   ![Выберите подписку, которую требуется отменить.](./media/directory-delete-howto/cancel-choose-subscription.png)

4. Заполните форму обратной связи и выберите **Отменить подписку**, чтобы отменить подписку.

   ![Команда «Отмена» в предварительной версии подписки](./media/directory-delete-howto/cancel-command.png)

5. Теперь подписку можно удалить. Выберите **Удалить** напротив удаляемой подписки. Если вы не можете найти подписку на странице **Продукты и услуги**, убедитесь, что для параметра **Состояние подписки** задано значение **Все**.

   ![Удаление связи для удаления подписки](./media/directory-delete-howto/delete-command.png)

6. Нажмите **Удалить подписку**, чтобы удалить подписку и принять условия и положения. Все данные будут безвозвратно удалены в течение трех дней. Если вы передумаете, вы можете [повторно активировать подписку](/office365/admin/subscriptions-and-billing/reactivate-your-subscription?view=o365-worldwide) в течение трех дней.
  
   ![Внимательно прочитайте условия и положения.](./media/directory-delete-howto/delete-terms.png)

7. Теперь состояние подписки изменилось, подписка помечена для удаления. Подписка входит в состояние **Отозвано** через 72 часа.

8. После удаления подписки в организации и по истечении 72 часов вы можете снова войти в центр администрирования Azure AD. Теперь от вас не требуется никаких действий, и никакие подписки не должны мешать удалению организации. Вы можете успешно удалить организацию Azure AD.
  
   ![пройденная проверка подписки на экране удаления](./media/directory-delete-howto/delete-checks-passed.png)

## <a name="i-have-a-trial-subscription-that-blocks-deletion"></a>У меня есть пробная подписка, которая блокирует удаление

Существуют такие [продукты самостоятельной регистрации](/office365/admin/misc/self-service-sign-up?view=o365-worldwide) , как Microsoft Power BI, Rights Management Services, Microsoft Power Apps или Dynamics 365, отдельные пользователи могут зарегистрироваться через Microsoft 365, что также создает гостевого пользователя для проверки подлинности в Организации Azure AD. Эти продукты самообслуживания блокируют удаление каталогов, пока продукты не будут полностью удалены из организации, чтобы избежать потери данных. Удалить их может только администратор Azure независимо от того, зарегистрировался ли пользователь самостоятельно или продукт был ему назначен.

Существует два типа продуктов с самостоятельной регистрацией. Они различаются в зависимости от типа назначения. 

* Назначение на уровне организации. Администратор Azure AD назначает продукт всей организации, и пользователь может активно использовать службу с назначением на уровне организации, даже если не имеет индивидуальной лицензии.
* Назначение на уровне пользователя. Пользователь в процессе самостоятельной регистрации назначает себе продукт сам, без администратора. Как только организация перейдет в управление администратора (см. раздел [Переход неуправляемой организации под управление администратора](domains-admin-takeover.md)), он может назначать продукт пользователям напрямую, минуя процедуру самостоятельной регистрации.  

Когда вы начинаете удалять продукт с самостоятельной регистрацией, это действие безвозвратно удаляет данные и доступ пользователей к службе. Любой пользователь, которому предложение было назначено индивидуально или на уровне организации, после этого не сможет войти в систему или получить доступ к существующим данным. Во избежание потери данных при работе с продуктами с самостоятельной регистрацией, такими как [панели мониторинга Microsoft Power BI](/power-bi/service-export-to-pbix) или [конфигурация политик для служб управления правами](/azure/information-protection/configure-policy#how-to-configure-the-azure-information-protection-policy), убедитесь, что выполняется резервное копирование данных и они сохраняются в другом расположении.

Дополнительные сведения о доступных в настоящее время продуктах и службах с самостоятельной регистрацией доступны в разделе [Доступные программы самообслуживания](/office365/admin/misc/self-service-sign-up?view=o365-worldwide#available-self-service-programs).

Если срок действия пробной подписки Microsoft 365 истекает (не включая платного партнера/CSP, Соглашение Enterprise или корпоративного лицензирования), см. следующую таблицу. Дополнительные сведения о Microsoft 365 сроках хранения данных и подписки см. в статье [что происходит с моими данными и доступ к ним при завершении подписки Microsoft 365 для бизнеса?](/office365/admin/subscriptions-and-billing/what-if-my-subscription-expires?view=o365-worldwide).

Состояние продукта | Данные | Доступ к данным
------------- | ---- | --------------
Активно (пробная версия — 30 дней) | Данные доступны для всех | Пользователи осуществляют стандартный доступ к продуктам, файлам или приложениям с самостоятельной регистрацией<br>Администраторы имеют обычный доступ к центру администрирования и ресурсам Microsoft 365
Deleted | Данные удалены | Пользователи не могут осуществлять доступ к продуктам, файлам или приложениям с самостоятельной регистрацией<br>Администраторы имеют доступ к центру администрирования Microsoft 365 для покупки и управления другими подписками

## <a name="how-can-i-delete-a-self-service-sign-up-product-in-the-azure-portal"></a>Как удалить продукт с самостоятельной регистрацией на портале Azure?

Можно перевести продукт с самостоятельной регистрацией, такой как Microsoft Power BI или службы управления правами Azure, в состояние **Удалено**, после чего они будут немедленно удалены с портала Azure AD.

1. Войдите в [центр администрирования Azure](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) с учетной записью глобального администратора в организации. Если вы пытаетесь удалить организацию Contoso с начальным доменом по умолчанию contoso.onmicrosoft.com, войдите с именем участника-пользователя, например admin@contoso.onmicrosoft.com.

2. Выберите **Лицензии**, а затем **Продукты с самостоятельной регистрацией**. В подписках на рабочее место можно просмотреть все продукты с самостоятельной регистрацией по отдельности. Выберите продукт для удаления без возможности восстановления. Ниже приведен пример в Microsoft Power BI.

    ![Снимок экрана, на котором показана страница "лицензии — самостоятельная регистрация продуктов".](./media/directory-delete-howto/licenses-page.png)

3. Выберите **Удалить**, чтобы удалить продукт и принять условие о том, что данные удаляются немедленно и безвозвратно. Это действие удаления приведет к удалению всех пользователей и удалению доступа организации к продукту. Нажмите кнопку «Да», чтобы продолжить процедуру удаления.  

    ![Снимок экрана, на котором показана страница "лицензии — самостоятельная регистрация продуктов" с открытым окном "Удаление самостоятельной регистрации продукта".](./media/directory-delete-howto/delete-product.png)

4. Если вы выберете **Да**, запустится процесс удаления продукта с самостоятельной регистрацией. Отобразится уведомление о том, что выполняется удаление.  

    ![Снимок экрана, на котором показана страница "лицензии — самостоятельная регистрация продуктов" с отображением уведомления "выполняется удаление".](./media/directory-delete-howto/progress-message.png)

5. Теперь состояние продукта с самостоятельной регистрацией изменилось на **Удалено**. При обновлении страницы продукт необходимо удалить со страницы **Продукты с самостоятельной регистрацией**.  

    ![Снимок экрана, на котором показана страница «лицензии — самостоятельная регистрация продуктов» с областью «самостоятельное удаление продукта для регистрации» на правой стороне.](./media/directory-delete-howto/product-deleted.png)

6. После удаления всех продуктов можно снова зайти в центр администрирования Azure AD. Там не должно отображаться никаких требуемых действий и никаких продуктов, препятствующих удалению организации. Вы можете успешно удалить организацию Azure AD.

    ![имя пользователя введено неправильно или не найдено](./media/directory-delete-howto/delete-organization.png)

## <a name="next-steps"></a>Дальнейшие действия

[Документация Azure Active Directory](../index.yml)