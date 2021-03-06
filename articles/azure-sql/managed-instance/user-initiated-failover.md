---
title: Запуск отработки отказа Управляемый экземпляр SQL вручную
description: Узнайте, как вручную выполнить отработку отказа первичной и вторичной реплик в Управляемый экземпляр Azure SQL.
services: sql-database
ms.service: sql-managed-instance
ms.custom: seo-lt-2019, sqldbrb=1, devx-track-azurecli
ms.devlang: ''
ms.topic: how-to
author: danimir
ms.author: danil
ms.reviewer: douglas, sstein
ms.date: 08/31/2020
ms.openlocfilehash: 51e9e66e2fd8ff60dd20c275a66fd13c047cc629
ms.sourcegitcommit: 9889a3983b88222c30275fd0cfe60807976fd65b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/20/2020
ms.locfileid: "94985524"
---
# <a name="user-initiated-manual-failover-on-sql-managed-instance"></a>Ручная отработка отказа, инициированная пользователем в SQL Управляемый экземпляр

В этой статье объясняется, как вручную отработка отказа основного узла на уровнях служб SQL Управляемый экземпляр общего назначения (GP) и критически важный для бизнеса (BC) и как вручную отработка отказа вторичного узла реплики только для чтения на уровне службы BC.

## <a name="when-to-use-manual-failover"></a>Когда следует использовать отработку отказа вручную

[Высокий уровень доступности](../database/high-availability-sla.md) — это фундаментальная часть платформы SQL управляемый экземпляр, которая прозрачно работает для приложений баз данных. Отработка отказа с первичного на вторичные узлы в случае снижения производительности узла или обнаружения сбоя или во время регулярного ежемесячного обновления программного обеспечения — это ожидаемое событие для всех приложений, использующих SQL Управляемый экземпляр в Azure.

Вы можете выполнить [отработку отказа вручную](../database/high-availability-sla.md#testing-application-fault-resiliency) на управляемый экземпляр SQL по следующим причинам:
- Тестирование приложения на отказоустойчивость перед развертыванием в рабочей среде
- Тестирование комплексных систем на отказоустойчивость при автоматическом переходе на другой ресурс
- Проверка влияния отработки отказа на существующие сеансы базы данных
- Проверьте, изменяет ли отработка отказа сквозную производительность из-за изменений в сетевой задержке.
- В некоторых случаях снижения производительности запросов отработка отказа вручную может помочь устранить проблемы с производительностью.

> [!NOTE]
> Обеспечение отказоустойчивости приложений до развертывания в рабочей среде поможет снизить риск сбоев приложений в рабочей среде и повлиять на доступность приложений для ваших клиентов.

## <a name="initiate-manual-failover-on-sql-managed-instance"></a>Запуск отработки отказа вручную на Управляемый экземпляр SQL

### <a name="azure-rbac-permissions-required"></a>Требуются разрешения RBAC Azure

Пользователь, инициирующий отработку отказа, должен иметь одну из следующих ролей Azure:

- Роль владельца подписки или
- Роль участника Управляемый экземпляр или
- Пользовательская роль со следующим разрешением:
  - `Microsoft.Sql/managedInstances/failover/action`

### <a name="using-powershell"></a>Регистрация с помощью PowerShell

Минимальная версия AZ. SQL должна быть [v 2.9.0](https://www.powershellgallery.com/packages/Az.Sql/2.9.0). Рассмотрите возможность использования [Azure Cloud Shell](../../cloud-shell/overview.md) из портал Azure, где всегда доступна последняя версия PowerShell. 

Для установки необходимых модулей Azure в качестве предварительных требований используйте следующий сценарий PowerShell. Кроме того, выберите подписку, в которой находится Управляемый экземпляр, для которой требуется выполнить отработку отказа.

```powershell
$subscription = 'enter your subscription ID here'
Install-Module -Name Az
Import-Module Az.Accounts
Import-Module Az.Sql

Connect-AzAccount
Select-AzSubscription -SubscriptionId $subscription
```

Используйте командлет PowerShell Command [-азсклинстанцефаиловер](/powershell/module/az.sql/invoke-azsqlinstancefailover) в следующем примере, чтобы инициировать отработку отказа основного узла, применимую к уровню служб BC и GP.

```powershell
$ResourceGroup = 'enter resource group of your MI'
$ManagedInstanceName = 'enter MI name'
Invoke-AzSqlInstanceFailover -ResourceGroupName $ResourceGroup -Name $ManagedInstanceName
```

Используйте следующую команду PS для отработки отказа для вторичного узла, доступного только для уровня служб BC.

```powershell
$ResourceGroup = 'enter resource group of your MI'
$ManagedInstanceName = 'enter MI name'
Invoke-AzSqlInstanceFailover -ResourceGroupName $ResourceGroup -Name $ManagedInstanceName -ReadableSecondary
```

### <a name="using-cli"></a>Использование синтаксиса командной строки

Убедитесь, что установлены последние версии скриптов CLI.

Используйте команду AZ SQL MI Failover в следующем примере, чтобы инициировать отработку отказа основного узла, применимого к уровню служб BC и GP.

```cli
az sql mi failover -g myresourcegroup -n myinstancename
```

Используйте следующую команду CLI для отработки отказа вторичного узла, доступного только для уровня служб BC.

```cli
az sql mi failover -g myresourcegroup -n myinstancename --replica-type ReadableSecondary
```

### <a name="using-rest-api"></a>Использование REST API

Для опытных пользователей, которым, возможно, потребуется автоматизировать отработку отказа управляемых экземпляров SQL в целях реализации непрерывного конвейера тестирования или автоматизированного механизма снижения производительности, эту функцию можно выполнить, инициируя отработку отказа через вызов API. Дополнительные сведения см. в разделе [управляемые экземпляры — REST API отработки отказа](/rest/api/sql/managed%20instances%20-%20failover/failover) .

Чтобы инициировать отработку отказа с помощью вызова REST API, сначала создайте маркер проверки подлинности с помощью клиента API по своему усмотрению. Созданный маркер проверки подлинности используется в качестве свойства авторизации в заголовке запроса API и является обязательным.

Ниже приведен пример кода URI API для вызова:

```HTTP
POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/managedInstances/{managedInstanceName}/failover?api-version=2019-06-01-preview
```

В вызове API необходимо передать следующие свойства:

| **Свойство API** | **Параметр** |
| --- | --- |
| subscriptionId | Идентификатор подписки, в которой развернут управляемый экземпляр |
| имя_группы_ресурсов | Группа ресурсов, содержащая управляемый экземпляр |
| managedInstanceName | Имя управляемого экземпляра |
| репликатипе | Используемых (Первичный или Реадаблесекондари). Эти параметры представляют тип реплики для отработки отказа: первичная или вторичная. Если этот параметр не указан, по умолчанию отработка отказа будет инициирована в первичной реплике. |
| api-version | Статическое значение и в настоящее время должно быть "2019-06-01-Preview" |

Ответ API будет одним из следующих двух:

- 202 — принято
- Одна из 400 ошибок запроса.

Состояние операции можно отвести от просмотра ответов API в заголовках ответа. Дополнительные сведения см. в статье [Состояние асинхронных операций Azure](../../azure-resource-manager/management/async-operations.md).

## <a name="monitor-the-failover"></a>Мониторинг отработки отказа

Чтобы отслеживать ход выполнения отработки отказа пользователем вручную, выполните следующий запрос T-SQL в избранном клиенте (например, SSMS) на SQL Управляемый экземпляр. Будет прочитано системное представление sys.dm_hadr_fabric_replica_states и реплики отчетов, доступные в экземпляре. Обновите тот же запрос после инициации перехода на другой ресурс вручную.

```T-SQL
SELECT DISTINCT replication_endpoint_url, fabric_replica_role_desc FROM sys.dm_hadr_fabric_replica_states
```

Перед запуском отработки отказа выходные данные будут указывать на текущую первичную реплику на уровне службы BC, содержащую один первичный и три вторичных базы данных в группе доступности AlwaysOn. При выполнении отработки отказа повторное выполнение этого запроса должно указывать на изменение основного узла.

Вы не сможете увидеть те же выходные данные с уровнем службы групповой политики, как показано выше для BC. Это связано с тем, что уровень служб GP основан только на одном узле. Выходные данные запроса T-SQL для уровня службы групповой политики будут показывать только один узел до и после отработки отказа. Отключение подключения клиента во время отработки отказа, которое обычно длится через минуту, будет означать выполнение отработки отказа.

> [!NOTE]
> Завершение процесса отработки отказа (а не самого короткого недоступного) может занять несколько минут в случае **интенсивных** рабочих нагрузок. Это обусловлено тем, что подсистема экземпляра следит за всеми текущими транзакциями на сервере-источнике и дохватывается на дополнительном узле перед отработкой отказа.

> [!IMPORTANT]
> Функциональные ограничения инициированной пользователем ручной отработки отказа:
> - Может быть один (1) отработка отказа, инициированная на одном Управляемый экземпляр каждые **30 минут**.
> - Для экземпляров BC должен существовать кворум реплик, чтобы запрос отработки отказа был принят.
> - Для экземпляров BC невозможно указать, на какой вторичной реплике для запуска отработки отказа будет выполняться операция.

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте больше о высокой доступности управляемого экземпляра [Высокая доступность для управляемый экземпляр Azure SQL](../database/high-availability-sla.md).
- Общие сведения см. в статье [что такое Azure SQL управляемый экземпляр?](sql-managed-instance-paas-overview.md).
