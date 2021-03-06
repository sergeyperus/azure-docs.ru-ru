---
title: Поддержка перемещения ресурсов SQL Azure между регионами с помощью перемещения ресурсов Azure.
description: Ознакомьтесь со статьей поддержка перемещения ресурсов SQL Azure между регионами с помощью перемещения ресурсов Azure.
author: rayne-wiselman
manager: evansma
ms.service: resource-move
ms.topic: conceptual
ms.date: 09/07/2020
ms.author: raynew
ms.openlocfilehash: 573d52b836aef36063dd288bf5a5016b98d220ef
ms.sourcegitcommit: c95e2d89a5a3cf5e2983ffcc206f056a7992df7d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2020
ms.locfileid: "95524136"
---
# <a name="support-for-moving-azure-sql-resources-between-azure-regions"></a>Поддержка перемещения ресурсов SQL Azure между регионами Azure

В этой статье приведены сведения о поддержке и предварительных требованиях для перемещения ресурсов SQL Azure между регионами Azure с помощью перемещения ресурсов Azure.

## <a name="requirements"></a>Требования

Требования приведены в следующей таблице.

**Возможность** | **Поддержка** | **Сведения**
--- | --- | ---
**База данных SQL Azure с гипермасштабированием** | Не поддерживается | Не удается переместить базы данных на уровне службы "масштабирование SQL Azure" с помощью перемещения ресурсов.
**Избыточность в пределах зоны** | Поддерживается |  Поддерживаемые параметры перемещения:<br/><br/> — Между регионами, поддерживающими избыточность зоны.<br/><br/> — Между регионами, которые не поддерживают избыточность зоны.<br/><br/> — Между регионом, поддерживающим избыточность зоны, в регион, который не поддерживает избыточность зоны.<br/><br/> — Между регионом, который не поддерживает избыточность зоны, в регион, поддерживающий избыточность зоны. 
**Синхронизация данных** | База данных концентратора или синхронизации: не поддерживается<br/><br/> Член синхронизации: поддерживается. | При перемещении члена синхронизации необходимо настроить синхронизацию данных с новой целевой базой данных.
**Существующая Георепликация** | Поддерживается | Существующие геореплики повторно сопоставляются с новым источником в целевом регионе.<br/><br/> Начальное заполнение должно быть инициализировано после перемещения. [Дополнительные сведения](../azure-sql/database/active-geo-replication-configure-portal.md)
**Прозрачное шифрование данных (TDE) с создание собственных ключей (BYOK)** | Поддерживается | Дополнительные [сведения](../key-vault/general/move-region.md) о перемещении хранилищ ключей в разных регионах.
**TDE с ключом, управляемым службой** | Поддерживается. |  Дополнительные [сведения](../key-vault/general/move-region.md) о перемещении хранилищ ключей в разных регионах.
**Правила динамического маскирования данных** | Поддерживается. | Правила автоматически копируются в целевой регион в процессе перемещения. [Подробнее](../azure-sql/database/dynamic-data-masking-configure-portal.md).
**Расширенная защита данных** | Не поддерживается. | Обходное решение. Настройте на уровне SQL Server в целевом регионе. [Подробнее](../azure-sql/database/azure-defender-for-sql.md).
**Правила брандмауэра** | Не поддерживается. | Обходное решение. Настройте правила брандмауэра для SQL Server в целевом регионе. Правила брандмауэра уровня базы данных копируются с исходного сервера на целевой сервер. [Подробнее](../azure-sql/database/firewall-create-server-level-portal-quickstart.md).
**Политики аудита** | Не поддерживается. | Политики будут сброшены к значениям по умолчанию после перемещения. [Узнайте](../azure-sql/database/auditing-overview.md) , как выполнить сброс.
**Хранение архивных копий** | Поддерживается. | Политики хранения резервных копий для исходной базы данных переносятся в целевую базу данных. [Узнайте](../azure-sql/database/long-term-backup-retention-configure.md) , как изменить параметры после перемещения.
**Автоматическая настройка** | Не поддерживается. | Обходное решение. Задайте параметры автоматической настройки после перемещения. [Подробнее](../azure-sql/database/automatic-tuning-enable.md).
**Предупреждения базы данных** | Не поддерживается. | Обходное решение. Настройте оповещения после перемещения. [Подробнее](../azure-sql/database/alerts-insights-configure-portal.md).
**База данных Stretch SQL Server Azure** | Не поддерживается | Не удается переместить базы данных Stretch SQL Server с помощью перемещения ресурсов.
**Azure Synapse Analytics** | Не поддерживается | Не удается переместить синапсе Analytics (ранее — хранилище данных SQL) с помощью перемещения ресурсов.
## <a name="next-steps"></a>Следующие шаги

Попробуйте использовать [ресурсы SQL Azure](tutorial-move-region-sql.md) в другом регионе с помощью перемещения ресурсов.