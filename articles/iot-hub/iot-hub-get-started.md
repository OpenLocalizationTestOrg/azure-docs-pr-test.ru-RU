---
title: "Центр IoT Azure — начать подключение облака toohello устройств IoT | Документы Microsoft"
description: "Узнайте, как tooconnect ваших досок IoT и начальные наборы tooAzure центр IoT. Устройства можно отправить tooIoT телеметрии концентратора и центра IoT можно отслеживать и управлять устройствами."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: "Руководство по работе с Центром Интернета вещей Azure"
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a>Руководства по началу работы с Центром Интернета вещей Azure

Можно использовать центр IoT Azure и hello Azure IoT SDK toobuild Интернета вещей (IoT) устройствами:

* Центр IoT Azure — это полностью управляемая служба в облаке hello, безопасно подключаются, отслеживает и управляет устройствами IoT. Используйте пакеты SDK Azure IoT tooimplement hello устройствами IoT.
* С помощью шлюза Интернета вещей можно реализовать более сложные сценарии, связанные с Интернетом вещей. Например, когда необходимо tooconsider факторов, таких как устаревшие устройства, затраты на полосу пропускания, политик безопасности и конфиденциальности или край обработки данных. В этих сценариях используется tooimplement Azure IoT пограничного шлюза, который соединяет центр IoT tooyour устройств.

## <a name="what-hello-tutorials-cover"></a>Что входит в учебниках hello

В этих учебниках представлены tooAzure центр IoT и устройством hello пакетов SDK. Hello учебниках рассматриваются общие возможности IoT сценариев toodemonstrate hello из центра IoT. Hello учебниках также представлены как toocombine центр IoT с другими Azure службы и средств toobuild более мощные решения IoT. В учебниках hello вы можете toouse либо имитируемой или реальной устройствами IoT. Кроме того, рассказывается, как toouse шлюза tooenable устройств tooconnect tooyour центр IoT.

## <a name="set-up-your-device"></a>Настройка устройства

Подключите IoT устройства или шлюза tooAzure центр IoT. Можно выбрать tooget физического или имитации устройства к работе.

| Устройство IoT                       | Язык программирования |
|----------------------------------|----------------------|
| Raspberry Pi                     | [Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]  |
| IoT DevKit                       | [Arduino в VSCode][DevKit]     |
| Intel Edison                     | [Node.js][Ed_Nd], [C][Ed_C]    |
| Adafruit Feather HUZZAH ESP8266  | [Arduino][Hu_Ard]              |
| Sparkfun ESP8266 Thing Dev       | [Arduino][Th_Ard]              |
| Adafruit Feather M0              | [Arduino][M0_Ard]              |
| Имитация устройства на компьютере           | [.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth] |
| Онлайн-симулятор устройства         | [Raspberry Pi (Node.js)][Ol_Sim] |

Кроме того можно использовать центр IoT tooyour IoT пограничного шлюза tooenable устройств tooconnect:

| Устройство шлюза               | Язык программирования | Платформа         |
|------------------------------|----------------------|------------------|
| Intel NUC (модель DE3815TYKE) | C                    | [Wind River Linux][NUC_Lnx] |
| Виртуальное устройство            | C                    | [Linux][Sim_Lnx], [Windows][Sim_Win] |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
