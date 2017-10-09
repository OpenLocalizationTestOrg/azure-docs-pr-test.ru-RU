---
title: "aaaTroubleshoot Application Insights в веб-проекте Java"
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
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="a90af-103">Устранение неполадок, а также вопросы и ответы по Application Insights для Java</span><span class="sxs-lookup"><span data-stu-id="a90af-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="a90af-104">Возникли вопросы или проблемы при использовании [Azure Application Insights в Java][java]?</span><span class="sxs-lookup"><span data-stu-id="a90af-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="a90af-105">Ниже приведен ряд советов.</span><span class="sxs-lookup"><span data-stu-id="a90af-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="a90af-106">Ошибки сборки</span><span class="sxs-lookup"><span data-stu-id="a90af-106">Build errors</span></span>
<span data-ttu-id="a90af-107">**В Eclipse при добавлении hello пакет SDK Application Insights через Maven или Gradle, получить ошибки проверки построения или контрольной суммы.**</span><span class="sxs-lookup"><span data-stu-id="a90af-107">**In Eclipse, when adding hello Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="a90af-108">Если hello зависимостей <version> элемент использует шаблон с подстановочными знаками (например (Maven) `<version>[1.0,)</version>` или (Gradle) `version:'1.0.+'`), попробуйте вместо этого указать конкретную версию как `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="a90af-108">If hello dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="a90af-109">В разделе hello [заметки о выпуске](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) для hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="a90af-109">See hello [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for hello latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="a90af-110">Нет данных</span><span class="sxs-lookup"><span data-stu-id="a90af-110">No data</span></span>
<span data-ttu-id="a90af-111">**Успешно добавлен Application Insights и запуска приложения, но никогда не видели данные на портале hello.**</span><span class="sxs-lookup"><span data-stu-id="a90af-111">**I added Application Insights successfully and ran my app, but I've never seen data in hello portal.**</span></span>

* <span data-ttu-id="a90af-112">Подождите минуту и нажмите «Обновить».</span><span class="sxs-lookup"><span data-stu-id="a90af-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="a90af-113">сами периодически обновлять Hello диаграммы, но вы также можете обновить вручную.</span><span class="sxs-lookup"><span data-stu-id="a90af-113">hello charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="a90af-114">Интервал обновления Hello зависит от диапазон времени hello hello диаграммы.</span><span class="sxs-lookup"><span data-stu-id="a90af-114">hello refresh interval depends on hello time range of hello chart.</span></span>
* <span data-ttu-id="a90af-115">Убедитесь, что ключ инструментирования, определенные в файле ApplicationInsights.xml hello (в hello ресурсов в папке проекта)</span><span class="sxs-lookup"><span data-stu-id="a90af-115">Check that you have an instrumentation key defined in hello ApplicationInsights.xml file (in hello resources folder in your project)</span></span>
* <span data-ttu-id="a90af-116">Убедитесь, что не `<DisableTelemetry>true</DisableTelemetry>` узла в XML-файле hello.</span><span class="sxs-lookup"><span data-stu-id="a90af-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in hello xml file.</span></span>
* <span data-ttu-id="a90af-117">В брандмауэре может потребоваться tooopen TCP-порты 80 и 443 для исходящего трафика toodc.services.visualstudio.com. В разделе hello [полный список исключений брандмауэра](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="a90af-117">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com. See hello [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="a90af-118">В Microsoft Azure hello запустите доски, посмотрите на hello сопоставления состояния службы.</span><span class="sxs-lookup"><span data-stu-id="a90af-118">In hello Microsoft Azure start board, look at hello service status map.</span></span> <span data-ttu-id="a90af-119">Если некоторые предупреждения указывают, подождите, пока они возвратили tooOK и затем закройте и снова откройте колонку приложения в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a90af-119">If there are some alert indications, wait until they have returned tooOK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="a90af-120">Включите ведение журналов окно консоли toohello интегрированной среды разработки, добавив `<SDKLogger />` элемент в корневом узле hello в файл ApplicationInsights.xml hello (в папке ресурсов hello в проекте) и проверить наличие записей, предваряемые фразой [ошибка].</span><span class="sxs-lookup"><span data-stu-id="a90af-120">Turn on logging toohello IDE console window, by adding an `<SDKLogger />` element under hello root node in hello ApplicationInsights.xml file (in hello resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="a90af-121">Убедитесь, что правильных ApplicationInsights.xml файл успешно загрузил hello пакет SDK для Java, просмотрев сообщения hello консоли вывода для инструкции «файл конфигурации был успешно найден» hello.</span><span class="sxs-lookup"><span data-stu-id="a90af-121">Make sure that hello correct ApplicationInsights.xml file has been successfully loaded by hello Java SDK, by looking at hello console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="a90af-122">Если не найден файл конфигурации hello, проверьте toosee сообщений hello выходных данных, где искать файл конфигурации hello для и убедитесь в том, что hello ApplicationInsights.xml находится в одном из этих расположений для поиска.</span><span class="sxs-lookup"><span data-stu-id="a90af-122">If hello config file is not found, check hello output messages toosee where hello config file is being searched for, and make sure that hello ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="a90af-123">Как правило можно поместить файл конфигурации hello рядом hello приложения аналитики SDK JAR-файлов.</span><span class="sxs-lookup"><span data-stu-id="a90af-123">As a rule of thumb, you can place hello config file near hello Application Insights SDK JARs.</span></span> <span data-ttu-id="a90af-124">Например: в Tomcat, это будет означать hello папки веб-INF/lib.</span><span class="sxs-lookup"><span data-stu-id="a90af-124">For example: in Tomcat, this would mean hello WEB-INF/lib folder.</span></span>

#### <a name="i-used-toosee-data-but-it-has-stopped"></a><span data-ttu-id="a90af-125">Я использовал toosee данных, но он был остановлен</span><span class="sxs-lookup"><span data-stu-id="a90af-125">I used toosee data, but it has stopped</span></span>
* <span data-ttu-id="a90af-126">Проверьте hello [состояние блог](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="a90af-126">Check hello [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="a90af-127">Вы достигли месячной квоты точек данных?</span><span class="sxs-lookup"><span data-stu-id="a90af-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="a90af-128">Откройте параметры/Квота и цены toofind out. Если вы достигли квоты, вы можете изменить свой тарифный план или заплатить за дополнительную емкость.</span><span class="sxs-lookup"><span data-stu-id="a90af-128">Open Settings/Quota and Pricing toofind out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="a90af-129">В разделе hello [цены схемы](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="a90af-129">See hello [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-hello-data-im-expecting"></a><span data-ttu-id="a90af-130">Я не вижу все данные hello, я ожидаемой</span><span class="sxs-lookup"><span data-stu-id="a90af-130">I don't see all hello data I'm expecting</span></span>
* <span data-ttu-id="a90af-131">Откройте hello квоты и цены колонки и проверьте ли [выборки](app-insights-sampling.md) в операции.</span><span class="sxs-lookup"><span data-stu-id="a90af-131">Open hello Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="a90af-132">(передачи 100% означает, что выборка не в операции). Hello служба Application Insights может быть набор tooaccept лишь часть hello телеметрии, поступившего от приложения.</span><span class="sxs-lookup"><span data-stu-id="a90af-132">(100% transmission means that sampling isn't in operation.) hello Application Insights service can be set tooaccept only a fraction of hello telemetry that arrives from your app.</span></span> <span data-ttu-id="a90af-133">Это помогает не выходить за пределы месячной квоты.</span><span class="sxs-lookup"><span data-stu-id="a90af-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="a90af-134">Нет данных по использованию</span><span class="sxs-lookup"><span data-stu-id="a90af-134">No usage data</span></span>
<span data-ttu-id="a90af-135">**Приводятся данные по запросам и времени ответа, но нет данных по просмотру страниц, использованию браузеров и пользователям.**</span><span class="sxs-lookup"><span data-stu-id="a90af-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="a90af-136">Вы успешно настроить данные телеметрии вашего приложения toosend с сервера hello.</span><span class="sxs-lookup"><span data-stu-id="a90af-136">You successfully set up your app toosend telemetry from hello server.</span></span> <span data-ttu-id="a90af-137">Теперь следующим шагом является слишком[Настройка телеметрии toosend веб-страницы в веб-браузере hello][usage].</span><span class="sxs-lookup"><span data-stu-id="a90af-137">Now your next step is too[set up your web pages toosend telemetry from hello web browser][usage].</span></span>

<span data-ttu-id="a90af-138">Если клиент является приложением на [телефоне или другом устройстве][platforms], из него также можно отправлять данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a90af-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="a90af-139">Используйте hello же tooset ключа инструментирования копии сервера и клиента телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a90af-139">Use hello same instrumentation key tooset up both your client and server telemetry.</span></span> <span data-ttu-id="a90af-140">Hello данных появляется в hello одного ресурса Application Insights, и вы будете иметь доступ toocorrelate события из клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="a90af-140">hello data will appear in hello same Application Insights resource, and you'll be able toocorrelate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="a90af-141">Отключение телеметрии</span><span class="sxs-lookup"><span data-stu-id="a90af-141">Disabling telemetry</span></span>
<span data-ttu-id="a90af-142">**Как отключить сбор данных телеметрии?**</span><span class="sxs-lookup"><span data-stu-id="a90af-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="a90af-143">В коде:</span><span class="sxs-lookup"><span data-stu-id="a90af-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="a90af-144">**Или**</span><span class="sxs-lookup"><span data-stu-id="a90af-144">**Or**</span></span> 

<span data-ttu-id="a90af-145">Обновите ApplicationInsights.xml (в папке ресурсов hello в проекте).</span><span class="sxs-lookup"><span data-stu-id="a90af-145">Update ApplicationInsights.xml (in hello resources folder in your project).</span></span> <span data-ttu-id="a90af-146">Добавьте следующее hello в корневом узле hello:</span><span class="sxs-lookup"><span data-stu-id="a90af-146">Add hello following under hello root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="a90af-147">При использовании метода hello XML имеется приложение hello toorestart при изменении значения hello.</span><span class="sxs-lookup"><span data-stu-id="a90af-147">Using hello XML method, you have toorestart hello application when you change hello value.</span></span>

## <a name="changing-hello-target"></a><span data-ttu-id="a90af-148">Изменение целевой hello</span><span class="sxs-lookup"><span data-stu-id="a90af-148">Changing hello target</span></span>
<span data-ttu-id="a90af-149">**Как изменить ресурс Azure, в который проект отправляет данные?**</span><span class="sxs-lookup"><span data-stu-id="a90af-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="a90af-150">[Получите ключ инструментирования hello hello новый ресурс.][java]</span><span class="sxs-lookup"><span data-stu-id="a90af-150">[Get hello instrumentation key of hello new resource.][java]</span></span>
* <span data-ttu-id="a90af-151">Если вы добавили Application Insights tooyour проект с помощью hello набора средств Azure для Eclipse, щелкните правой кнопкой мыши веб-проект, выберите **Azure**, **настроить Application Insights**и изменить ключ hello.</span><span class="sxs-lookup"><span data-stu-id="a90af-151">If you added Application Insights tooyour project using hello Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change hello key.</span></span>
* <span data-ttu-id="a90af-152">В противном случае измените раздел hello ApplicationInsights.xml в hello ресурсов в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="a90af-152">Otherwise, update hello key in ApplicationInsights.xml in hello resources folder in your project.</span></span>

## <a name="debug-data-from-hello-sdk"></a><span data-ttu-id="a90af-153">Данные из пакета SDK для hello отладки</span><span class="sxs-lookup"><span data-stu-id="a90af-153">Debug data from hello SDK</span></span>

<span data-ttu-id="a90af-154">**Как узнать какие hello, выполнив SDK**</span><span class="sxs-lookup"><span data-stu-id="a90af-154">**How can I find out what hello SDK is doing?**</span></span>

<span data-ttu-id="a90af-155">добавить дополнительные сведения о выполняемых в hello API, tooget `<SDKLogger/>` в корневом узле hello файла конфигурации ApplicationInsights.xml hello.</span><span class="sxs-lookup"><span data-stu-id="a90af-155">tooget more information about what's happening in hello API, add `<SDKLogger/>` under hello root node of hello ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="a90af-156">Можно также указать файл tooa toooutput hello средства ведения журнала:</span><span class="sxs-lookup"><span data-stu-id="a90af-156">You can also instruct hello logger toooutput tooa file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="a90af-157">Hello файлы можно найти в разделе `%temp%\javasdklogs` или `java.io.tmpdir` в случае сервера Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a90af-157">hello files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="hello-azure-start-screen"></a><span data-ttu-id="a90af-158">Hello Azure начального экрана</span><span class="sxs-lookup"><span data-stu-id="a90af-158">hello Azure start screen</span></span>
<span data-ttu-id="a90af-159">**Я просматриваю [hello портал Azure](https://portal.azure.com). Карты hello сказать мне, что-нибудь о моем приложении?**</span><span class="sxs-lookup"><span data-stu-id="a90af-159">**I'm looking at [hello Azure portal](https://portal.azure.com). Does hello map tell me something about my app?**</span></span>

<span data-ttu-id="a90af-160">Нет, он показывает hello работоспособности серверов Azure вокруг Здравствуй, мир.</span><span class="sxs-lookup"><span data-stu-id="a90af-160">No, it shows hello health of Azure servers around hello world.</span></span>

<span data-ttu-id="a90af-161">*Запуск Azure hello на доске (начальный экран) как найти данные о моем приложении?*</span><span class="sxs-lookup"><span data-stu-id="a90af-161">*From hello Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="a90af-162">При условии, что [Настройка приложения для Application Insights][java], нажмите кнопку обзора, щелкните Application Insights и выберите ресурс приложения hello, созданный для приложения.</span><span class="sxs-lookup"><span data-stu-id="a90af-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select hello app resource you created for your app.</span></span> <span data-ttu-id="a90af-163">tooget существует быстрее в будущем вы можете закрепить доске toohello запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="a90af-163">tooget there faster in future, you can pin your app toohello start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="a90af-164">Серверы в интрасети</span><span class="sxs-lookup"><span data-stu-id="a90af-164">Intranet servers</span></span>
<span data-ttu-id="a90af-165">**Можно ли наблюдать за сервером в интрасети?**</span><span class="sxs-lookup"><span data-stu-id="a90af-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="a90af-166">Да, предоставляемых ваш сервер может отправлять портал Application Insights toohello телеметрии через hello общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="a90af-166">Yes, provided your server can send telemetry toohello Application Insights portal through hello public internet.</span></span> 

<span data-ttu-id="a90af-167">В брандмауэре может потребоваться tooopen TCP-порты 80 и 443 для исходящего трафика toodc.services.visualstudio.com и f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="a90af-167">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="a90af-168">Хранение данных</span><span class="sxs-lookup"><span data-stu-id="a90af-168">Data retention</span></span>
<span data-ttu-id="a90af-169">**Как долго хранятся данные на портале hello Защищен ли он?**</span><span class="sxs-lookup"><span data-stu-id="a90af-169">**How long is data retained in hello portal? Is it secure?**</span></span>

<span data-ttu-id="a90af-170">Ознакомьтесь с разделом [Хранение данных и конфиденциальность][data].</span><span class="sxs-lookup"><span data-stu-id="a90af-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="a90af-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a90af-171">Next steps</span></span>
<span data-ttu-id="a90af-172">**Служба Application Insights настроена для серверного приложения Java. Что еще можно сделать?**</span><span class="sxs-lookup"><span data-stu-id="a90af-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="a90af-173">[Отслеживать доступность веб-страниц][availability]</span><span class="sxs-lookup"><span data-stu-id="a90af-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="a90af-174">[Отслеживать использование веб-страниц][usage]</span><span class="sxs-lookup"><span data-stu-id="a90af-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="a90af-175">[Отслеживать использование и диагностировать проблемы в приложениях для устройств][platforms]</span><span class="sxs-lookup"><span data-stu-id="a90af-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="a90af-176">[Запись tootrack использование кода приложения][track]</span><span class="sxs-lookup"><span data-stu-id="a90af-176">[Write code tootrack usage of your app][track]</span></span>
* <span data-ttu-id="a90af-177">[Записать журналы диагностики][javalogs]</span><span class="sxs-lookup"><span data-stu-id="a90af-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="a90af-178">Получение справки</span><span class="sxs-lookup"><span data-stu-id="a90af-178">Get help</span></span>
* [<span data-ttu-id="a90af-179">Переполнение стека</span><span class="sxs-lookup"><span data-stu-id="a90af-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

