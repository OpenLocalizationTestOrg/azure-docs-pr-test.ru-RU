---
title: "Использование Azure CDN с CORS | Документация Майкрософт"
description: "Сведения об использовании сети доставки содержимого (CDN) Azure с общим доступом к ресурсам независимо от источника (CORS)."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7070397f6e69b21add75bad8220f0b8ebe36d266
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="23f01-103">Использование Azure CDN с CORS</span><span class="sxs-lookup"><span data-stu-id="23f01-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="23f01-104">Что такое CORS?</span><span class="sxs-lookup"><span data-stu-id="23f01-104">What is CORS?</span></span>
<span data-ttu-id="23f01-105">CORS (общий доступ к ресурсам независимо от источника) — функция HTTP, которая позволяет веб-приложению, работающему в одном домене, обращаться к ресурсам другого домена.</span><span class="sxs-lookup"><span data-stu-id="23f01-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="23f01-106">Чтобы снизить вероятность атак с использованием межузловых сценариев, все современные веб-браузеры реализуют ограничение безопасности, известное как [политика одного источника](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="23f01-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="23f01-107">Это ограничение не позволяет веб-страницы вызывать интерфейсы API в другом домене.</span><span class="sxs-lookup"><span data-stu-id="23f01-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="23f01-108">CORS позволяет одному источнику (исходному домену) безопасно вызывать интерфейсы API в другом источнике.</span><span class="sxs-lookup"><span data-stu-id="23f01-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="23f01-109">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="23f01-109">How it works</span></span>
<span data-ttu-id="23f01-110">Существует два типа запросов CORS, *простые запросы* и *сложные запросы*.</span><span class="sxs-lookup"><span data-stu-id="23f01-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="23f01-111">Простые запросы</span><span class="sxs-lookup"><span data-stu-id="23f01-111">For simple requests:</span></span>

1. <span data-ttu-id="23f01-112">Браузер отправляет запрос CORS с дополнительным заголовком HTTP-запроса **Origin**.</span><span class="sxs-lookup"><span data-stu-id="23f01-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="23f01-113">Значение этого заголовка является источником, обслужившим родительскую страницу, который определяется как сочетание *протокола*, *домена* и *порта*.</span><span class="sxs-lookup"><span data-stu-id="23f01-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="23f01-114">Когда страница сайта https://www.contoso.com попытается получить доступ к данным пользователя в источнике fabrikam.com, на fabrikam.com отправится запрос со следующим заголовком.</span><span class="sxs-lookup"><span data-stu-id="23f01-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="23f01-115">Сервер может отправить в ответ следующее:</span><span class="sxs-lookup"><span data-stu-id="23f01-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="23f01-116">Ответ с заголовком **Access-Control-Allow-Origin**, который указывает, какие исходные сайты разрешены.</span><span class="sxs-lookup"><span data-stu-id="23f01-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="23f01-117">Например:</span><span class="sxs-lookup"><span data-stu-id="23f01-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="23f01-118">Код ошибки HTTP (например, 403), если сервер запрещает запрос независимо от источника после проверки заголовка Origin.</span><span class="sxs-lookup"><span data-stu-id="23f01-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="23f01-119">Заголовок **Access-Control-Allow-Origin** с подстановочным знаком, который разрешает все источники:</span><span class="sxs-lookup"><span data-stu-id="23f01-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="23f01-120">Сложные запросы</span><span class="sxs-lookup"><span data-stu-id="23f01-120">For complex requests:</span></span>

<span data-ttu-id="23f01-121">Сложный запрос — это запрос CORS, для выполнения которого браузер должен отправить *предварительный запрос* (т. е. предварительную пробу) перед отправкой самого запроса CORS.</span><span class="sxs-lookup"><span data-stu-id="23f01-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="23f01-122">Предварительный запрос запрашивает у сервера разрешения на выполнение исходного запроса CORS. Он представляет собой запрос `OPTIONS` к тому же URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="23f01-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="23f01-123">Дополнительные сведения о процедурах CORS и типичных проблемах доступны в [руководстве по CORS для REST API](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="23f01-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="23f01-124">Подстановочный знак или сценарии с одним источником</span><span class="sxs-lookup"><span data-stu-id="23f01-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="23f01-125">CORS в Azure CDN будет работать автоматически без дополнительной настройки, если в заголовке **Access-Control-Allow-Origin** указан подстановочный знак (*) или один источник.</span><span class="sxs-lookup"><span data-stu-id="23f01-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin.</span></span>  <span data-ttu-id="23f01-126">В этом случае CDN кэширует первый ответ, и в последующих запросах будет использоваться тот же заголовок.</span><span class="sxs-lookup"><span data-stu-id="23f01-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="23f01-127">Если запросы в CDN были отправлены до настройки CORS на вашем источнике, потребуется очистить содержимое конечной точки, чтобы обновить содержимое с заголовком **Access-Control-Allow-Origin** .</span><span class="sxs-lookup"><span data-stu-id="23f01-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="23f01-128">Сценарии с несколькими источниками</span><span class="sxs-lookup"><span data-stu-id="23f01-128">Multiple origin scenarios</span></span>
<span data-ttu-id="23f01-129">Если необходимо разрешить для CORS определенный набор источников, задача несколько усложняется.</span><span class="sxs-lookup"><span data-stu-id="23f01-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="23f01-130">Проблема возникает, когда CDN кэширует заголовок **Access-Control-Allow-Origin** для первого источника CORS.</span><span class="sxs-lookup"><span data-stu-id="23f01-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="23f01-131">При последующем запросе от другого источника CORS сеть CDN отправит кэшированный заголовок **Access-Control-Allow-Origin**, который не будет соответствовать заголовку другого источника.</span><span class="sxs-lookup"><span data-stu-id="23f01-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="23f01-132">Исправить это можно несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="23f01-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="23f01-133">Azure CDN уровня "Премиум" от Verizon</span><span class="sxs-lookup"><span data-stu-id="23f01-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="23f01-134">Удобнее всего воспользоваться **Azure CDN уровня "Премиум" от Verizon**с некоторыми дополнительными функциями.</span><span class="sxs-lookup"><span data-stu-id="23f01-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="23f01-135">Вам потребуется [создать правило](cdn-rules-engine.md) для проверки заголовка запроса **Origin** .</span><span class="sxs-lookup"><span data-stu-id="23f01-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="23f01-136">Если это допустимый источник, то ваше правило установит заголовок **Access-Control-Allow-Origin** в соответствии с источником, указанным в запросе.</span><span class="sxs-lookup"><span data-stu-id="23f01-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="23f01-137">Если источник, указанный в заголовке **Origin**, не является допустимым, то ваше правило должно опустить заголовок **Access-Control-Allow-Origin**, что заставит браузер отклонить запрос.</span><span class="sxs-lookup"><span data-stu-id="23f01-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="23f01-138">С помощью обработчика правил это можно сделать двумя способами.</span><span class="sxs-lookup"><span data-stu-id="23f01-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="23f01-139">В обоих случаях заголовок **Access-Control-Allow-Origin** из файла сервера-источника полностью игнорируется, и разрешенными источниками CORS управляет только обработчик правил CDN.</span><span class="sxs-lookup"><span data-stu-id="23f01-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="23f01-140">Одно регулярное выражение со всеми допустимыми источниками</span><span class="sxs-lookup"><span data-stu-id="23f01-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="23f01-141">В этом случае создается регулярное выражение, которое включает все источники, которые вы хотите разрешить:</span><span class="sxs-lookup"><span data-stu-id="23f01-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="23f01-142">В **Azure CDN от Verizon** в качестве основного механизма регулярных выражений используются [совместимые с Perl регулярные выражения](http://pcre.org/).</span><span class="sxs-lookup"><span data-stu-id="23f01-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="23f01-143">Для проверки регулярного выражения можно использовать такие ресурсы, как [Regular Expressions 101](https://regex101.com/).</span><span class="sxs-lookup"><span data-stu-id="23f01-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="23f01-144">Обратите внимание, что символ "/" в регулярных выражениях является допустимым и экранировать его необязательно. Однако его все же рекомендуется экранировать, и некоторые средства проверки регулярных выражений ожидают, что он будет экранирован.</span><span class="sxs-lookup"><span data-stu-id="23f01-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="23f01-145">Если регулярное выражение соответствует запросу, то правило заменит заголовок **Access-Control-Allow-Origin** источника (если он есть) на источник, который отправил запрос.</span><span class="sxs-lookup"><span data-stu-id="23f01-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="23f01-146">Также можно добавить дополнительные заголовки CORS, например **Access-Control-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="23f01-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Пример правил с регулярным выражением](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="23f01-148">Правило заголовка запроса для каждого источника.</span><span class="sxs-lookup"><span data-stu-id="23f01-148">Request header rule for each origin.</span></span>
<span data-ttu-id="23f01-149">Вместо регулярных выражений можно создать отдельное правило для каждого источника, который вы хотите разрешить, с помощью **условия соответствия** [подстановочного знака в заголовке запроса](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="23f01-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="23f01-150">Как и регулярное выражение, заголовки CORS задаются только обработчиком правил.</span><span class="sxs-lookup"><span data-stu-id="23f01-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![Пример правил без регулярного выражения](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="23f01-152">В примере выше подстановочный знак * означает, что обработчик правил будет проверять на соответствие как HTTP-, так и HTTPS-запросы.</span><span class="sxs-lookup"><span data-stu-id="23f01-152">In the example above, the use of the wildcard character * tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="23f01-153">Azure CDN уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="23f01-153">Azure CDN Standard</span></span>
<span data-ttu-id="23f01-154">Единственный механизм, который разрешает наличие нескольких источников без использования источника с подстановочным знаком в профилях Azure CDN уровня "Стандартный" — это [кэширование строки запроса](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="23f01-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="23f01-155">Вам необходимо включить параметр строки запроса для конечной точки CDN, а затем использовать уникальную строку запроса для запросов от каждого разрешенного домена.</span><span class="sxs-lookup"><span data-stu-id="23f01-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="23f01-156">Это приведет к тому, что CDN будет кэшировать отдельный объект для каждой уникальной строки запроса.</span><span class="sxs-lookup"><span data-stu-id="23f01-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="23f01-157">Однако этот подход не является идеальным, так как он приведет к появлению нескольких копий одного файла в кэше CDN.</span><span class="sxs-lookup"><span data-stu-id="23f01-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  

