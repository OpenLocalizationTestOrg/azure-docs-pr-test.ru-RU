---
title: "aaaGet работы с Application Insights Azure с Java в Eclipse | Документы Microsoft"
description: "Используйте hello производительности tooadd подключаемый модуль Eclipse и использование отслеживание tooyour веб-сайте Java с помощью Application Insights"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a>Приступая к работе с Application Insights на Java в Eclipse
Hello пакет SDK Application Insights отправляет телеметрии из веб-приложения Java, так что можно анализировать использование и производительность. Hello Eclipse подключаемый модуль Application Insights автоматически устанавливает hello SDK в проекте, чтобы получить из hello поле телеметрии, а также API, которые можно использовать пользовательские телеметрии toowrite.   

## <a name="prerequisites"></a>Предварительные требования
В настоящее время hello работает подключаемый модуль для проектов Maven и динамические веб-проектов в Eclipse.
([Добавить Application Insights tooother типов проекта Java][java].)

Что вам понадобится:

* Oracle JRE 1.6 или более поздней версии;
* Подписка слишком[Microsoft Azure](https://azure.microsoft.com/).
* [интегрированная среда разработки Eclipse для разработчиков Java EE](http://www.eclipse.org/downloads/), версия Indigo или более поздняя;
* Windows 7 или более поздней версии либо Windows Server 2008 или более поздней версии.

## <a name="install-hello-sdk-on-eclipse-one-time"></a>Установка hello пакета SDK для Eclipse (один раз)
Имеется только toodo этот один раз на каждый компьютер. Это действие устанавливает набор средств, который затем можно добавить пакет SDK для hello tooeach динамический веб-проект.

1. В Eclipse щелкните "Help" (Справка), "Install New Software" (Установка нового программного обеспечения).

    ![Help, Install New Software](./media/app-insights-java-eclipse/0-plugin.png)
2. пакет SDK для Hello находится в http://dl.microsoft.com/eclipse в набор средств Azure.
3. Снимите флажок **Contact all update sites...**

    ![Для установки пакета SDK Application Insights снимите флажок "Contact all update sites..."](./media/app-insights-java-eclipse/1-plugin.png)

Выполните оставшиеся шаги для каждого проекта Java hello.

## <a name="create-an-application-insights-resource-in-azure"></a>Создание ресурса Application Insights в Azure
1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Создайте новый ресурс Application Insights. Задать hello приложения типа tooJava веб-приложения.  

    ![Нажмите кнопку "+" и выберите пункт "Application Insights"](./media/app-insights-java-eclipse/01-create.png)  

4. Найти ключ инструментирования hello hello нового ресурса. Вам потребуется toopaste это в проекте кода чуть ниже.  

    ![Обзор нового ресурса hello нажмите кнопку Свойства и скопируйте hello ключ инструментирования](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a>Добавление проекта tooyour Application Insights
1. Добавьте Application Insights hello контекстном меню веб-проекта Java.

    ![Обзор нового ресурса hello нажмите кнопку Свойства и скопируйте hello ключ инструментирования](./media/app-insights-java-eclipse/02-context-menu.png)
2. Вставьте ключ инструментирования hello, полученного от hello портал Azure.

    ![Обзор нового ресурса hello нажмите кнопку Свойства и скопируйте hello ключ инструментирования](./media/app-insights-java-eclipse/03-ikey.png)

ключ Hello отправляется вместе с каждого элемента телеметрии и сообщает toodisplay Application Insights в ресурс.

## <a name="run-hello-application-and-see-metrics"></a>Запустите приложение hello и просматривать показатели
Запустите приложение.

Вернуть ресурс Application Insights tooyour в Microsoft Azure.

HTTP-запросы данных появится в колонке Обзор hello. (Если данные отсутствуют, подождите несколько секунд и нажмите кнопку обновления).

![Ответ сервера, счетчики запросов и сбои ](./media/app-insights-java-eclipse/5-results.png)

Нажмите кнопку через любой toosee диаграммы более подробные показатели.

![Счетчики запросов по имени](./media/app-insights-java-eclipse/6-barchart.png)

[Дополнительные сведения о метриках.][metrics]

И при просмотре свойств hello запроса, можно просмотреть события телеметрии hello, связанные с ним, такие как запросы и исключения.

![Все трассировки для данного запроса](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a>Телеметрия на стороне клиента
Из колонки hello краткое руководство нажмите кнопку Get toomonitor код веб-страницы:

![В колонке обзор вашего приложения выберите Быстрый запуск, получить код toomonitor веб-страницы. Скопируйте сценарий hello.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

Вставьте фрагмент кода hello в голове hello файлов HTML.

#### <a name="view-client-side-data"></a>Просмотр данных на стороне клиента
Откройте обновленные веб-страницы и выполните с ними какое-либо действие. Подождите одну-две минуты, а затем вернуть tooApplication аналитики и откройте hello использования колонки. (Из колонки Обзор hello, прокрутите вниз и выберите использование).

Страница представления, пользователей и сеансов метрики будет отображаться на колонки hello использования:

![Сеансы, пользователи и просмотры страниц](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

[Дополнительные сведения о настройке телеметрии на стороне клиента][usage]

## <a name="publish-your-application"></a>Публикация приложения
Теперь публикации сервера toohello приложения, позволяют использовать его и посмотреть телеметрии hello отображаются на портале hello.

* Убедитесь, что брандмауэр разрешает вашего приложения toosend телеметрии toothese порты:

  * dc.services.visualstudio.com:443
  * dc.services.visualstudio.com:80
  * f5.services.visualstudio.com:443
  * f5.services.visualstudio.com:80
* На серверах Windows необходимо установить следующее:

  * [распространяемые компоненты Microsoft Visual C++.](http://www.microsoft.com/download/details.aspx?id=40784)

    (Сюда входят счетчики производительности).

## <a name="exceptions-and-request-failures"></a>Исключения и ошибки запросов
Необработанные исключения автоматически фиксируются:

![](./media/app-insights-java-eclipse/21-exceptions.png)

toocollect данные на другие исключения, у вас есть два варианта:

* [Вставить tooTrackException вызовы в коде](app-insights-api-custom-events-metrics.md#trackexception).
* [Установка агента Java hello на сервер](app-insights-java-agent.md). Можно указать hello методы, которые нужно toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Мониторинг вызовов методов и внешних зависимостей.
[Установка агента Java hello](app-insights-java-agent.md) toolog указан внутренние методы и вызовы через JDBC, с данными о времени.

## <a name="performance-counters"></a>Счетчики производительности
В колонке Обзор прокрутите список вниз и щелкните hello **серверы** плитки. Вы увидите несколько счетчиков производительности.

![Прокрутите вниз tooclick hello серверы плитки](./media/app-insights-java-eclipse/11-perf-counters.png)

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

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Счетчики производительности Unix
* [Установить подключаемый модуль Application Insights hello collectd](app-insights-java-collectd.md) tooget разнообразных данных системы и сети.

## <a name="availability-web-tests"></a>Доступность веб-тестов
Application Insights можно проверить веб-сайта на toocheck регулярные интервалы, он работает и отвечает хорошо. [tooset копирование][availability], прокрутите вниз tooclick доступности.

![Прокрутите вниз, щелкните "Доступность", затем "Добавить веб-тест"](./media/app-insights-java-eclipse/31-config-web-test.png)

Если ваш сайт выйдет из строя, вы получите диаграмму значений времени ответа, а также уведомление по электронной почте.

![Пример веб-теста](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

[Дополнительные сведения о веб-тестах для определения доступности.][availability]

## <a name="diagnostic-logs"></a>Журналы диагностики
Если вы используете Logback или Log4J (версия 1.2 или 2.0) для трассировки, что журналы трассировки отправляются автоматически tooApplication аналитики, где вы можете анализировать и поиск на них.

[Дополнительные сведения о журналах диагностики][javalogs]

## <a name="custom-telemetry"></a>Пользовательская телеметрия
Вставить несколько строк кода в ваш web для Java приложения toofind out действиями пользователей с ним или toohelp диагностики проблем.

Код можно вставить в веб-страницы JavaScript и на стороне сервера Java hello.

[Дополнительные сведения о пользовательской телеметрии][track]

## <a name="next-steps"></a>Дальнейшие действия
#### <a name="detect-and-diagnose-issues"></a>Обнаружение и диагностика неполадок
* [Добавить клиента телеметрии веб] [ usage] tooget телеметрии производительности с hello веб-клиента.
* [Настройка веб-тестов] [ availability] toomake убедиться, что приложение остается динамической и отвечать на запросы.
* [Поиск событий и журналов] [ diagnostic] toohelp диагностики проблем.
* [Используйте функции ведения журналов Log4J или Logback][javalogs].

#### <a name="track-usage"></a>Отслеживание использования
* [Добавить клиента телеметрии веб] [ usage] toomonitor страницы представлений и метрики, обычный пользователь.
* [Отслеживать пользовательские события и метрики](app-insights-web-track-usage.md) toolearn об использовании приложения, как на приветствия клиента и сервера hello.

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
