---
title: "запрос aaaAdvanced регулирования со службой управления API Azure"
description: "Узнайте, как toocreate применение гибкую квоту и политики управления API Azure ограничение частоты."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="5e6da-103">Расширенное регулирование запросов с помощью API Management</span><span class="sxs-lookup"><span data-stu-id="5e6da-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="5e6da-104">Может toothrottle входящие запросы, — это ключевой роль управления API Azure.</span><span class="sxs-lookup"><span data-stu-id="5e6da-104">Being able toothrottle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="5e6da-105">Позволяет либо управляющий hello скорости запросов или общее количество запросов в hello данных перемещаются, API управления API поставщиков tooprotect их интерфейсов API из о нарушении и создания значения для различных уровней API продукта.</span><span class="sxs-lookup"><span data-stu-id="5e6da-105">Either by controlling hello rate of requests or hello total requests/data transferred, API Management allows API providers tooprotect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="5e6da-106">Регулирование запросов на основе продукта</span><span class="sxs-lookup"><span data-stu-id="5e6da-106">Product based throttling</span></span>
<span data-ttu-id="5e6da-107">toodate скорость hello возможности регулирования были определенной подписки ограниченный toobeing области tooa (фактически ключ), определенные на hello портал издателя управления API.</span><span class="sxs-lookup"><span data-stu-id="5e6da-107">toodate, hello rate throttling capabilities have been limited toobeing scoped tooa particular Product subscription (essentially a key), defined in hello API Management publisher portal.</span></span> <span data-ttu-id="5e6da-108">Это полезно для hello API поставщика tooapply ограничения на hello разработчики, которые зарегистрировались toouse их API, однако он не помогает, например, регулирования отдельным конечным пользователям hello API.</span><span class="sxs-lookup"><span data-stu-id="5e6da-108">This is useful for hello API provider tooapply limits on hello developers who have signed up toouse their API, however, it does not help, for example, in throttling individual end-users of hello API.</span></span> <span data-ttu-id="5e6da-109">Это возможно, что для одного пользователя tooconsume hello разработчик приложения hello всей квоты и затем предотвращают другим клиентам hello разработчик может toouse приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5e6da-109">It is possible that for single user of hello developer's application tooconsume hello entire quota and then prevent other customers of hello developer from being able toouse hello application.</span></span> <span data-ttu-id="5e6da-110">Кроме того несколько клиентов, которые может создавать большое количество запросов может ограничить доступ toooccasional пользователей.</span><span class="sxs-lookup"><span data-stu-id="5e6da-110">Also, several customers who might generate a high volume of requests may limit access toooccasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="5e6da-111">Регулирование запросов на основе настраиваемых ключей</span><span class="sxs-lookup"><span data-stu-id="5e6da-111">Custom key based throttling</span></span>
<span data-ttu-id="5e6da-112">новый Hello [скорость ограничение по ключ](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) и [ключ квоты](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) политики предоставляют значительно более гибкий элемент управления tootraffic решения.</span><span class="sxs-lookup"><span data-stu-id="5e6da-112">hello new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution tootraffic control.</span></span> <span data-ttu-id="5e6da-113">Эти новые политики позволяют toodefine выражений tooidentify hello ключи, которые будут используется tootrack использования трафика.</span><span class="sxs-lookup"><span data-stu-id="5e6da-113">These new policies allow you toodefine expressions tooidentify hello keys that will be used tootrack traffic usage.</span></span> <span data-ttu-id="5e6da-114">Привет, как это работает простых проиллюстрирован с примерами.</span><span class="sxs-lookup"><span data-stu-id="5e6da-114">hello way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="5e6da-115">Регулирование запросов по IP-адресам</span><span class="sxs-lookup"><span data-stu-id="5e6da-115">IP Address throttling</span></span>
<span data-ttu-id="5e6da-116">Hello следующие политики ограничения один tooonly адрес IP клиента 10 вызывает каждую минуту с общим 1 000 000 вызовов и 10 000 килобайт пропускной способности для каждого месяца.</span><span class="sxs-lookup"><span data-stu-id="5e6da-116">hello following policies restrict a single client IP address tooonly 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="5e6da-117">Если все клиенты в Интернете hello уникальный IP-адрес, это может быть эффективным способом ограничения использования пользователем.</span><span class="sxs-lookup"><span data-stu-id="5e6da-117">If all clients on hello Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="5e6da-118">Тем не менее вполне вероятно, что несколько пользователей будут один общий IP-адрес из-за доступ к hello toothem Интернета через устройство NAT для управления доступом.</span><span class="sxs-lookup"><span data-stu-id="5e6da-118">However, it is quite likely that multiple users will sharing a single public IP address due toothem accessing hello Internet via a NAT device.</span></span> <span data-ttu-id="5e6da-119">Несмотря на это, для интерфейсов API, позволяющих доступ без проверки подлинности hello `IpAddress` может быть лучшим вариантом hello.</span><span class="sxs-lookup"><span data-stu-id="5e6da-119">Despite this, for APIs that allow unauthenticated access hello `IpAddress` might be hello best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="5e6da-120">Регулирование запросов по удостоверениям пользователя</span><span class="sxs-lookup"><span data-stu-id="5e6da-120">User identity throttling</span></span>
<span data-ttu-id="5e6da-121">Если пользователь прошел проверку подлинности, на основе данных, уникально идентифицирующих этого пользователя, генерируется ключ регулирования.</span><span class="sxs-lookup"><span data-stu-id="5e6da-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="5e6da-122">В этом примере мы извлечь hello заголовок Authorization, преобразуйте его слишком`JWT` объекта и использовать субъекта hello hello маркера tooidentify hello пользователя и использовать его как ограничение ключа частоты hello.</span><span class="sxs-lookup"><span data-stu-id="5e6da-122">In this example we extract hello Authorization header, convert it too`JWT` object and use hello subject of hello token tooidentify hello user and use that as hello rate limiting key.</span></span> <span data-ttu-id="5e6da-123">Если удостоверение пользователя hello хранится в hello `JWT` как один из других hello утверждений затем значение может использоваться вместо него.</span><span class="sxs-lookup"><span data-stu-id="5e6da-123">If hello user identity is stored in hello `JWT` as one of hello other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="5e6da-124">Объединенные политики</span><span class="sxs-lookup"><span data-stu-id="5e6da-124">Combined policies</span></span>
<span data-ttu-id="5e6da-125">Несмотря на то, что новые политики регулирования hello обеспечивают больший контроль, чем hello существующую политику регулирования, по-прежнему значение объединение обе возможности.</span><span class="sxs-lookup"><span data-stu-id="5e6da-125">Although hello new throttling policies provide more control than hello existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="5e6da-126">Регулирование по ключу продукта подписки ([ограничение частоты вызовов по подписке](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) и [набор квоты на использование по подписке](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) является отличным способом tooenable monetizing API-интерфейса путем однократного списания на основе использования уровней.</span><span class="sxs-lookup"><span data-stu-id="5e6da-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way tooenable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="5e6da-127">Hello более точный контроль того, что может toothrottle пользователем дополняет и предотвращает ухудшения качества hello другого поведение одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="5e6da-127">hello finer grained control of being able toothrottle by user is complementary and prevents one user's behavior from degrading hello experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="5e6da-128">Регулирование со стороны клиента</span><span class="sxs-lookup"><span data-stu-id="5e6da-128">Client driven throttling</span></span>
<span data-ttu-id="5e6da-129">Если hello регулирования ключ определен с помощью [выражение политики](https://msdn.microsoft.com/library/azure/dn910913.aspx), то hello API поставщика, который выбирает действует как регулирование hello.</span><span class="sxs-lookup"><span data-stu-id="5e6da-129">When hello throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is hello API provider that is choosing how hello throttling is scoped.</span></span> <span data-ttu-id="5e6da-130">Однако разработчик может потребоваться toocontrol, как они интенсивность ограничить своих клиентов.</span><span class="sxs-lookup"><span data-stu-id="5e6da-130">However, a developer might want toocontrol how they rate limit their own customers.</span></span> <span data-ttu-id="5e6da-131">Это может включить hello API поставщика путем введения разработчика tooallow пользовательский заголовок hello клиентского приложения toocommunicate hello ключа toohello API.</span><span class="sxs-lookup"><span data-stu-id="5e6da-131">This could be enabled by hello API provider by introducing a custom header tooallow hello developer's client application toocommunicate hello key toohello API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="5e6da-132">Это позволяет toochoose приложения hello разработчик клиента способ ограничение ключа частоты toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="5e6da-132">This enables hello developer's client application toochoose how they want toocreate hello rate limiting key.</span></span> <span data-ttu-id="5e6da-133">С помощью немного ingenuity разработчик клиента создать свои собственные уровни норм путем выделения наборов ключей toousers и поворот hello использования ключа.</span><span class="sxs-lookup"><span data-stu-id="5e6da-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys toousers and rotating hello key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="5e6da-134">Сводка</span><span class="sxs-lookup"><span data-stu-id="5e6da-134">Summary</span></span>
<span data-ttu-id="5e6da-135">Управления API Azure предоставляет скорость и квоты, регулирование tooboth защиты и добавить значение tooyour API-службы.</span><span class="sxs-lookup"><span data-stu-id="5e6da-135">Azure API Management provides rate and quote throttling tooboth protect and add value tooyour API service.</span></span> <span data-ttu-id="5e6da-136">новые политики настраиваемые правила выбора области регулирования Hello разрешающее вы точно Контролируемая контроль над tooenable этих политик приложений еще лучше toobuild клиентов.</span><span class="sxs-lookup"><span data-stu-id="5e6da-136">hello new throttling policies with custom scoping rules allow you finer grained control over those policies tooenable your customers toobuild even better applications.</span></span> <span data-ttu-id="5e6da-137">Hello в этой статье примерах hello использовать эти новые политики, ограничение ключи с IP-адресов клиентов, удостоверения пользователя и клиента, созданного значения частоты производства.</span><span class="sxs-lookup"><span data-stu-id="5e6da-137">hello examples in this article demonstrate hello use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="5e6da-138">Тем не менее существует много других частей сообщения hello, который может быть использован как агент пользователя, фрагментов пути URL-адрес, размер сообщения.</span><span class="sxs-lookup"><span data-stu-id="5e6da-138">However, there are many other parts of hello message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e6da-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e6da-139">Next steps</span></span>
<span data-ttu-id="5e6da-140">Отправьте нам ваши отзывы в потоке hello Disqus для этого раздела.</span><span class="sxs-lookup"><span data-stu-id="5e6da-140">Please give us your feedback in hello Disqus thread for this topic.</span></span> <span data-ttu-id="5e6da-141">Было бы отлично toohear о других возможных значений ключа, были логичным выбором в ваших сценариях.</span><span class="sxs-lookup"><span data-stu-id="5e6da-141">It would be great toohear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="5e6da-142">Посмотрите видеообзор этих политик.</span><span class="sxs-lookup"><span data-stu-id="5e6da-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="5e6da-143">Дополнительные сведения о hello [скорость ограничение по ключ](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) и [ключ квоты](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) политики, описанные в данной статье, обратите внимание на следующие видео hello.</span><span class="sxs-lookup"><span data-stu-id="5e6da-143">For more information on hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

