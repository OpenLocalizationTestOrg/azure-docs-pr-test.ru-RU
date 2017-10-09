---
title: "toocloud aaaSimulated Raspberry Pi (Node.js) - tooAzure симулятор web Pi Raspberry подключения центр IoT | Документы Microsoft"
description: "Подключение web Raspberry Pi симулятор tooAzure центр IoT для Raspberry Pi toosend данные toohello облако Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "малиновая pi симулятор, azure iot малиновая pi, малиновая pi центра iot, малиновая pi отправки данных toocloud, малиновая pi toocloud"
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 83736caf6ce723a49001058495a780f7f51946a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>Подключение tooAzure online симулятор Raspberry Pi центр IoT (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

В этом учебнике сначала обучения hello основы работы с симулятором online Raspberry Pi. Затем вы узнаете, как tooseamlessly подключаться hello Pi симулятор toohello облака с помощью [центр IoT Azure](iot-hub-what-is-iot-hub.md). 

При наличии физических устройств посетите [tooAzure подключения Pi Raspberry центр IoT](iot-hub-raspberry-pi-kit-node-get-started.md) tooget работы. 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>В рамках этого руководства мы:

* Hello с основами online симулятор Raspberry Pi.
* Создайте Центр Интернета вещей.
* Зарегистрируем устройство для Pi в Центре Интернета вещей.
* Выполнение примера приложения на Pi toosend имитировать центра IoT tooyour данных датчика.

Подключите имитацию центра IoT tooan Raspberry Pi, создаваемом. Тогда выполнение примера приложения с данными датчика toogenerate симулятор hello. Отправьте центра IoT tooyour данных датчика hello.

## <a name="what-you-learn"></a>Что вы узнаете

* Как toocreate центр Azure IoT и получить новые строки подключения устройства. Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.
* Как toowork с имитатором online Raspberry Pi.
* Как центр IoT tooyour данных датчика toosend.

## <a name="overview-of-raspberry-pi-web-simulator"></a>Общие сведения о веб-симуляторе Raspberry Pi

Щелкните online симулятор toolaunch кнопку Raspberry Pi hello.

> [!div class="button"]
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Запустить симулятор Raspberry Pi</a>

В симуляторе hello web имеется три области.
1. Область сборки - схемы по умолчанию hello — что Pi подключается с BME280 датчика и Индикатора. область Hello заблокирован в предварительной версии таким образом, в настоящее время не удается выполнить настройку.
2. Кодирование область - toocode с Raspberry Pi редактора кода в Интернете. Образец приложения по умолчанию Hello помогает toocollect датчиков с BME280 датчиков и отправляет tooyour центр IoT Azure. приложение Hello полностью совместима с реальными Pi устройств. 
3. Окно интегрированной консоли - показывает hello вывода кода. Hello верхней части окна имеются три кнопки.
   * **Запустите** -запустите приложение hello в область кода hello.
   * **Сброс** -кодирования области toohello по умолчанию образец приложения hello сброса.
   * **Свертки/расширение** — в правой стороне существует — кнопка для вас toofold или свернут hello окна консоли hello.

> [!NOTE] 
Имитатор web Raspberry Pi Hello теперь доступна в предварительной версии. Мы хотели бы toohear голоса в hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator). исходный код Hello public на [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).

![Общие сведения об онлайн-симуляторе Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>Запуск примера приложения на веб-симуляторе Pi

1. В программировании области, убедитесь, что вы работаете в пример приложения hello по умолчанию. Подставьте вместо приветствия в строке 15 hello строки подключения устройства Azure IoT hub.
   ![Замените строку подключения устройства hello](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. Нажмите кнопку **запуска** или тип `npm start` toorun приложения hello.


Вы увидите hello следующие выходные данные, показаны hello датчиков и hello сообщений, отправленных центра IoT tooyour ![вывод — данные датчика, отправленные из центра IoT tooyour Raspberry Pi](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>Дальнейшие действия

Вы впервые запускаете в образце данных датчика toocollect приложения и отправьте его центр IoT tooyour.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
