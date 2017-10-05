---
title: "Отладчик моментальных снимков Azure Application Insights для приложений .NET | Документация Майкрософт"
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
ms.openlocfilehash: 56eba2ff7af228b3c44354ad43b384288b4e1972
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="60f0d-103">Отладочные моментальные снимки для исключений в приложениях .NET</span><span class="sxs-lookup"><span data-stu-id="60f0d-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="60f0d-104">При возникновении исключения, можно автоматически собирать отладочный моментальный снимок из работающего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="60f0d-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="60f0d-105">Моментальный снимок отображает состояние исходного кода и переменных в момент порождения этого исключения.</span><span class="sxs-lookup"><span data-stu-id="60f0d-105">The snapshot shows the state of source code and variables at the moment the exception was thrown.</span></span> <span data-ttu-id="60f0d-106">Отладчик моментальных снимков (предварительная версия) в [Azure Application Insights](app-insights-overview.md) отслеживает телеметрию исключений, поступающую из веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="60f0d-106">The Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="60f0d-107">Он собирает моментальные снимки для наиболее частых исключений, чтобы предоставить вам необходимые сведения для диагностики проблем в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="60f0d-107">It collects snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span> <span data-ttu-id="60f0d-108">Добавьте [пакет NuGet сборщика моментальных снимков](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) в приложение и, при необходимости, настройте параметры сбора в файле [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Моментальные снимки для [исключений](app-insights-asp-net-exceptions.md) отображаются на портале Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60f0d-108">Include the [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

<span data-ttu-id="60f0d-109">Вы можете просмотреть отладочные моментальные снимки на портале, чтобы изучить стек вызовов и проверить значения переменных в каждом кадре стека вызовов.</span><span class="sxs-lookup"><span data-stu-id="60f0d-109">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="60f0d-110">Чтобы воспользоваться более мощными средствами отладки исходного кода, откройте моментальные снимки в Visual Studio 2017 Enterprise, [скачав расширение отладчика моментальных снимков для Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="60f0d-110">To get a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="60f0d-111">Коллекция моментальных снимков доступна для:</span><span class="sxs-lookup"><span data-stu-id="60f0d-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="60f0d-112">.NET Framework и приложений ASP.NET выполняющихся с помощью .NET Framework 4.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="60f0d-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="60f0d-113">.NET Core 2.0 и приложений ASP.NET Core 2.0 под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="60f0d-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="60f0d-114">Настройка сбора моментальных снимков для приложений</span><span class="sxs-lookup"><span data-stu-id="60f0d-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="60f0d-115">[Включите Application Insights в веб-приложении](app-insights-asp-net.md), если вы еще не сделали это.</span><span class="sxs-lookup"><span data-stu-id="60f0d-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="60f0d-116">Добавьте в приложение пакет NuGet [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector).</span><span class="sxs-lookup"><span data-stu-id="60f0d-116">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="60f0d-117">Просмотрите параметры по умолчанию, добавленные этим пакетом в файл [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="60f0d-117">Review the default options that the package added to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- The default is true, but you can disable Snapshot Debugging by setting it to false -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this to true. -->
        <!-- DeveloperMode is a property on the active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need to see an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- The maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- The maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often to reset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- The maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- The maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="60f0d-118">Моментальные снимки собираются только для исключений, которые передаются в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60f0d-118">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="60f0d-119">В некоторых случаях (например, в более старых версиях платформы .NET) может потребоваться [настроить сбор исключений](app-insights-asp-net-exceptions.md#exceptions), чтобы просматривать исключения с помощью моментальных снимков, которые отображаются на портале.</span><span class="sxs-lookup"><span data-stu-id="60f0d-119">In some cases (for example, older versions of the .NET platform), you might need to [configure exception collection](app-insights-asp-net-exceptions.md#exceptions) to see exceptions with snapshots in the portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="60f0d-120">Настройка сбора моментальных снимков для приложений ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="60f0d-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="60f0d-121">[Включите Application Insights в веб-приложении ASP.NET Core](app-insights-asp-net-core.md), если вы еще не сделали это.</span><span class="sxs-lookup"><span data-stu-id="60f0d-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="60f0d-122">Добавьте в приложение пакет NuGet [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector).</span><span class="sxs-lookup"><span data-stu-id="60f0d-122">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="60f0d-123">Измените метод `ConfigureServices` в классе `Startup` приложения, чтобы добавить обработчик телеметрии сборщика моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="60f0d-123">Modify the `ConfigureServices` method in your application's `Startup` class to add the Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="60f0d-124">Код, который следует добавить, зависит от указанной версии пакета NuGet Microsoft.ApplicationInsights.ASPNETCore.</span><span class="sxs-lookup"><span data-stu-id="60f0d-124">The code you should add depends on the referenced version of the Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="60f0d-125">Для Microsoft.ApplicationInsights.AspNetCore 2.1.0 добавьте:</span><span class="sxs-lookup"><span data-stu-id="60f0d-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="60f0d-126">Для Microsoft.ApplicationInsights.AspNetCore 2.1.1 добавьте:</span><span class="sxs-lookup"><span data-stu-id="60f0d-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
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

       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="60f0d-127">Настройка сбора моментальных снимков для других приложений .NET</span><span class="sxs-lookup"><span data-stu-id="60f0d-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="60f0d-128">Если приложение еще не инструментировано с помощью Application Insights, начните с [включения Application Insights и установки ключа инструментирования](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="60f0d-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting the instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="60f0d-129">Добавьте в приложение пакет NuGet [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector).</span><span class="sxs-lookup"><span data-stu-id="60f0d-129">Add the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="60f0d-130">Моментальные снимки собираются только для исключений, которые передаются в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60f0d-130">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="60f0d-131">Для их передачи может потребоваться изменить код.</span><span class="sxs-lookup"><span data-stu-id="60f0d-131">You may need to modify your code to report them.</span></span> <span data-ttu-id="60f0d-132">Код обработки исключений зависит от структуры приложения. Пример приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="60f0d-132">The exception handling code depends on the structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle the request.
        }
        catch (Exception ex)
        {
            // Report the exception to Application Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow the exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="60f0d-133">Предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="60f0d-133">Grant permissions</span></span>

<span data-ttu-id="60f0d-134">Владельцы подписок Azure могут проверять моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="60f0d-134">Owners of the Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="60f0d-135">Другие пользователи должны иметь разрешение предоставленное владельцем.</span><span class="sxs-lookup"><span data-stu-id="60f0d-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="60f0d-136">Чтобы предоставить разрешение, назначьте роль `Application Insights Snapshot Debugger` пользователям, которые будут проверять моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="60f0d-136">To grant permission, assign the `Application Insights Snapshot Debugger` role to users who will inspect snapshots.</span></span> <span data-ttu-id="60f0d-137">Владельцы подписок могут назначить эту роль отдельным пользователям или группам для целевого ресурса Application Insights или его группы ресурсов или подписки.</span><span class="sxs-lookup"><span data-stu-id="60f0d-137">This role can be assigned to individual users or groups by subscription owners for the target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="60f0d-138">Откройте колонку "Управление доступом (IAM)".</span><span class="sxs-lookup"><span data-stu-id="60f0d-138">Open the Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="60f0d-139">Нажмите кнопку "+ Добавить".</span><span class="sxs-lookup"><span data-stu-id="60f0d-139">Click the +Add button.</span></span>
1. <span data-ttu-id="60f0d-140">В раскрывающемся списке "Роли" выберите "Отладчик моментальных снимков Application Insights".</span><span class="sxs-lookup"><span data-stu-id="60f0d-140">Select Application Insights Snapshot Debugger from the Roles drop-down list.</span></span>
1. <span data-ttu-id="60f0d-141">Выполните поиск и введите имя пользователя, который будет добавлен.</span><span class="sxs-lookup"><span data-stu-id="60f0d-141">Search for and enter a name for the user to add.</span></span>
1. <span data-ttu-id="60f0d-142">Нажмите кнопку "Сохранить", чтобы добавить пользователя к роли.</span><span class="sxs-lookup"><span data-stu-id="60f0d-142">Click the Save button to add the user to the role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="60f0d-143">Моментальные снимки могут содержать личные и другие конфиденциальные данные в значениях переменных и параметров.</span><span class="sxs-lookup"><span data-stu-id="60f0d-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-the-application-insights-portal"></a><span data-ttu-id="60f0d-144">Отладка моментальных снимков на портале Application Insights</span><span class="sxs-lookup"><span data-stu-id="60f0d-144">Debug snapshots in the Application Insights portal</span></span>

<span data-ttu-id="60f0d-145">Если для заданного исключения или идентификатора проблемы доступен моментальный снимок, то для этого [исключения](app-insights-asp-net-exceptions.md) на портале Application Insights доступна кнопка **Open Debug Snapshot** (Открыть отладочный моментальный снимок).</span><span class="sxs-lookup"><span data-stu-id="60f0d-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on the [exception](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

![Кнопка "Open Debug Snapshot" (Открыть отладочный моментальный снимок) для исключения](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="60f0d-147">В представлении "Debug Snapshot" (Отладочный моментальный снимок) можно увидеть стек вызовов и область переменных.</span><span class="sxs-lookup"><span data-stu-id="60f0d-147">In the Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="60f0d-148">При выборе кадров стека вызовов в области стека вызовов можно просматривать локальные переменные и параметры для этого вызова функции в области переменных.</span><span class="sxs-lookup"><span data-stu-id="60f0d-148">When you select frames of the call stack in the call stack pane, you can view local variables and parameters for that function call in the variables pane.</span></span>

![Просмотр отладочного моментального снимка на портале](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="60f0d-150">Моментальные снимки могут содержать конфиденциальные сведения и по умолчанию не отображаются.</span><span class="sxs-lookup"><span data-stu-id="60f0d-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="60f0d-151">Для просмотра моментальных снимков вам должна быть назначена роль `Application Insights Snapshot Debugger`.</span><span class="sxs-lookup"><span data-stu-id="60f0d-151">To view snapshots, you must have the `Application Insights Snapshot Debugger` role assigned to you.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="60f0d-152">Отладка моментальных снимков с помощью Visual Studio 2017 Enterprise</span><span class="sxs-lookup"><span data-stu-id="60f0d-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="60f0d-153">Нажмите кнопку **Download Snapshot** (Скачать моментальный снимок), чтобы скачать файл с расширением `.diagsession`, который можно открыть в Visual Studio 2017 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="60f0d-153">Click the **Download Snapshot** button to download a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="60f0d-154">Чтобы открыть файл с расширением `.diagsession`, сначала нужно [скачать и установить расширение отладчика моментальных снимков для Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="60f0d-154">To open the `.diagsession` file, you must first [download and install the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="60f0d-155">После открытия файла моментального снимка в Visual Studio появится страница мини-дампа отладки.</span><span class="sxs-lookup"><span data-stu-id="60f0d-155">After you open the snapshot file, the Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="60f0d-156">Щелкните **Debug Managed Code** (Отладить управляемый код), чтобы начать отладку моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="60f0d-156">Click **Debug Managed Code** to start debugging the snapshot.</span></span> <span data-ttu-id="60f0d-157">Откроется строка кода, на которой было порождено исключение, и вы сможете выполнить отладку текущего состояния процесса.</span><span class="sxs-lookup"><span data-stu-id="60f0d-157">The snapshot opens to the line of code where the exception was thrown so that you can debug the current state of the process.</span></span>

    ![Просмотр отладочного моментального снимка в Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="60f0d-159">Скачанный моментальный снимок содержит все файлы символов, найденные на сервере веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="60f0d-159">The downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="60f0d-160">Эти файлы символов требуются для связывания данных моментального снимка с исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="60f0d-160">These symbol files are required to associate snapshot data with source code.</span></span> <span data-ttu-id="60f0d-161">Для приложений службы приложений не забудьте включить развертывание символов при публикации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="60f0d-161">For App Service apps, make sure to enable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="60f0d-162">Как работают моментальные снимки</span><span class="sxs-lookup"><span data-stu-id="60f0d-162">How snapshots work</span></span>

<span data-ttu-id="60f0d-163">При запуске приложения создается отдельный процесс передачи моментальных снимков, отслеживающий запросы на создание моментальных снимков для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="60f0d-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="60f0d-164">При запросе создания моментального снимка за 10–20 минут создается теневая копия выполняющегося процесса.</span><span class="sxs-lookup"><span data-stu-id="60f0d-164">When a snapshot is requested, a shadow copy of the running process is made in about 10 to 20 minutes.</span></span> <span data-ttu-id="60f0d-165">Затем теневой процесс анализируется и создается моментальный снимок. При этом основной процесс продолжает работать и обслуживать трафик для пользователей.</span><span class="sxs-lookup"><span data-stu-id="60f0d-165">The shadow process is then analyzed, and a snapshot is created while the main process continues to run and serve traffic to users.</span></span> <span data-ttu-id="60f0d-166">Моментальный снимок передается в Application Insights вместе с соответствующими PDB-файлами символов, необходимыми для просмотра моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="60f0d-166">The snapshot is then uploaded to Application Insights along with any relevant symbol (.pdb) files that are needed to view the snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="60f0d-167">Текущие ограничения</span><span class="sxs-lookup"><span data-stu-id="60f0d-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="60f0d-168">Публикация символов</span><span class="sxs-lookup"><span data-stu-id="60f0d-168">Publish symbols</span></span>
<span data-ttu-id="60f0d-169">Отладчику моментальных снимков требуется наличие файлов символов на рабочем сервере для декодирования переменных и обеспечения возможности отладки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60f0d-169">The Snapshot Debugger requires symbol files on the production server to decode variables and to provide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="60f0d-170">Выпуск 15.2 приложения Visual Studio 2017 по умолчанию публикует символы для сборок выпуска при публикации в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="60f0d-170">The 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes to App Service.</span></span> <span data-ttu-id="60f0d-171">В предыдущих версиях в профиль публикации `.pubxml` необходимо добавить приведенную ниже строку, чтобы символы публиковались в режиме выпуска.</span><span class="sxs-lookup"><span data-stu-id="60f0d-171">In prior versions, you need to add the following line to your publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="60f0d-172">Для среды вычислений Azure и других типов сред убедитесь, что файлы символов находятся в той же папке, что и библиотеки DLL основного приложения (обычно это `wwwroot/bin`), или доступны по текущему пути.</span><span class="sxs-lookup"><span data-stu-id="60f0d-172">For Azure Compute and other types, ensure that the symbol files are in the same folder of the main application .dll (typically, `wwwroot/bin`) or are available on the current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="60f0d-173">Оптимизированные сборки</span><span class="sxs-lookup"><span data-stu-id="60f0d-173">Optimized builds</span></span>
<span data-ttu-id="60f0d-174">В некоторых случаях локальные переменные не могут отображаться в сборках выпуска из-за оптимизаций, примененных во время процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="60f0d-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during the build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="60f0d-175">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="60f0d-175">Troubleshooting</span></span>

<span data-ttu-id="60f0d-176">Эти советы помогут при устранении проблем, связанных с отладчиком моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="60f0d-176">These tips help you troubleshoot problems with the Snapshot Debugger.</span></span>

### <a name="verify-the-instrumentation-key"></a><span data-ttu-id="60f0d-177">Проверка ключа инструментирования</span><span class="sxs-lookup"><span data-stu-id="60f0d-177">Verify the instrumentation key</span></span>

<span data-ttu-id="60f0d-178">Убедитесь, что в опубликованном приложении используется правильный ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="60f0d-178">Make sure that you're using the correct instrumentation key in your published application.</span></span> <span data-ttu-id="60f0d-179">Как правило, Application Insights счтывает ключ инструментирования из файла ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="60f0d-179">Usually, Application Insights reads the instrumentation key from the ApplicationInsights.config file.</span></span> <span data-ttu-id="60f0d-180">Убедитесь, что его значение такое же, что и у ключа инструментирования для ресурса Application Insights, который отображается на портале.</span><span class="sxs-lookup"><span data-stu-id="60f0d-180">Verify that the value is the same as the instrumentation key for the Application Insights resource that you see in the portal.</span></span>

### <a name="check-the-uploader-logs"></a><span data-ttu-id="60f0d-181">Проверьте журналы отправителя</span><span class="sxs-lookup"><span data-stu-id="60f0d-181">Check the uploader logs</span></span>

<span data-ttu-id="60f0d-182">После создания моментального снимка на диске создается файл минидампа (.dmp).</span><span class="sxs-lookup"><span data-stu-id="60f0d-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="60f0d-183">Этот файл минидампа и любые связанные PDB-файлы отправляются в отдельном процессе передачи в хранилище отладчика моментальных снимков Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60f0d-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, to Application Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="60f0d-184">После успешной передачи минидамп удаляется с диска.</span><span class="sxs-lookup"><span data-stu-id="60f0d-184">After the minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="60f0d-185">Файлы журнала для отправителя минидампа сохраняются на диске.</span><span class="sxs-lookup"><span data-stu-id="60f0d-185">The log files for the minidump uploader are retained on disk.</span></span> <span data-ttu-id="60f0d-186">В среде службы приложений эти журналы можно найти в `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="60f0d-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="60f0d-187">Используйте веб-сайт управления Kudu для службы приложений, чтобы найти эти файлы журнала.</span><span class="sxs-lookup"><span data-stu-id="60f0d-187">Use the Kudu management site for App Service to find these log files.</span></span>

1. <span data-ttu-id="60f0d-188">Откройте службу приложений на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="60f0d-188">Open your App Service application in the Azure portal.</span></span>

2. <span data-ttu-id="60f0d-189">Щелкните колонку **Дополнительные инструменты** или найдите **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="60f0d-189">Select the **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="60f0d-190">Щелкните **Переход**.</span><span class="sxs-lookup"><span data-stu-id="60f0d-190">Click **Go**.</span></span>
4. <span data-ttu-id="60f0d-191">В раскрывающемся списке **Debug console** (Консоль отладки) выберите **CMD** (Команда).</span><span class="sxs-lookup"><span data-stu-id="60f0d-191">In the **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="60f0d-192">Щелкните **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="60f0d-192">Click **LogFiles**.</span></span>

<span data-ttu-id="60f0d-193">Вы увидите хотя бы один файл с именем, начинающимся с `Uploader_` и расширением `.log`.</span><span class="sxs-lookup"><span data-stu-id="60f0d-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="60f0d-194">Щелкните соответствующую пиктограмму, чтобы скачать все файлы журналов, или открыть их в браузере.</span><span class="sxs-lookup"><span data-stu-id="60f0d-194">Click the appropriate icon to download any log files or open them in a browser.</span></span>
<span data-ttu-id="60f0d-195">Имя файла содержит имя компьютера.</span><span class="sxs-lookup"><span data-stu-id="60f0d-195">The file name includes the machine name.</span></span> <span data-ttu-id="60f0d-196">Если экземпляр службы приложений размещен на нескольких компьютерах, для каждого компьютера существуют отдельные файлы журналов.</span><span class="sxs-lookup"><span data-stu-id="60f0d-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="60f0d-197">Когда отправитель обнаруживает новый файл минидампа, он записывается в файл журнала.</span><span class="sxs-lookup"><span data-stu-id="60f0d-197">When the uploader detects a new minidump file, it is recorded in the log file.</span></span> <span data-ttu-id="60f0d-198">Ниже приведен пример успешной отправки:</span><span class="sxs-lookup"><span data-stu-id="60f0d-198">Here's an example of a successful upload:</span></span>

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

<span data-ttu-id="60f0d-199">В предыдущем примере, ключ инструментирования — это `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="60f0d-199">In the previous example, the instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="60f0d-200">Это значение должно соответствовать ключу инструментирования для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="60f0d-200">This value should match the instrumentation key for your application.</span></span>
<span data-ttu-id="60f0d-201">Минидамп связан с моментальным снимком с идентификатором `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="60f0d-201">The minidump is associated with a snapshot with the ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="60f0d-202">Позже этот идентификатор можно использовать для поиска связанной телеметрии исключений в аналитике Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60f0d-202">You can use this ID later to locate the associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="60f0d-203">Отправитель проверяет наличие новых PDB-файлов примерно один раз каждые 15 минут.</span><span class="sxs-lookup"><span data-stu-id="60f0d-203">The uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="60f0d-204">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="60f0d-204">Here's an example:</span></span>

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

<span data-ttu-id="60f0d-205">Для приложений, которые _не_ размещаются в службе приложений, журналы отправителя находятся в той же папке минидампов: `%TEMP%\Dumps\<ikey>` (где `<ikey>` ваш ключ инструментирования).</span><span class="sxs-lookup"><span data-stu-id="60f0d-205">For applications that are _not_ hosted in App Service, the uploader logs are in the same folder as the minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-to-find-exceptions-with-snapshots"></a><span data-ttu-id="60f0d-206">Поиск исключений с моментальными снимками с помощью поиска Application Insights</span><span class="sxs-lookup"><span data-stu-id="60f0d-206">Use Application Insights search to find exceptions with snapshots</span></span>

<span data-ttu-id="60f0d-207">При создании моментального снимка вызванное исключение обозначается идентификатором моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="60f0d-207">When a snapshot is created, the throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="60f0d-208">При передаче телеметрии исключения в Application Insights этот идентификатор моментального снимка включается в качестве пользовательского свойства.</span><span class="sxs-lookup"><span data-stu-id="60f0d-208">When the exception telemetry is reported to Application Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="60f0d-209">В колонке поиска Application Insights можно найти все данные телеметрии с пользовательским свойством `ai.snapshot.id`.</span><span class="sxs-lookup"><span data-stu-id="60f0d-209">Using the Search blade in Application Insights, you can find all telemetry with the `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="60f0d-210">Перейдите к ресурсу Application Insights на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="60f0d-210">Browse to your Application Insights resource in the Azure portal.</span></span>
2. <span data-ttu-id="60f0d-211">Щелкните **Search**(Поиск).</span><span class="sxs-lookup"><span data-stu-id="60f0d-211">Click **Search**.</span></span>
3. <span data-ttu-id="60f0d-212">В текстовом поле поиска введите `ai.snapshot.id` и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="60f0d-212">Type `ai.snapshot.id` in the Search text box and press Enter.</span></span>

![Поиск телеметрии с помощью идентификатора моментального снимка на портале](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="60f0d-214">Если этот поиск не дал результатов, значит в Application Insights не передавались моментальные снимки для приложения в выбранный диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="60f0d-214">If this search returns no results, then no snapshots were reported to Application Insights for your application in the selected time range.</span></span>

<span data-ttu-id="60f0d-215">Чтобы найти определенный идентификатор снимка из журналов отправителя, введите этот идентификатор в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="60f0d-215">To search for a specific snapshot ID from the Uploader logs, type that ID in the Search box.</span></span> <span data-ttu-id="60f0d-216">Если не удается найти данные телеметрии для моментального снимка, который был отправлен, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="60f0d-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="60f0d-217">Еще раз проверьте, что вы смотрите на правильный ресурс Application Insights при проверке ключа инструментирования.</span><span class="sxs-lookup"><span data-stu-id="60f0d-217">Double-check that you're looking at the right Application Insights resource by verifying the instrumentation key.</span></span>

2. <span data-ttu-id="60f0d-218">С помощью метки времени из журнала отправителя, настройте фильтр диапазона времени поиска так, чтобы охватить этот диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="60f0d-218">Using the timestamp from the Uploader log, adjust the Time Range filter of the search to cover that time range.</span></span>

<span data-ttu-id="60f0d-219">Если исключение с таким идентификатором моментальных снимков по-прежнему не отображается, значит телеметрия исключения не отправлялась в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60f0d-219">If you still don't see an exception with that snapshot ID, then the exception telemetry wasn't reported to Application Insights.</span></span> <span data-ttu-id="60f0d-220">Это происходит в случае сбоя приложения после снятия снимка, но до того как оно передало телеметрию исключений.</span><span class="sxs-lookup"><span data-stu-id="60f0d-220">This situation can happen if your application crashed after it took the snapshot but before it reported the exception telemetry.</span></span> <span data-ttu-id="60f0d-221">В этом случае проверьте журналы службы приложений в `Diagnose and solve problems`, чтобы проверить, были ли неожиданные перезагрузки или необработанные исключения.</span><span class="sxs-lookup"><span data-stu-id="60f0d-221">In this case, check the App Service logs under `Diagnose and solve problems` to see if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60f0d-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="60f0d-222">Next steps</span></span>

* <span data-ttu-id="60f0d-223">[Установите в коде точки прикрепления](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/), чтобы получать моментальные снимки не ожидая исключений.</span><span class="sxs-lookup"><span data-stu-id="60f0d-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) to get snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="60f0d-224">В статье [Диагностика исключений в веб-приложениях с помощью Application Insights](app-insights-asp-net-exceptions.md) объясняется, как отобразить дополнительные исключения в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="60f0d-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how to make more exceptions visible to Application Insights.</span></span> 
* <span data-ttu-id="60f0d-225">В статье [Интеллектуальное обнаружение в Application Insights](app-insights-proactive-diagnostics.md) описывается автоматическое обнаружение аномалий производительности.</span><span class="sxs-lookup"><span data-stu-id="60f0d-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
