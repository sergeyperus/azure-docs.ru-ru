---
title: Azure Defender для SQL
description: Узнайте о функциях для управления уязвимостями базы данных и обнаружения аномальных действий, которые могут указывать на угрозу для базы данных в базе данных SQL Azure, Управляемый экземпляр Azure SQL или Azure синапсе.
services: sql-database
ms.service: sql-db-mi
ms.subservice: security
ms.devlang: ''
ms.custom: sqldbrb=2
ms.topic: conceptual
ms.author: memildin
manager: rkarlin
author: memildin
ms.reviewer: vanto
ms.date: 09/21/2020
ms.openlocfilehash: d147303df43c4f86843df518c71316e6a97b6671
ms.sourcegitcommit: 4cb89d880be26a2a4531fedcc59317471fe729cd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678086"
---
# <a name="azure-defender-for-sql"></a>Azure Defender для SQL
[!INCLUDE[appliesto-sqldb-sqlmi-asa](../includes/appliesto-sqldb-sqlmi-asa.md)]


Azure Defender для SQL — это унифицированный пакет расширенных функций защиты SQL, Служба "защитник Azure" доступна для базы данных SQL Azure, Azure SQL Управляемый экземпляр и Azure синапсе Analytics. Он включает в себя функции для обнаружения и классификации конфиденциальных данных, обнаружения и устранения потенциальных уязвимостей базы данных и обнаружения аномальных действий, которые могут указывать на угрозу для вашей базы данных. Эта служба предоставляет единый центр для включения этих возможностей и управления ими.

## <a name="overview"></a>Обзор

Защитник Azure предоставляет набор расширенных возможностей безопасности SQL, включая оценку уязвимостей SQL и расширенную защиту от угроз.
- [Оценка уязвимостей](sql-vulnerability-assessment.md) — это простая в настройке служба, которая может обнаруживать, записывать и помогать устранять потенциальные уязвимости базы данных. Он предоставляет сведения о состоянии безопасности и содержит действия по устранению проблем безопасности и улучшению фортификатионс базы данных.
- [Расширенная защита от угроз](threat-detection-overview.md) позволяет выявить подозрительную активность, указывающую на необычные и потенциально опасные попытки получить доступ к базам данных или воспользоваться ими. Она постоянно отслеживает подозрительные действия в базе данных и обеспечивает немедленное оповещение системы безопасности о потенциальных уязвимостях, атаках путем внедрения кода SQL Azure и аномальных шаблонах доступа к базам данных. Оповещения Расширенной защиты от угроз содержат сведения о подозрительных операциях и рекомендации о том, как исследовать причину угрозы и устранить ее.

Включите Azure Defender для SQL один раз, чтобы активировать все эти встроенные функции. Одним щелчком можно включить защитник Azure для всех баз данных на [сервере](logical-servers.md) в Azure или в управляемый экземпляр SQL. Для включения или управления параметрами защитника Azure требуется принадлежность к роли [диспетчера безопасности SQL](../../role-based-access-control/built-in-roles.md#sql-security-manager) или одной из ролей администратора базы данных или сервера.

Дополнительные сведения о ценах на службу "защитник Azure для SQL" см. на [странице цен на центр безопасности Azure](https://azure.microsoft.com/pricing/details/security-center/).

## <a name="getting-started-with-azure-defender"></a>Приступая к работе с защитником Azure

Чтобы приступить к работе с защитником Azure, выполните следующие действия.

## <a name="enable-azure-defender"></a>Включение Azure Defender

Доступ к защитнику Azure можно получить с помощью [портал Azure](https://portal.azure.com). Включите защитник Azure, перейдя в **Центр безопасности** под заголовком **безопасности** для сервера или управляемого экземпляра.

> [!NOTE]
> Учетная запись хранения автоматически создается и настраивается для хранения результатов проверки **уязвимостей** . Если вы уже включили защитник Azure для другого сервера в той же группе ресурсов и регионе, используется существующая учетная запись хранения.
>
> Стоимость защитника Azure соответствует ценам на стандартный уровень центра безопасности Azure на каждый узел, где узел является полностью сервером или управляемым экземпляром. Поэтому вы платите только один раз для защиты всех баз данных на сервере или управляемом экземпляре с помощью защитника Azure. Вы можете опробовать Azure Defender изначально с помощью бесплатной пробной версии.

## <a name="start-tracking-vulnerabilities-and-investigating-threat-alerts"></a>Запуск отслеживания уязвимостей и изучения оповещений об угрозах

Щелкните карту **Оценка уязвимостей** , чтобы просмотреть отчеты о поиске уязвимостей, управлять проверками и отслеживать состояние безопасности. Если оповещения системы безопасности получены, щелкните карту **Advanced Threat protection** , чтобы просмотреть подробные сведения о предупреждениях, а также чтобы просмотреть объединенный отчет по всем оповещениям в подписке Azure на странице оповещения безопасности центра безопасности Azure.

## <a name="manage-azure-defender-settings"></a>Управление параметрами защитника Azure

Чтобы просмотреть параметры защитника Azure и управлять ими, перейдите в **Центр безопасности** под заголовком **Безопасность** для сервера или управляемого экземпляра. На этой странице можно включить или отключить защитник Azure, а также изменить средства оценки уязвимостей и дополнительные параметры защиты от угроз для всего сервера или управляемого экземпляра.

## <a name="manage-azure-defender-settings-for-a-database"></a>Управление параметрами защитника Azure для базы данных

Чтобы переопределить параметры защитника Azure для определенной базы данных, установите флажок **включить защитник Azure для SQL на уровне базы данных** . Используйте этот параметр только в том случае, если у вас есть определенное требование для получения отдельных оповещений о повышенной защите от угроз или результатов оценки уязвимостей для отдельной базы данных вместо предупреждений и результатов, полученных для всех баз данных на сервере или управляемом экземпляре.

После выбора флажка можно настроить соответствующие параметры для этой базы данных.

Параметры защитника Azure для сервера или управляемого экземпляра можно также получить в области базы данных защитника Azure. Щелкните **Параметры** на главной панели защитника Azure, а затем щелкните **Просмотреть параметры защитника Azure для SQL Server** .

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения об [оценке уязвимостей](sql-vulnerability-assessment.md)
- Дополнительные сведения о [расширенной защите от угроз](threat-detection-configure.md)
- Узнайте больше о [центре безопасности Azure](../../security-center/security-center-introduction.md).