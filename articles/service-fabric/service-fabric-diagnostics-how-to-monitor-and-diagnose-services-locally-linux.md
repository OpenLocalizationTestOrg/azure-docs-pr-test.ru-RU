---
title: "Отладка микрослужб Azure в Linux | Документация Майкрософт"
description: "Узнайте, как осуществлять мониторинг и диагностику состояния служб с использованием платформы Microsoft Azure Service Fabric на локальном компьютере для разработки."
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
ms.openlocfilehash: 4bc73f581f4855ebc724df19dd56fab8bf103854
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="e4ae8-103">Мониторинг и диагностика состояния служб в локальной среде разработки</span><span class="sxs-lookup"><span data-stu-id="e4ae8-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4ae8-104">Windows</span><span class="sxs-lookup"><span data-stu-id="e4ae8-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="e4ae8-105">Linux</span><span class="sxs-lookup"><span data-stu-id="e4ae8-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="e4ae8-106">Благодаря возможностям мониторинга состояния, а также выявления, диагностики и устранения неполадок службы могут работать практически без перерывов.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="e4ae8-107">Мониторинг и диагностика критически важны в фактически развернутой рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="e4ae8-108">Внедрение аналогичной модели при разработке служб гарантирует работу конвейера диагностики при переходе в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-108">Adopting a similar model during development of services ensures that the diagnostic pipeline works when you move to a production environment.</span></span> <span data-ttu-id="e4ae8-109">Платформа Service Fabric позволяет использовать средства диагностики, которые одинаково хорошо работают как в среде разработки на одном локальном компьютере, так и в условиях реального рабочего кластера.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-109">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="e4ae8-110">Отладка приложений Java в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e4ae8-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="e4ae8-111">Для приложений Java доступно [несколько платформ ведения журналов](http://en.wikipedia.org/wiki/Java_logging_framework) .</span><span class="sxs-lookup"><span data-stu-id="e4ae8-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="e4ae8-112">Так как `java.util.logging` является параметром по умолчанию в среде JRE, он также используется для [примеров кода в GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="e4ae8-112">Since `java.util.logging` is the default option with the JRE, it is also used for the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="e4ae8-113">Далее в этой статье описывается настройка платформы `java.util.logging` .</span><span class="sxs-lookup"><span data-stu-id="e4ae8-113">The following discussion explains how to configure the `java.util.logging` framework.</span></span>

<span data-ttu-id="e4ae8-114">С помощью java.util.logging журналы приложения можно перенаправлять в память, потоки вывода, файлы консоли или сокеты.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-114">Using java.util.logging you can redirect your application logs to memory, output streams, console files, or sockets.</span></span> <span data-ttu-id="e4ae8-115">Для каждого из этих вариантов существуют обработчики по умолчанию, входящие в состав платформы.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-115">For each of these options, there are default handlers already provided in the framework.</span></span> <span data-ttu-id="e4ae8-116">Чтобы настроить обработчик файлов для приложения, который будет перенаправлять все журналы в локальный файл, можно создать файл `app.properties`.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-116">You can create a `app.properties` file to configure the file handler for your application to redirect all logs to a local file.</span></span>

<span data-ttu-id="e4ae8-117">Пример конфигурации приведен в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="e4ae8-117">The following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="e4ae8-118">Файл `app.properties` должен указывать на существующую папку.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-118">The folder pointed to by the `app.properties` file must exist.</span></span> <span data-ttu-id="e4ae8-119">Затем, после создания файла `app.properties`, необходимо также изменить сценарий точки входа `entrypoint.sh` в папке `<applicationfolder>/<servicePkg>/Code/`, указав в качестве значения свойства `java.util.logging.config.file` файл `app.propertes`.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-119">After the `app.properties` file is created, you need to also modify your entry point script, `entrypoint.sh` in the `<applicationfolder>/<servicePkg>/Code/` folder to set the property `java.util.logging.config.file` to `app.propertes` file.</span></span> <span data-ttu-id="e4ae8-120">Запись должна выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="e4ae8-120">The entry should look like the following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path to app.properties> -jar <service name>.jar
```


<span data-ttu-id="e4ae8-121">В результате применения этой конфигурации журналы будут циклически собираться в папку `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="e4ae8-122">В этом случае файл журнала называется mysfapp%u.%g.log, где:</span><span class="sxs-lookup"><span data-stu-id="e4ae8-122">The log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="e4ae8-123">**%u** — это уникальный номер для разрешения конфликтов между параллельными процессами Java.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-123">**%u** is a unique number to resolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="e4ae8-124">**%g** — это номер версии для отличия чередующихся журналов.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-124">**%g** is the generation number to distinguish between rotating logs.</span></span>

<span data-ttu-id="e4ae8-125">Если обработчик не настроен явно, по умолчанию регистрируется обработчик консоли.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-125">By default if no handler is explicitly configured, the console handler is registered.</span></span> <span data-ttu-id="e4ae8-126">Просмотреть журналы в системном журнале можно в папке /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-126">One can view the logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="e4ae8-127">Дополнительные сведения см. на странице с [примерами кода на GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="e4ae8-127">For more information, see the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="e4ae8-128">Отладка приложений C# в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e4ae8-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="e4ae8-129">Для трассировки приложений CoreCLR на платформе Linux доступно несколько платформ.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="e4ae8-130">Дополнительные сведения см. в разделе о [ведении журналов](http:/github.com/aspnet/logging) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="e4ae8-131">Так как EventSource знаком разработчикам на языке C#, в этой статье он используется для трассировки в образцах CoreCLR на Linux.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-131">Since EventSource is familiar to C# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="e4ae8-132">Сначала необходимо добавить System.Diagnostics.Tracing, чтобы иметь возможность записывать журналы в память, выходные потоки или файлы консоли.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-132">The first step is to include System.Diagnostics.Tracing so that you can write your logs to memory, output streams, or console files.</span></span>  <span data-ttu-id="e4ae8-133">Для ведения журналов с помощью EventSource добавьте в project.json следующий проект:</span><span class="sxs-lookup"><span data-stu-id="e4ae8-133">For logging using EventSource, add the following project to your project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="e4ae8-134">Можно использовать пользовательский EventListener, чтобы прослушивать события службы и соответствующим образом перенаправлять их в файлы трассировки.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-134">You can use a custom EventListener to listen for the service event and then appropriately redirect them to trace files.</span></span> <span data-ttu-id="e4ae8-135">В следующем фрагменте кода показан пример реализации ведения журналов с помощью EventSource и пользовательского EventListener.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-135">The following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


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

        // TBD: Need to add method for sample event.

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


<span data-ttu-id="e4ae8-136">Предыдущий фрагмент кода выводит журналы в файл в `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-136">The preceding snippet outputs the logs to a file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="e4ae8-137">Это имя файла должно быть обновлено соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-137">This file name needs to be appropriately updated.</span></span> <span data-ttu-id="e4ae8-138">Если вы хотите перенаправить журналы в консоль, используйте следующий фрагмент кода в классе настраиваемого EventListener:</span><span class="sxs-lookup"><span data-stu-id="e4ae8-138">In case you want to redirect the logs to console, use the following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="e4ae8-139">Образцы на языке C# [в репозитории GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) регистрируют события в файл с помощью EventSource и пользовательского EventListener.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-139">The samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener to log events to a file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e4ae8-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4ae8-140">Next steps</span></span>
<span data-ttu-id="e4ae8-141">Код трассировки, добавленный в приложение, также можно использовать для диагностики приложения в кластере Azure.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-141">The same tracing code added to your application also works with the diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="e4ae8-142">Ознакомьтесь с этими статьями, в которых рассматриваются различные варианты инструментов и описывается, как их настроить.</span><span class="sxs-lookup"><span data-stu-id="e4ae8-142">Check out these articles that discuss the different options for the tools and describe how to set them up.</span></span>
* [<span data-ttu-id="e4ae8-143">Сбор журналов с помощью системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="e4ae8-143">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
