---
title: "Azure IoT Suite и приложения логики | Документация Майкрософт"
description: "Руководство по подключению приложений логики к Azure IoT Suite для бизнес-процесса."
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
ms.openlocfilehash: 2e7997e2a8bdeeec6083d40acb55e653f87e140b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-connect-logic-app-to-your-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="9c82d-103">Руководство. Подключение приложения логики к предварительно настроенному решению для удаленного мониторинга Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="9c82d-103">Tutorial: Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="9c82d-104">Предварительно настроенное решение для удаленного мониторинга [Microsoft Azure IoT Suite][lnk-internetofthings] позволяет быстро начать работу с полным набором возможностей, которыми обладает решение Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="9c82d-104">The [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way to get started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="9c82d-105">В этом учебнике описаны действия по добавлению приложения логики к предварительно настроенному решению для удаленного мониторинга Microsoft Azure IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="9c82d-105">This tutorial walks you through how to add Logic App to your Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="9c82d-106">Эти шаги показывают, как продвинуть свое решение IoT еще дальше, подключив его к бизнес-процессу.</span><span class="sxs-lookup"><span data-stu-id="9c82d-106">These steps demonstrate how you can take your IoT solution even further by connecting it to a business process.</span></span>

<span data-ttu-id="9c82d-107">*Если вы ищете пошаговое руководство по подготовке предварительно настроенного решения для удаленного мониторинга, обратитесь к статье [Учебник: начало работы с предварительно настроенными решениями][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="9c82d-107">*If you’re looking for a walkthrough on how to provision a remote monitoring preconfigured solution, see [Tutorial: Get started with the IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="9c82d-108">Перед началом работы с данным учебником необходимо выполнить описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="9c82d-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="9c82d-109">Подготовьте в своей подписке Azure предварительно настроенное решение для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="9c82d-109">Provision the remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="9c82d-110">Создайте учетную запись SendGrid для отправки сообщений электронной почты, которые будут запускать бизнес-процесс.</span><span class="sxs-lookup"><span data-stu-id="9c82d-110">Create a SendGrid account to enable you to send an email that triggers your business process.</span></span> <span data-ttu-id="9c82d-111">Бесплатную пробную учетную запись можно создать на сайте [SendGrid](https://sendgrid.com/) , нажав кнопку **Try for Free**(Попробовать бесплатно).</span><span class="sxs-lookup"><span data-stu-id="9c82d-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="9c82d-112">После регистрации бесплатной пробной учетной записи необходимо создать в SendGrid [ключ API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) , который предоставляет разрешения на отправку электронной почты.</span><span class="sxs-lookup"><span data-stu-id="9c82d-112">After you have registered for your free trial account, you need to create an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions to send mail.</span></span> <span data-ttu-id="9c82d-113">Ключ API используется далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9c82d-113">You need this API key later in the tutorial.</span></span>

<span data-ttu-id="9c82d-114">Для работы с этим руководством вам понадобится Visual Studio 2015 или Visual Studio 2017, чтобы изменять действия на серверной стороне предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="9c82d-114">To complete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 to modify the actions in the preconfigured solution back end.</span></span>

<span data-ttu-id="9c82d-115">Если вы уже подготовили предварительно настроенное решение для удаленного мониторинга, то перейдите к группе ресурсов для этого решения на [портале Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="9c82d-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate to the resource group for that solution in the [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="9c82d-116">Имя группы ресурсов совпадает с именем решения, которое было выбрано при подготовке решения для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="9c82d-116">The resource group has the same name as the solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="9c82d-117">В группе ресурсов можно просмотреть все подготовленные ресурсы Azure для вашего решения (за исключением приложения Azure Active Directory, которое можно найти на классическом портале Azure).</span><span class="sxs-lookup"><span data-stu-id="9c82d-117">In the resource group, you can see all the provisioned Azure resources for your solution except for the Azure Active Directory application that you can find in the Azure Classic Portal.</span></span> <span data-ttu-id="9c82d-118">На следующем рисунке показан пример колонки **Группа ресурсов** для предварительного настроенного решения для удаленного мониторинга:</span><span class="sxs-lookup"><span data-stu-id="9c82d-118">The following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="9c82d-119">Для начала настройте приложение логики, которое будет использоваться с предварительно настроенным решением.</span><span class="sxs-lookup"><span data-stu-id="9c82d-119">To begin, set up the logic app to use with the preconfigured solution.</span></span>

## <a name="set-up-the-logic-app"></a><span data-ttu-id="9c82d-120">Настройка приложения логики</span><span class="sxs-lookup"><span data-stu-id="9c82d-120">Set up the Logic App</span></span>
1. <span data-ttu-id="9c82d-121">Щелкните **Добавить** в верхней части колонки группы ресурсов на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9c82d-121">Click **Add** at the top of your resource group blade in the Azure portal.</span></span>
2. <span data-ttu-id="9c82d-122">Найдите **Приложение логики**, выберите его и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9c82d-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="9c82d-123">Заполните поле **Имя**. Затем укажите те же подписку и группу ресурсов в полях **Подписка** и **Группа ресурсов**, которые использовались при подготовке решения для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="9c82d-123">Fill out the **Name** and use the same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="9c82d-124">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9c82d-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="9c82d-125">После завершения развертывания приложение логики отобразится в качестве ресурса в вашей группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9c82d-125">When your deployment completes, you can see the Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="9c82d-126">Щелкните приложение логики, чтобы перейти к колонке "Приложение логики". Выберите шаблон **Blank Logic App** (Пустое приложение логики). При этом откроется **Конструктор Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="9c82d-126">Click the Logic App to navigate to the Logic App blade, select the **Blank Logic App** template to open the **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="9c82d-127">Выберите **Запрос**.</span><span class="sxs-lookup"><span data-stu-id="9c82d-127">Select **Request**.</span></span> <span data-ttu-id="9c82d-128">Это действие указывает, что в качестве триггера выступает входящий HTTP-запрос с полезными данными в определенном формате JSON.</span><span class="sxs-lookup"><span data-stu-id="9c82d-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="9c82d-129">Вставьте следующий код в поле "Схема JSON текста запроса":</span><span class="sxs-lookup"><span data-stu-id="9c82d-129">Paste the following code into the Request Body JSON Schema:</span></span>
   
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
   > <span data-ttu-id="9c82d-130">Примечание. Сохранив приложение логики, можно скопировать URL-адрес метода HTTP POST, но сначала необходимо добавить действие.</span><span class="sxs-lookup"><span data-stu-id="9c82d-130">You can copy the URL for the HTTP post after you save the logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="9c82d-131">Щелкните **+ Новый шаг** под своим триггером.</span><span class="sxs-lookup"><span data-stu-id="9c82d-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="9c82d-132">Затем выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="9c82d-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="9c82d-133">Найдите действие **SendGrid - Send email** (SendGrid — отправить письмо) и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="9c82d-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="9c82d-134">Введите имя подключения, например **SendGridConnection**, в соответствующем поле укажите **ключ API SendGrid**, созданный при настройке учетной записи SendGrid, и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9c82d-134">Enter a name for the connection, such as **SendGridConnection**, enter the **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="9c82d-135">Добавьте свои адреса электронной почты в поля **From** (От) и **To** (Кому).</span><span class="sxs-lookup"><span data-stu-id="9c82d-135">Add email addresses you own to both the **From** and **To** fields.</span></span> <span data-ttu-id="9c82d-136">В поле **Тема** добавьте **Remote monitoring alert [DeviceId]** (Оповещение удаленного мониторинга [DeviceId]).</span><span class="sxs-lookup"><span data-stu-id="9c82d-136">Add **Remote monitoring alert [DeviceId]** to the **Subject** field.</span></span> <span data-ttu-id="9c82d-137">В поле **Текст сообщения электронной почты** укажите **Device [DeviceId] has reported [measurementName] with value [measuredValue]** (Устройство [DeviceId] передало значение [measuredValue] для измерения [measurementName]).</span><span class="sxs-lookup"><span data-stu-id="9c82d-137">In the **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="9c82d-138">Параметры **[DeviceId]**, **[measurementName]** и **[measuredValue]** можно добавить с помощью раздела **Можно вставить данные из предыдущих шагов**.</span><span class="sxs-lookup"><span data-stu-id="9c82d-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in the **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="9c82d-139">Щелкните **Сохранить** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="9c82d-139">Click **Save** in the top menu.</span></span>
13. <span data-ttu-id="9c82d-140">Щелкните триггер **Запрос** и скопируйте значение **HTTP POST на этот URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="9c82d-140">Click the **Request** trigger and copy the **Http Post to this URL** value.</span></span> <span data-ttu-id="9c82d-141">Этот URL-адрес потребуется далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9c82d-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="9c82d-142">Приложения логики позволяют запускать [множество действий различных типов][lnk-logic-apps-actions], в том числе действия в Office 365.</span><span class="sxs-lookup"><span data-stu-id="9c82d-142">Logic Apps enable you to run [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-the-eventprocessor-web-job"></a><span data-ttu-id="9c82d-143">Настройка веб-задания EventProcessor</span><span class="sxs-lookup"><span data-stu-id="9c82d-143">Set up the EventProcessor Web Job</span></span>
<span data-ttu-id="9c82d-144">В этом разделе вы подключите предварительно настроенное решение к созданному приложению логики.</span><span class="sxs-lookup"><span data-stu-id="9c82d-144">In this section, you connect your preconfigured solution to the Logic App you created.</span></span> <span data-ttu-id="9c82d-145">Чтобы выполнить эту задачу, необходимо добавить URL-адрес для вызова приложения логики к действию, которое запускается, когда значение датчика устройства превышает пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="9c82d-145">To complete this task, you add the URL to trigger the Logic App to the action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="9c82d-146">С помощью клиента git клонируйте последнюю версию [репозитория github azure-iot-remote-monitoring][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="9c82d-146">Use your git client to clone the latest version of the [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="9c82d-147">Например:</span><span class="sxs-lookup"><span data-stu-id="9c82d-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="9c82d-148">В Visual Studio откройте файл **RemoteMonitoring.sln** из локальной копии репозитория.</span><span class="sxs-lookup"><span data-stu-id="9c82d-148">In Visual Studio, open the **RemoteMonitoring.sln** from the local copy of the repository.</span></span>
3. <span data-ttu-id="9c82d-149">Откройте файл **ActionRepository.cs** в папке **Infrastructure\\Repository**.</span><span class="sxs-lookup"><span data-stu-id="9c82d-149">Open the **ActionRepository.cs** file in the **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="9c82d-150">Измените словарь **actionIds**, указав в нем значение **HTTP POST на этот URL-адрес**, записанное из приложения логики.</span><span class="sxs-lookup"><span data-stu-id="9c82d-150">Update the **actionIds** dictionary with the **Http Post to this URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post to this URL>" },
        { "Raise Alarm", "<Http Post to this URL>" }
    };
    ```
5. <span data-ttu-id="9c82d-151">Сохраните изменения в решении и закройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c82d-151">Save the changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-the-command-line"></a><span data-ttu-id="9c82d-152">Развертывание из командной строки</span><span class="sxs-lookup"><span data-stu-id="9c82d-152">Deploy from the command line</span></span>
<span data-ttu-id="9c82d-153">В этом разделе вы развернете обновленную версию решения для удаленного мониторинга, заменив ту версию, которая в настоящее время работает в Azure.</span><span class="sxs-lookup"><span data-stu-id="9c82d-153">In this section, you deploy your updated version of the remote monitoring solution to replace the version currently running in Azure.</span></span>

1. <span data-ttu-id="9c82d-154">Следуйте инструкциям [по настройке для разработчиков][lnk-devsetup], чтобы настроить свою среду для развертывания.</span><span class="sxs-lookup"><span data-stu-id="9c82d-154">Following the [dev set-up][lnk-devsetup] instructions to set up your environment for deployment.</span></span>
2. <span data-ttu-id="9c82d-155">Для локального развертывания следуйте инструкциям [по локальному развертыванию][lnk-localdeploy].</span><span class="sxs-lookup"><span data-stu-id="9c82d-155">To deploy locally, follow the [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="9c82d-156">Для развертывания в облако с обновлением существующего развертывания в облаке следуйте [этим][lnk-clouddeploy] инструкциям.</span><span class="sxs-lookup"><span data-stu-id="9c82d-156">To deploy to the cloud and update your existing cloud deployment, follow the [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="9c82d-157">В качестве имени развертывания используйте имя исходного развертывания.</span><span class="sxs-lookup"><span data-stu-id="9c82d-157">Use the name of your original deployment as the deployment name.</span></span> <span data-ttu-id="9c82d-158">Например, если исходное развертывание называлось **demologicapp**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9c82d-158">For example if the original deployment was called **demologicapp**, use the following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="9c82d-159">При запуске сценария сборки обязательно используйте те же учетную запись, подписку, регион Azure и экземпляр Active Directory, которые применялись при подготовке решения.</span><span class="sxs-lookup"><span data-stu-id="9c82d-159">When the build script runs, be sure to use the same Azure account, subscription, region, and Active Directory instance you used when you provisioned the solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="9c82d-160">Проверка приложения логики в действии</span><span class="sxs-lookup"><span data-stu-id="9c82d-160">See your Logic App in action</span></span>
<span data-ttu-id="9c82d-161">При подготовке предварительно настроенного решения для удаленного мониторинга в нем по умолчанию настроены два правила.</span><span class="sxs-lookup"><span data-stu-id="9c82d-161">The remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="9c82d-162">Оба правила применяются к устройству **SampleDevice001** :</span><span class="sxs-lookup"><span data-stu-id="9c82d-162">Both rules are on the **SampleDevice001** device:</span></span>

* <span data-ttu-id="9c82d-163">Температура > 38,00</span><span class="sxs-lookup"><span data-stu-id="9c82d-163">Temperature > 38.00</span></span>
* <span data-ttu-id="9c82d-164">Влажность > 48,00</span><span class="sxs-lookup"><span data-stu-id="9c82d-164">Humidity > 48.00</span></span>

<span data-ttu-id="9c82d-165">Правило для температуры активирует действие **Raise Alarm**, а правило для влажности — действие **SendMessage**.</span><span class="sxs-lookup"><span data-stu-id="9c82d-165">The temperature rule triggers the **Raise Alarm** action and the Humidity rule triggers the **SendMessage** action.</span></span> <span data-ttu-id="9c82d-166">При условии, что для обоих действий в классе **ActionRepository** используется один и тот же URL-адрес, приложение логики срабатывает для каждого правила.</span><span class="sxs-lookup"><span data-stu-id="9c82d-166">Assuming you used the same URL for both actions the **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="9c82d-167">Оба правила используют SendGrid для отправки электронной почты с подробными сведениями о предупреждении на адрес, указанный в поле **Кому** .</span><span class="sxs-lookup"><span data-stu-id="9c82d-167">Both rules use SendGrid to send an email to the **To** address with details of the alert.</span></span>

> [!NOTE]
> <span data-ttu-id="9c82d-168">Приложение логики будет срабатывать при каждом превышении порогового значения.</span><span class="sxs-lookup"><span data-stu-id="9c82d-168">The Logic App continues to trigger every time the threshold is met.</span></span> <span data-ttu-id="9c82d-169">Чтобы избежать получения ненужных электронных сообщений, можно отключить правила на портале решения или приложение логики на [портале Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="9c82d-169">To avoid unnecessary emails, you can either disable the rules in your solution portal or disable the Logic App in the [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="9c82d-170">Наряду с получением электронных писем вы также можете наблюдать за работой приложения логики на портале:</span><span class="sxs-lookup"><span data-stu-id="9c82d-170">In addition to receiving emails, you can also see when the Logic App runs in the portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="9c82d-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c82d-171">Next steps</span></span>
<span data-ttu-id="9c82d-172">Теперь когда вы использовали приложение логики для подключения предварительно настроенного решения к бизнес-процессу, можете ознакомиться с дополнительными сведениями о настройке таких решений:</span><span class="sxs-lookup"><span data-stu-id="9c82d-172">Now that you've used a Logic App to connect the preconfigured solution to a business process, you can learn more about the options for customizing the preconfigured solutions:</span></span>

* <span data-ttu-id="9c82d-173">[Использование динамической телеметрии с предварительно настроенным решением для удаленного мониторинга][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="9c82d-173">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="9c82d-174">[Метаданные сведений об устройстве в предварительно настроенном решении для удаленного мониторинга][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="9c82d-174">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>

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
