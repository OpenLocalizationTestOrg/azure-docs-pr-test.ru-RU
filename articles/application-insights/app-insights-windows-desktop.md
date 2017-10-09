---
title: "Использование aaaMonitoring и производительность приложений рабочего стола Windows"
description: "Анализ использования и производительности классического приложения для Windows с помощью HockeyApp и Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="800b7-103">Мониторинг использования и производительности в классических приложениях для Windows</span><span class="sxs-lookup"><span data-stu-id="800b7-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="800b7-104">С помощью [Azure Application Insights](app-insights-overview.md) и [HockeyApp](https://hockeyapp.net) можно отслеживать показатели использования и производительности развернутого приложения.</span><span class="sxs-lookup"><span data-stu-id="800b7-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="800b7-105">Мы рекомендуем [HockeyApp](https://hockeyapp.net) toodistribute и монитор ПК и устройств приложения.</span><span class="sxs-lookup"><span data-stu-id="800b7-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="800b7-106">С помощью HockeyApp можно управлять распространением, тестированием в реальном времени и отзывами пользователей, а также отслеживать отчеты об использовании и сбоях.</span><span class="sxs-lookup"><span data-stu-id="800b7-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="800b7-107">Вы также можете [экспортировать и запросить данные телеметрии с помощью аналитики](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="800b7-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="800b7-108">Несмотря на то, что данные телеметрии могут отправляться tooApplication аналитики из классического приложения, это главным полезным для отладки и экспериментальный.</span><span class="sxs-lookup"><span data-stu-id="800b7-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="800b7-109">tooApplication телеметрии toosend аналитики из приложения Windows</span><span class="sxs-lookup"><span data-stu-id="800b7-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="800b7-110">В hello [портал Azure](https://portal.azure.com), [создать ресурс Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="800b7-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="800b7-111">Для параметра типа приложения выберите приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="800b7-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="800b7-112">Сделайте копию hello ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="800b7-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="800b7-113">Найти ключ hello в hello Essentials раскрывающемся hello новый ресурс, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="800b7-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="800b7-114">В Visual Studio измените пакеты NuGet hello проекта приложения и добавьте Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="800b7-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="800b7-115">(Или нажмите Microsoft.ApplicationInsights, если необходимо просто hello API состояния системы, без hello стандартной телеметрии коллекцию модулей.)</span><span class="sxs-lookup"><span data-stu-id="800b7-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="800b7-116">Задайте ключ инструментирования hello, либо в коде:</span><span class="sxs-lookup"><span data-stu-id="800b7-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="800b7-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *ваш ключ* `";`</span><span class="sxs-lookup"><span data-stu-id="800b7-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="800b7-118">или в файле ApplicationInsights.config (Если вы установили один из пакетов стандартной телеметрии hello):</span><span class="sxs-lookup"><span data-stu-id="800b7-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="800b7-119">`<InstrumentationKey>`*ваш ключ*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="800b7-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="800b7-120">Если вы используете ApplicationInsights.config, убедитесь, что его свойства в обозревателе решений заданы слишком**действие построения = содержимое tooOutput копирования каталога = копирование**.</span><span class="sxs-lookup"><span data-stu-id="800b7-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="800b7-121">[Используйте hello API](app-insights-api-custom-events-metrics.md) toosend телеметрии.</span><span class="sxs-lookup"><span data-stu-id="800b7-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="800b7-122">Запуск приложения и разделе телеметрии hello в ресурсе hello, созданный на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="800b7-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="800b7-123"><a name="telemetry"></a>Пример кода</span><span class="sxs-lookup"><span data-stu-id="800b7-123"><a name="telemetry"></a>Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a><span data-ttu-id="800b7-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="800b7-124">Next steps</span></span>
* [<span data-ttu-id="800b7-125">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="800b7-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="800b7-126">Поиск по журналу диагностики</span><span class="sxs-lookup"><span data-stu-id="800b7-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="800b7-127">Изучение метрик</span><span class="sxs-lookup"><span data-stu-id="800b7-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="800b7-128">Написание запросов аналитики</span><span class="sxs-lookup"><span data-stu-id="800b7-128">Write Analytics queries</span></span>](app-insights-analytics.md)

