---
title: Перезапуск сервера-Azure CLI — база данных Azure для MariaDB
description: В этой статье описывается, как можно перезапустить сервер базы данных Azure для MariaDB с помощью Azure CLI.
author: savjani
ms.author: pariks
ms.service: mariadb
ms.topic: how-to
ms.date: 3/18/2020
ms.custom: devx-track-azurecli
ms.openlocfilehash: 8ae69adfe83b871eb29c85fc4d03e817026ec006
ms.sourcegitcommit: 6ab718e1be2767db2605eeebe974ee9e2c07022b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/12/2020
ms.locfileid: "94541374"
---
# <a name="restart-azure-database-for-mariadb-server-using-the-azure-cli"></a>Перезапустите базу данных Azure для сервера MariaDB с помощью Azure CLI
В этой статье объясняется, как перезапустить сервер Базы данных Azure для MariaDB. Возможно, вам потребуется перезапустить сервер в целях обслуживания, что приводит к кратковременному отключению во время выполнения операции.

Если служба занята, перезапустить сервер не удастся. Например, служба может обрабатывать запрошенную ранее операцию, такую как масштабирование виртуальных ядер.

Время, необходимое для завершения перезапуска, зависит от процесса восстановления MariaDB. Чтобы уменьшить время перезапуска, рекомендуем свести к минимуму объем действий, выполняемых на сервере перед перезапуском.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>Обязательные условия

Для работы с этим руководством должны быть выполнены следующие условия.

- Необходим [сервер базы данных Azure для MariaDB](quickstart-create-mariadb-server-database-using-azure-cli.md).
 
[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](../../includes/azure-cli-prepare-your-environment-no-header.md)]

- Для работы с этой статьей требуется версия 2,0 или более поздняя Azure CLI. Если вы используете Azure Cloud Shell, последняя версия уже установлена.


## <a name="restart-the-server"></a>Перезагрузите сервер.

Перезапустите сервер с помощью следующей команды:

```azurecli-interactive
az mariadb server restart --name mydemoserver --resource-group myresourcegroup
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о [настройке параметров в базе данных Azure для MariaDB](howto-configure-server-parameters-cli.md)
