---
title: "Центр IoT Azure aaaUse прямой методы (.NET или узел) | Документы Microsoft"
description: "Как toouse центр IoT Azure направлять методы. Использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement приложение имитированное устройство, которое включает прямой метод и hello Azure IoT служба пакета SDK для .NET tooimplement приложение службы, которое вызывает метод прямой hello."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a>Использование прямых методов (.NET или Node)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

В этом учебнике мы будем toodevelop .NET и Node.js консольного приложения:

* **CallMethodOnDevice.sln**, приложении серверной части .NET, который вызывает метод в приложение hello имитированное устройство и отображает hello ответа.
* **SimulatedDevice.js**, Node.js приложение, которое имитирует устройство соединение центра IoT tooyour с помощью удостоверения устройства hello, созданного ранее и отвечает toohello методе, вызванном hello облака.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.
> 
> 

toocomplete этого учебника, необходимо:

* Visual Studio 2015 или Visual Studio 2017.
* Node.js версии 0.10.x или более поздней.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства
В этом разделе создайте консольное приложение Node.js, которое отвечает tooa методе, вызванном обратно в решение hello окончания.

1. Создайте пустую папку с именем **simulateddevice**. В hello **simulateddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **simulateddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** и **azure iot устройства mqtt** пакетов:
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. В текстовом редакторе создайте файл в hello **simulateddevice** папки и назовите его **SimulatedDevice.js**.
4. Добавьте следующее hello `require` инструкции на hello начала hello **SimulatedDevice.js** файла:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Добавить **connectionString** переменной и использовать его toocreate **DeviceClient** экземпляра. Замените **{строка подключения устройства}** со строкой подключения устройства hello, созданное в hello *создать удостоверение устройства* раздела:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Добавьте следующие функции tooimplement hello прямого метода на устройстве hello hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Откройте центр IoT tooyour подключения hello и инициализировать прослушиватель hello метод:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Сохраните и закройте hello **SimulatedDevice.js** файла.

> [!NOTE]
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например, повторного соединения), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Вызов прямого метода на устройстве
В этом разделе создайте консольное приложение .NET, которое вызывает метод в приложение hello имитированное устройство, а затем отображает hello ответа.

1. В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта. Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии. Имя проекта hello **CallMethodOnDevice**.
   
    ![Новый проект классического приложения Windows на языке Visual C#][10]
2. В обозревателе решений щелкните правой кнопкой мыши hello **CallMethodOnDevice** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .
3. В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.
   
    ![Окно "Диспетчер пакетов NuGet"][11]

4. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Добавьте следующий метод toohello hello **программы** класса:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Этот метод вызывает прямой метод с именем `writeLine` на hello `myDeviceId` устройства. Затем она записывает ответ hello, предоставляемый hello устройства на консоли hello. Обратите внимание, как возможные toospecify значение времени ожидания для hello toorespond устройства.
7. Наконец, добавьте следующие строки toohello hello **Main** метод:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a>Запускать приложения hello
Теперь вы находитесь toorun готовности приложения hello.

1. В обозревателе решений Visual Studio hello, щелкните правой кнопкой мыши решение и нажмите кнопку **назначить запускаемые проекты...** . Выберите **один запускаемый проект**, а затем выберите hello **CallMethodOnDevice** проект в раскрывающемся меню hello.

2. В командной строке в hello **simulateddevice** папки, запустите следующие команды toostart прослушивание вызовы методов из вашего центра IoT hello:
   
    ```
    node SimulatedDevice.js
    ```
   Ожидание tooopen hello имитируемые устройства.![][7]
3. Теперь это устройство hello подключен и ожидание вызовов методов, запустите hello .NET **CallMethodOnDevice** метод hello tooinvoke приложения в приложение hello имитированное устройство. Должно появиться hello устройства записи в консоли hello.
   
    ![][8]
4. Затем устройство Hello реагирует метод toohello с печати это сообщение:
   
    ![][9]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Вы использовали этот устройства удостоверения tooenable hello имитируемые устройства приложения tooreact toomethods вызываемая hello облака. Также было создано приложение, которое вызывает методы на устройстве hello и отображает hello ответа от устройства hello. 

Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:

* [Приступая к работе с Центром Интернета вещей]
* [Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)

toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Приступая к работе с Центром Интернета вещей]: iot-hub-node-node-getstarted.md
