---
title: "aaaGet к работе с близнецы устройства Azure IoT Hub (.NET/.NET) | Документы Microsoft"
description: "Как tooadd близнецы устройства Azure IoT Hub toouse теги и затем использовать запрос центр IoT. Использовать устройства Azure IoT hello SDK для .NET tooimplement hello имитированное устройство и приложения hello служба Azure IoT SDK для .NET tooimplement приложение службы, которое добавляет теги hello и запускает hello центра IoT запроса."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a>Начало работы с двойниками устройств (.NET/.NET)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

В конце этого учебника hello будет иметь следующие консольные приложения .NET:

* **CreateDeviceIdentity**, приложение .NET, который создает удостоверения устройства и связанная с защитой ключа tooconnect приложение имитации устройства.
* **AddTagsAndQuery** — внутреннее приложение .NET, которое добавляет теги и выполняет запросы к двойникам устройств.
* **ReportConnectivity**, приложение .NET устройства, которое имитирует устройство, соединяющее центра IoT tooyour с идентификатором hello устройства, созданного ранее и сообщает о условия его подключения.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.
> 
> 

toocomplete этого учебника требуется hello следующее:

* Visual Studio 2015 или Visual Studio 2017.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Следует удостоверения устройства hello toocreate программно вместо чтения hello соответствующий раздел в hello [подключиться с помощью .NET концентратор IoT tooyour имитированное устройство] [ lnk-device-identity-csharp] статьи.

## <a name="create-hello-service-app"></a>Создание приложения hello службы
В этом разделе создайте .NET консольного приложения (с помощью C#), добавляет связанные с устройством двойных расположение метаданных toohello **myDeviceId**. Затем выполняется запрос близнецы hello устройства хранится в центр IoT hello, выбрав hello устройствах, находящихся в hello нам и Здравствуйте, те, о которых сообщает сотовой связи.

1. В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **AddTagsAndQuery**.
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]
1. В обозревателе решений щелкните правой кнопкой мыши hello **AddTagsAndQuery** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .
1. В hello **диспетчера пакетов NuGet** выберите **Обзор** и выполните поиск **microsoft.azure.devices**. Выберите **установить** tooinstall hello **Microsoft.Azure.Devices** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
        using Microsoft.Azure.Devices;
1. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Добавьте следующий метод toohello hello **программы** класса:
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    Hello **RegistryManager** класс предоставляет все необходимые toointeract hello методы с близнецы устройства из службы hello. Предыдущий код Hello сначала инициализирует hello **registryManager** объекта, а затем извлекает hello двойных устройства для **myDeviceId**и наконец обновляет сведения о расположении hello требуемого этим тегам.
   
    После обновления, он выполняет два запроса: hello сначала выделяются hello близнецы устройств для устройств, расположенных в hello **Redmond43** здания, сооружения и hello второй уточняет hello запроса tooselect только hello устройства, подключенные через также сети мобильной связи.
   
    Обратите внимание, что предыдущего код hello, при создании hello **запроса** объекта, указывает максимальное количество возвращенных документов. Hello **запроса** объект содержит **HasMoreResults** логического свойства, которые можно использовать tooinvoke hello **GetNextAsTwinAsync** методы все tooretrieve несколько раз результаты. Метод **GetNextAsJson** доступен для результатов, которые не являются двойниками устройств, например результатов статистических запросов.
1. Наконец, добавьте следующие строки toohello hello **Main** метод:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **AddTagsAndQuery** проект является **запустить**. Выполните сборку решения hello.
1. Запустить это приложение, щелкнув hello **AddTagsAndQuery** проекта и выбрав **отладки**, за которым следует **запустить новый экземпляр**. Вы увидите одно устройство в результатах hello для hello запрос запросом для всех устройств, расположенных в **Redmond43** и для hello запрос, который ограничивает hello нет результатов toodevices используемой сети мобильной связи.
   
    ![Результаты запроса в окне][img-addtagapp]

В следующем разделе hello создается приложение устройства, которое сообщает сведения о подключении hello и изменения hello результат запроса hello в предыдущем разделе hello.

## <a name="create-hello-device-app"></a>Создание приложения hello устройства
В этом разделе создайте консольное приложение .NET, которое подключается tooyour концентратора, **myDeviceId**и обновляет сведения о hello toocontain свойства отчета, он соединяется с использованием сети мобильной связи.

1. В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **ReportConnectivity**.
   
    ![Новое классическое приложение устройства Windows на языке Visual C#][img-createdeviceapp]
    
1. В обозревателе решений щелкните правой кнопкой мыши hello **ReportConnectivity** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .
1. В hello **диспетчера пакетов NuGet** выберите **Обзор** и выполните поиск **microsoft.azure.devices.client**. Выберите **установить** tooinstall hello **Microsoft.Azure.Devices.Client** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [устройств Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet пакет и его зависимости.
   
    ![Клиентское приложение в окне "Диспетчер пакетов NuGet"][img-clientnuget]
1. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello строкой подключения устройства hello, записанное в предыдущем разделе hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Добавьте следующий метод toohello hello **программы** класса:

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    Hello **клиента** объект представляет все методы hello, требующих toointeract с близнецы устройства с устройства hello. Здравствуйте, приведенный выше код инициализирует hello **клиента** объекта, а затем извлекает hello устройства двойных для **myDeviceId**.

1. Добавьте следующий метод toohello hello **программы** класса:
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   Здравствуйте кода выше обновления **myDeviceId**сообщила свойство с данных о связности hello.

1. Наконец, добавьте следующие строки toohello hello **Main** метод:
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **ReportConnectivity** проект является **запустить**. Выполните сборку решения hello.
1. Запустить это приложение, щелкнув hello **ReportConnectivity** проекта и выбрав **отладки**, за которым следует **запустить новый экземпляр**. Вы должны увидеть, получение сведений о двойных hello и последующей отправки подключения, как *сообщил свойство*.
   
    ![Запустите подключения tooreport приложения для устройств][img-rundeviceapp]
    
    
1. Теперь, когда hello устройство сообщило его сведения о соединении, он должен отображаться в обоих запросов. Запустите hello .NET **AddTagsAndQuery** hello toorun приложение запрашивает еще раз. На этот раз **myDeviceId** должен появиться в результатах обоих запросов.
   
    ![Сведения о подключении устройства успешно переданы][img-tagappsuccess]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Добавить метаданные устройства как теги из серверной части приложения, а написал имитированное устройство приложения tooreport подключения сведений об устройстве в двойных hello устройства. Вы также узнали, каким образом tooquery эти сведения, с помощью языка запросов SQL-подобного центра IoT hello.

Hello используйте следующие ресурсы toolearn как для:

* Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT] [ lnk-iothub-getstarted] учебника
* Настройка устройств с нужными свойствами устройства двойных hello [используйте требуемого свойства устройства tooconfigure] [ lnk-twin-how-to-configure] учебника
* Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения) с hello [использовать прямые методы] [ lnk-methods-tutorial] учебника.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

