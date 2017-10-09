---
title: "aaaAzure аналитики приложений для Windows server ролей и рабочих ролей | Документы Microsoft"
description: "Вручную добавьте использование tooanalyze приложения ASP.NET tooyour hello пакет SDK Application Insights, доступности и производительности."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="8c204-103">Настройка Application Insights вручную для приложений .NET</span><span class="sxs-lookup"><span data-stu-id="8c204-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="8c204-104">Можно настроить [Application Insights](app-insights-overview.md) toomonitor широкий спектр приложений или ролей приложения, компоненты или микрослужбами.</span><span class="sxs-lookup"><span data-stu-id="8c204-104">You can configure [Application Insights](app-insights-overview.md) toomonitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="8c204-105">Для веб-приложений и служб Visual Studio предлагает [одноэтапную настройку](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="8c204-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="8c204-106">Для других типов приложений .NET, таких как внутренние роли сервера или классические приложения, вы можете настроить Application Insights вручную.</span><span class="sxs-lookup"><span data-stu-id="8c204-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Пример диаграмм мониторинга производительности](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="8c204-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="8c204-108">Before you start</span></span>

<span data-ttu-id="8c204-109">Вам необходимы:</span><span class="sxs-lookup"><span data-stu-id="8c204-109">You need:</span></span>

* <span data-ttu-id="8c204-110">Подписка слишком[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c204-110">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="8c204-111">Если в команде или организации имеет подписку Azure, в владелец hello добавлять tooit, с помощью вашей [учетную запись Майкрософт](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="8c204-111">If your team or organization has an Azure subscription, hello owner can add you tooit, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="8c204-112">Visual Studio 2013 или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="8c204-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="8c204-113"><a name="add"></a>1. Выбор ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="8c204-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="8c204-114">ресурс «Hello» — где собираются и отображаются в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8c204-114">hello 'resource' is where your data is collected and displayed in hello Azure portal.</span></span> <span data-ttu-id="8c204-115">Toodecide требуется ли toocreate создать новую или существующую общую папку.</span><span class="sxs-lookup"><span data-stu-id="8c204-115">You need toodecide whether toocreate a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="8c204-116">Часть большего приложения. Использование имеющегося ресурса</span><span class="sxs-lookup"><span data-stu-id="8c204-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="8c204-117">Если веб-приложение содержит несколько компонентов — например, интерфейсный веб-приложения и один или несколько служб, -, то необходимо отправлять данные телеметрии из всех toohello компонентов hello того же ресурса.</span><span class="sxs-lookup"><span data-stu-id="8c204-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all hello components toohello same resource.</span></span> <span data-ttu-id="8c204-118">Это включает их toobe, отображаемые на карте одного приложения и сделать его возможных tootrace запроса из одного компонента tooanother.</span><span class="sxs-lookup"><span data-stu-id="8c204-118">This will enable them toobe displayed on a single Application Map, and make it possible tootrace a request from one component tooanother.</span></span>

<span data-ttu-id="8c204-119">Таким образом, если другие компоненты этого приложения уже мониторинг, затем просто воспользуйтесь hello же ресурса.</span><span class="sxs-lookup"><span data-stu-id="8c204-119">So, if you're already monitoring other components of this app, then just use hello same resource.</span></span>

<span data-ttu-id="8c204-120">Откройте ресурс hello в hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8c204-120">Open hello resource in hello [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="8c204-121">Автономное приложение. Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="8c204-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="8c204-122">Если новое приложение hello связаны tooother приложений, он должен иметь свой собственный ресурс.</span><span class="sxs-lookup"><span data-stu-id="8c204-122">If hello new app is unrelated tooother applications, then it should have its own resource.</span></span>

<span data-ttu-id="8c204-123">Войдите в toohello [портал Azure](https://portal.azure.com/)и создать новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8c204-123">Sign in toohello [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="8c204-124">Выберите в качестве типа приложения hello ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8c204-124">Choose ASP.NET as hello application type.</span></span>

![Нажмите "Создать" и "Application Insights"](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="8c204-126">Выбор типа приложения Hello задает содержимое по умолчанию hello колонки ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="8c204-126">hello choice of application type sets hello default content of hello resource blades.</span></span>

## <a name="2-copy-hello-instrumentation-key"></a><span data-ttu-id="8c204-127">2. Скопируйте ключ инструментирования hello</span><span class="sxs-lookup"><span data-stu-id="8c204-127">2. Copy hello Instrumentation Key</span></span>
<span data-ttu-id="8c204-128">ключ Hello идентифицирует ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="8c204-128">hello key identifies hello resource.</span></span> <span data-ttu-id="8c204-129">Оно будет установлено только в hello SDK, в порядке toodirect данных toohello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8c204-129">You'll install it soon in hello SDK, in order toodirect data toohello resource.</span></span>

![Щелкните свойства, выберите раздел hello и нажмите клавиши ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="8c204-131"><a name="sdk"></a>3. Установить пакет аналитики приложения hello в приложении</span><span class="sxs-lookup"><span data-stu-id="8c204-131"><a name="sdk"></a>3. Install hello Application Insights package in your application</span></span>
<span data-ttu-id="8c204-132">Установка и настройка hello Application Insights пакета зависит от платформы hello, над которым вы работаете.</span><span class="sxs-lookup"><span data-stu-id="8c204-132">Installing and configuring hello Application Insights package varies depending on hello platform you're working on.</span></span> 

1. <span data-ttu-id="8c204-133">В Visual Studio щелкните проект правой кнопкой мыши и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8c204-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Щелкните правой кнопкой мыши проект hello и выберите Управление пакетами Nuget](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="8c204-135">Установить пакет hello Application Insights для приложений Windows server, «Microsoft.ApplicationInsights.WindowsServer.»</span><span class="sxs-lookup"><span data-stu-id="8c204-135">Install hello Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Поиск Application Insights](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="8c204-137">*Какую версию выбрать?*</span><span class="sxs-lookup"><span data-stu-id="8c204-137">*Which version?*</span></span>

    <span data-ttu-id="8c204-138">Проверьте **включить предварительный выпуск** Если tootry нашей новейших функций.</span><span class="sxs-lookup"><span data-stu-id="8c204-138">Check **Include prerelease** if you want tootry our latest features.</span></span> <span data-ttu-id="8c204-139">Hello соответствующих документов или блоги Обратите внимание, следует ли предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="8c204-139">hello relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="8c204-140">*Можно ли использовать другие пакеты?*</span><span class="sxs-lookup"><span data-stu-id="8c204-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="8c204-141">Да.</span><span class="sxs-lookup"><span data-stu-id="8c204-141">Yes.</span></span> <span data-ttu-id="8c204-142">Выберите «Microsoft.ApplicationInsights» только toouse hello API toosend собственные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="8c204-142">Choose "Microsoft.ApplicationInsights" if you only want toouse hello API toosend your own telemetry.</span></span> <span data-ttu-id="8c204-143">пакет Windows Server Hello включает hello API, а также ряд других пакетов, таких как сбор данных счетчика производительности и отслеживание зависимостей.</span><span class="sxs-lookup"><span data-stu-id="8c204-143">hello Windows Server package includes hello API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="tooupgrade-toofuture-package-versions"></a><span data-ttu-id="8c204-144">версии пакетов toofuture tooupgrade</span><span class="sxs-lookup"><span data-stu-id="8c204-144">tooupgrade toofuture package versions</span></span>
<span data-ttu-id="8c204-145">Мы выпуска новой версии hello SDK из tootime времени.</span><span class="sxs-lookup"><span data-stu-id="8c204-145">We release a new version of hello SDK from time tootime.</span></span>

<span data-ttu-id="8c204-146">tooupgrade tooa [новый выпуск пакета hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), снова откройте диспетчер пакетов NuGet и фильтрации установленных пакетов.</span><span class="sxs-lookup"><span data-stu-id="8c204-146">tooupgrade tooa [new release of hello package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="8c204-147">Выберите **Microsoft.ApplicationInsights.WindowsServer**, а затем — **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="8c204-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="8c204-148">При внесении любого tooApplicationInsights.config настроек, сохраните ее копию перед выполнением обновления, а впоследствии объединить изменения в новой версии hello.</span><span class="sxs-lookup"><span data-stu-id="8c204-148">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into hello new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="8c204-149">4. Отправка данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="8c204-149">4. Send telemetry</span></span>
<span data-ttu-id="8c204-150">**Если установлен только пакет hello API:**</span><span class="sxs-lookup"><span data-stu-id="8c204-150">**If you installed only hello API package:**</span></span>

* <span data-ttu-id="8c204-151">Задать ключ инструментирования hello в коде, например в `main()`:</span><span class="sxs-lookup"><span data-stu-id="8c204-151">Set hello instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="8c204-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *ваш ключ* `";`</span><span class="sxs-lookup"><span data-stu-id="8c204-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="8c204-153">[Запись телеметрии с помощью hello API](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="8c204-153">[Write your own telemetry using hello API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="8c204-154">**Если вы установили другие пакеты Application Insights** Если вы предпочитаете, воспользуйтесь разделом hello .config файл tooset hello инструментирования:</span><span class="sxs-lookup"><span data-stu-id="8c204-154">**If you installed other Application Insights packages,** you can, if you prefer, use hello .config file tooset hello instrumentation key:</span></span>

* <span data-ttu-id="8c204-155">Измените файл ApplicationInsights.config (которая была добавлена, установить NuGet hello).</span><span class="sxs-lookup"><span data-stu-id="8c204-155">Edit ApplicationInsights.config (which was added by hello NuGet install).</span></span> <span data-ttu-id="8c204-156">Вставьте это непосредственно перед закрывающим тегом hello:</span><span class="sxs-lookup"><span data-stu-id="8c204-156">Insert this just before hello closing tag:</span></span>
  
    <span data-ttu-id="8c204-157">`<InstrumentationKey>`*вы скопировали ключ инструментирования hello*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="8c204-157">`<InstrumentationKey>` *hello instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="8c204-158">Убедитесь, что свойства hello ApplicationInsights.config в обозревателе решений задано слишком**действие построения = содержимое tooOutput копирования каталога = копирование**.</span><span class="sxs-lookup"><span data-stu-id="8c204-158">Make sure that hello properties of ApplicationInsights.config in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>

<span data-ttu-id="8c204-159">Это полезно tooset ключ инструментирования hello в коде, если требуется слишком[ключ hello коммутатора для разных конфигураций построения](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8c204-159">It's useful tooset hello instrumentation key in code if you want too[switch hello key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="8c204-160">Если значение ключа hello в коде, не нужно tooset в hello `.config` файла.</span><span class="sxs-lookup"><span data-stu-id="8c204-160">If you set hello key in code, you don't have tooset it in hello `.config` file.</span></span>

## <span data-ttu-id="8c204-161"><a name="run"></a>Запуск проекта</span><span class="sxs-lookup"><span data-stu-id="8c204-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="8c204-162">Используйте hello **F5** toorun приложения и попробуйте: открытые различные страницы toogenerate некоторые телеметрии.</span><span class="sxs-lookup"><span data-stu-id="8c204-162">Use hello **F5** toorun your application and try it out: open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="8c204-163">В Visual Studio вы увидите количество hello событий, которые были отправлены.</span><span class="sxs-lookup"><span data-stu-id="8c204-163">In Visual Studio, you'll see a count of hello events that have been sent.</span></span>

![Количество событий в Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="8c204-165"><a name="monitor"></a> Просмотр своих данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="8c204-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="8c204-166">Вернуть toohello [портал Azure](https://portal.azure.com/) и найдите ресурс Application Insights tooyour.</span><span class="sxs-lookup"><span data-stu-id="8c204-166">Return toohello [Azure portal](https://portal.azure.com/) and browse tooyour Application Insights resource.</span></span>

<span data-ttu-id="8c204-167">Поиск данных в диаграммах Обзор hello.</span><span class="sxs-lookup"><span data-stu-id="8c204-167">Look for data in hello Overview charts.</span></span> <span data-ttu-id="8c204-168">Сначала вы увидите только одну или две точки.</span><span class="sxs-lookup"><span data-stu-id="8c204-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="8c204-169">Например:</span><span class="sxs-lookup"><span data-stu-id="8c204-169">For example:</span></span>

![Перемещаться по данным toomore](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="8c204-171">Нажмите кнопку через любой toosee диаграммы более подробные показатели.</span><span class="sxs-lookup"><span data-stu-id="8c204-171">Click through any chart toosee more detailed metrics.</span></span> [<span data-ttu-id="8c204-172">Дополнительные сведения о метриках.</span><span class="sxs-lookup"><span data-stu-id="8c204-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="8c204-173">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="8c204-173">No data?</span></span>
* <span data-ttu-id="8c204-174">С помощью приложения hello, открыв разные страницы, чтобы он создает некоторые телеметрии.</span><span class="sxs-lookup"><span data-stu-id="8c204-174">Use hello application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="8c204-175">Откройте hello [поиска](app-insights-diagnostic-search.md) плитки toosee отдельные события.</span><span class="sxs-lookup"><span data-stu-id="8c204-175">Open hello [Search](app-insights-diagnostic-search.md) tile, toosee individual events.</span></span> <span data-ttu-id="8c204-176">Иногда принимает события немного больше времени, во время tooget через конвейер метрики hello.</span><span class="sxs-lookup"><span data-stu-id="8c204-176">Sometimes it takes events a little while longer tooget through hello metrics pipeline.</span></span>
* <span data-ttu-id="8c204-177">Подождите несколько секунд и нажмите **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="8c204-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="8c204-178">Сами периодически обновлять диаграммы, но можно обновить вручную, если вы ожидаете для некоторых данных tooshow.</span><span class="sxs-lookup"><span data-stu-id="8c204-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data tooshow up.</span></span>
* <span data-ttu-id="8c204-179">См. раздел [Устранение неполадок](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="8c204-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="8c204-180">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="8c204-180">Publish your app</span></span>
<span data-ttu-id="8c204-181">Теперь развертывания сервера tooyour приложения или накапливать данные hello tooAzure и контрольных значений.</span><span class="sxs-lookup"><span data-stu-id="8c204-181">Now deploy your application tooyour server or tooAzure and watch hello data accumulate.</span></span>

![Используйте Visual Studio toopublish приложения](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="8c204-183">При запуске в режиме отладки телеметрии ускорено через конвейер hello, чтобы вы увидите данные за несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="8c204-183">When you run in debug mode, telemetry is expedited through hello pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="8c204-184">При развертывании приложения в конфигурации выпуска данные накапливаются медленнее.</span><span class="sxs-lookup"><span data-stu-id="8c204-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-tooyour-server"></a><span data-ttu-id="8c204-185">Нет данных после публикации tooyour сервера?</span><span class="sxs-lookup"><span data-stu-id="8c204-185">No data after you publish tooyour server?</span></span>
<span data-ttu-id="8c204-186">Откройте порты для исходящего трафика в брандмауэре сервера.</span><span class="sxs-lookup"><span data-stu-id="8c204-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="8c204-187">В разделе [эту страницу](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) hello перечень необходимых адресов</span><span class="sxs-lookup"><span data-stu-id="8c204-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for hello list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="8c204-188">Проблемы на сервере сборки?</span><span class="sxs-lookup"><span data-stu-id="8c204-188">Trouble on your build server?</span></span>
<span data-ttu-id="8c204-189">Изучите [этот элемент устранения неполадок](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="8c204-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="8c204-190">Если приложение создает большой объем данных телеметрии, модуль адаптивной выборки hello автоматически уменьшит hello тома, отправляемое toohello портала, отправляя репрезентативной часть событий.</span><span class="sxs-lookup"><span data-stu-id="8c204-190">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="8c204-191">Тем не менее события, которые связанные toohello того же запроса будет иметь или отмену выбора как группой, чтобы могли перемещаться между связанными событиями.</span><span class="sxs-lookup"><span data-stu-id="8c204-191">However, events that are related toohello same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="8c204-192">[Дополнительная информация о выборке](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="8c204-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="8c204-193">Видео</span><span class="sxs-lookup"><span data-stu-id="8c204-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="8c204-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c204-194">Next steps</span></span>
* <span data-ttu-id="8c204-195">[Добавьте дополнительные телеметрии](app-insights-asp-net-more.md) tooget hello полной 360 градусов представления приложения.</span><span class="sxs-lookup"><span data-stu-id="8c204-195">[Add more telemetry](app-insights-asp-net-more.md) tooget hello full 360-degree view of your application.</span></span>

