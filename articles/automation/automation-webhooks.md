---
title: "runbook службы автоматизации Azure с веб-перехватчика aaaStarting | Документы Microsoft"
description: "Веб-перехватчика, позволяющую toostart клиента runbook в автоматизации Azure вызова HTTP.  В этой статье описывается как toocreate веб-перехватчика и как один toostart toocall runbook."
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
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="06d0f-104">Запуск Runbook службы автоматизации Azure с помощью объекта webhook</span><span class="sxs-lookup"><span data-stu-id="06d0f-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="06d0f-105">Объект *веб-перехватчика* позволяет toostart конкретного модуля runbook в автоматизации Azure через один HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="06d0f-105">A *webhook* allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="06d0f-106">Это позволяет внешней службы, такие как Visual Studio Team Services, GitHub, аналитика журналов пакета управления Operations Microsoft или пользовательских приложений toostart модулей Runbook без реализации полного решения с использованием hello API автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="06d0f-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications toostart runbooks without implementing a full solution using hello Azure Automation API.</span></span>  
<span data-ttu-id="06d0f-107">![Обзор веб-перехватчиков](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="06d0f-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="06d0f-108">Вы можете сравнить веб-перехватчиков tooother способов запуска модуля runbook [запуск runbook в автоматизации Azure](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="06d0f-108">You can compare webhooks tooother methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="06d0f-109">Подробные сведения о Webhook</span><span class="sxs-lookup"><span data-stu-id="06d0f-109">Details of a webhook</span></span>
<span data-ttu-id="06d0f-110">Hello следующей таблице описаны свойства hello, необходимо настроить для веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="06d0f-110">hello following table describes hello properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="06d0f-111">Свойство</span><span class="sxs-lookup"><span data-stu-id="06d0f-111">Property</span></span> | <span data-ttu-id="06d0f-112">Описание</span><span class="sxs-lookup"><span data-stu-id="06d0f-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="06d0f-113">Имя</span><span class="sxs-lookup"><span data-stu-id="06d0f-113">Name</span></span> |<span data-ttu-id="06d0f-114">Вы можете указать любое имя, которое требуется для веб-перехватчика, так как это не предоставляется toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="06d0f-114">You can provide any name you want for a webhook since this is not exposed toohello client.</span></span>  <span data-ttu-id="06d0f-115">Оно используется только для вас tooidentify hello runbook в автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="06d0f-115">It is only used for you tooidentify hello runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="06d0f-116">Рекомендуется следует предоставить веб-перехватчика hello имя связанных toohello клиента, который будет его использовать.</span><span class="sxs-lookup"><span data-stu-id="06d0f-116">As a best practice, you should give hello webhook a name related toohello client that will use it.</span></span> |
| <span data-ttu-id="06d0f-117">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="06d0f-117">URL</span></span> |<span data-ttu-id="06d0f-118">Hello URL-адрес веб-перехватчика hello: hello уникальный адрес, что клиент вызывает с runbook hello HTTP POST toostart связанные toohello веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="06d0f-118">hello URL of hello webhook is hello unique address that a client calls with an HTTP POST toostart hello runbook linked toohello webhook.</span></span>  <span data-ttu-id="06d0f-119">Он создается автоматически при создании веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-119">It is automatically generated when you create hello webhook.</span></span>  <span data-ttu-id="06d0f-120">Нельзя указать другой URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="06d0f-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="06d0f-121">Hello URL-адрес содержит маркер безопасности, позволяющий hello toobe runbook, вызываемые сторонняя система без дальнейшей проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="06d0f-121">hello URL contains a security token that allows hello runbook toobe invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="06d0f-122">По этой причине он должен рассматриваться как пароль.</span><span class="sxs-lookup"><span data-stu-id="06d0f-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="06d0f-123">По соображениям безопасности можно только hello представление создается URL-адрес в Azure портал на веб-перехватчика hello время hello hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-123">For security reasons, you can only view hello URL in hello Azure portal at hello time hello webhook is created.</span></span> <span data-ttu-id="06d0f-124">Следует отметить hello URL-адрес в безопасном месте для будущего использования.</span><span class="sxs-lookup"><span data-stu-id="06d0f-124">You should note hello URL in a secure location for future use.</span></span> |
| <span data-ttu-id="06d0f-125">Срок действия</span><span class="sxs-lookup"><span data-stu-id="06d0f-125">Expiration date</span></span> |<span data-ttu-id="06d0f-126">Как и сертификат, каждый объект Webhook имеет срок действия, после которого он больше не используется.</span><span class="sxs-lookup"><span data-stu-id="06d0f-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="06d0f-127">Эта дата истечения срока действия можно изменить после создания веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-127">This expiration date can be modified after hello webhook is created.</span></span> |
| <span data-ttu-id="06d0f-128">Включено</span><span class="sxs-lookup"><span data-stu-id="06d0f-128">Enabled</span></span> |<span data-ttu-id="06d0f-129">При создании объекта Webhook он по умолчанию включается.</span><span class="sxs-lookup"><span data-stu-id="06d0f-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="06d0f-130">Если задать tooDisabled, то клиент не будет возможности toouse его.</span><span class="sxs-lookup"><span data-stu-id="06d0f-130">If you set it tooDisabled, then no client will be able toouse it.</span></span>  <span data-ttu-id="06d0f-131">Можно задать hello **включено** создается свойство при создании веб-перехватчика hello, или в любое время один раз.</span><span class="sxs-lookup"><span data-stu-id="06d0f-131">You can set hello **Enabled** property when you create hello webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="06d0f-132">Параметры</span><span class="sxs-lookup"><span data-stu-id="06d0f-132">Parameters</span></span>
<span data-ttu-id="06d0f-133">Веб-перехватчика можно определить значения для параметров runbook, которые используются при запуске hello runbook, что веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="06d0f-133">A webhook can define values for runbook parameters that are used when hello runbook is started by that webhook.</span></span> <span data-ttu-id="06d0f-134">веб-перехватчика Hello должна содержать значения для всех обязательных параметров hello runbook и могут включать значения для необязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="06d0f-134">hello webhook must include values for any mandatory parameters of hello runbook and may include values for optional parameters.</span></span> <span data-ttu-id="06d0f-135">Веб-перехватчика tooa настроить значение параметра можно изменить даже после создания hello webhoook.</span><span class="sxs-lookup"><span data-stu-id="06d0f-135">A parameter value configured tooa webhook can be modified even after creating hello webhoook.</span></span> <span data-ttu-id="06d0f-136">Несколько связанных веб-перехватчиков tooa отдельного модуля runbook можно использовать различные значения параметра.</span><span class="sxs-lookup"><span data-stu-id="06d0f-136">Multiple webhooks linked tooa single runbook can each use different parameter values.</span></span>

<span data-ttu-id="06d0f-137">При запуске модуля runbook с помощью веб-перехватчика клиента, он не может переопределить hello значения параметров, определенные в веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-137">When a client starts a runbook using a webhook, it cannot override hello parameter values defined in hello webhook.</span></span>  <span data-ttu-id="06d0f-138">tooreceive данные от клиента hello, hello runbook может принимать один параметр с именем **$WebhookData** тип [object], который будет содержать данные этого клиента hello включает в себя в запросе POST hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-138">tooreceive data from hello client, hello runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that hello client includes in hello POST request.</span></span>

![Свойства Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="06d0f-140">Hello **$WebhookData** объект будет иметь hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="06d0f-140">hello **$WebhookData** object will have hello following properties:</span></span>

| <span data-ttu-id="06d0f-141">Свойство</span><span class="sxs-lookup"><span data-stu-id="06d0f-141">Property</span></span> | <span data-ttu-id="06d0f-142">Описание</span><span class="sxs-lookup"><span data-stu-id="06d0f-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="06d0f-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="06d0f-143">WebhookName</span></span> |<span data-ttu-id="06d0f-144">Имя веб-перехватчика hello Hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-144">hello name of hello webhook.</span></span> |
| <span data-ttu-id="06d0f-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="06d0f-145">RequestHeader</span></span> |<span data-ttu-id="06d0f-146">Хэш-таблица с заголовками hello hello входящего запроса POST.</span><span class="sxs-lookup"><span data-stu-id="06d0f-146">Hash table containing hello headers of hello incoming POST request.</span></span> |
| <span data-ttu-id="06d0f-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="06d0f-147">RequestBody</span></span> |<span data-ttu-id="06d0f-148">текст Hello hello входящего запроса POST.</span><span class="sxs-lookup"><span data-stu-id="06d0f-148">hello body of hello incoming POST request.</span></span>  <span data-ttu-id="06d0f-149">Это сохранит все форматирование, такое как строка, JSON, XML или данные, закодированные в форме.</span><span class="sxs-lookup"><span data-stu-id="06d0f-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="06d0f-150">Hello runbook должно быть написано toowork с форматом данных hello, которая ожидается.</span><span class="sxs-lookup"><span data-stu-id="06d0f-150">hello runbook must be written toowork with hello data format that is expected.</span></span> |

<span data-ttu-id="06d0f-151">Нет конфигураций hello необходимые toosupport веб-перехватчика hello **$WebhookData** параметра, и hello runbook не требуется tooaccept его.</span><span class="sxs-lookup"><span data-stu-id="06d0f-151">There is no configuration of hello webhook required toosupport hello **$WebhookData** parameter, and hello runbook is not required tooaccept it.</span></span>  <span data-ttu-id="06d0f-152">Если hello runbook не определяет параметр hello, все сведения о запросе hello, отправляемых с клиента hello учитывается.</span><span class="sxs-lookup"><span data-stu-id="06d0f-152">If hello runbook does not define hello parameter, then any details of hello request sent from hello client is ignored.</span></span>

<span data-ttu-id="06d0f-153">Если указать значение для $WebhookData при создании веб-перехватчика hello, что значение будет переопределенное в начале веб-перехватчика hello hello runbook hello данными из hello клиентский запрос POST, даже если клиент hello не включать данные в текст запроса hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-153">If you specify a value for $WebhookData when you create hello webhook, that value will be overriden when hello webhook starts hello runbook with hello data from hello client POST request, even if hello client does not include any data in hello request body.</span></span>  <span data-ttu-id="06d0f-154">При запуске модуля runbook, который имеет $WebhookData с помощью метода, отличного от веб-перехватчик может предоставить значение для $Webhookdata, будут распознаваться hello runbook.</span><span class="sxs-lookup"><span data-stu-id="06d0f-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by hello runbook.</span></span>  <span data-ttu-id="06d0f-155">Это значение должно быть объектом с hello же [свойства](#details-of-a-webhook) как $Webhookdata, этого модуля hello должным образом можно работать с ними, как если бы он работал фактическое WebhookData, переданных веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="06d0f-155">This value should be an object with hello same [properties](#details-of-a-webhook) as $Webhookdata so that hello runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="06d0f-156">Например если вы начинаете hello следующую runbook из портала Azure hello и toopass WebhookData некоторые образцы для тестирования, так как WebhookData — это объект, он должен передаваться как JSON в hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="06d0f-156">For example, if you are starting hello following runbook from hello Azure Portal and want toopass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in hello UI.</span></span>

![Параметр WebhookData из пользовательского интерфейса](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="06d0f-158">Для hello выше runbook, если у вас есть следующие свойства для параметра WebhookData hello hello:</span><span class="sxs-lookup"><span data-stu-id="06d0f-158">For hello above runbook, if you have hello following properties for hello WebhookData parameter:</span></span>

1. <span data-ttu-id="06d0f-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="06d0f-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="06d0f-160">RequestHeader: *From=Test User*</span><span class="sxs-lookup"><span data-stu-id="06d0f-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="06d0f-161">RequestBody: *[“VM1”, “VM2”]*</span><span class="sxs-lookup"><span data-stu-id="06d0f-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="06d0f-162">Затем можно передать следующие значения JSON в hello пользовательского интерфейса для параметра WebhookData hello hello:</span><span class="sxs-lookup"><span data-stu-id="06d0f-162">Then you would pass hello following JSON value in hello UI for hello WebhookData parameter:</span></span>  

* <span data-ttu-id="06d0f-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="06d0f-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Запуск параметра WebhookData из пользовательского интерфейса](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="06d0f-165">с заданием runbook hello регистрируются Hello значения всех входных параметров.</span><span class="sxs-lookup"><span data-stu-id="06d0f-165">hello values of all input parameters are logged with hello runbook job.</span></span>  <span data-ttu-id="06d0f-166">Это означает, что любой входных данных, предоставленных клиентом hello в запрос веб-перехватчика hello будет tooanyone регистрируются и доступны с помощью задания автоматизации toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="06d0f-166">This means that any input provided by hello client in hello webhook request will be logged and available tooanyone with access toohello automation job.</span></span>  <span data-ttu-id="06d0f-167">По этой причине необходимо соблюдать осторожность при указании критических данных в вызовах Webhook.</span><span class="sxs-lookup"><span data-stu-id="06d0f-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="06d0f-168">Безопасность</span><span class="sxs-lookup"><span data-stu-id="06d0f-168">Security</span></span>
<span data-ttu-id="06d0f-169">безопасность веб-перехватчика Hello зависит от hello конфиденциальность его URL-адрес, который содержит маркер безопасности, позволяющий ему toobe вызывается.</span><span class="sxs-lookup"><span data-stu-id="06d0f-169">hello security of a webhook relies on hello privacy of its URL which contains a security token that allows it toobe invoked.</span></span> <span data-ttu-id="06d0f-170">Службы автоматизации Azure не будет выполнять проверку подлинности hello запроса до тех пор, пока он станет toohello правильный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="06d0f-170">Azure Automation does not perform any authentication on hello request as long as it is made toohello correct URL.</span></span> <span data-ttu-id="06d0f-171">По этой причине веб-привязок не должен использоваться для модулей Runbook, которые выполняют конфиденциальными функции без использования альтернативный способ проверки запроса hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating hello request.</span></span>

<span data-ttu-id="06d0f-172">Можно включить логику в toodetermine runbook hello, что она была вызвана веб-перехватчика, проверив hello **WebhookName** свойства параметра hello $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="06d0f-172">You can include logic within hello runbook toodetermine that it was called by a webhook by checking hello **WebhookName** property of hello $WebhookData parameter.</span></span> <span data-ttu-id="06d0f-173">Hello runbook может выполнять последующие проверки путем поиска определенной информации в hello **RequestHeader** или **RequestBody** свойства.</span><span class="sxs-lookup"><span data-stu-id="06d0f-173">hello runbook could perform further validation by looking for particular information in hello **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="06d0f-174">Другая стратегия — toohave hello runbook выполнить некоторые проверки внешнего условия при получении запроса на веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="06d0f-174">Another strategy is toohave hello runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="06d0f-175">Например рассмотрим книгу выполнения, вызывается GitHub всякий раз, когда новый репозиторий GitHub tooa фиксации.</span><span class="sxs-lookup"><span data-stu-id="06d0f-175">For example, consider a runbook that is called by GitHub whenever there is a new commit tooa GitHub repository.</span></span>  <span data-ttu-id="06d0f-176">Hello runbook может подключиться toovalidate tooGitHub, новые фиксации просто возникла перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="06d0f-176">hello runbook might connect tooGitHub toovalidate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="06d0f-177">Создание объекта Webhook</span><span class="sxs-lookup"><span data-stu-id="06d0f-177">Creating a webhook</span></span>
<span data-ttu-id="06d0f-178">Используйте следующие процедуры toocreate новый модуль runbook связан с веб-перехватчика tooa в hello портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-178">Use hello following procedure toocreate a new webhook linked tooa runbook in hello Azure portal.</span></span>

1. <span data-ttu-id="06d0f-179">Из hello **Runbooks колонки** hello портал Azure, щелкните runbook hello, hello веб-перехватчика начнет tooview колонке детализации.</span><span class="sxs-lookup"><span data-stu-id="06d0f-179">From hello **Runbooks blade** in hello Azure portal, click hello runbook that hello webhook will start tooview its detail blade.</span></span>
2. <span data-ttu-id="06d0f-180">Нажмите кнопку **веб-перехватчика** вверху hello hello колонке tooopen hello **добавить веб-перехватчика** колонку.</span><span class="sxs-lookup"><span data-stu-id="06d0f-180">Click **Webhook** at hello top of hello blade tooopen hello **Add Webhook** blade.</span></span> <br><span data-ttu-id="06d0f-181">
   ![Кнопка Webhook](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="06d0f-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="06d0f-182">Нажмите кнопку **создать новый веб-перехватчика** tooopen hello **создать веб-перехватчика колонке**.</span><span class="sxs-lookup"><span data-stu-id="06d0f-182">Click **Create new webhook** tooopen hello **Create webhook blade**.</span></span>
4. <span data-ttu-id="06d0f-183">Укажите **имя**, **Дата окончания срока действия** для веб-перехватчика hello и является ли он должен быть включен.</span><span class="sxs-lookup"><span data-stu-id="06d0f-183">Specify a **Name**, **Expiration Date** for hello webhook and whether it should be enabled.</span></span> <span data-ttu-id="06d0f-184">Подробные сведения об этих свойствах см. в разделе [Details of a webhook](#details-of-a-webhook) (Сведения об объекте webhook).</span><span class="sxs-lookup"><span data-stu-id="06d0f-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="06d0f-185">Щелкните значок копирования hello и нажмите Ctrl + C toocopy hello URL-адрес веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-185">Click hello copy icon and press Ctrl+C toocopy hello URL of hello webhook.</span></span>  <span data-ttu-id="06d0f-186">Сохраните URL-адрес в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="06d0f-186">Then record it in a safe place.</span></span>  <span data-ttu-id="06d0f-187">**После создания веб-перехватчика hello hello URL-адрес не удается получить еще раз.**</span><span class="sxs-lookup"><span data-stu-id="06d0f-187">**Once you create hello webhook, you cannot retrieve hello URL again.**</span></span> <br><span data-ttu-id="06d0f-188">
   ![URL-адрес объекта webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="06d0f-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="06d0f-189">Нажмите кнопку **параметры** tooprovide значения для параметров runbook hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-189">Click **Parameters** tooprovide values for hello runbook parameters.</span></span>  <span data-ttu-id="06d0f-190">Если hello runbook обязательные параметры, затем нельзя веб-перехватчик может toocreate hello, если не предоставлены значения.</span><span class="sxs-lookup"><span data-stu-id="06d0f-190">If hello runbook has mandatory parameters, then you will not be able toocreate hello webhook unless values are provided.</span></span>
7. <span data-ttu-id="06d0f-191">Нажмите кнопку **создать** веб-перехватчика toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-191">Click **Create** toocreate hello webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="06d0f-192">Использование объекта Webhook</span><span class="sxs-lookup"><span data-stu-id="06d0f-192">Using a webhook</span></span>
<span data-ttu-id="06d0f-193">toouse веб-перехватчика после его создания клиентского приложения должен выдать HTTP POST с hello URL-адрес для веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-193">toouse a webhook after it has been created, your client application must issue an HTTP POST with hello URL for hello webhook.</span></span>  <span data-ttu-id="06d0f-194">синтаксис Hello веб-перехватчика hello будут в кодировке hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-194">hello syntax of hello webhook will be in hello following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="06d0f-195">Hello клиент получит следующие коды возврата из запроса POST hello hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-195">hello client will receive one of hello following return codes from hello POST request.</span></span>  

| <span data-ttu-id="06d0f-196">Код</span><span class="sxs-lookup"><span data-stu-id="06d0f-196">Code</span></span> | <span data-ttu-id="06d0f-197">текст</span><span class="sxs-lookup"><span data-stu-id="06d0f-197">Text</span></span> | <span data-ttu-id="06d0f-198">Описание</span><span class="sxs-lookup"><span data-stu-id="06d0f-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="06d0f-199">202</span><span class="sxs-lookup"><span data-stu-id="06d0f-199">202</span></span> |<span data-ttu-id="06d0f-200">Принято</span><span class="sxs-lookup"><span data-stu-id="06d0f-200">Accepted</span></span> |<span data-ttu-id="06d0f-201">Hello запрос принят и hello runbook был успешно помещен в очередь.</span><span class="sxs-lookup"><span data-stu-id="06d0f-201">hello request was accepted, and hello runbook was successfully queued.</span></span> |
| <span data-ttu-id="06d0f-202">400</span><span class="sxs-lookup"><span data-stu-id="06d0f-202">400</span></span> |<span data-ttu-id="06d0f-203">Ошибка запроса</span><span class="sxs-lookup"><span data-stu-id="06d0f-203">Bad Request</span></span> |<span data-ttu-id="06d0f-204">Hello запрос не был принят для одной из следующих причин hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-204">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="06d0f-205">веб-перехватчика Hello истек.</span><span class="sxs-lookup"><span data-stu-id="06d0f-205">hello webhook has expired.</span></span></li> <li><span data-ttu-id="06d0f-206">Hello веб-перехватчик отключен.</span><span class="sxs-lookup"><span data-stu-id="06d0f-206">hello webhook is disabled.</span></span></li> <li><span data-ttu-id="06d0f-207">Недопустимый токен Hello в URL-АДРЕСЕ hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-207">hello token in hello URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="06d0f-208">404</span><span class="sxs-lookup"><span data-stu-id="06d0f-208">404</span></span> |<span data-ttu-id="06d0f-209">Не найдено</span><span class="sxs-lookup"><span data-stu-id="06d0f-209">Not Found</span></span> |<span data-ttu-id="06d0f-210">Hello запрос не был принят для одной из следующих причин hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-210">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="06d0f-211">веб-перехватчика Hello не найден.</span><span class="sxs-lookup"><span data-stu-id="06d0f-211">hello webhook was not found.</span></span></li> <li><span data-ttu-id="06d0f-212">Hello runbook не найдено.</span><span class="sxs-lookup"><span data-stu-id="06d0f-212">hello runbook was not found.</span></span></li> <li><span data-ttu-id="06d0f-213">Hello учетная запись не найдена.</span><span class="sxs-lookup"><span data-stu-id="06d0f-213">hello account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="06d0f-214">500</span><span class="sxs-lookup"><span data-stu-id="06d0f-214">500</span></span> |<span data-ttu-id="06d0f-215">Внутренняя ошибка сервера</span><span class="sxs-lookup"><span data-stu-id="06d0f-215">Internal Server Error</span></span> |<span data-ttu-id="06d0f-216">Hello URL-адрес является допустимым, но произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="06d0f-216">hello URL was valid, but an error occurred.</span></span>  <span data-ttu-id="06d0f-217">Повторно отправьте запрос hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-217">Please resubmit hello request.</span></span> |

<span data-ttu-id="06d0f-218">Предположим, что hello запрос выполнен успешно, hello веб-перехватчика ответ содержит идентификатор задания hello в формате JSON следующим образом.</span><span class="sxs-lookup"><span data-stu-id="06d0f-218">Assuming hello request is successful, hello webhook response contains hello job id in JSON format as follows.</span></span> <span data-ttu-id="06d0f-219">Он будет содержать идентификатор одним заданием, но позволяет hello формат JSON для возможных будущих улучшений.</span><span class="sxs-lookup"><span data-stu-id="06d0f-219">It will contain a single job id, but hello JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="06d0f-220">Hello клиент не может определить при завершении задания runbook hello или его состояние завершения с веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-220">hello client cannot determine when hello runbook job completes or its completion status from hello webhook.</span></span>  <span data-ttu-id="06d0f-221">Он определяет эти сведения, такие как с помощью идентификатора задания hello одного метода другим [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) или hello [API автоматизации Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="06d0f-221">It can determine this information using hello job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or hello [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="06d0f-222">Пример</span><span class="sxs-lookup"><span data-stu-id="06d0f-222">Example</span></span>
<span data-ttu-id="06d0f-223">Следующий пример Hello использует Windows PowerShell toostart runbook с веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="06d0f-223">hello following example uses Windows PowerShell toostart a runbook with a webhook.</span></span>  <span data-ttu-id="06d0f-224">Обратите внимание, что в любом языке, способном выполнить HTTP-запрос, можно использовать объект Webhook; Windows PowerShell используется здесь просто для примера.</span><span class="sxs-lookup"><span data-stu-id="06d0f-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="06d0f-225">Hello runbook ожидает список виртуальных машин, в формате JSON в тексте hello hello запроса в формате.</span><span class="sxs-lookup"><span data-stu-id="06d0f-225">hello runbook is expecting a list of virtual machines formatted in JSON in hello body of hello request.</span></span> <span data-ttu-id="06d0f-226">Сведения о, выполняется запуск hello runbook и hello даты и времени, она запущена в заголовке hello hello запроса также предоставляются вместе.</span><span class="sxs-lookup"><span data-stu-id="06d0f-226">We also are including information about who is starting hello runbook and hello date and time it is being started in hello header of hello request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="06d0f-227">Hello на рисунке показаны сведения о заголовке hello (с помощью [Fiddler](http://www.telerik.com/fiddler) трассировки) из этого запроса.</span><span class="sxs-lookup"><span data-stu-id="06d0f-227">hello following image shows hello header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="06d0f-228">Сюда входят стандартные заголовки HTTP-запроса на добавление toohello настраиваемые дата и из заголовков, которые мы добавили.</span><span class="sxs-lookup"><span data-stu-id="06d0f-228">This includes standard headers of an HTTP request in addition toohello custom Date and From headers that we added.</span></span>  <span data-ttu-id="06d0f-229">Каждое из этих значений является доступной toohello runbook в hello **RequestHeaders** свойство **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="06d0f-229">Each of these values is available toohello runbook in hello **RequestHeaders** property of **WebhookData**.</span></span>

![Кнопка Webhook](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="06d0f-231">Hello на рисунке показаны hello тексте hello запроса (с помощью [Fiddler](http://www.telerik.com/fiddler) трассировки), доступные toohello runbook в hello **RequestBody** свойство **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="06d0f-231">hello following image shows hello body of hello request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available toohello runbook in hello **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="06d0f-232">Это в формате JSON за hello формат, который был включен в тексте hello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="06d0f-232">This is formatted as JSON because that was hello format that was included in hello body of hello request.</span></span>     

![Кнопка Webhook](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="06d0f-234">Hello следующем рисунке показан запрос hello, отправляемых из Windows PowerShell, а также получаемые ответы hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-234">hello following image shows hello request being sent from Windows PowerShell and hello resulting response.</span></span>  <span data-ttu-id="06d0f-235">Идентификатор задания Hello извлекается из ответа hello и tooa преобразованной строки.</span><span class="sxs-lookup"><span data-stu-id="06d0f-235">hello job id is extracted from hello response and converted tooa string.</span></span>

![Кнопка Webhook](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="06d0f-237">Hello следующий пример модуля runbook принимает hello предыдущего примера запрос и запускает hello виртуальных машин, указанный в тексте запроса hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-237">hello following sample runbook accepts hello previous example request and starts hello virtual machines specified in hello request body.</span></span>

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

            # Authenticate tooAzure resources
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
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a><span data-ttu-id="06d0f-238">Запуск модулей Runbook в ответ tooAzure оповещения</span><span class="sxs-lookup"><span data-stu-id="06d0f-238">Starting runbooks in response tooAzure alerts</span></span>
<span data-ttu-id="06d0f-239">Модули Runbook с поддержкой веб-перехватчика также может быть используется tooreact[оповещения Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="06d0f-239">Webhook-enabled runbooks can be used tooreact too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="06d0f-240">Ресурсы в Azure можно отслеживать путем сбора статистики hello как производительности, доступности и использования с помощью hello оповещения Azure.</span><span class="sxs-lookup"><span data-stu-id="06d0f-240">Resources in Azure can be monitored by collecting hello statistics like performance, availability and usage with hello help of Azure alerts.</span></span> <span data-ttu-id="06d0f-241">Вы можете получать оповещения на основе отслеживания метрик или событий в ресурсах Azure, сейчас учетные записи автоматизации поддерживают только метрики.</span><span class="sxs-lookup"><span data-stu-id="06d0f-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="06d0f-242">Если значение hello указанной метрики превышает hello установленный порог, заданный или, если настроена hello события затем toohello администратора или соадминистраторам tooresolve hello предупреждение службы, Дополнительные сведения о показателях отправляется уведомление о и событий можно найти слишком[ Оповещения Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="06d0f-242">When hello value of a specified metric exceeds hello threshold assigned or if hello configured event is triggered then a notification is sent toohello service admin or co-admins tooresolve hello alert, for more information on metrics and events please refer too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="06d0f-243">Помимо использования оповещения Azure как система уведомлений, можно также начнем Runbook в tooalerts ответа.</span><span class="sxs-lookup"><span data-stu-id="06d0f-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response tooalerts.</span></span> <span data-ttu-id="06d0f-244">Служба автоматизации Azure обеспечивает hello возможность toorun включен веб-перехватчика Runbook с оповещения Azure.</span><span class="sxs-lookup"><span data-stu-id="06d0f-244">Azure Automation provides hello capability toorun webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="06d0f-245">При превышении показателем hello настроен пороговое значение, то hello правило оповещения становится активным и триггеры hello веб-перехватчика автоматизации, который в свою очередь выполняет hello runbook.</span><span class="sxs-lookup"><span data-stu-id="06d0f-245">When a metric exceeds hello configured threshold value then hello alert rule becomes active and triggers hello automation webhook which in turn executes hello runbook.</span></span>

![Объекты Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="06d0f-247">Контекст оповещения</span><span class="sxs-lookup"><span data-stu-id="06d0f-247">Alert context</span></span>
<span data-ttu-id="06d0f-248">ЦП этой машины является одним из hello метрики производительности, учитывайте ресурс Azure, такие как виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="06d0f-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of hello key performance metric.</span></span> <span data-ttu-id="06d0f-249">Если hello ЦП — 100% или превышает определенное длительного периода времени, может потребоваться toorestart hello виртуальной машины toofix hello проблему.</span><span class="sxs-lookup"><span data-stu-id="06d0f-249">If hello CPU utilization is 100% or more than a certain amount for long period of time, you might want toorestart hello virtual machine toofix hello problem.</span></span> <span data-ttu-id="06d0f-250">Это может быть решена Настройка виртуальной машины toohello правила оповещения и это правило имеет процент использования ЦП в качестве его метрик.</span><span class="sxs-lookup"><span data-stu-id="06d0f-250">This can be solved by configuring an alert rule toohello virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="06d0f-251">Здесь процент использования ЦП берется только в качестве примера, но существует множество метрик, которые можно настроить tooyour Azure ресурсов и перезапуск hello виртуальной машины — это действие, будет предпринято toofix эту проблему, hello runbook tootake можно настроить другие действия.</span><span class="sxs-lookup"><span data-stu-id="06d0f-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure tooyour Azure resources and restarting hello virtual machine is an action that is taken toofix this issue, you can configure hello runbook tootake other actions.</span></span>

<span data-ttu-id="06d0f-252">После этого правила оповещения hello становится активным и триггеры hello runbook с поддержкой веб-перехватчика, он отправляет runbook toohello hello контекст предупреждения.</span><span class="sxs-lookup"><span data-stu-id="06d0f-252">When this hello alert rule becomes active and triggers hello webhook-enabled runbook, it sends hello alert context toohello runbook.</span></span> <span data-ttu-id="06d0f-253">[Контекст предупреждения](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) содержит сведения, включая **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** и **Timestamp** , необходимые для hello runbook tooidentify hello ресурса, на котором он будет предпринимать действия.</span><span class="sxs-lookup"><span data-stu-id="06d0f-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span> <span data-ttu-id="06d0f-254">Предупреждения, контекст внедрен в часть текста hello hello **WebhookData** объекта отправленных toohello runbook, и можно осуществить с помощью **Webhook.RequestBody** свойство</span><span class="sxs-lookup"><span data-stu-id="06d0f-254">Alert context is embedded in hello body part of hello **WebhookData** object sent toohello runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="06d0f-255">Пример</span><span class="sxs-lookup"><span data-stu-id="06d0f-255">Example</span></span>
<span data-ttu-id="06d0f-256">Создание виртуальной машины Azure в подписку и связывание [предупреждения toomonitor ЦП в процентах метрика](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="06d0f-256">Create an Azure virtual machine in your subscription and associate an [alert toomonitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="06d0f-257">При создании предупреждения hello убедитесь, что необходимо заполнить поле веб-перехватчика hello hello URL-адрес веб-перехватчика hello, который был создан при создании веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="06d0f-257">While creating hello alert make sure you populate hello webhook field with hello URL of hello webhook which was generated while creating hello webhook.</span></span>

<span data-ttu-id="06d0f-258">Hello следующий пример модуля runbook инициируется при hello правило оповещения становится активным и собирает параметры hello контекст предупреждения, которые требуются для hello tooidentify runbook hello ресурса, на котором он будет предпринимать действия.</span><span class="sxs-lookup"><span data-stu-id="06d0f-258">hello following sample runbook is triggered when hello alert rule becomes active and it collects hello Alert context parameters which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span>

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

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
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

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="06d0f-259">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06d0f-259">Next steps</span></span>
* <span data-ttu-id="06d0f-260">Дополнительные сведения о различных способов toostart runbook см. в разделе [запуск Runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="06d0f-260">For details on different ways toostart a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="06d0f-261">Сведения о hello Просмотр состояния задания Runbook, см. в разделе слишком[выполнение модуля Runbook в автоматизации Azure](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="06d0f-261">For information on viewing hello Status of a Runbook Job, refer too[Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="06d0f-262">toouse действия tootake автоматизации Azure в Azure Alerts. в статье toolearn [устранения предупреждения виртуальной Машины Azure с Runbook автоматизации](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="06d0f-262">toolearn how toouse Azure Automation tootake action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
