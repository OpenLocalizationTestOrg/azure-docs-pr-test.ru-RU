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
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>Отслеживание зависимостей, исключений и времени выполнения в веб-приложениях Java


Если у вас есть [инструментированы веб-приложения Java с помощью Application Insights][java], можно использовать hello агента Java tooget более глубокого понимания, без необходимости изменения кода:

* **Зависимости:** данные о вызовы, сделанные tooother компонентов, включая приложения:
  * **вызовы REST** через HttpClient, OkHttp и RestTemplate (Spring);
  * **Redis** вызовов, выполненных с помощью клиента Jedis hello. Если вызов hello занимает больше времени, чем десятках, hello агент также извлечет hello аргументы вызова.
  * **[Вызовы JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** — MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB или Apache Derby DB. Поддерживаются вызовы "executeBatch". MySQL и PostgreSQL Если вызов hello занимает больше времени, чем десятках, hello агента сообщает hello плана запроса.
* **Перехваченные исключения:** данные об исключениях, обработанных вашим кодом.
* **Время выполнения метода:** данные о hello время принимает tooexecute определенных методов.

агент Java toouse hello, его установить на сервере. Веб-приложения должны быть встроены hello [пакет SDK для Java Application Insights][java]. 

## <a name="install-hello-application-insights-agent-for-java"></a>Установка агента hello Application Insights для Java
1. На компьютере hello на котором запущен сервер Java [загрузить агент hello](https://aka.ms/aijavasdk).
2. Измените сценарий запуска сервера приложения hello и добавьте hello, следуя виртуальной машины Java:
   
    `javaagent:`*Полный путь агента toohello JAR-файл*
   
    Например, в Tomcat на компьютере Linux:
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. Перезапустите сервер приложений.

## <a name="configure-hello-agent"></a>Настройка агента hello
Создайте файл с именем `AI-Agent.xml` и поместить его в hello же папке, что агент hello JAR-файл.

Задайте содержимое hello hello XML-файла. Измените следующие tooinclude пример hello или удалите компоненты hello.

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

У вас есть tooenable отчеты исключение и метод расписание для отдельных методов.

По умолчанию `reportExecutionTime` имеет значение true, а `reportCaughtExceptions` — значение false.

## <a name="view-hello-data"></a>Просмотр данных hello
В hello ресурс Application Insights, отображается агрегированных удаленного времени выполнения зависимостей и метод [под hello производительности плитку][metrics].

Откройте toosearch для отдельных экземпляров зависимостей, исключение и метод отчеты, [поиска][diagnostic].

[Дополнительные сведения о диагностировании проблем зависимостей](app-insights-asp-net-dependencies.md#diagnosis).

## <a name="questions-problems"></a>Вопросы? Проблемы?
* Данные отсутствуют? [Настройте исключения брандмауэра](app-insights-ip-addresses.md)
* [Устранение неполадок Java](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
