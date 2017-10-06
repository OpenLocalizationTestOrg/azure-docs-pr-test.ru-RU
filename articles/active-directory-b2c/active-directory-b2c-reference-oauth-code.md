---
title: "Azure AD B2C: поток кода авторизации | Документация Майкрософт"
description: "Узнайте, как toobuild веб-приложений с помощью протокола проверки подлинности Azure AD B2C и OpenID Connect."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Azure Active Directory B2C: поток кода авторизации OAuth 2.0
Можно использовать предоставления кода авторизации OAuth 2.0 hello в приложения, установленные на устройстве toogain доступа tooprotected ресурсы, такие как веб-API. С помощью hello Azure Active Directory B2C (Azure AD B2C) реализацию OAuth 2.0, можно добавить регистрации, вход и управление других идентификаторов задач tooyour мобильных и настольных приложений. Эта статья не зависит от языка. В статье hello описывается как toosend и получать сообщения HTTP без использования все библиотеки с открытым исходным кодом.

<!-- TODO: Need link toolibraries -->

Описывается Hello потока кода авторизации OAuth 2.0 в [раздел 4.1 спецификации OAuth 2.0 hello](http://tools.ietf.org/html/rfc6749). Его можно использовать для проверки подлинности и авторизации в большинстве типов приложений, включая [веб-приложения](active-directory-b2c-apps.md#web-apps) и [изначально установленные приложения](active-directory-b2c-apps.md#mobile-and-native-apps). Можно использовать hello получить toosecurely потока кода авторизации OAuth 2.0 *маркеры доступа* для приложений, которые могут быть используется tooaccess ресурсы, которые защищены с помощью [сервер авторизации](active-directory-b2c-reference-protocols.md#the-basics).

Эта статья посвящена hello **открытый клиентов** потока кода авторизации OAuth 2.0. Открытый клиент — это любое клиентское приложение, которое не может быть доверенным toosecurely целостность hello секретного пароля. Сюда входят мобильных приложений, классических приложениях и сущности, любое приложение, выполняется на устройстве, которому требуется tooget маркеры доступа. 

> [!NOTE]
> tooadd identity management tooa веб-приложения с помощью Azure AD B2C используйте [OpenID Connect](active-directory-b2c-reference-oidc.md) вместо OAuth 2.0.

Azure AD B2C расширяет стандарт hello потоков OAuth 2.0 toodo больше, чем простой проверки подлинности и авторизации. Он представляет hello [параметра политики](active-directory-b2c-reference-policies.md). С помощью встроенных политик можно использовать tooadd взаимодействие с пользователем; tooyour приложения, такие как OAuth 2.0 регистрации, вход и управление профилями пользователей. В этой статье мы покажем, как toouse OAuth 2.0 и политики tooimplement, каждый из них возникает в машинном коде приложения. Мы также показано, как tooget токены доступа для доступа к веб-API.

В запросах HTTP пример hello в этой статье, мы используем наш каталог Azure AD B2C образцов, **fabrikamb2c.onmicrosoft.com**. а также наши примеры приложения и политик. Попробуйте hello запросы вручную с помощью этих значений или их можно заменить собственные значения.
Узнайте, каким образом слишком[собственного каталога Azure AD B2C, приложения и политики](#use-your-own-azure-ad-b2c-directory).

## <a name="1-get-an-authorization-code"></a>1. Получение кода авторизации
поток authorization code Hello начинается с клиента hello направления hello пользователя toohello `/authorize` конечной точки. Это hello интерактивную часть потока hello, где hello пользователь предпринимает действия. В этом запросе hello клиент указывает в hello `scope` параметр hello разрешения, необходимость tooacquire от пользователя hello. В hello `p` параметра, он указывает tooexecute политики hello. Hello следующих трех примерах (с разбиением на строки для удобства чтения) каждого с помощью другой политики.

### <a name="use-a-sign-in-policy"></a>Пример с политикой входа в систему
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Пример с политикой регистрации
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Пример с политикой изменения профиля
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| Параметр | Обязательный? | Описание |
| --- | --- | --- |
| client_id |Обязательно |Идентификатор приложения Hello назначен tooyour приложения hello [портал Azure](https://portal.azure.com). |
| response_type |Обязательно |Тип ответа Hello, который должен включать `code` для потока кода авторизации hello. |
| redirect_uri |Обязательно |URI приложения, где запросы проверки подлинности отправляемых и получаемых приложением перенаправления Hello. Его должен точно соответствовать одно перенаправление hello URI, которые зарегистрированы в портале hello, за исключением того, он должен быть в кодировке URL. |
| scope |Обязательно |Список областей с разделителями-пробелами. Значение одной области указывает tooAzure Active Directory (Azure AD) обоих hello разрешений, которые запрашиваются. С помощью клиента hello идентификатор как область hello указывает, что приложение должно маркер доступа, который можно использовать для собственных служб или веб-API, представленный hello же идентификатор клиента.  Hello `offline_access` области показывает, что приложение требует токен обновления для tooresources долгоживущие доступа. Также можно использовать hello `openid` toorequest область маркер идентификатора из Azure AD B2C. |
| response_mode |Рекомендуется |метод Hello использовать назад tooyour toosend hello полученный авторизации кода приложения. Он может иметь значение `query`, `form_post` или `fragment`. |
| state |Рекомендуется |Значение, включенных в запрос hello, возвращаемых в ответ на токен hello. Он может быть строка любое содержимое, которое следует toouse. Как правило, используется случайный уникальное значение, tooprevent атак с подделкой межсайтовых запросов. состояние Hello также является используется tooencode сведения о состоянии пользователя hello в приложение hello, до возникновения hello запрос проверки подлинности. Например пользователь hello hello страницы на или hello политики, который выполнялся. |
| p |Обязательно |политика Hello, выполняется. Он является hello имя политики, которая создается в каталоге Azure AD B2C. Имя политики Hello значение должна начинаться с **b2c\_1\_**. в разделе toolearn о политиках, [встроенных политик Azure AD B2C](active-directory-b2c-reference-policies.md). |
| prompt |Необязательно |Тип Hello это требует взаимодействия с пользователем. В настоящее время является единственным допустимым значением hello `login`, который принудительно hello пользователя tooenter свои учетные данные для этого запроса. Единый вход не сработает. |

На этом этапе hello пользователя запрашивается toocomplete hello политики рабочего процесса. Это может вызвать hello пользователь вводит свое имя пользователя и пароль, вход удостоверений из социальных сетей, зарегистрировавшись для каталога hello или любое другое число шагов. Действие пользователя зависит от того, как определяется политика hello.

После завершения политики hello hello пользователя Azure AD возвращает приложении tooyour ответа hello значения, используемые для `redirect_uri`. Она использует hello метода, указанного в hello `response_mode` параметра. Hello ответа ровно hello же для каждого hello действия сценариев пользователя, независимо от политики hello, который был выполнен.

Успешный ответ с использованием метода `response_mode=query` выглядит следующим образом:

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| Параметр | Описание |
| --- | --- |
| Код |Здравствуйте, приложение hello запрошенный код авторизации. приложение Hello можно использовать toorequest код авторизации hello маркер доступа для целевого ресурса. Срок действия кодов авторизации крайне мал. и обычно истекает по прошествии порядка 10 минут. |
| state |В разделе hello полное описание в таблице hello в предшествующих раздел hello. Если `state` параметр включен в запрос hello hello же значение должно содержаться в ответе hello. Hello приложения следует убедиться, что hello `state` значения в hello запроса и ответа идентичны. |

Сообщения об ошибках могут отправляться также toohello URI перенаправления, чтобы hello приложение может обрабатывать их соответствующим образом:

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| Параметр | Описание |
| --- | --- |
| error |Строка кода ошибки, который можно использовать типы hello tooclassify возникающие ошибки. Также можно использовать tooerrors tooreact строку hello. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello. |
| state |См. полное описание hello в предшествующей таблице hello. Если `state` параметр включен в запрос hello hello же значение должно содержаться в ответе hello. Hello приложения следует убедиться, что hello `state` значения в hello запроса и ответа идентичны. |

## <a name="2-get-a-token"></a>2. Получение маркера
Теперь, когда вы получили код авторизации, можно активировать hello `code` для токена toohello ресурсов, отправив запрос POST toohello `/token` конечной точки. В Azure AD B2C hello только ресурсов, можно запросить маркер является серверной части приложения собственных веб-API. Hello соглашение, которое используется для запроса маркера tooyourself имеет идентификатор клиента приложения hello областью toouse:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| Параметр | Обязательный? | Описание |
| --- | --- | --- |
| p |Обязательно |Здравствуйте, политики, которая была используется tooacquire hello авторизации кода. Другую политику в этом запросе использовать нельзя. Обратите внимание, что вы добавить toohello этот параметр *строку запроса*, а не в hello тело POST. |
| client_id |Обязательно |Идентификатор приложения Hello назначен tooyour приложения hello [портал Azure](https://portal.azure.com). |
| grant_type |Обязательно |Hello тип используемого предоставления прав. Для потока кода авторизации hello, должен быть тип предоставления hello `authorization_code`. |
| scope |Рекомендуется |Список областей с разделителями-пробелами. Значение одной области указывает tooAzure AD обоих hello разрешений, которые запрашиваются. С помощью клиента hello идентификатор как область hello указывает, что приложение должно маркер доступа, который можно использовать для собственных служб или веб-API, представленный hello же идентификатор клиента.  Hello `offline_access` области показывает, что приложение требует токен обновления для tooresources долгоживущие доступа.  Также можно использовать hello `openid` toorequest область маркер идентификатора из Azure AD B2C. |
| Код |Обязательно |Код авторизации Hello, полученному в первый участок потока hello hello. |
| redirect_uri |Обязательно |URI приложения hello, которого вы получили код авторизации hello перенаправления Hello. |

Успешный ответ маркера выглядит следующим образом:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Параметр | Описание |
| --- | --- |
| not_before |время Hello, на какие hello считается действительным, во время эпохи маркер. |
| token_type |значение типа токена Hello. Hello вводить только что поддерживает Azure AD является носителя. |
| access_token |Hello подпись JSON Web Token (JWT) по запросу. |
| scope |Hello областям hello маркер является допустимым для. Также можно использовать токены toocache областей для последующего использования. |
| expires_in |Hello продолжительность hello маркер является допустимым (в секундах). |
| refresh_token |Маркер обновления OAuth 2.0. приложение Hello можно использовать этот токен tooacquire дополнительные маркеры, после истечения срока действия текущего маркера hello. Маркеры обновления имеют большой срок действия. Их tooresources tooretain доступа можно использовать на длительное время. Дополнительные сведения см. в разделе hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md). |

Сообщения об ошибках выглядят следующим образом:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Параметр | Описание |
| --- | --- |
| error |Строка кода ошибки, который можно использовать типы hello tooclassify возникающие ошибки. Также можно использовать tooerrors tooreact строку hello. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello. |

## <a name="3-use-hello-token"></a>3. Использование маркера hello
Теперь, когда вы успешно получили маркер доступа, можно использовать токен hello в запросы tooyour серверной части веб-API, включив его в hello `Authorization` заголовка:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4. Обновление маркера hello
Срок действия маркеров доступа и маркеров идентификации крайне мал. После истечения срока их действия, необходимо обновить их toocontinue tooaccess ресурсов. toodo, отправить другой toohello запрос POST `/token` конечной точки. На этот раз укажите hello `refresh_token` вместо hello `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| Параметр | Обязательный? | Описание |
| --- | --- | --- |
| p |Обязательно |политика Hello, исходный токен обновления используется tooacquire hello. Другую политику в этом запросе использовать нельзя. Обратите внимание, что вы добавить toohello этот параметр *строку запроса*, а не в hello тело POST. |
| client_id |Рекомендуется |Идентификатор приложения Hello назначен tooyour приложения hello [портал Azure](https://portal.azure.com). |
| grant_type |Обязательно |Hello тип используемого предоставления прав. Для этого участок потока кода авторизации hello должен быть тип предоставления hello `refresh_token`. |
| scope |Рекомендуется |Список областей с разделителями-пробелами. Значение одной области указывает tooAzure AD обоих hello разрешений, которые запрашиваются. С помощью клиента hello идентификатор как область hello указывает, что приложение должно маркер доступа, который можно использовать для собственных служб или веб-API, представленный hello же идентификатор клиента.  Hello `offline_access` область показывает, что вашему приложению потребуется токен обновления для tooresources долгоживущие доступа.  Также можно использовать hello `openid` toorequest область маркер идентификатора из Azure AD B2C. |
| redirect_uri |Необязательно |URI приложения hello, которого вы получили код авторизации hello перенаправления Hello. |
| refresh_token |Обязательно |Hello исходный токен обновления, полученному в hello второго участка hello потока. |

Успешный ответ маркера выглядит следующим образом:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Параметр | Описание |
| --- | --- |
| not_before |время Hello, на какие hello считается действительным, во время эпохи маркер. |
| token_type |значение типа токена Hello. Hello вводить только что поддерживает Azure AD является носителя. |
| access_token |Hello подпись JWT по запросу. |
| scope |Hello областям hello маркер является допустимым для. Также можно использовать токены toocache hello областей для последующего использования. |
| expires_in |Hello продолжительность hello маркер является допустимым (в секундах). |
| refresh_token |Маркер обновления OAuth 2.0. приложение Hello можно использовать этот токен tooacquire дополнительные маркеры, после истечения срока действия текущего маркера hello. Обновить долгоживущие токены и может быть tooresources доступа используется tooretain на длительное время. Дополнительные сведения см. в разделе hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md). |

Сообщения об ошибках выглядят следующим образом:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Параметр | Описание |
| --- | --- |
| error |Строка кода ошибки, который можно использовать типы tooclassify возникающие ошибки. Также можно использовать tooerrors tooreact строку hello. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello. |

## <a name="use-your-own-azure-ad-b2c-directory"></a>Использование собственного каталога Azure AD B2C
tootry эти запросы самостоятельно, полный hello следующие шаги. Замените hello примеры значений, которые были использованы в этой статье собственными значениями.

1. [Создайте каталог Azure AD B2C](active-directory-b2c-get-started.md). Используйте hello имя каталога в запросах hello.
2. [Создание приложения](active-directory-b2c-app-registration.md) tooobtain идентификатора приложения и URI перенаправления. Включите собственный клиент в приложение.
3. [Создание политик](active-directory-b2c-reference-policies.md) tooobtain имена ваших политики.

