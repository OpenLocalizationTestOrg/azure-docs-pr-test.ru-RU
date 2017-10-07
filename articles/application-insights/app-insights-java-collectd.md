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
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="405f3-103">collectd: метрики производительности Linux в Application Insights</span><span class="sxs-lookup"><span data-stu-id="405f3-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="405f3-104">метрики производительности системы Linux tooexplore в [Application Insights](app-insights-overview.md), установите [collectd](http://collectd.org/)вместе с его подключаемый модуль Application Insights.</span><span class="sxs-lookup"><span data-stu-id="405f3-104">tooexplore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="405f3-105">Это решение с открытым исходным кодом собирает разнообразные данные системной и сетевой статистики.</span><span class="sxs-lookup"><span data-stu-id="405f3-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="405f3-106">Обычно collectd используется, если вы уже [инструментировали веб-службу Java с помощью Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="405f3-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="405f3-107">Предоставляет дополнительные данные toohelp вы tooenhance производительность приложения или диагностировать проблемы.</span><span class="sxs-lookup"><span data-stu-id="405f3-107">It gives you more data toohelp you tooenhance your app's performance or diagnose problems.</span></span> 

![Примеры диаграмм](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="405f3-109">Получение ключа инструментирования</span><span class="sxs-lookup"><span data-stu-id="405f3-109">Get your instrumentation key</span></span>
<span data-ttu-id="405f3-110">В hello [портал Microsoft Azure](https://portal.azure.com)откройте hello [Application Insights](app-insights-overview.md) место tooappear hello данных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="405f3-110">In hello [Microsoft Azure portal](https://portal.azure.com), open hello [Application Insights](app-insights-overview.md) resource where you want hello data tooappear.</span></span> <span data-ttu-id="405f3-111">(Либо [создайте новый ресурс](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="405f3-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="405f3-112">Использование копии ключа инструментирования hello, который определяет ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="405f3-112">Take a copy of hello instrumentation key, which identifies hello resource.</span></span>

![Просмотреть все, открыть ресурс и затем в hello Essentials раскрывающегося списка, выберите и скопируйте hello ключ инструментирования](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a><span data-ttu-id="405f3-114">Установка collectd и hello подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="405f3-114">Install collectd and hello plug-in</span></span>
<span data-ttu-id="405f3-115">На компьютерах с сервером Unix выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="405f3-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="405f3-116">Установите [collectd](http://collectd.org/) 5.4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="405f3-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="405f3-117">Загрузите hello [подключаемый модуль Application Insights collectd записи](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="405f3-117">Download hello [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="405f3-118">Запишите номер версии hello.</span><span class="sxs-lookup"><span data-stu-id="405f3-118">Note hello version number.</span></span>
3. <span data-ttu-id="405f3-119">Скопируйте подключаемого модуля hello JAR в `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="405f3-119">Copy hello plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="405f3-120">Отредактируйте файл `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="405f3-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="405f3-121">Убедитесь, что [hello подключаемый модуль Java](https://collectd.org/wiki/index.php/Plugin:Java) включен.</span><span class="sxs-lookup"><span data-stu-id="405f3-121">Ensure that [hello Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="405f3-122">Обновите hello JVMArg для hello java.class.path tooinclude hello следующие JAR-ФАЙЛ.</span><span class="sxs-lookup"><span data-stu-id="405f3-122">Update hello JVMArg for hello java.class.path tooinclude hello following JAR.</span></span> <span data-ttu-id="405f3-123">Обновление hello версии номеров toomatch hello загруженный один:</span><span class="sxs-lookup"><span data-stu-id="405f3-123">Update hello version number toomatch hello one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="405f3-124">Добавьте этот фрагмент, с помощью hello ключ инструментирования из ресурса:</span><span class="sxs-lookup"><span data-stu-id="405f3-124">Add this snippet, using hello Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="405f3-125">Пример файла конфигурации (фрагмент):</span><span class="sxs-lookup"><span data-stu-id="405f3-125">Here's part of a sample configuration file:</span></span>

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

<span data-ttu-id="405f3-126">Настройте другие [подключаемые модули collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), которые могут собирать разные данные из разных источников.</span><span class="sxs-lookup"><span data-stu-id="405f3-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="405f3-127">Перезапустите tooits в соответствии с collectd [вручную](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="405f3-127">Restart collectd according tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-hello-data-in-application-insights"></a><span data-ttu-id="405f3-128">Просмотр данных hello в Application Insights</span><span class="sxs-lookup"><span data-stu-id="405f3-128">View hello data in Application Insights</span></span>
<span data-ttu-id="405f3-129">В ресурс Application Insights, откройте [обозревателя метрик и добавьте диаграммы][metrics], выбрав hello метрик требуется toosee из hello пользовательскую категорию.</span><span class="sxs-lookup"><span data-stu-id="405f3-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting hello metrics you want toosee from hello Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="405f3-130">По умолчанию на всех компьютерах узлов, с которых были собраны показатели hello объединяются метрики hello.</span><span class="sxs-lookup"><span data-stu-id="405f3-130">By default, hello metrics are aggregated across all host machines from which hello metrics were collected.</span></span> <span data-ttu-id="405f3-131">tooview hello показатели для каждого узла в колонке сведения о диаграмме hello, включите группирования, а затем выберите toogroup CollectD узлом.</span><span class="sxs-lookup"><span data-stu-id="405f3-131">tooview hello metrics per host, in hello Chart details blade, turn on Grouping and then choose toogroup by CollectD-Host.</span></span>

## <a name="tooexclude-upload-of-specific-statistics"></a><span data-ttu-id="405f3-132">Отправка tooexclude заданной статистики</span><span class="sxs-lookup"><span data-stu-id="405f3-132">tooexclude upload of specific statistics</span></span>
<span data-ttu-id="405f3-133">По умолчанию подключаемый модуль Application Insights hello отправляет все hello данными, собранными все collectd hello включена «read» подключаемые модули.</span><span class="sxs-lookup"><span data-stu-id="405f3-133">By default, hello Application Insights plugin sends all hello data collected by all hello enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="405f3-134">tooexclude данные из определенных источников данных или подключаемые модули:</span><span class="sxs-lookup"><span data-stu-id="405f3-134">tooexclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="405f3-135">Измените файл конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="405f3-135">Edit hello configuration file.</span></span> 
* <span data-ttu-id="405f3-136">В `<Plugin ApplicationInsightsWriter>`добавьте строки директив следующего вида:</span><span class="sxs-lookup"><span data-stu-id="405f3-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="405f3-137">Директива</span><span class="sxs-lookup"><span data-stu-id="405f3-137">Directive</span></span> | <span data-ttu-id="405f3-138">Результат</span><span class="sxs-lookup"><span data-stu-id="405f3-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="405f3-139">Исключить все данные, собранные hello `disk` подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="405f3-139">Exclude all data collected by hello `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="405f3-140">Исключить источники hello с именем `read` и `write` из hello `disk` подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="405f3-140">Exclude hello sources named `read` and `write` from hello `disk` plugin.</span></span> |

<span data-ttu-id="405f3-141">Каждая директива должна начинаться с новой строки.</span><span class="sxs-lookup"><span data-stu-id="405f3-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="405f3-142">Проблемы?</span><span class="sxs-lookup"><span data-stu-id="405f3-142">Problems?</span></span>
<span data-ttu-id="405f3-143">*Я не вижу данных в портале hello*</span><span class="sxs-lookup"><span data-stu-id="405f3-143">*I don't see data in hello portal*</span></span>

* <span data-ttu-id="405f3-144">Откройте [поиска] [ diagnostic] toosee при доставке hello необработанных событий.</span><span class="sxs-lookup"><span data-stu-id="405f3-144">Open [Search][diagnostic] toosee if hello raw events have arrived.</span></span> <span data-ttu-id="405f3-145">Иногда они принимают tooappear больше времени, в обозревателе метрик.</span><span class="sxs-lookup"><span data-stu-id="405f3-145">Sometimes they take longer tooappear in metrics explorer.</span></span>
* <span data-ttu-id="405f3-146">Может потребоваться слишком[задать исключения брандмауэра для выходных данных](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="405f3-146">You might need too[set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="405f3-147">Включите трассировку в подключаемый модуль Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="405f3-147">Enable tracing in hello Application Insights plugin.</span></span> <span data-ttu-id="405f3-148">Добавьте в `<Plugin ApplicationInsightsWriter>`следующую строку:</span><span class="sxs-lookup"><span data-stu-id="405f3-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="405f3-149">Откройте терминал и запустите collectd в подробном режиме toosee отчеты отправляются проблем.</span><span class="sxs-lookup"><span data-stu-id="405f3-149">Open a terminal and start collectd in verbose mode, toosee any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="405f3-150">Известная проблема</span><span class="sxs-lookup"><span data-stu-id="405f3-150">Known issue</span></span>

<span data-ttu-id="405f3-151">Подключаемый модуль записи аналитики приложения Hello несовместим с определенным подключаемых модулей чтения.</span><span class="sxs-lookup"><span data-stu-id="405f3-151">hello Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="405f3-152">Некоторые подключаемые модули иногда отправить «NaN», где подключаемый модуль Application Insights hello ожидает число с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="405f3-152">Some plugins sometimes send "NaN" where hello Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="405f3-153">Симптом: hello collectd журнала видно, что ошибки, включающие «AI:... SyntaxError: непредвиденный токен N".</span><span class="sxs-lookup"><span data-stu-id="405f3-153">Symptom: hello collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="405f3-154">Обходной путь: Исключить данные, собираемые подключаемые модули записи проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="405f3-154">Workaround: Exclude data collected by hello problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


