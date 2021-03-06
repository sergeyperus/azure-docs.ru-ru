---
title: Конечные точки и правила виртуальной сети для баз данных в базе данных SQL Azure
description: Пометьте подсеть как конечную точку службы для виртуальной сети. Затем конечная точка как правило виртуальной сети для ACL вашей базы данных. Затем база данных принимает подключения со всех виртуальных машин и других узлов в подсети.
services: sql-database
ms.service: sql-database
ms.subservice: security
ms.custom: sqldbrb=1
ms.devlang: ''
ms.topic: how-to
author: rohitnayakmsft
ms.author: rohitna
ms.reviewer: vanto, genemi
ms.date: 11/14/2019
ms.openlocfilehash: 97be3bf0ecec20c4bf2e1633f893c9aa0d9ba49d
ms.sourcegitcommit: 10d00006fec1f4b69289ce18fdd0452c3458eca5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2020
ms.locfileid: "95020288"
---
# <a name="use-virtual-network-service-endpoints-and-rules-for-servers-in-azure-sql-database"></a>Использование конечных точек службы и правил виртуальной сети для серверов в базе данных SQL Azure
[!INCLUDE[appliesto-sqldb-asa](../includes/appliesto-sqldb-asa.md)]

*Правила виртуальной сети* — это одна из функций безопасности брандмауэра, которая определяет, принимает ли сервер для баз данных и эластичных пулов в [базе данных SQL Azure](sql-database-paas-overview.md) или для баз данных в [Azure синапсе](../../synapse-analytics/sql-data-warehouse/sql-data-warehouse-overview-what-is.md) связь, отправляемую из определенных подсетей в виртуальных сетях. В этой статье объясняется, почему функция правила виртуальной сети иногда является лучшим вариантом для безопасного подключения к базе данных в базе данных SQL Azure и Azure синапсе Analytics (ранее — хранилище данных SQL).

> [!NOTE]
> Эта статья относится как к базе данных SQL Azure, так и к Azure синапсе Analytics. Для простоты термин "база данных" применяется к обеим из них. Аналогичным образом, "сервером" называется [логический сервер SQL Server](logical-servers.md), на котором размещены База данных SQL Azure и Azure Synapse Analytics.

Чтобы создать правило виртуальной сети, требуется [конечная точка службы для виртуальной сети][vm-virtual-network-service-endpoints-overview-649d], используемая для ссылки.

## <a name="how-to-create-a-virtual-network-rule"></a>Как создать правило виртуальной сети

Если вы собираетесь просто создать правило виртуальной сети, то можете сразу перейти к инструкциям и пояснениям, приведенным [далее в этой статье](#anchor-how-to-by-using-firewall-portal-59j).

## <a name="details-about-virtual-network-rules"></a>Сведения о правилах виртуальной сети

В этом разделе приводятся некоторые сведения о правилах виртуальной сети.

### <a name="only-one-geographic-region"></a>Только один географический регион

Каждая конечная точка службы для виртуальной сети может использоваться только в одном регионе Azure. Конечная точка не поддерживает прием подключений из подсети в других регионах.

Любое правило виртуальной сети ограничена регионом, в котором используется базовая конечная точка.

### <a name="server-level-not-database-level"></a>На уровне сервера, а не базы данных

Каждое правило виртуальной сети применяется ко всему серверу, а не только к одной конкретной базе данных на сервере. Другими словами, правило виртуальной сети применяется на уровне сервера,а не на уровне базы данных.

- Для сравнения, правило фильтрации IP-адресов можно применить на любом уровне.

### <a name="security-administration-roles"></a>Роли администратора безопасности

Роли безопасности для администрирования конечных точек служб для виртуальной сети разделены. Требуется действие каждой из следующих ролей:

- **администратор сети:** &nbsp; включение конечной точки;
- **Администратор базы данных:** &nbsp; Обновите список управления доступом (ACL), чтобы добавить указанную подсеть на сервер.

*Альтернатива Azure RBAC:*

Роли администратора сети и администратора базы данных имеют больше возможностей, чем требуется для управления правилами виртуальной сети. На самом деле для этого требуется только часть их возможностей.

Вы можете использовать [Управление доступом на основе ролей Azure (Azure RBAC)][rbac-what-is-813s] в Azure, чтобы создать одну настраиваемую роль, имеющую только необходимое подмножество возможностей. Вместо администратора сети или администратора базы данных можно использовать пользовательскую роль. При добавлении пользователя в пользовательскую роль контактная зона снижает уровень безопасности, а не добавляет пользователя к двум другим основным ролям администратора.

> [!NOTE]
> В некоторых случаях база данных в базе данных SQL Azure и подсеть виртуальной сети находятся в разных подписках. В этих случаях необходимо обеспечить следующую конфигурацию:
>
> - Обе подписки должны быть в одном клиенте Azure Active Directory.
> - Пользователь должен иметь необходимые разрешения для запуска операций, например для включения конечных точек службы или добавления подсети виртуальной сети к заданному серверу.
> - Обе подписки должны иметь зарегистрированного поставщика Microsoft.Sql.

## <a name="limitations"></a>Ограничения

Для базы данных SQL Azure правила виртуальной сети имеют следующие ограничения.

- В брандмауэре для базы данных в базе данных SQL Azure каждое правило виртуальной сети ссылается на подсеть. Все указанные подсети должны размещаться в том же географическом регионе, где размещена база данных.

- Каждый сервер может иметь до 128 записей ACL для любой заданной виртуальной сети.

- Правила виртуальной сети применяются только к виртуальным сетям Azure Resource Manager, но не к сетям на основе [классической модели развертывания][arm-deployment-model-568f].

- Включение конечных точек службы виртуальной сети для Базы данных SQL Azure также включает конечные точки для служб MySQL и PostgreSQL Azure. Тем не менее, если конечные точки включены в базе данных, подключение через них к экземплярам MySQL или PostgreSQL может завершиться ошибкой.
  - В основном это происходит из-за того, что для MySQL и PostgreSQL не настроены правила виртуальной сети. Настройте правило виртуальной сети для Базы данных Azure для MySQL и PostgreSQL, чтобы установить подключение.
  - Чтобы определить правила брандмауэра виртуальной сети на логическом сервере SQL, который уже настроен с частными конечными точками, установите для параметра **запретить доступ к общедоступной сети** значение **нет**.

- К приведенным ниже элементам сети применяются диапазоны IP-адресов в брандмауэре, а правила виртуальной сети — нет:
  - [виртуальная частная сеть (VPN) типа "сеть — сеть"][vpn-gateway-indexmd-608y].
  - Локальная среда с помощью [ExpressRoute](../../expressroute/index.yml)

### <a name="considerations-when-using-service-endpoints"></a>Рекомендации по использованию конечных точек служб

При использовании конечных точек служб Базы данных SQL Azure обратите внимание на следующие моменты:

- **Требуется исходящее подключение к общедоступным IP-адресам Базы данных SQL Azure.** Чтобы предоставить возможность подключения, группы безопасности сети (NSG) необходимо открыть для IP-адресов Базы данных SQL Azure. Это можно сделать с помощью [тегов службы](../../virtual-network/network-security-groups-overview.md#service-tags) NSG для Базы данных SQL Azure.

### <a name="expressroute"></a>ExpressRoute

Если вы используете [ExpressRoute](../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) для локальной среды, для общедоступного пиринга или пиринга Майкрософт, то вам необходимо определить используемые IP-адреса NAT. Для общедоступного пиринга в каждом канале ExpressRoute по умолчанию используется два IP-адреса NAT для трафика служб Azure, когда он входит в основную магистральную сеть Microsoft Azure. Для пиринга Майкрософт используются IP-адреса NAT, предоставленные клиентом или поставщиком услуг. Чтобы разрешить доступ к ресурсам служб, необходимо разрешить эти общедоступные IP-адреса в настройках брандмауэра IP-адресов ресурсов. Чтобы найти IP-адреса канала ExpressRoute для общедоступного пиринга, [отправьте запрос по ExpressRoute в службу поддержки](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) через портал Azure. Узнайте больше о [NAT для общедоступного пиринга и пиринга Майкрософт](../../expressroute/expressroute-nat.md?toc=%2fazure%2fvirtual-network%2ftoc.json#nat-requirements-for-azure-public-peering).
  
Чтобы разрешить взаимодействие канала с Базой данных SQL Azure, необходимо создать правила IP-сети для общедоступных IP-адресов NAT.

<!--
FYI: Re ARM, 'Azure Service Management (ASM)' was the old name of 'classic deployment model'.
When searching for blogs about ASM, you probably need to use this old and now-forbidden name.
-->

## <a name="impact-of-using-vnet-service-endpoints-with-azure-storage"></a>Влияние использования конечных точек службы виртуальной сети со службой хранилища Azure

Служба хранилища Azure реализовала ту же функцию, которая позволяет ограничить возможность подключения к учетной записи службы хранилища Azure. Если вы решили применить эту функцию к учетной записи службы хранилища Azure, используемой Базой данных Azure SQL, могут возникнуть проблемы. Далее приведен список и обсуждение функций Azure синапсе Analytics и базы данных SQL Azure, на которые повлияла эта функция.

### <a name="azure-synapse-polybase-and-copy-statement"></a>Azure синапсе Polybase и инструкция COPY

Polybase и инструкция COPY обычно используются для загрузки данных в Azure синапсе Analytics из учетных записей хранения Azure для приема данных с высокой пропускной способностью. Если учетная запись хранения Azure, из которой загружаются данные, ограничивает доступ только на набор подсетей виртуальной сети, подключение при использовании Polybase и инструкция COPY в учетной записи хранения будут нарушены. Чтобы включить сценарии импорта и экспорта с использованием копирования и Polybase с помощью Azure синапсе Analytics и подключения к службе хранилища Azure, защищенной для виртуальной сети, выполните указанные ниже действия.

#### <a name="prerequisites"></a>Предварительные требования

- Установите Azure PowerShell, следуя инструкциям в этом [руководстве](/powershell/azure/install-az-ps).
- При наличии учетной записи хранения общего назначения версии 1 или учетной записи хранилища BLOB-объектов необходимо сначала выполнить обновление до учетной записи хранения общего назначения версии 2, следуя инструкциям в этом [руководстве](../../storage/common/storage-account-upgrade.md).
- Необходимо включить параметр **Разрешить доверенным службам Майкрософт доступ к этой учетной записи хранения** в меню параметров **Брандмауэры и виртуальные сети** учетной записи службы хранилища Azure. Включение этой конфигурации позволит использовать Polybase и инструкцию COPY для подключения к учетной записи хранения с помощью надежной проверки подлинности, когда сетевой трафик остается в магистрали Azure. Дополнительные сведения см. в [этом руководстве](../../storage/common/storage-network-security.md#exceptions).

> [!IMPORTANT]
> Модуль PowerShell Azure Resource Manager по-прежнему поддерживается базой данных SQL Azure, но вся будущая разработка сосредоточена на модуле Az.Sql. Исправления ошибок для модуля AzureRM будут продолжать выпускаться как минимум до декабря 2020 г.  Аргументы команд в модулях Az и AzureRm практически идентичны. Дополнительные сведения о совместимости см. в статье [Знакомство с новым модулем Az для Azure PowerShell](/powershell/azure/new-azureps-module-az).

#### <a name="steps"></a>Шаги

1. В PowerShell **Зарегистрируйте сервер** , на котором размещена служба Azure синапсе, с Azure Active Directory (AAD):

   ```powershell
   Connect-AzAccount
   Select-AzSubscription -SubscriptionId <subscriptionId>
   Set-AzSqlServer -ResourceGroupName your-database-server-resourceGroup -ServerName your-SQL-servername -AssignIdentity
   ```

1. Создайте **учетную запись хранения общего назначения версии 2** с помощью этого [руководства](../../storage/common/storage-account-create.md).

   > [!NOTE]
   >
   > - При наличии учетной записи хранения общего назначения версии 1 или учетной записи хранилища BLOB-объектов необходимо **сначала выполнить обновление до учетной записи хранения версии 2**, следуя инструкциям в этом [руководстве](../../storage/common/storage-account-upgrade.md).
   > - Сведения об известных проблемах с Azure Data Lake Storage 2-го поколения см. в этом [руководстве](../../storage/blobs/data-lake-storage-known-issues.md).

1. В своей учетной записи хранения перейдите к элементу **Управление доступом (IAM)** и выберите **Добавить назначение ролей**. Назначьте роль Azure " **участник данных BLOB-объекта хранилища** " серверу, на котором размещена аналитика Azure синапсе Analytics, зарегистрированная в Azure Active Directory (AAD), как на шаге #1.

   > [!NOTE]
   > Этот шаг могут выполнять только члены с правами владельца в учетной записи хранения. Сведения о различных встроенных ролях Azure см. в этом [руководстве](../../role-based-access-control/built-in-roles.md).
  
1. **Установка подключения Polybase к учетной записи службы хранилища Azure:**

   1. Создайте **[главный ключ](/sql/t-sql/statements/create-master-key-transact-sql)** базы данных, если он еще не создан:

       ```sql
       CREATE MASTER KEY [ENCRYPTION BY PASSWORD = 'somepassword'];
       ```

   1. Создайте учетные данные базы данных, указав **IDENTITY = 'Managed Service Identity'**:

       ```sql
       CREATE DATABASE SCOPED CREDENTIAL msi_cred WITH IDENTITY = 'Managed Service Identity';
       ```

       > [!NOTE]
       >
       > - Не нужно указывать СЕКРЕТ с использованием ключа доступа к хранилищу Azure, так как на самом деле этот механизм использует [управляемое удостоверение](../../active-directory/managed-identities-azure-resources/overview.md).
       > - Имя IDENTITY должно быть **Managed Service Identity**, чтобы подключения PolyBase работали с учетной записью службы хранилища Azure, прикрепленной к виртуальной сети.

   1. Создайте внешний источник данных с помощью `abfss://` схемы для подключения к учетной записи хранения общего назначения версии 2 с помощью polybase:

       ```SQL
       CREATE EXTERNAL DATA SOURCE ext_datasource_with_abfss WITH (TYPE = hadoop, LOCATION = 'abfss://myfile@mystorageaccount.dfs.core.windows.net', CREDENTIAL = msi_cred);
       ```

       > [!NOTE]
       >
       > - При наличии внешних таблиц, связанных с учетной записью общего назначения версии 1 или учетной записью хранилища BLOB-объектов, сначала удалите эти внешние таблицы, а затем удалите соответствующий внешний источник данных. Затем создайте внешний источник данных со `abfss://` схемой подключения к учетной записи хранения общего назначения версии 2 и повторно создайте все внешние таблицы с помощью этого нового внешнего источника данных. Для удобства вы можете создать сценарии для всех внешних таблиц с помощью [мастера создания и публикации сценариев](/sql/ssms/scripting/generate-and-publish-scripts-wizard).
       > - Дополнительные сведения о `abfss://` схеме см. в этом [руководстве](../../storage/blobs/data-lake-storage-introduction-abfs-uri.md).
       > - Дополнительные сведения об инструкции CREATE EXTERNAL DATA SOURCE см. в этом [руководстве](/sql/t-sql/statements/create-external-data-source-transact-sql).

   1. Выполните запрос как обычно, используя [внешние таблицы](/sql/t-sql/statements/create-external-table-transact-sql).

### <a name="azure-sql-database-blob-auditing"></a>Аудит BLOB-объектов в базе данных SQL Azure

При аудите больших двоичных объектов журналы аудита отправляются в вашу учетную запись хранения. Если эта учетная запись хранения использует функцию конечных точек службы виртуальной сети, то подключение из базы данных SQL Azure к учетной записи хранения будет прервано.

## <a name="adding-a-vnet-firewall-rule-to-your-server-without-turning-on-vnet-service-endpoints"></a>Добавление правила брандмауэра виртуальной сети к серверу без включения конечных точек службы виртуальной сети

Пока возможности этой функции не были расширены, вам нужно было включить конечные точки службы виртуальной сети, чтобы реализовать динамическое правило виртуальной сети в брандмауэре. Конечные точки, связанные с заданной подсетью виртуальной сети, с базой данных в базе данных SQL Azure. По состоянию на январь 2018 г. это требование можно обойти, задав параметр **IgnoreMissingVNetServiceEndpoint**.

Если задать лишь правило брандмауэра, вы не сможете обеспечить безопасность сервера. Для этого вам также потребуется включить конечные точки службы виртуальной сети. При включении конечных точек службы подсеть виртуальной сети будет простаивать, пока не будет выполнен переход из состояния "Выкл." в состояние "Вкл.". Это особенно верно в случае с большими виртуальными сетями. С помощью параметра **IgnoreMissingVNetServiceEndpoint** можно уменьшить или исключить время простоя во время перехода.

Задать параметр **IgnoreMissingVNetServiceEndpoint** можно с помощью PowerShell. Дополнительные сведения см. в статье [Создание конечной точки службы и правила виртуальной сети для Базы данных SQL Azure с помощью PowerShell][sql-db-vnet-service-endpoint-rule-powershell-md-52d].

## <a name="errors-40914-and-40615"></a>Ошибки 40914 и 40615

Ошибка подключения 40914 относится к *правилам виртуальной сети*, указанным в области "Брандмауэр" на портале Azure. Ошибка 40615 отличается от предыдущей тем, что относится к *правилам IP-адресов* в брандмауэре.

### <a name="error-40914"></a>Ошибка 40914

*Текст сообщения.* Невозможно открыть сервер *[имя-сервера]*, запрашиваемый именем входа. Клиенту запрещен доступ к серверу.

*Описание ошибки.* Клиент находится в подсети, которая содержит конечные точки сервера виртуальной сети. Но у сервера нет правила виртуальной сети, которое предоставляет подсети право на взаимодействие с базой данных.

*Устранение ошибки.* В области "Брандмауэр" портала Azure с помощью элемента управления правилами виртуальных сетей [добавьте правило виртуальной сети](#anchor-how-to-by-using-firewall-portal-59j) для этой подсети.

### <a name="error-40615"></a>Ошибка 40615

*Текст сообщения.* Не удается открыть сервер {0}, запрашиваемый при попытке входа. Для клиента с IP-адресом {1} доступ к серверу запрещен.

*Описание ошибки:* Клиент пытается подключиться с IP-адреса, который не имеет полномочий для подключения к серверу. В брандмауэре сервера не указано правило IP-адресов, которое позволяет клиенту обмениваться данными с данным IP-адресом с базой данных.

*Устранение ошибки.* Введите IP-адрес клиента в качестве правила IP-адреса. Это следует сделать в области "Брандмауэр" на портале Azure.

<a name="anchor-how-to-by-using-firewall-portal-59j"></a>

## <a name="portal-can-create-a-virtual-network-rule"></a>Портал может создать правило виртуальной сети

В этом разделе показано, как можно использовать [портал Azure][http-azure-portal-link-ref-477t] для создания *правила виртуальной сети* в базе данных SQL Azure. Правило указывает, что база данных должна принимать подключения из определенной подсети, помеченной как *Конечная точка службы виртуальной сети*.

> [!NOTE]
> Если вы собираетесь добавить конечную точку службы к правилам брандмауэра виртуальной сети сервера, сначала убедитесь, что конечные точки службы включены для подсети.
>
> Если конечные точки службы не включены для подсети, портал предложит их включить. Нажмите кнопку **Включить** в той же колонке, в которой вы добавляете правило.

## <a name="powershell-alternative"></a>Альтернатива PowerShell

Скрипт также может создавать правила виртуальной сети с помощью командлета PowerShell **New-азсклсервервиртуалнетворкруле** или [AZ Network vnet Create](/cli/azure/network/vnet#az-network-vnet-create). Если вам это интересно, ознакомьтесь с разделом [Создание конечной точки службы и правила виртуальной сети для базы данных SQL Azure с помощью PowerShell][sql-db-vnet-service-endpoint-rule-powershell-md-52d].

## <a name="rest-api-alternative"></a>Альтернативный REST API

На внутреннем уровне командлеты PowerShell для действий виртуальной сети SQL вызывают REST API. REST API можно вызывать напрямую.

- [Virtual Network Rules][rest-api-virtual-network-rules-operations-862r] (Правила виртуальной сети)

## <a name="prerequisites"></a>Предварительные требования

Необходима подсеть, помеченная определенным *именем типа* конечной точки службы для виртуальной сети, относящимся к базе данных SQL Azure.

- В нашем случае именем типа конечной точки является **Microsoft.Sql**.
- Если ваша подсеть, возможно, не помечена именем типа, прочитайте раздел [Проверка того, является ли подсеть конечной точкой][sql-db-vnet-service-endpoint-rule-powershell-md-a-verify-subnet-is-endpoint-ps-100].

<a name="a-portal-steps-for-vnet-rule-200"></a>

## <a name="azure-portal-steps"></a>Инструкции для портала Azure

1. Войдите на [портал Azure][http-azure-portal-link-ref-477t].

2. Найдите и выберите **серверы SQL Server**, а затем выберите свой сервер. В разделе **Безопасность** выберите **брандмауэры и виртуальные сети**.

3. Задайте для элемента управления **Разрешить доступ к службам Azure** значение "Выкл.".

    > [!IMPORTANT]
    > Если оставить этот элемент управления ВКЛЮЧЕНным, сервер будет принимать данные из любой подсети в границах Azure, т. е. исходит от одного из IP-адресов, распознаваемых в диапазонах, определенных для центров обработки данных Azure. что сделает доступ слишком незащищенным. Используя конечные точки службы для виртуальной сети Microsoft Azure с правилами виртуальной сети базы данных SQL можно уменьшить контактную зону системы безопасности.

4. Щелкните элемент управления **+ Добавить существующий** в разделе **Виртуальные сети**.

    ![Щелкните "Добавить существующий" (добавьте конечную точку подсети в виде правила SQL).][image-portal-firewall-vnet-add-existing-10-png]

5. В новой области **Создание или изменение** введите в элементы управления имена ресурсов Azure.

    > [!TIP]
    > Необходимо указать правильный **префикс адреса** для подсети. Его значение можно найти на портале.
    > Выберите **Все ресурсы** &gt; **Все типы** &gt; **Виртуальные сети**. Фильтр отобразит ваши виртуальные сети. Выберите свою виртуальную сеть и щелкните **Подсети**. Столбец **Диапазон адресов** содержит интересующий вас префикс адреса.

    ![Заполните поля для нового правила.][image-portal-firewall-create-update-vnet-rule-20-png]

6. Нажмите кнопку **ОК** в нижней части области.

7. Созданное правило виртуальной сети отобразится в области брандмауэра.

    ![Просмотрите новое правило в области брандмауэра.][image-portal-firewall-vnet-result-rule-30-png]

> [!NOTE]
> К правилам применяются следующие статусы или состояния:
>
> - **Готово.** Указывает, что операция, которую вы инициировали, завершена успешно.
> - **Сбой.** Указывает, что операция, которую вы инициировали, завершена сбоем.
> - **Удалено.** Применяется только к операции удаления и указывает, что привило удалено и больше не применяется.
> - **Выполняется.** Указывает, что операция выполняется. Старое правило применяется, когда операция находится в этом состоянии.

<a name="anchor-how-to-links-60h"></a>

## <a name="related-articles"></a>Связанные статьи

- [Конечные точки службы виртуальной сети Azure][vm-virtual-network-service-endpoints-overview-649d]
- [Правила брандмауэра уровня сервера и базы данных][sql-db-firewall-rules-config-715d]

## <a name="next-steps"></a>Дальнейшие действия

- [С помощью PowerShell создайте конечную точку службы виртуальной сети, а затем правило виртуальной сети для базы данных SQL Azure.][sql-db-vnet-service-endpoint-rule-powershell-md-52d]
- [Правила виртуальной сети: операции][rest-api-virtual-network-rules-operations-862r] с REST API

<!-- Link references, to images. -->
[image-portal-firewall-vnet-add-existing-10-png]: ../../sql-database/media/sql-database-vnet-service-endpoint-rule-overview/portal-firewall-vnet-add-existing-10.png
[image-portal-firewall-create-update-vnet-rule-20-png]: ../../sql-database/media/sql-database-vnet-service-endpoint-rule-overview/portal-firewall-create-update-vnet-rule-20.png
[image-portal-firewall-vnet-result-rule-30-png]: ../../sql-database/media/sql-database-vnet-service-endpoint-rule-overview/portal-firewall-vnet-result-rule-30.png

<!-- Link references, to text, Within this same GitHub repo. -->
[arm-deployment-model-568f]: ../../azure-resource-manager/management/deployment-models.md
[expressroute-indexmd-744v]:../index.yml
[rbac-what-is-813s]:../../role-based-access-control/overview.md
[sql-db-firewall-rules-config-715d]:firewall-configure.md
[sql-db-vnet-service-endpoint-rule-powershell-md-52d]:scripts/vnet-service-endpoint-rule-powershell-create.md
[sql-db-vnet-service-endpoint-rule-powershell-md-a-verify-subnet-is-endpoint-ps-100]:scripts/vnet-service-endpoint-rule-powershell-create.md#a-verify-subnet-is-endpoint-ps-100
[vm-configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal-321w]: ../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[vm-virtual-network-service-endpoints-overview-649d]: ../../virtual-network/virtual-network-service-endpoints-overview.md
[vpn-gateway-indexmd-608y]: ../../vpn-gateway/index.yml

<!-- Link references, to text, Outside this GitHub repo (HTTP). -->
[http-azure-portal-link-ref-477t]: https://portal.azure.com/
[rest-api-virtual-network-rules-operations-862r]: /rest/api/sql/virtualnetworkrules

<!-- ??2
#### Syntax related articles
- REST API Reference, including JSON
- Azure CLI
- ARM templates
-->
