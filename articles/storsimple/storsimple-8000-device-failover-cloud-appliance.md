---
title: "aaaStorSimple перехода на другой ресурс tooa восстановления после сбоев облачных устройств StorSimple | Документы Microsoft"
description: "Дополнительные сведения об toofail по вашей tooa физического устройства серии StorSimple 8000 облачных устройств."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a>При сбое tooyour облачных устройств StorSimple

## <a name="overview"></a>Обзор

В данном учебнике требуется toofail hello действия над tooa физического устройства серии StorSimple 8000 устройство StorSimple облака при аварии. StorSimple использует данные hello устройства отработки отказа компонентов toomigrate из источника физического устройства в hello tooa центра обработки данных облака устройства, работающие в Azure. руководство Hello в этом учебнике применяется физических устройств серии tooStorSimple 8000 и облачных устройств под управлением версий программного обеспечения обновления 3 и более поздних версий.

toolearn Дополнительные сведения о отработки отказа устройства и как она используется toorecover после аварии, go слишком[отработки отказа и аварийного восстановления для устройства серии StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail на физическое устройство tooanother физическом устройстве StorSimple, перейдите в слишком[при сбое физических устройств StorSimple tooa](storsimple-8000-device-failover-physical-device.md). toofail над tooitself устройства go слишком[при сбое toohello же физических устройств StorSimple](storsimple-8000-device-failover-same-device.md).

## <a name="prerequisites"></a>Предварительные требования

- Убедитесь, можно ознакомиться с разделом hello рекомендации для обработки отказа устройства. Дополнительные сведения см. слишком[Общие рекомендации для обработки отказа устройства](storsimple-8000-device-failover-disaster-recovery.md).

- Перед началом этой процедуры нужно создать и настроить облачное устройство StorSimple. Если выполняется обновление 3 версии программного обеспечения или более поздней версии, рекомендуется использовать устройство 8020 облака для hello аварийного восстановления. модели 8020 Hello 64 ТБ и использует хранилище Premium. Дополнительные сведения см. слишком[развертывание и управление ими в StorSimple Appliance облака](storsimple-8000-cloud-appliance-u2.md).

## <a name="steps-toofail-over-tooa-cloud-appliance"></a>Toofail действия над tooa облачному устройству

Выполните hello после целевого действия toorestore hello устройства tooa облачному устройству StorSimple.

1.  Убедитесь, что нужные toofail через контейнера томов hello связаны облачные моментальные снимки. Дополнительные сведения см. слишком[резервные копии toocreate службы с помощью диспетчера устройств StorSimple](storsimple-8000-manage-backup-policies-u2.md).
2. Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**. В hello **устройств** колонки, последовательно выберите toohello список устройств, подключенных с помощью службы.
    ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)
3. Выберите и щелкните исходное устройство. Hello исходное устройство имеет hello контейнеры томов, которые требуется toofail к. Go слишком**параметры > контейнеры томов**.

    ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. Выберите контейнер томов, желательно toofail над tooanother устройством. Выберите hello тома контейнера toodisplay hello список томов в контейнере. Выберите тома, щелкните правой кнопкой мыши и нажмите кнопку **перевести в автономный режим** tootake том hello в автономный режим.

    ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. Повторите эту процедуру для всех томов hello в контейнер тома hello.

     ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. Hello повторите предыдущий шаг для всех hello контейнеры томов хотелось бы toofail над tooanother устройством.

7. Вернитесь к предыдущему окну toohello **устройств** колонку. На панели команд hello, нажмите кнопку **при сбое**.

    ![Команда "Отработка отказа"](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. В hello **при сбое** колонки, выполните следующие шаги hello:
   
    1. Щелкните **Источник**. Выберите контейнеры toofail hello тома по. **Здравствуйте, только контейнеры томов со связанных облачных моментальных снимков и отображаются томами в автономном режиме.**
        ![Выбрать источник](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)
    2. Щелкните **Цель**. Выберите целевой облачному устройству hello в раскрывающемся списке доступных устройств. **В списке hello отображаются только hello устройства имеют достаточно мощности tooaccommodate исходные контейнеры тома.**

        ![Выбор цели](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. Просмотрите параметры hello отработки отказа в группе **Сводка** и выберите hello флажок, указывающее, что hello томов в контейнере выбранного тома находятся в автономном режиме. 

        ![Просмотр параметров отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. Задание отработки отказа создано. отработка отказа hello toomonitor задания, щелкните уведомление задания hello.

    ![Мониторинг задания отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. После завершения отработки отказа hello, вернитесь к предыдущему окну toohello **устройств** колонку.

    1. Выберите устройство hello, используемой в качестве целевой hello hello перехода на другой ресурс.

       ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. Щелкните **Контейнеры томов**. Должны появиться все контейнеры томов hello и hello томами из старого устройства hello.

       Если контейнер томов hello отработку отказа локально закрепленные тома, эти тома являются отработку отказа, как и многоуровневые тома. Локально закрепленные тома не поддерживаются облачным устройством StorSimple.

       ![Просмотр целевых контейнеров томов](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a>Дальнейшие действия

* После выполнения отработки отказа, может потребоваться слишком[отключение или удаление устройства StorSimple](storsimple-8000-deactivate-and-delete-device.md).

* Сведения о toouse Здравствуйте устройства StorSimple, как службы, перейдите в слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).

