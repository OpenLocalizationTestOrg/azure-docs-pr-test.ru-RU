---
title: "aaaSchedule заданий с центром IoT Azure (.NET или узел) | Документы Microsoft"
description: "Как tooschedule центр IoT Azure заданий tooinvoke прямой метод на нескольких устройствах. Использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement hello имитируемые приложения для устройств и hello Azure IoT служба пакета SDK для .NET tooimplement задание службы toorun приложения hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a>Планирование и трансляция заданий (.NET или Node.js)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Используйте центр IoT Azure tooschedule и отслеживать задания, которые обновляют миллионов устройств. Что можно сделать с помощью заданий?

* Обновление требуемых свойств
* Обновление тегов
* Вызов прямых методов

Задание включает одно из следующих действий и отслеживает hello выполнения для набора устройств, определяется запрос двойных устройства. Например приложение серверной части можно использовать tooinvoke задания прямой метод на 10 000 устройств, которые перезагрузки устройства hello. Укажите hello устройств с помощью запроса двойных устройства и запланировать задание toorun hello в будущем. отслеживает ход выполнения задания Hello имени каждого из устройств hello получают и выполнить прямой метод перезагрузки hello.

toolearn Дополнительные сведения о каждой из этих возможностей см.:

* Двойных устройства и свойства: [Приступая к работе с устройством близнецы] [ lnk-get-started-twin] и [учебника: как свойства двойных toouse устройства][lnk-twin-props]
* Прямые методы: [Общие сведения о прямых методах и информация о вызове этих методов из Центра Интернета вещей][lnk-dev-methods] и [Использование прямых методов на устройстве Интернета вещей (Node.js)][lnk-c2d-methods].

В этом учебнике описаны следующие процедуры.

* Создание приложения для устройств, реализующий прямой метод с именем **lockDoor** , может быть вызван приложение hello серверной части. приложение Hello устройства также получает изменения требуемое свойство из серверной части приложения hello.
* Создания серверной части приложения, которое создает задание toocall hello **lockDoor** прямой метод на нескольких устройствах. Требуемое свойство обновить устройства toomultiple отправляет другим заданием.

В конце этого учебника hello у вас есть приложение Node.js консоли устройства и консольного приложения серверной части .NET (C#):

**simDevice.js** , соединяет центр IoT tooyour, реализующий hello **lockDoor** прямой метод и обрабатывает требуемого свойства.

**ScheduleJob** , использующий hello задания toocall **lockDoor** прямой метод и обновление двойных hello устройства требуемого свойства на нескольких устройствах.

toocomplete этого учебника требуется hello следующие:

* Visual Studio 2015 или Visual Studio 2017.
* Node.js 0.12.x или более поздней версии. статья Hello [подготовить среду разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.
* Активная учетная запись Azure. Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a>Планирование заданий для вызова прямого метода и обновления свойств двойника устройства

В этом разделе создайте .NET консольного приложения (с помощью C#), использующий hello задания toocall **lockDoor** прямой метод и отправить требуемое свойство обновить toomultiple устройства.

1. В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **ScheduleJob**.

    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]

1. В обозревателе решений щелкните правой кнопкой мыши hello **ScheduleJob** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .
1. В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello. Этот шаг загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.

    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. Добавьте следующее hello `using` инструкции, если он уже имеется в инструкциях по умолчанию hello.

    ```csharp
    using System.Threading.Tasks;
    ```

1. Добавьте следующие поля toohello hello **программы** класса. Замените заполнитель hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. Добавьте следующий метод toohello hello **программы** класса:

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. Добавьте следующий метод toohello hello **программы** класса:

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. Добавьте следующий метод toohello hello **программы** класса:

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. Наконец, добавьте следующие строки toohello hello **Main** метод:

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **ScheduleJob** проект является **запустить**. Выполните сборку решения hello.

## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства

В этом разделе создайте консольное приложение Node.js, которое отвечает tooa прямой метод, вызываемый hello облака, активизирующий перезагрузка имитации устройства и использует hello выводятся свойства tooenable устройствами двойных запросы tooidentify устройства и когда они последней перезагрузки.

1. Создайте пустую папку с именем **simDevice**.  В hello **simDevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.  Примите все значения по умолчанию hello:

    ```cmd/sh
    npm init
    ```

1. В командной строке в hello **simDevice** папку, следующая команда tooinstall hello hello **azure iot устройства** и **azure iot устройства mqtt** пакетов:

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. В текстовом редакторе создайте новый **simDevice.js** файла в hello **simDevice** папки.

1. Добавьте следующие hello «требовать» операторы в начале hello hello **simDevice.js** файла:

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. Добавить **connectionString** переменной и использовать его toocreate **клиента** экземпляра. Сделайте заполнители hello убедиться, что tooreplace установки tooyour соответствующие значения.

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Добавить следующие функции hello toohandle hello **lockDoor** метод.

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. Добавьте следующий код обработчика hello tooregister для hello hello **lockDoor** метод.

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. Сохраните и закройте hello **simDevice.js** файла.

> [!NOTE]
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].

## <a name="run-hello-apps"></a>Запускайте приложения hello

Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке hello в hello **simDevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.

    ```cmd/sh
    node simDevice.js
    ```

1. Консольное приложение hello выполнения C# **ScheduleJob** , щелкнув hello **ScheduleJob** проект, выбрав **отладки** и **запустить новый экземпляр**.

1. Вы видите hello выходные данные из устройства и серверной части приложения.

    ![Запуск приложения hello tooschedule заданий][img-schedulejobs]

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике используется задание tooschedule прямой метод tooa устройства и hello обновление свойств устройства двойных hello.

Приступая к работе с центр IoT и устройства управления шаблонами, например удаленного через обновление встроенного по воздуху hello, чтение toocontinue [учебника: как toodo встроенное по обновить][lnk-fwupdate].

Приступая к работе с центром IoT toocontinue в разделе [Приступая к работе с краем IoT][lnk-iot-edge].

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
