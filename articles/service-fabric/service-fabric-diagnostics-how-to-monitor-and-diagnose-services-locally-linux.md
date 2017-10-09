---
title: "aaaDebug микрослужбами Azure в Linux | Документы Microsoft"
description: "Узнайте, как toomonitor и диагностики вашей службы, написанные с помощью Microsoft Azure Service Fabric на локальном компьютере разработчика."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="812af-103">Мониторинг и диагностика состояния служб в локальной среде разработки</span><span class="sxs-lookup"><span data-stu-id="812af-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="812af-104">Windows</span><span class="sxs-lookup"><span data-stu-id="812af-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="812af-105">Linux</span><span class="sxs-lookup"><span data-stu-id="812af-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="812af-106">Мониторинг, обнаружение, диагностика и устранение неполадок позволяют toocontinue служб с минимальными нарушениями toohello пользователями.</span><span class="sxs-lookup"><span data-stu-id="812af-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="812af-107">Мониторинг и диагностика критически важны в фактически развернутой рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="812af-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="812af-108">Внедрение аналогичной модели во время разработки служб гарантирует, что диагностики конвейера hello работает при перемещении tooa рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="812af-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="812af-109">Service Fabric упрощает диагностику tooimplement разработчики службы, можно легко работайте с одним компьютером локальная разработка настройки и настройки кластера реальных рабочих.</span><span class="sxs-lookup"><span data-stu-id="812af-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="812af-110">Отладка приложений Java в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="812af-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="812af-111">Для приложений Java доступно [несколько платформ ведения журналов](http://en.wikipedia.org/wiki/Java_logging_framework) .</span><span class="sxs-lookup"><span data-stu-id="812af-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="812af-112">Поскольку `java.util.logging` является параметром по умолчанию hello с hello JRE также используется для hello [примеров кода в github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="812af-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="812af-113">Hello следующее обсуждение объясняется, как tooconfigure hello `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="812af-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="812af-114">С помощью java.util.logging, вы можете перенаправлять приложения журналы toomemory, выходных потоков, файлов консоли или сокетов.</span><span class="sxs-lookup"><span data-stu-id="812af-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="812af-115">Для каждого из этих параметров существуют обработчики по умолчанию уже содержится в hello framework.</span><span class="sxs-lookup"><span data-stu-id="812af-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="812af-116">Можно создать `app.properties` обработчика файлов tooconfigure hello файла для вашего приложения tooredirect все журналы tooa локального файла.</span><span class="sxs-lookup"><span data-stu-id="812af-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="812af-117">Следующий фрагмент кода Hello содержит пример конфигурации:</span><span class="sxs-lookup"><span data-stu-id="812af-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="812af-118">hello указывает tooby папку Hello `app.properties` файл должен существовать.</span><span class="sxs-lookup"><span data-stu-id="812af-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="812af-119">После hello `app.properties` создается файл, вы должны tooalso изменить сценарий точки входа, `entrypoint.sh` в hello `<applicationfolder>/<servicePkg>/Code/` свойство hello папки tooset `java.util.logging.config.file` слишком`app.propertes` файла.</span><span class="sxs-lookup"><span data-stu-id="812af-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="812af-120">запись Hello должно иметь вид hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="812af-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="812af-121">В результате применения этой конфигурации журналы будут циклически собираться в папку `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="812af-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="812af-122">файл журнала Hello в этом случае называется mysfapp%u.%g.log где:</span><span class="sxs-lookup"><span data-stu-id="812af-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="812af-123">**%u** — уникальный номер tooresolve конфликтов между параллельных процессов Java.</span><span class="sxs-lookup"><span data-stu-id="812af-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="812af-124">**%g** — toodistinguish номер поколения hello между поворот журналы.</span><span class="sxs-lookup"><span data-stu-id="812af-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="812af-125">По умолчанию, если обработчик не настроена явным образом, регистрируется обработчик консоли hello.</span><span class="sxs-lookup"><span data-stu-id="812af-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="812af-126">Просмотреть журналы hello в системном журнале в разделе /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="812af-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="812af-127">Дополнительные сведения см. в разделе hello [примеров кода в github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="812af-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="812af-128">Отладка приложений C# в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="812af-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="812af-129">Для трассировки приложений CoreCLR на платформе Linux доступно несколько платформ.</span><span class="sxs-lookup"><span data-stu-id="812af-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="812af-130">Дополнительные сведения см. в разделе о [ведении журналов](http:/github.com/aspnet/logging) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="812af-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="812af-131">Так как разработчики знакомы tooC # EventSource "в этой статье используется EventSource для трассировки CoreCLR выборок в Linux.</span><span class="sxs-lookup"><span data-stu-id="812af-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="812af-132">Hello первым делом tooinclude System.Diagnostics.Tracing, чтобы можно было написать вашей toomemory журналы, выходные потоки или файлы консоли.</span><span class="sxs-lookup"><span data-stu-id="812af-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="812af-133">Для ведения журнала с помощью EventSource, добавьте следующий проект tooyour project.json hello:</span><span class="sxs-lookup"><span data-stu-id="812af-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="812af-134">Можно использовать настраиваемые toolisten EventListener для события службы hello и затем соответствующим образом перенаправит их tootrace файлы.</span><span class="sxs-lookup"><span data-stu-id="812af-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="812af-135">Hello следующий фрагмент кода показывает пример реализации ведения журналов с помощью EventSource и пользовательские EventListener:</span><span class="sxs-lookup"><span data-stu-id="812af-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need tooadd method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


<span data-ttu-id="812af-136">Hello предыдущем фрагменте выводит файл tooa журналы hello в `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="812af-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="812af-137">Это имя файла должно toobe соответствующим образом обновлены.</span><span class="sxs-lookup"><span data-stu-id="812af-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="812af-138">В случае, если требуется, чтобы журналы tooconsole tooredirect hello, используйте следующий фрагмент кода в классе настраиваемого EventListener hello:</span><span class="sxs-lookup"><span data-stu-id="812af-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="812af-139">Здравствуйте, образцов [примеры C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) использовать EventSource и пользовательский файл tooa события toolog EventListener.</span><span class="sxs-lookup"><span data-stu-id="812af-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="812af-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="812af-140">Next steps</span></span>
<span data-ttu-id="812af-141">Здравствуйте добавлены же код трассировки приложения tooyour также работает с hello диагностики приложения на кластере Azure.</span><span class="sxs-lookup"><span data-stu-id="812af-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="812af-142">Извлечение этих статей, которые рассматриваются различные варианты hello hello средств и описаны как tooset их вверх.</span><span class="sxs-lookup"><span data-stu-id="812af-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="812af-143">Каким образом toocollect ведет журнал диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="812af-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
