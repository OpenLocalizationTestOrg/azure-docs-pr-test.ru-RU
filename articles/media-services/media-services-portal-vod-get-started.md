---
title: "Начало работы с доставкой видео по запросу с помощью портала Azure | Документация Майкрософт"
description: "В этом руководстве описано, как реализовать простую службу доставки видео по запросу (VOD) с помощью приложения служб мультимедиа Azure (AMS) и портала Azure."
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
ms.openlocfilehash: a8eeeeff412837acba14b441a3c590edf7e3597a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-the-azure-portal"></a><span data-ttu-id="5af4a-103">Приступая к работе с доставкой содержимого по запросу с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="5af4a-103">Get started with delivering content on demand using the Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="5af4a-104">В этом руководстве описано, как реализовать простую службу доставки видео по запросу (VOD) с помощью приложения служб мультимедиа Azure (AMS) и портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5af4a-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5af4a-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5af4a-105">Prerequisites</span></span>
<span data-ttu-id="5af4a-106">Ниже перечислены необходимые условия для выполнения действий, описанных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5af4a-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="5af4a-107">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="5af4a-107">An Azure account.</span></span> <span data-ttu-id="5af4a-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5af4a-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="5af4a-109">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5af4a-109">A Media Services account.</span></span> <span data-ttu-id="5af4a-110">Инструкции по созданию учетной записи служб мультимедиа см. в статье [Создание учетной записи служб мультимедиа Azure с помощью портала Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="5af4a-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="5af4a-111">Учебник включает в себя следующие разделы:</span><span class="sxs-lookup"><span data-stu-id="5af4a-111">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="5af4a-112">Запуск конечной точки потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="5af4a-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="5af4a-113">Загрузка видеофайла.</span><span class="sxs-lookup"><span data-stu-id="5af4a-113">Upload a video file.</span></span>
3. <span data-ttu-id="5af4a-114">Кодирование исходного файла в набор MP4-файлов с адаптивным битрейтом.</span><span class="sxs-lookup"><span data-stu-id="5af4a-114">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="5af4a-115">Публикация ресурса и получение URL-адресов потоковой передачи и поэтапного скачивания.</span><span class="sxs-lookup"><span data-stu-id="5af4a-115">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="5af4a-116">Воспроизведение содержимого.</span><span class="sxs-lookup"><span data-stu-id="5af4a-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="5af4a-117">Запуск конечной точки потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="5af4a-117">Start streaming endpoints</span></span> 

<span data-ttu-id="5af4a-118">При работе со службами мультимедиа Azure один из самых частых сценариев — потоковая передача видео с переменной скоростью.</span><span class="sxs-lookup"><span data-stu-id="5af4a-118">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="5af4a-119">Службы мультимедиа обеспечивают динамическую упаковку, которая позволяет своевременно доставлять закодированное содержимое MP4-файлов с переменной скоростью в форматах потоковой передачи, которые поддерживаются службами мультимедиа (MPEG DASH, HLS, Smooth Streaming), без необходимости хранения предварительно упакованных версий каждого из этих форматов потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="5af4a-119">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="5af4a-120">При создании учетной записи AMS в нее добавляется конечная точка потоковой передачи **по умолчанию** в состоянии **Остановлена**.</span><span class="sxs-lookup"><span data-stu-id="5af4a-120">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="5af4a-121">Чтобы начать потоковую передачу содержимого и воспользоваться динамической упаковкой и динамическим шифрованием, конечная точка потоковой передачи, из которой необходимо выполнять потоковую передачу содержимого, должна находиться в состоянии **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="5af4a-121">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="5af4a-122">Чтобы запустить конечную точку потоковой передачи, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5af4a-122">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="5af4a-123">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5af4a-123">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5af4a-124">В окне "Параметры" щелкните элемент "Потоковые конечные точки".</span><span class="sxs-lookup"><span data-stu-id="5af4a-124">In the Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="5af4a-125">Щелкните конечную точку потоковой передачи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5af4a-125">Click the default streaming endpoint.</span></span> 

    <span data-ttu-id="5af4a-126">Появится окно сведений о конечной точке потоковой передачи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5af4a-126">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="5af4a-127">Щелкните значок "Пуск".</span><span class="sxs-lookup"><span data-stu-id="5af4a-127">Click the Start icon.</span></span>
5. <span data-ttu-id="5af4a-128">Нажмите кнопку "Сохранить", чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="5af4a-128">Click the Save button to save your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="5af4a-129">Отправка файлов</span><span class="sxs-lookup"><span data-stu-id="5af4a-129">Upload files</span></span>
<span data-ttu-id="5af4a-130">Для потоковой передачи видео с помощью служб мультимедиа Azure необходимо передать и закодировать исходные видео с использованием нескольких скоростей, а затем опубликовать результат.</span><span class="sxs-lookup"><span data-stu-id="5af4a-130">To stream videos using Azure Media Services, you need to upload the source videos, encode them into multiple bitrates, and publish the result.</span></span> <span data-ttu-id="5af4a-131">В этом разделе описан первый шаг.</span><span class="sxs-lookup"><span data-stu-id="5af4a-131">The first step is covered in this section.</span></span> 

1. <span data-ttu-id="5af4a-132">В окне **Параметры** щелкните **Ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="5af4a-132">In the **Setting** window, click **Assets**.</span></span>
   
    ![Отправка файлов](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="5af4a-134">Нажмите кнопку **Отправить** .</span><span class="sxs-lookup"><span data-stu-id="5af4a-134">Click the **Upload** button.</span></span>
   
    <span data-ttu-id="5af4a-135">Появится окно **загрузки видеоресурса** .</span><span class="sxs-lookup"><span data-stu-id="5af4a-135">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5af4a-136">Размер файлов неограничен.</span><span class="sxs-lookup"><span data-stu-id="5af4a-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="5af4a-137">Найдите нужное видео на компьютере, выберите его и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="5af4a-137">Browse to the desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="5af4a-138">Начнется передача. За ходом загрузки можно наблюдать под именем файла.</span><span class="sxs-lookup"><span data-stu-id="5af4a-138">The upload starts and you can see the progress under the file name.</span></span>  

<span data-ttu-id="5af4a-139">По завершении загрузки в окне **Ресурсы-контейнеры** появится новый элемент.</span><span class="sxs-lookup"><span data-stu-id="5af4a-139">Once the upload completes, you see the new asset listed in the **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="5af4a-140">Кодирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="5af4a-140">Encode assets</span></span>

<span data-ttu-id="5af4a-141">При работе со службами мультимедиа Azure один из самых частых сценариев — доставка потоковой передачи с адаптивным битрейтом клиентам.</span><span class="sxs-lookup"><span data-stu-id="5af4a-141">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="5af4a-142">Службы мультимедиа поддерживают следующие технологии потоковой передачи с переменной скоростью: HTTP Live Streaming (HLS), Smooth Streaming и MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="5af4a-142">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="5af4a-143">Чтобы подготовить видео к потоковой передаче с переменной скоростью, необходимо закодировать исходное видео в файлы с поддержкой разных скоростей.</span><span class="sxs-lookup"><span data-stu-id="5af4a-143">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="5af4a-144">Для кодирования этого видео следует использовать **Media Encoder Standard** .</span><span class="sxs-lookup"><span data-stu-id="5af4a-144">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="5af4a-145">Службы мультимедиа также обеспечивают динамическую упаковку, которая позволяет доставлять MP4-файлы с поддержкой нескольких скоростей в форматах потоковой передачи (MPEG DASH, HLS, Smooth Streaming) без необходимости повторной упаковки в эти форматы потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="5af4a-145">Media Services also provides dynamic packaging, which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to repackage into these streaming formats.</span></span> <span data-ttu-id="5af4a-146">Благодаря динамической упаковке вы оплачиваете хранение файлов только в одном формате, так как службы мультимедиа автоматически подготавливают и передают содержимое в нужном формате, исходя из полученных от клиента запросов.</span><span class="sxs-lookup"><span data-stu-id="5af4a-146">With dynamic packaging, you only need to store and pay for the files in single storage format and Media Services builds and serves the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="5af4a-147">Чтобы воспользоваться динамической упаковкой, закодируйте исходный файл в набор MP4-файлов с поддержкой нескольких скоростей (шаги кодирования показаны далее в этом руководстве).</span><span class="sxs-lookup"><span data-stu-id="5af4a-147">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

### <a name="to-use-the-portal-to-encode"></a><span data-ttu-id="5af4a-148">Кодирование с помощью портала</span><span class="sxs-lookup"><span data-stu-id="5af4a-148">To use the portal to encode</span></span>
<span data-ttu-id="5af4a-149">В этом разделе описаны шаги, которые можно предпринять для кодирования содержимого с помощью стандартного кодировщика служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5af4a-149">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="5af4a-150">В окне **Параметры** выберите элемент **Ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="5af4a-150">In the **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="5af4a-151">В окне **Ресурсы-контейнеры** выберите ресурс, который требуется закодировать.</span><span class="sxs-lookup"><span data-stu-id="5af4a-151">In the **Assets** window, select the asset that you would like to encode.</span></span>
3. <span data-ttu-id="5af4a-152">Нажмите кнопку **Кодировать** .</span><span class="sxs-lookup"><span data-stu-id="5af4a-152">Press the **Encode** button.</span></span>
4. <span data-ttu-id="5af4a-153">В окне**кодирования ресурса** выберите обработчик Media Encoder Standard с предустановкой.</span><span class="sxs-lookup"><span data-stu-id="5af4a-153">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="5af4a-154">Дополнительные сведения о предустановках см. в статьях [Использование стандартной версии кодировщика мультимедиа Azure для автоматического создания схемы скоростей](media-services-autogen-bitrate-ladder-with-mes.md) и [Предустановки задач для Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5af4a-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="5af4a-155">Если вы планируете контролировать используемую предустановку кодирования, не забывайте следующее правило: важно выбрать предустановку в соответствии с параметрами входного видео.</span><span class="sxs-lookup"><span data-stu-id="5af4a-155">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="5af4a-156">Например, если известно, что исходное видео имеет разрешение 1920 x 1080 пикселей, можно использовать предустановку "H264 Multiple Bitrate 1080p".</span><span class="sxs-lookup"><span data-stu-id="5af4a-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="5af4a-157">Если у вас есть видео с низким разрешением (640 x 360), не следует использовать предустановку H264 Multiple Bitrate 1080p.</span><span class="sxs-lookup"><span data-stu-id="5af4a-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="5af4a-158">Для упрощения управления предусмотрена возможность изменения имени выходного ресурса и задания.</span><span class="sxs-lookup"><span data-stu-id="5af4a-158">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Кодирование ресурсов](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="5af4a-160">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5af4a-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="5af4a-161">Мониторинг хода выполнения задания кодирования</span><span class="sxs-lookup"><span data-stu-id="5af4a-161">Monitor encoding job progress</span></span>
<span data-ttu-id="5af4a-162">Чтобы отслеживать выполнение задания кодирования, в верхней части страницы щелкните элемент **Параметры**, а затем выберите пункт **Задания**.</span><span class="sxs-lookup"><span data-stu-id="5af4a-162">To monitor the progress of the encoding job, click **Settings** (at the top of the page) and then select **Jobs**.</span></span>

![Задания](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="5af4a-164">Публикация контента</span><span class="sxs-lookup"><span data-stu-id="5af4a-164">Publish content</span></span>
<span data-ttu-id="5af4a-165">Чтобы предоставить пользователю URL-ссылку, которую можно использовать для потоковой передачи или скачивания содержимого, сначала необходимо "опубликовать" ресурс, создав указатель.</span><span class="sxs-lookup"><span data-stu-id="5af4a-165">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="5af4a-166">Указатели предоставляют доступ к файлам, содержащимся в активе.</span><span class="sxs-lookup"><span data-stu-id="5af4a-166">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="5af4a-167">Службы мультимедиа поддерживают два типа указателей:</span><span class="sxs-lookup"><span data-stu-id="5af4a-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="5af4a-168">Указатели потоковой передачи (OnDemandOrigin), используемые для потоковой передачи с переменной скоростью (например, для потоковой передачи в форматах MPEG DASH, HLS или Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="5af4a-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="5af4a-169">Чтобы создать указатель потоковой передачи, ресурс должен содержать ISM-файл.</span><span class="sxs-lookup"><span data-stu-id="5af4a-169">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="5af4a-170">Последовательные указатели (SAS), используемые для доставки видео путем последовательного скачивания.</span><span class="sxs-lookup"><span data-stu-id="5af4a-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="5af4a-171">URL-адрес потоковой передачи имеет следующий формат, и его можно использовать для воспроизведения ресурсов Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="5af4a-171">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="5af4a-172">Чтобы создать URL-адрес потоковой передачи HLS, добавьте (format=m3u8-aapl) к URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="5af4a-172">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="5af4a-173">Чтобы создать URL-адрес для потоковой передачи в формате MPEG DASH, добавьте к исходному адресу строку (format=mpd-time-csf).</span><span class="sxs-lookup"><span data-stu-id="5af4a-173">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="5af4a-174">URL-адрес SAS имеет следующий формат.</span><span class="sxs-lookup"><span data-stu-id="5af4a-174">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="5af4a-175">Для указателей, созданных до марта 2015 года, срок действия составляет два года.</span><span class="sxs-lookup"><span data-stu-id="5af4a-175">If you used the portal to create locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="5af4a-176">Чтобы обновить срок действия указателя, используйте [REST API](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) или [.NET API](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="5af4a-176">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="5af4a-177">При обновлении срока действия указателя SAS URL-адрес изменяется.</span><span class="sxs-lookup"><span data-stu-id="5af4a-177">When you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="5af4a-178">Публикация ресурса с помощью портала</span><span class="sxs-lookup"><span data-stu-id="5af4a-178">To use the portal to publish an asset</span></span>
<span data-ttu-id="5af4a-179">Для публикации ресурса с помощью портала выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5af4a-179">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="5af4a-180">Установите флажок **Параметры** > **Ресурсы-контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="5af4a-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="5af4a-181">Выберите ресурс, который требуется опубликовать.</span><span class="sxs-lookup"><span data-stu-id="5af4a-181">Select the asset that you want to publish.</span></span>
3. <span data-ttu-id="5af4a-182">Нажмите кнопку **Опубликовать** .</span><span class="sxs-lookup"><span data-stu-id="5af4a-182">Click the **Publish** button.</span></span>
4. <span data-ttu-id="5af4a-183">Выберите тип указателя.</span><span class="sxs-lookup"><span data-stu-id="5af4a-183">Select the locator type.</span></span>
5. <span data-ttu-id="5af4a-184">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5af4a-184">Press **Add**.</span></span>
   
    ![Опубликовать](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="5af4a-186">URL-адрес будет добавлен в список **опубликованных URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="5af4a-186">The URL is added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="5af4a-187">Воспроизведение контента на портале</span><span class="sxs-lookup"><span data-stu-id="5af4a-187">Play content from the portal</span></span>
<span data-ttu-id="5af4a-188">Портал Azure предлагает проигрыватель содержимого, с помощью которого можно проверить видео.</span><span class="sxs-lookup"><span data-stu-id="5af4a-188">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="5af4a-189">Выберите нужное видео и нажмите кнопку **Воспроизвести** .</span><span class="sxs-lookup"><span data-stu-id="5af4a-189">Click the desired video and then click the **Play** button.</span></span>

![Опубликовать](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="5af4a-191">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="5af4a-191">Some considerations apply:</span></span>

* <span data-ttu-id="5af4a-192">Чтобы начать потоковую передачу, запустите конечную точку потоковой передачи **по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="5af4a-192">To begin streaming, start running the **default** streaming endpoint.</span></span>
* <span data-ttu-id="5af4a-193">Убедитесь, что видео опубликовано.</span><span class="sxs-lookup"><span data-stu-id="5af4a-193">Make sure the video has been published.</span></span>
* <span data-ttu-id="5af4a-194">Этот **проигрыватель мультимедиа** воспроизводит содержимое из конечной точки потоковой передачи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5af4a-194">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="5af4a-195">Если требуется воспроизвести из конечной точки потоковой передачи не по умолчанию, щелкните, чтобы скопировать URL-адрес, и используйте другой проигрыватель.</span><span class="sxs-lookup"><span data-stu-id="5af4a-195">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="5af4a-196">Например, [Проигрыватель служб мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="5af4a-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5af4a-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5af4a-197">Next steps</span></span>
<span data-ttu-id="5af4a-198">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5af4a-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5af4a-199">Отзывы</span><span class="sxs-lookup"><span data-stu-id="5af4a-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

