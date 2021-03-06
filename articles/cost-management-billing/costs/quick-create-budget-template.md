---
title: Краткое руководство. Создание бюджета с помощью шаблона Azure Resource Manager
description: Краткое руководство по созданию бюджета с помощью шаблона Azure Resource Manager.
author: bandersmsft
ms.author: banders
tags: azure-resource-manager
ms.service: cost-management-billing
ms.subservice: cost-management
ms.topic: quickstart
ms.date: 07/28/2020
ms.custom: subject-armqs, devx-track-azurecli
ms.openlocfilehash: 7d93bd757a39247302a6bc09009a1a814425c32f
ms.sourcegitcommit: 8c7f47cc301ca07e7901d95b5fb81f08e6577550
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/27/2020
ms.locfileid: "92745368"
---
# <a name="quickstart-create-a-budget-with-an-arm-template"></a>Краткое руководство. Создание бюджета с помощью шаблона ARM

Бюджеты в службе "Управление затратами" помогают планировать и отслеживать отчетность на уровне организации. С бюджетами вы можете учитывать службы Azure, которые используете или на которые подписываетесь в течение определенного периода. Они помогают сообщать другим пользователям о своих расходах, чтобы эффективно управлять затратами и контролировать то, как они возрастают с течением времени. Когда созданные вами пороговые значения бюджета превышены, активируются уведомления. Ни один из ваших ресурсов не затронут а потребление не остановлено. Анализируя затраты, можно использовать бюджеты для их сравнения и отслеживания. В этом кратком руководстве описано, как создать бюджет с помощью шаблона Azure Resource Manager (шаблона ARM).

[!INCLUDE [About Azure Resource Manager](../../../includes/resource-manager-quickstart-introduction.md)]

Если среда соответствует предварительным требованиям и вы знакомы с использованием шаблонов ARM, нажмите кнопку **Развертывание в Azure** . Шаблон откроется на портале Azure.

[![Развертывание в Azure](../../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fcreate-budget%2Fazuredeploy.json)

## <a name="prerequisites"></a>Предварительные требования

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

Если вы используете новую подписку, вы не сможете сразу создать бюджет или использовать другие функции службы "Управление затратами". Полная активация всех функций Управления затратами может потребовать до 48 часов.

Бюджеты поддерживаются для следующих областей и типов учетных записей Azure:

- Области управления доступом на основе ролей (Azure RBAC)
    - Группы управления
    - Подписка
- Области Соглашения Enterprise
    - учетная запись выставления счетов;
    - отдел;
    - учетная запись регистрации;
- Отдельные соглашения:
    - учетная запись выставления счетов;
- Области Клиентского соглашения Майкрософт
    - учетная запись выставления счетов;
    - Профиль выставления счетов
    - Раздел счета
    - Customer
- Области AWS
    - Внешняя учетная запись
    - Внешняя подписка

Чтобы просмотреть данные о бюджете, вам нужен как минимум доступ на чтение для учетной записи Azure.

Для подписок Azure EA вам необходимо иметь доступ на чтение для просмотра данных о бюджете. А для создания и администрирования бюджетов требуется разрешение уровня участника.

На подписку для бюджетов по пользователям и группам поддерживаются следующие разрешения или области Azure. См. [основные сведения об областях и работе с ними](understand-work-scopes.md).

- Владелец может создавать, изменять или удалять бюджеты для подписки.
- Участник и участник службы "Управление затратами" может создавать, изменять или удалять свои собственные бюджеты. Можно изменить сумму бюджета для бюджетов, созданных другими пользователями.
- Читатель и читатель службы "Управление затратами" может просматривать бюджеты, к которым имеет доступ.

Дополнительные сведения о назначении разрешений на доступ к данным службы "Управление затратами" см. в [этой статье](assign-access-acm-data.md).

## <a name="review-the-template"></a>Изучение шаблона

Шаблон, используемый в этом кратком руководстве, взят из [шаблонов быстрого запуска Azure](https://azure.microsoft.com/resources/templates/create-budget).

:::code language="json" source="~/quickstart-templates/create-budget/azuredeploy.json" :::

В этом шаблоне определяется один ресурс Azure.

* [Microsoft.Consumption/budgets](/azure/templates/microsoft.consumption/budgets): создание бюджета Azure.

## <a name="deploy-the-template"></a>Развертывание шаблона

1. Выберите следующее изображение, чтобы войти на портал Azure и открыть шаблон. Шаблон создаст бюджет.

   [![Развертывание в Azure](../../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fcreate-budget%2Fazuredeploy.json)

2. Введите или выберите следующие значения.

   :::image type="content" source="./media/quick-create-budget-template/create-budget-using-template-portal.png" alt-text="Шаблон Resource Manager, создание бюджета, развертывание на портале" lightbox="./media/quick-create-budget-template/create-budget-using-template-portal.png" :::
   
    * **Подписка** . Выберите нужную подписку Azure.
    * **Группа ресурсов** : при необходимости **создайте** группу ресурсов или выберите существующую.
    * **Регион** : выберите регион Azure. Например, **центральная часть США** .
    * **Имя бюджета** . Введите имя для этого бюджета. Оно должно быть уникальным в пределах группы ресурсов. Допустимы только буквы, цифры, знаки подчеркивания и дефисы.
    * **Сумма** . Введите общий объем затрат, который будет отслеживаться этим бюджетом.
    * **Интервал времени** . Введите период времени, охватываемый этим бюджетом. Допустимые значения: ежемесячно, ежеквартально или ежегодно. По истечении интервала времени сумма бюджета сбрасывается.
    * **Дата начала** . Введите дату начала, которая соответствует первому дню месяца в формате ГГГГ-ММ-ДД. Дата начала в будущем должна быть не позже, чем через три месяца от текущей даты. Вы можете указать дату начала в прошлом в сочетании с интервалом времени.
    * **Дата окончания** . Введите дату окончания учета бюджета в формате ГГГГ-ММ-ДД. 
    * **First Threshold** (Первое пороговое значение). Введите пороговое значение для первого уведомления. Уведомление отправляется, когда накопленная стоимость превысит пороговое значение. Это значение всегда выражается в процентах и должно находиться в диапазоне от 0 до 1000.
    * **Second Threshold** (Второе пороговое значение). Введите пороговое значение для второго уведомления. Уведомление отправляется, когда накопленная стоимость превысит пороговое значение. Это значение всегда выражается в процентах и должно находиться в диапазоне от 0 до 1000.
    * **Contact Roles** (Роли для связи). Введите список ролей для связи, которым будет отправлено уведомление о превышении порогового значения для бюджета. По умолчанию поддерживаются роли владельца, участника и читателя. Ожидается формат `["Owner","Contributor","Reader"]`.
    * **Contact Emails** (Адреса электронной почты для связи). Введите список адресов электронной почты, на которые будет отправлено уведомление о превышении порогового значения для бюджета. Ожидается формат `["user1@domain.com","user2@domain.com"]`.
    * **Contact Groups** (Контакты для связи). Введите список идентификаторов ресурсов групп действий (в виде полного URI ресурса), в которые будет отправлено уведомление о превышении порогового значения для бюджета. Здесь принимается массив строк. Ожидается формат `["action group resource ID1","action group resource ID2"]`. Если вы не хотите использовать группы действий, введите значение `[]`.
    * **Resource Group Filter Values** (Значения фильтра группы ресурсов). Введите список имен групп ресурсов для фильтрации. Ожидается формат `["Resource Group Name1","Resource Group Name2"]`. Если вы не хотите применять фильтр, введите значение `[]`. 
    * **Meter Category Filter Values** (Значения фильтра категории средств измерения). Введите список категорий средств измерения служб Azure. Ожидается формат `["Meter Category1","Meter Category2"]`. Если вы не хотели применять фильтр, введите значение `[]`.
   
3. В зависимости от типа подписки Azure выполните одно из следующих действий:
   - Выберите **Review + create** (Просмотреть и создать).
   - Просмотрите условия использования и выберите **Я принимаю указанные выше условия** , а затем нажмите кнопку **Приобрести** .

4. Если вы выбрали **Просмотреть и создать** , шаблон будет проверен. Нажмите кнопку **создания** .  

   ![Шаблон Resource Manager: уведомление о развертывании бюджета на портале](./media/quick-create-budget-template/resource-manager-template-portal-deployment-notification.png)

Для развертывания шаблона используется портал Azure. Помимо портала Azure можно также использовать Azure PowerShell, Azure CLI и REST API. Сведения о других шаблонах развертывания см. в [этой статье](../../azure-resource-manager/templates/deploy-powershell.md).

## <a name="validate-the-deployment"></a>Проверка развертывания

С помощью портала Azure вы можете убедиться, что бюджет успешно развернут. Для этого выберите **Управление затратами и выставление счетов**  > область действия > **Бюджеты** . Также для просмотра бюджета вы можете использовать следующие скрипты в Azure CLI или Azure PowerShell.

# <a name="cli"></a>[CLI](#tab/CLI)

```azurecli-interactive
az consumption budget list
```

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

```azurepowershell-interactive
Get-AzConsumptionBudget
```

---

## <a name="clean-up-resources"></a>Очистка ресурсов

Если бюджет вам больше не нужен, удалите его, используя один из описанных ниже способов.

### <a name="azure-portal"></a>Портал Azure

Перейдите в раздел **Управление затратами и выставление счетов** , выберите область выставления счетов, щелкните **Бюджеты** , выберите бюджет, а затем щелкните **Удалить бюджет** .

### <a name="command-line"></a>Командная строка

Бюджет можно удалить с помощью Azure CLI или Azure PowerShell.

# <a name="cli"></a>[CLI](#tab/CLI)

```azurecli-interactive
echo "Enter the budget name:" &&
read budgetName &&
az consumption budget delete --budget-name $budgetName &&
echo "Press [ENTER] to continue ..."
```

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

```azurepowershell-interactive
$budgetName = Read-Host -Prompt "Enter the budget name"
Remove-AzConsumptionBudget -Name $budgetName
Write-Host "Press [ENTER] to continue..."
```

---

## <a name="next-steps"></a>Дальнейшие действия

Из этого краткого руководства вы узнали, как создать бюджет Azure для развертывания. Дополнительные сведения об управлении затратами и выставлением счетов в Azure и Azure Resource Manager см. в статьях ниже.

- Изучите обзорные сведения об [управлении затратами и выставлении счетов](../cost-management-billing-overview.md).
- [Создайте бюджеты](tutorial-acm-create-budgets.md) на портале Azure.
- Сведения об [Azure Resource Manager](../../azure-resource-manager/management/overview.md)
