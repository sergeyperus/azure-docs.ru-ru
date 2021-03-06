---
title: Рекомендации по оценке для оценки сервера в Azure
description: Советы по созданию оценок с оценкой сервера "миграция Azure".
author: rayne-wiselman
ms.service: azure-migrate
ms.topic: conceptual
ms.date: 11/19/2019
ms.author: raynew
ms.openlocfilehash: e007f0272a693f5117b0182dad82de2f4a6e252a
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2020
ms.locfileid: "91576886"
---
# <a name="best-practices-for-creating-assessments"></a>Рекомендации по созданию оценок

Служба [Миграция Azure](./migrate-services-overview.md) объединяет в себе инструменты, которые используются для поиска, оценки и переноса приложений, инфраструктуры и рабочих нагрузок в Microsoft Azure. Она включает в себя инструменты Миграции Azure и предложения независимых поставщиков программного обеспечения.

В этой статье приводятся рекомендации по созданию оценок с помощью средства Azure Migrate Server для оценки.

## <a name="about-assessments"></a>Об оценках

Оценки, создаваемые с помощью Azure "миграция сервера", — это моментальный снимок данных на момент времени. Существует два типа оценок, которые можно создать с помощью функции "миграция Azure": Оценка сервера:

**Тип оценки** | **Сведения**
--- | --- 
**Azure** | Оценки для переноса локальных серверов на виртуальные машины Azure. <br/><br/> С помощью этого типа оценки вы можете оценить возможность миграции на виртуальные машины Azure для локальных [виртуальных машин VMware](how-to-set-up-appliance-vmware.md), [виртуальных машин Hyper-V](how-to-set-up-appliance-hyper-v.md) и [физических серверов](how-to-set-up-appliance-physical.md). [Дополнительные сведения](concepts-assessment-calculation.md)
**Решение Azure VMware (AVS)** | Оценки для переноса локальных серверов в [Решение Azure VMware (AVS)](../azure-vmware/introduction.md). <br/><br/> С помощью этого типа оценки вы можете оценить возможность миграции в Решение Azure VMware (AVS) для локальных [виртуальных машин VMware](how-to-set-up-appliance-vmware.md). [Дополнительные сведения](concepts-azure-vmware-solution-assessment-calculation.md)


### <a name="sizing-criteria"></a>Критерии определения размера
Оценка сервера предоставляет два варианта критериев для определения размера.

**Критерии определения размера** | **Сведения** | **Data**
--- | --- | ---
**На основе производительности** | Оценки, которые предоставляют рекомендации на основе собранных данных о производительности | **Оценка для виртуальных машин Azure.** Рекомендуемый размер виртуальной машины подбирается на основе данных об использовании ЦП и памяти.<br/><br/> Рекомендации по типу диска (HDD или SSD цен. категории "Стандартный" или управляемые диски цен. категории "Премиум") основываются на значениях операций ввода-вывода в секунду и пропускной способности локальных дисков.<br/><br/> **Оценка для Решения Azure VMware.** Рекомендуемый размер узлов AVS подбирается на основе данных об использовании ЦП и памяти.
**Как в локальной среде** | Оценки, в которых не учитываются данные о производительности для создания рекомендаций. | **Оценка для виртуальных машин Azure.** Рекомендуемый размер виртуальной машины подбирается на основе размера локальной виртуальной машины.<br/><br> Рекомендуемый тип диска зависит от того, какое значение вы выбрали для параметра типа хранилища при выполнении оценки.<br/><br/> **Оценка для Решения Azure VMware.** Рекомендуемый размер узлов AVS подбирается на основе размера локальной виртуальной машины.

#### <a name="example"></a>Пример
Например, если у вас есть локальная виртуальная машина с четырьмя ядрами с использованием 20% и объем памяти в 8 ГБ с использованием 10%, оценка виртуальной машины Azure будет следующей:

- **Оценка на основе производительности**:
    - Определяет действующие ядра и память на основе ядра (4 x 0,20 = 0,8) и использования памяти (8 ГБ x 0,10 = 0,8).
    - Применяет коэффициент использования, указанный в свойствах оценки (предположим, 1.3 x), чтобы получить значения, которые будут использоваться для изменения размера. 
    - Рекомендует ближайший размер виртуальной машины в Azure, который может поддерживать память размером не более 1,04 ядер (0,8 x 1,3) и ~ 1,04 ГБ (0,8 x 1,3).

- **Оценка "как есть" (как и в локальной среде)**:
    -  Рекомендует виртуальную машину с четырьмя ядрами; 8 ГБ памяти.


## <a name="best-practices-for-creating-assessments"></a>Рекомендации по созданию оценок

Устройство "миграция Azure" постоянно выполняет профилирование локальной среды и отправляет метаданные и данные о производительности в Azure. Следуйте этим рекомендациям по оценке серверов, обнаруженных с помощью устройства:

- **Создание оценки "как есть**". Вы можете создавать оценки "как есть" сразу же после того, как компьютеры будут отображаться на портале службы "миграция Azure".
- **Создание оценки на основе производительности**. После настройки обнаружения рекомендуется подождать по крайней мере один день, прежде чем выполнять оценку на основе производительности:
    - Сбор данных о производительности занимает некоторое время. Ожидание по крайней мере дня гарантирует наличие достаточного количества точек данных о производительности перед выполнением оценки.
    - При выполнении оценки на основе производительности убедитесь, что вы проведете Профилирование среды для оценки длительности. Например, если вы создаете оценку с длительностью производительности, равной одной неделе, необходимо подождать не менее недели после начала обнаружения, чтобы собирать все точки данных. Если этого не сделать, оценка не будет оцениваться пятью звездами.
- **Пересчет оценок**. Поскольку оценки представляют собой моментальные снимки на момент времени, они не обновляются автоматически последними данными. Чтобы обновить оценку с использованием последних данных, необходимо повторно вычислить их.

Следуйте этим рекомендациям по оценке серверов, импортированных в службу "миграция Azure", с помощью. CSV-файл:

- **Создание оценки "как есть**". Вы можете создавать оценки "как есть" сразу же после того, как компьютеры будут отображаться на портале службы "миграция Azure".
- **Создание оценки на основе производительности**. это поможет получить лучшую оценку затрат, особенно если вы настроили избыточную емкость сервера в локальной среде. Однако точность оценки на основе производительности зависит от данных производительности, указанных для серверов. 
- **Пересчет оценок**. Поскольку оценки представляют собой моментальные снимки на момент времени, они не обновляются автоматически последними данными. Чтобы обновить оценку с использованием последних импортированных данных, необходимо повторно вычислить их.
 
### <a name="ftt-sizing-parameters-for-avs-assessments"></a>ФТТ параметры размера для оценок AVS

Подсистема хранилища, используемая в AVS, — это vSAN. Политики хранилища vSAN определяют требования к хранилищу для виртуальных машин. Они гарантируют требуемый уровень обслуживания для виртуальных машин, так как определяют способ выделения ресурсов хранилища для виртуальной машины. Доступны следующие сочетания FTT-RAID: 

**Отказоустойчивость (FTT)** | **Конфигурация RAID** | **Минимальное требуемое число узлов** | **Рекомендации по размеру**
--- | --- | --- | --- 
1 | RAID-1 (зеркальное отображение) | 3 | Виртуальная машина размером 100 ГБ будет потреблять 200 ГБ.
1 | RAID-5 (удаляющее кодирование) | 4 | Виртуальная машина размером 100 ГБ будет потреблять 133,33 ГБ.
2 | RAID-1 (зеркальное отображение) | 5 | Виртуальная машина размером 100 ГБ будет потреблять 300 ГБ.
2 | RAID-6 (удаляющее кодирование) | 6 | Виртуальная машина размером 100 ГБ будет потреблять 150 ГБ.
3 | RAID-1 (зеркальное отображение) | 7 | Виртуальная машина размером 100 ГБ будет потреблять 400 ГБ.


## <a name="best-practices-for-confidence-ratings"></a>Рекомендации по оценкам достоверности

При выполнении оценок на основе производительности Оценка достоверности от 1 до 5 звезд (самая высокая) выдается для оценки. Эффективное использование оценок достоверности:
- Для оценки сервера "миграция Azure" требуются данные об использовании ЦП или памяти виртуальной машины.
- Для каждого диска, подключенного к локальной виртуальной машине, требуются данные о пропускной способности для операций чтения и записи.
- Для каждого сетевого адаптера, подключенного к виртуальной машине, требуются данные сети и.

В зависимости от процента точек данных, доступных в течение выбранного времени, Оценка достоверности для оценки предоставляется, как показано в следующей таблице.

   **Доступность точки данных** | **Оценка достоверности**
   --- | ---
   0–20 % | 1 звезда
   21–40 % | 2 звезды
   41–60 % | 3 звезды
   61–80 % | 4 звезды
   81–100 % | 5 звезд


## <a name="common-assessment-issues"></a>Распространенные проблемы с оценкой

Вот как можно решить некоторые распространенные проблемы среды, влияющие на оценку.

###  <a name="out-of-sync-assessments"></a>Оценки вне синхронизации

Если после создания оценки вы добавите или удалите компьютеры из группы, то созданная вами оценка будет помечена как **Несинхронизированная**. Запустите оценку еще раз (**пересчитать**), чтобы отразить изменения группы.

### <a name="outdated-assessments"></a>Устаревшие оценки

При наличии локальных изменений на виртуальных машинах, которые находятся в оцениваемой группе, оценка будет помечена как **устаревшая**. Оценка может быть помечена как устаревшая из-за одного или нескольких изменений в следующих свойствах:

- Число ядер процессора
- Выделенная память
- Тип загрузки или встроенное по
- Имя, версия и архитектура операционной системы
- Количество дисков
- Число сетевых адаптеров
- Размер диска (распределено ГБ)
- Свойства сетевого адаптера обновлены. Пример: изменение MAC-адреса, Добавление IP адреса и т. д.

Запустите оценку еще раз (**пересчитать**), чтобы отразить изменения.

### <a name="low-confidence-rating"></a>Низкая степень достоверности

Оценка может не иметь всех точек данных по ряду причин:

- Среда не была профилирована на период времени, для которого создается оценка. Например, если вы создаете *оценку на основе производительности* с длительностью "одна неделя", необходимо подождать минимум в неделю после начала обнаружения всех точек данных для сбора. Чтобы увидеть последнюю применимую оценку достоверности, всегда можно щелкнуть **пересчитать** . Оценка достоверности применяется, только если вы создаете оценку *на основе производительности* .

- В течение периода, для которого рассчитывается оценка, несколько виртуальных машин были отключены. Если какие-либо виртуальные машины были отключены в течение некоторого времени, функция оценки сервера не сможет собрать данные о производительности за этот период.

- Несколько виртуальных машин были созданы после запуска обнаружения в решении "Оценка сервера". Например, вы создаете оценку для журнала производительности за последний месяц, при этом несколько виртуальных машин были созданы всего неделю назад. В этом случает данные о производительности новых машин будут недоступны для всего периода анализа, а рейтинг достоверности будет низким.

### <a name="migration-tool-guidance-for-avs-assessments"></a>Руководство по средствам миграции для оценки AVS

В отчете о готовности к работе в Azure для оценки Решения Azure VMware приведены следующие рекомендуемые инструменты: 
- **VMware хккс или Enterprise**: для виртуальных машин VMware — это рекомендуемое средство миграции, которое позволяет перенести локальную рабочую нагрузку в частное облако решения Azure VMware (AVS). [Подробнее](../azure-vmware/tutorial-deploy-vmware-hcx.md)
- **Неизвестно**: для виртуальных машин, импортированных с помощью CSV-файла, инструмент миграции по умолчанию неизвестен. Однако для компьютеров VMware рекомендуется использовать решение гибридного облака VMware (ХККС).


## <a name="next-steps"></a>Дальнейшие шаги

- [Узнайте](concepts-assessment-calculation.md) , как рассчитываются оценки.
- [Узнайте](how-to-modify-assessment.md) , как настроить оценку.
