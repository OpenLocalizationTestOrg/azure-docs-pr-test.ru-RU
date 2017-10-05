---
title: "Мониторинг веб-приложения | Документы Майкрософт"
description: "Узнайте, как настроить мониторинг веб-приложения"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="2f49e-103">Мониторинг службы приложений</span><span class="sxs-lookup"><span data-stu-id="2f49e-103">Monitor App Service</span></span>
<span data-ttu-id="2f49e-104">Это руководство описывает мониторинг приложения и использование встроенных средств платформы для решения возникающих проблем.</span><span class="sxs-lookup"><span data-stu-id="2f49e-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="2f49e-105">Каждый раздел этого документа посвящен определенной функции.</span><span class="sxs-lookup"><span data-stu-id="2f49e-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="2f49e-106">Совместное использование этих функций позволяет:</span><span class="sxs-lookup"><span data-stu-id="2f49e-106">Using the features together let you:</span></span>
- <span data-ttu-id="2f49e-107">выявить проблему в приложении;</span><span class="sxs-lookup"><span data-stu-id="2f49e-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="2f49e-108">определить, вызвана ли проблема кодом или платформой;</span><span class="sxs-lookup"><span data-stu-id="2f49e-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="2f49e-109">сузить число причин проблемы в коде;</span><span class="sxs-lookup"><span data-stu-id="2f49e-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="2f49e-110">отладить и устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="2f49e-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2f49e-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2f49e-111">Before you begin</span></span>
- <span data-ttu-id="2f49e-112">Для выполнения описанных действий вам понадобится веб-приложение, которое и будет отслеживаться.</span><span class="sxs-lookup"><span data-stu-id="2f49e-112">You need a Web App to monitor and follow the outlined steps.</span></span>
    - <span data-ttu-id="2f49e-113">Чтобы создать приложение, можно выполнить действия, описанные в руководстве [Создание приложения ASP.NET в Azure с подключением к базе данных SQL](app-service-web-tutorial-dotnet-sqldatabase.md).</span><span class="sxs-lookup"><span data-stu-id="2f49e-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="2f49e-114">Если вы хотите попробовать **удаленную отладку** приложения, потребуется Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f49e-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="2f49e-115">Если вы еще не установили Visual Studio 2017, вы можете скачать и использовать бесплатную среду [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2f49e-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="2f49e-116">При установке Visual Studio необходимо включить возможность **разработки для Azure**.</span><span class="sxs-lookup"><span data-stu-id="2f49e-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <span data-ttu-id="2f49e-117"><a name="metrics"></a>Шаг 1. Просмотр метрик</span><span class="sxs-lookup"><span data-stu-id="2f49e-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="2f49e-118">Важно разбираться в значении **метрик**:</span><span class="sxs-lookup"><span data-stu-id="2f49e-118">**Metrics** are useful to understand:</span></span>
- <span data-ttu-id="2f49e-119">Работоспособность приложения</span><span class="sxs-lookup"><span data-stu-id="2f49e-119">Application health</span></span>
- <span data-ttu-id="2f49e-120">Производительность приложения</span><span class="sxs-lookup"><span data-stu-id="2f49e-120">App performance</span></span>
- <span data-ttu-id="2f49e-121">Потребление ресурсов</span><span class="sxs-lookup"><span data-stu-id="2f49e-121">Resource consumption</span></span>

<span data-ttu-id="2f49e-122">При исследовании проблемы в приложении начать лучше всего с обзора метрик.</span><span class="sxs-lookup"><span data-stu-id="2f49e-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="2f49e-123">На портале Azure можно быстро визуально оценить метрики приложения с помощью **Azure Monitor**.</span><span class="sxs-lookup"><span data-stu-id="2f49e-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="2f49e-124">Метрики обеспечивают историческое представление по нескольким ключевым агрегатам для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="2f49e-125">Для любого приложения, размещенного в службе приложений, нужно отслеживать как веб-приложение, так и план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="2f49e-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="2f49e-126">План службы приложений представляет собой коллекцию физических ресурсов, используемых для размещения приложений.</span><span class="sxs-lookup"><span data-stu-id="2f49e-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="2f49e-127">Все приложения, назначенные плану службы приложений, совместно используют ресурсы, определенные в нем. Поэтому, разместив несколько приложений, вы сможете сэкономить.</span><span class="sxs-lookup"><span data-stu-id="2f49e-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="2f49e-128">Планы службы приложений определяют такие компоненты:</span><span class="sxs-lookup"><span data-stu-id="2f49e-128">App Service plans define:</span></span>
> * <span data-ttu-id="2f49e-129">Регион: Северная Европа, восточная часть США, Юго-Восточная Азия и т. д.</span><span class="sxs-lookup"><span data-stu-id="2f49e-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="2f49e-130">Размер экземпляра: небольшой, средний, крупный и т. д.</span><span class="sxs-lookup"><span data-stu-id="2f49e-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="2f49e-131">Число масштабируемых элементов: один, два, три экземпляра и т. д.</span><span class="sxs-lookup"><span data-stu-id="2f49e-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="2f49e-132">SKU: "Бесплатный", "Общий", "Базовый", "Стандартный", "Премиум" и т. д.</span><span class="sxs-lookup"><span data-stu-id="2f49e-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="2f49e-133">Для просмотра метрик веб-приложения перейдите в колонку **Обзор** приложения, которое требуется отслеживать.</span><span class="sxs-lookup"><span data-stu-id="2f49e-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="2f49e-134">Здесь можно просмотреть диаграмму для метрик приложения в **элементе "Мониторинг"**.</span><span class="sxs-lookup"><span data-stu-id="2f49e-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="2f49e-135">Щелкните элемент, чтобы изменить и настроить отображаемые метрики и интервал времени.</span><span class="sxs-lookup"><span data-stu-id="2f49e-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span>

<span data-ttu-id="2f49e-136">По умолчанию колонка ресурсов содержит представление для запросов приложений и ошибки за последний час.</span><span class="sxs-lookup"><span data-stu-id="2f49e-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="2f49e-137">![Мониторинг приложения](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="2f49e-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="2f49e-138">Как видно из примера, у нас есть приложения, создающее множество **ошибок HTTP-сервера**.</span><span class="sxs-lookup"><span data-stu-id="2f49e-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="2f49e-139">Большое число ошибок является первым признаком того, что нужно изучить это приложение.</span><span class="sxs-lookup"><span data-stu-id="2f49e-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="2f49e-140">Дополнительные сведения об Azure Monitor доступны в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="2f49e-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="2f49e-141">Приступая к работе с Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="2f49e-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="2f49e-142">Метрики Azure</span><span class="sxs-lookup"><span data-stu-id="2f49e-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="2f49e-143">Метрики, поддерживаемые Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="2f49e-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="2f49e-144">Панели мониторинга Azure</span><span class="sxs-lookup"><span data-stu-id="2f49e-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="2f49e-145"><a name="alerts"></a> Шаг 2. Настройка оповещений</span><span class="sxs-lookup"><span data-stu-id="2f49e-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="2f49e-146">**Оповещения** можно настроить для активации по определенным условиям для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="2f49e-147">В разделе [Шаг 1. Просмотр метрик](#metrics) мы видели, что приложение имеет большое количество ошибок.</span><span class="sxs-lookup"><span data-stu-id="2f49e-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span>

<span data-ttu-id="2f49e-148">Давайте настроим оповещение, чтобы автоматически получать уведомления при возникновении ошибок.</span><span class="sxs-lookup"><span data-stu-id="2f49e-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="2f49e-149">В этом случае нам нужно, чтобы оповещение отправляло сообщение электронной почты каждый раз, когда число ошибок HTTP 50X превышает определенный порог.</span><span class="sxs-lookup"><span data-stu-id="2f49e-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="2f49e-150">Чтобы создать оповещение, перейдите в **Мониторинг** > **Оповещения** и щелкните **[+] Добавить оповещение**.</span><span class="sxs-lookup"><span data-stu-id="2f49e-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Оповещения](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="2f49e-152">Укажите значения для конфигурации оповещений:</span><span class="sxs-lookup"><span data-stu-id="2f49e-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="2f49e-153">**Ресурс:** сайт для мониторинга с помощью оповещения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-153">**Resource:** The site to monitor with the alert.</span></span>
- <span data-ttu-id="2f49e-154">**Имя:** имя оповещения, в данном случае это *High HTTP 50X* (Большое число HTTP 50X).</span><span class="sxs-lookup"><span data-stu-id="2f49e-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="2f49e-155">**Описание:** пояснение, что отслеживает это оповещение, в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="2f49e-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="2f49e-156">**Оповещения включены:** оповещения могут отслеживать метрики или события. В этом примере нас интересуют метрики.</span><span class="sxs-lookup"><span data-stu-id="2f49e-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="2f49e-157">**Метрика:** отслеживаемая метрика, в данном случае это *Ошибки сервера Http*.</span><span class="sxs-lookup"><span data-stu-id="2f49e-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="2f49e-158">**Условие:** когда активируется оповещение, в данном случае выберите параметр *больше*.</span><span class="sxs-lookup"><span data-stu-id="2f49e-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="2f49e-159">**Пороговое значение:** искомое значение, в данном случае это *400*.</span><span class="sxs-lookup"><span data-stu-id="2f49e-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="2f49e-160">**Период:** оповещения учитывают среднее значение метрики.</span><span class="sxs-lookup"><span data-stu-id="2f49e-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="2f49e-161">При уменьшении периодов чувствительность оповещений возрастает.</span><span class="sxs-lookup"><span data-stu-id="2f49e-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="2f49e-162">В данном случае мы используем значение *5 минут*.</span><span class="sxs-lookup"><span data-stu-id="2f49e-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="2f49e-163">**Email Owners and contributors** (Участники и владельцы электронной почты): в данном случае установлено значение *Включено*.</span><span class="sxs-lookup"><span data-stu-id="2f49e-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="2f49e-164">Теперь, когда оповещение создано, сообщение электронной почты отправляется каждый раз, когда приложение превышает заданное пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="2f49e-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="2f49e-165">Активные оповещения также можно просмотреть на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2f49e-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![Активированные оповещения](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="2f49e-167">Дополнительные сведения об оповещениях Azure доступны в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="2f49e-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="2f49e-168">Что такое оповещения в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2f49e-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="2f49e-169">Действия с метриками</span><span class="sxs-lookup"><span data-stu-id="2f49e-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="2f49e-170">Создание оповещений о метриках</span><span class="sxs-lookup"><span data-stu-id="2f49e-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="2f49e-171"><a name="companion"></a> Шаг 3. Дополнительное приложение для службы приложений</span><span class="sxs-lookup"><span data-stu-id="2f49e-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="2f49e-172">С помощью **вспомогательного приложения для службы приложений** можно удобно отслеживать приложение с привычным интерфейсом на мобильном устройстве (iOS или Android).</span><span class="sxs-lookup"><span data-stu-id="2f49e-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="2f49e-173">Вспомогательное приложение для службы приложений Azure позволяет выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2f49e-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="2f49e-174">Просматривать метрики приложения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-174">Review application metrics</span></span>
- <span data-ttu-id="2f49e-175">Просматривать уведомления для приложения и выполнять необходимые действия, а также получать рекомендации.</span><span class="sxs-lookup"><span data-stu-id="2f49e-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="2f49e-176">Выполнять базовые действия при устранении неполадок (просмотр, запуск, остановка, перезапуск приложения).</span><span class="sxs-lookup"><span data-stu-id="2f49e-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="2f49e-177">Получать push-уведомления о важных событиях.</span><span class="sxs-lookup"><span data-stu-id="2f49e-177">Get push notifications for critical events.</span></span>

![Вспомогательное приложение для службы приложений](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="2f49e-179">[![Вспомогательное приложение для службы приложений в магазине приложений](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Вспомогательное приложение для службы приложений в Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="2f49e-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="2f49e-180">Вспомогательное приложение для службы приложений можно установить из [магазина приложений](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) или [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="2f49e-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="2f49e-181"><a name="diagnose"></a> Шаг 4. Диагностика и решение проблем</span><span class="sxs-lookup"><span data-stu-id="2f49e-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="2f49e-182">Пункт **Диагностика и решение проблем** помогает отделить проблемы приложений от проблем платформы.</span><span class="sxs-lookup"><span data-stu-id="2f49e-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="2f49e-183">Он также может предложить возможные способы для восстановления работоспособности веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>

![Диагностика и решение проблем](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="2f49e-185">Продолжив работу с примером из предыдущих шагов, мы видим, что в приложении возникли проблемы с доступностью.</span><span class="sxs-lookup"><span data-stu-id="2f49e-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="2f49e-186">Доступность платформы, напротив, неизменно оставалась на уровне 100 %.</span><span class="sxs-lookup"><span data-stu-id="2f49e-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="2f49e-187">Если приложение испытывает проблемы, а платформа остается работоспособной, это указывает на то, что проблема связана именно с приложением.</span><span class="sxs-lookup"><span data-stu-id="2f49e-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="2f49e-188"><a name="logging"></a> Шаг 5. Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="2f49e-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="2f49e-189">Теперь, когда мы связали сбои с проблемами в приложении, нужно просмотреть журналы приложения и сервера для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="2f49e-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="2f49e-190">Ведение журналов позволяет собирать сведения из журналов **диагностики приложений** и **диагностики веб-сервера** для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="2f49e-191">Диагностика приложений</span><span class="sxs-lookup"><span data-stu-id="2f49e-191">Application Diagnostics</span></span>
<span data-ttu-id="2f49e-192">Диагностика приложений позволяет записывать сведения трассировки, создаваемые приложением во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span>

<span data-ttu-id="2f49e-193">Добавление трассировки в приложение значительно улучшает возможности отладки и выявления проблем.</span><span class="sxs-lookup"><span data-stu-id="2f49e-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="2f49e-194">В ASP.NET можно воспользоваться [классом System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) для создания событий трассировки приложений, которые будут зафиксированы инфраструктурой ведения журналов и записаны в журнал.</span><span class="sxs-lookup"><span data-stu-id="2f49e-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="2f49e-195">Для упрощения фильтрации записей также можно указать уровень важности трассировки.</span><span class="sxs-lookup"><span data-stu-id="2f49e-195">You can also specify the severity of the trace for easier filtering.</span></span>

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
<span data-ttu-id="2f49e-196">Чтобы включить ведение журнала приложений, перейдите в раздел **Мониторинг** > **Журналы диагностики** и включите ведение журналов приложений с помощью переключателей.</span><span class="sxs-lookup"><span data-stu-id="2f49e-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![Мониторинг приложения](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="2f49e-198">Журналы приложений можно хранить в файловой системе веб-приложения или отправлять в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2f49e-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="2f49e-199">В рабочей среде рекомендуется использовать хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2f49e-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f49e-200">Ведение журналов оказывает влияние на производительность приложения и использование ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2f49e-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="2f49e-201">В рабочей среде рекомендуется вести журналы ошибок.</span><span class="sxs-lookup"><span data-stu-id="2f49e-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="2f49e-202">Более подробное ведение журнала следует использовать только при устранении ошибок.</span><span class="sxs-lookup"><span data-stu-id="2f49e-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="2f49e-203">Диагностика веб-сервера</span><span class="sxs-lookup"><span data-stu-id="2f49e-203">Web Server Diagnostics</span></span>
<span data-ttu-id="2f49e-204">Журналы веб-сервера создаются, даже если приложение не инструментировано.</span><span class="sxs-lookup"><span data-stu-id="2f49e-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="2f49e-205">Служба приложений может собирать сведения для трех различных типов журналов сервера:</span><span class="sxs-lookup"><span data-stu-id="2f49e-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="2f49e-206">**Ведение журнала веб-сервера**</span><span class="sxs-lookup"><span data-stu-id="2f49e-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="2f49e-207">Сведения об HTTP-транзакциях в [расширенном формате файла журнала W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f49e-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="2f49e-208">Это удобно при определении общих показателей сайта, например количества обработанных запросов или количества запросов, поступивших с определенного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="2f49e-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="2f49e-209">**Ведение журнала подробных ошибок**</span><span class="sxs-lookup"><span data-stu-id="2f49e-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="2f49e-210">Подробные сведения об ошибке для кодов состояния HTTP, которые указывают на сбой (код состояния 400 и выше).</span><span class="sxs-lookup"><span data-stu-id="2f49e-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="2f49e-211">Дополнительные сведения о подробных журналах ошибок</span><span class="sxs-lookup"><span data-stu-id="2f49e-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="2f49e-212">**Трассировка невыполненных запросов**</span><span class="sxs-lookup"><span data-stu-id="2f49e-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="2f49e-213">Подробные сведения о невыполненных запросах, включая трассировку компонентов IIS, использованных для обработки запроса, и время, потраченное для каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="2f49e-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span>
    - <span data-ttu-id="2f49e-214">Журналы невыполненных запросов особенно удобны при выявлении причины конкретной ошибки HTTP.</span><span class="sxs-lookup"><span data-stu-id="2f49e-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="2f49e-215">Дополнительные сведения о трассировке невыполненных запросов</span><span class="sxs-lookup"><span data-stu-id="2f49e-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="2f49e-216">Чтобы включить ведение журнала сервера, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2f49e-216">To enable Server logging:</span></span>
- <span data-ttu-id="2f49e-217">Выберите **Мониторинг** > **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="2f49e-217">go to **Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="2f49e-218">Включите различные типы диагностики веб-сервера с помощью переключателей.</span><span class="sxs-lookup"><span data-stu-id="2f49e-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![Мониторинг приложения](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="2f49e-220">Ведение журналов оказывает влияние на производительность приложения и использование ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2f49e-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="2f49e-221">В рабочей среде рекомендуется вести журналы ошибок. Более подробное ведение журнала следует использовать только при устранении ошибок.</span><span class="sxs-lookup"><span data-stu-id="2f49e-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="2f49e-222">Доступ к журналам</span><span class="sxs-lookup"><span data-stu-id="2f49e-222">Accessing Logs</span></span>
<span data-ttu-id="2f49e-223">Для доступа к журналам в хранилище BLOB-объектов используется обозреватель хранилищ Azure.</span><span class="sxs-lookup"><span data-stu-id="2f49e-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="2f49e-224">Для доступа к журналам в файловой системе веб-приложения используется протокол FTP. Журналы доступны по следующим путям:</span><span class="sxs-lookup"><span data-stu-id="2f49e-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="2f49e-225">**Журналы приложений** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="2f49e-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="2f49e-226">Эта папка содержит один или несколько текстовых файлов со сведениями, созданными при ведении журнала приложения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="2f49e-227">**Трассировка невыполненных запросов** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="2f49e-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="2f49e-228">Эта папка содержит XSL-файл и один или несколько XML-файлов.</span><span class="sxs-lookup"><span data-stu-id="2f49e-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="2f49e-229">**Подробные журналы ошибок** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="2f49e-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="2f49e-230">Эта папка содержит один или несколько HTML-файлов с подробными сведениями об ошибках HTTP, которые возникли в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="2f49e-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="2f49e-231">**Журналы веб-сервера** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="2f49e-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="2f49e-232">Эта папка содержит один или несколько текстовых файлов, отформатированных с применением расширенного формата журнала W3C.</span><span class="sxs-lookup"><span data-stu-id="2f49e-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <span data-ttu-id="2f49e-233"><a name="streaming"></a> Шаг 6. Потоковая передача журналов</span><span class="sxs-lookup"><span data-stu-id="2f49e-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="2f49e-234">Потоковая передача журналов удобна при отладке приложения, так как позволяет сэкономить время по сравнению с [обращением к журналам](#Accessing-Logs) через FTP.</span><span class="sxs-lookup"><span data-stu-id="2f49e-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="2f49e-235">Служба приложения может передавать **журналы приложений** и **журналы веб-сервера** при их создании.</span><span class="sxs-lookup"><span data-stu-id="2f49e-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="2f49e-236">Перед включением потоковой передачи журналов убедитесь, что вы включили сбор журналов, как описано в разделе [Ведение журнала](#logging).</span><span class="sxs-lookup"><span data-stu-id="2f49e-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="2f49e-237">Для потоковой передачи журналов выберите **Мониторинг**> **Потоковая передача журналов**.</span><span class="sxs-lookup"><span data-stu-id="2f49e-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="2f49e-238">Выберите **Журналы приложений** или **Журналы веб-сервера** в зависимости от того, какие сведения вам необходимы.</span><span class="sxs-lookup"><span data-stu-id="2f49e-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="2f49e-239">Здесь можно также приостановить, перезапустить и очистить буфер.</span><span class="sxs-lookup"><span data-stu-id="2f49e-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![Журналы потоковой передачи](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="2f49e-241">Журналы создаются только при наличии трафика у приложения. Также можно повысить уровень детализации журналов, чтобы получить дополнительные события или сведения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <span data-ttu-id="2f49e-242"><a name="remote"></a> Шаг 7. Удаленная отладка</span><span class="sxs-lookup"><span data-stu-id="2f49e-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="2f49e-243">Установив источник проблем в приложении, используйте **удаленную отладку** для прохода по коду.</span><span class="sxs-lookup"><span data-stu-id="2f49e-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="2f49e-244">Удаленная отладка позволяет подключить отладчик к веб-приложению, запущенному в облаке.</span><span class="sxs-lookup"><span data-stu-id="2f49e-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="2f49e-245">Вы можете устанавливать точки останова, обращаться к памяти напрямую, пошагово выполнять код и даже изменять путь к коду, как и для приложения, запускаемого локально.</span><span class="sxs-lookup"><span data-stu-id="2f49e-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="2f49e-246">Чтобы подключить отладчик к приложению, запущенному в облаке, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2f49e-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="2f49e-247">Откройте решение для приложения, для которого нужно выполнить отладку, в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2f49e-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span>
- <span data-ttu-id="2f49e-248">Установите несколько точек останова так же, как и для локального приложения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="2f49e-249">Откройте **Cloud Explorer** (CTRL+/, CTRL+X).</span><span class="sxs-lookup"><span data-stu-id="2f49e-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="2f49e-250">При необходимости войдите в систему с учетными данными Azure.</span><span class="sxs-lookup"><span data-stu-id="2f49e-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="2f49e-251">Найдите приложение, для которого нужно выполнить отладку.</span><span class="sxs-lookup"><span data-stu-id="2f49e-251">Find the app you want to debug</span></span>
- <span data-ttu-id="2f49e-252">Выберите **Подключить отладчик** в области **Действия**.</span><span class="sxs-lookup"><span data-stu-id="2f49e-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![Удаленная отладка](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="2f49e-254">Visual Studio настраивает приложение для удаленной отладки и затем открывает ваше приложение в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="2f49e-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="2f49e-255">Выполните необходимые действия в приложении для срабатывания точек останова и пройдитесь по коду.</span><span class="sxs-lookup"><span data-stu-id="2f49e-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="2f49e-256">В рабочей среде выполнение в режиме отладки не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="2f49e-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="2f49e-257">Если ваше рабочее приложение не развернуто на несколько экземпляров сервера, то веб-сервер во время отладки не сможет отвечать на запросы от других приложений.</span><span class="sxs-lookup"><span data-stu-id="2f49e-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="2f49e-258">Для устранения неполадок в рабочей среде лучше всего [настроить ведение журналов](#logging) и использовать [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="2f49e-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="2f49e-259"><a name="explorer"></a> Шаг 8. Обозреватель процессов</span><span class="sxs-lookup"><span data-stu-id="2f49e-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="2f49e-260">Когда приложение масштабируется до нескольких экземпляров, **обозреватель процессов** позволяет выявить проблемы конкретного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="2f49e-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="2f49e-261">С помощью **обозревателя процессов** можно выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2f49e-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="2f49e-262">Получить список всех процессов для различных экземпляров плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="2f49e-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="2f49e-263">Просматривать подробные сведения о каждом процессе, в том числе дескрипторы и модули.</span><span class="sxs-lookup"><span data-stu-id="2f49e-263">Drill down and view the handles and modules associated with each process.</span></span>
- <span data-ttu-id="2f49e-264">Просматривать сведения об использовании ЦП, рабочих наборах и количестве потоков на уровне процесса, чтобы определить процессы, выходящие за допустимые пределы.</span><span class="sxs-lookup"><span data-stu-id="2f49e-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="2f49e-265">Находить открытые дескрипторы файлов и даже завершать конкретные экземпляры процессов.</span><span class="sxs-lookup"><span data-stu-id="2f49e-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="2f49e-266">Чтобы открыть обозреватель процессов, выберите **Мониторинг** > **Обозреватель процессов**.</span><span class="sxs-lookup"><span data-stu-id="2f49e-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Обозреватель процессов](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="2f49e-268"><a name="insights"></a> Шаг 9. Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f49e-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="2f49e-269">**Application Insights** предоставляет функции профилирования и расширенные функции мониторинга для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="2f49e-270">Application Insights позволяет выявлять и диагностировать исключения и проблемы производительности в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="2f49e-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="2f49e-271">Вы можете включить Application Insights для своего веб-приложения в разделе **Мониторинг** > **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="2f49e-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="2f49e-272">Application Insights может предложить вам установить расширение сайта Application Insights, чтобы начать сбор данных.</span><span class="sxs-lookup"><span data-stu-id="2f49e-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="2f49e-273">Установка расширения сайта приводит к перезапуску приложения.</span><span class="sxs-lookup"><span data-stu-id="2f49e-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="2f49e-275">Application Insights обладает богатым набором функций. Дополнительные сведения см. в статьях, указанных в разделе [Дальнейшие действия](#next).</span><span class="sxs-lookup"><span data-stu-id="2f49e-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <span data-ttu-id="2f49e-276"><a name="next"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f49e-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="2f49e-277">Что такое Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f49e-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="2f49e-278">Мониторинг производительности веб-приложения Azure с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f49e-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="2f49e-279">Мониторинг доступности и скорости реагирования веб-сайта с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f49e-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
