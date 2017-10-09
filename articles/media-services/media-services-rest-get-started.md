---
title: "aaaGet работы с доставки содержимого по требованию с помощью REST | Документы Microsoft"
description: "Этот учебник поможет выполнить действия hello реализации приложения доставки содержимого по запросу с помощью служб мультимедиа Azure с помощью API-интерфейса REST."
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
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="b7b2c-103">Начало работы с доставкой содержимого по запросу с помощью REST</span><span class="sxs-lookup"><span data-stu-id="b7b2c-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="b7b2c-104">Это краткое руководство поможет hello шагов по реализации приложения доставки содержимого видео по запросу (VoD) с помощью API REST служб мультимедиа Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-104">This quickstart walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="b7b2c-105">Hello учебнике рассказывается hello базовый рабочий процесс служб мультимедиа и hello распространенных объектов и задач, необходимых для разработки служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-105">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="b7b2c-106">По завершении hello учебника hello будет toostream может быть или постепенно загрузить образец файла мультимедиа, отправки, закодированные и загружены.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-106">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="b7b2c-107">Hello рисунке показаны некоторые из наиболее часто используемых hello объектов при разработке приложений VoD к модели hello OData служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-107">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="b7b2c-108">Щелкните tooview изображение hello его полный размер.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-108">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="b7b2c-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b7b2c-109">Prerequisites</span></span>
<span data-ttu-id="b7b2c-110">Hello следующих предварительных требований, необходимых toostart разработки с помощью служб мультимедиа с API REST.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-110">hello following prerequisites are required toostart developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="b7b2c-111">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-111">An Azure account.</span></span> <span data-ttu-id="b7b2c-112">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b7b2c-113">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-113">A Media Services account.</span></span> <span data-ttu-id="b7b2c-114">toocreate учетную запись служб носителей в разделе [как учетную запись служб мультимедиа tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-114">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="b7b2c-115">О том, как toodevelop с API REST служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-115">Understanding of how toodevelop with Media Services REST API.</span></span> <span data-ttu-id="b7b2c-116">Дополнительные сведения см. в статье [Обзор REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="b7b2c-117">Выбранное вами приложение, способное отправлять HTTP-запросы и ответы.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="b7b2c-118">В этом учебнике используется [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="b7b2c-119">в этом кратком руководстве показаны Hello следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-119">hello following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="b7b2c-120">Запустите (с помощью портала Azure hello) конечной точки потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-120">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="b7b2c-121">Учетная запись служб мультимедиа toohello подключитесь с помощью API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-121">Connect toohello Media Services account with REST API.</span></span>
3. <span data-ttu-id="b7b2c-122">Создание нового ресурса и отправка видеофайла с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="b7b2c-123">Кодирование hello исходный файл в набор MP4-файлов с адаптивной скоростью, с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-123">Encode hello source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="b7b2c-124">Публикация активов hello и get потоковой передачи и URL-адресов прогрессивной загрузки с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-124">Publish hello asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="b7b2c-125">Воспроизведение содержимого.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="b7b2c-126">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="b7b2c-127">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-127">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="b7b2c-128">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="b7b2c-129">Дополнительные сведения о сущностях AMS REST, используемых в этом разделе, см. в статье [Справочник по интерфейсу API REST служб мультимедиа Azure](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="b7b2c-130">См. также статью [Основные понятия служб мультимедиа Azure](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="b7b2c-131">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="b7b2c-132">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="b7b2c-133">Запустить с помощью портала Azure hello конечные точки потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="b7b2c-133">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="b7b2c-134">При работе со службами мультимедиа Azure одним из наиболее распространенных сценариев hello разрабатывает видео через потоковой передачи с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-134">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="b7b2c-135">Служба Media Services предоставляет динамической упаковки, что позволяет вам toodeliver с адаптивным битрейтом MP4 кодируются содержимого в форматах, поддерживаемых служб мультимедиа (MPEG DASH, HLS, Smooth Streaming) just-in-time, без необходимости toostore упакована заранее потоковой передачи версии каждого из этих форматов потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-135">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="b7b2c-136">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-136">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="b7b2c-137">Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-137">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="b7b2c-138">toostart Здравствуйте конечной точки потоковой передачи, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-138">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="b7b2c-139">Войдите на hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-139">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b7b2c-140">В окне "Параметры" hello щелкните конечных точек потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-140">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="b7b2c-141">Щелкните конечную точку потоковой передачи по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-141">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="b7b2c-142">Появится окно Hello по умолчанию потоковая передача сведений о конечной ТОЧКЕ.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-142">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="b7b2c-143">Щелкните значок запуска hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-143">Click hello Start icon.</span></span>
5. <span data-ttu-id="b7b2c-144">Щелкните toosave кнопку hello сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-144">Click hello Save button toosave your changes.</span></span>

## <span data-ttu-id="b7b2c-145"><a id="connect"></a>Подключение toohello учетная запись служб мультимедиа с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="b7b2c-145"><a id="connect"></a>Connect toohello Media Services account with REST API</span></span>

<span data-ttu-id="b7b2c-146">Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-146">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="b7b2c-147">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-147">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="b7b2c-148">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-148">You must make subsequent calls toohello new URI.</span></span>

<span data-ttu-id="b7b2c-149">Например если после попытки tooconnect, полученный hello следующее:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-149">For example, if after trying tooconnect, you got hello following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="b7b2c-150">Вам следует опубликовать в последующих toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ вызовы API.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-150">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="b7b2c-151"><a id="upload"></a>Создание нового актива и отправка видеофайла с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="b7b2c-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="b7b2c-152">В службах мультимедиа цифровые файлы отправляются в актив.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="b7b2c-153">Hello **активов** может содержать сущности, видео, аудио, изображения, коллекции эскизов, текст отслеживает и титров файлов (и hello метаданные об этих файлах.)  После отправки файлов hello в актив hello, контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-153">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="b7b2c-154">Одно из значений hello имеют tooprovide при создании ресурса параметров создания ресурса.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-154">One of hello values that you have tooprovide when creating an asset is asset creation options.</span></span> <span data-ttu-id="b7b2c-155">Hello **параметры** свойство является значением перечисления, описывающее параметры шифрования hello, которые ресурс может быть создан с.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-155">hello **Options** property is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="b7b2c-156">Допустимым значением является одним из значений hello из списка hello ниже, а не сочетание значений из этого списка:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-156">A valid value is one of hello values from hello list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="b7b2c-157">**None** = **0**. Шифрование не используется.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="b7b2c-158">При использовании этого параметра содержимое не защищено при передаче и хранении.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="b7b2c-159">Если планируется toodeliver MP4-файл с помощью прогрессивной загрузки, используйте этот параметр.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-159">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="b7b2c-160">**StorageEncrypted** = **1** - шифрует локально с помощью AES-256-разрядного шифрования незащищенного контента, а затем передает его tooAzure хранилища, где она хранится в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="b7b2c-161">Активы, защищенные с помощью шифрования хранилища, автоматически дешифруются и помещаются в предыдущих tooencoding зашифрованный файл системы и при необходимости повторно зашифрован предыдущих toouploading возвращены в виде нового выходного актива.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="b7b2c-162">Hello основным случаем использования шифрования хранилища при необходимости toosecure файлов входном файле мультимедиа высокого качества с помощью криптостойкого шифрования на диске.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-162">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="b7b2c-163">**CommonEncryptionProtected** = **2**. Используйте этот параметр при отправке содержимого, которое уже зашифровано и защищено с помощью стандартного шифрования или PlayReady DRM (например, Smooth Streaming с защитой PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="b7b2c-164">**EnvelopeEncryptionProtected** = **4**. Используйте этот параметр при отправке HLS с шифрованием AES.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="b7b2c-165">необходимо, Hello файлы были закодированы и зашифрованы диспетчером преобразования.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-165">hello files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="b7b2c-166">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="b7b2c-166">Create an asset</span></span>
<span data-ttu-id="b7b2c-167">Ресурс — это контейнер, состоящий из нескольких наборов объектов или объектов разного типа в службах мультимедиа, в том числе видео, аудио, изображения, коллекции отпечатков, текстовые каналы и файлы скрытых субтитров.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="b7b2c-168">В API-Интерфейс REST, создания ресурса необходимо отправить POST hello запроса tooMedia служб и поместить все сведения о свойствах ресурса в тексте запроса hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-168">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="b7b2c-169">Следующий пример показывает как Hello toocreate актива.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-169">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="b7b2c-170">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-170">**HTTP Request**</span></span>

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


<span data-ttu-id="b7b2c-171">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-171">**HTTP Response**</span></span>

<span data-ttu-id="b7b2c-172">В случае успешного выполнения возвращается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-172">If successful, hello following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="b7b2c-173">Создание сущности AssetFile</span><span class="sxs-lookup"><span data-stu-id="b7b2c-173">Create an AssetFile</span></span>
<span data-ttu-id="b7b2c-174">Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) сущности представляет видео- или файл, хранящийся в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="b7b2c-175">Файл ресурса всегда связан с ресурсом, который, в свою очередь, может содержать одну или несколько сущностей AssetFile.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="b7b2c-176">задачу Hello Media Services Encoder завершается ошибкой, если объект файла ресурса не связан с цифровым файлом в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-176">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="b7b2c-177">После отправки файла мультимедиа в контейнер больших двоичных объектов, с помощью hello **СЛИЯНИЯ** hello tooupdate HTTP-запроса AssetFile со сведениями о файл (как показано далее в разделе hello).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-177">After you upload your digital media file into a blob container, you use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span>

<span data-ttu-id="b7b2c-178">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-178">**HTTP Request**</span></span>

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


<span data-ttu-id="b7b2c-179">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-179">**HTTP Response**</span></span>

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


### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="b7b2c-180">Создание hello AccessPolicy с разрешениями на запись</span><span class="sxs-lookup"><span data-stu-id="b7b2c-180">Creating hello AccessPolicy with write permission</span></span>
<span data-ttu-id="b7b2c-181">Перед отправкой файлов в хранилище больших двоичных объектов, выбор hello права политики для записи tooan активов.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-181">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="b7b2c-182">задать toodo, учет toohello запрос HTTP сущностей AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-182">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="b7b2c-183">При создании сущности необходимо задать значение DurationInMinutes. В противном случае вы получите сообщение 500 (внутренняя ошибка сервера).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="b7b2c-184">Дополнительную информацию о сущностях AccessPolicy см. в разделе [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="b7b2c-185">Следующий пример показывает как Hello toocreate AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-185">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="b7b2c-186">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-186">**HTTP Request**</span></span>

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

<span data-ttu-id="b7b2c-187">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-187">**HTTP Response**</span></span>

<span data-ttu-id="b7b2c-188">В случае успешного выполнения возвращается следующий ответ hello:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-188">If successful, hello following response is returned:</span></span>

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="b7b2c-189">Получить hello передать URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b7b2c-189">Get hello Upload URL</span></span>

<span data-ttu-id="b7b2c-190">tooreceive Здравствуйте непосредственную отправку URL-адрес, создания указателя SAS.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-190">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="b7b2c-191">Указатели определяют время начала hello и тип конечной точки подключения для клиентов, которые хотят tooaccess файлы в активе.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-191">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="b7b2c-192">Можно создать несколько объектов указателя для заданного параметра AccessPolicy и активов пары toohandle другого клиента, запросы и требования.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="b7b2c-193">Каждый из этих указателей использует значения StartTime hello и hello DurationInMinutes параметра hello toodetermine AccessPolicy hello продолжительность времени, можно использовать URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-193">Each of these Locators uses hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="b7b2c-194">Дополнительную информацию см. в разделе [Указатель](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="b7b2c-195">URL-адрес SAS имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-195">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="b7b2c-196">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="b7b2c-196">Some considerations apply:</span></span>

* <span data-ttu-id="b7b2c-197">С определенным ресурсом нельзя связать более пяти уникальных указателей одновременно.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="b7b2c-198">Дополнительную информацию см. в разделе "Указатель".</span><span class="sxs-lookup"><span data-stu-id="b7b2c-198">For more information, see Locator.</span></span>
* <span data-ttu-id="b7b2c-199">Если вам требуется tooupload файлов сразу, необходимо задать toofive минут значение StartTime вашей hello текущее время.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-199">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="b7b2c-200">Это необходимо из-за возможного расхождения в показаниях часов на клиентском компьютере и в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="b7b2c-201">Кроме того, значение StartTime должно находиться в hello следующая формата даты и времени: гггг-мм-: ssz (например, «2014-05-23T17:53:50Z»).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-201">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="b7b2c-202">Может быть 30-40 секунд задержки после создания локатора toowhen доступен для использования.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-202">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="b7b2c-203">Эта проблема относится tooboth URL-адрес SAS и Локаторы источника.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-203">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="b7b2c-204">Дополнительные сведения об указателях SAS см. в [этой](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) записи блога.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="b7b2c-205">Hello в следующем примере показано, как toocreate указатель URL-адрес SAS, в соответствии с определением hello свойство типа в тексте запроса hello («1» для указателя SAS) и «2» для указателя origin по требованию.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-205">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="b7b2c-206">Hello **путь** hello URL-адрес, что необходимо использовать tooupload файл содержит свойство, которое возвращается.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-206">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="b7b2c-207">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-207">**HTTP Request**</span></span>

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


<span data-ttu-id="b7b2c-208">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-208">**HTTP Response**</span></span>

<span data-ttu-id="b7b2c-209">В случае успешного выполнения возвращается следующий ответ hello:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-209">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="b7b2c-210">Отправка файла в контейнер хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="b7b2c-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="b7b2c-211">После создания hello AccessPolicy и указателя набор hello файл находится в контейнер хранилища BLOB-объектов Azure отправленного tooan, с помощью hello API REST хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-211">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure blob storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="b7b2c-212">Hello файлы необходимо отправить в виде блочных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-212">You must upload hello files as block blobs.</span></span> <span data-ttu-id="b7b2c-213">Страничные BLOB-объекты не поддерживаются службами мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="b7b2c-214">Необходимо добавить имя файла hello hello файла требуется tooupload toohello локатора **путь** значение, полученное в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-214">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="b7b2c-215">Например, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="b7b2c-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="b7b2c-216">.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-216">.</span></span> <span data-ttu-id="b7b2c-217">.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-217">.</span></span> <span data-ttu-id="b7b2c-218">.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-218">.</span></span>
>
>

<span data-ttu-id="b7b2c-219">Дополнительную информацию о работе с большими двоичными объектами службы хранилища Azure см. в статье [API-интерфейс REST службы BLOB-объектов](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="b7b2c-220">Hello обновление AssetFile</span><span class="sxs-lookup"><span data-stu-id="b7b2c-220">Update hello AssetFile</span></span>
<span data-ttu-id="b7b2c-221">После отправки файла обновите сведения о hello FileAsset размер (и другие).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-221">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="b7b2c-222">Например:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-222">For example:</span></span>

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


<span data-ttu-id="b7b2c-223">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-223">**HTTP Response**</span></span>

<span data-ttu-id="b7b2c-224">В случае успешного выполнения возвращается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-224">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="b7b2c-225">Удаление локатора hello и AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="b7b2c-225">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="b7b2c-226">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="b7b2c-227">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-227">**HTTP Response**</span></span>

<span data-ttu-id="b7b2c-228">В случае успешного выполнения возвращается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-228">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="b7b2c-229">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="b7b2c-230">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-230">**HTTP Response**</span></span>

<span data-ttu-id="b7b2c-231">В случае успешного выполнения возвращается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-231">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="b7b2c-232"><a id="encode"></a>Кодирование hello исходный файл в набор файлов MP4 с адаптивной скоростью</span><span class="sxs-lookup"><span data-stu-id="b7b2c-232"><a id="encode"></a>Encode hello source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="b7b2c-233">После получения кодирования ресурсов в службах мультимедиа media, transmuxed, водяные знаки и т. д. перед отправкой tooclients.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="b7b2c-234">Эти операции планируются и выполняются несколько фона роль экземпляров tooensure высокой производительности и доступности.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-234">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="b7b2c-235">Эти действия называются заданиями, и каждое задание состоит из атомарных задач, которые hello фактические трудозатраты на файл актива hello (Дополнительные сведения см. в разделе [задания](/rest/api/media/services/job), [задачи](/rest/api/media/services/task) описания).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-235">These activities are called Jobs and each Job is composed of atomic Tasks that do hello actual work on hello Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="b7b2c-236">Как упоминалось ранее, при работе с помощью Azure Media Services один из наиболее распространенных сценариев hello разрабатывает клиентов tooyour потоковой передачи с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-236">As was mentioned earlier, when working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="b7b2c-237">Службы мультимедиа можно динамически упаковать набор файлов MP4 с адаптивной скоростью в один из следующих форматов hello: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="b7b2c-238">Hello в следующем разделе показано, как toocreate задание, содержащее одной кодировки задач.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-238">hello following section shows how toocreate a job that contains one encoding task.</span></span> <span data-ttu-id="b7b2c-239">Hello указываются tootranscode hello мезонинный файл в набор MP4-файлов с адаптивной скоростью, с помощью **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-239">hello task specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="b7b2c-240">Hello разделе также рассказывается, как toomonitor hello ход выполнения задания обработки.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-240">hello section also shows how toomonitor hello job processing progress.</span></span> <span data-ttu-id="b7b2c-241">По завершении задания hello будет может toocreate указатели, которые являются ресурсами tooyour необходимые tooget доступа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-241">When hello job is complete, you would be able toocreate locators that are needed tooget access tooyour assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="b7b2c-242">Получение обработчика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b7b2c-242">Get a media processor</span></span>
<span data-ttu-id="b7b2c-243">В службах мультимедиа обработчик мультимедиа — это компонент, который работает со специфическими задачами обработки, такими как кодирование, преобразование формата, шифрование или расшифровка мультимедийного содержимого.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="b7b2c-244">Для hello кодирование задачи, показанные в этом учебнике мы будем toouse hello стандартный кодировщик мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-244">For hello encoding task shown in this tutorial, we are going toouse hello Media Encoder Standard.</span></span>

<span data-ttu-id="b7b2c-245">Здравствуйте, кода запросы hello кодировщика код подписки.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-245">hello following code requests hello encoder's id.</span></span>

<span data-ttu-id="b7b2c-246">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="b7b2c-247">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-247">**HTTP Response**</span></span>

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

### <a name="create-a-job"></a><span data-ttu-id="b7b2c-248">Создание задания</span><span class="sxs-lookup"><span data-stu-id="b7b2c-248">Create a job</span></span>
<span data-ttu-id="b7b2c-249">Каждое задание может включать один или несколько задач в зависимости от типа hello обработки, которую хотите tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-249">Each Job can have one or more Tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="b7b2c-250">Через hello REST API, можно создавать задания и связанные задачи одним из двух способов: задачи может быть определен как встроенный через hello свойства навигации Tasks объекта сущности задания, или пакетной обработки OData.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-250">Through hello REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through hello Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="b7b2c-251">Hello пакета SDK служб мультимедиа использует пакетную обработку.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-251">hello Media Services SDK uses batch processing.</span></span> <span data-ttu-id="b7b2c-252">Однако для удобства чтения hello hello примеры кода в этом разделе, задачи не определен как встроенный.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-252">However, for hello readability of hello code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="b7b2c-253">Чтобы узнать больше о пакетной обработке, ознакомьтесь с [пакетной обработкой посредством протокола OData](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="b7b2c-254">Hello в следующем примере показано, как toocreate и post задание с одной задачи набор tooencode видео с определенным разрешением и качества.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-254">hello following example shows you how toocreate and post a Job with one Task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="b7b2c-255">Hello следующий раздел документации содержит список всех hello hello [задач предустановки](http://msdn.microsoft.com/library/mt269960) поддерживаемых процессором Media Encoder Стандартная hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-255">hello following documentation section contains hello list of all hello [task presets](http://msdn.microsoft.com/library/mt269960) supported by hello Media Encoder Standard processor.</span></span>  

<span data-ttu-id="b7b2c-256">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-256">**HTTP Request**</span></span>

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

<span data-ttu-id="b7b2c-257">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-257">**HTTP Response**</span></span>

<span data-ttu-id="b7b2c-258">В случае успешного выполнения возвращается следующий ответ hello:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-258">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="b7b2c-259">Существует несколько важных событий toonote запросов задания:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-259">There are a few important things toonote in any Job request:</span></span>

* <span data-ttu-id="b7b2c-260">Свойства TaskBody должны использовать числовой литерал XML toodefine hello ввода или выходные активы, используемых hello задачи.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-260">TaskBody properties MUST use literal XML toodefine hello number of input, or output assets that are used by hello Task.</span></span> <span data-ttu-id="b7b2c-261">раздел задача Hello содержит hello определения схемы XML для hello XML.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-261">hello Task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="b7b2c-262">В hello TaskBody определение каждого внутреннее значение атрибута <inputAsset> и <outputAsset> должен быть задан как JobInputAsset(value) или JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-262">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="b7b2c-263">В задаче может содержаться несколько выходных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-263">A task can have multiple output assets.</span></span> <span data-ttu-id="b7b2c-264">Значение JobOutputAsset(x) может использоваться только один раз в качестве выходных данных задачи в задании.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="b7b2c-265">В качестве входного ресурса задачи можно указать JobInputAsset или JobOutputAsset.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="b7b2c-266">Задачи не должны образовывать цикл.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="b7b2c-267">значение параметра Hello передается tooJobInputAsset или JobOutputAsset представляет значение индекса hello для актива.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-267">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an Asset.</span></span> <span data-ttu-id="b7b2c-268">Hello фактические ресурсы определяются в hello InputMediaAssets и OutputMediaAssets свойства навигации в определении объекта Job hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-268">hello actual Assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="b7b2c-269">Поскольку службы мультимедиа разработаны на основе OData v3, hello отдельные ресурсы в свойствах InputMediaAssets и OutputMediaAssets навигации свойства указываются с помощью «__metadata: uri» пары "имя значение".</span><span class="sxs-lookup"><span data-stu-id="b7b2c-269">Because Media Services is built on OData v3, hello individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="b7b2c-270">Объекты InputMediaAssets сопоставляются tooone или несколько ресурсов, созданные в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-270">InputMediaAssets maps tooone or more Assets you have created in Media Services.</span></span> <span data-ttu-id="b7b2c-271">Объекты OutputMediaAssets создаются системой hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-271">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="b7b2c-272">Они не ссылаются на существующий ресурс.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="b7b2c-273">Может иметь имя OutputMediaAssets с помощью атрибута assetName hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-273">OutputMediaAssets can be named using hello assetName attribute.</span></span> <span data-ttu-id="b7b2c-274">Если этот атрибут не задан, то имя hello hello объекта OutputMediaAsset будет любое значение внутренний текст hello hello <outputAsset> существует элемент с суффиксом hello имя задания значение или значение идентификатора задания hello (в случае hello, где свойство Name hello не определено).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-274">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="b7b2c-275">Например если задать значение для assetName слишком «Пример», а затем hello Name объекта OutputMediaAsset будет иметь значение свойства слишком «Sample».</span><span class="sxs-lookup"><span data-stu-id="b7b2c-275">For example, if you set a value for assetName too"Sample", then hello OutputMediaAsset Name property would be set too"Sample".</span></span> <span data-ttu-id="b7b2c-276">Однако если не удалось задать значение для assetName, но был указан hello имя задания слишком «NewJob», а затем hello Name объекта OutputMediaAsset будет «JobOutputAsset (значение) _NewJob».</span><span class="sxs-lookup"><span data-stu-id="b7b2c-276">However, if you did not set a value for assetName, but did set hello job name too"NewJob", then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="b7b2c-277">Привет, в следующем примере показано, как tooset hello атрибута assetName:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-277">hello following example shows how tooset hello assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="b7b2c-278">tooenable цепочки задач:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-278">tooenable task chaining:</span></span>

  * <span data-ttu-id="b7b2c-279">в задании должно быть по крайней мере две задачи;</span><span class="sxs-lookup"><span data-stu-id="b7b2c-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="b7b2c-280">Должен существовать хотя бы одна задача, входные данные которых является выходными данными другой задачи в задании hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-280">There must be at least one task whose input is output of another task in hello job.</span></span>

<span data-ttu-id="b7b2c-281">Дополнительные сведения см. в разделе [Создание задания кодирования с API REST служб мультимедиа hello](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-281">For more information see, [Creating an Encoding Job with hello Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="b7b2c-282">Отслеживание хода обработки</span><span class="sxs-lookup"><span data-stu-id="b7b2c-282">Monitor Processing Progress</span></span>
<span data-ttu-id="b7b2c-283">Состояние задания hello можно получить с помощью свойства State hello, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-283">You can retrieve hello Job status by using hello State property, as shown in hello following example.</span></span>

<span data-ttu-id="b7b2c-284">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="b7b2c-285">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-285">**HTTP Response**</span></span>

<span data-ttu-id="b7b2c-286">В случае успешного выполнения возвращается следующий ответ hello:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-286">If successful, hello following response is returned:</span></span>

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


### <a name="cancel-a-job"></a><span data-ttu-id="b7b2c-287">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="b7b2c-287">Cancel a job</span></span>
<span data-ttu-id="b7b2c-288">Службы мультимедиа можно toocancel запуска задания с помощью функции CancelJob hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-288">Media Services allows you toocancel running jobs through hello CancelJob function.</span></span> <span data-ttu-id="b7b2c-289">Этот вызов возвращает код ошибки 400, при попытке toocancel задания при отмене свое состояние, Отмена, ошибка или завершен.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-289">This call returns a 400 error code if you try toocancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="b7b2c-290">Следующий пример показывает как Hello toocall CancelJob.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-290">hello following example shows how toocall CancelJob.</span></span>

<span data-ttu-id="b7b2c-291">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="b7b2c-292">В случае успешного выполнения возвращается код ответа 204 без текста сообщения.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="b7b2c-293">Необходимо закодировать в URL-адрес идентификатор задания hello (обычно nb:jid:UUID: somevalue) при передаче в качестве tooCancelJob параметра.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-293">You must URL-encode hello job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter tooCancelJob.</span></span>
>
>

### <a name="get-hello-output-asset"></a><span data-ttu-id="b7b2c-294">Получение выходного актива hello</span><span class="sxs-lookup"><span data-stu-id="b7b2c-294">Get hello output asset</span></span>
<span data-ttu-id="b7b2c-295">Hello следующий код показывает, как toorequest hello вывода код актива.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-295">hello following code shows how toorequest hello output asset Id.</span></span>

<span data-ttu-id="b7b2c-296">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="b7b2c-297">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="b7b2c-297">**HTTP Response**</span></span>

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



## <span data-ttu-id="b7b2c-298"><a id="publish_get_urls"></a>Публикация активов hello и get потоковой передачи и URL-адресов прогрессивной загрузки с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="b7b2c-298"><a id="publish_get_urls"></a>Publish hello asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="b7b2c-299">toostream или загрузки актив, сначала требуется слишком «публикацией» путем создания локатора.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-299">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="b7b2c-300">Локаторы предоставляют доступ toofiles, содержащиеся в ресурсе hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-300">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="b7b2c-301">Службы мультимедиа поддерживают два типа локаторов: OnDemandOrigin локаторы, используемые toostream мультимедиа (например, MPEG DASH, HLS или Smooth Streaming) и указатели подписи доступа (SAS), используемый toodownload файлов мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-301">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files.</span></span> <span data-ttu-id="b7b2c-302">Дополнительные сведения об указателях SAS см. в [этой](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) записи блога.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="b7b2c-303">После создания hello указателей, можно построить hello URL-адреса, используемые toostream или загружать файлы.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-303">Once you create hello locators, you can build hello URLs that are used toostream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="b7b2c-304">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-304">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="b7b2c-305">Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-305">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="b7b2c-306">URL-адрес потоковой передачи для Smooth Streaming имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-306">A streaming URL for Smooth Streaming has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="b7b2c-307">URL-адрес потоковой передачи для HLS имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-307">A streaming URL for HLS has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="b7b2c-308">URL-адрес потоковой передачи для MPEG DASH имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-308">A streaming URL for MPEG DASH has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="b7b2c-309">URL-адрес SAS используется toodownload файлов имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-309">A SAS URL used toodownload files has hello following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="b7b2c-310">В этом разделе показано выполнение следующих hello tooperform задач необходимые слишком активов «опубликовать».</span><span class="sxs-lookup"><span data-stu-id="b7b2c-310">This section shows how tooperform hello following tasks necessary too"publish" your assets.</span></span>  

* <span data-ttu-id="b7b2c-311">Создание hello AccessPolicy с разрешением на чтение</span><span class="sxs-lookup"><span data-stu-id="b7b2c-311">Creating hello AccessPolicy with read permission</span></span>
* <span data-ttu-id="b7b2c-312">Создание URL-адреса SAS для скачивания содержимого</span><span class="sxs-lookup"><span data-stu-id="b7b2c-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="b7b2c-313">Создание исходного URL-адреса для потоковой передачи содержимого</span><span class="sxs-lookup"><span data-stu-id="b7b2c-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-hello-accesspolicy-with-read-permission"></a><span data-ttu-id="b7b2c-314">Создание hello AccessPolicy с разрешением на чтение</span><span class="sxs-lookup"><span data-stu-id="b7b2c-314">Creating hello AccessPolicy with read permission</span></span>
<span data-ttu-id="b7b2c-315">Перед загрузкой или потоковой передачи мультимедиа-контента, сначала определите AccessPolicy с разрешениями на чтение и создать hello соответствующий объект Locator, указывающий тип hello механизма доставки tooenable требуется для клиентов.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create hello appropriate Locator entity that specifies hello type of delivery mechanism you want tooenable for your clients.</span></span> <span data-ttu-id="b7b2c-316">Дополнительные сведения о свойствах hello, доступных в разделе [свойства сущности AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-316">For more information on hello properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="b7b2c-317">Hello в следующем примере показано, как toospecify hello AccessPolicy разрешениями на чтение для данного актива.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-317">hello following example shows how toospecify hello AccessPolicy for read permissions for a given Asset.</span></span>

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

<span data-ttu-id="b7b2c-318">В случае успешного выполнения код 201 успеха возвращается описания сущности AccessPolicy hello, созданный вами.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-318">If successful, a 201 success code is returned describing hello AccessPolicy entity that you created.</span></span> <span data-ttu-id="b7b2c-319">Затем с помощью hello Id объекта AccessPolicy вместе с hello идентификатор ресурса hello, содержащий файл hello требуется сущность указателя hello toocreate toodeliver (например, выходной ресурс).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-319">You then use hello AccessPolicy Id along with hello Asset Id of hello asset that contains hello file you want toodeliver(such as an output asset) toocreate hello Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="b7b2c-320">Этот базовый рабочий процесс hello аналогично передаче файла при передаче актива (как было описано ранее в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-320">This basic workflow is hello same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="b7b2c-321">Кроме того как передача файлов, если вы (или клиенты) должны tooaccess файлов сразу, задайте toofive минут значение StartTime вашей hello текущее время.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-321">Also, like uploading files, if you (or your clients) need tooaccess your files immediately, set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="b7b2c-322">Это действие является необходимым, поскольку может быть рассинхронизация времени между клиентом hello и служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-322">This action is necessary because there may be clock skew between hello client and Media Services.</span></span> <span data-ttu-id="b7b2c-323">Hello значение StartTime должно быть в hello следующая формата даты и времени: YYYY-MM-: ssz (например, «2014-05-23T17:53:50Z»).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-323">hello StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="b7b2c-324">Создание URL-адреса SAS для скачивания содержимого</span><span class="sxs-lookup"><span data-stu-id="b7b2c-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="b7b2c-325">Привет, следующий код показывает, как tooget URL-адрес, который можно использовать toodownload файл мультимедиа созданный и загруженный ранее.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-325">hello following code shows how tooget a URL that can be used toodownload a media file created and uploaded previously.</span></span> <span data-ttu-id="b7b2c-326">Hello AccessPolicy заданы разрешения чтения и путь локатора hello указывает URL-адрес загрузки SAS tooa.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-326">hello AccessPolicy has read permissions set and hello Locator path refers tooa SAS download URL.</span></span>

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

<span data-ttu-id="b7b2c-327">В случае успешного выполнения возвращается следующий ответ hello:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-327">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="b7b2c-328">Возвращаемый Hello **путь** свойство содержит hello URL-адрес SAS.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-328">hello returned **Path** property contains hello SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="b7b2c-329">Если вы загружаете зашифрованный контент, необходимо вручную расшифровать его перед его отображением или использовать hello обработчика мультимедиа расшифровки хранилища в toooutput обработки задач обработки файлов в hello снимите tooan OutputAsset, а затем загрузите из этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use hello Storage Decryption MediaProcessor in a processing task toooutput processed files in hello clear tooan OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="b7b2c-330">Дополнительные сведения об обработке см. в разделе Создание задания кодирования с hello API REST служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-330">For more information on processing, see Creating an Encoding Job with hello Media Services REST API.</span></span> <span data-ttu-id="b7b2c-331">Кроме того, указатели URL-адреса SAS нельзя обновить после их создания.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="b7b2c-332">Например, нельзя повторно использовать один объект Locator с обновленным значением StartTime hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-332">For example, you cannot reuse hello same Locator with an updated StartTime value.</span></span> <span data-ttu-id="b7b2c-333">Это вызвано hello, как создаются URL-адреса SAS.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-333">This is because of hello way SAS URLs are created.</span></span> <span data-ttu-id="b7b2c-334">Если tooaccess актива для загрузки локатора истек, необходимо создать новую с новым значением StartTime.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-334">If you want tooaccess an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="b7b2c-335">Скачивание файлов</span><span class="sxs-lookup"><span data-stu-id="b7b2c-335">Download files</span></span>
<span data-ttu-id="b7b2c-336">После создания hello AccessPolicy и указателя набор можно загрузить файлы с помощью hello API REST хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-336">Once you have hello AccessPolicy and Locator set, you can download files using hello Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="b7b2c-337">Необходимо добавить имя файла hello hello файла требуется toodownload toohello локатора **путь** значение, полученное в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-337">You must add hello file name for hello file you want toodownload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="b7b2c-338">Например, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="b7b2c-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="b7b2c-339">.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-339">.</span></span> <span data-ttu-id="b7b2c-340">.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-340">.</span></span> <span data-ttu-id="b7b2c-341">.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-341">.</span></span>
>
>

<span data-ttu-id="b7b2c-342">Дополнительную информацию о работе с большими двоичными объектами службы хранилища Azure см. в статье [API-интерфейс REST службы BLOB-объектов](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="b7b2c-343">В результате hello кодирования задание, которое вы осуществили ранее (кодировка в набор MP4 с адаптивной) у вас есть несколько MP4-файлов, которые можно загружать постепенно.</span><span class="sxs-lookup"><span data-stu-id="b7b2c-343">As a result of hello encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="b7b2c-344">Например:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="b7b2c-345">Создание URL-адреса потоковой передачи потокового содержимого</span><span class="sxs-lookup"><span data-stu-id="b7b2c-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="b7b2c-346">Здравствуйте, как следующий код показывает toocreate указатель потоковой передачи URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-346">hello following code shows how toocreate a streaming URL Locator:</span></span>

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

<span data-ttu-id="b7b2c-347">В случае успешного выполнения возвращается следующий ответ hello:</span><span class="sxs-lookup"><span data-stu-id="b7b2c-347">If successful, hello following response is returned:</span></span>

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

<span data-ttu-id="b7b2c-348">toostream Smooth Streaming URL-адрес источника в проигрывателе потоковой передачи мультимедиа, необходимо добавить свойство Path hello с именем hello hello Smooth Streaming манифест файла, за которым следует «/ manifest».</span><span class="sxs-lookup"><span data-stu-id="b7b2c-348">toostream a Smooth Streaming origin URL in a streaming media player, you must append hello Path property with hello name of hello Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="b7b2c-349">append toostream HLS (format = m3u8-aapl) после hello «/ manifest».</span><span class="sxs-lookup"><span data-stu-id="b7b2c-349">toostream HLS, append (format=m3u8-aapl) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="b7b2c-350">Добавление toostream MPEG DASH (формат = mpd время csf) после hello «/ manifest».</span><span class="sxs-lookup"><span data-stu-id="b7b2c-350">toostream MPEG DASH, append (format=mpd-time-csf) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="b7b2c-351"><a id="play"></a>Воспроизведение содержимого</span><span class="sxs-lookup"><span data-stu-id="b7b2c-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="b7b2c-352">toostream видео, используется [проигрыватель служб мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-352">toostream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="b7b2c-353">tootest прогрессивной загрузки, вставьте URL-адрес в адресную строку браузера (например, IE, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="b7b2c-353">tootest progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="b7b2c-354">Дальнейшие действия: схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b7b2c-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b7b2c-355">Отзывы</span><span class="sxs-lookup"><span data-stu-id="b7b2c-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
