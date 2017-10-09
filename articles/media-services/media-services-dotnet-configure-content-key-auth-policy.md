---
title: "с помощью Media Services .NET SDK политики авторизации ключа контента aaaConfigure | Документы Microsoft"
description: "Узнайте, как tooconfigure политику авторизации для ключа контента с помощью пакета SDK .NET служб мультимедиа."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: cfcbc5da9819bcec8b163fef183988a8beff9ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a>Динамическое шифрование: настройка политики авторизации ключа содержимого
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Обзор
Службы мультимедиа Microsoft Azure позволяет toodeliver MPEG-DASH, Smooth Streaming и HTTP-Live-Streaming (HLS) потоки, защищенных с помощью Advanced Encryption Standard (AES) (с помощью 128-битные ключи шифрования) или [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS также позволяет вам toodeliver ТИРЕ потоки зашифрован Widevine DRM. PlayReady и Widevine шифруются на hello спецификации общее шифрование (CENC ISO/IEC 23001-7).

Службы мультимедиа также предоставляют **служба доставки ключа/лицензий** из которых клиенты могут получить ключи AES или PlayReady или Widevine лицензий tooplay hello зашифрованное содержимое.

Если требуется для служб мультимедиа tooencrypt актива, необходимо tooassociate ключ шифрования (**CommonEncryption** или **EnvelopeEncryption**) с активом hello (как описано [здесь](media-services-dotnet-create-contentkey.md)) а также настроить политики авторизации для ключа hello (как описано в этой статье).

Когда проигрыватель запрашивает поток, службы мультимедиа используют указанный hello toodynamically ключа шифрования контента с помощью шифрования AES или DRM. поток toodecrypt hello, hello проигрыватель будет запрашивать ключ hello из службы доставки ключей hello. toodecide ли он hello авторизованных tooget hello ключ, hello служба оценивает политики авторизации hello, заданные для ключа hello.

Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи. Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: **откройте** или **маркера** ограниченного использования программ. политика с ограничением токенов Hello должны сопровождаться маркера, выданного по токенов безопасности службы (STS). Службы мультимедиа поддерживают только токены в hello **токенов SWT** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) формат и **веб-маркера JSON** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) формате.

Службы мультимедиа не предоставляют службы маркеров безопасности. Можно создать настраиваемую STS или использовать токены tooissue Microsoft Azure ACS. Hello STS должна быть настроенный toocreate токен, подписанным с указанным ключом hello и выдающими утверждения, указанные в конфигурации ограничения токенов hello (как описано в этой статье). Hello служба доставки ключей Media Services возвратит клиент toohello ключа шифрования hello Если hello маркер является допустимым и hello утверждения маркера hello соответствуют настроенным для ключа контента hello.

Дополнительную информацию см. в разделе

[JWT token Authentication in Azure Media Services and Dynamic Encryption](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/) (Аутентификация токена JWT в службах мультимедиа Azure и динамическое шифрование)

[Интегрируйте приложение на основе OWIN MVC служб мультимедиа Azure с Azure Active Directory и ограничьте доставку ключей содержимого на основе утверждений JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Использовать токены Azure ACS tooissue](http://mingfeiy.com/acs-with-key-services).

### <a name="some-considerations-apply"></a>Важные особенности
* При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. toostart вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования, потоковой передачи конечной точки потоковой передачи имеет toobe в hello **под управлением** состояния. 
* Ресурс должен содержать набор MP4-файлов или файлов Smooth Streaming с переменной скоростью. Дополнительные сведения см. в статье о [кодировании ресурсов](media-services-encode-asset.md).
* Отправляйте и кодируйте ресурсы с помощью параметра **AssetCreationOptions.StorageEncrypted** .
* Если планируется toohave нескольких ключей контента, требующих hello же конфигурации политики, это настоятельно рекомендуется toocreate одну политику авторизации и использовать ее с несколькими ключами контента.
* Hello служба доставки ключей кэширует ContentKeyAuthorizationPolicy и связанные объекты (параметры политики и ограничения) в течение 15 минут.  Если создать политику ContentKeyAuthorizationPolicy и укажите toouse ограничения «Token», а затем проверить его, а затем обновить политику hello слишком «открыть» ограниченного использования программ, займет примерно 15 минут, прежде чем hello политики коммутаторы toohello версию «Open» политики hello.
* При добавлении или обновлении политики доставки ресурсов необходимо удалить существующий указатель (если он есть) и создать новый.
* В настоящее время невозможно шифровать последовательно скачиваемые данные.

## <a name="aes-128-dynamic-encryption"></a>Динамическое шифрование AES-128
### <a name="open-restriction"></a>Ограничение "открытая"
Ограничение Open означает, что система hello будет предоставлять tooanyone ключа hello, выполняющий запрос ключа. Это ограничение подходит для тестирования.

Следующий пример Hello создается политика открытой авторизации и добавляет его ключ содержимого toohello.

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a>Ограничение "по маркеру"
В этом разделе описывается политика авторизации ключа и связать его с помощью ключа содержимого hello toocreate контента. Политика авторизации Hello описывает, какие требования проверки подлинности должно быть toodetermine будут выполнены, если пользователь hello является авторизованным tooreceive hello ключ (например, список «ключ проверки» hello содержит ключ hello был подписан этот токен hello).

Параметр ограничения маркеров tooconfigure hello, необходимо toouse XML toodescribe hello токен требования к проверке подлинности. Hello XML конфигурации ограничений токенов должен соответствовать toohello следующие XML-схемы.

#### <a id="schema"></a>Схема ограничения «по токену»
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

При настройке hello **маркера** ограниченной политики, необходимо указать hello основной ** проверки ключ ** **издателя** и **аудитории** параметров. Hello ** основной ключ проверки ** содержит ключ hello, hello токена был подписан, **издателя** является службой маркеров безопасности hello этот токен hello проблемы. Hello **аудитории** (иногда называется **область**) описывает намерение hello токен hello или ресурса hello hello токен разрешает доступ. Hello служба доставки ключей Media Services проверяет, эти значения в токене hello соответствуют значениям hello в шаблоне hello. 

При использовании **пакета SDK служб мультимедиа для .NET**, можно использовать hello **TokenRestrictionTemplate** токена ограничения класса toogenerate hello.
Следующий пример Hello создает политику авторизации с ограничением токенов. В этом примере hello клиент должен будет toopresent маркер, содержащий: подписывания ключа (VerificationKey), поставщика маркера и необходимых утверждений.

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {
        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();

        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    }

#### <a id="test"></a>Тестовый токен
tooget тестовый токен на основании hello ограничения токенов, которое использовалось для политики авторизации ключа hello, hello следующие.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
    // Note, you need toopass hello key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a>Динамическое шифрование на основе PlayReady
Службы мультимедиа позволяют tooconfigure hello права и ограничения, что требуется для hello tooenforce среда выполнения PlayReady DRM при попытке пользователя tooplay контент, защищенный обратно. 

При защите контента с помощью PlayReady, одно из действий hello необходимо toospecify в политике авторизации является XML-строку, определяющий hello [шаблон лицензии PlayReady](media-services-playready-license-template-overview.md). В пакет SDK служб мультимедиа для .NET, hello **PlayReadyLicenseResponseTemplate** и **PlayReadyLicenseTemplate** классов, помогающая определить hello шаблон лицензии PlayReady.

[В этом разделе](media-services-protect-with-drm.md) показано, как tooencrypt контента с **PlayReady** и **Widevine**.

### <a name="open-restriction"></a>Ограничение "открытая"
Ограничение Open означает, что система hello будет предоставлять tooanyone ключа hello, выполняющий запрос ключа. Это ограничение подходит для тестирования.

Следующий пример Hello создается политика открытой авторизации и добавляет его ключ содержимого toohello.

    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {

        // Create ContentKeyAuthorizationPolicy with Open restrictions 
        // and create authorization policy          

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Open", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                Requirements = null
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a>Ограничение "по маркеру"
Параметр ограничения маркеров tooconfigure hello, необходимо toouse XML toodescribe hello токен требования к проверке подлинности. Hello XML конфигурации ограничений токенов должен соответствовать toohello схемы XML, показанный на [это](#schema) раздела.

    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy tooContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate hello content key authorization policy with hello content key
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;

        return tokenTemplateString;
    }

    static private string GenerateTokenRequirements()
    {

        TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

        template.PrimaryVerificationKey = new SymmetricVerificationKey();
        template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();


        template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

        return TokenRestrictionTemplateSerializer.Serialize(template);
    } 

    static private string ConfigurePlayReadyLicenseTemplate()
    {
        // hello following code configures PlayReady License Template using .NET classes
        // and returns hello XML string.

        //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user. 
        //It contains a field for a custom data string between hello license server and hello application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // toobe returned toohello end users. 
        //It contains hello data on hello content key in hello license and any rights or restrictions toobe 
        //enforced by hello PlayReady DRM runtime when using hello content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether hello license is persistent (saved in persistent storage on hello client) 
        //or non-persistent (only held in memory while hello player is using hello license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use hello license or not.  
        // If true, hello MinimumSecurityLevel property of hello license
        // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class. 
        // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions 
        // configured in hello license and on hello PlayRight itself (for playback specific policy). 
        // Much of hello policy on hello PlayRight has toodo with output restrictions 
        // which control hello types of outputs that hello content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if hello DigitalVideoOnlyContentRestriction is enabled, 
        //then hello DRM runtime will only allow hello video toobe displayed over digital outputs 
        //(analog video outputs won’t be allowed toopass hello content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience. 
        // If hello output protections are configured too restrictive, 
        // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


Тестовый токен на основе hello токена ограничения, используемый для см. политику авторизации ключа hello tooget [это](#test) раздела. 

## <a id="types"></a>Типы, используемые при определении ContentKeyAuthorizationPolicy
### <a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <a id="TokenType"></a>TokenType
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Дальнейшие действия
Настройки политики авторизации ключа содержимого go toohello [как политики доставки активов tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) раздела.

