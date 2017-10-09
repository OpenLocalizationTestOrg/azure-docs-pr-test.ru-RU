---
title: "aaaUsing CDN Azure с CORS | Документы Microsoft"
description: "Узнайте, как toouse hello Azure доставки содержимого сети (CDN) toowith общий доступ к ресурсам независимо от источника (CORS)."
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
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="9e632-103">Использование Azure CDN с CORS</span><span class="sxs-lookup"><span data-stu-id="9e632-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="9e632-104">Что такое CORS?</span><span class="sxs-lookup"><span data-stu-id="9e632-104">What is CORS?</span></span>
<span data-ttu-id="9e632-105">CORS (кросс-Origin доступ к ресурсам) является функцией HTTP, который позволяет веб-приложение в пределах одного домена tooaccess ресурсы в другом домене.</span><span class="sxs-lookup"><span data-stu-id="9e632-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain tooaccess resources in another domain.</span></span> <span data-ttu-id="9e632-106">В порядке tooreduce hello вероятность атак с использованием межсайтовых сценариев, все современных веб-браузеры имеют ограничение безопасности называется [политика одного источника](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="9e632-106">In order tooreduce hello possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="9e632-107">Это ограничение не позволяет веб-страницы вызывать интерфейсы API в другом домене.</span><span class="sxs-lookup"><span data-stu-id="9e632-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="9e632-108">CORS обеспечивают безопасный способ tooallow один источник (hello исходный домен) toocall API-интерфейсы в другой источник.</span><span class="sxs-lookup"><span data-stu-id="9e632-108">CORS provides a secure way tooallow one origin (hello origin domain) toocall APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="9e632-109">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="9e632-109">How it works</span></span>
<span data-ttu-id="9e632-110">Существует два типа запросов CORS, *простые запросы* и *сложные запросы*.</span><span class="sxs-lookup"><span data-stu-id="9e632-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="9e632-111">Простые запросы</span><span class="sxs-lookup"><span data-stu-id="9e632-111">For simple requests:</span></span>

1. <span data-ttu-id="9e632-112">Hello браузер отправляет запрос CORS hello с дополнительным **источника** заголовка HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="9e632-112">hello browser sends hello CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="9e632-113">Hello значение этого заголовка — источник hello, обработавшего hello родительская страница, которая определяется как сочетание hello *протокола,* *домена,* и *порта.*</span><span class="sxs-lookup"><span data-stu-id="9e632-113">hello value of this header is hello origin that served hello parent page, which is defined as hello combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="9e632-114">Если отображается страница https://www.contoso.com пытается tooaccess пользовательские данные в источник fabrikam.com hello, hello после заголовка запроса были бы отправлены toofabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="9e632-114">When a page from https://www.contoso.com attempts tooaccess a user's data in hello fabrikam.com origin, hello following request header would be sent toofabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="9e632-115">Hello сервер может ответить с любым из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="9e632-115">hello server may respond with any of hello following:</span></span>

   * <span data-ttu-id="9e632-116">Ответ с заголовком **Access-Control-Allow-Origin**, который указывает, какие исходные сайты разрешены.</span><span class="sxs-lookup"><span data-stu-id="9e632-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="9e632-117">Например:</span><span class="sxs-lookup"><span data-stu-id="9e632-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="9e632-118">Ошибка HTTP код например 403, если сервер hello не допускает hello независимо от источника запроса после проверки заголовка Origin hello</span><span class="sxs-lookup"><span data-stu-id="9e632-118">An HTTP error code such as 403 if hello server does not allow hello cross-origin request after checking hello Origin header</span></span>

   * <span data-ttu-id="9e632-119">Заголовок **Access-Control-Allow-Origin** с подстановочным знаком, который разрешает все источники:</span><span class="sxs-lookup"><span data-stu-id="9e632-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="9e632-120">Сложные запросы</span><span class="sxs-lookup"><span data-stu-id="9e632-120">For complex requests:</span></span>

<span data-ttu-id="9e632-121">Сложный запрос является запросом CORS, где требуется toosend браузера hello *Предварительный запрос* (т. е. предварительной выборки) перед отправкой самого запроса CORS hello.</span><span class="sxs-lookup"><span data-stu-id="9e632-121">A complex request is a CORS request where hello browser is required toosend a *preflight request* (i.e. a preliminary probe) before sending hello actual CORS request.</span></span> <span data-ttu-id="9e632-122">Hello Предварительный запрос запрашивает разрешение hello server Если hello первоначальный запрос CORS можно продолжить работу, а `OPTIONS` запроса toohello же URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9e632-122">hello preflight request asks hello server permission if hello original CORS request can proceed and is an `OPTIONS` request toohello same URL.</span></span>

> [!TIP]
> <span data-ttu-id="9e632-123">Дополнительные сведения о CORS потоков и типичные проблемы просмотрите hello [руководства по API REST tooCORS](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="9e632-123">For more details on CORS flows and common pitfalls, view hello [Guide tooCORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="9e632-124">Подстановочный знак или сценарии с одним источником</span><span class="sxs-lookup"><span data-stu-id="9e632-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="9e632-125">CORS в Azure CDN будет автоматически работать без дополнительной настройки, когда hello **Access-Control-Allow-Origin** задан заголовок toowildcard (*) или один источник.</span><span class="sxs-lookup"><span data-stu-id="9e632-125">CORS on Azure CDN will work automatically with no additional configuration when hello **Access-Control-Allow-Origin** header is set toowildcard (*) or a single origin.</span></span>  <span data-ttu-id="9e632-126">Hello CDN кэширует первого ответа hello и последующие запросы будут использовать hello же заголовок.</span><span class="sxs-lookup"><span data-stu-id="9e632-126">hello CDN will cache hello first response and subsequent requests will use hello same header.</span></span>

<span data-ttu-id="9e632-127">Если запросы уже выполнены предыдущие tooCORS toohello CDN, задаваемого hello источника, необходимо будет toopurge содержимое на ваш конечная точка содержимого tooreload hello содержимого с hello **Access-Control-Allow-Origin** заголовок.</span><span class="sxs-lookup"><span data-stu-id="9e632-127">If requests have already been made toohello CDN prior tooCORS being set on hello your origin, you will need toopurge content on your endpoint content tooreload hello content with hello **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="9e632-128">Сценарии с несколькими источниками</span><span class="sxs-lookup"><span data-stu-id="9e632-128">Multiple origin scenarios</span></span>
<span data-ttu-id="9e632-129">Если вам требуется tooallow определенного списка toobe источников, разрешенное для CORS, все еще немного усложняется.</span><span class="sxs-lookup"><span data-stu-id="9e632-129">If you need tooallow a specific list of origins toobe allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="9e632-130">Hello проблема возникает, когда hello CDN кэширует hello **Access-Control-Allow-Origin** заголовок для hello первый источник CORS.</span><span class="sxs-lookup"><span data-stu-id="9e632-130">hello problem occurs when hello CDN caches hello **Access-Control-Allow-Origin** header for hello first CORS origin.</span></span>  <span data-ttu-id="9e632-131">При последующих запрашивает другой источник CORS, hello CDN будет обслуживать hello в кэше **Access-Control-Allow-Origin** заголовок, который не будет совпадать.</span><span class="sxs-lookup"><span data-stu-id="9e632-131">When a different CORS origin makes a subsequent request, hello CDN will serve hello cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="9e632-132">Существует несколько способов toocorrect это.</span><span class="sxs-lookup"><span data-stu-id="9e632-132">There are several ways toocorrect this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="9e632-133">Azure CDN уровня "Премиум" от Verizon</span><span class="sxs-lookup"><span data-stu-id="9e632-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="9e632-134">Здравствуйте, лучшим способом tooenable это toouse **Azure CDN Premium из Verizon**, которая предоставляет некоторые расширенные функции.</span><span class="sxs-lookup"><span data-stu-id="9e632-134">hello best way tooenable this is toouse **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="9e632-135">Вам потребуется слишком[создать правило](cdn-rules-engine.md) toocheck hello **источника** заголовка запроса hello.</span><span class="sxs-lookup"><span data-stu-id="9e632-135">You'll need too[create a rule](cdn-rules-engine.md) toocheck hello **Origin** header on hello request.</span></span>  <span data-ttu-id="9e632-136">Если это допустимый источник вашей правило будет задавать hello **Access-Control-Allow-Origin** заголовок с hello источник, указанный в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="9e632-136">If it's a valid origin, your rule will set hello **Access-Control-Allow-Origin** header with hello origin provided in hello request.</span></span>  <span data-ttu-id="9e632-137">Если указан источник hello в hello **источника** заголовок не допускается, правила следует пропустить hello **Access-Control-Allow-Origin** заголовок, что вызовет запроса hello tooreject обозревателя hello.</span><span class="sxs-lookup"><span data-stu-id="9e632-137">If hello origin specified in hello **Origin** header is not allowed, your rule should omit hello **Access-Control-Allow-Origin** header which will cause hello browser tooreject hello request.</span></span> 

<span data-ttu-id="9e632-138">Существует два способа toodo это с помощью модуля правил hello.</span><span class="sxs-lookup"><span data-stu-id="9e632-138">There are two ways toodo this with hello rules engine.</span></span>  <span data-ttu-id="9e632-139">В обоих случаях hello **Access-Control-Allow-Origin** заголовок из файла hello исходного сервера не оказывает никакого влияния, обработчик правил hello CDN полностью управляет hello допускается источников CORS.</span><span class="sxs-lookup"><span data-stu-id="9e632-139">In both cases, hello **Access-Control-Allow-Origin** header from hello file's origin server is completely ignored, hello CDN's rules engine completely manages hello allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="9e632-140">Одно регулярное выражение со всеми допустимыми источниками</span><span class="sxs-lookup"><span data-stu-id="9e632-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="9e632-141">В этом случае вы создадите регулярное выражение, которое включает в себя все источники hello требуется tooallow:</span><span class="sxs-lookup"><span data-stu-id="9e632-141">In this case, you'll create a regular expression that includes all of hello origins you want tooallow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="9e632-142">В **Azure CDN от Verizon** в качестве основного механизма регулярных выражений используются [совместимые с Perl регулярные выражения](http://pcre.org/).</span><span class="sxs-lookup"><span data-stu-id="9e632-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="9e632-143">Можно использовать средства, подобного [регулярных выражений 101](https://regex101.com/) toovalidate регулярное выражение.</span><span class="sxs-lookup"><span data-stu-id="9e632-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) toovalidate your regular expression.</span></span>  <span data-ttu-id="9e632-144">Обратите внимание, что символ hello «/» является допустимым в регулярных выражениях и не требует toobe escape-последовательность, однако экранирование этим символом считается лучшим способом и ожидаемых некоторые проверки регулярного выражения.</span><span class="sxs-lookup"><span data-stu-id="9e632-144">Note that hello "/" character is valid in regular expressions and doesn't need toobe escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="9e632-145">Если hello регулярное выражение сопоставляет, правила приведет к замене hello **Access-Control-Allow-Origin** заголовок (если таковые имеются), от начала координат hello с основанием hello, отправившего запрос hello.</span><span class="sxs-lookup"><span data-stu-id="9e632-145">If hello regular expression matches, your rule will replace hello **Access-Control-Allow-Origin** header (if any) from hello origin with hello origin that sent hello request.</span></span>  <span data-ttu-id="9e632-146">Также можно добавить дополнительные заголовки CORS, например **Access-Control-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="9e632-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Пример правил с регулярным выражением](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="9e632-148">Правило заголовка запроса для каждого источника.</span><span class="sxs-lookup"><span data-stu-id="9e632-148">Request header rule for each origin.</span></span>
<span data-ttu-id="9e632-149">Вместо того чтобы регулярные выражения, вместо этого можно создать отдельные правила для каждого источника нужно с помощью hello tooallow **подстановочные заголовок запроса** [условию](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="9e632-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish tooallow using hello **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="9e632-150">Как с помощью метода регулярного выражения hello hello система правил отдельно заголовки CORS hello наборов.</span><span class="sxs-lookup"><span data-stu-id="9e632-150">As with hello regular expression method, hello rules engine alone sets hello CORS headers.</span></span> 

![Пример правил без регулярного выражения](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="9e632-152">В приведенном выше примере hello, hello использование hello подстановочный знак * сообщает toomatch система правил hello HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9e632-152">In hello example above, hello use of hello wildcard character * tells hello rules engine toomatch both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="9e632-153">Azure CDN уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="9e632-153">Azure CDN Standard</span></span>
<span data-ttu-id="9e632-154">На Azure CDN стандартные профили hello только tooallow механизм для нескольких источников без использования hello происхождения hello подстановочный знак — toouse [запроса кэширование строки](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="9e632-154">On Azure CDN Standard profiles, hello only mechanism tooallow for multiple origins without hello use of hello wildcard origin is toouse [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="9e632-155">Требуется параметр строки запроса tooenable для конечной точки CDN hello и затем использовать строку запроса, уникальный для запросов в каждом домене разрешенных.</span><span class="sxs-lookup"><span data-stu-id="9e632-155">You need tooenable query string setting for hello CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="9e632-156">Это приведет к hello кэша отдельный объект для каждой строки уникальных запросов CDN.</span><span class="sxs-lookup"><span data-stu-id="9e632-156">Doing this will result in hello CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="9e632-157">Этот подход не является идеальным, тем не менее, как это приведет к несколько копий hello тот же файл в кэш hello CDN.</span><span class="sxs-lookup"><span data-stu-id="9e632-157">This approach is not ideal, however, as it will result in multiple copies of hello same file cached on hello CDN.</span></span>  

