---
title: "Анализ веб-приложений Java с помощью Azure Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: a75815885d7ccd7cd56db3da2f3f92cae78fe033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="af059-103">Приступая к работе с Application Insights в веб-проекте Java</span><span class="sxs-lookup"><span data-stu-id="af059-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="af059-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) — это расширяемая служба аналитики для разработчиков веб-ресурсов, позволяющая оценивать производительность и использование работающего приложения.</span><span class="sxs-lookup"><span data-stu-id="af059-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand the performance and usage of your live application.</span></span> <span data-ttu-id="af059-105">С ее помощью можно [выявлять и диагностировать проблемы с производительностью и исключения](app-insights-detect-triage-diagnose.md), а также [писать код][api] для отслеживания действий, которые пользователи выполняют с приложением.</span><span class="sxs-lookup"><span data-stu-id="af059-105">Use it to [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] to track what users do with your app.</span></span>

![пример данных](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="af059-107">Надстройка Application Insights поддерживает приложения Java, работающие под управлением Linux, Unix или Windows.</span><span class="sxs-lookup"><span data-stu-id="af059-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="af059-108">Вам необходимы:</span><span class="sxs-lookup"><span data-stu-id="af059-108">You need:</span></span>

* <span data-ttu-id="af059-109">Oracle JRE 1.6 или более поздней версии либо Zulu JRE 1.6 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="af059-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="af059-110">подписка на [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="af059-110">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="af059-111">*Если у вас уже есть развернутое веб-приложение, воспользуйтесь альтернативным способом, который описан в статье о [добавлении пакета SDK на веб-сервер во время выполнения](app-insights-java-live.md). В этом случае вам не нужно повторно компилировать код, но в то же время вы не сможете написать код для отслеживания действий пользователей.*</span><span class="sxs-lookup"><span data-stu-id="af059-111">*If you have a web app that's already live, you could follow the alternative procedure to [add the SDK at runtime in the web server](app-insights-java-live.md). That alternative avoids rebuilding the code, but you don't get the option to write code to track user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="af059-112">1. Получение ключа инструментирования Application Insights</span><span class="sxs-lookup"><span data-stu-id="af059-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="af059-113">Войдите на [портал Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="af059-113">Sign in to the [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="af059-114">Создайте ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="af059-114">Create an Application Insights resource.</span></span> <span data-ttu-id="af059-115">Задайте тип приложения: веб-приложение Java.</span><span class="sxs-lookup"><span data-stu-id="af059-115">Set the application type to Java web application.</span></span>

    ![Введите имя, выберите веб-приложение Java и нажмите кнопку "Создать"](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="af059-117">Найдите ключ инструментирования нового ресурса.</span><span class="sxs-lookup"><span data-stu-id="af059-117">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="af059-118">Далее будет необходимо вставить его в проект кода.</span><span class="sxs-lookup"><span data-stu-id="af059-118">You'll need to paste this key into your code project shortly.</span></span>

    ![В обзоре нового ресурса щелкните "Свойства" и скопируйте ключ инструментирования](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-the-application-insights-sdk-for-java-to-your-project"></a><span data-ttu-id="af059-120">2) Добавление в проект пакета SDK Application Insights для Java</span><span class="sxs-lookup"><span data-stu-id="af059-120">2. Add the Application Insights SDK for Java to your project</span></span>
<span data-ttu-id="af059-121">*Выберите подходящий метод для проекта.*</span><span class="sxs-lookup"><span data-stu-id="af059-121">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-to-create-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="af059-122">Если вы используете Eclipse для создания проекта Maven или динамического веб-проекта…</span><span class="sxs-lookup"><span data-stu-id="af059-122">If you're using Eclipse to create a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="af059-123">Используйте [пакет SDK Application Insights для подключаемого модуля Java][eclipse].</span><span class="sxs-lookup"><span data-stu-id="af059-123">Use the [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="af059-124">Если вы используете Maven...</span><span class="sxs-lookup"><span data-stu-id="af059-124">If you're using Maven...</span></span>
<span data-ttu-id="af059-125">Если проект уже настроен для сборки с использованием Maven, добавьте следующий код в файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="af059-125">If your project is already set up to use Maven for build, merge the following code to your pom.xml file.</span></span>

<span data-ttu-id="af059-126">Затем обновите зависимости проекта, чтобы скачать двоичные файлы.</span><span class="sxs-lookup"><span data-stu-id="af059-126">Then, refresh the project dependencies to get the binaries downloaded.</span></span>

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

* <span data-ttu-id="af059-127">*Ошибки проверки сборки или контрольной суммы?*</span><span class="sxs-lookup"><span data-stu-id="af059-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="af059-128">Попробуйте указать конкретную версию, например `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="af059-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="af059-129">Сведения о последней версии см. в статье [Заметки о выпуске пакета SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) или в [артефактах репозитория Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="af059-129">You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="af059-130">*Требуется обновить пакет SDK до новой версии?*</span><span class="sxs-lookup"><span data-stu-id="af059-130">*Need to update to a new SDK?*</span></span> <span data-ttu-id="af059-131">Обновите зависимости проекта.</span><span class="sxs-lookup"><span data-stu-id="af059-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="af059-132">Если вы используете Gradle...</span><span class="sxs-lookup"><span data-stu-id="af059-132">If you're using Gradle...</span></span>
<span data-ttu-id="af059-133">Если проект уже настроен для сборки с использованием Gradle, добавьте следующий фрагмент кода в файл build.gradle.</span><span class="sxs-lookup"><span data-stu-id="af059-133">If your project is already set up to use Gradle for build, merge the following code to your build.gradle file.</span></span>

<span data-ttu-id="af059-134">Затем обновите зависимости проекта, чтобы скачать двоичные файлы.</span><span class="sxs-lookup"><span data-stu-id="af059-134">Then refresh the project dependencies to get the binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="af059-135">*Ошибки проверки сборки или контрольной суммы? Попробуйте указать конкретную версию, например* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="af059-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="af059-136">*Сведения о последней версии см. в статье [Заметки о выпуске пакета SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="af059-136">*You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="af059-137">*Обновление пакета SDK до новой версии*</span><span class="sxs-lookup"><span data-stu-id="af059-137">*To update to a new SDK*</span></span>
  * <span data-ttu-id="af059-138">Обновите зависимости проекта.</span><span class="sxs-lookup"><span data-stu-id="af059-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="af059-139">В противном случае...</span><span class="sxs-lookup"><span data-stu-id="af059-139">Otherwise ...</span></span>
<span data-ttu-id="af059-140">Вручную добавьте пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="af059-140">Manually add the SDK:</span></span>

1. <span data-ttu-id="af059-141">Загрузите [пакет SDK Application Insights для Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="af059-141">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="af059-142">Извлеките из ZIP-файла двоичные файлы и добавьте их в проект.</span><span class="sxs-lookup"><span data-stu-id="af059-142">Extract the binaries from the zip file and add them to your project.</span></span>

### <a name="questions"></a><span data-ttu-id="af059-143">Вопросы</span><span class="sxs-lookup"><span data-stu-id="af059-143">Questions...</span></span>
* <span data-ttu-id="af059-144">*Каковы отношения между компонентами `-core` и `-web` в ZIP-архиве?*</span><span class="sxs-lookup"><span data-stu-id="af059-144">*What's the relationship between the `-core` and `-web` components in the zip?*</span></span>

  * <span data-ttu-id="af059-145">`applicationinsights-core` предоставляет чистый API.</span><span class="sxs-lookup"><span data-stu-id="af059-145">`applicationinsights-core` gives you the bare API.</span></span> <span data-ttu-id="af059-146">Этот компонент требуется всегда.</span><span class="sxs-lookup"><span data-stu-id="af059-146">You always need this component.</span></span>
  * <span data-ttu-id="af059-147">Компонент `applicationinsights-web` предоставляет метрики для отслеживания количества запросов HTTP и значений времени ответа.</span><span class="sxs-lookup"><span data-stu-id="af059-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="af059-148">Его можно опустить, если автоматический сбор данных телеметрии не требуется,</span><span class="sxs-lookup"><span data-stu-id="af059-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="af059-149">например, если вы хотите написать собственный код сбора данных.</span><span class="sxs-lookup"><span data-stu-id="af059-149">For example, if you want to write your own.</span></span>
* <span data-ttu-id="af059-150">*Чтобы обновить пакет SDK после появления новой версии:*</span><span class="sxs-lookup"><span data-stu-id="af059-150">*To update the SDK when we publish changes*</span></span>

  * <span data-ttu-id="af059-151">Загрузите последнюю версию [пакета SDK Application Insights для Java](https://aka.ms/qqkaq6) и установите ее вместо более старых версий.</span><span class="sxs-lookup"><span data-stu-id="af059-151">Download the latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace the old ones.</span></span>
  * <span data-ttu-id="af059-152">Изменения описаны в статье [Заметки о выпуске пакета SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="af059-152">Changes are described in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="af059-153">3. Добавление XML-файла Application Insights</span><span class="sxs-lookup"><span data-stu-id="af059-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="af059-154">Добавьте ApplicationInsights.xml в папку ресурсов проекта или проверьте, добавлен ли этот файл в путь класса развертывания проекта.</span><span class="sxs-lookup"><span data-stu-id="af059-154">Add ApplicationInsights.xml to the resources folder in your project, or make sure it is added to your project’s deployment class path.</span></span> <span data-ttu-id="af059-155">Скопируйте в него следующий код XML.</span><span class="sxs-lookup"><span data-stu-id="af059-155">Copy the following XML into it.</span></span>

<span data-ttu-id="af059-156">Замените ключ инструментирования на полученный в портале Azure.</span><span class="sxs-lookup"><span data-stu-id="af059-156">Substitute the instrumentation key that you got from the Azure portal.</span></span>

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


* <span data-ttu-id="af059-157">Ключ инструментирования пересылается вместе с каждым элементом телеметрии; служба Application Insights отобразит его в ресурсе.</span><span class="sxs-lookup"><span data-stu-id="af059-157">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="af059-158">Компонент HTTP-запросов является необязательным.</span><span class="sxs-lookup"><span data-stu-id="af059-158">The HTTP Request component is optional.</span></span> <span data-ttu-id="af059-159">Он автоматически передает на портал телеметрию о запросах и значения времени ответа.</span><span class="sxs-lookup"><span data-stu-id="af059-159">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="af059-160">Корреляционные данные для событий являются дополнением к компоненту HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="af059-160">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="af059-161">Это дополнение назначает идентификатор для каждого запроса, полученного сервером, и добавляет его в качестве свойства каждого элемента телеметрии в форме "Операция.ИД".</span><span class="sxs-lookup"><span data-stu-id="af059-161">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="af059-162">Благодаря этому можно выделить данные телеметрии, связанные с каждым из запросов. Для этого нужно установить фильтр [Diagnostic search][diagnostic] (Поиск по журналу диагностики).</span><span class="sxs-lookup"><span data-stu-id="af059-162">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="af059-163">Ключ Application Insights можно динамически передать с портала Azure в качестве свойства системы (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span><span class="sxs-lookup"><span data-stu-id="af059-163">The Application Insights key can be passed dynamically from the Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="af059-164">Если свойство не указано, оно проверяет Azure Appsetting на наличие переменной среды (APPLICATION_INSIGHTS_IKEY).</span><span class="sxs-lookup"><span data-stu-id="af059-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="af059-165">Если оба свойства не определены, по умолчанию используется InstrumentationKey из ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="af059-165">If both the properties are undefined, the default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="af059-166">Эта последовательность позволяет динамически управлять разными ключами InstrumentationKey для разных сред.</span><span class="sxs-lookup"><span data-stu-id="af059-166">This sequence helps you to manage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-to-set-the-instrumentation-key"></a><span data-ttu-id="af059-167">Другие способы задать ключ инструментирования</span><span class="sxs-lookup"><span data-stu-id="af059-167">Alternative ways to set the instrumentation key</span></span>
<span data-ttu-id="af059-168">Пакет SDK Application Insights ищет ключ в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="af059-168">Application Insights SDK looks for the key in this order:</span></span>

1. <span data-ttu-id="af059-169">Системное свойство: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="af059-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="af059-170">Переменная среды: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="af059-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="af059-171">Файл конфигурации: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="af059-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="af059-172">Вы также можете [задать его в коде](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="af059-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="af059-173">4. Добавление фильтра HTTP</span><span class="sxs-lookup"><span data-stu-id="af059-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="af059-174">Последний шаг настройки позволяет компоненту HTTP-запросов выполнить протоколирование каждого веб-запроса.</span><span class="sxs-lookup"><span data-stu-id="af059-174">The last configuration step allows the HTTP request component to log each web request.</span></span> <span data-ttu-id="af059-175">(Не обязательно, если используется только упрощенный интерфейс API.)</span><span class="sxs-lookup"><span data-stu-id="af059-175">(Not required if you just want the bare API.)</span></span>

<span data-ttu-id="af059-176">Найдите и откройте файл web.xml в проекте, добавьте следующий фрагмент кода в узел web-app, где настраиваются фильтры вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="af059-176">Locate and open the web.xml file in your project, and merge the following code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="af059-177">Для получения наиболее точных результатов этот фильтр должен применяться до всех остальных фильтров.</span><span class="sxs-lookup"><span data-stu-id="af059-177">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="af059-178">Если вы используете Spring Web MVC 3.1 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="af059-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="af059-179">Для включения пакета Application Insights измените следующие элементы в *-servlet.xml:</span><span class="sxs-lookup"><span data-stu-id="af059-179">Edit these elements in *-servlet.xml to include the Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="af059-180">Если вы используете Struts 2</span><span class="sxs-lookup"><span data-stu-id="af059-180">If you're using Struts 2</span></span>
<span data-ttu-id="af059-181">Добавьте в файл конфигурации Struts следующий элемент (обычно называется struts.xml или struts-default.xml):</span><span class="sxs-lookup"><span data-stu-id="af059-181">Add this item to the Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="af059-182">(При наличии перехватчиков, определенных в стандартном стеке, перехватчик можно просто добавить в стек.)</span><span class="sxs-lookup"><span data-stu-id="af059-182">(If you have interceptors defined in a default stack, the interceptor can simply be added to that stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="af059-183">5. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="af059-183">5. Run your application</span></span>
<span data-ttu-id="af059-184">Запустите приложение в режиме отладки на компьютере разработки или опубликуйте его на своем сервере.</span><span class="sxs-lookup"><span data-stu-id="af059-184">Either run it in debug mode on your development machine, or publish to your server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="af059-185">6. Просмотр данных телеметрии в Application Insights</span><span class="sxs-lookup"><span data-stu-id="af059-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="af059-186">Вернитесь к ресурсу Application Insights на [портале Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="af059-186">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="af059-187">В колонке обзора появятся данные HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="af059-187">HTTP requests data appears on the overview blade.</span></span> <span data-ttu-id="af059-188">(Если данные отсутствуют, подождите несколько секунд и нажмите кнопку обновления).</span><span class="sxs-lookup"><span data-stu-id="af059-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![пример данных](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="af059-190">[Дополнительные сведения о метриках.][metrics]</span><span class="sxs-lookup"><span data-stu-id="af059-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="af059-191">Щелкните любую диаграмму, чтобы увидеть более подробные агрегированные метрики.</span><span class="sxs-lookup"><span data-stu-id="af059-191">Click through any chart to see more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="af059-192">Служба Application Insights предполагает, что HTTP-запросы для приложений MVC имеют следующий формат: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="af059-192">Application Insights assumes the format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="af059-193">Например, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` и `GET Home/Product/sdf96vws` сгруппированы в `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="af059-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="af059-194">Это позволяет осмысленно группировать запросы, получая, например, число запросов и среднее время выполнения запросов.</span><span class="sxs-lookup"><span data-stu-id="af059-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="af059-195">Данные экземпляров</span><span class="sxs-lookup"><span data-stu-id="af059-195">Instance data</span></span>
<span data-ttu-id="af059-196">Щелкните тип запроса, чтобы просмотреть отдельные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="af059-196">Click through a specific request type to see individual instances.</span></span>

<span data-ttu-id="af059-197">В Application Insights отображаются два типа данных: 1) объединенные данные, хранимые и отображаемые как средние значения, количества и суммы; 2) данные экземпляров, например отдельные отчеты HTTP-запросов, исключения, число просмотров страниц или пользовательские события.</span><span class="sxs-lookup"><span data-stu-id="af059-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="af059-198">При просмотре свойств запроса можно увидеть связанные с ним события телеметрии, например запросы и исключения.</span><span class="sxs-lookup"><span data-stu-id="af059-198">When viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="af059-199">Аналитика: мощный язык запросов</span><span class="sxs-lookup"><span data-stu-id="af059-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="af059-200">По мере увеличения объема накопленных данных вы сможете использовать запросы для объедения данных и поиска отдельных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="af059-200">As you accumulate more data, you can run queries both to aggregate data and to find individual instances.</span></span>  <span data-ttu-id="af059-201">[Аналитика](app-insights-analytics.md) — это мощный инструмент, который не только позволяет изучать сведения о производительности и использовании, но и диагностировать возможные неполадки.</span><span class="sxs-lookup"><span data-stu-id="af059-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Пример аналитики](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-the-server"></a><span data-ttu-id="af059-203">7. Установка приложения на сервере</span><span class="sxs-lookup"><span data-stu-id="af059-203">7. Install your app on the server</span></span>
<span data-ttu-id="af059-204">Теперь опубликуйте приложение на сервере, откройте доступ для пользователей и изучайте телеметрию на портале.</span><span class="sxs-lookup"><span data-stu-id="af059-204">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="af059-205">Убедитесь, что брандмауэр позволяет приложению отправлять телеметрию на следующие порты:</span><span class="sxs-lookup"><span data-stu-id="af059-205">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="af059-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="af059-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="af059-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="af059-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="af059-208">Если исходящий трафик должен проходить через брандмауэр, определите системные свойства `http.proxyHost` и `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="af059-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="af059-209">На серверах Windows необходимо установить следующее:</span><span class="sxs-lookup"><span data-stu-id="af059-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="af059-210">распространяемые компоненты Microsoft Visual C++.</span><span class="sxs-lookup"><span data-stu-id="af059-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="af059-211">(Сюда входят счетчики производительности).</span><span class="sxs-lookup"><span data-stu-id="af059-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="af059-212">Исключения и ошибки запросов</span><span class="sxs-lookup"><span data-stu-id="af059-212">Exceptions and request failures</span></span>
<span data-ttu-id="af059-213">Необработанные исключения автоматически фиксируются:</span><span class="sxs-lookup"><span data-stu-id="af059-213">Unhandled exceptions are automatically collected:</span></span>

![Последовательно выберите элементы "Параметры" и "Сбои".](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="af059-215">Для сбора данных по другим исключениям доступны два варианта:</span><span class="sxs-lookup"><span data-stu-id="af059-215">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="af059-216">[вставить в код вызовы функции trackException()][apiexceptions];</span><span class="sxs-lookup"><span data-stu-id="af059-216">[Insert calls to trackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="af059-217">[установить на сервере агент для Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="af059-217">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="af059-218">Необходимо указать методы, которые требуется отслеживать.</span><span class="sxs-lookup"><span data-stu-id="af059-218">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="af059-219">Мониторинг вызовов методов и внешних зависимостей.</span><span class="sxs-lookup"><span data-stu-id="af059-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="af059-220">[установить агент для Java](app-insights-java-agent.md) .</span><span class="sxs-lookup"><span data-stu-id="af059-220">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="af059-221">Счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="af059-221">Performance counters</span></span>
<span data-ttu-id="af059-222">Чтобы отобразить диапазон счетчиков производительности, щелкните **Параметры**, **Серверы**.</span><span class="sxs-lookup"><span data-stu-id="af059-222">Open **Settings**, **Servers**, to see a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="af059-223">Настройка сбора данных счетчиками производительности</span><span class="sxs-lookup"><span data-stu-id="af059-223">Customize performance counter collection</span></span>
<span data-ttu-id="af059-224">Чтобы отключить сбор данных стандартным набором счетчиков производительности, добавьте следующий фрагмент кода в корневой узел файла ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="af059-224">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="af059-225">Сбор данных дополнительными счетчиками производительности</span><span class="sxs-lookup"><span data-stu-id="af059-225">Collect additional performance counters</span></span>
<span data-ttu-id="af059-226">Можно задать необходимость сбора данных дополнительными счетчиками производительности.</span><span class="sxs-lookup"><span data-stu-id="af059-226">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="af059-227">Счетчики JMX (предоставляются виртуальной машиной Java)</span><span class="sxs-lookup"><span data-stu-id="af059-227">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="af059-228">`displayName` — имя, отображаемое в портале Application Insights.</span><span class="sxs-lookup"><span data-stu-id="af059-228">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="af059-229">`objectName` — имя объекта JMX.</span><span class="sxs-lookup"><span data-stu-id="af059-229">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="af059-230">`attribute` — атрибут имени объекта JMX для выборки</span><span class="sxs-lookup"><span data-stu-id="af059-230">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="af059-231">`type` (необязательно) — тип атрибута объекта JMX:</span><span class="sxs-lookup"><span data-stu-id="af059-231">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="af059-232">по умолчанию: простой тип, такой как int или long;</span><span class="sxs-lookup"><span data-stu-id="af059-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="af059-233">`composite`— данные счетчика производительности имеют формат "Атрибут.Данные";</span><span class="sxs-lookup"><span data-stu-id="af059-233">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="af059-234">`tabular`— данные счетчика производительности имеют формат строки таблицы.</span><span class="sxs-lookup"><span data-stu-id="af059-234">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="af059-235">Счетчики производительности Windows</span><span class="sxs-lookup"><span data-stu-id="af059-235">Windows performance counters</span></span>
<span data-ttu-id="af059-236">Каждый [счетчик производительности Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) входит в состав категории (аналогично поле является членом класса).</span><span class="sxs-lookup"><span data-stu-id="af059-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="af059-237">Категория может быть глобальной либо иметь пронумерованные или именованные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="af059-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="af059-238">displayName — имя, отображаемое в портале Application Insights.</span><span class="sxs-lookup"><span data-stu-id="af059-238">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="af059-239">categoryName — категория счетчика производительности (объект производительности), с которой связан этот счетчик производительности.</span><span class="sxs-lookup"><span data-stu-id="af059-239">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="af059-240">counterName — имя счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="af059-240">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="af059-241">instanceName — имя экземпляра категории счетчика производительности или пустая строка (""), если категория содержит единственный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="af059-241">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="af059-242">Если categoryName имеет значение "Process", и источником данных для счетчиков производительности является текущий процесс виртуальной машины Java, на которой выполняется ваше приложение, укажите `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="af059-242">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="af059-243">Счетчики производительности отображаются как пользовательские метрики в [обозревателе метрик][metrics].</span><span class="sxs-lookup"><span data-stu-id="af059-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="af059-244">Счетчики производительности Unix</span><span class="sxs-lookup"><span data-stu-id="af059-244">Unix performance counters</span></span>
* <span data-ttu-id="af059-245">[установите collectd с подключаемым модулем Application Insights](app-insights-java-collectd.md) .</span><span class="sxs-lookup"><span data-stu-id="af059-245">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="af059-246">Получение данных о пользователях и сеансах</span><span class="sxs-lookup"><span data-stu-id="af059-246">Get user and session data</span></span>
<span data-ttu-id="af059-247">Итак, вы отправляете телеметрию с веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="af059-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="af059-248">Теперь для получения полного представления о приложении можно настроить дополнительные функции мониторинга:</span><span class="sxs-lookup"><span data-stu-id="af059-248">Now to get the full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="af059-249">[Добавьте телеметрию на веб-страницы][usage] для мониторинга просмотров страниц и метрик пользователя.</span><span class="sxs-lookup"><span data-stu-id="af059-249">[Add telemetry to your web pages][usage] to monitor page views and user metrics.</span></span>
* <span data-ttu-id="af059-250">[Настройте веб-тесты][availability], которые помогут быть уверенными в том, что приложение остается работоспособным и правильно отвечает на запросы.</span><span class="sxs-lookup"><span data-stu-id="af059-250">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="af059-251">Журнал трассировки</span><span class="sxs-lookup"><span data-stu-id="af059-251">Capture log traces</span></span>
<span data-ttu-id="af059-252">Службу Application Insights можно использовать для протоколирования продольных и поперечных срезов данных из Log4J, Logback или других платформ ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="af059-252">You can use Application Insights to slice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="af059-253">Записи журналов можно соотносить с HTTP-запросами и другими данными телеметрии.</span><span class="sxs-lookup"><span data-stu-id="af059-253">You can correlate the logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="af059-254">[Подробнее][javalogs].</span><span class="sxs-lookup"><span data-stu-id="af059-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="af059-255">Отправка собственных данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="af059-255">Send your own telemetry</span></span>
<span data-ttu-id="af059-256">После установки пакета SDK можно использовать интерфейс API для отправки собственных данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="af059-256">Now that you've installed the SDK, you can use the API to send your own telemetry.</span></span>

* <span data-ttu-id="af059-257">[Отслеживайте пользовательские события и метрики][api], чтобы знать, какие операции выполняют пользователи в приложении.</span><span class="sxs-lookup"><span data-stu-id="af059-257">[Track custom events and metrics][api] to learn what users are doing with your application.</span></span>
* <span data-ttu-id="af059-258">[Выполняйте поиск событий и журналов][diagnostic] для диагностики неполадок.</span><span class="sxs-lookup"><span data-stu-id="af059-258">[Search events and logs][diagnostic] to help diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="af059-259">Доступность веб-тестов</span><span class="sxs-lookup"><span data-stu-id="af059-259">Availability web tests</span></span>
<span data-ttu-id="af059-260">Application Insights может тестировать ваш веб-сайт через равные промежутки времени для проверки, работает ли он и правильно ли отвечает на запросы.</span><span class="sxs-lookup"><span data-stu-id="af059-260">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="af059-261">[Чтобы выполнить настройку][availability], щелкните "Веб-тесты".</span><span class="sxs-lookup"><span data-stu-id="af059-261">[To set up][availability], click Web tests.</span></span>

![Щелкните "Веб-тесты", а затем — "Добавить веб-тест".](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="af059-263">Если ваш сайт выйдет из строя, вы получите диаграмму значений времени ответа, а также уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="af059-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Пример веб-теста](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="af059-265">[Дополнительные сведения о веб-тестах для определения доступности.][availability]</span><span class="sxs-lookup"><span data-stu-id="af059-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="af059-266">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="af059-266">Questions?</span></span> <span data-ttu-id="af059-267">Проблемы?</span><span class="sxs-lookup"><span data-stu-id="af059-267">Problems?</span></span>
[<span data-ttu-id="af059-268">Устранение неполадок Java</span><span class="sxs-lookup"><span data-stu-id="af059-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="af059-269">Видео</span><span class="sxs-lookup"><span data-stu-id="af059-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="af059-270">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af059-270">Next steps</span></span>
* [<span data-ttu-id="af059-271">Отслеживайте вызовы зависимостей.</span><span class="sxs-lookup"><span data-stu-id="af059-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="af059-272">Отслеживайте счетчики производительности Unix.</span><span class="sxs-lookup"><span data-stu-id="af059-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="af059-273">Добавляйте [мониторинг на веб-страницы](app-insights-javascript.md), чтобы отслеживать время загрузки страниц, вызовы AJAX и исключения браузера.</span><span class="sxs-lookup"><span data-stu-id="af059-273">Add [monitoring to your web pages](app-insights-javascript.md) to monitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="af059-274">Пишите [пользовательскую телеметрию](app-insights-api-custom-events-metrics.md) для отслеживания использования в браузере или на сервере.</span><span class="sxs-lookup"><span data-stu-id="af059-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) to track usage in the browser or at the server.</span></span>
* <span data-ttu-id="af059-275">Создавайте [панели мониторинга](app-insights-dashboards.md) для объединения основных диаграмм, позволяющих выполнять мониторинг системы.</span><span class="sxs-lookup"><span data-stu-id="af059-275">Create [dashboards](app-insights-dashboards.md) to bring together the key charts for monitoring your system.</span></span>
* <span data-ttu-id="af059-276">Используйте [аналитику](app-insights-analytics.md), чтобы выполнять эффективные запросы телеметрии из приложения.</span><span class="sxs-lookup"><span data-stu-id="af059-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="af059-277">Дополнительные сведения см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).</span><span class="sxs-lookup"><span data-stu-id="af059-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
