---
author: alkohli
ms.service: storsimple
ms.topic: include
ms.date: 10/26/2018
ms.author: alkohli
ms.openlocfilehash: 746198f87e23cd7aca2a3177c23974917cb4b12a
ms.sourcegitcommit: a43a59e44c14d349d597c3d2fd2bc779989c71d7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "96027236"
---
#### <a name="to-create-a-new-service"></a>Создание новой службы

1. Войдите на [портал Azure](https://portal.azure.com/) с помощью данных своей учетной записи Майкрософт.

2. На портале Azure щелкните **Создать ресурс**, а затем в Marketplace выберите **See all** (Просмотреть все).

    ![Создание диспетчера устройств StorSimple](./media/storsimple-8000-create-new-service/createssdevman1.png)

    Найдите _физическое устройство StorSimple_. Выберите **Серия физического устройства StorSimple** и щелкните **Создать**. Кроме того, в портал Azure щелкните, **+** а затем в разделе **хранилище** выберите **серия физических устройств StorSimple**.

    ![Создание StorSimple Device Manager 2](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. В колонке **диспетчера устройств StorSimple** выполните следующие действия.

   1. В поле **Имя ресурса** укажите уникальное имя для службы. Здесь необходимо указать понятное имя, пригодное для идентификации службы. Имя может содержать от 2 до 50 символов, среди которых могут быть буквы, цифры и дефисы. Имя должно начинаться и заканчиваться буквой или цифрой.

   2. Выберите **Подписка** в раскрывающемся списке. Подписка привязана к учетной записи для выставления счетов. Это поле отсутствует, если у вас имеется только одна подписка.

   3. **Группа ресурсов** — **создайте** группу ресурсов или выберите **имеющуюся**. Дополнительные сведения см. в статье [Рекомендации по группам ресурсов Azure](../articles/azure-resource-manager/management/manage-resource-groups-portal.md).

   4. Введите **Местоположение** для службы. В общем, выберите расположение, ближайшее к географическому региону, в котором вы хотите развернуть устройство. Кроме того, необходимо учитывать следующее:

      * Если у вас есть рабочие нагрузки в Azure, которые также будут развернуты на устройстве StorSimple, используйте этот центр обработки данных.
      * Служба диспетчера устройств StorSimple и служба хранилища Azure могут находиться в разных расположениях. В этом случае следует отдельно создать диспетчер устройств StorSimple и учетную запись хранения Azure. Чтобы создать учетную запись хранения Azure, перейдите в службу хранилища Azure на портале Azure и следуйте указаниям из раздела [Создайте учетную запись хранения](../articles/storage/common/storage-account-create.md). Создав учетную запись, добавьте ее в службу диспетчера устройств StorSimple. Для этого выполните действия, описанные в разделе [Настройка новой учетной записи хранения для службы](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).

   5. Установите флажок **Создать новую учетную запись хранения** для автоматического создания учетной записи хранения вместе со службой. Укажите имя для этой учетной записи хранения. Если требуется хранить данные в другом расположении, снимите этот флажок.

   6. Установите флажок **Закрепить на панели мониторинга**, если вам нужен быстрый доступ к этой службе с панели мониторинга.

   7. Щелкните **Создать**, чтобы создать диспетчер устройств StorSimple.

       ![Создание StorSimple Device Manager 3](./media/storsimple-8000-create-new-service/createssdevman2.png)

Создание службы займет несколько минут. После успешного создания службы вы получите уведомление и откроется новая колонка службы.

![Создание StorSimple Device Manager 4](./media/storsimple-8000-create-new-service/createssdevman5.png)