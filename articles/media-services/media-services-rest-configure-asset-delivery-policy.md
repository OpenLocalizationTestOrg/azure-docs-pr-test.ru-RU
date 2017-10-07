---
title: "с помощью API REST служб мультимедиа политики доставки активов aaaConfiguring | Документы Microsoft"
description: "В этом разделе показано, как политики доставки активов tooconfigure, с помощью API REST служб мультимедиа."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="57191-103">Настройка политик доставки ресурсов-контейнеров</span><span class="sxs-lookup"><span data-stu-id="57191-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="57191-104">Если планируется toodeliver динамически зашифрованные активы, один из hello шагов в hello Media Services содержимого, что рабочий процесс доставки является настройка политики доставки активов.</span><span class="sxs-lookup"><span data-stu-id="57191-104">If you plan toodeliver dynamically encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="57191-105">политики доставки активов Hello сообщает служб мультимедиа, порядок отображения для вашего toobe активов доставить: в какой протокол потоковой передачи следует актива динамического упаковать (для примера, MPEG DASH, HLS, Smooth Streaming или все), ли требуется toodynamically шифрование актива и способ (конверта или общее шифрование).</span><span class="sxs-lookup"><span data-stu-id="57191-105">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="57191-106">В этом разделе обсуждаются почему и как toocreate и настроить политики доставки активов.</span><span class="sxs-lookup"><span data-stu-id="57191-106">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="57191-107">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="57191-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="57191-108">Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="57191-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="57191-109">Кроме того, toobe может toouse динамической упаковки и динамического шифрования ваш ресурс должен содержать набор MP4 с адаптивным битрейтом или файлов Smooth Streaming с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="57191-109">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="57191-110">Можно применить различные политики toohello одного средства.</span><span class="sxs-lookup"><span data-stu-id="57191-110">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="57191-111">Например, можно применить PlayReady шифрования tooSmooth потоковой передачи и AES Envelope шифрования tooMPEG DASH и HLS.</span><span class="sxs-lookup"><span data-stu-id="57191-111">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="57191-112">Все протоколы, которые не определены в политике доставки (например, добавить отдельную политику, которая указывает в качестве протокола hello только HLS) будут заблокированы для потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="57191-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="57191-113">Hello toothis исключение — когда нет определенных политик доставки активов.</span><span class="sxs-lookup"><span data-stu-id="57191-113">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="57191-114">Затем все протоколы будут разрешены в hello снимите флажок.</span><span class="sxs-lookup"><span data-stu-id="57191-114">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="57191-115">Если вы хотите toodeliver зашифрованного актива хранилища, необходимо настроить политику доставки актива hello.</span><span class="sxs-lookup"><span data-stu-id="57191-115">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="57191-116">Перед потоковой актива hello, потоковая передача контента с помощью hello шифрование хранилища сервера удаляет hello и потоки указан политики доставки.</span><span class="sxs-lookup"><span data-stu-id="57191-116">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="57191-117">Например, toodeliver актива зашифрован ключ шифрования конвертов Advanced Encryption Standard (AES), установите тип политики hello слишком**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="57191-117">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="57191-118">шифрование хранилища tooremove и средства hello потока в hello очевидна, установите тип политики hello слишком**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="57191-118">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="57191-119">Примеры, которые показывают, как tooconfigure этими типами политики выполните.</span><span class="sxs-lookup"><span data-stu-id="57191-119">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="57191-120">В зависимости от способа настройки политики доставки активов hello вы бы быть пакета может toodynamically, динамически зашифровать и поток hello следующие протоколы потоковых: Smooth Streaming, HLS, потоки MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="57191-120">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="57191-121">Следующий список показывает hello Hello форматирует используется toostream Smooth, HLS, ТИРЕ.</span><span class="sxs-lookup"><span data-stu-id="57191-121">hello following list shows hello formats that you use toostream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="57191-122">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="57191-122">Smooth Streaming:</span></span>

<span data-ttu-id="57191-123">{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="57191-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="57191-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="57191-124">HLS:</span></span>

<span data-ttu-id="57191-125">{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="57191-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="57191-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="57191-126">MPEG DASH</span></span>

<span data-ttu-id="57191-127">{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="57191-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="57191-128">Инструкции по статье toopublish актива и построения URL-АДРЕСЕ потоковой передачи, [построения URL-адрес потоковой передачи](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="57191-128">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="57191-129">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="57191-129">Considerations</span></span>
* <span data-ttu-id="57191-130">Невозможно удалить политику доставки ресурсов-контейнеров (AssetDeliveryPolicy), связанную с ресурсом-контейнером, пока существует указатель OnDemand (потоковой передачи) для этого ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="57191-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="57191-131">Hello рекомендуется tooremove hello политику из ресурса hello перед удалением политики hello.</span><span class="sxs-lookup"><span data-stu-id="57191-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="57191-132">Если политика доставки ресурсов-контейнеров не задана, создать указатель потоковой передачи в зашифрованном ресурсе-контейнере хранилища.</span><span class="sxs-lookup"><span data-stu-id="57191-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="57191-133">При hello активов не зашифрованного в хранилище, система hello позволит создать hello средства обнаружения и потоком в hello снимите без политики доставки активов.</span><span class="sxs-lookup"><span data-stu-id="57191-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="57191-134">Может существовать несколько политик доставки активов, связанные с одного актива, но можно указать только один из способов toohandle данного AssetDeliveryProtocol.</span><span class="sxs-lookup"><span data-stu-id="57191-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="57191-135">То есть при попытке toolink две доставки политики, которые необходимо указать протокол AssetDeliveryProtocol.SmoothStreaming hello, вызовет ошибку поскольку hello системы неизвестно, какой из них необходимо tooapply когда клиент делает запрос Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="57191-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="57191-136">При наличии актива с существующий указатель потоковой передачи нельзя связать новый актив toohello политики, отменить привязку существующую политику из ресурса hello или обновлении политики доставки, связанный с активом hello.</span><span class="sxs-lookup"><span data-stu-id="57191-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset, unlink an existing policy from hello asset, or update a delivery policy associated with hello asset.</span></span>  <span data-ttu-id="57191-137">Сначала имеют указатель потоковой передачи tooremove hello, настройте политики hello и повторного создания hello потоковой передачи указателя.</span><span class="sxs-lookup"><span data-stu-id="57191-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="57191-138">Можно использовать приветствия же locatorId при повторном создании hello потоковой передачи указателя, но следует убедиться, не будут вызывать проблемы для клиентов, так как содержимое, кэшируемых средой hello происхождения или подчиненным CDN.</span><span class="sxs-lookup"><span data-stu-id="57191-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="57191-139">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="57191-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="57191-140">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="57191-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="57191-141">Подключение служб tooMedia</span><span class="sxs-lookup"><span data-stu-id="57191-141">Connect tooMedia Services</span></span>

<span data-ttu-id="57191-142">Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="57191-142">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="57191-143">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="57191-143">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="57191-144">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="57191-144">You must make subsequent calls toohello new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="57191-145">Политики доставки незашифрованных ресурсов</span><span class="sxs-lookup"><span data-stu-id="57191-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="57191-146"><a id="create_asset_delivery_policy"></a>Создание политики доставки активов</span><span class="sxs-lookup"><span data-stu-id="57191-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="57191-147">Hello следующий запрос HTTP создает политики доставки активов, указывающее toonot применения динамического шифрования и протоколов toodeliver поток hello в любом из следующих hello: протоколы MPEG DASH, HLS и Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="57191-147">hello following HTTP request creates an asset delivery policy that specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="57191-148">Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.</span><span class="sxs-lookup"><span data-stu-id="57191-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="57191-149">Запрос:</span><span class="sxs-lookup"><span data-stu-id="57191-149">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

<span data-ttu-id="57191-150">Ответ:</span><span class="sxs-lookup"><span data-stu-id="57191-150">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <span data-ttu-id="57191-151"><a id="link_asset_with_asset_delivery_policy"></a>Привязка ресурса к политике доставки ресурсов</span><span class="sxs-lookup"><span data-stu-id="57191-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="57191-152">Привет, следуя hello ссылки запроса HTTP указан политики доставки активов toohello активов для.</span><span class="sxs-lookup"><span data-stu-id="57191-152">hello following HTTP request links hello specified asset toohello asset delivery policy to.</span></span>

<span data-ttu-id="57191-153">Запрос:</span><span class="sxs-lookup"><span data-stu-id="57191-153">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

<span data-ttu-id="57191-154">Ответ:</span><span class="sxs-lookup"><span data-stu-id="57191-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="57191-155">Политика доставки ресурсов DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="57191-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="57191-156">Создать ключ контента для типа EnvelopeEncryption hello и связать его toohello активов</span><span class="sxs-lookup"><span data-stu-id="57191-156">Create content key of hello EnvelopeEncryption type and link it toohello asset</span></span>
<span data-ttu-id="57191-157">При определении политики доставки DynamicEnvelopeEncryption, что toolink toomake необходимо активов tooa ключа содержимого из hello EnvelopeEncryption типа.</span><span class="sxs-lookup"><span data-stu-id="57191-157">When specifying DynamicEnvelopeEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello EnvelopeEncryption type.</span></span> <span data-ttu-id="57191-158">Дополнительные сведения см. в статье, посвященной [созданию ключей содержимого](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="57191-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="57191-159"><a id="get_delivery_url"></a>Получение URL-адреса доставки</span><span class="sxs-lookup"><span data-stu-id="57191-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="57191-160">URL-адрес доставки hello Get для hello указанного метода доставки ключа контента hello на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="57191-160">Get hello delivery URL for hello specified delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="57191-161">Клиент использует hello, возвращаемый URL-адрес toorequest ключ AES или лицензию PlayReady в порядке tooplayback hello защищенного содержимого.</span><span class="sxs-lookup"><span data-stu-id="57191-161">A client uses hello returned URL toorequest an AES key or a PlayReady license in order tooplayback hello protected content.</span></span>

<span data-ttu-id="57191-162">Укажите тип hello hello tooget URL-адрес в тексте hello hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="57191-162">Specify hello type of hello URL tooget in hello body of hello HTTP request.</span></span> <span data-ttu-id="57191-163">Если необходимо обеспечить защиту содержимого с помощью PlayReady, запрошенный URL приобретения лицензий PlayReady служб мультимедиа, используя 1 для hello keyDeliveryType: {«keyDeliveryType»: 1}.</span><span class="sxs-lookup"><span data-stu-id="57191-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for hello keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="57191-164">При защите контента с шифрование конвертов hello запроса URL-адрес получения ключа путем указания 2 для keyDeliveryType: {«keyDeliveryType»: 2}.</span><span class="sxs-lookup"><span data-stu-id="57191-164">If you are protecting your content with hello envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="57191-165">Запрос:</span><span class="sxs-lookup"><span data-stu-id="57191-165">Request:</span></span>

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

<span data-ttu-id="57191-166">Ответ:</span><span class="sxs-lookup"><span data-stu-id="57191-166">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="57191-167">Создание политики доставки активов</span><span class="sxs-lookup"><span data-stu-id="57191-167">Create asset delivery policy</span></span>
<span data-ttu-id="57191-168">Hello следующий запрос HTTP создает hello **AssetDeliveryPolicy** , настроенных tooapply динамического конверта шифрования (**DynamicEnvelopeEncryption**) toohello **HLS**протокола (в этом примере другие протоколы, будет заблокирован потоковой передачи).</span><span class="sxs-lookup"><span data-stu-id="57191-168">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) toohello **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="57191-169">Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.</span><span class="sxs-lookup"><span data-stu-id="57191-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="57191-170">Запрос:</span><span class="sxs-lookup"><span data-stu-id="57191-170">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


<span data-ttu-id="57191-171">Ответ:</span><span class="sxs-lookup"><span data-stu-id="57191-171">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="57191-172">Привязка ресурса к политике доставки ресурсов</span><span class="sxs-lookup"><span data-stu-id="57191-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="57191-173">См. раздел [Привязка ресурса к политике доставки ресурсов](#link_asset_with_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="57191-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="57191-174">Политика доставки ресурсов DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="57191-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="57191-175">Создать ключ контента для типа CommonEncryption hello и связать его toohello активов</span><span class="sxs-lookup"><span data-stu-id="57191-175">Create content key of hello CommonEncryption type and link it toohello asset</span></span>
<span data-ttu-id="57191-176">При определении политики доставки DynamicCommonEncryption, что toolink toomake необходимо активов tooa ключа содержимого из hello CommonEncryption типа.</span><span class="sxs-lookup"><span data-stu-id="57191-176">When specifying DynamicCommonEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello CommonEncryption type.</span></span> <span data-ttu-id="57191-177">Дополнительные сведения см. в статье, посвященной [созданию ключей содержимого](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="57191-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="57191-178">Получение URL-адреса доставки</span><span class="sxs-lookup"><span data-stu-id="57191-178">Get Delivery URL</span></span>
<span data-ttu-id="57191-179">Получите URL-адрес доставки hello для метода доставки PlayReady hello hello ключа контента на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="57191-179">Get hello delivery URL for hello PlayReady delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="57191-180">Клиент использует hello вернул toorequest URL-адрес лицензии PlayReady в порядке tooplayback hello защищенного содержимого.</span><span class="sxs-lookup"><span data-stu-id="57191-180">A client uses hello returned URL toorequest a PlayReady license in order tooplayback hello protected content.</span></span> <span data-ttu-id="57191-181">Дополнительные сведения см. в разделе [Получение URL-адреса доставки](#get_delivery_url).</span><span class="sxs-lookup"><span data-stu-id="57191-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="57191-182">Создание политики доставки активов</span><span class="sxs-lookup"><span data-stu-id="57191-182">Create asset delivery policy</span></span>
<span data-ttu-id="57191-183">Hello следующий запрос HTTP создает hello **AssetDeliveryPolicy** , настроенных tooapply динамического общее шифрование (**DynamicCommonEncryption**) toohello **Smooth Streaming**  протокола (в этом примере другие протоколы, будет заблокирован потоковой передачи).</span><span class="sxs-lookup"><span data-stu-id="57191-183">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="57191-184">Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.</span><span class="sxs-lookup"><span data-stu-id="57191-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="57191-185">Запрос:</span><span class="sxs-lookup"><span data-stu-id="57191-185">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


<span data-ttu-id="57191-186">Если требуется tooprotect контент с помощью Widevine DRM обновления hello AssetDeliveryConfiguration значения toouse WidevineLicenseAcquisitionUrl (которая имеет значение hello 7) и укажите hello URL-адрес службы доставки лицензий.</span><span class="sxs-lookup"><span data-stu-id="57191-186">If you want tooprotect your content using Widevine DRM, update hello AssetDeliveryConfiguration values toouse WidevineLicenseAcquisitionUrl (which has hello value of 7) and specify hello URL of a license delivery service.</span></span> <span data-ttu-id="57191-187">Можно использовать следующие toohelp партнеров AMS доставки лицензии Widevine hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="57191-187">You can use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="57191-188">Например:</span><span class="sxs-lookup"><span data-stu-id="57191-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="57191-189">При шифровании с Widevine будет только может toodeliver, с помощью ТИРЕ.</span><span class="sxs-lookup"><span data-stu-id="57191-189">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="57191-190">Убедитесь, что toospecify протокол доставки актива ТИРЕ (2) в hello.</span><span class="sxs-lookup"><span data-stu-id="57191-190">Make sure toospecify DASH (2) in hello asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="57191-191">Привязка ресурса к политике доставки ресурсов</span><span class="sxs-lookup"><span data-stu-id="57191-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="57191-192">См. раздел [Привязка ресурса к политике доставки ресурсов](#link_asset_with_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="57191-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="57191-193"><a id="types"></a>Типы, используемые при определении AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="57191-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="57191-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="57191-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="57191-195">Hello следующие перечисления описаны значения, которые можно задать для hello протокол доставки актива.</span><span class="sxs-lookup"><span data-stu-id="57191-195">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="57191-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="57191-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="57191-197">Hello следующие перечисления описаны значения, которые можно задать для типа политики доставки активов hello.</span><span class="sxs-lookup"><span data-stu-id="57191-197">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a><span data-ttu-id="57191-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="57191-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="57191-199">Hello следующие перечисления описаны значения, можно использовать метод доставки hello tooconfigure hello содержимого toohello ключа клиента.</span><span class="sxs-lookup"><span data-stu-id="57191-199">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="57191-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="57191-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="57191-201">следующие перечисления Hello описаны значения, можно задать tooconfigure ключи, используемые tooget конфигурация политики доставки активов.</span><span class="sxs-lookup"><span data-stu-id="57191-201">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="57191-202">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="57191-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="57191-203">Отзывы</span><span class="sxs-lookup"><span data-stu-id="57191-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

