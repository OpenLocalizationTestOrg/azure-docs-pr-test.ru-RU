---
title: "При сбое aaaStorSimple, аварийное восстановление для устройств серии 8000 | Документы Microsoft"
description: "Узнайте, как toofail по вашей toohello устройства StorSimple одного устройства."
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>При сбое устройства toosame физического устройства StorSimple

## <a name="overview"></a>Обзор

В данном учебнике требуется toofail hello действия над tooitself физического устройства серии StorSimple 8000 при аварии. StorSimple использует данные hello устройства отработки отказа компонентов toomigrate из источника физического устройства в hello datacenter tooanother физического устройства. руководство Hello в этом учебнике применяется tooStorSimple 8000 ряда физических устройств под управлением версий программного обеспечения обновления 3 и более поздних версий.

toolearn Дополнительные сведения о отработки отказа устройства и как она используется toorecover после аварии, go слишком[отработки отказа и аварийного восстановления для устройства серии StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail на физическое устройство tooanother физическое устройство, перейдите в слишком[при сбое toohello же физических устройств StorSimple](storsimple-8000-device-failover-physical-device.md). toofail над tooa физическое устройство StorSimple облачному устройству StorSimple, перейдите в слишком[tooa StorSimple Appliance облака при сбое](storsimple-8000-device-failover-cloud-appliance.md).


## <a name="prerequisites"></a>Предварительные требования

- Убедитесь, можно ознакомиться с разделом hello рекомендации для обработки отказа устройства. Дополнительные сведения см. слишком[Общие рекомендации для обработки отказа устройства](storsimple-8000-device-failover-disaster-recovery.md).


## <a name="steps-toofail-over-toohello-same-device"></a>Toofail действия над toohello одного устройства

Выполните следующие действия, если требуется toofail по сравнению с toohello hello одного устройства.

1. Выполните моментальные облачные снимки всех томов hello в вашем устройстве. Дополнительные сведения см. слишком[резервные копии toocreate службы с помощью диспетчера устройств StorSimple](storsimple-8000-manage-backup-policies-u2.md).
2. Сбросьте настройки устройства toofactory по умолчанию. Выполните hello подробные инструкции в [как параметры по умолчанию tooreset toofactory устройство StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Службе диспетчера StorSimple устройство toohello перейдите и выберите **устройств**. В hello **устройств** колонке hello старое устройство должно отображаться как **Offline**.

    ![Исходное устройство не в сети](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. Настройте устройство и снова зарегистрируйте его в службе диспетчера устройств StorSimple. Hello вновь зарегистрированного устройства должно отображаться как **готов tooset копирование**. Имя устройства Hello для нового устройства hello — hello так же, как старое устройство hello но с добавлением чисел tooindicate hello устройства по умолчанию toofactory сброса и зарегистрировать его заново.

    ![Только что зарегистрированные устройства готовы tooset вверх](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Для hello новое устройство выполните настройку hello. Дополнительные сведения см. слишком[шаг 4: выполнение минимальной настройки устройства](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup). На hello **устройств** колонке hello состояние устройства hello изменяет слишком**Online**.

   > [!IMPORTANT]
   > **Сначала завершите hello минимальной конфигурации или решение аварийного восстановления может завершиться ошибкой.**

    ![Только что зарегистрированное устройство включено](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. Выберите старое устройство hello (состояние вне сети) и на панели команд hello, нажмите кнопку **при сбое**. В hello **при сбое** колонке выберите старое устройство в качестве источника hello и укажите целевое устройство hello hello вновь зарегистрированного устройства.

    ![Сводка отработки отказа](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    Подробные инструкции см. в разделе слишком[отработки отказа физического устройства tooanother](#fail-over-to-another-physical-device).

7. Создается задание восстановления устройства, можно отслеживать из hello **заданий** колонку.

8. После успешного завершения задания hello, для доступа к hello новое устройство, так и для перехода toohello **контейнеры томов** колонку. Убедитесь, что все контейнеры томов hello из старого устройства hello перенесены toohello новое устройство.

   ![Контейнеры томов перенесены](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. После завершения отработки отказа hello, можно отключить и удалить hello старое устройство с портала hello. Выберите hello старое устройство (вне сети), щелкните правой кнопкой мыши, а затем выберите **деактивировать**. После деактивации устройство hello обновляется состояние hello hello устройства.

     ![Исходное устройство отключено](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. Выберите hello деактивации устройства, щелкните правой кнопкой мыши, а затем выберите **удалить**. При этом будет удалено hello устройство из списка устройств hello.

    ![Исходное устройство удалено](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>Дальнейшие действия

* После выполнения отработки отказа, может потребоваться слишком[отключение или удаление устройства StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Сведения о toouse Здравствуйте устройства StorSimple, как службы, перейдите в слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).

