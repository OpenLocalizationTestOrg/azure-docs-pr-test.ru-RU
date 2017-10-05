---
title: "Изменения в конечной точке Azure AD версии 2.0 | Документация Майкрософт"
description: "Описание изменений, которые будут внесены в протоколы общедоступной предварительной версии модели приложения версии 2.0."
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
ms.openlocfilehash: ae73833a68db14804dc40eaf07ff7d3effaa9052
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="f14be-103">Важные обновления протоколов проверки подлинности версии 2.0</span><span class="sxs-lookup"><span data-stu-id="f14be-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="f14be-104">Вниманию разработчиков!</span><span class="sxs-lookup"><span data-stu-id="f14be-104">Attention developers!</span></span> <span data-ttu-id="f14be-105">В течение следующих двух недель будут внесены некоторые изменения в протоколы проверки подлинности версии 2.0. Это могут быть критические изменения для любых приложений, написанных в течение периода действия предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="f14be-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="f14be-106">Приложения, на которые повлияют обновления</span><span class="sxs-lookup"><span data-stu-id="f14be-106">Who does this affect?</span></span>
<span data-ttu-id="f14be-107">Обновления повлияют на все приложения, которые предусматривают использование объединенной конечной точки проверки подлинности версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="f14be-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="f14be-108">Дополнительные сведения о конечной точке версии 2.0 можно найти [здесь](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f14be-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="f14be-109">Если приложение разработано с использованием конечной точки версии 2.0 путем написания кода непосредственно в протокол версии 2.0, а для проверки подлинности использовалось наше ПО промежуточного слоя (OpenID Connect или OAuth) или другие библиотеки сторонних производителей, понадобится протестировать проекты и, возможно, внести некоторые изменения.</span><span class="sxs-lookup"><span data-stu-id="f14be-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="f14be-110">Приложения, на которые не повлияют обновления</span><span class="sxs-lookup"><span data-stu-id="f14be-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="f14be-111">Обновления не повлияют на все приложения, написанные с помощью конечной точки проверки подлинности рабочей среды Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f14be-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="f14be-112">Этот протокол окончательный и не подлежит изменению.</span><span class="sxs-lookup"><span data-stu-id="f14be-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="f14be-113">Если для проверки подлинности в приложении используется **только** наша библиотека ADAL, вносить изменения также не потребуется.</span><span class="sxs-lookup"><span data-stu-id="f14be-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="f14be-114">При использовании библиотеки ADAL ваше приложение защищено от изменений.</span><span class="sxs-lookup"><span data-stu-id="f14be-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="f14be-115">Изменения</span><span class="sxs-lookup"><span data-stu-id="f14be-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="f14be-116">Удаление значения x5t из заголовков маркера JWT</span><span class="sxs-lookup"><span data-stu-id="f14be-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="f14be-117">Для конечной точки версии 2.0 широко используются маркеры JWT, в которых содержится раздел параметров заголовка с соответствующими метаданными о маркере.</span><span class="sxs-lookup"><span data-stu-id="f14be-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="f14be-118">Если декодировать заголовок текущего маркера JWT, вы увидите нечто вроде этого:</span><span class="sxs-lookup"><span data-stu-id="f14be-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="f14be-119">Здесь свойства x5t и kid определяют открытый ключ, который следует использовать для проверки подписи маркера, полученной из конечной точки метаданных OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f14be-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="f14be-120">Изменение заключается в удалении свойства x5t.</span><span class="sxs-lookup"><span data-stu-id="f14be-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="f14be-121">Вы можете по-прежнему использовать те же механизмы для проверки маркеров, но чтобы получить правильный открытый ключ, следует использовать только значение свойства kid, как указано в протоколе OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f14be-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f14be-122">**Задание. Убедитесь, что работа приложения не зависит от значения x5t.**</span><span class="sxs-lookup"><span data-stu-id="f14be-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="f14be-123">Удаление profile_info</span><span class="sxs-lookup"><span data-stu-id="f14be-123">Removing profile_info</span></span>
<span data-ttu-id="f14be-124">Ранее конечная точка версии 2.0 возвращала объект JSON в кодировке base64 в ответах маркера `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="f14be-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="f14be-125">При запросе маркера доступа из конечной точки версии 2.0 по следующему адресу отправлялся запрос:</span><span class="sxs-lookup"><span data-stu-id="f14be-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="f14be-126">Ответ при этом выглядел как следующий объект JSON:</span><span class="sxs-lookup"><span data-stu-id="f14be-126">The response would look like the following JSON object:</span></span>

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

<span data-ttu-id="f14be-127">В значении `profile_info` содержатся сведения о пользователе, выполнившем вход в приложение, а именно: отображаемое имя, имя, фамилия, адрес электронной почты, идентификатор и т. д.</span><span class="sxs-lookup"><span data-stu-id="f14be-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="f14be-128">`profile_info` преимущественно использовался для кэширования и отображения маркеров.</span><span class="sxs-lookup"><span data-stu-id="f14be-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="f14be-129">Теперь значение `profile_info` удалено. Не волнуйтесь, эти сведения по-прежнему предоставляются разработчикам, но в другом месте.</span><span class="sxs-lookup"><span data-stu-id="f14be-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="f14be-130">Теперь конечная точка версии 2.0 в каждом ответе маркера вместо `profile_info` возвращает `id_token`:</span><span class="sxs-lookup"><span data-stu-id="f14be-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="f14be-131">Чтобы получить сведения, которые ранее содержались в profile_info, можно декодировать id_token и выполнить его синтаксический анализ.</span><span class="sxs-lookup"><span data-stu-id="f14be-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="f14be-132">(id_token — это веб-маркер JSON (JWT) с содержимым, которое указано в OpenID Connect.)</span><span class="sxs-lookup"><span data-stu-id="f14be-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="f14be-133">Сделать это достаточно просто — нужно извлечь средний сегмент (текст) id_token и декодировать его из кодировки base64, чтобы получить доступ к находящемуся в нем объекту JSON.</span><span class="sxs-lookup"><span data-stu-id="f14be-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="f14be-134">В течение следующих двух недель вам необходимо кодировать приложение, чтобы получить сведения о пользователе из `id_token` или `profile_info` (в зависимости от наличия).</span><span class="sxs-lookup"><span data-stu-id="f14be-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="f14be-135">Таким образом после внесения изменений приложение может беспроблемно перейти с `profile_info` на `id_token`, не прекращая работу.</span><span class="sxs-lookup"><span data-stu-id="f14be-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f14be-136">**Задание. Убедитесь, что работа приложения не зависит от наличия значения `profile_info`.**</span><span class="sxs-lookup"><span data-stu-id="f14be-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="f14be-137">Удаление id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="f14be-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="f14be-138">Подобно `profile_info`, из ответов также будет удален параметр `id_token_expires_in`.</span><span class="sxs-lookup"><span data-stu-id="f14be-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="f14be-139">До этого конечная точка версии 2.0 возвращала значение параметра `id_token_expires_in` вместе с каждым ответом id_token, например в ответе авторизации:</span><span class="sxs-lookup"><span data-stu-id="f14be-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="f14be-140">Или в ответе маркера:</span><span class="sxs-lookup"><span data-stu-id="f14be-140">Or in a token response:</span></span>

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

<span data-ttu-id="f14be-141">Значение `id_token_expires_in` указывает количество секунд, в течение которых id_token остается допустимым.</span><span class="sxs-lookup"><span data-stu-id="f14be-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="f14be-142">Теперь значение `id_token_expires_in` будет полностью удалено.</span><span class="sxs-lookup"><span data-stu-id="f14be-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="f14be-143">Чтобы проверить допустимость id_token, вместо него можно использовать стандартные утверждения `nbf` и `exp` OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f14be-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="f14be-144">Дополнительные сведения об этих утверждениях см. [справочнике по маркерам версии 2.0](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="f14be-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f14be-145">**Задание. Убедитесь, что работа приложения не зависит от наличия значения `id_token_expires_in`.**</span><span class="sxs-lookup"><span data-stu-id="f14be-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="f14be-146">Изменение утверждений, возвращенных с помощью области openid</span><span class="sxs-lookup"><span data-stu-id="f14be-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="f14be-147">Это изменение наиболее значимое, так как оно повлияет практически на все приложения, использующие конечную точку версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="f14be-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="f14be-148">Многие приложения отправляют запросы в конечную точку версии 2.0, используя область `openid`, например:</span><span class="sxs-lookup"><span data-stu-id="f14be-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="f14be-149">Сейчас, когда пользователь предоставляет разрешение на доступ к области `openid`, приложение получает подробные сведения о пользователе в полученном id_token.</span><span class="sxs-lookup"><span data-stu-id="f14be-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="f14be-150">В этих утверждениях может содержаться его имя, предпочтительное имя пользователя, адрес электронной почты, идентификатор объекта и многое другое.</span><span class="sxs-lookup"><span data-stu-id="f14be-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="f14be-151">В этом обновлении изменяются данные, которые доступны приложению через область `openid`. Это обеспечивает соответствие спецификации OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f14be-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="f14be-152">Теперь с помощью области `openid` пользователь сможет лишь войти в приложение и получить идентификатор для конкретного приложения в утверждении `sub` id_token.</span><span class="sxs-lookup"><span data-stu-id="f14be-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="f14be-153">Утверждения в id_token с доступом только к области `openid` не будут содержать личных сведений.</span><span class="sxs-lookup"><span data-stu-id="f14be-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="f14be-154">Примеры утверждений id_token:</span><span class="sxs-lookup"><span data-stu-id="f14be-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="f14be-155">Чтобы получить личные сведения о пользователе в приложении, приложение должно запросить дополнительные разрешения у пользователя.</span><span class="sxs-lookup"><span data-stu-id="f14be-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="f14be-156">Мы представляем две новые области из спецификации OpenID Connect, с помощью которых можно это сделать: `email` и `profile`.</span><span class="sxs-lookup"><span data-stu-id="f14be-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="f14be-157">Область `email` достаточно проста. С ее помощью приложение получает доступ к основному адресу электронной почты пользователя через утверждение `email` в id_token.</span><span class="sxs-lookup"><span data-stu-id="f14be-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="f14be-158">Обратите внимание, что утверждение `email` не всегда представлено в id_tokens, а только если оно указано в профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="f14be-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="f14be-159">С помощью области `profile` приложение может получить другие основные сведения о пользователе: имя, предпочтительное имя пользователя, идентификатор объекта и т. д.</span><span class="sxs-lookup"><span data-stu-id="f14be-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="f14be-160">Это позволяет писать код приложения с минимальным разглашением сведений. Вы можете запросить у пользователя только те сведения, которые необходимы приложению для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="f14be-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="f14be-161">Если вы хотите по-прежнему получать полный набор сведений о пользователе, необходимо включить в запросы авторизации все три области:</span><span class="sxs-lookup"><span data-stu-id="f14be-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="f14be-162">Приложение может немедленно начать отправку областей `email` и `profile`, а конечная точка версии 2.0 примет эти области и начнет запрашивать разрешения у пользователей при необходимости.</span><span class="sxs-lookup"><span data-stu-id="f14be-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="f14be-163">Однако изменения интерпретации области `openid` вступят в силу только через несколько недель.</span><span class="sxs-lookup"><span data-stu-id="f14be-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f14be-164">**Задание. Добавьте области `profile` и `email`, если приложению требуются сведения о пользователе.**</span><span class="sxs-lookup"><span data-stu-id="f14be-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="f14be-165">Обратите внимание, что при использовании ADAL эти разрешения запрашиваются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f14be-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="f14be-166">Удаление завершающей косой черты из значения издателя</span><span class="sxs-lookup"><span data-stu-id="f14be-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="f14be-167">До этого значение издателя, которое отображается в маркерах конечной точки версии 2.0, выглядело следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f14be-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="f14be-168">guid здесь — идентификатор клиента Azure AD, который выдал маркер.</span><span class="sxs-lookup"><span data-stu-id="f14be-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="f14be-169">После внесения изменений значение издателя будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="f14be-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="f14be-170">Это касается как обоих маркеров, так и документа обнаружения OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f14be-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f14be-171">**Задание. Убедитесь, что во время проверки издателя приложение принимает значение издателя и с завершающей косой чертой, и без нее.**</span><span class="sxs-lookup"><span data-stu-id="f14be-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="f14be-172">Цель изменений</span><span class="sxs-lookup"><span data-stu-id="f14be-172">Why change?</span></span>
<span data-ttu-id="f14be-173">Эти изменения главным образом предназначены для соответствия стандартной спецификации OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f14be-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="f14be-174">Мы надеемся, что таким образом можно свести к минимуму различия между интеграцией со службами идентификации Майкрософт и другими службами идентификации в этой отрасли.</span><span class="sxs-lookup"><span data-stu-id="f14be-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="f14be-175">Мы хотим предоставить разработчикам возможность использовать привычные библиотеки проверки подлинности с открытым исходным кодом без каких-либо изменений в связи с различиями служб Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f14be-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="f14be-176">Советы разработчикам</span><span class="sxs-lookup"><span data-stu-id="f14be-176">What can you do?</span></span>
<span data-ttu-id="f14be-177">С сегодняшнего дня вы можете начать вносить все описанные выше изменения.</span><span class="sxs-lookup"><span data-stu-id="f14be-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="f14be-178">Незамедлительно сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f14be-178">You should immediately:</span></span>

1. <span data-ttu-id="f14be-179">**Устраните все зависимости от параметра заголовка `x5t`.**</span><span class="sxs-lookup"><span data-stu-id="f14be-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="f14be-180">**Надлежащим образом выполните переход с `profile_info` на `id_token` в ответах маркеров.**</span><span class="sxs-lookup"><span data-stu-id="f14be-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="f14be-181">**Устраните все зависимости от параметра ответа `id_token_expires_in`.**</span><span class="sxs-lookup"><span data-stu-id="f14be-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="f14be-182">**Добавьте области `profile` и `email` в приложение, если ему необходимы основные сведения о пользователе.**</span><span class="sxs-lookup"><span data-stu-id="f14be-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="f14be-183">**Настройте принятие значений издателя в маркерах с завершающей косой чертой и без нее.**</span><span class="sxs-lookup"><span data-stu-id="f14be-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="f14be-184">Статья [Предварительная версия модели приложений 2.0: протоколы — OAuth 2.0 и OpenID Connect](active-directory-v2-protocols.md) уже обновлена с учетом этих изменений, так что вы можете использовать ее в качестве справочных материалов во время обновления кода.</span><span class="sxs-lookup"><span data-stu-id="f14be-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="f14be-185">Если в дальнейшем у вас возникнут вопросы по этим изменениям, вы можете связаться с нами в Twitter через канал @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="f14be-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="f14be-186">Частота изменений протокола</span><span class="sxs-lookup"><span data-stu-id="f14be-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="f14be-187">Никакие критические изменения для протоколов проверки подлинности в дальнейшем не предусмотрены.</span><span class="sxs-lookup"><span data-stu-id="f14be-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="f14be-188">Мы намеренно объединили эти изменения в одной версии, чтобы вам в ближайшее время не пришлось выполнять этот процесс обновления снова.</span><span class="sxs-lookup"><span data-stu-id="f14be-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="f14be-189">Безусловно, мы продолжаем добавлять удобные функции в объединенную службу проверки подлинности версии 2.0, но эти изменения являются добавочными и не нарушают существующий код.</span><span class="sxs-lookup"><span data-stu-id="f14be-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="f14be-190">И наконец, мы бы хотели выразить благодарность за то, что вы опробовали на практике эту предварительную версию.</span><span class="sxs-lookup"><span data-stu-id="f14be-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="f14be-191">Аналитические сведения и опыт первых исследователей имели неоценимое значение, и мы надеемся, что вы продолжите делиться своим мнением и идеями.</span><span class="sxs-lookup"><span data-stu-id="f14be-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="f14be-192">Удачного программирования!</span><span class="sxs-lookup"><span data-stu-id="f14be-192">Happy coding!</span></span>

<span data-ttu-id="f14be-193">Подразделение Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="f14be-193">The Microsoft Identity Division</span></span>

