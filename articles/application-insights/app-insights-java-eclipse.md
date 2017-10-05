---
title: "Приступая к работе с Azure Application Insights на Java в Eclipse | Документация Майкрософт"
description: "Используйте подключаемый модуль Eclipse, чтобы добавить в свой веб-сайт Java функцию Application Insights мониторинга производительности и использования."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: f2f696a3bbe7893c1f521a3e5588f4f93805d6a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="a5c2a-103">Приступая к работе с Application Insights на Java в Eclipse</span><span class="sxs-lookup"><span data-stu-id="a5c2a-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="a5c2a-104">Пакет SDK Application Insights передает телеметрию из веб-приложения Java, что позволяет вам анализировать параметры использования и производительности.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="a5c2a-105">Подключаемый модуль Eclipse для Application Insights автоматически устанавливает пакет SDK в проекте (что позволяет вам получать актуальную телеметрию) и интерфейс API, который можно использовать для написания пользовательских элементов телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="a5c2a-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a5c2a-106">Prerequisites</span></span>
<span data-ttu-id="a5c2a-107">В настоящее время подключаемый модуль работает для проектов Maven и динамических веб-проектов в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="a5c2a-108">([Приступая к работе с Application Insights в веб-проекте Java][java].)</span><span class="sxs-lookup"><span data-stu-id="a5c2a-108">([Add Application Insights to other types of Java project][java].)</span></span>

<span data-ttu-id="a5c2a-109">Что вам понадобится:</span><span class="sxs-lookup"><span data-stu-id="a5c2a-109">You'll need:</span></span>

* <span data-ttu-id="a5c2a-110">Oracle JRE 1.6 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="a5c2a-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="a5c2a-111">подписка на [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a5c2a-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="a5c2a-112">[интегрированная среда разработки Eclipse для разработчиков Java EE](http://www.eclipse.org/downloads/), версия Indigo или более поздняя;</span><span class="sxs-lookup"><span data-stu-id="a5c2a-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="a5c2a-113">Windows 7 или более поздней версии либо Windows Server 2008 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-the-sdk-on-eclipse-one-time"></a><span data-ttu-id="a5c2a-114">Установка пакета SDK для Eclipse (один раз)</span><span class="sxs-lookup"><span data-stu-id="a5c2a-114">Install the SDK on Eclipse (one time)</span></span>
<span data-ttu-id="a5c2a-115">Необходимо выполнить один раз на каждом из компьютеров.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-115">You only have to do this one time per machine.</span></span> <span data-ttu-id="a5c2a-116">На этом шаге устанавливается набор средств, который позволит добавить пакет SDK для каждого динамического веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span></span>

1. <span data-ttu-id="a5c2a-117">В Eclipse щелкните "Help" (Справка), "Install New Software" (Установка нового программного обеспечения).</span><span class="sxs-lookup"><span data-stu-id="a5c2a-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Help, Install New Software](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="a5c2a-119">Пакет SDK находится по адресу http://dl.microsoft.com/eclipse в разделе "Azure Toolkit" ("Набор средств Azure).</span><span class="sxs-lookup"><span data-stu-id="a5c2a-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="a5c2a-120">Снимите флажок **Contact all update sites...**</span><span class="sxs-lookup"><span data-stu-id="a5c2a-120">Uncheck **Contact all update sites...**</span></span>

    ![Для установки пакета SDK Application Insights снимите флажок "Contact all update sites..."](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="a5c2a-122">Оставшиеся действия выполните для каждого проекта Java.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-122">Follow the remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="a5c2a-123">Создание ресурса Application Insights в Azure</span><span class="sxs-lookup"><span data-stu-id="a5c2a-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="a5c2a-124">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5c2a-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5c2a-125">Создайте новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="a5c2a-126">Задайте тип приложения: веб-приложение Java.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-126">Set the application type to Java web application.</span></span>  

    ![Нажмите кнопку "+" и выберите пункт "Application Insights"](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="a5c2a-128">Найдите ключ инструментирования нового ресурса.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-128">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="a5c2a-129">Далее будет необходимо вставить его в проект кода.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-129">You'll need to paste this into your code project shortly.</span></span>  

    ![В обзоре нового ресурса щелкните "Свойства" и скопируйте ключ инструментирования](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="a5c2a-131">Добавление Application Insights в ваш проект</span><span class="sxs-lookup"><span data-stu-id="a5c2a-131">Add Application Insights to your project</span></span>
1. <span data-ttu-id="a5c2a-132">Добавьте Application Insights из контекстного меню веб-проекта Java.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-132">Add Application Insights from the context menu of your Java web project.</span></span>

    ![В обзоре нового ресурса щелкните "Свойства" и скопируйте ключ инструментирования](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="a5c2a-134">Вставьте ключ инструментирования, полученный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-134">Paste the instrumentation key that you got from the Azure portal.</span></span>

    ![В обзоре нового ресурса щелкните "Свойства" и скопируйте ключ инструментирования](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="a5c2a-136">Ключ пересылается вместе с каждым элементом телеметрии; служба Application Insights отобразит его в ресурсе.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>

## <a name="run-the-application-and-see-metrics"></a><span data-ttu-id="a5c2a-137">Запуск приложения и просмотр метрик</span><span class="sxs-lookup"><span data-stu-id="a5c2a-137">Run the application and see metrics</span></span>
<span data-ttu-id="a5c2a-138">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-138">Run your application.</span></span>

<span data-ttu-id="a5c2a-139">Вернитесь к ресурсу Application Insights в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-139">Return to your Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="a5c2a-140">В колонке обзора появятся данные HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-140">HTTP requests data will appear on the overview blade.</span></span> <span data-ttu-id="a5c2a-141">(Если данные отсутствуют, подождите несколько секунд и нажмите кнопку обновления).</span><span class="sxs-lookup"><span data-stu-id="a5c2a-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="a5c2a-142">Ответ сервера, счетчики запросов и сбои</span><span class="sxs-lookup"><span data-stu-id="a5c2a-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="a5c2a-143">Щелкните любую диаграмму, чтобы увидеть более подробные метрики.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-143">Click through any chart to see more detailed metrics.</span></span>

![Счетчики запросов по имени](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="a5c2a-145">[Дополнительные сведения о метриках.][metrics]</span><span class="sxs-lookup"><span data-stu-id="a5c2a-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="a5c2a-146">При просмотре свойств запроса можно увидеть события телеметрии, связанные с ним, такие как запросы и исключения.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![Все трассировки для данного запроса](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="a5c2a-148">Телеметрия на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="a5c2a-148">Client-side telemetry</span></span>
<span data-ttu-id="a5c2a-149">В колонке быстрого запуска щелкните ссылку "Получить код для мониторинга моих веб-страниц":</span><span class="sxs-lookup"><span data-stu-id="a5c2a-149">From the QuickStart blade, click Get code to monitor my web pages:</span></span>

![В колонке обзора приложения последовательно выберите элементы "Быстрый запуск", "Получить код для мониторинга моих веб-страниц".](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="a5c2a-152">Вставьте фрагмент кода в заголовок HTML-файлов.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-152">Insert the code snippet in the head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="a5c2a-153">Просмотр данных на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="a5c2a-153">View client-side data</span></span>
<span data-ttu-id="a5c2a-154">Откройте обновленные веб-страницы и выполните с ними какое-либо действие.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="a5c2a-155">Подождите минуту или две, а затем вернитесь в Application Insights и откройте колонку использования.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span></span> <span data-ttu-id="a5c2a-156">(Прокрутите колонку обзора вниз и щелкните элемент "Использование".)</span><span class="sxs-lookup"><span data-stu-id="a5c2a-156">(From the Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="a5c2a-157">В колонке использования появятся метрики просмотра страниц, пользователей и сеансов:</span><span class="sxs-lookup"><span data-stu-id="a5c2a-157">Page view, user, and session metrics will appear on the usage blade:</span></span>

![Сеансы, пользователи и просмотры страниц](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="a5c2a-159">[Дополнительные сведения о настройке телеметрии на стороне клиента][usage]</span><span class="sxs-lookup"><span data-stu-id="a5c2a-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="a5c2a-160">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="a5c2a-160">Publish your application</span></span>
<span data-ttu-id="a5c2a-161">Теперь опубликуйте приложение на сервере, откройте доступ для пользователей и изучайте телеметрию на портале.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="a5c2a-162">Убедитесь, что брандмауэр позволяет приложению отправлять телеметрию на следующие порты:</span><span class="sxs-lookup"><span data-stu-id="a5c2a-162">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="a5c2a-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="a5c2a-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="a5c2a-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="a5c2a-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="a5c2a-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="a5c2a-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="a5c2a-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="a5c2a-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="a5c2a-167">На серверах Windows необходимо установить следующее:</span><span class="sxs-lookup"><span data-stu-id="a5c2a-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="a5c2a-168">распространяемые компоненты Microsoft Visual C++.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="a5c2a-169">(Сюда входят счетчики производительности).</span><span class="sxs-lookup"><span data-stu-id="a5c2a-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="a5c2a-170">Исключения и ошибки запросов</span><span class="sxs-lookup"><span data-stu-id="a5c2a-170">Exceptions and request failures</span></span>
<span data-ttu-id="a5c2a-171">Необработанные исключения автоматически фиксируются:</span><span class="sxs-lookup"><span data-stu-id="a5c2a-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="a5c2a-172">Для сбора данных по другим исключениям доступны два варианта:</span><span class="sxs-lookup"><span data-stu-id="a5c2a-172">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="a5c2a-173">[вставить в код вызовы функции TrackException](app-insights-api-custom-events-metrics.md#trackexception);</span><span class="sxs-lookup"><span data-stu-id="a5c2a-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="a5c2a-174">[установить на сервере агент для Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="a5c2a-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="a5c2a-175">Необходимо указать методы, которые требуется отслеживать.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-175">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="a5c2a-176">Мониторинг вызовов методов и внешних зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="a5c2a-177">[установить агент для Java](app-insights-java-agent.md) .</span><span class="sxs-lookup"><span data-stu-id="a5c2a-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="a5c2a-178">Счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="a5c2a-178">Performance counters</span></span>
<span data-ttu-id="a5c2a-179">Прокрутите колонку "Обзор" вниз и щелкните плитку **Серверы**.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-179">On your Overview blade, scroll down and click the  **Servers** tile.</span></span> <span data-ttu-id="a5c2a-180">Вы увидите несколько счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-180">You'll see a range of performance counters.</span></span>

![Прокрутите вниз и щелкните плитку "Серверы"](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="a5c2a-182">Настройка сбора данных счетчиками производительности</span><span class="sxs-lookup"><span data-stu-id="a5c2a-182">Customize performance counter collection</span></span>
<span data-ttu-id="a5c2a-183">Чтобы отключить сбор данных стандартным набором счетчиков производительности, добавьте следующий фрагмент кода в корневой узел файла ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="a5c2a-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="a5c2a-184">Сбор данных дополнительными счетчиками производительности</span><span class="sxs-lookup"><span data-stu-id="a5c2a-184">Collect additional performance counters</span></span>
<span data-ttu-id="a5c2a-185">Можно задать необходимость сбора данных дополнительными счетчиками производительности.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-185">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="a5c2a-186">Счетчики JMX (предоставляются виртуальной машиной Java)</span><span class="sxs-lookup"><span data-stu-id="a5c2a-186">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="a5c2a-187">`displayName` — имя, отображаемое в портале Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-187">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="a5c2a-188">`objectName` — имя объекта JMX.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-188">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="a5c2a-189">`attribute` — атрибут имени объекта JMX для выборки</span><span class="sxs-lookup"><span data-stu-id="a5c2a-189">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="a5c2a-190">`type` (необязательно) — тип атрибута объекта JMX:</span><span class="sxs-lookup"><span data-stu-id="a5c2a-190">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="a5c2a-191">по умолчанию: простой тип, такой как int или long;</span><span class="sxs-lookup"><span data-stu-id="a5c2a-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="a5c2a-192">`composite`— данные счетчика производительности имеют формат "Атрибут.Данные";</span><span class="sxs-lookup"><span data-stu-id="a5c2a-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="a5c2a-193">`tabular`— данные счетчика производительности имеют формат строки таблицы.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-193">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="a5c2a-194">Счетчики производительности Windows</span><span class="sxs-lookup"><span data-stu-id="a5c2a-194">Windows performance counters</span></span>
<span data-ttu-id="a5c2a-195">Каждый [счетчик производительности Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) входит в состав категории (аналогично поле является членом класса).</span><span class="sxs-lookup"><span data-stu-id="a5c2a-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="a5c2a-196">Категория может быть глобальной либо иметь пронумерованные или именованные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="a5c2a-197">displayName — имя, отображаемое в портале Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-197">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="a5c2a-198">categoryName — категория счетчика производительности (объект производительности), с которой связан этот счетчик производительности.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="a5c2a-199">counterName — имя счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-199">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="a5c2a-200">instanceName — имя экземпляра категории счетчика производительности или пустая строка (""), если категория содержит единственный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="a5c2a-201">Если categoryName имеет значение "Process", и источником данных для счетчиков производительности является текущий процесс виртуальной машины Java, на которой выполняется ваше приложение, укажите `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="a5c2a-202">Счетчики производительности отображаются как пользовательские метрики в [обозревателе метрик][metrics].</span><span class="sxs-lookup"><span data-stu-id="a5c2a-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="a5c2a-203">Счетчики производительности Unix</span><span class="sxs-lookup"><span data-stu-id="a5c2a-203">Unix performance counters</span></span>
* <span data-ttu-id="a5c2a-204">[установите collectd с подключаемым модулем Application Insights](app-insights-java-collectd.md) .</span><span class="sxs-lookup"><span data-stu-id="a5c2a-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="a5c2a-205">Доступность веб-тестов</span><span class="sxs-lookup"><span data-stu-id="a5c2a-205">Availability web tests</span></span>
<span data-ttu-id="a5c2a-206">Application Insights может тестировать ваш веб-сайт через равные промежутки времени для проверки, работает ли он и правильно ли отвечает на запросы.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="a5c2a-207">[Чтобы выполнить настройку][availability], прокрутите вниз и щелкните "Доступность".</span><span class="sxs-lookup"><span data-stu-id="a5c2a-207">[To set up][availability], scroll down to click Availability.</span></span>

![Прокрутите вниз, щелкните "Доступность", затем "Добавить веб-тест"](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="a5c2a-209">Если ваш сайт выйдет из строя, вы получите диаграмму значений времени ответа, а также уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Пример веб-теста](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="a5c2a-211">[Дополнительные сведения о веб-тестах для определения доступности.][availability]</span><span class="sxs-lookup"><span data-stu-id="a5c2a-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="a5c2a-212">Журналы диагностики</span><span class="sxs-lookup"><span data-stu-id="a5c2a-212">Diagnostic logs</span></span>
<span data-ttu-id="a5c2a-213">Если вы используете Logback или Log4J (версия 1.2 или 2.0) для трассировки, можно настроить автоматическую пересылку журналов в Application Insights, где вы сможете их изучить.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

<span data-ttu-id="a5c2a-214">[Дополнительные сведения о журналах диагностики][javalogs]</span><span class="sxs-lookup"><span data-stu-id="a5c2a-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="a5c2a-215">Пользовательская телеметрия</span><span class="sxs-lookup"><span data-stu-id="a5c2a-215">Custom telemetry</span></span>
<span data-ttu-id="a5c2a-216">Вставьте несколько строк кода в свое веб-приложение Java, чтобы узнать, как пользователи его используют, или для диагностики неполадок.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span></span>

<span data-ttu-id="a5c2a-217">Код можно вставить на веб-страницу JavaScript и на стороне сервера Java.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-217">You can insert code both in web page JavaScript and in the server-side Java.</span></span>

<span data-ttu-id="a5c2a-218">[Дополнительные сведения о пользовательской телеметрии][track]</span><span class="sxs-lookup"><span data-stu-id="a5c2a-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5c2a-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5c2a-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="a5c2a-220">Обнаружение и диагностика неполадок</span><span class="sxs-lookup"><span data-stu-id="a5c2a-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="a5c2a-221">[Добавьте сбор данных телеметрии веб-клиента][usage] для получения телеметрии производительности из веб-клиента.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span></span>
* <span data-ttu-id="a5c2a-222">[Настройте веб-тесты][availability], которые помогут быть уверенными в том, что приложение остается работоспособным и правильно отвечает на запросы.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>
* <span data-ttu-id="a5c2a-223">[Выполняйте поиск событий и журналов][diagnostic] для диагностики неполадок.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-223">[Search events and logs][diagnostic] to help diagnose problems.</span></span>
* <span data-ttu-id="a5c2a-224">[Используйте функции ведения журналов Log4J или Logback][javalogs].</span><span class="sxs-lookup"><span data-stu-id="a5c2a-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="a5c2a-225">Отслеживание использования</span><span class="sxs-lookup"><span data-stu-id="a5c2a-225">Track usage</span></span>
* <span data-ttu-id="a5c2a-226">[Добавьте сбор данных телеметрии веб-клиента][usage] для отслеживания просмотров страниц и основных метрик пользователей.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span></span>
* <span data-ttu-id="a5c2a-227">[Отслеживайте пользовательские события и метрики](app-insights-web-track-usage.md) для получения сведений об использовании приложения как в клиенте, так и на сервере.</span><span class="sxs-lookup"><span data-stu-id="a5c2a-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
