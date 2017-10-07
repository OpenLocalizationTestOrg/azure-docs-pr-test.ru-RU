---
title: "aaaMonitor производительности веб-приложения Java в Linux - Azure | Документы Microsoft"
description: "Расширенные наблюдение за производительностью приложений Java веб-сайта с hello CollectD подключаемый модуль Application Insights."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a>collectd: метрики производительности Linux в Application Insights


метрики производительности системы Linux tooexplore в [Application Insights](app-insights-overview.md), установите [collectd](http://collectd.org/)вместе с его подключаемый модуль Application Insights. Это решение с открытым исходным кодом собирает разнообразные данные системной и сетевой статистики.

Обычно collectd используется, если вы уже [инструментировали веб-службу Java с помощью Application Insights][java]. Предоставляет дополнительные данные toohelp вы tooenhance производительность приложения или диагностировать проблемы. 

![Примеры диаграмм](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a>Получение ключа инструментирования
В hello [портал Microsoft Azure](https://portal.azure.com)откройте hello [Application Insights](app-insights-overview.md) место tooappear hello данных ресурсов. (Либо [создайте новый ресурс](app-insights-create-new-resource.md).)

Использование копии ключа инструментирования hello, который определяет ресурс hello.

![Просмотреть все, открыть ресурс и затем в hello Essentials раскрывающегося списка, выберите и скопируйте hello ключ инструментирования](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a>Установка collectd и hello подключаемого модуля
На компьютерах с сервером Unix выполните следующие действия.

1. Установите [collectd](http://collectd.org/) 5.4.0 или более поздней версии.
2. Загрузите hello [подключаемый модуль Application Insights collectd записи](https://aka.ms/aijavasdk). Запишите номер версии hello.
3. Скопируйте подключаемого модуля hello JAR в `/usr/share/collectd/java`.
4. Отредактируйте файл `/etc/collectd/collectd.conf`:
   * Убедитесь, что [hello подключаемый модуль Java](https://collectd.org/wiki/index.php/Plugin:Java) включен.
   * Обновите hello JVMArg для hello java.class.path tooinclude hello следующие JAR-ФАЙЛ. Обновление hello версии номеров toomatch hello загруженный один:
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * Добавьте этот фрагмент, с помощью hello ключ инструментирования из ресурса:

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

Пример файла конфигурации (фрагмент):

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

Настройте другие [подключаемые модули collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), которые могут собирать разные данные из разных источников.

Перезапустите tooits в соответствии с collectd [вручную](https://collectd.org/wiki/index.php/First_steps).

## <a name="view-hello-data-in-application-insights"></a>Просмотр данных hello в Application Insights
В ресурс Application Insights, откройте [обозревателя метрик и добавьте диаграммы][metrics], выбрав hello метрик требуется toosee из hello пользовательскую категорию.

![](./media/app-insights-java-collectd/result.png)

По умолчанию на всех компьютерах узлов, с которых были собраны показатели hello объединяются метрики hello. tooview hello показатели для каждого узла в колонке сведения о диаграмме hello, включите группирования, а затем выберите toogroup CollectD узлом.

## <a name="tooexclude-upload-of-specific-statistics"></a>Отправка tooexclude заданной статистики
По умолчанию подключаемый модуль Application Insights hello отправляет все hello данными, собранными все collectd hello включена «read» подключаемые модули. 

tooexclude данные из определенных источников данных или подключаемые модули:

* Измените файл конфигурации hello. 
* В `<Plugin ApplicationInsightsWriter>`добавьте строки директив следующего вида:

| Директива | Результат |
| --- | --- |
| `Exclude disk` |Исключить все данные, собранные hello `disk` подключаемого модуля |
| `Exclude disk:read,write` |Исключить источники hello с именем `read` и `write` из hello `disk` подключаемого модуля. |

Каждая директива должна начинаться с новой строки.

## <a name="problems"></a>Проблемы?
*Я не вижу данных в портале hello*

* Откройте [поиска] [ diagnostic] toosee при доставке hello необработанных событий. Иногда они принимают tooappear больше времени, в обозревателе метрик.
* Может потребоваться слишком[задать исключения брандмауэра для выходных данных](app-insights-ip-addresses.md)
* Включите трассировку в подключаемый модуль Application Insights hello. Добавьте в `<Plugin ApplicationInsightsWriter>`следующую строку:
  * `SDKLogger true`
* Откройте терминал и запустите collectd в подробном режиме toosee отчеты отправляются проблем.
  * `sudo collectd -f`

## <a name="known-issue"></a>Известная проблема

Подключаемый модуль записи аналитики приложения Hello несовместим с определенным подключаемых модулей чтения. Некоторые подключаемые модули иногда отправить «NaN», где подключаемый модуль Application Insights hello ожидает число с плавающей запятой.

Симптом: hello collectd журнала видно, что ошибки, включающие «AI:... SyntaxError: непредвиденный токен N".

Обходной путь: Исключить данные, собираемые подключаемые модули записи проблемы hello. 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


