---
title: "динамические данные телеметрии aaaUse | Документы Microsoft"
description: "Выполните этот учебник toolearn как toouse динамические данные телеметрии с удаленного мониторинга hello Azure IoT Suite предварительно настроенных решений."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>Используйте динамические данные телеметрии с hello удаленное наблюдение предварительно настроенных решений

Динамические данные телеметрии позволяет вы toovisualize все отправленные данные телеметрии toohello удаленное наблюдение предварительно настроенных решений. Hello имитируемые устройства, развертываемые hello предварительно настроенное решение отправляют температуры и влажности для телеметрии, то можно отобразить на панели мониторинга hello. При настройке существующих устройств, имитация создания новых устройств, имитация или физических устройств toohello предварительно настроенных решений можно отправить другим значениям телеметрии, например hello температура, RPM или windspeed подключения. Затем можно отобразить дополнительные данные телеметрии на панели мониторинга hello.

В этом учебнике используется простой Node.js имитированное устройство, можно легко изменить tooexperiment с динамической телеметрии.

toocomplete этого учебника вам потребуется:

* Активная подписка Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].
* [Node.js][lnk-node] версии 0.12.x или более поздней.

Этот учебник подходит для любой операционной системы, например Windows или Linux, в которой можно установить Node.js.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>Добавление типа данных телеметрии

Hello следующим шагом является tooreplace hello телеметрии, созданные hello Node.js имитированное устройство с новым набором значений:

1. Остановка hello Node.js имитированное устройство, введя **Ctrl + C** в командной строке или оболочки.
2. В файле remote_monitoring.js hello вы увидите hello основные значения данных для существующих температуры hello, влажность и температура телеметрии. Добавьте базовое значение данных для **rpm** следующим образом.

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. Hello Node.js имитированное устройство использует hello **generateRandomIncrement** функционировать в hello remote_monitoring.js файл tooadd toohello случайных приращения основные значения данных. Случайный выбор hello **rpm** значение, добавив строку кода после существующего метода рандомизации hello следующим образом:

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. Добавьте hello новый rpm значение toohello JSON полезных данных hello устройство отправляет tooIoT концентратора.

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. Запустите имитированное устройство hello Node.js с помощью hello следующую команду:

    `node remote_monitoring.js`

6. Изучите hello новый RPM телеметрии тип, который отображается на диаграмме hello в панели мониторинга hello:

![Добавление панели мониторинга toohello об/мин][image3]

> [!NOTE]
> Может требуется toodisable и затем включите устройство Node.js hello hello **устройств** страницу изменения hello toosee мониторинга hello немедленно.

## <a name="customize-hello-dashboard-display"></a>Настройте отображение панели мониторинга hello

Hello **сведения об устройстве** сообщение может содержать метаданные о телеметрии hello hello устройство может отправлять tooIoT концентратора. Эти метаданные можно указать типы телеметрии hello, отправляемую hello устройства. Изменение hello **deviceMetaData** значения в файл tooinclude hello remote_monitoring.js **телеметрии** hello после определения **команды** определения. Hello следующий фрагмент кода показывает hello **команды** определение (быть убедиться, что tooadd `,` после hello **команды** определение):

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> решение для удаленного мониторинга Hello используется определение метаданных hello toocompare сравнение без учета регистра с данными в потоке данных телеметрии hello.


Добавление **телеметрии** определения, как показано в предыдущем hello фрагмент кода hello поведение мониторинга hello не меняется. Тем не менее, может также включать метаданные hello **DisplayName** атрибута toocustomize hello, отображаются в панели мониторинга hello. Обновление hello **телеметрии** определение метаданных, как показано в hello, следующий фрагмент кода:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

Hello следующем снимке экрана показано это изменение изменение hello условные обозначения диаграммы на панели мониторинга hello:

![Настройка условных обозначений диаграммы hello][image4]

> [!NOTE]
> Может требуется toodisable и затем включите устройство Node.js hello hello **устройств** страницу изменения hello toosee мониторинга hello немедленно.

## <a name="filter-hello-telemetry-types"></a>Фильтровать типы телеметрии hello

По умолчанию hello диаграммы на панели мониторинга hello отображает каждого ряда данных в потоке данных телеметрии hello. Можно использовать hello **сведения об устройстве** toosuppress метаданных hello Отображение типов определенной телеметрии на диаграмме hello. 

Диаграмма hello toomake Показать только температуры и влажности телеметрии, опустить **ExternalTemperature** из hello **сведения об устройстве** **телеметрии** метаданных следующим образом:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

Hello **наружной температуры** больше не отображается на диаграмме hello:

![Данные телеметрии hello фильтра на панели мониторинга hello][image5]

Это изменение влияет только на отображение диаграммы hello. Hello **ExternalTemperature** значение данных по-прежнему сохраняются и становятся доступными для обработки базы данных.

> [!NOTE]
> Может требуется toodisable и затем включите устройство Node.js hello hello **устройств** страницу изменения hello toosee мониторинга hello немедленно.

## <a name="handle-errors"></a>Обработка ошибок

Для toodisplay потока данных на диаграмме hello его **тип** в hello **сведения об устройстве** метаданных должен соответствовать типу данных hello hello телеметрии значений. Например, если hello метаданные указывают, hello **тип** влажности является данных **int** и **двойные** найден в потоке данных телеметрии hello телеметрии влажности hello не не отображать на диаграмме hello. Здравствуйте, однако **влажность** значения по-прежнему сохраняются и становятся доступными для внутренней обработки.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы знаете, как toouse динамические данные телеметрии, можно узнать больше о том, как hello предварительно настроенных решений использовать сведения об устройстве: [метаданных сведения устройства в удаленный мониторинг hello предварительно настроенное решение] [ lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
