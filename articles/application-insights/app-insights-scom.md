---
title: "aaaSCOM интеграция с Application Insights | Документы Microsoft"
description: "Если вы используете SCOM, примените Application Insights для мониторинга производительности и диагностики. Подробные панели мониторинга, смарт-оповещения, мощные средства диагностики и аналитические запросы."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="5cd5b-104">Мониторинг производительности приложений с помощью Application Insights для SCOM</span><span class="sxs-lookup"><span data-stu-id="5cd5b-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="5cd5b-105">При использовании серверов toomanage System Center Operations Manager (SCOM) можно отслеживать производительности и диагностики проблем с производительностью с помощью hello [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="5cd5b-105">If you use System Center Operations Manager (SCOM) toomanage your servers, you can monitor performance and diagnose performance issues with hello help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="5cd5b-106">Application Insights отслеживает входящие запросы вашего веб-приложения, исходящие вызовы REST и SQL, а также исключения и трассировку журналов.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="5cd5b-107">Вы можете использовать панели мониторинга с диаграммами метрик и смарт-оповещениями, а также мощные средства диагностического поиска и аналитических запросов для работы с данными телеметрии.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="5cd5b-108">Мониторинг Application Insights можно включить с помощью пакета управления SCOM.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5cd5b-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="5cd5b-109">Before you start</span></span>
<span data-ttu-id="5cd5b-110">Предполагается следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="5cd5b-110">We assume:</span></span>

* <span data-ttu-id="5cd5b-111">Веб-серверы, вы уже знакомы с SCOM и использовать SCOM 2012 R2 или 2016 toomanage служб IIS.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 toomanage your IIS web servers.</span></span>
* <span data-ttu-id="5cd5b-112">Уже установки на серверах веб-приложения, которые должны toomonitor с помощью Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-112">You have already installed on your servers a web application that you want toomonitor with Application Insights.</span></span>
* <span data-ttu-id="5cd5b-113">Используется платформа .NET версии 4.5 и выше.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="5cd5b-114">У вас есть подписка tooa доступ [Microsoft Azure](https://azure.com) и может подписывать в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5cd5b-114">You have access tooa subscription in [Microsoft Azure](https://azure.com) and can sign in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5cd5b-115">Организации могут иметь подписку, а также добавлять вашей tooit учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-115">Your organization may have a subscription, and can add your Microsoft account tooit.</span></span>

<span data-ttu-id="5cd5b-116">(команда разработчиков hello может построить hello [пакет SDK Application Insights](app-insights-asp-net.md) в веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-116">(hello development team might build hello [Application Insights SDK](app-insights-asp-net.md) into hello web app.</span></span> <span data-ttu-id="5cd5b-117">Этот инструментарий, подключаемый во время сборки, делает процесс написания пользовательской телеметрии более гибким.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="5cd5b-118">Тем не менее, не имеет значения: можно использовать hello действия, описанные здесь, с указанием или без hello встроенные SDK.)</span><span class="sxs-lookup"><span data-stu-id="5cd5b-118">However, it doesn't matter: you can follow hello steps described here either with or without hello SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="5cd5b-119">(Однократно) Установка пакета управления Application Insights</span><span class="sxs-lookup"><span data-stu-id="5cd5b-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="5cd5b-120">На компьютере, где запускается Operations Manager для hello:</span><span class="sxs-lookup"><span data-stu-id="5cd5b-120">On hello machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="5cd5b-121">Удалите все старые версии пакета управления hello:</span><span class="sxs-lookup"><span data-stu-id="5cd5b-121">Uninstall any old version of hello management pack:</span></span>
   1. <span data-ttu-id="5cd5b-122">В Operations Manager откройте меню "Администрирование", щелкните "Пакеты управления".</span><span class="sxs-lookup"><span data-stu-id="5cd5b-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="5cd5b-123">Удалите старую версию hello.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-123">Delete hello old version.</span></span>
2. <span data-ttu-id="5cd5b-124">Загрузите и установите пакет управления hello из каталога hello.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-124">Download and install hello management pack from hello catalog.</span></span>
3. <span data-ttu-id="5cd5b-125">Перезапустите Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="5cd5b-126">Создание пакета управления</span><span class="sxs-lookup"><span data-stu-id="5cd5b-126">Create a management pack</span></span>
1. <span data-ttu-id="5cd5b-127">В Operations Manager откройте **Разработка**, **.NET...with Application Insights** (.NET... с Application Insights), **Мастер добавления объекта мониторинга**, а затем снова выберите **.NET...with Application Insights** (.NET... с Application Insights).</span><span class="sxs-lookup"><span data-stu-id="5cd5b-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="5cd5b-128">Имя конфигурации hello после приложения.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-128">Name hello configuration after your app.</span></span> <span data-ttu-id="5cd5b-129">(Имеется tooinstrument одно приложение за раз.)</span><span class="sxs-lookup"><span data-stu-id="5cd5b-129">(You have tooinstrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="5cd5b-130">Hello же на странице мастера, либо создать новый управления пакет, или выберите пакет, созданный для Application Insights, более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-130">On hello same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="5cd5b-131">(hello Application Insights [пакет управления](https://technet.microsoft.com/library/cc974491.aspx) — это шаблон, из которого можно создать экземпляр.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-131">(hello Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="5cd5b-132">Можно повторно использовать hello же экземпляр более поздней версии.)</span><span class="sxs-lookup"><span data-stu-id="5cd5b-132">You can reuse hello same instance later.)</span></span>

    ![В hello вкладка «Общие свойства» введите имя hello приложение hello.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="5cd5b-136">Выберите одно приложение, которые должны toomonitor.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-136">Choose one app that you want toomonitor.</span></span> <span data-ttu-id="5cd5b-137">Функция поиска Hello поиск среди приложений, установленных на серверах.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-137">hello search feature searches among apps installed on your servers.</span></span>
   
    ![Какие вкладки tooMonitor нажмите кнопку Добавить, введите часть имени приложения hello, нажмите кнопку поиска, выберите OK приложение hello, а затем добавить.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="5cd5b-139">Hello необязательный мониторинг поле «область» может быть используется toospecify подмножество серверов, если не нужно, чтобы приложение hello toomonitor на всех серверах.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-139">hello optional Monitoring scope field can be used toospecify a subset of your servers, if you don't want toomonitor hello app in all servers.</span></span>
2. <span data-ttu-id="5cd5b-140">На следующей странице мастера hello прежде всего необходимо указать вашей toosign учетные данные в tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-140">On hello next wizard page, you must first provide your credentials toosign in tooMicrosoft Azure.</span></span>
   
    <span data-ttu-id="5cd5b-141">На этой странице выберите ресурс Application Insights hello место hello toobe данных телеметрии анализируются и отображаются.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-141">On this page, you choose hello Application Insights resource where you want hello telemetry data toobe analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="5cd5b-142">Hello приложение настроено для Application Insights во время разработки, выберите его в существующий ресурс.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-142">If hello application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="5cd5b-143">В противном случае создайте новый ресурс с именем для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-143">Otherwise, create a new resource named for hello app.</span></span> <span data-ttu-id="5cd5b-144">Если имеются другие приложения, которые являются компонентами для hello одной системе, поместите их в hello одну группу ресурсов, проще toomanage телеметрии toohello toomake доступа.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-144">If there are other apps that are components of hello same system, put them in hello same resource group, toomake access toohello telemetry easier toomanage.</span></span>
     
     <span data-ttu-id="5cd5b-145">Эти параметры можно изменить позже.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-145">You can change these settings later.</span></span>
     
     ![На вкладке параметров Application Insights нажмите кнопку "Войти" и укажите учетные данные учетной записи Майкрософт для Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="5cd5b-148">Мастер завершения hello.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-148">Complete hello wizard.</span></span>
   
    ![Нажмите кнопку "Создать"](./media/app-insights-scom/070.png)

<span data-ttu-id="5cd5b-150">Повторите эту процедуру для каждого приложения, которое следует toomonitor.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-150">Repeat this procedure for each app that you want toomonitor.</span></span>

<span data-ttu-id="5cd5b-151">Если требуется toochange параметры позже, снова откройте hello свойства монитора hello из окна "Создание и настройка hello".</span><span class="sxs-lookup"><span data-stu-id="5cd5b-151">If you need toochange settings later, re-open hello properties of hello monitor from hello Authoring window.</span></span>

![В разделе "Создание" выберите ".NET Application Performance Monitoring with Application Insights" (Мониторинг производительности приложений .NET с помощью Application Insights), укажите монитор и щелкните "Свойства".](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="5cd5b-153">Проверка мониторинга</span><span class="sxs-lookup"><span data-stu-id="5cd5b-153">Verify monitoring</span></span>
<span data-ttu-id="5cd5b-154">монитор Hello, что вы установили ищет приложения на каждом сервере.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-154">hello monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="5cd5b-155">Где находит приложение hello, настраивает приложение hello toomonitor монитор состояния Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-155">Where it finds hello app, it configures Application Insights Status Monitor toomonitor hello app.</span></span> <span data-ttu-id="5cd5b-156">При необходимости сначала устанавливает монитор состояния на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-156">If necessary, it first installs Status Monitor on hello server.</span></span>

<span data-ttu-id="5cd5b-157">Можно проверить, какие экземпляры приложение hello нахождения.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-157">You can verify which instances of hello app it has found:</span></span>

![В разделе "Мониторинг" откройте Application Insights.](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="5cd5b-159">Просмотр данных телеметрии в Application Insights</span><span class="sxs-lookup"><span data-stu-id="5cd5b-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="5cd5b-160">В hello [портал Azure](https://portal.azure.com), Обзор ресурсов toohello для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-160">In hello [Azure portal](https://portal.azure.com), browse toohello resource for your app.</span></span> <span data-ttu-id="5cd5b-161">Вы увидите [диаграммы телеметрии](app-insights-dashboards.md) для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="5cd5b-162">(Если он еще не отображаются на главной странице hello еще, щелкните обновляющегося потока метрики).</span><span class="sxs-lookup"><span data-stu-id="5cd5b-162">(If it hasn't shown up on hello main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cd5b-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5cd5b-163">Next steps</span></span>
* <span data-ttu-id="5cd5b-164">[Настройка панели мониторинга](app-insights-dashboards.md) toobring вместе hello наиболее важных диаграмм мониторинг это и другие приложения.</span><span class="sxs-lookup"><span data-stu-id="5cd5b-164">[Set up a dashboard](app-insights-dashboards.md) toobring together hello most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="5cd5b-165">Дополнительная информация о метриках</span><span class="sxs-lookup"><span data-stu-id="5cd5b-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="5cd5b-166">Настройка оповещений</span><span class="sxs-lookup"><span data-stu-id="5cd5b-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="5cd5b-167">Диагностика проблем с производительностью</span><span class="sxs-lookup"><span data-stu-id="5cd5b-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="5cd5b-168">Мощные аналитические запросы</span><span class="sxs-lookup"><span data-stu-id="5cd5b-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="5cd5b-169">Доступность веб-тестов</span><span class="sxs-lookup"><span data-stu-id="5cd5b-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

