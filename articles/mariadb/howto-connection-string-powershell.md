---
title: Создание строки подключения с помощью PowerShell в Базе данных Azure для MariaDB
description: В этой статье приводится пример скрипта Azure PowerShell для создания строки подключения к Базе данных Azure для MariaDB.
author: savjani
ms.author: pariks
ms.service: mariadb
ms.custom: mvc, devx-track-azurepowershell
ms.topic: how-to
ms.date: 8/5/2020
ms.openlocfilehash: 9dee109c701d3760c93f39e639dcfd7cae07b595
ms.sourcegitcommit: 6ab718e1be2767db2605eeebe974ee9e2c07022b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/12/2020
ms.locfileid: "94538059"
---
# <a name="how-to-generate-an-azure-database-for-mariadb-connection-string-with-powershell"></a>Как создать строку подключения к Базе данных Azure для MariaDB с помощью PowerShell

В этой статье описывается, как создать строку подключения для сервера Базы данных Azure для MariaDB. Строку подключения можно использовать для подключения к Базе данных Azure для MariaDB из множества различных приложений.

## <a name="requirements"></a>Требования

В качестве отправной точки в этой статье используются ресурсы, созданные в соответствии со следующим руководством:

* [Краткое руководство. Создание сервера Базы данных Azure для MariaDB с помощью PowerShell](quickstart-create-mariadb-server-database-using-azure-powershell.md)

## <a name="get-the-connection-string"></a>Получение строки подключения

Командлет `Get-AzMariaDbConnectionString` используется для создания строки подключения, позволяющей приложениям подключаться к Базе данных Azure для MariaDB. В примере ниже возвращается строка подключения для клиента PHP от **mydemoserver**.

```azurepowershell-interactive
Get-AzMariaDbConnectionString -Client PHP -Name mydemoserver -ResourceGroupName myresourcegroup
```

```Output
$con=mysqli_init();mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL); mysqli_real_connect($con, "mydemoserver.mariadb.database.azure.com", "myadmin@mydemoserver", {your_password}, {your_database}, 3306);
```

Допустимые значения для параметра `Client` включают следующие:

* ADO&#46;NET
* JDBC
* Node.js
* PHP
* Python
* Ruby
* WebApp

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Настройка параметров сервера Базы данных Azure для MariaDB с помощью PowerShell](howto-configure-server-parameters-using-powershell.md)
