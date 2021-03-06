---
title: Устойчивость сборки с помощью оценки непрерывного доступа в Azure Active Directory
description: Рекомендации для архитекторов и ИТ-администраторов по использованию автоматизированного конструирования
services: active-directory
author: BarbaraSelden
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.subservice: fundamentals
ms.topic: conceptual
ms.date: 11/30/2020
ms.author: baselden
ms.reviewer: ajburnle
ms.custom: it-pro, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8ad36c2a7f47948d9362b85e78355e6046cda703
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "95919868"
---
# <a name="build-resilience-by-using-continuous-access-evaluation"></a>Устойчивость сборки с помощью оценки непрерывного доступа

[Оценка непрерывного доступа](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-continuous-access-evaluation) (автоматизированного конструирования) позволяет ПРИЛОЖЕНИЯМ Azure AD подписываться на критические события, которые затем могут быть оценены и применены. Это включает оценку следующих событий:

* Удаляемая или отключенная учетная запись пользователя

* Пароль пользователя изменен

* MFA включен для пользователя.

* Администратор явно отзывает маркер.

* Обнаружен риск с повышенными правами пользователя.

В результате приложения могут отклонять маркеры с неистекшим сроком действия на основе событий, сигнальных с помощью Azure AD, как показано на следующей схеме.

![концептуалиаграм автоматизированного конструирования](./media/resilience-with-cae/admin-resilience-continuous-access-evaluation.png)

## <a name="how-does-cae-help"></a>Как автоматизированного конструирования справку?

Этот механизм позволяет Azure AD выдавать более длинные токены, в то же время позволяя приложениям отменять доступ и принудительно выполнять повторную проверку подлинности только при необходимости. Результатом этого шаблона является меньше вызовов для получения маркеров, что означает, что сквозной поток более устойчив. 

Чтобы использовать автоматизированного конструирования, служба и клиент должны поддерживать автоматизированного конструирования. Службы Microsoft 365, такие как Exchange Online, Teams и SharePoint Online, поддерживают автоматизированного конструирования. На стороне клиента веб-интерфейс, использующий эти службы Office 365 (например, Outlook Web App) и определенные версии Office 365 Native Clients, поддерживают автоматизированного конструирования. Другие облачные службы Майкрософт станут автоматизированного конструирования.

Корпорация Майкрософт работает с отраслевыми стандартами для создания [стандартов](https://openid.net/wg/sse/) , которые позволяют сторонним приложениям использовать эту возможность. Вы также можете разрабатывать приложения, поддерживающие автоматизированного конструирования. Дополнительные сведения см. в разделе Создание устойчивости в приложении.

## <a name="how-do-i-implement-cae"></a>Разделы справки реализовать автоматизированного конструирования?

* [Включите автоматизированного конструирования](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-continuous-access-evaluation) в конфигурации безопасности Azure AD.

* Убедитесь, что ваша организация использует [совместимые версии](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-continuous-access-evaluation) Microsoft Office собственных приложений.

* [Оптимизируйте запросы повторной проверки подлинности](https://docs.microsoft.com/azure/active-directory/authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime).

 
## <a name="next-steps"></a>Дальнейшие действия
Ресурсы по устойчивости для администраторов и архитекторов
 
* [Устойчивость к сборке с помощью управления учетными данными](resilience-in-credentials.md)

* [Устойчивость сборки к состояниям устройств](resilience-with-device-states.md)

* [Устойчивость к сборке при аутентификации внешних пользователей](resilience-b2b-authentication.md)

* [Устойчивость к сборке в гибридной проверке подлинности](resilience-in-hybrid.md)

* [Устойчивость к сборке в доступе к приложениям с помощью прокси приложения](resilience-on-premises-access.md)

Обеспечение устойчивости ресурсов для разработчиков

* [Создание устойчивости IAM в приложениях](resilience-app-development-overview.md)

* [Устойчивость сборок в CIAM Systems](resilience-b2c.md)
