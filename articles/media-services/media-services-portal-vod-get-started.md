---
title: "aaaGet работы с доставки VoD, с помощью hello портал Azure | Документы Microsoft"
description: "Этот учебник поможет выполнить шаги hello реализации базовой службы доставки содержимого видео по запросу (VoD) с приложением служб мультимедиа Azure (AMS) с помощью портала Azure hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a><span data-ttu-id="a8c06-103">Приступая к работе с доставки содержимого по требованию с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="a8c06-103">Get started with delivering content on demand using hello Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="a8c06-104">Этот учебник поможет выполнить шаги hello реализации базовой службы доставки содержимого видео по запросу (VoD) с приложением служб мультимедиа Azure (AMS) с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a8c06-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8c06-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a8c06-105">Prerequisites</span></span>
<span data-ttu-id="a8c06-106">Здесь представлены Hello необходимые toocomplete hello учебника:</span><span class="sxs-lookup"><span data-stu-id="a8c06-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="a8c06-107">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a8c06-107">An Azure account.</span></span> <span data-ttu-id="a8c06-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8c06-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="a8c06-109">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a8c06-109">A Media Services account.</span></span> <span data-ttu-id="a8c06-110">toocreate учетную запись служб носителей в разделе [как учетную запись служб мультимедиа tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a8c06-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="a8c06-111">Этот учебник включает hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a8c06-111">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="a8c06-112">Запуск конечной точки потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a8c06-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="a8c06-113">Загрузка видеофайла.</span><span class="sxs-lookup"><span data-stu-id="a8c06-113">Upload a video file.</span></span>
3. <span data-ttu-id="a8c06-114">Кодирование hello исходный файл в набор файлов MP4 с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="a8c06-114">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="a8c06-115">Публикация активов hello и get потоковой передачи и URL-адресов прогрессивной загрузки.</span><span class="sxs-lookup"><span data-stu-id="a8c06-115">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="a8c06-116">Воспроизведение содержимого.</span><span class="sxs-lookup"><span data-stu-id="a8c06-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="a8c06-117">Запуск конечной точки потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="a8c06-117">Start streaming endpoints</span></span> 

<span data-ttu-id="a8c06-118">При работе со службами мультимедиа Azure одним из наиболее распространенных сценариев hello разрабатывает видео через потоковой передачи с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="a8c06-118">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="a8c06-119">Служба Media Services предоставляет динамической упаковки, что позволяет вам toodeliver с адаптивным битрейтом MP4 кодируются содержимого в форматах, поддерживаемых служб мультимедиа (MPEG DASH, HLS, Smooth Streaming) just-in-time, без необходимости toostore упакована заранее потоковой передачи версии каждого из этих форматов потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a8c06-119">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="a8c06-120">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="a8c06-120">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="a8c06-121">Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="a8c06-121">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="a8c06-122">toostart Здравствуйте конечной точки потоковой передачи, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a8c06-122">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="a8c06-123">Войдите на hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a8c06-123">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a8c06-124">В окне "Параметры" hello щелкните конечных точек потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a8c06-124">In hello Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="a8c06-125">Щелкните конечную точку потоковой передачи по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a8c06-125">Click hello default streaming endpoint.</span></span> 

    <span data-ttu-id="a8c06-126">Появится окно Hello по умолчанию потоковая передача сведений о конечной ТОЧКЕ.</span><span class="sxs-lookup"><span data-stu-id="a8c06-126">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="a8c06-127">Щелкните значок запуска hello.</span><span class="sxs-lookup"><span data-stu-id="a8c06-127">Click hello Start icon.</span></span>
5. <span data-ttu-id="a8c06-128">Щелкните toosave кнопку hello сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="a8c06-128">Click hello Save button toosave your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="a8c06-129">Отправка файлов</span><span class="sxs-lookup"><span data-stu-id="a8c06-129">Upload files</span></span>
<span data-ttu-id="a8c06-130">toostream видео с помощью служб мультимедиа Azure, необходимо tooupload hello источник видео, кодировать несколько битрейтов и опубликуйте результат hello.</span><span class="sxs-lookup"><span data-stu-id="a8c06-130">toostream videos using Azure Media Services, you need tooupload hello source videos, encode them into multiple bitrates, and publish hello result.</span></span> <span data-ttu-id="a8c06-131">Первым шагом Hello, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="a8c06-131">hello first step is covered in this section.</span></span> 

1. <span data-ttu-id="a8c06-132">В hello **параметр** окно, нажмите кнопку **активы**.</span><span class="sxs-lookup"><span data-stu-id="a8c06-132">In hello **Setting** window, click **Assets**.</span></span>
   
    ![Отправка файлов](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="a8c06-134">Нажмите кнопку hello **отправить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8c06-134">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="a8c06-135">Hello **отправить видео активов** появится окно.</span><span class="sxs-lookup"><span data-stu-id="a8c06-135">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a8c06-136">Размер файлов неограничен.</span><span class="sxs-lookup"><span data-stu-id="a8c06-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="a8c06-137">Обзор toohello требуемого видео на компьютере, выберите его и нажмите ОК.</span><span class="sxs-lookup"><span data-stu-id="a8c06-137">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="a8c06-138">начнется загрузка Hello и следить за ходом hello в файле с именем hello можно.</span><span class="sxs-lookup"><span data-stu-id="a8c06-138">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="a8c06-139">После завершения отправки hello, можно увидеть новый актив hello, перечисленные в hello **активы** окна.</span><span class="sxs-lookup"><span data-stu-id="a8c06-139">Once hello upload completes, you see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="a8c06-140">Кодирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="a8c06-140">Encode assets</span></span>

<span data-ttu-id="a8c06-141">При работе со службами мультимедиа Azure одним из наиболее распространенных сценариев hello разрабатывает tooyour клиентам потоковой передачи с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="a8c06-141">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="a8c06-142">Службы мультимедиа поддерживают следующие технологии потоковой передачи с адаптивной скоростью hello: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="a8c06-142">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="a8c06-143">tooprepare видео для потоковой передачи с адаптивной скоростью необходимо tooencode источника видео в файлы с разными скоростями.</span><span class="sxs-lookup"><span data-stu-id="a8c06-143">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="a8c06-144">Следует использовать hello **Media Encoder Стандартная** tooencode кодировщик видео.</span><span class="sxs-lookup"><span data-stu-id="a8c06-144">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="a8c06-145">Службы мультимедиа также предоставляют динамическую упаковку, позволяющий toodeliver вашей MP4-файлов с несколькими скоростями в hello следующие форматы потоковой передачи: MPEG DASH, HLS, Smooth Streaming, без необходимости toorepackage в такие форматы потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a8c06-145">Media Services also provides dynamic packaging, which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toorepackage into these streaming formats.</span></span> <span data-ttu-id="a8c06-146">При использовании динамической упаковки достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа создает и обслуживает hello соответствующий ответ на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="a8c06-146">With dynamic packaging, you only need toostore and pay for hello files in single storage format and Media Services builds and serves hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="a8c06-147">tootake преимущества динамической упаковки необходимо tooencode файла исходного кода в набор MP4-файлов с несколькими скоростями (hello кодирования шаги демонстрируются позже в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="a8c06-147">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

### <a name="toouse-hello-portal-tooencode"></a><span data-ttu-id="a8c06-148">портала tooencode toouse hello</span><span class="sxs-lookup"><span data-stu-id="a8c06-148">toouse hello portal tooencode</span></span>
<span data-ttu-id="a8c06-149">В этом разделе описывается hello может занять tooencode свое содержимое в стандартный кодировщик мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a8c06-149">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="a8c06-150">В hello **параметры** выберите **активы**.</span><span class="sxs-lookup"><span data-stu-id="a8c06-150">In hello **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="a8c06-151">В hello **активы** окно, выберите hello активов, желательно tooencode.</span><span class="sxs-lookup"><span data-stu-id="a8c06-151">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
3. <span data-ttu-id="a8c06-152">Нажмите клавишу hello **Encode** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8c06-152">Press hello **Encode** button.</span></span>
4. <span data-ttu-id="a8c06-153">В hello **закодировать ресурс** окно, выберите hello «Стандартный кодировщик мультимедиа» процессор и стиль.</span><span class="sxs-lookup"><span data-stu-id="a8c06-153">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="a8c06-154">Дополнительные сведения о предустановках см. в статьях [Использование стандартной версии кодировщика мультимедиа Azure для автоматического создания схемы скоростей](media-services-autogen-bitrate-ladder-with-mes.md) и [Предустановки задач для Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8c06-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="a8c06-155">Если планируется использовать какие предустановку toocontrol, имейте в виду: важно tooselect hello стиль, лучше всего подходит для ввода видео.</span><span class="sxs-lookup"><span data-stu-id="a8c06-155">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="a8c06-156">Например, если вы знаете, входной видео с разрешением 1920 x 1080 пикселей, затем можно использовать hello «H264 Multiple Bitrate 1080p» стиль.</span><span class="sxs-lookup"><span data-stu-id="a8c06-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="a8c06-157">Если у вас есть видео с низким разрешением (640 x 360), не следует использовать предустановку H264 Multiple Bitrate 1080p.</span><span class="sxs-lookup"><span data-stu-id="a8c06-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="a8c06-158">Чтобы упростить управление имеется возможность редактирования hello имя выходной актив hello и hello имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="a8c06-158">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Кодирование ресурсов](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="a8c06-160">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a8c06-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="a8c06-161">Мониторинг хода выполнения задания кодирования</span><span class="sxs-lookup"><span data-stu-id="a8c06-161">Monitor encoding job progress</span></span>
<span data-ttu-id="a8c06-162">Щелкните toomonitor hello ход выполнения задания кодирования hello **параметры** (вверху hello hello страницы), а затем выберите **задания**.</span><span class="sxs-lookup"><span data-stu-id="a8c06-162">toomonitor hello progress of hello encoding job, click **Settings** (at hello top of hello page) and then select **Jobs**.</span></span>

![Задания](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="a8c06-164">Публикация контента</span><span class="sxs-lookup"><span data-stu-id="a8c06-164">Publish content</span></span>
<span data-ttu-id="a8c06-165">tooprovide на пользователя с URL-адрес, который можно использовать toostream или загрузить содержимое, сначала требуется слишком «публикации» актива путем создания локатора.</span><span class="sxs-lookup"><span data-stu-id="a8c06-165">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="a8c06-166">Локаторы предоставляют доступ toofiles, содержащиеся в ресурсе hello.</span><span class="sxs-lookup"><span data-stu-id="a8c06-166">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="a8c06-167">Службы мультимедиа поддерживают два типа указателей:</span><span class="sxs-lookup"><span data-stu-id="a8c06-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="a8c06-168">Потоковая передача указателей (OnDemandOrigin), используемый для адаптивной потоковой передачи (например, toostream MPEG DASH, HLS или Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="a8c06-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="a8c06-169">toocreate указатель потоковой передачи актива должно содержать ISM-файла.</span><span class="sxs-lookup"><span data-stu-id="a8c06-169">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="a8c06-170">Последовательные указатели (SAS), используемые для доставки видео путем последовательного скачивания.</span><span class="sxs-lookup"><span data-stu-id="a8c06-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="a8c06-171">URL-адрес потоковой передачи имеет следующий формат hello и его можно использовать ресурсы Smooth Streaming tooplay.</span><span class="sxs-lookup"><span data-stu-id="a8c06-171">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="a8c06-172">append toobuild на URL-адрес потоковой передачи HLS (format = m3u8-aapl) toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a8c06-172">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="a8c06-173">Добавление toobuild на URL-адрес потоковой передачи MPEG DASH (формат = mpd время csf) toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a8c06-173">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="a8c06-174">URL-адрес SAS имеет следующий формат hello.</span><span class="sxs-lookup"><span data-stu-id="a8c06-174">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="a8c06-175">Указатели с датой окончания срока действия два года были созданы, при использовании портала toocreate локаторов hello до марта 2015 г.</span><span class="sxs-lookup"><span data-stu-id="a8c06-175">If you used hello portal toocreate locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="a8c06-176">tooupdate дату окончания срока действия на указатель, используйте [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) или [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="a8c06-176">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="a8c06-177">При обновлении срок действия локатора SAS hello изменяет hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a8c06-177">When you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="a8c06-178">toouse hello портала toopublish актива</span><span class="sxs-lookup"><span data-stu-id="a8c06-178">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="a8c06-179">toouse hello портала toopublish актива, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a8c06-179">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="a8c06-180">Установите флажок **Параметры** > **Ресурсы-контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="a8c06-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="a8c06-181">Выберите требуемый toopublish средство hello.</span><span class="sxs-lookup"><span data-stu-id="a8c06-181">Select hello asset that you want toopublish.</span></span>
3. <span data-ttu-id="a8c06-182">Нажмите кнопку hello **публикации** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8c06-182">Click hello **Publish** button.</span></span>
4. <span data-ttu-id="a8c06-183">Выберите тип локатора hello.</span><span class="sxs-lookup"><span data-stu-id="a8c06-183">Select hello locator type.</span></span>
5. <span data-ttu-id="a8c06-184">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a8c06-184">Press **Add**.</span></span>
   
    ![Опубликовать](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="a8c06-186">URL-адрес Hello добавляется список toohello **URL-адреса в опубликованные**.</span><span class="sxs-lookup"><span data-stu-id="a8c06-186">hello URL is added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="a8c06-187">Воспроизведение контента из портала hello</span><span class="sxs-lookup"><span data-stu-id="a8c06-187">Play content from hello portal</span></span>
<span data-ttu-id="a8c06-188">Hello портал Azure предоставляет проигрыватель контента, которые можно использовать tootest видео.</span><span class="sxs-lookup"><span data-stu-id="a8c06-188">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="a8c06-189">Выберите требуемого hello видео и нажмите кнопку hello **воспроизведение** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8c06-189">Click hello desired video and then click hello **Play** button.</span></span>

![Опубликовать](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="a8c06-191">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="a8c06-191">Some considerations apply:</span></span>

* <span data-ttu-id="a8c06-192">toobegin потоковой передачи, запустить выполнение hello **по умолчанию** конечной точки потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a8c06-192">toobegin streaming, start running hello **default** streaming endpoint.</span></span>
* <span data-ttu-id="a8c06-193">Убедитесь, что опубликованный hello видео.</span><span class="sxs-lookup"><span data-stu-id="a8c06-193">Make sure hello video has been published.</span></span>
* <span data-ttu-id="a8c06-194">Это **проигрыватель** воспроизводит контент из конечной точки потоковой передачи по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a8c06-194">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="a8c06-195">Если требуется, чтобы tooplay из не по умолчанию потоковой передачи конечной точки, выберите URL-адрес toocopy hello и используйте другой проигрыватель.</span><span class="sxs-lookup"><span data-stu-id="a8c06-195">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="a8c06-196">Например, [Проигрыватель служб мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="a8c06-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8c06-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8c06-197">Next steps</span></span>
<span data-ttu-id="a8c06-198">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a8c06-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a8c06-199">Отзывы</span><span class="sxs-lookup"><span data-stu-id="a8c06-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

