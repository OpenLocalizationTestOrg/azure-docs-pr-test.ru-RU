---
title: "aaaDeactivate и удалять устройства серии StorSimple 8000 | Документы Microsoft"
description: "Описывает способ tooremove устройство StorSimple из службы, сначала отключить его, а затем удаляет его."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>Отключение и удаление устройства StorSimple

## <a name="overview"></a>Обзор

В этой статье описывается как toodeactivate и удалить устройство StorSimple, подключенный tooa службы диспетчера StorSimple устройство. руководство Hello в данной статье применяется только устройств серии 8000 tooStorSimple, включая hello приложениями облака Storsimple. Если вы используете StorSimple Virtual Array, зарегистрироваться слишком[отключить и удалить StorSimple Virtual Array](storsimple-virtual-array-deactivate-and-delete-device.md).

Деактивация разрывает подключение hello hello устройства к соответствующей службы диспетчера StorSimple устройство hello. Вы можете tootake устройство StorSimple из службы (например, в том случае, если замены или обновления устройства или если вы больше не используете StorSimple). В этом случае необходимо toodeactivate hello устройства, прежде чем удалять его.

При деактивации устройства все данные, хранящиеся локально на устройстве hello больше не доступен. Может быть восстановлена только hello данные, связанные с устройством hello, хранящиеся в облаке hello.

> [!WARNING]
> Отключение является НЕОБРАТИМОЙ операцией. Деактивированное устройство нельзя зарегистрировать с hello службы диспетчера StorSimple устройство, если он не является по умолчанию toofactory.
>
> Hello сброса процесс приводит к удалению всех данных hello, которые хранились локально на устройстве. Таким образом необходимо создать облачный моментальный снимок всех данных перед отключением устройства. Этот моментальный снимок облака позволяет toorecover все hello данных в дальнейшем.

После изучения этого учебника вы сможете сделать следующее.

* Деактивировать устройство и удалить данные hello.
* Деактивировать устройство и обеспечить сохранность данных hello.

> [!NOTE]
> Перед отключением физического или облачного устройства StorSimple удалите зависящие от него клиенты и узлы или прекратите их работу.


## <a name="deactivate-and-delete-data"></a>Отключение и удаление данных

Если полностью удалить устройство hello и tooretain hello данные на устройстве hello не нужно, выполните следующие шаги hello.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello устройство и удалить hello данных

1. Перед отключением устройства вы и необходимо удалить все hello тома контейнеры (hello томов) связанные с устройством hello. Контейнеры томов можно удалить только после удаления hello связанные резервные копии.

    > [!NOTE]
    > Перед отключением физических устройств StorSimple или облачному устройству, убедитесь, что hello из контейнера томов hello удалены фактически данные будут удалены с устройства hello. Вы можете отслеживать диаграммы потребления hello облака, а если удалить из-за hello резервных копий, которые вы удалили использование облака hello, то вы можете перейти toodeactivate hello устройства. При отключении hello устройство перед спад происходит, hello данных оказались в учетной записи хранения hello и начисляемые расходов.

2. Деактивировать устройство hello следующим образом:
   
   1. Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**. В hello **устройств** колонки, hello выберите устройство, нужно toodeactivate, щелкните правой кнопкой мыши и выберите команду **деактивировать**.

        ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. В hello **деактивировать** колонки, введите имя tooconfirm hello устройства и нажмите кнопку **деактивировать**. Hello отключить начинается процесс и занимает несколько минут toocomplete.

        ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. После деактивации можно полностью удалить устройство hello. При удалении устройства удаляется из списка hello службы toohello подключенных устройств. Hello службы могут больше не сможете управлять hello удалить устройство. Используйте следующие шаги toodelete hello устройства hello.
   
   1. Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**. В hello **устройств** колонки, выберите hello деактивировать устройство, нужно toodelete, щелкните правой кнопкой мыши и выберите команду **удалить**.

        ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. В hello **удаление** колонки, введите имя tooconfirm hello устройства и нажмите кнопку **удалить**. Удаление Hello занимает несколько минут toocomplete.

        ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. После успешного завершения удаления hello пользователь получает уведомление. Список устройств Hello также обновляет tooreflect hello удаления.

## <a name="deactivate-and-retain-data"></a>Отключение и сохранение данных

Если интересуют удалением hello устройства, но данные tooretain hello, после чего завершите hello следующие шаги:

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate устройство и обеспечить сохранность данных hello
1. Деактивировать устройство hello. Здравствуйте, все контейнеры томов и моментальные снимки hello hello устройства остаются.
   
   1. Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**. В hello **устройств** колонки, hello выберите устройство, нужно toodeactivate, щелкните правой кнопкой мыши и выберите команду **деактивировать**.

         ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. В hello **деактивировать** колонки, введите имя tooconfirm hello устройства и нажмите кнопку **деактивировать**. Hello отключить начинается процесс и занимает несколько минут toocomplete.

         ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. Теперь можно выполнить переход hello контейнеры томов и моментальные снимки связанные hello. Для процедур go слишком[отработки отказа и аварийного восстановления для устройства StorSimple](storsimple-8000-device-failover-disaster-recovery.md).
3. После деактивации и отработки отказа можно полностью удалить устройство hello. При удалении устройства удаляется из списка hello службы toohello подключенных устройств. Hello службы могут больше не сможете управлять hello удалить устройство. устройство toodelete hello, полный hello, следующие шаги:
   
   1. Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**. В hello **устройств** колонки, выберите hello деактивировать устройство, нужно toodelete, щелкните правой кнопкой мыши и выберите команду **удалить**.

       ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. В hello **удаление** колонки, введите имя tooconfirm hello устройства и нажмите кнопку **удалить**. Удаление Hello занимает несколько минут toocomplete.

       ![Отключение устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. После успешного завершения удаления hello пользователь получает уведомление. Список устройств Hello также обновляет tooreflect hello удаления.

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>Отключение и удаление облачного устройства

Для устройства StorSimple облака деактивации из портала hello освобождает и удаляет hello виртуальной машины и hello ресурсы, созданные во время его инициализации. После деактивации устройство облака hello, он не может быть восстановлена tooits предыдущее состояние.

![Отключение облачного устройства StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

Деактивация результаты в hello, следующие действия:

* Hello устройство StorSimple облака выводится из эксплуатации hello.
* удаляется Hello виртуальную машину для hello облачных устройств StorSimple.
* диск ОС Hello и дисков данных, созданных для hello облачных устройств StorSimple, удаляются.
* Hello размещенной службы или виртуальной сети, созданные во время инициализации сохраняются. Если вы их не используете их, удалите их вручную.
* Сохраняются облачные моментальные снимки, созданные hello облачных устройств StorSimple.

После деактивации устройство облака hello, его можно удалить из списка устройств hello. Выберите hello деактивации устройства, щелкните правой кнопкой мыши и выберите команду **удалить**. StorSimple уведомит после hello устройство удаляется и hello список обновлений устройств.

## <a name="next-steps"></a>Дальнейшие действия

* toorestore Здравствуйте значения по умолчанию toofactory деактивированное устройство, перейдите в слишком[сбросить параметры по умолчанию hello устройства toofactory](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Чтобы получить техническую поддержку, [обратитесь в службу поддержки Майкрософт](storsimple-8000-contact-microsoft-support.md).
* Дополнительные сведения о toolearn как hello toouse службы диспетчера StorSimple устройство go слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).

