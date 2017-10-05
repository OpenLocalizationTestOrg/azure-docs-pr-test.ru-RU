---
title: "Устранение ошибок \"502 — недопустимый шлюз\" и \"503 — служба недоступна\" | Документация Майкрософт"
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
ms.openlocfilehash: 397a6aaf7dc27adfa0fc0e722b8a2be5cc1d75f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="4f6a6-104">Устранение ошибок HTTP "502 — недопустимый шлюз" и "503 — служба недоступна" в работе ваших веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4f6a6-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="4f6a6-105">"502 — недопустимый шлюз" и "503 — служба недоступна" — распространенные ошибки, возникающие при работе веб-приложения, размещенного в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="4f6a6-106">Эта статья поможет вам устранить эти ошибки.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="4f6a6-107">Если вам потребуется дополнительная помощь по любому из вопросов, рассматриваемых в статье, вы можете обратиться к экспертам по Azure на [форумах MSDN Azure и Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="4f6a6-108">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="4f6a6-109">Перейдите на [сайт службы поддержки Azure](https://azure.microsoft.com/support/options/) и щелкните **Поддержка**.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="4f6a6-110">Симптом</span><span class="sxs-lookup"><span data-stu-id="4f6a6-110">Symptom</span></span>
<span data-ttu-id="4f6a6-111">При открытии веб-приложения браузер возвращает ошибку HTTP "502 — недопустимый шлюз" или HTTP "503 — служба недоступна".</span><span class="sxs-lookup"><span data-stu-id="4f6a6-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="4f6a6-112">Причина:</span><span class="sxs-lookup"><span data-stu-id="4f6a6-112">Cause</span></span>
<span data-ttu-id="4f6a6-113">Эта проблема часто связана с проблемами на уровне приложения, например:</span><span class="sxs-lookup"><span data-stu-id="4f6a6-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="4f6a6-114">слишком долгое выполнение запросов;</span><span class="sxs-lookup"><span data-stu-id="4f6a6-114">requests taking a long time</span></span>
* <span data-ttu-id="4f6a6-115">слишком высокие требования приложения к памяти и процессору;</span><span class="sxs-lookup"><span data-stu-id="4f6a6-115">application using high memory/CPU</span></span>
* <span data-ttu-id="4f6a6-116">сбой приложения из-за исключения.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-116">application crashing due to an exception.</span></span>

## <a name="troubleshooting-steps-to-solve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="4f6a6-117">Действия по устранению ошибок "502 — недопустимый шлюз" и "503 — служба недоступна"</span><span class="sxs-lookup"><span data-stu-id="4f6a6-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="4f6a6-118">Процесс устранения неполадок можно разделить на три последовательных задачи.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="4f6a6-119">Наблюдение за поведением приложения.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="4f6a6-120">Сбор данных.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="4f6a6-121">Устранение проблемы.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="4f6a6-122">[Веб-приложения службы приложений](/services/app-service/web/) содержат несколько инструментов для каждого из этих этапов.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="4f6a6-123">1. Наблюдение за поведением приложения</span><span class="sxs-lookup"><span data-stu-id="4f6a6-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="4f6a6-124">Мониторинг работоспособности службы</span><span class="sxs-lookup"><span data-stu-id="4f6a6-124">Track Service health</span></span>
<span data-ttu-id="4f6a6-125">Microsoft Azure информирует о каждом случае прерывания работы или снижения производительности службы.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="4f6a6-126">Можно следить за работоспособностью службы на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="4f6a6-127">Дополнительные сведения см. в статье [Получение информации о работоспособности службы](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="4f6a6-128">Мониторинг веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4f6a6-128">Monitor your web app</span></span>
<span data-ttu-id="4f6a6-129">Этот инструмент позволяет определить наличие проблем с приложением.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="4f6a6-130">В колонке веб-приложения щелкните элемент **Запросы и ошибки** .</span><span class="sxs-lookup"><span data-stu-id="4f6a6-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="4f6a6-131">Колонка **Метрика** содержит все метрики, которые вы можете добавить.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-131">The **Metric** blade will show you all the metrics you can add.</span></span>

<span data-ttu-id="4f6a6-132">Некоторые из этих метрик помогут вам отслеживать работу веб-приложения, например:</span><span class="sxs-lookup"><span data-stu-id="4f6a6-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="4f6a6-133">средний размер рабочего набора памяти;</span><span class="sxs-lookup"><span data-stu-id="4f6a6-133">Average memory working set</span></span>
* <span data-ttu-id="4f6a6-134">Среднее время ответа</span><span class="sxs-lookup"><span data-stu-id="4f6a6-134">Average response time</span></span>
* <span data-ttu-id="4f6a6-135">время ЦП;</span><span class="sxs-lookup"><span data-stu-id="4f6a6-135">CPU time</span></span>
* <span data-ttu-id="4f6a6-136">рабочий набор памяти;</span><span class="sxs-lookup"><span data-stu-id="4f6a6-136">Memory working set</span></span>
* <span data-ttu-id="4f6a6-137">Requests (Запросы)</span><span class="sxs-lookup"><span data-stu-id="4f6a6-137">Requests</span></span>

![Мониторинг веб-приложения для устранения ошибок HTTP "502 — недопустимый шлюз" и "503 — служба недоступна"](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="4f6a6-139">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="4f6a6-139">For more information, see:</span></span>

* [<span data-ttu-id="4f6a6-140">Мониторинг веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4f6a6-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="4f6a6-141">Создание оповещений для служб Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4f6a6-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="4f6a6-142">2) Сбор данных</span><span class="sxs-lookup"><span data-stu-id="4f6a6-142">2. Collect data</span></span>
#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="4f6a6-143">Использование портала поддержки службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4f6a6-143">Use the Azure App Service Support Portal</span></span>
<span data-ttu-id="4f6a6-144">Веб-приложения позволяют вам просматривать HTTP-журналы, журналы событий, дампы процессов и другую информацию для диагностики неполадок, связанных с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="4f6a6-145">Эту информацию вы сможете найти на нашем портале поддержки по адресу **http://&lt;имя приложения>.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="4f6a6-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="4f6a6-146">На портале поддержки службы приложений Azure вы увидите три отдельные вкладки, соответствующие трем этапам стандартного процесса устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="4f6a6-147">Наблюдение за поведением.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-147">Observe current behavior</span></span>
2. <span data-ttu-id="4f6a6-148">Сбор диагностических данных и запуск встроенных средств анализа.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-148">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="4f6a6-149">Устранение неполадки.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-149">Mitigate</span></span>

<span data-ttu-id="4f6a6-150">Если проблема происходит прямо сейчас, щелкните **Анализ** > **Диагностика** > **Диагностировать**. Так вы создадите сеанс диагностики, в ходе которого будут собираться HTTP-журналы, журналы просмотра событий, дампы памяти, журналы ошибок PHP и отчеты процесса PHP.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="4f6a6-151">После сбора данных будет выполнен их анализ и создан отчет в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span></span>

<span data-ttu-id="4f6a6-152">Вы также можете загрузить собранные данные на свой компьютер. По умолчанию они сохраняются в папке D:\home\data\DaaS.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="4f6a6-153">Дополнительные сведения о возможностях портала поддержки службы приложений Azure см. в описании [обновлений расширения портала поддержки Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="4f6a6-154">Использование консоли отладки Kudu</span><span class="sxs-lookup"><span data-stu-id="4f6a6-154">Use the Kudu Debug Console</span></span>
<span data-ttu-id="4f6a6-155">Веб-приложения оснащены консолью отладки, с помощью которой вы можете получать сведения о среде, используя функции отладки, изучения, передачи файлов и конечных точек JSON.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="4f6a6-156">Она называется *консолью Kudu* или *панелью SCM* приложения.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="4f6a6-157">Вы можете открыть эту панель по ссылке **https://&lt;имя приложения>.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="4f6a6-158">Вот некоторые возможности консоли Kudu:</span><span class="sxs-lookup"><span data-stu-id="4f6a6-158">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="4f6a6-159">настройки среды для вашего приложения;</span><span class="sxs-lookup"><span data-stu-id="4f6a6-159">environment settings for your application</span></span>
* <span data-ttu-id="4f6a6-160">потоковая передача журналов;</span><span class="sxs-lookup"><span data-stu-id="4f6a6-160">log stream</span></span>
* <span data-ttu-id="4f6a6-161">диагностический дамп;</span><span class="sxs-lookup"><span data-stu-id="4f6a6-161">diagnostic dump</span></span>
* <span data-ttu-id="4f6a6-162">консоль отладки с возможностью запуска командлетов Powershell и основных команд DOS.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="4f6a6-163">У консоли Kudu есть еще одна очень полезная функция. Если приложение создает обрабатываемые исключения, с помощью консоли Kudu и средства SysInternals Procdump вы можете получать дампы памяти.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="4f6a6-164">Эти дампы представляют собой снимок процессов, выполняемых в момент создания исключения. Вы можете использовать эти данные при анализе сложных проблем в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="4f6a6-165">Дополнительные сведения о возможностях консоли Kudu см. в статье [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/) (Интерактивные инструменты веб-сайтов Azure, о которых вам нужно знать).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="4f6a6-166">3. Устранение проблемы</span><span class="sxs-lookup"><span data-stu-id="4f6a6-166">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="4f6a6-167">Масштабирование веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4f6a6-167">Scale the web app</span></span>
<span data-ttu-id="4f6a6-168">В службе приложений Azure вы можете изменять масштаб выполнения приложения, чтобы увеличить его производительность и пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="4f6a6-169">Масштабирование веб-приложений предполагает два связанных действия: изменение ценовой категории для используемого плана службы приложений на более высокую с последующей настройкой некоторых параметров.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="4f6a6-170">Дополнительные сведения о масштабировании см. в статье [Увеличение масштаба приложения в Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="4f6a6-171">Кроме того, вы можете запустить более одного экземпляра приложения.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-171">Additionally, you can choose to run your application on more than one instance .</span></span> <span data-ttu-id="4f6a6-172">Это не только увеличит возможности обработки, но и повысит устойчивость приложения к сбоям.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="4f6a6-173">Если прекратит работу один экземпляр приложения, другой экземпляр продолжит обрабатывать запросы.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-173">If the process goes down on one instance, the other instance will still continue serving requests.</span></span>

<span data-ttu-id="4f6a6-174">Вы можете выбрать ручной или автоматический режим масштабирования.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-174">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="4f6a6-175">Использование функции AutoHeal</span><span class="sxs-lookup"><span data-stu-id="4f6a6-175">Use AutoHeal</span></span>
<span data-ttu-id="4f6a6-176">Функция AutoHeal перезапускает рабочий процесс вашего приложения при определенных условиях, которые вы определяете в настройках (например, при изменении конфигурации, при определенном количестве запросов, при достижении ограничений памяти или времени выполнения запроса).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="4f6a6-177">В большинстве случаев повторный запуск процесса будет самым быстрым способом устранения проблемы.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="4f6a6-178">Хотя веб-приложение всегда можно вручную перезапустить на портале Azure, функция AutoHeal позволяет выполнять перезапуск автоматически.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="4f6a6-179">Для этого достаточно добавить в корневой файл web.config вашего веб-приложения некоторые триггеры.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-179">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="4f6a6-180">Эти параметры одинаково работают во всех приложениях, а не только в приложениях .NET.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-180">Note that these settings would work in the same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="4f6a6-181">Дополнительные сведения см. в статье об [автоматическом восстановлении веб-сайтов Microsoft Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="4f6a6-182">Перезапуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4f6a6-182">Restart the web app</span></span>
<span data-ttu-id="4f6a6-183">Обычно это самый простой способ восстановления после проблемы, которая возникла один раз.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-183">This is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="4f6a6-184">Остановить или перезапустить приложение можно при помощи колонки веб-приложения на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![Перезапуск приложения для устранения ошибок HTTP "502 — недопустимый шлюз" и "503 — служба недоступна"](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="4f6a6-186">Управлять приложениями можно также с помощью Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="4f6a6-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="4f6a6-187">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4f6a6-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

