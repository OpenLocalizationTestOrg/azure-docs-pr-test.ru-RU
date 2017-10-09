---
title: "кодирование кодов ошибок служб мультимедиа aaaAzure | Документы Microsoft"
description: "В этом разделе перечислены коды ошибок, которые могут быть возвращены в случае, если произошла ошибка во время кодировки выполнения задачи hello..."
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
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="b11a8-103">Коды ошибок кодирования</span><span class="sxs-lookup"><span data-stu-id="b11a8-103">Encoding error codes</span></span>

<span data-ttu-id="b11a8-104">Hello следующей таблице перечислены коды ошибок, которые могут быть возвращены в случае, если произошла ошибка во время hello кодировки выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="b11a8-104">hello following table lists error codes that could be returned in case an error was encountered during hello encoding task execution.</span></span>  <span data-ttu-id="b11a8-105">tooget сведения об ошибке в коде .NET, используйте hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) класса.</span><span class="sxs-lookup"><span data-stu-id="b11a8-105">tooget error details in your .NET code, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="b11a8-106">использовать tooget сведения об ошибке в коде REST hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="b11a8-106">tooget error details in your REST code, use hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="b11a8-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="b11a8-107">ErrorDetail.Code</span></span> | <span data-ttu-id="b11a8-108">Возможные причины ошибки</span><span class="sxs-lookup"><span data-stu-id="b11a8-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="b11a8-109">Unknown</span><span class="sxs-lookup"><span data-stu-id="b11a8-109">Unknown</span></span> |<span data-ttu-id="b11a8-110">Неизвестная ошибка при выполнении задачи hello</span><span class="sxs-lookup"><span data-stu-id="b11a8-110">Unknown error while executing hello task</span></span> |
| <span data-ttu-id="b11a8-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="b11a8-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="b11a8-112">Категория ошибок, охватывающая ошибки загрузки входного ресурса, такие как некорректное имя файлов, файлы нулевой длины, неправильное форматирование и т. д.</span><span class="sxs-lookup"><span data-stu-id="b11a8-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="b11a8-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="b11a8-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="b11a8-114">Категория ошибок, рассматриваются проблемы на стороне службы hello - пример сети или хранилища ошибок при загрузке.</span><span class="sxs-lookup"><span data-stu-id="b11a8-114">Category of errors that covers problems on hello service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="b11a8-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="b11a8-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="b11a8-116">Категория ошибок, где задач <see cref="MediaTask.PrivateData"/> (конфигурация) является недопустимым, например конфигурации hello не является допустимой системы конфигурации, или он содержит недопустимый XML.</span><span class="sxs-lookup"><span data-stu-id="b11a8-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example hello configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="b11a8-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="b11a8-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="b11a8-118">Категория ошибок во время выполнения hello задачу hello, где вопросы внутри hello входных файлов мультимедиа к сбою.</span><span class="sxs-lookup"><span data-stu-id="b11a8-118">Category of errors during hello execution of hello task where issues inside hello input media files cause failure.</span></span> |
| <span data-ttu-id="b11a8-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="b11a8-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="b11a8-120">Категория ошибок, где обработчик мультимедиа hello не удается обработать предоставленных файлах hello - формата media не поддерживается или не соответствует конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="b11a8-120">Category of errors where hello media processor cannot process hello files provided - media format not supported, or does not match hello Configuration.</span></span> <span data-ttu-id="b11a8-121">Например при tooproduce только вывод актив, который содержит только видео</span><span class="sxs-lookup"><span data-stu-id="b11a8-121">For example, trying tooproduce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="b11a8-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="b11a8-122">ErrorProcessingTask</span></span> |<span data-ttu-id="b11a8-123">Во время обработки hello hello задачи, которые связаны toocontent встретится категории других ошибок, которые hello обработчика мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b11a8-123">Category of other errors that hello media processor encounters during hello processing of hello task that are unrelated toocontent.</span></span> |
| <span data-ttu-id="b11a8-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="b11a8-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="b11a8-125">Категория ошибок при передаче hello выходной актив</span><span class="sxs-lookup"><span data-stu-id="b11a8-125">Category of errors when uploading hello output asset</span></span> |
| <span data-ttu-id="b11a8-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="b11a8-126">ErrorCancelingTask</span></span> |<span data-ttu-id="b11a8-127">Категория ошибки toocover сбоев при hello toocancel задач</span><span class="sxs-lookup"><span data-stu-id="b11a8-127">Category of errors toocover failures when attempting toocancel hello Task</span></span> |
| <span data-ttu-id="b11a8-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="b11a8-128">TransientError</span></span> |<span data-ttu-id="b11a8-129">Категория ошибки toocover временных проблем (например)</span><span class="sxs-lookup"><span data-stu-id="b11a8-129">Category of errors toocover transient issues (eg.</span></span> <span data-ttu-id="b11a8-130">(например, временные сетевые проблемы со службой хранилища Azure)</span><span class="sxs-lookup"><span data-stu-id="b11a8-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="b11a8-131">Справка tooget из hello **Media Services** команды, откройте [обращение в службу поддержки](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="b11a8-131">tooget help from hello **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b11a8-132">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b11a8-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b11a8-133">Отзывы</span><span class="sxs-lookup"><span data-stu-id="b11a8-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="b11a8-134">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="b11a8-134">Related articles</span></span>
* [<span data-ttu-id="b11a8-135">Выполняйте расширенные задачи кодирования путем настройки предустановок стандартного кодировщика служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b11a8-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="b11a8-136">Квоты и ограничения</span><span class="sxs-lookup"><span data-stu-id="b11a8-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
