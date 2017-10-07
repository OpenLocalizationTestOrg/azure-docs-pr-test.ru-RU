---
title: "aaaAzure Application Insights поддерживает несколько компонентов, микрослужбами и контейнеры | Документы Microsoft"
description: "Мониторинг приложений, которые состоят из нескольких компонентов или ролей, для получения данных производительности и использования."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="a6cff-103">Мониторинг приложений с несколькими компонентами с помощью Application Insights (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="a6cff-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="a6cff-104">Вы можете отслеживать приложения, которые состоят из нескольких серверных компонентов, ролей или служб, с помощью [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6cff-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="a6cff-105">Hello работоспособности компонентов hello и hello связи между ними, отображаются на карте одного приложения.</span><span class="sxs-lookup"><span data-stu-id="a6cff-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="a6cff-106">Вы можете отслеживать отдельные операции для нескольких компонентов за счет автоматической корреляции HTTP.</span><span class="sxs-lookup"><span data-stu-id="a6cff-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="a6cff-107">Диагностика контейнеров может быть интегрирована и сопоставлена с телеметрией приложения.</span><span class="sxs-lookup"><span data-stu-id="a6cff-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="a6cff-108">Используйте один ресурс Application Insights для всех компонентов приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a6cff-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![Схема сопоставления многокомпонентных приложений](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="a6cff-110">Мы используем «компонент» здесь toomean любой работающую часть большого приложения.</span><span class="sxs-lookup"><span data-stu-id="a6cff-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="a6cff-111">Например типичный бизнес-приложений может состоять из клиентского кода, выполняемого в веб-браузерами, идет речь tooone или дополнительные веб-приложения служб, которые в свою очередь, используют обратно завершения службы.</span><span class="sxs-lookup"><span data-stu-id="a6cff-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="a6cff-112">Компоненты сервера может быть размещена локально на в облаке hello или может быть Azure рабочих и веб-ролей может работать в контейнерах, например Docker или Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a6cff-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="a6cff-113">Совместное использование одного ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="a6cff-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="a6cff-114">Hello ключа методикой является toosend телеметрии из вашего приложения toohello каждый компонент одного ресурса Application Insights, но использование hello `cloud_RoleName` свойство toodistinguish компоненты при необходимости.</span><span class="sxs-lookup"><span data-stu-id="a6cff-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="a6cff-115">пакет SDK для Application Insights Hello добавляет hello `cloud_RoleName` порождение свойство toohello телеметрии компонентов.</span><span class="sxs-lookup"><span data-stu-id="a6cff-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="a6cff-116">Например, добавление hello SDK, имя веб-сайта или toohello имя службы роли `cloud_RoleName` свойство.</span><span class="sxs-lookup"><span data-stu-id="a6cff-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="a6cff-117">Это значение можно переопределить с помощью telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="a6cff-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="a6cff-118">Сопоставления приложения Hello использует hello `cloud_RoleName` свойство tooidentify hello компоненты на карте hello.</span><span class="sxs-lookup"><span data-stu-id="a6cff-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="a6cff-119">Дополнительные сведения о том, как переопределить hello `cloud_RoleName` см. свойство [добавлять свойства: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="a6cff-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="a6cff-120">В некоторых случаях это может быть неприемлемо, и могут предпочесть toouse отдельные ресурсы для разных групп компонентов.</span><span class="sxs-lookup"><span data-stu-id="a6cff-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="a6cff-121">Например может потребоваться toouse различные ресурсы для управления или составления счетов.</span><span class="sxs-lookup"><span data-stu-id="a6cff-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="a6cff-122">Использование разных ресурсах означает, что вы не видите все компоненты hello, отображаемые на карте одного приложения; и что не удается запросить во всех компонентах в [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="a6cff-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="a6cff-123">Также имеется tooset hello отдельных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a6cff-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="a6cff-124">С этой оговорка мы предположим, в hello остальной части этого документа, вы должны toosend данные из нескольких компонентов tooone ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a6cff-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="a6cff-125">Настройка многокомпонентных приложений</span><span class="sxs-lookup"><span data-stu-id="a6cff-125">Configure multi-component applications</span></span>

<span data-ttu-id="a6cff-126">сопоставление tooget многокомпонентные приложения, вы должны tooachieve этих целей:</span><span class="sxs-lookup"><span data-stu-id="a6cff-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="a6cff-127">**Установить последнюю предварительную hello** пакета Application Insights в каждом компоненте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a6cff-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="a6cff-128">**Совместно использовать один ресурс Application Insights** для всех hello компоненты приложения.</span><span class="sxs-lookup"><span data-stu-id="a6cff-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="a6cff-129">**Включить сопоставление нескольких ролей приложения** в колонке hello предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="a6cff-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="a6cff-130">Настройте каждый компонент приложения с помощью hello соответствующий метод для его типа.</span><span class="sxs-lookup"><span data-stu-id="a6cff-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="a6cff-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md)).</span><span class="sxs-lookup"><span data-stu-id="a6cff-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="a6cff-132">1. Установите последнюю версию пакета предварительного выпуска hello</span><span class="sxs-lookup"><span data-stu-id="a6cff-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="a6cff-133">Обновление или установка пакетов аналитики приложений hello в проекте hello для каждого компонента сервера.</span><span class="sxs-lookup"><span data-stu-id="a6cff-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="a6cff-134">Если вы используете Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a6cff-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="a6cff-135">Щелкните проект правой кнопкой мыши и выберите **Управление пакетами Nuget**.</span><span class="sxs-lookup"><span data-stu-id="a6cff-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="a6cff-136">Выберите параметр **Включить предварительные выпуски**.</span><span class="sxs-lookup"><span data-stu-id="a6cff-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="a6cff-137">Если пакеты Application Insights отображаются в списке обновлений, выберите их.</span><span class="sxs-lookup"><span data-stu-id="a6cff-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="a6cff-138">В противном случае — найти и установить соответствующий пакет hello:</span><span class="sxs-lookup"><span data-stu-id="a6cff-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="a6cff-139">Microsoft.ApplicationInsights.WindowsServer;</span><span class="sxs-lookup"><span data-stu-id="a6cff-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="a6cff-140">Microsoft.ApplicationInsights.ServiceFabric — для компонентов, выполняющихся в качестве гостевых исполняемых файлов, и контейнеров Docker, работающих в приложениях Service Fabric;</span><span class="sxs-lookup"><span data-stu-id="a6cff-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="a6cff-141">Microsoft.ApplicationInsights.ServiceFabric.Native — для надежных служб в приложениях ServiceFabric;</span><span class="sxs-lookup"><span data-stu-id="a6cff-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="a6cff-142">Microsoft.ApplicationInsights.Kubernetes — для компонентов, выполняемых в Docker на Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a6cff-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="a6cff-143">2. Настройка совместного использования одного ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="a6cff-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="a6cff-144">В Visual Studio щелкните проект правой кнопкой мыши и выберите **Настроить Application Insights** или **Application Insights > Настроить**.</span><span class="sxs-lookup"><span data-stu-id="a6cff-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="a6cff-145">Для первого проекта hello используйте мастер hello toocreate ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a6cff-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="a6cff-146">Для последующих проектов выберите hello того же ресурса.</span><span class="sxs-lookup"><span data-stu-id="a6cff-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="a6cff-147">Если вы не видите меню Application Insights, выполните настройку вручную:</span><span class="sxs-lookup"><span data-stu-id="a6cff-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="a6cff-148">В [портал Azure](https://portal,azure.com), открыть ресурс Application Insights hello уже создан для другого компонента.</span><span class="sxs-lookup"><span data-stu-id="a6cff-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="a6cff-149">В колонке Обзор hello, вкладку Привет открыть Essentials раскрывающегося списка и копирования hello **ключ инструментирования.**</span><span class="sxs-lookup"><span data-stu-id="a6cff-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="a6cff-150">В своем проекте откройте файл ApplicationInsights.config и вставьте: `<InstrumentationKey>your copied key</InstrumentationKey>`.</span><span class="sxs-lookup"><span data-stu-id="a6cff-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Скопируйте файл .config toohello ключа инструментирования hello](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="a6cff-152">3. Включение схемы сопоставления приложений с несколькими ролями</span><span class="sxs-lookup"><span data-stu-id="a6cff-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="a6cff-153">Hello портал Azure откройте hello ресурса для приложения.</span><span class="sxs-lookup"><span data-stu-id="a6cff-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="a6cff-154">В колонке hello предварительные версии, включите *карты несколькими ролями приложения*.</span><span class="sxs-lookup"><span data-stu-id="a6cff-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="a6cff-155">4. Включение метрик Docker (необязательно)</span><span class="sxs-lookup"><span data-stu-id="a6cff-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="a6cff-156">Если компонент работает в Docker, размещенной на виртуальной Машине Windows Azure, вы можете собирать дополнительные метрики из контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="a6cff-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="a6cff-157">Вставьте в файл конфигурации [системы диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics.md) следующий код:</span><span class="sxs-lookup"><span data-stu-id="a6cff-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="a6cff-158">Использование компонентов tooseparate cloud_RoleName</span><span class="sxs-lookup"><span data-stu-id="a6cff-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="a6cff-159">Hello `cloud_RoleName` свойство имеет вложенные tooall телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a6cff-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="a6cff-160">Он идентифицирует компонент hello - hello роли или службы -, рассчитанная телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="a6cff-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="a6cff-161">(Это не Здравствуйте таким же, как cloud_RoleInstance, который отделяет идентичные роли, которые выполняются параллельно на несколько серверных процессов или машины.)</span><span class="sxs-lookup"><span data-stu-id="a6cff-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="a6cff-162">На портале hello можно отфильтровать или сегментирования телеметрии с помощью этого свойства.</span><span class="sxs-lookup"><span data-stu-id="a6cff-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="a6cff-163">В этом примере hello сбоев колонка находится отфильтрованные tooshow только сведения из hello интерфейсный веб-службы, отфильтровывая сбоев из внутренних CRM API hello:</span><span class="sxs-lookup"><span data-stu-id="a6cff-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![Диаграмма метрик, сегментированная по имени облачной роли](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="a6cff-165">Отслеживание операций между компонентами</span><span class="sxs-lookup"><span data-stu-id="a6cff-165">Trace operations between components</span></span>

<span data-ttu-id="a6cff-166">Можно выполнить трассировку из одного компонента tooanother, hello вызовы, сделанные во время обработки отдельной операции.</span><span class="sxs-lookup"><span data-stu-id="a6cff-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![Отображение данных телеметрии для операции](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="a6cff-168">Пролистайте список коррелированные tooa телеметрии для этой операции через hello интерфейсного веб-сервера и внутреннего интерфейса API hello:</span><span class="sxs-lookup"><span data-stu-id="a6cff-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![Поиск по компонентам](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="a6cff-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a6cff-170">Next steps</span></span>

* [<span data-ttu-id="a6cff-171">Отделение телеметрии стадий разработки, тестирования и эксплуатации</span><span class="sxs-lookup"><span data-stu-id="a6cff-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
