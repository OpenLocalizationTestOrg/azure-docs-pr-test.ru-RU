---
title: "Настройка политики авторизации ключей содержимого с помощью пакета SDK служб мультимедиа для .NET | Документация Майкрософт"
description: "Узнайте, как настроить политику авторизации для ключа содержимого с помощью пакета SDK для .NET служб мультимедиа."
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
ms.openlocfilehash: 75dd9107dca215a0b31db3d44bada69210fe9ac6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="b9229-103">Динамическое шифрование: настройка политики авторизации ключа содержимого</span><span class="sxs-lookup"><span data-stu-id="b9229-103">Dynamic encryption: configure content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="b9229-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b9229-104">Overview</span></span>
<span data-ttu-id="b9229-105">Службы мультимедиа Microsoft Azure позволяют защищать потоковое содержимое MPEG-DASH, Smooth Streaming и HTTP Live Streaming (HLS) с помощью стандарта AES (использующего 128-разрядные ключи шифрования) или технологии [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="b9229-105">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="b9229-106">AMS позволяет также передавать потоки MPEG DASH с шифрованием Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="b9229-106">AMS also enables you to deliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="b9229-107">PlayReady и Widewine шифруются согласно спецификации общего шифрования (ISO/IEC 23001-7 CENC).</span><span class="sxs-lookup"><span data-stu-id="b9229-107">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="b9229-108">Кроме того, службы мультимедиа включают в себя **службы доставки ключей и лицензий** , с помощью которых клиенты могут получать ключи AES либо лицензии PlayReady или Widevine для воспроизведения зашифрованного содержимого.</span><span class="sxs-lookup"><span data-stu-id="b9229-108">Media Services also provides a **Key/License Delivery Service** from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.</span></span>

<span data-ttu-id="b9229-109">Если вы хотите, чтобы службы мультимедиа зашифровали ресурс-контейнер, свяжите ключ шифрования (**CommonEncryption** или **EnvelopeEncryption**) с этим ресурсом (как описано [здесь](media-services-dotnet-create-contentkey.md)) и настройте политики авторизации для ключа (следуя инструкциям в этой статье).</span><span class="sxs-lookup"><span data-stu-id="b9229-109">If you want for Media Services to encrypt an asset, you need to associate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with the asset (as described [here](media-services-dotnet-create-contentkey.md)) and also configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="b9229-110">Когда поток запрашивается проигрывателем, службы мультимедиа используют указанный ключ для динамического шифрования содержимого с помощью AES или DRM.</span><span class="sxs-lookup"><span data-stu-id="b9229-110">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES or DRM encryption.</span></span> <span data-ttu-id="b9229-111">Чтобы расшифровать поток, проигрыватель запросит ключ у службы доставки ключей.</span><span class="sxs-lookup"><span data-stu-id="b9229-111">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="b9229-112">Чтобы определить, есть ли у пользователя право на получение ключа, служба оценивает политики авторизации, заданные для ключа.</span><span class="sxs-lookup"><span data-stu-id="b9229-112">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="b9229-113">Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи.</span><span class="sxs-lookup"><span data-stu-id="b9229-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="b9229-114">Для политики авторизации ключа содержимого можно задать одно или несколько ограничений: **открытая** авторизация или авторизация с помощью **маркера**.</span><span class="sxs-lookup"><span data-stu-id="b9229-114">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="b9229-115">При ограничении по маркеру к политике должен прилагаться маркер, выданный службой маркеров безопасности (STS).</span><span class="sxs-lookup"><span data-stu-id="b9229-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="b9229-116">Службы мультимедиа поддерживают маркеры в формате **простого веб-маркера** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) и формате **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)).</span><span class="sxs-lookup"><span data-stu-id="b9229-116">Media Services supports tokens in the **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token** ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="b9229-117">Службы мультимедиа не предоставляют службы маркеров безопасности.</span><span class="sxs-lookup"><span data-stu-id="b9229-117">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="b9229-118">Для выдачи маркеров можно создать пользовательскую службу STS или использовать службу Microsoft Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="b9229-118">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="b9229-119">Чтобы создать маркер, подписанный указанным ключом, и получить утверждения, указанные в конфигурации ограничения по маркерам, должна быть настроена служба маркеров безопасности (как описано в этой статье).</span><span class="sxs-lookup"><span data-stu-id="b9229-119">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="b9229-120">Служба доставки ключей служб мультимедиа возвращает клиенту ключ шифрования, если маркер является допустимым и утверждения маркера соответствуют утверждениям, настроенным для ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="b9229-120">The Media Services key delivery service will return the encryption key to the client if the token is valid and the claims in the token match those configured for the content key.</span></span>

<span data-ttu-id="b9229-121">Дополнительную информацию см. в разделе</span><span class="sxs-lookup"><span data-stu-id="b9229-121">For more information, see</span></span>

<span data-ttu-id="b9229-122">[JWT token Authentication in Azure Media Services and Dynamic Encryption](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/) (Аутентификация токена JWT в службах мультимедиа Azure и динамическое шифрование)</span><span class="sxs-lookup"><span data-stu-id="b9229-122">[JWT token authentication](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)</span></span>

<span data-ttu-id="b9229-123">[Интегрируйте приложение на основе OWIN MVC служб мультимедиа Azure с Azure Active Directory и ограничьте доставку ключей содержимого на основе утверждений JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="b9229-123">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="b9229-124">[Используйте Azure ACS для выдачи токенов](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="b9229-124">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="b9229-125">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="b9229-125">Some considerations apply:</span></span>
* <span data-ttu-id="b9229-126">При создании учетной записи AMS в нее добавляется конечная точка потоковой передачи **по умолчанию** в состоянии **Остановлена**.</span><span class="sxs-lookup"><span data-stu-id="b9229-126">When your AMS account is created a **default** streaming endpoint is added  to your account in the **Stopped** state.</span></span> <span data-ttu-id="b9229-127">Чтобы начать потоковую передачу содержимого и воспользоваться динамической упаковкой и динамическим шифрованием, конечная точка потоковой передачи должна находиться в состоянии **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="b9229-127">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint has to be in the **Running** state.</span></span> 
* <span data-ttu-id="b9229-128">Ресурс должен содержать набор MP4-файлов или файлов Smooth Streaming с переменной скоростью.</span><span class="sxs-lookup"><span data-stu-id="b9229-128">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="b9229-129">Дополнительные сведения см. в статье о [кодировании ресурсов](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="b9229-129">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="b9229-130">Отправляйте и кодируйте ресурсы с помощью параметра **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="b9229-130">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="b9229-131">Если вы планируете использовать несколько ключей содержимого, для которых требуется одинаковая конфигурация политики, настоятельно рекомендуется создать единую политику авторизации и повторно использовать ее с несколькими ключами содержимого.</span><span class="sxs-lookup"><span data-stu-id="b9229-131">If you plan to have multiple content keys that require the same policy configuration, it is strongly recommended to create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="b9229-132">Служба доставки ключей кэширует политику ContentKeyAuthorizationPolicy и связанные с ней объекты (параметры и ограничения политики) за 15 минут.</span><span class="sxs-lookup"><span data-stu-id="b9229-132">The Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="b9229-133">Если создать политику ContentKeyAuthorizationPolicy и задать для нее ограничение "по маркеру", а затем протестировать ее, то последующее обновление для использования ограничения "открытая" займет примерно 15 минут.</span><span class="sxs-lookup"><span data-stu-id="b9229-133">If you create a ContentKeyAuthorizationPolicy and specify to use a “Token” restriction, then test it, and then update the policy to “Open” restriction, it will take roughly 15 minutes before the policy switches to the “Open” version of the policy.</span></span>
* <span data-ttu-id="b9229-134">При добавлении или обновлении политики доставки ресурсов необходимо удалить существующий указатель (если он есть) и создать новый.</span><span class="sxs-lookup"><span data-stu-id="b9229-134">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="b9229-135">В настоящее время невозможно шифровать последовательно скачиваемые данные.</span><span class="sxs-lookup"><span data-stu-id="b9229-135">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="b9229-136">Динамическое шифрование AES-128</span><span class="sxs-lookup"><span data-stu-id="b9229-136">AES-128 Dynamic Encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="b9229-137">Ограничение "открытая"</span><span class="sxs-lookup"><span data-stu-id="b9229-137">Open Restriction</span></span>
<span data-ttu-id="b9229-138">Ограничение открытого типа означает, что система будет доставлять ключ всем, кто его запросит.</span><span class="sxs-lookup"><span data-stu-id="b9229-138">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="b9229-139">Это ограничение подходит для тестирования.</span><span class="sxs-lookup"><span data-stu-id="b9229-139">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="b9229-140">В следующем примере создается политика авторизации типа "открытая", которая затем добавляется в ключ содержимого.</span><span class="sxs-lookup"><span data-stu-id="b9229-140">The following example creates an open authorization policy and adds it to the content key.</span></span>

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

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
    }


### <a name="token-restriction"></a><span data-ttu-id="b9229-141">Ограничение "по маркеру"</span><span class="sxs-lookup"><span data-stu-id="b9229-141">Token Restriction</span></span>
<span data-ttu-id="b9229-142">В этом разделе рассказывается о том, как создать политику авторизации ключа содержимого и связать ее с ключом содержимого.</span><span class="sxs-lookup"><span data-stu-id="b9229-142">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="b9229-143">Политика авторизации определяет, какие требования авторизации должны быть удовлетворены, чтобы у пользователя было право на получения ключа (например, должен ли список ключей проверки содержать ключ, с помощью которого был подписан маркер).</span><span class="sxs-lookup"><span data-stu-id="b9229-143">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key (for example, does the “verification key” list contain the key that the token was signed with).</span></span>

<span data-ttu-id="b9229-144">Чтобы настроить параметр ограничения маркера, необходимо использовать XML для описания требований к авторизации маркера.</span><span class="sxs-lookup"><span data-stu-id="b9229-144">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="b9229-145">XML-файл конфигурации ограничений по маркеру должен соответствовать следующей схеме XML.</span><span class="sxs-lookup"><span data-stu-id="b9229-145">The token restriction configuration XML must conform to the following XML schema.</span></span>

#### <span data-ttu-id="b9229-146"><a id="schema"></a>Схема ограничения «по токену»</span><span class="sxs-lookup"><span data-stu-id="b9229-146"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="b9229-147">При настройке политики ограничения по **маркеру** необходимо задать такие параметры, как **основной ключ проверки**, **издатель** и **аудитория**.</span><span class="sxs-lookup"><span data-stu-id="b9229-147">When configuring the **token** restricted policy, you must specify the primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="b9229-148">**Основной ключ проверки** содержит ключ, которым подписан маркер, а **издатель** — это служба маркеров безопасности, которая выдает маркер.</span><span class="sxs-lookup"><span data-stu-id="b9229-148">The **primary verification key **contains the key that the token was signed with, **issuer** is the secure token service that issues the token.</span></span> <span data-ttu-id="b9229-149">**Аудитория** (иногда называется **областью**) описывает назначение маркера или ресурс, доступ к которому обеспечивает маркер.</span><span class="sxs-lookup"><span data-stu-id="b9229-149">The **audience** (sometimes called **scope**) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="b9229-150">Служба доставки ключей служб мультимедиа проверяет, соответствуют ли эти значения в маркере значениям в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="b9229-150">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span> 

<span data-ttu-id="b9229-151">При использовании **пакета SDK служб мультимедиа для .NET** можно использовать класс **TokenRestrictionTemplate** для создания токена ограничения.</span><span class="sxs-lookup"><span data-stu-id="b9229-151">When using **Media Services SDK for .NET**, you can use the **TokenRestrictionTemplate** class to generate the restriction token.</span></span>
<span data-ttu-id="b9229-152">В следующем примере создается политика авторизации с ограничением "по маркеру".</span><span class="sxs-lookup"><span data-stu-id="b9229-152">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="b9229-153">В этом примере клиенту нужно будет предоставить маркер, в котором содержатся: ключ подписывания (VerificationKey), поставщик маркера и требуемые утверждения.</span><span class="sxs-lookup"><span data-stu-id="b9229-153">In this example, the client would have to present a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

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

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

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

#### <span data-ttu-id="b9229-154"><a id="test"></a>Тестовый токен</span><span class="sxs-lookup"><span data-stu-id="b9229-154"><a id="test"></a>Test token</span></span>
<span data-ttu-id="b9229-155">Чтобы получить маркер тестирования на основе маркера ограничения, который использовался для политики авторизации ключа, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="b9229-155">To get a test token based on the token restriction that was used for the key authorization policy, do the following.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the the data in the given TokenRestrictionTemplate.
    // Note, you need to pass the key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();


## <a name="playready-dynamic-encryption"></a><span data-ttu-id="b9229-156">Динамическое шифрование на основе PlayReady</span><span class="sxs-lookup"><span data-stu-id="b9229-156">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="b9229-157">Службы мультимедиа позволяют настраивать права и ограничения, которые должны применяться в среде выполнения PlayReady DRM при попытке пользователя воспроизвести защищенное содержимое.</span><span class="sxs-lookup"><span data-stu-id="b9229-157">Media Services enables you to configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to play back protected content.</span></span> 

<span data-ttu-id="b9229-158">При защите содержимого с помощью PlayReady, среди прочего, в политике авторизации необходимо указать XML-строку, определяющую [шаблон лицензии PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9229-158">When protecting your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="b9229-159">Классы **PlayReadyLicenseResponseTemplate** и **PlayReadyLicenseTemplate** в пакет SDK служб мультимедиа для .NET помогут определить шаблон лицензии PlayReady.</span><span class="sxs-lookup"><span data-stu-id="b9229-159">In Media Services SDK for .NET, the **PlayReadyLicenseResponseTemplate** and **PlayReadyLicenseTemplate** classes will help you define the PlayReady License Template.</span></span>

<span data-ttu-id="b9229-160">[В этой статье](media-services-protect-with-drm.md) описывается шифрование содержимого с помощью **PlayReady** и **Widevine**.</span><span class="sxs-lookup"><span data-stu-id="b9229-160">[This topic](media-services-protect-with-drm.md) shows how to encrypt your content with **PlayReady** and **Widevine**.</span></span>

### <a name="open-restriction"></a><span data-ttu-id="b9229-161">Ограничение "открытая"</span><span class="sxs-lookup"><span data-stu-id="b9229-161">Open Restriction</span></span>
<span data-ttu-id="b9229-162">Ограничение открытого типа означает, что система будет доставлять ключ всем, кто его запросит.</span><span class="sxs-lookup"><span data-stu-id="b9229-162">Open restriction means the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="b9229-163">Это ограничение подходит для тестирования.</span><span class="sxs-lookup"><span data-stu-id="b9229-163">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="b9229-164">В следующем примере создается политика авторизации типа "открытая", которая затем добавляется в ключ содержимого.</span><span class="sxs-lookup"><span data-stu-id="b9229-164">The following example creates an open authorization policy and adds it to the content key.</span></span>

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

        // Associate the content key authorization policy with the content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }

### <a name="token-restriction"></a><span data-ttu-id="b9229-165">Ограничение "по маркеру"</span><span class="sxs-lookup"><span data-stu-id="b9229-165">Token Restriction</span></span>
<span data-ttu-id="b9229-166">Чтобы настроить параметр ограничения маркера, необходимо использовать XML для описания требований к авторизации маркера.</span><span class="sxs-lookup"><span data-stu-id="b9229-166">To configure the token restriction option, you need to use an XML to describe the token’s authorization requirements.</span></span> <span data-ttu-id="b9229-167">XML-файл конфигурации ограничений по токену должен соответствовать схеме XML, показанной в [этом](#schema) разделе.</span><span class="sxs-lookup"><span data-stu-id="b9229-167">The token restriction configuration XML must conform to the XML schema shown in [this](#schema) section.</span></span>

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

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key
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
        // The following code configures PlayReady License Template using .NET classes
        // and returns the XML string.

        //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user. 
        //It contains a field for a custom data string between the license server and the application 
        //(may be useful for custom app logic) as well as a list of one or more license templates.
        PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

        // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
        // to be returned to the end users. 
        //It contains the data on the content key in the license and any rights or restrictions to be 
        //enforced by the PlayReady DRM runtime when using the content key.
        PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
        //Configure whether the license is persistent (saved in persistent storage on the client) 
        //or non-persistent (only held in memory while the player is using the license).  
        licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

        // AllowTestDevices controls whether test devices can use the license or not.  
        // If true, the MinimumSecurityLevel property of the license
        // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
        licenseTemplate.AllowTestDevices = true;


        // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class. 
        // It grants the user the ability to playback the content subject to the zero or more restrictions 
        // configured in the license and on the PlayRight itself (for playback specific policy). 
        // Much of the policy on the PlayRight has to do with output restrictions 
        // which control the types of outputs that the content can be played over and 
        // any restrictions that must be put in place when using a given output.
        // For example, if the DigitalVideoOnlyContentRestriction is enabled, 
        //then the DRM runtime will only allow the video to be displayed over digital outputs 
        //(analog video outputs won’t be allowed to pass the content).

        //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience. 
        // If the output protections are configured too restrictive, 
        // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

        // For example:
        //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

        responseTemplate.LicenseTemplates.Add(licenseTemplate);

        return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
    }


<span data-ttu-id="b9229-168">Для получения тестового токена на основе токена ограничения, который использовался для политики авторизации ключа, см. [этот](#test) раздел.</span><span class="sxs-lookup"><span data-stu-id="b9229-168">To get a test token based on the token restriction that was used for the key authorization policy see [this](#test) section.</span></span> 

## <span data-ttu-id="b9229-169"><a id="types"></a>Типы, используемые при определении ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="b9229-169"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="b9229-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="b9229-170"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="b9229-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="b9229-171"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }

### <span data-ttu-id="b9229-172"><a id="TokenType"></a>TokenType</span><span class="sxs-lookup"><span data-stu-id="b9229-172"><a id="TokenType"></a>TokenType</span></span>
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="b9229-173">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b9229-173">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b9229-174">Отзывы</span><span class="sxs-lookup"><span data-stu-id="b9229-174">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="b9229-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9229-175">Next step</span></span>
<span data-ttu-id="b9229-176">Теперь, после настройки политики авторизации ключа содержимого, перейдите к разделу [Как настроить политику доставки ресурсов](media-services-dotnet-configure-asset-delivery-policy.md) .</span><span class="sxs-lookup"><span data-stu-id="b9229-176">Now that you have configured content key's authorization policy, go to the [How to configure asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md) topic.</span></span>

