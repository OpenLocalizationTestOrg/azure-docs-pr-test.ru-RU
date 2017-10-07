---
title: "aaaConfigure политик доставки активов с помощью пакета SDK для .NET | Документы Microsoft"
description: "В этом разделе показано, как tooconfigure политик доставки активов с помощью Azure Media Services .NET SDK."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="91471-103">Настройка политик доставки ресурсов-контейнеров с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="91471-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="91471-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="91471-104">Overview</span></span>
<span data-ttu-id="91471-105">Если планируется toodelivery зашифрованные активы, один из hello шагов в hello Media Services содержимого, что рабочий процесс доставки является настройка политики доставки активов.</span><span class="sxs-lookup"><span data-stu-id="91471-105">If you plan toodelivery encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="91471-106">политики доставки активов Hello сообщает служб мультимедиа, порядок отображения для вашего toobe активов доставить: в какой протокол потоковой передачи следует актива динамического упаковать (для примера, MPEG DASH, HLS, Smooth Streaming или все), ли требуется toodynamically шифрование актива и способ (конверта или общее шифрование).</span><span class="sxs-lookup"><span data-stu-id="91471-106">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="91471-107">В этом разделе обсуждаются почему и как toocreate и настроить политики доставки активов.</span><span class="sxs-lookup"><span data-stu-id="91471-107">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="91471-108">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="91471-108">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="91471-109">Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="91471-109">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="91471-110">Кроме того, toobe может toouse динамической упаковки и динамического шифрования ваш ресурс должен содержать набор MP4 с адаптивным битрейтом или файлов Smooth Streaming с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="91471-110">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="91471-111">Можно применить различные политики toohello одного средства.</span><span class="sxs-lookup"><span data-stu-id="91471-111">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="91471-112">Например, можно применить PlayReady шифрования tooSmooth потоковой передачи и AES Envelope шифрования tooMPEG DASH и HLS.</span><span class="sxs-lookup"><span data-stu-id="91471-112">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="91471-113">Все протоколы, которые не определены в политике доставки (например, добавить отдельную политику, которая указывает в качестве протокола hello только HLS) будут заблокированы для потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="91471-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="91471-114">Hello toothis исключение — когда нет определенных политик доставки активов.</span><span class="sxs-lookup"><span data-stu-id="91471-114">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="91471-115">Затем все протоколы будут разрешены в hello снимите флажок.</span><span class="sxs-lookup"><span data-stu-id="91471-115">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="91471-116">Если вы хотите toodeliver зашифрованного актива хранилища, необходимо настроить политику доставки актива hello.</span><span class="sxs-lookup"><span data-stu-id="91471-116">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="91471-117">Перед потоковой актива hello, потоковая передача контента с помощью hello шифрование хранилища сервера удаляет hello и потоки указан политики доставки.</span><span class="sxs-lookup"><span data-stu-id="91471-117">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="91471-118">Например, toodeliver актива зашифрован ключ шифрования конвертов Advanced Encryption Standard (AES), установите тип политики hello слишком**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="91471-118">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="91471-119">шифрование хранилища tooremove и средства hello потока в hello очевидна, установите тип политики hello слишком**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="91471-119">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="91471-120">Примеры, которые показывают, как tooconfigure этими типами политики выполните.</span><span class="sxs-lookup"><span data-stu-id="91471-120">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="91471-121">В зависимости от способа настройки политики доставки активов hello вы бы быть пакета может toodynamically, динамически зашифровать и поток hello следующие протоколы потоковых: потоки Smooth Streaming, HLS и MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="91471-121">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="91471-122">Hello ниже перечислены форматы hello использовать toostream Smooth, HLS и ТИРЕ.</span><span class="sxs-lookup"><span data-stu-id="91471-122">hello following list shows hello formats that you use toostream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="91471-123">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="91471-123">Smooth Streaming:</span></span>

<span data-ttu-id="91471-124">{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="91471-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="91471-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="91471-125">HLS:</span></span>

<span data-ttu-id="91471-126">{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="91471-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="91471-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="91471-127">MPEG DASH</span></span>

<span data-ttu-id="91471-128">{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="91471-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="91471-129">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="91471-129">Considerations</span></span>
* <span data-ttu-id="91471-130">Невозможно удалить политику доставки ресурсов-контейнеров (AssetDeliveryPolicy), связанную с ресурсом-контейнером, пока существует указатель OnDemand (потоковой передачи) для этого ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="91471-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="91471-131">Hello рекомендуется tooremove hello политику из ресурса hello перед удалением политики hello.</span><span class="sxs-lookup"><span data-stu-id="91471-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="91471-132">Если политика доставки ресурсов-контейнеров не задана, создать указатель потоковой передачи в зашифрованном ресурсе-контейнере хранилища.</span><span class="sxs-lookup"><span data-stu-id="91471-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="91471-133">При hello активов не зашифрованного в хранилище, система hello позволит создать hello средства обнаружения и потоком в hello снимите без политики доставки активов.</span><span class="sxs-lookup"><span data-stu-id="91471-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="91471-134">Может существовать несколько политик доставки активов, связанные с одного актива, но можно указать только один из способов toohandle данного AssetDeliveryProtocol.</span><span class="sxs-lookup"><span data-stu-id="91471-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="91471-135">То есть при попытке toolink две доставки политики, которые необходимо указать протокол AssetDeliveryProtocol.SmoothStreaming hello, вызовет ошибку поскольку hello системы неизвестно, какой из них необходимо tooapply когда клиент делает запрос Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="91471-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="91471-136">При наличии актива с существующий указатель потоковой передачи нельзя связать новое средство toohello политики (можно разорвать связь существующую политику из ресурса hello, или обновлении политики доставки, связанный с активом hello).</span><span class="sxs-lookup"><span data-stu-id="91471-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset (you can either unlink an existing policy from hello asset, or update a delivery policy associated with hello asset).</span></span>  <span data-ttu-id="91471-137">Сначала имеют указатель потоковой передачи tooremove hello, настройте политики hello и повторного создания hello потоковой передачи указателя.</span><span class="sxs-lookup"><span data-stu-id="91471-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="91471-138">Можно использовать приветствия же locatorId при повторном создании hello потоковой передачи указателя, но следует убедиться, не будут вызывать проблемы для клиентов, так как содержимое, кэшируемых средой hello происхождения или подчиненным CDN.</span><span class="sxs-lookup"><span data-stu-id="91471-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="91471-139">Политики доставки незашифрованных ресурсов</span><span class="sxs-lookup"><span data-stu-id="91471-139">Clear asset delivery policy</span></span>

<span data-ttu-id="91471-140">следующие Hello **ConfigureClearAssetDeliveryPolicy** метод задает toonot применения динамического шифрования и протоколов toodeliver поток hello в любом из следующих hello: протоколы MPEG DASH, HLS и Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="91471-140">hello following **ConfigureClearAssetDeliveryPolicy** method specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="91471-141">Может потребоваться tooapply этой политики tooyour зашифрованные активы хранилища.</span><span class="sxs-lookup"><span data-stu-id="91471-141">You might want tooapply this policy tooyour storage encrypted assets.</span></span>

<span data-ttu-id="91471-142">Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.</span><span class="sxs-lookup"><span data-stu-id="91471-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="91471-143">Политика доставки ресурсов DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="91471-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="91471-144">следующие Hello **CreateAssetDeliveryPolicy** метод создает hello **AssetDeliveryPolicy** , настроенных tooapply динамического общее шифрование (**DynamicCommonEncryption**) tooa smooth streaming протокола (другие протоколы будут заблокированы для потоковой передачи).</span><span class="sxs-lookup"><span data-stu-id="91471-144">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="91471-145">метод Hello принимает два параметра: **активов** (hello toowhich активов, требуется политики доставки hello tooapply) и **IContentKey** (hello ключ контента для hello **CommonEncryption**типов, Дополнительные сведения см. в разделе: [Создание ключа контента](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="91471-145">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="91471-146">Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.</span><span class="sxs-lookup"><span data-stu-id="91471-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="91471-147">Службы мультимедиа Azure также позволяет tooadd Widevine шифрования.</span><span class="sxs-lookup"><span data-stu-id="91471-147">Azure Media Services also enables you tooadd Widevine encryption.</span></span> <span data-ttu-id="91471-148">Hello ниже приведен пример PlayReady и Widevine добавляемый toohello политики доставки активов.</span><span class="sxs-lookup"><span data-stu-id="91471-148">hello following example demonstrates both PlayReady and Widevine being added toohello asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get hello PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

        Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
        UriBuilder uriBuilder = new UriBuilder(widevineUrl);
        uriBuilder.Query = String.Empty;
        widevineUrl = uriBuilder.Uri;

        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
        {
            {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="91471-149">При шифровании с Widevine будет только может toodeliver, с помощью ТИРЕ.</span><span class="sxs-lookup"><span data-stu-id="91471-149">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="91471-150">Протокол доставки актива hello сделать убедиться, что toospecify ТИРЕ.</span><span class="sxs-lookup"><span data-stu-id="91471-150">Make sure toospecify DASH in hello asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="91471-151">Политика доставки ресурсов DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="91471-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="91471-152">следующие Hello **CreateAssetDeliveryPolicy** метод создает hello **AssetDeliveryPolicy** , настроенных tooapply динамического конверта шифрования (**DynamicEnvelopeEncryption** ) tooSmooth Streaming, HLS и DASH протоколы (если было принято решение toonot указать некоторые протоколы, они будут заблокированы для потоковой передачи).</span><span class="sxs-lookup"><span data-stu-id="91471-152">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) tooSmooth Streaming, HLS, and DASH protocols (if you decide toonot specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="91471-153">метод Hello принимает два параметра: **активов** (hello toowhich активов, требуется политики доставки hello tooapply) и **IContentKey** (hello ключ контента для hello **EnvelopeEncryption**типов, Дополнительные сведения см. в разделе: [Создание ключа контента](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="91471-153">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="91471-154">Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.</span><span class="sxs-lookup"><span data-stu-id="91471-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
        };

        IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                        "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                        AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);

        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="91471-155"><a id="types"></a>Типы, используемые при определении AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="91471-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="91471-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="91471-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="91471-157">Hello следующие перечисления описаны значения, которые можно задать для hello протокол доставки актива.</span><span class="sxs-lookup"><span data-stu-id="91471-157">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <span data-ttu-id="91471-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="91471-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="91471-159">Hello следующие перечисления описаны значения, которые можно задать для типа политики доставки активов hello.</span><span class="sxs-lookup"><span data-stu-id="91471-159">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <span data-ttu-id="91471-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="91471-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="91471-161">Hello следующие перечисления описаны значения, можно использовать метод доставки hello tooconfigure hello содержимого toohello ключа клиента.</span><span class="sxs-lookup"><span data-stu-id="91471-161">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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

### <span data-ttu-id="91471-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="91471-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="91471-163">следующие перечисления Hello описаны значения, можно задать tooconfigure ключи, используемые tooget конфигурация политики доставки активов.</span><span class="sxs-lookup"><span data-stu-id="91471-163">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="91471-164">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="91471-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="91471-165">Отзывы</span><span class="sxs-lookup"><span data-stu-id="91471-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

