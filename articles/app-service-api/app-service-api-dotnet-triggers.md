---
title: "Триггеры приложения API службы приложений | Документация Майкрософт"
description: "Как реализовать триггеры в приложении API в службе приложений Azure"
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
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="452e9-103">Триггеры приложения API службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="452e9-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="452e9-104">Эта версия статьи предназначена для приложений API со схемой версии 2014-12-01-preview.</span><span class="sxs-lookup"><span data-stu-id="452e9-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="452e9-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="452e9-105">Overview</span></span>
<span data-ttu-id="452e9-106">В этой статье описывается, как реализовать триггеры приложения API и использовать их из приложения логики.</span><span class="sxs-lookup"><span data-stu-id="452e9-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="452e9-107">Все фрагменты кода в этом разделе копируются из [примера кода приложения API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="452e9-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="452e9-108">Обратите внимание, что необходимо загрузить следующий пакет nuget для создания и запуска кода в этой статье: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="452e9-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="452e9-109">Что такое триггеры приложения API?</span><span class="sxs-lookup"><span data-stu-id="452e9-109">What are API app triggers?</span></span>
<span data-ttu-id="452e9-110">Приложения API создают события, чтобы клиенты приложения API могли предпринять соответствующие действия в ответ на событие.</span><span class="sxs-lookup"><span data-stu-id="452e9-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="452e9-111">Механизм на основе REST API, который поддерживает такой сценарий, называется триггер приложения API.</span><span class="sxs-lookup"><span data-stu-id="452e9-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="452e9-112">Например, предположим, что код клиента использует [приложение API с соединителем Twitter](../connectors/connectors-create-api-twitter.md) и код должен выполнять определенное действие на основании новых твитов с конкретными словами.</span><span class="sxs-lookup"><span data-stu-id="452e9-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="452e9-113">В таком случае можно настроить извещающий или опрашивающий триггер для упрощения этой задачи.</span><span class="sxs-lookup"><span data-stu-id="452e9-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="452e9-114">Сравнение триггера опроса и извещающего триггера</span><span class="sxs-lookup"><span data-stu-id="452e9-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="452e9-115">На данный момент поддерживаются два типа триггеров:</span><span class="sxs-lookup"><span data-stu-id="452e9-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="452e9-116">триггер опроса — клиент опрашивает приложение API для обнаружения уведомления о событии, которые было создано;</span><span class="sxs-lookup"><span data-stu-id="452e9-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="452e9-117">извещающий триггер — клиент получает уведомление от приложения API, когда создается событие.</span><span class="sxs-lookup"><span data-stu-id="452e9-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="452e9-118">Триггер опроса</span><span class="sxs-lookup"><span data-stu-id="452e9-118">Poll trigger</span></span>
<span data-ttu-id="452e9-119">Триггер опроса реализуется как обычный REST API и ожидает, что его клиенты (например, приложения логики) опросят его для получения уведомлений.</span><span class="sxs-lookup"><span data-stu-id="452e9-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="452e9-120">Хотя клиент может сохранять состояние, сам триггер опроса не имеет состояния.</span><span class="sxs-lookup"><span data-stu-id="452e9-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="452e9-121">Следующая информация о пакетах запросов и ответов показывает некоторые ключевые аспекты контракта триггера опроса:</span><span class="sxs-lookup"><span data-stu-id="452e9-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="452e9-122">Запрос</span><span class="sxs-lookup"><span data-stu-id="452e9-122">Request</span></span>
  * <span data-ttu-id="452e9-123">Метод HTTP: GET</span><span class="sxs-lookup"><span data-stu-id="452e9-123">HTTP method: GET</span></span>
  * <span data-ttu-id="452e9-124">Параметры</span><span class="sxs-lookup"><span data-stu-id="452e9-124">Parameters</span></span>
    * <span data-ttu-id="452e9-125">triggerState — этот необязательный параметр позволяет клиентам указать их состояние, чтобы триггер опроса мог правильно определить, следует ли возвращать уведомления, основываясь на указанном состоянии.</span><span class="sxs-lookup"><span data-stu-id="452e9-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="452e9-126">Параметры, относящиеся к API</span><span class="sxs-lookup"><span data-stu-id="452e9-126">API-specific parameters</span></span>
* <span data-ttu-id="452e9-127">Ответ</span><span class="sxs-lookup"><span data-stu-id="452e9-127">Response</span></span>
  * <span data-ttu-id="452e9-128">Код состояния **200** — запрос действителен, и существует уведомление от триггера.</span><span class="sxs-lookup"><span data-stu-id="452e9-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="452e9-129">Содержимое уведомления будет являться текстом ответа.</span><span class="sxs-lookup"><span data-stu-id="452e9-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="452e9-130">Заголовок «Retry-After» в ответе указывает, что необходимо получить дополнительные данные уведомления с последующим вызовом запроса.</span><span class="sxs-lookup"><span data-stu-id="452e9-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="452e9-131">Код состояния **202** — запрос действителен, но нет новых уведомлений от триггера.</span><span class="sxs-lookup"><span data-stu-id="452e9-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="452e9-132">Код состояния **4xx** — запрос недействителен.</span><span class="sxs-lookup"><span data-stu-id="452e9-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="452e9-133">Клиенту не следует повторять запрос.</span><span class="sxs-lookup"><span data-stu-id="452e9-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="452e9-134">Код состояния **5xx** — запрос привел к появлению внутренней ошибки сервера и/или временной проблемы.</span><span class="sxs-lookup"><span data-stu-id="452e9-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="452e9-135">Клиенту следует повторить запрос.</span><span class="sxs-lookup"><span data-stu-id="452e9-135">The client should retry the request.</span></span>

<span data-ttu-id="452e9-136">В следующем фрагменте кода приведен пример реализации триггера опроса.</span><span class="sxs-lookup"><span data-stu-id="452e9-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="452e9-137">Чтобы протестировать этот триггер опроса, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="452e9-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="452e9-138">Разверните приложение API с параметром проверки подлинности **общедоступный (анонимный)**.</span><span class="sxs-lookup"><span data-stu-id="452e9-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="452e9-139">Вызовите операцию **touch** для обращения к файлу.</span><span class="sxs-lookup"><span data-stu-id="452e9-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="452e9-140">На следующем изображении приведен пример запроса через инструмент Postman.</span><span class="sxs-lookup"><span data-stu-id="452e9-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="452e9-141">![Вызов операции «touch» через Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="452e9-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="452e9-142">Вызовите триггер опроса, для которого значение параметра **triggerState** соответствует метке времени ранее шага 2.</span><span class="sxs-lookup"><span data-stu-id="452e9-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="452e9-143">На следующем изображении приведен пример запроса через инструмент Postman.</span><span class="sxs-lookup"><span data-stu-id="452e9-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="452e9-144">![Вызов триггера опроса через Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="452e9-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="452e9-145">Извещающий триггер</span><span class="sxs-lookup"><span data-stu-id="452e9-145">Push trigger</span></span>
<span data-ttu-id="452e9-146">Извещающий триггер реализован в виде регулярного REST API, который отправляет уведомления на клиенты, зарегистрированные для получения уведомлений о возникновении определенных событий.</span><span class="sxs-lookup"><span data-stu-id="452e9-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="452e9-147">Следующая информация о пакетах запросов и ответов показывает некоторые ключевые аспекты контракта извещающего триггера.</span><span class="sxs-lookup"><span data-stu-id="452e9-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="452e9-148">Запрос</span><span class="sxs-lookup"><span data-stu-id="452e9-148">Request</span></span>
  * <span data-ttu-id="452e9-149">Метод HTTP: PUT</span><span class="sxs-lookup"><span data-stu-id="452e9-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="452e9-150">Параметры</span><span class="sxs-lookup"><span data-stu-id="452e9-150">Parameters</span></span>
    * <span data-ttu-id="452e9-151">triggerId: обязательно — непрозрачная строка (например, GUID), представляющая регистрацию извещающего триггера.</span><span class="sxs-lookup"><span data-stu-id="452e9-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="452e9-152">callbackUrl: обязательно — URL-адрес обратного вызова, осуществляемого при возникновении события.</span><span class="sxs-lookup"><span data-stu-id="452e9-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="452e9-153">Вызов — это простой вызов POST HTTP.</span><span class="sxs-lookup"><span data-stu-id="452e9-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="452e9-154">Параметры, относящиеся к API</span><span class="sxs-lookup"><span data-stu-id="452e9-154">API-specific parameters</span></span>
* <span data-ttu-id="452e9-155">Ответ</span><span class="sxs-lookup"><span data-stu-id="452e9-155">Response</span></span>
  * <span data-ttu-id="452e9-156">Код состояния **200** — запрос на регистрацию клиента успешно завершен.</span><span class="sxs-lookup"><span data-stu-id="452e9-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="452e9-157">Код состояния **4xx** — запрос недействителен.</span><span class="sxs-lookup"><span data-stu-id="452e9-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="452e9-158">Клиенту не следует повторять запрос.</span><span class="sxs-lookup"><span data-stu-id="452e9-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="452e9-159">Код состояния **5xx** — запрос привел к появлению внутренней ошибки сервера и/или временной проблемы.</span><span class="sxs-lookup"><span data-stu-id="452e9-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="452e9-160">Клиенту следует повторить запрос.</span><span class="sxs-lookup"><span data-stu-id="452e9-160">The client should retry the request.</span></span>
* <span data-ttu-id="452e9-161">Обратный вызов</span><span class="sxs-lookup"><span data-stu-id="452e9-161">Callback</span></span>
  * <span data-ttu-id="452e9-162">Метод HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="452e9-162">HTTP method: POST</span></span>
  * <span data-ttu-id="452e9-163">Текст запроса: содержимое уведомления.</span><span class="sxs-lookup"><span data-stu-id="452e9-163">Request body: Notification content.</span></span>

<span data-ttu-id="452e9-164">В следующем фрагменте кода приведен пример реализации извещающего триггера.</span><span class="sxs-lookup"><span data-stu-id="452e9-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
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
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="452e9-165">Чтобы протестировать этот триггер опроса, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="452e9-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="452e9-166">Разверните приложение API с параметром проверки подлинности **общедоступный (анонимный)**.</span><span class="sxs-lookup"><span data-stu-id="452e9-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="452e9-167">Перейдите к [http://requestb.in/](http://requestb.in/) для создания RequestBin, который будет использоваться в качестве URL-адрес обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="452e9-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="452e9-168">Вызовите извещающий триггер со значением идентификатора GUID **triggerId** и URL-адресом RequestBin — **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="452e9-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="452e9-169">![Вызов извещающего триггера через Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="452e9-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="452e9-170">Вызовите операцию **touch** для обращения к файлу.</span><span class="sxs-lookup"><span data-stu-id="452e9-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="452e9-171">На следующем изображении приведен пример запроса через инструмент Postman.</span><span class="sxs-lookup"><span data-stu-id="452e9-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="452e9-172">![Вызов операции «touch» через Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="452e9-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="452e9-173">Проверьте RequestBin, чтобы убедиться, что обратный вызов извещающего триггера выполняется с выводом свойства.</span><span class="sxs-lookup"><span data-stu-id="452e9-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="452e9-174">![Вызов триггера опроса через Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="452e9-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="452e9-175">Описание триггеров в определении API</span><span class="sxs-lookup"><span data-stu-id="452e9-175">Describe triggers in API definition</span></span>
<span data-ttu-id="452e9-176">После реализации триггеров и развертывания приложения API в Azure перейдите к колонке **Определение API** на портале предварительной версии Azure и вы увидите, что триггеры автоматически распознаются в пользовательском интерфейсе, управляемом с помощью определения Swagger 2.0 приложения API.</span><span class="sxs-lookup"><span data-stu-id="452e9-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![Колонка определения API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="452e9-178">Если нажать кнопку **Загрузить Swagger** и открыть файл JSON, вы увидите результаты, аналогичные следующим:</span><span class="sxs-lookup"><span data-stu-id="452e9-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

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

<span data-ttu-id="452e9-179">Свойство расширения **x-ms-schedular-trigger** определяет, как триггеры описаны в определении API, оно автоматически добавляется на шлюзе приложения API при запросе определения API через шлюз, если запрос осуществляется к одному из следующих критериев.</span><span class="sxs-lookup"><span data-stu-id="452e9-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="452e9-180">(Это свойство также можно добавить вручную.)</span><span class="sxs-lookup"><span data-stu-id="452e9-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="452e9-181">Триггер опроса</span><span class="sxs-lookup"><span data-stu-id="452e9-181">Poll trigger</span></span>
  * <span data-ttu-id="452e9-182">Если используется метод HTTP **GET**.</span><span class="sxs-lookup"><span data-stu-id="452e9-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="452e9-183">Если свойство **operationId** содержит строку **trigger**.</span><span class="sxs-lookup"><span data-stu-id="452e9-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="452e9-184">Если свойство **parameters** включает параметр со свойством **name**, для которого установлено значение **triggerState**.</span><span class="sxs-lookup"><span data-stu-id="452e9-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="452e9-185">Извещающий триггер</span><span class="sxs-lookup"><span data-stu-id="452e9-185">Push trigger</span></span>
  * <span data-ttu-id="452e9-186">Если используется метод HTTP **PUT**.</span><span class="sxs-lookup"><span data-stu-id="452e9-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="452e9-187">Если свойство **operationId** содержит строку **trigger**.</span><span class="sxs-lookup"><span data-stu-id="452e9-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="452e9-188">Если свойство **parameters** включает параметр со свойством **name**, для которого установлено значение **triggerId**.</span><span class="sxs-lookup"><span data-stu-id="452e9-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="452e9-189">Использование триггеров приложения API в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="452e9-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="452e9-190">Перечисление и настройка триггеров приложения API в конструкторе приложений логики</span><span class="sxs-lookup"><span data-stu-id="452e9-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="452e9-191">При создании приложения логики в той же группе ресурсов, что и приложение API, можно добавить его на полотно конструктора, просто щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="452e9-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="452e9-192">Это показано на следующих изображениях.</span><span class="sxs-lookup"><span data-stu-id="452e9-192">The following images illustrate this:</span></span>

![Триггеры в конструкторе приложения логики](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Настройка триггера опроса в конструкторе приложения логики](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Настройка извещающего триггера в конструкторе приложения логики](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="452e9-196">Оптимизация триггеров приложения API для приложений логики</span><span class="sxs-lookup"><span data-stu-id="452e9-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="452e9-197">После добавления триггеров в приложение API можно выполнить несколько действий для более удобного использования приложения API в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="452e9-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="452e9-198">Например, для параметра **triggerState** триггеров опроса должно быть присвоено следующее выражение в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="452e9-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="452e9-199">Это выражение должно оценивать последний вызов триггера из приложения логики и возвращают данное значение.</span><span class="sxs-lookup"><span data-stu-id="452e9-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="452e9-200">Примечание. Объяснение функций, используемых в выражении выше, см. в документации о [языке определения рабочего процесса приложения логики](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="452e9-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="452e9-201">Пользователям приложения логики необходимо указать упомянутое выше выражение для параметра **triggerState** при использовании триггера.</span><span class="sxs-lookup"><span data-stu-id="452e9-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="452e9-202">Это значение может быть предварительно задано с помощью конструктора приложения логики через свойство расширения **x-ms-scheduler-recommendation**.</span><span class="sxs-lookup"><span data-stu-id="452e9-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="452e9-203">Свойству расширения **x-ms-visibility** может быть присвоено значение *internal* , чтобы сам параметр не отображался в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="452e9-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="452e9-204">Это показано в следующем фрагменте.</span><span class="sxs-lookup"><span data-stu-id="452e9-204">The following snippet illustrates that.</span></span>

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

<span data-ttu-id="452e9-205">Для извещающих триггеров параметр **triggerId** должен однозначно определять приложение логики.</span><span class="sxs-lookup"><span data-stu-id="452e9-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="452e9-206">Рекомендуется присвоить этому свойству имя рабочего процесса с помощью следующего выражения:</span><span class="sxs-lookup"><span data-stu-id="452e9-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="452e9-207">С помощью свойств расширения **x-ms-scheduler-recommendation** и **x-ms-visibility** в его определении API приложение API может настроить конструктор приложения логики на автоматическую установку этого выражения для пользователя.</span><span class="sxs-lookup"><span data-stu-id="452e9-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="452e9-208">Добавление свойств расширения в определение API</span><span class="sxs-lookup"><span data-stu-id="452e9-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="452e9-209">В определение API можно добавить дополнительные сведения о метаданных, например свойства расширения **x-ms-scheduler-recommendation** и **x-ms-visibility**, одним из двух способов: статическим или динамическим.</span><span class="sxs-lookup"><span data-stu-id="452e9-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="452e9-210">Для статических метаданных можно непосредственно редактировать файл */metadata/apiDefinition.swagger.json* в проекте и добавить свойства вручную.</span><span class="sxs-lookup"><span data-stu-id="452e9-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="452e9-211">Для приложений API, использующих динамические метаданные, можно изменить файл SwaggerConfig.cs и добавить фильтр операции, который может добавить эти расширения.</span><span class="sxs-lookup"><span data-stu-id="452e9-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="452e9-212">Ниже приведен пример реализации этого класса для упрощения сценария с динамическими метаданными.</span><span class="sxs-lookup"><span data-stu-id="452e9-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
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
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
