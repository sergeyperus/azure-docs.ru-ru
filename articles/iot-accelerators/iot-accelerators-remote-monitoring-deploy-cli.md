---
title: Развертывание решения для удаленного мониторинга с помощью интерфейса командной строки в Azure | Документация Майкрософт
description: В этом руководстве показано, как с помощью интерфейса командной строки подготовить акселератор решения для удаленного мониторинга.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 03/08/2019
ms.topic: conceptual
ms.openlocfilehash: f9dcf19f5318021df5d9fdde777b8786942e33d8
ms.sourcegitcommit: a92fbc09b859941ed64128db6ff72b7a7bcec6ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2020
ms.locfileid: "92072260"
---
# <a name="deploy-the-remote-monitoring-solution-accelerator-using-the-cli"></a>Развертывание акселератора решения для удаленного мониторинга с помощью CLI

В этом руководстве показано, как развернуть акселератор решения для удаленного мониторинга. Решение развертывается с помощью интерфейса командной строки. Вы также можете развернуть решение с помощью веб-интерфейса пользователя на сайте azureiotsolutions.com. Дополнительные сведения об этом параметре см. в руководстве по [развертыванию решения для удаленного мониторинга](quickstart-remote-monitoring-deploy.md) .

## <a name="prerequisites"></a>Предварительные требования

Чтобы развернуть акселератор решения для удаленного мониторинга, нужна активная подписка Azure.

Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).

Чтобы запустить интерфейс командной строки, на локальном компьютере необходимо установить [Node.js](https://nodejs.org/).

## <a name="install-the-cli"></a>Установка интерфейса командной строки

Чтобы установить интерфейс командной строки, в среде командной строки выполните следующую команду:

```cmd/sh
npm install iot-solutions -g
```

## <a name="sign-in-to-the-cli"></a>Вход в интерфейс командной строки

Прежде чем развернуть акселератор решений, необходимо войти в подписку Azure с помощью интерфейса командной строки.

```cmd/sh
pcs login
```

Для завершения процесса входа следуйте инструкциям на экране.

## <a name="deployment-options"></a>Варианты развертывания

При развертывании акселератора решений существует несколько вариантов для настройки процесса.

| Параметр | Значения | Описание |
| ------ | ------ | ----------- |
| номер SKU    | `basic`, `standard`, `local` | _Базовое_ развертывание предназначено для тестирования и демонстрации. При этом все микрослужбы развертываются на одной виртуальной машине. _Стандартное_ развертывание предназначено для рабочей среды. При этом микрослужбы развертываются на нескольких виртуальных машинах. При _локальном_ развертывании контейнер Docker настраивается для запуска микрослужб на локальном компьютере и использует облачные службы Azure, например, хранилище и Cosmos DB. |
| Среда выполнения | `dotnet`, `java` | Позволяет выбирать языковую реализацию микрослужб. |

Дополнительные сведения об использовании локального развертывания см. в разделе [Локальное развертывание акселератора решения для удаленного мониторинга](iot-accelerators-remote-monitoring-deploy-local.md).

## <a name="basic-and-standard-deployments"></a>Базовые и стандартные развертывания

В этом разделе перечислены основные различия между базовыми и стандартными развертываниями.

### <a name="basic"></a>Basic

Вы можете выполнить базовое развертывание из [azureiotsolutions.com](https://www.azureiotsolutions.com/Accelerators) или с помощью интерфейса командной строки.

Базовое развертывание предназначено только для демонстрации решения. Чтобы снизить затраты, все микрослужбы развертываются в одной виртуальной машине. Это развертывание не использует архитектуру для промышленной эксплуатации.

Базовое развертывание создает в вашей подписке следующие группы ресурсов.

| Count | Ресурс                       | Тип         | Область использования |
|-------|--------------------------------|--------------|----------|
| 1     | [Виртуальная машина Linux](https://azure.microsoft.com/services/virtual-machines/) | Standard D1 V2  | Размещение микрослужб |
| 1     | [Центр Интернета вещей Azure](https://azure.microsoft.com/services/iot-hub/)                  | S1 — уровень "Стандартный" | Управление устройствами и обмен данными |
| 1     | [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)              | Стандартный        | Хранение данных конфигурации, правил, оповещений и других холодных данных |  
| 1     | [Учетная запись хранения Azure](../storage/common/storage-introduction.md#types-of-storage-accounts)  | Стандартный        | Хранилище для виртуальных машин и контрольных точек потоковой передачи |
| 1     | [Веб-приложение](https://azure.microsoft.com/services/app-service/web/)        |                 | Размещение интерфейсных веб-приложений |
| 1     | [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)        |                 | Управление удостоверениями пользователей и безопасностью |
| 1     | [Azure Maps](https://azure.microsoft.com/services/azure-maps/)        | Стандартный                | Просмотр расположений ресурса |
| 1     | [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)        |   3 единицы              | Поддержка аналитики в режиме реального времени |
| 1     | [Служба подготовки устройств Azure](../iot-dps/index.yml)        |       S1          | Подготовка устройств в нужном масштабе |
| 1     | [Аналитика временных рядов Azure](https://azure.microsoft.com/services/time-series-insights/)        |   S1 — 1 единица              | Хранилище для данных сообщений и глубокий анализ данных телеметрии |

### <a name="standard"></a>Стандартный

Стандартное развертывание можно выполнить только с помощью интерфейса командной строки.

Стандартное развертывание — это развертывание для промышленной эксплуатации, которое разработчик может настроить или расширить. Вариант стандартного развертывания следует применять, когда все будет готово к настройке архитектуры для промышленной эксплуатации с соответствующим уровнем масштабируемости и расширяемости. Микрослужбы приложений разработаны как контейнеры Docker и развернуты с помощью Службы Azure Kubernetes (AKS). Оркестратор Kubernetes развертывает, масштабирует и управляет микрослужбами.

Стандартное развертывание создает в вашей подписке Azure следующие группы ресурсов.

| Count | Ресурс                                     | Размер (номер SKU)      | Область использования |
|-------|----------------------------------------------|-----------------|----------|
| 1     | [Служба Azure Kubernetes](https://azure.microsoft.com/services/kubernetes-service)| Используйте полностью управляемую службу оркестрации контейнеров Kubernetes; по умолчанию применяется 3 агента|
| 1     | [Центр Интернета вещей Azure](https://azure.microsoft.com/services/iot-hub/)                     | S2 — уровень "Стандартный" | Команды и средства для управления устройствами |
| 1     | [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)                 | Стандартный        | Хранение данных конфигурации и данных телеметрии, например правил, оповещений и сообщений |
| 5     | [Учетные записи хранения Azure](../storage/common/storage-introduction.md#types-of-storage-accounts)    | Стандартный        | 4 для хранения виртуальных машин и 1 для контрольных точек потоковой передачи |
| 1     | [Служба приложений](https://azure.microsoft.com/services/app-service/web/)             | Стандартный S1     | Шлюз приложений через TLS |
| 1     | [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)        |                 | Управление удостоверениями пользователей и безопасностью |
| 1     | [Azure Maps](https://azure.microsoft.com/services/azure-maps/)        | Стандартный                | Просмотр расположений ресурса |
| 1     | [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)        |   3 единицы              | Поддержка аналитики в режиме реального времени |
| 1     | [Служба подготовки устройств Azure](../iot-dps/index.yml)        |       S1          | Подготовка устройств в нужном масштабе |
| 1     | [Аналитика временных рядов Azure](https://azure.microsoft.com/services/time-series-insights/)        |   S1 — 1 единица              | Хранилище для данных сообщений и глубокий анализ данных телеметрии |

> [!NOTE]
> Сведения о ценах на эти службы можно найти по адресу [https://azure.microsoft.com/pricing](https://azure.microsoft.com/pricing) . Сведения об объеме потребления и выставлении счетов для подписки можно найти на [портале Azure](https://portal.azure.com/).

## <a name="deploy-the-solution-accelerator"></a>Развертывание акселератора решений

Примеры развертывания

### <a name="example-deploy-net-version"></a>Пример: развертывание версии .NET

В примере ниже представлено развертывание базовой версии .NET акселератора решения для удаленного мониторинга:

```cmd/sh
pcs -t remotemonitoring -s basic -r dotnet
```

### <a name="example-deploy-java-version"></a>Пример: развертывание версии Java

В примере ниже представлено развертывание стандартной версии Java акселератора решения для удаленного мониторинга:

```cmd/sh
pcs -t remotemonitoring -s standard -r java
```

### <a name="pcs-command-options"></a>параметры команд предварительно настроенного решения

При выполнении команды `pcs` для развертывания решения запрашивается:

- Имя для решения. Имя должно быть уникальным.
- Подписка Azure, которую нужно использовать.
- Расположение.
- Учетные данные для виртуальных машин, на которых размещены микрослужбы. Эти учетные данные можно использовать для доступа к виртуальным машинам, используемым для устранения неполадок.

После выполнения команды `pcs` отобразится URL-адрес нового акселератора решений. Кроме того, команда `pcs` создает файл `{deployment-name}-output.json` с дополнительной информацией, например, имя созданного Центра Интернета вещей.

Чтобы получить дополнительные сведения о параметрах командной строки, выполните следующую команду:

```cmd/sh
pcs -h
```

Дополнительные сведения об интерфейсе командной строки см. в статье [Azure IoT PCS CLI Overview](https://github.com/Azure/pcs-cli/blob/master/README.md)(Обзор интерфейса командной строки для предварительно настроенного решения Центра Интернета вещей Azure).

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы узнали следующее:

> [!div class="checklist"]
> * настройка акселератора решений;
> * Развертывание акселератора решений
> * вход в акселератор решений.

Теперь, когда вы развернули решение для удаленного мониторинга, ознакомьтесь со статьей [Краткое руководство. Использование облачного решения для удаленного мониторинга](./quickstart-remote-monitoring-deploy.md).

<!-- Next how-to guides in the sequence -->