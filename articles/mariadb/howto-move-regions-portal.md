---
title: Перемещение регионов Azure. портал Azure — база данных Azure для MariaDB
description: Переместите сервер базы данных Azure для MariaDB из одного региона Azure в другой с помощью реплики чтения и портал Azure.
author: savjani
ms.author: pariks
ms.service: mariadb
ms.topic: how-to
ms.custom: subject-moving-resources
ms.date: 06/29/2020
ms.openlocfilehash: f4ce34bc1a1af7b2c0ee57a3297415bd9d033517
ms.sourcegitcommit: 6ab718e1be2767db2605eeebe974ee9e2c07022b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/12/2020
ms.locfileid: "94540830"
---
# <a name="move-an-azure-database-for-mariadb-server-to-another-region-by-using-the-azure-portal"></a>Перемещение сервера базы данных Azure для MariaDB в другой регион с помощью портал Azure

Существует несколько сценариев перемещения существующей базы данных Azure для сервера MariaDB из одного региона в другой. Например, может потребоваться переместить рабочий сервер в другой регион в рамках планирования аварийного восстановления.

Для завершения перемещения в другой регион можно использовать базу данных Azure для [реплики чтения между регионами](concepts-read-replicas.md#cross-region-replication) MariaDB. Для этого сначала создайте реплику чтения в целевом регионе. Затем следует выполнить репликацию на сервер реплики чтения, чтобы сделать его автономным сервером, принимающим трафик как для чтения, так и для записи. 

> [!NOTE]
> В этой статье рассматривается перемещение сервера в другой регион. Если вы хотите переместить сервер в другую группу ресурсов или подписку, см. статью [Перемещение](../azure-resource-manager/management/move-resource-group-and-subscription.md) . 

## <a name="prerequisites"></a>Обязательные условия

- Функция чтения реплики доступна только для серверов базы данных Azure для MariaDB в общего назначения или ценовой категории, оптимизированные для памяти. Убедитесь, что исходный сервер находится в одной из этих ценовых категорий.

- Убедитесь, что исходный сервер базы данных Azure для MariaDB находится в регионе Azure, из которого вы хотите переместиться.

## <a name="prepare-to-move"></a>Подготовка к переносу

Чтобы создать сервер реплики для чтения между регионами в целевом регионе с помощью портал Azure, выполните следующие действия.

1. Войдите на [портал Azure](https://portal.azure.com/).
1. Выберите существующий сервер базы данных Azure для MariaDB, который будет использоваться в качестве исходного сервера. Откроется страница **Обзор**.
1. В меню в разделе **Параметры** выберите **Репликация**.
1. Выберите **Добавить реплику**.
1. Введите имя сервера реплики.
1. Укажите расположение сервера реплики. Расположение по умолчанию совпадает с местоположением исходного сервера. Убедитесь, что выбрано целевое расположение, в котором должна быть развернута реплика.
1. Нажмите кнопку **ОК** , чтобы подтвердить создание реплики. Во время создания реплики данные копируются с исходного сервера в реплику. Время создания может быть в несколько минут или более, пропорционально размеру исходного сервера.

>[!NOTE]
> При создании реплики она не наследует конечные точки службы виртуальной сети исходного сервера. Эти правила следует настроить для каждой реплики отдельно.

## <a name="move"></a>Переместить

> [!IMPORTANT]
> Это сервер нельзя снова преобразовать в реплику.
> Прежде, чем останавливать репликацию в реплике чтения убедитесь, что реплика содержит все необходимые данные.

Остановка репликации на сервере реплики приводит к тому, что она становится автономным сервером. Чтобы отключить репликацию в реплику из портал Azure, выполните следующие действия.

1. После создания реплики выберите базу данных Azure для исходного сервера MariaDB. 
1. В меню в разделе **Параметры** выберите **Репликация**.
1. Выберите сервер реплики.
1. Щелкните **Остановить репликацию**.
1. Подтвердите остановку репликации, нажав кнопку **ОК**.

## <a name="clean-up-source-server"></a>Очистка исходного сервера

Возможно, потребуется удалить исходный сервер базы данных Azure для MariaDB. Для этого выполните следующие действия.

1. После создания реплики выберите базу данных Azure для исходного сервера MariaDB.
1. В окне **Обзор** выберите **Удалить**.
1. Введите имя исходного сервера для подтверждения, которое нужно удалить.
1. Выберите команду **Удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы переместили сервер базы данных Azure для MariaDB из одного региона в другой с помощью портал Azure а затем очистили ненужные исходные ресурсы. 

- Узнайте больше о [репликах чтения](concepts-read-replicas.md)
- Дополнительные сведения об [управлении репликами чтения в портал Azure](howto-read-replicas-portal.md)
- Дополнительные сведения о возможностях обеспечения [непрерывности бизнес-процессов](concepts-business-continuity.md)