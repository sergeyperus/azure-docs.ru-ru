---
title: Синтаксис и выражения шаблона
description: Описывает декларативный синтаксис JSON для шаблонов Azure Resource Manager.
ms.topic: conceptual
ms.date: 03/17/2020
ms.openlocfilehash: baddedae1b918502e579d2ed230e0779960f45e7
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2020
ms.locfileid: "82203834"
---
# <a name="syntax-and-expressions-in-azure-resource-manager-templates"></a>Синтаксис и выражения в шаблонах Azure Resource Manager

Базовый синтаксис шаблона — это JSON. Однако можно использовать выражения для расширения значений JSON, доступных в шаблоне.  Выражения начинаются и заканчиваются квадратными скобками: `[` и `]` соответственно. Значение выражения вычисляется при развертывании шаблона. Выражение может возвращать строку, целое число, логическое значение, массив или объект.

Выражение шаблона не может содержать более 24 576 символов.

## <a name="use-functions"></a>Использование функций

Azure Resource Manager предоставляет [функции](template-functions.md) , которые можно использовать в шаблоне. В следующем примере показано выражение, использующее функцию в значении по умолчанию для параметра:

```json
"parameters": {
  "location": {
    "type": "string",
    "defaultValue": "[resourceGroup().location]"
  }
},
```

В выражении синтаксис `resourceGroup()` вызывает одну из функций, которые диспетчер ресурсов предоставляет для использования в шаблоне. В этом случае это функция [resourceGroup](template-functions-resource.md#resourcegroup) . Как и в языке JavaScript, вызовы функций форматируются так: `functionName(arg1,arg2,arg3)`. Синтаксис `.location` получает одно свойство из объекта, возвращаемого этой функцией.

Функции шаблонов и их параметры зависят от регистра. Например, Resource Manager одинаково преобразует **variables('var1')** и **VARIABLES('VAR1')**. При вычислении функция сохранит регистр, если его изменение не является ее явным предназначением (например, функции toUpper и toLower). Некоторые типы ресурсов могут иметь требования к регистру, которые отделены от того, как оцениваются функции.

Чтобы передать строковое значение в качестве параметра функции, используйте одинарные кавычки.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]"
```

Большинство функций работают одинаково при развертывании в группе ресурсов, подписке, группе управления или клиенте. Следующие функции имеют ограничения в зависимости от области действия:

* [resourceGroup](template-functions-resource.md#resourcegroup) — может использоваться только в развертываниях для группы ресурсов.
* [resourceId](template-functions-resource.md#resourceid) — может использоваться в любой области, но допустимые параметры изменяются в зависимости от области.
* [Подписка](template-functions-resource.md#subscription) — может использоваться только в развертываниях для группы ресурсов или подписки.

## <a name="escape-characters"></a>Escape-символы

Чтобы литеральная строка начинались с левой квадратной скобки `[` и заканчиваться правой квадратной скобкой `]` , но не интерпретировать ее как выражение, добавьте лишнюю скобку, чтобы начать строку с `[[` . Например, переменная:

```json
"demoVar1": "[[test value]"
```

Разрешается в `[test value]` .

Однако если литеральная строка не заканчивается квадратной скобкой, не нужно заключать первую квадратную скобку. Например, переменная:

```json
"demoVar2": "[test] value"
```

Разрешается в `[test] value` .

Для экранирования двойных кавычек в выражении, например для добавления объекта JSON в шаблон, используйте обратную косую черту.

```json
"tags": {
    "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
},
```

При передаче значений параметров использование escape-символов зависит от того, где указано значение параметра. Если в шаблоне задано значение по умолчанию, то требуется закрывающая левая скобка.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "demoParam1":{
            "type": "string",
            "defaultValue": "[[test value]"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput": {
            "type": "string",
            "value": "[parameters('demoParam1')]"
        }
    }
}
```

Если используется значение по умолчанию, шаблон возвращает `[test value]` .

Однако если передать значение параметра через командную строку, символы будут интерпретироваться буквально. Развертывание предыдущего шаблона с помощью:

```azurepowershell
New-AzResourceGroupDeployment -ResourceGroupName demoGroup -TemplateFile azuredeploy.json -demoParam1 "[[test value]"
```

Возвращает `[[test value]`. Вместо этого используйте:

```azurepowershell
New-AzResourceGroupDeployment -ResourceGroupName demoGroup -TemplateFile azuredeploy.json -demoParam1 "[test value]"
```

То же самое форматирование применяется при передаче значений из файла параметров. Символы обрабатываются буквально. При использовании с предыдущим шаблоном следующий файл параметров возвращает `[test value]` :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "demoParam1": {
            "value": "[test value]"
        }
   }
}
```

## <a name="null-values"></a>Значения NULL

Чтобы установить свойство в значение null, можно использовать **значение NULL** или **[JSON (' null ')]**. [Функция JSON](template-functions-object.md#json) возвращает пустой объект, если `null` в качестве параметра указано значение. В обоих случаях диспетчер ресурсов шаблоны обрабатывают его так, как если бы свойство не присутствовало.

```json
"stringValue": null,
"objectValue": "[json('null')]"
```

## <a name="next-steps"></a>Дальнейшие действия

* Полный список функций шаблонов см. в статье [Функции шаблонов диспетчера ресурсов Azure](template-functions.md).
* Дополнительные сведения о файлах шаблонов см. [в разделе сведения о структуре и синтаксисе шаблонов Azure Resource Manager](template-syntax.md).
