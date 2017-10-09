---
title: "aaaExplore Java трассировки журналов в Azure Application Insights | Документы Microsoft"
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
ms.openlocfilehash: e5f8e8c67e57753ba7574b97aa96dbb41db00ce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="1fc2c-103">Просмотр журналов трассировки Java в Application Insights</span><span class="sxs-lookup"><span data-stu-id="1fc2c-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="1fc2c-104">Если вы используете Logback или Log4J (версия 1.2 или 2.0) для трассировки, что журналы трассировки отправляются автоматически tooApplication аналитики, где вы можете анализировать и поиск на них.</span><span class="sxs-lookup"><span data-stu-id="1fc2c-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

## <a name="install-hello-java-sdk"></a><span data-ttu-id="1fc2c-105">Установка пакета SDK для Java hello</span><span class="sxs-lookup"><span data-stu-id="1fc2c-105">Install hello Java SDK</span></span>

<span data-ttu-id="1fc2c-106">Установите пакет [SDK Application Insights для Java][java], если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="1fc2c-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="1fc2c-107">(Если вы не хотите tootrack HTTP-запросов, можно опустить большинство hello XML-файл конфигурации, но необходимо включить по крайней мере hello `InstrumentationKey` элемента.</span><span class="sxs-lookup"><span data-stu-id="1fc2c-107">(If you don't want tootrack HTTP requests, you can omit most of hello .xml configuration file, but you must at least include hello `InstrumentationKey` element.</span></span> <span data-ttu-id="1fc2c-108">Вам также следует вызвать `new TelemetryClient()` tooinitialize hello SDK.)</span><span class="sxs-lookup"><span data-stu-id="1fc2c-108">You should also call `new TelemetryClient()` tooinitialize hello SDK.)</span></span>


## <a name="add-logging-libraries-tooyour-project"></a><span data-ttu-id="1fc2c-109">Добавление проекта tooyour библиотеки ведения журнала</span><span class="sxs-lookup"><span data-stu-id="1fc2c-109">Add logging libraries tooyour project</span></span>
<span data-ttu-id="1fc2c-110">*Выберите подходящий способ hello для проекта.*</span><span class="sxs-lookup"><span data-stu-id="1fc2c-110">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="1fc2c-111">Если вы используете Maven...</span><span class="sxs-lookup"><span data-stu-id="1fc2c-111">If you're using Maven...</span></span>
<span data-ttu-id="1fc2c-112">Если проект уже настроен toouse Maven для сборки, слияние одного следующие фрагменты кода в файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="1fc2c-112">If your project is already set up toouse Maven for build, merge one of hello following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="1fc2c-113">Зависимости проекта hello, hello tooget двоичных файлов, загруженных обновите.</span><span class="sxs-lookup"><span data-stu-id="1fc2c-113">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="1fc2c-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="1fc2c-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="1fc2c-115">*Log4J версии 2.0*</span><span class="sxs-lookup"><span data-stu-id="1fc2c-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="1fc2c-116">*Log4J версии 1.2*</span><span class="sxs-lookup"><span data-stu-id="1fc2c-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="1fc2c-117">Если вы используете Gradle...</span><span class="sxs-lookup"><span data-stu-id="1fc2c-117">If you're using Gradle...</span></span>
<span data-ttu-id="1fc2c-118">Если проект уже настроен toouse Gradle для сборки, добавьте один из следующих строк toohello hello `dependencies` в файл build.gradle:</span><span class="sxs-lookup"><span data-stu-id="1fc2c-118">If your project is already set up toouse Gradle for build, add one of hello following lines toohello `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="1fc2c-119">Зависимости проекта hello, hello tooget двоичных файлов, загруженных обновите.</span><span class="sxs-lookup"><span data-stu-id="1fc2c-119">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="1fc2c-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="1fc2c-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="1fc2c-121">**Log4J версии 2.0**</span><span class="sxs-lookup"><span data-stu-id="1fc2c-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="1fc2c-122">**Log4J версии 1.2**</span><span class="sxs-lookup"><span data-stu-id="1fc2c-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="1fc2c-123">В противном случае...</span><span class="sxs-lookup"><span data-stu-id="1fc2c-123">Otherwise ...</span></span>
<span data-ttu-id="1fc2c-124">Загрузите и извлеките соответствующие аппендера hello, а затем добавьте hello соответствующую библиотеку tooyour проекта:</span><span class="sxs-lookup"><span data-stu-id="1fc2c-124">Download and extract hello appropriate appender, then add hello appropriate library tooyour project:</span></span>

| <span data-ttu-id="1fc2c-125">Средство ведения журнала</span><span class="sxs-lookup"><span data-stu-id="1fc2c-125">Logger</span></span> | <span data-ttu-id="1fc2c-126">Загрузить</span><span class="sxs-lookup"><span data-stu-id="1fc2c-126">Download</span></span> | <span data-ttu-id="1fc2c-127">Библиотека</span><span class="sxs-lookup"><span data-stu-id="1fc2c-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1fc2c-128">Logback</span><span class="sxs-lookup"><span data-stu-id="1fc2c-128">Logback</span></span> |[<span data-ttu-id="1fc2c-129">Пакет SDK с аппендером Logback</span><span class="sxs-lookup"><span data-stu-id="1fc2c-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="1fc2c-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="1fc2c-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="1fc2c-131">Log4J версии 2.0</span><span class="sxs-lookup"><span data-stu-id="1fc2c-131">Log4J v2.0</span></span> |[<span data-ttu-id="1fc2c-132">Пакет SDK с аппендером Log4J версии 2.0</span><span class="sxs-lookup"><span data-stu-id="1fc2c-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="1fc2c-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="1fc2c-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="1fc2c-134">Log4J версии 1.2</span><span class="sxs-lookup"><span data-stu-id="1fc2c-134">Log4j v1.2</span></span> |[<span data-ttu-id="1fc2c-135">Пакет SDK с аппендером Log4J версии 1.2</span><span class="sxs-lookup"><span data-stu-id="1fc2c-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="1fc2c-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="1fc2c-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-hello-appender-tooyour-logging-framework"></a><span data-ttu-id="1fc2c-137">Добавление ведения журнала tooyour аппендера платформы hello</span><span class="sxs-lookup"><span data-stu-id="1fc2c-137">Add hello appender tooyour logging framework</span></span>
<span data-ttu-id="1fc2c-138">toostart начало трассировки, слияния hello соответствующего фрагмента кода toohello Log4J или Logback файла конфигурации:</span><span class="sxs-lookup"><span data-stu-id="1fc2c-138">toostart getting traces, merge hello relevant snippet of code toohello Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="1fc2c-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="1fc2c-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="1fc2c-140">*Log4J версии 2.0*</span><span class="sxs-lookup"><span data-stu-id="1fc2c-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="1fc2c-141">*Log4J версии 1.2*</span><span class="sxs-lookup"><span data-stu-id="1fc2c-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="1fc2c-142">Hello добавители Application Insights можно ссылаться по любой настроенное средство ведения журнала, а не обязательно по hello корневой средство ведения журнала (как показано в примерах кода hello выше).</span><span class="sxs-lookup"><span data-stu-id="1fc2c-142">hello Application Insights appenders can be referenced by any configured logger, and not necessarily by hello root logger (as shown in hello code samples above).</span></span>

## <a name="explore-your-traces-in-hello-application-insights-portal"></a><span data-ttu-id="1fc2c-143">Изучать данные трассировок на портале Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="1fc2c-143">Explore your traces in hello Application Insights portal</span></span>
<span data-ttu-id="1fc2c-144">Теперь, когда вы настроили ваш проект toosend отслеживает tooApplication аналитики, можно просматривать и искать эти данные трассировки в hello портале Application Insights hello [поиска] [ diagnostic] колонку.</span><span class="sxs-lookup"><span data-stu-id="1fc2c-144">Now that you've configured your project toosend traces tooApplication Insights, you can view and search these traces in hello Application Insights portal, in hello [Search][diagnostic] blade.</span></span>

![На портале Application Insights hello откройте раздел поиска](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="1fc2c-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1fc2c-146">Next steps</span></span>
<span data-ttu-id="1fc2c-147">[Поиск по журналу диагностики][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="1fc2c-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


