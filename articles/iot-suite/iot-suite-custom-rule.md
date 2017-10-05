---
title: "Создание настраиваемых правил в Azure IoT Suite | Документация Майкрософт"
description: "Создание настраиваемых правил в предварительно настроенном решении Azure IoT Suite."
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
ms.openlocfilehash: d58c27234ea05a82aaa3e8d72f70c1449980df09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-custom-rule-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="b69ac-103">Создание настраиваемого правила в предварительно настроенном решении для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="b69ac-103">Create a custom rule in the remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="b69ac-104">Введение</span><span class="sxs-lookup"><span data-stu-id="b69ac-104">Introduction</span></span>

<span data-ttu-id="b69ac-105">В предварительно настроенных решениях вы можете создавать [правила, которые активируются при достижении определенного порога для значения телеметрии устройства][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="b69ac-105">In the preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="b69ac-106">В статье [Использование динамической телеметрии с предварительно настроенным решением для удаленного мониторинга][lnk-dynamic-telemetry] описывается, как добавлять в решение пользовательские параметры телеметрии, например *ExternalTemperature*.</span><span class="sxs-lookup"><span data-stu-id="b69ac-106">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* to your solution.</span></span> <span data-ttu-id="b69ac-107">В этой статье показано, как создать в решении настраиваемое правило для динамических типов данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="b69ac-107">This article shows you how to create custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="b69ac-108">В этом руководстве мы с помощью простого виртуального устройства, созданного на основе Node.js, будем генерировать динамические данные телеметрии для отправки в серверную часть предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="b69ac-108">This tutorial uses a simple Node.js simulated device to generate dynamic telemetry to send to the preconfigured solution back end.</span></span> <span data-ttu-id="b69ac-109">Затем вы добавите настраиваемые правила в решение Visual Studio **RemoteMonitoring** и развернете настроенную серверную часть в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="b69ac-109">You then add custom rules in the **RemoteMonitoring** Visual Studio solution and deploy this customized back end to your Azure subscription.</span></span>

<span data-ttu-id="b69ac-110">Для работы с этим учебником необходимы указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="b69ac-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="b69ac-111">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="b69ac-111">An active Azure subscription.</span></span> <span data-ttu-id="b69ac-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b69ac-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b69ac-113">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="b69ac-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="b69ac-114">[Node.js][lnk-node] 0.12.x или более поздней версии для создания виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="b69ac-114">[Node.js][lnk-node] version 0.12.x or later to create a simulated device.</span></span>
* <span data-ttu-id="b69ac-115">Visual Studio 2015 или Visual Studio 2017 для внесения новых правил в серверную часть предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="b69ac-115">Visual Studio 2015 or Visual Studio 2017 to modify the preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="b69ac-116">Запишите имя решения, которое вы выбрали для развертывания.</span><span class="sxs-lookup"><span data-stu-id="b69ac-116">Make a note of the solution name you chose for your deployment.</span></span> <span data-ttu-id="b69ac-117">Это имя понадобится вам дальше.</span><span class="sxs-lookup"><span data-stu-id="b69ac-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="b69ac-118">Вы можете остановить консольное приложение Node.js, когда убедитесь, что оно отправляет телеметрию **ExternalTemperature** в предварительно настроенное решение.</span><span class="sxs-lookup"><span data-stu-id="b69ac-118">You can stop the Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry to the preconfigured solution.</span></span> <span data-ttu-id="b69ac-119">Не закрывайте окно консоли, так как это консольное приложение Node.js нужно запустить еще раз, когда будет добавлено настраиваемое правило.</span><span class="sxs-lookup"><span data-stu-id="b69ac-119">Keep the console window open because you run this Node.js console app again after you add the custom rule to the solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="b69ac-120">Расположения хранения правил</span><span class="sxs-lookup"><span data-stu-id="b69ac-120">Rule storage locations</span></span>

<span data-ttu-id="b69ac-121">Сведения о правилах сохраняются в двух расположениях:</span><span class="sxs-lookup"><span data-stu-id="b69ac-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="b69ac-122">Таблица **DeviceRulesNormalizedTable**, в которой хранятся нормализованные ссылки на правила, определенные на портале решения.</span><span class="sxs-lookup"><span data-stu-id="b69ac-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference to the rules defined by the solution portal.</span></span> <span data-ttu-id="b69ac-123">Когда портал решения отображает правила устройства, он отправляет запрос в эту таблицу на получение определений правил.</span><span class="sxs-lookup"><span data-stu-id="b69ac-123">When the solution portal displays device rules, it queries this table for the rule definitions.</span></span>
* <span data-ttu-id="b69ac-124">Большой двоичный объект **DeviceRules**, который хранит все правила, определенные для всех зарегистрированных устройств. Он определен как источник ссылочных данных для заданий Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="b69ac-124">**DeviceRules** blob – This blob stores all the rules defined for all registered devices and is defined as a reference input to the Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="b69ac-125">Когда вы изменяете существующее правило или создаете новое на портале решения, необходимые изменения вносятся одновременно в таблицу и в большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="b69ac-125">When you update an existing rule or define a new rule in the solution portal, both the table and blob are updated to reflect the changes.</span></span> <span data-ttu-id="b69ac-126">Определения правил, которые отображаются на портале, поступают из таблицы хранилища. Определения правила, на которые ссылаются задания Stream Analytics, извлекаются из большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="b69ac-126">The rule definition displayed in the portal comes from the table store, and the rule definition referenced by the Stream Analytics jobs comes from the blob.</span></span> 

## <a name="update-the-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="b69ac-127">Обновление решения Visual Studio RemoteMonitoring</span><span class="sxs-lookup"><span data-stu-id="b69ac-127">Update the RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="b69ac-128">Ниже показано, как добавить в решение Visual Studio RemoteMonitoring новое правило, которое использует телеметрию **ExternalTemperature**, отправляемую виртуальным устройством.</span><span class="sxs-lookup"><span data-stu-id="b69ac-128">The following steps show you how to modify the RemoteMonitoring Visual Studio solution to include a new rule that uses the **ExternalTemperature** telemetry sent from the simulated device:</span></span>

1. <span data-ttu-id="b69ac-129">Клонируйте репозиторий **azure-iot-remote-monitoring** в любое удобное расположение на локальном компьютере, если вы этого не сделали ранее, с помощью такой команды Git:</span><span class="sxs-lookup"><span data-stu-id="b69ac-129">If you have not already done so, clone the **azure-iot-remote-monitoring** repository to a suitable location on your local machine using the following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="b69ac-130">В Visual Studio откройте файл RemoteMonitoring.sln из локальной копии репозитория **azure-iot-remote-monitoring**.</span><span class="sxs-lookup"><span data-stu-id="b69ac-130">In Visual Studio, open the RemoteMonitoring.sln file from your local copy of the **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="b69ac-131">Откройте файл Infrastructure\Models\DeviceRuleBlobEntity.cs и добавьте свойство **ExternalTemperature** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b69ac-131">Open the file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="b69ac-132">В тот же файл добавьте свойство **ExternalTemperatureRuleOutput**:</span><span class="sxs-lookup"><span data-stu-id="b69ac-132">In the same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="b69ac-133">Откройте файл Infrastructure\Models\DeviceRuleDataFields.cs и добавьте представленное ниже свойство **ExternalTemperature** после существующего свойства **Humidity**:</span><span class="sxs-lookup"><span data-stu-id="b69ac-133">Open the file Infrastructure\Models\DeviceRuleDataFields.cs and add the following **ExternalTemperature** property after the existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="b69ac-134">В том же файле измените метод **_availableDataFields**, чтобы он содержал **ExternalTemperature**, вот так:</span><span class="sxs-lookup"><span data-stu-id="b69ac-134">In the same file, update the **_availableDataFields** method to include **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="b69ac-135">Откройте файл Infrastructure\Repository\DeviceRulesRepository.cs и измените метод **BuildBlobEntityListFromTableRows** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b69ac-135">Open the file Infrastructure\Repository\DeviceRulesRepository.cs and modify the **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-the-solution"></a><span data-ttu-id="b69ac-136">Заново создайте и повторно разверните это решение.</span><span class="sxs-lookup"><span data-stu-id="b69ac-136">Rebuild and redeploy the solution.</span></span>

<span data-ttu-id="b69ac-137">Теперь его можно развернуть в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="b69ac-137">You can now deploy the updated solution to your Azure subscription.</span></span>

1. <span data-ttu-id="b69ac-138">Откройте командную строку с повышенными правами и перейдите к корню локальной копии репозитория azure-iot-remote-monitoring.</span><span class="sxs-lookup"><span data-stu-id="b69ac-138">Open an elevated command prompt and navigate to the root of your local copy of the azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="b69ac-139">Чтобы развернуть обновленное решение, выполните следующие команды, заменив **{deployment name}** именем предварительно настроенного решения, которое вы записали ранее:</span><span class="sxs-lookup"><span data-stu-id="b69ac-139">To deploy your updated solution, run the following command substituting **{deployment name}** with the name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-the-stream-analytics-job"></a><span data-ttu-id="b69ac-140">Обновление задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b69ac-140">Update the Stream Analytics job</span></span>

<span data-ttu-id="b69ac-141">Когда развертывание завершится, можно обновить задание Stream Analytics, чтобы оно использовало новые определения правил.</span><span class="sxs-lookup"><span data-stu-id="b69ac-141">When the deployment is complete, you can update the Stream Analytics job to use the new rule definitions.</span></span>

1. <span data-ttu-id="b69ac-142">На портале Azure перейдите в группу ресурсов, которая содержит ресурсы предварительно настроенного решения.</span><span class="sxs-lookup"><span data-stu-id="b69ac-142">In the Azure portal, navigate to the resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="b69ac-143">Эта группа ресурсов имеет то же имя, которое вы указали для решения во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="b69ac-143">This resource group has the same name you specified for the solution during the deployment.</span></span>

2. <span data-ttu-id="b69ac-144">Перейдите к заданию Stream Analytics {deployment name}-Rules.</span><span class="sxs-lookup"><span data-stu-id="b69ac-144">Navigate to the {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="b69ac-145">Щелкните **Остановить**, чтобы прекратить выполнение задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="b69ac-145">Click **Stop** to stop the Stream Analytics job from running.</span></span> <span data-ttu-id="b69ac-146">(Прежде чем вносить изменения в запрос, дождитесь остановки задания потоковой передачи.)</span><span class="sxs-lookup"><span data-stu-id="b69ac-146">(You must wait for the streaming job to stop before you can edit the query).</span></span>

4. <span data-ttu-id="b69ac-147">Щелкните **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="b69ac-147">Click **Query**.</span></span> <span data-ttu-id="b69ac-148">Измените запрос, добавив в него инструкцию **SELECT** для параметра **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="b69ac-148">Edit the query to include the **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="b69ac-149">Далее представлен полный текст измененного запроса с новой инструкцией **SELECT**:</span><span class="sxs-lookup"><span data-stu-id="b69ac-149">The following sample shows the complete query with the new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="b69ac-150">Щелкните **Сохранить**, чтобы внести изменения в запрос для этого правила.</span><span class="sxs-lookup"><span data-stu-id="b69ac-150">Click **Save** to change the updated rule query.</span></span>

6. <span data-ttu-id="b69ac-151">Щелкните **Запустить**, чтобы снова включить задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="b69ac-151">Click **Start** to start the Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-the-dashboard"></a><span data-ttu-id="b69ac-152">Добавление нового правила на панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="b69ac-152">Add your new rule in the dashboard</span></span>

<span data-ttu-id="b69ac-153">Теперь можно добавить правило **ExternalTemperature** в устройство на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="b69ac-153">You can now add the **ExternalTemperature** rule to a device in the solution dashboard.</span></span>

1. <span data-ttu-id="b69ac-154">Перейдите на портал решения.</span><span class="sxs-lookup"><span data-stu-id="b69ac-154">Navigate to the solution portal.</span></span>

2. <span data-ttu-id="b69ac-155">Откройте панель **Устройства**.</span><span class="sxs-lookup"><span data-stu-id="b69ac-155">Navigate to the **Devices** panel.</span></span>

3. <span data-ttu-id="b69ac-156">Найдите созданное ранее пользовательское устройство, которое отправляет телеметрию **ExternalTemperature**, затем на панели **сведений об устройстве** щелкните **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="b69ac-156">Locate the custom device you created that sends **ExternalTemperature** telemetry and on the **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="b69ac-157">Выберите значение **ExternalTemperature** для параметра **Поле данных**.</span><span class="sxs-lookup"><span data-stu-id="b69ac-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="b69ac-158">Для параметра **Пороговое значение** задайте значение 56.</span><span class="sxs-lookup"><span data-stu-id="b69ac-158">Set **Threshold** to 56.</span></span> <span data-ttu-id="b69ac-159">Щелкните **Сохранить и просмотреть правила**.</span><span class="sxs-lookup"><span data-stu-id="b69ac-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="b69ac-160">Вернитесь к панели мониторинга, чтобы просмотреть историю оповещений.</span><span class="sxs-lookup"><span data-stu-id="b69ac-160">Return to the dashboard to view the alarm history.</span></span>

7. <span data-ttu-id="b69ac-161">В открытом окне консоли запустите консольное приложение Node.js, которое начнет отправлять данные телеметрии **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="b69ac-161">In the console window you left open, start the Node.js console app to begin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="b69ac-162">Обратите внимание, что в таблице **Alarm History** появляются новые сигналы при каждой активации нового правила.</span><span class="sxs-lookup"><span data-stu-id="b69ac-162">Notice that the **Alarm History** table shows new alarms when the new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="b69ac-163">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="b69ac-163">Additional information</span></span>

<span data-ttu-id="b69ac-164">Изменение оператора **>** является более сложной задачей и выходит за рамки процессов, описанных в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="b69ac-164">Changing the operator **>** is more complex and goes beyond the steps outlined in this tutorial.</span></span> <span data-ttu-id="b69ac-165">Вы можете изменить задание Stream Analytics, чтобы оно использовало любой удобный оператор, но отобразить этот оператор на портале решения намного сложнее.</span><span class="sxs-lookup"><span data-stu-id="b69ac-165">While you can change the Stream Analytics job to use whatever operator you like, reflecting that operator in the solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b69ac-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b69ac-166">Next steps</span></span>
<span data-ttu-id="b69ac-167">Теперь, когда вы узнали, как создавать настраиваемые правила, вы можете подробнее изучить предварительно настроенные решения.</span><span class="sxs-lookup"><span data-stu-id="b69ac-167">Now that you've seen how to create custom rules, you can learn more about the preconfigured solutions:</span></span>

- <span data-ttu-id="b69ac-168">[Руководство. Подключение приложения логики к предварительно настроенному решению для удаленного мониторинга Azure IoT Suite][lnk-logic-app].</span><span class="sxs-lookup"><span data-stu-id="b69ac-168">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="b69ac-169">[Метаданные сведений об устройстве в предварительно настроенном решении для удаленного мониторинга][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="b69ac-169">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md