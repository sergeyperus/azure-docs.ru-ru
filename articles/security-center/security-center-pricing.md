---
title: Цены на Центр безопасности Azure
description: 'Центр безопасности Azure предлагается в двух режимах: с Azure Defender и без него.'
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/22/2020
ms.author: memildin
ms.openlocfilehash: bc17b63ef8f83e4086262d52334a518ec85f4fc6
ms.sourcegitcommit: 6a770fc07237f02bea8cc463f3d8cc5c246d7c65
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95792599"
---
# <a name="pricing-of-azure-security-center"></a>Цены на Центр безопасности Azure
Центр безопасности Azure предоставляет возможности унифицированного управления безопасностью и расширенной защиты от угроз для рабочих нагрузок в Azure, в локальной среде и в других облаках. Он повышает вашу информированность о гибридных облачных рабочих нагрузках, обеспечивает управление ими, а также предоставляет активные средства защиты, снижающие уровень риска угроз, и интеллектуальные средства обнаружения, которые позволяют быть в курсе быстро развивающихся рисков для кибербезопасности.


## <a name="free-option-vs-azure-defender-enabled"></a>Сравнение вариантов: "Бесплатный" и с Azure Defender

Центр безопасности предлагается в следующих двух режимах:

- **БЕЗ Azure Defender** (Бесплатный). Центр безопасности без Azure Defender бесплатно подключается для всех подписок Azure, когда вы впервые открываете панель мониторинга Центра безопасности Azure на портале Azure или включаете Центр безопасности программным способом через API. В уровне "Бесплатный" предоставляются политики безопасности, непрерывная оценка безопасности и практические рекомендации по безопасности для защиты ресурсов Azure.

- **С Azure Defender.** Включение Azure Defender расширяет возможности уровня "Бесплатный", добавляя выполнение рабочих нагрузок в частных и других общедоступных облаках, объединенное управление безопасностью и защиту от угроз в гибридных облачных рабочих нагрузках. Вот некоторые основные функции Azure Defender:

    - **Microsoft Defender для конечных точек**. Azure Defender для серверов содержит компонент [Microsoft Defender для конечной точки](https://www.microsoft.com/microsoft-365/security/endpoint-defender), позволяющий обеспечить широкие возможности обнаружения и нейтрализации атак на конечные точки (EDR). Дополнительные сведения о преимуществах использования Microsoft Defender для конечных точек вместе с Azure Defender см. в статье об [использовании интегрированного решения EDR Центра безопасности](security-center-wdatp.md).
    - **Сканирование уязвимостей для виртуальных машин и реестров контейнеров.** Средство сканирования очень легко развернуть на всех виртуальных машинах для доступа к самому развитому в отрасли решению для управления уязвимостями. Просматривайте, изучайте результаты и применяйте исправления непосредственно в Центре безопасности. 
    - **Гибридная защита.** Получите комплексный обзор безопасности всех локальных и облачных рабочих нагрузок. Применяйте политики безопасности и непрерывно проверяйте уровень безопасности гибридных облачных рабочих нагрузок, чтобы обеспечить соответствие стандартам безопасности. Выполняйте сбор, поиск и анализ данных о безопасности из нескольких источников, включая брандмауэры и другие партнерские решения.
    - **Оповещения о защите от угроз.** Расширенная аналитика поведения и Microsoft Intelligent Security Graph позволят противодействовать постоянно совершенствующимся кибератакам. Встроенные возможности анализа поведения и машинное обучение позволяют определять атаки и уязвимости нулевого дня. Обнаруживайте входящие атаки и отслеживайте дальнейшую работу систем за счет мониторинга сетей, компьютеров и облачных служб. Ускорьте анализ с помощью интерактивных инструментов и контекстной аналитики угроз.
    - **Элементы управления доступом и приложениями (AAC).** Блокируйте вредоносные и другие нежелательные приложения, создавая списки разрешений и запретов на основе рекомендаций машинного обучения, адаптированных к конкретным рабочим нагрузкам. Сократите направления атак на сеть с помощью управляемого JIT-доступа к портам управления на виртуальных машинах Azure. Элементы AAC значительно снижают уязвимость к сетевым атакам, особенно методом перебора.
    - **Функции безопасности контейнеров.** Воспользуйтесь возможностями управления уязвимостями и защиты от угроз в реальном времени в контейнерных средах. После включения **Azure Defender для реестра контейнеров** может пройти до 12 ч, пока активируются все его компоненты. Размер платы зависит от количества уникальных образов контейнеров, отправленных в подключенный реестр. Каждый образ сканируется один раз, и далее плата не взимается до следующего цикла изменения и отправки. 

## <a name="try-azure-defender-free-for-30-days"></a>Бесплатное использование Azure Defender в течение 30 дней
Azure Defender предоставляется бесплатно в течение 30 дней с начала использования. Если по истечении 30 дней вы продолжаете использовать службу, мы автоматически начнем начислять плату за использование.

## <a name="enable-azure-defender"></a>Включение Azure Defender
С помощью Azure Defender вы можете защитить всю подписку Azure, и эта защита будет наследоваться всеми ресурсами в подписке.

Чтобы включить Azure Defender:

1. В главном меню Центра безопасности выберите **Цены и параметры**.
1. Выберите подписку, которую вы хотите изменить.
1. Выберите **Включить Azure Defender**.
1. Щелкните **Сохранить**.

Ниже приведена страница с примером цен на подписку. Здесь вы видите, что каждый план в Azure Defender оплачивается отдельно и может быть включен или отключен отдельно.

:::image type="content" source="./media/security-center-pricing/pricing-tier-page.png" alt-text="Страница цен Центра безопасности на портале":::

> [!NOTE]
> Чтобы реализовать все возможности Центра безопасности, включая защиту от угроз, необходимо включить Azure Defender для подписки, которая содержит соответствующие рабочие нагрузки. Включение на уровне рабочей области не включает JIT-доступ к виртуальной машине, адаптивные элементы управления приложениями и возможности сетевого обнаружения для ресурсов Azure. Кроме того, единственные планы Azure Defender, доступные на уровне рабочей области, — это Azure Defender для серверов и Azure Defender для экземпляров SQL Server на компьютерах.
>
> Вы можете включить **Azure Defender для учетных записей хранения** на уровне подписки или ресурсов.
> Вы можете включить **Azure Defender для SQL** на уровне подписки или ресурсов.
> Для **Базы данных Azure для MariaDB, MySQL и PostgreSQL** защиту от угроз можно включить только на уровне ресурсов.


## <a name="faq---pricing-and-billing"></a>Вопросы и ответы: цены и выставление счетов 

### <a name="how-can-i-track-who-in-my-organization-enabled-azure-defender-changes-in-azure-security-center"></a>Как узнать, кто из сотрудников моей организации включил изменения Azure Defender в Центре безопасности Azure?
В подписках Azure может быть несколько администраторов с разрешениями на изменение параметров цен. Чтобы узнать, какой именно пользователь внес изменения, используйте журнал действий Azure.

Если сведения о пользователе не указаны в столбце **Кем инициировано событие**, ознакомьтесь с соответствующим подробным описанием события.

:::image type="content" source="media/security-center-pricing/logged-change-to-pricing.png" alt-text="Журнал событий Azure со сведениями о событии изменения цен":::


### <a name="what-are-the-plans-offered-by-security-center"></a>Какие планы предлагаются в Центре безопасности? 
В Центре безопасности есть два предложения: 

- Центр безопасности Azure (бесплатный) 
- Azure Defender  

### <a name="how-do-i-enable-azure-defender-for-my-subscription"></a>Как включить Azure Defender для моей подписки? 
Включить Azure Defender для подписки можно любым из приведенных ниже способов. 

|Метод  |Инструкции  |
|---------|---------|
|Страницы Центра безопасности Azure на портале Azure|[Включение Azure Defender](#enable-azure-defender)|
|REST API|[API цен](https://docs.microsoft.com/rest/api/securitycenter/pricings)|
|Azure CLI|[az security pricing](https://docs.microsoft.com/cli/azure/security/pricing)|
|PowerShell|[Set-AzSecurityPricing](https://docs.microsoft.com/powershell/module/az.security/set-azsecuritypricing)|
|Политика Azure|[Цены на пакеты](https://github.com/Azure/Azure-Security-Center/tree/master/Pricing%20%26%20Settings/Azure%20Policy%20definitions/Bundle%20Pricings)|
|||

### <a name="can-i-enable-azure-defender-for-servers-on-a-subset-of-servers-in-my-subscription"></a>Можно ли включить Azure Defender для серверов из подмножества серверов в моей подписке?
Нет. Если в подписке включено средство [Azure Defender для серверов](defender-for-servers-introduction.md), оно будет защищать все относящиеся к ней серверы. 

Альтернативный вариант — включить Azure Defender для серверов на уровне рабочей области Log Analytics. В этом случае защита и выставление счетов будет осуществляться только для серверов, отправляющих отчеты в эту рабочую область. Но некоторые возможности будут недоступны. К ним относятся JIT-доступ к виртуальным машинам, обнаружение сетей, обеспечение соответствия нормативным требованиям, адаптивное усиление защиты сети, адаптивные элементы управления приложениями и другое. 


### <a name="my-subscription-has-azure-defender-for-servers-enabled-do-i-pay-for-not-running-servers"></a>В моей подписке включено средство "Azure Defender для серверов". Будет ли взиматься плата за незапущенные серверы? 
Нет. Если вы включите в подписке [Azure Defender для серверов](defender-for-servers-introduction.md), счета будут выставляться за каждый час только для работающих серверов. С вас не будет взиматься плата за все отключенные серверы в то время, когда они не работают. 

> [!TIP]
> Это относится и к другим типам ресурсов, защищенным Центром безопасности. 

### <a name="will-i-be-charged-for-machines-without-the-log-analytics-agent-installed"></a>Будет ли взиматься плата за компьютеры без установленного агента Log Analytics?
Да. Если вы включите в подписке [Azure Defender для серверов](defender-for-servers-introduction.md), компьютеры в ней получают ряд средств защиты, даже если агент Log Analytics не установлен.

### <a name="if-a-log-analytics-agent-reports-to-multiple-workspaces-will-i-be-charged-twice"></a>Если агент Log Analytics отправляет отчеты в несколько рабочих областей, будет ли плата взиматься дважды? 
Да. Если вы настроили агент Log Analytics для отправки данных в две или более рабочих областей Log Analytics (многоадресная рассылка), вам будет выставляться счет за каждую рабочую область, в которой установлены решения с отметкой "Безопасность" или "Антивредоносная программа". 

### <a name="if-a-log-analytics-agent-reports-to-multiple-workspaces-is-the-500-mb-free-data-ingestion-available-on-all-of-them"></a>Если агент Log Analytics отправляет отчеты в несколько рабочих областей, распространяется ли возможность бесплатного приема данных объемом 500 МБ на все рабочие области?
Да. Если вы настроили агент Log Analytics для отправки данных в две или более рабочих областей Log Analytics (многоадресная рассылка), вы получите возможность бесплатного приема данных объемом 500 МБ. Расчет выполняется для каждого узла и каждой рабочей области в день. Возможность предоставляется для каждой рабочей области, в которой установлены решения с отметкой "Безопасность" или "Антивредоносная программа". За любые принятые данные свыше 500 МБ с вас будет взиматься плата.


## <a name="next-steps"></a>Дальнейшие действия
В этой статье описаны варианты цен в Центре безопасности. Дополнительные материалы:

- [Как оптимизировать расходы на рабочую нагрузку в Azure](https://azure.microsoft.com/blog/how-to-optimize-your-azure-workload-costs/)
- [Цены на Центр безопасности для определенной валюты и региона](https://azure.microsoft.com/pricing/details/security-center/)
- Вам может потребоваться выполнить управление затратами и ограничить объем данных, собираемых для решения, ограничив его конкретным набором агентов. [Нацеливание решений](../azure-monitor/insights/solution-targeting.md) позволяет применять область к решениям и выполнять нацеливание подмножества компьютеров в рабочей области. Если используется нацеливание решений, рабочая область в Центре безопасности отображается как область без решения.