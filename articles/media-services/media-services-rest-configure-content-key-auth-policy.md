---
title: "Политика авторизации ключей содержимого aaaConfigure с REST - Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure политику авторизации для ключа контента с помощью API REST служб мультимедиа."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7af5f9e2-8ed8-43f2-843b-580ce8759fd4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: c058b7682bcbfb736faba18ec7fce33f2f2acb49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="db93d-103">Динамическое шифрование: настройка политики авторизации ключа содержимого</span><span class="sxs-lookup"><span data-stu-id="db93d-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="db93d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="db93d-104">Overview</span></span>
<span data-ttu-id="db93d-105">Службы мультимедиа Microsoft Azure позволяет вам toodeliver содержимого (динамически) зашифрован Advanced Encryption Standard (AES) (с помощью 128-битные ключи шифрования) и PlayReady или Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="db93d-105">Microsoft Azure Media Services enables you toodeliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="db93d-106">Службы мультимедиа также предоставляет услугу для доставки ключей и лицензии PlayReady или Widevine tooauthorized клиентов.</span><span class="sxs-lookup"><span data-stu-id="db93d-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses tooauthorized clients.</span></span>

<span data-ttu-id="db93d-107">Если требуется для служб мультимедиа tooencrypt актива, необходимо tooassociate ключ шифрования (**CommonEncryption** или **EnvelopeEncryption**) с активом hello (как описано [здесь](media-services-rest-create-contentkey.md)) а также настроить политики авторизации для ключа hello (как описано в этой статье).</span><span class="sxs-lookup"><span data-stu-id="db93d-107">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="db93d-108">Когда проигрыватель запрашивает поток, службы мультимедиа используют указанный hello toodynamically ключа шифрования с помощью шифрования AES или PlayReady контента.</span><span class="sxs-lookup"><span data-stu-id="db93d-108">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="db93d-109">поток toodecrypt hello, hello проигрыватель будет запрашивать ключ hello из службы доставки ключей hello.</span><span class="sxs-lookup"><span data-stu-id="db93d-109">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="db93d-110">toodecide ли он hello авторизованных tooget hello ключ, hello служба оценивает политики авторизации hello, заданные для ключа hello.</span><span class="sxs-lookup"><span data-stu-id="db93d-110">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="db93d-111">Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи.</span><span class="sxs-lookup"><span data-stu-id="db93d-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="db93d-112">Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: **откройте** или **маркера** ограниченного использования программ.</span><span class="sxs-lookup"><span data-stu-id="db93d-112">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="db93d-113">политика с ограничением токенов Hello должны сопровождаться маркера, выданного по токенов безопасности службы (STS).</span><span class="sxs-lookup"><span data-stu-id="db93d-113">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="db93d-114">Службы мультимедиа поддерживают только токены в hello **токенов SWT** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) формат и ** формата JSON Web Token **(JWT).</span><span class="sxs-lookup"><span data-stu-id="db93d-114">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="db93d-115">Службы мультимедиа не предоставляют службы маркеров безопасности.</span><span class="sxs-lookup"><span data-stu-id="db93d-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="db93d-116">Можно создать настраиваемую STS или использовать токены tooissue Microsoft Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="db93d-116">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="db93d-117">Hello STS должна быть настроенный toocreate токен, подписанным с указанным ключом hello и выдающими утверждения, указанные в конфигурации ограничения токенов hello (как описано в этой статье).</span><span class="sxs-lookup"><span data-stu-id="db93d-117">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="db93d-118">Hello служба доставки ключей Media Services возвратит клиент toohello ключа шифрования hello Если hello маркер является допустимым и hello утверждения маркера hello соответствуют настроенным для ключа контента hello.</span><span class="sxs-lookup"><span data-stu-id="db93d-118">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="db93d-119">Дополнительную информацию см. в разделе</span><span class="sxs-lookup"><span data-stu-id="db93d-119">For more information, see</span></span>

<span data-ttu-id="db93d-120">[JWT token Authentication in Azure Media Services and Dynamic Encryption](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/) (Аутентификация токена JWT в службах мультимедиа Azure и динамическое шифрование)</span><span class="sxs-lookup"><span data-stu-id="db93d-120">[JWT token authentication](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)</span></span>

<span data-ttu-id="db93d-121">[Интегрируйте приложение на основе OWIN MVC служб мультимедиа Azure с Azure Active Directory и ограничьте доставку ключей содержимого на основе утверждений JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="db93d-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="db93d-122">[Использовать токены Azure ACS tooissue](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="db93d-122">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="db93d-123">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="db93d-123">Some considerations apply:</span></span>
* <span data-ttu-id="db93d-124">toobe может toouse динамической упаковки и динамического шифрования, убедитесь, что hello потоковой передачи конечной точки, из которого нужно toostream содержимого находится в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="db93d-124">toobe able toouse dynamic packaging and dynamic encryption, make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>
* <span data-ttu-id="db93d-125">Ресурс должен содержать набор MP4-файлов или файлов Smooth Streaming с переменной скоростью.</span><span class="sxs-lookup"><span data-stu-id="db93d-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="db93d-126">Дополнительные сведения см. в статье о [кодировании ресурсов](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="db93d-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="db93d-127">Отправляйте и кодируйте ресурсы с помощью параметра **AssetCreationOptions.StorageEncrypted** .</span><span class="sxs-lookup"><span data-stu-id="db93d-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="db93d-128">Если планируется toohave нескольких ключей контента, требующих hello же конфигурации политики, это настоятельно рекомендуется toocreate одну политику авторизации и использовать ее с несколькими ключами контента.</span><span class="sxs-lookup"><span data-stu-id="db93d-128">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="db93d-129">Hello служба доставки ключей кэширует ContentKeyAuthorizationPolicy и связанные объекты (параметры политики и ограничения) в течение 15 минут.</span><span class="sxs-lookup"><span data-stu-id="db93d-129">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="db93d-130">Если создать политику ContentKeyAuthorizationPolicy и укажите toouse ограничения «Token», а затем проверить его, а затем обновить политику hello слишком «открыть» ограниченного использования программ, займет примерно 15 минут, прежде чем hello политики коммутаторы toohello версию «Open» политики hello.</span><span class="sxs-lookup"><span data-stu-id="db93d-130">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="db93d-131">При добавлении или обновлении политики доставки ресурсов необходимо удалить существующий указатель (если он есть) и создать новый.</span><span class="sxs-lookup"><span data-stu-id="db93d-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="db93d-132">В настоящее время невозможно шифровать последовательно скачиваемые данные.</span><span class="sxs-lookup"><span data-stu-id="db93d-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="db93d-133">Динамическое шифрование AES-128</span><span class="sxs-lookup"><span data-stu-id="db93d-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="db93d-134">При работе с API REST служб мультимедиа hello hello действуют следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="db93d-134">When working with hello Media Services REST API, hello following considerations apply:</span></span>
> 
> <span data-ttu-id="db93d-135">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="db93d-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="db93d-136">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="db93d-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="db93d-137">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="db93d-137">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="db93d-138">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="db93d-138">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="db93d-139">Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="db93d-139">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="db93d-140">Ограничение "открытая"</span><span class="sxs-lookup"><span data-stu-id="db93d-140">Open Restriction</span></span>
<span data-ttu-id="db93d-141">Ограничение Open означает, что система hello будет предоставлять tooanyone ключа hello, выполняющий запрос ключа.</span><span class="sxs-lookup"><span data-stu-id="db93d-141">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="db93d-142">Это ограничение подходит для тестирования.</span><span class="sxs-lookup"><span data-stu-id="db93d-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="db93d-143">Следующий пример Hello создается политика открытой авторизации и добавляет его ключ содержимого toohello.</span><span class="sxs-lookup"><span data-stu-id="db93d-143">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="db93d-144"><a id="ContentKeyAuthorizationPolicies"></a>Создание ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="db93d-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="db93d-145">Запрос:</span><span class="sxs-lookup"><span data-stu-id="db93d-145">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423578086&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lZlyQ2%2bvH73qtJsb42%2fH3xF7r7EvQFR3UXyezuDENFU%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 36

    {"Name":"Open Authorization Policy"}

<span data-ttu-id="db93d-146">Ответ:</span><span class="sxs-lookup"><span data-stu-id="db93d-146">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 211
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Adb4593da-f4d1-4cc5-a92a-d20eacbabee4')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    x-ms-request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:25:56 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:db4593da-f4d1-4cc5-a92a-d20eacbabee4","Name":"Open Authorization Policy"}

#### <span data-ttu-id="db93d-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Создание ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="db93d-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="db93d-148">Запрос:</span><span class="sxs-lookup"><span data-stu-id="db93d-148">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 168

    {"Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="db93d-149">Ответ:</span><span class="sxs-lookup"><span data-stu-id="db93d-149">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 349
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    x-ms-request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:56:40 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:57829b17-1101-4797-919b-f816f4a007b7","Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

#### <span data-ttu-id="db93d-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Привязка ContentKeyAuthorizationPolicies к Options</span><span class="sxs-lookup"><span data-stu-id="db93d-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="db93d-151">Запрос:</span><span class="sxs-lookup"><span data-stu-id="db93d-151">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3A0baa438b-8ac2-4c40-a53c-4d4722b78715')/$links/Options HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9847f705-f2ca-4e95-a478-8f823dbbaa29
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 154

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')"}

<span data-ttu-id="db93d-152">Ответ:</span><span class="sxs-lookup"><span data-stu-id="db93d-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="db93d-153"><a id="AddAuthorizationPolicyToKey"></a>Добавить ключ содержимого toohello политики авторизации</span><span class="sxs-lookup"><span data-stu-id="db93d-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy toohello content key</span></span>
<span data-ttu-id="db93d-154">Запрос:</span><span class="sxs-lookup"><span data-stu-id="db93d-154">Request:</span></span>

    PUT https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A2e6d36a7-a17c-4e9a-830d-eca23ad1a6f9') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: e613efff-cb6a-41b4-984a-f4f8fb6e76a4
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 78

    {"AuthorizationPolicyId":"nb:ckpid:UUID:c06cebb8-c4f0-4d1a-ba00-3273fb2bc3ad"}

<span data-ttu-id="db93d-155">Ответ:</span><span class="sxs-lookup"><span data-stu-id="db93d-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="db93d-156">Ограничение "по маркеру"</span><span class="sxs-lookup"><span data-stu-id="db93d-156">Token Restriction</span></span>
<span data-ttu-id="db93d-157">В этом разделе описывается политика авторизации ключа и связать его с помощью ключа содержимого hello toocreate контента.</span><span class="sxs-lookup"><span data-stu-id="db93d-157">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="db93d-158">Политика авторизации Hello описывает, какие требования проверки подлинности должно быть toodetermine будут выполнены, если пользователь hello является авторизованным tooreceive hello ключ (например, список «ключ проверки» hello содержит ключ hello был подписан этот токен hello).</span><span class="sxs-lookup"><span data-stu-id="db93d-158">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="db93d-159">Параметр ограничения маркеров tooconfigure hello, необходимо toouse XML toodescribe hello токен требования к проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="db93d-159">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="db93d-160">Hello XML конфигурации ограничений токенов должен соответствовать toohello следующие XML-схемы.</span><span class="sxs-lookup"><span data-stu-id="db93d-160">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="db93d-161"><a id="schema"></a>Схема ограничения «по токену»</span><span class="sxs-lookup"><span data-stu-id="db93d-161"><a id="schema"></a>Token restriction schema</span></span>
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

<span data-ttu-id="db93d-162">При настройке hello **маркера** ограниченной политики, необходимо указать hello основной ** проверки ключ ** **издателя** и **аудитории** параметров.</span><span class="sxs-lookup"><span data-stu-id="db93d-162">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="db93d-163">Hello ** основной ключ проверки ** содержит ключ hello, hello токена был подписан, **издателя** является службой маркеров безопасности hello этот токен hello проблемы.</span><span class="sxs-lookup"><span data-stu-id="db93d-163">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="db93d-164">Hello **аудитории** (иногда называется **область**) описывает намерение hello токен hello или ресурса hello hello токен разрешает доступ.</span><span class="sxs-lookup"><span data-stu-id="db93d-164">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="db93d-165">Hello служба доставки ключей Media Services проверяет, эти значения в токене hello соответствуют значениям hello в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="db93d-165">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="db93d-166">Следующий пример Hello создает политику авторизации с ограничением токенов.</span><span class="sxs-lookup"><span data-stu-id="db93d-166">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="db93d-167">В этом примере hello клиент должен будет toopresent маркер, содержащий: подписывания ключа (VerificationKey), поставщика маркера и необходимых утверждений.</span><span class="sxs-lookup"><span data-stu-id="db93d-167">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="db93d-168">Создание ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="db93d-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="db93d-169">Создайте hello «Маркера политики ограниченного использования программ», как показано [здесь](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="db93d-169">Create hello "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="db93d-170">Создание ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="db93d-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="db93d-171">Запрос:</span><span class="sxs-lookup"><span data-stu-id="db93d-171">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580720&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5LsNu%2b0D4eD3UOP3BviTLDkUjaErdUx0ekJ8402xidQ%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1079

    {"Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="db93d-172">Ответ:</span><span class="sxs-lookup"><span data-stu-id="db93d-172">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1260
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae1ef6145-46e8-4ee6-9756-b1cf96328c23')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    x-ms-request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:10:37 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e1ef6145-46e8-4ee6-9756-b1cf96328c23","Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="db93d-173">Привязка ContentKeyAuthorizationPolicies к Options</span><span class="sxs-lookup"><span data-stu-id="db93d-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="db93d-174">Привяжите ContentKeyAuthorizationPolicies к Options, как показано [здесь](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="db93d-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="db93d-175">Добавить ключ содержимого toohello политики авторизации</span><span class="sxs-lookup"><span data-stu-id="db93d-175">Add authorization policy toohello content key</span></span>
<span data-ttu-id="db93d-176">Добавьте AuthorizationPolicy toohello ContentKey, как показано [здесь](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="db93d-176">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="db93d-177">Динамическое шифрование на основе PlayReady</span><span class="sxs-lookup"><span data-stu-id="db93d-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="db93d-178">Службы мультимедиа позволяют tooconfigure hello права и ограничения, что требуется для hello tooenforce среда выполнения PlayReady DRM при попытке пользователя tooplay контент, защищенный обратно.</span><span class="sxs-lookup"><span data-stu-id="db93d-178">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="db93d-179">При защите контента с помощью PlayReady, одно из действий hello необходимо toospecify в политике авторизации является XML-строку, определяющий hello [шаблон лицензии PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db93d-179">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="db93d-180">Ограничение "открытая"</span><span class="sxs-lookup"><span data-stu-id="db93d-180">Open Restriction</span></span>
<span data-ttu-id="db93d-181">Ограничение Open означает, что система hello будет предоставлять tooanyone ключа hello, выполняющий запрос ключа.</span><span class="sxs-lookup"><span data-stu-id="db93d-181">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="db93d-182">Это ограничение подходит для тестирования.</span><span class="sxs-lookup"><span data-stu-id="db93d-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="db93d-183">Следующий пример Hello создается политика открытой авторизации и добавляет его ключ содержимого toohello.</span><span class="sxs-lookup"><span data-stu-id="db93d-183">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="db93d-184"><a id="ContentKeyAuthorizationPolicies2"></a>Создание ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="db93d-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="db93d-185">Запрос:</span><span class="sxs-lookup"><span data-stu-id="db93d-185">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 58

    {"Name":"Deliver Common Content Key"}

<span data-ttu-id="db93d-186">Ответ:</span><span class="sxs-lookup"><span data-stu-id="db93d-186">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 233
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Acc3c64a8-e2fc-4e09-bf60-ac954251a387')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    x-ms-request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:26:00 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:cc3c64a8-e2fc-4e09-bf60-ac954251a387","Name":"Deliver Common Content Key"}


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="db93d-187">Создание ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="db93d-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="db93d-188">Запрос:</span><span class="sxs-lookup"><span data-stu-id="db93d-188">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 593

    {"Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="db93d-189">Ответ:</span><span class="sxs-lookup"><span data-stu-id="db93d-189">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 774
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A1052308c-4df7-4fdb-8d21-4d2141fc2be0')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    x-ms-request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:23:24 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:1052308c-4df7-4fdb-8d21-4d2141fc2be0","Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="db93d-190">Привязка ContentKeyAuthorizationPolicies к Options</span><span class="sxs-lookup"><span data-stu-id="db93d-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="db93d-191">Привяжите ContentKeyAuthorizationPolicies к Options, как показано [здесь](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="db93d-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="db93d-192">Добавить ключ содержимого toohello политики авторизации</span><span class="sxs-lookup"><span data-stu-id="db93d-192">Add authorization policy toohello content key</span></span>
<span data-ttu-id="db93d-193">Добавьте AuthorizationPolicy toohello ContentKey, как показано [здесь](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="db93d-193">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="db93d-194">Ограничение "по маркеру"</span><span class="sxs-lookup"><span data-stu-id="db93d-194">Token Restriction</span></span>
<span data-ttu-id="db93d-195">Параметр ограничения маркеров tooconfigure hello, необходимо toouse XML toodescribe hello токен требования к проверке подлинности.</span><span class="sxs-lookup"><span data-stu-id="db93d-195">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="db93d-196">Hello XML конфигурации ограничений токенов должен соответствовать toohello схемы XML, показанный на [это](#schema) раздела.</span><span class="sxs-lookup"><span data-stu-id="db93d-196">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="db93d-197">Создание ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="db93d-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="db93d-198">Создайте ContentKeyAuthorizationPolicies, как показано [здесь](#ContentKeyAuthorizationPolicies2).</span><span class="sxs-lookup"><span data-stu-id="db93d-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="db93d-199">Создание ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="db93d-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="db93d-200">Запрос:</span><span class="sxs-lookup"><span data-stu-id="db93d-200">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423583561&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5eZnkOsSv%2fLLEKmS%2bWObBlsNYyee8BQlp%2bUYbjugcJg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1525

    {"Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="db93d-201">Ответ:</span><span class="sxs-lookup"><span data-stu-id="db93d-201">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1706
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae42bbeae-de42-4077-90e9-a844f297ef70')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    x-ms-request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:58:47 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e42bbeae-de42-4077-90e9-a844f297ef70","Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="db93d-202">Привязка ContentKeyAuthorizationPolicies к Options</span><span class="sxs-lookup"><span data-stu-id="db93d-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="db93d-203">Привяжите ContentKeyAuthorizationPolicies к Options, как показано [здесь](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="db93d-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="db93d-204">Добавить ключ содержимого toohello политики авторизации</span><span class="sxs-lookup"><span data-stu-id="db93d-204">Add authorization policy toohello content key</span></span>
<span data-ttu-id="db93d-205">Добавьте AuthorizationPolicy toohello ContentKey, как показано [здесь](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="db93d-205">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="db93d-206"><a id="types"></a>Типы, используемые при определении ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="db93d-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="db93d-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="db93d-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="db93d-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="db93d-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="db93d-209">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="db93d-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="db93d-210">Отзывы</span><span class="sxs-lookup"><span data-stu-id="db93d-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="db93d-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="db93d-211">Next Steps</span></span>
<span data-ttu-id="db93d-212">Настройки политики авторизации ключа содержимого go toohello [как политики доставки активов tooconfigure](media-services-rest-configure-asset-delivery-policy.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="db93d-212">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

