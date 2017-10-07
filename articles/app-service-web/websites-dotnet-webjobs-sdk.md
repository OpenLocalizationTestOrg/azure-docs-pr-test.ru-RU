---
title: "aaaWhat — hello Azure SDK веб-заданий"
description: "Toohello введение веб-заданий Azure SDK. Объясняется, какие hello SDK — типичные сценарии бывает удобно для и примеры кода."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a>Что такое hello SDK веб-заданий Azure
## <a id="overview"></a>Обзор
В этой статье объясняется, что hello SDK веб-задания —, рассматриваются некоторые распространенные сценарии, он используется для и позволяет получить представление о том, как можно использовать в коде.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[Веб-заданий](websites-webjobs-resources.md) — это функция службы приложений Azure, которая позволяет toorun программу или скрипт в hello же контексте, что веб-приложения, приложения API или мобильного приложения. Здравствуйте, назначение hello [SDK веб-заданий](websites-webjobs-resources.md) является toosimplify hello код, предназначенный для выполнения стандартных задач, которые могут выполнять веб-задания, например обработки изображений, обработки очередей, объединение RSS, обслуживание файлов и отправки сообщений электронной почты. Hello SDK веб-задания имеет встроенные функции для работы с хранилищем Azure и Service Bus, планирование задач и обработка ошибок и других стандартных сценариев. Кроме того, он разработан toobe расширяемые. Hello [SDK веб-задания — открытым исходным кодом](https://github.com/Azure/azure-webjobs-sdk/)и [репозитория открытым исходным кодом для расширений](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Hello веб-заданий SDK включает hello следующие компоненты:

* **Пакеты NuGet**. Пакеты NuGet, добавленный tooa проект консольного приложения Visual Studio предоставляют платформу, которая использует кода с помощью оформления методов с атрибутами SDK веб-заданий.
* **Панель мониторинга**. Часть hello SDK веб-задания включается в службе приложений Azure и предоставляет широкие возможности мониторинга и диагностики для программ, использующих пакеты NuGet hello. У вас нет кода toouse toowrite эти возможности наблюдения и диагностики.

## <a id="scenarios"></a>Сценарии
Ниже приведены некоторые стандартные сценарии, которые может обслуживать проще с hello Azure SDK веб-заданий.

* Обработка изображений или другая нагружающая ЦП задача. Это стандартная функция веб-сайтов — hello возможность tooupload изображения или видео. Часто требуется toomanipulate hello содержимое после отправки, но вы не хотите toomake hello пользователя ожидания при выполнении этой операции.
* Обработка очередей. В большинстве случаев для web toocommunicate переднего плана, с помощью серверной службы возникает toouse очереди. Необходимости tooget работа, выполненная hello веб-сайта он помещает сообщения в очереди. Серверная служба извлекает сообщения из очереди hello и рабочих "hello". Можно использовать очереди для обработки изображений: например, после hello пользователь отправляет на сервер несколько файлов, поместите приветствия имен файлов в toobe очереди сообщений, заберет hello серверной части для обработки. Или можно использовать очереди tooimprove сайта отклика. Например вместо записи непосредственно tooa базы данных SQL, записи tooa очереди, сообщите hello пользователя, завершения работы и позволить hello серверной службы дескриптор большой задержкой реляционной базы данных работает. Пример очереди обработка с помощью образа см. в разделе hello [приступить к работе веб-заданий SDK учебника](websites-dotnet-webjobs-sdk-get-started.md).
* Объединение RSS-каналов. Если имеется сайт, который ведет список RSS-каналов, можно запросить во всех статьях hello из каналов hello в фоновом процессе.
* Обработка файлов, например, объединение или очистка файлов журнала.  Возможно, файлы журнала, который создается с несколькими узлами или для отдельного промежутками времени, в которых требуется toocombine в порядок задания анализа toorun на них. Или может потребоваться tooschedule еженедельно tooclean задачи toorun старых файлов журнала.
* Ввод данных в таблицы Azure. Может иметь файлы, хранящиеся и больших двоичных объектов и хотите tooparse их и хранить данные hello в таблицах. функция входящих сообщений Hello удалось записи большого количества строк (в некоторых случаях нескольких миллионов) и hello SDK веб-заданий упрощает возможных tooimplement эта функциональность легко. Hello SDK также предоставляет мониторинг индикаторы выполнения, например hello число строк, записанных в таблице hello в реальном времени.
* Других длительно выполняемых задач необходимо toorun в фоновом потоке, например [отправки сообщений электронной почты](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* Все задачи, которые должны toorun по расписанию, например выполнение операции резервного копирования каждую ночь.

Во многих из этих сценариев можно tooscale toorun приложения web на нескольких виртуальных машин, которые будут выполняться одновременно несколько веб-заданий. В некоторых случаях это может привести к hello же начало обработки данных несколько раз, но это не вызывает проблем при использовании встроенных очереди hello, BLOB-объекта и триггеры Service Bus для hello SDK веб-заданий. Hello SDK гарантирует, что функций будет обрабатываться только один раз для каждого сообщения или большого двоичного объекта.

Hello SDK веб-заданий также позволяет легко toohandle распространенные сценарии обработки ошибок. Можно выполнить настройку оповещений toosend уведомлений при сбое функции, а также можно задать время ожидания, чтобы функция отменяется автоматически, если она не была завершена в течение заданного времени.

## <a id="code"></a> Примеры кода
Hello код для обработки типичных задач, которые работают со службой хранилища Azure является простым. В приложении консоли `Main` метод создания `JobHost` toomethods написании вызывает объект, который координирует hello. Hello framework SDK веб-заданий знает при toocall свои методы и какие значения параметров toouse с учетом hello SDK веб-задания атрибутов можно использовать в них. Hello пакет SDK предоставляет *триггеры* , в которых указывается условий возникновения вызове toobe функции hello и *связыватели* , в которых указывается как tooget сведения в действие и из параметров метода.

Например, hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) атрибут вызывает функцию toobe, вызывается при получении сообщения в очередь и если сообщение hello в формате JSON для массива байтов или пользовательский тип, требуется автоматически десериализовать сообщение hello. Hello [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) атрибут запускает процесс, при создании нового большого двоичного объекта в учетной записи хранилища Azure.

Здесь приводится пример программы, которая опрашивает очередь и для каждого полученного от очереди сообщения создает BLOB-объект.

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

Hello `JobHost` объект-контейнер для набора функций в фоновом режиме. Hello `JobHost` мониторы hello объекта функции, следит за событиями, которые вызывают их и выполняет функции hello при возникновении событий триггера. Можно вызвать `JobHost` tooindicate метод, следует ли использовать toorun процесс контейнера hello на hello текущего потока или в фоновом потоке. В примере hello hello `RunAndBlock` метод выполняет процесс hello постоянно hello текущем потоке.

Поскольку hello `ProcessQueueMessage` метод в этом примере имеет `QueueTrigger` атрибута hello триггер для этой функции является hello приема сообщения в очереди. Hello `JobHost` объект следит за новые сообщения очереди в указанной очереди hello («webjobsqueue» в этом образце), и если он найден, он вызывает `ProcessQueueMessage`. 

Hello `QueueTrigger` атрибут привязывает hello `inputText` toohello значение параметра из очереди сообщение hello. И hello `Blob` атрибут привязывает `TextWriter` tooa объект BLOB-объект с именем «blobname» в контейнер с именем «имя_контейнера».  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

функции Hello затем использует эти параметры toowrite hello значения большого двоичного объекта toohello сообщение hello очереди:

        writer.WriteLine(inputText);

Hello триггера и привязки функции hello SDK веб-задания значительно упростить кода hello, у вас есть toowrite. Здравствуйте очереди tooprocess низкоуровневые код, необходимый, BLOB-объектов или файлов или tooinitiate запланированные задачи, можно сделать для вас, hello framework SDK веб-заданий. Например hello платформа создает очередей, которые еще не существует, откроется hello очереди, операций чтения очередь сообщений, удаляет очередь сообщений, когда обработку завершения, создает контейнеры больших двоичных объектов, которые не существуют, но, записывает tooblobs и т. д.

Hello примере кода показаны различные варианты триггеров в одной веб-задания: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, и `ErrorTrigger`. 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a> Планирование
Hello `TimerTrigger` атрибут дает hello toorun функции tootrigger возможности по расписанию. Вы можете запланировать веб-задания через Azure или расписание отдельных функций веб-задание с помощью hello SDK веб-задания `TimerTrigger`. Ниже приведен пример кода.

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

Несколько примеров кода в разделе [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) в хранилище azure веб-задания — пакет sdk расширения hello на GitHub.com.

## <a name="extensibility"></a>Расширяемость
Вы не ограничены в toobuilt функциональность--hello SDK веб-заданий позволяет toowrite настраиваемых триггеров и привязки.  Например, можно написать триггеры событий кэша и периодического расписания. [Репозитория с открытым исходным кодом](https://github.com/Azure/azure-webjobs-sdk-extensions) содержит [подробное руководство на SDK веб-заданий расширяемости](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) и образец кода toohelp приступить к работе написанием собственных триггеров и привязки.

## <a id="workerrole"></a>С помощью пакета SDK веб-задания вне веб-заданий hello
Программа, использующая hello hello пакет SDK веб-заданий для стандартного приложения консоли и можно запускать где угодно — это не обязательно toorun как веб-задания. Программа hello можно протестировать локально на компьютере разработчика и в рабочей среде, при желании этих средах могут выполняться в рабочей роли облачной службы или службы Windows. 

Однако панель мониторинга hello доступна только как расширение для веб-приложение службы приложений Azure. Toorun вне веб-задания и по-прежнему использовать hello панели мониторинга, можно настроить веб-узел toouse приложения hello учетную запись хранения ссылается мониторинга SDK веб-задания строки подключения, что панель мониторинга веб-заданий для этого веб-приложения, затем будут отображаться данные о функции выполнение программы, на котором работает где-то еще. Toohello панели мониторинга можно получить с помощью URL-адрес https:// hello*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Дополнительные сведения см. в разделе [получение панели мониторинга для локальной разработки с помощью hello SDK веб-заданий](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), но Обратите внимание, что hello записи блога показано старое имя строки подключения. 

## <a id="nostorage"></a>Функции панели мониторинга
Hello SDK веб-заданий обеспечивает ряд преимуществ, даже если вы не используете пакет SDK веб-заданий триггеры или связыватели:

* Можно вызывать функции из hello панели мониторинга.
* Можно воспроизводить функций hello панели мониторинга.
* Для просмотра журналов в панели мониторинга, связанные toohello hello определенного веб-задания (журналы приложений, написанных с использованием Console.Out, Console.Error, трассировки и т. д.) или связанным вызова определенной функции toohello, которая создала их (журналы, написанные с использованием `TextWriter` Объект, приветствия SDK передает toohello функции в качестве параметра). 

Дополнительные сведения см. в разделе [как toomanually вызова функции](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) и [как toowrite журналы](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Дальнейшие действия
Дополнительные сведения о hello SDK веб-заданий см. в разделе [рекомендуется заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).

Сведения о toohello последние улучшения hello SDK веб-заданий содержатся hello [заметки о выпуске](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

