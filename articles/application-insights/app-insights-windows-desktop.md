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
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Мониторинг использования и производительности в классических приложениях для Windows


С помощью [Azure Application Insights](app-insights-overview.md) и [HockeyApp](https://hockeyapp.net) можно отслеживать показатели использования и производительности развернутого приложения.

> [!IMPORTANT]
> Мы рекомендуем [HockeyApp](https://hockeyapp.net) toodistribute и монитор ПК и устройств приложения. С помощью HockeyApp можно управлять распространением, тестированием в реальном времени и отзывами пользователей, а также отслеживать отчеты об использовании и сбоях. Вы также можете [экспортировать и запросить данные телеметрии с помощью аналитики](app-insights-hockeyapp-bridge-app.md).
> 
> Несмотря на то, что данные телеметрии могут отправляться tooApplication аналитики из классического приложения, это главным полезным для отладки и экспериментальный.
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>tooApplication телеметрии toosend аналитики из приложения Windows
1. В hello [портал Azure](https://portal.azure.com), [создать ресурс Application Insights](app-insights-create-new-resource.md). Для параметра типа приложения выберите приложение ASP.NET.
2. Сделайте копию hello ключ инструментирования. Найти ключ hello в hello Essentials раскрывающемся hello новый ресурс, который вы только что создали. 
3. В Visual Studio измените пакеты NuGet hello проекта приложения и добавьте Microsoft.ApplicationInsights.WindowsServer. (Или нажмите Microsoft.ApplicationInsights, если необходимо просто hello API состояния системы, без hello стандартной телеметрии коллекцию модулей.)
4. Задайте ключ инструментирования hello, либо в коде:
   
    `TelemetryConfiguration.Active.InstrumentationKey = "` *ваш ключ* `";` 
   
    или в файле ApplicationInsights.config (Если вы установили один из пакетов стандартной телеметрии hello):
   
    `<InstrumentationKey>`*ваш ключ*`</InstrumentationKey>` 
   
    Если вы используете ApplicationInsights.config, убедитесь, что его свойства в обозревателе решений заданы слишком**действие построения = содержимое tooOutput копирования каталога = копирование**.
5. [Используйте hello API](app-insights-api-custom-events-metrics.md) toosend телеметрии.
6. Запуск приложения и разделе телеметрии hello в ресурсе hello, созданный на портале Azure hello.

## <a name="telemetry"></a>Пример кода
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

## <a name="next-steps"></a>Дальнейшие действия
* [Создание панели мониторинга](app-insights-dashboards.md)
* [Поиск по журналу диагностики](app-insights-diagnostic-search.md)
* [Изучение метрик](app-insights-metrics-explorer.md)
* [Написание запросов аналитики](app-insights-analytics.md)

