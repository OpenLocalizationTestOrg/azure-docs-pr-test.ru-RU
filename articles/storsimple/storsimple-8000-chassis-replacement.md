---
title: "корпус aaaReplace на устройства серии StorSimple 8000 | Документы Microsoft"
description: "Описывает, как tooremove и замены hello корпуса для StorSimple основного корпуса или корпуса EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 94bbd3d354a9b8866ece036238927e67ec5ce2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>Замена шасси hello на устройстве StorSimple
## <a name="overview"></a>Обзор
В этом учебнике описано как tooremove и заменить шасси в устройства серии StorSimple 8000. модель StorSimple 8100 Hello является устройство с одним корпусом (одним шасси), тогда как hello 8600 состоит из двух корпусов (два шасси). В моделях 8600 являются потенциально два шасси, которые может завершиться ошибкой в устройстве hello: hello шасси для основного корпуса hello или hello шасси для корпуса EBOD hello.

В любом случае hello запасное шасси, поставляемое компанией Майкрософт является пустым. В комплект поставки не входят блоки питания и охлаждения (БПО), модули контроллера, твердотельные дисковые накопители (SSD), жесткие диски (HDD) и модули EBOD.

> [!IMPORTANT]
> До удаления и замены шасси hello, просмотрите сведения о безопасности hello в [замена компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).


## <a name="remove-hello-chassis"></a>Удаление шасси hello
Выполните следующие шаги tooremove hello корпуса на устройстве StorSimple hello.

#### <a name="tooremove-a-chassis"></a>tooremove шасси
1. Убедитесь в том, что это устройство StorSimple hello выключено и отключено от всех источников питания hello.
2. Удалите все сети hello и кабели SAS, если это применимо.
3. Удалите устройство hello из стойки hello.
4. Извлеките каждого из устройств hello и отметьте слоты hello, от которых они будут удалены. Дополнительные сведения см. в разделе [удалить диск hello](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).
5. Удалите hello модулей контроллера EBOD на hello корпуса EBOD (если это hello шасси, сбой). Дополнительные сведения см. в разделе [Снятие контроллера EBOD](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).
   
    На hello основной корпус (если это hello шасси, сбой), удалите hello контроллеры и отметьте слоты hello, от которых они будут удалены. Дополнительные сведения см. в разделе [Снятие контроллера](storsimple-8000-controller-replacement.md#remove-a-controller).

## <a name="install-hello-chassis"></a>Установка шасси hello
Выполните следующие шаги tooinstall hello корпуса на устройстве StorSimple hello.

#### <a name="tooinstall-a-chassis"></a>tooinstall шасси
1. Подключите hello корпуса в стойку hello. Дополнительные сведения см. в разделах [Установка устройства StorSimple 8100 в стойку](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) или [Установка устройства StorSimple 8600 в стойку](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).
2. После hello шасси в стойке hello, установите модули контроллера hello в приветствия же устанавливает, что они были установлены в.
3. Установка hello дисков в hello же размещает и слотов, они были установлены в.
   
   > [!NOTE]
   > Рекомендуется сначала установить hello SSDs в слотах hello и затем установить HDD hello.
  
4. С hello устройства в стойку hello и установленных компонентов hello подключение вашего устройства toohello соответствующим источниками питания, включите устройство hello. Дополнительные сведения см. в разделах [Подключение кабельного хозяйства к устройству StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) или [Подключение кабельного хозяйства к устройству StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

## <a name="next-steps"></a>Дальнейшие действия
Узнайте подробнее о [замене компонентов оборудования StorSimple](storsimple-8000-hardware-component-replacement.md).

