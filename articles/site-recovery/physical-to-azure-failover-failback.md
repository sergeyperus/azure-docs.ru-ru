---
title: Настройка отработки отказа и восстановления размещения для физических серверов с помощью Site Recovery
description: Узнайте, как выполнить отработку отказа физических серверов в Azure и восстановить размещение на локальном сайте для аварийного восстановления с помощью Azure Site Recovery
services: site-recovery
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.topic: article
ms.date: 12/17/2019
ms.author: raynew
ms.openlocfilehash: 2994f68e4159c7c4aa7d82bef7a5891deb5055a0
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "96017429"
---
# <a name="fail-over-and-fail-back-physical-servers-replicated-to-azure"></a>Отработка отказа и восстановление размещения физических серверов, реплицированных в Azure

В этом руководстве описывается, как выполнить отработку отказа локальных физических серверов, которые реплицируются в Azure с помощью [Azure Site Recovery](site-recovery-overview.md). После отработки отказа вы можете восстановить диск из Azure на локальный сайт, когда он будет доступен.

## <a name="before-you-start"></a>Перед началом работы

- [Сведения](failover-failback-overview.md) о процессе отработки отказа в аварийном восстановлении.
- Если вы хотите выполнить отработку отказа нескольких компьютеров, [Узнайте](recovery-plan-overview.md) , как собирать компьютеры вместе в плане восстановления.
- Прежде чем выполнять полную отработку отказа, выполните [детализацию аварийного восстановления](site-recovery-test-failover-to-azure.md) , чтобы убедиться, что все работает правильно.
- Выполните [эти инструкции](site-recovery-failover.md#prepare-to-connect-after-failover) для подготовки к подключению к виртуальным машинам Azure после отработки отказа.



## <a name="run-a-failover"></a>Запуск отработки отказа

### <a name="verify-server-properties"></a>Проверка свойств сервера

Проверьте свойства сервера и убедитесь, что он соответствует [требованиям Azure](vmware-physical-azure-support-matrix.md#replicated-machines) к виртуальным машинам Azure.

1. В разделе **Защищенные элементы** щелкните **Реплицированные элементы** и выберите виртуальную машину.
2. В области **Реплицированный элемент** находятся сводные данные о компьютере, в том числе состояние работоспособности и последние доступные точки восстановления. Щелкните **Свойства**, чтобы просмотреть дополнительные сведения.
3. В окне " **расчеты и сеть**" можно изменить имя Azure, группу ресурсов, целевой размер, [набор доступности](../virtual-machines/windows/tutorial-availability-sets.md)и параметры управляемого диска.
4. Можно просмотреть или изменить параметры сети, включая сеть (или подсеть), в которой будет размещаться виртуальная машина Azure после отработки отказа, и IP-адрес, который будет ей назначен.
5. В разделе **Диски** отображаются сведения об операционной системе и дисках данных на компьютере.

### <a name="fail-over-to-azure"></a>Отработка отказа с переходом в Azure

1. В разделе **Параметры** > **Реплицированные элементы** выберите компьютер и щелкните **Отработка отказа**.
2. В разделе **Отработка отказа** выберите **точку восстановления**, в которую будет выполнена отработка отказа. Можно выбрать один из следующих вариантов:
   - **Последние**. В этом случае сначала обрабатываются все данные, отправляемые в Site Recovery. Этот вариант обеспечивает самое низкое значение RPO (целевая точка восстановления), так как виртуальная машина Azure, созданная после отработки отказа, будет иметь все данные, реплицированные в службу Site Recovery до момента активации отработки отказа.
   - **Последняя обработанная.** Отработка отказа выполняется до последней точки восстановления компьютера, которая была обработана Site Recovery. Этот вариант обеспечивает низкий показатель целевого времени восстановления, так как не требует времени на обработку данных.
   - **Последняя точка во времени согласованности приложений.** Отработка отказа компьютера выполняется до последней точки восстановления с согласованным состоянием приложений, которая была обработана Site Recovery.
   - **Настраиваемая.** Следует указать точку восстановления.

3. Выберите **Завершение работы виртуальной машины перед началом отработки отказа.**, чтобы служба Site Recovery попыталась выключить исходный компьютер, прежде чем запускать отработку отказа. Отработка отказа продолжится, даже если их не удастся отключить. На странице **Задания** можно следить за ходом выполнения отработки отказа.
4. Если вы готовы подключиться к виртуальной машине Azure, сделайте это, чтобы проверить ее после отработки отказа.
5. После проверки **зафиксируйте** отработку отказа. При этом будут удалены все доступные точки восстановления.

> [!WARNING]
> Не отменяйте отработку отказа в процессе выполнения. Перед началом отработки отказа репликация компьютера останавливается. Если отменить отработку отказа, она останавливается, но компьютер не будет реплицироваться повторно.
> Дополнительная отработка отказа физических серверов может длиться 8–10 минут.

## <a name="automate-actions-during-failover"></a>Автоматизация действий во время отработки отказа

Может потребоваться автоматизировать действия во время отработки отказа. Для этого можно использовать сценарии или модули Runbook службы автоматизации Azure в планах восстановления.

- [Узнайте](site-recovery-create-recovery-plans.md) о создании и настройке планов восстановления, включая добавление скриптов.
- [Узнайте, как](site-recovery-runbook-automation.md) добавить модули Runbook службы автоматизации Azure в планы восстановления о.

## <a name="configure-settings-after-failover"></a>Настройка параметров после отработки отказа

После отработки отказа необходимо [настроить параметры Azure](site-recovery-failover.md#prepare-in-azure-to-connect-after-failover) для подключения к реплицированным виртуальным машинам Azure. Кроме того, настройте [внутренние и общедоступные](site-recovery-failover.md#set-up-ip-addressing) IP-адреса.

## <a name="prepare-for-reprotection-and-failback"></a>Подготовка к повторному включению защиты и восстановлению размещения

После отработки отказа в Azure вы повторно защищаете виртуальные машины Azure, реплицируют их на локальный сайт. После того как они будут реплицированы, вы можете вернуть их в локальную среду, запустив отработку отказа из Azure на локальный сайт.

1. Размещение физических серверов, реплицированных в Azure, можно восстановить только на виртуальных машинах VMware. Для этого вам требуется локальная инфраструктура VMware. Выполните действия, описанные в [этой статье](vmware-azure-prepare-failback.md) , чтобы подготовиться к повторной защите и восстановлению размещения, включая настройку сервера обработки в Azure и локального главного целевого сервера, а также настройку VPN типа "сеть — сеть" или частный пиринг ExpressRoute для восстановления размещения.
2. Убедитесь, что локальный сервер конфигурации работает и подключен к Azure. Во время отработки отказа в Azure локальный сайт может быть недоступен, а сервер конфигурации может быть недоступен или выключен. Во время восстановления размещения виртуальная машина должна существовать в базе данных сервера конфигурации. В противном случае восстановление размещения завершается сбоем.
3. Удалите все моментальные снимки на локальном главном целевом сервере. В противном случае повторная защита не будет работать.  Во время выполнения задания повторного включения защиты моментальные снимки на виртуальной машине автоматически объединяются.
4. При повторной защите виртуальных машин, объединенных в группу репликации для согласованности нескольких виртуальных машин, убедитесь, что все они имеют одинаковую операционную систему (Windows или Linux), и что на развертываемом главном целевом сервере установлен тот же тип операционной системы. Все виртуальные машины в группе репликации должны использовать тот же главный целевой сервер.
5. Откройте [требуемые порты](vmware-azure-prepare-failback.md#ports-for-reprotectionfailback) для восстановления размещения.
6. Перед восстановлением размещения убедитесь, что подключен сервер vCenter Server. В противном случае отключение дисков и их присоединение к виртуальной машине завершится сбоем.
7. Если управление виртуальными машинами, в которые необходимо выполнить восстановление размещения, осуществляется с помощью сервера vCenter Server, убедитесь в наличии требуемых разрешений. Если выполнить обнаружение vCenter в режиме пользователя только для чтения и защитить виртуальные машины, операция настройки защиты завершится успешно и отработка отказа будет работать. Однако во время повторного включения защиты происходит сбой отработки отказа, так как невозможно обнаружить хранилища данных, и они не указаны во время повторной защиты. Для устранения этой проблемы можно обновить учетные данные vCenter, указав [соответствующую учетную запись или разрешения](vmware-azure-tutorial-prepare-on-premises.md#prepare-an-account-for-automatic-discovery), и повторить задание. 
8. Если виртуальные машины созданы с помощью шаблона, убедитесь в том, что диски каждой виртуальной машины имеют UUID. Если локальный UUID виртуальной машины конфликтует с UUID главного целевого сервера, поскольку оба были созданы из одного и того же шаблона, повторное включение защиты завершится сбоем. Выполните развертывание из другого шаблона.
9. Если вы восстанавливаете размещение на альтернативном сервере vCenter Server, убедитесь в том, что новый сервер vCenter Server и главный целевой сервер обнаружены. Как правило, если они не являются хранилищами данных, они недоступны или не отображаются в списке **повторной защиты**.
10. Ознакомьтесь со следующими сценариями, в которых невозможно выполнить восстановление размещения.
    - Если вы используете бесплатный выпуск ESXi 5.5 или бесплатный выпуск vSphere 6 Hypervisor. Выполните обновление до другой версии.
    - Если вы используете физический сервер Windows Server 2008 R2 с пакетом обновления 1 (SP1).
    - Виртуальные машины, которые были перенесены.
    - Виртуальная машина, которая была перемещена в другую группу ресурсов.
    - Реплика виртуальной машины Azure, которая была удалена.
    - Реплика виртуальной машины Azure, которая не защищена (реплицируется на локальный сайт).
10. [Изучите типы восстановления размещения](concepts-types-of-failback.md), которые можно использовать, — восстановление в исходное расположение и восстановление в альтернативное расположение.


## <a name="reprotect-azure-vms-to-an-alternate-location"></a>Повторное включение защиты виртуальных машин Azure в альтернативное расположение

Эта процедура предполагает, что локальная виртуальная машина недоступна.

1. В хранилище > **Параметры**  >  **реплицированные элементы** щелкните правой кнопкой мыши компьютер, для которого выполнена отработка отказа > **повторно защитить**.
2. В окне **Повторная защита** выберите **Из Azure в локальную среду**.
3. Укажите локальный главный целевой сервер и сервер обработки.
4. В поле **Хранилище данных** выберите главное целевое хранилище данных, для которого нужно восстановить диски локальной среды.
       - Используйте этот параметр, если локальная виртуальная машина удалена или не существует, и вам необходимо создать новые диски.
       - Этот параметр пропускается, если диски уже существуют, но необходимо указать значение.
5. Выберите главный целевой диск для хранения. Политика восстановления размещения выбирается автоматически.
6. Нажмите кнопку **ОК**, чтобы начать процесс повторной защиты. Задание начинает реплицировать виртуальную машину Azure на локальный сайт. Ход выполнения операции можно отслеживать на вкладке **Задания** .

> [!NOTE]
> Если вы хотите восстановить виртуальную машину Azure в существующую локальную виртуальную машину, подключите ее хранилище данных локальной виртуальной машины с доступом на чтение и запись к узлу ESXi главного целевого сервера.


## <a name="fail-back-from-azure"></a>Восстановление размещения из Azure

Выполните отработку отказа следующим образом:

1. На странице **Реплицированные элементы** щелкните правой кнопкой мыши виртуальную машину и выберите пункт **Внеплановая отработка отказа**.
2. На странице **Подтверждение отработки отказа** должно быть указано направление отработки отказа "Из Azure".
3. Выберите точку восстановления, которая будет использоваться для отработки отказа.
    - Рекомендуется использовать **последнюю** точку восстановления. Точка, согласованная с приложением, следует за последней точкой во времени, что приведет к потере некоторых данных.
    - **Последняя** точка восстановления является отказоустойчивой точкой восстановления.
    - При отработке отказа служба Site Recovery отключает виртуальные машины Azure и загружает локальную виртуальную машину. Чтобы исключить время простоя, выберите подходящий момент.
4. Щелкните машину правой кнопкой мыши, а затем выберите пункт **Зафиксировать**. Будет запущено задание по удалению виртуальных машин Azure.
5. Убедитесь, что работа виртуальной машины Azure была завершена должным образом.


## <a name="reprotect-on-premises-machines-to-azure"></a>Повторное включение защиты локальных машин в Azure

Теперь данные будут снова находиться на локальном сайте, но они не реплицируются в Azure. Чтобы еще раз выполнить репликацию в Azure, сделайте следующее.

1. В разделе "Хранилище" > **Параметры** >**Реплицированные элементы** выберите виртуальные машины, для которых выполнено восстановление размещения, и щелкните **Защитить повторно**.
2. Выберите сервер обработки, который используется для отправки реплицированных данных в Azure, и нажмите кнопку **ОК**.


## <a name="next-steps"></a>Следующие шаги

После завершения задания повторной защиты локальная виртуальная машина реплицируется в Azure. При необходимости можно [запустить другую процедуру отработки отказа](site-recovery-failover.md) в Azure.
