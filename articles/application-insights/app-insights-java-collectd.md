---
title: "Мониторинг производительности веб-приложения Java в Linux в среде Azure | Документация Майкрософт"
description: "Расширенный мониторинг производительности приложений на веб-сайте Java с подключаемым модулем CollectD для Application Insights."
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
ms.openlocfilehash: 4ea917b068e0242bfb88d7357eca032607a43a3f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="7542a-103">collectd: метрики производительности Linux в Application Insights</span><span class="sxs-lookup"><span data-stu-id="7542a-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="7542a-104">Для работы с метриками производительности Linux в [Application Insights](app-insights-overview.md) установите инструмент [collectd](http://collectd.org/) вместе с его подключаемым модулем Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7542a-104">To explore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="7542a-105">Это решение с открытым исходным кодом собирает разнообразные данные системной и сетевой статистики.</span><span class="sxs-lookup"><span data-stu-id="7542a-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="7542a-106">Обычно collectd используется, если вы уже [инструментировали веб-службу Java с помощью Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="7542a-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="7542a-107">Это средство предоставляет больше данных, помогая вам повысить производительность приложения или диагностировать неполадки.</span><span class="sxs-lookup"><span data-stu-id="7542a-107">It gives you more data to help you to enhance your app's performance or diagnose problems.</span></span> 

![Примеры диаграмм](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="7542a-109">Получение ключа инструментирования</span><span class="sxs-lookup"><span data-stu-id="7542a-109">Get your instrumentation key</span></span>
<span data-ttu-id="7542a-110">На [портале Microsoft Azure](https://portal.azure.com) откройте ресурс [Application Insights](app-insights-overview.md), в котором требуется отобразить данные.</span><span class="sxs-lookup"><span data-stu-id="7542a-110">In the [Microsoft Azure portal](https://portal.azure.com), open the [Application Insights](app-insights-overview.md) resource where you want the data to appear.</span></span> <span data-ttu-id="7542a-111">(Либо [создайте новый ресурс](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="7542a-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="7542a-112">Скопируйте ключ инструментирования, идентифицирующий этот ресурс.</span><span class="sxs-lookup"><span data-stu-id="7542a-112">Take a copy of the instrumentation key, which identifies the resource.</span></span>

![Просмотрите все, откройте свой ресурс и затем в раскрывающемся списке основных компонентов выберите и скопируйте ключ инструментирования](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-the-plug-in"></a><span data-ttu-id="7542a-114">Установка collectd и подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="7542a-114">Install collectd and the plug-in</span></span>
<span data-ttu-id="7542a-115">На компьютерах с сервером Unix выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7542a-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="7542a-116">Установите [collectd](http://collectd.org/) 5.4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7542a-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="7542a-117">Загрузите [подключаемый модуль записи Application Insights collectd](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="7542a-117">Download the [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="7542a-118">Запишите номер версии.</span><span class="sxs-lookup"><span data-stu-id="7542a-118">Note the version number.</span></span>
3. <span data-ttu-id="7542a-119">Скопируйте подключаемый модуль JAR в `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="7542a-119">Copy the plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="7542a-120">Отредактируйте файл `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="7542a-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="7542a-121">Убедитесь, что [подключаемый модуль Java](https://collectd.org/wiki/index.php/Plugin:Java) включен.</span><span class="sxs-lookup"><span data-stu-id="7542a-121">Ensure that [the Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="7542a-122">Обновите JVMArg для java.class.path, включив в него указанный ниже файл JAR.</span><span class="sxs-lookup"><span data-stu-id="7542a-122">Update the JVMArg for the java.class.path to include the following JAR.</span></span> <span data-ttu-id="7542a-123">Номер версии должен совпадать с номером версии, которую вы загрузили:</span><span class="sxs-lookup"><span data-stu-id="7542a-123">Update the version number to match the one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="7542a-124">Добавьте следующий фрагмент кода, используя ключ инструментирования из ресурса:</span><span class="sxs-lookup"><span data-stu-id="7542a-124">Add this snippet, using the Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="7542a-125">Пример файла конфигурации (фрагмент):</span><span class="sxs-lookup"><span data-stu-id="7542a-125">Here's part of a sample configuration file:</span></span>

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

<span data-ttu-id="7542a-126">Настройте другие [подключаемые модули collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), которые могут собирать разные данные из разных источников.</span><span class="sxs-lookup"><span data-stu-id="7542a-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="7542a-127">Перезапустите collectd в соответствии с его [документацией](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="7542a-127">Restart collectd according to its [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-the-data-in-application-insights"></a><span data-ttu-id="7542a-128">Просмотр данных в Application Insights</span><span class="sxs-lookup"><span data-stu-id="7542a-128">View the data in Application Insights</span></span>
<span data-ttu-id="7542a-129">В ресурсе Application Insights откройте [обозреватель метрик и добавьте диаграммы][metrics], выбрав нужные метрики в пользовательской категории.</span><span class="sxs-lookup"><span data-stu-id="7542a-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting the metrics you want to see from the Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="7542a-130">По умолчанию метрики со всех хост-компьютеров, которые их поставляют, объединяются.</span><span class="sxs-lookup"><span data-stu-id="7542a-130">By default, the metrics are aggregated across all host machines from which the metrics were collected.</span></span> <span data-ttu-id="7542a-131">Чтобы просмотреть метрики по хостам, в колонке сведений о диаграмме включите группировку и выберите группировку по параметру CollectD-Host.</span><span class="sxs-lookup"><span data-stu-id="7542a-131">To view the metrics per host, in the Chart details blade, turn on Grouping and then choose to group by CollectD-Host.</span></span>

## <a name="to-exclude-upload-of-specific-statistics"></a><span data-ttu-id="7542a-132">Исключение загрузки определенных статистических данных</span><span class="sxs-lookup"><span data-stu-id="7542a-132">To exclude upload of specific statistics</span></span>
<span data-ttu-id="7542a-133">По умолчанию подключаемый модуль Application Insights отправляет все данные, собранные всеми подключаемыми модулями read collectd.</span><span class="sxs-lookup"><span data-stu-id="7542a-133">By default, the Application Insights plugin sends all the data collected by all the enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="7542a-134">Чтобы исключить данные из определенных подключаемых модулей или источников данных, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="7542a-134">To exclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="7542a-135">Измените файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7542a-135">Edit the configuration file.</span></span> 
* <span data-ttu-id="7542a-136">В `<Plugin ApplicationInsightsWriter>`добавьте строки директив следующего вида:</span><span class="sxs-lookup"><span data-stu-id="7542a-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="7542a-137">Директива</span><span class="sxs-lookup"><span data-stu-id="7542a-137">Directive</span></span> | <span data-ttu-id="7542a-138">Результат</span><span class="sxs-lookup"><span data-stu-id="7542a-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="7542a-139">Исключаются все данные, собранные подключаемым модулем `disk`</span><span class="sxs-lookup"><span data-stu-id="7542a-139">Exclude all data collected by the `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="7542a-140">Исключаются источники `read` и `write` из подключаемого модуля `disk`</span><span class="sxs-lookup"><span data-stu-id="7542a-140">Exclude the sources named `read` and `write` from the `disk` plugin.</span></span> |

<span data-ttu-id="7542a-141">Каждая директива должна начинаться с новой строки.</span><span class="sxs-lookup"><span data-stu-id="7542a-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="7542a-142">Проблемы?</span><span class="sxs-lookup"><span data-stu-id="7542a-142">Problems?</span></span>
<span data-ttu-id="7542a-143">*Данные не отображаются в портале*</span><span class="sxs-lookup"><span data-stu-id="7542a-143">*I don't see data in the portal*</span></span>

* <span data-ttu-id="7542a-144">Откройте [Поиск][diagnostic] и проверьте поступление необработанных событий.</span><span class="sxs-lookup"><span data-stu-id="7542a-144">Open [Search][diagnostic] to see if the raw events have arrived.</span></span> <span data-ttu-id="7542a-145">Иногда они появляются в обозревателе метрик не сразу.</span><span class="sxs-lookup"><span data-stu-id="7542a-145">Sometimes they take longer to appear in metrics explorer.</span></span>
* <span data-ttu-id="7542a-146">Вам может понадобиться [указать исключения брандмауэра для исходящих данных](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="7542a-146">You might need to [set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="7542a-147">Включите трассировку в подключаемом модуле Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7542a-147">Enable tracing in the Application Insights plugin.</span></span> <span data-ttu-id="7542a-148">Добавьте в `<Plugin ApplicationInsightsWriter>`следующую строку:</span><span class="sxs-lookup"><span data-stu-id="7542a-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="7542a-149">Откройте терминал и запустите collectd в режиме подробного протоколирования, чтобы проверить, не сообщает ли он о каких-либо неполадках:</span><span class="sxs-lookup"><span data-stu-id="7542a-149">Open a terminal and start collectd in verbose mode, to see any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="7542a-150">Известная проблема</span><span class="sxs-lookup"><span data-stu-id="7542a-150">Known issue</span></span>

<span data-ttu-id="7542a-151">Подключаемый модуль записи для Application Insights несовместим с некоторыми подключаемыми модулями чтения.</span><span class="sxs-lookup"><span data-stu-id="7542a-151">The Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="7542a-152">Некоторые подключаемые модули иногда отправляют сообщение "не число", когда подключаемый модуль Application Insights ожидает число с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="7542a-152">Some plugins sometimes send "NaN" where the Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="7542a-153">Симптом. В журнале collectd содержатся ошибки, в которых есть текст "AI: ... SyntaxError: непредвиденный токен N".</span><span class="sxs-lookup"><span data-stu-id="7542a-153">Symptom: The collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="7542a-154">Обходное решение. Исключите данные, собранные подключаемым модулем записи, с которым связана проблема.</span><span class="sxs-lookup"><span data-stu-id="7542a-154">Workaround: Exclude data collected by the problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


