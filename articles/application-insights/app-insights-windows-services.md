---
title: "Azure Application Insights для рабочих ролей и служб Windows | Документация Майкрософт"
description: "Добавьте вручную пакет SDK Application Insights в приложение ASP.NET для анализа использования, доступности и производительности."
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
ms.openlocfilehash: 4b9f8c618a69c4c157dafeb7f726aae24efad428
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="9dd11-103">Настройка Application Insights вручную для приложений .NET</span><span class="sxs-lookup"><span data-stu-id="9dd11-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="9dd11-104">Вы можете настроить [Application Insights](app-insights-overview.md) для мониторинга разнообразных приложений, ролей приложений, компонентов или микрослужб.</span><span class="sxs-lookup"><span data-stu-id="9dd11-104">You can configure [Application Insights](app-insights-overview.md) to monitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="9dd11-105">Для веб-приложений и служб Visual Studio предлагает [одноэтапную настройку](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="9dd11-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="9dd11-106">Для других типов приложений .NET, таких как внутренние роли сервера или классические приложения, вы можете настроить Application Insights вручную.</span><span class="sxs-lookup"><span data-stu-id="9dd11-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Пример диаграмм мониторинга производительности](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="9dd11-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9dd11-108">Before you start</span></span>

<span data-ttu-id="9dd11-109">Вам необходимы:</span><span class="sxs-lookup"><span data-stu-id="9dd11-109">You need:</span></span>

* <span data-ttu-id="9dd11-110">подписка на [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="9dd11-110">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="9dd11-111">Если у вашей группы или организации есть подписка Azure, владелец может добавить вас в нее с помощью вашей [учетной записи Майкрософт](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="9dd11-111">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="9dd11-112">Visual Studio 2013 или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="9dd11-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="9dd11-113"><a name="add"></a>1. Выбор ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="9dd11-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="9dd11-114">Ресурс — место, где ваши данные собираются и отображаются на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd11-114">The 'resource' is where your data is collected and displayed in the Azure portal.</span></span> <span data-ttu-id="9dd11-115">Определитесь, что вам нужно: создать еще один ресурс или совместно использовать имеющийся.</span><span class="sxs-lookup"><span data-stu-id="9dd11-115">You need to decide whether to create a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="9dd11-116">Часть большего приложения. Использование имеющегося ресурса</span><span class="sxs-lookup"><span data-stu-id="9dd11-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="9dd11-117">Если веб-приложение состоит из нескольких компонентов, например интерфейсное веб-приложение и одна или несколько серверных служб, вы должны отправлять телеметрию со всех компонентов в один ресурс.</span><span class="sxs-lookup"><span data-stu-id="9dd11-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all the components to the same resource.</span></span> <span data-ttu-id="9dd11-118">Так они будут отображаться на единой схеме сопоставления приложений, а вы сможете отслеживать запрос от одного компонента к другому.</span><span class="sxs-lookup"><span data-stu-id="9dd11-118">This will enable them to be displayed on a single Application Map, and make it possible to trace a request from one component to another.</span></span>

<span data-ttu-id="9dd11-119">Если вы уже отслеживаете другие компоненты этого приложения, просто используйте тот же ресурс.</span><span class="sxs-lookup"><span data-stu-id="9dd11-119">So, if you're already monitoring other components of this app, then just use the same resource.</span></span>

<span data-ttu-id="9dd11-120">Откройте ресурс на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9dd11-120">Open the resource in the [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="9dd11-121">Автономное приложение. Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="9dd11-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="9dd11-122">Если новое приложение не связано с другими приложениями, оно должно иметь свой ресурс.</span><span class="sxs-lookup"><span data-stu-id="9dd11-122">If the new app is unrelated to other applications, then it should have its own resource.</span></span>

<span data-ttu-id="9dd11-123">Войдите на [портал Azure](https://portal.azure.com/)и создайте новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9dd11-123">Sign in to the [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="9dd11-124">Выберите приложение ASP.NET в качестве типа приложения.</span><span class="sxs-lookup"><span data-stu-id="9dd11-124">Choose ASP.NET as the application type.</span></span>

![Нажмите "Создать" и "Application Insights"](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="9dd11-126">От выбранного типа приложения зависит содержимое по умолчанию столбцов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9dd11-126">The choice of application type sets the default content of the resource blades.</span></span>

## <a name="2-copy-the-instrumentation-key"></a><span data-ttu-id="9dd11-127">2) Копирование ключа инструментирования</span><span class="sxs-lookup"><span data-stu-id="9dd11-127">2. Copy the Instrumentation Key</span></span>
<span data-ttu-id="9dd11-128">Ключ идентифицирует ресурс.</span><span class="sxs-lookup"><span data-stu-id="9dd11-128">The key identifies the resource.</span></span> <span data-ttu-id="9dd11-129">Вы установите его в пакет SDK для направления данных ресурсу.</span><span class="sxs-lookup"><span data-stu-id="9dd11-129">You'll install it soon in the SDK, in order to direct data to the resource.</span></span>

![Нажмите "Свойства", выберите ключ и нажмите сочетание клавиш CTRL + C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="9dd11-131"><a name="sdk"></a>3. Установка пакета Application Insights в приложении</span><span class="sxs-lookup"><span data-stu-id="9dd11-131"><a name="sdk"></a>3. Install the Application Insights package in your application</span></span>
<span data-ttu-id="9dd11-132">Установка и настройка пакета Application Insights зависит от платформы, на которой вы работаете.</span><span class="sxs-lookup"><span data-stu-id="9dd11-132">Installing and configuring the Application Insights package varies depending on the platform you're working on.</span></span> 

1. <span data-ttu-id="9dd11-133">В Visual Studio щелкните проект правой кнопкой мыши и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9dd11-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Щелкните проект правой кнопкой мыши и выберите пункт "Управление пакетами Nuget"](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="9dd11-135">Установите пакет Application Insights Microsoft.ApplicationInsights.WindowsServer. для приложений Windows Server.</span><span class="sxs-lookup"><span data-stu-id="9dd11-135">Install the Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Поиск Application Insights](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="9dd11-137">*Какую версию выбрать?*</span><span class="sxs-lookup"><span data-stu-id="9dd11-137">*Which version?*</span></span>

    <span data-ttu-id="9dd11-138">Установите флажок **Включить предварительные выпуски**, если вы хотите воспользоваться нашими новыми функциями.</span><span class="sxs-lookup"><span data-stu-id="9dd11-138">Check **Include prerelease** if you want to try our latest features.</span></span> <span data-ttu-id="9dd11-139">Дополнительные сведения о том, нужна ли вам предварительная версия, см. в соответствующих документах или блогах.</span><span class="sxs-lookup"><span data-stu-id="9dd11-139">The relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="9dd11-140">*Можно ли использовать другие пакеты?*</span><span class="sxs-lookup"><span data-stu-id="9dd11-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="9dd11-141">Да.</span><span class="sxs-lookup"><span data-stu-id="9dd11-141">Yes.</span></span> <span data-ttu-id="9dd11-142">Выберите Microsoft.ApplicationInsights, если вы хотите использовать API для отправки собственной телеметрии.</span><span class="sxs-lookup"><span data-stu-id="9dd11-142">Choose "Microsoft.ApplicationInsights" if you only want to use the API to send your own telemetry.</span></span> <span data-ttu-id="9dd11-143">Пакет Windows Server включает API, а также ряд других пакетов, например для сбора данных счетчиков производительности и отслеживания зависимостей.</span><span class="sxs-lookup"><span data-stu-id="9dd11-143">The Windows Server package includes the API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="to-upgrade-to-future-package-versions"></a><span data-ttu-id="9dd11-144">Обновление до будущих версий пакета</span><span class="sxs-lookup"><span data-stu-id="9dd11-144">To upgrade to future package versions</span></span>
<span data-ttu-id="9dd11-145">Время от времени мы выпускаем новую версию пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="9dd11-145">We release a new version of the SDK from time to time.</span></span>

<span data-ttu-id="9dd11-146">Чтобы выполнить обновление до [нового выпуска пакета](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), еще раз откройте диспетчер пакетов NuGet и выполните фильтрацию по установленным пакетам.</span><span class="sxs-lookup"><span data-stu-id="9dd11-146">To upgrade to a [new release of the package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="9dd11-147">Выберите **Microsoft.ApplicationInsights.WindowsServer**, а затем — **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="9dd11-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="9dd11-148">Если были выполнены какие-либо настройки файла ApplicationInsights.config, то, прежде чем выполнять обновление, сохраните его копию, а затем объедините изменения в новой версии.</span><span class="sxs-lookup"><span data-stu-id="9dd11-148">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into the new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="9dd11-149">4. Отправка данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="9dd11-149">4. Send telemetry</span></span>
<span data-ttu-id="9dd11-150">**Если установлен только пакет API:**</span><span class="sxs-lookup"><span data-stu-id="9dd11-150">**If you installed only the API package:**</span></span>

* <span data-ttu-id="9dd11-151">Задайте ключ инструментирования в коде, например в `main()`:</span><span class="sxs-lookup"><span data-stu-id="9dd11-151">Set the instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="9dd11-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *ваш ключ* `";`</span><span class="sxs-lookup"><span data-stu-id="9dd11-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="9dd11-153">[Создайте собственную телеметрию с помощью](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="9dd11-153">[Write your own telemetry using the API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="9dd11-154">**Если у вас установлены другие пакеты Application Insights** , ключ инструментирования можно задать с помощью CONFIG-файла:</span><span class="sxs-lookup"><span data-stu-id="9dd11-154">**If you installed other Application Insights packages,** you can, if you prefer, use the .config file to set the instrumentation key:</span></span>

* <span data-ttu-id="9dd11-155">Отредактируйте файл ApplicationInsights.config (который был добавлен при установке NuGet).</span><span class="sxs-lookup"><span data-stu-id="9dd11-155">Edit ApplicationInsights.config (which was added by the NuGet install).</span></span> <span data-ttu-id="9dd11-156">Вставьте следующий фрагмент непосредственно перед закрывающим тегом:</span><span class="sxs-lookup"><span data-stu-id="9dd11-156">Insert this just before the closing tag:</span></span>
  
    <span data-ttu-id="9dd11-157">`<InstrumentationKey>` *скопированный ключ инструментирования* `</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="9dd11-157">`<InstrumentationKey>` *the instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="9dd11-158">Убедитесь, что свойства файла ApplicationInsights.config в обозревателе решений имеют следующие значения: **"Действие сборки = содержимое", "Копировать в выходной каталог = копировать"**.</span><span class="sxs-lookup"><span data-stu-id="9dd11-158">Make sure that the properties of ApplicationInsights.config in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>

<span data-ttu-id="9dd11-159">Если вы хотите [изменить ключ для разных конфигураций сборки](app-insights-separate-resources.md), можно задать ключ инструментирования в коде.</span><span class="sxs-lookup"><span data-stu-id="9dd11-159">It's useful to set the instrumentation key in code if you want to [switch the key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="9dd11-160">Если ключ задан в коде, его не нужно задавать в файле `.config`.</span><span class="sxs-lookup"><span data-stu-id="9dd11-160">If you set the key in code, you don't have to set it in the `.config` file.</span></span>

## <span data-ttu-id="9dd11-161"><a name="run"></a>Запуск проекта</span><span class="sxs-lookup"><span data-stu-id="9dd11-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="9dd11-162">Запустите приложение, нажав клавишу **F5** , и попробуйте открывать разные страницы, чтобы создать некоторый объем данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="9dd11-162">Use the **F5** to run your application and try it out: open different pages to generate some telemetry.</span></span>

<span data-ttu-id="9dd11-163">В Visual Studio вы увидите число отправленных событий.</span><span class="sxs-lookup"><span data-stu-id="9dd11-163">In Visual Studio, you'll see a count of the events that have been sent.</span></span>

![Количество событий в Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="9dd11-165"><a name="monitor"></a> Просмотр своих данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="9dd11-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="9dd11-166">Вернитесь на [портал Azure](https://portal.azure.com/) и перейдите к своему ресурсу Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9dd11-166">Return to the [Azure portal](https://portal.azure.com/) and browse to your Application Insights resource.</span></span>

<span data-ttu-id="9dd11-167">Выполните поиск данных в диаграммах "Обзор".</span><span class="sxs-lookup"><span data-stu-id="9dd11-167">Look for data in the Overview charts.</span></span> <span data-ttu-id="9dd11-168">Сначала вы увидите только одну или две точки.</span><span class="sxs-lookup"><span data-stu-id="9dd11-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="9dd11-169">Например:</span><span class="sxs-lookup"><span data-stu-id="9dd11-169">For example:</span></span>

![Щелкните плитки, чтобы увидеть больше данных](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="9dd11-171">Щелкните любую диаграмму, чтобы увидеть более подробные метрики.</span><span class="sxs-lookup"><span data-stu-id="9dd11-171">Click through any chart to see more detailed metrics.</span></span> [<span data-ttu-id="9dd11-172">Дополнительные сведения о метриках.</span><span class="sxs-lookup"><span data-stu-id="9dd11-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="9dd11-173">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="9dd11-173">No data?</span></span>
* <span data-ttu-id="9dd11-174">Используйте приложение, открывая различные страницы, чтобы создать некоторый объем данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="9dd11-174">Use the application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="9dd11-175">Откройте плитку [Поиск](app-insights-diagnostic-search.md) , чтобы просмотреть отдельные события.</span><span class="sxs-lookup"><span data-stu-id="9dd11-175">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span></span> <span data-ttu-id="9dd11-176">Иногда для прохождения событий через конвейер метрики требуется чуть больше времени.</span><span class="sxs-lookup"><span data-stu-id="9dd11-176">Sometimes it takes events a little while longer to get through the metrics pipeline.</span></span>
* <span data-ttu-id="9dd11-177">Подождите несколько секунд и нажмите **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="9dd11-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="9dd11-178">Диаграмма периодически обновляется, однако ее можно обновить и вручную, если вы ждете появления каких-либо данных.</span><span class="sxs-lookup"><span data-stu-id="9dd11-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span></span>
* <span data-ttu-id="9dd11-179">См. раздел [Устранение неполадок](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9dd11-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="9dd11-180">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="9dd11-180">Publish your app</span></span>
<span data-ttu-id="9dd11-181">Теперь разверните свое приложение на сервере или в Azure и наблюдайте за тем, как накапливаются данные.</span><span class="sxs-lookup"><span data-stu-id="9dd11-181">Now deploy your application to your server or to Azure and watch the data accumulate.</span></span>

![Опубликуйте свое веб-приложение с помощью Visual Studio](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="9dd11-183">При работе в режиме отладки телеметрия передается через конвейер, поэтому данные должны появиться в течение нескольких секунд.</span><span class="sxs-lookup"><span data-stu-id="9dd11-183">When you run in debug mode, telemetry is expedited through the pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="9dd11-184">При развертывании приложения в конфигурации выпуска данные накапливаются медленнее.</span><span class="sxs-lookup"><span data-stu-id="9dd11-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-to-your-server"></a><span data-ttu-id="9dd11-185">Отсутствуют данные после публикации на сервере?</span><span class="sxs-lookup"><span data-stu-id="9dd11-185">No data after you publish to your server?</span></span>
<span data-ttu-id="9dd11-186">Откройте порты для исходящего трафика в брандмауэре сервера.</span><span class="sxs-lookup"><span data-stu-id="9dd11-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="9dd11-187">Список необходимых адресов можно просмотреть на [этой странице](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="9dd11-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for the list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="9dd11-188">Проблемы на сервере сборки?</span><span class="sxs-lookup"><span data-stu-id="9dd11-188">Trouble on your build server?</span></span>
<span data-ttu-id="9dd11-189">Изучите [этот элемент устранения неполадок](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="9dd11-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="9dd11-190">Если приложение генерирует много телеметрических данных, модуль адаптивной выборки автоматически сокращает объем отправляемых на портал данных, пересылая только репрезентативную часть событий.</span><span class="sxs-lookup"><span data-stu-id="9dd11-190">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="9dd11-191">При этом связанные с тем же запросом события отбираются как группа, что позволяет перемещаться между связанными событиями.</span><span class="sxs-lookup"><span data-stu-id="9dd11-191">However, events that are related to the same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="9dd11-192">[Дополнительная информация о выборке](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9dd11-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="9dd11-193">Видео</span><span class="sxs-lookup"><span data-stu-id="9dd11-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="9dd11-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9dd11-194">Next steps</span></span>
* <span data-ttu-id="9dd11-195">[добавить дополнительную телеметрию](app-insights-asp-net-more.md) .</span><span class="sxs-lookup"><span data-stu-id="9dd11-195">[Add more telemetry](app-insights-asp-net-more.md) to get the full 360-degree view of your application.</span></span>

