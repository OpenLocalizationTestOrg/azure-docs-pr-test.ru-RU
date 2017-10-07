---
title: "aaaAuthentication и авторизации в службе приложений Azure | Документы Microsoft"
description: "Ссылки на концептуальные и обзор hello проверки подлинности / авторизации компонентов для службы приложений Azure"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: b7151b57-09e5-4c77-a10c-375a262f17e5
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/29/2016
ms.author: mahender
ms.openlocfilehash: dc2074b16cce47b72b78ea7afeda89dbc4832166
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-app-service"></a>Проверка подлинности и авторизация в службе приложений Azure
## <a name="what-is-app-service-authentication--authorization"></a>Что такое проверка подлинности и авторизация службы приложений?
Проверка подлинности службы для приложения / авторизация — это компонент, который предоставляет способ для вашего приложения toosign пользователей, чтобы не нужно toochange код на внутреннем сервере приложения hello. Он предоставляет простой способ tooprotect приложения и рабочие данные для каждого пользователя.

Служба приложений использует федеративную идентификацию, при которой сторонний поставщик удостоверений сохраняет учетные записи и проводит аутентификацию пользователей. приложения Hello использует сведения об удостоверении hello поставщика, чтобы hello приложение не имеет toostore, сами сведения. Службы приложений поддерживает пять Поставщики удостоверений стандартной hello: Azure Active Directory, Facebook, Google, учетной записи Майкрософт и Twitter. Приложение может использовать любое количество этих tooprovide Поставщики удостоверений пользователей с параметрами для как в систему. Встроенная поддержка tooexpand hello, вы можете интегрировать другой поставщик удостоверений или [решении пользовательское удостоверение][custom-auth].

Если вы хотите tooget работу прямо сейчас, см. в одном hello следующие учебники:

* [Добавление приложения iOS для проверки подлинности tooyour] [ iOS] (или [Android], [Windows], [Xamarin.iOS], [ Xamarin.Android], [Xamarin.Forms], или [Cordova])
* [Проверка подлинности пользователя для приложений API в службе приложений Azure][apia-user]
* [Начало работы со службой приложений Azure (часть 2)][web-getstarted]

## <a name="how-authentication-works-in-app-service"></a>Как устроена проверка подлинности в службе приложений
В порядке tooauthenticate с помощью одного из поставщиков удостоверений hello необходимо сначала tooknow поставщика удостоверений hello tooconfigure о своем приложении. Поставщик удостоверений Hello будет предоставить идентификаторы и секретные данные, необходимо указать tooApp службы. На этом завершается hello отношения доверия, чтобы приложение службы можно проверить пользователя утверждения, таких как маркеры проверки подлинности, от поставщика удостоверений hello.

toosign в пользователя с помощью одного из этих поставщиков hello пользователь должен быть перенаправленный tooan конечную точку, которая выполняет вход пользователей для этого поставщика. Если веб-браузера, используемые клиентами, можно использовать службу приложения автоматически перенаправляются все toohello непроверенных пользователей конечной точки, которая выполняет вход пользователей. В противном случае вам потребуется toodirect клиентов слишком`{your App Service base URL}/.auth/login/<provider>`, где `<provider>` является одним из hello следующие значения: aad, facebook, google, microsoft или twitter. Сценарии для мобильных устройств и API рассматриваются в следующих разделах этой статьи.

У пользователей, которые взаимодействуют с приложением через веб-браузер, файл cookie будет настроен таким образом, чтобы при просмотре приложения они оставались аутентифицированными. Для других типов клиентов, например мобильные веб-токен JSON (JWT), который должны быть представлены в hello `X-ZUMO-AUTH` заголовок, будет выдано toohello клиента. Мобильные приложения Hello клиентских SDK будет обрабатывать это для вас. Кроме того, токен идентификации Azure Active Directory или токен доступа непосредственно в могут включаться hello `Authorization` заголовок как [токена носителя](https://tools.ietf.org/html/rfc6750).

Службы приложений будет проверять все файлы cookie или токен, что приложение выдает tooauthenticate пользователей. toorestrict, кто может получить доступ к приложению, в разделе hello [авторизации](#authorization) далее в этой статье.

### <a name="mobile-authentication-with-a-provider-sdk"></a>Мобильная проверка подлинности с пакетом SDK поставщика
После все настроено hello серверную часть, можно изменить toosign мобильных клиентов с использованием службы приложений. Существует два подхода:

* Используйте пакет SDK, что поставщик указанному идентификатору публикует tooestablish удостоверение и получить доступ tooApp службы.
* Использованием одной строки кода, поэтому этот пакет SDK для клиента мобильные приложения hello можно регистрация пользователей.

> [!TIP]
> Большинство приложений следует использовать поставщик SDK tooget более согласованной работы пользователей в систему, toouse обновления поддержки и tooget указывает другие преимущества, поставщик hello.
> 
> 

При использовании поставщика пакета SDK, пользователи могут войти в tooan взаимодействие, более тесно интегрируется с операционной системой hello, приложение hello ОС. Это также позволяет токен поставщика и некоторые сведения о пользователе на приветствия клиента, который позволяет гораздо проще tooconsume graph API-интерфейсов и настроить взаимодействие с пользователем hello. Время от времени на блоги и форумы вы увидите это ссылка tooas hello «потока клиента» или «клиент перенаправлен потока» тем код на клиенте hello выполняет вход пользователей, а код клиента hello Поставщик маркера доступа tooa.

После получения маркера поставщика ему toobe отправлено tooApp службы для проверки. Службы приложений проверяет токен hello, службы приложений создает новый маркер службы приложений, возвращаемый toohello клиента. пакет SDK для клиента мобильные приложения Hello имеет toomanage вспомогательные методы этого обмена и автоматически связать внутренняя служба приложения hello маркера tooall запросов toohello. Разработчики могут также содержать токен ссылки на поставщик toohello по усмотрению.

### <a name="mobile-authentication-without-a-provider-sdk"></a>Мобильная проверка подлинности без пакета SDK поставщика
Если tooset поставщика SDK не требуется, можно разрешить функция мобильные приложения hello toosign службе приложений Azure в для вас. Мобильные приложения Hello клиенту SDK откройте представление toohello поставщике по своему выбору и вход пользователя hello. Иногда на блоги и форумы, вы увидите этот hello tooas ссылка «потока сервера» или «потока, направленных на сервере» так, как hello процесс, выполняющий вход пользователей, которыми управляет сервер hello и пакет SDK для клиента hello не получает токен поставщика hello.

Код toostart этого потока, включенный в учебнике hello проверки подлинности для каждой платформы. В конце потока hello hello hello клиентский пакет SDK содержит токен службы приложений и hello маркер является внутренняя служба приложения toohello tooall автоматически вложенные запросы.

### <a name="service-to-service-authentication"></a>Взаимодействие между службами
Несмотря на то, что может предоставить приложения tooyour доступа пользователей, можно также доверять другой toocall приложения собственных API. Например, одно веб-приложение может вызывать API в другом веб-приложении. В этом случае использовать учетные данные для учетной записи службы вместо tooget учетные данные пользователя маркер. Учетная запись службы в терминологии Azure Active Directory также называется *субъектом-службой* , а проверка подлинности с использованием такой учетной записи называется сценарием взаимодействия между службами.

> [!IMPORTANT]
> Так как мобильные приложения работают на клиентских устройствах, эти приложения *не* считаются доверенными и не должны использовать поток субъекта-службы. Вместо этого они должны использовать пользовательский поток, описанный выше.
> 
> 

В сценариях взаимодействия между службами служба приложений может защитить приложение с помощью Azure Active Directory. вызывающее приложение Hello достаточно tooprovide маркер авторизации основной службы Azure Active Directory, полученный путем предоставления hello идентификатор клиента и секрет Azure Active Directory в клиент. Пример такого сценария, использующего ASP.NET API приложения описан в учебнике hello [основной проверки подлинности службы для приложений API][apia-service].

Следует toouse toohandle проверки подлинности службы приложений сценарий service to service можно использовать клиентские сертификаты или обычной проверки подлинности. Сведения о клиентских сертификатов в Azure см. в разделе [как tooConfigure TLS взаимной проверки подлинности для веб-приложений](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Сведения об обычной проверке подлинности в ASP.NET см. в статье [Authentication Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters) (Фильтры проверки подлинности в веб-API ASP.NET 2).

Проверка подлинности учетной записи службы из приложения tooan API службы приложений логики приложения является особым случаем, который подробно описан в [с помощью настраиваемого API, размещенных в службе приложений с приложениями логики](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="authorization"></a>Принцип действия авторизации в службе приложений
У вас есть полный контроль над hello запросов, которые можно получить доступ к приложению. Проверка подлинности службы для приложения / авторизации можно настроить с помощью любого из следующих поведений hello:

* Разрешить только tooreach запросов проверки подлинности приложения.
  
    Если обозреватель получает анонимный запрос, служба приложение будет осуществлять перенаправление tooa страницы для поставщика удостоверений hello, выберите, чтобы пользователи могли войти. При поступлении запроса hello с мобильного устройства, hello возвращается ответ HTTP *проверки подлинности 401* ответа.
  
    Этот параметр не требуется toowrite любой код проверки подлинности во всех в вашем приложении. Если требуется более точное авторизации, сведения о пользователе hello — доступные tooyour код.
* Разрешить все запросы tooreach приложения, но проверки запросов на проверку подлинности и передают сведения о проверке подлинности в заголовках hello HTTP.
  
    Этот параметр откладывает код приложения tooyour решения об авторизации. Обеспечивает большую гибкость при обработке анонимных запросов, но у вас есть код toowrite.
* Разрешить все запросы tooreach приложения и не выполнять никаких действий на сведения о проверке подлинности в запросах hello.
  
    В этом случае hello проверки подлинности и авторизации функция выключена. Hello задачи проверки подлинности и авторизации полностью функционируют tooyour кода приложения.

Hello предыдущего поведения управляются hello **tootake действия, если запрос не прошел проверку подлинности** параметр в hello портал Azure. При выборе ** входа в систему *имя поставщика* **, все запросы имеют toobe с проверкой подлинности. **Разрешить запрос (никаких действий)** откладывает hello кода tooyour авторизации для принятия решений, но по-прежнему содержит сведения о проверке подлинности. Если toohave код обрабатывать все данные, можно отключить hello проверки подлинности и авторизации компонентов.

## <a name="working-with-user-identities-in-your-application"></a>Работа с удостоверениями пользователей в приложении
Службы приложений передает каким-либо приложением tooyour сведения пользователя с использованием особых заголовков. Эти заголовки не могут использоваться во внешних запросах. Они могут присутствовать, только если были установлены службой приложений при проверке подлинности или авторизации. Некоторые примеры заголовков включают:

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Код, написанный на любом языке, framework можно получить hello информацию, необходимую эти заголовки. Приложения ASP.NET 4.6 hello **ClaimsPrincipal** автоматически устанавливается с соответствующими значениями hello.

Приложения можно также получить дополнительные сведения по HTTP GET на hello `/.auth/me` конечную точку приложения. Допустимый токен, который включен в запросе hello будет возвращать полезных данных JSON с подробными сведениями о hello поставщика, который используется, hello базового поставщика маркера и сведения о пользователе. Hello мобильные приложения сервер SDK предоставляет вспомогательные методы toowork с этими данными. Дополнительные сведения см. в разделе [как toouse hello SDK Azure Mobile приложений Node.js](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), и [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info).

## <a name="documentation-and-additional-resources"></a>Документация и дополнительные ресурсы
### <a name="identity-providers"></a>Поставщики удостоверений
Здравствуйте, как следующие учебники Показать tooconfigure службы приложений toouse разные поставщики проверки подлинности:

* [Как tooconfigure входа приложения toouse Azure Active Directory][AAD]
* [Как tooconfigure входа Facebook toouse приложения][Facebook]
* [Как tooconfigure входа Google toouse приложения][Google]
* [Как tooconfigure входа приложения toouse учетной записи Майкрософт][MSA]
* [Как tooconfigure входа Twitter toouse приложения][Twitter]

Если требуется toouse системы удостоверений, отличный от hello историй, предоставляемых здесь, можно также использовать hello [поддержка нестандартной проверки подлинности в SDK сервера мобильных приложений .NET hello предварительного просмотра][custom-auth], который может использоваться в веб-приложениях мобильные приложения или приложения API.

### <a name="web-applications"></a>Веб-приложения
следующие учебники Hello показывают, как tooa tooadd проверки подлинности веб-приложения:

* [Начало работы со службой приложений Azure (часть 2)][web-getstarted]

### <a name="mobile-applications"></a>Мобильные приложения
следующие учебники Hello показывают, как tooadd проверки подлинности tooyour мобильных клиентов с помощью hello потока, направленных на сервере:

* [Добавление приложения iOS tooyour проверки подлинности][iOS]
* [Добавить приложение Android проверки подлинности tooyour][Android]
* [Добавление приложения Windows Authentication tooyour][Windows]
* [Добавление проверки подлинности приложения Xamarin.iOS tooyour][Xamarin.iOS]
* [Добавить приложение Xamarin.Android проверки подлинности tooyour][ Xamarin.Android]
* [Добавить приложение Xamarin.Forms проверки подлинности tooyour][Xamarin.Forms]
* [Добавление проверки подлинности приложения Cordova tooyour][Cordova]

Используйте следующие ресурсы, если требуется, чтобы поток toouse hello управляемая клиентом для Azure Active Directory hello.

* [Использовать hello библиотеку аутентификации Active Directory для iOS][ADAL-iOS]
* [Использовать hello библиотеку аутентификации Active Directory для Android][ADAL-Android]
* [Используйте hello Active Directory Authentication библиотеки для Windows и Xamarin][ADAL-dotnet]

Используйте следующие ресурсы, если требуется, чтобы поток toouse hello управляемая клиентом для Facebook hello.

* [Использовать hello Facebook SDK для iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#facebook-sdk)

Используйте следующие ресурсы, если требуется, чтобы toouse hello клиент перенаправлен поток Twitter hello.

* [Практическое руководство: проверка подлинности пользователей с помощью структуры Twitter для iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#twitter-fabric)

Используйте следующие ресурсы, если требуется, чтобы поток toouse hello управляемая клиентом для Google hello.

* [Использовать hello Google входа в пакет SDK для iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#google-sdk)

### <a name="api-applications"></a>Приложения API
Здравствуйте, следующие учебники Показать как tooprotect приложения API:

* [Проверка подлинности пользователя для приложений API в службе приложений Azure][apia-user]
* [Проверка подлинности с использованием субъекта-службы для приложений API в службе приложений Azure][apia-service]

[apia-user]: ../app-service-api/app-service-api-dotnet-user-principal-auth.md
[apia-service]: ../app-service-api/app-service-api-dotnet-service-principal-auth.md

[web-getstarted]: ../app-service-web/app-service-web-get-started-2.md#authenticate-your-users

[iOS]: ../app-service-mobile/app-service-mobile-ios-get-started-users.md
[Android]: ../app-service-mobile/app-service-mobile-android-get-started-users.md
[Xamarin.iOS]: ../app-service-mobile/app-service-mobile-xamarin-ios-get-started-users.md
[ Xamarin.Android]: ../app-service-mobile/app-service-mobile-xamarin-android-get-started-users.md
[Xamarin.Forms]: ../app-service-mobile/app-service-mobile-xamarin-forms-get-started-users.md
[Windows]: ../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-users.md
[Cordova]: ../app-service-mobile/app-service-mobile-cordova-get-started-users.md

[AAD]: ../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook]: ../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md
[Google]: ../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md
[MSA]: ../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter]: ../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md

[custom-auth]: ../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth

[ADAL-Android]: ../app-service-mobile/app-service-mobile-android-how-to-use-client-library.md#adal
[ADAL-iOS]: ../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#adal
[ADAL-dotnet]: ../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md#adal
