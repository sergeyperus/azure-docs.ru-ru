---
title: Преобразование конфигураций в составные ресурсы для компонента State Configuration службы автоматизации Azure
description: Сведения о том, как преобразовать конфигурации в составные ресурсы для компонента State Configuration службы автоматизации Azure.
keywords: dsc,powershell,конфигурация,установка
services: automation
ms.service: automation
ms.subservice: dsc
author: mgreenegit
ms.author: migreene
ms.date: 08/08/2019
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 8c834caa2285135b7d39c440489b42c366418042
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2020
ms.locfileid: "86186475"
---
# <a name="convert-configurations-to-composite-resources"></a>Преобразование конфигураций в составные ресурсы

> Область применения: Windows PowerShell 5.1

Начав создавать собственные конфигурации, вы можете быстро подготовить сценарии для управления группами параметров.
Пример будет следующим:

- создание веб-службы;
- создание DNS-сервера;
- создание сервера SharePoint;
- настройка кластера SQL;
- управление параметрами брандмауэра;
- управление параметрами паролей.

Если вы желаете поделиться своей работой с другими, оформите свои конфигурации как пакет [составного ресурса](/powershell/scripting/dsc/resources/authoringresourcecomposite).
Создание составных ресурсов в первый раз может показаться неподъемной задачей.

> [!NOTE]
> В этой статье рассматривается решение, которое поддерживается сообществом разработчиков ПО с открытым кодом.
> Поддержка этого решения предоставляется только на форуме GitHub и не имеет отношения к корпорации Майкрософт.

## <a name="community-project-compositeresource"></a>Проект сообщества: CompositeResource

Для решения этой задачи было создано поддерживаемое сообществом решение с именем [CompositeResource](https://github.com/microsoft/compositeresource).

CompositeResource автоматизирует процесс создания нового модуля на основе конфигурации.
Для начала вам нужно вызвать скрипт конфигурации [с использованием точки](https://devblogs.microsoft.com/scripting/how-to-reuse-windows-powershell-functions-in-scripts/) в рабочей станции или на сервере сборки, чтобы загрузить этот скрипт в память.
Далее вместо обычного запуска конфигурации для создания MOF-файла примените функцию из модуля CompositeResource для автоматического преобразования.
Этот командлет загрузит остальное содержимое конфигурации, получит список параметров и создаст новый модуль со всем необходимым.

Когда создание модуля завершится, увеличьте номер версии и добавьте заметки о выпуске. Это нужно делать каждый раз после внесения изменений и до публикации модуля в [репозиторий PowerShellGet](https://powershellexplained.com/2018-03-03-Powershell-Using-a-NuGet-server-for-a-PSRepository/?utm_source=blog&utm_medium=blog&utm_content=psscriptrepo).

Создав готовый модуль составного ресурса с нужной конфигурацией (или с несколькими конфигурациями), вы сможете применить его в [интерфейсе составного создания](./compose-configurationwithcompositeresources.md) в Azure или добавить в [скрипты конфигурации DSC](/powershell/scripting/dsc/configurations/configurations) для получения MOF-файлов, которые вы затем [отправите в службу автоматизации Azure](./tutorial-configure-servers-desired-state.md#create-and-upload-a-configuration-to-azure-automation).
Затем зарегистрируйте серверы [локально](./automation-dsc-onboarding.md#enable-physicalvirtual-linux-machines) или [в Azure](./automation-dsc-onboarding.md#enable-azure-vms) для получения конфигураций.
В последнем обновлении этого проекта предоставляются опубликованные [runbook](https://www.powershellgallery.com/packages?q=DscGallerySamples) для службы автоматизации Azure, которые позволяют автоматизировать процесс импорта конфигураций из коллекции PowerShell.

Чтобы испытать в работе наш процесс автоматизированного создания составных ресурсов для DSC, откройте [коллекцию PowerShell](https://www.powershellgallery.com/packages/compositeresource/) и скачайте решение или щелкните ссылку "Project Site" (Сайт проекта) для перехода к [документации](https://github.com/microsoft/compositeresource).

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о DSC для PowerShell см. в статье [Общие сведения о службе настройки требуемого состояния Windows PowerShell](/powershell/scripting/dsc/overview/overview).
- Сведения о ресурсах для PowerShell DSC см. в статье [Ресурсы DSC](/powershell/scripting/dsc/resources/resources).
- Дополнительные сведения см. в статье [Настройка локального диспетчера конфигураций](/powershell/scripting/dsc/managing-nodes/metaconfig).
