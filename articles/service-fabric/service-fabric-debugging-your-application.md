---
title: "aaaDebug приложения в Visual Studio | Документы Microsoft"
description: "Улучшить hello надежность и производительность служб по разработке и отладке их в кластере локальной разработки в Visual Studio."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="a6f81-103">Отладка приложения Service Fabric с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6f81-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6f81-104">Visual Studio и CSharp</span><span class="sxs-lookup"><span data-stu-id="a6f81-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="a6f81-105">Eclipse и Java</span><span class="sxs-lookup"><span data-stu-id="a6f81-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="a6f81-106">Отладка локального приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a6f81-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="a6f81-107">Вы можете сэкономить время и деньги, развернув приложение Azure Service Fabric и выполнив его отладку в кластере для разработки, состоящем из локальных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="a6f81-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="a6f81-108">Visual Studio 2017 г. или Visual Studio 2015 можно развернуть локальный кластер hello приложения toohello и автоматически подключить hello отладчик tooall экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="a6f81-108">Visual Studio 2017 or Visual Studio 2015 can deploy hello application toohello local cluster and automatically connect hello debugger tooall instances of your application.</span></span>

1. <span data-ttu-id="a6f81-109">Запуск разработки локального кластера с помощью инструкции hello в [Настройка среды разработки Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a6f81-109">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="a6f81-110">Нажмите клавишу **F5** или выберите в меню **Отладка** > **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="a6f81-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Запуск отладки приложения][startdebugging]
3. <span data-ttu-id="a6f81-112">Установите точки останова в коде и пошаговое выполнение приложения hello, выбирая команды в hello **отладки** меню.</span><span class="sxs-lookup"><span data-stu-id="a6f81-112">Set breakpoints in your code and step through hello application by clicking commands in hello **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a6f81-113">Visual Studio подключает tooall экземпляры приложения.</span><span class="sxs-lookup"><span data-stu-id="a6f81-113">Visual Studio attaches tooall instances of your application.</span></span> <span data-ttu-id="a6f81-114">При пошаговом выполнении кода разные процессы могут одновременно достигать точек останова. Это приводит к возникновению параллельных сеансов.</span><span class="sxs-lookup"><span data-stu-id="a6f81-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="a6f81-115">Попробуйте отключить hello точки останова после их работе, сделав условного на идентификатор потока hello каждой точке останова или с помощью событий диагностики.</span><span class="sxs-lookup"><span data-stu-id="a6f81-115">Try disabling hello breakpoints after they're hit, by making each breakpoint conditional on hello thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="a6f81-116">Hello **события диагностики** автоматически будет открыто окно, чтобы можно было просматривать диагностические события в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="a6f81-116">hello **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Просмотр событий диагностики в режиме реального времени][diagnosticevents]
5. <span data-ttu-id="a6f81-118">Можно также открыть hello **события диагностики** окна в Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="a6f81-118">You can also open hello **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="a6f81-119">В разделе **Service Fabric** щелкните любой узел правой кнопкой мыши и выберите пункт **Показать потоковую передачу трассировок**.</span><span class="sxs-lookup"><span data-stu-id="a6f81-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Привет открыть окно событий диагностики][viewdiagnosticevents]
   
    <span data-ttu-id="a6f81-121">Если требуется toofilter трассировок tooa определенной службы или приложения, просто включите потоковой передачи трассировки во время этой конкретной службы или приложения.</span><span class="sxs-lookup"><span data-stu-id="a6f81-121">If you want toofilter your traces tooa specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="a6f81-122">события диагностики Hello можно увидеть в hello автоматически создается **ServiceEventSource.cs** файла и вызова из кода приложения.</span><span class="sxs-lookup"><span data-stu-id="a6f81-122">hello diagnostic events can be seen in hello automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="a6f81-123">Hello **события диагностики** окно поддерживает фильтрацию, приостановка и проверка события в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="a6f81-123">hello **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="a6f81-124">Фильтр Hello — простой поиск строки сообщения hello события, включая его содержимое.</span><span class="sxs-lookup"><span data-stu-id="a6f81-124">hello filter is a simple string search of hello event message, including its contents.</span></span>
   
    ![Фильтрация, приостановка, возобновление и проверка событий в реальном времени][diagnosticeventsactions]
8. <span data-ttu-id="a6f81-126">Отладка служб аналогична отладке приложений.</span><span class="sxs-lookup"><span data-stu-id="a6f81-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="a6f81-127">Обычно для простой отладки точки останова задаются в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6f81-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="a6f81-128">Несмотря на то, что надежные коллекции реплицируются на нескольких узлах, они все равно реализуют интерфейс IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="a6f81-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="a6f81-129">Это означает, что можно использовать hello Просмотр результатов в Visual Studio во время отладки toosee хранятся внутри.</span><span class="sxs-lookup"><span data-stu-id="a6f81-129">This means that you can use hello Results View in Visual Studio while debugging toosee what you've stored inside.</span></span> <span data-ttu-id="a6f81-130">Просто задайте точку останова в любом месте своего кода.</span><span class="sxs-lookup"><span data-stu-id="a6f81-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Запуск отладки приложения][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="a6f81-132">Отладка удаленного приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a6f81-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="a6f81-133">Если приложения Service Fabric запущены в кластере Service Fabric в Azure,-можно tooremotely отладки их непосредственно из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6f81-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able tooremotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="a6f81-134">функции Hello требуется [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) и [пакет Azure SDK для .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a6f81-134">hello feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="a6f81-135">Удаленная отладка предназначена для сценариев разработки и тестирования и не toobe, используемый в производственной среде, из-за hello влияние на выполнение приложений hello.</span><span class="sxs-lookup"><span data-stu-id="a6f81-135">Remote debugging is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> 
> 

1. <span data-ttu-id="a6f81-136">Перехода кластера tooyour в **Cloud Explorer**, щелкните правой кнопкой мыши и выберите **Включение отладки**</span><span class="sxs-lookup"><span data-stu-id="a6f81-136">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Включение удаленной отладки][enableremotedebugging]
   
    <span data-ttu-id="a6f81-138">Это запускается процесс hello включения hello удаленной отладки расширения на узлы кластера, а также необходимые конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="a6f81-138">This will kick off hello process of enabling hello remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="a6f81-139">Щелкните правой кнопкой мыши узел кластера hello в **Cloud Explorer**и выберите **присоединить отладчик**</span><span class="sxs-lookup"><span data-stu-id="a6f81-139">Right-click hello cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Подключить отладчик][attachdebugger]
3. <span data-ttu-id="a6f81-141">В hello **присоединения tooprocess** диалоговое окно, выберите процесс hello toodebug и нажмите кнопку **присоединения**</span><span class="sxs-lookup"><span data-stu-id="a6f81-141">In hello **Attach tooprocess** dialog, choose hello process you want toodebug, and click **Attach**</span></span>
   
    ![Выбор процесса][chooseprocess]
   
    <span data-ttu-id="a6f81-143">Имя Hello hello процесса нужно tooattach для, равно hello имя службы имя сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="a6f81-143">hello name of hello process you want tooattach to, equals hello name of your service project assembly name.</span></span>
   
    <span data-ttu-id="a6f81-144">узлы tooall hello процесс присоединения отладчика Hello.</span><span class="sxs-lookup"><span data-stu-id="a6f81-144">hello debugger will attach tooall nodes running hello process.</span></span>
   
   * <span data-ttu-id="a6f81-145">В случае hello, где при отладке службы без отслеживания состояния все экземпляры службы hello на всех узлах являются частью сеанса отладки hello.</span><span class="sxs-lookup"><span data-stu-id="a6f81-145">In hello case where you are debugging a stateless service, all instances of hello service on all nodes are part of hello debug session.</span></span>
   * <span data-ttu-id="a6f81-146">При отладке службы с отслеживанием состояния hello только первичная реплика любого раздела будет активна и поэтому перехваченного отладчиком hello.</span><span class="sxs-lookup"><span data-stu-id="a6f81-146">If you are debugging a stateful service, only hello primary replica of any partition will be active and therefore caught by hello debugger.</span></span> <span data-ttu-id="a6f81-147">Если первичная реплика hello перемещается во время сеанса отладки hello, hello обработки этой реплики будет по-прежнему входить hello сеанса отладки.</span><span class="sxs-lookup"><span data-stu-id="a6f81-147">If hello primary replica moves during hello debug session, hello processing of that replica will still be part of hello debug session.</span></span>
   * <span data-ttu-id="a6f81-148">В порядке tooonly catch секций или экземпляров данной службы можно использовать условные точки останова tooonly разрыв определенный раздел или экземпляр.</span><span class="sxs-lookup"><span data-stu-id="a6f81-148">In order tooonly catch relevant partitions or instances of a given service, you can use conditional breakpoints tooonly break a specific partition or instance.</span></span>
     
     ![Условная точка останова][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="a6f81-150">В настоящее время мы не поддерживают отладку кластера Service Fabric с несколькими экземплярами hello же имя исполняемого файла службы.</span><span class="sxs-lookup"><span data-stu-id="a6f81-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of hello same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="a6f81-151">После завершения отладки приложения hello расширение удаленной отладки можно отключить, щелкнув правой кнопкой мыши кластер hello в **Cloud Explorer** и выберите **Запретить отладку**</span><span class="sxs-lookup"><span data-stu-id="a6f81-151">Once you finish debugging your application, you can disable hello remote debugging extension by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Отключение удаленной отладки][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="a6f81-153">Потоковая передача трассировок из удаленного узла кластера</span><span class="sxs-lookup"><span data-stu-id="a6f81-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="a6f81-154">Вы также являются трассировки может toostream непосредственно из удаленного кластера узла tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6f81-154">You are also able toostream traces directly from a remote cluster node tooVisual Studio.</span></span> <span data-ttu-id="a6f81-155">Эта функция позволяет события трассировки ETW toostream, полученных на узле кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a6f81-155">This feature allows you toostream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="a6f81-156">Компоненту требуется [пакет SDK 2.0 для Service Fabric](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) и [пакет SDK Azure для .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a6f81-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="a6f81-157">Эта функция поддерживает только кластеры на платформе Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f81-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="a6f81-158">Потоковая передача трассировок предназначена для сценариев разработки и тестирования и не toobe, используемый в производственной среде, из-за hello влияние на выполнение приложений hello.</span><span class="sxs-lookup"><span data-stu-id="a6f81-158">Streaming traces is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> <span data-ttu-id="a6f81-159">В рабочем сценарии следует применять пересылку событий с помощью средств диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f81-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="a6f81-160">Перехода кластера tooyour в **Cloud Explorer**, щелкните правой кнопкой мыши и выберите **Включение трассировки потоковой передачи**</span><span class="sxs-lookup"><span data-stu-id="a6f81-160">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Включение трассировки удаленной потоковой передачи][enablestreamingtraces]
   
    <span data-ttu-id="a6f81-162">Это запускается процесс hello включения hello потоковой передачи расширение трассировки на узлы кластера, а также необходимые конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="a6f81-162">This will kick off hello process of enabling hello streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="a6f81-163">Разверните hello **узлы** элемент в **Cloud Explorer**, щелкните правой кнопкой мыши узел hello toostream трассировок из и задайте **представление трассировки потоковой передачи**</span><span class="sxs-lookup"><span data-stu-id="a6f81-163">Expand hello **Nodes** element in **Cloud Explorer**, right-click hello node you want toostream traces from and choose **View Streaming Traces**</span></span>
   
    ![Просмотр трассировки удаленной потоковой передачи][viewremotestreamingtraces]
   
    <span data-ttu-id="a6f81-165">Повторите шаг 2 для столько требуется toosee трассировок из узлов.</span><span class="sxs-lookup"><span data-stu-id="a6f81-165">Repeat step 2 for as many nodes as you want toosee traces from.</span></span> <span data-ttu-id="a6f81-166">Потоковая передача каждого узла будет отображаться в отдельном окне.</span><span class="sxs-lookup"><span data-stu-id="a6f81-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="a6f81-167">Теперь вы находитесь может toosee hello трассировки, относящиеся к Service Fabric и служб.</span><span class="sxs-lookup"><span data-stu-id="a6f81-167">You are now able toosee hello traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="a6f81-168">Если вы хотите toofilter hello события tooonly отображение конкретного приложения, просто введите имя hello приложения hello в фильтре hello.</span><span class="sxs-lookup"><span data-stu-id="a6f81-168">If you want toofilter hello events tooonly show a specific application, simply type in hello name of hello application in hello filter.</span></span>
   
    ![Просмотр трассировки потоковой передачи][viewingstreamingtraces]
3. <span data-ttu-id="a6f81-170">После завершения трассировки потоковой передачи из кластера, можно отключить трассировку удаленной потоковой передачи, щелкните правой кнопкой мыши кластер hello в **Cloud Explorer** и выберите **отключить потоковую передачу трассировок**</span><span class="sxs-lookup"><span data-stu-id="a6f81-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Отключение трассировки удаленной потоковой передачи][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="a6f81-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a6f81-172">Next steps</span></span>
* <span data-ttu-id="a6f81-173">[Проверка службы Service Fabric](service-fabric-testability-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a6f81-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="a6f81-174">[Управление приложениями Service Fabric в Visual Studio](service-fabric-manage-application-in-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="a6f81-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
