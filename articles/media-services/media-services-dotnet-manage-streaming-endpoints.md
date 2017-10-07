---
title: "aaaManage конечные точки с помощью пакета SDK .NET потоковой передачи. | Документация Майкрософт"
description: "В этом разделе показано, как toomanage конечных точек потоковой передачи с hello портал Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 30c092a8ebf4e2b2902392f4cf98f46d812ccdbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="dee7b-104">Управление конечными точками потоковой передачи с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="dee7b-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="dee7b-105">Убедитесь, что hello tooreview [Обзор](media-services-streaming-endpoints-overview.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="dee7b-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="dee7b-106">Просмотрите также статью [Конечная точка потоковой передачи](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="dee7b-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="dee7b-107">Hello кода в этом разделе показано, как hello toodo следующие задачи с помощью hello Azure Media Services .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="dee7b-107">hello code in this topic shows how toodo hello following tasks using hello Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="dee7b-108">Изучите конечной точки потоковой передачи по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="dee7b-108">Examine hello default streaming endpoint.</span></span>
- <span data-ttu-id="dee7b-109">создать и добавить конечную точку потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="dee7b-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="dee7b-110">Вы можете toohave несколько конечных точек потоковой передачи при планировании toohave различных CDN или CDN и прямой доступ.</span><span class="sxs-lookup"><span data-stu-id="dee7b-110">You might want toohave multiple streaming endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dee7b-111">Плата взимается, только когда конечная точка потоковой передачи используется.</span><span class="sxs-lookup"><span data-stu-id="dee7b-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="dee7b-112">Обновление конечной точки потоковой передачи hello.</span><span class="sxs-lookup"><span data-stu-id="dee7b-112">Update hello streaming endpoint.</span></span>
    
    <span data-ttu-id="dee7b-113">Убедитесь, что toocall hello функция Update().</span><span class="sxs-lookup"><span data-stu-id="dee7b-113">Make sure toocall hello Update() function.</span></span>

- <span data-ttu-id="dee7b-114">Удаление конечной точки потоковой передачи hello.</span><span class="sxs-lookup"><span data-stu-id="dee7b-114">Delete hello streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="dee7b-115">не удается удалить конечную точку потоковой передачи по умолчанию Hello.</span><span class="sxs-lookup"><span data-stu-id="dee7b-115">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="dee7b-116">Сведения о том, как tooscale hello конечной точки потоковой передачи см. в разделе [это](media-services-portal-scale-streaming-endpoints.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="dee7b-116">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="dee7b-117">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dee7b-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="dee7b-118">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="dee7b-118">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="dee7b-119">Добавление кода, который управляет конечными точками потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="dee7b-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="dee7b-120">Замените hello код в hello Program.cs hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="dee7b-120">Replace hello code in hello Program.cs with hello following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
            ExamineStreamingEndpoint(defaultStreamingEndpoint);

            IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
            UpdateStreamingEndpoint(newStreamingEndpoint);
            DeleteStreamingEndpoint(newStreamingEndpoint);
        }

        static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            Console.WriteLine(streamingEndpoint.Name);
            Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
            Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
            Console.WriteLine(streamingEndpoint.ScaleUnits);
            Console.WriteLine(streamingEndpoint.CdnProvider);
            Console.WriteLine(streamingEndpoint.CdnProfile);
            Console.WriteLine(streamingEndpoint.CdnEnabled);
        }

        static public IStreamingEndpoint AddStreamingEndpoint()
        {
            var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
            var option = new StreamingEndpointCreationOptions(name, 1)
            {
            StreamingEndpointVersion = new Version("2.0"),
            CdnEnabled = true,
            CdnProfile = "CdnProfile",
            CdnProvider = CdnProviderType.PremiumVerizon
            };

            var streamingEndpoint = _context.StreamingEndpoints.Create(option);

            return streamingEndpoint;
        }

        static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
            streamingEndpoint.StreamingEndpointVersion = "2.0";

            streamingEndpoint.CdnEnabled = false;
            streamingEndpoint.Update();
        }

        static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            streamingEndpoint.Delete();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="dee7b-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dee7b-121">Next steps</span></span>
<span data-ttu-id="dee7b-122">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="dee7b-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dee7b-123">Отзывы</span><span class="sxs-lookup"><span data-stu-id="dee7b-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

