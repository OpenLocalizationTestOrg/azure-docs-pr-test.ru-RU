---
title: "aaaMonitor динамической ASP.NET веб-приложения с помощью Azure Application Insights | Документы Microsoft"
description: "Мониторинг производительности веб-сайта без необходимости его повторного развертывания. Работает с веб-приложениями ASP.NET, размещенными локально, на виртуальных машинах или в Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="c0055-104">Инструментирование веб-приложений во время выполнения с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="c0055-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="c0055-105">Можно инструментировать динамической веб-приложения с помощью Azure Application Insights, без необходимости toomodify или повторного развертывания вашего кода.</span><span class="sxs-lookup"><span data-stu-id="c0055-105">You can instrument a live web app with Azure Application Insights, without having toomodify or redeploy your code.</span></span> <span data-ttu-id="c0055-106">Если приложения размещаются на локальном сервере IIS, необходимо установить монитор состояний.</span><span class="sxs-lookup"><span data-stu-id="c0055-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="c0055-107">Случае веб-приложениях Azure или запустить на виртуальной Машине Azure, вы можете включить мониторинг Application Insights с помощью панели управления Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c0055-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from hello Azure control panel.</span></span> <span data-ttu-id="c0055-108">(См. статьи об инструментировании [динамических веб-приложений J2EE](app-insights-java-live.md) и [облачных служб Azure](app-insights-cloudservices.md).) Вам потребуется подписка [Microsoft Azure](http://azure.com) .</span><span class="sxs-lookup"><span data-stu-id="c0055-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![примеры диаграмм](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="c0055-110">Имеется выбор из трех маршруты tooapply Application Insights tooyour веб-приложений .NET:</span><span class="sxs-lookup"><span data-stu-id="c0055-110">You have a choice of three routes tooapply Application Insights tooyour .NET web applications:</span></span>

* <span data-ttu-id="c0055-111">**Время сборки:** [hello добавить пакет SDK Application Insights] [ greenbrown] tooyour кода веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c0055-111">**Build time:** [Add hello Application Insights SDK][greenbrown] tooyour web app code.</span></span>
* <span data-ttu-id="c0055-112">**Время выполнения:** инструментирования веб-приложения на сервере hello, как описано ниже, без повторное создание и развертывание кода hello.</span><span class="sxs-lookup"><span data-stu-id="c0055-112">**Run time:** Instrument your web app on hello server, as described below, without rebuilding and redeploying hello code.</span></span>
* <span data-ttu-id="c0055-113">**Both:** сборка hello SDK в код веб-приложения и также применить hello расширения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c0055-113">**Both:** Build hello SDK into your web app code, and also apply hello run-time extensions.</span></span> <span data-ttu-id="c0055-114">Получение hello наиболее обоих вариантов.</span><span class="sxs-lookup"><span data-stu-id="c0055-114">Get hello best of both options.</span></span>

<span data-ttu-id="c0055-115">Ниже представлено общее сравнение предлагаемых вариантов.</span><span class="sxs-lookup"><span data-stu-id="c0055-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="c0055-116">Во время сборки</span><span class="sxs-lookup"><span data-stu-id="c0055-116">Build time</span></span> | <span data-ttu-id="c0055-117">Во время выполнения</span><span class="sxs-lookup"><span data-stu-id="c0055-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0055-118">Запросы и исключения</span><span class="sxs-lookup"><span data-stu-id="c0055-118">Requests & exceptions</span></span> |<span data-ttu-id="c0055-119">Да</span><span class="sxs-lookup"><span data-stu-id="c0055-119">Yes</span></span> |<span data-ttu-id="c0055-120">Да</span><span class="sxs-lookup"><span data-stu-id="c0055-120">Yes</span></span> |
| [<span data-ttu-id="c0055-121">Более подробные исключения</span><span class="sxs-lookup"><span data-stu-id="c0055-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="c0055-122">Да</span><span class="sxs-lookup"><span data-stu-id="c0055-122">Yes</span></span> |
| [<span data-ttu-id="c0055-123">Диагностика зависимостей</span><span class="sxs-lookup"><span data-stu-id="c0055-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="c0055-124">На платформе .NET 4.6 или более поздней, неполные сведения</span><span class="sxs-lookup"><span data-stu-id="c0055-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="c0055-125">Да, полные сведения: коды результатов, текст команд SQL, HTTP-команда</span><span class="sxs-lookup"><span data-stu-id="c0055-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="c0055-126">Счетчики производительности системы</span><span class="sxs-lookup"><span data-stu-id="c0055-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="c0055-127">Да</span><span class="sxs-lookup"><span data-stu-id="c0055-127">Yes</span></span> |<span data-ttu-id="c0055-128">Да</span><span class="sxs-lookup"><span data-stu-id="c0055-128">Yes</span></span> |
| <span data-ttu-id="c0055-129">[API для пользовательской телеметрии][api]</span><span class="sxs-lookup"><span data-stu-id="c0055-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="c0055-130">Да</span><span class="sxs-lookup"><span data-stu-id="c0055-130">Yes</span></span> |<span data-ttu-id="c0055-131">Нет</span><span class="sxs-lookup"><span data-stu-id="c0055-131">No</span></span> |
| [<span data-ttu-id="c0055-132">Интеграция журнала трассировки</span><span class="sxs-lookup"><span data-stu-id="c0055-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="c0055-133">Да</span><span class="sxs-lookup"><span data-stu-id="c0055-133">Yes</span></span> |<span data-ttu-id="c0055-134">Нет</span><span class="sxs-lookup"><span data-stu-id="c0055-134">No</span></span> |
| [<span data-ttu-id="c0055-135">Просмотр страницы и пользовательские данные</span><span class="sxs-lookup"><span data-stu-id="c0055-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="c0055-136">Да</span><span class="sxs-lookup"><span data-stu-id="c0055-136">Yes</span></span> |<span data-ttu-id="c0055-137">Нет</span><span class="sxs-lookup"><span data-stu-id="c0055-137">No</span></span> |
| <span data-ttu-id="c0055-138">Требуется код toorebuild</span><span class="sxs-lookup"><span data-stu-id="c0055-138">Need toorebuild code</span></span> |<span data-ttu-id="c0055-139">Да</span><span class="sxs-lookup"><span data-stu-id="c0055-139">Yes</span></span> | <span data-ttu-id="c0055-140">Нет</span><span class="sxs-lookup"><span data-stu-id="c0055-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="c0055-141">Мониторинг активного веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="c0055-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="c0055-142">Если приложение выполняется как Azure веб-службы, здесь как tooswitch о наблюдении за:</span><span class="sxs-lookup"><span data-stu-id="c0055-142">If your application is running as an Azure web service, here's how tooswitch on monitoring:</span></span>

* <span data-ttu-id="c0055-143">Выберите Application Insights на панели управления приложение hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="c0055-143">Select Application Insights on hello app's control panel in Azure.</span></span>

    ![Настройка Application Insights для веб-приложения Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="c0055-145">Когда открывается страница сводки hello Application Insights, щелкните ссылку hello в hello нижней tooopen hello полный ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c0055-145">When hello Application Insights summary page opens, click hello link at hello bottom tooopen hello full Application Insights resource.</span></span>

    ![Пролистайте tooApplication аналитики](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="c0055-147">[Мониторинг облачных приложений и приложений виртуальной машины](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="c0055-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="c0055-148">Включение мониторинга на стороне клиента в Azure</span><span class="sxs-lookup"><span data-stu-id="c0055-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="c0055-149">Если вы включили Application Insights в Azure, можно добавить функцию для получения сведений о просмотрах страниц и данных телеметрии пользователя.</span><span class="sxs-lookup"><span data-stu-id="c0055-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="c0055-150">Выберите элементы "Параметры > Параметры приложения".</span><span class="sxs-lookup"><span data-stu-id="c0055-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="c0055-151">В разделе "Параметры приложения" добавьте новую пару "ключ — значение":</span><span class="sxs-lookup"><span data-stu-id="c0055-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="c0055-152">Ключ: `APPINSIGHTS_JAVASCRIPT_ENABLED`.</span><span class="sxs-lookup"><span data-stu-id="c0055-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="c0055-153">Значение: `true`</span><span class="sxs-lookup"><span data-stu-id="c0055-153">Value: `true`</span></span>
3. <span data-ttu-id="c0055-154">**Сохранить** hello параметры и **перезапустите** приложения.</span><span class="sxs-lookup"><span data-stu-id="c0055-154">**Save** hello settings and **Restart** your app.</span></span>

<span data-ttu-id="c0055-155">Теперь пакет SDK для Application Insights JavaScript Hello вставляется в каждой веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="c0055-155">hello Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="c0055-156">Мониторинг активного веб-приложения IIS</span><span class="sxs-lookup"><span data-stu-id="c0055-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="c0055-157">Если приложение размещено на сервере IIS, включите Application Insights с помощью монитора состояний.</span><span class="sxs-lookup"><span data-stu-id="c0055-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="c0055-158">Войдите на веб-сервер IIS с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="c0055-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="c0055-159">Если монитор состояния Application Insights не установлена, загрузите и запустите hello [установщика монитор состояния](http://go.microsoft.com/fwlink/?LinkId=506648) (или запустите [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) и найдите в нем аналитики состояние приложения Монитор).</span><span class="sxs-lookup"><span data-stu-id="c0055-159">If Application Insights Status Monitor is not already installed, download and run hello [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="c0055-160">В мониторе состояния выберите hello установлен веб-приложение или веб-сайта, которые должны toomonitor.</span><span class="sxs-lookup"><span data-stu-id="c0055-160">In Status Monitor, select hello installed web application or website that you want toomonitor.</span></span> <span data-ttu-id="c0055-161">Выполните вход с использованием учетных данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c0055-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="c0055-162">Настройка ресурсов hello место toosee hello результаты на портале Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="c0055-162">Configure hello resource where you want toosee hello results in hello Application Insights portal.</span></span> <span data-ttu-id="c0055-163">(Обычно является наилучшим toocreate новый ресурс.</span><span class="sxs-lookup"><span data-stu-id="c0055-163">(Normally, it's best toocreate a new resource.</span></span> <span data-ttu-id="c0055-164">Выберите имеющийся ресурс, если у вас уже есть [веб-тесты][availability] или [наблюдение за клиентами][client] для этого приложения.)</span><span class="sxs-lookup"><span data-stu-id="c0055-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Выберите приложение и ресурс.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="c0055-166">Перезапустите IIS.</span><span class="sxs-lookup"><span data-stu-id="c0055-166">Restart IIS.</span></span>

    ![Выберите перезапуска вверху hello диалогового окна "hello".](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="c0055-168">Работа вашей веб-службы будет ненадолго прервана.</span><span class="sxs-lookup"><span data-stu-id="c0055-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="c0055-169">Настройка параметров мониторинга</span><span class="sxs-lookup"><span data-stu-id="c0055-169">Customize monitoring options</span></span>

<span data-ttu-id="c0055-170">Application Insights задействуется библиотек DLL и ApplicationInsights.config tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c0055-170">Enabling Application Insights adds DLLs and ApplicationInsights.config tooyour web app.</span></span> <span data-ttu-id="c0055-171">Вы можете [изменить файл .config hello](app-insights-configuration-with-applicationinsights-config.md) toochange некоторых параметров hello.</span><span class="sxs-lookup"><span data-stu-id="c0055-171">You can [edit hello .config file](app-insights-configuration-with-applicationinsights-config.md) toochange some of hello options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="c0055-172">При повторной публикации приложения необходимо повторно включить Application Insights</span><span class="sxs-lookup"><span data-stu-id="c0055-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="c0055-173">Прежде чем повторно опубликовать приложение, рассмотрите возможность [добавления Application Insights toohello кода в Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="c0055-173">Before you re-publish your app, consider [adding Application Insights toohello code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="c0055-174">Вы сможете получить более подробные данные телеметрии hello возможность toowrite настроенной телеметрии и.</span><span class="sxs-lookup"><span data-stu-id="c0055-174">You'll get more detailed telemetry and hello ability toowrite custom telemetry.</span></span>

<span data-ttu-id="c0055-175">Если требуется, чтобы toore-публикации без добавления Application Insights toohello кода, имейте в виду, что процесс развертывания hello может привести к удалению библиотек DLL hello и ApplicationInsights.config из hello публикации веб-узла.</span><span class="sxs-lookup"><span data-stu-id="c0055-175">If you want toore-publish without adding Application Insights toohello code, be aware that hello deployment process may delete hello DLLs and ApplicationInsights.config from hello published web site.</span></span> <span data-ttu-id="c0055-176">Таким образом:</span><span class="sxs-lookup"><span data-stu-id="c0055-176">Therefore:</span></span>

1. <span data-ttu-id="c0055-177">При редактировании файла ApplicationInsights.config сделайте его копию, прежде чем повторно опубликовать приложение.</span><span class="sxs-lookup"><span data-stu-id="c0055-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="c0055-178">Повторно опубликуйте приложение.</span><span class="sxs-lookup"><span data-stu-id="c0055-178">Republish your app.</span></span>
3. <span data-ttu-id="c0055-179">Повторно включите мониторинг Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c0055-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="c0055-180">(Используйте соответствующий метод hello: панель управления hello Azure web app или hello монитор состояния узла IIS.)</span><span class="sxs-lookup"><span data-stu-id="c0055-180">(Use hello appropriate method: either hello Azure web app control panel, or hello Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="c0055-181">Возобновить, любые изменения, выполняемые на hello config-файла.</span><span class="sxs-lookup"><span data-stu-id="c0055-181">Reinstate any edits you performed on hello .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="c0055-182">Устранение неполадок конфигурации среды выполнения Application Insights</span><span class="sxs-lookup"><span data-stu-id="c0055-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="c0055-183">Проблемы с подключением?</span><span class="sxs-lookup"><span data-stu-id="c0055-183">Can't connect?</span></span> <span data-ttu-id="c0055-184">Отсутствие данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="c0055-184">No telemetry?</span></span>

* <span data-ttu-id="c0055-185">Откройте [hello необходимые исходящие порты](app-insights-ip-addresses.md#outgoing-ports) в toowork монитор состояния tooallow брандмауэра сервера.</span><span class="sxs-lookup"><span data-stu-id="c0055-185">Open [hello necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall tooallow Status Monitor toowork.</span></span>

* <span data-ttu-id="c0055-186">Откройте монитор состояний и на левой панели выберите свое приложение.</span><span class="sxs-lookup"><span data-stu-id="c0055-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="c0055-187">Проверка наличия любые диагностические сообщения для этого приложения в раздел «Уведомления конфигурации» hello:</span><span class="sxs-lookup"><span data-stu-id="c0055-187">Check if there are any diagnostics messages for this application in hello "Configuration notifications" section:</span></span>

  ![Откройте колонку toosee hello производительность запроса, время отклика, зависимости и другие данные](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="c0055-189">На сервере hello Если вы видите сообщение «Недостаточно прав», выполните hello следующих действий:</span><span class="sxs-lookup"><span data-stu-id="c0055-189">On hello server, if you see a message about "insufficient permissions", try hello following:</span></span>
  * <span data-ttu-id="c0055-190">В диспетчере служб IIS выберите пул приложений, откройте **Дополнительные параметры**и в разделе **модель процесса** Обратите внимание, идентификация hello.</span><span class="sxs-lookup"><span data-stu-id="c0055-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note hello identity.</span></span>
  * <span data-ttu-id="c0055-191">В панели управления компьютера добавьте эту группу пользователей монитора производительности toohello удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c0055-191">In Computer management control panel, add this identity toohello Performance Monitor Users group.</span></span>
* <span data-ttu-id="c0055-192">Если на вашем сервере установлен MMA/SCOM (Systems Center Operations Manager), некоторые версии могут конфликтовать.</span><span class="sxs-lookup"><span data-stu-id="c0055-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="c0055-193">Удалите SCOM и состояние монитора и снова установите последние версии hello.</span><span class="sxs-lookup"><span data-stu-id="c0055-193">Uninstall both SCOM and Status Monitor, and re-install hello latest versions.</span></span>
* <span data-ttu-id="c0055-194">Ознакомьтесь с разделом [Устранение неполадок][qna].</span><span class="sxs-lookup"><span data-stu-id="c0055-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="c0055-195">Требования к системе</span><span class="sxs-lookup"><span data-stu-id="c0055-195">System Requirements</span></span>
<span data-ttu-id="c0055-196">Операционные системы, которые поддерживаются для монитора состояний Application Insights на сервере:</span><span class="sxs-lookup"><span data-stu-id="c0055-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="c0055-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="c0055-197">Windows Server 2008</span></span>
* <span data-ttu-id="c0055-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c0055-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="c0055-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c0055-199">Windows Server 2012</span></span>
* <span data-ttu-id="c0055-200">Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="c0055-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="c0055-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c0055-201">Windows Server 2016</span></span>

<span data-ttu-id="c0055-202">На них должны быть установлены последний пакет обновления и платформа .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="c0055-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="c0055-203">На стороне клиента hello: Windows 7, 8, 8.1 и 10, с .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="c0055-203">On hello client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="c0055-204">Поддерживаются такие версии IIS: 7, 7.5, 8, 8.5 (IIS – обязательный компонент).</span><span class="sxs-lookup"><span data-stu-id="c0055-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="c0055-205">Автоматизация с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0055-205">Automation with PowerShell</span></span>
<span data-ttu-id="c0055-206">Мониторинг можно запускать и останавливать с помощью PowerShell на сервере IIS.</span><span class="sxs-lookup"><span data-stu-id="c0055-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="c0055-207">Сначала следует импортируйте модуль hello Application Insights:</span><span class="sxs-lookup"><span data-stu-id="c0055-207">First import hello Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="c0055-208">Узнайте, какие приложения отслеживаются:</span><span class="sxs-lookup"><span data-stu-id="c0055-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="c0055-209">`-Name`Имя веб-приложения hello (необязательно).</span><span class="sxs-lookup"><span data-stu-id="c0055-209">`-Name` (Optional) hello name of a web app.</span></span>
* <span data-ttu-id="c0055-210">Отображает состояние мониторинга Application Insights для каждого веб-приложения (или с именем приложения hello) hello в сервер IIS.</span><span class="sxs-lookup"><span data-stu-id="c0055-210">Displays hello Application Insights monitoring status for each web app (or hello named app) in this IIS server.</span></span>
* <span data-ttu-id="c0055-211">Возвращает `ApplicationInsightsApplication` для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="c0055-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="c0055-212">`SdkState==EnabledAfterDeployment`: Приложение отслеживается и была инструментирована во время выполнения средством hello монитор состояния либо с помощью `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="c0055-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by hello Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="c0055-213">`SdkState==Disabled`: приложение hello не инструментированы для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c0055-213">`SdkState==Disabled`: hello app is not instrumented for Application Insights.</span></span> <span data-ttu-id="c0055-214">Он никогда не были инструментированы, либо во время выполнения наблюдение отключено средство hello монитор состояния или с `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="c0055-214">Either it was never instrumented, or run-time monitoring was disabled with hello Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="c0055-215">`SdkState==EnabledByCodeInstrumentation`: приложение hello были инструментированы, добавив hello SDK toohello исходного кода.</span><span class="sxs-lookup"><span data-stu-id="c0055-215">`SdkState==EnabledByCodeInstrumentation`: hello app was instrumented by adding hello SDK toohello source code.</span></span> <span data-ttu-id="c0055-216">Этот пакет SDK нельзя обновить или остановить.</span><span class="sxs-lookup"><span data-stu-id="c0055-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="c0055-217">`SdkVersion`отображается версия hello используется для наблюдения за этим приложением.</span><span class="sxs-lookup"><span data-stu-id="c0055-217">`SdkVersion` shows hello version in use for monitoring this app.</span></span>
  * <span data-ttu-id="c0055-218">`LatestAvailableSdkVersion`Показывает в настоящее время доступна версия hello hello NuGet gallery.</span><span class="sxs-lookup"><span data-stu-id="c0055-218">`LatestAvailableSdkVersion`shows hello version currently available on hello NuGet gallery.</span></span> <span data-ttu-id="c0055-219">версия toothis приложения hello tooupgrade, используйте `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="c0055-219">tooupgrade hello app toothis version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="c0055-220">`-Name`Имя Hello приложение hello в службах IIS</span><span class="sxs-lookup"><span data-stu-id="c0055-220">`-Name` hello name of hello app in IIS</span></span>
* <span data-ttu-id="c0055-221">`-InstrumentationKey`Здравствуйте, ikey из hello место отображения toobe результаты hello ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c0055-221">`-InstrumentationKey` hello ikey of hello Application Insights resource where you want hello results toobe displayed.</span></span>
* <span data-ttu-id="c0055-222">Этот командлет влияет только на приложения, которые еще не инструментированы, то есть SdkState==NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="c0055-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="c0055-223">командлет Hello не влияет на приложение, которое уже инструментирован.</span><span class="sxs-lookup"><span data-stu-id="c0055-223">hello cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="c0055-224">Она не важно, содержит ли приложение hello была инструментирована во время сборки, добавив код toohello SDK hello, или во время выполнения при предыдущем использовании этого командлета.</span><span class="sxs-lookup"><span data-stu-id="c0055-224">It does not matter whether hello app was instrumented at build time by adding hello SDK toohello code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="c0055-225">приложение hello tooinstrument версия пакета SDK для Hello — hello версию, которая последний раз загрузили toothis сервер.</span><span class="sxs-lookup"><span data-stu-id="c0055-225">hello SDK version used tooinstrument hello app is hello version that was most recently downloaded toothis server.</span></span>

    <span data-ttu-id="c0055-226">последнюю версию toodownload hello, используйте ApplicationInsightsVersion обновления.</span><span class="sxs-lookup"><span data-stu-id="c0055-226">toodownload hello latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="c0055-227">В случае успешного выполнения возвращает `ApplicationInsightsApplication` .</span><span class="sxs-lookup"><span data-stu-id="c0055-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="c0055-228">Если не удается, он регистрирует toostderr трассировки.</span><span class="sxs-lookup"><span data-stu-id="c0055-228">If it fails, it logs a trace toostderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="c0055-229">`-Name`Hello имя приложения в IIS</span><span class="sxs-lookup"><span data-stu-id="c0055-229">`-Name` hello name of an app in IIS</span></span>
* <span data-ttu-id="c0055-230">`-All` — останавливает мониторинг всех приложений на этом сервере IIS, для которых `SdkState==EnabledAfterDeployment`.</span><span class="sxs-lookup"><span data-stu-id="c0055-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="c0055-231">Останавливает наблюдение для hello иные приложения и удаляет инструментирования.</span><span class="sxs-lookup"><span data-stu-id="c0055-231">Stops monitoring hello specified apps and removes instrumentation.</span></span> <span data-ttu-id="c0055-232">Работает только для приложений, которые были инструментированы, во время выполнения с помощью hello наблюдение за состоянием средства или ApplicationInsightsApplication запуска.</span><span class="sxs-lookup"><span data-stu-id="c0055-232">It only works for apps that have been instrumented at run-time using hello Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="c0055-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="c0055-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="c0055-234">Возвращает ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="c0055-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="c0055-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="c0055-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="c0055-236">`-Name`: hello имя веб-приложения в IIS.</span><span class="sxs-lookup"><span data-stu-id="c0055-236">`-Name`: hello name of a web app in IIS.</span></span>
* <span data-ttu-id="c0055-237">`-InstrumentationKey` (необязательный параметр). Используйте этот toochange hello ресурсов toowhich hello телеметрии приложения отправляется.</span><span class="sxs-lookup"><span data-stu-id="c0055-237">`-InstrumentationKey` (Optional.) Use this toochange hello resource toowhich hello app's telemetry is sent.</span></span>
* <span data-ttu-id="c0055-238">Этот командлет:</span><span class="sxs-lookup"><span data-stu-id="c0055-238">This cmdlet:</span></span>
  * <span data-ttu-id="c0055-239">Hello обновления с именем toohello версии приложения hello SDK недавно загрузить toothis машины.</span><span class="sxs-lookup"><span data-stu-id="c0055-239">Upgrades hello named app toohello version of hello SDK most recently downloaded toothis machine.</span></span> <span data-ttu-id="c0055-240">(работает, только если `SdkState==EnabledAfterDeployment`).</span><span class="sxs-lookup"><span data-stu-id="c0055-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="c0055-241">При указании ключа инструментирования с именем приложения hello — перенастроен toosend телеметрии toohello ресурс с этим ключом.</span><span class="sxs-lookup"><span data-stu-id="c0055-241">If you provide an instrumentation key, hello named app is reconfigured toosend telemetry toohello resource with that key.</span></span> <span data-ttu-id="c0055-242">(работает, если `SdkState != Disabled`).</span><span class="sxs-lookup"><span data-stu-id="c0055-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="c0055-243">Загружает hello последнего пакета SDK Application Insights toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="c0055-243">Downloads hello latest Application Insights SDK toohello server.</span></span>

## <span data-ttu-id="c0055-244"><a name="questions"></a>Вопросы о мониторе состояния</span><span class="sxs-lookup"><span data-stu-id="c0055-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="c0055-245">Что такое монитор состояния?</span><span class="sxs-lookup"><span data-stu-id="c0055-245">What is Status Monitor?</span></span>

<span data-ttu-id="c0055-246">Классическое приложение, установленное на веб-сервер IIS.</span><span class="sxs-lookup"><span data-stu-id="c0055-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="c0055-247">Оно позволяет инструментировать и настраивать веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c0055-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="c0055-248">В каких случаях нужно использовать монитор состояния?</span><span class="sxs-lookup"><span data-stu-id="c0055-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="c0055-249">tooinstrument любого веб-приложения, запущенного на сервере IIS -, даже если она уже запущена.</span><span class="sxs-lookup"><span data-stu-id="c0055-249">tooinstrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="c0055-250">tooenable дополнительные данные телеметрии для веб-приложений, которые были [созданного с помощью пакета SDK Application Insights hello](app-insights-asp-net.md) во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="c0055-250">tooenable additional telemetry for web apps that have been [built with hello Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="c0055-251">Можно ли его закрыть после выполнения?</span><span class="sxs-lookup"><span data-stu-id="c0055-251">Can I close it after it runs?</span></span>

<span data-ttu-id="c0055-252">Да.</span><span class="sxs-lookup"><span data-stu-id="c0055-252">Yes.</span></span> <span data-ttu-id="c0055-253">После его инструментирования hello веб-сайтов, при выборе, ее можно закрыть.</span><span class="sxs-lookup"><span data-stu-id="c0055-253">After it has instrumented hello websites you select, you can close it.</span></span>

<span data-ttu-id="c0055-254">Монитор состояния не собирает данные телеметрии самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="c0055-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="c0055-255">Просто настраивает веб-приложения hello и задает некоторые разрешения.</span><span class="sxs-lookup"><span data-stu-id="c0055-255">It just configures hello web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="c0055-256">Как работает монитор состояния?</span><span class="sxs-lookup"><span data-stu-id="c0055-256">What does Status Monitor do?</span></span>

<span data-ttu-id="c0055-257">При выборе веб-приложения для tooinstrument монитор состояния:</span><span class="sxs-lookup"><span data-stu-id="c0055-257">When you select a web app for Status Monitor tooinstrument:</span></span>

* <span data-ttu-id="c0055-258">Загружает и помещает сборки hello Application Insights и config-файл в папку с двоичными файлами веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c0055-258">Downloads and places hello Application Insights assemblies and .config file in hello web app's binaries folder.</span></span>
* <span data-ttu-id="c0055-259">Изменяет `web.config` tooadd hello приложения аналитики отслеживания модуль HTTP.</span><span class="sxs-lookup"><span data-stu-id="c0055-259">Modifies `web.config` tooadd hello Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="c0055-260">Включает вызовы зависимостей toocollect профилирования среды CLR.</span><span class="sxs-lookup"><span data-stu-id="c0055-260">Enables CLR profiling toocollect dependency calls.</span></span>

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a><span data-ttu-id="c0055-261">Зачем мне toorun монитор состояния при каждом обновлении приложение hello?</span><span class="sxs-lookup"><span data-stu-id="c0055-261">Do I need toorun Status Monitor whenever I update hello app?</span></span>

<span data-ttu-id="c0055-262">Нет, если повторное развертывание выполняется поэтапно.</span><span class="sxs-lookup"><span data-stu-id="c0055-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="c0055-263">При выборе параметра «Удалить существующие файлы» hello в hello процесса публикации, необходимо выполнить toore монитор состояния tooconfigure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c0055-263">If you select hello 'delete existing files' option in hello publish process, you would need toore-run Status Monitor tooconfigure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="c0055-264">Какие данные телеметрии собираются?</span><span class="sxs-lookup"><span data-stu-id="c0055-264">What telemetry is collected?</span></span>

<span data-ttu-id="c0055-265">Для приложений, инструментированных во время выполнения с использованием монитора состояния:</span><span class="sxs-lookup"><span data-stu-id="c0055-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="c0055-266">HTTP-запросы;</span><span class="sxs-lookup"><span data-stu-id="c0055-266">HTTP requests</span></span>
* <span data-ttu-id="c0055-267">Вызывает toodependencies</span><span class="sxs-lookup"><span data-stu-id="c0055-267">Calls toodependencies</span></span>
* <span data-ttu-id="c0055-268">Исключения</span><span class="sxs-lookup"><span data-stu-id="c0055-268">Exceptions</span></span>
* <span data-ttu-id="c0055-269">Счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="c0055-269">Performance counters</span></span>

<span data-ttu-id="c0055-270">Для уже инструментированных приложений во время компиляции:</span><span class="sxs-lookup"><span data-stu-id="c0055-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="c0055-271">счетчики процессов;</span><span class="sxs-lookup"><span data-stu-id="c0055-271">Process counters.</span></span>
 * <span data-ttu-id="c0055-272">вызовы зависимостей (.NET 4.5) и возвращаемые значения в вызовах зависимостей (.NET 4.6);</span><span class="sxs-lookup"><span data-stu-id="c0055-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="c0055-273">значения трассировки стека исключений.</span><span class="sxs-lookup"><span data-stu-id="c0055-273">Exception stack trace values.</span></span>

[<span data-ttu-id="c0055-274">Подробнее</span><span class="sxs-lookup"><span data-stu-id="c0055-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="c0055-275">Видео</span><span class="sxs-lookup"><span data-stu-id="c0055-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="c0055-276"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0055-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="c0055-277">Просмотр телеметрии:</span><span class="sxs-lookup"><span data-stu-id="c0055-277">View your telemetry:</span></span>

* <span data-ttu-id="c0055-278">[Просмотр метрик](app-insights-metrics-explorer.md) toomonitor производительности и использовании</span><span class="sxs-lookup"><span data-stu-id="c0055-278">[Explore metrics](app-insights-metrics-explorer.md) toomonitor performance and usage</span></span>
* <span data-ttu-id="c0055-279">[Поиск событий и журналов] [ diagnostic] toodiagnose проблемы</span><span class="sxs-lookup"><span data-stu-id="c0055-279">[Search events and logs][diagnostic] toodiagnose problems</span></span>
* <span data-ttu-id="c0055-280">[Аналитика](app-insights-analytics.md) для создания расширенных запросов.</span><span class="sxs-lookup"><span data-stu-id="c0055-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="c0055-281">Создайте панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="c0055-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="c0055-282">Добавление данных телеметрии:</span><span class="sxs-lookup"><span data-stu-id="c0055-282">Add more telemetry:</span></span>

* <span data-ttu-id="c0055-283">[Создание веб-тестов] [ availability] toomake убедиться, что веб-узла остается в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="c0055-283">[Create web tests][availability] toomake sure your site stays live.</span></span>
* <span data-ttu-id="c0055-284">[Добавить клиента телеметрии веб] [ usage] toosee исключения из кода веб-страниц и вставке toolet Трассировка вызовов.</span><span class="sxs-lookup"><span data-stu-id="c0055-284">[Add web client telemetry][usage] toosee exceptions from web page code and toolet you insert trace calls.</span></span>
* <span data-ttu-id="c0055-285">[Добавьте код, пакет SDK Application Insights tooyour] [ greenbrown] , чтобы можно было вставить трассировки и записывать вызовы</span><span class="sxs-lookup"><span data-stu-id="c0055-285">[Add Application Insights SDK tooyour code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
