---
title: "Коды ошибок кодирования служб мультимедиа Azure | Документация Майкрософт"
description: "В этом разделе перечислены коды ошибок, которые могут быть возвращены при возникновении ошибок во время выполнения задачи кодирования."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: f4fd2212d19f89148dde08c75c5a48cdd322d029
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="71949-103">Коды ошибок кодирования</span><span class="sxs-lookup"><span data-stu-id="71949-103">Encoding error codes</span></span>

<span data-ttu-id="71949-104">В следующей таблице перечислены коды ошибок, которые могут быть возвращены при возникновении ошибок во время выполнения задачи кодирования.</span><span class="sxs-lookup"><span data-stu-id="71949-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span></span>  <span data-ttu-id="71949-105">Чтобы получить сведения об ошибке в коде .NET, используйте класс [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) .</span><span class="sxs-lookup"><span data-stu-id="71949-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="71949-106">Чтобы получить сведения об ошибке в коде REST, используйте REST API [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) .</span><span class="sxs-lookup"><span data-stu-id="71949-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="71949-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="71949-107">ErrorDetail.Code</span></span> | <span data-ttu-id="71949-108">Возможные причины ошибки</span><span class="sxs-lookup"><span data-stu-id="71949-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="71949-109">Unknown</span><span class="sxs-lookup"><span data-stu-id="71949-109">Unknown</span></span> |<span data-ttu-id="71949-110">Неизвестная ошибка при выполнении задачи</span><span class="sxs-lookup"><span data-stu-id="71949-110">Unknown error while executing the task</span></span> |
| <span data-ttu-id="71949-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="71949-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="71949-112">Категория ошибок, охватывающая ошибки загрузки входного ресурса, такие как некорректное имя файлов, файлы нулевой длины, неправильное форматирование и т. д.</span><span class="sxs-lookup"><span data-stu-id="71949-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="71949-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="71949-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="71949-114">Категория ошибок, охватывающая проблемы на стороне службы, например проблемы с сетью или хранилищем во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="71949-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="71949-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="71949-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="71949-116">Категория ошибок, в которых задача <see cref="MediaTask.PrivateData"/> (конфигурация) является недопустимой, например: конфигурация не является допустимой конфигурацией системы или содержит недопустимый XML.</span><span class="sxs-lookup"><span data-stu-id="71949-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="71949-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="71949-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="71949-118">Категория ошибок, возникающих во время выполнения задачи, которые могут быть вызваны проблемами во входных файлах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="71949-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span></span> |
| <span data-ttu-id="71949-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="71949-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="71949-120">Категория ошибок, в которой обработчик мультимедиа не может обработать представленные файлы — формат мультимедиа не поддерживается или не соответствует конфигурации.</span><span class="sxs-lookup"><span data-stu-id="71949-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span></span> <span data-ttu-id="71949-121">Например, при попытке получить только звук из ресурса, который содержит видео.</span><span class="sxs-lookup"><span data-stu-id="71949-121">For example, trying to produce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="71949-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="71949-122">ErrorProcessingTask</span></span> |<span data-ttu-id="71949-123">Категория других ошибок обработчика мультимедиа, возникших во время обработки задачи, которые не связаны с содержимым.</span><span class="sxs-lookup"><span data-stu-id="71949-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span></span> |
| <span data-ttu-id="71949-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="71949-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="71949-125">Категория ошибок при отправке выходного ресурса</span><span class="sxs-lookup"><span data-stu-id="71949-125">Category of errors when uploading the output asset</span></span> |
| <span data-ttu-id="71949-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="71949-126">ErrorCancelingTask</span></span> |<span data-ttu-id="71949-127">Категория ошибок, охватывающая ошибки, возникающие при попытке отменить задачу</span><span class="sxs-lookup"><span data-stu-id="71949-127">Category of errors to cover failures when attempting to cancel the Task</span></span> |
| <span data-ttu-id="71949-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="71949-128">TransientError</span></span> |<span data-ttu-id="71949-129">Категория ошибок, охватывающая временные проблемы</span><span class="sxs-lookup"><span data-stu-id="71949-129">Category of errors to cover transient issues (eg.</span></span> <span data-ttu-id="71949-130">(например, временные сетевые проблемы со службой хранилища Azure)</span><span class="sxs-lookup"><span data-stu-id="71949-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="71949-131">Для получения помощи от команды разработчиков для **служб мультимедиа** создайте [запрос в службу поддержки](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="71949-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="71949-132">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="71949-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="71949-133">Отзывы</span><span class="sxs-lookup"><span data-stu-id="71949-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="71949-134">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="71949-134">Related articles</span></span>
* [<span data-ttu-id="71949-135">Выполняйте расширенные задачи кодирования путем настройки предустановок стандартного кодировщика служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="71949-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="71949-136">Квоты и ограничения</span><span class="sxs-lookup"><span data-stu-id="71949-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
