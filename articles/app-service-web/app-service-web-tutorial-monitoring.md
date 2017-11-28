---
title: "веб-приложения aaaMonitor | Документы Microsoft"
description: "Узнайте, как tooset копирование мониторинг на веб-приложения"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="6df3e-103">Мониторинг службы приложений</span><span class="sxs-lookup"><span data-stu-id="6df3e-103">Monitor App Service</span></span>
<span data-ttu-id="6df3e-104">В этом учебнике рассматриваются путем отслеживания приложения и с помощью hello встроенных средств toosolve проблем платформы, при их возникновении.</span><span class="sxs-lookup"><span data-stu-id="6df3e-104">This tutorial walks you through monitoring your app and using hello built-in platform tools toosolve problems when they occur.</span></span>

<span data-ttu-id="6df3e-105">Каждый раздел этого документа посвящен определенной функции.</span><span class="sxs-lookup"><span data-stu-id="6df3e-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="6df3e-106">Совместное использование функций hello позволяют:</span><span class="sxs-lookup"><span data-stu-id="6df3e-106">Using hello features together let you:</span></span>
- <span data-ttu-id="6df3e-107">выявить проблему в приложении;</span><span class="sxs-lookup"><span data-stu-id="6df3e-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="6df3e-108">Определение, когда hello проблема вызвана вашего кода или hello платформы.</span><span class="sxs-lookup"><span data-stu-id="6df3e-108">Determining when hello issue is caused by your code or hello platform.</span></span>
- <span data-ttu-id="6df3e-109">Отфильтровать hello источник hello проблемы в коде.</span><span class="sxs-lookup"><span data-stu-id="6df3e-109">Narrow down hello source of hello problem in your code.</span></span>
- <span data-ttu-id="6df3e-110">Отладка и исправление проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-110">Debugging and fixing hello issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6df3e-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="6df3e-111">Before you begin</span></span>
- <span data-ttu-id="6df3e-112">Требуется toomonitor веб-приложение и выполните hello описанные действия.</span><span class="sxs-lookup"><span data-stu-id="6df3e-112">You need a Web App toomonitor and follow hello outlined steps.</span></span>
    - <span data-ttu-id="6df3e-113">Можно создать приложение hello действий, описанных в hello [создания приложения ASP.NET в Azure с базой данных SQL](app-service-web-tutorial-dotnet-sqldatabase.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="6df3e-113">You can create an application following hello steps described in hello [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="6df3e-114">Если требуется tootry out **удаленной отладки** приложения, требуется Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6df3e-114">If you want tootry out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="6df3e-115">Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello свободного [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6df3e-115">If you don’t already have Visual Studio 2017 installed, you can download and use hello free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="6df3e-116">Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-116">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

## <span data-ttu-id="6df3e-117"><a name="metrics"></a>Шаг 1. Просмотр метрик</span><span class="sxs-lookup"><span data-stu-id="6df3e-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="6df3e-118">**Метрики** являются полезным toounderstand:</span><span class="sxs-lookup"><span data-stu-id="6df3e-118">**Metrics** are useful toounderstand:</span></span>
- <span data-ttu-id="6df3e-119">Работоспособность приложения</span><span class="sxs-lookup"><span data-stu-id="6df3e-119">Application health</span></span>
- <span data-ttu-id="6df3e-120">Производительность приложения</span><span class="sxs-lookup"><span data-stu-id="6df3e-120">App performance</span></span>
- <span data-ttu-id="6df3e-121">Потребление ресурсов</span><span class="sxs-lookup"><span data-stu-id="6df3e-121">Resource consumption</span></span>

<span data-ttu-id="6df3e-122">При исследовании проблемы приложения, просмотрев метрики является toostart лучше всего.</span><span class="sxs-lookup"><span data-stu-id="6df3e-122">When investigating an application issue, reviewing metrics is a good place toostart.</span></span> <span data-ttu-id="6df3e-123">Портал Azure имеет toovisually быстрый способ проверить приложения с использованием метрик hello **монитора Azure**.</span><span class="sxs-lookup"><span data-stu-id="6df3e-123">Azure portal has a quick way toovisually inspect hello metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="6df3e-124">Метрики обеспечивают историческое представление по нескольким ключевым агрегатам для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="6df3e-125">Для любого приложения, размещенного в службе приложений необходимо отслеживать hello веб-приложения и hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="6df3e-125">For any app hosted in app service, you should monitor both hello Web App and hello App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="6df3e-126">План службы приложений представляет коллекцию hello toohost физические ресурсы, используемые приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-126">An App Service plan represents hello collection of physical resources used toohost your apps.</span></span> <span data-ttu-id="6df3e-127">Все приложения назначенные tooan службы приложений плана общего ресурса hello ресурсы определяемое позволяя toosave затрат при размещении нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="6df3e-127">All applications assigned tooan App Service plan share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="6df3e-128">Планы службы приложений определяют такие компоненты:</span><span class="sxs-lookup"><span data-stu-id="6df3e-128">App Service plans define:</span></span>
> * <span data-ttu-id="6df3e-129">Регион: Северная Европа, восточная часть США, Юго-Восточная Азия и т. д.</span><span class="sxs-lookup"><span data-stu-id="6df3e-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="6df3e-130">Размер экземпляра: небольшой, средний, крупный и т. д.</span><span class="sxs-lookup"><span data-stu-id="6df3e-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="6df3e-131">Число масштабируемых элементов: один, два, три экземпляра и т. д.</span><span class="sxs-lookup"><span data-stu-id="6df3e-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="6df3e-132">SKU: "Бесплатный", "Общий", "Базовый", "Стандартный", "Премиум" и т. д.</span><span class="sxs-lookup"><span data-stu-id="6df3e-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="6df3e-133">tooreview метрики для веб-приложения, перейдите toohello **Обзор** колонке приложение hello нужно toomonitor.</span><span class="sxs-lookup"><span data-stu-id="6df3e-133">tooreview metrics for your Web App, go toohello **Overview** blade of hello app you want toomonitor.</span></span> <span data-ttu-id="6df3e-134">Здесь можно просмотреть диаграмму для метрик приложения в **элементе "Мониторинг"**.</span><span class="sxs-lookup"><span data-stu-id="6df3e-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="6df3e-135">Щелкните плитку tooedit hello и настроить какие tooview метрик и hello toodisplay диапазона времени.</span><span class="sxs-lookup"><span data-stu-id="6df3e-135">Click hello tile tooedit and configure what metrics tooview and hello time range toodisplay.</span></span>

<span data-ttu-id="6df3e-136">По колонки ресурсов по умолчанию hello предоставляет представления для hello запросы приложений и ошибок для hello последний час.</span><span class="sxs-lookup"><span data-stu-id="6df3e-136">By default hello resource blade provides a view for hello Application Requests and errors for hello last hour.</span></span>
<span data-ttu-id="6df3e-137">![Мониторинг приложения](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="6df3e-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="6df3e-138">Как видно в примере hello, у нас есть приложение, которое создает многие **ошибки HTTP сервера**.</span><span class="sxs-lookup"><span data-stu-id="6df3e-138">As you can see in hello example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="6df3e-139">Hello большого количества ошибок — hello первое Указание, что нам нужна tooinvestigate этого приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-139">hello high volume of errors is hello first indication we need tooinvestigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="6df3e-140">Дополнительные сведения о мониторе Azure с hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="6df3e-140">Learn more about Azure Monitor with hello following links:</span></span>
> - [<span data-ttu-id="6df3e-141">Приступая к работе с Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="6df3e-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="6df3e-142">Метрики Azure</span><span class="sxs-lookup"><span data-stu-id="6df3e-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="6df3e-143">Метрики, поддерживаемые Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="6df3e-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="6df3e-144">Панели мониторинга Azure</span><span class="sxs-lookup"><span data-stu-id="6df3e-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="6df3e-145"><a name="alerts"></a> Шаг 2. Настройка оповещений</span><span class="sxs-lookup"><span data-stu-id="6df3e-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="6df3e-146">**Оповещения** может быть tootrigger, настроенный на определенных условий для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-146">**Alerts** can be configured tootrigger on specific conditions for your app.</span></span>

<span data-ttu-id="6df3e-147">В [шаг 1 - Просмотр метрик](#metrics), мы узнали, что приложение hello имеет большое количество ошибок.</span><span class="sxs-lookup"><span data-stu-id="6df3e-147">In [Step 1 - View metrics](#metrics), we saw that hello application had a high number of errors.</span></span>

<span data-ttu-id="6df3e-148">Позволяет настроить оповещение tooautomatically получение уведомлений при возникновении ошибок.</span><span class="sxs-lookup"><span data-stu-id="6df3e-148">Lets configure an alert tooautomatically get notified when errors occur.</span></span> <span data-ttu-id="6df3e-149">В этом случае мы должны предупреждения toosend hello и электронной почты каждый раз hello количество ошибок HTTP 50 X превышает определенный порог.</span><span class="sxs-lookup"><span data-stu-id="6df3e-149">In this case, we want hello alert toosend and e-mail every time hello number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="6df3e-150">toocreate оповещения, перейдите в слишком**мониторинг** > **оповещения** и нажмите кнопку **[+] добавить оповещение**.</span><span class="sxs-lookup"><span data-stu-id="6df3e-150">toocreate an alert, navigate too**Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Оповещения](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="6df3e-152">Укажите значения для конфигурации оповещений hello:</span><span class="sxs-lookup"><span data-stu-id="6df3e-152">Provide values for hello Alert configuration:</span></span>
- <span data-ttu-id="6df3e-153">**Ресурс:** hello toomonitor сайта с предупреждением hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-153">**Resource:** hello site toomonitor with hello alert.</span></span>
- <span data-ttu-id="6df3e-154">**Имя:** имя оповещения, в данном случае это *High HTTP 50X* (Большое число HTTP 50X).</span><span class="sxs-lookup"><span data-stu-id="6df3e-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="6df3e-155">**Описание:** пояснение, что отслеживает это оповещение, в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="6df3e-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="6df3e-156">**Оповещения включены:** оповещения могут отслеживать метрики или события. В этом примере нас интересуют метрики.</span><span class="sxs-lookup"><span data-stu-id="6df3e-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="6df3e-157">**Метрика:** какие метрики toomonitor в данном случае: *ошибки HTTP сервера*.</span><span class="sxs-lookup"><span data-stu-id="6df3e-157">**Metric:** What metric toomonitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="6df3e-158">**Условие:** при tooalert, в данном случае выберите hello *больше* параметр.</span><span class="sxs-lookup"><span data-stu-id="6df3e-158">**Condition:** When tooalert, in this case select hello *greater than* option.</span></span>
- <span data-ttu-id="6df3e-159">**Пороговое значение:** toolook значение, что в этом случае является: *400*.</span><span class="sxs-lookup"><span data-stu-id="6df3e-159">**Threshold:** What is value toolook for, in this case: *400*.</span></span>
- <span data-ttu-id="6df3e-160">**Период:** оповещения оперируют hello среднее значение метрики.</span><span class="sxs-lookup"><span data-stu-id="6df3e-160">**Period:** Alerts operate over hello average value of a metric.</span></span> <span data-ttu-id="6df3e-161">При уменьшении периодов чувствительность оповещений возрастает.</span><span class="sxs-lookup"><span data-stu-id="6df3e-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="6df3e-162">В данном случае мы используем значение *5 минут*.</span><span class="sxs-lookup"><span data-stu-id="6df3e-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="6df3e-163">**Email Owners and contributors** (Участники и владельцы электронной почты): в данном случае установлено значение *Включено*.</span><span class="sxs-lookup"><span data-stu-id="6df3e-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="6df3e-164">Теперь, когда hello предупреждение создается сообщение электронной почты отправляется при каждом hello приложение переходит выше порогового значения настроен hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-164">Now that hello alert is created an email is sent every time hello app goes over hello configured threshold.</span></span> <span data-ttu-id="6df3e-165">Активные предупреждения также могут быть просмотрены hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6df3e-165">Active alerts can also be reviewed in hello Azure portal.</span></span>

![Активированные оповещения](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="6df3e-167">Дополнительные сведения о Azure Alerts с hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="6df3e-167">Learn more about Azure Alerts with hello following links:</span></span>
> - [<span data-ttu-id="6df3e-168">Что такое оповещения в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6df3e-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="6df3e-169">Действия с метриками</span><span class="sxs-lookup"><span data-stu-id="6df3e-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="6df3e-170">Создание оповещений о метриках</span><span class="sxs-lookup"><span data-stu-id="6df3e-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="6df3e-171"><a name="companion"></a> Шаг 3. Дополнительное приложение для службы приложений</span><span class="sxs-lookup"><span data-stu-id="6df3e-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="6df3e-172">**Дополнительное приложение службы** обеспечивает удобный способ toomonitor приложения с собственным взаимодействием в мобильном устройстве (iOS или Android).</span><span class="sxs-lookup"><span data-stu-id="6df3e-172">**App Service companion** offers a convenient way toomonitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="6df3e-173">Вспомогательное приложение для службы приложений Azure позволяет выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6df3e-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="6df3e-174">Просматривать метрики приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-174">Review application metrics</span></span>
- <span data-ttu-id="6df3e-175">Просматривать уведомления для приложения и выполнять необходимые действия, а также получать рекомендации.</span><span class="sxs-lookup"><span data-stu-id="6df3e-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="6df3e-176">Выполните устранение основных неполадок (обзора, запуск, остановка, перезапуск приложения hello)</span><span class="sxs-lookup"><span data-stu-id="6df3e-176">Perform basic troubleshooting (browse, start, stop, restart hello app)</span></span>
- <span data-ttu-id="6df3e-177">Получать push-уведомления о важных событиях.</span><span class="sxs-lookup"><span data-stu-id="6df3e-177">Get push notifications for critical events.</span></span>

![Вспомогательное приложение для службы приложений](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="6df3e-179">[![Вспомогательное приложение для службы приложений в магазине приложений](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Вспомогательное приложение для службы приложений в Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="6df3e-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="6df3e-180">Вы можете установить дополнительное приложение службы из hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) или [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="6df3e-180">You can install App Service companion from hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="6df3e-181"><a name="diagnose"></a> Шаг 4. Диагностика и решение проблем</span><span class="sxs-lookup"><span data-stu-id="6df3e-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="6df3e-182">Пункт **Диагностика и решение проблем** помогает отделить проблемы приложений от проблем платформы.</span><span class="sxs-lookup"><span data-stu-id="6df3e-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="6df3e-183">Он может предложить возможные меры сдерживания tooget задней toohealthy вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-183">It can also suggest possible mitigations tooget your Web App back toohealthy.</span></span>

![Диагностика и решение проблем](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="6df3e-185">Продолжая hello пример формы предыдущих шагах, мы видим, что приложение hello эксклюзивном возникли проблемы с.</span><span class="sxs-lookup"><span data-stu-id="6df3e-185">Continuing with hello example form previous steps, we can see that hello application has been having availably issues.</span></span> <span data-ttu-id="6df3e-186">Напротив доступность платформы hello не перемещен из 100%.</span><span class="sxs-lookup"><span data-stu-id="6df3e-186">In contrast, hello platform availability has not moved from 100%.</span></span>

<span data-ttu-id="6df3e-187">При приложение hello испытывает проблемы и hello остается платформы вверх, это индикации, сейчас мы работаем с проблемы приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-187">When hello app is having issue and hello platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="6df3e-188"><a name="logging"></a> Шаг 5. Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="6df3e-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="6df3e-189">Теперь, когда мы сужается tooan приложения hello сбоев проблему, можно взглянуть на tooget журналы сервера и приложения hello Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-189">Now that we have narrowed down hello failures tooan application issue, we can look at hello application and server logs tooget more information.</span></span>

<span data-ttu-id="6df3e-190">Ведение журнала позволяет toocollect оба **Application Diagnostics** и **диагностики Web Server** журналов для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-190">Logging allows you toocollect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="6df3e-191">Диагностика приложений</span><span class="sxs-lookup"><span data-stu-id="6df3e-191">Application Diagnostics</span></span>
<span data-ttu-id="6df3e-192">Диагностика приложений позволяет вам toocapture трассировки, создаваемые во время выполнения приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-192">Application diagnostics allows you toocapture traces produced by hello application at runtime.</span></span>

<span data-ttu-id="6df3e-193">Добавление tooyour трассировки приложения значительно улучшает вашей проблемы точки ПИН-кода и возможность toodebug.</span><span class="sxs-lookup"><span data-stu-id="6df3e-193">Adding tracing tooyour application greatly improves your ability toodebug and pin-point issues.</span></span>

<span data-ttu-id="6df3e-194">В ASP.NET, можно записывать в журнал трассировки приложения с помощью [класса System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate события, записываемые в журнал инфраструктурой hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate events that are captured by hello log infrastructure.</span></span> <span data-ttu-id="6df3e-195">Можно также указать hello серьезность hello трассировки для упрощения фильтрации.</span><span class="sxs-lookup"><span data-stu-id="6df3e-195">You can also specify hello severity of hello trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="6df3e-196">Ведение журналов для приложений tooenable Go слишком**мониторинг** > **журналы диагностики** и включить ведение журнала приложения с помощью переключателей hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-196">tooenable Application logging Go too**Monitoring** > **Diagnostic Logs** and Enable Application Logging using hello toggles.</span></span>

![Мониторинг приложения](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="6df3e-198">Журналы приложений могут быть хранимые tooyour веб-приложения файловой системы или распространить tooblob хранилища.</span><span class="sxs-lookup"><span data-stu-id="6df3e-198">Application logs can be stored tooyour Web App's file system or pushed out tooblob storage.</span></span> <span data-ttu-id="6df3e-199">Для рабочих сценариев это рекомендуемый toouse хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="6df3e-199">For production scenarios, it's recommended toouse blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6df3e-200">Ведение журналов оказывает влияние на производительность приложения и использование ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6df3e-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="6df3e-201">В рабочей среде рекомендуется вести журналы ошибок.</span><span class="sxs-lookup"><span data-stu-id="6df3e-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="6df3e-202">Более подробное ведение журнала следует использовать только при устранении ошибок.</span><span class="sxs-lookup"><span data-stu-id="6df3e-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="6df3e-203">Диагностика веб-сервера</span><span class="sxs-lookup"><span data-stu-id="6df3e-203">Web Server Diagnostics</span></span>
<span data-ttu-id="6df3e-204">Журналы веб-сервера создаются, даже если приложение не инструментировано.</span><span class="sxs-lookup"><span data-stu-id="6df3e-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="6df3e-205">Служба приложений может собирать сведения для трех различных типов журналов сервера:</span><span class="sxs-lookup"><span data-stu-id="6df3e-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="6df3e-206">**Ведение журнала веб-сервера**</span><span class="sxs-lookup"><span data-stu-id="6df3e-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="6df3e-207">Сведения о HTTP-транзакций с помощью hello [расширенного формата файла журнала W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="6df3e-207">Information about HTTP transactions using hello [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="6df3e-208">Это удобно при определении общей сайта метрик, таких как количество hello запросы обрабатываются или сколько запросы отправляются определенный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="6df3e-208">Useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="6df3e-209">**Ведение журнала подробных ошибок**</span><span class="sxs-lookup"><span data-stu-id="6df3e-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="6df3e-210">Подробные сведения об ошибке для кодов состояния HTTP, которые указывают на сбой (код состояния 400 и выше).</span><span class="sxs-lookup"><span data-stu-id="6df3e-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="6df3e-211">Дополнительные сведения о подробных журналах ошибок</span><span class="sxs-lookup"><span data-stu-id="6df3e-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="6df3e-212">**Трассировка невыполненных запросов**</span><span class="sxs-lookup"><span data-stu-id="6df3e-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="6df3e-213">Подробные сведения о невыполненных запросов, включая трассировку компонентов IIS hello используется tooprocess hello запроса и hello время, затраченное в каждом компоненте.</span><span class="sxs-lookup"><span data-stu-id="6df3e-213">Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span>
    - <span data-ttu-id="6df3e-214">Журналы невыполненных запросов полезны при попытке tooisolate причину возникновения определенной ошибки HTTP.</span><span class="sxs-lookup"><span data-stu-id="6df3e-214">Failed request logs are useful when trying tooisolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="6df3e-215">Дополнительные сведения о трассировке невыполненных запросов</span><span class="sxs-lookup"><span data-stu-id="6df3e-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="6df3e-216">Ведение журнала tooenable сервера:</span><span class="sxs-lookup"><span data-stu-id="6df3e-216">tooenable Server logging:</span></span>
- <span data-ttu-id="6df3e-217">go слишком**мониторинг** > **журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="6df3e-217">go too**Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="6df3e-218">Включение различных типов hello Web Server диагностики с помощью переключателей hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-218">Enable hello different types of Web Server Diagnostics using hello toggles.</span></span>

![Мониторинг приложения](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="6df3e-220">Ведение журналов оказывает влияние на производительность приложения и использование ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6df3e-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="6df3e-221">В рабочей среде рекомендуется вести журналы ошибок. Более подробное ведение журнала следует использовать только при устранении ошибок.</span><span class="sxs-lookup"><span data-stu-id="6df3e-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="6df3e-222">Доступ к журналам</span><span class="sxs-lookup"><span data-stu-id="6df3e-222">Accessing Logs</span></span>
<span data-ttu-id="6df3e-223">Для доступа к журналам в хранилище BLOB-объектов используется обозреватель хранилищ Azure.</span><span class="sxs-lookup"><span data-stu-id="6df3e-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="6df3e-224">Журналов, хранящихся в файловой системе веб-приложения hello осуществляется по протоколу FTP в разделе hello, следующие пути:</span><span class="sxs-lookup"><span data-stu-id="6df3e-224">Logs stored in hello Web App's filesystem are accessed through FTP under hello following paths:</span></span>

- <span data-ttu-id="6df3e-225">**Журналы приложений** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="6df3e-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="6df3e-226">Эта папка содержит один или несколько текстовых файлов со сведениями, созданными при ведении журнала приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="6df3e-227">**Трассировка невыполненных запросов** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="6df3e-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="6df3e-228">Эта папка содержит XSL-файл и один или несколько XML-файлов.</span><span class="sxs-lookup"><span data-stu-id="6df3e-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="6df3e-229">**Подробные журналы ошибок** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="6df3e-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="6df3e-230">Эта папка содержит один или несколько HTML-файлов с подробными сведениями об ошибках HTTP, которые возникли в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="6df3e-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="6df3e-231">**Журналы веб-сервера** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="6df3e-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="6df3e-232">Эта папка содержит один или несколько текстовых файлов в формате с помощью расширенного формата файла журнала hello W3C.</span><span class="sxs-lookup"><span data-stu-id="6df3e-232">This folder contains one or more text files formatted using hello W3C extended log file format.</span></span>

## <span data-ttu-id="6df3e-233"><a name="streaming"></a> Шаг 6. Потоковая передача журналов</span><span class="sxs-lookup"><span data-stu-id="6df3e-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="6df3e-234">Журналы потоковой передачи удобны при отладке приложения, так как он позволяет сэкономить время, сравнивать слишком[доступе к журналам hello](#Accessing-Logs) по протоколу FTP.</span><span class="sxs-lookup"><span data-stu-id="6df3e-234">Streaming logs are convenient when debugging an application since it saves time compared too[accessing hello logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="6df3e-235">Служба приложения может передавать **журналы приложений** и **журналы веб-сервера** при их создании.</span><span class="sxs-lookup"><span data-stu-id="6df3e-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="6df3e-236">Прежде чем журналы toostream, убедитесь, что вы включили сбор журналов, как описано в hello [ведение журнала](#logging) раздела.</span><span class="sxs-lookup"><span data-stu-id="6df3e-236">Before trying toostream logs, make sure you have enabled collecting logs as described in hello [Logging](#logging) section.</span></span>

<span data-ttu-id="6df3e-237">журналы toostream go слишком**мониторинг**> **потока журнала**.</span><span class="sxs-lookup"><span data-stu-id="6df3e-237">toostream logs, go too**Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="6df3e-238">Выберите **Журналы приложений** или **Журналы веб-сервера** в зависимости от того, какие сведения вам необходимы.</span><span class="sxs-lookup"><span data-stu-id="6df3e-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="6df3e-239">Здесь можно также Приостановка, перезапуск и очистку буфера hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-239">From here, you can also pause, restart, and clear hello buffer.</span></span>

![Журналы потоковой передачи](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="6df3e-241">Журналы создаются только в том случае, когда приложение hello трафика, можно также увеличить уровень детализации hello tooget журналы дополнительные события и сведения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-241">Logs are only generated when there is traffic on hello app, you can also increase hello verbosity of logs tooget more events or information.</span></span>

## <span data-ttu-id="6df3e-242"><a name="remote"></a> Шаг 7. Удаленная отладка</span><span class="sxs-lookup"><span data-stu-id="6df3e-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="6df3e-243">После получения ПИН-кода указывает hello источником проблем приложения hello использовать **удаленной отладки** toowalk посредством кода hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-243">Once you have pin-pointed hello source of hello applications problems, use **Remote Debugging** toowalk through hello code.</span></span>

<span data-ttu-id="6df3e-244">Удаленная отладка позволяет присоединить отладчик tooyour веб-приложение работает в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-244">Remote debugging lets you attach a debugger tooyour Web App running in hello cloud.</span></span> <span data-ttu-id="6df3e-245">Можно установить точки останова, напрямую управлять памяти, пошагового выполнения кода и даже изменить путь кода hello так же, как и для приложения, работающего локально.</span><span class="sxs-lookup"><span data-stu-id="6df3e-245">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path just like you do for an app running locally.</span></span>

<span data-ttu-id="6df3e-246">tooattach hello отладчик tooyour приложение, работающее в облаке hello:</span><span class="sxs-lookup"><span data-stu-id="6df3e-246">tooattach hello debugger tooyour app running in hello cloud:</span></span>

- <span data-ttu-id="6df3e-247">С помощью Visual Studio 2017 г., Привет открыть решение для приложения hello требуется toodebug</span><span class="sxs-lookup"><span data-stu-id="6df3e-247">Using Visual Studio 2017, open hello solution for hello app you want toodebug</span></span>
- <span data-ttu-id="6df3e-248">Установите несколько точек останова так же, как и для локального приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="6df3e-249">Откройте **Cloud Explorer** (CTRL+/, CTRL+X).</span><span class="sxs-lookup"><span data-stu-id="6df3e-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="6df3e-250">При необходимости войдите в систему с учетными данными Azure.</span><span class="sxs-lookup"><span data-stu-id="6df3e-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="6df3e-251">Требуется toodebug приложение hello поиска</span><span class="sxs-lookup"><span data-stu-id="6df3e-251">Find hello app you want toodebug</span></span>
- <span data-ttu-id="6df3e-252">Выберите **подключить отладчик** hello формы **действия** области.</span><span class="sxs-lookup"><span data-stu-id="6df3e-252">Select **Attach Debugger** form hello **Actions** pane.</span></span>

![Удаленная отладка](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="6df3e-254">Настраивает приложение для удаленной отладки Visual Studio и открывает окно браузера, который осуществляет переход приложения tooyour.</span><span class="sxs-lookup"><span data-stu-id="6df3e-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates tooyour app.</span></span> <span data-ttu-id="6df3e-255">Просматривайте заданных точек останова tootrigger приложения и пошагового выполнения кода hello.</span><span class="sxs-lookup"><span data-stu-id="6df3e-255">Browse through your app tootrigger break points and step through hello code.</span></span>

> [!WARNING]
> <span data-ttu-id="6df3e-256">В рабочей среде выполнение в режиме отладки не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="6df3e-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="6df3e-257">Если на рабочее приложение не масштабировать toomultiple экземпляров сервера, отладка не hello веб-сервера от отвечает tooother запросов.</span><span class="sxs-lookup"><span data-stu-id="6df3e-257">If your production app is not scaled out toomultiple server instances, debugging prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="6df3e-258">Для устранения неполадок производства, лучший ресурс является слишком[настроить ведение журнала](#logging) и [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="6df3e-258">For troubleshooting production problems, your best resource is too[configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="6df3e-259"><a name="explorer"></a> Шаг 8. Обозреватель процессов</span><span class="sxs-lookup"><span data-stu-id="6df3e-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="6df3e-260">При масштабировании приложения out toomore более одной операции **обозреватель процессов** может помочь выявить проблемы конкретного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="6df3e-260">When your application is scaled out toomore than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="6df3e-261">С помощью **обозревателя процессов** можно выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6df3e-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="6df3e-262">Перечислить все процессы hello среди различных экземпляров плана служб приложений.</span><span class="sxs-lookup"><span data-stu-id="6df3e-262">Enumerate all hello processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="6df3e-263">Детализацию и просмотр hello дескрипторов и модулей, связанных с каждым процессом.</span><span class="sxs-lookup"><span data-stu-id="6df3e-263">Drill down and view hello handles and modules associated with each process.</span></span>
- <span data-ttu-id="6df3e-264">Число ЦП представление рабочего набора и потока при hello обработать уровня toohelp, необходимо указать предельное число процессов</span><span class="sxs-lookup"><span data-stu-id="6df3e-264">View CPU, Working Set, and Thread count at hello process level toohelp you identify runaway processes</span></span>
- <span data-ttu-id="6df3e-265">Находить открытые дескрипторы файлов и даже завершать конкретные экземпляры процессов.</span><span class="sxs-lookup"><span data-stu-id="6df3e-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="6df3e-266">Чтобы открыть обозреватель процессов, выберите **Мониторинг** > **Обозреватель процессов**.</span><span class="sxs-lookup"><span data-stu-id="6df3e-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Обозреватель процессов](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="6df3e-268"><a name="insights"></a> Шаг 9. Application Insights</span><span class="sxs-lookup"><span data-stu-id="6df3e-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="6df3e-269">**Application Insights** предоставляет функции профилирования и расширенные функции мониторинга для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="6df3e-270">Используйте toodetect Application Insights и диагностика исключений и проблем с производительностью в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-270">Use Application Insights toodetect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="6df3e-271">Вы можете включить Application Insights для своего веб-приложения в разделе **Мониторинг** > **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="6df3e-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="6df3e-272">Application Insights может предложить tooinstall hello Application Insights узел расширения toostart сбора данных.</span><span class="sxs-lookup"><span data-stu-id="6df3e-272">Application Insights might prompt you tooinstall hello Application Insights site extension toostart collecting data.</span></span> <span data-ttu-id="6df3e-273">Установка расширения сайта hello вызывает перезапуск приложения.</span><span class="sxs-lookup"><span data-stu-id="6df3e-273">Installing hello site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="6df3e-275">Аналитика приложений имеет обширных возможностей задано, toolearn более, ссылкам hello состава hello [дальнейшие действия](#next) раздела.</span><span class="sxs-lookup"><span data-stu-id="6df3e-275">Application Insights has a rich feature set, toolearn more, follow hello links included in hello [Next Steps](#next) section.</span></span>

## <span data-ttu-id="6df3e-276"><a name="next"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6df3e-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="6df3e-277">Что такое Application Insights</span><span class="sxs-lookup"><span data-stu-id="6df3e-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="6df3e-278">Мониторинг производительности веб-приложения Azure с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="6df3e-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="6df3e-279">Мониторинг доступности и скорости реагирования веб-сайта с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="6df3e-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
