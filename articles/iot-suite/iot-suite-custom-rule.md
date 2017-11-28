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
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="9e1a1-103">Создание пользовательского правила hello удаленное наблюдение предварительно настроенных решений</span><span class="sxs-lookup"><span data-stu-id="9e1a1-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="9e1a1-104">Введение</span><span class="sxs-lookup"><span data-stu-id="9e1a1-104">Introduction</span></span>

<span data-ttu-id="9e1a1-105">В решениях hello предварительно настроен, можно настроить [значение правила, которые активированы при телеметрии для устройства, достигает определенного порога][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="9e1a1-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="9e1a1-106">[Используйте динамические данные телеметрии с hello удаленное наблюдение предварительно настроенных решений] [ lnk-dynamic-telemetry] описывает, как добавить пользовательскую телеметрию значения, такие как *ExternalTemperature* tooyour решения.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="9e1a1-107">В этой статье показано, как типы toocreate настраиваемое правило для динамического телеметрии в решении.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="9e1a1-108">В этом учебнике используется простой Node.js имитированное устройство toogenerate динамического телеметрии toosend toohello предварительно настроенных решений серверную часть.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="9e1a1-109">Затем можно добавить пользовательские правила в hello **RemoteMonitoring** решения Visual Studio и развертывать этот настроенный серверной части tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="9e1a1-110">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="9e1a1-111">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-111">An active Azure subscription.</span></span> <span data-ttu-id="9e1a1-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9e1a1-113">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="9e1a1-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="9e1a1-114">[Node.js] [ lnk-node] версии 0.12.x или более поздней версии toocreate имитированное устройство.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="9e1a1-115">Visual Studio 2015 или Visual Studio 2017 г toomodify hello предварительно настроенное решение обратно заканчиваться новых правил.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="9e1a1-116">Запишите имя решения hello, выбранная для развертывания.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="9e1a1-117">Это имя понадобится вам дальше.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="9e1a1-118">Можно остановить hello Node.js консольного приложения, когда вы убедились, что он отправляет **ExternalTemperature** toohello телеметрии предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="9e1a1-119">Не закрывайте окно консоли hello поскольку снова запустите это консольное приложение Node.js после добавления решения toohello hello настраиваемое правило.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="9e1a1-120">Расположения хранения правил</span><span class="sxs-lookup"><span data-stu-id="9e1a1-120">Rule storage locations</span></span>

<span data-ttu-id="9e1a1-121">Сведения о правилах сохраняются в двух расположениях:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="9e1a1-122">**DeviceRulesNormalizedTable** таблице — в этой таблице хранятся нормализованный ссылки toohello правилами, определенными в портал hello решения.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="9e1a1-123">Когда hello решения портал отобразит правилами для устройств, он запрашивает этой таблицы для определения правил hello.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="9e1a1-124">**DeviceRules** BLOB-объекта — Этот большой двоичный объект сохраняет hello правила, определенные все зарегистрированные устройства и определяется как задания Azure Stream Analytics ввода toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="9e1a1-125">При обновлении существующего правила или определить новое правило в портал решения hello, таблица hello и больших двоичных объектов изменяются обновленные tooreflect hello.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="9e1a1-126">Hello правила определения отображается на портале hello извлекаются из хранилища таблиц hello и hello правила определения ссылается заданий Stream Analytics hello поступает из hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="9e1a1-127">Обновить решение RemoteMonitoring Visual Studio hello</span><span class="sxs-lookup"><span data-stu-id="9e1a1-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="9e1a1-128">Hello следующие шаги показывают, как toomodify hello tooinclude решения RemoteMonitoring Visual Studio новое правило, который использует hello **ExternalTemperature** телеметрии, отправленные hello имитированное устройство:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="9e1a1-129">Если вы еще не сделано, клон hello **azure iot удаленного мониторинга** репозитория tooa подходящее расположение на локальном компьютере, используя следующую команду Git hello:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="9e1a1-130">В Visual Studio откройте файл RemoteMonitoring.sln hello из локальной копии hello **azure iot удаленного мониторинга** репозитория.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="9e1a1-131">Откройте файл hello Infrastructure\Models\DeviceRuleBlobEntity.cs и добавьте **ExternalTemperature** свойства следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="9e1a1-132">В hello того же файла, добавьте **ExternalTemperatureRuleOutput** свойства следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="9e1a1-133">Откройте файл hello Infrastructure\Models\DeviceRuleDataFields.cs и добавьте следующее hello **ExternalTemperature** свойство после существующих hello **влажность** свойство:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="9e1a1-134">В hello того же файла, обновить hello **_availableDataFields** tooinclude метод **ExternalTemperature** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="9e1a1-135">Откройте файл hello Infrastructure\Repository\DeviceRulesRepository.cs и изменить hello **BuildBlobEntityListFromTableRows** метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="9e1a1-136">Повторить сборку и развертывание решения hello.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="9e1a1-137">Теперь можно развернуть hello обновить решение tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="9e1a1-138">Откройте окно командной строки с повышенными привилегиями и перейдите корневой toohello локальной копии hello azure iot удаленного мониторинга репозитория.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="9e1a1-139">toodeploy обновленного решения, запустите следующие команды, подставив вместо hello **{имя развертывания}** с именем hello, записанное ранее развертывания предварительно настроенных решений:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="9e1a1-140">Обновить задание Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="9e1a1-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="9e1a1-141">После завершения развертывания hello можно обновить hello Stream Analytics toouse hello новое правило определения заданий.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="9e1a1-142">В hello портал Azure перейдите toohello группы ресурсов, содержащий ресурсы предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="9e1a1-143">Эта группа ресурсов имеет точно такое же имя, которое указано для hello hello решения во время развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="9e1a1-144">Перейдите toohello {имя развертывания}-задания Stream Analytics правила.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="9e1a1-145">Нажмите кнопку **остановить** выполняемого задания Stream Analytics hello toostop.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="9e1a1-146">(Необходимо дождаться hello потоковой передачи toostop задания, прежде чем редактировать запрос hello).</span><span class="sxs-lookup"><span data-stu-id="9e1a1-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="9e1a1-147">Щелкните **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-147">Click **Query**.</span></span> <span data-ttu-id="9e1a1-148">Изменить hello запроса tooinclude hello **ВЫБЕРИТЕ** инструкции для **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="9e1a1-149">Hello ниже приведен пример hello полный запрос с hello новый **ВЫБЕРИТЕ** инструкции:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="9e1a1-150">Нажмите кнопку **Сохранить** toochange hello обновить правила запроса.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="9e1a1-151">Нажмите кнопку **запустить** еще раз запустить задание Stream Analytics hello toostart.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="9e1a1-152">Добавить новое правило в панели мониторинга hello</span><span class="sxs-lookup"><span data-stu-id="9e1a1-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="9e1a1-153">Теперь вы можете добавить hello **ExternalTemperature** устройства tooa правило в панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="9e1a1-154">Перейдите toohello решение портала.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="9e1a1-155">Перейдите toohello **устройств** панель.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="9e1a1-156">Найдите hello настраиваемые параметры устройства вы создали, отправляющий **ExternalTemperature** телеметрии и на hello **сведений об устройстве** нажмите кнопку **добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="9e1a1-157">Выберите значение **ExternalTemperature** для параметра **Поле данных**.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="9e1a1-158">Задать **пороговое значение** too56.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-158">Set **Threshold** too56.</span></span> <span data-ttu-id="9e1a1-159">Щелкните **Сохранить и просмотреть правила**.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="9e1a1-160">Возвращает toohello мониторинга tooview hello звуковых сигналов журнала.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="9e1a1-161">В окне консоли hello вы оставлена открытой, запуска консольного приложения hello Node.js toobegin отправки **ExternalTemperature** данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="9e1a1-162">Обратите внимание, что hello **журнал сигнала** таблице показаны новые предупреждения при запуске нового правила hello.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="9e1a1-163">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="9e1a1-163">Additional information</span></span>

<span data-ttu-id="9e1a1-164">Изменение оператора hello  **>**  является более сложной и выходит за рамки hello шаги, описанные в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="9e1a1-165">Хотя toouse задания Stream Analytics hello можно изменять независимо от оператора, вам нравится, отражения оператор портале hello решение является более сложной задачей.</span><span class="sxs-lookup"><span data-stu-id="9e1a1-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9e1a1-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e1a1-166">Next steps</span></span>
<span data-ttu-id="9e1a1-167">Теперь, когда вы познакомились с как toocreate настраиваемых правил, Дополнительные сведения о hello предварительно настроенных решений:</span><span class="sxs-lookup"><span data-stu-id="9e1a1-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="9e1a1-168">[Подключение приложения логики tooyour IoT Suite удаленного мониторинга Azure предварительно настроенных решения][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="9e1a1-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="9e1a1-169">[Метаданные сведения устройства в удаленный мониторинг hello предварительно настроенное решение][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="9e1a1-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md