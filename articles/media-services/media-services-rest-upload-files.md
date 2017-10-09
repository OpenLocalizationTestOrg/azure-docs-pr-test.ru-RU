---
title: "aaaUpload файлы в учетную запись служб мультимедиа с помощью REST | Документы Microsoft"
description: "Узнайте, как носитель tooget содержимого в службы мультимедиа, создав и загрузив активы."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="181b5-103">Передача файлов в учетную запись служб мультимедиа с помощью REST</span><span class="sxs-lookup"><span data-stu-id="181b5-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="181b5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="181b5-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="181b5-105">REST</span><span class="sxs-lookup"><span data-stu-id="181b5-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="181b5-106">Портал</span><span class="sxs-lookup"><span data-stu-id="181b5-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="181b5-107">В службах мультимедиа цифровые файлы отправляются в актив.</span><span class="sxs-lookup"><span data-stu-id="181b5-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="181b5-108">Hello [активов](https://docs.microsoft.com/rest/api/media/operations/asset) может содержать сущности, видео, аудио, изображения, коллекции эскизов, текст отслеживает и титров файлов (и hello метаданные об этих файлах.)  После отправки файлов hello в актив hello, контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="181b5-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="181b5-109">применить Hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="181b5-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="181b5-110">Службы мультимедиа используют значение hello hello свойство IAssetFile.Name при построении URL-адреса для hello, потоковая передача содержимого (например, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) По этой причине кодирование с помощью знака процента не допускается.</span><span class="sxs-lookup"><span data-stu-id="181b5-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="181b5-111">Здравствуйте, значение hello **имя** свойство не может иметь любой из следующих hello [процентов зарезервированные символы](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? % # []».</span><span class="sxs-lookup"><span data-stu-id="181b5-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="181b5-112">Кроме того, может существовать только один "." для расширения имени файла hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="181b5-113">Длина Hello hello имени не должна быть более 260 знаков.</span><span class="sxs-lookup"><span data-stu-id="181b5-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="181b5-114">Имеется ограничение toohello максимальный размер файла поддерживается для обработки в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="181b5-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="181b5-115">См. в разделе [это](media-services-quotas-and-limitations.md) сведения о hello ограничения размера файла.</span><span class="sxs-lookup"><span data-stu-id="181b5-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="181b5-116">Базовый рабочий процесс для передачи активы Hello состоит из hello в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="181b5-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="181b5-117">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="181b5-117">Create an Asset</span></span>
* <span data-ttu-id="181b5-118">Шифрование актива (необязательно)</span><span class="sxs-lookup"><span data-stu-id="181b5-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="181b5-119">Отправка файла tooblob хранилища</span><span class="sxs-lookup"><span data-stu-id="181b5-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="181b5-120">AMS также позволяет tooupload активы в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="181b5-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="181b5-121">Дополнительные сведения см. в [этом разделе](media-services-rest-upload-files.md#upload_in_bulk).</span><span class="sxs-lookup"><span data-stu-id="181b5-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="181b5-122">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="181b5-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="181b5-123">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="181b5-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="181b5-124">Подключение служб tooMedia</span><span class="sxs-lookup"><span data-stu-id="181b5-124">Connect tooMedia Services</span></span>

<span data-ttu-id="181b5-125">Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="181b5-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="181b5-126">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="181b5-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="181b5-127">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="181b5-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="181b5-128">Отправка ресурсов</span><span class="sxs-lookup"><span data-stu-id="181b5-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="181b5-129">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="181b5-129">Create an asset</span></span>

<span data-ttu-id="181b5-130">Ресурс — это контейнер, состоящий из нескольких наборов объектов или объектов разного типа в службах мультимедиа, в том числе видео, аудио, изображения, коллекции отпечатков, текстовые каналы и файлы скрытых субтитров.</span><span class="sxs-lookup"><span data-stu-id="181b5-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="181b5-131">В API-Интерфейс REST, создания ресурса необходимо отправить POST hello запроса tooMedia служб и поместить все сведения о свойствах ресурса в тексте запроса hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="181b5-132">Одно из свойств hello, которые можно указать при создании ресурса **параметры**.</span><span class="sxs-lookup"><span data-stu-id="181b5-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="181b5-133">**Параметры** является значением перечисления, описывающее параметры шифрования hello, которые ресурс может быть создан с.</span><span class="sxs-lookup"><span data-stu-id="181b5-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="181b5-134">Допустимым значением является одним из значений hello hello списке ниже, не сочетания значений.</span><span class="sxs-lookup"><span data-stu-id="181b5-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="181b5-135">**None** = **0**. Шифрование использоваться не будет.</span><span class="sxs-lookup"><span data-stu-id="181b5-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="181b5-136">Это значение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-136">This is hello default value.</span></span> <span data-ttu-id="181b5-137">Обратите внимание, что при использовании этого параметра содержимое не защищено при передаче или в хранилище.</span><span class="sxs-lookup"><span data-stu-id="181b5-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="181b5-138">Если планируется toodeliver MP4-файл с помощью прогрессивной загрузки, используйте этот параметр.</span><span class="sxs-lookup"><span data-stu-id="181b5-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="181b5-139">**StorageEncrypted** = **1**: Укажите, нужна ли для вашего toobe файлы, зашифрованные с помощью AES-256-разрядного шифрования для отправки и хранения.</span><span class="sxs-lookup"><span data-stu-id="181b5-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="181b5-140">Если ресурс зашифрован в хранилище, необходимо настроить политику доставки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="181b5-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="181b5-141">Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="181b5-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="181b5-142">**CommonEncryptionProtected** = **2**. Укажите, если передаются файлы, защищенные с использованием общего метода шифрования (например, PlayReady).</span><span class="sxs-lookup"><span data-stu-id="181b5-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="181b5-143">**EnvelopeEncryptionProtected** = **4**. Используйте этот параметр при отправке HLS с шифрованием AES.</span><span class="sxs-lookup"><span data-stu-id="181b5-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="181b5-144">Обратите внимание, что hello файлы необходимо были закодированы и зашифрованы диспетчером преобразования.</span><span class="sxs-lookup"><span data-stu-id="181b5-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="181b5-145">Если ресурс будет использовать шифрование, необходимо создать **ContentKey** и связать его tooyour средств, как описано в разделе hello:[как toocreate ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="181b5-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="181b5-146">Обратите внимание, что после загрузки файлов hello в актив hello, свойства шифрования tooupdate hello в hello **AssetFile** сущности со значениями hello, полученный во время hello **активов** шифрования.</span><span class="sxs-lookup"><span data-stu-id="181b5-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="181b5-147">Сделать это с помощью hello **СЛИЯНИЯ** HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="181b5-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="181b5-148">Следующий пример показывает как Hello toocreate актива.</span><span class="sxs-lookup"><span data-stu-id="181b5-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="181b5-149">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="181b5-149">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

<span data-ttu-id="181b5-150">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-150">**HTTP Response**</span></span>

<span data-ttu-id="181b5-151">В случае успешного выполнения возвращается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="181b5-151">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="181b5-152">Создание сущности AssetFile</span><span class="sxs-lookup"><span data-stu-id="181b5-152">Create an AssetFile</span></span>
<span data-ttu-id="181b5-153">Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) сущности представляет видео- или файл, хранящийся в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="181b5-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="181b5-154">Файл ресурса всегда связан с ресурсом, который, в свою очередь, может содержать один или несколько файлов ресурса.</span><span class="sxs-lookup"><span data-stu-id="181b5-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="181b5-155">задачу Hello Media Services Encoder завершается ошибкой, если объект файла ресурса не связан с цифровым файлом в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="181b5-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="181b5-156">Обратите внимание, что hello **AssetFile** экземпляра и hello фактический файл мультимедиа являются двумя отдельными объектами.</span><span class="sxs-lookup"><span data-stu-id="181b5-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="181b5-157">экземпляр AssetFile Hello содержит метаданные о файле мультимедиа hello, а файл мультимедиа hello hello фактический контент мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="181b5-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="181b5-158">После отправки файла мультимедиа в контейнер больших двоичных объектов, используется hello **СЛИЯНИЯ** hello tooupdate HTTP-запроса AssetFile со сведениями о файл (как показано далее в разделе hello).</span><span class="sxs-lookup"><span data-stu-id="181b5-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="181b5-159">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="181b5-159">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="181b5-160">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-160">**HTTP Response**</span></span>

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="181b5-161">Создание hello AccessPolicy с разрешениями на запись.</span><span class="sxs-lookup"><span data-stu-id="181b5-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="181b5-162">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="181b5-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="181b5-163">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="181b5-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="181b5-164">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="181b5-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="181b5-165">Перед отправкой файлов в хранилище больших двоичных объектов, выбор hello права политики для записи tooan активов.</span><span class="sxs-lookup"><span data-stu-id="181b5-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="181b5-166">задать toodo, учет toohello запрос HTTP сущностей AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="181b5-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="181b5-167">При создании сущности необходимо задать значение DurationInMinutes. В противном случае вы получите сообщение об ошибке 500 (внутренняя ошибка сервера).</span><span class="sxs-lookup"><span data-stu-id="181b5-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="181b5-168">Дополнительную информацию о сущностях AccessPolicy см. в разделе [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="181b5-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="181b5-169">Следующий пример показывает как Hello toocreate AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="181b5-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="181b5-170">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="181b5-170">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="181b5-171">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="181b5-171">**HTTP Request**</span></span>

    If successful, hello following response is returned:

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="181b5-172">Получить hello передать URL-адрес</span><span class="sxs-lookup"><span data-stu-id="181b5-172">Get hello Upload URL</span></span>
<span data-ttu-id="181b5-173">tooreceive Здравствуйте непосредственную отправку URL-адрес, создания указателя SAS.</span><span class="sxs-lookup"><span data-stu-id="181b5-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="181b5-174">Указатели определяют время начала hello и тип конечной точки подключения для клиентов, которые хотят tooaccess файлы в активе.</span><span class="sxs-lookup"><span data-stu-id="181b5-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="181b5-175">Можно создать несколько объектов указателя для заданного параметра AccessPolicy и активов пары toohandle другого клиента, запросы и требования.</span><span class="sxs-lookup"><span data-stu-id="181b5-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="181b5-176">Каждый из этих указателей использует значения StartTime hello и hello DurationInMinutes параметра hello AccessPolicy toodetermine hello продолжительность URL-адрес может использоваться.</span><span class="sxs-lookup"><span data-stu-id="181b5-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="181b5-177">Дополнительную информацию см. в разделе [Указатель](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="181b5-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="181b5-178">URL-адрес SAS имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="181b5-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="181b5-179">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="181b5-179">Some considerations apply:</span></span>

* <span data-ttu-id="181b5-180">С определенным ресурсом нельзя связать более пяти уникальных указателей одновременно.</span><span class="sxs-lookup"><span data-stu-id="181b5-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="181b5-181">Дополнительную информацию см. в разделе "Указатель".</span><span class="sxs-lookup"><span data-stu-id="181b5-181">For more information, see Locator.</span></span>
* <span data-ttu-id="181b5-182">Если вам требуется tooupload файлов сразу, необходимо задать toofive минут значение StartTime вашей hello текущее время.</span><span class="sxs-lookup"><span data-stu-id="181b5-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="181b5-183">Это необходимо из-за возможного расхождения в показаниях часов на клиентском компьютере и в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="181b5-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="181b5-184">Кроме того, значение StartTime должно находиться в hello следующая формата даты и времени: гггг-мм-: ssz (например, «2014-05-23T17:53:50Z»).</span><span class="sxs-lookup"><span data-stu-id="181b5-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="181b5-185">Может быть 30-40 секунд задержки после создания локатора toowhen доступен для использования.</span><span class="sxs-lookup"><span data-stu-id="181b5-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="181b5-186">Эта проблема относится tooboth URL-адрес SAS и Локаторы источника.</span><span class="sxs-lookup"><span data-stu-id="181b5-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="181b5-187">Hello в следующем примере показано, как toocreate указатель URL-адрес SAS, в соответствии с определением hello свойство типа в тексте запроса hello («1» для указателя SAS) и «2» для указателя origin по требованию.</span><span class="sxs-lookup"><span data-stu-id="181b5-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="181b5-188">Hello **путь** hello URL-адрес, что необходимо использовать tooupload файл содержит свойство, которое возвращается.</span><span class="sxs-lookup"><span data-stu-id="181b5-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="181b5-189">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="181b5-189">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

<span data-ttu-id="181b5-190">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-190">**HTTP Response**</span></span>

<span data-ttu-id="181b5-191">В случае успешного выполнения возвращается следующий ответ hello:</span><span class="sxs-lookup"><span data-stu-id="181b5-191">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="181b5-192">Отправка файла в контейнер хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="181b5-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="181b5-193">После создания hello AccessPolicy и указателя набор hello файл находится загруженный tooan контейнер хранилища больших двоичных объектов, с помощью hello API REST хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="181b5-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="181b5-194">Hello файлы необходимо отправить в виде блочных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="181b5-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="181b5-195">Страничные BLOB-объекты не поддерживаются службами мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="181b5-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="181b5-196">Необходимо добавить имя файла hello hello файла требуется tooupload toohello локатора **путь** значение, полученное в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="181b5-197">Например, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="181b5-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="181b5-198">.</span><span class="sxs-lookup"><span data-stu-id="181b5-198">.</span></span> <span data-ttu-id="181b5-199">.</span><span class="sxs-lookup"><span data-stu-id="181b5-199">.</span></span> <span data-ttu-id="181b5-200">.</span><span class="sxs-lookup"><span data-stu-id="181b5-200">.</span></span> 
> 
> 

<span data-ttu-id="181b5-201">Дополнительную информацию о работе с большими двоичными объектами службы хранилища Azure см. в статье [API-интерфейс REST службы BLOB-объектов](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="181b5-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="181b5-202">Hello обновление AssetFile</span><span class="sxs-lookup"><span data-stu-id="181b5-202">Update hello AssetFile</span></span>
<span data-ttu-id="181b5-203">После отправки файла обновите сведения о hello FileAsset размер (и другие).</span><span class="sxs-lookup"><span data-stu-id="181b5-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="181b5-204">Например:</span><span class="sxs-lookup"><span data-stu-id="181b5-204">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="181b5-205">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-205">**HTTP Response**</span></span>

<span data-ttu-id="181b5-206">Если успешно, следующие hello возвращается: HTTP/1.1 204 Нет содержимого</span><span class="sxs-lookup"><span data-stu-id="181b5-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="181b5-207">Удаление локатора hello и AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="181b5-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="181b5-208">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="181b5-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="181b5-209">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-209">**HTTP Response**</span></span>

<span data-ttu-id="181b5-210">В случае успешного выполнения возвращается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="181b5-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="181b5-211">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="181b5-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="181b5-212">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-212">**HTTP Response**</span></span>

<span data-ttu-id="181b5-213">В случае успешного выполнения возвращается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="181b5-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="181b5-214"><a id="upload_in_bulk"></a>Отправка ресурсов в пакетном режиме</span><span class="sxs-lookup"><span data-stu-id="181b5-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="181b5-215">Создать hello IngestManifest</span><span class="sxs-lookup"><span data-stu-id="181b5-215">Create hello IngestManifest</span></span>
<span data-ttu-id="181b5-216">Hello IngestManifest — это контейнер для набора активов, файлов ресурсов и статистических данных, которые можно использовать toodetermine hello ход выполнения массовой передачи для набора hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="181b5-217">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="181b5-217">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="181b5-218">Создание ресурсов</span><span class="sxs-lookup"><span data-stu-id="181b5-218">Create assets</span></span>
<span data-ttu-id="181b5-219">Перед созданием hello IngestManifestAsset, необходимо toocreate hello актива, который будет выполняться с помощью массовой передачи.</span><span class="sxs-lookup"><span data-stu-id="181b5-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="181b5-220">Ресурс — это контейнер, состоящий из нескольких наборов объектов или объектов разного типа в службах мультимедиа, в том числе видео, аудио, изображения, коллекции отпечатков, текстовые каналы и файлы скрытых субтитров.</span><span class="sxs-lookup"><span data-stu-id="181b5-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="181b5-221">В hello REST API создания ресурса необходимо отправки tooMicrosoft запрос HTTP POST служб мультимедиа Azure и поместить все сведения о свойствах ресурса в тексте запроса hello. В этом примере hello активов создается с помощью параметра StorageEncrption(1) hello, входящий в состав hello текст запроса.</span><span class="sxs-lookup"><span data-stu-id="181b5-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="181b5-222">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-222">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="181b5-223">Создание IngestManifestAssets hello</span><span class="sxs-lookup"><span data-stu-id="181b5-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="181b5-224">Сущность IngestManifestAssets представляет ресурсы в сущности IngestManifest, используемые при массовом приеме.</span><span class="sxs-lookup"><span data-stu-id="181b5-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="181b5-225">Привет, по сути, связывают манифест toohello активов hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="181b5-226">Службы мультимедиа Azure отслеживает внутренне для отправки файла hello основании toohello связанные коллекции IngestManifestFiles IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="181b5-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="181b5-227">После загрузки файлов, hello ресурса завершено.</span><span class="sxs-lookup"><span data-stu-id="181b5-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="181b5-228">Новую сущность IngestManifestAsset можно создать с помощью HTTP-запроса POST.</span><span class="sxs-lookup"><span data-stu-id="181b5-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="181b5-229">В тексте запроса hello включают hello код IngestManifest и hello идентификатор ресурса, которые IngestManifestAsset должен связать для массовой передачи hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="181b5-230">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-230">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="181b5-231">Создать hello IngestManifestFiles для каждого ресурса</span><span class="sxs-lookup"><span data-stu-id="181b5-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="181b5-232">IngestManifestFile фактически представляет собой большой двоичный объект видео- или аудиоданных, который будет отправляться в рамках массового приема.</span><span class="sxs-lookup"><span data-stu-id="181b5-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="181b5-233">Свойства не являются обязательными, если активов hello не использует параметр шифрования, связанные с шифрованием.</span><span class="sxs-lookup"><span data-stu-id="181b5-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="181b5-234">пример Hello, используемые в данном разделе показано создание IngestManifestFile, который использует StorageEncryption для ранее создания активов hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="181b5-235">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-235">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="181b5-236">Отправка файлов hello tooBlob хранилища</span><span class="sxs-lookup"><span data-stu-id="181b5-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="181b5-237">Можно использовать любое высокоскоростное клиентское приложение может загрузить контейнер больших двоичных объектов хранилища для активов файлы hello toohello Uri, предоставляемые hello свойство BlobStorageUriForUpload hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="181b5-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="181b5-238">[Приложение Aspera On Demand for Azure](http://go.microsoft.com/fwlink/?LinkId=272001)— одна из наиболее примечательных служб высокоскоростной передачи.</span><span class="sxs-lookup"><span data-stu-id="181b5-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="181b5-239">Контроль за ходом выполнения массового приема</span><span class="sxs-lookup"><span data-stu-id="181b5-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="181b5-240">Вы можете отслеживать ход выполнения массовой передачи для IngestManifest путем опроса свойства статистики hello hello IngestManifest hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="181b5-241">Это свойство комплексного типа, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="181b5-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="181b5-242">hello toopoll свойства статистики отправить запрос HTTP GET, передав hello код IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="181b5-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="181b5-243">Создание сущности ContentKeys, используемой для шифрования</span><span class="sxs-lookup"><span data-stu-id="181b5-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="181b5-244">Если ресурс будет использовать шифрование, необходимо создать ContentKey toobe hello, используемый для шифрования перед созданием hello файлов активов.</span><span class="sxs-lookup"><span data-stu-id="181b5-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="181b5-245">Для шифрования хранилища hello следующие свойства должны быть включены в текст запроса hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="181b5-246">Свойство текста запроса</span><span class="sxs-lookup"><span data-stu-id="181b5-246">Request body property</span></span> | <span data-ttu-id="181b5-247">Описание</span><span class="sxs-lookup"><span data-stu-id="181b5-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="181b5-248">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="181b5-248">Id</span></span> |<span data-ttu-id="181b5-249">Hello код ContentKey, который мы создаем сами с помощью следующих hello отформатировать, «nb:kid:UUID:<NEW GUID>».</span><span class="sxs-lookup"><span data-stu-id="181b5-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="181b5-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="181b5-250">ContentKeyType</span></span> |<span data-ttu-id="181b5-251">Это тип ключа контента hello как целое число для этого ключа контента.</span><span class="sxs-lookup"><span data-stu-id="181b5-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="181b5-252">Мы передаем hello значение 1 для шифрования хранилища.</span><span class="sxs-lookup"><span data-stu-id="181b5-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="181b5-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="181b5-253">EncryptedContentKey</span></span> |<span data-ttu-id="181b5-254">Мы создаем новое значение ключа содержимого, которое представляет собой 256-битное (32-байтное) значение.</span><span class="sxs-lookup"><span data-stu-id="181b5-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="181b5-255">Hello ключ шифруется с помощью hello сертификата хранилища шифрования X.509 который получен из службы мультимедиа Microsoft Azure, выполнив запрос HTTP GET для hello GetProtectionKeyId и GetProtectionKey методов.</span><span class="sxs-lookup"><span data-stu-id="181b5-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="181b5-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="181b5-256">ProtectionKeyId</span></span> |<span data-ttu-id="181b5-257">Это является hello код ключа защиты для hello сертификата хранилища шифрования X.509, используемый tooencrypt ключа контента.</span><span class="sxs-lookup"><span data-stu-id="181b5-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="181b5-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="181b5-258">ProtectionKeyType</span></span> |<span data-ttu-id="181b5-259">Это тип шифрования hello для hello защиты ключа, который был ключ содержимого используется tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="181b5-260">В нашем примере этим значением является StorageEncryption(1).</span><span class="sxs-lookup"><span data-stu-id="181b5-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="181b5-261">Checksum</span><span class="sxs-lookup"><span data-stu-id="181b5-261">Checksum</span></span> |<span data-ttu-id="181b5-262">Hello MD5 вычисленная контрольная сумма для ключа контента hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="181b5-263">Она рассчитывается при шифровании кода hello контента с помощью ключа содержимого hello.</span><span class="sxs-lookup"><span data-stu-id="181b5-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="181b5-264">Hello примере кода показано, как toocalculate hello контрольной суммы.</span><span class="sxs-lookup"><span data-stu-id="181b5-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="181b5-265">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-265">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="181b5-266">Связывание ContentKey hello toohello активов</span><span class="sxs-lookup"><span data-stu-id="181b5-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="181b5-267">Hello ContentKey — связанные tooone или несколько ресурсов, отправив запрос HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="181b5-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="181b5-268">Hello следующий запрос — пример toolink hello пример ContentKey toohello примере актив по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="181b5-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="181b5-269">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-269">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="181b5-270">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="181b5-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="181b5-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="181b5-271">Next steps</span></span>

<span data-ttu-id="181b5-272">Теперь можно закодировать отправленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="181b5-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="181b5-273">Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="181b5-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="181b5-274">Также можно использовать функции Azure tootrigger задание кодирования на основе файла, поступающих в контейнере hello настроен.</span><span class="sxs-lookup"><span data-stu-id="181b5-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="181b5-275">Дополнительные сведения см. в [этом примере](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="181b5-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="181b5-276">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="181b5-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="181b5-277">Отзывы</span><span class="sxs-lookup"><span data-stu-id="181b5-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

