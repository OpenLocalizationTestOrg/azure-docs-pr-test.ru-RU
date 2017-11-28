---
title: "aaaAzure отладчика моментального снимка аналитики приложений для приложений .NET | Документы Microsoft"
description: "Отладочные моментальные снимки автоматически собираются при порождении исключений в рабочих приложениях .NET"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="8264c-103">Отладочные моментальные снимки для исключений в приложениях .NET</span><span class="sxs-lookup"><span data-stu-id="8264c-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="8264c-104">При возникновении исключения, можно автоматически собирать отладочный моментальный снимок из работающего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8264c-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="8264c-105">снимок Hello отображает состояние hello исходного кода и переменные в hello момент hello исключение создано исключение.</span><span class="sxs-lookup"><span data-stu-id="8264c-105">hello snapshot shows hello state of source code and variables at hello moment hello exception was thrown.</span></span> <span data-ttu-id="8264c-106">Hello отладчик моментальных снимков (Предварительная версия) в [Azure Application Insights](app-insights-overview.md) отслеживает телеметрии исключения из веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8264c-106">hello Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="8264c-107">Собирает моментальные снимки на свои исключения, создающие top, чтобы получить сведения hello необходимы toodiagnose проблем в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8264c-107">It collects snapshots on your top-throwing exceptions so that you have hello information you need toodiagnose issues in production.</span></span> <span data-ttu-id="8264c-108">Включить hello [пакет NuGet сборщика данных моментального снимка](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) в приложении и при необходимости настроить параметры сбора в [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Снимки появятся на [исключения](app-insights-asp-net-exceptions.md) на портале Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-108">Include hello [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

<span data-ttu-id="8264c-109">Можно просмотреть моментальные снимки отладки в стеке вызовов hello портала toosee hello и просматривать переменные в каждом кадре стека вызовов.</span><span class="sxs-lookup"><span data-stu-id="8264c-109">You can view debug snapshots in hello portal toosee hello call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="8264c-110">более широкие возможности отладки для работы с исходным кодом, откройте моментальные снимки с помощью Visual Studio Enterprise 2017 г., tooget [загрузка расширения отладчика моментального снимка hello для Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="8264c-110">tooget a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="8264c-111">Коллекция моментальных снимков доступна для:</span><span class="sxs-lookup"><span data-stu-id="8264c-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="8264c-112">.NET Framework и приложений ASP.NET выполняющихся с помощью .NET Framework 4.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8264c-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="8264c-113">.NET Core 2.0 и приложений ASP.NET Core 2.0 под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="8264c-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="8264c-114">Настройка сбора моментальных снимков для приложений</span><span class="sxs-lookup"><span data-stu-id="8264c-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="8264c-115">[Включите Application Insights в веб-приложении](app-insights-asp-net.md), если вы еще не сделали это.</span><span class="sxs-lookup"><span data-stu-id="8264c-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="8264c-116">Включить hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) пакета NuGet в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="8264c-116">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="8264c-117">Просмотрите параметры по умолчанию hello, hello пакет добавлен слишком[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="8264c-117">Review hello default options that hello package added too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="8264c-118">Моментальные снимки собираются только на исключения, которые выводятся tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="8264c-118">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="8264c-119">В некоторых случаях (например, предыдущие версии платформы .NET hello) может потребоваться слишком[настроить коллекцию исключений](app-insights-asp-net-exceptions.md#exceptions) toosee исключения с моментальными снимками в портале hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-119">In some cases (for example, older versions of hello .NET platform), you might need too[configure exception collection](app-insights-asp-net-exceptions.md#exceptions) toosee exceptions with snapshots in hello portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="8264c-120">Настройка сбора моментальных снимков для приложений ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="8264c-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="8264c-121">[Включите Application Insights в веб-приложении ASP.NET Core](app-insights-asp-net-core.md), если вы еще не сделали это.</span><span class="sxs-lookup"><span data-stu-id="8264c-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="8264c-122">Включить hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) пакета NuGet в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="8264c-122">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="8264c-123">Изменение hello `ConfigureServices` метод в вашем приложении `Startup` класса процессора телеметрии tooadd hello моментального снимка сборщика.</span><span class="sxs-lookup"><span data-stu-id="8264c-123">Modify hello `ConfigureServices` method in your application's `Startup` class tooadd hello Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="8264c-124">Hello кода, который следует добавить зависит от указанной версии hello пакет Microsoft.ApplicationInsights.ASPNETCore NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-124">hello code you should add depends on hello referenced version of hello Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="8264c-125">Для Microsoft.ApplicationInsights.AspNetCore 2.1.0 добавьте:</span><span class="sxs-lookup"><span data-stu-id="8264c-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="8264c-126">Для Microsoft.ApplicationInsights.AspNetCore 2.1.1 добавьте:</span><span class="sxs-lookup"><span data-stu-id="8264c-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="8264c-127">Настройка сбора моментальных снимков для других приложений .NET</span><span class="sxs-lookup"><span data-stu-id="8264c-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="8264c-128">Если приложение уже не инструментированы с помощью Application Insights, начните с [Включение Application Insights и ключ инструментирования hello параметр](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="8264c-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting hello instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="8264c-129">Добавить hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) пакета NuGet в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="8264c-129">Add hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="8264c-130">Моментальные снимки собираются только на исключения, которые выводятся tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="8264c-130">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="8264c-131">Может потребоваться toomodify tooreport вашего кода их.</span><span class="sxs-lookup"><span data-stu-id="8264c-131">You may need toomodify your code tooreport them.</span></span> <span data-ttu-id="8264c-132">код обработки исключений Hello зависит от структуры приложения hello, но пример приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="8264c-132">hello exception handling code depends on hello structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="8264c-133">Предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="8264c-133">Grant permissions</span></span>

<span data-ttu-id="8264c-134">Владельцы hello подписки Azure можно проверить и моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="8264c-134">Owners of hello Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="8264c-135">Другие пользователи должны иметь разрешение предоставленное владельцем.</span><span class="sxs-lookup"><span data-stu-id="8264c-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="8264c-136">toogrant разрешений, назначьте hello `Application Insights Snapshot Debugger` toousers роли, который будет проверять моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="8264c-136">toogrant permission, assign hello `Application Insights Snapshot Debugger` role toousers who will inspect snapshots.</span></span> <span data-ttu-id="8264c-137">Этой роли могут назначаться tooindividual пользователи или группы, ответственные за подписку для hello целевой ресурс Application Insights или его группы ресурсов или подписки.</span><span class="sxs-lookup"><span data-stu-id="8264c-137">This role can be assigned tooindividual users or groups by subscription owners for hello target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="8264c-138">Откройте колонку hello управления доступа (IAM).</span><span class="sxs-lookup"><span data-stu-id="8264c-138">Open hello Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="8264c-139">Щелкните Здравствуйте, "+" Кнопка "Добавить".</span><span class="sxs-lookup"><span data-stu-id="8264c-139">Click hello +Add button.</span></span>
1. <span data-ttu-id="8264c-140">Выберите отладчик моментального снимка аналитики приложения из раскрывающегося списка ролей hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-140">Select Application Insights Snapshot Debugger from hello Roles drop-down list.</span></span>
1. <span data-ttu-id="8264c-141">Поиск и введите имя пользователя tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-141">Search for and enter a name for hello user tooadd.</span></span>
1. <span data-ttu-id="8264c-142">Щелкните hello tooadd кнопки Save hello роли toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="8264c-142">Click hello Save button tooadd hello user toohello role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="8264c-143">Моментальные снимки могут содержать личные и другие конфиденциальные данные в значениях переменных и параметров.</span><span class="sxs-lookup"><span data-stu-id="8264c-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-hello-application-insights-portal"></a><span data-ttu-id="8264c-144">Отладка моментальные снимки на портале Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="8264c-144">Debug snapshots in hello Application Insights portal</span></span>

<span data-ttu-id="8264c-145">Если моментальный снимок доступен для данного исключения или проблемный идентификатор **открыть снимок отладки** кнопка на hello [исключение](app-insights-asp-net-exceptions.md) на портале Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on hello [exception](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

![Кнопка "Open Debug Snapshot" (Открыть отладочный моментальный снимок) для исключения](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="8264c-147">В hello снимок отладки отображается стек вызовов и панель «переменные».</span><span class="sxs-lookup"><span data-stu-id="8264c-147">In hello Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="8264c-148">При выборе кадров вызова hello стека в панели стека вызова hello, можно просматривать локальные переменные и параметры для этой функции вызова в панель «переменные» hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-148">When you select frames of hello call stack in hello call stack pane, you can view local variables and parameters for that function call in hello variables pane.</span></span>

![Представление отладки моментального снимка в портале hello](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="8264c-150">Моментальные снимки могут содержать конфиденциальные сведения и по умолчанию не отображаются.</span><span class="sxs-lookup"><span data-stu-id="8264c-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="8264c-151">моментальные снимки tooview, необходимо иметь hello `Application Insights Snapshot Debugger` tooyou ролью.</span><span class="sxs-lookup"><span data-stu-id="8264c-151">tooview snapshots, you must have hello `Application Insights Snapshot Debugger` role assigned tooyou.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="8264c-152">Отладка моментальных снимков с помощью Visual Studio 2017 Enterprise</span><span class="sxs-lookup"><span data-stu-id="8264c-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="8264c-153">Щелкните hello **загрузить моментальный снимок** toodownload кнопку `.diagsession` файл, который можно открыть в Visual Studio Enterprise 2017 г.</span><span class="sxs-lookup"><span data-stu-id="8264c-153">Click hello **Download Snapshot** button toodownload a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="8264c-154">tooopen hello `.diagsession` файл, сначала необходимо выполнить [загрузить и установить расширения hello отладчика моментальных снимков для Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="8264c-154">tooopen hello `.diagsession` file, you must first [download and install hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="8264c-155">После открытия файла моментального снимка hello, откроется страница отладки минидампа hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8264c-155">After you open hello snapshot file, hello Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="8264c-156">Нажмите кнопку **отладки управляемого кода** toostart отладки hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="8264c-156">Click **Debug Managed Code** toostart debugging hello snapshot.</span></span> <span data-ttu-id="8264c-157">моментальный снимок Hello открывает toohello строку кода, где hello возникло исключение, чтобы выполнить отладку hello текущему состоянию процесса hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-157">hello snapshot opens toohello line of code where hello exception was thrown so that you can debug hello current state of hello process.</span></span>

    ![Просмотр отладочного моментального снимка в Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="8264c-159">загруженный моментальный снимок Hello содержит все файлы символов, которые найдены на сервер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8264c-159">hello downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="8264c-160">Эти файлы символов, необходимых tooassociate данных моментального снимка с исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="8264c-160">These symbol files are required tooassociate snapshot data with source code.</span></span> <span data-ttu-id="8264c-161">Для приложений служб приложений легко и убедиться, что развертывание символ tooenable при публикации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8264c-161">For App Service apps, make sure tooenable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="8264c-162">Как работают моментальные снимки</span><span class="sxs-lookup"><span data-stu-id="8264c-162">How snapshots work</span></span>

<span data-ttu-id="8264c-163">При запуске приложения создается отдельный процесс передачи моментальных снимков, отслеживающий запросы на создание моментальных снимков для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="8264c-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="8264c-164">При запросе моментального снимка около 10 минут too20 теневая копия выполнения процесса hello производится.</span><span class="sxs-lookup"><span data-stu-id="8264c-164">When a snapshot is requested, a shadow copy of hello running process is made in about 10 too20 minutes.</span></span> <span data-ttu-id="8264c-165">процесс теневого Hello затем анализируется и моментальный снимок создается прерывая toorun основной процесс hello и обслуживать toousers трафика.</span><span class="sxs-lookup"><span data-stu-id="8264c-165">hello shadow process is then analyzed, and a snapshot is created while hello main process continues toorun and serve traffic toousers.</span></span> <span data-ttu-id="8264c-166">Hello моментального снимка является то отправленного tooApplication аналитики вместе с любой соответствующих символов (.pdb) файлы, необходимые tooview hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="8264c-166">hello snapshot is then uploaded tooApplication Insights along with any relevant symbol (.pdb) files that are needed tooview hello snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="8264c-167">Текущие ограничения</span><span class="sxs-lookup"><span data-stu-id="8264c-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="8264c-168">Публикация символов</span><span class="sxs-lookup"><span data-stu-id="8264c-168">Publish symbols</span></span>
<span data-ttu-id="8264c-169">Hello отладчик моментальных снимков требуются файлы символов на hello рабочей toodecode переменные сервера и tooprovide возможности отладки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8264c-169">hello Snapshot Debugger requires symbol files on hello production server toodecode variables and tooprovide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="8264c-170">символы для сборки выпуска публикует Hello 15,2 выпуска Visual Studio 2017 г. по умолчанию при публикации tooApp службы.</span><span class="sxs-lookup"><span data-stu-id="8264c-170">hello 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes tooApp Service.</span></span> <span data-ttu-id="8264c-171">В предыдущих версиях требуются следующие hello tooadd профиль публикации tooyour строки `.pubxml` так, чтобы символы публикуются в режиме выпуска:</span><span class="sxs-lookup"><span data-stu-id="8264c-171">In prior versions, you need tooadd hello following line tooyour publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="8264c-172">Для вычисления Azure и других типов, убедитесь, что файлы символов hello в hello папке .dll основного приложения hello (как правило, `wwwroot/bin`) и доступные в текущем пути hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-172">For Azure Compute and other types, ensure that hello symbol files are in hello same folder of hello main application .dll (typically, `wwwroot/bin`) or are available on hello current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="8264c-173">Оптимизированные сборки</span><span class="sxs-lookup"><span data-stu-id="8264c-173">Optimized builds</span></span>
<span data-ttu-id="8264c-174">В некоторых случаях нельзя просмотреть локальные переменные в сборках выпуска из-за оптимизации, которые применяются во время сборки hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during hello build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8264c-175">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="8264c-175">Troubleshooting</span></span>

<span data-ttu-id="8264c-176">Эти советы помочь при устранении проблем с hello отладчик моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="8264c-176">These tips help you troubleshoot problems with hello Snapshot Debugger.</span></span>

### <a name="verify-hello-instrumentation-key"></a><span data-ttu-id="8264c-177">Проверьте ключ инструментирования hello</span><span class="sxs-lookup"><span data-stu-id="8264c-177">Verify hello instrumentation key</span></span>

<span data-ttu-id="8264c-178">Убедитесь, что вы используете ключ правильный инструментирования hello опубликованного приложения.</span><span class="sxs-lookup"><span data-stu-id="8264c-178">Make sure that you're using hello correct instrumentation key in your published application.</span></span> <span data-ttu-id="8264c-179">Как правило Application Insights считывает hello ключ инструментирования из файла ApplicationInsights.config hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-179">Usually, Application Insights reads hello instrumentation key from hello ApplicationInsights.config file.</span></span> <span data-ttu-id="8264c-180">Убедитесь, что значение hello hello таким же как ключ инструментирования hello для ресурса Application Insights hello, который представлен в портал hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-180">Verify that hello value is hello same as hello instrumentation key for hello Application Insights resource that you see in hello portal.</span></span>

### <a name="check-hello-uploader-logs"></a><span data-ttu-id="8264c-181">Проверьте журналы средства отправки hello</span><span class="sxs-lookup"><span data-stu-id="8264c-181">Check hello uploader logs</span></span>

<span data-ttu-id="8264c-182">После создания моментального снимка на диске создается файл минидампа (.dmp).</span><span class="sxs-lookup"><span data-stu-id="8264c-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="8264c-183">Процесс передачи отдельных принимает этот файл минидампа и передает его, а также любые связанные PDB-файлы tooApplication отладчик моментального снимка аналитики хранилища.</span><span class="sxs-lookup"><span data-stu-id="8264c-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, tooApplication Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="8264c-184">После успешной загрузки минидампа hello удаляется с диска.</span><span class="sxs-lookup"><span data-stu-id="8264c-184">After hello minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="8264c-185">файлы журнала Hello для передачи минидампа hello сохраняются на диске.</span><span class="sxs-lookup"><span data-stu-id="8264c-185">hello log files for hello minidump uploader are retained on disk.</span></span> <span data-ttu-id="8264c-186">В среде службы приложений эти журналы можно найти в `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="8264c-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="8264c-187">Kudu управления использовать hello сайт для служб приложений toofind файлов журналов.</span><span class="sxs-lookup"><span data-stu-id="8264c-187">Use hello Kudu management site for App Service toofind these log files.</span></span>

1. <span data-ttu-id="8264c-188">Откройте приложение службы приложений в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8264c-188">Open your App Service application in hello Azure portal.</span></span>

2. <span data-ttu-id="8264c-189">Выберите hello **дополнительные средства** колонке или выполните поиск **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="8264c-189">Select hello **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="8264c-190">Щелкните **Переход**.</span><span class="sxs-lookup"><span data-stu-id="8264c-190">Click **Go**.</span></span>
4. <span data-ttu-id="8264c-191">В hello **консоли отладки** раскрывающегося списка и выберите **CMD**.</span><span class="sxs-lookup"><span data-stu-id="8264c-191">In hello **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="8264c-192">Щелкните **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="8264c-192">Click **LogFiles**.</span></span>

<span data-ttu-id="8264c-193">Вы увидите хотя бы один файл с именем, начинающимся с `Uploader_` и расширением `.log`.</span><span class="sxs-lookup"><span data-stu-id="8264c-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="8264c-194">Щелкните соответствующий значок toodownload hello все файлы журналов, или открыть их в браузере.</span><span class="sxs-lookup"><span data-stu-id="8264c-194">Click hello appropriate icon toodownload any log files or open them in a browser.</span></span>
<span data-ttu-id="8264c-195">Имя файла Hello включает имя машины hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-195">hello file name includes hello machine name.</span></span> <span data-ttu-id="8264c-196">Если экземпляр службы приложений размещен на нескольких компьютерах, для каждого компьютера существуют отдельные файлы журналов.</span><span class="sxs-lookup"><span data-stu-id="8264c-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="8264c-197">Когда средства отправки hello обнаруживает новый файл минидампа, она заносится в файл журнала hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-197">When hello uploader detects a new minidump file, it is recorded in hello log file.</span></span> <span data-ttu-id="8264c-198">Ниже приведен пример успешной отправки:</span><span class="sxs-lookup"><span data-stu-id="8264c-198">Here's an example of a successful upload:</span></span>

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

<span data-ttu-id="8264c-199">В предыдущем примере hello является ключ инструментирования hello `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="8264c-199">In hello previous example, hello instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="8264c-200">Это значение должно соответствовать hello ключ инструментирования для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="8264c-200">This value should match hello instrumentation key for your application.</span></span>
<span data-ttu-id="8264c-201">Hello минидампа связан с помощью моментального снимка с Идентификатором hello `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="8264c-201">hello minidump is associated with a snapshot with hello ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="8264c-202">Вы можете использовать этот идентификатор более поздней версии toolocate hello связанные данные телеметрии исключения из приложения аналитика Analytics.</span><span class="sxs-lookup"><span data-stu-id="8264c-202">You can use this ID later toolocate hello associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="8264c-203">средства отправки Hello проверяет наличие новых PDB-файлы примерно один раз каждые 15 минут.</span><span class="sxs-lookup"><span data-stu-id="8264c-203">hello uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="8264c-204">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="8264c-204">Here's an example:</span></span>

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

<span data-ttu-id="8264c-205">Для приложений, которые являются _не_ размещенных в службе приложений hello средства отправки записываются hello же папке, что мини-дампов hello: `%TEMP%\Dumps\<ikey>` (где `<ikey>` ваш ключ инструментирования).</span><span class="sxs-lookup"><span data-stu-id="8264c-205">For applications that are _not_ hosted in App Service, hello uploader logs are in hello same folder as hello minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a><span data-ttu-id="8264c-206">Используйте Application Insights поиска toofind исключения с помощью моментальных снимков</span><span class="sxs-lookup"><span data-stu-id="8264c-206">Use Application Insights search toofind exceptions with snapshots</span></span>

<span data-ttu-id="8264c-207">При создании моментального снимка hello исключения обозначен цифрой идентификатора моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="8264c-207">When a snapshot is created, hello throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="8264c-208">Когда телеметрии исключения hello обнаруженную tooApplication аналитики, этот идентификатор моментального снимка включается в качестве пользовательского свойства.</span><span class="sxs-lookup"><span data-stu-id="8264c-208">When hello exception telemetry is reported tooApplication Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="8264c-209">С помощью поиска колонке hello в Application Insights, можно найти все данные телеметрии с hello `ai.snapshot.id` пользовательское свойство.</span><span class="sxs-lookup"><span data-stu-id="8264c-209">Using hello Search blade in Application Insights, you can find all telemetry with hello `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="8264c-210">Обзор tooyour ресурс Application Insights в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8264c-210">Browse tooyour Application Insights resource in hello Azure portal.</span></span>
2. <span data-ttu-id="8264c-211">Щелкните **Search**(Поиск).</span><span class="sxs-lookup"><span data-stu-id="8264c-211">Click **Search**.</span></span>
3. <span data-ttu-id="8264c-212">Тип `ai.snapshot.id` в hello текстовое поле поиска и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="8264c-212">Type `ai.snapshot.id` in hello Search text box and press Enter.</span></span>

![Поиск телеметрии с идентификатор снимка в портале hello](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="8264c-214">Если этот поиск не дал результатов, без моментальных снимков были обнаруженную tooApplication аналитики для приложения hello выбранного диапазона времени.</span><span class="sxs-lookup"><span data-stu-id="8264c-214">If this search returns no results, then no snapshots were reported tooApplication Insights for your application in hello selected time range.</span></span>

<span data-ttu-id="8264c-215">toosearch для идентификатора конкретного моментального снимка из журналов средства отправки hello, введите этот идентификатор в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-215">toosearch for a specific snapshot ID from hello Uploader logs, type that ID in hello Search box.</span></span> <span data-ttu-id="8264c-216">Если не удается найти данные телеметрии для моментального снимка, который был отправлен, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8264c-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="8264c-217">Проверьте, что вы рассматриваете возможность hello ресурса Application Insights, проверяя ключ инструментирования hello.</span><span class="sxs-lookup"><span data-stu-id="8264c-217">Double-check that you're looking at hello right Application Insights resource by verifying hello instrumentation key.</span></span>

2. <span data-ttu-id="8264c-218">С помощью hello меткам hello средства отправки журнала, настройте этот диапазон фильтр поиска toocover hello hello диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="8264c-218">Using hello timestamp from hello Uploader log, adjust hello Time Range filter of hello search toocover that time range.</span></span>

<span data-ttu-id="8264c-219">Если исключение с таким Идентификатором моментальных снимков по-прежнему отсутствует, телеметрии исключения hello не обнаруженную tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="8264c-219">If you still don't see an exception with that snapshot ID, then hello exception telemetry wasn't reported tooApplication Insights.</span></span> <span data-ttu-id="8264c-220">Это происходит в случае сбоя приложения после потребовалось hello моментального снимка, но прежде чем они отчет hello телеметрии исключений.</span><span class="sxs-lookup"><span data-stu-id="8264c-220">This situation can happen if your application crashed after it took hello snapshot but before it reported hello exception telemetry.</span></span> <span data-ttu-id="8264c-221">В этом случае проверьте hello, приложение будет зарегистрировано в `Diagnose and solve problems` toosee, если возникли непредвиденные перезагрузки или необработанные исключения.</span><span class="sxs-lookup"><span data-stu-id="8264c-221">In this case, check hello App Service logs under `Diagnose and solve problems` toosee if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8264c-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8264c-222">Next steps</span></span>

* <span data-ttu-id="8264c-223">[Установить в коде snappoints](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget моментальные снимки, не дожидаясь исключение.</span><span class="sxs-lookup"><span data-stu-id="8264c-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="8264c-224">[Диагностика исключения в веб-приложения](app-insights-asp-net-exceptions.md) объясняет, как toomake дополнительные исключения видимым tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="8264c-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how toomake more exceptions visible tooApplication Insights.</span></span> 
* <span data-ttu-id="8264c-225">В статье [Интеллектуальное обнаружение в Application Insights](app-insights-proactive-diagnostics.md) описывается автоматическое обнаружение аномалий производительности.</span><span class="sxs-lookup"><span data-stu-id="8264c-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
