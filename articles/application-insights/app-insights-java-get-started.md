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
# <a name="get-started-with-application-insights-in-a-java-web-project"></a>Приступая к работе с Application Insights в веб-проекте Java


[Application Insights](https://azure.microsoft.com/services/application-insights/) -это служба расширенного analytics для веб-разработчиков, которая помогает понять hello производительности и использовании работающего приложения. Также использовать[обнаружение и диагностика проблем производительности и исключений](app-insights-detect-triage-diagnose.md), и [писать код] [ api] tootrack, каких пользователей следует вместе с приложением.

![пример данных](./media/app-insights-java-get-started/5-results.png)

Надстройка Application Insights поддерживает приложения Java, работающие под управлением Linux, Unix или Windows.

Вам необходимы:

* Oracle JRE 1.6 или более поздней версии либо Zulu JRE 1.6 или более поздней версии;
* Подписка слишком[Microsoft Azure](https://azure.microsoft.com/).

*Если у вас есть веб-приложения, которые уже существуют, могут следовать альтернативная процедура hello слишком[добавить hello SDK во время выполнения в веб-сервере hello](app-insights-java-live.md). Этот вариант позволяет избежать повторного построения кода hello, но не получаете hello параметр toowrite кода tootrack активности пользователей.*

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Получение ключа инструментирования Application Insights
1. Войдите в toohello [портал Microsoft Azure](https://portal.azure.com).
2. Создайте ресурс Application Insights. Задать hello приложения типа tooJava веб-приложения.

    ![Введите имя, выберите веб-приложение Java и нажмите кнопку "Создать"](./media/app-insights-java-get-started/02-create.png)
3. Найти ключ инструментирования hello hello нового ресурса. Вам потребуется toopaste этот ключ в проект кода чуть ниже.

    ![Обзор нового ресурса hello нажмите кнопку Свойства и скопируйте hello ключ инструментирования](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a>2. Добавить hello пакет SDK Application Insights для Java tooyour проекта
*Выберите подходящий способ hello для проекта.*

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a>Если вы используете Eclipse toocreate Maven или динамических веб-проекта...
Используйте hello [пакет SDK Application Insights для Java подключаемый модуль][eclipse].

#### <a name="if-youre-using-maven"></a>Если вы используете Maven...
Если проект уже настроен toouse Maven для сборки, объединить следующие файл pom.xml tooyour кода hello.

Затем загрузить обновления hello проекта зависимости tooget hello двоичных файлов.

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

* *Ошибки проверки сборки или контрольной суммы?* Попробуйте указать конкретную версию, например `<version>1.0.n</version>`. Вы найдете последние версии hello hello [заметки о выпуске пакета SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) или в нашем [Maven артефакты](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).
* *Требуется tooupdate tooa новый пакет SDK?* Обновите зависимости проекта.

#### <a name="if-youre-using-gradle"></a>Если вы используете Gradle...
Если проект уже настроен toouse Gradle для сборки, объединить следующие файл build.gradle tooyour кода hello.

Затем обновления hello проекта зависимости tooget hello двоичные файлы загружаются.

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* *Ошибки проверки сборки или контрольной суммы? Попробуйте указать конкретную версию, например* `version:'1.0.n'`. *Вы найдете последние версии hello hello [заметки о выпуске пакета SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*
* *tooupdate tooa новый пакет SDK*
  * Обновите зависимости проекта.

#### <a name="otherwise-"></a>В противном случае...
Вручную добавьте hello SDK:

1. Загрузите hello [пакет SDK Application Insights для Java](https://aka.ms/aijavasdk).
2. Извлечь hello двоичные файлы из ZIP-файла hello и добавить их tooyour проекта.

### <a name="questions"></a>Вопросы
* *Какова связь hello hello `-core` и `-web` компоненты в hello архив?*

  * `applicationinsights-core`предоставляет hello API состояния системы. Этот компонент требуется всегда.
  * Компонент `applicationinsights-web` предоставляет метрики для отслеживания количества запросов HTTP и значений времени ответа. Его можно опустить, если автоматический сбор данных телеметрии не требуется, Например, если требуется toowrite свои собственные.
* *hello tooupdate пакета SDK, когда мы публикации изменений*

  * Загрузить последний hello [пакет SDK Application Insights для Java](https://aka.ms/qqkaq6) и замены старых hello.
  * Описываются изменения в hello [заметки о выпуске пакета SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).

## <a name="3-add-an-application-insights-xml-file"></a>3. Добавление XML-файла Application Insights
Добавьте в проект папку resources toohello ApplicationInsights.xml или убедитесь, что он добавляется путь класса tooyour проекта развертывания. Скопируйте следующий XML-код в него hello.

Заменить ключ инструментирования hello, полученного от hello портал Azure.

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


* ключ инструментирования Hello отправляется вместе с каждого элемента телеметрии и сообщает toodisplay Application Insights в ресурс.
* Hello HTTP-запроса компонент является необязательным. Он автоматически отправляет телеметрии о запросах и портал toohello времени ответа.
* Корреляция событий является компонентом запроса HTTP toohello сложения. Он назначает tooeach идентификатор запроса, полученных сервером hello и добавляет этот идентификатор как элемент свойства tooevery телеметрии как свойство hello «Operation.Id». Позволяет toocorrelate hello телеметрии, связанные с каждым запросом, можно установить фильтр в [диагностики поиска][diagnostic].
* ключ Hello Application Insights можно передать динамически из hello портал Azure как свойство системы (-DAPPLICATION_INSIGHTS_IKEY = your_ikey). Если свойство не указано, оно проверяет Azure Appsetting на наличие переменной среды (APPLICATION_INSIGHTS_IKEY). Если оба свойства hello не определены, по умолчанию hello InstrumentationKey используется из ApplicationInsights.xml. Эта последовательность помогает toomanage различные InstrumentationKeys для различных сред динамически.

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a>Ключ инструментирования альтернативные способы tooset hello
Пакет SDK для Application Insights ищет ключ hello в следующем порядке:

1. Системное свойство: -DAPPLICATION_INSIGHTS_IKEY=your_ikey
2. Переменная среды: APPLICATION_INSIGHTS_IKEY
3. Файл конфигурации: ApplicationInsights.xml

Вы также можете [задать его в коде](app-insights-api-custom-events-metrics.md#ikey):

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a>4. Добавление фильтра HTTP
Последний шаг настройки Hello позволяет toolog компонент запроса HTTP hello каждого веб-запроса. (Не обязательно, если только состояния системы API hello.)

Найдите и откройте файл web.xml hello в проекте, а следующий код в узле веб-приложения hello, где настраиваются фильтры приложения hello слияния.

Прежде чем все остальные фильтры должны сопоставляться tooget hello наиболее точные результаты, фильтр hello.

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a>Если вы используете Spring Web MVC 3.1 или более поздней версии
Изменять эти элементы в *-servlet.xml tooinclude hello Application Insights пакета:

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a>Если вы используете Struts 2
Добавьте этот элемент toohello Struts файл конфигурации (обычно именованный struts.xml или struts default.xml):

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

(При наличии перехватчики, определенные в стек по умолчанию hello перехватчик можно просто добавить стека toothat.)

## <a name="5-run-your-application"></a>5. Запуск приложения
Возможно, запустите его в режиме отладки на компьютере разработки или публикации tooyour сервера.

## <a name="6-view-your-telemetry-in-application-insights"></a>6. Просмотр данных телеметрии в Application Insights
Вернуть ресурс Application Insights tooyour в [портал Microsoft Azure](https://portal.azure.com).

HTTP-запросы данных появится в колонке Обзор hello. (Если данные отсутствуют, подождите несколько секунд и нажмите кнопку обновления).

![пример данных](./media/app-insights-java-get-started/5-results.png)

[Дополнительные сведения о метриках.][metrics]

Пройдите по любой более подробные toosee диаграммы суммарный метрики.

![](./media/app-insights-java-get-started/6-barchart.png)

> Application Insights предполагает, что формат hello HTTP-запросов для приложений MVC: `VERB controller/action`. Например, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` и `GET Home/Product/sdf96vws` сгруппированы в `GET Home/Product`. Это позволяет осмысленно группировать запросы, получая, например, число запросов и среднее время выполнения запросов.
>
>

### <a name="instance-data"></a>Данные экземпляров
Используйте запрос типа toosee отдельных экземпляров.

В Application Insights отображаются два типа данных: 1) объединенные данные, хранимые и отображаемые как средние значения, количества и суммы; 2) данные экземпляров, например отдельные отчеты HTTP-запросов, исключения, число просмотров страниц или пользовательские события.

При просмотре свойств hello запроса, можно просмотреть события телеметрии hello, связанные с ним, такие как запросы и исключения.

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a>Аналитика: мощный язык запросов
Как вы накапливают дополнительные данные, можно запустить запросы обоих tooaggregate данных и toofind отдельных экземпляров.  [Аналитика](app-insights-analytics.md) — это мощный инструмент, который не только позволяет изучать сведения о производительности и использовании, но и диагностировать возможные неполадки.

![Пример аналитики](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a>7. Для установки приложения на сервере hello
Теперь публикации сервера toohello приложения, позволяют использовать его и посмотреть телеметрии hello отображаются на портале hello.

* Убедитесь, что брандмауэр разрешает вашего приложения toosend телеметрии toothese порты:

  * dc.services.visualstudio.com:443
  * f5.services.visualstudio.com:443

* Если исходящий трафик должен проходить через брандмауэр, определите системные свойства `http.proxyHost` и `http.proxyPort`.

* На серверах Windows необходимо установить следующее:

  * [распространяемые компоненты Microsoft Visual C++.](http://www.microsoft.com/download/details.aspx?id=40784)

    (Сюда входят счетчики производительности).


## <a name="exceptions-and-request-failures"></a>Исключения и ошибки запросов
Необработанные исключения автоматически фиксируются:

![Последовательно выберите элементы "Параметры" и "Сбои".](./media/app-insights-java-get-started/21-exceptions.png)

toocollect данные на другие исключения, у вас есть два варианта:

* [Вставить tootrackException() вызовы в коде][apiexceptions].
* [Установка агента Java hello на сервер](app-insights-java-agent.md). Можно указать hello методы, которые нужно toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Мониторинг вызовов методов и внешних зависимостей.
[Установка агента Java hello](app-insights-java-agent.md) toolog указан внутренние методы и вызовы через JDBC, с данными о времени.

## <a name="performance-counters"></a>Счетчики производительности
Откройте **параметры**, **серверы**, toosee широкий набор счетчиков производительности.

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a>Настройка сбора данных счетчиками производительности
Коллекция toodisable hello стандартный набор счетчиков производительности, добавьте следующий код в корневом узле hello файла ApplicationInsights.xml hello hello:

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a>Сбор данных дополнительными счетчиками производительности
Можно указать собранных toobe счетчики производительности.

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a>Счетчики JMX (предоставляемые hello виртуальной машины Java)

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* `displayName`— Имя hello, отображается на портале Application Insights hello.
* `objectName`— Имя объекта JMX hello.
* `attribute`— атрибут hello объекта имя hello JMX toofetch
* `type`(необязательно) — hello тип атрибута JMX объекта:
  * по умолчанию: простой тип, такой как int или long;
  * `composite`: данные счетчика производительности hello находится в формате «Attribute.Data» hello
  * `tabular`: hello данные счетчика производительности имеет формат hello строки в таблице

#### <a name="windows-performance-counters"></a>Счетчики производительности Windows
Каждый [счетчика производительности Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) входит в категорию (в hello так же, что поле является членом класса). Категория может быть глобальной либо иметь пронумерованные или именованные экземпляры.

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* отображаемое имя — имя hello, отображается на портале Application Insights hello.
* Категория — hello категории счетчика производительности (производительности объект) с которым связан этот счетчик производительности.
* counterName — hello имя счетчика производительности "hello".
* instanceName — имя экземпляра категории счетчика производительности hello hello, или пустая строка ("»), если категория hello содержит единственный экземпляр. Если hello categoryName — процесс, а счетчик производительности hello хотелось бы toocollect от текущего процесса виртуальной машины Java hello на котором выполняется приложение, укажите `"__SELF__"`.

Счетчики производительности отображаются как пользовательские метрики в [обозревателе метрик][metrics].

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Счетчики производительности Unix
* [Установить подключаемый модуль Application Insights hello collectd](app-insights-java-collectd.md) tooget разнообразных данных системы и сети.

## <a name="get-user-and-session-data"></a>Получение данных о пользователях и сеансах
Итак, вы отправляете телеметрию с веб-сервера. Теперь tooget hello представление полной 360 градусов, приложения, можно добавить более мониторинга:

* [Добавить веб-страницы телеметрии tooyour] [ usage] toomonitor страницы представлений и метрики пользователь.
* [Настройка веб-тестов] [ availability] toomake убедиться, что приложение остается динамической и отвечать на запросы.

## <a name="capture-log-traces"></a>Журнал трассировки
Можно использовать tooslice Application Insights и поперечные срезы в журналы с Log4J Logback и других платформ ведения журналов. Вы можете соотнести журналы hello с HTTP-запросы и другие данные телеметрии. [Подробнее][javalogs].

## <a name="send-your-own-telemetry"></a>Отправка собственных данных телеметрии
Установки пакета SDK для hello hello API toosend можно использовать собственные телеметрии.

* [Отслеживать пользовательские события и метрики] [ api] toolearn, какие пользователи делают вместе с приложением.
* [Поиск событий и журналов] [ diagnostic] toohelp диагностики проблем.

## <a name="availability-web-tests"></a>Доступность веб-тестов
Application Insights можно проверить веб-сайта на toocheck регулярные интервалы, он работает и отвечает хорошо. [tooset копирование][availability], нажмите кнопку веб-тестов.

![Щелкните "Веб-тесты", а затем — "Добавить веб-тест".](./media/app-insights-java-get-started/31-config-web-test.png)

Если ваш сайт выйдет из строя, вы получите диаграмму значений времени ответа, а также уведомление по электронной почте.

![Пример веб-теста](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

[Дополнительные сведения о веб-тестах для определения доступности.][availability]

## <a name="questions-problems"></a>Вопросы? Проблемы?
[Устранение неполадок Java](app-insights-java-troubleshoot.md)

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Дальнейшие действия
* [Отслеживайте вызовы зависимостей.](app-insights-java-agent.md)
* [Отслеживайте счетчики производительности Unix.](app-insights-java-collectd.md)
* Добавить [наблюдения за веб-страницы tooyour](app-insights-javascript.md) время загрузки страницы toomonitor, вызовы AJAX исключения браузера.
* Запись [пользовательского телеметрии](app-insights-api-custom-events-metrics.md) tootrack использование в браузере hello, или на сервере, hello.
* Создание [панелей мониторинга](app-insights-dashboards.md) toobring вместе hello основные диаграммы для наблюдение за системой.
* Используйте [аналитику](app-insights-analytics.md), чтобы выполнять эффективные запросы телеметрии из приложения.
* Дополнительные сведения см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
