---
title: "Центр IoT Azure aaaUse прямой методы (.NET/.NET) | Документы Microsoft"
description: "Как toouse центр IoT Azure направлять методы. Использовать устройства Azure IoT hello SDK для .NET tooimplement приложение имитированное устройство, которое включает прямой метод и hello Azure IoT служба пакета SDK для .NET tooimplement приложение службы, которое вызывает метод прямой hello."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a>Использование прямых методов (.NET/.NET)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

В этом учебнике мы являются постоянной toodevelop два .NET консольного приложения:

* **CallMethodOnDevice**, серверная часть приложения, который вызывает метод в приложение hello имитированное устройство и отображает ответ hello.
* **SimulateDeviceMethods**, консольного приложения имитирует устройство соединение центра IoT tooyour с помощью удостоверения устройства hello, созданную ранее, которое отвечает toohello методе, вызванном hello облака.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.
> 
> 

toocomplete этого учебника, необходимо:

* Visual Studio 2015 или Visual Studio 2017.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Следует удостоверения устройства hello toocreate программно вместо чтения hello соответствующий раздел в hello [подключиться с помощью .NET концентратор IoT tooyour имитированное устройство] [ lnk-device-identity-csharp] статьи.


## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства
В этом разделе создайте консольное приложение .NET, которое отвечает tooa методе, вызванном обратно в решение hello end.

1. В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **SimulateDeviceMethods**.
   
    ![Новое классическое приложение устройства Windows на языке Visual C#][img-createdeviceapp]
    
1. В обозревателе решений щелкните правой кнопкой мыши hello **SimulateDeviceMethods** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .
1. В hello **диспетчера пакетов NuGet** выберите **Обзор** и выполните поиск **microsoft.azure.devices.client**. Выберите **установить** tooinstall hello **Microsoft.Azure.Devices.Client** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [устройств Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet пакет и его зависимости.
   
    ![Клиентское приложение в окне "Диспетчер пакетов NuGet"][img-clientnuget]
1. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello строкой подключения устройства hello, записанное в предыдущем разделе hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Добавьте следующие прямой метод tooimplement hello на устройстве hello hello:

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. Наконец, добавьте следующий код toohello hello **Main** метод tooopen hello tooyour IoT концентратора и инициализируйте hello метод прослушивателе подключений:
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. В обозревателе решений Visual Studio hello, щелкните правой кнопкой мыши решение и нажмите кнопку **назначить запускаемые проекты...** . Выберите **один запускаемый проект**, а затем выберите hello **SimulateDeviceMethods** проект в раскрывающемся меню hello.        

> [!NOTE]
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например, повторного соединения), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Вызов прямого метода на устройстве
В этом разделе создайте консольное приложение .NET, которое вызывает метод в приложение hello имитированное устройство, а затем отображает hello ответа.

1. В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта. Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии. Имя проекта hello **CallMethodOnDevice**.
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createserviceapp]
2. В обозревателе решений щелкните правой кнопкой мыши hello **CallMethodOnDevice** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .
3. В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]

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

1. В обозревателе решений Visual Studio hello, щелкните правой кнопкой мыши решение и нажмите кнопку **назначить запускаемые проекты...** . Выберите **один запускаемый проект**, а затем выберите hello **CallMethodOnDevice** проект в раскрывающемся меню hello.

## <a name="run-hello-applications"></a>Запускать приложения hello
Теперь вы находитесь toorun готовности приложения hello.

1. Выполните приложение устройства .NET hello **SimulateDeviceMethods**. Оно будет ожидать вызовы методов от вашего Центра Интернета вещей. 

    ![Запуск приложения для устройства][img-deviceapprun]
1. Теперь это устройство hello подключен и ожидание вызовов методов, запустите hello .NET **CallMethodOnDevice** метод hello tooinvoke приложения в приложение hello имитированное устройство. Должно появиться hello устройства записи в консоли hello.
   
    ![Запуск приложения службы][img-serviceapprun]
1. Затем устройство Hello реагирует метод toohello с печати это сообщение:
   
    ![Прямой метод, вызываемый на устройстве hello][img-directmethodinvoked]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Вы использовали этот устройства удостоверения tooenable hello имитируемые устройства приложения tooreact toomethods вызываемая hello облака. Также было создано приложение, которое вызывает методы на устройстве hello и отображает hello ответа от устройства hello. 

Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:

* [Приступая к работе с Центром Интернета вещей]
* [Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)

toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Приступая к работе с Центром Интернета вещей]: iot-hub-node-node-getstarted.md
