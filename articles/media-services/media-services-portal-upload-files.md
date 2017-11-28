---
title: "AAA» передавать файлы в учетную запись служб мультимедиа с помощью hello портал Azure | Документы Microsoft»"
description: "Этот учебник поможет вам выполнить hello этапы загрузки файлов в учетную запись служб мультимедиа с помощью портала Azure hello"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="596dc-103">Отправка файлов в учетную запись служб мультимедиа с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="596dc-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="596dc-104">Портал</span><span class="sxs-lookup"><span data-stu-id="596dc-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="596dc-105">.NET</span><span class="sxs-lookup"><span data-stu-id="596dc-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="596dc-106">REST</span><span class="sxs-lookup"><span data-stu-id="596dc-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="596dc-107">toocomplete этого учебника необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="596dc-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="596dc-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="596dc-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="596dc-109">В службах мультимедиа цифровые файлы отправляются в актив.</span><span class="sxs-lookup"><span data-stu-id="596dc-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="596dc-110">Hello актива может содержать видео, аудио, изображения, коллекции эскизов, текст отслеживает и титров файлов (и hello метаданные об этих файлах.) После загрузки файлов hello контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="596dc-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="596dc-111">Отправка файлов</span><span class="sxs-lookup"><span data-stu-id="596dc-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="596dc-112">Имеется ограничение toohello максимальный размер файла поддерживается для обработки в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="596dc-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="596dc-113">См. в разделе [это](media-services-quotas-and-limitations.md) сведения о hello ограничения размера файла.</span><span class="sxs-lookup"><span data-stu-id="596dc-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="596dc-114">В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="596dc-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="596dc-115">На hello **параметры** колонка, щелкните **активы**.</span><span class="sxs-lookup"><span data-stu-id="596dc-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![Отправка файлов](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="596dc-117">Нажмите кнопку hello **отправить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="596dc-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="596dc-118">Hello **отправить видео активов** появится окно.</span><span class="sxs-lookup"><span data-stu-id="596dc-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="596dc-119">Размер файлов неограничен.</span><span class="sxs-lookup"><span data-stu-id="596dc-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="596dc-120">Обзор toohello требуемого видео на компьютере, выберите его и нажмите ОК.</span><span class="sxs-lookup"><span data-stu-id="596dc-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="596dc-121">начнется загрузка Hello и следить за ходом hello в файле с именем hello можно.</span><span class="sxs-lookup"><span data-stu-id="596dc-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="596dc-122">После завершения отправки hello, вы увидите новый актив hello, перечисленные в hello **активы** окна.</span><span class="sxs-lookup"><span data-stu-id="596dc-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="596dc-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="596dc-123">Next steps</span></span>
<span data-ttu-id="596dc-124">Теперь можно закодировать отправленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="596dc-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="596dc-125">Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="596dc-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="596dc-126">Также можно использовать функции Azure tootrigger задание кодирования на основе файла, поступающих в контейнере hello настроен.</span><span class="sxs-lookup"><span data-stu-id="596dc-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="596dc-127">Дополнительные сведения см. в [этом примере](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="596dc-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="596dc-128">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="596dc-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="596dc-129">Отзывы</span><span class="sxs-lookup"><span data-stu-id="596dc-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

