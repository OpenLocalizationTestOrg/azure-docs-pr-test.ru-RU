---
title: "aaaAzure единого входа Out протокола SAML | Документы Microsoft"
description: "В этой статье описывается hello одного протокола выхода SAML в Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Протокол единого выхода SAML
Azure hello поддерживает Active Directory (Azure AD), SAML 2.0 веб-браузера единого выхода профиль. Правильно, один выход toowork hello **LogoutURL** для приложения hello должны быть явно зарегистрированы в Azure AD во время регистрации приложения. Azure AD использует hello LogoutURL tooredirect пользователей после выхода.

Эта диаграмма показывает рабочий процесс hello hello Azure AD едином процессе выхода.

![Рабочий процесс единого выхода](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
Здравствуйте, облачная служба отправляет `LogoutRequest` tooindicate tooAzure AD сообщение, что сеанс завершен. Hello следующем фрагменте кода показан пример `LogoutRequest` элемента.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
Hello `LogoutRequest` tooAzure, отправленный AD требует hello следующие атрибуты:

* `ID`: Это идентифицирует запрос выхода hello. Здравствуйте, значение `ID` не должно начинаться с цифры. Hello обычной практикой является tooappend **идентификатор** toohello строковое представление идентификатора GUID.
* `Version`: Значение hello этого элемента слишком**2.0**. Это обязательное значение.
* `IssueInstant`: это строка `DateTime` со значением в формате всемирного времени (UTC) и с [преобразованием без потери данных ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD ожидает значение такого типа, но не требует его наличия.

### Издатель
Hello `Issuer` элемент в `LogoutRequest` должен точно соответствовать одному из hello **ServicePrincipalNames** в облачной службе hello в Azure AD. Как правило, устанавливается toohello **URI идентификатора приложения** , указанным во время регистрации приложения.

### NameID
Здравствуйте, значение hello `NameID` должно полностью совпадать с hello `NameID` hello пользователя, выполняющего выход.

## LogoutResponse
Azure AD отправляет `LogoutResponse` в ответ tooa `LogoutRequest` элемента. Hello следующем фрагменте кода показан пример `LogoutResponse`.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
Azure AD присваивает Привет `ID`, `Version` и `IssueInstant` значения в hello `LogoutResponse` элемента. Этот параметр также устанавливает hello `InResponseTo` toohello имеет значение hello `ID` атрибут hello `LogoutRequest` , вызвавшего hello ответа.

### Издатель
Azure AD присваивает этому параметру значение слишком`https://login.microsoftonline.com/<TenantIdGUID>/` где <TenantIdGUID> является hello идентификатор клиента hello Azure AD.

значение hello tooevaluate hello `Issuer` элемент, используйте значение hello hello **URI идентификатора приложения** предоставленного во время регистрации приложения.

### Состояние
Azure AD использует hello `StatusCode` элемент в hello `Status` элемент tooindicate hello успешности выхода. Когда hello неудачного выхода из системы, hello `StatusCode` элемент также может содержать пользовательские сообщения об ошибках.
