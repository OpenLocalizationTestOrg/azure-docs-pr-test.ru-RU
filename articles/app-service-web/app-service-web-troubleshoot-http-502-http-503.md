---
title: "Недопустимый шлюз aaaFix 502, 503 службы недоступны ошибки | Документы Microsoft"
description: "Устранение ошибок \"502 — недопустимый шлюз\" и \"503 — служба недоступна\", возникающих при работе веб-приложения, размещенного в службе приложений Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 — недопустимый шлюз, 503 — служба недоступна, ошибка 503, ошибка 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="90bce-104">Устранение ошибок HTTP "502 — недопустимый шлюз" и "503 — служба недоступна" в работе ваших веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="90bce-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="90bce-105">"502 — недопустимый шлюз" и "503 — служба недоступна" — распространенные ошибки, возникающие при работе веб-приложения, размещенного в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="90bce-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="90bce-106">Эта статья поможет вам устранить эти ошибки.</span><span class="sxs-lookup"><span data-stu-id="90bce-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="90bce-107">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello MSDN Azure и hello переполнения стека форумы](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="90bce-107">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="90bce-108">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="90bce-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="90bce-109">Go toohello [сайте поддержки Azure](https://azure.microsoft.com/support/options/) и выберите команду **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="90bce-109">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="90bce-110">Симптом</span><span class="sxs-lookup"><span data-stu-id="90bce-110">Symptom</span></span>
<span data-ttu-id="90bce-111">При просмотре toohello веб-приложения, он возвращает HTTP «502 — неправильный шлюз» ошибка "или" HTTP «503 Служба недоступна» ошибка.</span><span class="sxs-lookup"><span data-stu-id="90bce-111">When you browse toohello web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="90bce-112">Причина:</span><span class="sxs-lookup"><span data-stu-id="90bce-112">Cause</span></span>
<span data-ttu-id="90bce-113">Эта проблема часто связана с проблемами на уровне приложения, например:</span><span class="sxs-lookup"><span data-stu-id="90bce-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="90bce-114">слишком долгое выполнение запросов;</span><span class="sxs-lookup"><span data-stu-id="90bce-114">requests taking a long time</span></span>
* <span data-ttu-id="90bce-115">слишком высокие требования приложения к памяти и процессору;</span><span class="sxs-lookup"><span data-stu-id="90bce-115">application using high memory/CPU</span></span>
* <span data-ttu-id="90bce-116">Сбой из-за исключения tooan приложения.</span><span class="sxs-lookup"><span data-stu-id="90bce-116">application crashing due tooan exception.</span></span>

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="90bce-117">Устранение неполадок действия toosolve «502 — неправильный шлюз» и «503 — Служба недоступна» ошибки</span><span class="sxs-lookup"><span data-stu-id="90bce-117">Troubleshooting steps toosolve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="90bce-118">Процесс устранения неполадок можно разделить на три последовательных задачи.</span><span class="sxs-lookup"><span data-stu-id="90bce-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="90bce-119">Наблюдение за поведением приложения.</span><span class="sxs-lookup"><span data-stu-id="90bce-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="90bce-120">Сбор данных.</span><span class="sxs-lookup"><span data-stu-id="90bce-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="90bce-121">Hello проблем</span><span class="sxs-lookup"><span data-stu-id="90bce-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="90bce-122">[Веб-приложения службы приложений](/services/app-service/web/) содержат несколько инструментов для каждого из этих этапов.</span><span class="sxs-lookup"><span data-stu-id="90bce-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="90bce-123">1. Наблюдение за поведением приложения</span><span class="sxs-lookup"><span data-stu-id="90bce-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="90bce-124">Мониторинг работоспособности службы</span><span class="sxs-lookup"><span data-stu-id="90bce-124">Track Service health</span></span>
<span data-ttu-id="90bce-125">Microsoft Azure информирует о каждом случае прерывания работы или снижения производительности службы.</span><span class="sxs-lookup"><span data-stu-id="90bce-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="90bce-126">Можно отслеживать работоспособность hello hello службы на hello [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="90bce-126">You can track hello health of hello service on hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="90bce-127">Дополнительные сведения см. в статье [Получение информации о работоспособности службы](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="90bce-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="90bce-128">Мониторинг веб-приложения</span><span class="sxs-lookup"><span data-stu-id="90bce-128">Monitor your web app</span></span>
<span data-ttu-id="90bce-129">Этот параметр позволяет toofind ожидания, если в приложении возникают проблемы.</span><span class="sxs-lookup"><span data-stu-id="90bce-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="90bce-130">В колонке веб-приложение, щелкните hello **запросов и ошибок** плитки.</span><span class="sxs-lookup"><span data-stu-id="90bce-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="90bce-131">Hello **метрика** колонке Показать все показатели hello, можно добавить.</span><span class="sxs-lookup"><span data-stu-id="90bce-131">hello **Metric** blade will show you all hello metrics you can add.</span></span>

<span data-ttu-id="90bce-132">Некоторые показатели hello, вам может быть toomonitor для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="90bce-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="90bce-133">средний размер рабочего набора памяти;</span><span class="sxs-lookup"><span data-stu-id="90bce-133">Average memory working set</span></span>
* <span data-ttu-id="90bce-134">Среднее время ответа</span><span class="sxs-lookup"><span data-stu-id="90bce-134">Average response time</span></span>
* <span data-ttu-id="90bce-135">время ЦП;</span><span class="sxs-lookup"><span data-stu-id="90bce-135">CPU time</span></span>
* <span data-ttu-id="90bce-136">рабочий набор памяти;</span><span class="sxs-lookup"><span data-stu-id="90bce-136">Memory working set</span></span>
* <span data-ttu-id="90bce-137">Requests (Запросы)</span><span class="sxs-lookup"><span data-stu-id="90bce-137">Requests</span></span>

![Мониторинг веб-приложения для устранения ошибок HTTP "502 — недопустимый шлюз" и "503 — служба недоступна"](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="90bce-139">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="90bce-139">For more information, see:</span></span>

* [<span data-ttu-id="90bce-140">Мониторинг веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="90bce-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="90bce-141">Создание оповещений для служб Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="90bce-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="90bce-142">2) Сбор данных</span><span class="sxs-lookup"><span data-stu-id="90bce-142">2. Collect data</span></span>
#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="90bce-143">Использовать hello портал поддержки службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="90bce-143">Use hello Azure App Service Support Portal</span></span>
<span data-ttu-id="90bce-144">Веб-приложения предоставляет возможность hello tootroubleshoot связанные tooyour проблемы веб-приложения, просмотрев HTTP журналы, журналы событий, дамп и многое другое.</span><span class="sxs-lookup"><span data-stu-id="90bce-144">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="90bce-145">Эту информацию вы сможете найти на нашем портале поддержки по адресу **http://&lt;имя приложения>.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="90bce-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="90bce-146">портал Hello поддержка службы приложения Azure предоставляет три отдельных вкладках toosupport hello три действия по устранению неполадок чаще.</span><span class="sxs-lookup"><span data-stu-id="90bce-146">hello Azure App Service Support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="90bce-147">Наблюдение за поведением.</span><span class="sxs-lookup"><span data-stu-id="90bce-147">Observe current behavior</span></span>
2. <span data-ttu-id="90bce-148">Анализ, сбор данных диагностики и запустив hello встроенных анализаторы</span><span class="sxs-lookup"><span data-stu-id="90bce-148">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="90bce-149">Устранение неполадки.</span><span class="sxs-lookup"><span data-stu-id="90bce-149">Mitigate</span></span>

<span data-ttu-id="90bce-150">Если происходит проблема hello прямо сейчас, нажмите кнопку **анализ** > **диагностики** > **диагностики теперь** toocreate сеанс диагностики, который будет собирать HTTP журналы, журналы программы просмотра событий, памяти, дампы, журналы ошибок PHP и PHP обработки отчета.</span><span class="sxs-lookup"><span data-stu-id="90bce-150">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="90bce-151">После сбора данных hello, он также выполните анализ данных hello и предоставить вам HTML-отчета.</span><span class="sxs-lookup"><span data-stu-id="90bce-151">Once hello data is collected, it will also run an analysis on hello data and provide you with an HTML report.</span></span>

<span data-ttu-id="90bce-152">В случае, если вам нужны данные toodownload hello, по умолчанию, он будет храниться в папке D:\home\data\DaaS hello.</span><span class="sxs-lookup"><span data-stu-id="90bce-152">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="90bce-153">Дополнительные сведения на портале hello поддержка службы приложения Azure см. в разделе [tooSupport обновлений расширение сайта для веб-сайтов Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="90bce-153">For more information on hello Azure App Service Support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="90bce-154">Использование консоли отладки Kudu hello</span><span class="sxs-lookup"><span data-stu-id="90bce-154">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="90bce-155">Веб-приложения оснащены консолью отладки, с помощью которой вы можете получать сведения о среде, используя функции отладки, изучения, передачи файлов и конечных точек JSON.</span><span class="sxs-lookup"><span data-stu-id="90bce-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="90bce-156">Это называется hello *консоли Kudu* или hello *SCM мониторинга* веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="90bce-156">This is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="90bce-157">Доступ к этой панели мониторинга переходит в ссылке toohello **https://&lt;имя вашего приложения >.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="90bce-157">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="90bce-158">Ниже приведены некоторые Kudu предоставляет следующие аспекты hello.</span><span class="sxs-lookup"><span data-stu-id="90bce-158">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="90bce-159">настройки среды для вашего приложения;</span><span class="sxs-lookup"><span data-stu-id="90bce-159">environment settings for your application</span></span>
* <span data-ttu-id="90bce-160">потоковая передача журналов;</span><span class="sxs-lookup"><span data-stu-id="90bce-160">log stream</span></span>
* <span data-ttu-id="90bce-161">диагностический дамп;</span><span class="sxs-lookup"><span data-stu-id="90bce-161">diagnostic dump</span></span>
* <span data-ttu-id="90bce-162">консоль отладки с возможностью запуска командлетов Powershell и основных команд DOS.</span><span class="sxs-lookup"><span data-stu-id="90bce-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="90bce-163">Другой полезной функцией Kudu является, в случае, если приложение является создание исключений первого шанса, можно использовать Kudu и дампы hello SysInternals средство Procdump toocreate памяти.</span><span class="sxs-lookup"><span data-stu-id="90bce-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="90bce-164">Эти дампы памяти представляют собой моментальные снимки процесса hello и часто помогает устранить устранения более серьезных проблем с веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="90bce-164">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="90bce-165">Дополнительные сведения о возможностях консоли Kudu см. в статье [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/) (Интерактивные инструменты веб-сайтов Azure, о которых вам нужно знать).</span><span class="sxs-lookup"><span data-stu-id="90bce-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="90bce-166">3. Hello проблем</span><span class="sxs-lookup"><span data-stu-id="90bce-166">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="90bce-167">Масштаб hello веб-приложения</span><span class="sxs-lookup"><span data-stu-id="90bce-167">Scale hello web app</span></span>
<span data-ttu-id="90bce-168">В службе приложений Azure для повышения производительности и пропускной способности, можно изменить масштаб hello, с которой выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="90bce-168">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="90bce-169">Вертикальное масштабирование веб-приложение включает в себя два связанных действий: изменение вашей tooa план службы приложений, выше ценовой категории и определенных настроек после переключения toohello выше ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="90bce-169">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="90bce-170">Дополнительные сведения о масштабировании см. в статье [Увеличение масштаба приложения в Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="90bce-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="90bce-171">Кроме того вы можете toorun приложения на более одного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="90bce-171">Additionally, you can choose toorun your application on more than one instance .</span></span> <span data-ttu-id="90bce-172">Это не только увеличит возможности обработки, но и повысит устойчивость приложения к сбоям.</span><span class="sxs-lookup"><span data-stu-id="90bce-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="90bce-173">Если hello процесс перестает работать на одном экземпляре, hello другого экземпляра будет по-прежнему обработку запросов.</span><span class="sxs-lookup"><span data-stu-id="90bce-173">If hello process goes down on one instance, hello other instance will still continue serving requests.</span></span>

<span data-ttu-id="90bce-174">Можно задать hello масштабирования toobe вручную или автоматически.</span><span class="sxs-lookup"><span data-stu-id="90bce-174">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="90bce-175">Использование функции AutoHeal</span><span class="sxs-lookup"><span data-stu-id="90bce-175">Use AutoHeal</span></span>
<span data-ttu-id="90bce-176">Функция AutoHeal перезапускается hello рабочий процесс для приложения с учетом выбранных (например, изменения конфигурации, запросы, ограничения памяти или время hello необходимости tooexecute запрос) параметров.</span><span class="sxs-lookup"><span data-stu-id="90bce-176">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="90bce-177">Большую часть времени hello hello процесс очистки является hello самый быстрый способ toorecover из-за проблемы.</span><span class="sxs-lookup"><span data-stu-id="90bce-177">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="90bce-178">Хотя можно всегда перезапускать веб-приложения hello из непосредственно в hello портал Azure, AutoHeal будет сделать это автоматически.</span><span class="sxs-lookup"><span data-stu-id="90bce-178">Though you can always restart hello web app from directly within hello Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="90bce-179">Требуется toodo всего добавить некоторые триггеры в hello корневом файле web.config для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="90bce-179">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="90bce-180">Обратите внимание, что эти параметры будут работать в hello таким же способом, даже если приложение не один .net.</span><span class="sxs-lookup"><span data-stu-id="90bce-180">Note that these settings would work in hello same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="90bce-181">Дополнительные сведения см. в статье об [автоматическом восстановлении веб-сайтов Microsoft Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="90bce-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="90bce-182">Перезапустить веб-приложение hello</span><span class="sxs-lookup"><span data-stu-id="90bce-182">Restart hello web app</span></span>
<span data-ttu-id="90bce-183">Это часто toorecover простейший способ hello после однократного возникновения проблем.</span><span class="sxs-lookup"><span data-stu-id="90bce-183">This is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="90bce-184">На hello [портала Azure](https://portal.azure.com/), в колонке веб-приложения вы toostop параметры hello или перезапустите приложение.</span><span class="sxs-lookup"><span data-stu-id="90bce-184">On hello [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![Перезапустите приложения ошибки HTTP toosolve 502 — неправильный шлюз и 503 — Служба недоступна](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="90bce-186">Управлять приложениями можно также с помощью Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="90bce-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="90bce-187">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="90bce-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

