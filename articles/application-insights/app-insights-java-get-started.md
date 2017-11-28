---
title: "aaaJava веб-приложение аналитики с помощью Azure Application Insights | Документы Microsoft"
description: "Сведения о мониторинге производительности веб-приложений Java с помощью Application Insights. "
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="a403e-103">Приступая к работе с Application Insights в веб-проекте Java</span><span class="sxs-lookup"><span data-stu-id="a403e-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="a403e-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) -это служба расширенного analytics для веб-разработчиков, которая помогает понять hello производительности и использовании работающего приложения.</span><span class="sxs-lookup"><span data-stu-id="a403e-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand hello performance and usage of your live application.</span></span> <span data-ttu-id="a403e-105">Также использовать[обнаружение и диагностика проблем производительности и исключений](app-insights-detect-triage-diagnose.md), и [писать код] [ api] tootrack, каких пользователей следует вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="a403e-105">Use it too[detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] tootrack what users do with your app.</span></span>

![пример данных](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="a403e-107">Надстройка Application Insights поддерживает приложения Java, работающие под управлением Linux, Unix или Windows.</span><span class="sxs-lookup"><span data-stu-id="a403e-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="a403e-108">Вам необходимы:</span><span class="sxs-lookup"><span data-stu-id="a403e-108">You need:</span></span>

* <span data-ttu-id="a403e-109">Oracle JRE 1.6 или более поздней версии либо Zulu JRE 1.6 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="a403e-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="a403e-110">Подписка слишком[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a403e-110">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="a403e-111">*Если у вас есть веб-приложения, которые уже существуют, могут следовать альтернативная процедура hello слишком[добавить hello SDK во время выполнения в веб-сервере hello](app-insights-java-live.md). Этот вариант позволяет избежать повторного построения кода hello, но не получаете hello параметр toowrite кода tootrack активности пользователей.*</span><span class="sxs-lookup"><span data-stu-id="a403e-111">*If you have a web app that's already live, you could follow hello alternative procedure too[add hello SDK at runtime in hello web server](app-insights-java-live.md). That alternative avoids rebuilding hello code, but you don't get hello option toowrite code tootrack user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="a403e-112">1. Получение ключа инструментирования Application Insights</span><span class="sxs-lookup"><span data-stu-id="a403e-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="a403e-113">Войдите в toohello [портал Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a403e-113">Sign in toohello [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a403e-114">Создайте ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a403e-114">Create an Application Insights resource.</span></span> <span data-ttu-id="a403e-115">Задать hello приложения типа tooJava веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a403e-115">Set hello application type tooJava web application.</span></span>

    ![Введите имя, выберите веб-приложение Java и нажмите кнопку "Создать"](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="a403e-117">Найти ключ инструментирования hello hello нового ресурса.</span><span class="sxs-lookup"><span data-stu-id="a403e-117">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="a403e-118">Вам потребуется toopaste этот ключ в проект кода чуть ниже.</span><span class="sxs-lookup"><span data-stu-id="a403e-118">You'll need toopaste this key into your code project shortly.</span></span>

    ![Обзор нового ресурса hello нажмите кнопку Свойства и скопируйте hello ключ инструментирования](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a><span data-ttu-id="a403e-120">2. Добавить hello пакет SDK Application Insights для Java tooyour проекта</span><span class="sxs-lookup"><span data-stu-id="a403e-120">2. Add hello Application Insights SDK for Java tooyour project</span></span>
<span data-ttu-id="a403e-121">*Выберите подходящий способ hello для проекта.*</span><span class="sxs-lookup"><span data-stu-id="a403e-121">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="a403e-122">Если вы используете Eclipse toocreate Maven или динамических веб-проекта...</span><span class="sxs-lookup"><span data-stu-id="a403e-122">If you're using Eclipse toocreate a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="a403e-123">Используйте hello [пакет SDK Application Insights для Java подключаемый модуль][eclipse].</span><span class="sxs-lookup"><span data-stu-id="a403e-123">Use hello [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="a403e-124">Если вы используете Maven...</span><span class="sxs-lookup"><span data-stu-id="a403e-124">If you're using Maven...</span></span>
<span data-ttu-id="a403e-125">Если проект уже настроен toouse Maven для сборки, объединить следующие файл pom.xml tooyour кода hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-125">If your project is already set up toouse Maven for build, merge hello following code tooyour pom.xml file.</span></span>

<span data-ttu-id="a403e-126">Затем загрузить обновления hello проекта зависимости tooget hello двоичных файлов.</span><span class="sxs-lookup"><span data-stu-id="a403e-126">Then, refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* <span data-ttu-id="a403e-127">*Ошибки проверки сборки или контрольной суммы?*</span><span class="sxs-lookup"><span data-stu-id="a403e-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="a403e-128">Попробуйте указать конкретную версию, например `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="a403e-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="a403e-129">Вы найдете последние версии hello hello [заметки о выпуске пакета SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) или в нашем [Maven артефакты](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="a403e-129">You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="a403e-130">*Требуется tooupdate tooa новый пакет SDK?*</span><span class="sxs-lookup"><span data-stu-id="a403e-130">*Need tooupdate tooa new SDK?*</span></span> <span data-ttu-id="a403e-131">Обновите зависимости проекта.</span><span class="sxs-lookup"><span data-stu-id="a403e-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="a403e-132">Если вы используете Gradle...</span><span class="sxs-lookup"><span data-stu-id="a403e-132">If you're using Gradle...</span></span>
<span data-ttu-id="a403e-133">Если проект уже настроен toouse Gradle для сборки, объединить следующие файл build.gradle tooyour кода hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-133">If your project is already set up toouse Gradle for build, merge hello following code tooyour build.gradle file.</span></span>

<span data-ttu-id="a403e-134">Затем обновления hello проекта зависимости tooget hello двоичные файлы загружаются.</span><span class="sxs-lookup"><span data-stu-id="a403e-134">Then refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="a403e-135">*Ошибки проверки сборки или контрольной суммы? Попробуйте указать конкретную версию, например* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="a403e-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="a403e-136">*Вы найдете последние версии hello hello [заметки о выпуске пакета SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="a403e-136">*You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="a403e-137">*tooupdate tooa новый пакет SDK*</span><span class="sxs-lookup"><span data-stu-id="a403e-137">*tooupdate tooa new SDK*</span></span>
  * <span data-ttu-id="a403e-138">Обновите зависимости проекта.</span><span class="sxs-lookup"><span data-stu-id="a403e-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="a403e-139">В противном случае...</span><span class="sxs-lookup"><span data-stu-id="a403e-139">Otherwise ...</span></span>
<span data-ttu-id="a403e-140">Вручную добавьте hello SDK:</span><span class="sxs-lookup"><span data-stu-id="a403e-140">Manually add hello SDK:</span></span>

1. <span data-ttu-id="a403e-141">Загрузите hello [пакет SDK Application Insights для Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="a403e-141">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="a403e-142">Извлечь hello двоичные файлы из ZIP-файла hello и добавить их tooyour проекта.</span><span class="sxs-lookup"><span data-stu-id="a403e-142">Extract hello binaries from hello zip file and add them tooyour project.</span></span>

### <a name="questions"></a><span data-ttu-id="a403e-143">Вопросы</span><span class="sxs-lookup"><span data-stu-id="a403e-143">Questions...</span></span>
* <span data-ttu-id="a403e-144">*Какова связь hello hello `-core` и `-web` компоненты в hello архив?*</span><span class="sxs-lookup"><span data-stu-id="a403e-144">*What's hello relationship between hello `-core` and `-web` components in hello zip?*</span></span>

  * <span data-ttu-id="a403e-145">`applicationinsights-core`предоставляет hello API состояния системы.</span><span class="sxs-lookup"><span data-stu-id="a403e-145">`applicationinsights-core` gives you hello bare API.</span></span> <span data-ttu-id="a403e-146">Этот компонент требуется всегда.</span><span class="sxs-lookup"><span data-stu-id="a403e-146">You always need this component.</span></span>
  * <span data-ttu-id="a403e-147">Компонент `applicationinsights-web` предоставляет метрики для отслеживания количества запросов HTTP и значений времени ответа.</span><span class="sxs-lookup"><span data-stu-id="a403e-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="a403e-148">Его можно опустить, если автоматический сбор данных телеметрии не требуется,</span><span class="sxs-lookup"><span data-stu-id="a403e-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="a403e-149">Например, если требуется toowrite свои собственные.</span><span class="sxs-lookup"><span data-stu-id="a403e-149">For example, if you want toowrite your own.</span></span>
* <span data-ttu-id="a403e-150">*hello tooupdate пакета SDK, когда мы публикации изменений*</span><span class="sxs-lookup"><span data-stu-id="a403e-150">*tooupdate hello SDK when we publish changes*</span></span>

  * <span data-ttu-id="a403e-151">Загрузить последний hello [пакет SDK Application Insights для Java](https://aka.ms/qqkaq6) и замены старых hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-151">Download hello latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace hello old ones.</span></span>
  * <span data-ttu-id="a403e-152">Описываются изменения в hello [заметки о выпуске пакета SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="a403e-152">Changes are described in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="a403e-153">3. Добавление XML-файла Application Insights</span><span class="sxs-lookup"><span data-stu-id="a403e-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="a403e-154">Добавьте в проект папку resources toohello ApplicationInsights.xml или убедитесь, что он добавляется путь класса tooyour проекта развертывания.</span><span class="sxs-lookup"><span data-stu-id="a403e-154">Add ApplicationInsights.xml toohello resources folder in your project, or make sure it is added tooyour project’s deployment class path.</span></span> <span data-ttu-id="a403e-155">Скопируйте следующий XML-код в него hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-155">Copy hello following XML into it.</span></span>

<span data-ttu-id="a403e-156">Заменить ключ инструментирования hello, полученного от hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a403e-156">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* <span data-ttu-id="a403e-157">ключ инструментирования Hello отправляется вместе с каждого элемента телеметрии и сообщает toodisplay Application Insights в ресурс.</span><span class="sxs-lookup"><span data-stu-id="a403e-157">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="a403e-158">Hello HTTP-запроса компонент является необязательным.</span><span class="sxs-lookup"><span data-stu-id="a403e-158">hello HTTP Request component is optional.</span></span> <span data-ttu-id="a403e-159">Он автоматически отправляет телеметрии о запросах и портал toohello времени ответа.</span><span class="sxs-lookup"><span data-stu-id="a403e-159">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="a403e-160">Корреляция событий является компонентом запроса HTTP toohello сложения.</span><span class="sxs-lookup"><span data-stu-id="a403e-160">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="a403e-161">Он назначает tooeach идентификатор запроса, полученных сервером hello и добавляет этот идентификатор как элемент свойства tooevery телеметрии как свойство hello «Operation.Id».</span><span class="sxs-lookup"><span data-stu-id="a403e-161">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="a403e-162">Позволяет toocorrelate hello телеметрии, связанные с каждым запросом, можно установить фильтр в [диагностики поиска][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="a403e-162">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="a403e-163">ключ Hello Application Insights можно передать динамически из hello портал Azure как свойство системы (-DAPPLICATION_INSIGHTS_IKEY = your_ikey).</span><span class="sxs-lookup"><span data-stu-id="a403e-163">hello Application Insights key can be passed dynamically from hello Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="a403e-164">Если свойство не указано, оно проверяет Azure Appsetting на наличие переменной среды (APPLICATION_INSIGHTS_IKEY).</span><span class="sxs-lookup"><span data-stu-id="a403e-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="a403e-165">Если оба свойства hello не определены, по умолчанию hello InstrumentationKey используется из ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="a403e-165">If both hello properties are undefined, hello default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="a403e-166">Эта последовательность помогает toomanage различные InstrumentationKeys для различных сред динамически.</span><span class="sxs-lookup"><span data-stu-id="a403e-166">This sequence helps you toomanage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a><span data-ttu-id="a403e-167">Ключ инструментирования альтернативные способы tooset hello</span><span class="sxs-lookup"><span data-stu-id="a403e-167">Alternative ways tooset hello instrumentation key</span></span>
<span data-ttu-id="a403e-168">Пакет SDK для Application Insights ищет ключ hello в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="a403e-168">Application Insights SDK looks for hello key in this order:</span></span>

1. <span data-ttu-id="a403e-169">Системное свойство: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="a403e-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="a403e-170">Переменная среды: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="a403e-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="a403e-171">Файл конфигурации: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="a403e-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="a403e-172">Вы также можете [задать его в коде](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="a403e-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="a403e-173">4. Добавление фильтра HTTP</span><span class="sxs-lookup"><span data-stu-id="a403e-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="a403e-174">Последний шаг настройки Hello позволяет toolog компонент запроса HTTP hello каждого веб-запроса.</span><span class="sxs-lookup"><span data-stu-id="a403e-174">hello last configuration step allows hello HTTP request component toolog each web request.</span></span> <span data-ttu-id="a403e-175">(Не обязательно, если только состояния системы API hello.)</span><span class="sxs-lookup"><span data-stu-id="a403e-175">(Not required if you just want hello bare API.)</span></span>

<span data-ttu-id="a403e-176">Найдите и откройте файл web.xml hello в проекте, а следующий код в узле веб-приложения hello, где настраиваются фильтры приложения hello слияния.</span><span class="sxs-lookup"><span data-stu-id="a403e-176">Locate and open hello web.xml file in your project, and merge hello following code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="a403e-177">Прежде чем все остальные фильтры должны сопоставляться tooget hello наиболее точные результаты, фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-177">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="a403e-178">Если вы используете Spring Web MVC 3.1 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="a403e-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="a403e-179">Изменять эти элементы в *-servlet.xml tooinclude hello Application Insights пакета:</span><span class="sxs-lookup"><span data-stu-id="a403e-179">Edit these elements in *-servlet.xml tooinclude hello Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="a403e-180">Если вы используете Struts 2</span><span class="sxs-lookup"><span data-stu-id="a403e-180">If you're using Struts 2</span></span>
<span data-ttu-id="a403e-181">Добавьте этот элемент toohello Struts файл конфигурации (обычно именованный struts.xml или struts default.xml):</span><span class="sxs-lookup"><span data-stu-id="a403e-181">Add this item toohello Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="a403e-182">(При наличии перехватчики, определенные в стек по умолчанию hello перехватчик можно просто добавить стека toothat.)</span><span class="sxs-lookup"><span data-stu-id="a403e-182">(If you have interceptors defined in a default stack, hello interceptor can simply be added toothat stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="a403e-183">5. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="a403e-183">5. Run your application</span></span>
<span data-ttu-id="a403e-184">Возможно, запустите его в режиме отладки на компьютере разработки или публикации tooyour сервера.</span><span class="sxs-lookup"><span data-stu-id="a403e-184">Either run it in debug mode on your development machine, or publish tooyour server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="a403e-185">6. Просмотр данных телеметрии в Application Insights</span><span class="sxs-lookup"><span data-stu-id="a403e-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="a403e-186">Вернуть ресурс Application Insights tooyour в [портал Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a403e-186">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="a403e-187">HTTP-запросы данных появится в колонке Обзор hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-187">HTTP requests data appears on hello overview blade.</span></span> <span data-ttu-id="a403e-188">(Если данные отсутствуют, подождите несколько секунд и нажмите кнопку обновления).</span><span class="sxs-lookup"><span data-stu-id="a403e-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![пример данных](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="a403e-190">[Дополнительные сведения о метриках.][metrics]</span><span class="sxs-lookup"><span data-stu-id="a403e-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="a403e-191">Пройдите по любой более подробные toosee диаграммы суммарный метрики.</span><span class="sxs-lookup"><span data-stu-id="a403e-191">Click through any chart toosee more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="a403e-192">Application Insights предполагает, что формат hello HTTP-запросов для приложений MVC: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="a403e-192">Application Insights assumes hello format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="a403e-193">Например, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` и `GET Home/Product/sdf96vws` сгруппированы в `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="a403e-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="a403e-194">Это позволяет осмысленно группировать запросы, получая, например, число запросов и среднее время выполнения запросов.</span><span class="sxs-lookup"><span data-stu-id="a403e-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="a403e-195">Данные экземпляров</span><span class="sxs-lookup"><span data-stu-id="a403e-195">Instance data</span></span>
<span data-ttu-id="a403e-196">Используйте запрос типа toosee отдельных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="a403e-196">Click through a specific request type toosee individual instances.</span></span>

<span data-ttu-id="a403e-197">В Application Insights отображаются два типа данных: 1) объединенные данные, хранимые и отображаемые как средние значения, количества и суммы; 2) данные экземпляров, например отдельные отчеты HTTP-запросов, исключения, число просмотров страниц или пользовательские события.</span><span class="sxs-lookup"><span data-stu-id="a403e-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="a403e-198">При просмотре свойств hello запроса, можно просмотреть события телеметрии hello, связанные с ним, такие как запросы и исключения.</span><span class="sxs-lookup"><span data-stu-id="a403e-198">When viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="a403e-199">Аналитика: мощный язык запросов</span><span class="sxs-lookup"><span data-stu-id="a403e-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="a403e-200">Как вы накапливают дополнительные данные, можно запустить запросы обоих tooaggregate данных и toofind отдельных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="a403e-200">As you accumulate more data, you can run queries both tooaggregate data and toofind individual instances.</span></span>  <span data-ttu-id="a403e-201">[Аналитика](app-insights-analytics.md) — это мощный инструмент, который не только позволяет изучать сведения о производительности и использовании, но и диагностировать возможные неполадки.</span><span class="sxs-lookup"><span data-stu-id="a403e-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Пример аналитики](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a><span data-ttu-id="a403e-203">7. Для установки приложения на сервере hello</span><span class="sxs-lookup"><span data-stu-id="a403e-203">7. Install your app on hello server</span></span>
<span data-ttu-id="a403e-204">Теперь публикации сервера toohello приложения, позволяют использовать его и посмотреть телеметрии hello отображаются на портале hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-204">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="a403e-205">Убедитесь, что брандмауэр разрешает вашего приложения toosend телеметрии toothese порты:</span><span class="sxs-lookup"><span data-stu-id="a403e-205">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="a403e-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="a403e-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="a403e-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="a403e-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="a403e-208">Если исходящий трафик должен проходить через брандмауэр, определите системные свойства `http.proxyHost` и `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="a403e-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="a403e-209">На серверах Windows необходимо установить следующее:</span><span class="sxs-lookup"><span data-stu-id="a403e-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="a403e-210">распространяемые компоненты Microsoft Visual C++.</span><span class="sxs-lookup"><span data-stu-id="a403e-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="a403e-211">(Сюда входят счетчики производительности).</span><span class="sxs-lookup"><span data-stu-id="a403e-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="a403e-212">Исключения и ошибки запросов</span><span class="sxs-lookup"><span data-stu-id="a403e-212">Exceptions and request failures</span></span>
<span data-ttu-id="a403e-213">Необработанные исключения автоматически фиксируются:</span><span class="sxs-lookup"><span data-stu-id="a403e-213">Unhandled exceptions are automatically collected:</span></span>

![Последовательно выберите элементы "Параметры" и "Сбои".](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="a403e-215">toocollect данные на другие исключения, у вас есть два варианта:</span><span class="sxs-lookup"><span data-stu-id="a403e-215">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="a403e-216">[Вставить tootrackException() вызовы в коде][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="a403e-216">[Insert calls tootrackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="a403e-217">[Установка агента Java hello на сервер](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="a403e-217">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="a403e-218">Можно указать hello методы, которые нужно toowatch.</span><span class="sxs-lookup"><span data-stu-id="a403e-218">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="a403e-219">Мониторинг вызовов методов и внешних зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a403e-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="a403e-220">[Установка агента Java hello](app-insights-java-agent.md) toolog указан внутренние методы и вызовы через JDBC, с данными о времени.</span><span class="sxs-lookup"><span data-stu-id="a403e-220">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="a403e-221">Счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="a403e-221">Performance counters</span></span>
<span data-ttu-id="a403e-222">Откройте **параметры**, **серверы**, toosee широкий набор счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="a403e-222">Open **Settings**, **Servers**, toosee a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="a403e-223">Настройка сбора данных счетчиками производительности</span><span class="sxs-lookup"><span data-stu-id="a403e-223">Customize performance counter collection</span></span>
<span data-ttu-id="a403e-224">Коллекция toodisable hello стандартный набор счетчиков производительности, добавьте следующий код в корневом узле hello файла ApplicationInsights.xml hello hello:</span><span class="sxs-lookup"><span data-stu-id="a403e-224">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="a403e-225">Сбор данных дополнительными счетчиками производительности</span><span class="sxs-lookup"><span data-stu-id="a403e-225">Collect additional performance counters</span></span>
<span data-ttu-id="a403e-226">Можно указать собранных toobe счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="a403e-226">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="a403e-227">Счетчики JMX (предоставляемые hello виртуальной машины Java)</span><span class="sxs-lookup"><span data-stu-id="a403e-227">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="a403e-228">`displayName`— Имя hello, отображается на портале Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-228">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="a403e-229">`objectName`— Имя объекта JMX hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-229">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="a403e-230">`attribute`— атрибут hello объекта имя hello JMX toofetch</span><span class="sxs-lookup"><span data-stu-id="a403e-230">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="a403e-231">`type`(необязательно) — hello тип атрибута JMX объекта:</span><span class="sxs-lookup"><span data-stu-id="a403e-231">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="a403e-232">по умолчанию: простой тип, такой как int или long;</span><span class="sxs-lookup"><span data-stu-id="a403e-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="a403e-233">`composite`: данные счетчика производительности hello находится в формате «Attribute.Data» hello</span><span class="sxs-lookup"><span data-stu-id="a403e-233">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="a403e-234">`tabular`: hello данные счетчика производительности имеет формат hello строки в таблице</span><span class="sxs-lookup"><span data-stu-id="a403e-234">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="a403e-235">Счетчики производительности Windows</span><span class="sxs-lookup"><span data-stu-id="a403e-235">Windows performance counters</span></span>
<span data-ttu-id="a403e-236">Каждый [счетчика производительности Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) входит в категорию (в hello так же, что поле является членом класса).</span><span class="sxs-lookup"><span data-stu-id="a403e-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="a403e-237">Категория может быть глобальной либо иметь пронумерованные или именованные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="a403e-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="a403e-238">отображаемое имя — имя hello, отображается на портале Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-238">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="a403e-239">Категория — hello категории счетчика производительности (производительности объект) с которым связан этот счетчик производительности.</span><span class="sxs-lookup"><span data-stu-id="a403e-239">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="a403e-240">counterName — hello имя счетчика производительности "hello".</span><span class="sxs-lookup"><span data-stu-id="a403e-240">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="a403e-241">instanceName — имя экземпляра категории счетчика производительности hello hello, или пустая строка ("»), если категория hello содержит единственный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="a403e-241">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="a403e-242">Если hello categoryName — процесс, а счетчик производительности hello хотелось бы toocollect от текущего процесса виртуальной машины Java hello на котором выполняется приложение, укажите `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="a403e-242">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="a403e-243">Счетчики производительности отображаются как пользовательские метрики в [обозревателе метрик][metrics].</span><span class="sxs-lookup"><span data-stu-id="a403e-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="a403e-244">Счетчики производительности Unix</span><span class="sxs-lookup"><span data-stu-id="a403e-244">Unix performance counters</span></span>
* <span data-ttu-id="a403e-245">[Установить подключаемый модуль Application Insights hello collectd](app-insights-java-collectd.md) tooget разнообразных данных системы и сети.</span><span class="sxs-lookup"><span data-stu-id="a403e-245">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="a403e-246">Получение данных о пользователях и сеансах</span><span class="sxs-lookup"><span data-stu-id="a403e-246">Get user and session data</span></span>
<span data-ttu-id="a403e-247">Итак, вы отправляете телеметрию с веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="a403e-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="a403e-248">Теперь tooget hello представление полной 360 градусов, приложения, можно добавить более мониторинга:</span><span class="sxs-lookup"><span data-stu-id="a403e-248">Now tooget hello full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="a403e-249">[Добавить веб-страницы телеметрии tooyour] [ usage] toomonitor страницы представлений и метрики пользователь.</span><span class="sxs-lookup"><span data-stu-id="a403e-249">[Add telemetry tooyour web pages][usage] toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="a403e-250">[Настройка веб-тестов] [ availability] toomake убедиться, что приложение остается динамической и отвечать на запросы.</span><span class="sxs-lookup"><span data-stu-id="a403e-250">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="a403e-251">Журнал трассировки</span><span class="sxs-lookup"><span data-stu-id="a403e-251">Capture log traces</span></span>
<span data-ttu-id="a403e-252">Можно использовать tooslice Application Insights и поперечные срезы в журналы с Log4J Logback и других платформ ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="a403e-252">You can use Application Insights tooslice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="a403e-253">Вы можете соотнести журналы hello с HTTP-запросы и другие данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a403e-253">You can correlate hello logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="a403e-254">[Подробнее][javalogs].</span><span class="sxs-lookup"><span data-stu-id="a403e-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="a403e-255">Отправка собственных данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="a403e-255">Send your own telemetry</span></span>
<span data-ttu-id="a403e-256">Установки пакета SDK для hello hello API toosend можно использовать собственные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a403e-256">Now that you've installed hello SDK, you can use hello API toosend your own telemetry.</span></span>

* <span data-ttu-id="a403e-257">[Отслеживать пользовательские события и метрики] [ api] toolearn, какие пользователи делают вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="a403e-257">[Track custom events and metrics][api] toolearn what users are doing with your application.</span></span>
* <span data-ttu-id="a403e-258">[Поиск событий и журналов] [ diagnostic] toohelp диагностики проблем.</span><span class="sxs-lookup"><span data-stu-id="a403e-258">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="a403e-259">Доступность веб-тестов</span><span class="sxs-lookup"><span data-stu-id="a403e-259">Availability web tests</span></span>
<span data-ttu-id="a403e-260">Application Insights можно проверить веб-сайта на toocheck регулярные интервалы, он работает и отвечает хорошо.</span><span class="sxs-lookup"><span data-stu-id="a403e-260">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="a403e-261">[tooset копирование][availability], нажмите кнопку веб-тестов.</span><span class="sxs-lookup"><span data-stu-id="a403e-261">[tooset up][availability], click Web tests.</span></span>

![Щелкните "Веб-тесты", а затем — "Добавить веб-тест".](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="a403e-263">Если ваш сайт выйдет из строя, вы получите диаграмму значений времени ответа, а также уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="a403e-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Пример веб-теста](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="a403e-265">[Дополнительные сведения о веб-тестах для определения доступности.][availability]</span><span class="sxs-lookup"><span data-stu-id="a403e-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="a403e-266">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="a403e-266">Questions?</span></span> <span data-ttu-id="a403e-267">Проблемы?</span><span class="sxs-lookup"><span data-stu-id="a403e-267">Problems?</span></span>
[<span data-ttu-id="a403e-268">Устранение неполадок Java</span><span class="sxs-lookup"><span data-stu-id="a403e-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="a403e-269">Видео</span><span class="sxs-lookup"><span data-stu-id="a403e-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="a403e-270">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a403e-270">Next steps</span></span>
* [<span data-ttu-id="a403e-271">Отслеживайте вызовы зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a403e-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="a403e-272">Отслеживайте счетчики производительности Unix.</span><span class="sxs-lookup"><span data-stu-id="a403e-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="a403e-273">Добавить [наблюдения за веб-страницы tooyour](app-insights-javascript.md) время загрузки страницы toomonitor, вызовы AJAX исключения браузера.</span><span class="sxs-lookup"><span data-stu-id="a403e-273">Add [monitoring tooyour web pages](app-insights-javascript.md) toomonitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="a403e-274">Запись [пользовательского телеметрии](app-insights-api-custom-events-metrics.md) tootrack использование в браузере hello, или на сервере, hello.</span><span class="sxs-lookup"><span data-stu-id="a403e-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) tootrack usage in hello browser or at hello server.</span></span>
* <span data-ttu-id="a403e-275">Создание [панелей мониторинга](app-insights-dashboards.md) toobring вместе hello основные диаграммы для наблюдение за системой.</span><span class="sxs-lookup"><span data-stu-id="a403e-275">Create [dashboards](app-insights-dashboards.md) toobring together hello key charts for monitoring your system.</span></span>
* <span data-ttu-id="a403e-276">Используйте [аналитику](app-insights-analytics.md), чтобы выполнять эффективные запросы телеметрии из приложения.</span><span class="sxs-lookup"><span data-stu-id="a403e-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="a403e-277">Дополнительные сведения см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).</span><span class="sxs-lookup"><span data-stu-id="a403e-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
