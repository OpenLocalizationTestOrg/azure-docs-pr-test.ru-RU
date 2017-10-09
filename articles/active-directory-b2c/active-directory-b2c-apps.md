---
title: "aaaAzure AD B2C | Документы Microsoft"
description: "типы приложений, которые можно создать в Azure Active Directory B2C hello Hello."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a>Azure Active Directory B2C: типы приложений
Служба Azure Active Directory (Azure AD) B2C поддерживает проверку подлинности для различных архитектур современных приложений. Все они основаны на стандартных отраслевых протоколов hello [OAuth 2.0](active-directory-b2c-reference-protocols.md) или [OpenID Connect](active-directory-b2c-reference-protocols.md). В этом документе кратко описывается hello типы приложений, которые можно создавать, зависят от hello языков или платформ вы предпочитаете. Он также позволяет понять hello сценариев высокого уровня, прежде чем [создания приложений](active-directory-b2c-overview.md#get-started).

## <a name="hello-basics"></a>Основы Hello
Все приложения, использующего Azure AD B2C должен быть зарегистрирован в вашей [каталоге B2C](active-directory-b2c-get-started.md) через hello [портала Azure](https://portal.azure.com/). процесс регистрации приложения Hello собирает и назначает несколько значений tooyour приложения:

* **идентификатор приложения** , который определяет конкретное приложение;
* Объект **URI перенаправления** , может быть используется toodirect ответы задней tooyour приложения.
* несколько других зависящих от сценария значений. Дополнительные сведения, узнайте, как слишком[Регистрация приложения](active-directory-b2c-app-registration.md).

После регистрации приложения hello, он взаимодействует с Azure AD, отправляя запросы toohello Azure AD версии 2.0, конечной точки:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

Указывает, каждый запрос, отправленный tooAzure AD B2C **политики**. Политика управляет поведением hello Azure AD. Можно также использовать эти конечные точки toocreate настраиваемый набор пользовательских интерфейсов. В число распространенных политик входят политики регистрации, входа и редактирования профилей. Если вы не знакомы с политиками, которыми необходимо ознакомиться hello Azure AD B2C [расширяемая инфраструктура политик](active-directory-b2c-reference-policies.md) перед продолжением.

взаимодействие Hello каждое приложение с конечной точкой v2.0 следует той же модели высокого уровня:

1. приложение Hello направляет hello пользователя toohello v2.0 конечной точки tooexecute [политики](active-directory-b2c-reference-policies.md).
2. Hello пользователь завершает toohello определения политики в соответствии с политикой hello.
3. приложение Hello получает каких-либо маркер безопасности от конечной точки v2.0 hello.
4. приложение Hello использует hello безопасности маркера tooaccess защищенные сведения или защищенному ресурсу.
5. сервер ресурсов Hello проверяет токен tooverify безопасности hello, который может быть предоставлен доступ.
6. приложение Hello периодически обновляет hello маркера безопасности.

<!-- TODO: Need a page for libraries toolink too-->
Эти шаги могут различаться, немного на основе hello типа приложения, построение которого выполняется. Библиотеки c открытым исходным ситуацию можно исправить hello сведения для вас.

## <a name="web-apps"></a>веб-приложений:
Для размещенных на сервере веб-приложений (.NET, PHP, Java, Ruby, Python, Node.js и пр.), доступ к которым осуществляется через браузер, Azure AD B2C предоставляет поддержку всех пользовательских действий с помощью [OpenID Connect](active-directory-b2c-reference-protocols.md). К этим действиям относятся вход, регистрация и редактирование профилей. В Azure AD B2C hello реализации OpenID Connect веб-приложение инициирует этих взаимодействий с пользователем, выполнив tooAzure запросы проверки подлинности AD. результат запроса hello Hello `id_token`. Этот маркер безопасности представляет удостоверение пользователя hello. Он также предоставляет сведения о пользователе hello в форме hello утверждений:

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Дополнительные сведения о типах hello приложения доступны tooan утверждения и маркеры в hello [ссылку на маркер B2C](active-directory-b2c-reference-tokens.md).

В веб-приложениях выполнение любой [политики](active-directory-b2c-reference-policies.md) включает в себя следующие действия.

![Изображение веб-приложения Swimlanes](./media/active-directory-b2c-apps/webapp.png)

Проверка hello `id_token` с помощью открытого ключа подписывания, полученный из Azure AD является достаточно удостоверение пользователя hello tooverify hello. Эта команда также задает файл cookie сеанса, который может быть пользователем hello используется tooidentify запросов последующих страниц.

toosee данного сценария для действия, попробуйте один из hello web app вход в примерах кода в нашем [Приступая к работе раздел](active-directory-b2c-overview.md#get-started).

В добавление toofacilitating простого входа в систему сервера веб-приложения также может понадобиться tooaccess серверной части веб-службы. В этом случае hello веб-приложения можно выполнять несколько разных [OpenID Connect потока](active-directory-b2c-reference-oidc.md) и токены с помощью коды авторизации и токенов обновления. Этот сценарий показан на следующих hello [раздел веб-API](#web-apis).

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a>Веб-API
Можно использовать Azure AD B2C toosecure веб-службы, например RESTful веб-приложения API. Веб-API можно использовать свои данные toosecure OAuth 2.0, входящие запросы HTTP с использованием маркеров проверки подлинности. код, вызывающий Hello веб-API добавляет маркер в hello заголовок авторизации HTTP-запроса:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hello веб-API можно использовать вызывающего hello API hello tooverify маркера удостоверения и tooextract сведения о hello вызывающей стороне из утверждений, которые шифруются в токене hello. Дополнительные сведения о типах hello приложения доступны tooan утверждения и маркеры в hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md).

> [!NOTE]
> Azure AD B2C в настоящее время поддерживает только интерфейсы веб-API, используемые собственными известными клиентами. Например, готовое приложение может включать приложение iOS, приложение Android и серверный интерфейс веб-API. Такая архитектура поддерживается полностью. Клиент партнера, например другое приложение iOS, позволяя tooaccess hello же веб-API в настоящий момент не поддерживается. Все компоненты hello завершения приложения должны совместно использовать с идентификатором одного приложения.
>
>

Интерфейс веб-API может получать маркеры от всех типов клиентов, включая веб-приложения, классические и мобильные приложения, одностраничные приложения, серверные управляющие программы и даже другие интерфейсы веб-API. Ниже приведен пример hello завершения потока для веб-приложения, которое вызывает веб-API:

![Изображение веб-API веб-приложения Swimlanes](./media/active-directory-b2c-apps/webapi.png)

toolearn Дополнительные сведения о кодах авторизации, токенов обновления и hello действия для получения маркеров, узнайте, как hello [протокол OAuth 2.0](active-directory-b2c-reference-oauth-code.md).

как toosecure веб-API с помощью Azure AD B2C извлечение hello веб-API учебников по toolearn наших [Приступая к работе раздел](active-directory-b2c-overview.md#get-started).

## <a name="mobile-and-native-apps"></a>Мобильные и собственные приложения
Приложения, которые установлены на устройствах, например мобильным и классическим приложениям часто требуется tooaccess внутренних служб или веб-API от имени пользователей. Можно добавить удостоверение настроенного управления взаимодействий tooyour приложений в машинном коде и безопасно вызывать серверными службами с помощью Azure AD B2C и hello [потока кода авторизации OAuth 2.0](active-directory-b2c-reference-oauth-code.md).  

В этой процедуре выполняется приложение hello [политики](active-directory-b2c-reference-policies.md) и получает `authorization_code` из Azure AD, после завершения пользователем hello hello политики. Hello `authorization_code` представляет hello приложения разрешение toocall служб, от имени пользователя hello, который подключен к сети. приложение Hello затем могут обмениваться hello `authorization_code` в фоновом режиме hello `id_token` и `refresh_token`.  приложение Hello можно использовать hello `id_token` tooauthenticate tooa серверной части веб-API в HTTP-запросов. Также можно использовать hello `refresh_token` tooget новый `id_token` после истечения срока действия старая версия.

> [!NOTE]
> Azure AD B2C в настоящее время поддерживает только те маркеры, используемые tooaccess службу фоновая веб-приложении. Например, готовое приложение может включать приложение iOS, приложение Android и серверный интерфейс веб-API. Такая архитектура поддерживается полностью. Позволяя партнера веб-API вашей tooaccess приложения iOS с помощью маркера доступа OAuth 2.0 в настоящее время не поддерживается. Все компоненты hello завершения приложения должны совместно использовать с идентификатором одного приложения.
>
>

![Изображение собственного приложения Swimlanes](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a>Текущие ограничения
Azure AD B2C в настоящее время не поддерживает следующие типы приложений hello, но они находятся в стратегия hello. 

### <a name="daemonsserver-side-apps"></a>Управляющие программы и серверные приложения
Приложения, которые содержат долго выполняющихся процессов или для работы без hello присутствия пользователя, также требуется способ tooaccess защищенные ресурсы, такие как веб-API. Эти приложения могут проверять подлинность и получить маркеры с помощью удостоверения приложение hello (а не удостоверения делегированного пользователя), с помощью hello OAuth 2.0 поток клиентских учетных данных.

На текущий момент служба Azure AD B2C не поддерживает этот поток. Эти приложения могут получить маркеры, только после того как появится интерактивный пользовательский поток.

### <a name="web-api-chains-on-behalf-of-flow"></a>Цепочки веб-API (поток On-Behalf-Of)
Многие архитектуры включают веб-API, который должен toocall другой нисходящий веб-API, где оба защищены с помощью Azure AD B2C. Этот сценарий характерен для собственных клиентов, содержащих интерфейс веб-API в качестве серверного компонента. Затем он вызывает интерактивным службам Майкрософт, например hello API Azure AD Graph.

Этот сценарий цепочек веб-API может поддерживаться с использованием учетных данных hello OAuth 2.0 JWT носителя grant, также известные как hello от имени представляет потока.  Однако hello от имени представляет поток еще не реализован в Azure AD B2C hello.
