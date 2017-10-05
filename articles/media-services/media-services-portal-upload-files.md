---
title: " Отправка файлов в учетную запись служб мультимедиа с помощью портала Azure | Документация Майкрософт"
description: "В этом руководстве описаны этапы отправки файлов в учетную запись служб мультимедиа Azure с помощью портала Azure."
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
ms.openlocfilehash: 3a1dd7470f940da839687478b636464d930d8ab7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-the-azure-portal"></a><span data-ttu-id="995d2-103">Отправка файлов в учетную запись служб мультимедиа с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="995d2-103">Upload files into a Media Services account using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="995d2-104">Портал</span><span class="sxs-lookup"><span data-stu-id="995d2-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="995d2-105">.NET</span><span class="sxs-lookup"><span data-stu-id="995d2-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="995d2-106">REST</span><span class="sxs-lookup"><span data-stu-id="995d2-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="995d2-107">Для работы с этим учебником требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="995d2-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="995d2-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="995d2-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="995d2-109">В службах мультимедиа цифровые файлы отправляются в актив.</span><span class="sxs-lookup"><span data-stu-id="995d2-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="995d2-110">Ресурс может содержать видео, аудио, изображения, коллекции эскизов, текстовые каналы и файлы скрытых субтитров (и метаданные этих файлов). После отправки этих файлов содержимое сохраняется в безопасном расположении в облаке для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="995d2-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="995d2-111">Отправка файлов</span><span class="sxs-lookup"><span data-stu-id="995d2-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="995d2-112">Существует ограничение на максимальный размер файла, который могут обработать службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="995d2-112">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="995d2-113">Подробные сведения об этом см. [здесь](media-services-quotas-and-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="995d2-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
>

1. <span data-ttu-id="995d2-114">Создание учетной записи служб мультимедиа Azure с помощью [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="995d2-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="995d2-115">В колонке **Параметры** выберите **Ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="995d2-115">On the **Settings** blade, click **Assets**.</span></span>
   
    ![Отправка файлов](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="995d2-117">Нажмите кнопку **Отправить** .</span><span class="sxs-lookup"><span data-stu-id="995d2-117">Click the **Upload** button.</span></span>
   
    <span data-ttu-id="995d2-118">Появится окно **загрузки видеоресурса** .</span><span class="sxs-lookup"><span data-stu-id="995d2-118">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="995d2-119">Размер файлов неограничен.</span><span class="sxs-lookup"><span data-stu-id="995d2-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="995d2-120">Найдите нужное видео на компьютере, выберите его и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="995d2-120">Browse to the desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="995d2-121">Начнется передача. За ходом загрузки можно наблюдать под именем файла.</span><span class="sxs-lookup"><span data-stu-id="995d2-121">The upload starts and you can see the progress under the file name.</span></span>  

<span data-ttu-id="995d2-122">По завершении загрузки в окне **Ресурсы** появится новый ресурс.</span><span class="sxs-lookup"><span data-stu-id="995d2-122">Once the upload completes, you will see the new asset listed in the **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="995d2-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="995d2-123">Next steps</span></span>
<span data-ttu-id="995d2-124">Теперь можно закодировать отправленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="995d2-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="995d2-125">Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="995d2-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="995d2-126">Можно также использовать функции Azure для запуска задания кодирования на основе файла, поступающего в настроенный контейнер.</span><span class="sxs-lookup"><span data-stu-id="995d2-126">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="995d2-127">Дополнительные сведения см. в [этом примере](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="995d2-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="995d2-128">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="995d2-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="995d2-129">Отзывы</span><span class="sxs-lookup"><span data-stu-id="995d2-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

