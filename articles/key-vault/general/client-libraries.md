---
title: Клиентские библиотеки для Azure Key Vault | Документация Майкрософт
description: Клиентские библиотеки для Azure Key Vault
services: key-vault
author: msmbaldwin
tags: azure-resource-manager
ms.service: key-vault
ms.subservice: general
ms.topic: tutorial
ms.date: 08/14/2020
ms.author: mbaldwin
ms.openlocfilehash: 2c48917e7205bca03380267c1c97469acc245fa6
ms.sourcegitcommit: d479ad7ae4b6c2c416049cb0e0221ce15470acf6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2020
ms.locfileid: "91628033"
---
# <a name="client-libraries-for-azure-key-vault"></a>Клиентские библиотеки для Azure Key Vault

Клиентские библиотеки для Azure Key Vault обеспечивают программный доступ к функциям Key Vault из кода на различных языках, включая .NET, Python, Java и JavaScript.

## <a name="client-libraries-per-language-and-object"></a>Клиентские библиотеки для конкретных языков и объектов

Каждый пакет SDK включает отдельные клиентские библиотеки для хранилища ключей, секретов, ключей и сертификатов, как описано в таблице ниже.

| Язык | Секреты | Ключи | Сертификаты | Хранилище ключей (плоскость управления)
|--|--|--|--|
| .NET | - [Справочник по API](/dotnet/api/azure.security.keyvault.secrets?view=azure-dotnet)<br>- [Пакет NuGet](https://www.nuget.org/packages/Azure.Security.KeyVault.Secrets/)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Azure.Security.KeyVault.Secrets)<br>- [Краткое руководство](../secrets/quick-create-net.md) | - [Справочник по API](/dotnet/api/azure.security.keyvault.keys?view=azure-dotnet)<br>- [Пакет NuGet](https://www.nuget.org/packages/Azure.Security.KeyVault.Keys/)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Azure.Security.KeyVault.Keys) | - [Справочник по API](/dotnet/api/azure.security.keyvault.certificates?view=azure-dotnet)<br>- [Пакет NuGet](https://www.nuget.org/packages/Azure.Security.KeyVault.Certificates/)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Azure.Security.KeyVault.Certificates) | - [Справочник по API](/dotnet/api/microsoft.azure.management.keyvault?view=azure-dotnet)<br>- [Пакет NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault/)<br> - [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/keyvault/Microsoft.Azure.Management.KeyVault)|
| Python| - [Справочник по API](/python/api/overview/azure/keyvault-secrets-readme?view=azure-python)<br>- [Пакет PyPi](https://pypi.org/project/azure-keyvault-secrets/)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/keyvault/azure-keyvault-secrets)<br>- [Краткое руководство](../secrets/quick-create-python.md) |- [Справочник по API](/python/api/overview/azure/keyvault-keys-readme?view=azure-python)<br>- [Пакет PyPi](https://pypi.org/project/azure-keyvault-keys/)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/keyvault/azure-keyvault-keys)<br>- [Краткое руководство](../keys/quick-create-python.md) | - [Справочник по API](/python/api/overview/azure/keyvault-certificates-readme?view=azure-python)<br>- [Пакет PyPi](https://pypi.org/project/azure-keyvault-certificates/)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/keyvault/azure-keyvault-certificates)<br>- [Краткое руководство](../certificates/quick-create-python.md) | - [Справочник по API](/python/api/azure-mgmt-keyvault/azure.mgmt.keyvault?view=azure-python)<br> - [Пакет PyPi](https://pypi.org/project/azure-mgmt-keyvault/)<br> - [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/keyvault/azure-mgmt-keyvault)|
| Java | - [Справочник по API](https://azuresdkdocs.blob.core.windows.net/$web/java/azure-security-keyvault-secrets/4.2.0/index.html)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/keyvault/azure-security-keyvault-secrets)<br>- [Краткое руководство](../secrets/quick-create-java.md) |- [Справочник по API](https://azuresdkdocs.blob.core.windows.net/$web/java/azure-security-keyvault-keys/4.2.0/index.html)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/keyvault/azure-security-keyvault-keys) | - [Справочник по API](https://azuresdkdocs.blob.core.windows.net/$web/java/azure-security-keyvault-certificates/4.1.0/index.html)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/keyvault/azure-security-keyvault-certificates) |- [Справочник по API](/java/api/com.microsoft.azure.management.keyvault?view=azure-java-stable)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/keyvault/mgmt-v2016_10_01)|
| Node.js | - [Справочник по API](/javascript/api/@azure/keyvault-secrets/?view=azure-node-latest)<br>- [Пакет npm](https://www.npmjs.com/package/@azure/keyvault-secrest)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/keyvault/keyvault-secrets)<br>- [Краткое руководство](../secrets/quick-create-node.md) |- [Справочник по API](/javascript/api/@azure/keyvault-keys/?view=azure-node-latest)<br>- [Пакет npm](https://www.npmjs.com/package/@azure/keyvault-keys)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/keyvault/keyvault-keys)| - [Справочник по API](/javascript/api/@azure/keyvault-certificates/?view=azure-node-latest)<br>- [Пакет npm](https://www.npmjs.com/package/@azure/keyvault-certificates)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/keyvault/keyvault-certificates) |  - [Справочник по API](/javascript/api/@azure/arm-keyvault/?view=azure-node-latest)<br>- [Пакет npm](https://www.npmjs.com/package/@azure/arm-keyvault)<br>- [Исходный код библиотеки](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/keyvault/arm-keyvault)

## <a name="next-steps"></a>Дальнейшие действия

- См. [руководство разработчика Azure Key Vault](developers-guide.md).
- См. дополнительные сведения о [проверке подлинности в Key Vault](authentication.md).
- См. дополнительные сведения о [защите доступа к Key Vault](secure-your-key-vault.md)
