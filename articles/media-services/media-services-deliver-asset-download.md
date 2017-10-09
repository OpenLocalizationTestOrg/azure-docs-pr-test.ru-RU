---
title: "компьютер tooyour активы служб мультимедиа aaaDownload - Azure | Документы Microsoft"
description: "Дополнительные сведения о компьютере tooyour toodownload активы. Примеры кода на языке C# и используйте hello пакета SDK служб мультимедиа для .NET."
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
ms.openlocfilehash: 6c6e764720caa59d8371178a2682700345f7bc57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="2c517-104">Доставка актива путем загрузки</span><span class="sxs-lookup"><span data-stu-id="2c517-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="2c517-105">В этом разделе обсуждаются параметры для доставки мультимедиа отправлен tooMedia служб.</span><span class="sxs-lookup"><span data-stu-id="2c517-105">This topic discusses options for delivering media assets uploaded tooMedia Services.</span></span> <span data-ttu-id="2c517-106">Для доставки контента служб мультимедиа можно использовать различные сценарии.</span><span class="sxs-lookup"><span data-stu-id="2c517-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="2c517-107">Можно загрузить мультимедийные активы или получить к ним доступ с помощью указателя.</span><span class="sxs-lookup"><span data-stu-id="2c517-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="2c517-108">Можно отправить приложение tooanother содержимого мультимедиа или tooanother поставщика содержимого.</span><span class="sxs-lookup"><span data-stu-id="2c517-108">You can send media content tooanother application or tooanother content provider.</span></span> <span data-ttu-id="2c517-109">Для повышения производительности и масштабируемости можно также доставлять контент с помощью сети доставки содержимого (CDN).</span><span class="sxs-lookup"><span data-stu-id="2c517-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="2c517-110">В этом примере показано, как toodownload активы мультимедиа из службы мультимедиа tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="2c517-110">This example shows how toodownload media assets from Media Services tooyour local computer.</span></span> <span data-ttu-id="2c517-111">Hello запросы кода hello заданий, связанных с учетной записью служб мультимедиа hello по Идентификатору задания и обращается к его **OutputMediaAssets** коллекции (то есть набор hello один или несколько мультимедийным активам, полученный в результате выполнения задания).</span><span class="sxs-lookup"><span data-stu-id="2c517-111">hello code queries hello jobs associated with hello Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is hello set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="2c517-112">Этот пример показывает, как носитель вывода toodownload ресурсам с помощью задания, но могут применяться hello же подход toodownload других средств.</span><span class="sxs-lookup"><span data-stu-id="2c517-112">This  example shows how toodownload output media assets from a job, but you can apply hello same approach toodownload other assets.</span></span>

>[!NOTE]
><span data-ttu-id="2c517-113">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="2c517-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="2c517-114">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="2c517-114">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="2c517-115">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="2c517-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download hello output asset of hello specified job tooa local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how toodownload a single asset. 
        // However, you can iterate through hello OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference toohello job. 
        IJob job = GetJob(jobId);

        // Get a reference toohello first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator toodownload hello asset
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
            // Use hello following event handler toocheck download progress.
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="2c517-116">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="2c517-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2c517-117">Отзывы</span><span class="sxs-lookup"><span data-stu-id="2c517-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="2c517-118">См. также</span><span class="sxs-lookup"><span data-stu-id="2c517-118">See Also</span></span>
[<span data-ttu-id="2c517-119">Доставка потокового контента</span><span class="sxs-lookup"><span data-stu-id="2c517-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

