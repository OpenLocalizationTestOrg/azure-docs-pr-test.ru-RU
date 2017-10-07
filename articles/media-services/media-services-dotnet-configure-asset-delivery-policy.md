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
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>Настройка политик доставки ресурсов-контейнеров с помощью пакета SDK для .NET
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>Обзор
Если планируется toodelivery зашифрованные активы, один из hello шагов в hello Media Services содержимого, что рабочий процесс доставки является настройка политики доставки активов. политики доставки активов Hello сообщает служб мультимедиа, порядок отображения для вашего toobe активов доставить: в какой протокол потоковой передачи следует актива динамического упаковать (для примера, MPEG DASH, HLS, Smooth Streaming или все), ли требуется toodynamically шифрование актива и способ (конверта или общее шифрование).

В этом разделе обсуждаются почему и как toocreate и настроить политики доставки активов.

>[!NOTE]
>При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния. 
>
>Кроме того, toobe может toouse динамической упаковки и динамического шифрования ваш ресурс должен содержать набор MP4 с адаптивным битрейтом или файлов Smooth Streaming с адаптивной скоростью.


Можно применить различные политики toohello одного средства. Например, можно применить PlayReady шифрования tooSmooth потоковой передачи и AES Envelope шифрования tooMPEG DASH и HLS. Все протоколы, которые не определены в политике доставки (например, добавить отдельную политику, которая указывает в качестве протокола hello только HLS) будут заблокированы для потоковой передачи. Hello toothis исключение — когда нет определенных политик доставки активов. Затем все протоколы будут разрешены в hello снимите флажок.

Если вы хотите toodeliver зашифрованного актива хранилища, необходимо настроить политику доставки актива hello. Перед потоковой актива hello, потоковая передача контента с помощью hello шифрование хранилища сервера удаляет hello и потоки указан политики доставки. Например, toodeliver актива зашифрован ключ шифрования конвертов Advanced Encryption Standard (AES), установите тип политики hello слишком**DynamicEnvelopeEncryption**. шифрование хранилища tooremove и средства hello потока в hello очевидна, установите тип политики hello слишком**NoDynamicEncryption**. Примеры, которые показывают, как tooconfigure этими типами политики выполните.

В зависимости от способа настройки политики доставки активов hello вы бы быть пакета может toodynamically, динамически зашифровать и поток hello следующие протоколы потоковых: потоки Smooth Streaming, HLS и MPEG DASH.

Hello ниже перечислены форматы hello использовать toostream Smooth, HLS и ТИРЕ.

Smooth Streaming:

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest

HLS:

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=mpd-time-csf)


## <a name="considerations"></a>Рекомендации
* Невозможно удалить политику доставки ресурсов-контейнеров (AssetDeliveryPolicy), связанную с ресурсом-контейнером, пока существует указатель OnDemand (потоковой передачи) для этого ресурса-контейнера. Hello рекомендуется tooremove hello политику из ресурса hello перед удалением политики hello.
* Если политика доставки ресурсов-контейнеров не задана, создать указатель потоковой передачи в зашифрованном ресурсе-контейнере хранилища.  При hello активов не зашифрованного в хранилище, система hello позволит создать hello средства обнаружения и потоком в hello снимите без политики доставки активов.
* Может существовать несколько политик доставки активов, связанные с одного актива, но можно указать только один из способов toohandle данного AssetDeliveryProtocol.  То есть при попытке toolink две доставки политики, которые необходимо указать протокол AssetDeliveryProtocol.SmoothStreaming hello, вызовет ошибку поскольку hello системы неизвестно, какой из них необходимо tooapply когда клиент делает запрос Smooth Streaming.
* При наличии актива с существующий указатель потоковой передачи нельзя связать новое средство toohello политики (можно разорвать связь существующую политику из ресурса hello, или обновлении политики доставки, связанный с активом hello).  Сначала имеют указатель потоковой передачи tooremove hello, настройте политики hello и повторного создания hello потоковой передачи указателя.  Можно использовать приветствия же locatorId при повторном создании hello потоковой передачи указателя, но следует убедиться, не будут вызывать проблемы для клиентов, так как содержимое, кэшируемых средой hello происхождения или подчиненным CDN.

## <a name="clear-asset-delivery-policy"></a>Политики доставки незашифрованных ресурсов

следующие Hello **ConfigureClearAssetDeliveryPolicy** метод задает toonot применения динамического шифрования и протоколов toodeliver поток hello в любом из следующих hello: протоколы MPEG DASH, HLS и Smooth Streaming. Может потребоваться tooapply этой политики tooyour зашифрованные активы хранилища.

Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Политика доставки ресурсов DynamicCommonEncryption

следующие Hello **CreateAssetDeliveryPolicy** метод создает hello **AssetDeliveryPolicy** , настроенных tooapply динамического общее шифрование (**DynamicCommonEncryption**) tooa smooth streaming протокола (другие протоколы будут заблокированы для потоковой передачи). метод Hello принимает два параметра: **активов** (hello toowhich активов, требуется политики доставки hello tooapply) и **IContentKey** (hello ключ контента для hello **CommonEncryption**типов, Дополнительные сведения см. в разделе: [Создание ключа контента](media-services-dotnet-create-contentkey.md#common_contentkey)).

Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.

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

Службы мультимедиа Azure также позволяет tooadd Widevine шифрования. Hello ниже приведен пример PlayReady и Widevine добавляемый toohello политики доставки активов.

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
> При шифровании с Widevine будет только может toodeliver, с помощью ТИРЕ. Протокол доставки актива hello сделать убедиться, что toospecify ТИРЕ.
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Политика доставки ресурсов DynamicEnvelopeEncryption
следующие Hello **CreateAssetDeliveryPolicy** метод создает hello **AssetDeliveryPolicy** , настроенных tooapply динамического конверта шифрования (**DynamicEnvelopeEncryption** ) tooSmooth Streaming, HLS и DASH протоколы (если было принято решение toonot указать некоторые протоколы, они будут заблокированы для потоковой передачи). метод Hello принимает два параметра: **активов** (hello toowhich активов, требуется политики доставки hello tooapply) и **IContentKey** (hello ключ контента для hello **EnvelopeEncryption**типов, Дополнительные сведения см. в разделе: [Создание ключа контента](media-services-dotnet-create-contentkey.md#envelope_contentkey)).

Сведения по вы значений можно указать при создании AssetDeliveryPolicy, см. в разделе hello [типы, используемые при определении AssetDeliveryPolicy](#types) раздела.   

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


## <a id="types"></a>Типы, используемые при определении AssetDeliveryPolicy

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

Hello следующие перечисления описаны значения, которые можно задать для hello протокол доставки актива.

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

### <a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType

Hello следующие перечисления описаны значения, которые можно задать для типа политики доставки активов hello.  

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

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType

Hello следующие перечисления описаны значения, можно использовать метод доставки hello tooconfigure hello содержимого toohello ключа клиента.
    
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

### <a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey

следующие перечисления Hello описаны значения, можно задать tooconfigure ключи, используемые tooget конфигурация политики доставки активов.

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

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

