---
title: "Интеграция SCOM с Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: 9c205465981fabdbb696cdc44f765532bbb992b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="a7573-104">Мониторинг производительности приложений с помощью Application Insights для SCOM</span><span class="sxs-lookup"><span data-stu-id="a7573-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="a7573-105">Если для управления серверами вы используете System Center Operations Manager (SCOM), мониторинг производительности и диагностику проблем можно выполнять с помощью [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="a7573-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="a7573-106">Application Insights отслеживает входящие запросы вашего веб-приложения, исходящие вызовы REST и SQL, а также исключения и трассировку журналов.</span><span class="sxs-lookup"><span data-stu-id="a7573-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="a7573-107">Вы можете использовать панели мониторинга с диаграммами метрик и смарт-оповещениями, а также мощные средства диагностического поиска и аналитических запросов для работы с данными телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a7573-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="a7573-108">Мониторинг Application Insights можно включить с помощью пакета управления SCOM.</span><span class="sxs-lookup"><span data-stu-id="a7573-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a7573-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a7573-109">Before you start</span></span>
<span data-ttu-id="a7573-110">Предполагается следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="a7573-110">We assume:</span></span>

* <span data-ttu-id="a7573-111">Вы уже знакомы с SCOM и используете SCOM 2012 R2 или 2016 для управления веб-серверами IIS.</span><span class="sxs-lookup"><span data-stu-id="a7573-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span></span>
* <span data-ttu-id="a7573-112">Вы уже установили на серверах веб-приложение, которое будет отслеживаться средствами Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a7573-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span></span>
* <span data-ttu-id="a7573-113">Используется платформа .NET версии 4.5 и выше.</span><span class="sxs-lookup"><span data-stu-id="a7573-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="a7573-114">У вас есть подписка [Microsoft Azure](https://azure.com) и доступ к [порталу Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a7573-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a7573-115">Если у вашей организации есть такая подписка, вы можете добавить к ней свою учетную запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="a7573-115">Your organization may have a subscription, and can add your Microsoft account to it.</span></span>

<span data-ttu-id="a7573-116">(Команда разработчиков может встроить в веб-приложение [пакет SDK Application Insights](app-insights-asp-net.md) .</span><span class="sxs-lookup"><span data-stu-id="a7573-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span></span> <span data-ttu-id="a7573-117">Этот инструментарий, подключаемый во время сборки, делает процесс написания пользовательской телеметрии более гибким.</span><span class="sxs-lookup"><span data-stu-id="a7573-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="a7573-118">Но это необязательно: описанные здесь действия можно выполнять как с установленным пакетом SDK, так и без него.)</span><span class="sxs-lookup"><span data-stu-id="a7573-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="a7573-119">(Однократно) Установка пакета управления Application Insights</span><span class="sxs-lookup"><span data-stu-id="a7573-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="a7573-120">Выполните эти действия на компьютере, на котором выполняется Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="a7573-120">On the machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="a7573-121">Удалите все старые версии пакета управления.</span><span class="sxs-lookup"><span data-stu-id="a7573-121">Uninstall any old version of the management pack:</span></span>
   1. <span data-ttu-id="a7573-122">В Operations Manager откройте меню "Администрирование", щелкните "Пакеты управления".</span><span class="sxs-lookup"><span data-stu-id="a7573-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="a7573-123">Затем удалите старую версию.</span><span class="sxs-lookup"><span data-stu-id="a7573-123">Delete the old version.</span></span>
2. <span data-ttu-id="a7573-124">Загрузите из каталога и установите пакет управления.</span><span class="sxs-lookup"><span data-stu-id="a7573-124">Download and install the management pack from the catalog.</span></span>
3. <span data-ttu-id="a7573-125">Перезапустите Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="a7573-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="a7573-126">Создание пакета управления</span><span class="sxs-lookup"><span data-stu-id="a7573-126">Create a management pack</span></span>
1. <span data-ttu-id="a7573-127">В Operations Manager откройте **Разработка**, **.NET...with Application Insights** (.NET... с Application Insights), **Мастер добавления объекта мониторинга**, а затем снова выберите **.NET...with Application Insights** (.NET... с Application Insights).</span><span class="sxs-lookup"><span data-stu-id="a7573-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="a7573-128">Присвойте конфигурации имя, соответствующее вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="a7573-128">Name the configuration after your app.</span></span> <span data-ttu-id="a7573-129">(Инструментарий добавляется отдельно для каждого приложения.)</span><span class="sxs-lookup"><span data-stu-id="a7573-129">(You have to instrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="a7573-130">На той же странице мастера создайте новый пакет управления или выберите пакет, созданный ранее для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a7573-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="a7573-131">( [Пакет управления](https://technet.microsoft.com/library/cc974491.aspx) Application Insights — это шаблон, на основе которого можно создать экземпляр.</span><span class="sxs-lookup"><span data-stu-id="a7573-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="a7573-132">Этот экземпляр затем можно использовать повторно.)</span><span class="sxs-lookup"><span data-stu-id="a7573-132">You can reuse the same instance later.)</span></span>

    ![На вкладке "Общие свойства" введите имя приложения.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="a7573-136">Выберите одно приложение, которое будет отслеживаться.</span><span class="sxs-lookup"><span data-stu-id="a7573-136">Choose one app that you want to monitor.</span></span> <span data-ttu-id="a7573-137">Функция поиска помогает найти нужное приложение среди установленных на ваших серверах.</span><span class="sxs-lookup"><span data-stu-id="a7573-137">The search feature searches among apps installed on your servers.</span></span>
   
    ![На вкладке "What to Monitor" (Что отслеживать) нажмите кнопку "Добавить", затем введите часть имени приложения, нажмите "Поиск", выберите нужное приложение и нажмите "Добавить", а затем щелкните "ОК".](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="a7573-139">Необязательное поле "Область мониторинга" позволяет указать подмножество серверов, если вы хотите отслеживать приложение не на всех серверах.</span><span class="sxs-lookup"><span data-stu-id="a7573-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span></span>
2. <span data-ttu-id="a7573-140">На следующей странице мастера введите учетные данные для входа в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a7573-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span></span>
   
    <span data-ttu-id="a7573-141">На этой странице выберите ресурс Application Insights, на котором будут анализироваться и отображаться данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a7573-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="a7573-142">Если при разработке приложение было настроено для использования с Application Insights, выберите существующий ресурс.</span><span class="sxs-lookup"><span data-stu-id="a7573-142">If the application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="a7573-143">В противном случае создайте ресурс с именем приложения.</span><span class="sxs-lookup"><span data-stu-id="a7573-143">Otherwise, create a new resource named for the app.</span></span> <span data-ttu-id="a7573-144">Если система состоит из нескольких приложений, поместите эти приложения в одну группу ресурсов, чтобы вам было удобнее управлять доступом к телеметрии.</span><span class="sxs-lookup"><span data-stu-id="a7573-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span></span>
     
     <span data-ttu-id="a7573-145">Эти параметры можно изменить позже.</span><span class="sxs-lookup"><span data-stu-id="a7573-145">You can change these settings later.</span></span>
     
     ![На вкладке параметров Application Insights нажмите кнопку "Войти" и укажите учетные данные учетной записи Майкрософт для Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="a7573-148">Завершите работу мастера.</span><span class="sxs-lookup"><span data-stu-id="a7573-148">Complete the wizard.</span></span>
   
    ![Нажмите кнопку "Создать"](./media/app-insights-scom/070.png)

<span data-ttu-id="a7573-150">Повторите эту процедуру для каждого приложения, которое нужно отслеживать.</span><span class="sxs-lookup"><span data-stu-id="a7573-150">Repeat this procedure for each app that you want to monitor.</span></span>

<span data-ttu-id="a7573-151">Если позже вы захотите изменить эти параметры, снова откройте окно свойств монитора из окна "Разработка".</span><span class="sxs-lookup"><span data-stu-id="a7573-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span></span>

![В разделе "Создание" выберите ".NET Application Performance Monitoring with Application Insights" (Мониторинг производительности приложений .NET с помощью Application Insights), укажите монитор и щелкните "Свойства".](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="a7573-153">Проверка мониторинга</span><span class="sxs-lookup"><span data-stu-id="a7573-153">Verify monitoring</span></span>
<span data-ttu-id="a7573-154">Установленный монитор будет искать нужное приложение на всех серверах.</span><span class="sxs-lookup"><span data-stu-id="a7573-154">The monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="a7573-155">Найдя приложение, он настроит монитор состояний Application Insights для отслеживания приложения.</span><span class="sxs-lookup"><span data-stu-id="a7573-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span></span> <span data-ttu-id="a7573-156">При необходимости монитор состояния сначала будет установлен на сервере.</span><span class="sxs-lookup"><span data-stu-id="a7573-156">If necessary, it first installs Status Monitor on the server.</span></span>

<span data-ttu-id="a7573-157">Вы можете проверить, какие экземпляры приложения были найдены:</span><span class="sxs-lookup"><span data-stu-id="a7573-157">You can verify which instances of the app it has found:</span></span>

![В разделе "Мониторинг" откройте Application Insights.](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="a7573-159">Просмотр данных телеметрии в Application Insights</span><span class="sxs-lookup"><span data-stu-id="a7573-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="a7573-160">На [портале Azure](https://portal.azure.com)перейдите к ресурсу для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a7573-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span></span> <span data-ttu-id="a7573-161">Вы увидите [диаграммы телеметрии](app-insights-dashboards.md) для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="a7573-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="a7573-162">(Если они еще не отображаются на главной странице, щелкните "Live Metrics Stream" (Динамический поток метрик).)</span><span class="sxs-lookup"><span data-stu-id="a7573-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7573-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7573-163">Next steps</span></span>
* <span data-ttu-id="a7573-164">[Настройка панели мониторинга](app-insights-dashboards.md) для объединения важнейших диаграмм мониторинга этого и других приложений.</span><span class="sxs-lookup"><span data-stu-id="a7573-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="a7573-165">Дополнительная информация о метриках</span><span class="sxs-lookup"><span data-stu-id="a7573-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="a7573-166">Настройка оповещений</span><span class="sxs-lookup"><span data-stu-id="a7573-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="a7573-167">Диагностика проблем с производительностью</span><span class="sxs-lookup"><span data-stu-id="a7573-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="a7573-168">Мощные аналитические запросы</span><span class="sxs-lookup"><span data-stu-id="a7573-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="a7573-169">Доступность веб-тестов</span><span class="sxs-lookup"><span data-stu-id="a7573-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

