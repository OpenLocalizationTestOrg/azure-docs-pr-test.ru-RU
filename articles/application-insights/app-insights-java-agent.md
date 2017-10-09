---
title: "aaaPerformance наблюдения для веб-приложений Java в Azure Application Insights | Документы Microsoft"
description: "Расширенный мониторинг производительности и использования веб-сайта Java с помощью Application Insights."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: bf3983e3b4a16e72bc606b6468a757288d05ebaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="20083-103">Отслеживание зависимостей, исключений и времени выполнения в веб-приложениях Java</span><span class="sxs-lookup"><span data-stu-id="20083-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="20083-104">Если у вас есть [инструментированы веб-приложения Java с помощью Application Insights][java], можно использовать hello агента Java tooget более глубокого понимания, без необходимости изменения кода:</span><span class="sxs-lookup"><span data-stu-id="20083-104">If you have [instrumented your Java web app with Application Insights][java], you can use hello Java Agent tooget deeper insights, without any code changes:</span></span>

* <span data-ttu-id="20083-105">**Зависимости:** данные о вызовы, сделанные tooother компонентов, включая приложения:</span><span class="sxs-lookup"><span data-stu-id="20083-105">**Dependencies:** Data about calls that your application makes tooother components, including:</span></span>
  * <span data-ttu-id="20083-106">**вызовы REST** через HttpClient, OkHttp и RestTemplate (Spring);</span><span class="sxs-lookup"><span data-stu-id="20083-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="20083-107">**Redis** вызовов, выполненных с помощью клиента Jedis hello.</span><span class="sxs-lookup"><span data-stu-id="20083-107">**Redis** calls made via hello Jedis client.</span></span> <span data-ttu-id="20083-108">Если вызов hello занимает больше времени, чем десятках, hello агент также извлечет hello аргументы вызова.</span><span class="sxs-lookup"><span data-stu-id="20083-108">If hello call takes longer than 10s, hello agent also fetches hello call arguments.</span></span>
  * <span data-ttu-id="20083-109">**[Вызовы JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** — MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB или Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="20083-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="20083-110">Поддерживаются вызовы "executeBatch".</span><span class="sxs-lookup"><span data-stu-id="20083-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="20083-111">MySQL и PostgreSQL Если вызов hello занимает больше времени, чем десятках, hello агента сообщает hello плана запроса.</span><span class="sxs-lookup"><span data-stu-id="20083-111">For MySQL and PostgreSQL, if hello call takes longer than 10s, hello agent reports hello query plan.</span></span>
* <span data-ttu-id="20083-112">**Перехваченные исключения:** данные об исключениях, обработанных вашим кодом.</span><span class="sxs-lookup"><span data-stu-id="20083-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="20083-113">**Время выполнения метода:** данные о hello время принимает tooexecute определенных методов.</span><span class="sxs-lookup"><span data-stu-id="20083-113">**Method execution time:** Data about hello time it takes tooexecute specific methods.</span></span>

<span data-ttu-id="20083-114">агент Java toouse hello, его установить на сервере.</span><span class="sxs-lookup"><span data-stu-id="20083-114">toouse hello Java agent, you install it on your server.</span></span> <span data-ttu-id="20083-115">Веб-приложения должны быть встроены hello [пакет SDK для Java Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="20083-115">Your web apps must be instrumented with hello [Application Insights Java SDK][java].</span></span> 

## <a name="install-hello-application-insights-agent-for-java"></a><span data-ttu-id="20083-116">Установка агента hello Application Insights для Java</span><span class="sxs-lookup"><span data-stu-id="20083-116">Install hello Application Insights agent for Java</span></span>
1. <span data-ttu-id="20083-117">На компьютере hello на котором запущен сервер Java [загрузить агент hello](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="20083-117">On hello machine running your Java server, [download hello agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="20083-118">Измените сценарий запуска сервера приложения hello и добавьте hello, следуя виртуальной машины Java:</span><span class="sxs-lookup"><span data-stu-id="20083-118">Edit hello application server startup script, and add hello following JVM:</span></span>
   
    <span data-ttu-id="20083-119">`javaagent:`*Полный путь агента toohello JAR-файл*</span><span class="sxs-lookup"><span data-stu-id="20083-119">`javaagent:`*full path toohello agent JAR file*</span></span>
   
    <span data-ttu-id="20083-120">Например, в Tomcat на компьютере Linux:</span><span class="sxs-lookup"><span data-stu-id="20083-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. <span data-ttu-id="20083-121">Перезапустите сервер приложений.</span><span class="sxs-lookup"><span data-stu-id="20083-121">Restart your application server.</span></span>

## <a name="configure-hello-agent"></a><span data-ttu-id="20083-122">Настройка агента hello</span><span class="sxs-lookup"><span data-stu-id="20083-122">Configure hello agent</span></span>
<span data-ttu-id="20083-123">Создайте файл с именем `AI-Agent.xml` и поместить его в hello же папке, что агент hello JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="20083-123">Create a file named `AI-Agent.xml` and place it in hello same folder as hello agent JAR file.</span></span>

<span data-ttu-id="20083-124">Задайте содержимое hello hello XML-файла.</span><span class="sxs-lookup"><span data-stu-id="20083-124">Set hello content of hello xml file.</span></span> <span data-ttu-id="20083-125">Измените следующие tooinclude пример hello или удалите компоненты hello.</span><span class="sxs-lookup"><span data-stu-id="20083-125">Edit hello following example tooinclude or omit hello features you want.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on hello particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="20083-126">У вас есть tooenable отчеты исключение и метод расписание для отдельных методов.</span><span class="sxs-lookup"><span data-stu-id="20083-126">You have tooenable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="20083-127">По умолчанию `reportExecutionTime` имеет значение true, а `reportCaughtExceptions` — значение false.</span><span class="sxs-lookup"><span data-stu-id="20083-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-hello-data"></a><span data-ttu-id="20083-128">Просмотр данных hello</span><span class="sxs-lookup"><span data-stu-id="20083-128">View hello data</span></span>
<span data-ttu-id="20083-129">В hello ресурс Application Insights, отображается агрегированных удаленного времени выполнения зависимостей и метод [под hello производительности плитку][metrics].</span><span class="sxs-lookup"><span data-stu-id="20083-129">In hello Application Insights resource, aggregated remote dependency and method execution times appears [under hello Performance tile][metrics].</span></span>

<span data-ttu-id="20083-130">Откройте toosearch для отдельных экземпляров зависимостей, исключение и метод отчеты, [поиска][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="20083-130">toosearch for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="20083-131">[Дополнительные сведения о диагностировании проблем зависимостей](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="20083-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="20083-132">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="20083-132">Questions?</span></span> <span data-ttu-id="20083-133">Проблемы?</span><span class="sxs-lookup"><span data-stu-id="20083-133">Problems?</span></span>
* <span data-ttu-id="20083-134">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="20083-134">No data?</span></span> [<span data-ttu-id="20083-135">Настройте исключения брандмауэра</span><span class="sxs-lookup"><span data-stu-id="20083-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="20083-136">Устранение неполадок Java</span><span class="sxs-lookup"><span data-stu-id="20083-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
