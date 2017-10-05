---
title: "Application Insights для уже действующих веб-приложений Java"
description: "Начните отслеживать веб-приложение, которое уже выполняется на вашем сервере."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: a2731e3e44f8f3d104d8abc7dbe71fe3a4c3a690
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="a7864-103">Application Insights для уже действующих веб-приложений Java</span><span class="sxs-lookup"><span data-stu-id="a7864-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="a7864-104">Если у вас уже есть запущенное на сервере J2EE веб-приложение, вы можете выполнять его мониторинг с помощью [Application Insights](app-insights-overview.md). Для этого вам не нужно вносить изменения в код или повторно компилировать проект.</span><span class="sxs-lookup"><span data-stu-id="a7864-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span></span> <span data-ttu-id="a7864-105">Таким образом вы сможете получать информацию об HTTP-запросах, отправляемых на сервер, необработанных исключениях и счетчиках производительности.</span><span class="sxs-lookup"><span data-stu-id="a7864-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="a7864-106">Вам понадобится подписка [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="a7864-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="a7864-107">В ходе описанной на этой странице процедуры в веб-приложение во время его выполнения добавляется пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="a7864-107">The procedure on this page adds the SDK to your web app at runtime.</span></span> <span data-ttu-id="a7864-108">Это инструментирование во время выполнения избавляет от необходимости изменять или повторно компилировать исходный код.</span><span class="sxs-lookup"><span data-stu-id="a7864-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span></span> <span data-ttu-id="a7864-109">Но если есть такая возможность, мы рекомендуем [добавлять пакет SDK непосредственно в исходный код](app-insights-java-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="a7864-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="a7864-110">Так вы получите дополнительные возможности, например сможете написать код для отслеживания действий пользователей.</span><span class="sxs-lookup"><span data-stu-id="a7864-110">That gives you more options such as writing code to track user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="a7864-111">1. Получение ключа инструментирования Application Insights</span><span class="sxs-lookup"><span data-stu-id="a7864-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="a7864-112">Войдите на [портал Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="a7864-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="a7864-113">Создайте ресурс Application Insights и задайте тип приложения "Веб-приложение Java".</span><span class="sxs-lookup"><span data-stu-id="a7864-113">Create a new Application Insights resource and set the application type to Java web application.</span></span>
   
    ![Введите имя, выберите веб-приложение Java и нажмите кнопку "Создать"](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="a7864-115">Через несколько секунд ресурс будет создан.</span><span class="sxs-lookup"><span data-stu-id="a7864-115">The resource is created in a few seconds.</span></span>

4. <span data-ttu-id="a7864-116">Откройте новый ресурс и получите его ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="a7864-116">Open the new resource and get its instrumentation key.</span></span> <span data-ttu-id="a7864-117">Далее будет необходимо вставить его в проект кода.</span><span class="sxs-lookup"><span data-stu-id="a7864-117">You'll need to paste this key into your code project shortly.</span></span>
   
    ![В обзоре нового ресурса щелкните "Свойства" и скопируйте ключ инструментирования](./media/app-insights-java-live/03-key.png)

## <a name="2-download-the-sdk"></a><span data-ttu-id="a7864-119">2. Скачивание пакета SDK</span><span class="sxs-lookup"><span data-stu-id="a7864-119">2. Download the SDK</span></span>
1. <span data-ttu-id="a7864-120">Загрузите [пакет SDK Application Insights для Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="a7864-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="a7864-121">На сервере извлеките содержимое пакета SDK в каталог, из которого загружаются двоичные файлы проекта.</span><span class="sxs-lookup"><span data-stu-id="a7864-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span></span> <span data-ttu-id="a7864-122">В случае с Tomcat обычно это каталог `webapps/<your_app_name>/WEB-INF/lib`.</span><span class="sxs-lookup"><span data-stu-id="a7864-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="a7864-123">Обратите внимание, что это необходимо сделать в каждом экземпляре сервера и для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="a7864-123">Note that you need to repeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="a7864-124">3. Добавление XML-файла Application Insights</span><span class="sxs-lookup"><span data-stu-id="a7864-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="a7864-125">Создайте файл ApplicationInsights.xml в папке, в которую добавили пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="a7864-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span></span> <span data-ttu-id="a7864-126">Вставьте в него следующий код XML.</span><span class="sxs-lookup"><span data-stu-id="a7864-126">Put into it the following XML.</span></span>

<span data-ttu-id="a7864-127">Замените ключ инструментирования на полученный в портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a7864-127">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="a7864-128">Ключ инструментирования пересылается вместе с каждым элементом телеметрии; служба Application Insights отобразит его в ресурсе.</span><span class="sxs-lookup"><span data-stu-id="a7864-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="a7864-129">Компонент HTTP-запросов является необязательным.</span><span class="sxs-lookup"><span data-stu-id="a7864-129">The HTTP Request component is optional.</span></span> <span data-ttu-id="a7864-130">Он автоматически передает на портал телеметрию о запросах и значения времени ответа.</span><span class="sxs-lookup"><span data-stu-id="a7864-130">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="a7864-131">Корреляционные данные для событий являются дополнением к компоненту HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="a7864-131">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="a7864-132">Это дополнение назначает идентификатор для каждого запроса, полученного сервером, и добавляет его в качестве свойства каждого элемента телеметрии в форме "Операция.ИД".</span><span class="sxs-lookup"><span data-stu-id="a7864-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="a7864-133">Благодаря этому можно выделить данные телеметрии, связанные с каждым из запросов, путем установки фильтра [Поиск по журналу диагностики](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="a7864-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="a7864-134">4. Добавление фильтра HTTP</span><span class="sxs-lookup"><span data-stu-id="a7864-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="a7864-135">Найдите и откройте файл web.xml в проекте, добавьте следующий фрагмент кода в узел web-app, где настраиваются фильтры вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a7864-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="a7864-136">Для получения наиболее точных результатов этот фильтр должен применяться до всех остальных фильтров.</span><span class="sxs-lookup"><span data-stu-id="a7864-136">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="a7864-137">5. Проверка исключений брандмауэра</span><span class="sxs-lookup"><span data-stu-id="a7864-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="a7864-138">Вам может понадобиться [задать исключения для отправки исходящих данных](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="a7864-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="a7864-139">6. Перезапуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a7864-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="a7864-140">7. Просмотр данных телеметрии в Application Insights</span><span class="sxs-lookup"><span data-stu-id="a7864-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="a7864-141">Вернитесь к ресурсу Application Insights на [портале Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a7864-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="a7864-142">В колонке обзора появятся данные телеметрии HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="a7864-142">Telemetry about HTTP requests appears on the overview blade.</span></span> <span data-ttu-id="a7864-143">(Если данные отсутствуют, подождите несколько секунд и нажмите кнопку обновления).</span><span class="sxs-lookup"><span data-stu-id="a7864-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![пример данных](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="a7864-145">Щелкните любую диаграмму, чтобы увидеть более подробные метрики.</span><span class="sxs-lookup"><span data-stu-id="a7864-145">Click through any chart to see more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="a7864-146">При просмотре свойств запроса можно увидеть события телеметрии, связанные с ним, такие как запросы и исключения.</span><span class="sxs-lookup"><span data-stu-id="a7864-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="a7864-147">Дополнительные сведения о метриках.</span><span class="sxs-lookup"><span data-stu-id="a7864-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="a7864-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7864-148">Next steps</span></span>
* <span data-ttu-id="a7864-149">[Добавьте телеметрии на веб-страницы](app-insights-javascript.md) для мониторинга просмотров страниц и метрик пользователя.</span><span class="sxs-lookup"><span data-stu-id="a7864-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span></span>
* <span data-ttu-id="a7864-150">[Настройте веб-тесты](app-insights-monitor-web-app-availability.md) , которые помогут быть уверенными в том, что приложение остается работоспособным и правильно отвечает на запросы.</span><span class="sxs-lookup"><span data-stu-id="a7864-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="a7864-151">Журнал трассировки</span><span class="sxs-lookup"><span data-stu-id="a7864-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="a7864-152">[Поиск событий и журналов](app-insights-diagnostic-search.md) для диагностики неполадок.</span><span class="sxs-lookup"><span data-stu-id="a7864-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span></span>

