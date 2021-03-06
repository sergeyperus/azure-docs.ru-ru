---
title: Подключение данных аналитики угроз к Azure Sentinel | Документация Майкрософт
description: Узнайте, как подключить данные аналитики угроз к Azure Sentinel.
documentationcenter: na
author: yelevin
manager: rkarlin
editor: ''
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.devlang: na
ms.topic: how-to
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/22/2019
ms.author: yelevin
ms.openlocfilehash: 205cc6eea5d1ac3be2d0e266621067dc8e20d2f9
ms.sourcegitcommit: b8a175b6391cddd5a2c92575c311cc3e8c820018
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "96121743"
---
# <a name="connect-data-from-threat-intelligence-providers"></a>Подключение данных из поставщиков аналитики угроз

> [!IMPORTANT]
> Соединители данных аналитики угроз в Azure Sentinel в настоящее время доступны в общедоступной предварительной версии.
> Эта функция предоставляется без соглашения об уровне обслуживания и не рекомендуется для рабочих нагрузок. Некоторые функции могут не поддерживаться или их возможности могут быть ограничены. Дополнительные сведения см. в статье [Дополнительные условия использования предварительных выпусков Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Azure Sentinel позволяет импортировать индикаторы угроз, используемые вашей организацией, что может улучшить возможности аналитики безопасности по обнаружению и приоритизации известных угроз. После этого становятся доступными или расширены несколько функций из Azure Sentinel:

- **Аналитика** включает набор шаблонов запланированных правил, которые можно включить для создания предупреждений и инцидентов на основе совпадений событий журнала из индикаторов угроз.

- **Книги** содержат сводные сведения о индикаторах угроз, импортированных в Azure Sentinel, и обо всех предупреждениях, созданных правилами аналитики, которые соответствуют индикаторам угроз.

- **Запросы на** Поиск позволяют использовать индикаторы угроз в контексте распространенных сценариев обнаружения.

- При исследовании аномалий и поиске вредоносных программ в **записных книжках** могут использоваться индикаторы угроз.

Вы можете передавать индикаторы угроз в Azure Sentinel с помощью одной из интегрированных продуктов для аналитики угроз (TIP), перечисленных в следующем разделе, подключении к серверам ТАКСИИ или с помощью прямой интеграции с [API Microsoft Graph Security тииндикаторс](/graph/api/resources/tiindicator).

## <a name="integrated-threat-intelligence-platform-products"></a>Интегрированные продукты платформы аналитики угроз

- [Платформа аналитики угроз с открытым исходным кодом МИСП](https://www.misp-project.org/)
    
    Пример скрипта, который предоставляет клиенты с экземплярами МИСП для переноса индикаторов угроз в API безопасности Microsoft Graph, см. в разделе [МИСП to Microsoft Graph Script Security](https://github.com/microsoftgraph/security-api-solutions/tree/master/Samples/MISP).

- [Аномали Среатстреам](https://www.anomali.com/products/threatstream)

    Чтобы скачать Среатстреам Integrator и Extensions, а также инструкции по подключению аналитики Среатстреам к API Microsoft Graph безопасности, см. страницу [загрузки среатстреам](https://ui.threatstream.com/downloads) .

- [Palo Alto Networks Минемелд](https://www.paloaltonetworks.com/products/secure-the-network/subscriptions/minemeld)
    
    Пошаговые инструкции см. [в статье отправка иокс в API безопасности Microsoft Graph с помощью минемелд](https://live.paloaltonetworks.com/t5/MineMeld-Articles/Sending-IOCs-to-the-Microsoft-Graph-Security-API-using-MineMeld/ta-p/258540).

- [Платформа Среатконнект](https://threatconnect.com/solution/)

    Дополнительные сведения см. в статье [Интеграция среатконнект](https://threatconnect.com/integrations/) и поиск Microsoft Graph API безопасности на странице.

- [Платформа ЕклектиЦик](https://www.eclecticiq.com/solutions)

- [Платформа аналитики угроз Среатк](https://www.threatq.com/)

    Сведения и инструкции см. в статье [Microsoft Sentinel Connector для интеграции с среатк](https://appsource.microsoft.com/product/web-apps/threatquotientinc1595345895602.microsoft-sentinel-connector-threatq?src=health&tab=Overview).

## <a name="connect-azure-sentinel-to-your-threat-intelligence-platform"></a>Подключение Sentinel Azure к платформе аналитики угроз

### <a name="prerequisites"></a>Предварительные требования  

- Роль Azure AD глобального администратора или администратора безопасности, чтобы предоставить разрешения для вашего продукта TIP или пользовательского приложения, использующего прямую интеграцию с API Microsoft Graph Security Тииндикаторс.

- Разрешения на чтение и запись в рабочей области Sentinel Azure для хранения индикаторов угроз.

### <a name="instructions"></a>Инструкции

1. [Зарегистрируйте приложение](/graph/auth-v2-service#1-register-your-app) в Azure Active Directory, чтобы получить идентификатор приложения, секрет приложения и идентификатор клиента Azure Active Directory. Эти значения понадобятся при настройке интегрированного продукта или приложения TIP, использующего прямую интеграцию с Microsoft Graph API Тииндикаторс безопасности.

2. [Настройка разрешений API](/graph/auth-v2-service#2-configure-permissions-for-microsoft-graph) для зарегистрированного приложения. добавьте разрешение Microsoft Graph приложения **среатиндикаторс. ReadWrite. овнедби** в зарегистрированное приложение.

3. Попросите администратора Azure Active Directory клиента предоставить согласие администратора зарегистрированному приложению для вашей организации. Из портал Azure: **Azure Active Directory**  >  **Регистрация приложений**  >  **\<_app name_>**  >  **разрешения**  >  **на доступ к \<_tenant name_> API предоставляют администратору** разрешение.

4. Настройте продукт или приложение TIP, которое использует прямую интеграцию с API Microsoft Graph Security Тииндикаторс для отправки индикаторов в Azure Sentinel, указав следующие параметры:
    
    а. Значения идентификатора зарегистрированного приложения, секрета и идентификатора клиента.
    
    b. Для целевого продукта укажите Sentinel Azure.
    
    c. Для действия укажите предупреждение.

5. В портал Azure перейдите к **Azure Sentinel**  >  **соединителям данных** Azure Sentinel и выберите соединитель платформы для **анализа угроз (Предварительная версия)** .

6. Выберите **открыть страницу соединителя** и **подключитесь**.

7. Чтобы просмотреть индикаторы угроз, импортированные в Azure Sentinel, перейдите в раздел **Azure Sentinel-Logs**  >  **секуритинсигхтс**, а затем разверните узел **среатинтеллиженцеиндикатор**.

## <a name="connect-azure-sentinel-to-taxii-servers"></a>Подключение Sentinel Azure к серверам ТАКСИИ

### <a name="prerequisites"></a>Предварительные требования

- Разрешения на чтение и запись в рабочей области Sentinel Azure для хранения индикаторов угроз.

- URI сервера ТАКСИИ 2,0 и идентификатор коллекции.

### <a name="instructions"></a>Инструкции

1. В портал Azure перейдите к **Azure Sentinel**  >  **соединителям данных** Sentinel Azure и выберите соединитель " **аналитика угроз — таксии (Предварительная версия)** ".

2. Выберите **открыть страницу соединителя**.

3. Укажите обязательные и необязательные сведения в текстовых полях.

4. Выберите **Добавить** , чтобы разрешить подключение к серверу таксии 2,0.

5. Если у вас есть дополнительные серверы ТАКСИИ 2,0: Повторите шаги 3 и 4.

6. Чтобы просмотреть индикаторы угроз, импортированные в Azure Sentinel, перейдите в раздел **Azure Sentinel-Logs**  >  **секуритинсигхтс**, а затем разверните узел **среатинтеллиженцеиндикатор**.

## <a name="next-steps"></a>Дальнейшие действия

В этом документе вы узнали, как подключить поставщик аналитики угроз к Azure Sentinel. Дополнительные сведения об Azure Sentinel см. в следующих статьях.

- Узнайте, как [отслеживать свои данные и потенциальные угрозы](quickstart-get-visibility.md).
- Узнайте, как приступить к [обнаружению угроз с помощью Azure Sentinel](./tutorial-detect-threats-built-in.md).