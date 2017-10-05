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
# <a name="how-to-deliver-an-asset-by-download"></a>Доставка актива путем загрузки
В этом разделе обсуждаются возможности доставки файлов мультимедиа, переданных в службы мультимедиа. Для доставки контента служб мультимедиа можно использовать различные сценарии. Можно загрузить мультимедийные активы или получить к ним доступ с помощью указателя. Можно отправить мультимедийный контент в другое приложение или другой поставщик контента. Для повышения производительности и масштабируемости можно также доставлять контент с помощью сети доставки содержимого (CDN).

В этом примере показано, как загрузить мультимедийные активы из служб мультимедиа на локальный компьютер. Код запрашивает задания, связанные с учетной записью служб мультимедиа, по идентификатору задания и обращается к соответствующей коллекции **OutputMediaAssets** (которая представляет собой набор из одного или нескольких выходных мультимедийных активов, являющихся результатом выполнения задания). В этом примере показано, как скачать выходные мультимедийные ресурсы из задания, но этот же метод можно использовать для скачивания и других ресурсов.

>[!NOTE]
>Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy). Следует указывать один и тот же идентификатор политики, если вы используете те же дни, разрешения доступа и т. д. Например, политики для указателей, которые должны оставаться на месте в течение длительного времени (не политики передачи). Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.

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



## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>См. также
[Доставка потокового контента](media-services-deliver-streaming-content.md)

