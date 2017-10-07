---
title: "aaaAzure AD метаданных федерации | Документы Microsoft"
description: "В этой статье описываются hello документа метаданных федерации, публикуемых Azure Active Directory для служб, которые принимают токены Azure Active Directory."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="9bc5a-103">Метаданные федерации</span><span class="sxs-lookup"><span data-stu-id="9bc5a-103">Federation metadata</span></span>
<span data-ttu-id="9bc5a-104">Azure Active Directory (Azure AD) публикует документ метаданных федерации для служб, которые будет настроить маркеры безопасности tooaccept hello, выдаваемых Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="9bc5a-105">Hello формат документа метаданных федерации описан в hello [язык федерации веб-служб (WS-Federation) версии 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), который расширяет [метаданные для hello OASIS Security Assertion Markup Language (SAML) версия 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="9bc5a-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="9bc5a-106">Клиентские и общие конечные точки метаданных</span><span class="sxs-lookup"><span data-stu-id="9bc5a-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="9bc5a-107">Azure AD публикует клиентские и общие конечные точки.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="9bc5a-108">Клиентские конечные точки предназначены только для одного конкретного клиента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="9bc5a-109">метаданные федерации конкретного клиента Hello включают сведения о клиенте hello, включая издателя конкретного клиента и сведения о конечной точке.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="9bc5a-110">Приложения, которые ограничивают доступ tooa одного клиента используйте клиентозависимые конечные точки.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="9bc5a-111">Клиентонезависимые конечные точки предоставляют сведения, общие клиентов tooall Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="9bc5a-112">Эти сведения применимы, размещенного в tootenants *login.microsoftonline.com* и общими для всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="9bc5a-113">Мы рекомендуем использовать общие конечные точки для мультитенантных приложений, так как они не связаны с каким-либо определенным клиентом.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="9bc5a-114">Конечные точки метаданных федерации</span><span class="sxs-lookup"><span data-stu-id="9bc5a-114">Federation metadata endpoints</span></span>
<span data-ttu-id="9bc5a-115">Azure AD публикует метаданные федерации по адресу `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="9bc5a-116">Для **клиентозависимые конечные точки**, hello `TenantDomainName` может принимать одно из hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="9bc5a-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="9bc5a-117">зарегистрированное доменное имя клиента Azure AD, например `contoso.onmicrosoft.com`;</span><span class="sxs-lookup"><span data-stu-id="9bc5a-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="9bc5a-118">неизменяемый Hello клиента идентификатор hello домена, например `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="9bc5a-119">Для **клиентонезависимые конечные точки**, hello `TenantDomainName` — `common`.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="9bc5a-120">В этом документе перечислены только hello метаданных федерации элементы, общие клиентов tooall Azure AD, размещаются на login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="9bc5a-121">Клиентская конечная точка может иметь такой адрес: `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="9bc5a-122">является независимой от клиента конечной точке Hello [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="9bc5a-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="9bc5a-123">Документ метаданных федерации hello можно просмотреть, введя этот URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="9bc5a-124">Содержимое метаданных федерации</span><span class="sxs-lookup"><span data-stu-id="9bc5a-124">Contents of federation Metadata</span></span>
<span data-ttu-id="9bc5a-125">Hello следующий раздел содержит сведения, необходимые для службы, обрабатывающие маркеры hello, выданного Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="9bc5a-126">Идентификатор сущности</span><span class="sxs-lookup"><span data-stu-id="9bc5a-126">Entity ID</span></span>
<span data-ttu-id="9bc5a-127">Hello `EntityDescriptor` элемент содержит `EntityID` атрибута.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="9bc5a-128">Здравствуйте, значение hello `EntityID` атрибут представляет hello издателя, то есть hello маркеров безопасности (STS) службы маркера, выданного hello.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="9bc5a-129">Это важные toovalidate hello издателя при получении маркера.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="9bc5a-130">Hello следующих метаданных показан пример определенного клиента `EntityDescriptor` элемент с `EntityID` элемента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="9bc5a-131">Можно заменить hello ИД клиента в клиентонезависимой конечной точке hello toocreate идентификатор вашего клиента конкретного клиента `EntityID` значение.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="9bc5a-132">результирующее значение Hello будет иметь hello так же, как hello издателя маркера.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="9bc5a-133">Стратегия Hello позволяет издателя hello toovalidate многопользовательского приложения для данного клиента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="9bc5a-134">Hello следующих метаданных показан пример независимой от клиента `EntityID` элемента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="9bc5a-135">Обратите внимание, что hello `{tenant}` — это литерал, а не заполнитель.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="9bc5a-136">Сертификаты подписи токенов</span><span class="sxs-lookup"><span data-stu-id="9bc5a-136">Token signing certificates</span></span>
<span data-ttu-id="9bc5a-137">Когда служба получает маркер, выданный клиентом Azure AD, hello подпись токена hello должны быть проверены с ключом подписывания, опубликованной в документе метаданных федерации hello.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="9bc5a-138">Hello метаданные федерации включают открытую часть hello hello сертификаты, которые hello клиенты используют для подписи токенов.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="9bc5a-139">необработанные байты сертификата Hello, присутствуют в hello `KeyDescriptor` элемента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="9bc5a-140">сертификат для подписи маркера Hello является допустимым для только при подписи hello значение hello `use` атрибут `signing`.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="9bc5a-141">Документ метаданных федерации, опубликованный Azure AD может иметь несколько ключей подписывания, например когда Azure AD готовится hello tooupdate сертификат для подписи.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="9bc5a-142">Если документ метаданных федерации содержит более одного сертификата, проверяющая токены hello службы должна поддерживать все сертификаты в документе hello.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="9bc5a-143">Hello следующих метаданных показан пример `KeyDescriptor` элемент с ключом подписывания.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

<span data-ttu-id="9bc5a-144">Hello `KeyDescriptor` элемент отображается в двух местах в документе метаданных федерации hello; WS-Federation определенного hello и hello SAML конкретных разделов.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="9bc5a-145">Hello сертификаты, опубликованные в обоих разделах будет hello же.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="9bc5a-146">В разделе hello WS-Federation определенного чтения метаданных WS-Federation читает сертификаты hello из `RoleDescriptor` элемент с hello `SecurityTokenServiceType` типа.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="9bc5a-147">Hello следующих метаданных показан пример `RoleDescriptor` элемента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="9bc5a-148">В разделе hello конкретного SAML чтения метаданных WS-Federation читает сертификаты hello из `IDPSSODescriptor` элемента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="9bc5a-149">Hello следующих метаданных показан пример `IDPSSODescriptor` элемента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="9bc5a-150">Изменений нет в формате hello сертификатов конкретного клиента и независимой от клиента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="9bc5a-151">URL-адрес конечной точки WS-Federation</span><span class="sxs-lookup"><span data-stu-id="9bc5a-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="9bc5a-152">Hello метаданные федерации включают hello, которое используется URL-адрес, Azure AD для единого входа и единого выхода в протоколе WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="9bc5a-153">Эта конечная точка отображается в hello `PassiveRequestorEndpoint` элемента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="9bc5a-154">Hello следующих метаданных показан пример `PassiveRequestorEndpoint` элемент для клиентозависимой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="9bc5a-155">Для клиентонезависимой конечной точке hello hello WS-Federation URL-адрес отображается в конечной точке hello WS-Federation, как показано в следующих образец hello.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="9bc5a-156">URL-адрес конечной точки протокола SAML</span><span class="sxs-lookup"><span data-stu-id="9bc5a-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="9bc5a-157">Hello метаданные федерации включают hello URL-адрес, используемый Azure AD для единого входа и единого выхода в протоколе SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="9bc5a-158">Эти конечные точки отображаются в hello `IDPSSODescriptor` элемента.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="9bc5a-159">Hello входа и выхода, URL-адреса отображаются в hello `SingleSignOnService` и `SingleLogoutService` элементы.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="9bc5a-160">Hello следующих метаданных показан пример `PassiveResistorEndpoint` для клиентозависимой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="9bc5a-161">Аналогичным образом hello конечных точек для конечных точек протокола hello общих SAML 2.0 публикуются в метаданных федерации независимой от клиента hello, как показано в следующих образец hello.</span><span class="sxs-lookup"><span data-stu-id="9bc5a-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
