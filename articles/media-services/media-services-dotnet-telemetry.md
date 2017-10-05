---
title: "Настройка телеметрии служб мультимедиа Azure с использованием .NET | Документация Майкрософт"
description: "В этой статье показано, как использовать телеметрию служб мультимедиа Azure с помощью пакета SDK для .NET."
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
ms.openlocfilehash: 1d857f3d062d8d1b15c64fa4b8c3e27ad6c2247e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="c8f8f-103">Настройка телеметрии служб мультимедиа Azure с использованием .NET</span><span class="sxs-lookup"><span data-stu-id="c8f8f-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="c8f8f-104">В этом разделе описываются общие действия по настройке телеметрии служб мультимедиа Azure (AMS) с помощью пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-104">This topic describes general steps that you might take when configuring the Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="c8f8f-105">Подробнее о том, что такое телеметрия AMS и как ее использовать, описывается в этом[обзоре](media-services-telemetry-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c8f8f-105">For the detailed explanation of what is AMS telemetry and how to consume it, see the [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="c8f8f-106">Данные телеметрии можно использовать одним из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-106">You can consume telemetry data in one of the following ways:</span></span>

- <span data-ttu-id="c8f8f-107">Можно считывать данные непосредственно из хранилища таблиц Azure (например, с помощью пакета SDK для хранилища).</span><span class="sxs-lookup"><span data-stu-id="c8f8f-107">Read data directly from Azure Table Storage (e.g. using the Storage SDK).</span></span> <span data-ttu-id="c8f8f-108">Описание таблиц хранилища телеметрии см. в подразделе **Использование данных телеметрии** [этого](https://msdn.microsoft.com/library/mt742089.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-108">For the description of telemetry storage tables, see the **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="c8f8f-109">Или</span><span class="sxs-lookup"><span data-stu-id="c8f8f-109">Or</span></span>

- <span data-ttu-id="c8f8f-110">Для чтения данных из хранилища можно использовать поддержку, реализованную в пакете SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-110">Use the support in the Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="c8f8f-111">В этом разделе показано, как включить телеметрию для указанной учетной записи AMS и как запросить метрики с помощью пакета SDK служб мультимедиа Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-111">This topic shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="c8f8f-112">Настройка данных телеметрии для учетной записи служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="c8f8f-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="c8f8f-113">Чтобы включить телеметрию, необходимо выполнить следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="c8f8f-113">The following steps are needed to enable telemetry:</span></span>

- <span data-ttu-id="c8f8f-114">Получите учетные данные учетной записи хранения, подключенной к учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-114">Get the credentials of the storage account attached to the Media Services account.</span></span> 
- <span data-ttu-id="c8f8f-115">Создайте конечную точку уведомления, задав для параметра **EndPointType** значение **AzureTable** и указав в качестве адреса endPointAddress таблицу хранилища.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-115">Create a Notification Endpoint with **EndPointType** set to **AzureTable** and endPointAddress pointing to the storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="c8f8f-116">Создайте параметры конфигурации мониторинга служб, которые требуется отслеживать.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-116">Create a monitoring configuration settings for the services you want to monitor.</span></span> <span data-ttu-id="c8f8f-117">Разрешено не более одного параметра конфигурации мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="c8f8f-118">Использование данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="c8f8f-118">Consuming telemetry information</span></span>

<span data-ttu-id="c8f8f-119">Сведения об использовании данных телеметрии см. в [этом](media-services-telemetry-overview.md) разделе.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c8f8f-120">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c8f8f-120">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="c8f8f-121">Настройте среду разработки и укажите в файле app.config сведения о подключении, как описано в статье [Разработка служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c8f8f-121">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

2. <span data-ttu-id="c8f8f-122">Добавьте следующий элемент в **appSettings**, определенный в файле app.config:</span><span class="sxs-lookup"><span data-stu-id="c8f8f-122">Add the following element to **appSettings** defined in your app.config file:</span></span>

    <add key="StorageAccountName" value="storage_name" />
 
## <a name="example"></a><span data-ttu-id="c8f8f-123">Пример</span><span class="sxs-lookup"><span data-stu-id="c8f8f-123">Example</span></span>  
    
<span data-ttu-id="c8f8f-124">В примере ниже показано, как включить телеметрию для указанной учетной записи AMS и запросить метрики с помощью пакета SDK служб мультимедиа Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="c8f8f-124">The following example shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

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

            // Print the channel metrics.
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


## <a name="next-steps"></a><span data-ttu-id="c8f8f-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8f8f-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c8f8f-126">Отзывы</span><span class="sxs-lookup"><span data-stu-id="c8f8f-126">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
