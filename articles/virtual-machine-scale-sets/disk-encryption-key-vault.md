---
title: Создание и настройка хранилища ключей для службы "Шифрование дисков Azure"
description: В этой статье описано, как создать и настроить хранилище ключей для использования со службой "Шифрование дисков Azure".
author: ju-shim
ms.author: jushiman
ms.topic: tutorial
ms.service: virtual-machine-scale-sets
ms.subservice: disks
ms.date: 10/10/2019
ms.reviewer: mimckitt
ms.custom: mimckitt
ms.openlocfilehash: acd2ae54d81fb508d5f8c02262cf8c2f0f071fb5
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "96016800"
---
# <a name="create-and-configure-a-key-vault-for-azure-disk-encryption"></a>Создание и настройка хранилища ключей для шифрования дисков Azure

Служба "Шифрование дисков Azure" использует Azure Key Vault, чтобы управлять секретами и ключами шифрования дисков и контролировать их использование.  Дополнительные сведения о хранилищах ключей см. в статье [Приступая к работе с Azure Key Vault](../key-vault/general/overview.md) и [Защита хранилища ключей](../key-vault/general/secure-your-key-vault.md).

Создание и настройка хранилища ключей для использования со службой шифрования дисков Azure состоит из трех этапов.

1. Создание группы ресурсов при необходимости.
2. Создание хранилища ключей. 
3. Установка политик расширенного доступа к хранилищу ключей.

Эти этапы продемонстрированы в следующих кратких руководствах.

При необходимости можно создать или импортировать ключ шифрования ключа (KEK).

## <a name="install-tools-and-connect-to-azure"></a>Установка средств и подключение к Azure

Действия, описанные в этой статье, можно выполнить с помощью [Azure CLI](/cli/azure/), [модуль Azure PowerShell Az](/powershell/azure/) или [портала Azure](https://portal.azure.com).

### <a name="connect-to-your-azure-account"></a>Подключение к учетной записи Azure

Перед использованием Azure CLI или Azure PowerShell необходимо сначала подключиться к подписке Azure. Для этого [войдите в систему с помощью Azure CLI](/cli/azure/authenticate-azure-cli?view=azure-cli-latest), [войдите в систему с помощью Azure PowerShell](/powershell/azure/authenticate-azureps?view=azps-2.5.0) или укажите учетные данные для портала Azure при появлении соответствующего запроса.

```azurecli-interactive
az login
```

```azurepowershell-interactive
Connect-AzAccount
```

[!INCLUDE [disk-encryption-key-vault](../../includes/disk-encryption-key-vault.md)]
 
## <a name="next-steps"></a>Дальнейшие действия

- [Общие сведения о шифровании дисков Azure](disk-encryption-overview.md)
- [Encrypt OS and attached data disks in a virtual machine scale set with the Azure CLI](disk-encryption-cli.md) (Шифрование ОС и подключенных дисков данных в масштабируемом наборе виртуальных машин с помощью Azure CLI)
- [Encrypt OS and attached data disks in a virtual machine scale set with Azure PowerShell](disk-encryption-powershell.md) (Шифрование ОС и подключенных дисков данных в масштабируемом наборе виртуальных машин с помощью Azure PowerShell)
