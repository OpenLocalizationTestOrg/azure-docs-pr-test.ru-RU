---
title: "Скачивание ресурсов служб мультимедиа на компьютер в Azure | Документация Майкрософт"
description: "Инструкции по загрузке ресурсов на компьютер. Примеры кода написаны на языке C# и используют пакет SDK служб мультимедиа для .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: d8e740e969f68c85842f42c109328423da1b4414
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="0e41f-104">Доставка актива путем загрузки</span><span class="sxs-lookup"><span data-stu-id="0e41f-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="0e41f-105">В этом разделе обсуждаются возможности доставки файлов мультимедиа, переданных в службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0e41f-105">This topic discusses options for delivering media assets uploaded to Media Services.</span></span> <span data-ttu-id="0e41f-106">Для доставки контента служб мультимедиа можно использовать различные сценарии.</span><span class="sxs-lookup"><span data-stu-id="0e41f-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="0e41f-107">Можно загрузить мультимедийные активы или получить к ним доступ с помощью указателя.</span><span class="sxs-lookup"><span data-stu-id="0e41f-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="0e41f-108">Можно отправить мультимедийный контент в другое приложение или другой поставщик контента.</span><span class="sxs-lookup"><span data-stu-id="0e41f-108">You can send media content to another application or to another content provider.</span></span> <span data-ttu-id="0e41f-109">Для повышения производительности и масштабируемости можно также доставлять контент с помощью сети доставки содержимого (CDN).</span><span class="sxs-lookup"><span data-stu-id="0e41f-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="0e41f-110">В этом примере показано, как загрузить мультимедийные активы из служб мультимедиа на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="0e41f-110">This example shows how to download media assets from Media Services to your local computer.</span></span> <span data-ttu-id="0e41f-111">Код запрашивает задания, связанные с учетной записью служб мультимедиа, по идентификатору задания и обращается к соответствующей коллекции **OutputMediaAssets** (которая представляет собой набор из одного или нескольких выходных мультимедийных активов, являющихся результатом выполнения задания).</span><span class="sxs-lookup"><span data-stu-id="0e41f-111">The code queries the jobs associated with the Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is the set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="0e41f-112">В этом примере показано, как скачать выходные мультимедийные ресурсы из задания, но этот же метод можно использовать для скачивания и других ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0e41f-112">This  example shows how to download output media assets from a job, but you can apply the same approach to download other assets.</span></span>

>[!NOTE]
><span data-ttu-id="0e41f-113">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="0e41f-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="0e41f-114">Следует указывать один и тот же идентификатор политики, если вы используете те же дни, разрешения доступа и т. д. Например, политики для указателей, которые должны оставаться на месте в течение длительного времени (не политики передачи).</span><span class="sxs-lookup"><span data-stu-id="0e41f-114">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="0e41f-115">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="0e41f-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download the output asset of the specified job to a local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how to download a single asset. 
        // However, you can iterate through the OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference to the job. 
        IJob job = GetJob(jobId);

        // Get a reference to the first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator to download the asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use the following event handler to check download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="0e41f-116">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="0e41f-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0e41f-117">Отзывы</span><span class="sxs-lookup"><span data-stu-id="0e41f-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="0e41f-118">См. также</span><span class="sxs-lookup"><span data-stu-id="0e41f-118">See Also</span></span>
[<span data-ttu-id="0e41f-119">Доставка потокового контента</span><span class="sxs-lookup"><span data-stu-id="0e41f-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

