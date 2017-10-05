---
title: "Метаданные федерации Azure AD | Документация Майкрософт"
description: "В этой статье описывается документ метаданных федерации, который Azure Active Directory публикует для каждой службы, принимающей токены Azure Active Directory."
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
ms.openlocfilehash: ecafb02a6ac13d1c3cd1fe77ef710cd8525e32b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="cb32d-103">Метаданные федерации</span><span class="sxs-lookup"><span data-stu-id="cb32d-103">Federation metadata</span></span>
<span data-ttu-id="cb32d-104">Azure Active Directory (Azure AD) публикует документ метаданных федерации для служб, который настроен на прием маркеров безопасности, выдаваемых Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb32d-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured to accept the security tokens that Azure AD issues.</span></span> <span data-ttu-id="cb32d-105">Формат документа метаданных федерации описан в стандарте [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) (язык федерации веб-служб (WS-Federation) версии 1.2), который является расширением стандарта [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf) (метаданные для языка разметки заявлений системы безопасности (SAML) OASIS версии 2.0).</span><span class="sxs-lookup"><span data-stu-id="cb32d-105">The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="cb32d-106">Клиентские и общие конечные точки метаданных</span><span class="sxs-lookup"><span data-stu-id="cb32d-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="cb32d-107">Azure AD публикует клиентские и общие конечные точки.</span><span class="sxs-lookup"><span data-stu-id="cb32d-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="cb32d-108">Клиентские конечные точки предназначены только для одного конкретного клиента.</span><span class="sxs-lookup"><span data-stu-id="cb32d-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="cb32d-109">Клиентские метаданные федерации содержат сведения о конкретном клиенте, в том числе данные о его издателе и конечной точке.</span><span class="sxs-lookup"><span data-stu-id="cb32d-109">The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="cb32d-110">Приложения, которые предлагают доступ только к одному клиенту, используют клиентские конечные точки.</span><span class="sxs-lookup"><span data-stu-id="cb32d-110">Applications that restrict access to a single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="cb32d-111">Общие конечные точки предоставляют сведения, общие для всех клиентов Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb32d-111">Tenant-independent endpoints provide information that is common to all Azure AD tenants.</span></span> <span data-ttu-id="cb32d-112">Эти сведения относятся к клиентам, которые размещены в домене *login.microsoftonline.com* , и данные одинаковы для всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="cb32d-112">This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="cb32d-113">Мы рекомендуем использовать общие конечные точки для мультитенантных приложений, так как они не связаны с каким-либо определенным клиентом.</span><span class="sxs-lookup"><span data-stu-id="cb32d-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="cb32d-114">Конечные точки метаданных федерации</span><span class="sxs-lookup"><span data-stu-id="cb32d-114">Federation metadata endpoints</span></span>
<span data-ttu-id="cb32d-115">Azure AD публикует метаданные федерации по адресу `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="cb32d-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="cb32d-116">Для **клиентских конечных точек** `TenantDomainName` может быть одного из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="cb32d-116">For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:</span></span>

* <span data-ttu-id="cb32d-117">зарегистрированное доменное имя клиента Azure AD, например `contoso.onmicrosoft.com`;</span><span class="sxs-lookup"><span data-stu-id="cb32d-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="cb32d-118">неизменяемый идентификатор клиента для домена, например `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="cb32d-118">The immutable tenant ID of the domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="cb32d-119">Для **общих конечных точек** `TenantDomainName` является `common`.</span><span class="sxs-lookup"><span data-stu-id="cb32d-119">For **tenant-independent endpoints**, the `TenantDomainName` is `common`.</span></span> <span data-ttu-id="cb32d-120">В этом документе перечислены только те элементы метаданных федерации, которые являются общими для всех клиентов Azure AD, размещенных на login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="cb32d-120">This document lists only the Federation Metadata elements that are common to all Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="cb32d-121">Клиентская конечная точка может иметь такой адрес: `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="cb32d-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="cb32d-122">Общая конечная точка имеет адрес [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="cb32d-122">The tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="cb32d-123">Документ метаданных федерации можно просмотреть, введя этот URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="cb32d-123">You can view the federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="cb32d-124">Содержимое метаданных федерации</span><span class="sxs-lookup"><span data-stu-id="cb32d-124">Contents of federation Metadata</span></span>
<span data-ttu-id="cb32d-125">В следующем разделе приведены сведения, необходимые для служб, которые используют токены, выданные службой Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb32d-125">The following section provides information needed by services that consume the tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="cb32d-126">Идентификатор сущности</span><span class="sxs-lookup"><span data-stu-id="cb32d-126">Entity ID</span></span>
<span data-ttu-id="cb32d-127">Элемент `EntityDescriptor` содержит атрибут `EntityID`.</span><span class="sxs-lookup"><span data-stu-id="cb32d-127">The `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="cb32d-128">Значение атрибута `EntityID` представляет издателя, то есть службу токенов безопасности, которая выдала этот токен.</span><span class="sxs-lookup"><span data-stu-id="cb32d-128">The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token.</span></span> <span data-ttu-id="cb32d-129">Очень важно проверить издателя при получении токена.</span><span class="sxs-lookup"><span data-stu-id="cb32d-129">It is important to validate the issuer when you receive a token.</span></span>

<span data-ttu-id="cb32d-130">В следующих метаданных показан пример клиентского элемента `EntityDescriptor` с элементом `EntityID`.</span><span class="sxs-lookup"><span data-stu-id="cb32d-130">The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="cb32d-131">Чтобы получить клиентское значение `EntityID` , замените в общей конечной точке стандартный идентификатор клиента своим собственным идентификатором клиента.</span><span class="sxs-lookup"><span data-stu-id="cb32d-131">You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="cb32d-132">Полученное значение будет совпадать со значением издателя токена.</span><span class="sxs-lookup"><span data-stu-id="cb32d-132">The resulting value will be the same as the token issuer.</span></span> <span data-ttu-id="cb32d-133">Такая стратегия позволяет мультитенантному приложению проверять издателя для конкретного клиента.</span><span class="sxs-lookup"><span data-stu-id="cb32d-133">The strategy allows a multi-tenant application to validate the issuer for a given tenant.</span></span>

<span data-ttu-id="cb32d-134">В следующих метаданных приведен пример общего элемента `EntityID` .</span><span class="sxs-lookup"><span data-stu-id="cb32d-134">The following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="cb32d-135">Обратите внимание, что `{tenant}` здесь является литералом, а не заполнителем.</span><span class="sxs-lookup"><span data-stu-id="cb32d-135">Please note, that the `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="cb32d-136">Сертификаты подписи токенов</span><span class="sxs-lookup"><span data-stu-id="cb32d-136">Token signing certificates</span></span>
<span data-ttu-id="cb32d-137">Когда служба получает токен, выданный клиентом Azure AD, подпись токена нужно проверить с помощью ключа подписывания, опубликованного в документе метаданных федерации.</span><span class="sxs-lookup"><span data-stu-id="cb32d-137">When a service receives a token that is issued by a Azure AD tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document.</span></span> <span data-ttu-id="cb32d-138">В метаданных федерации содержатся открытые ключи сертификатов, которые используются клиентами для подписывания токенов.</span><span class="sxs-lookup"><span data-stu-id="cb32d-138">The federation metadata includes the public portion of the certificates that the tenants use for token signing.</span></span> <span data-ttu-id="cb32d-139">Код сертификата отображается в элементе `KeyDescriptor` .</span><span class="sxs-lookup"><span data-stu-id="cb32d-139">The certificate raw bytes appear in the `KeyDescriptor` element.</span></span> <span data-ttu-id="cb32d-140">Сертификат для подписи маркера можно использовать, только если атрибут `use` имеет значение `signing`.</span><span class="sxs-lookup"><span data-stu-id="cb32d-140">The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.</span></span>

<span data-ttu-id="cb32d-141">Документ метаданных федерации, опубликованный службой Azure AD, может иметь несколько ключей подписывания, к примеру, когда Azure AD готовится к обновлению сертификата для подписывания.</span><span class="sxs-lookup"><span data-stu-id="cb32d-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing to update the signing certificate.</span></span> <span data-ttu-id="cb32d-142">Если документ метаданных федерации содержит более одного сертификата, служба, проверяющая токены, должна поддерживать все сертификаты в документе.</span><span class="sxs-lookup"><span data-stu-id="cb32d-142">When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.</span></span>

<span data-ttu-id="cb32d-143">В следующих метаданных приведен пример элемента `KeyDescriptor` с ключом подписывания.</span><span class="sxs-lookup"><span data-stu-id="cb32d-143">The following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="cb32d-144">Элемент `KeyDescriptor` отображается в двух местах в документе метаданных федерации: в разделах WS-Federation и SAML.</span><span class="sxs-lookup"><span data-stu-id="cb32d-144">The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section.</span></span> <span data-ttu-id="cb32d-145">Сертификаты, опубликованные в обоих разделах, будут одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="cb32d-145">The certificates published in both sections will be the same.</span></span>

<span data-ttu-id="cb32d-146">В разделе WS-Federation средство чтения метаданных WS-Federation будет считывать сертификаты из элемента `RoleDescriptor` с типом `SecurityTokenServiceType`.</span><span class="sxs-lookup"><span data-stu-id="cb32d-146">In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="cb32d-147">В следующих метаданных приведен пример элемента `RoleDescriptor` .</span><span class="sxs-lookup"><span data-stu-id="cb32d-147">The following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="cb32d-148">В разделе SAML средство чтения метаданных WS-Federation будет читать сертификаты из элемента `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="cb32d-148">In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="cb32d-149">В следующих метаданных приведен пример элемента `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="cb32d-149">The following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="cb32d-150">Форматы клиентских и общих сертификатов не отличаются.</span><span class="sxs-lookup"><span data-stu-id="cb32d-150">There are no differences in the format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="cb32d-151">URL-адрес конечной точки WS-Federation</span><span class="sxs-lookup"><span data-stu-id="cb32d-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="cb32d-152">Метаданные федерации включают URL-адрес, используемый службой Azure AD для единого входа и единого выхода в протоколе WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="cb32d-152">The federation metadata includes the URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="cb32d-153">Эта конечная точка отображается в элементе `PassiveRequestorEndpoint` .</span><span class="sxs-lookup"><span data-stu-id="cb32d-153">This endpoint appears in the `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="cb32d-154">В следующих метаданных приведен пример элемента `PassiveRequestorEndpoint` для клиентской конечной точки.</span><span class="sxs-lookup"><span data-stu-id="cb32d-154">The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="cb32d-155">Для общей конечной точки URL-адрес WS-Federation отображается в конечной точке WS-Federation, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="cb32d-155">For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="cb32d-156">URL-адрес конечной точки протокола SAML</span><span class="sxs-lookup"><span data-stu-id="cb32d-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="cb32d-157">Метаданные федерации содержат URL-адрес, используемый службой Azure AD для единого входа и единого выхода в протоколе SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="cb32d-157">The federation metadata includes the URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="cb32d-158">Эти конечные точки отображаются в элементе `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="cb32d-158">These endpoints appear in the `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="cb32d-159">URL-адреса для входа и выхода содержатся в элементах `SingleSignOnService` и `SingleLogoutService`.</span><span class="sxs-lookup"><span data-stu-id="cb32d-159">The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="cb32d-160">В следующих метаданных приведен пример элемента `PassiveResistorEndpoint` для клиентской конечной точки.</span><span class="sxs-lookup"><span data-stu-id="cb32d-160">The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="cb32d-161">Так же конечные точки для общих конечных точек протокола SAML 2.0 публикуются в общих метаданных федерации, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="cb32d-161">Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
