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
# <a name="important-updates-toohello-v20-authentication-protocols"></a><span data-ttu-id="553cf-103">Важные обновления toohello v2.0 протоколы проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="553cf-103">Important Updates toohello v2.0 Authentication Protocols</span></span>
<span data-ttu-id="553cf-104">Вниманию разработчиков!</span><span class="sxs-lookup"><span data-stu-id="553cf-104">Attention developers!</span></span> <span data-ttu-id="553cf-105">Через hello следующих двух недель, мы будут осуществлять несколько обновлений протоколов проверки подлинности v2.0 tooour, может означать критические изменения для любого приложения, написанного время нашей предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="553cf-105">Over hello next two weeks, we will be making a few updates tooour v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="553cf-106">Приложения, на которые повлияют обновления</span><span class="sxs-lookup"><span data-stu-id="553cf-106">Who does this affect?</span></span>
<span data-ttu-id="553cf-107">Все приложения, которые были записаны toouse hello v2.0 схождение выполнено конечную точку проверки подлинности,</span><span class="sxs-lookup"><span data-stu-id="553cf-107">Any apps that have been written toouse hello v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="553cf-108">Можно найти дополнительные сведения о конечной точке v2.0 hello [здесь](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="553cf-108">More information on hello v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="553cf-109">Если вы создавали приложения с помощью конечной точки v2.0 hello, задавая в коде непосредственно протокола toohello v2.0 любым из наших OpenID Connect или OAuth web middlewares или с помощью других сторонних производителей библиотеки tooperform для проверки подлинности, вы должны быть подготовлены tootest проекты и внести необходимые изменения.</span><span class="sxs-lookup"><span data-stu-id="553cf-109">If you have built an app using hello v2.0 endpoint by coding directly toohello v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries tooperform authentication, you should be prepared tootest your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="553cf-110">Приложения, на которые не повлияют обновления</span><span class="sxs-lookup"><span data-stu-id="553cf-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="553cf-111">Все приложения, которые были записаны для конечной точки проверки подлинности Azure AD рабочей hello</span><span class="sxs-lookup"><span data-stu-id="553cf-111">Any apps that have been written against hello production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="553cf-112">Этот протокол окончательный и не подлежит изменению.</span><span class="sxs-lookup"><span data-stu-id="553cf-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="553cf-113">Кроме того Если приложение **только** использует нашей tooperform библиотека ADAL проверку подлинности, должен быть toochange.</span><span class="sxs-lookup"><span data-stu-id="553cf-113">Furthermore, if your app **only** uses our ADAL library tooperform authentication, you won\`t have toochange anything.</span></span>  <span data-ttu-id="553cf-114">ADAL экранированный приложения от изменений hello.</span><span class="sxs-lookup"><span data-stu-id="553cf-114">ADAL has shielded your app from hello changes.</span></span>  

## <a name="what-are-hello-changes"></a><span data-ttu-id="553cf-115">Что такое hello изменения?</span><span class="sxs-lookup"><span data-stu-id="553cf-115">What are hello changes?</span></span>
### <a name="removing-hello-x5t-value-from-jwt-headers"></a><span data-ttu-id="553cf-116">Удаление значения x5t hello из заголовков JWT</span><span class="sxs-lookup"><span data-stu-id="553cf-116">Removing hello x5t value from JWT headers</span></span>
<span data-ttu-id="553cf-117">Конечная точка v2.0 Hello токенов JWT широко используются, который содержит параметры заголовок с соответствующие метаданные о токене hello.</span><span class="sxs-lookup"><span data-stu-id="553cf-117">hello v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about hello token.</span></span>  <span data-ttu-id="553cf-118">При декодировании hello заголовок одного из наших текущего JWT необходимо найти примерно так:</span><span class="sxs-lookup"><span data-stu-id="553cf-118">If you decode hello header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="553cf-119">Где оба свойства «x5t» и «kid» hello определить hello открытого ключа, должен быть используется toovalidate hello маркер подписи, как получить из конечной точки метаданных OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="553cf-119">Where both hello "x5t" and "kid" properties identify hello public key that should be used toovalidate hello token\`s signature, as retrieved from hello OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="553cf-120">Hello изменений, которые мы выполняем здесь — свойство tooremove hello «x5t».</span><span class="sxs-lookup"><span data-stu-id="553cf-120">hello change we are making here is tooremove hello "x5t" property.</span></span>  <span data-ttu-id="553cf-121">Вы можете продолжить hello toouse же механизмы toovalidate токены, но следует полагаться только на hello «kid» свойство tooretrieve hello правильный открытый ключ, как указано в hello протокола OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="553cf-121">You may continue toouse hello same mechanisms toovalidate tokens, but should rely only on hello "kid" property tooretrieve hello correct public key, as specified in hello OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="553cf-122">**Задание: Убедитесь, что приложение не зависит от существования hello hello x5t значение.**</span><span class="sxs-lookup"><span data-stu-id="553cf-122">**Your job: Make sure your app does not depend on hello existence of hello x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="553cf-123">Удаление profile_info</span><span class="sxs-lookup"><span data-stu-id="553cf-123">Removing profile_info</span></span>
<span data-ttu-id="553cf-124">Ранее, конечная точка v2.0 hello возврат объекта JSON в кодировке base64 в токен ответов под названием `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="553cf-124">Previously, hello v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="553cf-125">При запросе маркера доступа из конечной точки v2.0 hello, отправляя запрос на:</span><span class="sxs-lookup"><span data-stu-id="553cf-125">When requesting an access token from hello v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="553cf-126">Hello ответа выглядит следующим образом hello следующий объект JSON.</span><span class="sxs-lookup"><span data-stu-id="553cf-126">hello response would look like hello following JSON object:</span></span>

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

<span data-ttu-id="553cf-127">Hello `profile_info` значение, содержащееся сведения о пользователе hello, вход в приложение hello - их отображаемое имя, имя, фамилию, адрес электронной почты, идентификатор и т. д.</span><span class="sxs-lookup"><span data-stu-id="553cf-127">hello `profile_info` value contained information about hello user who signed into hello app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="553cf-128">В первую очередь, hello `profile_info` было использовано для кэширования токенов и в целях отображения.</span><span class="sxs-lookup"><span data-stu-id="553cf-128">Primarily, hello `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="553cf-129">Теперь мы удаляем hello `profile_info` значение, но не беспокойтесь, мы предоставляем по-прежнему toodevelopers этой информации в несколько разных местах.</span><span class="sxs-lookup"><span data-stu-id="553cf-129">We are now removing hello `profile_info` value – but don't worry, we are still providing this information toodevelopers in a slightly different place.</span></span>  <span data-ttu-id="553cf-130">Вместо `profile_info`, конечная точка v2.0 hello вернет `id_token` в ответ на каждый токен:</span><span class="sxs-lookup"><span data-stu-id="553cf-130">Instead of `profile_info`, hello v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="553cf-131">Может декодировать и анализировать hello id_token tooretrieve hello же сведения, полученные от profile_info.</span><span class="sxs-lookup"><span data-stu-id="553cf-131">You may decode and parse hello id_token tooretrieve hello same information that you received from profile_info.</span></span>  <span data-ttu-id="553cf-132">Hello id_token является JSON Web Token (JWT), с содержимым в соответствии с OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="553cf-132">hello id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="553cf-133">Hello код для этого должен быть подобен — необходимо просто tooextract hello среднего сегмента (hello тела) hello id_token и base64 декодировать tooaccess hello JSON-объект в пределах.</span><span class="sxs-lookup"><span data-stu-id="553cf-133">hello code for doing so should be very similar – you simply need tooextract hello middle segment (hello body) of hello id_token and base64 decode it tooaccess hello JSON object within.</span></span>

<span data-ttu-id="553cf-134">Через hello следующих двух недель, следует создавать приложения tooretrieve hello сведения о пользователе из либо hello `id_token` или `profile_info`; какое значение присутствует.</span><span class="sxs-lookup"><span data-stu-id="553cf-134">Over hello next two weeks, you should code your app tooretrieve hello user information from either hello `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="553cf-135">Таким образом, при внесении изменений hello, приложение легко может обрабатывать hello переход из `profile_info` слишком`id_token` без прерывания.</span><span class="sxs-lookup"><span data-stu-id="553cf-135">That way when hello change is made, your app can seamlessly handle hello transition from `profile_info` too`id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="553cf-136">**Задание: Убедитесь, что приложение не зависит от существования hello hello `profile_info` значение.**</span><span class="sxs-lookup"><span data-stu-id="553cf-136">**Your job: Make sure your app does not depend on hello existence of hello `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="553cf-137">Удаление id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="553cf-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="553cf-138">Аналогичные слишком`profile_info`, кроме того, мы удаляем hello `id_token_expires_in` параметра из ответов.</span><span class="sxs-lookup"><span data-stu-id="553cf-138">Similar too`profile_info`, we are also removing hello `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="553cf-139">Ранее, возвращает значение для конечной точки v2.0 hello `id_token_expires_in` вместе с каждый ответ id_token, например в ответе авторизовать:</span><span class="sxs-lookup"><span data-stu-id="553cf-139">Previously, hello v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="553cf-140">Или в ответе маркера:</span><span class="sxs-lookup"><span data-stu-id="553cf-140">Or in a token response:</span></span>

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

<span data-ttu-id="553cf-141">Hello `id_token_expires_in` значение означает hello количество секунд, остается действительным для hello id_token.</span><span class="sxs-lookup"><span data-stu-id="553cf-141">hello `id_token_expires_in` value would indicate hello number of seconds hello id_token would remain valid for.</span></span>  <span data-ttu-id="553cf-142">Теперь мы удаляем hello `id_token_expires_in` значение полностью.</span><span class="sxs-lookup"><span data-stu-id="553cf-142">Now, we are removing hello `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="553cf-143">Вместо этого можно использовать стандартный OpenID Connect hello `nbf` и `exp` утверждений допустимость hello tooexamine id_token.</span><span class="sxs-lookup"><span data-stu-id="553cf-143">Instead, you may use hello OpenID Connect standard `nbf` and `exp` claims tooexamine hello validity of an id_token.</span></span>  <span data-ttu-id="553cf-144">В разделе hello [ссылку на маркер v2.0](active-directory-v2-tokens.md) Дополнительные сведения об этих утверждений.</span><span class="sxs-lookup"><span data-stu-id="553cf-144">See hello [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="553cf-145">**Задание: Убедитесь, что приложение не зависит от существования hello hello `id_token_expires_in` значение.**</span><span class="sxs-lookup"><span data-stu-id="553cf-145">**Your job: Make sure your app does not depend on hello existence of hello `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a><span data-ttu-id="553cf-146">Изменение hello утверждений, возвращенную область = openid</span><span class="sxs-lookup"><span data-stu-id="553cf-146">Changing hello claims returned by scope=openid</span></span>
<span data-ttu-id="553cf-147">Это изменение будет наиболее значимых hello на самом деле, это повлияет на почти в каждом приложении, которое использует конечную точку v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="553cf-147">This change will be hello most significant – in fact, it will affect almost every app that uses hello v2.0 endpoint.</span></span>  <span data-ttu-id="553cf-148">Многие приложения отправки запросов toohello v2.0 конечную точку с помощью hello `openid` области, например:</span><span class="sxs-lookup"><span data-stu-id="553cf-148">Many applications send requests toohello v2.0 endpoint using hello `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="553cf-149">Сегодня, когда hello пользователь дает согласие hello `openid` области, приложение получит множество сведений о пользователе hello в hello, возникающие в id_token.</span><span class="sxs-lookup"><span data-stu-id="553cf-149">Today, when hello user grants consent for hello `openid` scope, your app receives a wealth of information about hello user in hello resulting id_token.</span></span>  <span data-ttu-id="553cf-150">В этих утверждениях может содержаться его имя, предпочтительное имя пользователя, адрес электронной почты, идентификатор объекта и многое другое.</span><span class="sxs-lookup"><span data-stu-id="553cf-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="553cf-151">В этом обновлении мы изменяем сведения hello, hello `openid` область позволяет вашему приложению доступ к toobetter comform с hello спецификация OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="553cf-151">In this update, we are changing hello information that hello `openid` scope affords your app access to, toobetter comform with hello OpenID Connect specification.</span></span>  <span data-ttu-id="553cf-152">Hello `openid` область только будет разрешить пользователя hello toosign приложения в, а также получить идентификатор конкретного приложения для пользователя hello в hello `sub` утверждение с правом hello id_token.</span><span class="sxs-lookup"><span data-stu-id="553cf-152">hello `openid` scope will only allow your app toosign hello user in, and receive an app-specific identifier for hello user in hello `sub` claim of hello id_token.</span></span>  <span data-ttu-id="553cf-153">Здравствуйте утверждения в id_token с только hello `openid` лишен персональные данные будут предоставлены области.</span><span class="sxs-lookup"><span data-stu-id="553cf-153">hello claims in an id_token with only hello `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="553cf-154">Примеры утверждений id_token:</span><span class="sxs-lookup"><span data-stu-id="553cf-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="553cf-155">Если требуется tooobtain персональные данные (PII) о пользователе hello в приложении, вашему приложению потребуется toorequest дополнительные разрешения у пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="553cf-155">If you want tooobtain personally identifiable information (PII) about hello user in your app, your app will need toorequest additional permissions from hello user.</span></span>  <span data-ttu-id="553cf-156">Мы представляем поддержка две новые области из hello spec OpenID Connect — hello `email` и `profile` областей — позволяющих toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="553cf-156">We are introducing support for two new scopes from hello OpenID Connect spec – hello `email` and `profile` scopes – which allow you toodo so.</span></span>

* <span data-ttu-id="553cf-157">Hello `email` область очень проста – он позволяет вашего приложения доступа toohello основной адрес электронной почты пользователя через hello `email` утверждения в hello id_token.</span><span class="sxs-lookup"><span data-stu-id="553cf-157">hello `email` scope is very straightforward – it allows your app access toohello user's primary email address via hello `email` claim in hello id_token.</span></span>  <span data-ttu-id="553cf-158">Обратите внимание, что hello `email` утверждения не всегда будут перенесены в id_tokens — он будет включен только при наличии в профиле пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="553cf-158">Note that hello `email` claim will not always be present in id_tokens – it will only be included if available in hello user's profile.</span></span>
* <span data-ttu-id="553cf-159">Hello `profile` область предоставляет доступ вашего приложения tooall другие основные сведения о hello пользователей и их имя, предпочтительным username, идентификатор объекта и т. д.</span><span class="sxs-lookup"><span data-stu-id="553cf-159">hello `profile` scope affords your app access tooall other basic information about hello user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="553cf-160">Это позволяет toocode приложения в режиме минимальной раскрытие — вы можете запросить hello пользователь просто hello набор сведений, что приложение требуется toodo свою работу.</span><span class="sxs-lookup"><span data-stu-id="553cf-160">This allows you toocode your app in a minimal-disclosure fashion – you can ask hello user for just hello set of information that your app requires toodo its job.</span></span>  <span data-ttu-id="553cf-161">Следует toocontinue начало hello полный набор сведений о пользователях, приложение получает в авторизации запросах следует включать все три области:</span><span class="sxs-lookup"><span data-stu-id="553cf-161">If you want toocontinue getting hello full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="553cf-162">Приложения можно начать отправку hello `email` и `profile` областей немедленно, а конечная точка v2.0 hello будет принимать эти две области и начать запрос разрешений у пользователей при необходимости.</span><span class="sxs-lookup"><span data-stu-id="553cf-162">Your app can begin sending hello `email` and `profile` scopes immediately, and hello v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="553cf-163">Однако изменить hello в интерпретации hello hello `openid` области не вступят в силу для нескольких недель.</span><span class="sxs-lookup"><span data-stu-id="553cf-163">However, hello change in hello interpretation of hello `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="553cf-164">**Задание: добавить hello `profile` и `email` областей, если вашему приложению требуется сведения о пользователе hello.**</span><span class="sxs-lookup"><span data-stu-id="553cf-164">**Your job: Add hello `profile` and `email` scopes if your app requires information about hello user.**</span></span>  <span data-ttu-id="553cf-165">Обратите внимание, что при использовании ADAL эти разрешения запрашиваются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="553cf-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a><span data-ttu-id="553cf-166">Удаление hello издателя косой чертой.</span><span class="sxs-lookup"><span data-stu-id="553cf-166">Removing hello issuer trailing slash.</span></span>
<span data-ttu-id="553cf-167">Ранее значение издателя hello, которое появляется в маркерах из конечной точки v2.0 hello заняло hello формы</span><span class="sxs-lookup"><span data-stu-id="553cf-167">Previously, hello issuer value that appears in tokens from hello v2.0 endpoint took hello form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="553cf-168">Где hello guid был hello tenantId клиента hello Azure AD, который выдал токен hello.</span><span class="sxs-lookup"><span data-stu-id="553cf-168">Where hello guid was hello tenantId of hello Azure AD tenant which issued hello token.</span></span>  <span data-ttu-id="553cf-169">Эти изменения становится значение издателя hello</span><span class="sxs-lookup"><span data-stu-id="553cf-169">With these changes, hello issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="553cf-170">в оба маркера и в документе обнаружения OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="553cf-170">in both tokens and in hello OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="553cf-171">**Задание: Убедитесь, что приложение принимает значение издателя hello как с и без косую черту в конце во время проверки издателя.**</span><span class="sxs-lookup"><span data-stu-id="553cf-171">**Your job: Make sure your app accepts hello issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="553cf-172">Цель изменений</span><span class="sxs-lookup"><span data-stu-id="553cf-172">Why change?</span></span>
<span data-ttu-id="553cf-173">Hello главной целью введения этих изменений является toobe соответствуют hello Стандартная спецификация OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="553cf-173">hello primary motivation for introducing these changes is toobe compliant with hello OpenID Connect standard specification.</span></span>  <span data-ttu-id="553cf-174">Будучи OpenID Connect совместимые, мы надеемся, что toominimize различия между интеграция со службами Microsoft identity и с другими службами удостоверений в отрасли hello.</span><span class="sxs-lookup"><span data-stu-id="553cf-174">By being OpenID Connect compliant, we hope toominimize differences between integrating with Microsoft identity services and with other identity services in hello industry.</span></span>  <span data-ttu-id="553cf-175">Мы хотим toouse разработчики tooenable свои избранные открытой библиотеки проверки подлинности без необходимости tooalter hello библиотеки tooaccommodate Microsoft различия.</span><span class="sxs-lookup"><span data-stu-id="553cf-175">We want tooenable developers toouse their favorite open source authentication libraries without having tooalter hello libraries tooaccommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="553cf-176">Советы разработчикам</span><span class="sxs-lookup"><span data-stu-id="553cf-176">What can you do?</span></span>
<span data-ttu-id="553cf-177">На сегодня можно начать выполнять все hello изменений, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="553cf-177">As of today, you can begin making all of hello changes described above.</span></span>  <span data-ttu-id="553cf-178">Незамедлительно сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="553cf-178">You should immediately:</span></span>

1. <span data-ttu-id="553cf-179">**Удалите все зависимости hello `x5t` параметра header.**</span><span class="sxs-lookup"><span data-stu-id="553cf-179">**Remove any dependencies on hello `x5t` header parameter.**</span></span>
2. <span data-ttu-id="553cf-180">**Аккуратно hello переход из `profile_info` слишком`id_token` в ответах токена.**</span><span class="sxs-lookup"><span data-stu-id="553cf-180">**Gracefully handle hello transition from `profile_info` too`id_token` in token responses.**</span></span>
3. <span data-ttu-id="553cf-181">**Удалите все зависимости hello `id_token_expires_in` параметр ответа.**</span><span class="sxs-lookup"><span data-stu-id="553cf-181">**Remove any dependencies on hello `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="553cf-182">**Добавить hello `profile` и `email` приложения tooyour областей, если ваше приложение должно обычного пользователя сведения.**</span><span class="sxs-lookup"><span data-stu-id="553cf-182">**Add hello `profile` and `email` scopes tooyour app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="553cf-183">**Настройте принятие значений издателя в маркерах с завершающей косой чертой и без нее.**</span><span class="sxs-lookup"><span data-stu-id="553cf-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="553cf-184">Наш [документации по протоколу v2.0](active-directory-v2-protocols.md) уже обновленные tooreflect эти изменения, вы можете использовать его как ссылку в обеспечении обновите ваш код.</span><span class="sxs-lookup"><span data-stu-id="553cf-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated tooreflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="553cf-185">При наличии вопросов на hello объем hello изменений вы можете бесплатно tooreach out toous в Twitter с @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="553cf-185">If you have any further questions on hello scope of hello changes, please feel free tooreach out toous on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="553cf-186">Частота изменений протокола</span><span class="sxs-lookup"><span data-stu-id="553cf-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="553cf-187">Мы не предусмотрели дальнейшей критические изменения toohello протоколы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="553cf-187">We do not foresee any further breaking changes toohello authentication protocols.</span></span>  <span data-ttu-id="553cf-188">Мы намеренно объединяете в разных версиях эти изменения, чтобы вы не будете иметь toogo через этот тип процесса обновления снова ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="553cf-188">We are intentionally bundling these changes into one release so that you won\`t have toogo through this type of update process again any time soon.</span></span>  <span data-ttu-id="553cf-189">Конечно, мы продолжим toohello функции tooadd v2.0 службы проверки подлинности, можно воспользоваться преимуществом схождение выполнено, но эти изменения должны быть друг к другу и приостановки выполнения существующего кода.</span><span class="sxs-lookup"><span data-stu-id="553cf-189">Of course, we will continue tooadd features toohello converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="553cf-190">Наконец мы хотели бы toosay Благодарим вас за ознакомление следующее время hello предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="553cf-190">Lastly, we would like toosay thank you for trying things out during hello preview period.</span></span>  <span data-ttu-id="553cf-191">аналитики Hello и взаимодействия с нашей первыми были очень полезным в до сих и надеемся, что вы перейдете tooshare мнения и идеи.</span><span class="sxs-lookup"><span data-stu-id="553cf-191">hello insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue tooshare your opinions and ideas.</span></span>

<span data-ttu-id="553cf-192">Удачного программирования!</span><span class="sxs-lookup"><span data-stu-id="553cf-192">Happy coding!</span></span>

<span data-ttu-id="553cf-193">Hello отделения удостоверений Майкрософт</span><span class="sxs-lookup"><span data-stu-id="553cf-193">hello Microsoft Identity Division</span></span>

