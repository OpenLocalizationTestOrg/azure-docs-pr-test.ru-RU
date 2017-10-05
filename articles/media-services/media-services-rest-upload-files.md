---
title: "Передача файлов в учетную запись служб мультимедиа с помощью REST | Документация Майкрософт"
description: "Узнайте, как включить мультимедийное содержимое в службы мультимедиа, создав и отправив ресурс."
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
ms.openlocfilehash: 955356ffe6fc524c1528364add7e2c2a336137b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="84c9c-103">Передача файлов в учетную запись служб мультимедиа с помощью REST</span><span class="sxs-lookup"><span data-stu-id="84c9c-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84c9c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="84c9c-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="84c9c-105">REST</span><span class="sxs-lookup"><span data-stu-id="84c9c-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="84c9c-106">Портал</span><span class="sxs-lookup"><span data-stu-id="84c9c-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="84c9c-107">В службах мультимедиа цифровые файлы отправляются в актив.</span><span class="sxs-lookup"><span data-stu-id="84c9c-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="84c9c-108">Сущность [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) может содержать видео, аудио, изображения, коллекции эскизов, текстовые дорожки и файлы скрытых субтитров (а также метаданные этих файлов).  После отправки этих файлов в ресурс содержимое сохраняется в безопасном расположении в облаке для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="84c9c-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="84c9c-109">Действительны следующие условия.</span><span class="sxs-lookup"><span data-stu-id="84c9c-109">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="84c9c-110">Службы мультимедиа используют значение свойства IAssetFile.Name при создании URL-адресов для потоковой передачи содержимого (например, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) По этой причине кодирование с помощью знака процента не допускается.</span><span class="sxs-lookup"><span data-stu-id="84c9c-110">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="84c9c-111">Значение свойства **Name** не может содержать такие [зарезервированные знаки, используемые для кодировки URL-адресов](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="84c9c-111">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="84c9c-112">Кроме того, может использоваться только один знак "." для расширения имени файла.</span><span class="sxs-lookup"><span data-stu-id="84c9c-112">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="84c9c-113">Длина имени не должна превышать 260 знаков.</span><span class="sxs-lookup"><span data-stu-id="84c9c-113">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="84c9c-114">Существует ограничение на максимальный размер файла, который могут обработать службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="84c9c-114">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="84c9c-115">Подробные сведения об этом см. [здесь](media-services-quotas-and-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="84c9c-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> 

<span data-ttu-id="84c9c-116">Основная процедура отправки ресурсов делится на следующие разделы:</span><span class="sxs-lookup"><span data-stu-id="84c9c-116">The basic workflow for uploading Assets is divided into the following sections:</span></span>

* <span data-ttu-id="84c9c-117">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="84c9c-117">Create an Asset</span></span>
* <span data-ttu-id="84c9c-118">Шифрование актива (необязательно)</span><span class="sxs-lookup"><span data-stu-id="84c9c-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="84c9c-119">Отправка файла в хранилище больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="84c9c-119">Upload a file to blob storage</span></span>

<span data-ttu-id="84c9c-120">AMS также позволяет передавать ресурсы в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="84c9c-120">AMS also enables you to upload assets in bulk.</span></span> <span data-ttu-id="84c9c-121">Дополнительные сведения см. в [этом разделе](media-services-rest-upload-files.md#upload_in_bulk).</span><span class="sxs-lookup"><span data-stu-id="84c9c-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="84c9c-122">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="84c9c-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="84c9c-123">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="84c9c-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="84c9c-124">Подключение к службам мультимедиа</span><span class="sxs-lookup"><span data-stu-id="84c9c-124">Connect to Media Services</span></span>

<span data-ttu-id="84c9c-125">Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="84c9c-125">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="84c9c-126">После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="84c9c-126">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="84c9c-127">Используйте для последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="84c9c-127">You must make subsequent calls to the new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="84c9c-128">Отправка ресурсов</span><span class="sxs-lookup"><span data-stu-id="84c9c-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="84c9c-129">Создание ресурса</span><span class="sxs-lookup"><span data-stu-id="84c9c-129">Create an asset</span></span>

<span data-ttu-id="84c9c-130">Ресурс — это контейнер, состоящий из нескольких наборов объектов или объектов разного типа в службах мультимедиа, в том числе видео, аудио, изображения, коллекции отпечатков, текстовые каналы и файлы скрытых субтитров.</span><span class="sxs-lookup"><span data-stu-id="84c9c-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="84c9c-131">Для создания ресурса в REST API нужно отправить запрос POST службам мультимедиа и разместить любую информацию о свойствах ресурса в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="84c9c-131">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="84c9c-132">Одно из свойств, которые можно указать при создании ресурса, – **Options**.</span><span class="sxs-lookup"><span data-stu-id="84c9c-132">One of the properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="84c9c-133">**Options** – это перечисление, описывающее параметры шифрования, которые могут использоваться при создании ресурса.</span><span class="sxs-lookup"><span data-stu-id="84c9c-133">**Options** is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="84c9c-134">Допустимые значения приведены в списке ниже (допустимы только сами значения, а не их сочетания).</span><span class="sxs-lookup"><span data-stu-id="84c9c-134">A valid value is one of the values from the list below, not a combination of values.</span></span> 

* <span data-ttu-id="84c9c-135">**None** = **0**. Шифрование использоваться не будет.</span><span class="sxs-lookup"><span data-stu-id="84c9c-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="84c9c-136">Это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="84c9c-136">This is the default value.</span></span> <span data-ttu-id="84c9c-137">Обратите внимание, что при использовании этого параметра содержимое не защищено при передаче или в хранилище.</span><span class="sxs-lookup"><span data-stu-id="84c9c-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="84c9c-138">Используйте этот параметр, если MP4-файл планируется доставить с помощью поэтапного скачивания.</span><span class="sxs-lookup"><span data-stu-id="84c9c-138">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="84c9c-139">**StorageEncrypted** = **1**. Укажите, если нужно использовать 256-разрядное шифрование AES для хранения и передачи файлов.</span><span class="sxs-lookup"><span data-stu-id="84c9c-139">**StorageEncrypted** = **1**: Specify if you want for your files to be encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="84c9c-140">Если ресурс зашифрован в хранилище, необходимо настроить политику доставки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="84c9c-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="84c9c-141">Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="84c9c-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="84c9c-142">**CommonEncryptionProtected** = **2**. Укажите, если передаются файлы, защищенные с использованием общего метода шифрования (например, PlayReady).</span><span class="sxs-lookup"><span data-stu-id="84c9c-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="84c9c-143">**EnvelopeEncryptionProtected** = **4**. Используйте этот параметр при отправке HLS с шифрованием AES.</span><span class="sxs-lookup"><span data-stu-id="84c9c-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="84c9c-144">Обратите внимание, что файлы должны быть закодированы и зашифрованы с помощью Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="84c9c-144">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="84c9c-145">Если для ресурса-контейнера будет использоваться шифрование, то следует создать сущность **ContentKey** и связать ее с ресурсом-контейнером, как описано в разделе[Как создать ключ содержимого](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="84c9c-145">If your asset will use encryption, you must create a **ContentKey** and link it to your asset as described in the following topic:[How to create a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="84c9c-146">Обратите внимание, что после передачи файлов в ресурс-контейнер необходимо обновить свойства шифрования для сущности **AssetFile**, задав значения, полученные во время шифрования ресурса **Asset**.</span><span class="sxs-lookup"><span data-stu-id="84c9c-146">Note that after you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption.</span></span> <span data-ttu-id="84c9c-147">Сделать это можно с помощью HTTP-запроса **MERGE** .</span><span class="sxs-lookup"><span data-stu-id="84c9c-147">Do it by using the **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="84c9c-148">В следующем примере показано, как создать ресурс.</span><span class="sxs-lookup"><span data-stu-id="84c9c-148">The following example shows how to create an asset.</span></span>

<span data-ttu-id="84c9c-149">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="84c9c-149">**HTTP Request**</span></span>

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

<span data-ttu-id="84c9c-150">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-150">**HTTP Response**</span></span>

<span data-ttu-id="84c9c-151">При успешном выполнении возвращается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="84c9c-151">If successful, the following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="84c9c-152">Создание сущности AssetFile</span><span class="sxs-lookup"><span data-stu-id="84c9c-152">Create an AssetFile</span></span>
<span data-ttu-id="84c9c-153">Сущность [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) представляет собой аудио- или видеофайл, который хранится в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="84c9c-153">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="84c9c-154">Файл ресурса всегда связан с ресурсом, который, в свою очередь, может содержать один или несколько файлов ресурса.</span><span class="sxs-lookup"><span data-stu-id="84c9c-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="84c9c-155">Задача кодировщика служб мультимедиа завершится с ошибкой, если объект файла ресурса не связан с цифровым файлом в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="84c9c-155">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="84c9c-156">Обратите внимание, что экземпляр **AssetFile** и фактический файл мультимедиа – это два разных объекта.</span><span class="sxs-lookup"><span data-stu-id="84c9c-156">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="84c9c-157">Экземпляр AssetFile содержит метаданные о файле мультимедиа, а сам файл мультимедиа — фактическое мультимедийное содержимое.</span><span class="sxs-lookup"><span data-stu-id="84c9c-157">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="84c9c-158">После передачи цифрового файла мультимедиа в контейнер больших двоичных объектов будет использоваться HTTP-запрос **MERGE** , чтобы обновить сущность AssetFile информацией о файле мультимедиа (как показано далее в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="84c9c-158">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span> 

<span data-ttu-id="84c9c-159">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="84c9c-159">**HTTP Request**</span></span>

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

<span data-ttu-id="84c9c-160">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-160">**HTTP Response**</span></span>

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

### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="84c9c-161">Создание сущности AccessPolicy с разрешением на запись</span><span class="sxs-lookup"><span data-stu-id="84c9c-161">Creating the AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="84c9c-162">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="84c9c-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="84c9c-163">Следует указывать один и тот же идентификатор политики, если вы используете те же дни, разрешения доступа и т. д. Например, политики для указателей, которые должны оставаться на месте в течение длительного времени (не политики передачи).</span><span class="sxs-lookup"><span data-stu-id="84c9c-163">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="84c9c-164">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="84c9c-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="84c9c-165">Перед отправкой файлов в хранилище больших двоичных объектов настройте для политики доступа права на запись в ресурс.</span><span class="sxs-lookup"><span data-stu-id="84c9c-165">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="84c9c-166">Для этого отправьте запрос HTTP POST в набор сущностей AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="84c9c-166">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="84c9c-167">При создании сущности необходимо задать значение DurationInMinutes. В противном случае вы получите сообщение об ошибке 500 (внутренняя ошибка сервера).</span><span class="sxs-lookup"><span data-stu-id="84c9c-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="84c9c-168">Дополнительную информацию о сущностях AccessPolicy см. в разделе [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="84c9c-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="84c9c-169">В следующем примере показано, как создать AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="84c9c-169">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="84c9c-170">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="84c9c-170">**HTTP Request**</span></span>

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

<span data-ttu-id="84c9c-171">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="84c9c-171">**HTTP Request**</span></span>

    If successful, the following response is returned:

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

### <a name="get-the-upload-url"></a><span data-ttu-id="84c9c-172">Получение URL-адреса отправки</span><span class="sxs-lookup"><span data-stu-id="84c9c-172">Get the Upload URL</span></span>
<span data-ttu-id="84c9c-173">Чтобы получить фактический URL-адрес отправки, создайте указатель SAS.</span><span class="sxs-lookup"><span data-stu-id="84c9c-173">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="84c9c-174">Указатели определяют время начала и тип конечной точки подключения для клиентов, которым требуется доступ к файлам в ресурсе.</span><span class="sxs-lookup"><span data-stu-id="84c9c-174">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="84c9c-175">Для обработки разных запросов клиентов и удовлетворения их потребностей можно создать несколько сущностей Locator для заданной пары AccessPolicy и Asset.</span><span class="sxs-lookup"><span data-stu-id="84c9c-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="84c9c-176">Каждый из этих указателей использует значения StartTime и DurationInMinutes сущности AccessPolicy, чтобы определить время, в течение которого можно использовать URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="84c9c-176">Each of these Locators use the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="84c9c-177">Дополнительную информацию см. в разделе [Указатель](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="84c9c-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="84c9c-178">Ниже приведен формат URL-адреса SAS:</span><span class="sxs-lookup"><span data-stu-id="84c9c-178">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="84c9c-179">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="84c9c-179">Some considerations apply:</span></span>

* <span data-ttu-id="84c9c-180">С определенным ресурсом нельзя связать более пяти уникальных указателей одновременно.</span><span class="sxs-lookup"><span data-stu-id="84c9c-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="84c9c-181">Дополнительную информацию см. в разделе "Указатель".</span><span class="sxs-lookup"><span data-stu-id="84c9c-181">For more information, see Locator.</span></span>
* <span data-ttu-id="84c9c-182">Если вам необходимо незамедлительно передать файлы, следует задать для StartTime значение, на пять минут предшествующее текущему моменту времени.</span><span class="sxs-lookup"><span data-stu-id="84c9c-182">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="84c9c-183">Это необходимо из-за возможного расхождения в показаниях часов на клиентском компьютере и в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="84c9c-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="84c9c-184">Кроме того, значение StartTime должно быть задано в следующем формате даты и времени: ГГГГ-ММ-ДДТЧЧ:мм:ссZ (например, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="84c9c-184">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="84c9c-185">Задержка между моментом создания сущности Locator и моментом, когда ее можно начинать использовать, может составлять 30-40 секунд.</span><span class="sxs-lookup"><span data-stu-id="84c9c-185">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="84c9c-186">Это касается URL-адресов SAS и исходных указателей.</span><span class="sxs-lookup"><span data-stu-id="84c9c-186">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="84c9c-187">В следующем примере показано, как создать указатель URL-адреса SAS в соответствии со значением свойства Type в тексте запроса (1 для указателя SAS и 2 для исходного указателя по требованию).</span><span class="sxs-lookup"><span data-stu-id="84c9c-187">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="84c9c-188">Возвращенное свойство **Path** содержит URL-адрес, который необходимо использовать для отправки файла.</span><span class="sxs-lookup"><span data-stu-id="84c9c-188">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="84c9c-189">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="84c9c-189">**HTTP Request**</span></span>

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

<span data-ttu-id="84c9c-190">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-190">**HTTP Response**</span></span>

<span data-ttu-id="84c9c-191">При успешном выполнении возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="84c9c-191">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="84c9c-192">Отправка файла в контейнер хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="84c9c-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="84c9c-193">Когда сущности AccessPolicy и Locator будут заданы, фактические файлы отправляются в контейнер хранилища больших двоичных объектов Azure с помощью интерфейсов REST API службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="84c9c-193">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="84c9c-194">Файлы необходимо отправить в виде блочных BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="84c9c-194">You must upload the files as block blobs.</span></span> <span data-ttu-id="84c9c-195">Страничные BLOB-объекты не поддерживаются службами мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="84c9c-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="84c9c-196">Нужно добавить имя файла для файла, который необходимо передать, в значение **Path** сущности Locator, полученное в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="84c9c-196">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="84c9c-197">Например, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="84c9c-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="84c9c-198">.</span><span class="sxs-lookup"><span data-stu-id="84c9c-198">.</span></span> <span data-ttu-id="84c9c-199">.</span><span class="sxs-lookup"><span data-stu-id="84c9c-199">.</span></span> <span data-ttu-id="84c9c-200">.</span><span class="sxs-lookup"><span data-stu-id="84c9c-200">.</span></span> 
> 
> 

<span data-ttu-id="84c9c-201">Дополнительную информацию о работе с большими двоичными объектами службы хранилища Azure см. в статье [API-интерфейс REST службы BLOB-объектов](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="84c9c-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="84c9c-202">Обновление AssetFile</span><span class="sxs-lookup"><span data-stu-id="84c9c-202">Update the AssetFile</span></span>
<span data-ttu-id="84c9c-203">После отправки файла обновите информацию о размере сущности FileAsset (и другую информацию).</span><span class="sxs-lookup"><span data-stu-id="84c9c-203">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="84c9c-204">Например:</span><span class="sxs-lookup"><span data-stu-id="84c9c-204">For example:</span></span>

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


<span data-ttu-id="84c9c-205">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-205">**HTTP Response**</span></span>

<span data-ttu-id="84c9c-206">При успешном выполнении возвращается следующий результат: HTTP/1.1 204 Нет содержимого</span><span class="sxs-lookup"><span data-stu-id="84c9c-206">If successful, the following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="84c9c-207">Удаление Locator и AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="84c9c-207">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="84c9c-208">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="84c9c-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="84c9c-209">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-209">**HTTP Response**</span></span>

<span data-ttu-id="84c9c-210">При успешном выполнении возвращается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="84c9c-210">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="84c9c-211">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="84c9c-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="84c9c-212">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-212">**HTTP Response**</span></span>

<span data-ttu-id="84c9c-213">При успешном выполнении возвращается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="84c9c-213">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="84c9c-214"><a id="upload_in_bulk"></a>Отправка ресурсов в пакетном режиме</span><span class="sxs-lookup"><span data-stu-id="84c9c-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-the-ingestmanifest"></a><span data-ttu-id="84c9c-215">Создание сущности IngestManifest</span><span class="sxs-lookup"><span data-stu-id="84c9c-215">Create the IngestManifest</span></span>
<span data-ttu-id="84c9c-216">IngestManifest — это контейнер для набора ресурсов, файлов ресурсов и статистических данных, которые можно использовать для определения хода массового приема этого набора.</span><span class="sxs-lookup"><span data-stu-id="84c9c-216">The IngestManifest is a container for a set of assets, asset files, and statistic information that can be used to determine the progress of bulk ingesting for the set.</span></span>

<span data-ttu-id="84c9c-217">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="84c9c-217">**HTTP Request**</span></span>

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

### <a name="create-assets"></a><span data-ttu-id="84c9c-218">Создание ресурсов</span><span class="sxs-lookup"><span data-stu-id="84c9c-218">Create assets</span></span>
<span data-ttu-id="84c9c-219">Прежде чем создать манифест IngestManifestAsset, необходимо создать ресурс, который будет выполняться с помощью массового приема.</span><span class="sxs-lookup"><span data-stu-id="84c9c-219">Before creating the IngestManifestAsset, you need to create the Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="84c9c-220">Ресурс — это контейнер, состоящий из нескольких наборов объектов или объектов разного типа в службах мультимедиа, в том числе видео, аудио, изображения, коллекции отпечатков, текстовые каналы и файлы скрытых субтитров.</span><span class="sxs-lookup"><span data-stu-id="84c9c-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="84c9c-221">Для создания ресурса в REST API нужно отправить HTTP-запрос POST службам мультимедиа Microsoft Azure и разместить информацию о свойствах ресурса в тексте запроса. В данном примере ресурс создается с помощью параметра StorageEncrption(1), включенного в текст запроса.</span><span class="sxs-lookup"><span data-stu-id="84c9c-221">In the REST API, creating an Asset requires sending a HTTP POST request to Microsoft Azure Media Services and placing any property information about your asset in the request body.In this example, the Asset is created using the StorageEncrption(1) option included with the request body.</span></span>

<span data-ttu-id="84c9c-222">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-222">**HTTP Response**</span></span>

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

### <a name="create-the-ingestmanifestassets"></a><span data-ttu-id="84c9c-223">Создание сущности IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="84c9c-223">Create the IngestManifestAssets</span></span>
<span data-ttu-id="84c9c-224">Сущность IngestManifestAssets представляет ресурсы в сущности IngestManifest, используемые при массовом приеме.</span><span class="sxs-lookup"><span data-stu-id="84c9c-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="84c9c-225">По сути это связь ресурса с манифестом.</span><span class="sxs-lookup"><span data-stu-id="84c9c-225">The basically link the asset to the manifest.</span></span> <span data-ttu-id="84c9c-226">Службы мультимедиа Azure выполняет внутренний поиск отправки файлов, используя для этого коллекцию IngestManifestFiles, связанную с IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="84c9c-226">Azure Media Services watches internally for the file upload based on IngestManifestFiles collection associated to the IngestManifestAsset.</span></span> <span data-ttu-id="84c9c-227">После отправки этих файлов ресурс считается завершенным.</span><span class="sxs-lookup"><span data-stu-id="84c9c-227">Once these files are uploaded, the asset is completed.</span></span> <span data-ttu-id="84c9c-228">Новую сущность IngestManifestAsset можно создать с помощью HTTP-запроса POST.</span><span class="sxs-lookup"><span data-stu-id="84c9c-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="84c9c-229">В текст запроса включите идентификатор IngestManifest и идентификатор ресурса, которые IngestManifestAsset должен связать воедино для массового приема.</span><span class="sxs-lookup"><span data-stu-id="84c9c-229">In the request body, include the IngestManifest Id and the Asset Id that the IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="84c9c-230">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-230">**HTTP Response**</span></span>

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


### <a name="create-the-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="84c9c-231">Создание сущности IngestManifestFiles для каждого ресурса</span><span class="sxs-lookup"><span data-stu-id="84c9c-231">Create the IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="84c9c-232">IngestManifestFile фактически представляет собой большой двоичный объект видео- или аудиоданных, который будет отправляться в рамках массового приема.</span><span class="sxs-lookup"><span data-stu-id="84c9c-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="84c9c-233">Свойства, связанные с шифрованием, не являются обязательными, если только в ресурсе не применяется шифрование.</span><span class="sxs-lookup"><span data-stu-id="84c9c-233">Encryption related properties are not required unless the asset is using an encryption option.</span></span> <span data-ttu-id="84c9c-234">В примере, который приводится в этом разделе, демонстрируется создание сущности IngestManifestFile, которая использует для созданного ранее ресурса параметр StorageEncryption.</span><span class="sxs-lookup"><span data-stu-id="84c9c-234">The example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for the Asset previously created.</span></span>

<span data-ttu-id="84c9c-235">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-235">**HTTP Response**</span></span>

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

### <a name="upload-the-files-to-blob-storage"></a><span data-ttu-id="84c9c-236">Отправка файлов в хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="84c9c-236">Upload the Files to Blob Storage</span></span>
<span data-ttu-id="84c9c-237">При этом можно использовать любое высокоскоростное клиентское приложение, которое может передавать файлы ресурсов по универсальному коду ресурса (URI) контейнера хранилища больших двоичных объектов, предоставляемому свойством BlobStorageUriForUpload сущности IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="84c9c-237">You can use any high speed client application capable of uploading the asset files to the blob storage container Uri provided by the BlobStorageUriForUpload property of the IngestManifest.</span></span> <span data-ttu-id="84c9c-238">[Приложение Aspera On Demand for Azure](http://go.microsoft.com/fwlink/?LinkId=272001)— одна из наиболее примечательных служб высокоскоростной передачи.</span><span class="sxs-lookup"><span data-stu-id="84c9c-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="84c9c-239">Контроль за ходом выполнения массового приема</span><span class="sxs-lookup"><span data-stu-id="84c9c-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="84c9c-240">Ход выполнения массового приема операций для сущности IngestManifest можно отслеживать путем опроса свойства Statistics сущности IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="84c9c-240">You can monitor the progress of bulk ingesting operations for an IngestManifest by polling the Statistics property of the IngestManifest.</span></span> <span data-ttu-id="84c9c-241">Это свойство комплексного типа, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="84c9c-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="84c9c-242">Чтобы опросить свойство Statistics, отправьте HTTP-запрос GET, передав идентификатор IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="84c9c-242">To poll the Statistics property, submit a HTTP GET request passing the IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="84c9c-243">Создание сущности ContentKeys, используемой для шифрования</span><span class="sxs-lookup"><span data-stu-id="84c9c-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="84c9c-244">Если ваш ресурс будет использовать шифрование, прежде чем создавать для него файлы ресурсов, создайте необходимую для шифрования сущность ContentKeys.</span><span class="sxs-lookup"><span data-stu-id="84c9c-244">If your asset will use encryption, you must create the ContentKey to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="84c9c-245">Для шифрования хранилища в текст запроса необходимо включить указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="84c9c-245">For storage encryption, the following properties should be included in the request body.</span></span>

| <span data-ttu-id="84c9c-246">Свойство текста запроса</span><span class="sxs-lookup"><span data-stu-id="84c9c-246">Request body property</span></span> | <span data-ttu-id="84c9c-247">Описание</span><span class="sxs-lookup"><span data-stu-id="84c9c-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="84c9c-248">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="84c9c-248">Id</span></span> |<span data-ttu-id="84c9c-249">Идентификатор ContentKey, созданный нами в следующем формате "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="84c9c-249">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="84c9c-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="84c9c-250">ContentKeyType</span></span> |<span data-ttu-id="84c9c-251">Тип ключа содержимого, который в данном случае выражается целым числом.</span><span class="sxs-lookup"><span data-stu-id="84c9c-251">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="84c9c-252">Для шифрования хранилища передается значение 1.</span><span class="sxs-lookup"><span data-stu-id="84c9c-252">We pass the value 1 for storage encryption.</span></span> |
| <span data-ttu-id="84c9c-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="84c9c-253">EncryptedContentKey</span></span> |<span data-ttu-id="84c9c-254">Мы создаем новое значение ключа содержимого, которое представляет собой 256-битное (32-байтное) значение.</span><span class="sxs-lookup"><span data-stu-id="84c9c-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="84c9c-255">Ключ шифруется с помощью сертификата шифрования хранилища X.509, полученного из служб мультимедиа Microsoft Azure с помощью HTTP- запроса GET для методов GetProtectionKeyId и GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="84c9c-255">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="84c9c-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="84c9c-256">ProtectionKeyId</span></span> |<span data-ttu-id="84c9c-257">Идентификатор ключа защиты для сертификата шифрования хранилища X.509, который использовался для шифрования ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="84c9c-257">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span> |
| <span data-ttu-id="84c9c-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="84c9c-258">ProtectionKeyType</span></span> |<span data-ttu-id="84c9c-259">Тип шифрования для защиты ключа, который использовался для шифрования ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="84c9c-259">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="84c9c-260">В нашем примере этим значением является StorageEncryption(1).</span><span class="sxs-lookup"><span data-stu-id="84c9c-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="84c9c-261">Checksum</span><span class="sxs-lookup"><span data-stu-id="84c9c-261">Checksum</span></span> |<span data-ttu-id="84c9c-262">Контрольная сумма, рассчитанная для ключа содержимого с помощью MD5.</span><span class="sxs-lookup"><span data-stu-id="84c9c-262">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="84c9c-263">Она вычисляется путем шифрования идентификатора содержимого с использованием ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="84c9c-263">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="84c9c-264">В примере кода показано, как вычислить контрольную сумму.</span><span class="sxs-lookup"><span data-stu-id="84c9c-264">The example code demonstrates how to calculate the checksum.</span></span> |

<span data-ttu-id="84c9c-265">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-265">**HTTP Response**</span></span>

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

### <a name="link-the-contentkey-to-the-asset"></a><span data-ttu-id="84c9c-266">Привязка ключа содержимого к ресурсу</span><span class="sxs-lookup"><span data-stu-id="84c9c-266">Link the ContentKey to the Asset</span></span>
<span data-ttu-id="84c9c-267">Ключ содержимого привязывается к одному или нескольким ресурсам с помощью HTTP-запроса POST.</span><span class="sxs-lookup"><span data-stu-id="84c9c-267">The ContentKey is associated to one or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="84c9c-268">Приведенный ниже запрос представляет собой пример привязки ключа содержимого к ресурсу по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="84c9c-268">The following request is an example to link the example ContentKey to the example asset by Id.</span></span>

<span data-ttu-id="84c9c-269">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-269">**HTTP Response**</span></span>

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

<span data-ttu-id="84c9c-270">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="84c9c-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="84c9c-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84c9c-271">Next steps</span></span>

<span data-ttu-id="84c9c-272">Теперь можно закодировать отправленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="84c9c-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="84c9c-273">Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="84c9c-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="84c9c-274">Можно также использовать функции Azure для запуска задания кодирования на основе файла, поступающего в настроенный контейнер.</span><span class="sxs-lookup"><span data-stu-id="84c9c-274">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="84c9c-275">Дополнительные сведения см. в [этом примере](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="84c9c-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="84c9c-276">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="84c9c-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="84c9c-277">Отзывы</span><span class="sxs-lookup"><span data-stu-id="84c9c-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How to Get a Media Processor]: media-services-get-media-processor.md

