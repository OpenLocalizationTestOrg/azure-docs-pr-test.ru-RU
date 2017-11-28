---
title: "Мониторинг производительности веб-приложений Java в Azure Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: 4e56998382610ad3d7224e6a8de5aee5419ebe43
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="52815-103">Отслеживание зависимостей, исключений и времени выполнения в веб-приложениях Java</span><span class="sxs-lookup"><span data-stu-id="52815-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="52815-104">[Инструментирование веб-приложения Java с помощью Application Insights][java] позволяет получать более подробную информацию без изменения кода, используя для этого агент для Java.</span><span class="sxs-lookup"><span data-stu-id="52815-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="52815-105">**Зависимости** — данные о вызовах других компонентов в вашем приложении, включая:</span><span class="sxs-lookup"><span data-stu-id="52815-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="52815-106">**вызовы REST** через HttpClient, OkHttp и RestTemplate (Spring);</span><span class="sxs-lookup"><span data-stu-id="52815-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="52815-107">**Redis** через клиент Jedis.</span><span class="sxs-lookup"><span data-stu-id="52815-107">**Redis** calls made via the Jedis client.</span></span> <span data-ttu-id="52815-108">Если вызов выполняется дольше 10 с, агент также получает аргументы вызова.</span><span class="sxs-lookup"><span data-stu-id="52815-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span></span>
  * <span data-ttu-id="52815-109">**[Вызовы JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** — MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB или Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="52815-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="52815-110">Поддерживаются вызовы "executeBatch".</span><span class="sxs-lookup"><span data-stu-id="52815-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="52815-111">Если для MySQL и PostgreSQL вызов выполняется дольше 10 с, агент сообщает о плане запроса.</span><span class="sxs-lookup"><span data-stu-id="52815-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="52815-112">**Перехваченные исключения:** данные об исключениях, обработанных вашим кодом.</span><span class="sxs-lookup"><span data-stu-id="52815-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="52815-113">**Время выполнения метода:** данные о времени, которое потребовалось для выполнения определенных методов.</span><span class="sxs-lookup"><span data-stu-id="52815-113">**Method execution time:** Data about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="52815-114">Чтобы использовать агент для Java, его необходимо установить на сервере.</span><span class="sxs-lookup"><span data-stu-id="52815-114">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="52815-115">Веб-приложения необходимо инструментировать [пакетом SDK для Java Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="52815-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="52815-116">Установка агента Application Insights для Java</span><span class="sxs-lookup"><span data-stu-id="52815-116">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="52815-117">[Скачайте агент](https://aka.ms/aijavasdk) на компьютер с сервером Java.</span><span class="sxs-lookup"><span data-stu-id="52815-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="52815-118">Измените скрипт запуска сервера приложений, добавив следующую виртуальную машину Java:</span><span class="sxs-lookup"><span data-stu-id="52815-118">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="52815-119">`javaagent:`*полный путь к файлу агента JAR*</span><span class="sxs-lookup"><span data-stu-id="52815-119">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="52815-120">Например, в Tomcat на компьютере Linux:</span><span class="sxs-lookup"><span data-stu-id="52815-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="52815-121">Перезапустите сервер приложений.</span><span class="sxs-lookup"><span data-stu-id="52815-121">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="52815-122">Настройка агента</span><span class="sxs-lookup"><span data-stu-id="52815-122">Configure the agent</span></span>
<span data-ttu-id="52815-123">Создайте файл с именем `AI-Agent.xml` и поместите его в ту же папку, где находится JAR-файл агента.</span><span class="sxs-lookup"><span data-stu-id="52815-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="52815-124">Настройка содержимого XML-файла.</span><span class="sxs-lookup"><span data-stu-id="52815-124">Set the content of the xml file.</span></span> <span data-ttu-id="52815-125">Измените приведенный ниже пример, включив необходимые функции или убрав ненужные.</span><span class="sxs-lookup"><span data-stu-id="52815-125">Edit the following example to include or omit the features you want.</span></span>

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

           <!-- Report on the particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="52815-126">Необходимо включить прием отчетов и контроль времени выполнения отдельных методов.</span><span class="sxs-lookup"><span data-stu-id="52815-126">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="52815-127">По умолчанию `reportExecutionTime` имеет значение true, а `reportCaughtExceptions` — значение false.</span><span class="sxs-lookup"><span data-stu-id="52815-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="52815-128">Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="52815-128">View the data</span></span>
<span data-ttu-id="52815-129">В ресурсе Application Insights сводные данные по удаленным зависимостям и времени выполнения методов отображаются в [элементе "Производительность"][metrics].</span><span class="sxs-lookup"><span data-stu-id="52815-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="52815-130">Для поиска отдельных экземпляров отчетов по зависимостям, исключениям и методам откройте [Поиск][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="52815-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="52815-131">[Дополнительные сведения о диагностировании проблем зависимостей](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="52815-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="52815-132">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="52815-132">Questions?</span></span> <span data-ttu-id="52815-133">Проблемы?</span><span class="sxs-lookup"><span data-stu-id="52815-133">Problems?</span></span>
* <span data-ttu-id="52815-134">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="52815-134">No data?</span></span> [<span data-ttu-id="52815-135">Настройте исключения брандмауэра</span><span class="sxs-lookup"><span data-stu-id="52815-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="52815-136">Устранение неполадок Java</span><span class="sxs-lookup"><span data-stu-id="52815-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
