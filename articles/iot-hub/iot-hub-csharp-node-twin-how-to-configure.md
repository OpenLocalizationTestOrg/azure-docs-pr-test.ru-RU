---
title: "свойства двойных устройства aaaUse центр IoT Azure (.NET или узел) | Документы Microsoft"
description: "Как устройства Azure IoT Hub toouse близнецы tooconfigure устройств. Можно использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement приложения имитированное устройство и hello Azure IoT служба пакета SDK для .NET tooimplement приложение службы, которое изменяет конфигурацию устройства, с помощью двойных устройства."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>Использовать нужными свойствами tooconfigure устройства
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

В конце этого учебника hello будет иметь два приложения консоли:

* **SimulateDeviceConfiguration.js**, приложение имитированное устройство, которое ожидает обновления требуемой конфигурацией и сообщает о состоянии hello имитацию конфигурации процесса обновления.
* **SetDesiredConfigurationAndQuery**, приложении серверной части .NET, который задает hello необходимой настройки на устройстве, и запросы hello процесс обновления конфигурации.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.
> 
> 

toocomplete этого учебника требуется hello следующее:

* Visual Studio 2015 или Visual Studio 2017.
* Node.js версии 0.10.x или более поздней.
* Активная учетная запись Azure. Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

Если вы следовали hello [Приступая к работе с устройством близнецы] [ lnk-twin-tutorial] учебник, вы уже имеется центр IoT и вызывается удостоверение устройства **myDeviceId**. В этом случае можно пропустить toohello [имитированное устройство hello создать приложение] [ lnk-how-to-configure-createapp] раздела.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Создание приложения hello имитированное устройство
В этом разделе создайте консольное приложение Node.js, которое подключается tooyour концентратора, **myDeviceId**, ожидает обновления требуемой конфигурацией, а затем информирует о на процесс обновления конфигурации имитируемые hello.

1. Создайте пустую папку с именем **simulatedeviceconfiguration**. В hello **simulatedeviceconfiguration** папки, создайте новый файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello.
   
    ```
    npm init
    ```
1. В командной строке в hello **simulatedeviceconfiguration** папку, следующая команда tooinstall hello hello **azure iot устройства** и **azure-iot устройства mqtt**пакетов:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. В текстовом редакторе создайте новый **SimulateDeviceConfiguration.js** файла в hello **simulatedeviceconfiguration** папки.
1. Добавьте следующий код toohello hello **SimulateDeviceConfiguration.js** файл и замените hello **{строка подключения устройства}** заполнитель со строкой подключения устройства hello, вы скопировали, когда вы создать hello **myDeviceId** удостоверение устройства:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Hello **клиента** объект предоставляет все необходимые toointeract hello методы с близнецы устройства с устройства hello. Этот код инициализирует hello **клиента** объекта извлекает hello двойных устройства для **myDeviceId**, а затем присоединяется обработчик hello обновления на *требуемого свойства*. Обработчик Hello проверяет, существует запроса на изменение фактических конфигурации путем сравнения hello configIds, затем вызывает метод, который запускает изменение конфигурации hello.
   
    Обратите внимание, что ради hello простоты этот код использует значение по умолчанию жестко hello начальной настройки. Настоящее приложение, вероятно, скачало бы эту конфигурацию из локального хранилища.
   
   > [!IMPORTANT]
   > События изменения требуемых свойств всегда инициируются единожды при подключении устройства. Убедитесь, что это реальное изменение hello toocheck нужными свойствами, прежде чем выполнять какие-либо действия.
   > 
   > 
1. Добавьте следующие методы перед hello hello `client.open()` вызова:
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Hello **initConfigChange** метод обновления hello сообщил свойства hello объекта двойных локального устройства с конфигурацией hello обновить запрос и задает состояние hello слишком**ожидающие**, а затем обновления hello двойных устройства в службе hello. После успешного обновления двойных hello устройства, в нем имитируется длительного процесса, который прерывает выполнение hello **completeConfigChange**. Этот метод обновляет hello локальные отчета свойства параметра состояния hello слишком**успех** и удаление hello **pendingConfig** объекта. Затем он обновляет hello двойных устройства в службе hello.
   
    Обратите внимание, что toosave пропускной способности, выводятся свойства обновляются путем указания изменен только toobe свойства hello (с именем **исправление** в hello над кодом), вместо замены всего документа hello.
   
   > [!NOTE]
   > В этом руководстве не имитируется поведение при одновременном обновлении конфигураций. Некоторые процессы обновления конфигурации могут быть изменения могут tooaccommodate целевой конфигурации, во время обновления hello, некоторые могут иметь tooqueue их, а некоторые может отклонить их с состоянием ошибки. Убедитесь, что tooconsider hello желаемое поведение для определенной конфигурации процесса и добавьте соответствующую логику hello перед запуском hello изменение конфигурации.
   > 
   > 
1. Запустите приложение hello устройства:
   
        node SimulateDeviceConfiguration.js
   
    Должно появиться сообщение hello `retrieved device twin`. Оставьте приложение hello под управлением.

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
   
            try
            {
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
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
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
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **SetDesiredConfigurationAndQuery** проект является **запустить**. Выполните сборку решения hello.
1. С **SimulateDeviceConfiguration.js** запущена, запустите приложение hello .NET из Visual Studio с помощью **F5** и вы увидите изменение из указанной конфигурации hello **успех** слишком**ожидающие** слишком**успех** снова новой активной hello отправить частоту 5 минут, а не 24 часа.

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
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
