---
title: "Мониторинг использования и производительности классических приложений для Windows"
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
ms.openlocfilehash: 9d7e2a390adf10cbf5d88dd0084ce09136987309
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="3412a-103">Мониторинг использования и производительности в классических приложениях для Windows</span><span class="sxs-lookup"><span data-stu-id="3412a-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="3412a-104">С помощью [Azure Application Insights](app-insights-overview.md) и [HockeyApp](https://hockeyapp.net) можно отслеживать показатели использования и производительности развернутого приложения.</span><span class="sxs-lookup"><span data-stu-id="3412a-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3412a-105">Мы рекомендуем использовать [HockeyApp](https://hockeyapp.net) для распространения и мониторинга классических приложений и приложений для устройств.</span><span class="sxs-lookup"><span data-stu-id="3412a-105">We recommend [HockeyApp](https://hockeyapp.net) to distribute and monitor desktop and device apps.</span></span> <span data-ttu-id="3412a-106">С помощью HockeyApp можно управлять распространением, тестированием в реальном времени и отзывами пользователей, а также отслеживать отчеты об использовании и сбоях.</span><span class="sxs-lookup"><span data-stu-id="3412a-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="3412a-107">Вы также можете [экспортировать и запросить данные телеметрии с помощью аналитики](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="3412a-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="3412a-108">Несмотря на то, что данные телеметрии можно отправлять в Application Insights из классического приложения, этот подход главным образом используется для отладки и проведения экспериментов.</span><span class="sxs-lookup"><span data-stu-id="3412a-108">Although telemetry can be sent to Application Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="to-send-telemetry-to-application-insights-from-a-windows-application"></a><span data-ttu-id="3412a-109">Отправка данных телеметрии в Application Insights из приложения для Windows</span><span class="sxs-lookup"><span data-stu-id="3412a-109">To send telemetry to Application Insights from a Windows application</span></span>
1. <span data-ttu-id="3412a-110">На [портале Azure](https://portal.azure.com) [создайте ресурс Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3412a-110">In the [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="3412a-111">Для параметра типа приложения выберите приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3412a-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="3412a-112">Сделайте копию ключа инструментирования.</span><span class="sxs-lookup"><span data-stu-id="3412a-112">Take a copy of the Instrumentation Key.</span></span> <span data-ttu-id="3412a-113">Найдите ключ в раскрывающемся списке "Основные компоненты" нового ресурса, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="3412a-113">Find the key in the Essentials drop-down of the new resource you just created.</span></span> 
3. <span data-ttu-id="3412a-114">В Visual Studio измените пакеты NuGet вашего проекта приложения и добавьте Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="3412a-114">In Visual Studio, edit the NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="3412a-115">(Выберите Microsoft.ApplicationInsights, если нужен чистый API без модулей сбора стандартной телеметрии.)</span><span class="sxs-lookup"><span data-stu-id="3412a-115">(Or choose Microsoft.ApplicationInsights if you just want the bare API, without the standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="3412a-116">Задайте ключ инструментирования в коде.</span><span class="sxs-lookup"><span data-stu-id="3412a-116">Set the instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="3412a-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *ваш ключ* `";`</span><span class="sxs-lookup"><span data-stu-id="3412a-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="3412a-118">Можно также задать его в файле ApplicationInsights.config (если установлен один из пакетов стандартной телеметрии).</span><span class="sxs-lookup"><span data-stu-id="3412a-118">or in ApplicationInsights.config (if you installed one of the standard telemetry packages):</span></span>
   
    <span data-ttu-id="3412a-119">`<InstrumentationKey>`*ваш ключ*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="3412a-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="3412a-120">Если используется файл ApplicationInsights.config, убедитесь, что его свойства в обозревателе решений имеют следующие значения: **"Действие сборки = содержимое", "Копировать в выходной каталог = копировать"**.</span><span class="sxs-lookup"><span data-stu-id="3412a-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>
5. <span data-ttu-id="3412a-121">[Используйте API](app-insights-api-custom-events-metrics.md) для отправки данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="3412a-121">[Use the API](app-insights-api-custom-events-metrics.md) to send telemetry.</span></span>
6. <span data-ttu-id="3412a-122">Запустите приложение и понаблюдайте за телеметрией в ресурсе, созданном на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3412a-122">Run your app, and see the telemetry in the resource you created in the Azure Portal.</span></span>

## <span data-ttu-id="3412a-123"><a name="telemetry"></a>Пример кода</span><span class="sxs-lookup"><span data-stu-id="3412a-123"><a name="telemetry"></a>Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative to setting ikey in config file:
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

## <a name="next-steps"></a><span data-ttu-id="3412a-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3412a-124">Next steps</span></span>
* [<span data-ttu-id="3412a-125">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="3412a-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="3412a-126">Поиск по журналу диагностики</span><span class="sxs-lookup"><span data-stu-id="3412a-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="3412a-127">Изучение метрик</span><span class="sxs-lookup"><span data-stu-id="3412a-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="3412a-128">Написание запросов аналитики</span><span class="sxs-lookup"><span data-stu-id="3412a-128">Write Analytics queries</span></span>](app-insights-analytics.md)

