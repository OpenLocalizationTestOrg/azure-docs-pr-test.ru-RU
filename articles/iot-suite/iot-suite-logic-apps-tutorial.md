---
title: "aaaAzure IoT Suite и Logic Apps | Документы Microsoft"
description: "Руководство по установке и toohook вверх tooAzure Logic Apps IoT Suite для бизнес-процесса."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="f5450-103">Учебник: Решение Azure IoT Suite удаленный мониторинг заранее настроенные приложения логики tooyour подключения</span><span class="sxs-lookup"><span data-stu-id="f5450-103">Tutorial: Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="f5450-104">Hello [Microsoft Azure IoT Suite] [ lnk-internetofthings] удаленное наблюдение предварительно настроенных решений является tooget удобно быстро начать работу с набор компонентов конца в конец которого дан пример решения IoT.</span><span class="sxs-lookup"><span data-stu-id="f5450-104">hello [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way tooget started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="f5450-105">Этот учебник поможет выполнить как tooadd приложения логики tooyour Microsoft Azure IoT Suite удаленный мониторинг предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="f5450-105">This tutorial walks you through how tooadd Logic App tooyour Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="f5450-106">Эти действия демонстрируют, как можно использовать еще более вашего решения IoT, подключив tooa бизнес-процесса.</span><span class="sxs-lookup"><span data-stu-id="f5450-106">These steps demonstrate how you can take your IoT solution even further by connecting it tooa business process.</span></span>

<span data-ttu-id="f5450-107">*Если вы ищете Пошаговое руководство по как удаленный мониторинг tooprovision предварительно настроенных решений, см. раздел [учебник: Приступая к работе с hello IoT предварительно настроенных решений][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="f5450-107">*If you’re looking for a walkthrough on how tooprovision a remote monitoring preconfigured solution, see [Tutorial: Get started with hello IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="f5450-108">Перед началом работы с данным учебником необходимо выполнить описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f5450-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="f5450-109">Удаленный мониторинг подготовки hello предварительно настроенное решение в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="f5450-109">Provision hello remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="f5450-110">Создание учетной записи SendGrid tooenable toosend сообщение электронной почты, которое запускает бизнес-процессов.</span><span class="sxs-lookup"><span data-stu-id="f5450-110">Create a SendGrid account tooenable you toosend an email that triggers your business process.</span></span> <span data-ttu-id="f5450-111">Бесплатную пробную учетную запись можно создать на сайте [SendGrid](https://sendgrid.com/) , нажав кнопку **Try for Free**(Попробовать бесплатно).</span><span class="sxs-lookup"><span data-stu-id="f5450-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="f5450-112">После регистрации для бесплатной пробной учетной записи, необходимо toocreate [ключ API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) в SendGrid, которая предоставляет разрешения toosend почты.</span><span class="sxs-lookup"><span data-stu-id="f5450-112">After you have registered for your free trial account, you need toocreate an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions toosend mail.</span></span> <span data-ttu-id="f5450-113">Этот ключ API должны далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="f5450-113">You need this API key later in hello tutorial.</span></span>

<span data-ttu-id="f5450-114">toocomplete этого учебника требуется Visual Studio 2015 или Visual Studio 2017 г toomodify hello действий в серверной части hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="f5450-114">toocomplete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 toomodify hello actions in hello preconfigured solution back end.</span></span>

<span data-ttu-id="f5450-115">При условии, что вы инициализированного удаленное наблюдение за предварительно настроенных решений, перейдите toohello группы ресурсов для этого решения в hello [портал Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="f5450-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate toohello resource group for that solution in hello [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="f5450-116">группы ресурсов Hello есть hello точно такое же имя, как hello решения именем вы выбрали при подготовке удаленного мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="f5450-116">hello resource group has hello same name as hello solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="f5450-117">В группе ресурсов hello вы увидите все hello подготовить ресурсы Azure для вашего решения, за исключением hello приложения Azure Active Directory, можно найти в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f5450-117">In hello resource group, you can see all hello provisioned Azure resources for your solution except for hello Azure Active Directory application that you can find in hello Azure Classic Portal.</span></span> <span data-ttu-id="f5450-118">Hello следующем снимке экрана показан пример **группы ресурсов** колонку для удаленного мониторинга предварительно настроенных решений:</span><span class="sxs-lookup"><span data-stu-id="f5450-118">hello following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="f5450-119">toobegin, Настройка toouse приложения hello логики с hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="f5450-119">toobegin, set up hello logic app toouse with hello preconfigured solution.</span></span>

## <a name="set-up-hello-logic-app"></a><span data-ttu-id="f5450-120">Настройка логики приложения hello</span><span class="sxs-lookup"><span data-stu-id="f5450-120">Set up hello Logic App</span></span>
1. <span data-ttu-id="f5450-121">Нажмите кнопку **добавить** вверху hello вашей колонки группы ресурсов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f5450-121">Click **Add** at hello top of your resource group blade in hello Azure portal.</span></span>
2. <span data-ttu-id="f5450-122">Найдите **Приложение логики**, выберите его и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f5450-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="f5450-123">Заполните hello **имя** и используйте hello же **подписки** и **группы ресурсов** , которые использовались при подготовке удаленного мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="f5450-123">Fill out hello **Name** and use hello same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="f5450-124">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f5450-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="f5450-125">После завершения развертывания появится hello логики приложения, указана как ресурс в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f5450-125">When your deployment completes, you can see hello Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="f5450-126">Нажмите кнопку колонки приложения логики toohello toonavigate логику приложения hello, выберите hello **пустое приложение логики** hello tooopen шаблона **конструктор приложений логики**.</span><span class="sxs-lookup"><span data-stu-id="f5450-126">Click hello Logic App toonavigate toohello Logic App blade, select hello **Blank Logic App** template tooopen hello **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="f5450-127">Выберите **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="f5450-127">Select **Request**.</span></span> <span data-ttu-id="f5450-128">Это действие указывает, что в качестве триггера выступает входящий HTTP-запрос с полезными данными в определенном формате JSON.</span><span class="sxs-lookup"><span data-stu-id="f5450-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="f5450-129">Вставьте следующий код в hello схемы JSON тело запроса hello:</span><span class="sxs-lookup"><span data-stu-id="f5450-129">Paste hello following code into hello Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="f5450-130">После сохранения логики приложения hello, но сначала необходимо добавить действие можно скопировать URL-адрес hello hello HTTP post.</span><span class="sxs-lookup"><span data-stu-id="f5450-130">You can copy hello URL for hello HTTP post after you save hello logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="f5450-131">Щелкните **+ Новый шаг** под своим триггером.</span><span class="sxs-lookup"><span data-stu-id="f5450-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="f5450-132">Затем выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="f5450-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="f5450-133">Найдите действие **SendGrid - Send email** (SendGrid — отправить письмо) и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="f5450-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="f5450-134">Введите имя подключения hello, например **SendGridConnection**, введите hello **ключ API SendGrid** были созданы при настройке учетной записи SendGrid и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="f5450-134">Enter a name for hello connection, such as **SendGridConnection**, enter hello **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="f5450-135">Добавление адресов электронной почты вы hello собственные tooboth **из** и **для** поля.</span><span class="sxs-lookup"><span data-stu-id="f5450-135">Add email addresses you own tooboth hello **From** and **To** fields.</span></span> <span data-ttu-id="f5450-136">Добавить **удаленного мониторинга оповещения [DeviceId]** toohello **субъекта** поля.</span><span class="sxs-lookup"><span data-stu-id="f5450-136">Add **Remote monitoring alert [DeviceId]** toohello **Subject** field.</span></span> <span data-ttu-id="f5450-137">В hello **тело сообщения электронной почты** поля, добавьте **устройства [DeviceId] сообщил [measurementName] со значением [measuredValue].**</span><span class="sxs-lookup"><span data-stu-id="f5450-137">In hello **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="f5450-138">Можно добавить **[DeviceId]**, **[measurementName]**, и **[measuredValue]** , щелкнув в hello **может вставлять данные из предыдущих шагов**раздел.</span><span class="sxs-lookup"><span data-stu-id="f5450-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in hello **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="f5450-139">Нажмите кнопку **Сохранить** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="f5450-139">Click **Save** in hello top menu.</span></span>
13. <span data-ttu-id="f5450-140">Нажмите кнопку hello **запроса** триггера и скопируйте hello **URL-адрес Http Post toothis** значение.</span><span class="sxs-lookup"><span data-stu-id="f5450-140">Click hello **Request** trigger and copy hello **Http Post toothis URL** value.</span></span> <span data-ttu-id="f5450-141">Этот URL-адрес потребуется далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="f5450-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="f5450-142">Приложения логики включить toorun [множество различных типов действий] [ lnk-logic-apps-actions] включая действий в Office 365.</span><span class="sxs-lookup"><span data-stu-id="f5450-142">Logic Apps enable you toorun [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a><span data-ttu-id="f5450-143">Настройка hello EventProcessor веб-задание</span><span class="sxs-lookup"><span data-stu-id="f5450-143">Set up hello EventProcessor Web Job</span></span>
<span data-ttu-id="f5450-144">В этом разделе подключиться к предварительно настроенных решений toohello логику приложения, созданного.</span><span class="sxs-lookup"><span data-stu-id="f5450-144">In this section, you connect your preconfigured solution toohello Logic App you created.</span></span> <span data-ttu-id="f5450-145">toocomplete этой задачи добавьте hello URL-адрес tootrigger hello приложения логики toohello действие, которое применяется, когда значение датчика устройства превышает пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="f5450-145">toocomplete this task, you add hello URL tootrigger hello Logic App toohello action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="f5450-146">Использовать git клиента tooclone hello последние версии hello [azure iot удаленного мониторинга репозитории github][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="f5450-146">Use your git client tooclone hello latest version of hello [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="f5450-147">Например:</span><span class="sxs-lookup"><span data-stu-id="f5450-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="f5450-148">В Visual Studio откройте hello **RemoteMonitoring.sln** из hello локальную копию репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="f5450-148">In Visual Studio, open hello **RemoteMonitoring.sln** from hello local copy of hello repository.</span></span>
3. <span data-ttu-id="f5450-149">Откройте hello **ActionRepository.cs** файла в hello **инфраструктуры\\репозитория** папки.</span><span class="sxs-lookup"><span data-stu-id="f5450-149">Open hello **ActionRepository.cs** file in hello **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="f5450-150">Обновление hello **actionIds** словарь с hello **URL-адрес Http Post toothis** записанными из логики приложения, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f5450-150">Update hello **actionIds** dictionary with hello **Http Post toothis URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. <span data-ttu-id="f5450-151">Сохранить изменения hello в решении и выйти из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f5450-151">Save hello changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-hello-command-line"></a><span data-ttu-id="f5450-152">Развертывание из командной строки hello</span><span class="sxs-lookup"><span data-stu-id="f5450-152">Deploy from hello command line</span></span>
<span data-ttu-id="f5450-153">В этом разделе развернуть обновленную версию hello удаленного мониторинга tooreplace hello версия решения выполняющихся в Azure.</span><span class="sxs-lookup"><span data-stu-id="f5450-153">In this section, you deploy your updated version of hello remote monitoring solution tooreplace hello version currently running in Azure.</span></span>

1. <span data-ttu-id="f5450-154">Следующие hello [настройки разработки] [ lnk-devsetup] tooset инструкции настройку среды для развертывания.</span><span class="sxs-lookup"><span data-stu-id="f5450-154">Following hello [dev set-up][lnk-devsetup] instructions tooset up your environment for deployment.</span></span>
2. <span data-ttu-id="f5450-155">toodeploy локально, выполните hello [локальное развертывание] [ lnk-localdeploy] инструкции.</span><span class="sxs-lookup"><span data-stu-id="f5450-155">toodeploy locally, follow hello [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="f5450-156">toodeploy toohello облако и обновить существующие развертывания облачной, выполните hello [облако развертывания] [ lnk-clouddeploy] инструкции.</span><span class="sxs-lookup"><span data-stu-id="f5450-156">toodeploy toohello cloud and update your existing cloud deployment, follow hello [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="f5450-157">Используйте имя hello исходного развертывания, как имя развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="f5450-157">Use hello name of your original deployment as hello deployment name.</span></span> <span data-ttu-id="f5450-158">Например, если вызывался hello исходного развертывания **demologicapp**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f5450-158">For example if hello original deployment was called **demologicapp**, use hello following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="f5450-159">При запуске сценария сборки hello убедитесь, что toouse hello же учетная запись Azure, подписки, регион и экземпляр Active Directory, который использовался при подготовке hello решения.</span><span class="sxs-lookup"><span data-stu-id="f5450-159">When hello build script runs, be sure toouse hello same Azure account, subscription, region, and Active Directory instance you used when you provisioned hello solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="f5450-160">Проверка приложения логики в действии</span><span class="sxs-lookup"><span data-stu-id="f5450-160">See your Logic App in action</span></span>
<span data-ttu-id="f5450-161">удаленный мониторинг предварительно настроенных решений Hello имеет два правила, установленные по умолчанию, при подготовке решения.</span><span class="sxs-lookup"><span data-stu-id="f5450-161">hello remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="f5450-162">Оба правила находятся на hello **SampleDevice001** устройства:</span><span class="sxs-lookup"><span data-stu-id="f5450-162">Both rules are on hello **SampleDevice001** device:</span></span>

* <span data-ttu-id="f5450-163">Температура > 38,00</span><span class="sxs-lookup"><span data-stu-id="f5450-163">Temperature > 38.00</span></span>
* <span data-ttu-id="f5450-164">Влажность > 48,00</span><span class="sxs-lookup"><span data-stu-id="f5450-164">Humidity > 48.00</span></span>

<span data-ttu-id="f5450-165">правило температуры Hello запускает hello **вызова сигнала** действие и hello влажности правило срабатывает hello **SendMessage** действие.</span><span class="sxs-lookup"><span data-stu-id="f5450-165">hello temperature rule triggers hello **Raise Alarm** action and hello Humidity rule triggers hello **SendMessage** action.</span></span> <span data-ttu-id="f5450-166">При условии, что вы использовали hello же URL-адрес для обоих действий hello **ActionRepository** класса триггеры логику приложения для этих правил.</span><span class="sxs-lookup"><span data-stu-id="f5450-166">Assuming you used hello same URL for both actions hello **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="f5450-167">Оба правила использования toosend SendGrid по электронной почте toohello **для** адрес с подробными сведениями hello предупреждения.</span><span class="sxs-lookup"><span data-stu-id="f5450-167">Both rules use SendGrid toosend an email toohello **To** address with details of hello alert.</span></span>

> [!NOTE]
> <span data-ttu-id="f5450-168">Hello логику приложения по-прежнему tootrigger каждый раз при достижении порогового значения hello.</span><span class="sxs-lookup"><span data-stu-id="f5450-168">hello Logic App continues tootrigger every time hello threshold is met.</span></span> <span data-ttu-id="f5450-169">tooavoid ненужные электронные сообщения, можно отключить правила hello в вашего решения портала или отключите hello приложения логики в hello [портал Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="f5450-169">tooavoid unnecessary emails, you can either disable hello rules in your solution portal or disable hello Logic App in hello [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="f5450-170">В дополнение к этому tooreceiving сообщений электронной почты, также видно при запуске приложения логики hello hello портала:</span><span class="sxs-lookup"><span data-stu-id="f5450-170">In addition tooreceiving emails, you can also see when hello Logic App runs in hello portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="f5450-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5450-171">Next steps</span></span>
<span data-ttu-id="f5450-172">Теперь, когда вы использовали приложения логики tooconnect hello предварительно настроенное решение tooa бизнес-процесс, изучите более подробную hello варианты настройки hello предварительно настроенных решений:</span><span class="sxs-lookup"><span data-stu-id="f5450-172">Now that you've used a Logic App tooconnect hello preconfigured solution tooa business process, you can learn more about hello options for customizing hello preconfigured solutions:</span></span>

* <span data-ttu-id="f5450-173">[Используйте динамические данные телеметрии с hello удаленное наблюдение предварительно настроенных решений][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="f5450-173">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="f5450-174">[Устройство сведения метаданных в удаленное наблюдение предварительно настроенных решений hello][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="f5450-174">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
