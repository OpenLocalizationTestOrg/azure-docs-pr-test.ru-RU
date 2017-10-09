---
title: "aaaSeparating телеметрии из среды разработки, тестирования и выпуска в Azure Application Insights | Документы Microsoft"
description: "Прямой телеметрии toodifferent ресурсы для разработки, тестирования и эксплуатации отметки."
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
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="3fe64-103">Отделение телеметрии стадий разработки, тестирования и эксплуатации</span><span class="sxs-lookup"><span data-stu-id="3fe64-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="3fe64-104">При разработке hello следующей версии веб-приложение, вы не хотите toomix копирование hello [Application Insights](app-insights-overview.md) телеметрии из hello новой версии и версии hello уже освобожден.</span><span class="sxs-lookup"><span data-stu-id="3fe64-104">When you are developing hello next version of a web application, you don't want toomix up hello [Application Insights](app-insights-overview.md) telemetry from hello new version and hello already released version.</span></span> <span data-ttu-id="3fe64-105">путаницы tooavoid отправки данных телеметрии hello разработки готовит tooseparate ресурсы Application Insights, ключи отдельные инструментария (ikeys).</span><span class="sxs-lookup"><span data-stu-id="3fe64-105">tooavoid confusion, send hello telemetry from different development stages tooseparate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="3fe64-106">toomake его проще ключ инструментирования hello toochange как версия перемещает из tooanother один этап, это может быть полезно tooset ikey hello в коде, а не в файле конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="3fe64-106">toomake it easier toochange hello instrumentation key as a version moves from one stage tooanother, it can be useful tooset hello ikey in code instead of in hello configuration file.</span></span> 

<span data-ttu-id="3fe64-107">(Если вы используете облачную службу Azure, есть [другой метод настройки отдельных ключей инструментирования ikey](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="3fe64-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="3fe64-108">Ресурсы и ключи инструментирования</span><span class="sxs-lookup"><span data-stu-id="3fe64-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="3fe64-109">При настройке мониторинга Application Insights для веб-приложения вы создаете *ресурс* Application Insights в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe64-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="3fe64-110">Открыть этот ресурс в портал Azure в порядке toosee hello и анализ телеметрии hello, собранная из приложения.</span><span class="sxs-lookup"><span data-stu-id="3fe64-110">You open this resource in hello Azure portal in order toosee and analyze hello telemetry collected from your app.</span></span> <span data-ttu-id="3fe64-111">Hello ресурсов определяется *ключ инструментирования* (ikey).</span><span class="sxs-lookup"><span data-stu-id="3fe64-111">hello resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="3fe64-112">При установке hello Application Insights пакета toomonitor приложения, нужно настроить его с ключом инструментирования hello, чтобы он знал, где toosend hello телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3fe64-112">When you install hello Application Insights package toomonitor your app, you configure it with hello instrumentation key, so that it knows where toosend hello telemetry.</span></span>

<span data-ttu-id="3fe64-113">Обычно выбрать отдельные ресурсы toouse или одного общего ресурса в различных сценариях:</span><span class="sxs-lookup"><span data-stu-id="3fe64-113">You typically choose toouse separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="3fe64-114">Различные, независимые приложения: используйте отдельный ресурс и ключ инструментирования для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="3fe64-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="3fe64-115">Использование нескольких компонентов или ролей приложения один бизнес - [один общий ресурс](app-insights-monitor-multi-role-apps.md) для всех hello компонента приложения.</span><span class="sxs-lookup"><span data-stu-id="3fe64-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all hello component apps.</span></span> <span data-ttu-id="3fe64-116">Можно выполнять фильтрацию и сегментируются свойством cloud_RoleName hello телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3fe64-116">Telemetry can be filtered or segmented by hello cloud_RoleName property.</span></span>
* <span data-ttu-id="3fe64-117">Разработка, тестирование и выпуски - использовать отдельный ресурс и ikey для версии системы hello, «метки» или этапа производства.</span><span class="sxs-lookup"><span data-stu-id="3fe64-117">Development, Test, and Release - Use a separate resource and ikey for versions of hello system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="3fe64-118">Тестирование A или B. Используйте один ресурс.</span><span class="sxs-lookup"><span data-stu-id="3fe64-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="3fe64-119">Создайте TelemetryInitializer tooadd телеметрии toohello свойство, идентифицирующее hello вариантов.</span><span class="sxs-lookup"><span data-stu-id="3fe64-119">Create a TelemetryInitializer tooadd a property toohello telemetry that identifies hello variants.</span></span>


## <span data-ttu-id="3fe64-120"><a name="dynamic-ikey"></a> Динамический ключ инструментирования</span><span class="sxs-lookup"><span data-stu-id="3fe64-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="3fe64-121">toomake упрощение ikey hello toochange как код hello перемещается между этапы производства, заданы в коде, а не в файле конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="3fe64-121">toomake it easier toochange hello ikey as hello code moves between stages of production, set it in code instead of in hello configuration file.</span></span>

<span data-ttu-id="3fe64-122">Установите раздел hello в метод инициализации, например global.aspx.cs в службы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3fe64-122">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="3fe64-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="3fe64-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="3fe64-124">В этом примере hello ikeys для разных ресурсов hello размещаются в различных версиях hello файл веб-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3fe64-124">In this example, hello ikeys for hello different resources are placed in different versions of hello web configuration file.</span></span> <span data-ttu-id="3fe64-125">Идет обмен файл веб-конфигурации hello - это можно сделать в скрипте выпуска hello - поменяет hello целевого ресурса.</span><span class="sxs-lookup"><span data-stu-id="3fe64-125">Swapping hello web configuration file - which you can do as part of hello release script - will swap hello target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="3fe64-126">Веб-страницы</span><span class="sxs-lookup"><span data-stu-id="3fe64-126">Web pages</span></span>
<span data-ttu-id="3fe64-127">Hello iKey также используется в веб-страницы приложения в hello [скрипт, который получен из колонки быстрого запуска hello](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="3fe64-127">hello iKey is also used in your app's web pages, in hello [script that you got from hello quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="3fe64-128">Вместо написания его буквально в сценарий hello, создайте его hello состояния сервера.</span><span class="sxs-lookup"><span data-stu-id="3fe64-128">Instead of coding it literally into hello script, generate it from hello server state.</span></span> <span data-ttu-id="3fe64-129">Например, в приложении ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="3fe64-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="3fe64-130">*JavaScript в Razor*</span><span class="sxs-lookup"><span data-stu-id="3fe64-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="3fe64-131">Создание дополнительных ресурсов Application Insights</span><span class="sxs-lookup"><span data-stu-id="3fe64-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="3fe64-132">tooseparate телеметрии для разные компоненты приложения или для разных метках (разработки или тестирования и рабочего) hello одного компонента, то получите toocreate новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3fe64-132">tooseparate telemetry for different application components, or for different stamps (dev/test/production) of hello same component, then you'll have toocreate a new Application Insights resource.</span></span>

<span data-ttu-id="3fe64-133">В hello [portal.azure.com](https://portal.azure.com), добавьте ресурс Application Insights:</span><span class="sxs-lookup"><span data-stu-id="3fe64-133">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Нажмите "Создать" и "Application Insights"](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="3fe64-135">**Тип приложения** влияет на содержимое, отображаемое на колонки Обзор hello и hello свойств, доступных в [метрики обозревателя](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="3fe64-135">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="3fe64-136">Если вы не видите того или иного типа приложения, выберите один из типов web hello для веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="3fe64-136">If you don't see your type of app, choose one of hello web types for web pages.</span></span>
* <span data-ttu-id="3fe64-137">**Группа ресурсов** — удобный способ для управления свойствами наподобие [контроля доступа](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="3fe64-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="3fe64-138">Для разработки, тестирования и эксплуатации можно использовать отдельные группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3fe64-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="3fe64-139">**Подписка** представляет собой учетную запись для оплаты в Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe64-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="3fe64-140">**Расположение** – это место, в котором мы храним ваши данные.</span><span class="sxs-lookup"><span data-stu-id="3fe64-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="3fe64-141">На данном этапе его нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="3fe64-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="3fe64-142">**Добавить toodashboard** помещает плитки быстрого доступа для ресурса на Azure домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="3fe64-142">**Add toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="3fe64-143">Создание ресурса hello занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="3fe64-143">Creating hello resource takes a few seconds.</span></span> <span data-ttu-id="3fe64-144">Как только ресурс будет создан, появится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="3fe64-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="3fe64-145">(Можно написать [сценарий PowerShell](app-insights-powershell-script-create-resource.md) toocreate ресурс автоматически.)</span><span class="sxs-lookup"><span data-stu-id="3fe64-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) toocreate a resource automatically.)</span></span>

### <a name="getting-hello-instrumentation-key"></a><span data-ttu-id="3fe64-146">Получение ключа инструментирования hello</span><span class="sxs-lookup"><span data-stu-id="3fe64-146">Getting hello instrumentation key</span></span>
<span data-ttu-id="3fe64-147">ключ инструментирования Hello идентифицирует созданный ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="3fe64-147">hello instrumentation key identifies hello resource that you created.</span></span> 

![Установите Essentials, щелкните hello ключ инструментирования, CTRL + C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="3fe64-149">Требуются ключи hello инструментирования из всех toowhich hello ресурсов приложения будет отправлять данные.</span><span class="sxs-lookup"><span data-stu-id="3fe64-149">You need hello instrumentation keys of all hello resources toowhich your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="3fe64-150">Фильтрация по номеру сборки</span><span class="sxs-lookup"><span data-stu-id="3fe64-150">Filter on build number</span></span>
<span data-ttu-id="3fe64-151">При публикации новой версии приложения, будет необходимо toobe может tooseparate hello телеметрии из другой сборки.</span><span class="sxs-lookup"><span data-stu-id="3fe64-151">When you publish a new version of your app, you'll want toobe able tooseparate hello telemetry from different builds.</span></span>

<span data-ttu-id="3fe64-152">Можно задать свойства версии приложения hello так, что позволяет фильтровать [поиска](app-insights-diagnostic-search.md) и [метрики explorer](app-insights-metrics-explorer.md) результаты.</span><span class="sxs-lookup"><span data-stu-id="3fe64-152">You can set hello Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Фильтрация по свойству](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="3fe64-154">Существует несколько разных способов задания свойства версии приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3fe64-154">There are several different methods of setting hello Application Version property.</span></span>

* <span data-ttu-id="3fe64-155">Напрямую:</span><span class="sxs-lookup"><span data-stu-id="3fe64-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="3fe64-156">Перенос эту строку в [инициализатора телеметрии](app-insights-api-custom-events-metrics.md#defaults) tooensure, все экземпляры TelemetryClient установлены постоянно.</span><span class="sxs-lookup"><span data-stu-id="3fe64-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) tooensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="3fe64-157">[ASP.NET] Версия набора hello в `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="3fe64-157">[ASP.NET] Set hello version in `BuildInfo.config`.</span></span> <span data-ttu-id="3fe64-158">веб-модуль Hello получат версии hello из узла BuildLabel hello.</span><span class="sxs-lookup"><span data-stu-id="3fe64-158">hello web module will pick up hello version from hello BuildLabel node.</span></span> <span data-ttu-id="3fe64-159">Включить этот файл в проект и запоминать tooset hello всегда Копировать свойства в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="3fe64-159">Include this file in your project and remember tooset hello Copy Always property in Solution Explorer.</span></span>

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
* <span data-ttu-id="3fe64-160">[ASP.NET] Настройте автоматическое создание файла BuildInfo.config в MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3fe64-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="3fe64-161">toodo это, добавьте несколько строк tooyour `.csproj` файла:</span><span class="sxs-lookup"><span data-stu-id="3fe64-161">toodo this, add a few lines tooyour `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="3fe64-162">Будет создан файл с именем *yourProjectName*. Hello BuildInfo.config. процесс публикации переименовывает его tooBuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="3fe64-162">This generates a file called *yourProjectName*.BuildInfo.config. hello Publish process renames it tooBuildInfo.config.</span></span>

    <span data-ttu-id="3fe64-163">Метка сборки Hello содержит заполнитель (AutoGen_), при построении с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fe64-163">hello build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="3fe64-164">Однако при построении с помощью MSBuild, он заполняется hello правильный номер версии.</span><span class="sxs-lookup"><span data-stu-id="3fe64-164">But when built with MSBuild, it is populated with hello correct version number.</span></span>

    <span data-ttu-id="3fe64-165">как версии набора hello tooallow номера версий MSBuild toogenerate `1.0.*` в AssemblyReference.cs</span><span class="sxs-lookup"><span data-stu-id="3fe64-165">tooallow MSBuild toogenerate version numbers, set hello version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="3fe64-166">Отслеживание версии и выпуска</span><span class="sxs-lookup"><span data-stu-id="3fe64-166">Version and release tracking</span></span>
<span data-ttu-id="3fe64-167">версия приложения hello tootrack, убедитесь, что `buildinfo.config` создается процессом Microsoft Build Engine.</span><span class="sxs-lookup"><span data-stu-id="3fe64-167">tootrack hello application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="3fe64-168">Добавьте в CSPROJ-файл:</span><span class="sxs-lookup"><span data-stu-id="3fe64-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="3fe64-169">Когда в нем сведения сборки hello, веб-модуля hello Application Insights автоматически добавляет **версия приложения** как элемент свойства tooevery телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3fe64-169">When it has hello build info, hello Application Insights web module automatically adds **Application version** as a property tooevery item of telemetry.</span></span> <span data-ttu-id="3fe64-170">Позволяющее вам toofilter версии при выполнении [диагностики выполняет](app-insights-diagnostic-search.md), или если вы [Просмотр метрик](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="3fe64-170">That allows you toofilter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="3fe64-171">Тем не менее Обратите внимание, что номер версии сборки hello формируется только hello Microsoft Build Engine, не разработчиком hello построения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fe64-171">However, notice that hello build version number is generated only by hello Microsoft Build Engine, not by hello developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="3fe64-172">Примечания к выпуску</span><span class="sxs-lookup"><span data-stu-id="3fe64-172">Release annotations</span></span>
<span data-ttu-id="3fe64-173">Если вы используете Visual Studio Team Services, вы можете [получить маркер заметки](app-insights-annotations.md) добавляется tooyour диаграммы, при выпуске новой версии.</span><span class="sxs-lookup"><span data-stu-id="3fe64-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added tooyour charts whenever you release a new version.</span></span> <span data-ttu-id="3fe64-174">Следующие изображения Hello показано, как выглядит этот маркер.</span><span class="sxs-lookup"><span data-stu-id="3fe64-174">hello following image shows how this marker appears.</span></span>

![Снимок экрана, где показана диаграмма с примером заметки о новом выпуске](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="3fe64-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3fe64-176">Next steps</span></span>

* <span data-ttu-id="3fe64-177">[Monitor multi-component applications with Application Insights (preview)](app-insights-monitor-multi-role-apps.md) (Мониторинг приложений с несколькими компонентами с помощью Application Insights (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="3fe64-177">[Shared resources for multiple roles](app-insights-monitor-multi-role-apps.md)</span></span>
* [<span data-ttu-id="3fe64-178">Создание toodistinguish инициализатора телеметрии A | Варианты B</span><span class="sxs-lookup"><span data-stu-id="3fe64-178">Create a Telemetry Initializer toodistinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
