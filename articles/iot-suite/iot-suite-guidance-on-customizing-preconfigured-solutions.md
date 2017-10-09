---
title: "aaaCustomizing предварительно настроенных решений | Документы Microsoft"
description: "Содержатся сведения о том, как toocustomize hello Azure IoT Suite предварительно настроенных решений."
services: 
suite: iot-suite
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4653ae53-4110-4a10-bd6c-7dc034c293a8
ms.service: iot-suite
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 1a8573f5ac6ed944c44459df495446f15174d513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-a-preconfigured-solution"></a>Настройка предварительно настроенного решения

Hello предварительно настроенных решений, в состав hello Azure IoT Suite Демонстрация служб hello в hello suite рабочий вместе toodeliver решения начала до конца. Из этой точки отсчета существуют в различных местах, в которых можно расширять и настраивать hello решения для конкретных сценариев. Привет, в следующих разделах описаны эти общие настройки точки.

## <a name="find-hello-source-code"></a>Поиск исходного кода hello

Hello исходного кода для hello предварительно настроенных решений можно найти в GitHub в следующих репозиториев hello:

* Удаленный мониторинг: [https://www.github.com/Azure/azure-iot-remote-monitoring](https://github.com/Azure/azure-iot-remote-monitoring)
* Прогнозируемое обслуживание: [https://github.com/Azure/azure-iot-predictive-maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* Подключенная фабрика: [https://github.com/Azure/azure-iot-connected-factory](https://github.com/Azure/azure-iot-connected-factory)

toodemonstrate hello шаблоны и методики используемым функциям конца в конец hello tooimplement IoT решения с помощью набора IoT Azure предоставляется Hello исходного кода для hello предварительно настроенных решений. Дополнительные сведения о том, как можно найти toobuild и развертывание решений hello в репозиториях GitHub hello.

## <a name="change-hello-preconfigured-rules"></a>Изменение hello предварительно настроенных правил

Hello удаленного мониторинга решение включает в себя три [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) задания сведений об устройстве toohandle, телеметрии и логики правил в решении hello.

Hello три потока analytics заданий и их синтаксиса описаны в глубину в hello [удаленный мониторинг заранее настроенные Пошаговое руководство по решениям](iot-suite-remote-monitoring-sample-walkthrough.md). 

Эти задания можно изменить напрямую tooalter hello логики или добавьте логику tooyour конкретного сценария. Можно найти hello заданий Stream Analytics следующим образом:

1. Go слишком[портал Azure](https://portal.azure.com).
2. Перейдите в группу ресурсов toohello hello точно такое же имя в качестве вашего решения IoT. 
3. Выберите задание Azure Stream Analytics hello хотелось бы toomodify. 
4. Остановка задания hello, выбрав **остановить** hello набора команд. 
5. Измените входные данные hello, запрос и выходные данные.
   
    Простое изменение — запрос hello toochange для hello **правила** toouse задания **«<»** вместо **» > «**. портал Hello решение по-прежнему показывает **» > «** при изменении правил, но Обратите внимание на то, как поведение hello отражается из-за изменения toohello hello базового задания.
6. Запустить задание hello

> [!NOTE]
> Hello удаленного мониторинга зависит от конкретных данных, поэтому изменение hello задания может привести к toofail hello панели мониторинга.

## <a name="add-your-own-rules"></a>Добавление собственных правил

В дополнение к этому toochanging hello заранее настроенные задания Azure Stream Analytics, можно использовать новые задания hello Azure портала tooadd или добавлять новые задания tooexisting запросов.

## <a name="customize-devices"></a>Настройка устройств

Одним из наиболее распространенных действий расширения hello работает со сценарием tooyour конкретного устройства. Существует несколько способов работы с устройствами. Это может быть изменение сценария toomatch имитированное устройство или с помощью hello [SDK устройств IoT] [ IoT Device SDK] tooconnect toohello решения физического устройства.

Пошаговое руководство по tooadding устройств, в разделе hello [Iot Suite подключение устройств](iot-suite-connecting-devices.md) статьи и hello [удаленного мониторинга образца пакета SDK C](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer/samples/remote_monitoring). Этот образец является спроектированный toowork с hello удаленное наблюдение предварительно настроенных решений.

### <a name="create-your-own-simulated-device"></a>Создание собственного виртуального устройства

Включенные в hello [удаленное наблюдение исходного кода решения](https://github.com/Azure/azure-iot-remote-monitoring), является симулятор .NET. Это симулятор является hello один подготовить как часть решения hello и можно изменить его toosend различные метаданные, телеметрии и реагирования на команды toodifferent и методы.

предварительно настроенный симулятор Hello в удаленное наблюдение предварительно настроенных решений hello имитирует охлаждающего устройства, которое выдает температуры и влажности телеметрии. Вы можете изменить симулятор hello в hello [Simulator.WebJob](https://github.com/Azure/azure-iot-remote-monitoring/tree/master/Simulator/Simulator.WebJob) проекта при разделенными репозитории GitHub hello.

### <a name="available-locations-for-simulated-devices"></a>Доступные расположения для виртуальных устройств

набор по умолчанию Hello расположения — Сиэтл и Редмонд, штат Вашингтон, США. Эти расположения можно изменить в файле [SampleDeviceFactory.cs][lnk-sample-device-factory].

### <a name="add-a-desired-property-update-handler-toohello-simulator"></a>Добавьте обработчик toohello нужного свойства обновления симулятора

Можно задать значение для нужного свойства для устройства на портале решения hello. Ответственность hello запроса на изменение hello устройства toohandle hello свойство состоит в том случае, когда устройство hello извлекает значение свойства hello требуемого. Поддержка tooadd для изменения значения свойства через нужное свойство, необходимо tooadd симулятора toohello обработчика.

Имитатор Hello содержит обработчики для hello **SetPointTemp** и **TelemetryInterval** свойства, которые можно обновить, установив требуемого значения hello решение портала.

Hello примере показан обработчик hello hello **SetPointTemp** требуемого свойства в hello **CoolerDevice** класса:

```csharp
protected async Task OnSetPointTempUpdate(object value)
{
    var telemetry = _telemetryController as ITelemetryWithSetPointTemperature;
    telemetry.SetPointTemperature = Convert.ToDouble(value);

    await SetReportedPropertyAsync(SetPointTempPropertyName, telemetry.SetPointTemperature);
}
```

Этот метод обновляет точки данных телеметрии hello температуры, а затем отчеты hello изменить задней tooIoT концентратора, задав свойство отчета.

Можно добавить собственные обработчики для собственные свойства по следующему шаблону hello в предшествующих пример hello.

Необходимо также привязать обработчик toohello hello нужное свойство, как показано в следующий пример из hello hello **CoolerDevice** конструктор:

```csharp
_desiredPropertyUpdateHandlers.Add(SetPointTempPropertyName, OnSetPointTempUpdate);
```

Обратите внимание, что **SetPointTempPropertyName** — это константа, определенная как Config.SetPointTemp.

### <a name="add-support-for-a-new-method-toohello-simulator"></a>Добавить поддержку нового симулятор toohello метод

Вы можете настроить hello симулятор tooadd поддержка новый [(прямой) метод][lnk-direct-methods]. Нужно выполнить два основных действия.

- Имитатор Hello необходимо уведомить центра IoT hello в решении hello предварительно настроен с данные метода hello.
- Имитатор Hello должен включать вызов метода hello toohandle кода, при вызове из hello **сведений об устройстве** панель в обозревателе решений hello или с помощью задания.

Hello удаленный мониторинг предварительно настроенное решение использует *сообщил свойства* toosend подробные сведения о поддерживаемых методах tooIoT концентратора. серверной части решения Hello поддерживает список всех методов hello, поддерживаемые для каждого устройства, а также журнал вызовов методов. Можно просмотреть эти сведения об устройствах и вызывать методы в портал hello решения.

Центр IoT hello toonotify, устройство поддерживает метод, hello устройства необходимо добавить сведения о hello метод toohello **SupportedMethods** узел в hello сообщил свойства:

```json
"SupportedMethods": {
  "<method signature>": "<method description>",
  "<method signature>": "<method description>"
}
```

Hello сигнатура метода имеет следующий формат hello: `<method name>--<parameter #0 name>-<parameter #1 type>-...-<parameter #n name>-<parameter #n type>`. Например, hello toospecify **InitiateFirmwareUpdate** методе ожидается строковый параметр с именем **FwPackageURI**, использовать hello, следуя сигнатуру метода:

```json
InitiateFirmwareUpate--FwPackageURI-string: "description of method"
```

Список поддерживаемых типов параметров см. в разделе hello **CommandTypes** класса в проекте инфраструктуры hello.

метод toodelete задать подпись метода hello слишком`null` включается в hello свойства.

> [!NOTE]
> Hello серверной части решения обновляет только сведения о поддерживаемых методах при получении *сведений об устройстве* сообщение hello устройства.

Следующий образец кода из hello Hello **SampleDeviceFactory** класса в hello общего проекта показано, как tooadd список toohello метод из **SupportedMethods** включается в hello свойства отправленных hello устройство:

```csharp
device.Commands.Add(new Command(
    "InitiateFirmwareUpdate",
    DeliveryType.Method,
    "Updates device Firmware. Use parameter 'FwPackageUri' toospecifiy hello URI of hello firmware file, e.g. https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin",
    new[] { new Parameter("FwPackageUri", "string") }
));
```

Этот фрагмент кода добавляет сведения о hello **InitiateFirmwareUpdate** метода, включая текст toodisplay портале решения hello и подробные сведения о hello необходимые параметры метода.

Имитатор Hello отправляет выводятся свойства, включая hello список поддерживаемых методов tooIoT концентратора при запуске симулятор hello.

Добавьте код обработчика toohello имитатор для каждого метода, который он поддерживает. Вы увидите hello существующих обработчиков в hello **CoolerDevice** класса в проекте Simulator.WebJob hello. Hello примере показан обработчик hello **InitiateFirmwareUpdate** метод:

```csharp
public async Task<MethodResponse> OnInitiateFirmwareUpdate(MethodRequest methodRequest, object userContext)
{
    if (_deviceManagementTask != null && !_deviceManagementTask.IsCompleted)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "Device is busy"
        }, 409));
    }

    try
    {
        var operation = new FirmwareUpdate(methodRequest);
        _deviceManagementTask = operation.Run(Transport).ContinueWith(async task =>
        {
            // after firmware completed, we reset telemetry
            var telemetry = _telemetryController as ITelemetryWithTemperatureMeanValue;
            if (telemetry != null)
            {
                telemetry.TemperatureMeanValue = 34.5;
            }

            await UpdateReportedTemperatureMeanValue();
        });

        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = "FirmwareUpdate accepted",
            Uri = operation.Uri
        }));
    }
    catch (Exception ex)
    {
        return await Task.FromResult(BuildMethodRespose(new
        {
            Message = ex.Message
        }, 400));
    }
}
```

Метод обработчика имена должны начинаться с `On` следуют hello имя метода hello. Hello **methodRequest** параметр содержит все передаваемые с помощью вызова метода hello из серверной части решения hello. Hello возвращаемое значение должно быть типа **задачи&lt;MethodResponse&gt;**. Hello **BuildMethodResponse** вспомогательный метод служит для создания hello возвращаемое значение.

В обработчике метод hello можно выполнить следующее.

- Запустить асинхронную задачу.
- Загрузить нужные свойства из hello *двойных устройства* в центр IoT.
- Обновления одного свойства отчета с помощью hello **SetReportedPropertyAsync** метод в hello **CoolerDevice** класса.
- Обновить несколько свойств отчета, создав **TwinCollection** экземпляра и вызова hello **Transport.UpdateReportedPropertiesAsync** метод.

Hello предыдущий пример обновления встроенного по выполняет следующие шаги hello.

- Проверяет hello устройство является запрос на обновление встроенного по может tooaccept hello.
- Асинхронно запускает операцию обновления встроенного по hello и сбрасывает данные телеметрии hello после завершения операции hello.
- Сразу же возвращает Здравствуйте «FirmwareUpdate принято» сообщения tooindicate hello запрос принят устройством hello.

### <a name="build-and-use-your-own-physical-device"></a>Построение и использование собственного (физического) устройства

Hello [пакеты SDK Azure IoT](https://github.com/Azure/azure-iot-sdks) предоставляют библиотеки для подключения различных типов устройств (языков и операционных систем) в решения IoT.

## <a name="modify-dashboard-limits"></a>Изменение ограничений панели мониторинга

### <a name="number-of-devices-displayed-in-dashboard-dropdown"></a>Количество устройств, отображаемых в раскрывающемся списке панели мониторинга

по умолчанию Hello — 200. Это количество можно изменить в файле [DashboardController.cs][lnk-dashboard-controller].

### <a name="number-of-pins-toodisplay-in-bing-map-control"></a>Количество toodisplay ПИН-кодов в элементе управления карты Bing

по умолчанию Hello — 200. Это количество можно изменить в файле [TelemetryApiController.cs][lnk-telemetry-api-controller-01].

### <a name="time-period-of-telemetry-graph"></a>Период времени графика телеметрии

по умолчанию Hello — 10 минут. Это значение можно изменить в файле [TelmetryApiController.cs][lnk-telemetry-api-controller-02].

## <a name="manually-set-up-application-roles"></a>Настройка ролей приложений вручную

Hello ниже описано, как tooadd **администратора** и **ReadOnly** tooa ролей приложения предварительно настроенных решений. Обратите внимание, что предварительно настроенных решений, которые уже подготовлены с сайта azureiotsuite.com hello включает hello **администратора** и **ReadOnly** ролей.

Члены hello **ReadOnly** роли можно увидеть панели мониторинга hello и hello список устройств, но не допускаются tooadd устройств, изменение атрибутов устройства или команд отправки.  Члены hello **администратора** роль имеет полный доступ tooall hello функциональность в решении hello.

1. Go toohello [классический портал Azure][lnk-classic-portal].
2. Выберите **Active Directory**.
3. Щелкните имя hello клиента AAD hello, которая использовалась при подготовке решения.
4. Щелкните **Приложения**.
5. Щелкните имя приложения hello, совпадающим с именем предварительно настроенных решений hello. Если вы не видите в списке hello приложения, выберите **приложений, которыми владеет Моя компания** в hello **Показать** раскрывающегося списка и нажмите кнопку hello флажок.
6. Внизу hello страницы приветствия щелкните **управление манифеста** и затем **загрузки манифеста**.
7. Эта процедура загружает файл .json tooyour локального компьютера. Откройте этот файл для редактирования в любом текстовом редакторе.
8. В hello третья строка hello JSON-файл можно увидеть:

   ```json
   "appRoles" : [],
   ```
   Замените эту строку hello, следующий код:

   ```json
   "appRoles": [
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Administrator access toohello application",
   "displayName": "Admin",
   "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
   "isEnabled": true,
   "value": "Admin"
   },
   {
   "allowedMemberTypes": [
   "User"
   ],
   "description": "Read only access toodevice information",
   "displayName": "Read Only",
   "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
   "isEnabled": true,
   "value": "ReadOnly"
   } ],
   ```

9. Сохраните Обновленный JSON-файл hello (можно перезаписать существующий файл hello).
10. В hello классический портал Azure, hello нижней части страницы приветствия выберите **управление манифеста** затем **отправить манифест** tooupload hello JSON-файл был сохранен на предыдущем шаге hello.
11. Теперь вы добавили hello **администратора** и **ReadOnly** ролей tooyour приложения.
12. tooassign один пользователь tooa эти роли в каталоге, в разделе [разрешения на сайт hello azureiotsuite.com][lnk-permissions].

## <a name="feedback"></a>Отзыв

У вас есть настройки хотелось бы toosee, рассматриваемые в данном документе? Добавление предложения функция слишком[User Voice](https://feedback.azure.com/forums/321918-azure-iot), или оставьте комментарий для этой статьи. 

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о hello варианты настройки hello предварительно настроенных решений, см.:

* [Подключение приложения логики tooyour IoT Suite удаленного мониторинга Azure предварительно настроенных решения][lnk-logicapp]
* [Используйте динамические данные телеметрии с hello удаленное наблюдение предварительно настроенных решений][lnk-dynamic]
* [Устройство сведения метаданных в удаленное наблюдение предварительно настроенных решений hello][lnk-devinfo]
* [Настроить способ hello подключения фабрики решений отображает данные с серверов OPC UA][lnk-cf-customize]

[lnk-logicapp]: iot-suite-logic-apps-tutorial.md
[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[IoT Device SDK]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-permissions]: iot-suite-permissions.md
[lnk-dashboard-controller]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/Controllers/DashboardController.cs#L27
[lnk-telemetry-api-controller-01]: https://github.com/Azure/azure-iot-remote-monitoring/blob/3fd43b8a9f7e0f2774d73f3569439063705cebe4/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L27
[lnk-telemetry-api-controller-02]: https://github.com/Azure/azure-iot-remote-monitoring/blob/e7003339f73e21d3930f71ceba1e74fb5c0d9ea0/DeviceAdministration/Web/WebApiControllers/TelemetryApiController.cs#L25 
[lnk-sample-device-factory]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Common/Factory/SampleDeviceFactory.cs#L40
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-cf-customize]: iot-suite-connected-factory-customize.md