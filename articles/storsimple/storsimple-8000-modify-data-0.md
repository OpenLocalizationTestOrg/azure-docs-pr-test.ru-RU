---
title: "aaaModify DATA 0 параметры устройства серии StorSimple 8000 | Документы Microsoft"
description: "Узнайте, как toouse Windows PowerShell для StorSimple tooreconfigure hello сетевого интерфейса DATA 0 на устройстве StorSimple."
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
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 2d3bdd3675017be86def45a81d94b6c03fc61da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a>Изменить параметры hello данных 0 сетевого интерфейса на устройстве серии StorSimple 8000

## <a name="overview"></a>Обзор

Устройство Microsoft Azure StorSimple имеет шесть сетевых интерфейсов: DATA 0 tooDATA 5. Здравствуйте, DATA 0 всегда настраивается через интерфейс Windows PowerShell hello или последовательной консоли hello интерфейс и автоматически облаком. Обратите внимание, что невозможно настроить сетевого интерфейса DATA 0 через портал Azure hello.

Здравствуйте, интерфейс сначала настраивается с помощью мастера установки hello во время первоначального развертывания устройства StorSimple hello DATA 0. При hello устройство находится в рабочем режиме, может возникнуть необходимость tooreconfigure DATA 0 параметров. Этот учебник содержит два метода toomodify настроек сети DATA 0, как с помощью Windows PowerShell для StorSimple.

После изучения этого учебника вы сможете сделать следующее.

* Изменение данных 0 сетевой параметр через приветствия мастера установки
* Изменение настроек сети DATA 0 через hello `Set-HcsNetInterface` командлета

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>Изменение сетевых параметров DATA 0 с помощью мастера установки
За счет подключения toohello интерфейс Windows PowerShell устройства StorSimple и запуск сеанса мастера установки можно перенастроить настроек сети DATA 0. Выполните следующие шаги toomodify DATA 0 hello параметры:

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>toomodify настроек сети DATA 0 через мастер установки
1. В меню последовательной консоли hello, выберите параметр 1, **войти с полным доступом**. При появлении запроса укажите hello **пароль администратора устройства**. пароль по умолчанию Hello — `Password1`.
2. Hello командной строки введите следующую команду:
   
    `Invoke-HcsSetupWizard`
3. Мастер установки отображается toohelp Настройка hello DATA 0 интерфейс устройства. Укажите новые значения для hello IP-адрес шлюза и маска подсети.

> [!NOTE]
> Hello фиксированной контроллеров, IP-адреса потребуется перенастроить через hello toobe **сетевые параметры** колонке hello устройства StorSimple в hello портал Azure. Дополнительные сведения см. слишком[изменить сетевые интерфейсы](storsimple-8000-modify-device-config.md#modify-network-interfaces).

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Изменение сетевых параметров DATA 0 с помощью командлета Set-HcsNetInterface
Альтернативный способ tooreconfigure DATA 0 сетевой интерфейс является использование hello hello `Set-HcsNetInterface` командлета. командлет Hello выполняется из hello в интерфейсе Windows PowerShell устройства StorSimple. При использовании этой процедуры, фиксированные IP-адреса контроллера hello также здесь можно настроить. Выполните следующие шаги toomodify hello DATA 0 hello параметры: 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>toomodify настроек сети DATA 0 через командлет Set-HcsNetInterface hello
1. В меню последовательной консоли hello, выберите параметр 1, **войти с полным доступом**. При появлении запроса укажите пароль администратора устройства hello. пароль по умолчанию Hello — `Password1`.
2. Hello командной строки введите следующую команду:
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    В квадратных скобках hello под углом введите следующие значения для DATA 0 hello:
   
   * IPv4-адреса;
   * шлюза IPv4;
   * маски подсети IPv4;
   * фиксированного IPv4-адреса для контроллера 0;
   * фиксированного IPv4-адреса для контроллера 1.
     
     Дополнительные сведения об использовании hello этот командлет go слишком[Windows PowerShell для StorSimple Справочник по командлетам](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Дальнейшие действия
* tooconfigure сетевые интерфейсы, отличные от DATA 0, могут использовать hello [Настройка параметров сети на портал Azure hello](storsimple-8000-modify-device-config.md). 
* Если возникают проблемы при настройке сетевых интерфейсов, см. слишком[устранения проблем развертывания](storsimple-troubleshoot-deployment.md).

