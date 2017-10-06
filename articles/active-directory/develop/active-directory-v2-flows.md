---
title: "типы aaaApp для конечной v2.0 hello Azure Active Directory | Документы Microsoft"
description: "Hello типы приложений и сценарии, поддерживаемые hello Azure Active Directory версии 2.0 конечной точкой."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a>Типы приложений для конечной v2.0 hello Azure Active Directory
Hello конечной точки Azure Active Directory (Azure AD) версии 2.0 поддерживает проверку подлинности для различных архитектур современных приложений, все из них на основе стандартных протоколов [OAuth 2.0 и OpenID Connect](active-directory-v2-protocols.md). Эта статья описывает hello типы приложений, которые можно создавать с помощью версии 2.0 Azure AD, независимо от выбранного языка и платформы. Hello сведения в этой статье — спроектированный toohelp понять сценариев высокого уровня, прежде чем [начала работы с кодом hello](active-directory-appmodel-v2-overview.md#getting-started).

> [!NOTE]
> Конечная точка v2.0 Hello не поддерживает все сценарии Azure Active Directory и возможности. toodetermine необходимость использования конечной точки v2.0 hello, узнайте, как [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="hello-basics"></a>Основы Hello
Необходимо зарегистрировать каждый приложение, которое использует конечную точку v2.0 hello в hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com). процесс регистрации приложения Hello собирает и назначает эти значения для приложения:

* **идентификатор приложения**, который определяет конкретное приложение;
* Объект **URI перенаправления** , которые можно использовать приложение назад tooyour toodirect ответов
* несколько других зависящих от сценария значений.

Дополнительные сведения, узнайте, как слишком[Регистрация приложения](active-directory-v2-app-registration.md).

После регистрации приложения hello приложение hello взаимодействует с Azure AD, отправляя запросы toohello Azure AD версии 2.0, конечной точки. Мы предоставляем с открытым исходным кодом платформы и библиотеки, которые обрабатывают сведения о hello этих запросов. Также имеется параметр tooimplement hello hello-логики проверки подлинности самостоятельно, создав запросы toothese конечные точки:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a>веб-приложений:
Для веб-приложения (.NET, PHP, Java, Ruby, Python, узла), пользователь имеет доступ через браузер hello, можно использовать [OpenID Connect](active-directory-v2-protocols.md) пользователя при входе. В OpenID Connect hello веб-приложение получает маркер идентификатора. Маркер идентификатора является маркером безопасности, который проверяет удостоверение пользователя hello и предоставляет сведения о пользователе hello в форме hello утверждений:

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Вы можете узнать о всех типов hello токенов и утверждений, которые доступны tooan приложения hello [v2.0 маркеры ссылка](active-directory-v2-tokens.md).

В веб-сервера приложений процесс входа в систему проверки подлинности hello принимает следующие общие действия:

![Поток аутентификации веб-приложения](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

Вы можете обеспечить удостоверение пользователя hello, проверка hello маркер идентификатора с помощью открытого ключа подписывания, полученные от конечной точки v2.0 hello. Файл cookie сеанса имеет значение, который может быть используется tooidentify hello пользователь запросов последующих страниц.

toosee данного сценария для действия, попробуйте сделать hello кода веб-приложения вход образцы в нашей v2.0 [Приступая к работе](active-directory-appmodel-v2-overview.md#getting-started) раздела.

В дополнение к этому toosimple входа, сервер веб-приложения может потребоваться tooaccess другой веб-службы, например API-интерфейса REST. В этом случае hello веб-сервера приложения использует объединенные потока OpenID Connect и OAuth 2.0, с помощью hello [потока кода авторизации OAuth 2.0](active-directory-v2-protocols.md). Чтобы больше узнать об этом сценарии, ознакомьтесь с тем, как [приступить к работе с веб-приложениями и интерфейсами веб-API](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).

## <a name="web-apis"></a>Веб-API
Можно использовать hello v2.0 конечной точки toosecure веб-служб, таких как веб-интерфейса API RESTful вашего приложения. Вместо маркеров безопасности и файлы cookie сеансов, веб-API использует toosecure маркера доступа OAuth 2.0, его данные и tooauthenticate входящие запросы. код, вызывающий Hello веб-API добавляет маркер доступа в заголовке авторизации hello HTTP-запроса, следующим образом:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hello веб-API использует hello access token tooverify hello API вызывающего удостоверения и tooextract сведения о hello вызывающей стороне из утверждений, которые шифруются в токене доступа hello. toolearn обо всех типах hello токенов и утверждений, которые приложение tooan доступны в разделе hello [v2.0 маркеры ссылка](active-directory-v2-tokens.md).

Задайте tooopt power hello пользователей веб-API или отказаться определенных функций или данных, предоставляя разрешения, также известный как [областей](active-directory-v2-scopes.md). Для вызова приложения tooacquire tooa область разрешений hello пользователь должен дать согласие toohello области во время потоку. Конечная точка v2.0 Hello запрашивает разрешение пользователя hello и затем записывает разрешения в все токены доступа, hello, получаемых веб-API. Hello веб-API проверяет маркеры доступа hello, он получает при каждом вызове и выполняет проверки авторизации.

Веб-API может получать маркеры доступа от всех типов приложений, включая приложения веб-сервера, классические и мобильные приложения, одностраничные приложения, серверные управляющие программы и даже другие веб-API. Hello поток высокого уровня для веб-API выглядит следующим образом:

![Поток аутентификации веб-API](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

toolearn как образцы toosecure веб-API с помощью маркера доступа OAuth2, извлечение hello кода веб-API в нашем [Приступая к работе](active-directory-appmodel-v2-overview.md#getting-started) раздела.

Во многих случаях веб-API также требуется toomake исходящих запросов tooother нижестоящим веб-API, защищенным Azure Active Directory.  toodo таким образом, веб-API можно использовать преимущества Azure AD **по имени из** потока, который разрешает входящий токен доступа для другой toobe маркера доступа, используемых в исходящих запросов tooexchange hello веб-API.  Описывается Hello v2.0 конечной точки от имени потока в [подробно описывается здесь](active-directory-v2-protocols-oauth-on-behalf-of.md).

## <a name="mobile-and-native-apps"></a>Мобильные и собственные приложения
Устройство установлено приложениям, например, мобильных и настольных приложений, часто требуется tooaccess внутренних служб или веб-API, хранения данных и выполнять действия от имени пользователя. Эти приложения можно добавить tooback входа и авторизации служб с помощью hello [потока кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

В этой процедуре приложение hello получает код авторизации из конечной точки v2.0 hello при входе пользователя hello. Представляет код авторизации Hello hello приложения разрешение toocall служб, от имени пользователя hello, вошедшему в систему. приложение Hello можно обменять код авторизации hello в фоновом режиме hello для токена доступа OAuth 2.0 и токен обновления. приложение Hello можно использовать tooWeb tooauthenticate токена доступа hello API-интерфейсы в HTTP-запросы и использовать новых токенов доступа hello обновления токена tooget срок действия старых маркера доступа.

![Поток аутентификации собственного приложения](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a>Одностраничные приложения (JavaScript)
Многие современные приложения содержат интерфейсное одностраничное приложение, созданное преимущественно на языке JavaScript. Часто они создаются с помощью таких платформ, как AngularJS, Ember.js или Durandal.js. Конечная точка v2.0 Hello Azure AD поддерживает эти приложения с помощью hello [неявного потока OAuth 2.0](active-directory-v2-protocols-implicit.md).

В этой процедуре приложение hello получение маркеров непосредственно из hello v2.0 авторизации конечной точки без обмен любого сервера на сервер. Все логики проверки подлинности и обработки принимает сеанса поместите полностью в клиенте JavaScript hello без перенаправления дополнительных страниц.

![Неявный поток аутентификации](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

toosee данного сценария для действия, попробуйте один из примеров кода одностраничного приложения hello в нашем [Приступая к работе](active-directory-appmodel-v2-overview.md#getting-started) раздела.

## <a name="daemons-and-server-side-apps"></a>Управляющие программы и серверные приложения
Приложения, имеющие долго выполняющихся процессов или для работы без взаимодействия с пользователем также нужна возможность прощелкать tooaccess ресурсы, такие как веб-API. Эти приложения могут проверять подлинность и получить токены, используя удостоверение приложения hello, а не пользователя делегировать удостоверение с hello OAuth 2.0 поток клиентских учетных данных.

В этой процедуре приложение hello взаимодействует непосредственно с hello `/token` конечные точки tooobtain конечной точки:

![Поток аутентификации управляющей программы](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

toobuild приложении управляющей программы см. в документации учетные данные клиента hello в нашем [Приступая к работе](active-directory-appmodel-v2-overview.md#getting-started) статьи или повторите [образец приложения .NET](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
