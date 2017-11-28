---
title: "Отделение телеметрии стадий разработки, тестирования и выпуска в Azure Application Insights | Документация Майкрософт"
description: "Отправка телеметрии к различным ресурсам для меток разработки, тестирования и эксплуатации."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: f51fa4639aaa60686cc349683713c6e5f9732bb9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="35127-103">Отделение телеметрии стадий разработки, тестирования и эксплуатации</span><span class="sxs-lookup"><span data-stu-id="35127-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="35127-104">Разрабатывая следующую версию веб-приложения, вы не хотели бы путать данные телеметрии [Application Insights](app-insights-overview.md), полученные для новой версии, с данными уже выпущенной.</span><span class="sxs-lookup"><span data-stu-id="35127-104">When you are developing the next version of a web application, you don't want to mix up the [Application Insights](app-insights-overview.md) telemetry from the new version and the already released version.</span></span> <span data-ttu-id="35127-105">Чтобы избежать путаницы, отправляйте данные телеметрии разных стадий разработки в отдельные ресурсы Application Insights, используя отдельные ключи инструментирования.</span><span class="sxs-lookup"><span data-stu-id="35127-105">To avoid confusion, send the telemetry from different development stages to separate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="35127-106">Чтобы облегчить изменение ключа инструментирования в зависимости от стадии разработки, вы можете задать ключи инструментирования в коде, а не в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="35127-106">To make it easier to change the instrumentation key as a version moves from one stage to another, it can be useful to set the ikey in code instead of in the configuration file.</span></span> 

<span data-ttu-id="35127-107">(Если вы используете облачную службу Azure, есть [другой метод настройки отдельных ключей инструментирования ikey](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="35127-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="35127-108">Ресурсы и ключи инструментирования</span><span class="sxs-lookup"><span data-stu-id="35127-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="35127-109">При настройке мониторинга Application Insights для веб-приложения вы создаете *ресурс* Application Insights в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="35127-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="35127-110">Вы открываете этот ресурс на портале Azure для просмотра и анализа телеметрии, собранной из приложения.</span><span class="sxs-lookup"><span data-stu-id="35127-110">You open this resource in the Azure portal in order to see and analyze the telemetry collected from your app.</span></span> <span data-ttu-id="35127-111">Каждый ресурс идентифицируется с помощью *ключа инструментирования* (ikey).</span><span class="sxs-lookup"><span data-stu-id="35127-111">The resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="35127-112">При установке пакета Application Insights для мониторинга приложения вы можете настроить для него ключ инструментирования. Так ему будет известно, куда отправлять телеметрию.</span><span class="sxs-lookup"><span data-stu-id="35127-112">When you install the Application Insights package to monitor your app, you configure it with the instrumentation key, so that it knows where to send the telemetry.</span></span>

<span data-ttu-id="35127-113">Необходимость использования разных ресурсов или одного общего ресурса зависит от сценария:</span><span class="sxs-lookup"><span data-stu-id="35127-113">You typically choose to use separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="35127-114">Различные, независимые приложения: используйте отдельный ресурс и ключ инструментирования для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="35127-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="35127-115">Несколько компонентов или ролей одного бизнес-приложения: используйте [один общий ресурс](app-insights-monitor-multi-role-apps.md) для всех компонентов приложения.</span><span class="sxs-lookup"><span data-stu-id="35127-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all the component apps.</span></span> <span data-ttu-id="35127-116">Данные телеметрии можно фильтровать и сегментировать с помощью свойства cloud_RoleName.</span><span class="sxs-lookup"><span data-stu-id="35127-116">Telemetry can be filtered or segmented by the cloud_RoleName property.</span></span>
* <span data-ttu-id="35127-117">Разработка, тестирование и выпуск: используйте отдельный ресурс и ключ инструментирования для версий системы отдельных стадий (меток).</span><span class="sxs-lookup"><span data-stu-id="35127-117">Development, Test, and Release - Use a separate resource and ikey for versions of the system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="35127-118">Тестирование A или B. Используйте один ресурс.</span><span class="sxs-lookup"><span data-stu-id="35127-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="35127-119">Создайте TelemetryInitializer для добавления к телеметрии свойства, определяющего варианты.</span><span class="sxs-lookup"><span data-stu-id="35127-119">Create a TelemetryInitializer to add a property to the telemetry that identifies the variants.</span></span>


## <span data-ttu-id="35127-120"><a name="dynamic-ikey"></a> Динамический ключ инструментирования</span><span class="sxs-lookup"><span data-stu-id="35127-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="35127-121">Чтобы упростить изменение ключа инструментирования при перемещении кода между этапами производства, задавайте его в коде, а не в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="35127-121">To make it easier to change the ikey as the code moves between stages of production, set it in code instead of in the configuration file.</span></span>

<span data-ttu-id="35127-122">Задайте ключ в методе инициализации, таком как global.aspx.cs, в службе ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="35127-122">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="35127-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="35127-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="35127-124">В этом примере ключи инструментирования (ikey) для различных ресурсов приводятся в различных версиях файла веб-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="35127-124">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span></span> <span data-ttu-id="35127-125">При смене файла веб-конфигурации, что можно сделать в рамках сценария выпуска, сменится и целевой ресурс.</span><span class="sxs-lookup"><span data-stu-id="35127-125">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="35127-126">Веб-страницы</span><span class="sxs-lookup"><span data-stu-id="35127-126">Web pages</span></span>
<span data-ttu-id="35127-127">Ключ инструментирования iKey также используется в веб-страницах приложения, в [сценарии, который вы получили в колонке быстрого запуска](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="35127-127">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="35127-128">Вместо того чтобы вставлять его в код сценария напрямую, генерируйте его из состояния сервера.</span><span class="sxs-lookup"><span data-stu-id="35127-128">Instead of coding it literally into the script, generate it from the server state.</span></span> <span data-ttu-id="35127-129">Например, в приложении ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="35127-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="35127-130">*JavaScript в Razor*</span><span class="sxs-lookup"><span data-stu-id="35127-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="35127-131">Создание дополнительных ресурсов Application Insights</span><span class="sxs-lookup"><span data-stu-id="35127-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="35127-132">Чтобы разделить данные телеметрии для разных компонентов приложения или для разных меток (разработки, тестирования или эксплуатации) одного и того же компонента, вам понадобится создать новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="35127-132">To separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span></span>

<span data-ttu-id="35127-133">Перейдите по адресу [portal.azure.com](https://portal.azure.com)и добавьте новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="35127-133">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Нажмите "Создать" и "Application Insights"](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="35127-135">**Тип приложения** определяет содержимое колонки «Обзор» и свойства, доступные в [обозревателе метрик](app-insights-metrics-explorer.md)Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="35127-135">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="35127-136">Если тип вашего приложения не отображается, выберите тип веб-ресурса для веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="35127-136">If you don't see your type of app, choose one of the web types for web pages.</span></span>
* <span data-ttu-id="35127-137">**Группа ресурсов** — удобный способ для управления свойствами наподобие [контроля доступа](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="35127-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="35127-138">Для разработки, тестирования и эксплуатации можно использовать отдельные группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="35127-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="35127-139">**Подписка** представляет собой учетную запись для оплаты в Azure.</span><span class="sxs-lookup"><span data-stu-id="35127-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="35127-140">**Расположение** – это место, в котором мы храним ваши данные.</span><span class="sxs-lookup"><span data-stu-id="35127-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="35127-141">На данном этапе его нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="35127-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="35127-142">**Добавить на панель мониторинга** позволяет поместить плитку для быстрого доступа к ресурсу на главную страницу Azure.</span><span class="sxs-lookup"><span data-stu-id="35127-142">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="35127-143">Создание ресурса занимает всего несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="35127-143">Creating the resource takes a few seconds.</span></span> <span data-ttu-id="35127-144">Как только ресурс будет создан, появится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="35127-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="35127-145">(Для автоматического создания ресурсов можно написать [сценарий PowerShell](app-insights-powershell-script-create-resource.md) .)</span><span class="sxs-lookup"><span data-stu-id="35127-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span></span>

### <a name="getting-the-instrumentation-key"></a><span data-ttu-id="35127-146">Получение ключа инструментирования</span><span class="sxs-lookup"><span data-stu-id="35127-146">Getting the instrumentation key</span></span>
<span data-ttu-id="35127-147">Ключ инструментирования идентифицирует созданный вами ресурс.</span><span class="sxs-lookup"><span data-stu-id="35127-147">The instrumentation key identifies the resource that you created.</span></span> 

![Щелкните Essentials, выделите ключ инструментирования и нажмите клавиши CTRL + C.](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="35127-149">Вам потребуются ключи инструментирования всех ресурсов, в которые приложение будет отправлять данные.</span><span class="sxs-lookup"><span data-stu-id="35127-149">You need the instrumentation keys of all the resources to which your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="35127-150">Фильтрация по номеру сборки</span><span class="sxs-lookup"><span data-stu-id="35127-150">Filter on build number</span></span>
<span data-ttu-id="35127-151">При публикации новой версии приложения имеет смысл отделить телеметрию от других сборок.</span><span class="sxs-lookup"><span data-stu-id="35127-151">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span></span>

<span data-ttu-id="35127-152">Для этого можно настроить свойство "Версия приложения" для фильтрации результатов [поиска](app-insights-diagnostic-search.md) и [обозревателя метрик](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="35127-152">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Фильтрация по свойству](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="35127-154">Свойство «Версия приложения» можно настроить различными способами.</span><span class="sxs-lookup"><span data-stu-id="35127-154">There are several different methods of setting the Application Version property.</span></span>

* <span data-ttu-id="35127-155">Напрямую:</span><span class="sxs-lookup"><span data-stu-id="35127-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="35127-156">Вставьте эту строку в [инициализатор телеметрии](app-insights-api-custom-events-metrics.md#defaults) , чтобы обеспечить согласованность всех экземпляров TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="35127-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="35127-157">[ASP.NET] Задайте версию в `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="35127-157">[ASP.NET] Set the version in `BuildInfo.config`.</span></span> <span data-ttu-id="35127-158">Веб-модуль берет номер версии из узла BuildLabel.</span><span class="sxs-lookup"><span data-stu-id="35127-158">The web module will pick up the version from the BuildLabel node.</span></span> <span data-ttu-id="35127-159">Включите этот файл в проект и не забудьте установить свойство «Всегда копировать» в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="35127-159">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="35127-160">[ASP.NET] Настройте автоматическое создание файла BuildInfo.config в MSBuild.</span><span class="sxs-lookup"><span data-stu-id="35127-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="35127-161">Для этого добавьте в файл `.csproj` несколько строк:</span><span class="sxs-lookup"><span data-stu-id="35127-161">To do this, add a few lines to your `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="35127-162">Вы получите файл *Имя_проекта*.BuildInfo.config. В процессе публикации он переименовывается в BuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="35127-162">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span></span>

    <span data-ttu-id="35127-163">При создании сборки с помощью Visual Studio в подпись включается заполнитель (AutoGen_...).</span><span class="sxs-lookup"><span data-stu-id="35127-163">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="35127-164">Если используется MSBuild, в подписи указывается правильный номер версии.</span><span class="sxs-lookup"><span data-stu-id="35127-164">But when built with MSBuild, it is populated with the correct version number.</span></span>

    <span data-ttu-id="35127-165">Чтобы разрешить MSBuild генерировать номера версий, задайте версию вида `1.0.*` в файле AssemblyReference.cs.</span><span class="sxs-lookup"><span data-stu-id="35127-165">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="35127-166">Отслеживание версии и выпуска</span><span class="sxs-lookup"><span data-stu-id="35127-166">Version and release tracking</span></span>
<span data-ttu-id="35127-167">Для отслеживания версии приложения убедитесь, что во время выполнения процесса Microsoft Build Engine создается `buildinfo.config`.</span><span class="sxs-lookup"><span data-stu-id="35127-167">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="35127-168">Добавьте в CSPROJ-файл:</span><span class="sxs-lookup"><span data-stu-id="35127-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="35127-169">При наличии данных сборки веб-модуль Application Insights автоматически добавляет **версию приложения** как свойство для каждого элемента телеметрии.</span><span class="sxs-lookup"><span data-stu-id="35127-169">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span></span> <span data-ttu-id="35127-170">Это позволяет применить фильтр по версии при [диагностическом поиске](app-insights-diagnostic-search.md) или [изучении метрик](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="35127-170">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="35127-171">Обратите внимание, что номер версии сборки создается только Microsoft Build Engine, а не в процессе сборки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35127-171">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="35127-172">Примечания к выпуску</span><span class="sxs-lookup"><span data-stu-id="35127-172">Release annotations</span></span>
<span data-ttu-id="35127-173">Если используется Visual Studio Team Services, можно настроить [добавление маркера заметки](app-insights-annotations.md) к диаграммам при выпуске новой версии.</span><span class="sxs-lookup"><span data-stu-id="35127-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span></span> <span data-ttu-id="35127-174">На следующем рисунке показано, как появляется этот маркер.</span><span class="sxs-lookup"><span data-stu-id="35127-174">The following image shows how this marker appears.</span></span>

![Снимок экрана, где показана диаграмма с примером заметки о новом выпуске](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="35127-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="35127-176">Next steps</span></span>

* <span data-ttu-id="35127-177">[Monitor multi-component applications with Application Insights (preview)](app-insights-monitor-multi-role-apps.md) (Мониторинг приложений с несколькими компонентами с помощью Application Insights (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="35127-177">[Shared resources for multiple roles](app-insights-monitor-multi-role-apps.md)</span></span>
* [<span data-ttu-id="35127-178">Добавление свойств: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="35127-178">Create a Telemetry Initializer to distinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
