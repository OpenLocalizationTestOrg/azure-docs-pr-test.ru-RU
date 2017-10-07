---
title: "настраиваемое правило в Azure IoT Suite aaaCreate | Документы Microsoft"
description: "Как toocreate настраиваемое правило в IoT Suite предварительно настроенных решений."
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
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a>Создание пользовательского правила hello удаленное наблюдение предварительно настроенных решений

## <a name="introduction"></a>Введение

В решениях hello предварительно настроен, можно настроить [значение правила, которые активированы при телеметрии для устройства, достигает определенного порога][lnk-builtin-rule]. [Используйте динамические данные телеметрии с hello удаленное наблюдение предварительно настроенных решений] [ lnk-dynamic-telemetry] описывает, как добавить пользовательскую телеметрию значения, такие как *ExternalTemperature* tooyour решения. В этой статье показано, как типы toocreate настраиваемое правило для динамического телеметрии в решении.

В этом учебнике используется простой Node.js имитированное устройство toogenerate динамического телеметрии toosend toohello предварительно настроенных решений серверную часть. Затем можно добавить пользовательские правила в hello **RemoteMonitoring** решения Visual Studio и развертывать этот настроенный серверной части tooyour подписки Azure.

toocomplete этого учебника, необходимо:

* Активная подписка Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].
* [Node.js] [ lnk-node] версии 0.12.x или более поздней версии toocreate имитированное устройство.
* Visual Studio 2015 или Visual Studio 2017 г toomodify hello предварительно настроенное решение обратно заканчиваться новых правил.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

Запишите имя решения hello, выбранная для развертывания. Это имя понадобится вам дальше.

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

Можно остановить hello Node.js консольного приложения, когда вы убедились, что он отправляет **ExternalTemperature** toohello телеметрии предварительно настроенных решений. Не закрывайте окно консоли hello поскольку снова запустите это консольное приложение Node.js после добавления решения toohello hello настраиваемое правило.

## <a name="rule-storage-locations"></a>Расположения хранения правил

Сведения о правилах сохраняются в двух расположениях:

* **DeviceRulesNormalizedTable** таблице — в этой таблице хранятся нормализованный ссылки toohello правилами, определенными в портал hello решения. Когда hello решения портал отобразит правилами для устройств, он запрашивает этой таблицы для определения правил hello.
* **DeviceRules** BLOB-объекта — Этот большой двоичный объект сохраняет hello правила, определенные все зарегистрированные устройства и определяется как задания Azure Stream Analytics ввода toohello ссылки.
 
При обновлении существующего правила или определить новое правило в портал решения hello, таблица hello и больших двоичных объектов изменяются обновленные tooreflect hello. Hello правила определения отображается на портале hello извлекаются из хранилища таблиц hello и hello правила определения ссылается заданий Stream Analytics hello поступает из hello большого двоичного объекта. 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a>Обновить решение RemoteMonitoring Visual Studio hello

Hello следующие шаги показывают, как toomodify hello tooinclude решения RemoteMonitoring Visual Studio новое правило, который использует hello **ExternalTemperature** телеметрии, отправленные hello имитированное устройство:

1. Если вы еще не сделано, клон hello **azure iot удаленного мониторинга** репозитория tooa подходящее расположение на локальном компьютере, используя следующую команду Git hello:

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. В Visual Studio откройте файл RemoteMonitoring.sln hello из локальной копии hello **azure iot удаленного мониторинга** репозитория.

3. Откройте файл hello Infrastructure\Models\DeviceRuleBlobEntity.cs и добавьте **ExternalTemperature** свойства следующим образом:

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. В hello того же файла, добавьте **ExternalTemperatureRuleOutput** свойства следующим образом:

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. Откройте файл hello Infrastructure\Models\DeviceRuleDataFields.cs и добавьте следующее hello **ExternalTemperature** свойство после существующих hello **влажность** свойство:

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. В hello того же файла, обновить hello **_availableDataFields** tooinclude метод **ExternalTemperature** следующим образом:

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. Откройте файл hello Infrastructure\Repository\DeviceRulesRepository.cs и изменить hello **BuildBlobEntityListFromTableRows** метод следующим образом:

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a>Повторить сборку и развертывание решения hello.

Теперь можно развернуть hello обновить решение tooyour подписки Azure.

1. Откройте окно командной строки с повышенными привилегиями и перейдите корневой toohello локальной копии hello azure iot удаленного мониторинга репозитория.

2. toodeploy обновленного решения, запустите следующие команды, подставив вместо hello **{имя развертывания}** с именем hello, записанное ранее развертывания предварительно настроенных решений:

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a>Обновить задание Stream Analytics hello

После завершения развертывания hello можно обновить hello Stream Analytics toouse hello новое правило определения заданий.

1. В hello портал Azure перейдите toohello группы ресурсов, содержащий ресурсы предварительно настроенных решений. Эта группа ресурсов имеет точно такое же имя, которое указано для hello hello решения во время развертывания hello.

2. Перейдите toohello {имя развертывания}-задания Stream Analytics правила. 

3. Нажмите кнопку **остановить** выполняемого задания Stream Analytics hello toostop. (Необходимо дождаться hello потоковой передачи toostop задания, прежде чем редактировать запрос hello).

4. Щелкните **Запрос**. Изменить hello запроса tooinclude hello **ВЫБЕРИТЕ** инструкции для **ExternalTemperature**. Hello ниже приведен пример hello полный запрос с hello новый **ВЫБЕРИТЕ** инструкции:

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. Нажмите кнопку **Сохранить** toochange hello обновить правила запроса.

6. Нажмите кнопку **запустить** еще раз запустить задание Stream Analytics hello toostart.

## <a name="add-your-new-rule-in-hello-dashboard"></a>Добавить новое правило в панели мониторинга hello

Теперь вы можете добавить hello **ExternalTemperature** устройства tooa правило в панели мониторинга hello решения.

1. Перейдите toohello решение портала.

2. Перейдите toohello **устройств** панель.

3. Найдите hello настраиваемые параметры устройства вы создали, отправляющий **ExternalTemperature** телеметрии и на hello **сведений об устройстве** нажмите кнопку **добавить правило**.

4. Выберите значение **ExternalTemperature** для параметра **Поле данных**.

5. Задать **пороговое значение** too56. Щелкните **Сохранить и просмотреть правила**.

6. Возвращает toohello мониторинга tooview hello звуковых сигналов журнала.

7. В окне консоли hello вы оставлена открытой, запуска консольного приложения hello Node.js toobegin отправки **ExternalTemperature** данные телеметрии.

8. Обратите внимание, что hello **журнал сигнала** таблице показаны новые предупреждения при запуске нового правила hello.
 
## <a name="additional-information"></a>Дополнительная информация

Изменение оператора hello  **>**  является более сложной и выходит за рамки hello шаги, описанные в этом учебнике. Хотя toouse задания Stream Analytics hello можно изменять независимо от оператора, вам нравится, отражения оператор портале hello решение является более сложной задачей. 

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы познакомились с как toocreate настраиваемых правил, Дополнительные сведения о hello предварительно настроенных решений:

- [Подключение приложения логики tooyour IoT Suite удаленного мониторинга Azure предварительно настроенных решения][lnk-logic-app]
- [Метаданные сведения устройства в удаленный мониторинг hello предварительно настроенное решение][lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md