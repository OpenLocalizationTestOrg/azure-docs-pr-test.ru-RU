---
title: "  Публикация содержимого с помощью портала Azure | Документация Майкрософт"
description: "В этом учебнике пошагово описано, как публиковать содержимое с помощью портала Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 68a2fbdda0996cf4ba5ea3b09816bf845af756f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="publish-content-with-the-azure-portal"></a><span data-ttu-id="425df-103">Публикация содержимого с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="425df-103">Publish content with the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="425df-104">Портал</span><span class="sxs-lookup"><span data-stu-id="425df-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="425df-105">.NET</span><span class="sxs-lookup"><span data-stu-id="425df-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="425df-106">REST</span><span class="sxs-lookup"><span data-stu-id="425df-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="425df-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="425df-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="425df-108">Для работы с этим учебником требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="425df-108">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="425df-109">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="425df-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="425df-110">Чтобы предоставить пользователю URL-ссылку, которую можно использовать для потоковой передачи или скачивания содержимого, сначала необходимо "опубликовать" ресурс-контейнер, создав указатель.</span><span class="sxs-lookup"><span data-stu-id="425df-110">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="425df-111">Указатели предоставляют доступ к файлам, содержащимся в активе.</span><span class="sxs-lookup"><span data-stu-id="425df-111">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="425df-112">Службы мультимедиа поддерживают два типа указателей:</span><span class="sxs-lookup"><span data-stu-id="425df-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="425df-113">Указатели потоковой передачи (OnDemandOrigin), используемые для потоковой передачи с переменной скоростью (например, для потоковой передачи в форматах MPEG DASH, HLS или Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="425df-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="425df-114">Чтобы создать указатель потоковой передачи, ресурс должен содержать ISM-файл.</span><span class="sxs-lookup"><span data-stu-id="425df-114">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="425df-115">Последовательные указатели (SAS), используемые для доставки видео путем последовательного скачивания.</span><span class="sxs-lookup"><span data-stu-id="425df-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="425df-116">URL-адрес потоковой передачи имеет следующий формат, и его можно использовать для воспроизведения ресурсов Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="425df-116">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="425df-117">Чтобы создать URL-адрес потоковой передачи HLS, добавьте (format=m3u8-aapl) к URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="425df-117">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="425df-118">Чтобы создать URL-адрес для потоковой передачи в формате MPEG DASH, добавьте к исходному адресу строку (format=mpd-time-csf).</span><span class="sxs-lookup"><span data-stu-id="425df-118">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="425df-119">URL-адрес SAS имеет следующий формат.</span><span class="sxs-lookup"><span data-stu-id="425df-119">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="425df-120">Дополнительные сведения см. в [обзоре доставки содержимого](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="425df-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="425df-121">Для указателей, созданных до марта 2015 года, срок действия составляет два года.</span><span class="sxs-lookup"><span data-stu-id="425df-121">If you used the portal to create locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="425df-122">Чтобы обновить срок действия указателя, используйте [REST API](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) или [.NET API](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="425df-122">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="425df-123">Обратите внимание, что при обновлении срока действия указателя SAS изменяется URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="425df-123">Note that when you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="425df-124">Публикация ресурса с помощью портала</span><span class="sxs-lookup"><span data-stu-id="425df-124">To use the portal to publish an asset</span></span>
<span data-ttu-id="425df-125">Для публикации ресурса с помощью портала выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="425df-125">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="425df-126">Выберите учетную запись служб мультимедиа Azure на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="425df-126">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="425df-127">Установите флажок **Параметры** > **Ресурсы-контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="425df-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="425df-128">Выберите ресурс, который требуется опубликовать.</span><span class="sxs-lookup"><span data-stu-id="425df-128">Select the asset that you want to publish.</span></span>
4. <span data-ttu-id="425df-129">Нажмите кнопку **Опубликовать** .</span><span class="sxs-lookup"><span data-stu-id="425df-129">Click the **Publish** button.</span></span>
5. <span data-ttu-id="425df-130">Выберите тип указателя.</span><span class="sxs-lookup"><span data-stu-id="425df-130">Select the locator type.</span></span>
6. <span data-ttu-id="425df-131">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="425df-131">Press **Add**.</span></span>
   
    ![Опубликовать](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="425df-133">URL-адрес будет добавлен в список **опубликованных URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="425df-133">The URL will be added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="425df-134">Воспроизведение контента на портале</span><span class="sxs-lookup"><span data-stu-id="425df-134">Play content from the portal</span></span>
<span data-ttu-id="425df-135">Портал Azure предлагает проигрыватель содержимого, с помощью которого можно проверить видео.</span><span class="sxs-lookup"><span data-stu-id="425df-135">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="425df-136">Выберите нужное видео и нажмите кнопку **Воспроизвести** .</span><span class="sxs-lookup"><span data-stu-id="425df-136">Click the desired video and then click the **Play** button.</span></span>

![Опубликовать](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="425df-138">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="425df-138">Some considerations apply:</span></span>

* <span data-ttu-id="425df-139">Убедитесь, что видео опубликовано.</span><span class="sxs-lookup"><span data-stu-id="425df-139">Make sure the video has been published.</span></span>
* <span data-ttu-id="425df-140">Этот **проигрыватель мультимедиа** воспроизводит содержимое из конечной точки потоковой передачи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="425df-140">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="425df-141">Если требуется воспроизвести из конечной точки потоковой передачи не по умолчанию, щелкните, чтобы скопировать URL-адрес, и используйте другой проигрыватель.</span><span class="sxs-lookup"><span data-stu-id="425df-141">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="425df-142">Например, [Проигрыватель служб мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="425df-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="425df-143">Конечная точка потоковой передачи, из которой осуществляется потоковая передача, должна быть запущена.</span><span class="sxs-lookup"><span data-stu-id="425df-143">The streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="425df-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="425df-144">Next steps</span></span>
<span data-ttu-id="425df-145">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="425df-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="425df-146">Отзывы</span><span class="sxs-lookup"><span data-stu-id="425df-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

