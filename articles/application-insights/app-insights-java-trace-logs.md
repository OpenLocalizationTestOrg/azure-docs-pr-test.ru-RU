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
# <a name="explore-java-trace-logs-in-application-insights"></a>Просмотр журналов трассировки Java в Application Insights
Если вы используете Logback или Log4J (версия 1.2 или 2.0) для трассировки, что журналы трассировки отправляются автоматически tooApplication аналитики, где вы можете анализировать и поиск на них.

## <a name="install-hello-java-sdk"></a>Установка пакета SDK для Java hello

Установите пакет [SDK Application Insights для Java][java], если это еще не сделано.

(Если вы не хотите tootrack HTTP-запросов, можно опустить большинство hello XML-файл конфигурации, но необходимо включить по крайней мере hello `InstrumentationKey` элемента. Вам также следует вызвать `new TelemetryClient()` tooinitialize hello SDK.)


## <a name="add-logging-libraries-tooyour-project"></a>Добавление проекта tooyour библиотеки ведения журнала
*Выберите подходящий способ hello для проекта.*

#### <a name="if-youre-using-maven"></a>Если вы используете Maven...
Если проект уже настроен toouse Maven для сборки, слияние одного следующие фрагменты кода в файл pom.xml hello.

Зависимости проекта hello, hello tooget двоичных файлов, загруженных обновите.

*Logback*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J версии 2.0*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J версии 1.2*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a>Если вы используете Gradle...
Если проект уже настроен toouse Gradle для сборки, добавьте один из следующих строк toohello hello `dependencies` в файл build.gradle:

Зависимости проекта hello, hello tooget двоичных файлов, загруженных обновите.

**Logback**

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

**Log4J версии 2.0**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

**Log4J версии 1.2**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a>В противном случае...
Загрузите и извлеките соответствующие аппендера hello, а затем добавьте hello соответствующую библиотеку tooyour проекта:

| Средство ведения журнала | Загрузить | Библиотека |
| --- | --- | --- |
| Logback |[Пакет SDK с аппендером Logback](https://aka.ms/xt62a4) |applicationinsights-logging-logback |
| Log4J версии 2.0 |[Пакет SDK с аппендером Log4J версии 2.0](https://aka.ms/qypznq) |applicationinsights-logging-log4j2 |
| Log4J версии 1.2 |[Пакет SDK с аппендером Log4J версии 1.2](https://aka.ms/ky9cbo) |applicationinsights-logging-log4j1_2 |

## <a name="add-hello-appender-tooyour-logging-framework"></a>Добавление ведения журнала tooyour аппендера платформы hello
toostart начало трассировки, слияния hello соответствующего фрагмента кода toohello Log4J или Logback файла конфигурации: 

*Logback*

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

*Log4J версии 2.0*

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

*Log4J версии 1.2*

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

Hello добавители Application Insights можно ссылаться по любой настроенное средство ведения журнала, а не обязательно по hello корневой средство ведения журнала (как показано в примерах кода hello выше).

## <a name="explore-your-traces-in-hello-application-insights-portal"></a>Изучать данные трассировок на портале Application Insights hello
Теперь, когда вы настроили ваш проект toosend отслеживает tooApplication аналитики, можно просматривать и искать эти данные трассировки в hello портале Application Insights hello [поиска] [ diagnostic] колонку.

![На портале Application Insights hello откройте раздел поиска](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a>Дальнейшие действия
[Поиск по журналу диагностики][diagnostic]

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


