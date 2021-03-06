---
title: Руководство. Масштабирование частного облака
description: В этом руководстве показано, как масштабировать частное облако Решения Azure VMware с помощью портала Azure.
ms.topic: tutorial
ms.date: 09/21/2020
ms.openlocfilehash: d49d973cc6d97280dc0c7ea6681f2602b871e1ba
ms.sourcegitcommit: 400f473e8aa6301539179d4b320ffbe7dfae42fe
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/28/2020
ms.locfileid: "92791245"
---
# <a name="tutorial-scale-an-azure-vmware-solution-private-cloud"></a>Руководство по Масштабирование частного облака Решения Azure VMware

Чтобы максимально эффективно работать с частным облаком Решения Azure VMware, масштабируйте кластеры и узлы в соответствии с запланированными рабочими нагрузками. Вы можете масштабировать кластеры и узлы в частном облаке в соответствии с рабочей нагрузкой приложения. Ограничения производительности и доступности для конкретных служб следует решать на индивидуальной основе. Ограничения количества кластеров и узлов см. в [описании частного облака](concepts-private-clouds-clusters.md).

В этом руководстве показано, как использовать портал Azure для таких целей:

> [!div class="checklist"]
> * добавление кластера в существующее частное облако;
> * добавление узлов в существующий кластер.

## <a name="prerequisites"></a>Предварительные требования

Частное облако для работы с этим учебником. Если вы еще не создали частное облако, воспользуйтесь [учебником по созданию частного облака](tutorial-create-private-cloud.md). Настройте сеть для своего частного облака VMware в Azure, чтобы развернуть необходимую виртуальную сеть.

## <a name="add-a-new-cluster"></a>Добавление нового кластера

1. На странице обзора существующего частного облака в разделе **Управление** щелкните **Масштабировать частное облако**. Затем щелкните **+ Добавить кластер**.

   :::image type="content" source="./media/tutorial-scale-private-cloud/ss2-select-add-cluster.png" alt-text="Добавление кластера" border="true":::

1. На странице **Добавление кластера** с помощью ползунка выберите нужное количество узлов. Щелкните **Сохранить**.

   :::image type="content" source="./media/tutorial-scale-private-cloud/ss3-configure-new-cluster.png" alt-text="На странице &quot;Добавление кластера&quot; с помощью ползунка выберите нужное количество узлов. Щелкните &quot;Сохранить&quot;." border="true":::

   Начнется развертывание нового кластера.

## <a name="scale-a-cluster"></a>Масштабировать кластер 

1. На странице обзора существующего частного облака щелкните **Масштабировать частное облако** , а затем щелкните значок карандаша, чтобы изменить кластер.

   :::image type="content" source="./media/tutorial-scale-private-cloud/ss4-select-scale-private-cloud-2.png" alt-text="Масштабирование частного облака на странице обзора" border="true":::

1. На странице **Изменение кластера** с помощью ползунка выберите нужное количество узлов. Щелкните **Сохранить**.

   :::image type="content" source="./media/tutorial-scale-private-cloud/ss5-scale-cluster.png" alt-text="На странице &quot;Изменение кластера&quot; с помощью ползунка выберите нужное количество узлов. Щелкните &quot;Сохранить&quot;." border="true":::

   Будет начато добавление узлов в кластер.

## <a name="next-steps"></a>Дальнейшие действия

Если вам требуется другое частное облако Решения Azure VMware, [создайте его](tutorial-create-private-cloud.md) с теми же предварительными требованиями к сети и ограничениями на количество кластеров и узлов.

<!-- LINKS - external-->

<!-- LINKS - internal -->
