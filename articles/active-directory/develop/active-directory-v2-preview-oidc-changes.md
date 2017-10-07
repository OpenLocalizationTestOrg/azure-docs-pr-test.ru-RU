---
title: "Конечная точка v2.0 toohello Azure AD aaaChanges | Документы Microsoft"
description: "Описание изменений, которые были сделаны toohello приложения модель v2.0 общедоступной предварительной версии протоколов."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a>Важные обновления toohello v2.0 протоколы проверки подлинности
Вниманию разработчиков! Через hello следующих двух недель, мы будут осуществлять несколько обновлений протоколов проверки подлинности v2.0 tooour, может означать критические изменения для любого приложения, написанного время нашей предварительной версии.  

## <a name="who-does-this-affect"></a>Приложения, на которые повлияют обновления
Все приложения, которые были записаны toouse hello v2.0 схождение выполнено конечную точку проверки подлинности,

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

Можно найти дополнительные сведения о конечной точке v2.0 hello [здесь](active-directory-appmodel-v2-overview.md).

Если вы создавали приложения с помощью конечной точки v2.0 hello, задавая в коде непосредственно протокола toohello v2.0 любым из наших OpenID Connect или OAuth web middlewares или с помощью других сторонних производителей библиотеки tooperform для проверки подлинности, вы должны быть подготовлены tootest проекты и внести необходимые изменения.

## <a name="who-doesnt-this-affect"></a>Приложения, на которые не повлияют обновления
Все приложения, которые были записаны для конечной точки проверки подлинности Azure AD рабочей hello

```
https://login.microsoftonline.com/common/oauth2/authorize
```

Этот протокол окончательный и не подлежит изменению.

Кроме того Если приложение **только** использует нашей tooperform библиотека ADAL проверку подлинности, должен быть toochange.  ADAL экранированный приложения от изменений hello.  

## <a name="what-are-hello-changes"></a>Что такое hello изменения?
### <a name="removing-hello-x5t-value-from-jwt-headers"></a>Удаление значения x5t hello из заголовков JWT
Конечная точка v2.0 Hello токенов JWT широко используются, который содержит параметры заголовок с соответствующие метаданные о токене hello.  При декодировании hello заголовок одного из наших текущего JWT необходимо найти примерно так:

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Где оба свойства «x5t» и «kid» hello определить hello открытого ключа, должен быть используется toovalidate hello маркер подписи, как получить из конечной точки метаданных OpenID Connect hello.

Hello изменений, которые мы выполняем здесь — свойство tooremove hello «x5t».  Вы можете продолжить hello toouse же механизмы toovalidate токены, но следует полагаться только на hello «kid» свойство tooretrieve hello правильный открытый ключ, как указано в hello протокола OpenID Connect. 

> [!IMPORTANT]
> **Задание: Убедитесь, что приложение не зависит от существования hello hello x5t значение.**
> 
> 

### <a name="removing-profileinfo"></a>Удаление profile_info
Ранее, конечная точка v2.0 hello возврат объекта JSON в кодировке base64 в токен ответов под названием `profile_info`.  При запросе маркера доступа из конечной точки v2.0 hello, отправляя запрос на:

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

Hello ответа выглядит следующим образом hello следующий объект JSON.

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Hello `profile_info` значение, содержащееся сведения о пользователе hello, вход в приложение hello - их отображаемое имя, имя, фамилию, адрес электронной почты, идентификатор и т. д.  В первую очередь, hello `profile_info` было использовано для кэширования токенов и в целях отображения.

Теперь мы удаляем hello `profile_info` значение, но не беспокойтесь, мы предоставляем по-прежнему toodevelopers этой информации в несколько разных местах.  Вместо `profile_info`, конечная точка v2.0 hello вернет `id_token` в ответ на каждый токен:

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Может декодировать и анализировать hello id_token tooretrieve hello же сведения, полученные от profile_info.  Hello id_token является JSON Web Token (JWT), с содержимым в соответствии с OpenID Connect.  Hello код для этого должен быть подобен — необходимо просто tooextract hello среднего сегмента (hello тела) hello id_token и base64 декодировать tooaccess hello JSON-объект в пределах.

Через hello следующих двух недель, следует создавать приложения tooretrieve hello сведения о пользователе из либо hello `id_token` или `profile_info`; какое значение присутствует.  Таким образом, при внесении изменений hello, приложение легко может обрабатывать hello переход из `profile_info` слишком`id_token` без прерывания.

> [!IMPORTANT]
> **Задание: Убедитесь, что приложение не зависит от существования hello hello `profile_info` значение.**
> 
> 

### <a name="removing-idtokenexpiresin"></a>Удаление id_token_expires_in
Аналогичные слишком`profile_info`, кроме того, мы удаляем hello `id_token_expires_in` параметра из ответов.  Ранее, возвращает значение для конечной точки v2.0 hello `id_token_expires_in` вместе с каждый ответ id_token, например в ответе авторизовать:

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

Или в ответе маркера:

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

Hello `id_token_expires_in` значение означает hello количество секунд, остается действительным для hello id_token.  Теперь мы удаляем hello `id_token_expires_in` значение полностью.  Вместо этого можно использовать стандартный OpenID Connect hello `nbf` и `exp` утверждений допустимость hello tooexamine id_token.  В разделе hello [ссылку на маркер v2.0](active-directory-v2-tokens.md) Дополнительные сведения об этих утверждений.

> [!IMPORTANT]
> **Задание: Убедитесь, что приложение не зависит от существования hello hello `id_token_expires_in` значение.**
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a>Изменение hello утверждений, возвращенную область = openid
Это изменение будет наиболее значимых hello на самом деле, это повлияет на почти в каждом приложении, которое использует конечную точку v2.0 hello.  Многие приложения отправки запросов toohello v2.0 конечную точку с помощью hello `openid` области, например:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

Сегодня, когда hello пользователь дает согласие hello `openid` области, приложение получит множество сведений о пользователе hello в hello, возникающие в id_token.  В этих утверждениях может содержаться его имя, предпочтительное имя пользователя, адрес электронной почты, идентификатор объекта и многое другое.

В этом обновлении мы изменяем сведения hello, hello `openid` область позволяет вашему приложению доступ к toobetter comform с hello спецификация OpenID Connect.  Hello `openid` область только будет разрешить пользователя hello toosign приложения в, а также получить идентификатор конкретного приложения для пользователя hello в hello `sub` утверждение с правом hello id_token.  Здравствуйте утверждения в id_token с только hello `openid` лишен персональные данные будут предоставлены области.  Примеры утверждений id_token:

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

Если требуется tooobtain персональные данные (PII) о пользователе hello в приложении, вашему приложению потребуется toorequest дополнительные разрешения у пользователя hello.  Мы представляем поддержка две новые области из hello spec OpenID Connect — hello `email` и `profile` областей — позволяющих toodo таким образом.

* Hello `email` область очень проста – он позволяет вашего приложения доступа toohello основной адрес электронной почты пользователя через hello `email` утверждения в hello id_token.  Обратите внимание, что hello `email` утверждения не всегда будут перенесены в id_tokens — он будет включен только при наличии в профиле пользователя hello.
* Hello `profile` область предоставляет доступ вашего приложения tooall другие основные сведения о hello пользователей и их имя, предпочтительным username, идентификатор объекта и т. д.

Это позволяет toocode приложения в режиме минимальной раскрытие — вы можете запросить hello пользователь просто hello набор сведений, что приложение требуется toodo свою работу.  Следует toocontinue начало hello полный набор сведений о пользователях, приложение получает в авторизации запросах следует включать все три области:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

Приложения можно начать отправку hello `email` и `profile` областей немедленно, а конечная точка v2.0 hello будет принимать эти две области и начать запрос разрешений у пользователей при необходимости.  Однако изменить hello в интерпретации hello hello `openid` области не вступят в силу для нескольких недель.

> [!IMPORTANT]
> **Задание: добавить hello `profile` и `email` областей, если вашему приложению требуется сведения о пользователе hello.**  Обратите внимание, что при использовании ADAL эти разрешения запрашиваются по умолчанию. 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a>Удаление hello издателя косой чертой.
Ранее значение издателя hello, которое появляется в маркерах из конечной точки v2.0 hello заняло hello формы

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

Где hello guid был hello tenantId клиента hello Azure AD, который выдал токен hello.  Эти изменения становится значение издателя hello

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

в оба маркера и в документе обнаружения OpenID Connect hello.

> [!IMPORTANT]
> **Задание: Убедитесь, что приложение принимает значение издателя hello как с и без косую черту в конце во время проверки издателя.**
> 
> 

## <a name="why-change"></a>Цель изменений
Hello главной целью введения этих изменений является toobe соответствуют hello Стандартная спецификация OpenID Connect.  Будучи OpenID Connect совместимые, мы надеемся, что toominimize различия между интеграция со службами Microsoft identity и с другими службами удостоверений в отрасли hello.  Мы хотим toouse разработчики tooenable свои избранные открытой библиотеки проверки подлинности без необходимости tooalter hello библиотеки tooaccommodate Microsoft различия.

## <a name="what-can-you-do"></a>Советы разработчикам
На сегодня можно начать выполнять все hello изменений, описанных выше.  Незамедлительно сделайте следующее:

1. **Удалите все зависимости hello `x5t` параметра header.**
2. **Аккуратно hello переход из `profile_info` слишком`id_token` в ответах токена.**
3. **Удалите все зависимости hello `id_token_expires_in` параметр ответа.**
4. **Добавить hello `profile` и `email` приложения tooyour областей, если ваше приложение должно обычного пользователя сведения.**
5. **Настройте принятие значений издателя в маркерах с завершающей косой чертой и без нее.**

Наш [документации по протоколу v2.0](active-directory-v2-protocols.md) уже обновленные tooreflect эти изменения, вы можете использовать его как ссылку в обеспечении обновите ваш код.

При наличии вопросов на hello объем hello изменений вы можете бесплатно tooreach out toous в Twitter с @AzureAD.

## <a name="how-often-will-protocol-changes-occur"></a>Частота изменений протокола
Мы не предусмотрели дальнейшей критические изменения toohello протоколы проверки подлинности.  Мы намеренно объединяете в разных версиях эти изменения, чтобы вы не будете иметь toogo через этот тип процесса обновления снова ближайшее время.  Конечно, мы продолжим toohello функции tooadd v2.0 службы проверки подлинности, можно воспользоваться преимуществом схождение выполнено, но эти изменения должны быть друг к другу и приостановки выполнения существующего кода.

Наконец мы хотели бы toosay Благодарим вас за ознакомление следующее время hello предварительной версии.  аналитики Hello и взаимодействия с нашей первыми были очень полезным в до сих и надеемся, что вы перейдете tooshare мнения и идеи.

Удачного программирования!

Hello отделения удостоверений Майкрософт

