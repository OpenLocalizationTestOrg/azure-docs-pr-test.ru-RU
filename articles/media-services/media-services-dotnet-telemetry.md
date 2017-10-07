---
title: "aaaConfiguring телеметрии служб мультимедиа Azure с помощью .NET | Документы Microsoft"
description: "В этой статье показано, как toouse hello телеметрии служб мультимедиа Azure с помощью пакета SDK .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f8f55e37-0714-49ea-bf4a-e6c1319bec44
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 4019fa7d080ca3f8a8709bd1e666f7062b883954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="cbe26-103">Настройка телеметрии служб мультимедиа Azure с использованием .NET</span><span class="sxs-lookup"><span data-stu-id="cbe26-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="cbe26-104">В этом разделе описаны общие шаги, которые может потребоваться при настройке телеметрии hello служб мультимедиа Azure (AMS), с помощью пакета SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="cbe26-104">This topic describes general steps that you might take when configuring hello Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="cbe26-105">Для hello подробное объяснение того, что является AMS телеметрии и как tooconsume, разделе hello [Обзор](media-services-telemetry-overview.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="cbe26-105">For hello detailed explanation of what is AMS telemetry and how tooconsume it, see hello [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="cbe26-106">Его можно использовать данные телеметрии в одном из следующих способов hello:</span><span class="sxs-lookup"><span data-stu-id="cbe26-106">You can consume telemetry data in one of hello following ways:</span></span>

- <span data-ttu-id="cbe26-107">Чтение данных непосредственно из табличного хранилища Azure (например, при использовании hello SDK хранилища).</span><span class="sxs-lookup"><span data-stu-id="cbe26-107">Read data directly from Azure Table Storage (e.g. using hello Storage SDK).</span></span> <span data-ttu-id="cbe26-108">Описание hello телеметрии хранилища таблиц см. hello **потребляет данные телеметрии** в [это](https://msdn.microsoft.com/library/mt742089.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="cbe26-108">For hello description of telemetry storage tables, see hello **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="cbe26-109">Или</span><span class="sxs-lookup"><span data-stu-id="cbe26-109">Or</span></span>

- <span data-ttu-id="cbe26-110">Поддержка использования hello в hello Media Services .NET SDK для чтения данных из хранилища.</span><span class="sxs-lookup"><span data-stu-id="cbe26-110">Use hello support in hello Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="cbe26-111">В этом разделе показано, как tooenable данные телеметрии для hello указана учетная запись AMS и как tooquery hello метрик с помощью hello Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="cbe26-111">This topic shows how tooenable telemetry for hello specified AMS account and how tooquery hello metrics using hello Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="cbe26-112">Настройка данных телеметрии для учетной записи служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="cbe26-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="cbe26-113">Hello следующие шаги, необходимые tooenable телеметрии:</span><span class="sxs-lookup"><span data-stu-id="cbe26-113">hello following steps are needed tooenable telemetry:</span></span>

- <span data-ttu-id="cbe26-114">Получите учетные данные hello toohello присоединенного учетной записи хранилища hello учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="cbe26-114">Get hello credentials of hello storage account attached toohello Media Services account.</span></span> 
- <span data-ttu-id="cbe26-115">Создание конечной точки уведомления с **EndPointType** значение слишком**AzureTable** и endPointAddress, указывающим таблицу toohello хранилища.</span><span class="sxs-lookup"><span data-stu-id="cbe26-115">Create a Notification Endpoint with **EndPointType** set too**AzureTable** and endPointAddress pointing toohello storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="cbe26-116">Создание параметров конфигурации мониторинга для hello служб, которые хотите toomonitor.</span><span class="sxs-lookup"><span data-stu-id="cbe26-116">Create a monitoring configuration settings for hello services you want toomonitor.</span></span> <span data-ttu-id="cbe26-117">Разрешено не более одного параметра конфигурации мониторинга.</span><span class="sxs-lookup"><span data-stu-id="cbe26-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="cbe26-118">Использование данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="cbe26-118">Consuming telemetry information</span></span>

<span data-ttu-id="cbe26-119">Сведения об использовании данных телеметрии см. в [этом](media-services-telemetry-overview.md) разделе.</span><span class="sxs-lookup"><span data-stu-id="cbe26-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="cbe26-120">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cbe26-120">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="cbe26-121">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="cbe26-121">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

2. <span data-ttu-id="cbe26-122">Добавьте следующий элемент слишком hello**appSettings** определенной в файле app.config:</span><span class="sxs-lookup"><span data-stu-id="cbe26-122">Add hello following element too**appSettings** defined in your app.config file:</span></span>

    <add key="StorageAccountName" value="storage_name" />
 
## <a name="example"></a><span data-ttu-id="cbe26-123">Пример</span><span class="sxs-lookup"><span data-stu-id="cbe26-123">Example</span></span>  
    
<span data-ttu-id="cbe26-124">Hello в следующем примере показано, как tooenable данные телеметрии для hello указана учетная запись AMS и как tooquery hello метрик с помощью hello Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="cbe26-124">hello following example shows how tooenable telemetry for hello specified AMS account and how tooquery hello metrics using hello Azure Media Services .NET SDK.</span></span>  

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSMetrics
    {
        class Program
        {
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly string _mediaServicesStorageAccountName =
            ConfigurationManager.AppSettings["StorageAccountName"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static IStreamingEndpoint _streamingEndpoint = null;
        private static IChannel _channel = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            _streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            _channel = _context.Channels.FirstOrDefault();

            var monitoringConfigurations = _context.MonitoringConfigurations;
            IMonitoringConfiguration monitoringConfiguration = null;

            // No more than one monitoring configuration settings is allowed.
            if (monitoringConfigurations.ToArray().Length != 0)
            {
            monitoringConfiguration = _context.MonitoringConfigurations.FirstOrDefault();
            }
            else
            {
            INotificationEndPoint notificationEndPoint =
                      _context.NotificationEndPoints.Create("monitoring",
                      NotificationEndPointType.AzureTable, GetTableEndPoint());

            monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
                new List<ComponentMonitoringSetting>()
                {
                    new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                    new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)

                });
            }

            //Print metrics for a Streaming Endpoint.
            PrintStreamingEndpointMetrics();

            Console.ReadLine();
        }

        private static string GetTableEndPoint()
        {
            return "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/";
        }

        private static void PrintStreamingEndpointMetrics()
        {
            Console.WriteLine(string.Format("Telemetry for streaming endpoint '{0}'", _streamingEndpoint.Name));

            DateTime timerangeEnd = DateTime.UtcNow;
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some streaming endpoint metrics.
            var telemetry = _streamingEndpoint.GetTelemetry();

            var res = telemetry.GetStreamingEndpointRequestLogs(timerangeStart, timerangeEnd);

            Console.Title = "Streaming endpoint metrics:";

            foreach (var log in res)
            {
            Console.WriteLine("AccountId: {0}", log.AccountId);
            Console.WriteLine("BytesSent: {0}", log.BytesSent);
            Console.WriteLine("EndToEndLatency: {0}", log.EndToEndLatency);
            Console.WriteLine("HostName: {0}", log.HostName);
            Console.WriteLine("ObservedTime: {0}", log.ObservedTime);
            Console.WriteLine("PartitionKey: {0}", log.PartitionKey);
            Console.WriteLine("RequestCount: {0}", log.RequestCount);
            Console.WriteLine("ResultCode: {0}", log.ResultCode);
            Console.WriteLine("RowKey: {0}", log.RowKey);
            Console.WriteLine("ServerLatency: {0}", log.ServerLatency);
            Console.WriteLine("StatusCode: {0}", log.StatusCode);
            Console.WriteLine("StreamingEndpointId: {0}", log.StreamingEndpointId);
            Console.WriteLine();
            }

            Console.WriteLine();
        }

        private static void PrintChannelMetrics()
        {
            if (_channel == null)
            {
            Console.WriteLine("There are no channels in this AMS account");
            return;
            }

            Console.WriteLine(string.Format("Telemetry for channel '{0}'", _channel.Name));

            DateTime timerangeEnd = DateTime.UtcNow; 
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some channel metrics.
            var telemetry = _channel.GetTelemetry();

            var channelMetrics = telemetry.GetChannelHeartbeats(timerangeStart, timerangeEnd);

            // Print hello channel metrics.
            Console.WriteLine("Channel metrics:");

            foreach (var channelHeartbeat in channelMetrics.OrderBy(x => x.ObservedTime))
            {
            Console.WriteLine(
                "    Observed time: {0}, Last timestamp: {1}, Incoming bitrate: {2}",
                channelHeartbeat.ObservedTime,
                channelHeartbeat.LastTimestamp,
                channelHeartbeat.IncomingBitrate);
            }

            Console.WriteLine();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="cbe26-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cbe26-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cbe26-126">Отзывы</span><span class="sxs-lookup"><span data-stu-id="cbe26-126">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
