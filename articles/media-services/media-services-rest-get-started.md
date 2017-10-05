---
title: "Приступая к работе с доставкой содержимого по запросу с помощью REST | Документация Майкрософт"
description: "В этом учебнике показаны шаги по реализации приложения доставки содержимого по запросу с помощью служб мультимедиа и API REST"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f304f7671465862123f64c8b0f9af95a7c828cc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="f9c93-103">Начало работы с доставкой содержимого по запросу с помощью REST</span><span class="sxs-lookup"><span data-stu-id="f9c93-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="f9c93-104">В этом кратком руководстве приведены пошаговые инструкции по реализации приложения доставки видео по запросу с помощью служб мультимедиа (AMS) Azure с использованием REST API.</span><span class="sxs-lookup"><span data-stu-id="f9c93-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="f9c93-105">В учебнике описывается базовый рабочий процесс служба мультимедиа и наиболее распространенные объекты и задачи программирования, необходимые для разработки с использованием служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f9c93-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="f9c93-106">По завершении работы с учебником вы сможете выполнить потоковую передачу и поэтапно скачать пример файла мультимедиа, который вы отправили, закодировали и скачали.</span><span class="sxs-lookup"><span data-stu-id="f9c93-106">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="f9c93-107">На следующем рисунке показаны некоторые объекты, которые чаще всего используются при разработке приложений VoD с использованием модели OData служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f9c93-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="f9c93-108">Щелкните изображение, чтобы просмотреть его полноразмерную версию.</span><span class="sxs-lookup"><span data-stu-id="f9c93-108">Click the image to view it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="f9c93-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f9c93-109">Prerequisites</span></span>
<span data-ttu-id="f9c93-110">Для начала разработки с помощью REST API служб мультимедиа необходимо выполнить следующие предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="f9c93-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="f9c93-111">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c93-111">An Azure account.</span></span> <span data-ttu-id="f9c93-112">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9c93-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f9c93-113">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f9c93-113">A Media Services account.</span></span> <span data-ttu-id="f9c93-114">Инструкции по созданию учетной записи служб мультимедиа см. в статье [Создание учетной записи служб мультимедиа Azure с помощью портала Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="f9c93-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="f9c93-115">Основная информация о разработке с помощью REST API служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f9c93-115">Understanding of how to develop with Media Services REST API.</span></span> <span data-ttu-id="f9c93-116">Дополнительные сведения см. в статье [Обзор REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f9c93-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="f9c93-117">Выбранное вами приложение, способное отправлять HTTP-запросы и ответы.</span><span class="sxs-lookup"><span data-stu-id="f9c93-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="f9c93-118">В этом учебнике используется [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="f9c93-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="f9c93-119">В этом кратком руководстве показаны следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="f9c93-119">The following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="f9c93-120">Запуск конечных точек потоковой передачи с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="f9c93-120">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="f9c93-121">Подключение к учетной записи служб мультимедиа с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="f9c93-121">Connect to the Media Services account with REST API.</span></span>
3. <span data-ttu-id="f9c93-122">Создание нового ресурса и отправка видеофайла с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="f9c93-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="f9c93-123">Кодирование исходного файла в набор MP4-файлов с адаптивной скоростью с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="f9c93-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="f9c93-124">Публикация актива и получение URL-адресов потоковой передачи и поэтапного скачивания с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="f9c93-124">Publish the asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="f9c93-125">Воспроизведение содержимого.</span><span class="sxs-lookup"><span data-stu-id="f9c93-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="f9c93-126">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="f9c93-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="f9c93-127">Следует указывать один и тот же идентификатор политики, если вы используете те же дни, разрешения доступа и т. д. Например, политики для указателей, которые должны оставаться на месте в течение длительного времени (не политики передачи).</span><span class="sxs-lookup"><span data-stu-id="f9c93-127">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="f9c93-128">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="f9c93-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="f9c93-129">Дополнительные сведения о сущностях AMS REST, используемых в этом разделе, см. в статье [Справочник по интерфейсу API REST служб мультимедиа Azure](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="f9c93-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="f9c93-130">См. также статью [Основные понятия служб мультимедиа Azure](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="f9c93-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="f9c93-131">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="f9c93-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="f9c93-132">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f9c93-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="f9c93-133">Запуск конечных точек потоковой передачи с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="f9c93-133">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="f9c93-134">При работе со службами мультимедиа Azure один из самых частых сценариев — потоковая передача видео с переменной скоростью.</span><span class="sxs-lookup"><span data-stu-id="f9c93-134">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="f9c93-135">Службы мультимедиа обеспечивают динамическую упаковку, которая позволяет своевременно доставлять закодированное содержимое MP4-файлов с переменной скоростью в форматах потоковой передачи, которые поддерживаются службами мультимедиа (MPEG DASH, HLS, Smooth Streaming), без необходимости хранения предварительно упакованных версий каждого из этих форматов потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="f9c93-135">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="f9c93-136">При создании учетной записи AMS в нее добавляется конечная точка потоковой передачи **по умолчанию** в состоянии **Остановлена**.</span><span class="sxs-lookup"><span data-stu-id="f9c93-136">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="f9c93-137">Чтобы начать потоковую передачу содержимого и воспользоваться динамической упаковкой и динамическим шифрованием, конечная точка потоковой передачи, из которой необходимо выполнять потоковую передачу содержимого, должна находиться в состоянии **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="f9c93-137">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="f9c93-138">Чтобы запустить конечную точку потоковой передачи, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f9c93-138">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="f9c93-139">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f9c93-139">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f9c93-140">В окне "Параметры" щелкните элемент "Потоковые конечные точки".</span><span class="sxs-lookup"><span data-stu-id="f9c93-140">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="f9c93-141">Щелкните конечную точку потоковой передачи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f9c93-141">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="f9c93-142">Появится окно сведений о конечной точке потоковой передачи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f9c93-142">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="f9c93-143">Щелкните значок "Пуск".</span><span class="sxs-lookup"><span data-stu-id="f9c93-143">Click the Start icon.</span></span>
5. <span data-ttu-id="f9c93-144">Нажмите кнопку "Сохранить", чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="f9c93-144">Click the Save button to save your changes.</span></span>

## <span data-ttu-id="f9c93-145"><a id="connect"></a>Подключение к учетной записи служб мультимедиа с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="f9c93-145"><a id="connect"></a>Connect to the Media Services account with REST API</span></span>

<span data-ttu-id="f9c93-146">Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="f9c93-146">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="f9c93-147">После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f9c93-147">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="f9c93-148">Используйте для последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="f9c93-148">You must make subsequent calls to the new URI.</span></span>

<span data-ttu-id="f9c93-149">Например, если после попытки подключения вы получите следующее:</span><span class="sxs-lookup"><span data-stu-id="f9c93-149">For example, if after trying to connect, you got the following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="f9c93-150">Отправляйте последующие вызовы API на адрес https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="f9c93-150">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="f9c93-151"><a id="upload"></a>Создание нового актива и отправка видеофайла с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="f9c93-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="f9c93-152">В службах мультимедиа цифровые файлы отправляются в актив.</span><span class="sxs-lookup"><span data-stu-id="f9c93-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="f9c93-153">Сущность **Asset** может содержать видео, аудио, изображения, коллекции эскизов, текстовые дорожки и файлы скрытых субтитров (а также метаданные этих файлов).  После отправки этих файлов в ресурс содержимое сохраняется в безопасном расположении в облаке для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="f9c93-153">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="f9c93-154">При создании ресурса нужно, в частности, указать параметры его создания.</span><span class="sxs-lookup"><span data-stu-id="f9c93-154">One of the values that you have to provide when creating an asset is asset creation options.</span></span> <span data-ttu-id="f9c93-155">Значение свойства **Options** — это значение перечисления, описывающее параметры шифрования, которые могут использоваться при создании сущности Asset.</span><span class="sxs-lookup"><span data-stu-id="f9c93-155">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="f9c93-156">Допустимые значения перечислены ниже (допустимы только сами значения, а не их сочетания).</span><span class="sxs-lookup"><span data-stu-id="f9c93-156">A valid value is one of the values from the list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="f9c93-157">**None** = **0**. Шифрование не используется.</span><span class="sxs-lookup"><span data-stu-id="f9c93-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="f9c93-158">При использовании этого параметра содержимое не защищено при передаче и хранении.</span><span class="sxs-lookup"><span data-stu-id="f9c93-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="f9c93-159">Используйте этот параметр, если MP4-файл планируется доставить с помощью поэтапного скачивания.</span><span class="sxs-lookup"><span data-stu-id="f9c93-159">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="f9c93-160">**StorageEncrypted** = **1**. Незашифрованное содержимое шифруется локально с помощью 256-разрядного алгоритма шифрования AES-256, а затем отправляется в службу хранилища Azure, где оно хранится в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="f9c93-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="f9c93-161">Активы, защищенные с помощью шифрования хранилища, автоматически расшифровываются и помещаются в систему зашифрованных файлов до кодирования и при необходимости повторно кодируются до отправки в виде нового выходного актива.</span><span class="sxs-lookup"><span data-stu-id="f9c93-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="f9c93-162">Шифрование хранилища чаще всего используется, если нужно защитить входные файлы мультимедиа высокого качества с помощью стойкого шифрования при хранении на диске.</span><span class="sxs-lookup"><span data-stu-id="f9c93-162">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="f9c93-163">**CommonEncryptionProtected** = **2**. Используйте этот параметр при отправке содержимого, которое уже зашифровано и защищено с помощью стандартного шифрования или PlayReady DRM (например, Smooth Streaming с защитой PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="f9c93-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="f9c93-164">**EnvelopeEncryptionProtected** = **4**. Используйте этот параметр при отправке HLS с шифрованием AES.</span><span class="sxs-lookup"><span data-stu-id="f9c93-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="f9c93-165">Файлы должны быть закодированы и зашифрованы с помощью Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="f9c93-165">The files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="f9c93-166">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="f9c93-166">Create an asset</span></span>
<span data-ttu-id="f9c93-167">Ресурс — это контейнер, состоящий из нескольких наборов объектов или объектов разного типа в службах мультимедиа, в том числе видео, аудио, изображения, коллекции отпечатков, текстовые каналы и файлы скрытых субтитров.</span><span class="sxs-lookup"><span data-stu-id="f9c93-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="f9c93-168">Для создания ресурса в REST API нужно отправить запрос POST службам мультимедиа и разместить любую информацию о свойствах ресурса в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="f9c93-168">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="f9c93-169">В следующем примере показано, как создать ресурс.</span><span class="sxs-lookup"><span data-stu-id="f9c93-169">The following example shows how to create an asset.</span></span>

<span data-ttu-id="f9c93-170">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-170">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="f9c93-171">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-171">**HTTP Response**</span></span>

<span data-ttu-id="f9c93-172">При успешном выполнении возвращается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="f9c93-172">If successful, the following is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="f9c93-173">Создание сущности AssetFile</span><span class="sxs-lookup"><span data-stu-id="f9c93-173">Create an AssetFile</span></span>
<span data-ttu-id="f9c93-174">Сущность [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) представляет собой аудио- или видеофайл, который хранится в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f9c93-174">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="f9c93-175">Файл ресурса всегда связан с ресурсом, который, в свою очередь, может содержать одну или несколько сущностей AssetFile.</span><span class="sxs-lookup"><span data-stu-id="f9c93-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="f9c93-176">Задача кодировщика служб мультимедиа завершится с ошибкой, если объект файла ресурса не связан с цифровым файлом в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="f9c93-176">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="f9c93-177">После отправки цифрового файла мультимедиа в контейнер больших двоичных объектов используйте HTTP-запрос **MERGE** , чтобы обновить сущность AssetFile информацией о файле мультимедиа (как показано далее в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="f9c93-177">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span>

<span data-ttu-id="f9c93-178">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-178">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="f9c93-179">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-179">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="f9c93-180">Создание сущности AccessPolicy с разрешением на запись</span><span class="sxs-lookup"><span data-stu-id="f9c93-180">Creating the AccessPolicy with write permission</span></span>
<span data-ttu-id="f9c93-181">Перед отправкой файлов в хранилище больших двоичных объектов настройте для политики доступа права на запись в ресурс.</span><span class="sxs-lookup"><span data-stu-id="f9c93-181">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="f9c93-182">Для этого отправьте запрос HTTP POST в набор сущностей AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="f9c93-182">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="f9c93-183">При создании сущности необходимо задать значение DurationInMinutes. В противном случае вы получите сообщение 500 (внутренняя ошибка сервера).</span><span class="sxs-lookup"><span data-stu-id="f9c93-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="f9c93-184">Дополнительную информацию о сущностях AccessPolicy см. в разделе [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="f9c93-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="f9c93-185">В следующем примере показано, как создать AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="f9c93-185">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="f9c93-186">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-186">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="f9c93-187">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-187">**HTTP Response**</span></span>

<span data-ttu-id="f9c93-188">При успешном выполнении возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="f9c93-188">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-the-upload-url"></a><span data-ttu-id="f9c93-189">Получение URL-адреса отправки</span><span class="sxs-lookup"><span data-stu-id="f9c93-189">Get the Upload URL</span></span>

<span data-ttu-id="f9c93-190">Чтобы получить фактический URL-адрес отправки, создайте указатель SAS.</span><span class="sxs-lookup"><span data-stu-id="f9c93-190">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="f9c93-191">Указатели определяют время начала и тип конечной точки подключения для клиентов, которым требуется доступ к файлам в ресурсе.</span><span class="sxs-lookup"><span data-stu-id="f9c93-191">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="f9c93-192">Для обработки разных запросов клиентов и удовлетворения их потребностей можно создать несколько сущностей Locator для заданной пары AccessPolicy и Asset.</span><span class="sxs-lookup"><span data-stu-id="f9c93-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="f9c93-193">Каждый из этих указателей использует значения StartTime и DurationInMinutes сущности AccessPolicy, чтобы определить время, в течение которого можно использовать URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="f9c93-193">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="f9c93-194">Дополнительную информацию см. в разделе [Указатель](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="f9c93-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="f9c93-195">Ниже приведен формат URL-адреса SAS:</span><span class="sxs-lookup"><span data-stu-id="f9c93-195">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="f9c93-196">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="f9c93-196">Some considerations apply:</span></span>

* <span data-ttu-id="f9c93-197">С определенным ресурсом нельзя связать более пяти уникальных указателей одновременно.</span><span class="sxs-lookup"><span data-stu-id="f9c93-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="f9c93-198">Дополнительную информацию см. в разделе "Указатель".</span><span class="sxs-lookup"><span data-stu-id="f9c93-198">For more information, see Locator.</span></span>
* <span data-ttu-id="f9c93-199">Если вам необходимо незамедлительно передать файлы, следует задать для StartTime значение, на пять минут предшествующее текущему моменту времени.</span><span class="sxs-lookup"><span data-stu-id="f9c93-199">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="f9c93-200">Это необходимо из-за возможного расхождения в показаниях часов на клиентском компьютере и в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f9c93-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="f9c93-201">Кроме того, значение StartTime должно быть задано в следующем формате даты и времени: ГГГГ-ММ-ДДТЧЧ:мм:ссZ (например, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="f9c93-201">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="f9c93-202">Задержка между моментом создания сущности Locator и моментом, когда ее можно начинать использовать, может составлять 30-40 секунд.</span><span class="sxs-lookup"><span data-stu-id="f9c93-202">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="f9c93-203">Это касается URL-адресов SAS и исходных указателей.</span><span class="sxs-lookup"><span data-stu-id="f9c93-203">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="f9c93-204">Дополнительные сведения об указателях SAS см. в [этой](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) записи блога.</span><span class="sxs-lookup"><span data-stu-id="f9c93-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="f9c93-205">В следующем примере показано, как создать указатель URL-адреса SAS в соответствии со значением свойства Type в тексте запроса (1 для указателя SAS и 2 для исходного указателя по требованию).</span><span class="sxs-lookup"><span data-stu-id="f9c93-205">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="f9c93-206">Возвращенное свойство **Path** содержит URL-адрес, который необходимо использовать для отправки файла.</span><span class="sxs-lookup"><span data-stu-id="f9c93-206">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="f9c93-207">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-207">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="f9c93-208">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-208">**HTTP Response**</span></span>

<span data-ttu-id="f9c93-209">При успешном выполнении возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="f9c93-209">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="f9c93-210">Отправка файла в контейнер хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="f9c93-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="f9c93-211">Когда сущности AccessPolicy и Locator будут заданы, фактические файлы отправляются в контейнер хранилища BLOB-объектов Azure с помощью интерфейсов REST API службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c93-211">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="f9c93-212">Файлы необходимо отправить в виде блочных BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="f9c93-212">You must upload the files as block blobs.</span></span> <span data-ttu-id="f9c93-213">Страничные BLOB-объекты не поддерживаются службами мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c93-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="f9c93-214">Нужно добавить имя файла для файла, который необходимо передать, в значение **Path** сущности Locator, полученное в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="f9c93-214">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="f9c93-215">Например, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="f9c93-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="f9c93-216">.</span><span class="sxs-lookup"><span data-stu-id="f9c93-216">.</span></span> <span data-ttu-id="f9c93-217">.</span><span class="sxs-lookup"><span data-stu-id="f9c93-217">.</span></span> <span data-ttu-id="f9c93-218">.</span><span class="sxs-lookup"><span data-stu-id="f9c93-218">.</span></span>
>
>

<span data-ttu-id="f9c93-219">Дополнительную информацию о работе с большими двоичными объектами службы хранилища Azure см. в статье [API-интерфейс REST службы BLOB-объектов](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="f9c93-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="f9c93-220">Обновление AssetFile</span><span class="sxs-lookup"><span data-stu-id="f9c93-220">Update the AssetFile</span></span>
<span data-ttu-id="f9c93-221">После отправки файла обновите информацию о размере сущности FileAsset (и другую информацию).</span><span class="sxs-lookup"><span data-stu-id="f9c93-221">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="f9c93-222">Например:</span><span class="sxs-lookup"><span data-stu-id="f9c93-222">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="f9c93-223">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-223">**HTTP Response**</span></span>

<span data-ttu-id="f9c93-224">При успешном выполнении возвращается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="f9c93-224">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="f9c93-225">Удаление Locator и AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="f9c93-225">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="f9c93-226">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="f9c93-227">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-227">**HTTP Response**</span></span>

<span data-ttu-id="f9c93-228">При успешном выполнении возвращается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="f9c93-228">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="f9c93-229">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="f9c93-230">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-230">**HTTP Response**</span></span>

<span data-ttu-id="f9c93-231">При успешном выполнении возвращается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="f9c93-231">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="f9c93-232"><a id="encode"></a>Кодирование исходного файла в набор MP4-файлов с адаптивным битрейтом</span><span class="sxs-lookup"><span data-stu-id="f9c93-232"><a id="encode"></a>Encode the source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="f9c93-233">После приема активов в службы мультимедиа файлы мультимедиа можно кодировать, менять их формат, добавлять водяные знаки и т. д. до их доставки клиентам.</span><span class="sxs-lookup"><span data-stu-id="f9c93-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="f9c93-234">Эти действия запланированы и выполняются в нескольких экземплярах фоновых ролей для обеспечения высокой производительности и доступности.</span><span class="sxs-lookup"><span data-stu-id="f9c93-234">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="f9c93-235">Эти действия называются заданиями, и каждое задание состоит из атомарных задач, которые выполняют фактическую работу с файлом ресурса-контейнера (дополнительные сведения см. в описаниях [заданий](/rest/api/media/services/job) и [задач](/rest/api/media/services/task)).</span><span class="sxs-lookup"><span data-stu-id="f9c93-235">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="f9c93-236">Как было упомянуто ранее, при работе со службами мультимедиа Azure один из наиболее распространенных сценариев — доставка потоковой передачи с адаптивным битрейтом клиентам.</span><span class="sxs-lookup"><span data-stu-id="f9c93-236">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="f9c93-237">Службы мультимедиа могут динамически упаковывать набор MP4-файлов с переменной скоростью в один из следующих форматов: HTTP Live Streaming (HLS), Smooth Streaming и MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="f9c93-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="f9c93-238">Ниже показано, как создать задание, содержащее одну задачу кодирования.</span><span class="sxs-lookup"><span data-stu-id="f9c93-238">The following section shows how to create a job that contains one encoding task.</span></span> <span data-ttu-id="f9c93-239">Эта задача задает перекодирование мезонинного файла в набор MP4-файлов с адаптивной скоростью с помощью **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="f9c93-239">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="f9c93-240">В данном разделе также показано, как отслеживать ход выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="f9c93-240">The section also shows how to monitor the job processing progress.</span></span> <span data-ttu-id="f9c93-241">После завершения задания можно будет создавать указатели, которые необходимы для получения доступа к ресурсам-контейнерам.</span><span class="sxs-lookup"><span data-stu-id="f9c93-241">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="f9c93-242">Получение обработчика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="f9c93-242">Get a media processor</span></span>
<span data-ttu-id="f9c93-243">В службах мультимедиа обработчик мультимедиа — это компонент, который работает со специфическими задачами обработки, такими как кодирование, преобразование формата, шифрование или расшифровка мультимедийного содержимого.</span><span class="sxs-lookup"><span data-stu-id="f9c93-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="f9c93-244">Для задачи кодирования, продемонстрированной в данном руководстве, будет использоваться Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="f9c93-244">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span></span>

<span data-ttu-id="f9c93-245">Следующий код запрашивает идентификатор кодировщика.</span><span class="sxs-lookup"><span data-stu-id="f9c93-245">The following code requests the encoder's id.</span></span>

<span data-ttu-id="f9c93-246">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="f9c93-247">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-247">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="f9c93-248">Создание задания</span><span class="sxs-lookup"><span data-stu-id="f9c93-248">Create a job</span></span>
<span data-ttu-id="f9c93-249">Каждое задание может состоять из одной или нескольких задач в зависимости от типа обработки, которую необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="f9c93-249">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="f9c93-250">Задания и связанные с ними задачи можно создавать через REST API двумя способами: задачи можно определять прямо в сущностях Job в свойстве навигации задач или через пакетную обработку по протоколу OData.</span><span class="sxs-lookup"><span data-stu-id="f9c93-250">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="f9c93-251">Пакет SDK для служб мультимедиа использует пакетную обработку.</span><span class="sxs-lookup"><span data-stu-id="f9c93-251">The Media Services SDK uses batch processing.</span></span> <span data-ttu-id="f9c93-252">Тем не менее для удобства чтения в этом разделе задачи определены прямо в тексте примеров кода.</span><span class="sxs-lookup"><span data-stu-id="f9c93-252">However, for the readability of the code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="f9c93-253">Чтобы узнать больше о пакетной обработке, ознакомьтесь с [пакетной обработкой посредством протокола OData](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="f9c93-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="f9c93-254">В следующем примере показано, как создать и опубликовать задание с одной задачей, предназначенной для кодирования видео с определенным разрешением и качеством.</span><span class="sxs-lookup"><span data-stu-id="f9c93-254">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="f9c93-255">Следующий раздел документации содержит список всех [предустановок задач](http://msdn.microsoft.com/library/mt269960) , поддерживаемых обработчиком Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="f9c93-255">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span></span>  

<span data-ttu-id="f9c93-256">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-256">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="f9c93-257">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-257">**HTTP Response**</span></span>

<span data-ttu-id="f9c93-258">При успешном выполнении возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="f9c93-258">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="f9c93-259">При создании любого запроса задания необходимо учитывать несколько важных моментов.</span><span class="sxs-lookup"><span data-stu-id="f9c93-259">There are a few important things to note in any Job request:</span></span>

* <span data-ttu-id="f9c93-260">Чтобы определить количество входных или выходных ресурсов, используемых задачей, в свойствах TaskBody НЕОБХОДИМО использовать XML-литерал.</span><span class="sxs-lookup"><span data-stu-id="f9c93-260">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span></span> <span data-ttu-id="f9c93-261">В статье "Задача" приведено определение схемы XML.</span><span class="sxs-lookup"><span data-stu-id="f9c93-261">The Task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="f9c93-262">В определении TaskBody каждое внутреннее значение <inputAsset> и <outputAsset> необходимо установить как JobInputAsset(value) или JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="f9c93-262">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="f9c93-263">В задаче может содержаться несколько выходных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f9c93-263">A task can have multiple output assets.</span></span> <span data-ttu-id="f9c93-264">Значение JobOutputAsset(x) может использоваться только один раз в качестве выходных данных задачи в задании.</span><span class="sxs-lookup"><span data-stu-id="f9c93-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="f9c93-265">В качестве входного ресурса задачи можно указать JobInputAsset или JobOutputAsset.</span><span class="sxs-lookup"><span data-stu-id="f9c93-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="f9c93-266">Задачи не должны образовывать цикл.</span><span class="sxs-lookup"><span data-stu-id="f9c93-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="f9c93-267">Значение параметра, которое передается в JobInputAsset или JobOutputAsset, — это значение индекса для ресурса.</span><span class="sxs-lookup"><span data-stu-id="f9c93-267">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span></span> <span data-ttu-id="f9c93-268">Фактические ресурсы определяются в свойствах навигации ресурсов InputMediaAsset и OutputMediaAsset в определении сущности Job.</span><span class="sxs-lookup"><span data-stu-id="f9c93-268">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c93-269">Так как службы мультимедиа созданы на платформе OData версии 3, ссылки на отдельные ресурсы в коллекциях свойств навигации ресурсов InputMediaAsset и OutputMediaAsset добавляются в виде пары "имя-значение" __metadata: uri.</span><span class="sxs-lookup"><span data-stu-id="f9c93-269">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="f9c93-270">Ресурсы InputMediaAsset сопоставляются с одним или несколькими ресурсами, созданными в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f9c93-270">InputMediaAssets maps to one or more Assets you have created in Media Services.</span></span> <span data-ttu-id="f9c93-271">Ресурсы OutputMediaAsset создаются системой.</span><span class="sxs-lookup"><span data-stu-id="f9c93-271">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="f9c93-272">Они не ссылаются на существующий ресурс.</span><span class="sxs-lookup"><span data-stu-id="f9c93-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="f9c93-273">Ресурсам OutputMediaAsset можно присвоить имя с помощью атрибута assetName.</span><span class="sxs-lookup"><span data-stu-id="f9c93-273">OutputMediaAssets can be named using the assetName attribute.</span></span> <span data-ttu-id="f9c93-274">Если этот атрибут отсутствует, то именем ресурса OutputMediaAsset будет внутреннее текстовое значение элемента <outputAsset> с суффиксом, которым может быть значение параметра имени задания или параметра идентификатора задания (если свойство Name не определено).</span><span class="sxs-lookup"><span data-stu-id="f9c93-274">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="f9c93-275">Например, если задать для атрибута assetName значение Sample, для свойства Name ресурса OutputMediaAsset будет задано значение Sample.</span><span class="sxs-lookup"><span data-stu-id="f9c93-275">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span></span> <span data-ttu-id="f9c93-276">Тем не менее, если значение атрибута assetName не задано, но в качестве имени задания задано NewJob, имя OutputMediaAsset будет выглядеть следующим образом: JobOutputAsset(значение)_NewJob.</span><span class="sxs-lookup"><span data-stu-id="f9c93-276">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="f9c93-277">В следующем примере показано, как установить атрибут assetName:</span><span class="sxs-lookup"><span data-stu-id="f9c93-277">The following example shows how to set the assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="f9c93-278">Чтобы включить создание цепных задач:</span><span class="sxs-lookup"><span data-stu-id="f9c93-278">To enable task chaining:</span></span>

  * <span data-ttu-id="f9c93-279">в задании должно быть по крайней мере две задачи;</span><span class="sxs-lookup"><span data-stu-id="f9c93-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="f9c93-280">должна существовать хотя бы одна задача, входные данные которой являются выходными данными другой задачи в задании.</span><span class="sxs-lookup"><span data-stu-id="f9c93-280">There must be at least one task whose input is output of another task in the job.</span></span>

<span data-ttu-id="f9c93-281">Дополнительную информацию см. в статье [Создание задания кодирования с помощью REST API служб мультимедиа](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="f9c93-281">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="f9c93-282">Отслеживание хода обработки</span><span class="sxs-lookup"><span data-stu-id="f9c93-282">Monitor Processing Progress</span></span>
<span data-ttu-id="f9c93-283">Состояние задания можно получить с помощью свойства State, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="f9c93-283">You can retrieve the Job status by using the State property, as shown in the following example.</span></span>

<span data-ttu-id="f9c93-284">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="f9c93-285">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-285">**HTTP Response**</span></span>

<span data-ttu-id="f9c93-286">При успешном выполнении возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="f9c93-286">If successful, the following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="f9c93-287">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="f9c93-287">Cancel a job</span></span>
<span data-ttu-id="f9c93-288">Службы мультимедиа позволяют отменить выполнение заданий с помощью функции CancelJob.</span><span class="sxs-lookup"><span data-stu-id="f9c93-288">Media Services allows you to cancel running jobs through the CancelJob function.</span></span> <span data-ttu-id="f9c93-289">Этот вызов вернет код ошибки 400 при попытке отменить задание, если оно находится в состоянии "Отменено", "Отменяется", "Ошибка" или "Завершено".</span><span class="sxs-lookup"><span data-stu-id="f9c93-289">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="f9c93-290">В следующем примере показано, как вызвать CancelJob.</span><span class="sxs-lookup"><span data-stu-id="f9c93-290">The following example shows how to call CancelJob.</span></span>

<span data-ttu-id="f9c93-291">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="f9c93-292">В случае успешного выполнения возвращается код ответа 204 без текста сообщения.</span><span class="sxs-lookup"><span data-stu-id="f9c93-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c93-293">При передаче идентификатора задания в качестве параметра CancelJob его необходимо закодировать идентификатор задания в URL-адресе (обычно в виде nb:jid:UUID: somevalue).</span><span class="sxs-lookup"><span data-stu-id="f9c93-293">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span></span>
>
>

### <a name="get-the-output-asset"></a><span data-ttu-id="f9c93-294">Получение выходного ресурса</span><span class="sxs-lookup"><span data-stu-id="f9c93-294">Get the output asset</span></span>
<span data-ttu-id="f9c93-295">В следующем коде показано, как запросить идентификатор выходного ресурса.</span><span class="sxs-lookup"><span data-stu-id="f9c93-295">The following code shows how to request the output asset Id.</span></span>

<span data-ttu-id="f9c93-296">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="f9c93-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="f9c93-297">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="f9c93-297">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <span data-ttu-id="f9c93-298"><a id="publish_get_urls"></a>Публикация актива и получение URL-адресов потоковой передачи и поэтапного скачивания с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="f9c93-298"><a id="publish_get_urls"></a>Publish the asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="f9c93-299">Чтобы выполнить потоковую передачу ресурса-контейнера или скачать его, сначала необходимо "опубликовать" его, создав указатель.</span><span class="sxs-lookup"><span data-stu-id="f9c93-299">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="f9c93-300">Указатели предоставляют доступ к файлам, содержащимся в активе.</span><span class="sxs-lookup"><span data-stu-id="f9c93-300">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="f9c93-301">Службы мультимедиа поддерживают два типа указателей: указатели на OnDemandOrigin, использующиеся для потоковой передачи служб мультимедиа (например, MPEG DASH, HLS или Smooth Streaming), и указатели на подписанный URL-адрес, использующиеся для скачивания файлов мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f9c93-301">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span> <span data-ttu-id="f9c93-302">Дополнительные сведения об указателях SAS см. в [этой](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) записи блога.</span><span class="sxs-lookup"><span data-stu-id="f9c93-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="f9c93-303">После создания указателей можно создать URL-адреса, которые используются для потоковой передачи или скачивания файлов.</span><span class="sxs-lookup"><span data-stu-id="f9c93-303">Once you create the locators, you can build the URLs that are used to stream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="f9c93-304">При создании учетной записи AMS в нее добавляется конечная точка потоковой передачи **по умолчанию** в состоянии **Остановлена**.</span><span class="sxs-lookup"><span data-stu-id="f9c93-304">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="f9c93-305">Чтобы начать потоковую передачу содержимого и воспользоваться динамической упаковкой и динамическим шифрованием, конечная точка потоковой передачи, из которой необходимо выполнять потоковую передачу содержимого, должна находиться в состоянии **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="f9c93-305">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="f9c93-306">URL-адрес потоковой передачи для Smooth Streaming имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="f9c93-306">A streaming URL for Smooth Streaming has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="f9c93-307">URL-адрес потоковой передачи для HLS имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="f9c93-307">A streaming URL for HLS has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="f9c93-308">URL-адрес потоковой передачи для MPEG DASH имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="f9c93-308">A streaming URL for MPEG DASH has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="f9c93-309">URL-адрес SAS, используемый для скачивания файлов, имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="f9c93-309">A SAS URL used to download files has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="f9c93-310">В этом разделе показано, как выполнять следующие задачи, необходимые для "публикации" ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f9c93-310">This section shows how to perform the following tasks necessary to "publish" your assets.</span></span>  

* <span data-ttu-id="f9c93-311">Создание сущности AccessPolicy с разрешением на чтение</span><span class="sxs-lookup"><span data-stu-id="f9c93-311">Creating the AccessPolicy with read permission</span></span>
* <span data-ttu-id="f9c93-312">Создание URL-адреса SAS для скачивания содержимого</span><span class="sxs-lookup"><span data-stu-id="f9c93-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="f9c93-313">Создание исходного URL-адреса для потоковой передачи содержимого</span><span class="sxs-lookup"><span data-stu-id="f9c93-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-the-accesspolicy-with-read-permission"></a><span data-ttu-id="f9c93-314">Создание сущности AccessPolicy с разрешением на чтение</span><span class="sxs-lookup"><span data-stu-id="f9c93-314">Creating the AccessPolicy with read permission</span></span>
<span data-ttu-id="f9c93-315">Перед скачиванием или потоковой передачей любого медиасодержимого сначала определите сущность AccessPolicy с разрешениями на чтение и создайте соответствующую сущность указателя, которая задает тип механизма доставки, который нужно включить для клиентов.</span><span class="sxs-lookup"><span data-stu-id="f9c93-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span></span> <span data-ttu-id="f9c93-316">Дополнительную информацию о доступных свойствах см. в статье [Свойства сущности AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="f9c93-316">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="f9c93-317">В следующем примере показано, как задать сущность AccessPolicy для разрешений на чтение для данного ресурса.</span><span class="sxs-lookup"><span data-stu-id="f9c93-317">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="f9c93-318">При успешном выполнении возвращается код успешного завершения 201, описывающий созданную сущность AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="f9c93-318">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span></span> <span data-ttu-id="f9c93-319">Затем идентификатор сущности AccessPolicy будет использоваться вместе с идентификатором сущности Asset ресурса, содержащего файл, который необходимо доставить (например, выходной ресурс), для создания сущности Locator.</span><span class="sxs-lookup"><span data-stu-id="f9c93-319">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c93-320">Этот основной рабочий процесс будет таким же, как при передаче файла во время приема ресурса (как было описано ранее в этой статье).</span><span class="sxs-lookup"><span data-stu-id="f9c93-320">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="f9c93-321">Кроме того, если вам (или вашим клиентам) необходимо незамедлительно получить доступ к файлам, как и при передаче файлов, установите для StartTime значение, на пять минут предшествующее текущему моменту времени.</span><span class="sxs-lookup"><span data-stu-id="f9c93-321">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="f9c93-322">Это действие необходимо из-за возможного расхождения в показаниях часов на клиенте и в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f9c93-322">This action is necessary because there may be clock skew between the client and Media Services.</span></span> <span data-ttu-id="f9c93-323">Значение StartTime должно быть задано в следующем формате даты и времени: ГГГГ-ММ-ДДТЧЧ:мм:ссZ (например, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="f9c93-323">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="f9c93-324">Создание URL-адреса SAS для скачивания содержимого</span><span class="sxs-lookup"><span data-stu-id="f9c93-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="f9c93-325">Следующий код показывает, как получить URL-адрес, который может использоваться для скачивания файла мультимедиа, созданного и переданного ранее.</span><span class="sxs-lookup"><span data-stu-id="f9c93-325">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span></span> <span data-ttu-id="f9c93-326">У сущности AccessPolicy есть разрешения на чтение, а путь указателя указывает на URL-адрес скачивания SAS.</span><span class="sxs-lookup"><span data-stu-id="f9c93-326">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="f9c93-327">При успешном выполнении возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="f9c93-327">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="f9c93-328">Возвращенное свойство **Path** содержит URL-адрес SAS.</span><span class="sxs-lookup"><span data-stu-id="f9c93-328">The returned **Path** property contains the SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c93-329">При скачивании зашифрованного содержимого хранилища необходимо вручную расшифровать его перед его отображением или использовать обработчик мультимедиа для расшифровки хранилища в задаче обработки, чтобы вывести обработанные файлы в незашифрованном виде в OutputAsset, а затем скачать их из этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="f9c93-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="f9c93-330">Дополнительную информацию об обработке см. в разделе "Создание задания кодирования с помощью REST API служб мультимедиа".</span><span class="sxs-lookup"><span data-stu-id="f9c93-330">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span></span> <span data-ttu-id="f9c93-331">Кроме того, указатели URL-адреса SAS нельзя обновить после их создания.</span><span class="sxs-lookup"><span data-stu-id="f9c93-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="f9c93-332">Например, нельзя повторно использовать один и тот же указатель с обновленным значением StartTime.</span><span class="sxs-lookup"><span data-stu-id="f9c93-332">For example, you cannot reuse the same Locator with an updated StartTime value.</span></span> <span data-ttu-id="f9c93-333">Это связано со способом создания URL-адресов SAS.</span><span class="sxs-lookup"><span data-stu-id="f9c93-333">This is because of the way SAS URLs are created.</span></span> <span data-ttu-id="f9c93-334">Если вы хотите получить доступ к ресурсу для скачивания после истечения срока действия указателя, необходимо создать новый указатель с новым значением StartTime.</span><span class="sxs-lookup"><span data-stu-id="f9c93-334">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="f9c93-335">Скачивание файлов</span><span class="sxs-lookup"><span data-stu-id="f9c93-335">Download files</span></span>
<span data-ttu-id="f9c93-336">Когда сущности AccessPolicy и Locator будут заданы, файлы можно будет скачать с помощью REST API службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c93-336">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="f9c93-337">Необходимо добавить имя файла для файла, который нужно скачать, в значение **Path** сущности Locator, полученное в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="f9c93-337">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="f9c93-338">Например, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="f9c93-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="f9c93-339">.</span><span class="sxs-lookup"><span data-stu-id="f9c93-339">.</span></span> <span data-ttu-id="f9c93-340">.</span><span class="sxs-lookup"><span data-stu-id="f9c93-340">.</span></span> <span data-ttu-id="f9c93-341">.</span><span class="sxs-lookup"><span data-stu-id="f9c93-341">.</span></span>
>
>

<span data-ttu-id="f9c93-342">Дополнительную информацию о работе с большими двоичными объектами службы хранилища Azure см. в статье [API-интерфейс REST службы BLOB-объектов](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="f9c93-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="f9c93-343">В результате задания кодирования, выполненного ранее (кодирования в набор MP4-файлов с адаптивной скоростью), у вас будет несколько MP4-файлов для поэтапного скачивания.</span><span class="sxs-lookup"><span data-stu-id="f9c93-343">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="f9c93-344">Например:</span><span class="sxs-lookup"><span data-stu-id="f9c93-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="f9c93-345">Создание URL-адреса потоковой передачи потокового содержимого</span><span class="sxs-lookup"><span data-stu-id="f9c93-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="f9c93-346">В следующем коде показано, как создать указатель URL-адреса потоковой передачи:</span><span class="sxs-lookup"><span data-stu-id="f9c93-346">The following code shows how to create a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="f9c93-347">При успешном выполнении возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="f9c93-347">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="f9c93-348">Для потоковой передачи с исходного URL-адреса Smooth Streaming в проигрывателе потокового мультимедиа необходимо добавить путь свойства с именем файла манифеста Smooth Streaming, за которым следует "/manifest".</span><span class="sxs-lookup"><span data-stu-id="f9c93-348">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="f9c93-349">Для потоковой передачи HLS добавьте (format=m3u8-aapl) после "/manifest".</span><span class="sxs-lookup"><span data-stu-id="f9c93-349">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="f9c93-350">Для потоковой передачи MPEG DASH добавьте (format=mpd-time-csf) после "/manifest".</span><span class="sxs-lookup"><span data-stu-id="f9c93-350">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="f9c93-351"><a id="play"></a>Воспроизведение содержимого</span><span class="sxs-lookup"><span data-stu-id="f9c93-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="f9c93-352">Чтобы воспроизвести видео, используйте [Проигрыватель служб мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="f9c93-352">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="f9c93-353">Для тестирования поэтапного скачивания вставьте URL-адрес в браузер (например, Internet Explorer, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="f9c93-353">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="f9c93-354">Дальнейшие действия: схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="f9c93-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f9c93-355">Отзывы</span><span class="sxs-lookup"><span data-stu-id="f9c93-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
