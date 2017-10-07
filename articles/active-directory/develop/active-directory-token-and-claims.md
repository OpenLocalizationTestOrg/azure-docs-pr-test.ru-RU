---
title: "aaaLearn об hello другой токен и типы, поддерживаемые Azure AD утверждений | Документы Microsoft"
description: "Руководство для понимания, оценке заявок hello в hello SAML 2.0 и веб-токены JSON (JWT) маркеры, выпущенные с Azure Active Directory (AAD)"
documentationcenter: na
author: dstrockis
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 166aa18e-1746-4c5e-b382-68338af921e2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: c512894476613e94d86a994c32a8459d6cf00fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-token-reference"></a>Справочник по токенам в Azure AD
Azure Active Directory (Azure AD) создает несколько типов маркеров безопасности во время обработки hello каждого потока проверки подлинности. В этом документе описывается формат hello, характеристики безопасности и содержимого каждого типа маркера.

## <a name="types-of-tokens"></a>Типы маркеров
Azure AD поддерживает hello [протокола авторизации OAuth 2.0](active-directory-protocols-oauth-code.md), который использует access_tokens и refresh_tokens.  Оно также поддерживает проверку подлинности и войти через [OpenID Connect](active-directory-protocols-openid-connect-code.md), который представляет тип маркера, id_token hello.  Каждый из этих маркеров представляется как "токен носителя".

Токен носителя — это упрощенный токен безопасности, предоставляет hello tooa доступа «bearer» защищенный ресурс. В этом смысле hello «bearer» является любая сторона, которая может предъявить токен hello. Если требуется проверка подлинности с помощью Azure AD в заказ tooreceive токен носителя, необходимо выполнить действия токена, перехват tooprevent toosecure hello несанкционированной стороной. Так как токены носителя нет сторон tooprevent несанкционированный встроенный механизм использовать их, они должны передаваться в защищенном канале, например безопасность на уровне транспорта (HTTPS). Если токен носителя, передается в очистить hello, атаке hello man в среднем можно токен используется tooacquire hello и получить несанкционированный доступ tooa защищенных ресурсов. Hello те же принципы безопасности применяются при сохранении или кэшировании токенов носителя для последующего использования. Необходимо всегда проверять, что приложение передает и сохраняет токены носителя безопасным образом. Дополнительные сведения о безопасности в случае применения токенов носителя см. в [RFC 6750, раздел 5](http://tools.ietf.org/html/rfc6750).

Многие hello токенов, выданных Azure AD реализуются как веб-маркеры JSON или JWT.  Маркер JWT — это компактное и безопасное для URL-адреса средство передачи информации между двумя сторонами.  Hello сведения, содержащиеся в JWT известны как «утверждения» или проверочные утверждения информации о носителя hello и субъект маркера hello.  утверждения Hello в JWT являются объектами JSON в кодировке и сериализацию для передачи.  Поскольку hello JWT, выданного Azure AD подписан, но не шифруется, можно легко проверять содержимое hello JWT для целей отладки.  Для этого существует несколько инструментов, таких как [jwt.calebb.net](http://jwt.calebb.net). Дополнительные сведения о JWT можно ссылаться toohello [спецификации JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

## <a name="idtokens"></a>Маркеры id_token
Маркеры id_token — это разновидность маркера безопасности входа, который приложение получается при аутентификации с использованием [OpenID Connect](active-directory-protocols-openid-connect-code.md).  Они представлены в виде [JWT](#types-of-tokens)и содержат утверждения, которые можно использовать для входа в приложение hello пользователя.  Можно использовать утверждения hello в id_token как угодно — обычно используется для отображения сведений учетной записи или принятия решений управления доступом в приложении.

На текущий момент маркеры "id_token" подписываются, но не зашифровываются.  Когда приложение получает id_token, он должен [проверки подписи hello](#validating-tokens) tooprove hello подлинность маркера и проверить его допустимость несколько утверждений в токен tooprove hello.  Hello утверждений, прошедшим проверку приложения зависят от требований к сценарию, но существуют некоторые [общие проверки утверждения](#validating-tokens) , приложение необходимо выполнить в каждом случае.

См. в следующем разделе сведения на id_tokens утверждений, а также id_token образец hello.  Обратите внимание, что утверждения hello в id_tokens не возвращаются в любом порядке.  Кроме того, в любой момент в маркеры "id_token" можно добавлять новые утверждения. При этом сбоев в работе приложения возникать не должно.  Hello следующий список содержит hello утверждения, которые приложение может надежно интерпретировать на момент написания этой статьи hello.  При необходимости еще более подробные сведения можно найти в hello [спецификация OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-idtoken"></a>Пример маркера id_token
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ.
```

> [!TIP]
> Для занятия, попробуйте проверки утверждений hello в id_token образец hello, вставив его в [calebb.net](http://jwt.calebb.net).
> 
> 

#### <a name="claims-in-idtokens"></a>Утверждения в маркерах id_token
> [!div class="mx-codeBreakAll"]
| Утверждение JWT | Name (Имя) | Описание |
| --- | --- | --- |
| `appid` |Идентификатор приложения |Идентифицирует hello приложение, использующее токен tooaccess hello ресурса. приложение Hello может действовать самостоятельно или от имени пользователя. Идентификатор приложения Hello обычно представляет объект приложения, но также может представлять объект участника службы в Azure AD. <br><br> **Пример значения JWT**: <br> `"appid":"15CB020F-3984-482A-864D-1D92265E8268"` |
| `aud` |Аудитория |Hello предназначен получателя токена hello. приложения Hello, которое получает токен hello необходимо убедиться, что значение, обозначающее аудиторию hello указано правильно и отклонять любые токены, предназначенные для другой аудитории. <br><br> **Пример значения SAML**: <br> `<AudienceRestriction>`<br>`<Audience>`<br>`https://contoso.com`<br>`</Audience>`<br>`</AudienceRestriction>` <br><br> **Пример значения JWT**: <br> `"aud":"https://contoso.com"` |
| `appidacr` |Application Authentication Context Class Reference |Указывает способ проверки подлинности клиента hello. Для открытого клиента значение hello — 0. Если используются ИД клиента и секрет клиента, hello значение равно 1. <br><br> **Пример значения JWT**: <br> `"appidacr": "0"` |
| `acr` |Authentication Context Class Reference |Указывает, как hello была выполнена проверка подлинности субъекта, как клиент противоположность toohello в утверждение ссылку на класс контекста аутентификации приложения hello. Значение «0» указывает, что аутентификация конечного пользователя hello не отвечает требованиям hello объекта ISO/IEC 29115. <br><br> **Пример значения JWT**: <br> `"acr": "0"` |
| Authentication Instant |Записи hello дату и время аутентификации. <br><br> **Пример значения SAML**: <br> `<AuthnStatement AuthnInstant="2011-12-29T05:35:22.000Z">` | |
| `amr` |Метод проверки подлинности |Определяет, как был аутентифицирован субъект hello hello маркера. <br><br> **Пример значения SAML**: <br> `<AuthnContextClassRef>`<br>`http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod/password`<br>`</AuthnContextClassRef>` <br><br> **Пример значения JWT**: `“amr”: ["pwd"]` |
| `given_name` |Имя |Предоставляет hello сначала или «данное имя пользователя hello» в виде набора в объекте пользователя Azure AD hello. <br><br> **Пример значения SAML**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname”>`<br>`<AttributeValue>Frank<AttributeValue>` <br><br> **Пример значения JWT**: <br> `"given_name": "Frank"` |
| `groups` |Группы |Предоставляет идентификаторы объектов, которые представляют Привет субъекта в группах. Эти значения являются уникальными (см. идентификатор объекта) и безопасно использовать для управления доступом, например принудительной авторизации tooaccess ресурса. Hello группы, входящие в группы утверждения hello настраиваются на основе каждого приложения посредством свойства «groupMembershipClaims» hello манифест приложения hello. Если установлено значение null, исключаются все группы, если значение SecurityGroup — включается только членство в группах безопасности Active Directory, а значение All подразумевает включение как групп безопасности, так и списков рассылки Office 365. <br><br> **Пример значения SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">`<br>`<AttributeValue>07dd8a60-bf6d-4e17-8844-230b77145381</AttributeValue>` <br><br> **Пример значения JWT**: <br> `“groups”: ["0e129f5b-6b0a-4944-982d-f776045632af", … ]` |
| `idp` |Identity Provider |Поставщик удостоверений записей hello проверку подлинности субъекта hello hello маркера. Это значение является значением идентичные toohello hello издателя утверждения, если учетная запись пользователя hello не работает в разным клиентам hello издателя. <br><br> **Пример значения SAML**: <br> `<Attribute Name=” http://schemas.microsoft.com/identity/claims/identityprovider”>`<br>`<AttributeValue>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/<AttributeValue>` <br><br> **Пример значения JWT**: <br> `"idp":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `iat` |IssuedAt |Хранит время hello, какие hello выдачи маркера. Чаще всего используется toomeasure возраста токена. <br><br> **Пример значения SAML**: <br> `<Assertion ID="_d5ec7a9b-8d8f-4b44-8c94-9812612142be" IssueInstant="2014-01-06T20:20:23.085Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">` <br><br> **Пример значения JWT**: <br> `"iat": 1390234181` |
| `iss` |Издатель |Идентифицирует hello службы маркеров безопасности (STS), создает и возвращает токен hello. В возвращаемых Azure AD токенах hello hello издателем является sts.windows.net. Hello GUID в значении утверждения издателя hello — идентификатор клиента hello hello каталог Azure AD. Идентификатор клиента Hello представляет неизменяемый и надежный идентификатор каталога hello. <br><br> **Пример значения SAML**: <br> `<Issuer>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/</Issuer>` <br><br> **Пример значения JWT**: <br>  `"iss":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `family_name` |Фамилия |Предоставляет фамилию hello, Фамилия или фамилию пользователя hello, как определено в объекте пользователя Azure AD hello. <br><br> **Пример значения SAML**: <br> `<Attribute Name=” http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname”>`<br>`<AttributeValue>Miller<AttributeValue>` <br><br> **Пример значения JWT**: <br> `"family_name": "Miller"` |
| `unique_name` |Имя |Предоставляет читаемое значение, идентифицирующее субъект hello hello маркера. Это значение не гарантируется, что toobe уникальный в пределах клиента и не спроектированных toobe используется только для отображения. <br><br> **Пример значения SAML**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name”>`<br>`<AttributeValue>frankm@contoso.com<AttributeValue>` <br><br> **Пример значения JWT**: <br> `"unique_name": "frankm@contoso.com"` |
| `oid` |Object ID |Содержит уникальный идентификатор объекта в Azure AD. Это значение является неизменяемым и не может быть переназначено или повторно использовано. Используйте tooidentify идентификатор объекта hello объекта в запросы tooAzure AD. <br><br> **Пример значения SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">`<br>`<AttributeValue>528b2ac2-aa9c-45e1-88d4-959b53bc7dd0<AttributeValue>` <br><br> **Пример значения JWT**: <br> `"oid":"528b2ac2-aa9c-45e1-88d4-959b53bc7dd0"` |
| `roles` |Роли |Контроль доступа представляет все роли приложений, которые hello субъекта был предоставлен напрямую или косвенно через членство в группе и может быть используется tooenforce на основе ролей. Роли приложения определяются на основе каждого приложения, используя hello `appRoles` свойства манифеста приложения hello. Hello `value` свойства каждой роли приложения — hello значение, которое отображается в утверждении ролей hello. <br><br> **Пример значения SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">`<br>`<AttributeValue>Admin</AttributeValue>` <br><br> **Пример значения JWT**: <br> `“roles”: ["Admin", … ]` |
| `scp` |Область |Указывает hello олицетворения разрешения предоставленный toohello клиентское приложение. разрешение по умолчанию Hello — `user_impersonation`. Владелец Hello hello, защищенному ресурсу может регистрировать дополнительные значения в Azure AD. <br><br> **Пример значения JWT**: <br> `"scp": "user_impersonation"` |
| `sub` |Субъект |Идентифицирует участника hello о какой hello подтверждает токен, сведения, такие как hello пользователя приложения. Это значение является постоянным и не может быть переназначены или повторно, поэтому его можно проверки авторизации используется tooperform безопасно. Поскольку hello субъект всегда присутствует в hello маркеры hello Azure AD токенах, мы рекомендуем использовать это значение в системе авторизации общего назначения. <br> `SubjectConfirmation` не является утверждением. Он описывает, как проверяется субъект hello hello маркера. `Bearer`Указывает, что этот hello субъект подтвержден благодаря владению токен hello. <br><br> **Пример значения SAML**: <br> `<Subject>`<br>`<NameID>S40rgb3XjhFTv6EQTETkEzcgVmToHKRkZUIsJlmLdVc</NameID>`<br>`<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />`<br>`</Subject>` <br><br> **Пример значения JWT**: <br> `"sub":"92d0312b-26b9-4887-a338-7b00fb3c5eab"` |
| `tid` |Tenant ID |Неизменяемый, однократного идентификатор, который идентифицирует клиента каталога hello, выдавшего токен hello. Ресурсы каталога конкретного клиента tooaccess это значение можно использовать в приложении несколькими клиентами. Например можно использовать этот клиент hello tooidentify значение в toohello вызова Graph API. <br><br> **Пример значения SAML**: <br> `<Attribute Name=”http://schemas.microsoft.com/identity/claims/tenantid”>`<br>`<AttributeValue>cbb1a5ac-f33b-45fa-9bf5-f37db0fed422<AttributeValue>` <br><br> **Пример значения JWT**: <br> `"tid":"cbb1a5ac-f33b-45fa-9bf5-f37db0fed422"` |
| `nbf`, `exp` |Token Lifetime |Определяет hello интервал времени, в течение которого действителен маркер. Hello служба, проверяющая токен hello следует убедиться в том, hello текущая дата — в hello время существования маркера, else отклонить токен hello. Hello службы может разрешить для копирования toofive минут после окончания tooaccount диапазон времени существования маркера hello различия в формате времени («отклонение во времени») между Azure AD и службы hello. <br><br> **Пример значения SAML**: <br> `<Conditions`<br>`NotBefore="2013-03-18T21:32:51.261Z"`<br>`NotOnOrAfter="2013-03-18T22:32:51.261Z"`<br>`>` <br><br> **Пример значения JWT**: <br> `"nbf":1363289634, "exp":1363293234` |
| `upn` |Имя участника-пользователя |Сохраняет hello имя основного пользователя hello.<br><br> **Пример значения JWT**: <br> `"upn": frankm@contoso.com` |
| `ver` |Version (версия) |Содержит номер версии hello hello маркера. <br><br> **Пример значения JWT**: <br> `"ver": "1.0"` |

## <a name="access-tokens"></a>Маркеры доступа
После успешной проверки подлинности Azure AD возвращает маркер доступа, который можно использовать tooaccess защищенных ресурсов. маркер доступа Hello является JSON Web Token (JWT) в кодировке base-64, и его содержимое может проверяться с помощью декодера.

Если приложение только *использует* tooAPIs доступа tooget маркеры доступа, можно (и следует обрабатываются токены доступа как полностью непрозрачный — это только строки, которые приложение сможет пройти tooresources HTTP-запросов.

При запросе маркера доступа Azure AD также возвращает некоторые метаданные hello маркер доступа для использования приложения.  Эти сведения включают hello срок действия маркера доступа hello и hello областей, для которых он допустим.  Это позволяет интеллектуальной кэширование маркеров доступа без необходимости tooparse открыть токен доступа hello сам tooperform вашего приложения.

Если приложение является интерфейсом API, защищенные с помощью Azure AD, который ожидает токены доступа в HTTP-запросы, затем следует выполнить проверку и проверки токенов hello, получаемых. Приложения должен выполнить проверку маркера доступа hello перед его использованием tooaccess ресурсов. Дополнительные сведения о проверке см. в разделе [Проверка маркеров](#validating-tokens).  
Дополнительные сведения о toodo это с помощью .NET, в статье [защитить веб-API, с помощью маркеров носителя из Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

## <a name="refresh-tokens"></a>Маркеры обновления

Обновить маркеры являются маркерами безопасности, которых приложение может использовать tooacquire новые маркеры доступа, см в потоке OAuth 2.0.  Он позволяет вашей tooresources приложения tooachieve долгосрочной доступ от имени пользователя, не требуя взаимодействие с пользователем hello.

Маркеры обновления относятся к нескольким ресурсам.  Это toosay, токен обновления, полученные во время запроса маркера для одного ресурса может быть активирован для маркеры доступа tooa совершенно разных ресурсов. toodo hello, этот набор `resource` параметр в запрос toohello hello целевой ресурс.

Токены обновления являются полностью непрозрачный tooyour приложения. Они находятся в течение продолжительного времени, но приложения не должны быть написаны tooexpect, токен обновления будут продолжаться в течение любого периода времени.  Маркеры обновления могут стать недействительными в любое время по разным причинам.  Здравствуйте, только для вашего приложения tooknow, если токен обновления является допустимым в том числе tooattempt tooredeem его, делая конечная точка маркера запроса маркера tooAzure AD.

Когда вы активируете токен обновления для нового маркера доступа, вы получите новый маркер обновления в ответ на токен hello.  Сохраняйте hello только что выданный маркер обновления, заменив hello, который используется в запросе hello.  Такой подход обеспечит максимальный срок действия маркеров обновления.

## <a name="validating-tokens"></a>Проверка маркеров

В порядке toovalidate букве id_token или access_token приложение должно проверять оба hello маркер подписи и hello утверждения. Маркеры доступа toovalidate заказа приложения должны также проверять hello издатель, аудитория hello и hello подписи маркеров. Они должны toobe проверяется hello значения в документе обнаружения hello OpenID. Например, hello клиента независимых версия документа hello расположен в [https://login.microsoftonline.com/common/.well-known/openid-configuration](https://login.microsoftonline.com/common/.well-known/openid-configuration). Azure AD по промежуточного слоя предусмотрены встроенные возможности для проверки маркеров доступа, а также можно выполнять поиск нашей [образцы](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-code-samples) toofind один языке hello по своему усмотрению. Дополнительные сведения о способ tooexplicitly проверки маркера JWT см. в разделе hello [вручную пример проверки JWT](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation).  

Мы предоставляем библиотеки и образцы кода, которые показывают, как tooeasily обрабатывать проверки токенов - hello ниже сведения просто предназначен для тех, кто обратиться hello toounderstand базовый процесс.  Для проверки токенов JWT также доступны несколько сторонних библиотек с открытым исходным кодом. Среди них вы найдете как минимум один вариант для каждой платформы и языка. Дополнительные сведения о библиотеках аутентификации Azure AD и примеры кода см. в статье [Библиотеки проверки подлинности Azure Active Directory](active-directory-authentication-libraries.md).

#### <a name="validating-hello-signature"></a>Проверка подписи hello

JWT содержит три сегмента, разделенные точками hello `.` символов.  Первый сегмент Hello называется hello **заголовок**, hello, во-вторых, как hello **текст**и hello в-третьих, как hello **подпись**.  Сегмент Hello подпись может быть используется toovalidate hello подлинность маркера hello, чтобы доверенным приложения.

Маркеры, выдаваемые Azure AD, подписываются при помощи стандартных отраслевых алгоритмов асимметричного шифрования, таких как RSA 256. Заголовок Hello hello JWT содержит сведения о ключе hello и метод шифрования используется токен hello toosign:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "kriMPdmBvx68skT8-mPAB3BseeA"
}
```

Hello `alg` утверждение указывает hello алгоритм, который был токен используется toosign hello, при hello `x5t` утверждение указывает hello определенный открытый ключ, который был toosign используется токен hello.

Azure AD может в любой момент времени подписать маркер идентификации с использованием любой пары открытого и закрытого ключей из определенного набора пар. Azure AD поворачивает hello возможный набор ключей на периодической основе так, что приложение должно записывать toohandle этих ключ автоматически изменяется.  Toocheck разумного частоты для обновления toohello открытых ключей, используемых Azure AD выполняется каждые 24 часа.

Можно получить hello подписание подпись hello необходимые toovalidate ключей данных с помощью документа OpenID Connect метаданных hello, расположенный в:

```
https://login.microsoftonline.com/common/.well-known/openid-configuration
```

> [!TIP]
> Попробуйте ввести этот URL-адрес в браузере.
> 
> 

Данный документ метаданных является объект JSON, содержащий несколько важных сведений, таких как расположение hello hello конечных точек, необходимые для выполнения проверки подлинности OpenID Connect.  

Он также включает `jwks_uri`, что дает hello расположение hello набор открытых ключей, как использовать toosign токены.  документ JSON Hello, расположенный hello `jwks_uri` содержит все hello сведения об открытом ключе используемый на этот конкретный момент времени.  Приложение может использовать hello `kid` утверждения в tooselect заголовок JWT hello, какие открытый ключ в этом документе было toosign используется данная лексема.  Затем можно выполнить проверку подписи с использованием hello правильный открытый ключ и hello указанного алгоритма.

Выполнение проверки подписи вне hello рамки данного документа — помогающие сделать это при необходимости доступны многие библиотеки с открытым исходным кодом.

#### <a name="validating-hello-claims"></a>Проверка утверждения hello

Когда приложение получает токен (id_token при входе пользователя, или маркер доступа в качестве токена носителя в запросе hello HTTP) его необходимо выполнить несколько проверки hello утверждений в токен hello.  Помимо прочего, к ним относятся:

* Hello **аудитории** утверждения - tooverify, hello маркера было предполагаемым toobe заданному tooyour приложения.
* Hello **вступления в силу** и **время истечения срока действия** утверждений - tooverify, hello маркера не истек.
* Hello **издателя** утверждения - tooverify, hello маркера действительно был выпущен tooyour приложения Azure AD.
* Hello **Nonce** -toomitigate атаки воспроизведения токена.
* и многое другое...

Полный список проверки утверждений, выполните приложение для маркеров безопасности, см. в разделе toohello [спецификация OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). Подробные сведения о hello ожидаемые значения для этих утверждений включаются в предыдущем hello [id_token раздел](#id-tokens) раздела.

## <a name="sample-tokens"></a>Примеры токенов

В этом разделе приводятся примеры токенов SAML и JWT, которые возвращает служба Azure AD. В этих примерах позволяет увидеть hello утверждения в контексте.

### <a name="saml-token"></a>Токен SAML

Ниже приведен пример типичного токена SAML.

    <?xml version="1.0" encoding="UTF-8"?>
    <t:RequestSecurityTokenResponse xmlns:t="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <t:Lifetime>
        <wsu:Created xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T05:15:47.060Z</wsu:Created>
        <wsu:Expires xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T06:15:47.060Z</wsu:Expires>
      </t:Lifetime>
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
          <Address>https://contoso.onmicrosoft.com/MyWebApp</Address>
        </EndpointReference>
      </wsp:AppliesTo>
      <t:RequestedSecurityToken>
        <Assertion xmlns="urn:oasis:names:tc:SAML:2.0:assertion" ID="_3ef08993-846b-41de-99df-b7f3ff77671b" IssueInstant="2014-12-24T05:20:47.060Z" Version="2.0">
          <Issuer>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</Issuer>
          <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
              <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
              <ds:Reference URI="#_3ef08993-846b-41de-99df-b7f3ff77671b">
                <ds:Transforms>
                  <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
                <ds:DigestValue>cV1J580U1pD24hEyGuAxrbtgROVyghCqI32UkER/nDY=</ds:DigestValue>
              </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>j+zPf6mti8Rq4Kyw2NU2nnu0pbJU1z5bR/zDaKaO7FCTdmjUzAvIVfF8pspVR6CbzcYM3HOAmLhuWmBkAAk6qQUBmKsw+XlmF/pB/ivJFdgZSLrtlBs1P/WBV3t04x6fRW4FcIDzh8KhctzJZfS5wGCfYw95er7WJxJi0nU41d7j5HRDidBoXgP755jQu2ZER7wOYZr6ff+ha+/Aj3UMw+8ZtC+WCJC3yyENHDAnp2RfgdElJal68enn668fk8pBDjKDGzbNBO6qBgFPaBT65YvE/tkEmrUxdWkmUKv3y7JWzUYNMD9oUlut93UTyTAIGOs5fvP9ZfK2vNeMVJW7Xg==</ds:SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <X509Data>
                <X509Certificate>MIIDPjCCAabcAwIBAgIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTQwMTAxMDcwMDAwWhcNMTYwMTAxMDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSCWg6q9iYxvJE2NIhSyOiKvqoWCO2GFipgH0sTSAs5FalHQosk9ZNTztX0ywS/AHsBeQPqYygfYVJL6/EgzVuwRk5txr9e3n1uml94fLyq/AXbwo9yAduf4dCHTP8CWR1dnDR+Qnz/4PYlWVEuuHHONOw/blbfdMjhY+C/BYM2E3pRxbohBb3x//CfueV7ddz2LYiH3wjz0QS/7kjPiNCsXcNyKQEOTkbHFi3mu0u13SQwNddhcynd/GTgWN8A+6SN1r4hzpjFKFLbZnBt77ACSiYx+IHK4Mp+NaVEi5wQtSsjQtI++XsokxRDqYLwus1I1SihgbV/STTg5enufuwIDAQABo2IwYDBeBgNVHQEEVzBVgBDLebM6bK3BjWGqIBrBNFeNoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAA4IBAQCJ4JApryF77EKC4zF5bUaBLQHQ1PNtA1uMDbdNVGKCmSp8M65b8h0NwlIjGGGy/unK8P6jWFdm5IlZ0YPTOgzcRZguXDPj7ajyvlVEQ2K2ICvTYiRQqrOhEhZMSSZsTKXFVwNfW6ADDkN3bvVOVbtpty+nBY5UqnI7xbcoHLZ4wYD251uj5+lo13YLnsVrmQ16NCBYq2nQFNPuNJw6t3XUbwBHXpF46aLT1/eGf/7Xx6iy8yPJX4DyrpFTutDz882RWofGEO5t4Cw+zZg70dJ/hH/ODYRMorfXEW+8uKmXMKmX2wyxMKvfiPbTy5LmAU8Jvjs2tLg4rOBcXWLAIarZ</X509Certificate>
              </X509Data>
            </KeyInfo>
          </ds:Signature>
          <Subject>
            <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">m_H3naDei2LNxUmEcWd0BZlNi_jVET1pMLR6iQSuYmo</NameID>
            <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
          </Subject>
          <Conditions NotBefore="2014-12-24T05:15:47.060Z" NotOnOrAfter="2014-12-24T06:15:47.060Z">
            <AudienceRestriction>
              <Audience>https://contoso.onmicrosoft.com/MyWebApp</Audience>
            </AudienceRestriction>
          </Conditions>
          <AttributeStatement>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
              <AttributeValue>a1addde8-e4f9-4571-ad93-3059e3750d23</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/tenantid">
              <AttributeValue>b9411234-09af-49c2-b0c3-653adc1f376e</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
              <AttributeValue>sample.admin@contoso.onmicrosoft.com</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname">
              <AttributeValue>Admin</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname">
              <AttributeValue>Sample</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">
              <AttributeValue>5581e43f-6096-41d4-8ffa-04e560bab39d</AttributeValue>
              <AttributeValue>07dd8a89-bf6d-4e81-8844-230b77145381</AttributeValue>
              <AttributeValue>0e129f4g-6b0a-4944-982d-f776000632af</AttributeValue>
              <AttributeValue>3ee07328-52ef-4739-a89b-109708c22fb5</AttributeValue>
              <AttributeValue>329k14b3-1851-4b94-947f-9a4dacb595f4</AttributeValue>
              <AttributeValue>6e32c650-9b0a-4491-b429-6c60d2ca9a42</AttributeValue>
              <AttributeValue>f3a169a7-9a58-4e8f-9d47-b70029v07424</AttributeValue>
              <AttributeValue>8e2c86b2-b1ad-476d-9574-544d155aa6ff</AttributeValue>
              <AttributeValue>1bf80264-ff24-4866-b22c-6212e5b9a847</AttributeValue>
              <AttributeValue>4075f9c3-072d-4c32-b542-03e6bc678f3e</AttributeValue>
              <AttributeValue>76f80527-f2cd-46f4-8c52-8jvd8bc749b1</AttributeValue>
              <AttributeValue>0ba31460-44d0-42b5-b90c-47b3fcc48e35</AttributeValue>
              <AttributeValue>edd41703-8652-4948-94a7-2d917bba7667</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/identityprovider">
              <AttributeValue>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</AttributeValue>
            </Attribute>
          </AttributeStatement>
          <AuthnStatement AuthnInstant="2014-12-23T18:51:11.000Z">
            <AuthnContext>
              <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
            </AuthnContext>
          </AuthnStatement>
        </Assertion>
      </t:RequestedSecurityToken>
      <t:RequestedAttachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedAttachedReference>
      <t:RequestedUnattachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedUnattachedReference>
      <t:TokenType>http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0</t:TokenType>
      <t:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</t:RequestType>
      <t:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</t:KeyType>
    </t:RequestSecurityTokenResponse>

### <a name="jwt-token---user-impersonation"></a>Токен JWT — олицетворение пользователя
Ниже приведен пример типичного токена JSON Web Token, используемого в потоке предоставления кода авторизации.
В tooclaims сложения hello токен включает номер версии в **ver** и **appidacr**, hello проверки подлинности ссылку на класс контекста, который указывает способ проверки подлинности клиента hello. Для открытого клиента значение hello — 0. Если использовался идентификатор клиента и секрет клиента, hello значение равно 1.

    {
     typ: "JWT",
     alg: "RS256",
     x5t: "kriMPdmBvx68skT8-mPAB3BseeA"
    }.
    {
     aud: "https://contoso.onmicrosoft.com/scratchservice",
     iss: "https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/",
     iat: 1416968588,
     nbf: 1416968588,
     exp: 1416972488,
     ver: "1.0",
     tid: "b9411234-09af-49c2-b0c3-653adc1f376e",
     amr: [
      "pwd"
     ],
     roles: [
      "Admin"
     ],
     oid: "6526e123-0ff9-4fec-ae64-a8d5a77cf287",
     upn: "sample.user@contoso.onmicrosoft.com",
     unique_name: "sample.user@contoso.onmicrosoft.com",
     sub: "yf8C5e_VRkR1egGxJSDt5_olDFay6L5ilBA81hZhQEI",
     family_name: "User",
     given_name: "Sample",
     groups: [
      "0e129f6b-6b0a-4944-982d-f776000632af",
      "323b13b3-1851-4b94-947f-9a4dacb595f4",
      "6e32c250-9b0a-4491-b429-6c60d2ca9a42",
      "f3a161a7-9a58-4e8f-9d47-b70022a07424",
      "8d4c81b2-b1ad-476d-9574-544d155aa6ff",
      "1bf80164-ff24-4866-b19c-6212e5b9a847",
      "76f80127-f2cd-46f4-8c52-8edd8bc749b1",
      "0ba27160-44d0-42b5-b90c-47b3fcc48e35"
     ],
     appid: "b075ddef-0efa-123b-997b-de1337c29185",
     appidacr: "1",
     scp: "user_impersonation",
     acr: "1"
    }.

## <a name="related-content"></a>Связанная информация
* В разделе hello Azure AD Graph [операции политики](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) и hello [объектом политики](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity), toolearn Дополнительные сведения об управлении политикой времени существования маркера через hello API Azure AD Graph.
* Дополнительные сведения об управлении политиками посредством командлетов PowerShell, включая примеры, см. в разделе [Configurable Token Lifetimes in Azure Active Directory (Public Preview)](../active-directory-configurable-token-lifetimes.md) (Настраиваемое время существования маркеров в Azure Active Directory (общедоступная предварительная версия)). 
