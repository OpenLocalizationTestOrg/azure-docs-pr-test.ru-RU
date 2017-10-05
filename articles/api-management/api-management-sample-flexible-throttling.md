---
title: "Расширенное регулирование запросов с помощью API Management"
description: "Узнайте, как создавать и применять гибкие квоты и политики ограничения частоты запросов, используя службу управления API Azure."
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
ms.openlocfilehash: 35375e599891a9443a91c4c3a8657e8c9c48c7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="3db8c-103">Расширенное регулирование запросов с помощью API Management</span><span class="sxs-lookup"><span data-stu-id="3db8c-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="3db8c-104">Возможность регулирования входящих запросов — ключевая роль службы управления Azure API.</span><span class="sxs-lookup"><span data-stu-id="3db8c-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="3db8c-105">Контролируя частоту запросов или общий объем запросов либо передаваемых данных, служба управления API позволяет поставщикам API предотвращать злоупотребление API и предлагать различные уровни API.</span><span class="sxs-lookup"><span data-stu-id="3db8c-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="3db8c-106">Регулирование запросов на основе продукта</span><span class="sxs-lookup"><span data-stu-id="3db8c-106">Product based throttling</span></span>
<span data-ttu-id="3db8c-107">На сегодняшний день возможности регулирования частоты запросов ограничиваются подпиской (ключом) конкретного продукта, определенной на портале издателя службы управления API.</span><span class="sxs-lookup"><span data-stu-id="3db8c-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span></span> <span data-ttu-id="3db8c-108">Это позволяет поставщику API устанавливать ограничения для разработчиков, зарегистрировавшихся для использования API, но не дает им возможность, например, регулировать отдельных конечных пользователей API.</span><span class="sxs-lookup"><span data-stu-id="3db8c-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span></span> <span data-ttu-id="3db8c-109">Есть вероятность, что отдельный пользователь приложения израсходует весь лимит, в результате чего остальные клиенты соответствующего разработчика не смогут работать с приложением.</span><span class="sxs-lookup"><span data-stu-id="3db8c-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="3db8c-110">Кроме того, несколько клиентов, создающих большое число запросов, могут затруднять доступ для пользователей, которые обращаются к приложению редко.</span><span class="sxs-lookup"><span data-stu-id="3db8c-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="3db8c-111">Регулирование запросов на основе настраиваемых ключей</span><span class="sxs-lookup"><span data-stu-id="3db8c-111">Custom key based throttling</span></span>
<span data-ttu-id="3db8c-112">Новые политики [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) и [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) увеличивают гибкость управления трафиком.</span><span class="sxs-lookup"><span data-stu-id="3db8c-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span></span> <span data-ttu-id="3db8c-113">Они позволяют определять выражения для идентификации ключей, которые будут использоваться для контроля за объемом трафика.</span><span class="sxs-lookup"><span data-stu-id="3db8c-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span></span> <span data-ttu-id="3db8c-114">Принцип работы этих политик лучше всего демонстрирует пример.</span><span class="sxs-lookup"><span data-stu-id="3db8c-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="3db8c-115">Регулирование запросов по IP-адресам</span><span class="sxs-lookup"><span data-stu-id="3db8c-115">IP Address throttling</span></span>
<span data-ttu-id="3db8c-116">Описанные ниже политики накладывают на каждый IP-адрес клиента следующие ограничения: не более 10 запросов в минуту и не более 1 000 000 вызовов и 10 000 килобайт пропускной способности в месяц.</span><span class="sxs-lookup"><span data-stu-id="3db8c-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="3db8c-117">Если все клиенты в Интернете используют уникальный IP-адрес, этот способ позволит эффективно ограничить расход трафика для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="3db8c-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="3db8c-118">Однако часто случается, что несколько пользователей делят один общедоступный IP-адрес, поскольку доступ в Интернет им предоставляется через транслятор сетевых адресов.</span><span class="sxs-lookup"><span data-stu-id="3db8c-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="3db8c-119">Но даже в этом случае для API, разрешающих доступ к `IpAddress` без проверки подлинности, этот вариант оптимален.</span><span class="sxs-lookup"><span data-stu-id="3db8c-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="3db8c-120">Регулирование запросов по удостоверениям пользователя</span><span class="sxs-lookup"><span data-stu-id="3db8c-120">User identity throttling</span></span>
<span data-ttu-id="3db8c-121">Если пользователь прошел проверку подлинности, на основе данных, уникально идентифицирующих этого пользователя, генерируется ключ регулирования.</span><span class="sxs-lookup"><span data-stu-id="3db8c-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="3db8c-122">В данном примере мы извлекаем заголовок Authorization (Авторизация), конвертируем его в объект `JWT` , а затем используем субъект маркера для идентификации пользователя и в качестве ключа для ограничения частоты запросов.</span><span class="sxs-lookup"><span data-stu-id="3db8c-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="3db8c-123">Если удостоверение пользователя хранится в `JWT` вместе с другими утверждениями, вместо него можно использовать соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="3db8c-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="3db8c-124">Объединенные политики</span><span class="sxs-lookup"><span data-stu-id="3db8c-124">Combined policies</span></span>
<span data-ttu-id="3db8c-125">Несмотря на то, что новые политики регулирования дают больше контроля, чем предыдущие, их можно выгодно объединять.</span><span class="sxs-lookup"><span data-stu-id="3db8c-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="3db8c-126">Регулирование с использованием ключа подписки продукта (см. разделы [Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) (Ограничение частоты вызовов по подписке) и [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) (Задание квоты использования по подписке)) — это отличный способ получения прибыли от API, основанный на уровнях использования.</span><span class="sxs-lookup"><span data-stu-id="3db8c-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="3db8c-127">Кроме того, появляется возможность более точно регулировать запросы по пользователям, не позволяя одному пользователю мешать другим.</span><span class="sxs-lookup"><span data-stu-id="3db8c-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="3db8c-128">Регулирование со стороны клиента</span><span class="sxs-lookup"><span data-stu-id="3db8c-128">Client driven throttling</span></span>
<span data-ttu-id="3db8c-129">Если ключ регулирования определяется с использованием [выражения политики](https://msdn.microsoft.com/library/azure/dn910913.aspx), объемы регулирования определяются поставщиком API.</span><span class="sxs-lookup"><span data-stu-id="3db8c-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="3db8c-130">При этом разработчик может предпочитать самостоятельный контроль над ограничением частоты запросов для своих пользователей.</span><span class="sxs-lookup"><span data-stu-id="3db8c-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="3db8c-131">Для этого поставщик API может ввести настраиваемый заголовок, позволяющий клиентскому приложению разработчика передавать ключ в API.</span><span class="sxs-lookup"><span data-stu-id="3db8c-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="3db8c-132">Это позволит клиентскому приложению разработчика выбирать способ создания ключа, ограничивающего частоту запросов.</span><span class="sxs-lookup"><span data-stu-id="3db8c-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="3db8c-133">Проявив немного изобретательности, разработчик клиента может создать свои собственные уровни частоты запросов, назначив пользователям наборы ключей и контролируя их использование.</span><span class="sxs-lookup"><span data-stu-id="3db8c-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="3db8c-134">Сводка</span><span class="sxs-lookup"><span data-stu-id="3db8c-134">Summary</span></span>
<span data-ttu-id="3db8c-135">Служба управления API позволяет регулировать частоту запросов и квоты для защиты и повышения эффективности API.</span><span class="sxs-lookup"><span data-stu-id="3db8c-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="3db8c-136">Новые политики регулирования с настраиваемыми правилами масштабирования позволяют контролировать политики более точно и дают вашим клиентам возможность создавать еще более качественные приложения.</span><span class="sxs-lookup"><span data-stu-id="3db8c-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="3db8c-137">Примеры в этой статье демонстрируют применение новых политик в виде создания ключей для ограничения частоты запросов по IP-адресам клиентов, удостоверениям пользователей и значениям, формируемым клиентами.</span><span class="sxs-lookup"><span data-stu-id="3db8c-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="3db8c-138">В то же время можно использовать и многие другие части сообщений, включая агентов пользователей, фрагменты URL-адресов и размеры сообщений.</span><span class="sxs-lookup"><span data-stu-id="3db8c-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3db8c-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3db8c-139">Next steps</span></span>
<span data-ttu-id="3db8c-140">Сообщите нам свое мнение в обсуждении Disqus.</span><span class="sxs-lookup"><span data-stu-id="3db8c-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="3db8c-141">Мы будем рады узнать о других возможных значениях ключей, подходящих для вашего случая.</span><span class="sxs-lookup"><span data-stu-id="3db8c-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="3db8c-142">Посмотрите видеообзор этих политик.</span><span class="sxs-lookup"><span data-stu-id="3db8c-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="3db8c-143">Дополнительные сведения о политиках [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) и [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey), которые рассматриваются в этой статье, см. в следующем видео.</span><span class="sxs-lookup"><span data-stu-id="3db8c-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

