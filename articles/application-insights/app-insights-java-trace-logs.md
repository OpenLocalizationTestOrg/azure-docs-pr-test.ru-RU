---
title: "Изучение журналов трассировки Java в Azure Application Insights | Документация Майкрософт"
description: "Поиск данных трассировки Log4J или Logback в Application Insights"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 5baba3deaf58a1a24995c60381592a9c2ffefd81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="ada88-103">Просмотр журналов трассировки Java в Application Insights</span><span class="sxs-lookup"><span data-stu-id="ada88-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="ada88-104">Если вы используете Logback или Log4J (версия 1.2 или 2.0) для трассировки, можно настроить автоматическую пересылку журналов в Application Insights, где вы сможете их изучить.</span><span class="sxs-lookup"><span data-stu-id="ada88-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

## <a name="install-the-java-sdk"></a><span data-ttu-id="ada88-105">Установка пакета SDK для Java</span><span class="sxs-lookup"><span data-stu-id="ada88-105">Install the Java SDK</span></span>

<span data-ttu-id="ada88-106">Установите пакет [SDK Application Insights для Java][java], если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="ada88-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="ada88-107">(Если не нужно отслеживать HTTP-запросы, можно опустить большую часть XML-файла конфигурации, но необходимо по крайней мере добавить элемент `InstrumentationKey`.</span><span class="sxs-lookup"><span data-stu-id="ada88-107">(If you don't want to track HTTP requests, you can omit most of the .xml configuration file, but you must at least include the `InstrumentationKey` element.</span></span> <span data-ttu-id="ada88-108">Кроме того, следует вызвать метод `new TelemetryClient()` для инициализации пакета SDK.)</span><span class="sxs-lookup"><span data-stu-id="ada88-108">You should also call `new TelemetryClient()` to initialize the SDK.)</span></span>


## <a name="add-logging-libraries-to-your-project"></a><span data-ttu-id="ada88-109">Добавление в проект библиотеки ведения журналов</span><span class="sxs-lookup"><span data-stu-id="ada88-109">Add logging libraries to your project</span></span>
<span data-ttu-id="ada88-110">*Выберите подходящий метод для проекта.*</span><span class="sxs-lookup"><span data-stu-id="ada88-110">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="ada88-111">Если вы используете Maven...</span><span class="sxs-lookup"><span data-stu-id="ada88-111">If you're using Maven...</span></span>
<span data-ttu-id="ada88-112">Если проект уже настроен для сборки с использованием Maven, добавьте один из следующих фрагментов кода в файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="ada88-112">If your project is already set up to use Maven for build, merge one of the following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="ada88-113">Затем обновите зависимости проекта, чтобы загрузить двоичные файлы.</span><span class="sxs-lookup"><span data-stu-id="ada88-113">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="ada88-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="ada88-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="ada88-115">*Log4J версии 2.0*</span><span class="sxs-lookup"><span data-stu-id="ada88-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="ada88-116">*Log4J версии 1.2*</span><span class="sxs-lookup"><span data-stu-id="ada88-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="ada88-117">Если вы используете Gradle...</span><span class="sxs-lookup"><span data-stu-id="ada88-117">If you're using Gradle...</span></span>
<span data-ttu-id="ada88-118">Если проект уже настроен для сборки с использованием Gradle, добавьте одну из следующих строк в группу `dependencies` в файле build.gradle.</span><span class="sxs-lookup"><span data-stu-id="ada88-118">If your project is already set up to use Gradle for build, add one of the following lines to the `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="ada88-119">Затем обновите зависимости проекта, чтобы загрузить двоичные файлы.</span><span class="sxs-lookup"><span data-stu-id="ada88-119">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="ada88-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="ada88-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="ada88-121">**Log4J версии 2.0**</span><span class="sxs-lookup"><span data-stu-id="ada88-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="ada88-122">**Log4J версии 1.2**</span><span class="sxs-lookup"><span data-stu-id="ada88-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="ada88-123">В противном случае...</span><span class="sxs-lookup"><span data-stu-id="ada88-123">Otherwise ...</span></span>
<span data-ttu-id="ada88-124">Загрузите и извлеките соответствующий аппендер, а затем добавьте подходящую библиотеку в проект:</span><span class="sxs-lookup"><span data-stu-id="ada88-124">Download and extract the appropriate appender, then add the appropriate library to your project:</span></span>

| <span data-ttu-id="ada88-125">Средство ведения журнала</span><span class="sxs-lookup"><span data-stu-id="ada88-125">Logger</span></span> | <span data-ttu-id="ada88-126">Загрузить</span><span class="sxs-lookup"><span data-stu-id="ada88-126">Download</span></span> | <span data-ttu-id="ada88-127">Библиотека</span><span class="sxs-lookup"><span data-stu-id="ada88-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ada88-128">Logback</span><span class="sxs-lookup"><span data-stu-id="ada88-128">Logback</span></span> |[<span data-ttu-id="ada88-129">Пакет SDK с аппендером Logback</span><span class="sxs-lookup"><span data-stu-id="ada88-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="ada88-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="ada88-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="ada88-131">Log4J версии 2.0</span><span class="sxs-lookup"><span data-stu-id="ada88-131">Log4J v2.0</span></span> |[<span data-ttu-id="ada88-132">Пакет SDK с аппендером Log4J версии 2.0</span><span class="sxs-lookup"><span data-stu-id="ada88-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="ada88-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="ada88-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="ada88-134">Log4J версии 1.2</span><span class="sxs-lookup"><span data-stu-id="ada88-134">Log4j v1.2</span></span> |[<span data-ttu-id="ada88-135">Пакет SDK с аппендером Log4J версии 1.2</span><span class="sxs-lookup"><span data-stu-id="ada88-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="ada88-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="ada88-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-the-appender-to-your-logging-framework"></a><span data-ttu-id="ada88-137">Добавление аппендера в платформу ведения журнала</span><span class="sxs-lookup"><span data-stu-id="ada88-137">Add the appender to your logging framework</span></span>
<span data-ttu-id="ada88-138">Чтобы начать трассировку, добавьте соответствующий фрагмент кода в файл конфигурации Log4J или Logback:</span><span class="sxs-lookup"><span data-stu-id="ada88-138">To start getting traces, merge the relevant snippet of code to the Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="ada88-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="ada88-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="ada88-140">*Log4J версии 2.0*</span><span class="sxs-lookup"><span data-stu-id="ada88-140">*Log4J v2.0*</span></span>

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

<span data-ttu-id="ada88-141">*Log4J версии 1.2*</span><span class="sxs-lookup"><span data-stu-id="ada88-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="ada88-142">К аппендерам Application Insights может обращаться любое сконфигурированное средство ведения журнала, а не только корневое средство ведения журнала (как показано в примерах выше).</span><span class="sxs-lookup"><span data-stu-id="ada88-142">The Application Insights appenders can be referenced by any configured logger, and not necessarily by the root logger (as shown in the code samples above).</span></span>

## <a name="explore-your-traces-in-the-application-insights-portal"></a><span data-ttu-id="ada88-143">Просмотр данных трассировки на портале Application Insights</span><span class="sxs-lookup"><span data-stu-id="ada88-143">Explore your traces in the Application Insights portal</span></span>
<span data-ttu-id="ada88-144">После настройки проекта для передачи данных трассировки в Application Insights можно выполнять поиск и просмотр этих данных на портале Application Insights в колонке [Поиск][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="ada88-144">Now that you've configured your project to send traces to Application Insights, you can view and search these traces in the Application Insights portal, in the [Search][diagnostic] blade.</span></span>

![На портале Application Insights откройте колонку "Поиск".](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="ada88-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ada88-146">Next steps</span></span>
<span data-ttu-id="ada88-147">[Поиск по журналу диагностики][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="ada88-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


