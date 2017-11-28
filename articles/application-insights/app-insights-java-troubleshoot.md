---
title: "Устранение неполадок Application Insights в веб-проекте Java"
description: "Руководство по устранению неполадок — мониторинг динамических приложений Java с помощью Application Insights."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="acb67-103">Устранение неполадок, а также вопросы и ответы по Application Insights для Java</span><span class="sxs-lookup"><span data-stu-id="acb67-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="acb67-104">Возникли вопросы или проблемы при использовании [Azure Application Insights в Java][java]?</span><span class="sxs-lookup"><span data-stu-id="acb67-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="acb67-105">Ниже приведен ряд советов.</span><span class="sxs-lookup"><span data-stu-id="acb67-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="acb67-106">Ошибки сборки</span><span class="sxs-lookup"><span data-stu-id="acb67-106">Build errors</span></span>
<span data-ttu-id="acb67-107">**При добавлении пакета SDK для Application Insights посредством Maven или Gradle в Eclipse возникают ошибки проверки сборки или контрольной суммы.**</span><span class="sxs-lookup"><span data-stu-id="acb67-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="acb67-108">Если в элементе зависимости <version> используется шаблон с подстановочными знаками (например, (Maven) `<version>[1.0,)</version>` или (Gradle) `version:'1.0.+'`), попробуйте указать конкретную версию, например `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="acb67-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="acb67-109">Сведения о последней версии см. в [заметках о выпуске](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="acb67-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="acb67-110">Нет данных</span><span class="sxs-lookup"><span data-stu-id="acb67-110">No data</span></span>
<span data-ttu-id="acb67-111">**Мне удалось успешно добавить Application Insights и запустить приложение, но данные не появились на портале.**</span><span class="sxs-lookup"><span data-stu-id="acb67-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="acb67-112">Подождите минуту и нажмите «Обновить».</span><span class="sxs-lookup"><span data-stu-id="acb67-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="acb67-113">Диаграммы автоматически обновляются через определенные интервалы, однако их можно обновлять и вручную.</span><span class="sxs-lookup"><span data-stu-id="acb67-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="acb67-114">Интервал обновления зависит от временного диапазона, выбранного для диаграммы.</span><span class="sxs-lookup"><span data-stu-id="acb67-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="acb67-115">Проверьте, есть ли у вас ключ инструментирования, указанный в файле ApplicationInsights.xml (в папке ресурсов проекта).</span><span class="sxs-lookup"><span data-stu-id="acb67-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span></span>
* <span data-ttu-id="acb67-116">Убедитесь в том, что в XML-файле нет узла `<DisableTelemetry>true</DisableTelemetry>`.</span><span class="sxs-lookup"><span data-stu-id="acb67-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="acb67-117">В вашем брандмауэре вам может потребоваться открыть TCP-порты 80 и 443 для исходящего трафика, идущего на сайт dc.services.visualstudio.com. Ознакомьтесь с [полным списком исключений брандмауэра](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="acb67-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com. See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="acb67-118">На начальном экране Microsoft Azure посмотрите на карту состояния службы.</span><span class="sxs-lookup"><span data-stu-id="acb67-118">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="acb67-119">Если есть какие-либо предупреждения, дождитесь возвращения всех модулей в состояние ОК, затем закройте и заново откройте модуль приложения Application Insights.</span><span class="sxs-lookup"><span data-stu-id="acb67-119">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="acb67-120">Включите ведение журнала в окне консоли IDE, добавив элемент `<SDKLogger />` в корневой узел в файле ApplicationInsights.xml (в папке ресурсов проекта), и проверьте наличие записей, начинающихся с [Error].</span><span class="sxs-lookup"><span data-stu-id="acb67-120">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="acb67-121">Убедитесь, что правильный файл ApplicationInsights.xml успешно загружен с помощью пакета SDK для Java. В случае успешной загрузки на консоли в разделе сообщений вывода отображается: «Файл конфигурации успешно найден».</span><span class="sxs-lookup"><span data-stu-id="acb67-121">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="acb67-122">Если файл конфигурации не найден, просмотрите сообщения вывода, чтобы узнать, где происходил поиск файла конфигурации, и убедитесь, что файл ApplicationInsights.xml находится в одном из этих расположений.</span><span class="sxs-lookup"><span data-stu-id="acb67-122">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="acb67-123">Как правило, файл конфигурации следует размещать вместе с JAR-файлами пакета SDK для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="acb67-123">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="acb67-124">Например, в Tomcat – это папка WEB-INF или lib.</span><span class="sxs-lookup"><span data-stu-id="acb67-124">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="acb67-125">Ранее видимые данные перестали отображаться</span><span class="sxs-lookup"><span data-stu-id="acb67-125">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="acb67-126">Проверьте [блог состояний](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="acb67-126">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="acb67-127">Вы достигли месячной квоты точек данных?</span><span class="sxs-lookup"><span data-stu-id="acb67-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="acb67-128">Чтобы выяснить это, см. разделы «Параметры», «Квота» и «Расценки». Если вы достигли квоты, вы можете изменить свой тарифный план или заплатить за дополнительную емкость.</span><span class="sxs-lookup"><span data-stu-id="acb67-128">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="acb67-129">См. [таблицу цен](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="acb67-129">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="acb67-130">Не отображаются все данные, которые ожидалось увидеть</span><span class="sxs-lookup"><span data-stu-id="acb67-130">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="acb67-131">Откройте колонку "Quotas and Pricing" (Квоты и цены) и проверьте, выполняется ли [выборка](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="acb67-131">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="acb67-132">(100 % передачи означает, что выборка не выполняется.) Службу Application Insights можно настроить на прием только части данных телеметрии, поступающих из приложения.</span><span class="sxs-lookup"><span data-stu-id="acb67-132">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="acb67-133">Это помогает не выходить за пределы месячной квоты.</span><span class="sxs-lookup"><span data-stu-id="acb67-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="acb67-134">Нет данных по использованию</span><span class="sxs-lookup"><span data-stu-id="acb67-134">No usage data</span></span>
<span data-ttu-id="acb67-135">**Приводятся данные по запросам и времени ответа, но нет данных по просмотру страниц, использованию браузеров и пользователям.**</span><span class="sxs-lookup"><span data-stu-id="acb67-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="acb67-136">Вы успешно настроили приложение для отправки данных телеметрии с сервера.</span><span class="sxs-lookup"><span data-stu-id="acb67-136">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="acb67-137">Теперь вам нужно [настроить веб-страницы для отправки данных телеметрии из веб-браузера][usage].</span><span class="sxs-lookup"><span data-stu-id="acb67-137">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="acb67-138">Если клиент является приложением на [телефоне или другом устройстве][platforms], из него также можно отправлять данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="acb67-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="acb67-139">Для настройки телеметрии в клиенте и на сервере используйте один и тот же ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="acb67-139">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="acb67-140">Данные будут приводиться в одном и том же ресурсе Application Insights, и вы сможете сопоставлять события, полученные от клиента и с сервера.</span><span class="sxs-lookup"><span data-stu-id="acb67-140">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="acb67-141">Отключение телеметрии</span><span class="sxs-lookup"><span data-stu-id="acb67-141">Disabling telemetry</span></span>
<span data-ttu-id="acb67-142">**Как отключить сбор данных телеметрии?**</span><span class="sxs-lookup"><span data-stu-id="acb67-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="acb67-143">В коде:</span><span class="sxs-lookup"><span data-stu-id="acb67-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="acb67-144">**Или**</span><span class="sxs-lookup"><span data-stu-id="acb67-144">**Or**</span></span> 

<span data-ttu-id="acb67-145">Измените файл ApplicationInsights.xml (в папке ресурсов проекта).</span><span class="sxs-lookup"><span data-stu-id="acb67-145">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="acb67-146">Добавьте следующий элемент в корневой узел:</span><span class="sxs-lookup"><span data-stu-id="acb67-146">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="acb67-147">При изменении значения в файле XML необходимо перезапустить приложение.</span><span class="sxs-lookup"><span data-stu-id="acb67-147">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="acb67-148">Изменение целевого ресурса</span><span class="sxs-lookup"><span data-stu-id="acb67-148">Changing the target</span></span>
<span data-ttu-id="acb67-149">**Как изменить ресурс Azure, в который проект отправляет данные?**</span><span class="sxs-lookup"><span data-stu-id="acb67-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="acb67-150">[Получите ключ инструментирования нового ресурса.][java]</span><span class="sxs-lookup"><span data-stu-id="acb67-150">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="acb67-151">Если вы добавили Application Insights в проект с помощью набора средств Azure для Eclipse, щелкните веб-проект правой кнопкой мыши, выберите **Azure**, а затем выберите **Настроить Application Insights** и измените ключ.</span><span class="sxs-lookup"><span data-stu-id="acb67-151">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="acb67-152">В противном случае измените ключ в файле ApplicationInsights.xml в папке ресурсов проекта.</span><span class="sxs-lookup"><span data-stu-id="acb67-152">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="acb67-153">Отладка данных из пакета SDK</span><span class="sxs-lookup"><span data-stu-id="acb67-153">Debug data from the SDK</span></span>

<span data-ttu-id="acb67-154">**Как определить, что делает пакет SDK?**</span><span class="sxs-lookup"><span data-stu-id="acb67-154">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="acb67-155">Чтобы получить дополнительные сведения о работе API, добавьте `<SDKLogger/>` в корневой узел файла конфигурации ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="acb67-155">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="acb67-156">Можно также указать средству ведения журнала выводить данные в файл.</span><span class="sxs-lookup"><span data-stu-id="acb67-156">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="acb67-157">Файлы можно найти в `%temp%\javasdklogs` или в `java.io.tmpdir` при использовании сервера Tomcat.</span><span class="sxs-lookup"><span data-stu-id="acb67-157">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="acb67-158">Начальный экран Azure</span><span class="sxs-lookup"><span data-stu-id="acb67-158">The Azure start screen</span></span>
<span data-ttu-id="acb67-159">**Я просматриваю [портал Azure](https://portal.azure.com). Скажет ли карта что-нибудь о приложении?**</span><span class="sxs-lookup"><span data-stu-id="acb67-159">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="acb67-160">Нет, она показывает работоспособность серверов Azure по всему миру.</span><span class="sxs-lookup"><span data-stu-id="acb67-160">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="acb67-161">*Как найти данные о приложении на начальной доске (начальном экране) Azure?*</span><span class="sxs-lookup"><span data-stu-id="acb67-161">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="acb67-162">Если вы [настроили приложение для использования Application Insights][java], нажмите кнопку "Обзор", выберите Application Insights, а затем выберите ресурс приложения, который вы создали для приложения.</span><span class="sxs-lookup"><span data-stu-id="acb67-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="acb67-163">Чтобы упростить эту операцию в будущем, можно закрепить приложение на начальном экране.</span><span class="sxs-lookup"><span data-stu-id="acb67-163">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="acb67-164">Серверы в интрасети</span><span class="sxs-lookup"><span data-stu-id="acb67-164">Intranet servers</span></span>
<span data-ttu-id="acb67-165">**Можно ли наблюдать за сервером в интрасети?**</span><span class="sxs-lookup"><span data-stu-id="acb67-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="acb67-166">Да, если ваш сервер может отправлять данные телеметрии на портал Application Insights через общедоступную сеть Интернет.</span><span class="sxs-lookup"><span data-stu-id="acb67-166">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="acb67-167">В вашем брандмауэре вам может потребоваться открыть TCP-порты 80 и 443 для исходящего трафика, идущего на сайты dc.services.visualstudio.com и f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="acb67-167">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="acb67-168">Хранение данных</span><span class="sxs-lookup"><span data-stu-id="acb67-168">Data retention</span></span>
<span data-ttu-id="acb67-169">**Как долго данные хранятся на портале? Защищен ли он?**</span><span class="sxs-lookup"><span data-stu-id="acb67-169">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="acb67-170">Ознакомьтесь с разделом [Хранение данных и конфиденциальность][data].</span><span class="sxs-lookup"><span data-stu-id="acb67-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="acb67-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="acb67-171">Next steps</span></span>
<span data-ttu-id="acb67-172">**Служба Application Insights настроена для серверного приложения Java. Что еще можно сделать?**</span><span class="sxs-lookup"><span data-stu-id="acb67-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="acb67-173">[Отслеживать доступность веб-страниц][availability]</span><span class="sxs-lookup"><span data-stu-id="acb67-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="acb67-174">[Отслеживать использование веб-страниц][usage]</span><span class="sxs-lookup"><span data-stu-id="acb67-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="acb67-175">[Отслеживать использование и диагностировать проблемы в приложениях для устройств][platforms]</span><span class="sxs-lookup"><span data-stu-id="acb67-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="acb67-176">[Написать код для отслеживания использования приложения][track]</span><span class="sxs-lookup"><span data-stu-id="acb67-176">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="acb67-177">[Записать журналы диагностики][javalogs]</span><span class="sxs-lookup"><span data-stu-id="acb67-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="acb67-178">Получение справки</span><span class="sxs-lookup"><span data-stu-id="acb67-178">Get help</span></span>
* [<span data-ttu-id="acb67-179">Переполнение стека</span><span class="sxs-lookup"><span data-stu-id="acb67-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

