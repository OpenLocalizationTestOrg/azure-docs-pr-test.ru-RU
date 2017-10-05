---
title: "Поддержка нескольких компонентов, микрослужб и контейнеров в Azure Application Insights | Документы Майкрософт"
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
ms.openlocfilehash: ca1bb8ee886c4b4e69be9dd653d6a52b874e1f5a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="7b2cd-103">Мониторинг приложений с несколькими компонентами с помощью Application Insights (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="7b2cd-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="7b2cd-104">Вы можете отслеживать приложения, которые состоят из нескольких серверных компонентов, ролей или служб, с помощью [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b2cd-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="7b2cd-105">Работоспособность компонентов и связи между ними отображаются на единой схеме сопоставления приложений.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-105">The health of the components and the relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="7b2cd-106">Вы можете отслеживать отдельные операции для нескольких компонентов за счет автоматической корреляции HTTP.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="7b2cd-107">Диагностика контейнеров может быть интегрирована и сопоставлена с телеметрией приложения.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="7b2cd-108">Используйте единый ресурс Application Insights для всех компонентов в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-108">Use a single Application Insights resource for all the components of your application.</span></span> 

![Схема сопоставления многокомпонентных приложений](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="7b2cd-110">Под компонентом здесь подразумевается любая функциональная часть большого приложения.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-110">We use 'component' here to mean any functioning part of a large application.</span></span> <span data-ttu-id="7b2cd-111">Например, типичное бизнес-приложение может состоять из клиентского кода, выполняемого в веб-браузерах и взаимодействующего с одной или несколькими службами веб-приложения, которые, в свою очередь, используют серверные службы.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-111">For example, a typical business application may consist of client code running in web browsers, talking to one or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="7b2cd-112">Серверные компоненты могут размещаться в локальной среде или в облаке, представлять собой веб-роли и рабочие роли Azure или выполняться в контейнерах, таких как Docker или Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-112">Server components may be hosted on-premises on in the cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="7b2cd-113">Совместное использование одного ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="7b2cd-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="7b2cd-114">Ключевой метод здесь — отправлять телеметрию каждого компонента в приложении в тот же ресурс Application Insights, но использовать свойство `cloud_RoleName`, чтобы различать компоненты, когда это необходимо.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-114">The key technique here is to send telemetry from every component in your application to the same Application Insights resource, but use the `cloud_RoleName` property to distinguish components when necessary.</span></span> <span data-ttu-id="7b2cd-115">Пакет SDK для Application Insights добавляет свойство `cloud_RoleName` в данные телеметрии, выдаваемые компонентами.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-115">The Application Insights SDK adds the `cloud_RoleName` property to the telemetry components emit.</span></span> <span data-ttu-id="7b2cd-116">Например, пакет SDK добавит имя веб-сайта или роли службы в свойство `cloud_RoleName`.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-116">For example, the SDK will add a web site name, or service role name to the `cloud_RoleName` property.</span></span> <span data-ttu-id="7b2cd-117">Это значение можно переопределить с помощью telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="7b2cd-118">В схеме сопоставления приложений свойство `cloud_RoleName` используется для идентификации компонентов в схеме.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-118">The Application Map uses the `cloud_RoleName` property to identify the components on the map.</span></span>

<span data-ttu-id="7b2cd-119">Дополнительные сведения о том, как переопределить свойство `cloud_RoleName`, см. в разделе [Добавление свойств: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="7b2cd-119">For more information about how do override the `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="7b2cd-120">В некоторых случаях это может быть неуместным, и вы можете использовать отдельные ресурсы для разных групп компонентов.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-120">In some cases, this may not be appropriate, and you may prefer to use separate resources for different groups of components.</span></span> <span data-ttu-id="7b2cd-121">Например, вам может потребоваться использовать разные ресурсы для управления и выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-121">For example, you might need to use different resources for management or billing purposes.</span></span> <span data-ttu-id="7b2cd-122">Использование отдельных ресурсов означает, что вы не видите все отображаемые компоненты на единой схеме сопоставления приложений и не можете запрашивать по компонентам в [аналитике](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="7b2cd-122">Using separate resources means that you don't see all the components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="7b2cd-123">Кроме того, отдельные ресурсы необходимо настроить.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-123">You also have to set up the separate resources.</span></span>

<span data-ttu-id="7b2cd-124">Исходя из этого, в оставшейся части этого документа рассматривается отправка данных из нескольких компонентов в один ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-124">With that caveat, we'll assume in the rest of this document that you want to send data from multiple components to one Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="7b2cd-125">Настройка многокомпонентных приложений</span><span class="sxs-lookup"><span data-stu-id="7b2cd-125">Configure multi-component applications</span></span>

<span data-ttu-id="7b2cd-126">Чтобы получить схему сопоставления приложений с несколькими компонентами, вам потребуется выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="7b2cd-126">To get a multi-component application map, you need to achieve these goals:</span></span>

* <span data-ttu-id="7b2cd-127">**установить последнюю предварительную версию** пакета Application Insights в каждом компоненте приложения;</span><span class="sxs-lookup"><span data-stu-id="7b2cd-127">**Install the latest pre-release** Application Insights package in each component of the application.</span></span> 
* <span data-ttu-id="7b2cd-128">**использовать единый ресурс Application Insights** для всех компонентов в вашем приложении;</span><span class="sxs-lookup"><span data-stu-id="7b2cd-128">**Share a single Application Insights resource** for all the components of your application.</span></span>
* <span data-ttu-id="7b2cd-129">**включить схему сопоставления приложений с несколькими ролями** в колонке "Предварительный просмотр".</span><span class="sxs-lookup"><span data-stu-id="7b2cd-129">**Enable Multi-role Application Map** in the Previews blade.</span></span>

<span data-ttu-id="7b2cd-130">Настройте каждый компонент своего приложения, используя соответствующий метод для его типа</span><span class="sxs-lookup"><span data-stu-id="7b2cd-130">Configure each component of your application using the appropriate method for its type.</span></span> <span data-ttu-id="7b2cd-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md)).</span><span class="sxs-lookup"><span data-stu-id="7b2cd-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-the-latest-pre-release-package"></a><span data-ttu-id="7b2cd-132">1. Установка последней предварительной версии пакета</span><span class="sxs-lookup"><span data-stu-id="7b2cd-132">1. Install the latest pre-release package</span></span>

<span data-ttu-id="7b2cd-133">Установите пакеты Appication Insights или обновите их для каждого серверного компонента в проекте.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-133">Update or install the Appication Insights packages in the project for each server component.</span></span> <span data-ttu-id="7b2cd-134">Если вы используете Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="7b2cd-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="7b2cd-135">Щелкните проект правой кнопкой мыши и выберите **Управление пакетами Nuget**.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="7b2cd-136">Выберите параметр **Включить предварительные выпуски**.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="7b2cd-137">Если пакеты Application Insights отображаются в списке обновлений, выберите их.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="7b2cd-138">В противном случае найдите и установите соответствующий пакет:</span><span class="sxs-lookup"><span data-stu-id="7b2cd-138">Otherwise, browse for and install the appropriate package:</span></span>
    
    * <span data-ttu-id="7b2cd-139">Microsoft.ApplicationInsights.WindowsServer;</span><span class="sxs-lookup"><span data-stu-id="7b2cd-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="7b2cd-140">Microsoft.ApplicationInsights.ServiceFabric — для компонентов, выполняющихся в качестве гостевых исполняемых файлов, и контейнеров Docker, работающих в приложениях Service Fabric;</span><span class="sxs-lookup"><span data-stu-id="7b2cd-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="7b2cd-141">Microsoft.ApplicationInsights.ServiceFabric.Native — для надежных служб в приложениях ServiceFabric;</span><span class="sxs-lookup"><span data-stu-id="7b2cd-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="7b2cd-142">Microsoft.ApplicationInsights.Kubernetes — для компонентов, выполняемых в Docker на Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="7b2cd-143">2. Настройка совместного использования одного ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="7b2cd-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="7b2cd-144">В Visual Studio щелкните проект правой кнопкой мыши и выберите **Настроить Application Insights** или **Application Insights > Настроить**.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="7b2cd-145">Для первого проекта используйте мастер для создания ресурса Application Insights,</span><span class="sxs-lookup"><span data-stu-id="7b2cd-145">For the first project, use the wizard to create an Application Insights resource.</span></span> <span data-ttu-id="7b2cd-146">а для последующих проектов выбирайте тот же ресурс.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-146">For subsequent projects, select the same resource.</span></span>
* <span data-ttu-id="7b2cd-147">Если вы не видите меню Application Insights, выполните настройку вручную:</span><span class="sxs-lookup"><span data-stu-id="7b2cd-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="7b2cd-148">На [портале Azure](https://portal,azure.com) откройте ресурс Application Insights, который вы уже создали для другого компонента.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-148">In [Azure portal](https://portal,azure.com), open the Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="7b2cd-149">В колонке "Обзор" щелкните раскрывающуюся вкладку "Основные компоненты" и скопируйте **ключ инструментирования**.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-149">In the Overview blade, open the Essentials drop-down tab, and copy the **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="7b2cd-150">В своем проекте откройте файл ApplicationInsights.config и вставьте: `<InstrumentationKey>your copied key</InstrumentationKey>`.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Скопируйте ключ инструментирования в CONFIG-файл.](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="7b2cd-152">3. Включение схемы сопоставления приложений с несколькими ролями</span><span class="sxs-lookup"><span data-stu-id="7b2cd-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="7b2cd-153">На портале Azure откройте ресурс для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-153">In the Azure portal, open the resource for your application.</span></span> <span data-ttu-id="7b2cd-154">Включите *схему сопоставления приложений с несколькими ролями* в колонке "Предварительный просмотр".</span><span class="sxs-lookup"><span data-stu-id="7b2cd-154">In the Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="7b2cd-155">4. Включение метрик Docker (необязательно)</span><span class="sxs-lookup"><span data-stu-id="7b2cd-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="7b2cd-156">Если компонент выполняется в Docker, который размещен в виртуальной машине Azure с ОС Windows, вы можете собрать дополнительные метрики из контейнера.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from the container.</span></span> <span data-ttu-id="7b2cd-157">Вставьте в файл конфигурации [системы диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics.md) следующий код:</span><span class="sxs-lookup"><span data-stu-id="7b2cd-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

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

## <a name="use-cloudrolename-to-separate-components"></a><span data-ttu-id="7b2cd-158">Использование свойства cloud_RoleName для разделения компонентов</span><span class="sxs-lookup"><span data-stu-id="7b2cd-158">Use cloud_RoleName to separate components</span></span>

<span data-ttu-id="7b2cd-159">Свойство `cloud_RoleName` присоединяется ко всей телеметрии.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-159">The `cloud_RoleName` property is attached to all telemetry.</span></span> <span data-ttu-id="7b2cd-160">Оно идентифицирует компонент (роль или службу), который создает телеметрию.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-160">It identifies the component - the role or service - that originates the telemetry.</span></span> <span data-ttu-id="7b2cd-161">(Оно отличается от свойства cloud_RoleInstance, которое разделяет идентичные роли, которые выполняются параллельно в нескольких процессах сервера или на нескольких машинах.)</span><span class="sxs-lookup"><span data-stu-id="7b2cd-161">(It is not the same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="7b2cd-162">На портале вы можете фильтровать или сегментировать данные телеметрии с помощью этого свойства.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-162">In the portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="7b2cd-163">В этом примере колонка "Сбои" отфильтрована для показа только информации из интерфейсной веб-службы, пропуская сбои из серверной части API CRM:</span><span class="sxs-lookup"><span data-stu-id="7b2cd-163">In this example, the Failures blade is filtered to show just information from the front-end web service, filtering out failures from the CRM API backend:</span></span>

![Диаграмма метрик, сегментированная по имени облачной роли](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="7b2cd-165">Отслеживание операций между компонентами</span><span class="sxs-lookup"><span data-stu-id="7b2cd-165">Trace operations between components</span></span>

<span data-ttu-id="7b2cd-166">Вы можете отслеживать вызовы от одного компонента к другому, сделанные во время обработки отдельной операции.</span><span class="sxs-lookup"><span data-stu-id="7b2cd-166">You can trace from one component to another, the calls made while processing an individual operation.</span></span>


![Отображение данных телеметрии для операции](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="7b2cd-168">Перейдите к связанному списку телеметрии для этой операции на интерфейсном веб-сервере и в API серверной части:</span><span class="sxs-lookup"><span data-stu-id="7b2cd-168">Click through to a correlated list of telemetry for this operation across the front-end web server and the back-end API:</span></span>

![Поиск по компонентам](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="7b2cd-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b2cd-170">Next steps</span></span>

* [<span data-ttu-id="7b2cd-171">Отделение телеметрии стадий разработки, тестирования и эксплуатации</span><span class="sxs-lookup"><span data-stu-id="7b2cd-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
