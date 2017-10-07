---
title: "режим устройства StorSimple aaaChange | Документы Microsoft"
description: "Описание режимов устройства StorSimple hello и как toouse Windows PowerShell для StorSimple toochange hello режим устройства."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a>Изменение режима hello устройства на устройстве StorSimple

В этой статье предоставляет краткое описание hello различные режимы, в которых могут работать устройства StorSimple. Устройство StorSimple может работать в трех режимах: нормальном, обслуживания и восстановления.

После прочтения этой статьи вы узнаете:

* Каковы hello режимов устройства StorSimple
* Как toofigure ожидания режима hello устройство StorSimple находится в
* Как toochange из toomaintenance в обычном режиме и *наоборот;*

Hello выше задач управления может выполняться только через интерфейс Windows PowerShell hello устройства StorSimple.

## <a name="about-storsimple-device-modes"></a>Режимы устройств StorSimple

Устройство StorSimple может работать в нормальном режиме, режиме обслуживания и режиме восстановления. Ниже кратко описан каждый из этих режимов.

### <a name="normal-mode"></a>Нормальный режим

Это определяется как hello обычный режим работы полностью настроенного устройства StorSimple. По умолчанию устройство должно находиться в нормальном режиме.

### <a name="maintenance-mode"></a>Режим обслуживания

Иногда hello устройство StorSimple может потребоваться toobe переведен в режим обслуживания. Этот режим позволяет tooperform обслуживания на устройстве hello и устанавливать обновления, например, связанных с ними toodisk встроенного по.

Можно поместить hello системы в режим обслуживания только через hello Windows PowerShell для StorSimple. В этом режиме приостанавливаются все запросы ввода-вывода. Службы, такие как энергонезависимой ОЗУ (NVRAM) или служба кластеров hello также останавливаются. Оба контроллера hello перезапускаются, при входе или выходе из этого режима. При выходе из режима обслуживания hello, все службы hello будет возобновлена и должен быть работоспособном состоянии. Это может занять несколько минут.

> [!NOTE]
> **Режим обслуживания поддерживается только на устройстве, которое работает корректно. Не поддерживается на устройстве, в котором одного или обоих контроллеров hello не работают.**


### <a name="recovery-mode"></a>Режим восстановления

Режим восстановления можно описать как "безопасный режим Windows с поддержкой сети". Режим восстановления использует службу поддержки Microsoft hello и позволяет tooperform диагностики в системе hello. Основная цель режима восстановления Hello — tooretrieve hello системные журналы.

Если система переходит в режим восстановления, вы должны обратиться в службу технической поддержки Майкрософт за дальнейшими действиями. Дополнительные сведения см. слишком[обратитесь в службу поддержки корпорации Майкрософт](storsimple-8000-contact-microsoft-support.md).

> [!NOTE]
> **Не удается разместить hello устройства в режиме восстановления. Если hello устройство находится в неисправном состоянии, режим восстановления пытается tooget hello устройство в состояние, в котором службу поддержки Microsoft смогут проанализировать его.**

## <a name="determine-storsimple-device-mode"></a>Определение режима устройства StorSimple

#### <a name="toodetermine-hello-current-device-mode"></a>текущий режим устройства toodetermine hello

1. Войдите на последовательную консоль устройства toohello, следуя указаниям hello [последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. Просмотрите сообщение hello баннер в hello меню последовательной консоли устройства hello. Это сообщение явным образом указывает ли hello устройство находится в режиме обслуживания или восстановления. Если сообщение hello не содержит никакой конкретной информации о режиме системы toohello, hello устройство находится в обычном режиме.

## <a name="change-hello-storsimple-device-mode"></a>Изменение режима устройства StorSimple hello

Можно поместить устройство StorSimple hello в процедур обслуживания tooperform режим (обычный режим) или установки обновлений режима обслуживания. Выполните следующие процедуры tooenter или завершения режима обслуживания hello.

> [!IMPORTANT]
> Перед переходом в режим обслуживания, убедитесь, что оба контроллера устройства находятся в работоспособном состоянии, обратившись к hello **параметры устройства > работоспособности оборудования** для вашего устройства в hello портал Azure. Если один или оба контроллера hello не находятся в работоспособном состоянии, обратитесь в службу поддержки Майкрософт hello дальнейшие действия. Дополнительные сведения см. слишком[обратитесь в службу поддержки корпорации Майкрософт](storsimple-8000-contact-microsoft-support.md).
 

#### <a name="tooenter-maintenance-mode"></a>режим обслуживания tooenter

1. Войдите на последовательную консоль устройства toohello, следуя указаниям hello [последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. В меню последовательной консоли hello, выберите параметр 1, **войти с полным доступом**. При появлении запроса укажите hello **пароль администратора устройства**. пароль по умолчанию Hello: `Password1`.
3. Введите в командной строке hello 
   
    `Enter-HcsMaintenanceMode`
4. Вы увидите предупреждение о том, что режим обслуживания прервет все запросы ввода-вывода и разорвет toohello подключения hello портал Azure и будет приглашение для подтверждения. Тип **Y** tooenter режима обслуживания.
5. Оба контроллера будут перезапущены. После завершения перезагрузки hello баннер hello последовательной консоли будет указать, что это hello устройство находится в режиме обслуживания. Результат выполнения команды показан ниже.

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a>режим обслуживания tooexit

1. Войдите на последовательную консоль устройства toohello. Проверьте из сообщения hello баннера, ваше устройство находится в режиме обслуживания.
2. Hello командной строки введите следующую команду:
   
    `Exit-HcsMaintenanceMode`
3. Отобразится сообщение с предупреждением и сообщение с запросом на подтверждение. Тип **Y** tooexit режима обслуживания.
4. Оба контроллера будут перезапущены. После завершения перезагрузки hello баннер последовательной консоли hello указывает, что это hello устройство находится в обычном режиме. Результат выполнения команды показан ниже.

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом слишком[применить обновления в режиме обычный и обслуживания](storsimple-update-device.md) на устройстве StorSimple.

