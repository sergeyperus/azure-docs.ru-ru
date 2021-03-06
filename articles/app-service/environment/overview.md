---
title: Обзор Среда службы приложений
description: Общие сведения о Среда службы приложений
author: ccompy
ms.assetid: 3d37f007-d6f2-4e47-8e26-b844e47ee919
ms.topic: article
ms.date: 11/16/2020
ms.author: ccompy
ms.custom: seodec18
ms.openlocfilehash: fbc498fcd654d16936c2548528e2600be68a2ad9
ms.sourcegitcommit: 8e7316bd4c4991de62ea485adca30065e5b86c67
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2020
ms.locfileid: "94663838"
---
# <a name="app-service-environment-overview"></a>Обзор Среда службы приложений 

> [!NOTE]
> Эта статья относится к Среда службы приложений v3 (Предварительная версия)
> 

Среда службы приложений Azure — это компонент службы приложений Azure, предоставляющий полностью изолированную и выделенную среду для безопасного выполнения приложений службы приложений в большом масштабе. Эта возможность позволяет разместить:

- веб-приложения Windows;
- веб-приложения Linux;
- контейнеры Docker;
- Функции

Среды службы приложений (ASE) подходят для рабочих нагрузок приложений, требующих выполнения указанных ниже условий:

- Высокое масштабирование.
- изоляция и безопасный доступ к сети;
- высокий уровень использования памяти.
- Высокий уровень запросов в секунду (RPS). Вы можете сделать несколько среды ASE в одном регионе Azure или в нескольких регионах Azure. Эта гибкость делает среды ASE идеальным решением для горизонтального масштабирования приложений без отслеживания состояния с высоким требованием RPS.

ASE ведущие приложения только одного клиента и делают это в одном из своих виртуальных сетей. Клиенты могут детально управлять входящим и исходящим сетевым трафиком приложений, а приложения — создавать высокоскоростные безопасные подключения к локальным корпоративным ресурсам через VPN.

ASEv3 имеет собственную ценовую категорию, изолированную v2.
Среда службы приложений v3 предоставляет окружающую защиту приложений в подсети сети и предоставляет собственное частное развертывание службы приложений Azure.
Несколько сред ASE можно использовать для горизонтального масштабирования. Приложения, работающие в средах ASE, могут получать доступ через такие устройства, как брандмауэр веб-приложений (WAF). Дополнительные сведения см. в статье о брандмауэре веб-приложения (WAF).

## <a name="usage-scenarios"></a>Сценарии использования

Среда службы приложений имеет много вариантов использования, в том числе:

- Внутренние бизнес-приложения
- Приложения, которым требуется более 30 экземпляров ASP
- Система с одним клиентом для удовлетворения требований внутреннего соответствия или безопасности
- Размещение приложений, изолированных от сети
- Многоуровневые приложения

Существует ряд сетевых функций, которые позволяют приложениям в службе многопользовательских приложений обращаться к изолированным сетевым ресурсам или быть изолированными от сети. Эти функции включены на уровне приложения.  В ASE нет дополнительной настройки приложений для их включения в виртуальную сеть. Приложения развертываются в сетевой изолированной среде, которая уже находится в виртуальной сети. В верхней части ASE, в которой размещаются изолированные сетевые приложения, это также единственная система с одним клиентом. Нет других клиентов, использующих ASE. Если вам действительно нужна полная история изоляции, вы также можете развернуть ASE на выделенном оборудовании. Между размещением изолированного сетевого приложения, одним клиентом и возможностью 

## <a name="dedicated-environment"></a>Выделенная среда
ASE выделяется исключительно для одной подписки и может размещать экземпляры плана службы приложений 200. Это может быть от 100 экземпляров в одном плане службы приложений до 100 одноэкземплярных планов службы приложений, а также все, что находится между ними.

ASE состоит из внешних интерфейсов и рабочих ролей. Внешние интерфейсы отвечают за завершение HTTP/HTTPS, а также за автоматическую балансировку нагрузки запросов приложения в среде ASE. Внешние интерфейсы автоматически добавляются по мере развертывания планов службы приложений в среде ASE.

Рабочие роли — это роли, в которых размещаются пользовательские приложения. Они доступны в трех фиксированных размерах:

- 2 виртуальных ЦП/8 ГБ ОЗУ
- Четыре виртуальных ЦП/16 ГБ ОЗУ
- Восемь виртуальных ЦП/32 ГБ ОЗУ

Клиентам не нужно управлять внешними интерфейсами и сотрудниками. Все инфраструктуры автоматически. Так как планы службы приложений создаются и развертываются в среде ASE, необходимая инфраструктура добавляется или удаляется соответствующим образом.

За изолированные экземпляры плана службы приложений v2 взимается плата. Если в вашей ASE нет планов службы приложений, плата взимается так, как если бы у вас был один план службы приложений с одним экземпляром двух основных рабочих ролей.

## <a name="virtual-network-support"></a>Поддержка виртуальной сети
Функция ASE позволяет развернуть службу приложений Azure непосредственно в виртуальной сети Azure Resource Manager клиента. ASE всегда существует в подсети виртуальной сети. можно использовать средства безопасности виртуальных сетей для управления как входящими, так и исходящими подключениями в сети для приложений.

Группы безопасности сети ограничивают входящие сетевые подключения для подсети, в которой находится среда ASE. Это позволяет запускать приложения за вышестоящими устройствами и службами, например брандмауэрами веб-приложений и поставщиками SaaS сети.

Приложениям также часто требуется доступ к корпоративным ресурсам, таким как внутренние базы данных и веб-службы. При развертывании ASE в виртуальной сети с VPN-подключением к локальной сети приложения в ASE смогут получить доступ к локальным ресурсам. При этом не играет роли тип VPN-подключения ("сеть — сеть" или Azure ExpressRoute).

## <a name="preview"></a>Предварительный просмотр
Среда службы приложений v3 находится в общедоступной предварительной версии.  Некоторые функции добавляются во время выполнения предварительной версии. К текущим ограничениям ASEv3 относятся:

- Невозможность масштабирования плана службы приложений за пять экземпляров
- Невозможность получения контейнера из частного реестра
- Невозможность неподдерживаемых функций службы приложений для прохождения через виртуальную сеть клиента
- Отсутствует внешняя модель развертывания с конечной точкой, доступной в Интернете
- Нет поддержки командной строки (AZ CLI и PowerShell)
- Отсутствует возможность обновления с ASEv2 до ASEv3
- Без поддержки FTP
- Некоторые функции службы приложений не поддерживаются в клиентской виртуальной сети. Резервное копирование и восстановление, Key Vault ссылок в параметрах приложения с помощью закрытого реестра контейнеров, а ведение журнала диагностики в хранилище не будет работать с конечными точками службы или частными конечными точками.
    
### <a name="asev3-preview-architecture"></a>Архитектура предварительной версии ASEv3
В ASEv3 Preview ASE будет использовать частные конечные точки для поддержки входящего трафика. Частная конечная точка будет заменена общедоступными подсистемами балансировки нагрузки. В предварительной версии ASE не имеет встроенной поддержки конечной точки, доступной в Интернете. Для такой цели можно добавить шлюз приложений. ASE требуются ресурсы в двух подсетях.  Входящий трафик будет проходить через закрытую конечную точку. Частная конечная точка может быть размещена в любой подсети, если она имеет доступный адрес, который может использоваться частными конечными точками.  Исходящая подсеть должна быть пустой и делегирована в Microsoft. Web/hostingEnvironments. При использовании ASE исходящая подсеть не может использоваться ни для чего еще.

При использовании ASEv3 в подсети ASE нет требований к входящему или исходящему сетевому подключению. Вы можете управлять трафиком с помощью групп безопасности сети и таблиц маршрутов. это повлияет только на трафик приложения. Не удаляйте закрытую конечную точку, связанную с ASE, так как это действие нельзя отменить. Частная конечная точка, используемая для ASE, используется для всех приложений в ASE. 
