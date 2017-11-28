---
title: "aaaSession управления - Microsoft средства моделирования угроз - Azure | Документы Microsoft"
description: "защиту от угроз, которые представлены в hello средства моделирования угроз"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="e1c5c-103">Механизм безопасности. Управление сеансами | Статьи</span><span class="sxs-lookup"><span data-stu-id="e1c5c-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="e1c5c-104">Продукт или служба</span><span class="sxs-lookup"><span data-stu-id="e1c5c-104">Product/Service</span></span> | <span data-ttu-id="e1c5c-105">Статья</span><span class="sxs-lookup"><span data-stu-id="e1c5c-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="e1c5c-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="e1c5c-107">Реализуйте надлежащее событие выхода с помощью методов ADAL при использовании Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1c5c-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="e1c5c-108">Устройства Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="e1c5c-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="e1c5c-109">Используйте токены SaS с ограниченным временем существования</span><span class="sxs-lookup"><span data-stu-id="e1c5c-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="e1c5c-110">**Azure DocumentDB**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="e1c5c-111">Используйте токены ресурсов с минимальным временем существования</span><span class="sxs-lookup"><span data-stu-id="e1c5c-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="e1c5c-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="e1c5c-113">Реализуйте надлежащее событие выхода с помощью методов WsFederation при использовании ADFS</span><span class="sxs-lookup"><span data-stu-id="e1c5c-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="e1c5c-114">**Сервер удостоверений**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="e1c5c-115">Реализуйте надлежащее событие выхода при использовании сервера удостоверений</span><span class="sxs-lookup"><span data-stu-id="e1c5c-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="e1c5c-116">**Веб-приложение**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="e1c5c-117">Используйте защищенные файлы cookie в приложениях, использующих протокол HTTPS</span><span class="sxs-lookup"><span data-stu-id="e1c5c-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="e1c5c-118">Укажите атрибут httpOnly в определении файла cookie всех приложений на основе протокола HTTP</span><span class="sxs-lookup"><span data-stu-id="e1c5c-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="e1c5c-119">Уменьшите риск атак с подделкой межсайтовых запросов на веб-страницах ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e1c5c-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="e1c5c-120">Настройте период бездействия сеанса</span><span class="sxs-lookup"><span data-stu-id="e1c5c-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="e1c5c-121">Реализация правильную выхода из приложения hello</span><span class="sxs-lookup"><span data-stu-id="e1c5c-121">Implement proper logout from hello application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="e1c5c-122">**Веб-интерфейс API**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="e1c5c-123">Уменьшите риск атак с подделкой межсайтовых запросов в веб-интерфейсах API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e1c5c-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="e1c5c-124"><a id="logout-adal"></a>Реализуйте надлежащее событие выхода с помощью методов ADAL при использовании Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1c5c-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="e1c5c-125">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-125">Title</span></span>                   | <span data-ttu-id="e1c5c-126">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-127">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-127">**Component**</span></span>               | <span data-ttu-id="e1c5c-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1c5c-128">Azure AD</span></span> | 
| <span data-ttu-id="e1c5c-129">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-129">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-130">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-130">Build</span></span> |  
| <span data-ttu-id="e1c5c-131">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-131">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-132">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-132">Generic</span></span> |
| <span data-ttu-id="e1c5c-133">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-133">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-134">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-134">N/A</span></span>  |
| <span data-ttu-id="e1c5c-135">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-135">**References**</span></span>              | <span data-ttu-id="e1c5c-136">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-136">N/A</span></span>  |
| <span data-ttu-id="e1c5c-137">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-137">**Steps**</span></span> | <span data-ttu-id="e1c5c-138">Если приложение hello использует маркер доступа, выданный Azure AD, должен вызывать обработчик события выхода hello</span><span class="sxs-lookup"><span data-stu-id="e1c5c-138">If hello application relies on access token issued by Azure AD, hello logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="e1c5c-139">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="e1c5c-140">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-140">Example</span></span>
<span data-ttu-id="e1c5c-141">Кроме того, также необходимо уничтожить сеанс пользователя путем вызова метода Session.Abandon().</span><span class="sxs-lookup"><span data-stu-id="e1c5c-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="e1c5c-142">Ниже приведен метод безопасной реализации события выхода пользователя.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-142">Following method shows secure implementation of user logout:</span></span>
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <span data-ttu-id="e1c5c-143"><a id="finite-tokens"></a>Используйте токены SaS с ограниченным временем существования</span><span class="sxs-lookup"><span data-stu-id="e1c5c-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="e1c5c-144">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-144">Title</span></span>                   | <span data-ttu-id="e1c5c-145">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-146">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-146">**Component**</span></span>               | <span data-ttu-id="e1c5c-147">Устройства Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="e1c5c-147">IoT Device</span></span> | 
| <span data-ttu-id="e1c5c-148">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-148">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-149">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-149">Build</span></span> |  
| <span data-ttu-id="e1c5c-150">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-150">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-151">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-151">Generic</span></span> |
| <span data-ttu-id="e1c5c-152">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-152">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-153">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-153">N/A</span></span>  |
| <span data-ttu-id="e1c5c-154">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-154">**References**</span></span>              | <span data-ttu-id="e1c5c-155">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-155">N/A</span></span>  |
| <span data-ttu-id="e1c5c-156">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-156">**Steps**</span></span> | <span data-ttu-id="e1c5c-157">SaS токены, созданные для проверки подлинности tooAzure центр IoT должен иметь ограничение срока.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-157">SaS tokens generated for authenticating tooAzure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="e1c5c-158">Сохраните hello SaS времени жизни токенов tooa минимальные toolimit hello количество раз, когда они могут быть воспроизведены в случае компрометации токены hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-158">Keep hello SaS token lifetimes tooa minimum toolimit hello amount of time they can be replayed in case hello tokens are compromised.</span></span>|

## <span data-ttu-id="e1c5c-159"><a id="resource-tokens"></a>Используйте токены ресурсов с минимальным временем существования</span><span class="sxs-lookup"><span data-stu-id="e1c5c-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="e1c5c-160">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-160">Title</span></span>                   | <span data-ttu-id="e1c5c-161">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-162">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-162">**Component**</span></span>               | <span data-ttu-id="e1c5c-163">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e1c5c-163">Azure Document DB</span></span> | 
| <span data-ttu-id="e1c5c-164">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-164">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-165">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-165">Build</span></span> |  
| <span data-ttu-id="e1c5c-166">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-166">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-167">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-167">Generic</span></span> |
| <span data-ttu-id="e1c5c-168">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-168">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-169">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-169">N/A</span></span>  |
| <span data-ttu-id="e1c5c-170">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-170">**References**</span></span>              | <span data-ttu-id="e1c5c-171">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-171">N/A</span></span>  |
| <span data-ttu-id="e1c5c-172">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-172">**Steps**</span></span> | <span data-ttu-id="e1c5c-173">Уменьшите время существования hello ресурсов маркера tooa минимальное значение.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-173">Reduce hello timespan of resource token tooa minimum value required.</span></span> <span data-ttu-id="e1c5c-174">Допустимый интервал времени по умолчанию для маркеров ресурсов составляет 1 час.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="e1c5c-175"><a id="wsfederation-logout"></a>Реализуйте надлежащее событие выхода с помощью методов WsFederation при использовании ADFS</span><span class="sxs-lookup"><span data-stu-id="e1c5c-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="e1c5c-176">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-176">Title</span></span>                   | <span data-ttu-id="e1c5c-177">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-178">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-178">**Component**</span></span>               | <span data-ttu-id="e1c5c-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="e1c5c-179">ADFS</span></span> | 
| <span data-ttu-id="e1c5c-180">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-180">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-181">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-181">Build</span></span> |  
| <span data-ttu-id="e1c5c-182">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-182">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-183">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-183">Generic</span></span> |
| <span data-ttu-id="e1c5c-184">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-184">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-185">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-185">N/A</span></span>  |
| <span data-ttu-id="e1c5c-186">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-186">**References**</span></span>              | <span data-ttu-id="e1c5c-187">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-187">N/A</span></span>  |
| <span data-ttu-id="e1c5c-188">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-188">**Steps**</span></span> | <span data-ttu-id="e1c5c-189">Если приложения hello зависит от службы маркеров безопасности маркера, выданного службой ADFS, обработчик событий выхода hello следует вызывать toolog метод WSFederationAuthenticationModule.FederatedSignOut() выход пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-189">If hello application relies on STS token issued by ADFS, hello logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method toolog out hello user.</span></span> <span data-ttu-id="e1c5c-190">Также hello текущего сеанса должен быть уничтожен, и значение маркера сеанса hello следует сбросить и nullified.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-190">Also hello current session should be destroyed, and hello session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="e1c5c-191">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="e1c5c-192"><a id="proper-logout"></a>Реализуйте надлежащее событие выхода при использовании сервера удостоверений</span><span class="sxs-lookup"><span data-stu-id="e1c5c-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="e1c5c-193">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-193">Title</span></span>                   | <span data-ttu-id="e1c5c-194">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-195">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-195">**Component**</span></span>               | <span data-ttu-id="e1c5c-196">Сервер удостоверений</span><span class="sxs-lookup"><span data-stu-id="e1c5c-196">Identity Server</span></span> | 
| <span data-ttu-id="e1c5c-197">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-197">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-198">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-198">Build</span></span> |  
| <span data-ttu-id="e1c5c-199">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-199">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-200">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-200">Generic</span></span> |
| <span data-ttu-id="e1c5c-201">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-201">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-202">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-202">N/A</span></span>  |
| <span data-ttu-id="e1c5c-203">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-203">**References**</span></span>              | [<span data-ttu-id="e1c5c-204">Сведения о федеративном выходе на платформе IdentityServer3</span><span class="sxs-lookup"><span data-stu-id="e1c5c-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="e1c5c-205">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-205">**Steps**</span></span> | <span data-ttu-id="e1c5c-206">IdentityServer поддерживает toofederate возможность hello с внешних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-206">IdentityServer supports hello ability toofederate with external identity providers.</span></span> <span data-ttu-id="e1c5c-207">Когда пользователь выходит из поставщика удостоверений вышестоящего, зависимости hello протокол, используемый, его может быть возможных tooreceive уведомление при hello пользователь выходит из системы. Она позволяет toonotify IdentityServer, ее клиентов, чтобы они могли войти hello пользователя. Просмотрите документацию hello в разделе references hello hello сведения о реализации.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-207">When a user signs out of an upstream identity provider, depending upon hello protocol used, it might be possible tooreceive a notification when hello user signs out. It allows IdentityServer toonotify its clients so they can also sign hello user out. Check hello documentation in hello references section for hello implementation details.</span></span>|

## <span data-ttu-id="e1c5c-208"><a id="https-secure-cookies"></a>Используйте защищенные файлы cookie в приложениях, использующих протокол HTTPS</span><span class="sxs-lookup"><span data-stu-id="e1c5c-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="e1c5c-209">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-209">Title</span></span>                   | <span data-ttu-id="e1c5c-210">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-211">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-211">**Component**</span></span>               | <span data-ttu-id="e1c5c-212">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-212">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-213">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-213">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-214">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-214">Build</span></span> |  
| <span data-ttu-id="e1c5c-215">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-215">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-216">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-216">Generic</span></span> |
| <span data-ttu-id="e1c5c-217">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-217">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-218">EnvironmentType: OnPrem</span><span class="sxs-lookup"><span data-stu-id="e1c5c-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="e1c5c-219">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-219">**References**</span></span>              | <span data-ttu-id="e1c5c-220">[Элемент httpCookies (схема параметров ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [Свойство HttpCookie.Secure](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="e1c5c-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="e1c5c-221">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-221">**Steps**</span></span> | <span data-ttu-id="e1c5c-222">Файлы cookie обычно являются только домен доступен toohello, для которого было ограничено.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-222">Cookies are normally only accessible toohello domain for which they were scoped.</span></span> <span data-ttu-id="e1c5c-223">К сожалению определение hello «домен» не включает протокол hello, файлы cookie, которые создаются по протоколу HTTPS, доступны по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-223">Unfortunately, hello definition of "domain" does not include hello protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="e1c5c-224">атрибут «безопасность» Hello указывает, что браузер toohello, hello cookie только стало доступным по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-224">hello "secure" attribute indicates toohello browser that hello cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="e1c5c-225">Убедитесь, что все файлы Сookie по протоколу HTTPS используют hello **безопасного** атрибута.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-225">Ensure that all cookies set over HTTPS use hello **secure** attribute.</span></span> <span data-ttu-id="e1c5c-226">требование Hello может применяться в файле web.config hello, задав tootrue атрибут requireSSL hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-226">hello requirement can be enforced in hello web.config file by setting hello requireSSL attribute tootrue.</span></span> <span data-ttu-id="e1c5c-227">Это hello основной подход, так как он будет обеспечивать hello **безопасного** любой дополнительный код изменения атрибутов для всех текущих и будущих куки-файлов без необходимости toomake hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-227">It is hello preferred approach because it will enforce hello **secure** attribute for all current and future cookies without hello need toomake any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="e1c5c-228">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="e1c5c-229">параметр Hello применяется, даже если протокол HTTP является приложение hello используется tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-229">hello setting is enforced even if HTTP is used tooaccess hello application.</span></span> <span data-ttu-id="e1c5c-230">Если используется протокол HTTP tooaccess hello приложения, hello параметр переводов, которые приложение hello так, как файлы cookie hello устанавливаются с помощью hello защищенный атрибут и hello браузер не будет отправлять их снова toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-230">If HTTP is used tooaccess hello application, hello setting breaks hello application because hello cookies are set with hello secure attribute and hello browser will not send them back toohello application.</span></span>

| <span data-ttu-id="e1c5c-231">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-231">Title</span></span>                   | <span data-ttu-id="e1c5c-232">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-233">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-233">**Component**</span></span>               | <span data-ttu-id="e1c5c-234">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-234">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-235">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-235">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-236">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-236">Build</span></span> |  
| <span data-ttu-id="e1c5c-237">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-237">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-238">Веб-формы, MVC 5</span><span class="sxs-lookup"><span data-stu-id="e1c5c-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="e1c5c-239">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-239">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-240">EnvironmentType: OnPrem</span><span class="sxs-lookup"><span data-stu-id="e1c5c-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="e1c5c-241">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-241">**References**</span></span>              | <span data-ttu-id="e1c5c-242">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-242">N/A</span></span>  |
| <span data-ttu-id="e1c5c-243">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-243">**Steps**</span></span> | <span data-ttu-id="e1c5c-244">Когда веб-приложение hello hello проверяющая сторона, который hello поставщика удостоверений сервер ADFS, атрибут hello FedAuth маркер безопасности можно настроить с параметра requireSSL tooTrue в `system.identityModel.services` файла Web.config:</span><span class="sxs-lookup"><span data-stu-id="e1c5c-244">When hello web application is hello Relying Party, and hello IdP is ADFS server, hello FedAuth token's secure attribute can be configured by setting requireSSL tooTrue in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="e1c5c-245">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="e1c5c-246"><a id="cookie-definition"></a>Укажите атрибут httpOnly в определении файла cookie всех приложений на основе протокола HTTP</span><span class="sxs-lookup"><span data-stu-id="e1c5c-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="e1c5c-247">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-247">Title</span></span>                   | <span data-ttu-id="e1c5c-248">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-249">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-249">**Component**</span></span>               | <span data-ttu-id="e1c5c-250">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-250">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-251">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-251">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-252">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-252">Build</span></span> |  
| <span data-ttu-id="e1c5c-253">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-253">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-254">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-254">Generic</span></span> |
| <span data-ttu-id="e1c5c-255">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-255">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-256">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-256">N/A</span></span>  |
| <span data-ttu-id="e1c5c-257">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-257">**References**</span></span>              | [<span data-ttu-id="e1c5c-258">Сведения об атрибуте secure в файлах cookie</span><span class="sxs-lookup"><span data-stu-id="e1c5c-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="e1c5c-259">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-259">**Steps**</span></span> | <span data-ttu-id="e1c5c-260">toomitigate hello риск раскрытия информации с атаке межсайтовых сценариев (XSS), новый атрибут - httpOnly - было введено toocookies и поддерживается всеми основными браузерами.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-260">toomitigate hello risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced toocookies and is supported by all major browsers.</span></span> <span data-ttu-id="e1c5c-261">атрибут Hello указывает, что куки-файл недоступен через сценарий.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-261">hello attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="e1c5c-262">С помощью файлов cookie HttpOnly, веб-приложении снижает вероятность hello можно, конфиденциальные данные, содержащиеся в файле cookie hello кражи через сценарий и отправленных веб-сайта злоумышленника tooan.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-262">By using HttpOnly cookies, a web application reduces hello possibility that sensitive information contained in hello cookie can be stolen via script and sent tooan attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="e1c5c-263">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-263">Example</span></span>
<span data-ttu-id="e1c5c-264">Все HTTP-приложений, которые используют файлы cookie следует указать HttpOnly в определении cookie hello, путем реализации следующие конфигурации в файле web.config:</span><span class="sxs-lookup"><span data-stu-id="e1c5c-264">All HTTP-based applications that use cookies should specify HttpOnly in hello cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="e1c5c-265">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-265">Title</span></span>                   | <span data-ttu-id="e1c5c-266">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-267">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-267">**Component**</span></span>               | <span data-ttu-id="e1c5c-268">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-268">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-269">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-269">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-270">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-270">Build</span></span> |  
| <span data-ttu-id="e1c5c-271">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-271">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-272">Веб-формы</span><span class="sxs-lookup"><span data-stu-id="e1c5c-272">Web Forms</span></span> |
| <span data-ttu-id="e1c5c-273">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-273">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-274">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-274">N/A</span></span>  |
| <span data-ttu-id="e1c5c-275">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-275">**References**</span></span>              | [<span data-ttu-id="e1c5c-276">Свойство FormsAuthentication.RequireSSL</span><span class="sxs-lookup"><span data-stu-id="e1c5c-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="e1c5c-277">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-277">**Steps**</span></span> | <span data-ttu-id="e1c5c-278">Hello RequireSSL значение свойства задается в файле конфигурации hello для приложения ASP.NET с помощью атрибут requireSSL hello hello элемента конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-278">hello RequireSSL property value is set in hello configuration file for an ASP.NET application by using hello requireSSL attribute of hello configuration element.</span></span> <span data-ttu-id="e1c5c-279">Вы можно указать в файле Web.config hello для приложения ASP.NET ли протокол SSL (Secure Sockets Layer) сервера требуется tooreturn hello проверки подлинности форм cookie toohello атрибутом requireSSL параметр hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-279">You can specify in hello Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required tooreturn hello forms-authentication cookie toohello server by setting hello requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="e1c5c-280">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-280">Example</span></span> 
<span data-ttu-id="e1c5c-281">Hello следующий пример кода задает атрибут requireSSL hello в файле Web.config hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-281">hello following code example sets hello requireSSL attribute in hello Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="e1c5c-282">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-282">Title</span></span>                   | <span data-ttu-id="e1c5c-283">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-284">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-284">**Component**</span></span>               | <span data-ttu-id="e1c5c-285">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-285">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-286">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-286">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-287">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-287">Build</span></span> |  
| <span data-ttu-id="e1c5c-288">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-288">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="e1c5c-289">MVC5</span></span> |
| <span data-ttu-id="e1c5c-290">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-290">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-291">EnvironmentType: OnPrem</span><span class="sxs-lookup"><span data-stu-id="e1c5c-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="e1c5c-292">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-292">**References**</span></span>              | [<span data-ttu-id="e1c5c-293">Запись блога о конфигурации Windows Identity Foundation (WIF). Часть 2</span><span class="sxs-lookup"><span data-stu-id="e1c5c-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="e1c5c-294">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-294">**Steps**</span></span> | <span data-ttu-id="e1c5c-295">атрибут httpOnly tooset для файлов cookie FedAuth, hideFromCsript атрибут должен иметь значение tooTrue.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-295">tooset httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set tooTrue.</span></span> |

### <a name="example"></a><span data-ttu-id="e1c5c-296">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-296">Example</span></span>
<span data-ttu-id="e1c5c-297">В конфигурации ниже показано hello правильной конфигурации:</span><span class="sxs-lookup"><span data-stu-id="e1c5c-297">Following configuration shows hello correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <span data-ttu-id="e1c5c-298"><a id="csrf-asp"></a>Уменьшите риск атак с подделкой межсайтовых запросов на веб-страницах ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e1c5c-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="e1c5c-299">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-299">Title</span></span>                   | <span data-ttu-id="e1c5c-300">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-301">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-301">**Component**</span></span>               | <span data-ttu-id="e1c5c-302">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-302">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-303">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-303">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-304">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-304">Build</span></span> |  
| <span data-ttu-id="e1c5c-305">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-305">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-306">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-306">Generic</span></span> |
| <span data-ttu-id="e1c5c-307">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-307">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-308">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-308">N/A</span></span>  |
| <span data-ttu-id="e1c5c-309">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-309">**References**</span></span>              | <span data-ttu-id="e1c5c-310">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-310">N/A</span></span>  |
| <span data-ttu-id="e1c5c-311">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-311">**Steps**</span></span> | <span data-ttu-id="e1c5c-312">Подделки межсайтовых запросов (CSRF или XSRF) — это тип атаки, в котором злоумышленник может выполнять действия в контексте безопасности hello установленного сеанса другого пользователя на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="e1c5c-313">Цель Hello является toomodify или удалить содержимое, если указанный веб-узел hello основывается только на запрос получен tooauthenticate файлы cookie сеанса.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-313">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="e1c5c-314">Злоумышленник может воспользоваться этой уязвимостью, получая URL-адрес с помощью команды tooload браузера другого пользователя с уязвимым сайта, на котором hello пользователь уже вошел в.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-314">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="e1c5c-315">Существует множество способов для toodo злоумышленник, такие как с помощью предоставления различных веб-сайта, загружает ресурс hello уязвимым сервера или получении tooclick пользователя hello ссылку.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-315">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="e1c5c-316">Если hello сервер отправляет клиенту дополнительных маркеров toohello, требует hello этого токена все последующие запросы клиента tooinclude и проверяет, что все последующие запросы включать маркер, который соответствует toohello текущего сеанса, например, можно предотвратить атаки Hello с помощью hello ASP.NET AntiForgeryToken или ViewState.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-316">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="e1c5c-317">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-317">Title</span></span>                   | <span data-ttu-id="e1c5c-318">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-319">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-319">**Component**</span></span>               | <span data-ttu-id="e1c5c-320">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-320">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-321">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-321">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-322">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-322">Build</span></span> |  
| <span data-ttu-id="e1c5c-323">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-323">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-324">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="e1c5c-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="e1c5c-325">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-325">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-326">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-326">N/A</span></span>  |
| <span data-ttu-id="e1c5c-327">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-327">**References**</span></span>              | [<span data-ttu-id="e1c5c-328">Сведения о предотвращении подделки межсайтовых запросов в ASP.NET MVC и на веб-страницах ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e1c5c-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="e1c5c-329">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-329">**Steps**</span></span> | <span data-ttu-id="e1c5c-330">Формы CSRF защиты и ASP.NET MVC - hello используйте `AntiForgeryToken` вспомогательный метод для представлений; заключите `Html.AntiForgeryToken()` в форму hello, например,</span><span class="sxs-lookup"><span data-stu-id="e1c5c-330">Anti-CSRF and ASP.NET MVC forms - Use hello `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into hello form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="e1c5c-331">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="e1c5c-332">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="e1c5c-333">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-333">Example</span></span>
<span data-ttu-id="e1c5c-334">В hello же время, Html.AntiForgeryToken() дает hello посетитель куки-файл называется __RequestVerificationToken с hello совпадает со значением в hello случайного скрытые значения показано выше.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-334">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="e1c5c-335">Toovalidate входящих формы post, добавьте метод hello [ValidateAntiForgeryToken] фильтр toohello целевого действия.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-335">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="e1c5c-336">Например:</span><span class="sxs-lookup"><span data-stu-id="e1c5c-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="e1c5c-337">Фильтр авторизации, проверяющий, что:</span><span class="sxs-lookup"><span data-stu-id="e1c5c-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="e1c5c-338">входящий запрос Hello имеет файл cookie, вызывается __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="e1c5c-338">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="e1c5c-339">Hello во входящем запросе есть `Request.Form` под названием __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="e1c5c-339">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="e1c5c-340">Этих файлов cookie и `Request.Form` значения совпадают, при условии, что все хорошо, hello запрос проходит через в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-340">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="e1c5c-341">В противном случае проверка подлинности завершается ошибкой и отображается следующее сообщение: "Обязательный маркер против подделки не был предоставлен или был недопустимым".</span><span class="sxs-lookup"><span data-stu-id="e1c5c-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="e1c5c-342">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-342">Example</span></span>
<span data-ttu-id="e1c5c-343">CSRF защиты и AJAX: hello маркера формы может вызвать проблемы для запросов AJAX, так как запрос AJAX может отправить данные JSON, а не данные HTML-формы.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-343">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="e1c5c-344">Одним из решений является toosend hello токенов в заголовок HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-344">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="e1c5c-345">Hello следующий код использует токены hello toogenerate синтаксис Razor, а затем добавляет маркеры tooan hello AJAX-запросом.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-345">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="e1c5c-346">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-346">Example</span></span>
<span data-ttu-id="e1c5c-347">При обработке запроса hello, извлеките hello токены из заголовка запроса hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-347">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="e1c5c-348">Затем метод hello AntiForgery.Validate toovalidate hello маркеры.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-348">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="e1c5c-349">метод Validate Hello вызывает исключение, если маркеры hello не допускаются.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-349">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="e1c5c-350">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-350">Title</span></span>                   | <span data-ttu-id="e1c5c-351">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-352">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-352">**Component**</span></span>               | <span data-ttu-id="e1c5c-353">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-353">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-354">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-354">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-355">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-355">Build</span></span> |  
| <span data-ttu-id="e1c5c-356">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-356">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-357">Веб-формы</span><span class="sxs-lookup"><span data-stu-id="e1c5c-357">Web Forms</span></span> |
| <span data-ttu-id="e1c5c-358">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-358">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-359">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-359">N/A</span></span>  |
| <span data-ttu-id="e1c5c-360">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-360">**References**</span></span>              | [<span data-ttu-id="e1c5c-361">Использовать преимущества от встроенных функций ASP.NET tooFend Off Web атак</span><span class="sxs-lookup"><span data-stu-id="e1c5c-361">Take Advantage of ASP.NET Built-in Features tooFend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="e1c5c-362">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-362">**Steps**</span></span> | <span data-ttu-id="e1c5c-363">Атаки CSRF в приложениях на основе веб-форма можно устранить путем настройки произвольная строка tooa ViewStateUserKey, изменяющийся для каждого пользователя - идентификатор пользователя или лучше, идентификатор сеанса.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey tooa random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="e1c5c-364">По разным техническим и социальным причинам идентификатор сеанса подходит гораздо лучше, так как его нельзя предсказать, время его ожидания истекает и он уникальный для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="e1c5c-365">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-365">Example</span></span>
<span data-ttu-id="e1c5c-366">Ниже приведен код hello необходимо toohave во всех веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-366">Here's hello code you need toohave in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="e1c5c-367"><a id="inactivity-lifetime"></a>Настройте период бездействия сеанса</span><span class="sxs-lookup"><span data-stu-id="e1c5c-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="e1c5c-368">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-368">Title</span></span>                   | <span data-ttu-id="e1c5c-369">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-370">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-370">**Component**</span></span>               | <span data-ttu-id="e1c5c-371">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-371">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-372">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-372">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-373">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-373">Build</span></span> |  
| <span data-ttu-id="e1c5c-374">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-374">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-375">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-375">Generic</span></span> |
| <span data-ttu-id="e1c5c-376">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-376">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-377">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-377">N/A</span></span>  |
| <span data-ttu-id="e1c5c-378">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-378">**References**</span></span>              | <span data-ttu-id="e1c5c-379">[Свойство HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="e1c5c-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="e1c5c-380">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-380">**Steps**</span></span> | <span data-ttu-id="e1c5c-381">Время ожидания сеанса представляет hello событий возникающая, если пользователь не выполняет никаких действий на веб-сайте на протяжении интервала (определяемые веб-сервера).</span><span class="sxs-lookup"><span data-stu-id="e1c5c-381">Session timeout represents hello event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="e1c5c-382">Здравствуйте событий на стороне сервера, изменить статус hello too'invalid сеанса пользователя hello "(например «больше не используются») и сообщить hello web server toodestroy (удаление всех данных, содержащихся в ней).</span><span class="sxs-lookup"><span data-stu-id="e1c5c-382">hello event, on server side, change hello status of hello user session too'invalid' (for example  "not used anymore") and instruct hello web server toodestroy it (deleting all data contained into it).</span></span> <span data-ttu-id="e1c5c-383">Hello следующий пример кода задает время ожидания сеанса hello атрибута в минутах too15 в файле Web.config hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-383">hello following code example sets hello timeout session attribute too15 minutes in hello Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="e1c5c-384">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-384">Example</span></span>
<span data-ttu-id="e1c5c-385">``\`XML-код <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span><span class="sxs-lookup"><span data-stu-id="e1c5c-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="e1c5c-386">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-386">Title</span></span>                   | <span data-ttu-id="e1c5c-387">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-388">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-388">**Component**</span></span>               | <span data-ttu-id="e1c5c-389">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-389">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-390">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-390">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-391">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-391">Build</span></span> |  
| <span data-ttu-id="e1c5c-392">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-392">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-393">Веб-формы</span><span class="sxs-lookup"><span data-stu-id="e1c5c-393">Web Forms</span></span> |
| <span data-ttu-id="e1c5c-394">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-394">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-395">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-395">N/A</span></span>  |
| <span data-ttu-id="e1c5c-396">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-396">**References**</span></span>              | <span data-ttu-id="e1c5c-397">[Элемент forms для элемента credentials для элемента authentication (схема параметров ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="e1c5c-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="e1c5c-398">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-398">**Steps**</span></span> | <span data-ttu-id="e1c5c-399">Значение минут hello too15 времени ожидания билета проверки подлинности форм куки-файл</span><span class="sxs-lookup"><span data-stu-id="e1c5c-399">Set hello Forms Authentication Ticket cookie timeout too15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="e1c5c-400">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-400">Example</span></span>
<span data-ttu-id="e1c5c-401">``\` XML-код <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="e1c5c-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="e1c5c-402">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-402">Example</span></span>
<span data-ttu-id="e1c5c-403">Также hello, выданных время жизни токена SAML утверждения служб федерации Active Directory должно быть установлено too15 минут, выполнив следующую команду powershell на сервере ADFS hello hello:</span><span class="sxs-lookup"><span data-stu-id="e1c5c-403">Also hello ADFS issued SAML claim token's lifetime should be set too15 minutes, by executing hello following powershell command on hello ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="e1c5c-404"><a id="proper-app-logout"></a>Реализация правильную выхода из приложения hello</span><span class="sxs-lookup"><span data-stu-id="e1c5c-404"><a id="proper-app-logout"></a>Implement proper logout from hello application</span></span>

| <span data-ttu-id="e1c5c-405">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-405">Title</span></span>                   | <span data-ttu-id="e1c5c-406">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-407">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-407">**Component**</span></span>               | <span data-ttu-id="e1c5c-408">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="e1c5c-408">Web Application</span></span> | 
| <span data-ttu-id="e1c5c-409">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-409">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-410">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-410">Build</span></span> |  
| <span data-ttu-id="e1c5c-411">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-411">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-412">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-412">Generic</span></span> |
| <span data-ttu-id="e1c5c-413">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-413">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-414">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-414">N/A</span></span>  |
| <span data-ttu-id="e1c5c-415">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-415">**References**</span></span>              | <span data-ttu-id="e1c5c-416">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-416">N/A</span></span>  |
| <span data-ttu-id="e1c5c-417">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-417">**Steps**</span></span> | <span data-ttu-id="e1c5c-418">Выполните правильную выйти из приложения hello, когда пользователь нажимает выход кнопки.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-418">Perform proper Sign Out from hello application, when user presses log out button.</span></span> <span data-ttu-id="e1c5c-419">То есть оно должно уничтожить сеанс пользователя, а также сбросить и обнулить значение файла cookie сеанса и файла cookie проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="e1c5c-420">Кроме того когда несколько сеансов равноценных tooa одного пользователя удостоверения, они должна совокупности заканчиваться на стороне сервера hello во время ожидания или выхода из системы.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-420">Also, when multiple sessions are tied tooa single user identity, they must be collectively terminated on hello server side at timeout or logout.</span></span> <span data-ttu-id="e1c5c-421">Наконец, убедитесь, что функция выхода доступна на каждой странице.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="e1c5c-422"><a id="csrf-api"></a>Уменьшите риск атак с подделкой межсайтовых запросов в веб-интерфейсах API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e1c5c-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="e1c5c-423">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-423">Title</span></span>                   | <span data-ttu-id="e1c5c-424">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-425">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-425">**Component**</span></span>               | <span data-ttu-id="e1c5c-426">Веб-интерфейс API</span><span class="sxs-lookup"><span data-stu-id="e1c5c-426">Web API</span></span> | 
| <span data-ttu-id="e1c5c-427">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-427">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-428">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-428">Build</span></span> |  
| <span data-ttu-id="e1c5c-429">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-429">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-430">Универсальный</span><span class="sxs-lookup"><span data-stu-id="e1c5c-430">Generic</span></span> |
| <span data-ttu-id="e1c5c-431">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-431">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-432">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-432">N/A</span></span>  |
| <span data-ttu-id="e1c5c-433">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-433">**References**</span></span>              | <span data-ttu-id="e1c5c-434">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-434">N/A</span></span>  |
| <span data-ttu-id="e1c5c-435">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-435">**Steps**</span></span> | <span data-ttu-id="e1c5c-436">Подделки межсайтовых запросов (CSRF или XSRF) — это тип атаки, в котором злоумышленник может выполнять действия в контексте безопасности hello установленного сеанса другого пользователя на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="e1c5c-437">Цель Hello является toomodify или удалить содержимое, если указанный веб-узел hello основывается только на запрос получен tooauthenticate файлы cookie сеанса.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-437">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="e1c5c-438">Злоумышленник может воспользоваться этой уязвимостью, получая URL-адрес с помощью команды tooload браузера другого пользователя с уязвимым сайта, на котором hello пользователь уже вошел в.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-438">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="e1c5c-439">Существует множество способов для toodo злоумышленник, такие как с помощью предоставления различных веб-сайта, загружает ресурс hello уязвимым сервера или получении tooclick пользователя hello ссылку.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-439">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="e1c5c-440">Если hello сервер отправляет клиенту дополнительных маркеров toohello, требует hello этого токена все последующие запросы клиента tooinclude и проверяет, что все последующие запросы включать маркер, который соответствует toohello текущего сеанса, например, можно предотвратить атаки Hello с помощью hello ASP.NET AntiForgeryToken или ViewState.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-440">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="e1c5c-441">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-441">Title</span></span>                   | <span data-ttu-id="e1c5c-442">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-443">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-443">**Component**</span></span>               | <span data-ttu-id="e1c5c-444">Веб-интерфейс API</span><span class="sxs-lookup"><span data-stu-id="e1c5c-444">Web API</span></span> | 
| <span data-ttu-id="e1c5c-445">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-445">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-446">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-446">Build</span></span> |  
| <span data-ttu-id="e1c5c-447">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-447">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-448">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="e1c5c-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="e1c5c-449">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-449">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-450">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e1c5c-450">N/A</span></span>  |
| <span data-ttu-id="e1c5c-451">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-451">**References**</span></span>              | [<span data-ttu-id="e1c5c-452">Статья о предотвращении риска атак с подделкой межсайтовых запросов в веб-интерфейсах API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e1c5c-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="e1c5c-453">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-453">**Steps**</span></span> | <span data-ttu-id="e1c5c-454">CSRF защиты и AJAX: hello маркера формы может вызвать проблемы для запросов AJAX, так как запрос AJAX может отправить данные JSON, а не данные HTML-формы.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-454">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="e1c5c-455">Одним из решений является toosend hello токенов в заголовок HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-455">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="e1c5c-456">Hello следующий код использует токены hello toogenerate синтаксис Razor, а затем добавляет маркеры tooan hello AJAX-запросом.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-456">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="e1c5c-457">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-457">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="e1c5c-458">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-458">Example</span></span>
<span data-ttu-id="e1c5c-459">При обработке запроса hello, извлеките hello токены из заголовка запроса hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-459">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="e1c5c-460">Затем метод hello AntiForgery.Validate toovalidate hello маркеры.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-460">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="e1c5c-461">метод Validate Hello вызывает исключение, если маркеры hello не допускаются.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-461">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="e1c5c-462">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-462">Example</span></span>
<span data-ttu-id="e1c5c-463">CSRF защиты и форм ASP.NET MVC - hello использование вспомогательного метода AntiForgeryToken для представлений; Например, поместите Html.AntiForgeryToken() в форму hello</span><span class="sxs-lookup"><span data-stu-id="e1c5c-463">Anti-CSRF and ASP.NET MVC forms - Use hello AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into hello form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="e1c5c-464">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-464">Example</span></span>
<span data-ttu-id="e1c5c-465">приведенном выше примере Hello выдаст примерно hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e1c5c-465">hello example above will output something like hello following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="e1c5c-466">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-466">Example</span></span>
<span data-ttu-id="e1c5c-467">В hello же время, Html.AntiForgeryToken() дает hello посетитель куки-файл называется __RequestVerificationToken с hello совпадает со значением в hello случайного скрытые значения показано выше.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-467">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="e1c5c-468">Toovalidate входящих формы post, добавьте метод hello [ValidateAntiForgeryToken] фильтр toohello целевого действия.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-468">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="e1c5c-469">Например:</span><span class="sxs-lookup"><span data-stu-id="e1c5c-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="e1c5c-470">Фильтр авторизации, проверяющий, что:</span><span class="sxs-lookup"><span data-stu-id="e1c5c-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="e1c5c-471">входящий запрос Hello имеет файл cookie, вызывается __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="e1c5c-471">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="e1c5c-472">Hello во входящем запросе есть `Request.Form` под названием __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="e1c5c-472">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="e1c5c-473">Этих файлов cookie и `Request.Form` значения совпадают, при условии, что все хорошо, hello запрос проходит через в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-473">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="e1c5c-474">В противном случае проверка подлинности завершается ошибкой и отображается следующее сообщение: "Обязательный маркер против подделки не был предоставлен или был недопустимым".</span><span class="sxs-lookup"><span data-stu-id="e1c5c-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="e1c5c-475">Название</span><span class="sxs-lookup"><span data-stu-id="e1c5c-475">Title</span></span>                   | <span data-ttu-id="e1c5c-476">Сведения</span><span class="sxs-lookup"><span data-stu-id="e1c5c-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="e1c5c-477">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-477">**Component**</span></span>               | <span data-ttu-id="e1c5c-478">Веб-интерфейс API</span><span class="sxs-lookup"><span data-stu-id="e1c5c-478">Web API</span></span> | 
| <span data-ttu-id="e1c5c-479">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-479">**SDL Phase**</span></span>               | <span data-ttu-id="e1c5c-480">Создание</span><span class="sxs-lookup"><span data-stu-id="e1c5c-480">Build</span></span> |  
| <span data-ttu-id="e1c5c-481">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-481">**Applicable Technologies**</span></span> | <span data-ttu-id="e1c5c-482">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="e1c5c-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="e1c5c-483">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-483">**Attributes**</span></span>              | <span data-ttu-id="e1c5c-484">Поставщик удостоверений — ADFS или Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1c5c-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="e1c5c-485">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-485">**References**</span></span>              | [<span data-ttu-id="e1c5c-486">Статья об обеспечении безопасности веб-интерфейсов API с помощью отдельной учетной записи и локального имени входа в веб-API ASP.NET 2.2</span><span class="sxs-lookup"><span data-stu-id="e1c5c-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="e1c5c-487">**Действия**</span><span class="sxs-lookup"><span data-stu-id="e1c5c-487">**Steps**</span></span> | <span data-ttu-id="e1c5c-488">Если веб-API hello защищена с помощью OAuth 2.0, затем ожидается, что токен носителя в запросе авторизации в запрос заголовок и предоставляет доступ toohello только в том случае, если маркер hello является действительным.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-488">If hello Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access toohello request only if hello token is valid.</span></span> <span data-ttu-id="e1c5c-489">В отличие от проверки подлинности на основе файла cookie браузеры не подключайте toorequests токенов предъявителя hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-489">Unlike cookie based authentication, browsers do not attach hello bearer tokens toorequests.</span></span> <span data-ttu-id="e1c5c-490">Клиент должен tooexplicitly запросом Hello присоединить hello токена носителя в заголовке запроса hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-490">hello requesting client needs tooexplicitly attach hello bearer token in hello request header.</span></span> <span data-ttu-id="e1c5c-491">Таким образом, в веб-интерфейсах API ASP.NET, защищенных с помощью OAuth 2.0, токены носителя используются для защиты от подделки межсайтовых запросов.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="e1c5c-492">Пожалуйста Обратите внимание, что если hello MVC часть приложения hello использует проверку подлинности форм (т. е. Использование куки-файлы), маркеров защиты от подделки toobe, используемые веб-приложения MVC hello.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-492">Please note that if hello MVC portion of hello application uses forms authentication (i.e., uses cookies), anti-forgery tokens have toobe used by hello MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="e1c5c-493">Пример</span><span class="sxs-lookup"><span data-stu-id="e1c5c-493">Example</span></span>
<span data-ttu-id="e1c5c-494">Hello веб-API имеет toobe проинформировать toorely только на токены носителя, а не на файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="e1c5c-494">hello Web API has toobe informed toorely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="e1c5c-495">Это можно сделать путем hello следующая конфигурация в `WebApiConfig.Register` метод: '' "Си-шарп кода конфигурации. SuppressDefaultHostAuthentication(); Конфигурация. Filters.Add (новый HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="e1c5c-495">It can be done by hello following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
