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
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="64bb9-103">Динамическое шифрование: настройка политики авторизации ключа содержимого</span><span class="sxs-lookup"><span data-stu-id="64bb9-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="64bb9-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="64bb9-104">Overview</span></span>
<span data-ttu-id="64bb9-105">Службы мультимедиа Microsoft Azure позволяет toodeliver MPEG-DASH, Smooth Streaming и HTTP-Live-Streaming (HLS) потоки, защищенных с помощью Advanced Encryption Standard (AES) (с помощью 128-битные ключи шифрования) или [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="64bb9-105">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="64bb9-106">AMS также позволяет вам toodeliver ТИРЕ потоки зашифрован Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="64bb9-106">AMS also enables you toodeliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="64bb9-107">PlayReady и Widevine шифруются на hello спецификации общее шифрование (CENC ISO/IEC 23001-7).</span><span class="sxs-lookup"><span data-stu-id="64bb9-107">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="64bb9-108">Службы мультимедиа также предоставляют **служба доставки ключа/лицензий** из которых клиенты могут получить ключи AES или PlayReady или Widevine лицензий tooplay hello зашифрованное содержимое.</span><span class="sxs-lookup"><span data-stu-id="64bb9-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses tooplay hello encrypted content.</span></span>

<span data-ttu-id="64bb9-109">Если требуется для служб мультимедиа tooencrypt актива, необходимо tooassociate ключ шифрования (**CommonEncryption** или **EnvelopeEncryption**) с активом hello (как описано [здесь](media-services-dotnet-create-contentkey.md)) а также настроить политики авторизации для ключа hello (как описано в этой статье).</span><span class="sxs-lookup"><span data-stu-id="64bb9-109">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="64bb9-110">Когда проигрыватель запрашивает поток, службы мультимедиа используют указанный hello toodynamically ключа шифрования контента с помощью шифрования AES или DRM.</span><span class="sxs-lookup"><span data-stu-id="64bb9-110">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="64bb9-111">поток toodecrypt hello, hello проигрыватель будет запрашивать ключ hello из службы доставки ключей hello.</span><span class="sxs-lookup"><span data-stu-id="64bb9-111">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="64bb9-112">toodecide ли он hello авторизованных tooget hello ключ, hello служба оценивает политики авторизации hello, заданные для ключа hello.</span><span class="sxs-lookup"><span data-stu-id="64bb9-112">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="64bb9-113">Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи.</span><span class="sxs-lookup"><span data-stu-id="64bb9-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="64bb9-114">Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: **откройте** или **маркера** ограниченного использования программ.</span><span class="sxs-lookup"><span data-stu-id="64bb9-114">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="64bb9-115">политика с ограничением токенов Hello должны сопровождаться маркера, выданного по токенов безопасности службы (STS).</span><span class="sxs-lookup"><span data-stu-id="64bb9-115">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="64bb9-116">Службы мультимедиа поддерживают только токены в hello **токенов SWT** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) формат и **веб-маркера JSON** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) формате.</span><span class="sxs-lookup"><span data-stu-id="64bb9-116">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="64bb9-117">Службы мультимедиа не предоставляют службы маркеров безопасности.</span><span class="sxs-lookup"><span data-stu-id="64bb9-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="64bb9-118">Можно создать настраиваемую STS или использовать токены tooissue Microsoft Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="64bb9-118">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="64bb9-119">Hello STS должна быть настроенный toocreate токен, подписанным с указанным ключом hello и выдающими утверждения, указанные в конфигурации ограничения токенов hello (как описано в этой статье).</span><span class="sxs-lookup"><span data-stu-id="64bb9-119">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="64bb9-120">Hello служба доставки ключей Media Services возвратит клиент toohello ключа шифрования hello Если hello маркер является допустимым и hello утверждения маркера hello соответствуют настроенным для ключа контента hello.</span><span class="sxs-lookup"><span data-stu-id="64bb9-120">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="64bb9-121">Дополнительную информацию см. в разделе</span><span class="sxs-lookup"><span data-stu-id="64bb9-121">For more information, see</span></span>

<span data-ttu-id="64bb9-122">[JWT token Authentication in Azure Media Services and Dynamic Encryption](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/) (Аутентификация токена JWT в службах мультимедиа Azure и динамическое шифрование)</span><span class="sxs-lookup"><span data-stu-id="64bb9-122">[JWT token authentication](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)</span></span>

<span data-ttu-id="64bb9-123">[Интегрируйте приложение на основе OWIN MVC служб мультимедиа Azure с Azure Active Directory и ограничьте доставку ключей содержимого на основе утверждений JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="64bb9-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="64bb9-124">[Использовать токены Azure ACS tooissue](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="64bb9-124">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="64bb9-125">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="64bb9-125">Some considerations apply:</span></span>
* <span data-ttu-id="64bb9-126">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="64bb9-126">When your AMS account is created a **default** streaming endpoint is added  tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="64bb9-127">toostart вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования, потоковой передачи конечной точки потоковой передачи имеет toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="64bb9-127">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has toobe in hello **Running** state.</span></span> 
* <span data-ttu-id="64bb9-128">Ресурс должен содержать набор MP4-файлов или файлов Smooth Streaming с переменной скоростью.</span><span class="sxs-lookup"><span data-stu-id="64bb9-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="64bb9-129">Дополнительные сведения см. в статье о [кодировании ресурсов](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="64bb9-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="64bb9-130">Отправляйте и кодируйте ресурсы с помощью параметра **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="64bb9-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="64bb9-131">Если планируется toohave нескольких ключей контента, требующих hello же конфигурации политики, это настоятельно рекомендуется toocreate одну политику авторизации и использовать ее с несколькими ключами контента.</span><span class="sxs-lookup"><span data-stu-id="64bb9-131">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="64bb9-132">Hello служба доставки ключей кэширует ContentKeyAuthorizationPolicy и связанные объекты (параметры политики и ограничения) в течение 15 минут.</span><span class="sxs-lookup"><span data-stu-id="64bb9-132">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="64bb9-133">Если создать политику ContentKeyAuthorizationPolicy и укажите toouse ограничения «Token», а затем проверить его, а затем обновить политику hello слишком «открыть» ограниченного использования программ, займет примерно 15 минут, прежде чем hello политики коммутаторы toohello версию «Open» политики hello.</span><span class="sxs-lookup"><span data-stu-id="64bb9-133">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="64bb9-134">При добавлении или обновлении политики доставки ресурсов необходимо удалить существующий указатель (если он есть) и создать новый.</span><span class="sxs-lookup"><span data-stu-id="64bb9-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="64bb9-135">В настоящее время невозможно шифровать последовательно скачиваемые данные.</span><span class="sxs-lookup"><span data-stu-id="64bb9-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="64bb9-136">Динамическое шифрование AES-128</span><span class="sxs-lookup"><span data-stu-id="64bb9-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="64bb9-137">Ограничение "открытая"</span><span class="sxs-lookup"><span data-stu-id="64bb9-137">Open Restriction</span></span>
<span data-ttu-id="64bb9-138">Ограничение Open означает, что система hello будет предоставлять tooanyone ключа hello, выполняющий запрос ключа.</span><span class="sxs-lookup"><span data-stu-id="64bb9-138">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="64bb9-139">Это ограничение подходит для тестирования.</span><span class="sxs-lookup"><span data-stu-id="64bb9-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="64bb9-140">Следующий пример Hello создается политика открытой авторизации и добавляет его ключ содержимого toohello.</span><span class="sxs-lookup"><span data-stu-id="64bb9-140">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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


### <a name="token-restriction"></a><span data-ttu-id="64bb9-141">Ограничение "по маркеру"</span><span class="sxs-lookup"><span data-stu-id="64bb9-141">Token Restriction</span></span>
<span data-ttu-id="64bb9-142">В этом разделе описывается политика авторизации ключа и связать его с помощью ключа содержимого hello toocreate контента.</span><span class="sxs-lookup"><span data-stu-id="64bb9-142">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="64bb9-143">Политика авторизации Hello описывает, какие требования проверки подлинности должно быть toodetermine будут выполнены, если пользователь hello является авторизованным tooreceive hello ключ (например, список «ключ проверки» hello содержит ключ hello был подписан этот токен hello).</span><span class="sxs-lookup"><span data-stu-id="64bb9-143">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="64bb9-144">Параметр ограничения маркеров tooconfigure hello, необходимо toouse XML toodescribe hello токен требования к проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="64bb9-144">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="64bb9-145">Hello XML конфигурации ограничений токенов должен соответствовать toohello следующие XML-схемы.</span><span class="sxs-lookup"><span data-stu-id="64bb9-145">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="64bb9-146"><a id="schema"></a>Схема ограничения «по токену»</span><span class="sxs-lookup"><span data-stu-id="64bb9-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="64bb9-147">При настройке hello **маркера** ограниченной политики, необходимо указать hello основной ** проверки ключ ** **издателя** и **аудитории** параметров.</span><span class="sxs-lookup"><span data-stu-id="64bb9-147">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="64bb9-148">Hello ** основной ключ проверки ** содержит ключ hello, hello токена был подписан, **издателя** является службой маркеров безопасности hello этот токен hello проблемы.</span><span class="sxs-lookup"><span data-stu-id="64bb9-148">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="64bb9-149">Hello **аудитории** (иногда называется **область**) описывает намерение hello токен hello или ресурса hello hello токен разрешает доступ.</span><span class="sxs-lookup"><span data-stu-id="64bb9-149">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="64bb9-150">Hello служба доставки ключей Media Services проверяет, эти значения в токене hello соответствуют значениям hello в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="64bb9-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="64bb9-151">При использовании **пакета SDK служб мультимедиа для .NET**, можно использовать hello **TokenRestrictionTemplate** токена ограничения класса toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="64bb9-151">When using **Media Services SDK for .NET**, you can use hello **TokenRestrictionTemplate** class toogenerate hello restriction token.</span></span>
<span data-ttu-id="64bb9-152">Следующий пример Hello создает политику авторизации с ограничением токенов.</span><span class="sxs-lookup"><span data-stu-id="64bb9-152">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="64bb9-153">В этом примере hello клиент должен будет toopresent маркер, содержащий: подписывания ключа (VerificationKey), поставщика маркера и необходимых утверждений.</span><span class="sxs-lookup"><span data-stu-id="64bb9-153">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

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

#### <span data-ttu-id="64bb9-154"><a id="test"></a>Тестовый токен</span><span class="sxs-lookup"><span data-stu-id="64bb9-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="64bb9-155">tooget тестовый токен на основании hello ограничения токенов, которое использовалось для политики авторизации ключа hello, hello следующие.</span><span class="sxs-lookup"><span data-stu-id="64bb9-155">tooget a test token based on hello token restriction that was used for hello key authorization policy, do hello following.</span></span>

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


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="64bb9-156">Динамическое шифрование на основе PlayReady</span><span class="sxs-lookup"><span data-stu-id="64bb9-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="64bb9-157">Службы мультимедиа позволяют tooconfigure hello права и ограничения, что требуется для hello tooenforce среда выполнения PlayReady DRM при попытке пользователя tooplay контент, защищенный обратно.</span><span class="sxs-lookup"><span data-stu-id="64bb9-157">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="64bb9-158">При защите контента с помощью PlayReady, одно из действий hello необходимо toospecify в политике авторизации является XML-строку, определяющий hello [шаблон лицензии PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64bb9-158">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="64bb9-159">В пакет SDK служб мультимедиа для .NET, hello **PlayReadyLicenseResponseTemplate** и **PlayReadyLicenseTemplate** классов, помогающая определить hello шаблон лицензии PlayReady.</span><span class="sxs-lookup"><span data-stu-id="64bb9-159">In Media Services SDK for .NET, hello **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define hello PlayReady License Template.</span></span>

<span data-ttu-id="64bb9-160">[В этом разделе](media-services-protect-with-drm.md) показано, как tooencrypt контента с **PlayReady** и **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="64bb9-160">[This topic](media-services-protect-with-drm.md) shows how tooencrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="64bb9-161">Ограничение "открытая"</span><span class="sxs-lookup"><span data-stu-id="64bb9-161">Open Restriction</span></span>
<span data-ttu-id="64bb9-162">Ограничение Open означает, что система hello будет предоставлять tooanyone ключа hello, выполняющий запрос ключа.</span><span class="sxs-lookup"><span data-stu-id="64bb9-162">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="64bb9-163">Это ограничение подходит для тестирования.</span><span class="sxs-lookup"><span data-stu-id="64bb9-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="64bb9-164">Следующий пример Hello создается политика открытой авторизации и добавляет его ключ содержимого toohello.</span><span class="sxs-lookup"><span data-stu-id="64bb9-164">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

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

### <a name="token-restriction"></a><span data-ttu-id="64bb9-165">Ограничение "по маркеру"</span><span class="sxs-lookup"><span data-stu-id="64bb9-165">Token Restriction</span></span>
<span data-ttu-id="64bb9-166">Параметр ограничения маркеров tooconfigure hello, необходимо toouse XML toodescribe hello токен требования к проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="64bb9-166">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="64bb9-167">Hello XML конфигурации ограничений токенов должен соответствовать toohello схемы XML, показанный на [это](#schema) раздела.</span><span class="sxs-lookup"><span data-stu-id="64bb9-167">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

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


<span data-ttu-id="64bb9-168">Тестовый токен на основе hello токена ограничения, используемый для см. политику авторизации ключа hello tooget [это](#test) раздела.</span><span class="sxs-lookup"><span data-stu-id="64bb9-168">tooget a test token based on hello token restriction that was used for hello key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="64bb9-169"><a id="types"></a>Типы, используемые при определении ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="64bb9-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="64bb9-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="64bb9-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="64bb9-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="64bb9-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="64bb9-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="64bb9-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="64bb9-173">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="64bb9-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="64bb9-174">Отзывы</span><span class="sxs-lookup"><span data-stu-id="64bb9-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="64bb9-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64bb9-175">Next step</span></span>
<span data-ttu-id="64bb9-176">Настройки политики авторизации ключа содержимого go toohello [как политики доставки активов tooconfigure](media-services-dotnet-configure-asset-delivery-policy.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="64bb9-176">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

