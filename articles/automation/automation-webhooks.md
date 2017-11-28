---
title: "Запуск Runbook службы автоматизации Azure с помощью объекта webhook | Документация Майкрософт"
description: "Объект Webhook, который позволяет клиенту запустить модуль Runbook в службе автоматизации Azure с помощью HTTP-запроса.  В статье рассматривается создание объекта Webhook и вызов такого объекта для запуска модуля Runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 6c65427fcd18e41a90dfb872aa9525f758b17b87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="42201-104">Запуск Runbook службы автоматизации Azure с помощью объекта webhook</span><span class="sxs-lookup"><span data-stu-id="42201-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="42201-105">*Webhook* позволяет запустить модуль Runbook в службе автоматизации Azure с помощью одного HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="42201-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="42201-106">Это позволяет внешним службам, таким как Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, или пользовательским приложениям запускать модули Runbook без реализации полного решения с помощью API службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="42201-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="42201-107">![Обзор веб-перехватчиков](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="42201-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="42201-108">Сравнение объектов webhook с другими методами запуска модуля Runbook см. в разделе [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="42201-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="42201-109">Подробные сведения о Webhook</span><span class="sxs-lookup"><span data-stu-id="42201-109">Details of a webhook</span></span>
<span data-ttu-id="42201-110">В следующей таблице описаны свойства, которые необходимо настроить для объекта Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="42201-111">Свойство</span><span class="sxs-lookup"><span data-stu-id="42201-111">Property</span></span> | <span data-ttu-id="42201-112">Описание</span><span class="sxs-lookup"><span data-stu-id="42201-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="42201-113">Имя</span><span class="sxs-lookup"><span data-stu-id="42201-113">Name</span></span> |<span data-ttu-id="42201-114">Для объекта Webhook можно указать любое имя, так как оно не раскрывается клиенту.</span><span class="sxs-lookup"><span data-stu-id="42201-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="42201-115">Имя используется для идентификации модуля Runbook в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="42201-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="42201-116">Рекомендуется задать объекту Webhook имя, связанное с клиентом, который будет его использовать.</span><span class="sxs-lookup"><span data-stu-id="42201-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="42201-117">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="42201-117">URL</span></span> |<span data-ttu-id="42201-118">URL-адрес Webhook — это уникальный адрес, который использует клиент для метода HTTP POST для запуска модуля Runbook, связанного с объектом Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="42201-119">URL-адрес создается автоматически при создании объекта Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="42201-120">Нельзя указать другой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="42201-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="42201-121">URL-адрес содержит токен безопасности, который позволяет сторонней системе вызвать модуль Runbook без дополнительной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="42201-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="42201-122">По этой причине он должен рассматриваться как пароль.</span><span class="sxs-lookup"><span data-stu-id="42201-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="42201-123">По соображениям безопасности просмотреть URL-адрес на портале Azure можно только в момент создания веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="42201-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="42201-124">URL-адрес следует записать в надежном месте, чтобы использовать его в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="42201-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="42201-125">Срок действия</span><span class="sxs-lookup"><span data-stu-id="42201-125">Expiration date</span></span> |<span data-ttu-id="42201-126">Как и сертификат, каждый объект Webhook имеет срок действия, после которого он больше не используется.</span><span class="sxs-lookup"><span data-stu-id="42201-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="42201-127">Этот срок можно изменить после создания объекта webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="42201-128">Включено</span><span class="sxs-lookup"><span data-stu-id="42201-128">Enabled</span></span> |<span data-ttu-id="42201-129">При создании объекта Webhook он по умолчанию включается.</span><span class="sxs-lookup"><span data-stu-id="42201-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="42201-130">Если его отключить, клиенты не смогут его использовать.</span><span class="sxs-lookup"><span data-stu-id="42201-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="42201-131">Свойство **Включен** можно задать при создании объекта Webhook или в любое время после его создания.</span><span class="sxs-lookup"><span data-stu-id="42201-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="42201-132">Параметры</span><span class="sxs-lookup"><span data-stu-id="42201-132">Parameters</span></span>
<span data-ttu-id="42201-133">Объект Webhook может определять значения для параметров модуля Runbook, которые используются при запуске модуля Runbook этим объектом Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="42201-134">Объект Webhook должен содержать значения для всех обязательных параметров модуля Runbook и может также включать необязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="42201-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="42201-135">Значение параметра, который настроен для объекта Webhook, можно изменить даже после создания объекта Webhoook.</span><span class="sxs-lookup"><span data-stu-id="42201-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="42201-136">Несколько объектов Webhook, привязанных к одному модулю Runbook, могут использовать разные значения параметров.</span><span class="sxs-lookup"><span data-stu-id="42201-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="42201-137">Когда клиент запускает модуль Runbook с помощью объекта Webhook, клиент не может переопределить значения параметров, определяемые Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="42201-138">Чтобы получать данные от клиента, модуль Runbook может принимать один параметр **$WebhookData** типа [object], который содержит данные, включаемые клиентом в POST-запрос.</span><span class="sxs-lookup"><span data-stu-id="42201-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Свойства Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="42201-140">Объект **$WebhookData** имеет следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="42201-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="42201-141">Свойство</span><span class="sxs-lookup"><span data-stu-id="42201-141">Property</span></span> | <span data-ttu-id="42201-142">Описание</span><span class="sxs-lookup"><span data-stu-id="42201-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="42201-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="42201-143">WebhookName</span></span> |<span data-ttu-id="42201-144">Имя объекта Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-144">The name of the webhook.</span></span> |
| <span data-ttu-id="42201-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="42201-145">RequestHeader</span></span> |<span data-ttu-id="42201-146">Хэш-таблица, содержащая заголовки входящего запроса POST.</span><span class="sxs-lookup"><span data-stu-id="42201-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="42201-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="42201-147">RequestBody</span></span> |<span data-ttu-id="42201-148">Текст входящего запроса POST.</span><span class="sxs-lookup"><span data-stu-id="42201-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="42201-149">Это сохранит все форматирование, такое как строка, JSON, XML или данные, закодированные в форме.</span><span class="sxs-lookup"><span data-stu-id="42201-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="42201-150">Модуль Runbook должен быть написан для работы с форматом данных, который ожидается.</span><span class="sxs-lookup"><span data-stu-id="42201-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="42201-151">Нет настройки объекта Webhook, которая была бы обязательной для поддержки параметра **$WebhookData** , однако модуль Runbook не обязан принимать его.</span><span class="sxs-lookup"><span data-stu-id="42201-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="42201-152">Если модуль Runbook не определяет параметр, любые сведения в запросе клиента пропускаются.</span><span class="sxs-lookup"><span data-stu-id="42201-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="42201-153">Если указать значение для параметра $WebhookData в момент создания объекта Webhook, это значение будет переопределено, когда объект Webhook запустит модуль Runbook с данными из клиентского POST-запроса, даже если клиент не включает какие-либо данные в текст запроса.</span><span class="sxs-lookup"><span data-stu-id="42201-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="42201-154">При запуске модуля Runbook, у которого параметр $WebhookData использует метод, отличный от Webhook, можно указать значение для $Webhookdata, которое будет распознаваться модулем Runbook.</span><span class="sxs-lookup"><span data-stu-id="42201-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="42201-155">Это значение должно быть объектом с теми же [свойствами](#details-of-a-webhook) , что и $Webhookdata, чтобы модуль Runbook смог с ним правильно работать как с фактическим WebhookData, переданным веб-перехватчиком.</span><span class="sxs-lookup"><span data-stu-id="42201-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="42201-156">Например, если на портале Azure запускается следующий модуль Runbook и требуется передать несколько примеров WebhookData для тестирования, то, так как WebhookData является объектом, он должен быть передан в пользовательском интерфейсе как JSON.</span><span class="sxs-lookup"><span data-stu-id="42201-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![Параметр WebhookData из пользовательского интерфейса](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="42201-158">Для приведенного выше модуля Runbook, если у вас есть следующие свойства для параметра WebhookData:</span><span class="sxs-lookup"><span data-stu-id="42201-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="42201-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="42201-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="42201-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="42201-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="42201-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="42201-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="42201-162">То в пользовательском интерфейсе для параметра WebhookData следует передать следующее значение JSON:</span><span class="sxs-lookup"><span data-stu-id="42201-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="42201-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="42201-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Запуск параметра WebhookData из пользовательского интерфейса](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="42201-165">Значения входных параметров вводятся вместе с заданием Runbook.</span><span class="sxs-lookup"><span data-stu-id="42201-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="42201-166">Это означает, что любые входные данные, предоставленные клиентом в запросе Webhook, будут записаны в журнал и станут доступны любому пользователю с доступом к заданию автоматизации.</span><span class="sxs-lookup"><span data-stu-id="42201-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="42201-167">По этой причине необходимо соблюдать осторожность при указании критических данных в вызовах Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="42201-168">Безопасность</span><span class="sxs-lookup"><span data-stu-id="42201-168">Security</span></span>
<span data-ttu-id="42201-169">Безопасность объекта Webhook зависит от безопасности URL-адреса, который содержит токен безопасности, позволяющий вызывать объект Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="42201-170">Служба автоматизации Azure не выполняет проверку подлинности для запроса, если он выполняется с правильным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="42201-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="42201-171">По этой причине объекты Webhook не следует применять для модулей Runbook, которые выполняют важные функции, без использования дополнительной проверки запроса.</span><span class="sxs-lookup"><span data-stu-id="42201-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="42201-172">Можно включить логику в модуль Runbook, которая будет определять вызов объектом Webhook путем проверки свойства **WebhookName** для параметра $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="42201-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="42201-173">Модуль Runbook может выполнять последующие проверки путем поиска определенной информации в свойствах **RequestHeader** или **RequestBody**.</span><span class="sxs-lookup"><span data-stu-id="42201-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="42201-174">Еще одна стратегия заключается в том, чтобы модуль Runbook выполнял проверку внешнего условия после получения запроса Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="42201-175">Например, рассмотрим модуль Runbook, вызываемый из GitHub каждый раз, когда на GitHub появляется обновление репозитория.</span><span class="sxs-lookup"><span data-stu-id="42201-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="42201-176">Модуль Runbook может подключаться к GitHub, чтобы проверить доступность обновления.</span><span class="sxs-lookup"><span data-stu-id="42201-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="42201-177">Создание объекта Webhook</span><span class="sxs-lookup"><span data-stu-id="42201-177">Creating a webhook</span></span>
<span data-ttu-id="42201-178">Чтобы создать новый веб-перехватчик, связанный с модулем Runbook, на портале Azure, воспользуйтесь следующей процедурой.</span><span class="sxs-lookup"><span data-stu-id="42201-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="42201-179">В колонке **Модули Runbook** на портале Azure щелкните модуль Runbook, запускаемый веб-перехватчиком, чтобы открыть колонку с подробной информацией о нем.</span><span class="sxs-lookup"><span data-stu-id="42201-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="42201-180">Щелкните **Webhook** в верхней части колонки, чтобы открыть колонку **Add Webhook** (Добавить объект webhook).</span><span class="sxs-lookup"><span data-stu-id="42201-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br><span data-ttu-id="42201-181">
   ![Кнопка Webhook](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="42201-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="42201-182">Щелкните **Create new webhook** (Создать объект webhook), чтобы открыть колонку **Create webhook blade** (Создание объекта webhook).</span><span class="sxs-lookup"><span data-stu-id="42201-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="42201-183">Укажите для объекта webhook **имя**, **Срок действия** и необходимость его включения.</span><span class="sxs-lookup"><span data-stu-id="42201-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="42201-184">Подробные сведения об этих свойствах см. в разделе [Details of a webhook](#details-of-a-webhook) (Сведения об объекте webhook).</span><span class="sxs-lookup"><span data-stu-id="42201-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="42201-185">Щелкните значок копирования и нажмите Ctrl+C, чтобы скопировать URL-адрес объекта Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="42201-186">Сохраните URL-адрес в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="42201-186">Then record it in a safe place.</span></span>  <span data-ttu-id="42201-187">**После создания объекта webhook URL-адрес нельзя получить повторно.**</span><span class="sxs-lookup"><span data-stu-id="42201-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br><span data-ttu-id="42201-188">
   ![URL-адрес объекта webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="42201-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="42201-189">Щелкните **Параметры** , чтобы указать значения для параметров модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="42201-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="42201-190">Если модуль Runbook содержит обязательные параметры, то его нельзя будет создать, не указав значения.</span><span class="sxs-lookup"><span data-stu-id="42201-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="42201-191">Щелкните **Создать** , чтобы создать объект Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="42201-192">Использование объекта Webhook</span><span class="sxs-lookup"><span data-stu-id="42201-192">Using a webhook</span></span>
<span data-ttu-id="42201-193">Чтобы использовать объект Webhook после его создания, клиентское приложение должно создать запрос HTTP POST с URL-адресом объекта Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="42201-194">Синтаксис объекта Webhook будет иметь следующий формат.</span><span class="sxs-lookup"><span data-stu-id="42201-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="42201-195">Клиент получит один из следующих кодов возврата в ответ на запрос POST.</span><span class="sxs-lookup"><span data-stu-id="42201-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="42201-196">Код</span><span class="sxs-lookup"><span data-stu-id="42201-196">Code</span></span> | <span data-ttu-id="42201-197">текст</span><span class="sxs-lookup"><span data-stu-id="42201-197">Text</span></span> | <span data-ttu-id="42201-198">Описание</span><span class="sxs-lookup"><span data-stu-id="42201-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="42201-199">202</span><span class="sxs-lookup"><span data-stu-id="42201-199">202</span></span> |<span data-ttu-id="42201-200">Принято</span><span class="sxs-lookup"><span data-stu-id="42201-200">Accepted</span></span> |<span data-ttu-id="42201-201">Запрос был принят, и модуль Runbook успешно поставлен в очередь.</span><span class="sxs-lookup"><span data-stu-id="42201-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="42201-202">400</span><span class="sxs-lookup"><span data-stu-id="42201-202">400</span></span> |<span data-ttu-id="42201-203">Ошибка запроса</span><span class="sxs-lookup"><span data-stu-id="42201-203">Bad Request</span></span> |<span data-ttu-id="42201-204">Запрос не был принят по одной из следующих причин.</span><span class="sxs-lookup"><span data-stu-id="42201-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="42201-205">Срок действия объекта webhook истек.</span><span class="sxs-lookup"><span data-stu-id="42201-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="42201-206">Объект webhook отключен.</span><span class="sxs-lookup"><span data-stu-id="42201-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="42201-207">Недопустимый токен в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="42201-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="42201-208">404</span><span class="sxs-lookup"><span data-stu-id="42201-208">404</span></span> |<span data-ttu-id="42201-209">Не найдено</span><span class="sxs-lookup"><span data-stu-id="42201-209">Not Found</span></span> |<span data-ttu-id="42201-210">Запрос не был принят по одной из следующих причин.</span><span class="sxs-lookup"><span data-stu-id="42201-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="42201-211">Объект webhook не найден.</span><span class="sxs-lookup"><span data-stu-id="42201-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="42201-212">Модуль Runbook не найден.</span><span class="sxs-lookup"><span data-stu-id="42201-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="42201-213">Учетная запись не найдена.</span><span class="sxs-lookup"><span data-stu-id="42201-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="42201-214">500</span><span class="sxs-lookup"><span data-stu-id="42201-214">500</span></span> |<span data-ttu-id="42201-215">Внутренняя ошибка сервера</span><span class="sxs-lookup"><span data-stu-id="42201-215">Internal Server Error</span></span> |<span data-ttu-id="42201-216">URL-адрес допустимый, но произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="42201-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="42201-217">Отправьте запрос повторно.</span><span class="sxs-lookup"><span data-stu-id="42201-217">Please resubmit the request.</span></span> |

<span data-ttu-id="42201-218">Если предположить, что запрос выполнен успешно, ответ Webhook будет содержать идентификатор задания в формате JSON, как показано далее.</span><span class="sxs-lookup"><span data-stu-id="42201-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="42201-219">Он будет содержать идентификатор одного задания, но формат JSON предоставляет возможность потенциальных будущих улучшений.</span><span class="sxs-lookup"><span data-stu-id="42201-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="42201-220">Клиент не может определить момент завершения задания Runbook и состояние его завершения из объекта Webhook.</span><span class="sxs-lookup"><span data-stu-id="42201-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="42201-221">Он может определить эти сведения с помощью идентификатора задания, используя другой метод, например [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) или [API службы автоматизации Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="42201-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="42201-222">Пример</span><span class="sxs-lookup"><span data-stu-id="42201-222">Example</span></span>
<span data-ttu-id="42201-223">В следующем примере модуль Runbook запускается с помощью Webhook из Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="42201-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="42201-224">Обратите внимание, что в любом языке, способном выполнить HTTP-запрос, можно использовать объект Webhook; Windows PowerShell используется здесь просто для примера.</span><span class="sxs-lookup"><span data-stu-id="42201-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="42201-225">Модуль Runbook ожидает список виртуальных машин, отформатированный в JSON, в теле запроса.</span><span class="sxs-lookup"><span data-stu-id="42201-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="42201-226">Также мы включаем в заголовок запроса сведения о том, кто запускает модуль Runbook, а также о дате и времени запуска.</span><span class="sxs-lookup"><span data-stu-id="42201-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="42201-227">На следующем рисунке показаны данные заголовка (с использованием трассировки [Fiddler](http://www.telerik.com/fiddler) ) из этого запроса.</span><span class="sxs-lookup"><span data-stu-id="42201-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="42201-228">Они включают стандартные заголовки HTTP-запроса в дополнение к пользовательским заголовкам Date и From, которые мы добавили.</span><span class="sxs-lookup"><span data-stu-id="42201-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="42201-229">Каждое из этих значений доступно модулю Runbook в свойстве **RequestHeaders** объекта **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="42201-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Кнопка Webhook](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="42201-231">На следующем рисунке показан текст запроса (с использованием трассировки [Fiddler](http://www.telerik.com/fiddler)), доступное модулю Runbook в свойстве **RequestBody** объекта **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="42201-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="42201-232">Оно отформатировано как JSON, так как это формат, который был включен в тело запроса.</span><span class="sxs-lookup"><span data-stu-id="42201-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Кнопка Webhook](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="42201-234">На следующем рисунке показан запрос, отправляемый из Windows PowerShell, а также получаемый в результате ответ.</span><span class="sxs-lookup"><span data-stu-id="42201-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="42201-235">Идентификатор задания извлекается из ответа и преобразуется в строку.</span><span class="sxs-lookup"><span data-stu-id="42201-235">The job id is extracted from the response and converted to a string.</span></span>

![Кнопка Webhook](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="42201-237">Следующий образец модуля Runbook принимает предыдущий пример запроса и запускает виртуальные машины, указанные в теле запроса.</span><span class="sxs-lookup"><span data-stu-id="42201-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate to Azure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="42201-238">Запуск модулей Runbook в ответ на оповещения Azure</span><span class="sxs-lookup"><span data-stu-id="42201-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="42201-239">Модули Runbook с поддержкой объектов webhook можно использовать для реагирования на [оповещения Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="42201-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="42201-240">Ресурсы в Azure можно отслеживать, собирая статистику производительности, доступности и использования с помощью оповещений Azure.</span><span class="sxs-lookup"><span data-stu-id="42201-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="42201-241">Вы можете получать оповещения на основе отслеживания метрик или событий в ресурсах Azure, сейчас учетные записи автоматизации поддерживают только метрики.</span><span class="sxs-lookup"><span data-stu-id="42201-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="42201-242">Когда значение заданной метрики превышает установленный порог или активируется заданное событие, администратору или соадминистраторам службы отправляется уведомление о том, что оповещение необходимо разрешить. Дополнительные сведения о метриках и событиях см. в статье [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) (Получение уведомлений об оповещениях).</span><span class="sxs-lookup"><span data-stu-id="42201-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="42201-243">Оповещения Azure можно использовать не только как систему уведомлений, но и для запуска модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="42201-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="42201-244">Служба автоматизации Azure позволяет запускать модули Runbook с поддержкой веб-перехватчика в ответ на оповещения Azure.</span><span class="sxs-lookup"><span data-stu-id="42201-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="42201-245">Как только метрика превышает заданное пороговое значение, правило оповещения становится активным и запускает веб-перехватчик службы автоматизации, который, в свою очередь, запускает модуль Runbook.</span><span class="sxs-lookup"><span data-stu-id="42201-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![Объекты Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="42201-247">Контекст оповещения</span><span class="sxs-lookup"><span data-stu-id="42201-247">Alert context</span></span>
<span data-ttu-id="42201-248">Для ресурса Azure, такого как виртуальная машина, одной из основных метрик производительности является загрузка ЦП.</span><span class="sxs-lookup"><span data-stu-id="42201-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="42201-249">Если загрузка ЦП составляет 100 % или превышает определенный порог в течение долгого времени, перезапустите виртуальную машину, чтобы решить проблему.</span><span class="sxs-lookup"><span data-stu-id="42201-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="42201-250">Ситуацию можно исправить, настроив правило оповещения для виртуальной машины, используя в качестве метрики процент загрузки ЦП.</span><span class="sxs-lookup"><span data-stu-id="42201-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="42201-251">Процент загрузки ЦП в данном случае взят для примера, и в ресурсах Azure можно настраивать другие метрики, а перезапуск виртуальной машины — лишь одно из действий по решению проблемы, и можно настраивать модуль Runbook на выполнение других действий.</span><span class="sxs-lookup"><span data-stu-id="42201-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="42201-252">Когда правило оповещения становится активным и запускает модуль Runbook с поддержкой веб-перехватчика, в модуль Runbook отправляется контекст оповещения.</span><span class="sxs-lookup"><span data-stu-id="42201-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="42201-253">[Контекст оповещения](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) содержит сведения, позволяющие модулю Runbook идентифицировать ресурс, к которому будет применено действие, включая **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** и **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="42201-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="42201-254">Контекст оповещения внедряется в основную часть объекта **WebhookData**, передаваемого в модуль Runbook, и извлекается с помощью свойства **Webhook.RequestBody**.</span><span class="sxs-lookup"><span data-stu-id="42201-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="42201-255">Пример</span><span class="sxs-lookup"><span data-stu-id="42201-255">Example</span></span>
<span data-ttu-id="42201-256">Создание виртуальной машины Azure в подписке и привязка [оповещения для мониторинга метрики процента загрузки ЦП](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="42201-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="42201-257">При создании оповещения введите в поле веб-перехватчика URL-адрес, сгенерированный при создании веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="42201-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="42201-258">Приведенный ниже пример модуля Runbook запускается, когда правило оповещения становится активным и собирает параметры контекста Azure, необходимые модулю Runbook для идентификации ресурса, к которому нужно применить действие.</span><span class="sxs-lookup"><span data-stu-id="42201-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="42201-259">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="42201-259">Next steps</span></span>
* <span data-ttu-id="42201-260">Дополнительные сведения о различных способах запуска модуля Runbook см. в статье [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="42201-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="42201-261">Сведения о просмотре состояния задания Runbook см. в статье [Выполнение модуля Runbook в службе автоматизации Azure](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="42201-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="42201-262">Узнать, как использовать службу автоматизации Azure для выполнения действий на основе оповещений Azure, можно в статье [Обработка оповещений виртуальной машины Azure с помощью модулей Runbook службы автоматизации](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="42201-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
