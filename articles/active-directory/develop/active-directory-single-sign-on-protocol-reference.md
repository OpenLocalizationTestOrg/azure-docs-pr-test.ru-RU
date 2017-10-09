---
title: "aaaAzure единого входа в протокол SAML | Документы Microsoft"
description: "В этой статье описывается протокол hello единого входа в SAML в Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Протокол единого входа SAML
В этой статье рассматриваются hello SAML 2.0 проверки подлинности запросов и ответов, которые поддерживает Azure Active Directory (Azure AD) для единого входа.

Схема протокола Hello ниже описывает hello единого входа для последовательности. Hello облачная служба (поставщик службы hello) использует привязку перенаправления HTTP toopass `AuthnRequest` tooAzure (запрос аутентификации) элемент AD (hello поставщика удостоверений). Затем Azure AD использует toopost привязку HTTP post `Response` элемент toohello облачной службы.

![Рабочий процесс единого входа](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
Отправить toorequest проверки подлинности пользователя, облачные службы `AuthnRequest` tooAzure элемент AD. Пример `AuthnRequest` SAML 2.0 может выглядеть так:

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| Параметр |  | Описание |
| --- | --- | --- |
| ИД |обязательно |Azure AD использует этот атрибут toopopulate hello `InResponseTo` атрибут hello отклик. Идентификатор не должно начинаться с цифры, поэтому распространенная стратегия tooprepend строки like «id» toohello строковое представление идентификатора GUID. Например, `id6c1c178c166d486687be4aaf5e482730` — допустимый идентификатор. |
| Версия |обязательно |Должна быть версия **2.0**. |
| IssueInstant |обязательно |Это строка DateTime со значением в формате всемирного времени (UTC) и с [преобразованием без потери данных ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD требует значения DateTime этого типа, но не оценки или используйте значение hello. |
| AssertionConsumerServiceUrl |необязательный |Если указано, оно должно совпадать hello `RedirectUri` hello облачной службы в Azure AD. |
| ForceAuthn |необязательный | Это логическое значение. Если значение равно true, это означает, этот пользователь hello принудительного toore-проверки подлинности, даже если они имеют действительный сеанс с Azure AD. |
| IsPassive |необязательный |Это значение типа boolean, указывает ли Azure AD должен пройти проверку подлинности пользователя hello автоматически, без вмешательства пользователя, с помощью файла cookie сеанса hello, если он существует. Если это так, Azure AD выполнит попытку tooauthenticate hello пользователя, с помощью файла cookie сеанса hello. |

Все остальные атрибуты `AuthnRequest` , включая Consent, Destination, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex и ProviderName, **игнорируются**.

Azure AD также игнорирует hello `Conditions` элемент в `AuthnRequest`.

### Издатель
Hello `Issuer` элемент в `AuthnRequest` должен точно соответствовать одному из hello **ServicePrincipalNames** в облачной службе hello в Azure AD. Как правило, устанавливается toohello **URI идентификатора приложения** , указанным во время регистрации приложения.

Образец отрывок кода SAML, содержащий hello `Issuer` элемент выглядит следующим образом:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
Этот элемент запрашивает определенного формата ИД имени в ответ hello и является необязательным в `AuthnRequest` tooAzure элементы, передаваемые AD.

Пример элемента `NameIdPolicy` выглядит так:

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

Если элемент `NameIDPolicy` указан, можно включить его необязательный атрибут `Format`. Hello `Format` атрибут может иметь только одно из последующих значений hello; любого другого значения приведет к ошибке.

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Azure Active Directory выдает утверждение hello NameID как парный идентификатор.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Azure Active Directory выдает утверждение NameID hello в формате адреса электронной почты.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: Это значение позволяет Azure Active Directory tooselect hello утверждения формата. Azure Active Directory выдает hello NameID как парный идентификатор.
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Azure Active Directory выдает утверждение NameID hello как значение формируется случайным образом, которое является уникальным toohello текущей операции единого входа. Это означает, что значение hello является временным и не может быть hello используется tooidentify проверки подлинности пользователя.

Azure AD не учитывает hello `AllowCreate` атрибута.

### RequestAuthnContext
Hello `RequestedAuthnContext` элемент указывает hello требуемого методы проверки подлинности. Он является необязательным в `AuthnRequest` tooAzure элементы, передаваемые AD. Azure AD поддерживает только одно значение `AuthnContextClassRef` — `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.

### Scoping
Hello `Scoping` элемент, который содержит список поставщиков удостоверений, является необязательным в `AuthnRequest` tooAzure элементы, передаваемые AD.

Если указано, не включайте hello `ProxyCount` атрибута `IDPListOption` или `RequesterID` элемент, как они не поддерживаются.

### Подпись
Не включайте элемент `Signature` в элементы `AuthnRequest`, так как Azure AD не поддерживает подписанные запросы проверки подлинности.

### Субъект
Azure AD не учитывает hello `Subject` элемент `AuthnRequest` элементов.

## Ответ
По завершении запрошенного единого входа Azure AD отправляет ответ toohello облачной службы. Образец ответа tooa входа успешного выглядит следующим образом:

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### Ответ
Hello `Response` элемент включает в себя hello результат запроса авторизации hello. Azure AD присваивает Привет `ID`, `Version` и `IssueInstant` значения в hello `Response` элемента. Кроме того, задается hello следующие атрибуты:

* `Destination`: При вход выполняется успешно, он задается toohello `RedirectUri` hello поставщика услуг (облачная служба).
* `InResponseTo`: Это свойство принимает значение toohello `ID` атрибут hello `AuthnRequest` , инициировавшего ответ hello.

### Издатель
Azure AD присваивает Привет `Issuer` элемент слишком`https://login.microsoftonline.com/<TenantIDGUID>/` где <TenantIDGUID> является hello идентификатор клиента hello Azure AD.

Пример ответа с элементом Issuer может выглядеть, к примеру, следующим образом:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### Состояние
Hello `Status` hello успешного или неуспешного входа содержимое элемента. Он включает hello `StatusCode` элемент, который содержит код или набор вложенных кодов, которые представляют Привет состояние запроса hello. Он также включает hello `StatusMessage` элемент, содержащий пользовательские сообщения об ошибках, сформированные в процессе входа hello.

<!-- TODO: Add a authentication protocol error reference -->

Hello Приведем SAML ответа tooan неудачных попытку входа.

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### Assertion
В дополнение toohello `ID`, `IssueInstant` и `Version`, Azure AD присваивает Привет, следующие элементы в hello `Assertion` элемент ответа hello.

#### Издатель
Задано слишком`https://sts.windows.net/<TenantIDGUID>/`где <TenantIDGUID> — hello ИД клиента службы hello Azure AD.

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### Подпись
Azure AD подписывает утверждение hello в ответ tooa успешный вход. Hello `Signature` элемент содержит цифровую подпись, hello облачной службы можно использовать целостность tooauthenticate hello источника tooverify hello hello утверждения.

Здравствуйте, toogenerate этой цифровой подписи Azure AD использует ключ подписывания в hello `IDPSSODescriptor` элемент документа метаданных.

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### Субъект
Указывает участника hello, является предметом hello hello операторов в утверждении hello. Он содержит `NameID` элемент, который представляет пользователя, прошедшего проверку подлинности hello. Hello `NameID` значение — целевой идентификатор, который является поставщиком службы направленной только toohello, hello аудитории для токена hello. Оно носит постоянный характер. Это значение можно отменить, но нельзя переназначить. Он также является непрозрачной и, поскольку она не раскрывает никаких сведений о пользователя hello и не может использоваться в качестве идентификатора для запросов атрибута.

Hello `Method` атрибут hello `SubjectConfirmation` элемент всегда имеет слишком`urn:oasis:names:tc:SAML:2.0:cm:bearer`.

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### Условия
Этот элемент задает условия, определяющие допустимые hello использование утверждений SAML.

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

Hello `NotBefore` и `NotOnOrAfter` атрибуты указывают интервал приветствия, во время которого hello утверждение недопустимо.

* Здравствуйте, значение hello `NotBefore` атрибут является равно tooor немного (менее секунды) позже, чем значение hello `IssueInstant` атрибут hello `Assertion` элемента. Azure AD не учитывает любые временные различия между собой и hello облачной службе (поставщике услуг) и не добавляются в любое время toothis буфера.
* Здравствуйте, значение hello `NotOnOrAfter` атрибут является более поздней, чем значение hello hello 70 минут `NotBefore` атрибута.

#### Аудитория
Он содержит код URI, который определяет предполагаемую аудиторию. Azure AD задает hello значение этого элемента toohello значение `Issuer` элемент hello `AuthnRequest` , инициировавшего вход hello. tooevaluate hello `Audience` , используйте значение hello hello `App ID URI` , указанный во время регистрации приложения.

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

Как hello `Issuer` значение hello `Audience` значение должно точно соответствовать одному из приветствия имен участников-служб, представляющих hello облачной службы в Azure AD. Однако если hello значение из hello `Issuer` элемент не является значением URI hello `Audience` значение в ответ hello — hello `Issuer` с префиксом `spn:`.

#### AttributeStatement
Содержит утверждения о hello субъекте или пользователе. Hello следующий фрагмент содержит образец `AttributeStatement` элемента. многоточие Hello указывает, что этот элемент hello может включать несколько атрибутов и значений атрибутов.

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **Имя утверждения** : hello значение hello `Name` атрибут (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) — hello имя участника-пользователя hello проверку подлинности пользователя, таких как `testuser@managedtenant.com`.
* **Утверждение ObjectIdentifier** : hello значение hello `ObjectIdentifier` атрибут (`http://schemas.microsoft.com/identity/claims/objectidentifier`) — hello `ObjectId` hello объекта каталога, представляющий hello проверку подлинности пользователя в Azure AD. `ObjectId`является неизменяемым, глобально уникальным, и повторно использовать безопасный идентификатор hello проверку подлинности пользователя.

#### AuthnStatement
Этот элемент подтверждает, что субъект утверждения hello выполнена определенным средством на определенный момент времени.

* Hello `AuthnInstant` атрибут задает время hello пользовательских hello проверку подлинности с помощью Azure AD.
* Hello `AuthnContext` элемент указывает, использовать контекст проверки подлинности hello tooauthenticate hello пользователя.

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```