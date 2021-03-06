---
title: Развертывание модели в службах Azure Analysis Services с помощью Visual Studio | Документация Майкрософт
description: Сведения о развертывании табличной модели на сервере служб Azure Analysis Services с помощью Visual Studio.
author: minewiskan
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 05/19/2020
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 45ea75b65e75f9bac4d6d4839ffe7fa095e3b25d
ms.sourcegitcommit: 2c586a0fbec6968205f3dc2af20e89e01f1b74b5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/14/2020
ms.locfileid: "92018782"
---
# <a name="deploy-a-model-from-visual-studio"></a>Развертывание модели из Visual Studio

После создания сервера в подписке Azure все готово к развертыванию на нем базы данных табличной модели. Visual Studio можно использовать совместно с проектами Analysis Services для создания и развертывания проекта табличной модели, над которым вы работаете. 

## <a name="prerequisites"></a>Предварительные требования

Для начала работы необходимы перечисленные ниже компоненты и данные.

* **Сервер Analysis Services** в Azure. См. дополнительные сведения о [создании сервера Azure Analysis Services](analysis-services-create-server.md).
* **Проект табличной модели** в Visual Studio или существующая табличная модель на уровне совместимости 1200 и выше. Не создавали такую модель ранее? Обратитесь к [руководству по табличному моделированию продаж в Интернете Adventure Works](/analysis-services/tutorial-tabular-1400/as-adventure-works-tutorial).
* **Локальный шлюз**. Если один или несколько источников данных находятся в локальной сети вашей организации, необходимо установить [локальный шлюз данных](analysis-services-gateway.md). Этот шлюз необходим для подключения сервера в облаке к локальным источникам данных для обработки и обновления данных в модели.

> [!TIP]
> Перед развертыванием убедитесь, что можете обрабатывать данные в таблицах. В Visual Studio последовательно выберите элементы **Модель** > **Обработать** > **Обработать все**. Если обработка завершается сбоем, вы не сможете выполнить развертывание.
> 
> 

## <a name="get-the-server-name"></a>Получение имени сервера

На **портале Azure** выберите сервер, а затем щелкните **Обзор** > **Имя сервера** и скопируйте имя сервера.
   
![Получение имени сервера в Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)

## <a name="to-deploy-from-visual-studio"></a>Развертывание из Visual Studio

1. В Visual Studio выберите **Обозреватель решений**, щелкните правой кнопкой мыши проект и выберите пункт **Свойства**. Затем в разделе **Развертывание** > **Сервер** вставьте имя сервера.   
   
    ![Вставьте имя сервера в свойства сервера развертывания](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
2. В окне **Обозреватель решений** щелкните правой кнопкой мыши элемент **Свойства** и выберите команду **Развернуть**. Возможно, вам будет предложено войти в Azure.
   
    ![Развертывание на сервере](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    Состояние развертывания отображается в окне "Вывод" и в разделе "Развертывание".
   
    ![Состояния развертывания](./media/analysis-services-deploy/aas-deploy-status.png)

Это все.


## <a name="troubleshooting"></a>Устранение неполадок

Если при развертывании метаданных возникает ошибка, вероятная ее причина заключается в том, что Visual Studio не удалось подключиться к серверу. Убедитесь, что вы можете подключиться к серверу, используя SQL Server Management Studio. Убедитесь, что правильно указано свойство сервера развертывания для проекта.

Если возникает сбой развертывания на таблице, скорее всего, причина в том, что серверу не удалось подключиться к источнику данных. Если источник данных является локальным в сети организации, не забудьте установить [Локальный шлюз данных](analysis-services-gateway.md).

## <a name="next-steps"></a>Дальнейшие действия

После развертывания табличной модели на сервере к нему можно подключиться. К серверу можно [подключиться к с помощью SQL Server Management Studio (SSMS)](analysis-services-manage.md). Также вы можете [подключиться к серверу с помощью клиентского средства](analysis-services-connect.md), например Power BI, Power BI Desktop или Excel, и начать создавать отчеты.   

Подробнее о дополнительных методах развертывания см. в разделе [Развертывание решений табличной модели](/analysis-services/deployment/tabular-model-solution-deployment?view=azure-analysis-services-current).