---
title: "свойства двойных устройства aaaUse центр IoT Azure (.NET/.NET) | Документы Microsoft"
description: "Как устройства Azure IoT Hub toouse близнецы tooconfigure устройств. Можно использовать устройства Azure IoT hello пакета SDK для .NET tooimplement приложения имитированное устройство и hello Azure IoT служба пакета SDK для .NET tooimplement приложение службы, которое изменяет конфигурацию устройства, с помощью двойных устройства."
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>Использовать нужными свойствами tooconfigure устройства
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

В конце этого учебника hello будет иметь два консольных приложений .NET:

* **SimulateDeviceConfiguration**, приложение имитированное устройство, которое ожидает обновления требуемой конфигурацией и сообщает о состоянии hello имитацию конфигурации процесса обновления.
* **SetDesiredConfigurationAndQuery**, серверная часть приложения, который устанавливает hello необходимой настройки на устройстве, и запросы hello процесс обновления конфигурации.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.
> 
> 

toocomplete этого учебника требуется hello следующее:

* Visual Studio 2015 или Visual Studio 2017.
* Активная учетная запись Azure. Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

Если вы следовали hello [Приступая к работе с устройством близнецы] [ lnk-twin-tutorial] учебник, вы уже имеется центр IoT и вызывается удостоверение устройства **myDeviceId**. В этом случае можно пропустить toohello [имитированное устройство hello создать приложение] [ lnk-how-to-configure-createapp] раздела.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Создание приложения hello имитированное устройство
В этом разделе создайте консольное приложение .NET, которое подключается tooyour концентратора, **myDeviceId**, ожидает обновления требуемой конфигурацией, а затем информирует о на процесс обновления конфигурации имитируемые hello.

1. В Visual Studio, создайте новый проект Visual C# Windows классического с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **SimulateDeviceConfiguration**.
   
    ![Новое классическое приложение устройства Windows на языке Visual C#][img-createdeviceapp]

1. В обозревателе решений щелкните правой кнопкой мыши hello **SimulateDeviceConfiguration** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .
1. В hello **диспетчера пакетов NuGet** выберите **Обзор** и выполните поиск **microsoft.azure.devices.client**. Выберите **установить** tooinstall hello **Microsoft.Azure.Devices.Client** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [устройств Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet пакет и его зависимости.
   
    ![Клиентское приложение в окне "Диспетчер пакетов NuGet"][img-clientnuget]
1. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello строкой подключения устройства hello, записанное в предыдущем разделе hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. Добавьте следующий метод toohello hello **программы** класса:
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    Hello **клиента** объект представляет все методы hello, требующих toointeract с близнецы устройства с устройства hello. Здравствуйте, приведенный выше код инициализирует hello **клиента** объекта, а затем извлекает hello устройства двойных для **myDeviceId**.

1. Добавьте следующий метод toohello hello **программы** класса. Этот метод задает начальные значения hello телеметрии на локальном устройстве hello и затем обновления hello двойных устройства.

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. Добавьте следующий метод toohello hello **программы** класса. Это обратный вызов, который обнаруживает изменения в *требуемого свойства* в двойных hello устройства.

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    Этот метод обновления hello сообщил свойства hello объекта двойных локального устройства с конфигурацией hello обновить запрос и задает состояние hello слишком**ожидающие**, а затем обновления hello двойных устройства в службе hello. После успешного обновления двойных устройства hello, изменение конфигурации hello завершается путем вызова метода hello `CompleteConfigChange` описано в следующей точке hello.

1. Добавьте следующий метод toohello hello **программы** класса. Этот метод имитирует сброса устройства, а затем обновления hello локальные свойства отчета, установка состояния hello слишком**успех** и удаляет hello **pendingConfig** элемента. Затем он обновляет hello двойных устройства в службе hello. 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. Наконец, добавьте следующие строки toohello hello **Main** метод:

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > В этом руководстве не имитируется поведение при одновременном обновлении конфигураций. Некоторые процессы обновления конфигурации могут быть изменения могут tooaccommodate целевой конфигурации, во время обновления hello, некоторые могут иметь tooqueue их, а некоторые может отклонить их с состоянием ошибки. Убедитесь, что tooconsider hello желаемое поведение для определенной конфигурации процесса и добавьте соответствующую логику hello перед запуском hello изменение конфигурации.
   > 
   > 
1. Выполните построение решения hello и запустите приложение hello устройства из Visual Studio, нажав кнопку **F5**. На консоли вывода hello вы увидите сообщений hello, указывающее, что имитированное устройство получение двойных hello устройства, Настройка телеметрии hello и ожидающих изменений нужного свойства. Оставьте приложение hello под управлением.

## <a name="create-hello-service-app"></a>Создание приложения hello службы
В этом разделе вы создадите консольное приложение .NET, hello обновления *требуемого свойства* на двойных hello устройства, связанные с **myDeviceId** новым объектом конфигурации телеметрии. Он запрашивает близнецы устройства hello, хранящихся в центр IoT hello и показывает разность hello hello требуемого и данные конфигурации устройства hello.

1. В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **SetDesiredConfigurationAndQuery**.
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]
1. В обозревателе решений щелкните правой кнопкой мыши hello **SetDesiredConfigurationAndQuery** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .
1. В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Добавьте следующий метод toohello hello **программы** класса:
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            while (true)
            {
                var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                var results = await query.GetNextAsTwinAsync();
                foreach (var result in results)
                {
                    Console.WriteLine("Config report for: {0}", result.DeviceId);
                    Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                    Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                    Console.WriteLine();
                }
                Thread.Sleep(10000);
            }
        }
   
    Hello **реестра** объект предоставляет все необходимые toointeract hello методы с близнецы устройства из службы hello. Этот код инициализирует hello **реестра** объекта извлекает hello двойных устройства для **myDeviceId**и затем обновляет ее нужными свойствами нового объекта конфигурации телеметрии.
    После этого он запрашивает близнецы устройства hello, хранящихся в центр IoT hello каждые 10 секунд и печатает hello требуемого и данные телеметрии конфигураций. См. toohello [язык запросов центра IoT] [ lnk-query] toolearn как toogenerate полнофункциональных отчетов на всех устройствах.
   
   > [!IMPORTANT]
   > Это приложение выполняет запрос к Центру Интернета вещей каждые 10 секунд в качестве примера. Используйте запрашивает toogenerate пользовательские отчеты для многих устройств и не toodetect изменения. Если вашему решению требуется отправка уведомлений о событиях устройства в реальном времени, используйте [уведомления двойников][lnk-twin-notifications].
   > 
   > 
1. Наконец, добавьте следующие строки toohello hello **Main** метод:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **SetDesiredConfigurationAndQuery** проект является **запустить**. Выполните сборку решения hello.
1. С **SimulateDeviceConfiguration** устройство под управлением приложения, приложение hello выполнения службы из Visual Studio с помощью **F5**. Вы увидите изменение из указанной конфигурации hello **ожидающие** слишком**успех** новой активной hello отправки частоту 5 минут, а не 24 часа.

 ![Устройство успешно настроено][img-deviceconfigured]
   
   > [!IMPORTANT]
   > Нет задержки мин tooa между hello устройство работы и отчетов hello результата запроса. Это toowork tooenable hello запроса инфраструктуры в очень широком масштабе. использовать tooretrieve согласованного представления двойных одно устройство hello **getDeviceTwin** метод в hello **реестра** класса.
   > 
   > 

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике можно задавать нужные параметры как *требуемого свойства* из решения hello серверной части и написал toodetect приложения устройства, изменение и имитировать обновления многоступенчатый процесс, его через hello сообщил о состоянии свойства.

Hello используйте следующие ресурсы toolearn как для:

* Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT] [ lnk-iothub-getstarted] учебника
* запланировать или выполнять операции с большими наборами устройств в разделе hello [расписание и широковещательных задания] [ lnk-schedule-jobs] учебника.
* Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения), с hello [использовать прямые методы] [ lnk-methods-tutorial] учебника.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
