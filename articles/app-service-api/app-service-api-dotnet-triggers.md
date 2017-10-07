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
# <a name="azure-app-service-api-app-triggers"></a>Триггеры приложения API службы приложений Azure
> [!NOTE]
> Эта версия статьи hello применяется версия схемы 2014-12-01-preview tooAPI приложений.
>
>

## <a name="overview"></a>Обзор
В этой статье объясняется, как приложение tooimplement API триггеры и использовать их из приложения логики.

Все фрагменты кода hello в этом разделе, копируются из hello [образец кода приложения API образца FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).

Обратите внимание, что вы будете toodownload hello следующий пакет nuget для кода hello в этой статье toobuild и запустите: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).

## <a name="what-are-api-app-triggers"></a>Что такое триггеры приложения API?
Это очень распространенный сценарий для API приложения toofire событие клиенты API приложение hello предпринять соответствующие действия hello в ответ toohello событий. Hello механизм на основе REST API, который поддерживает такой сценарий называется триггер приложения API.

Например, предположим, что код клиента использует hello [приложения Twitter API соединителя](../connectors/connectors-create-api-twitter.md) и код должен tooperform действие на основании новых твиты, которые содержат конкретные слова. В этом случае вы можете настроить триггер опроса и принудительной toofacilitate этой потребности.

## <a name="poll-trigger-versus-push-trigger"></a>Сравнение триггера опроса и извещающего триггера
На данный момент поддерживаются два типа триггеров:

* Триггер опроса - Клиент опрашивает приложения hello API для уведомления о событии активна в данный момент
* Триггер Push - клиент получает уведомление от приложения hello API при запуске события

### <a name="poll-trigger"></a>Триггер опроса
Триггер опроса реализуется в виде регулярного API REST и ожидает его toopoll клиентов (таких как приложения логики) в порядке tooget уведомления. Пока клиент hello могут сохранять состояние, самим триггером hello опроса без сохранения состояния.

следующие сведения, касающиеся приветственных пакетов запросов и ответов Hello иллюстрируют некоторые ключевые аспекты hello опроса триггер контракта.

* Запрос
  * Метод HTTP: GET
  * Параметры
    * triggerState - этот дополнительный параметр позволяет клиентам toospecify свое состояние так, hello опроса триггер может правильно решить, указано ли уведомление tooreturn или hello не на основе состояния.
    * Параметры, относящиеся к API
* Ответ
  * Код состояния **200** - запрос является допустимым, и есть уведомление из триггера hello. содержимое Hello hello уведомления будет hello текст ответа. Заголовок «Retry-After» в ответ hello указывает, что дополнительные уведомления данные необходимо получить с помощью вызова последующего запроса.
  * Код состояния **202** — запрос является допустимым, но нет новых уведомления из триггера hello.
  * Код состояния **4xx** — запрос недействителен. Hello клиента не следует повторить запрос hello.
  * Код состояния **5xx** — запрос привел к появлению внутренней ошибки сервера и/или временной проблемы. Hello клиенту следует повторить запрос hello.

Следующий фрагмент кода Hello примером может служить как триггер tooimplement опрос.

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

tootest запустить этот опроса, выполните следующие действия:

1. Развертывание hello API приложения с помощью параметра проверки подлинности из **открытого анонимного**.
2. Вызовите hello **touch** операции tootouch файла. Следующие изображения Hello показывает пример запроса через почтальон.
   ![Вызов операции «touch» через Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Вызвать триггер опроса hello с hello **triggerState** параметру tooa время отметки предыдущих tooStep #2. Hello на иллюстрации показан пример запроса hello через почтальон.
   ![Вызов триггера опроса через Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>Извещающий триггер
Извещающий триггер реализуется в виде регулярного API REST, который помещает tooclients уведомления, зарегистрировавшего toobe уведомления при запуске определенных событий.

следующие сведения, касающиеся приветственных пакетов запросов и ответов Hello иллюстрируют некоторые ключевые аспекты hello принудительной триггер контракта.

* Запрос
  * Метод HTTP: PUT
  * Параметры
    * triggerId: требуется — непрозрачный строки (например, GUID), представляет hello регистрации извещающий триггер.
    * callbackUrl: требуется - URL-адрес hello tooinvoke обратного вызова при запуске события hello. вызов Hello является простым вызовом POST HTTP.
    * Параметры, относящиеся к API
* Ответ
  * Код состояния **200** -клиент tooregister запрос успешно.
  * Код состояния **4xx** — запрос недействителен. Hello клиента не следует повторить запрос hello.
  * Код состояния **5xx** — запрос привел к появлению внутренней ошибки сервера и/или временной проблемы. Hello клиенту следует повторить запрос hello.
* Обратный вызов
  * Метод HTTP: POST
  * Текст запроса: содержимое уведомления.

Следующий фрагмент кода Hello примером может служить как триггер tooimplement push:

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

tootest запустить этот опроса, выполните следующие действия:

1. Развертывание hello API приложения с помощью параметра проверки подлинности из **открытого анонимного**.
2. Обзор слишком[http://requestb.in/](http://requestb.in/) toocreate RequestBin, который будет использоваться в качестве URL-адрес обратного вызова.
3. Вызовите hello извещающий триггер с GUID как **triggerId** и hello RequestBin URL-адрес как **callbackUrl**.
   ![Вызов извещающего триггера через Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Вызовите hello **touch** операции tootouch файла. Следующие изображения Hello показывает пример запроса через почтальон.
   ![Вызов операции «touch» через Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. Убедитесь, что tooconfirm RequestBin hello, hello обратного вызова триггера push вызывается с выходного свойства.
   ![Вызов триггера опроса через Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>Описание триггеров в определении API
После реализации триггеров hello и развертыванию ваш tooAzure API приложения, перейдите toohello **определения API** колонки в портал предварительной версии Azure hello и вы увидите, триггеры автоматически распознаются в hello пользовательского интерфейса, который управляется событиями Здравствуйте, определение Swagger 2.0 API приложение hello API.

![Колонка определения API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Если щелкнуть hello **загрузки Swagger** кнопку и откройте hello JSON-файл, вы увидите примерно toohello результаты следующие:

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

Здравствуйте, свойства расширения **x-ms-schedular триггер** заключается в том, как триггеры описанных в определении API и автоматически добавляется шлюзом приложения hello API при запросе определения hello API через шлюз hello hello запрос tooone из Здравствуйте, следующие условия. (Это свойство также можно добавить вручную.)

* Триггер опроса
  * Если hello метод HTTP **получить**.
  * Если hello **идентификатором операции** свойство содержит строку hello **триггер**.
  * Если hello **параметры** свойства включает параметр с **имя** значение свойства слишком**triggerState**.
* Извещающий триггер
  * Если hello метод HTTP **ПОМЕСТИТЬ**.
  * Если hello **идентификатором операции** свойство содержит строку hello **триггер**.
  * Если hello **параметры** свойства включает параметр с **имя** значение свойства слишком**triggerId**.

## <a name="use-api-app-triggers-in-logic-apps"></a>Использование триггеров приложения API в приложениях логики
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>Просматривать и настраивать триггеры API приложения в конструкторе приложений логики hello
При создании приложения логики в hello же группе ресурсов Здравствуйте приложения API, можно будет tooadd его toohello полотне конструктора, просто щелкнув его. Это иллюстрирует Hello следующие образы:

![Триггеры в конструкторе приложения логики](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Настройка триггера опроса в конструкторе приложения логики](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Настройка извещающего триггера в конструкторе приложения логики](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>Оптимизация триггеров приложения API для приложений логики
После добавления триггеры tooan API приложения существует несколько вы можете делать tooimprove hello качества при использовании приложения hello API в приложение логики.

Здравствуйте, например, **triggerState** параметр для триггеров опроса должен быть установлен toohello следующее выражение в приложение логику hello. Это выражение следует оценить hello последнего вызова hello триггера из hello логику приложения и возвращать это значение.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

Примечание: Описание функции hello, используемые в выражении hello выше, см. документацию toohello на [язык определения рабочих процессов приложений логики](https://msdn.microsoft.com/library/azure/dn948512.aspx).

Логика приложения пользователи должны будут выражение hello tooprovide выше для hello **triggerState** параметр при использовании hello триггера. Это возможно toohave это значение конфигурации hello логику приложения конструктора через свойство расширения hello **x-ms планировщика рекомендация**.  Hello **x-ms видимость** расширение может быть установлено значение tooa *внутренней* , чтобы сам параметр hello не отображается в конструкторе hello.  Привет, следующий фрагмент кода показывает, что.

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

Триггеры принудительной hello **triggerId** параметр должен однозначно определять приложение hello логику. Рекомендуется tooset toohello имени этого свойства hello рабочего процесса с помощью hello, следующее выражение:

    @workflow().name

С помощью hello **x-ms планировщика рекомендация** и **x-ms видимость** свойства расширения в его определения API, hello приложения API может передать задайте конструктора tooautomatically toohello логику приложения выражение для пользователя hello.

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>Добавление свойств расширения в определение API
Дополнительные сведения о метаданных - как свойства расширения hello **x-ms планировщика рекомендация** и **x-ms видимость** -могут добавляться в определении-hello API в одном из двух способов: статическим или динамическим.

Для статических метаданных можно непосредственно редактировать hello */metadata/apiDefinition.swagger.json* и вручную добавьте hello свойств файла в проекте.

Для приложений API, с помощью динамических метаданных можно изменить hello SwaggerConfig.cs файл tooadd операции фильтр, который можно добавить эти расширения.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


Hello ниже приведен пример как этот класс может быть реализовано toofacilitate hello динамических метаданных сценария.

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
