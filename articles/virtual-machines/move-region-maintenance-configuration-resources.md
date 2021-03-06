---
title: Перемещение ресурсов, связанных с конфигурацией обслуживания, в другой регион
description: Сведения о перемещении ресурсов, связанных с конфигурацией обслуживания виртуальных машин, в другой регион Azure
author: shants123
ms.service: virtual-machines
ms.topic: how-to
ms.date: 03/04/2020
ms.author: shants
ms.openlocfilehash: 38532fba2be1fedd275ed2e7f9dfc1bf5752499d
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2020
ms.locfileid: "86501659"
---
# <a name="move-resources-in-a-maintenance-control-configuration-to-another-region"></a>Перемещение ресурсов в конфигурации управления обслуживанием в другой регион

Чтобы переместить ресурсы, связанные с конфигурацией управления обслуживанием, в другой регион Azure, следуйте этой статье. Может потребоваться переместить конфигурацию по ряду причин. Например, чтобы воспользоваться преимуществами нового региона, можно развернуть компоненты или службы, доступные в определенном регионе, в соответствии с требованиями к внутренней политике и управлению, а также в ответ на планирование ресурсов.

Управление обслуживанием с пользовательскими конфигурациями обслуживания позволяет управлять применением обновлений платформы к виртуальным машинам [Windows](./maintenance-control-cli.md?toc=/azure/virtual-machines/windows/toc.json&bc=/azure/virtual-machines/windows/breadcrumb/toc.json) и [Linux](./maintenance-control-cli.md?toc=%2Fazure%2Fvirtual-machines%2Flinux%2Ftoc.json&bc=%2Fazure%2Fvirtual-machines%2Flinux%2Fbreadcrumb%2Ftoc.json&view=azure-java-stable) , а также к выделенным узлам Azure. Существует несколько сценариев перемещения управления обслуживанием в разных регионах:

- Чтобы переместить ресурсы, связанные с конфигурацией обслуживания, но не самой конфигурацией, следуйте этой статье.
- Чтобы переместить конфигурацию управления обслуживанием, но не ресурсы, связанные с конфигурацией, выполните следующие [инструкции](move-region-maintenance-configuration.md).
- Чтобы переместить конфигурацию обслуживания и связанные с ней ресурсы, сначала выполните [эти инструкции](move-region-maintenance-configuration.md). Затем следуйте инструкциям в этой статье.

## <a name="prerequisites"></a>Предварительные требования

Перед началом перемещения ресурсов, связанных с конфигурацией управления обслуживанием, выполните следующие действия.

- Прежде чем начать, убедитесь, что перемещаемые ресурсы существуют в новом регионе.
- Проверьте конфигурации управления обслуживанием, связанные с виртуальными машинами Azure и выделенными узлами Azure, которые требуется переместить. Проверьте каждый ресурс по отдельности. В настоящее время нет способа получить конфигурации для нескольких ресурсов.
- При получении конфигураций для ресурса:
    - Убедитесь, что вы используете идентификатор подписки для учетной записи, а не идентификатор выделенного узла Azure.
    - CLI: параметр--выходной таблицы используется только для удобочитаемости и может быть удален или изменен.
    - PowerShell: параметр имени Format-Table используется только для удобочитаемости и может быть удален или изменен.
    - Если вы используете PowerShell, при попытке перечисления конфигураций для ресурса, у которого нет связанных конфигураций, возникает ошибка. Ошибка будет выглядеть примерно так: "сбой операции с состоянием:" не найдено ". Сведения: ошибка клиента 404: не найден для URL-адреса ".

    
## <a name="prepare-to-move"></a>Подготовка к переносу

1. Прежде чем начать, определите эти переменные. Мы предоставили пример для каждого из них.

    **Переменная** | **Сведения** | **Пример**
    --- | ---
    $subId | Идентификатор подписки, содержащей конфигурации обслуживания | "наш-Subscription-ID"
    $rsrcGroupName | Имя группы ресурсов (виртуальная машина Azure) | "Вмресаурцеграуп"
    $vmName | Имя ресурса виртуальной машины |  MyVM
    $adhRsrcGroupName |  Группа ресурсов (выделенные узлы) | "Хостресаурцеграуп"
    $adh | Выделенное имя узла | "Михост"
    $adhParentName | Имя родительского ресурса | HostGroup
    
2. Чтобы получить конфигурации обслуживания с помощью команды PowerShell [Get-азконфигуратионассигнмент](/powershell/module/az.maintenance/get-azconfigurationassignment?view=azps-3.5.0) , выполните следующие действия:

    - Для выделенных узлов Azure выполните:
        ```
        Get-AzConfigurationAssignment -ResourceGroupName $adhRsrcGroupName -ResourceName $adh -ResourceType hosts -ProviderName Microsoft.Compute -ResourceParentName $adhParentName -ResourceParentType hostGroups | Format-Table Name
        ```

    - Для виртуальных машин Azure выполните:

        ```
        Get-AzConfigurationAssignment -ResourceGroupName $rgName -ResourceName $vmName -ProviderName Microsoft.Compute -ResourceType virtualMachines | Format-Table Name
        ```
3. Чтобы получить конфигурации обслуживания с помощью команды CLI [AZ Maintenance](/cli/azure/ext/maintenance/maintenance/assignment?view=azure-cli-latest) :

    - Для выделенных узлов Azure:

        ```
        az maintenance assignment list --subscription $subId --resource-group $adhRsrcGroupName --resource-name $adh --resource-type hosts --provider-name Microsoft.Compute --resource-parent-name $adhParentName --resource-parent-type hostGroups --query "[].{HostResourceGroup:resourceGroup,ConfigName:name}" --output table
        ```

    - Для виртуальных машин Azure:

        ```
        az maintenance assignment list --subscription $subId --provider-name Microsoft.Compute --resource-group $rsrcGroupName --resource-name $vmName --resource-type virtualMachines --query "[].{HostResourceGroup:resourceGroup, ConfigName:name}" --output table
        ```


## <a name="move"></a>Переместить 

1. [Выполните эти инструкции](../site-recovery/azure-to-azure-tutorial-migrate.md?toc=/azure/virtual-machines/windows/toc.json&bc=/azure/virtual-machines/windows/breadcrumb/toc.json) , чтобы переместить виртуальные машины Azure в новый регион.
2. После перемещения ресурсов повторно примените конфигурации обслуживания к ресурсам в новом регионе в зависимости от того, были ли перемещены конфигурации обслуживания. Вы можете применить конфигурацию обслуживания к ресурсу с помощью [PowerShell](../virtual-machines/maintenance-control-powershell.md) или [CLI](../virtual-machines/maintenance-control-cli.md).


## <a name="verify-the-move"></a>Проверка перемещения

Проверьте ресурсы в новом регионе и проверьте связанные конфигурации для ресурсов в новом регионе. 

## <a name="clean-up-source-resources"></a>Очистка исходных ресурсов

После перемещения рассмотрите возможность удаления перемещенных ресурсов в исходном регионе.


## <a name="next-steps"></a>Дальнейшие действия

Если необходимо переместить конфигурации обслуживания, следуйте [этим инструкциям](move-region-maintenance-configuration.md) . 
