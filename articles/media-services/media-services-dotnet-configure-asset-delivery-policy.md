---
title: "Настройка политик доставки ресурсов-контейнеров с помощью пакета SDK для .NET | Документация Майкрософт"
description: "В этом разделе демонстрируется настройка различных политик доставки ресурсов-контейнеров с помощью пакета SDK служб мультимедиа для .NET."
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
ms.openlocfilehash: 282fd9e24dc147e31613469926128894d48366f4
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>Настройка политик доставки ресурсов-контейнеров с помощью пакета SDK для .NET
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>Обзор
Если вы планируете доставлять зашифрованные ресурсы-контейнеры, вам следует настроить политику доставки таких ресурсов (один из этапов рабочего процесса доставки содержимого в службах мультимедиа). Политика доставки ресурсов сообщает службам мультимедиа способ доставки ресурса: какие протоколы передачи следует использовать для динамической упаковки ресурса (например, MPEG DASH, HLS, Smooth Streaming или все), следует ли использовать динамическое шифрование и как (конвертное или общее шифрование).

В этом разделе рассматриваются причины и способы создания и настройки политик доставки ресурсов-контейнеров.

>[!NOTE]
>При создании учетной записи AMS в нее добавляется конечная точка потоковой передачи **по умолчанию** в состоянии **Остановлена**. Чтобы начать потоковую передачу содержимого и воспользоваться динамической упаковкой и динамическим шифрованием, конечная точка потоковой передачи, из которой необходимо выполнять потоковую передачу содержимого, должна находиться в состоянии **Выполняется**. 
>
>Кроме того, чтобы использовать динамическую упаковку и динамическое шифрование, ресурс должен содержать набор файлов формата MP4 или потоковой передачи Smooth Streaming с переменной скоростью.


К одному ресурсу можно применить различные политики. Например, можно применить шифрование PlayReady при использовании Smooth Streaming и конвертное шифрование AES при использовании MPEG DASH и HLS. Потоковая передача по тем протоколам, которые не определены в политике доставки (например, если вы добавили одну политику, которая предусматривает использование только протокола HLS), будет блокироваться. Исключением являются те случаи, когда политика доставки ресурсов совсем не определена. Тогда все протоколы могут использоваться в незашифрованном виде.

Если необходимо доставить зашифрованный в хранилище ресурс-контейнер, необходимо настроить его политику доставки. Перед выполнением потоковой передачи ресурса сервер потоковой передачи удаляет шифрование хранилища и осуществляет потоковую передачу содержимого с помощью указанной политики доставки. Например, для доставки ресурса, зашифрованного с помощью ключа шифрования конвертного типа для AES, задайте для типа политики значение **DynamicEnvelopeEncryption**. Чтобы удалить шифрование хранилища и выполнить потоковую передачу ресурса в незашифрованном виде, задайте для типа политики значение **NoDynamicEncryption**. Далее приведены примеры, показывающие, как настроить эти типы политики.

В зависимости от способа настройки политики доставки ресурсов вы можете выполнить динамическую упаковку, динамическое шифрование и потоковую передачу с помощью следующих протоколов потоковой передачи: Smooth Streaming, HLS и MPEG-DASH.

В следующем списке приведены форматы, которые используются для потоковой передачи данных в формате Smooth, HLS и DASH.

Smooth Streaming:

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest

HLS:

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=mpd-time-csf)


## <a name="considerations"></a>Рекомендации
* Невозможно удалить политику доставки ресурсов-контейнеров (AssetDeliveryPolicy), связанную с ресурсом-контейнером, пока существует указатель OnDemand (потоковой передачи) для этого ресурса-контейнера. Рекомендуется удалить политику из ресурса-контейнера перед удалением политики.
* Если политика доставки ресурсов-контейнеров не задана, создать указатель потоковой передачи в зашифрованном ресурсе-контейнере хранилища.  Если ресурс-контейнер хранилища не зашифрован, система позволит создать указатель и выполнить потоковую передачу ресурса-контейнера в незашифрованном виде без политики доставки ресурса-контейнера.
* С одним ресурсом-контейнером можно связать несколько политик доставки ресурсов-контейнеров, но можно указать только один способ обработки заданного протокола доставки ресурса-контейнера (AssetDeliveryProtocol).  То есть при попытке связать две политики доставки, определяющие протокол AssetDeliveryProtocol.SmoothStreaming, появится ошибка, поскольку система не знает, какую из них необходимо применить, когда клиент выполняет запрос Smooth Streaming.
* При наличии ресурса-контейнера с существующим указателем потоковой передачи новую политику привязать к ресурсу-контейнеру нельзя (можно либо разорвать связь ресурса-контенера с существующей политикой, либо обновить политику доставки, связанную с ресурсом-контейнером).  Необходимо сначала удалить указатель потоковой передачи, затем настроить политики и повторно создать указатель потоковой передачи.  При повторном создании указателя потоковой передачи вы можете использовать тот же идентификатор указателя (locatorId), но необходимо убедиться, что это не приведет к проблемам для клиентов, так как кэширование содержимого с помощью исходного или нисходящего CDN выполнить нельзя.

## <a name="clear-asset-delivery-policy"></a>Политики доставки незашифрованных ресурсов

Следующий метод **ConfigureClearAssetDeliveryPolicy** указывает, что не следует применять динамическое шифрование и осуществлять доставку с помощью потоковой передачи по любому из следующих протоколов: MPEG DASH, HLS и Smooth Streaming. Эту политику можно применить к зашифрованным в хранилище ресурсам-контейнерам.

Сведения о том, какие значения можно задать при создании политики доставки ресурсов-контейнеров, см. в разделе [Типы, используемые при определении AssetDeliveryPolicy](#types).

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Политика доставки ресурсов DynamicCommonEncryption

Следующий метод **CreateAssetDeliveryPolicy** создает сущность **AssetDeliveryPolicy**, для которой настроено динамическое общее шифрование содержимого (**DynamicCommonEncryption**), передаваемого по протоколу Smooth Streaming (потоковая передача по другим протоколам будет блокироваться). Этот метод принимает два параметра: **Asset** (ресурс, к которому нужно применить политики доставки) и **IContentKey** (ключ содержимого типа **CommonEncryption**). Дополнительные сведения см. в статье [Создание ContentKey с использованием .NET](media-services-dotnet-create-contentkey.md#common_contentkey).

Сведения о том, какие значения можно задать при создании политики доставки ресурсов-контейнеров, см. в разделе [Типы, используемые при определении AssetDeliveryPolicy](#types).

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
    
            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

Службы мультимедиа Azure также позволяют добавить шифрование Widevine. В следующем примере показано добавление PlayReady и Widevine в политику доставки ресурсов-контейнеров.

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get the PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // to append /? KID =< keyId > to the end of the url when creating the manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

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


        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> При шифровании с помощью Widevine будет возможна только доставка посредством DASH. Обязательно укажите DASH в протоколе доставки ресурсов-контейнеров.
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Политика доставки ресурсов DynamicEnvelopeEncryption
Следующий метод **CreateAssetDeliveryPolicy** создает сущность **AssetDeliveryPolicy**, для которой настроено применение динамического конвертного шифрования (**DynamicEnvelopeEncryption**) для протоколов Smooth Streaming, HLS и DASH (если вы не укажете какие-либо протоколы, то потоковая передача по ним будет блокироваться). Этот метод принимает два параметра: **Asset** (ресурс, к которому нужно применить политики доставки) и **IContentKey** (ключ содержимого типа **EnvelopeEncryption**). Дополнительные сведения см. в статье [Создание ContentKey с использованием .NET](media-services-dotnet-create-contentkey.md#envelope_contentkey).

Сведения о том, какие значения можно задать при создании политики доставки ресурсов-контейнеров, см. в разделе [Типы, используемые при определении AssetDeliveryPolicy](#types).   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get the Key Delivery Base Url by removing the Query parameter.  The Dynamic Encryption service will
        //  automatically add the correct key identifier to the url when it generates the Envelope encrypted content
        //  manifest.  Omitting the IV will also cause the Dynamice Encryption service to generate a deterministic
        //  IV for the content automatically.  By using the EnvelopeBaseKeyAcquisitionUrl and omitting the IV, this
        //  allows the AssetDelivery policy to be reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // The following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended to the envelope and
        //   the Initialization Vector (IV) to use for the envelope encryption.
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

        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <a id="types"></a>Типы, используемые при определении AssetDeliveryPolicy

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

Следующее перечисление описывает значения, которые можно указать для протокола доставки ресурсов.

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

Следующее перечисление описывает значения, которые можно указать для типа политики доставки ресурсов.  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// The Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption to the asset.
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

Следующее перечисление описывает значения, с помощью которых можно настроить способ доставки ключей содержимого на клиент.
    
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

Следующее перечисление описывает значения, с помощью которых можно настроить ключи, используемые для получения конкретной конфигурации для политики доставки ресурсов.

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
        /// The initialization vector to use for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// The PlayReady License Acquisition Url to use for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// The PlayReady Custom Attributes to add to the PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// The initialization vector to use for envelope encryption.
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

