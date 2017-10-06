---
title: "aaaApplication Insights для Java веб-приложений, которые уже находятся в режиме реального времени"
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
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a>Application Insights для уже действующих веб-приложений Java


Если у вас есть веб-приложения, которая запущена на сервере J2EE, можно приступать к мониторингу его с [Application Insights](app-insights-overview.md) без hello toomake изменениями кода или повторную компиляцию проекта. Этот параметр получение сведений о запросы HTTP, отправленные tooyour сервера, необработанные исключения и счетчики производительности.

Вам потребуется подписка слишком[Microsoft Azure](https://azure.com).

> [!NOTE]
> процедура Hello на этой странице добавляет hello SDK tooyour веб-приложения во время выполнения. Этот инструментарий среды выполнения полезно в том случае, если вы не желаете tooupdate или перестроить исходный код. Но если это возможно, мы рекомендуем вам [Добавление hello SDK toohello исходного кода](app-insights-java-get-started.md) вместо него. Который предоставляет дополнительные параметры, такие как записи действий пользователей tootrack кода.
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Получение ключа инструментирования Application Insights
1. Войдите в toohello [портал Microsoft Azure](https://portal.azure.com)
2. Создайте новый ресурс Application Insights и задайте hello приложения типа tooJava веб-приложения.
   
    ![Введите имя, выберите веб-приложение Java и нажмите кнопку "Создать"](./media/app-insights-java-live/02-create.png)

    Hello ресурс создается через несколько секунд.

4. Откройте новый ресурс hello и получите свой ключ инструментирования. Вам потребуется toopaste этот ключ в проект кода чуть ниже.
   
    ![Обзор нового ресурса hello нажмите кнопку Свойства и скопируйте hello ключ инструментирования](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a>2. Загрузите пакет SDK для hello
1. Загрузите hello [пакет SDK Application Insights для Java](https://aka.ms/aijavasdk). 
2. На сервере Извлеките hello содержимое SDK toohello каталог, из которого загружаются двоичных файлов проекта. В случае с Tomcat обычно это каталог `webapps/<your_app_name>/WEB-INF/lib`.

Обратите внимание, что toorepeat это на каждом экземпляре сервера и для каждого приложения.

## <a name="3-add-an-application-insights-xml-file"></a>3. Добавление XML-файла Application Insights
Создание ApplicationInsights.xml в папке hello, в которую добавляется hello SDK. В ней хранятся hello следующий XML.

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
* Корреляция событий является компонентом запроса HTTP toohello сложения. Он назначает tooeach идентификатор запроса, полученных сервером hello и добавляет этот идентификатор как элемент свойства tooevery телеметрии как свойство hello «Operation.Id». Позволяет toocorrelate hello телеметрии, связанные с каждым запросом, можно установить фильтр в [диагностики поиска](app-insights-diagnostic-search.md).

## <a name="4-add-an-http-filter"></a>4. Добавление фильтра HTTP
Найдите и откройте файл web.xml hello в проекте, а следующий фрагмент кода hello узел веб-приложения и где настраиваются фильтры приложения hello слияния.

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

## <a name="5-check-firewall-exceptions"></a>5. Проверка исключений брандмауэра
Может потребоваться слишком[задавать исключения выходных данных toosend](app-insights-ip-addresses.md).

## <a name="6-restart-your-web-app"></a>6. Перезапуск веб-приложения
## <a name="7-view-your-telemetry-in-application-insights"></a>7. Просмотр данных телеметрии в Application Insights
Вернуть ресурс Application Insights tooyour в [портал Microsoft Azure](https://portal.azure.com).

Данные телеметрии об HTTP-запросов отображается на колонки Обзор hello. (Если данные отсутствуют, подождите несколько секунд и нажмите кнопку обновления).

![пример данных](./media/app-insights-java-live/5-results.png)

Нажмите кнопку через любой toosee диаграммы более подробные показатели. 

![](./media/app-insights-java-live/6-barchart.png)

И при просмотре свойств hello запроса, можно просмотреть события телеметрии hello, связанные с ним, такие как запросы и исключения.

![](./media/app-insights-java-live/7-instance.png)

[Дополнительные сведения о метриках.](app-insights-metrics-explorer.md)

## <a name="next-steps"></a>Дальнейшие действия
* [Добавить веб-страницы телеметрии tooyour](app-insights-javascript.md) toomonitor страницы представлений и метрики пользователь.
* [Настройка веб-тестов](app-insights-monitor-web-app-availability.md) toomake убедиться, что приложение остается динамической и отвечать на запросы.
* [Журнал трассировки](app-insights-java-trace-logs.md)
* [Поиск событий и журналов](app-insights-diagnostic-search.md) toohelp диагностики проблем.

