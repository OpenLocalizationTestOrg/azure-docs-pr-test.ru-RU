---
title: "aaaGet работы с Application Insights Azure с Java в Eclipse | Документы Microsoft"
description: "Используйте hello производительности tooadd подключаемый модуль Eclipse и использование отслеживание tooyour веб-сайте Java с помощью Application Insights"
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
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="e9813-103">Приступая к работе с Application Insights на Java в Eclipse</span><span class="sxs-lookup"><span data-stu-id="e9813-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="e9813-104">Hello пакет SDK Application Insights отправляет телеметрии из веб-приложения Java, так что можно анализировать использование и производительность.</span><span class="sxs-lookup"><span data-stu-id="e9813-104">hello Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="e9813-105">Hello Eclipse подключаемый модуль Application Insights автоматически устанавливает hello SDK в проекте, чтобы получить из hello поле телеметрии, а также API, которые можно использовать пользовательские телеметрии toowrite.</span><span class="sxs-lookup"><span data-stu-id="e9813-105">hello Eclipse plug-in for Application Insights automatically installs hello SDK in your project so that you get out of hello box telemetry, plus an API that you can use toowrite custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="e9813-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e9813-106">Prerequisites</span></span>
<span data-ttu-id="e9813-107">В настоящее время hello работает подключаемый модуль для проектов Maven и динамические веб-проектов в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e9813-107">Currently hello plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="e9813-108">([Добавить Application Insights tooother типов проекта Java][java].)</span><span class="sxs-lookup"><span data-stu-id="e9813-108">([Add Application Insights tooother types of Java project][java].)</span></span>

<span data-ttu-id="e9813-109">Что вам понадобится:</span><span class="sxs-lookup"><span data-stu-id="e9813-109">You'll need:</span></span>

* <span data-ttu-id="e9813-110">Oracle JRE 1.6 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="e9813-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="e9813-111">Подписка слишком[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="e9813-111">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="e9813-112">[интегрированная среда разработки Eclipse для разработчиков Java EE](http://www.eclipse.org/downloads/), версия Indigo или более поздняя;</span><span class="sxs-lookup"><span data-stu-id="e9813-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="e9813-113">Windows 7 или более поздней версии либо Windows Server 2008 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e9813-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-hello-sdk-on-eclipse-one-time"></a><span data-ttu-id="e9813-114">Установка hello пакета SDK для Eclipse (один раз)</span><span class="sxs-lookup"><span data-stu-id="e9813-114">Install hello SDK on Eclipse (one time)</span></span>
<span data-ttu-id="e9813-115">Имеется только toodo этот один раз на каждый компьютер.</span><span class="sxs-lookup"><span data-stu-id="e9813-115">You only have toodo this one time per machine.</span></span> <span data-ttu-id="e9813-116">Это действие устанавливает набор средств, который затем можно добавить пакет SDK для hello tooeach динамический веб-проект.</span><span class="sxs-lookup"><span data-stu-id="e9813-116">This step installs a toolkit which can then add hello SDK tooeach Dynamic Web Project.</span></span>

1. <span data-ttu-id="e9813-117">В Eclipse щелкните "Help" (Справка), "Install New Software" (Установка нового программного обеспечения).</span><span class="sxs-lookup"><span data-stu-id="e9813-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Help, Install New Software](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="e9813-119">пакет SDK для Hello находится в http://dl.microsoft.com/eclipse в набор средств Azure.</span><span class="sxs-lookup"><span data-stu-id="e9813-119">hello SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="e9813-120">Снимите флажок **Contact all update sites...**</span><span class="sxs-lookup"><span data-stu-id="e9813-120">Uncheck **Contact all update sites...**</span></span>

    ![Для установки пакета SDK Application Insights снимите флажок "Contact all update sites..."](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="e9813-122">Выполните оставшиеся шаги для каждого проекта Java hello.</span><span class="sxs-lookup"><span data-stu-id="e9813-122">Follow hello remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="e9813-123">Создание ресурса Application Insights в Azure</span><span class="sxs-lookup"><span data-stu-id="e9813-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="e9813-124">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e9813-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e9813-125">Создайте новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e9813-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="e9813-126">Задать hello приложения типа tooJava веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e9813-126">Set hello application type tooJava web application.</span></span>  

    ![Нажмите кнопку "+" и выберите пункт "Application Insights"](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="e9813-128">Найти ключ инструментирования hello hello нового ресурса.</span><span class="sxs-lookup"><span data-stu-id="e9813-128">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="e9813-129">Вам потребуется toopaste это в проекте кода чуть ниже.</span><span class="sxs-lookup"><span data-stu-id="e9813-129">You'll need toopaste this into your code project shortly.</span></span>  

    ![Обзор нового ресурса hello нажмите кнопку Свойства и скопируйте hello ключ инструментирования](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a><span data-ttu-id="e9813-131">Добавление проекта tooyour Application Insights</span><span class="sxs-lookup"><span data-stu-id="e9813-131">Add Application Insights tooyour project</span></span>
1. <span data-ttu-id="e9813-132">Добавьте Application Insights hello контекстном меню веб-проекта Java.</span><span class="sxs-lookup"><span data-stu-id="e9813-132">Add Application Insights from hello context menu of your Java web project.</span></span>

    ![Обзор нового ресурса hello нажмите кнопку Свойства и скопируйте hello ключ инструментирования](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="e9813-134">Вставьте ключ инструментирования hello, полученного от hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e9813-134">Paste hello instrumentation key that you got from hello Azure portal.</span></span>

    ![Обзор нового ресурса hello нажмите кнопку Свойства и скопируйте hello ключ инструментирования](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="e9813-136">ключ Hello отправляется вместе с каждого элемента телеметрии и сообщает toodisplay Application Insights в ресурс.</span><span class="sxs-lookup"><span data-stu-id="e9813-136">hello key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>

## <a name="run-hello-application-and-see-metrics"></a><span data-ttu-id="e9813-137">Запустите приложение hello и просматривать показатели</span><span class="sxs-lookup"><span data-stu-id="e9813-137">Run hello application and see metrics</span></span>
<span data-ttu-id="e9813-138">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="e9813-138">Run your application.</span></span>

<span data-ttu-id="e9813-139">Вернуть ресурс Application Insights tooyour в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e9813-139">Return tooyour Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="e9813-140">HTTP-запросы данных появится в колонке Обзор hello.</span><span class="sxs-lookup"><span data-stu-id="e9813-140">HTTP requests data will appear on hello overview blade.</span></span> <span data-ttu-id="e9813-141">(Если данные отсутствуют, подождите несколько секунд и нажмите кнопку обновления).</span><span class="sxs-lookup"><span data-stu-id="e9813-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="e9813-142">Ответ сервера, счетчики запросов и сбои</span><span class="sxs-lookup"><span data-stu-id="e9813-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="e9813-143">Нажмите кнопку через любой toosee диаграммы более подробные показатели.</span><span class="sxs-lookup"><span data-stu-id="e9813-143">Click through any chart toosee more detailed metrics.</span></span>

![Счетчики запросов по имени](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="e9813-145">[Дополнительные сведения о метриках.][metrics]</span><span class="sxs-lookup"><span data-stu-id="e9813-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="e9813-146">И при просмотре свойств hello запроса, можно просмотреть события телеметрии hello, связанные с ним, такие как запросы и исключения.</span><span class="sxs-lookup"><span data-stu-id="e9813-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![Все трассировки для данного запроса](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="e9813-148">Телеметрия на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="e9813-148">Client-side telemetry</span></span>
<span data-ttu-id="e9813-149">Из колонки hello краткое руководство нажмите кнопку Get toomonitor код веб-страницы:</span><span class="sxs-lookup"><span data-stu-id="e9813-149">From hello QuickStart blade, click Get code toomonitor my web pages:</span></span>

![В колонке обзор вашего приложения выберите Быстрый запуск, получить код toomonitor веб-страницы.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="e9813-152">Вставьте фрагмент кода hello в голове hello файлов HTML.</span><span class="sxs-lookup"><span data-stu-id="e9813-152">Insert hello code snippet in hello head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="e9813-153">Просмотр данных на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="e9813-153">View client-side data</span></span>
<span data-ttu-id="e9813-154">Откройте обновленные веб-страницы и выполните с ними какое-либо действие.</span><span class="sxs-lookup"><span data-stu-id="e9813-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="e9813-155">Подождите одну-две минуты, а затем вернуть tooApplication аналитики и откройте hello использования колонки.</span><span class="sxs-lookup"><span data-stu-id="e9813-155">Wait a minute or two, then return tooApplication Insights and open hello usage blade.</span></span> <span data-ttu-id="e9813-156">(Из колонки Обзор hello, прокрутите вниз и выберите использование).</span><span class="sxs-lookup"><span data-stu-id="e9813-156">(From hello Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="e9813-157">Страница представления, пользователей и сеансов метрики будет отображаться на колонки hello использования:</span><span class="sxs-lookup"><span data-stu-id="e9813-157">Page view, user, and session metrics will appear on hello usage blade:</span></span>

![Сеансы, пользователи и просмотры страниц](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="e9813-159">[Дополнительные сведения о настройке телеметрии на стороне клиента][usage]</span><span class="sxs-lookup"><span data-stu-id="e9813-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="e9813-160">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="e9813-160">Publish your application</span></span>
<span data-ttu-id="e9813-161">Теперь публикации сервера toohello приложения, позволяют использовать его и посмотреть телеметрии hello отображаются на портале hello.</span><span class="sxs-lookup"><span data-stu-id="e9813-161">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="e9813-162">Убедитесь, что брандмауэр разрешает вашего приложения toosend телеметрии toothese порты:</span><span class="sxs-lookup"><span data-stu-id="e9813-162">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="e9813-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="e9813-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="e9813-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="e9813-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="e9813-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="e9813-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="e9813-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="e9813-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="e9813-167">На серверах Windows необходимо установить следующее:</span><span class="sxs-lookup"><span data-stu-id="e9813-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="e9813-168">распространяемые компоненты Microsoft Visual C++.</span><span class="sxs-lookup"><span data-stu-id="e9813-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="e9813-169">(Сюда входят счетчики производительности).</span><span class="sxs-lookup"><span data-stu-id="e9813-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="e9813-170">Исключения и ошибки запросов</span><span class="sxs-lookup"><span data-stu-id="e9813-170">Exceptions and request failures</span></span>
<span data-ttu-id="e9813-171">Необработанные исключения автоматически фиксируются:</span><span class="sxs-lookup"><span data-stu-id="e9813-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="e9813-172">toocollect данные на другие исключения, у вас есть два варианта:</span><span class="sxs-lookup"><span data-stu-id="e9813-172">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="e9813-173">[Вставить tooTrackException вызовы в коде](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="e9813-173">[Insert calls tooTrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="e9813-174">[Установка агента Java hello на сервер](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="e9813-174">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="e9813-175">Можно указать hello методы, которые нужно toowatch.</span><span class="sxs-lookup"><span data-stu-id="e9813-175">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="e9813-176">Мониторинг вызовов методов и внешних зависимостей.</span><span class="sxs-lookup"><span data-stu-id="e9813-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="e9813-177">[Установка агента Java hello](app-insights-java-agent.md) toolog указан внутренние методы и вызовы через JDBC, с данными о времени.</span><span class="sxs-lookup"><span data-stu-id="e9813-177">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="e9813-178">Счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="e9813-178">Performance counters</span></span>
<span data-ttu-id="e9813-179">В колонке Обзор прокрутите список вниз и щелкните hello **серверы** плитки.</span><span class="sxs-lookup"><span data-stu-id="e9813-179">On your Overview blade, scroll down and click hello  **Servers** tile.</span></span> <span data-ttu-id="e9813-180">Вы увидите несколько счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="e9813-180">You'll see a range of performance counters.</span></span>

![Прокрутите вниз tooclick hello серверы плитки](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="e9813-182">Настройка сбора данных счетчиками производительности</span><span class="sxs-lookup"><span data-stu-id="e9813-182">Customize performance counter collection</span></span>
<span data-ttu-id="e9813-183">Коллекция toodisable hello стандартный набор счетчиков производительности, добавьте следующий код в корневом узле hello файла ApplicationInsights.xml hello hello:</span><span class="sxs-lookup"><span data-stu-id="e9813-183">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="e9813-184">Сбор данных дополнительными счетчиками производительности</span><span class="sxs-lookup"><span data-stu-id="e9813-184">Collect additional performance counters</span></span>
<span data-ttu-id="e9813-185">Можно указать собранных toobe счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="e9813-185">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="e9813-186">Счетчики JMX (предоставляемые hello виртуальной машины Java)</span><span class="sxs-lookup"><span data-stu-id="e9813-186">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="e9813-187">`displayName`— Имя hello, отображается на портале Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="e9813-187">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="e9813-188">`objectName`— Имя объекта JMX hello.</span><span class="sxs-lookup"><span data-stu-id="e9813-188">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="e9813-189">`attribute`— атрибут hello объекта имя hello JMX toofetch</span><span class="sxs-lookup"><span data-stu-id="e9813-189">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="e9813-190">`type`(необязательно) — hello тип атрибута JMX объекта:</span><span class="sxs-lookup"><span data-stu-id="e9813-190">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="e9813-191">по умолчанию: простой тип, такой как int или long;</span><span class="sxs-lookup"><span data-stu-id="e9813-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="e9813-192">`composite`: данные счетчика производительности hello находится в формате «Attribute.Data» hello</span><span class="sxs-lookup"><span data-stu-id="e9813-192">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="e9813-193">`tabular`: hello данные счетчика производительности имеет формат hello строки в таблице</span><span class="sxs-lookup"><span data-stu-id="e9813-193">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="e9813-194">Счетчики производительности Windows</span><span class="sxs-lookup"><span data-stu-id="e9813-194">Windows performance counters</span></span>
<span data-ttu-id="e9813-195">Каждый [счетчика производительности Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) входит в категорию (в hello так же, что поле является членом класса).</span><span class="sxs-lookup"><span data-stu-id="e9813-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="e9813-196">Категория может быть глобальной либо иметь пронумерованные или именованные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="e9813-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="e9813-197">отображаемое имя — имя hello, отображается на портале Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="e9813-197">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="e9813-198">Категория — hello категории счетчика производительности (производительности объект) с которым связан этот счетчик производительности.</span><span class="sxs-lookup"><span data-stu-id="e9813-198">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="e9813-199">counterName — hello имя счетчика производительности "hello".</span><span class="sxs-lookup"><span data-stu-id="e9813-199">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="e9813-200">instanceName — имя экземпляра категории счетчика производительности hello hello, или пустая строка ("»), если категория hello содержит единственный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="e9813-200">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="e9813-201">Если hello categoryName — процесс, а счетчик производительности hello хотелось бы toocollect от текущего процесса виртуальной машины Java hello на котором выполняется приложение, укажите `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="e9813-201">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="e9813-202">Счетчики производительности отображаются как пользовательские метрики в [обозревателе метрик][metrics].</span><span class="sxs-lookup"><span data-stu-id="e9813-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="e9813-203">Счетчики производительности Unix</span><span class="sxs-lookup"><span data-stu-id="e9813-203">Unix performance counters</span></span>
* <span data-ttu-id="e9813-204">[Установить подключаемый модуль Application Insights hello collectd](app-insights-java-collectd.md) tooget разнообразных данных системы и сети.</span><span class="sxs-lookup"><span data-stu-id="e9813-204">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="e9813-205">Доступность веб-тестов</span><span class="sxs-lookup"><span data-stu-id="e9813-205">Availability web tests</span></span>
<span data-ttu-id="e9813-206">Application Insights можно проверить веб-сайта на toocheck регулярные интервалы, он работает и отвечает хорошо.</span><span class="sxs-lookup"><span data-stu-id="e9813-206">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="e9813-207">[tooset копирование][availability], прокрутите вниз tooclick доступности.</span><span class="sxs-lookup"><span data-stu-id="e9813-207">[tooset up][availability], scroll down tooclick Availability.</span></span>

![Прокрутите вниз, щелкните "Доступность", затем "Добавить веб-тест"](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="e9813-209">Если ваш сайт выйдет из строя, вы получите диаграмму значений времени ответа, а также уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="e9813-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Пример веб-теста](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="e9813-211">[Дополнительные сведения о веб-тестах для определения доступности.][availability]</span><span class="sxs-lookup"><span data-stu-id="e9813-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="e9813-212">Журналы диагностики</span><span class="sxs-lookup"><span data-stu-id="e9813-212">Diagnostic logs</span></span>
<span data-ttu-id="e9813-213">Если вы используете Logback или Log4J (версия 1.2 или 2.0) для трассировки, что журналы трассировки отправляются автоматически tooApplication аналитики, где вы можете анализировать и поиск на них.</span><span class="sxs-lookup"><span data-stu-id="e9813-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

<span data-ttu-id="e9813-214">[Дополнительные сведения о журналах диагностики][javalogs]</span><span class="sxs-lookup"><span data-stu-id="e9813-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="e9813-215">Пользовательская телеметрия</span><span class="sxs-lookup"><span data-stu-id="e9813-215">Custom telemetry</span></span>
<span data-ttu-id="e9813-216">Вставить несколько строк кода в ваш web для Java приложения toofind out действиями пользователей с ним или toohelp диагностики проблем.</span><span class="sxs-lookup"><span data-stu-id="e9813-216">Insert a few lines of code in your Java web application toofind out what users are doing with it or toohelp diagnose problems.</span></span>

<span data-ttu-id="e9813-217">Код можно вставить в веб-страницы JavaScript и на стороне сервера Java hello.</span><span class="sxs-lookup"><span data-stu-id="e9813-217">You can insert code both in web page JavaScript and in hello server-side Java.</span></span>

<span data-ttu-id="e9813-218">[Дополнительные сведения о пользовательской телеметрии][track]</span><span class="sxs-lookup"><span data-stu-id="e9813-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9813-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e9813-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="e9813-220">Обнаружение и диагностика неполадок</span><span class="sxs-lookup"><span data-stu-id="e9813-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="e9813-221">[Добавить клиента телеметрии веб] [ usage] tooget телеметрии производительности с hello веб-клиента.</span><span class="sxs-lookup"><span data-stu-id="e9813-221">[Add web client telemetry][usage] tooget performance telemetry from hello web client.</span></span>
* <span data-ttu-id="e9813-222">[Настройка веб-тестов] [ availability] toomake убедиться, что приложение остается динамической и отвечать на запросы.</span><span class="sxs-lookup"><span data-stu-id="e9813-222">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>
* <span data-ttu-id="e9813-223">[Поиск событий и журналов] [ diagnostic] toohelp диагностики проблем.</span><span class="sxs-lookup"><span data-stu-id="e9813-223">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>
* <span data-ttu-id="e9813-224">[Используйте функции ведения журналов Log4J или Logback][javalogs].</span><span class="sxs-lookup"><span data-stu-id="e9813-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="e9813-225">Отслеживание использования</span><span class="sxs-lookup"><span data-stu-id="e9813-225">Track usage</span></span>
* <span data-ttu-id="e9813-226">[Добавить клиента телеметрии веб] [ usage] toomonitor страницы представлений и метрики, обычный пользователь.</span><span class="sxs-lookup"><span data-stu-id="e9813-226">[Add web client telemetry][usage] toomonitor page views and basic user metrics.</span></span>
* <span data-ttu-id="e9813-227">[Отслеживать пользовательские события и метрики](app-insights-web-track-usage.md) toolearn об использовании приложения, как на приветствия клиента и сервера hello.</span><span class="sxs-lookup"><span data-stu-id="e9813-227">[Track custom events and metrics](app-insights-web-track-usage.md) toolearn about how your application is used, both at hello client and hello server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
