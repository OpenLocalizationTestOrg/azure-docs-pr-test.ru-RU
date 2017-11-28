---
title: "триггеры приложение API службы aaaApp | Документы Microsoft"
description: "Как триггеры tooimplement в приложении API в службе приложений Azure"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="8dedf-103">Триггеры приложения API службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="8dedf-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="8dedf-104">Эта версия статьи hello применяется версия схемы 2014-12-01-preview tooAPI приложений.</span><span class="sxs-lookup"><span data-stu-id="8dedf-104">This version of hello article applies tooAPI apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="8dedf-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="8dedf-105">Overview</span></span>
<span data-ttu-id="8dedf-106">В этой статье объясняется, как приложение tooimplement API триггеры и использовать их из приложения логики.</span><span class="sxs-lookup"><span data-stu-id="8dedf-106">This article explains how tooimplement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="8dedf-107">Все фрагменты кода hello в этом разделе, копируются из hello [образец кода приложения API образца FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="8dedf-107">All of hello code snippets in this topic are copied from hello [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="8dedf-108">Обратите внимание, что вы будете toodownload hello следующий пакет nuget для кода hello в этой статье toobuild и запустите: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="8dedf-108">Note that you'll need toodownload hello following nuget package for hello code in this article toobuild and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="8dedf-109">Что такое триггеры приложения API?</span><span class="sxs-lookup"><span data-stu-id="8dedf-109">What are API app triggers?</span></span>
<span data-ttu-id="8dedf-110">Это очень распространенный сценарий для API приложения toofire событие клиенты API приложение hello предпринять соответствующие действия hello в ответ toohello событий.</span><span class="sxs-lookup"><span data-stu-id="8dedf-110">It's a common scenario for an API app toofire an event so that clients of hello API app can take hello appropriate action in response toohello event.</span></span> <span data-ttu-id="8dedf-111">Hello механизм на основе REST API, который поддерживает такой сценарий называется триггер приложения API.</span><span class="sxs-lookup"><span data-stu-id="8dedf-111">hello REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="8dedf-112">Например, предположим, что код клиента использует hello [приложения Twitter API соединителя](../connectors/connectors-create-api-twitter.md) и код должен tooperform действие на основании новых твиты, которые содержат конкретные слова.</span><span class="sxs-lookup"><span data-stu-id="8dedf-112">For example, let's say your client code is using hello [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs tooperform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="8dedf-113">В этом случае вы можете настроить триггер опроса и принудительной toofacilitate этой потребности.</span><span class="sxs-lookup"><span data-stu-id="8dedf-113">In this case, you might set up a poll or push trigger toofacilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="8dedf-114">Сравнение триггера опроса и извещающего триггера</span><span class="sxs-lookup"><span data-stu-id="8dedf-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="8dedf-115">На данный момент поддерживаются два типа триггеров:</span><span class="sxs-lookup"><span data-stu-id="8dedf-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="8dedf-116">Триггер опроса - Клиент опрашивает приложения hello API для уведомления о событии активна в данный момент</span><span class="sxs-lookup"><span data-stu-id="8dedf-116">Poll trigger - Client polls hello API app for notification of an event having been fired</span></span>
* <span data-ttu-id="8dedf-117">Триггер Push - клиент получает уведомление от приложения hello API при запуске события</span><span class="sxs-lookup"><span data-stu-id="8dedf-117">Push trigger - Client is notified by hello API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="8dedf-118">Триггер опроса</span><span class="sxs-lookup"><span data-stu-id="8dedf-118">Poll trigger</span></span>
<span data-ttu-id="8dedf-119">Триггер опроса реализуется в виде регулярного API REST и ожидает его toopoll клиентов (таких как приложения логики) в порядке tooget уведомления.</span><span class="sxs-lookup"><span data-stu-id="8dedf-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) toopoll it in order tooget notification.</span></span> <span data-ttu-id="8dedf-120">Пока клиент hello могут сохранять состояние, самим триггером hello опроса без сохранения состояния.</span><span class="sxs-lookup"><span data-stu-id="8dedf-120">While hello client may maintain state, hello poll trigger itself is stateless.</span></span>

<span data-ttu-id="8dedf-121">следующие сведения, касающиеся приветственных пакетов запросов и ответов Hello иллюстрируют некоторые ключевые аспекты hello опроса триггер контракта.</span><span class="sxs-lookup"><span data-stu-id="8dedf-121">hello following information regarding hello request and response packets illustrate some key aspects of hello poll trigger contract:</span></span>

* <span data-ttu-id="8dedf-122">Запрос</span><span class="sxs-lookup"><span data-stu-id="8dedf-122">Request</span></span>
  * <span data-ttu-id="8dedf-123">Метод HTTP: GET</span><span class="sxs-lookup"><span data-stu-id="8dedf-123">HTTP method: GET</span></span>
  * <span data-ttu-id="8dedf-124">Параметры</span><span class="sxs-lookup"><span data-stu-id="8dedf-124">Parameters</span></span>
    * <span data-ttu-id="8dedf-125">triggerState - этот дополнительный параметр позволяет клиентам toospecify свое состояние так, hello опроса триггер может правильно решить, указано ли уведомление tooreturn или hello не на основе состояния.</span><span class="sxs-lookup"><span data-stu-id="8dedf-125">triggerState - This optional parameter allows clients toospecify their state so that hello poll trigger can properly decide whether tooreturn notification or not based on hello specified state.</span></span>
    * <span data-ttu-id="8dedf-126">Параметры, относящиеся к API</span><span class="sxs-lookup"><span data-stu-id="8dedf-126">API-specific parameters</span></span>
* <span data-ttu-id="8dedf-127">Ответ</span><span class="sxs-lookup"><span data-stu-id="8dedf-127">Response</span></span>
  * <span data-ttu-id="8dedf-128">Код состояния **200** - запрос является допустимым, и есть уведомление из триггера hello.</span><span class="sxs-lookup"><span data-stu-id="8dedf-128">Status code **200** - Request is valid and there is a notification from hello trigger.</span></span> <span data-ttu-id="8dedf-129">содержимое Hello hello уведомления будет hello текст ответа.</span><span class="sxs-lookup"><span data-stu-id="8dedf-129">hello content of hello notification will be hello response body.</span></span> <span data-ttu-id="8dedf-130">Заголовок «Retry-After» в ответ hello указывает, что дополнительные уведомления данные необходимо получить с помощью вызова последующего запроса.</span><span class="sxs-lookup"><span data-stu-id="8dedf-130">A "Retry-After" header in hello response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="8dedf-131">Код состояния **202** — запрос является допустимым, но нет новых уведомления из триггера hello.</span><span class="sxs-lookup"><span data-stu-id="8dedf-131">Status code **202** - Request is valid, but there is no new notification from hello trigger.</span></span>
  * <span data-ttu-id="8dedf-132">Код состояния **4xx** — запрос недействителен.</span><span class="sxs-lookup"><span data-stu-id="8dedf-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="8dedf-133">Hello клиента не следует повторить запрос hello.</span><span class="sxs-lookup"><span data-stu-id="8dedf-133">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="8dedf-134">Код состояния **5xx** — запрос привел к появлению внутренней ошибки сервера и/или временной проблемы.</span><span class="sxs-lookup"><span data-stu-id="8dedf-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="8dedf-135">Hello клиенту следует повторить запрос hello.</span><span class="sxs-lookup"><span data-stu-id="8dedf-135">hello client should retry hello request.</span></span>

<span data-ttu-id="8dedf-136">Следующий фрагмент кода Hello примером может служить как триггер tooimplement опрос.</span><span class="sxs-lookup"><span data-stu-id="8dedf-136">hello following code snippet is an example of how tooimplement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="8dedf-137">tootest запустить этот опроса, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8dedf-137">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="8dedf-138">Развертывание hello API приложения с помощью параметра проверки подлинности из **открытого анонимного**.</span><span class="sxs-lookup"><span data-stu-id="8dedf-138">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="8dedf-139">Вызовите hello **touch** операции tootouch файла.</span><span class="sxs-lookup"><span data-stu-id="8dedf-139">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="8dedf-140">Следующие изображения Hello показывает пример запроса через почтальон.</span><span class="sxs-lookup"><span data-stu-id="8dedf-140">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="8dedf-141">![Вызов операции «touch» через Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="8dedf-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="8dedf-142">Вызвать триггер опроса hello с hello **triggerState** параметру tooa время отметки предыдущих tooStep #2.</span><span class="sxs-lookup"><span data-stu-id="8dedf-142">Call hello poll trigger with hello **triggerState** parameter set tooa time stamp prior tooStep #2.</span></span> <span data-ttu-id="8dedf-143">Hello на иллюстрации показан пример запроса hello через почтальон.</span><span class="sxs-lookup"><span data-stu-id="8dedf-143">hello following image shows hello sample request via Postman.</span></span>
   <span data-ttu-id="8dedf-144">![Вызов триггера опроса через Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="8dedf-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="8dedf-145">Извещающий триггер</span><span class="sxs-lookup"><span data-stu-id="8dedf-145">Push trigger</span></span>
<span data-ttu-id="8dedf-146">Извещающий триггер реализуется в виде регулярного API REST, который помещает tooclients уведомления, зарегистрировавшего toobe уведомления при запуске определенных событий.</span><span class="sxs-lookup"><span data-stu-id="8dedf-146">A push trigger is implemented as a regular REST API that pushes notifications tooclients who have registered toobe notified when specific events fire.</span></span>

<span data-ttu-id="8dedf-147">следующие сведения, касающиеся приветственных пакетов запросов и ответов Hello иллюстрируют некоторые ключевые аспекты hello принудительной триггер контракта.</span><span class="sxs-lookup"><span data-stu-id="8dedf-147">hello following information regarding hello request and response packets illustrate some key aspects of hello push trigger contract.</span></span>

* <span data-ttu-id="8dedf-148">Запрос</span><span class="sxs-lookup"><span data-stu-id="8dedf-148">Request</span></span>
  * <span data-ttu-id="8dedf-149">Метод HTTP: PUT</span><span class="sxs-lookup"><span data-stu-id="8dedf-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="8dedf-150">Параметры</span><span class="sxs-lookup"><span data-stu-id="8dedf-150">Parameters</span></span>
    * <span data-ttu-id="8dedf-151">triggerId: требуется — непрозрачный строки (например, GUID), представляет hello регистрации извещающий триггер.</span><span class="sxs-lookup"><span data-stu-id="8dedf-151">triggerId: required - Opaque string (such as a GUID) that represents hello registration of a push trigger.</span></span>
    * <span data-ttu-id="8dedf-152">callbackUrl: требуется - URL-адрес hello tooinvoke обратного вызова при запуске события hello.</span><span class="sxs-lookup"><span data-stu-id="8dedf-152">callbackUrl: required - URL of hello callback tooinvoke when hello event fires.</span></span> <span data-ttu-id="8dedf-153">вызов Hello является простым вызовом POST HTTP.</span><span class="sxs-lookup"><span data-stu-id="8dedf-153">hello invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="8dedf-154">Параметры, относящиеся к API</span><span class="sxs-lookup"><span data-stu-id="8dedf-154">API-specific parameters</span></span>
* <span data-ttu-id="8dedf-155">Ответ</span><span class="sxs-lookup"><span data-stu-id="8dedf-155">Response</span></span>
  * <span data-ttu-id="8dedf-156">Код состояния **200** -клиент tooregister запрос успешно.</span><span class="sxs-lookup"><span data-stu-id="8dedf-156">Status code **200** - Request tooregister client successful.</span></span>
  * <span data-ttu-id="8dedf-157">Код состояния **4xx** — запрос недействителен.</span><span class="sxs-lookup"><span data-stu-id="8dedf-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="8dedf-158">Hello клиента не следует повторить запрос hello.</span><span class="sxs-lookup"><span data-stu-id="8dedf-158">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="8dedf-159">Код состояния **5xx** — запрос привел к появлению внутренней ошибки сервера и/или временной проблемы.</span><span class="sxs-lookup"><span data-stu-id="8dedf-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="8dedf-160">Hello клиенту следует повторить запрос hello.</span><span class="sxs-lookup"><span data-stu-id="8dedf-160">hello client should retry hello request.</span></span>
* <span data-ttu-id="8dedf-161">Обратный вызов</span><span class="sxs-lookup"><span data-stu-id="8dedf-161">Callback</span></span>
  * <span data-ttu-id="8dedf-162">Метод HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="8dedf-162">HTTP method: POST</span></span>
  * <span data-ttu-id="8dedf-163">Текст запроса: содержимое уведомления.</span><span class="sxs-lookup"><span data-stu-id="8dedf-163">Request body: Notification content.</span></span>

<span data-ttu-id="8dedf-164">Следующий фрагмент кода Hello примером может служить как триггер tooimplement push:</span><span class="sxs-lookup"><span data-stu-id="8dedf-164">hello following code snippet is an example of how tooimplement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="8dedf-165">tootest запустить этот опроса, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8dedf-165">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="8dedf-166">Развертывание hello API приложения с помощью параметра проверки подлинности из **открытого анонимного**.</span><span class="sxs-lookup"><span data-stu-id="8dedf-166">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="8dedf-167">Обзор слишком[http://requestb.in/](http://requestb.in/) toocreate RequestBin, который будет использоваться в качестве URL-адрес обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="8dedf-167">Browse too[http://requestb.in/](http://requestb.in/) toocreate a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="8dedf-168">Вызовите hello извещающий триггер с GUID как **triggerId** и hello RequestBin URL-адрес как **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="8dedf-168">Call hello push trigger with a GUID as **triggerId** and hello RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="8dedf-169">![Вызов извещающего триггера через Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="8dedf-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="8dedf-170">Вызовите hello **touch** операции tootouch файла.</span><span class="sxs-lookup"><span data-stu-id="8dedf-170">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="8dedf-171">Следующие изображения Hello показывает пример запроса через почтальон.</span><span class="sxs-lookup"><span data-stu-id="8dedf-171">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="8dedf-172">![Вызов операции «touch» через Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="8dedf-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="8dedf-173">Убедитесь, что tooconfirm RequestBin hello, hello обратного вызова триггера push вызывается с выходного свойства.</span><span class="sxs-lookup"><span data-stu-id="8dedf-173">Check hello RequestBin tooconfirm that hello push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="8dedf-174">![Вызов триггера опроса через Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="8dedf-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="8dedf-175">Описание триггеров в определении API</span><span class="sxs-lookup"><span data-stu-id="8dedf-175">Describe triggers in API definition</span></span>
<span data-ttu-id="8dedf-176">После реализации триггеров hello и развертыванию ваш tooAzure API приложения, перейдите toohello **определения API** колонки в портал предварительной версии Azure hello и вы увидите, триггеры автоматически распознаются в hello пользовательского интерфейса, который управляется событиями Здравствуйте, определение Swagger 2.0 API приложение hello API.</span><span class="sxs-lookup"><span data-stu-id="8dedf-176">After implementing hello triggers and deploying your API app tooAzure, navigate toohello **API Definition** blade in hello Azure preview portal and you'll see that triggers are automatically recognized in hello UI, which is driven by hello Swagger 2.0 API definition of hello API app.</span></span>

![Колонка определения API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="8dedf-178">Если щелкнуть hello **загрузки Swagger** кнопку и откройте hello JSON-файл, вы увидите примерно toohello результаты следующие:</span><span class="sxs-lookup"><span data-stu-id="8dedf-178">If you click hello **Download Swagger** button and open hello JSON file, you'll see results similar toohello following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="8dedf-179">Здравствуйте, свойства расширения **x-ms-schedular триггер** заключается в том, как триггеры описанных в определении API и автоматически добавляется шлюзом приложения hello API при запросе определения hello API через шлюз hello hello запрос tooone из Здравствуйте, следующие условия.</span><span class="sxs-lookup"><span data-stu-id="8dedf-179">hello extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by hello API app gateway when you request hello API definition via hello gateway if hello request tooone of hello following criteria.</span></span> <span data-ttu-id="8dedf-180">(Это свойство также можно добавить вручную.)</span><span class="sxs-lookup"><span data-stu-id="8dedf-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="8dedf-181">Триггер опроса</span><span class="sxs-lookup"><span data-stu-id="8dedf-181">Poll trigger</span></span>
  * <span data-ttu-id="8dedf-182">Если hello метод HTTP **получить**.</span><span class="sxs-lookup"><span data-stu-id="8dedf-182">If hello HTTP method is **GET**.</span></span>
  * <span data-ttu-id="8dedf-183">Если hello **идентификатором операции** свойство содержит строку hello **триггер**.</span><span class="sxs-lookup"><span data-stu-id="8dedf-183">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="8dedf-184">Если hello **параметры** свойства включает параметр с **имя** значение свойства слишком**triggerState**.</span><span class="sxs-lookup"><span data-stu-id="8dedf-184">If hello **parameters** property includes a parameter with a **name** property set too**triggerState**.</span></span>
* <span data-ttu-id="8dedf-185">Извещающий триггер</span><span class="sxs-lookup"><span data-stu-id="8dedf-185">Push trigger</span></span>
  * <span data-ttu-id="8dedf-186">Если hello метод HTTP **ПОМЕСТИТЬ**.</span><span class="sxs-lookup"><span data-stu-id="8dedf-186">If hello HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="8dedf-187">Если hello **идентификатором операции** свойство содержит строку hello **триггер**.</span><span class="sxs-lookup"><span data-stu-id="8dedf-187">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="8dedf-188">Если hello **параметры** свойства включает параметр с **имя** значение свойства слишком**triggerId**.</span><span class="sxs-lookup"><span data-stu-id="8dedf-188">If hello **parameters** property includes a parameter with a **name** property set too**triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="8dedf-189">Использование триггеров приложения API в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="8dedf-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a><span data-ttu-id="8dedf-190">Просматривать и настраивать триггеры API приложения в конструкторе приложений логики hello</span><span class="sxs-lookup"><span data-stu-id="8dedf-190">List and configure API app triggers in hello Logic apps designer</span></span>
<span data-ttu-id="8dedf-191">При создании приложения логики в hello же группе ресурсов Здравствуйте приложения API, можно будет tooadd его toohello полотне конструктора, просто щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="8dedf-191">If you create a Logic app in hello same resource group as hello API app, you will be able tooadd it toohello designer canvas simply by clicking it.</span></span> <span data-ttu-id="8dedf-192">Это иллюстрирует Hello следующие образы:</span><span class="sxs-lookup"><span data-stu-id="8dedf-192">hello following images illustrate this:</span></span>

![Триггеры в конструкторе приложения логики](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Настройка триггера опроса в конструкторе приложения логики](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Настройка извещающего триггера в конструкторе приложения логики](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="8dedf-196">Оптимизация триггеров приложения API для приложений логики</span><span class="sxs-lookup"><span data-stu-id="8dedf-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="8dedf-197">После добавления триггеры tooan API приложения существует несколько вы можете делать tooimprove hello качества при использовании приложения hello API в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="8dedf-197">After you add triggers tooan API app, there are a few things you can do tooimprove hello experience when using hello API app in a Logic app.</span></span>

<span data-ttu-id="8dedf-198">Здравствуйте, например, **triggerState** параметр для триггеров опроса должен быть установлен toohello следующее выражение в приложение логику hello.</span><span class="sxs-lookup"><span data-stu-id="8dedf-198">For instance, hello **triggerState** parameter for poll triggers should be set toohello following expression in hello Logic app.</span></span> <span data-ttu-id="8dedf-199">Это выражение следует оценить hello последнего вызова hello триггера из hello логику приложения и возвращать это значение.</span><span class="sxs-lookup"><span data-stu-id="8dedf-199">This expression should evaluate hello last invocation of hello trigger from hello Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="8dedf-200">Примечание: Описание функции hello, используемые в выражении hello выше, см. документацию toohello на [язык определения рабочих процессов приложений логики](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="8dedf-200">NOTE: For an explanation of hello functions used in hello expression above, refer toohello documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="8dedf-201">Логика приложения пользователи должны будут выражение hello tooprovide выше для hello **triggerState** параметр при использовании hello триггера.</span><span class="sxs-lookup"><span data-stu-id="8dedf-201">Logic app users would need tooprovide hello expression above for hello **triggerState** parameter while using hello trigger.</span></span> <span data-ttu-id="8dedf-202">Это возможно toohave это значение конфигурации hello логику приложения конструктора через свойство расширения hello **x-ms планировщика рекомендация**.</span><span class="sxs-lookup"><span data-stu-id="8dedf-202">It is possible toohave this value preset by hello Logic app designer through hello extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="8dedf-203">Hello **x-ms видимость** расширение может быть установлено значение tooa *внутренней* , чтобы сам параметр hello не отображается в конструкторе hello.</span><span class="sxs-lookup"><span data-stu-id="8dedf-203">hello **x-ms-visibility** extension property can be set tooa value of *internal* so that hello parameter itself is not shown on hello designer.</span></span>  <span data-ttu-id="8dedf-204">Привет, следующий фрагмент кода показывает, что.</span><span class="sxs-lookup"><span data-stu-id="8dedf-204">hello following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="8dedf-205">Триггеры принудительной hello **triggerId** параметр должен однозначно определять приложение hello логику.</span><span class="sxs-lookup"><span data-stu-id="8dedf-205">For push triggers, hello **triggerId** parameter must uniquely identify hello Logic app.</span></span> <span data-ttu-id="8dedf-206">Рекомендуется tooset toohello имени этого свойства hello рабочего процесса с помощью hello, следующее выражение:</span><span class="sxs-lookup"><span data-stu-id="8dedf-206">A recommended best practice is tooset this property toohello name of hello workflow by using hello following expression:</span></span>

    @workflow().name

<span data-ttu-id="8dedf-207">С помощью hello **x-ms планировщика рекомендация** и **x-ms видимость** свойства расширения в его определения API, hello приложения API может передать задайте конструктора tooautomatically toohello логику приложения выражение для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="8dedf-207">Using hello **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, hello API app can convey toohello Logic app designer tooautomatically set this expression for hello user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="8dedf-208">Добавление свойств расширения в определение API</span><span class="sxs-lookup"><span data-stu-id="8dedf-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="8dedf-209">Дополнительные сведения о метаданных - как свойства расширения hello **x-ms планировщика рекомендация** и **x-ms видимость** -могут добавляться в определении-hello API в одном из двух способов: статическим или динамическим.</span><span class="sxs-lookup"><span data-stu-id="8dedf-209">Additional metadata information - such as hello extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in hello API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="8dedf-210">Для статических метаданных можно непосредственно редактировать hello */metadata/apiDefinition.swagger.json* и вручную добавьте hello свойств файла в проекте.</span><span class="sxs-lookup"><span data-stu-id="8dedf-210">For static metadata, you can directly edit hello */metadata/apiDefinition.swagger.json* file in your project and add hello properties manually.</span></span>

<span data-ttu-id="8dedf-211">Для приложений API, с помощью динамических метаданных можно изменить hello SwaggerConfig.cs файл tooadd операции фильтр, который можно добавить эти расширения.</span><span class="sxs-lookup"><span data-stu-id="8dedf-211">For API apps using dynamic metadata, you can edit hello SwaggerConfig.cs file tooadd an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="8dedf-212">Hello ниже приведен пример как этот класс может быть реализовано toofacilitate hello динамических метаданных сценария.</span><span class="sxs-lookup"><span data-stu-id="8dedf-212">hello following is an example of how this class can be implemented toofacilitate hello dynamic metadata scenario.</span></span>

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
