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
# <a name="federation-metadata"></a>Метаданные федерации
Azure Active Directory (Azure AD) публикует документ метаданных федерации для служб, которые будет настроить маркеры безопасности tooaccept hello, выдаваемых Azure AD. Hello формат документа метаданных федерации описан в hello [язык федерации веб-служб (WS-Federation) версии 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), который расширяет [метаданные для hello OASIS Security Assertion Markup Language (SAML) версия 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a>Клиентские и общие конечные точки метаданных
Azure AD публикует клиентские и общие конечные точки.

Клиентские конечные точки предназначены только для одного конкретного клиента. метаданные федерации конкретного клиента Hello включают сведения о клиенте hello, включая издателя конкретного клиента и сведения о конечной точке. Приложения, которые ограничивают доступ tooa одного клиента используйте клиентозависимые конечные точки.

Клиентонезависимые конечные точки предоставляют сведения, общие клиентов tooall Azure AD. Эти сведения применимы, размещенного в tootenants *login.microsoftonline.com* и общими для всех клиентов. Мы рекомендуем использовать общие конечные точки для мультитенантных приложений, так как они не связаны с каким-либо определенным клиентом.

## <a name="federation-metadata-endpoints"></a>Конечные точки метаданных федерации
Azure AD публикует метаданные федерации по адресу `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.

Для **клиентозависимые конечные точки**, hello `TenantDomainName` может принимать одно из hello следующие типы:

* зарегистрированное доменное имя клиента Azure AD, например `contoso.onmicrosoft.com`;
* неизменяемый Hello клиента идентификатор hello домена, например `72f988bf-86f1-41af-91ab-2d7cd011db45`.

Для **клиентонезависимые конечные точки**, hello `TenantDomainName` — `common`. В этом документе перечислены только hello метаданных федерации элементы, общие клиентов tooall Azure AD, размещаются на login.microsoftonline.com.

Клиентская конечная точка может иметь такой адрес: `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`. является независимой от клиента конечной точке Hello [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml). Документ метаданных федерации hello можно просмотреть, введя этот URL-адрес в браузере.

## <a name="contents-of-federation-metadata"></a>Содержимое метаданных федерации
Hello следующий раздел содержит сведения, необходимые для службы, обрабатывающие маркеры hello, выданного Azure AD.

### <a name="entity-id"></a>Идентификатор сущности
Hello `EntityDescriptor` элемент содержит `EntityID` атрибута. Здравствуйте, значение hello `EntityID` атрибут представляет hello издателя, то есть hello маркеров безопасности (STS) службы маркера, выданного hello. Это важные toovalidate hello издателя при получении маркера.

Hello следующих метаданных показан пример определенного клиента `EntityDescriptor` элемент с `EntityID` элемента.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
Можно заменить hello ИД клиента в клиентонезависимой конечной точке hello toocreate идентификатор вашего клиента конкретного клиента `EntityID` значение. результирующее значение Hello будет иметь hello так же, как hello издателя маркера. Стратегия Hello позволяет издателя hello toovalidate многопользовательского приложения для данного клиента.

Hello следующих метаданных показан пример независимой от клиента `EntityID` элемента. Обратите внимание, что hello `{tenant}` — это литерал, а не заполнитель.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a>Сертификаты подписи токенов
Когда служба получает маркер, выданный клиентом Azure AD, hello подпись токена hello должны быть проверены с ключом подписывания, опубликованной в документе метаданных федерации hello. Hello метаданные федерации включают открытую часть hello hello сертификаты, которые hello клиенты используют для подписи токенов. необработанные байты сертификата Hello, присутствуют в hello `KeyDescriptor` элемента. сертификат для подписи маркера Hello является допустимым для только при подписи hello значение hello `use` атрибут `signing`.

Документ метаданных федерации, опубликованный Azure AD может иметь несколько ключей подписывания, например когда Azure AD готовится hello tooupdate сертификат для подписи. Если документ метаданных федерации содержит более одного сертификата, проверяющая токены hello службы должна поддерживать все сертификаты в документе hello.

Hello следующих метаданных показан пример `KeyDescriptor` элемент с ключом подписывания.

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

Hello `KeyDescriptor` элемент отображается в двух местах в документе метаданных федерации hello; WS-Federation определенного hello и hello SAML конкретных разделов. Hello сертификаты, опубликованные в обоих разделах будет hello же.

В разделе hello WS-Federation определенного чтения метаданных WS-Federation читает сертификаты hello из `RoleDescriptor` элемент с hello `SecurityTokenServiceType` типа.

Hello следующих метаданных показан пример `RoleDescriptor` элемента.

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

В разделе hello конкретного SAML чтения метаданных WS-Federation читает сертификаты hello из `IDPSSODescriptor` элемента.

Hello следующих метаданных показан пример `IDPSSODescriptor` элемента.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
Изменений нет в формате hello сертификатов конкретного клиента и независимой от клиента.

### <a name="ws-federation-endpoint-url"></a>URL-адрес конечной точки WS-Federation
Hello метаданные федерации включают hello, которое используется URL-адрес, Azure AD для единого входа и единого выхода в протоколе WS-Federation. Эта конечная точка отображается в hello `PassiveRequestorEndpoint` элемента.

Hello следующих метаданных показан пример `PassiveRequestorEndpoint` элемент для клиентозависимой конечной точки.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
Для клиентонезависимой конечной точке hello hello WS-Federation URL-адрес отображается в конечной точке hello WS-Federation, как показано в следующих образец hello.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a>URL-адрес конечной точки протокола SAML
Hello метаданные федерации включают hello URL-адрес, используемый Azure AD для единого входа и единого выхода в протоколе SAML 2.0. Эти конечные точки отображаются в hello `IDPSSODescriptor` элемента.

Hello входа и выхода, URL-адреса отображаются в hello `SingleSignOnService` и `SingleLogoutService` элементы.

Hello следующих метаданных показан пример `PassiveResistorEndpoint` для клиентозависимой конечной точки.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

Аналогичным образом hello конечных точек для конечных точек протокола hello общих SAML 2.0 публикуются в метаданных федерации независимой от клиента hello, как показано в следующих образец hello.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
