---
title: "aaaStorSimple перехода на другой ресурс физического устройства серии tooa StorSimple 8000 аварийного восстановления | Документы Microsoft"
description: "Узнайте, как toofail через вашего устройства серии StorSimple 8000 физическое устройство tooanother физический."
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
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>При сбое физического устройства серии StorSimple 8000 tooa

## <a name="overview"></a>Обзор

В данном учебнике требуется toofail hello действия над устройства серии StorSimple 8000 физическое устройство tooanother StorSimple физического при аварии. StorSimple использует данные hello устройства отработки отказа компонентов toomigrate из источника физического устройства в hello datacenter tooanother физического устройства. руководство Hello в этом учебнике применяется tooStorSimple 8000 ряда физических устройств под управлением версий программного обеспечения обновления 3 и более поздних версий.

toolearn Дополнительные сведения о отработки отказа устройства и как она используется toorecover после аварии, go слишком[отработки отказа и аварийного восстановления для устройства серии StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail над tooa физическое устройство StorSimple облачному устройству StorSimple, перейдите в слишком[tooa StorSimple Appliance облака при сбое](storsimple-8000-device-failover-cloud-appliance.md). toofail над tooitself физическое устройство go слишком[при сбое toohello же физических устройств StorSimple](storsimple-8000-device-failover-same-device.md).


## <a name="prerequisites"></a>Предварительные требования

- Убедитесь, можно ознакомиться с разделом hello рекомендации для обработки отказа устройства. Дополнительные сведения см. слишком[Общие рекомендации для обработки отказа устройства](storsimple-8000-device-failover-disaster-recovery.md).

- Необходимо иметь устройства серии StorSimple 8000 физических развернутых в центре обработки данных hello. Hello устройства необходимо запустить с обновлением 3 или более поздней версии программного обеспечения. Дополнительные сведения см. слишком[развертывание локального устройства StorSimple](storsimple-8000-deployment-walkthrough-u2.md).


## <a name="steps-toofail-over-tooa-physical-device"></a>Toofail действия над tooa физического устройства

Выполните следующие шаги toorestore hello целевого устройства tooa физического устройства.

1. Убедитесь, что нужные toofail через контейнера томов hello связаны облачные моментальные снимки. Дополнительные сведения см. слишком[резервные копии toocreate службы с помощью диспетчера устройств StorSimple](storsimple-8000-manage-backup-policies-u2.md).
2. Go tooyour устройства StorSimple, а затем нажмите кнопку **устройств**. В hello **устройств** колонки, последовательно выберите toohello список устройств, подключенных с помощью службы.
    ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. Выберите и щелкните исходное устройство. Hello исходное устройство имеет hello контейнеры томов, которые требуется toofail к. Go слишком**параметры > контейнеры томов**.
4. Выберите контейнер томов, желательно toofail над tooanother устройством. Выберите hello тома контейнера toodisplay hello список томов в контейнере. Выберите тома, щелкните правой кнопкой мыши и нажмите кнопку **перевести в автономный режим** tootake том hello в автономный режим. Повторите эту процедуру для всех томов hello в контейнер тома hello.
5. Hello повторите предыдущий шаг для всех hello контейнеры томов хотелось бы toofail над tooanother устройством.
6. Вернитесь к предыдущему окну toohello **устройств** колонку. На панели команд hello, нажмите кнопку **при сбое**.
    ![Щелкните "Отработка отказа"](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)
    
7. В hello **при сбое** колонки, выполните следующие шаги hello:
   
   1. Щелкните **Источник**. отображаются Hello контейнеры томов с тома, связанные с облачными моментальными снимками. Для обработки отказа подходят только контейнеры hello отображается. В списке hello контейнеров томов выберите контейнеры томов hello, которой вы хотите toofail по. **Здравствуйте, только контейнеры томов со связанных облачных моментальных снимков и отображаются томами в автономном режиме.**

       ![Выбор источника](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. Щелкните **Цель**. Для контейнеров томов hello на предыдущем шаге hello выберите целевое устройство из hello раскрывающегося списка доступных устройств. В списке hello отображаются только hello устройства имеют достаточно мощности tooaccommodate исходные контейнеры тома.

        ![Выбор цели](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. Наконец, просмотрите все параметры отработки отказа hello под **Сводка**. После просмотра hello параметры, выберите hello флажок, указывающее, что hello томов в контейнере выбранного тома находятся в автономном режиме. Нажмите кнопку **ОК**.

       ![Просмотр параметров отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. StorSimple создаст задание отработки отказа. Нажмите кнопку hello задания уведомления toomonitor hello задание отработки отказа через hello **заданий** колонку.

    Если контейнер томов hello отработку отказа локального тома, вы видите отдельных заданий восстановления для каждого локального тома (не для многоуровневых томов), в контейнере hello. Эти задания восстановления может занять некоторое время toocomplete. Вполне вероятно, hello задание отработки отказа может завершиться ранее. Эти тома будет иметь локальные гарантии только после завершения задания восстановления hello.

    ![Мониторинг задания отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. После завершения перехода на другой ресурс hello go toohello **устройств** колонку.
   
   1. Выберите устройство hello, используемой в качестве hello целевое устройство для hello процесс отработки отказа.

       ![Выбор устройства](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. Go toohello **контейнеры томов** колонку. Должны появиться все контейнеры томов hello и hello томами из старого устройства hello.

       ![Просмотр целевых контейнеров томов](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>Дальнейшие действия

* После выполнения отработки отказа, может потребоваться слишком[отключение или удаление устройства StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Сведения о toouse Здравствуйте устройства StorSimple, как службы, перейдите в слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).

