---
title: "ограничения запросов диспетчера ресурсов aaaAzure | Документы Microsoft"
description: "Описывает, как toouse регулирования Azure Resource Manager запрашивает достижении ограничения подписки."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="fa720-103">Регулирование запросов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fa720-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="fa720-104">Для каждой подписки и клиента ограничения диспетчера ресурсов чтения too15 запросы, 000 в час и записи too1 запросы, 200 в час.</span><span class="sxs-lookup"><span data-stu-id="fa720-104">For each subscription and tenant, Resource Manager limits read requests too15,000 per hour and write requests too1,200 per hour.</span></span> <span data-ttu-id="fa720-105">Эти ограничения относятся tooeach экземпляр диспетчера ресурсов Azure; Существует несколько экземпляров в каждом регионе Azure, и диспетчер ресурсов Azure — развернутой tooall Azure областей.</span><span class="sxs-lookup"><span data-stu-id="fa720-105">These limits apply tooeach Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed tooall Azure regions.</span></span>  <span data-ttu-id="fa720-106">На практике ограничений гораздо больше, чем указано выше, так как запросы пользователя обычно обслуживаются многими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="fa720-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="fa720-107">Если приложению или сценарию, достигает этих ограничений, вы должны toothrottle запросов.</span><span class="sxs-lookup"><span data-stu-id="fa720-107">If your application or script reaches these limits, you need toothrottle your requests.</span></span> <span data-ttu-id="fa720-108">В этом разделе показано, как toodetermine hello оставшихся запрашивает у вас есть до достижения предела hello и как toorespond при достижении максимального hello.</span><span class="sxs-lookup"><span data-stu-id="fa720-108">This topic shows you how toodetermine hello remaining requests you have before reaching hello limit, and how toorespond when you have reached hello limit.</span></span>

<span data-ttu-id="fa720-109">По достижении предела hello появляется код состояния hello HTTP **429 слишком много запросов**.</span><span class="sxs-lookup"><span data-stu-id="fa720-109">When you reach hello limit, you receive hello HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="fa720-110">Здравствуйте, число запросов является областью tooeither подписки или клиента.</span><span class="sxs-lookup"><span data-stu-id="fa720-110">hello number of requests is scoped tooeither your subscription or your tenant.</span></span> <span data-ttu-id="fa720-111">При наличии нескольких параллельных приложений, выполняющие запросы в вашей подписке hello запросы от этих приложений суммируются toodetermine hello число оставшихся запросов.</span><span class="sxs-lookup"><span data-stu-id="fa720-111">If you have multiple, concurrent applications making requests in your subscription, hello requests from those applications are added together toodetermine hello number of remaining requests.</span></span>

<span data-ttu-id="fa720-112">Запросы подписок область — это аргументы, hello включают передача идентификатором подписки, такие как извлечение hello групп ресурсов в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="fa720-112">Subscription scoped requests are ones hello involve passing your subscription id, such as retrieving hello resource groups in your subscription.</span></span> <span data-ttu-id="fa720-113">Запросы, ограничиваемые клиентом, не включают в себя идентификатор подписки (например, извлечение действительных расположений Azure).</span><span class="sxs-lookup"><span data-stu-id="fa720-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="fa720-114">Количество оставшихся запросов</span><span class="sxs-lookup"><span data-stu-id="fa720-114">Remaining requests</span></span>
<span data-ttu-id="fa720-115">Можно определить hello число оставшихся запросов на основе заголовков ответа.</span><span class="sxs-lookup"><span data-stu-id="fa720-115">You can determine hello number of remaining requests by examining response headers.</span></span> <span data-ttu-id="fa720-116">Каждый запрос содержит значения для hello количества оставшихся чтения и записи запросов.</span><span class="sxs-lookup"><span data-stu-id="fa720-116">Each request includes values for hello number of remaining read and write requests.</span></span> <span data-ttu-id="fa720-117">Hello следующей таблице описаны заголовки ответа hello, можно изучить для этих значений.</span><span class="sxs-lookup"><span data-stu-id="fa720-117">hello following table describes hello response headers you can examine for those values:</span></span>

| <span data-ttu-id="fa720-118">Заголовок ответа</span><span class="sxs-lookup"><span data-stu-id="fa720-118">Response header</span></span> | <span data-ttu-id="fa720-119">Описание</span><span class="sxs-lookup"><span data-stu-id="fa720-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fa720-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="fa720-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="fa720-121">Оставшееся количество запросов на чтение для подписки.</span><span class="sxs-lookup"><span data-stu-id="fa720-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="fa720-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="fa720-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="fa720-123">Оставшееся количество запросов на запись для подписки.</span><span class="sxs-lookup"><span data-stu-id="fa720-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="fa720-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="fa720-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="fa720-125">Оставшееся количество запросов на чтение для клиента.</span><span class="sxs-lookup"><span data-stu-id="fa720-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="fa720-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="fa720-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="fa720-127">Оставшееся количество запросов на запись для клиента.</span><span class="sxs-lookup"><span data-stu-id="fa720-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="fa720-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="fa720-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="fa720-129">Оставшееся количество запросов для типа ресурса для подписки.</span><span class="sxs-lookup"><span data-stu-id="fa720-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="fa720-130">Значение заголовка возвращается только в том случае, если служба переопределил ограничение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="fa720-130">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="fa720-131">Диспетчер ресурсов добавляет это значение вместо hello подписки чтения или записи.</span><span class="sxs-lookup"><span data-stu-id="fa720-131">Resource Manager adds this value instead of hello subscription reads or writes.</span></span> |
| <span data-ttu-id="fa720-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="fa720-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="fa720-133">Оставшееся количество запросов коллекции типов ресурсов для подписки.</span><span class="sxs-lookup"><span data-stu-id="fa720-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="fa720-134">Значение заголовка возвращается только в том случае, если служба переопределил ограничение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="fa720-134">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="fa720-135">Это значение предоставляет hello количество оставшихся сбора запросов (список ресурсы).</span><span class="sxs-lookup"><span data-stu-id="fa720-135">This value provides hello number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="fa720-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="fa720-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="fa720-137">Оставшееся количество запросов для типа ресурса для клиента.</span><span class="sxs-lookup"><span data-stu-id="fa720-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="fa720-138">Этот заголовок добавляется только для запросов на уровне клиента и только в том случае, если служба переопределил ограничение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="fa720-138">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> <span data-ttu-id="fa720-139">Диспетчер ресурсов добавляет это значение вместо приветствия клиента чтения или записи.</span><span class="sxs-lookup"><span data-stu-id="fa720-139">Resource Manager adds this value instead of hello tenant reads or writes.</span></span> |
| <span data-ttu-id="fa720-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="fa720-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="fa720-141">Оставшееся количество запросов коллекции типов ресурсов для клиента.</span><span class="sxs-lookup"><span data-stu-id="fa720-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="fa720-142">Этот заголовок добавляется только для запросов на уровне клиента и только в том случае, если служба переопределил ограничение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="fa720-142">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> |

## <a name="retrieving-hello-header-values"></a><span data-ttu-id="fa720-143">Извлечение значений из заголовка hello</span><span class="sxs-lookup"><span data-stu-id="fa720-143">Retrieving hello header values</span></span>
<span data-ttu-id="fa720-144">Получение этих значений заголовков в коде или сценарии ничем не отличается от извлечения любого другого значения заголовка.</span><span class="sxs-lookup"><span data-stu-id="fa720-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="fa720-145">Например, в **C#**, получить значение заголовка hello из **HttpWebResponse** объект с именем **ответ** с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="fa720-145">For example, in **C#**, you retrieve hello header value from an **HttpWebResponse** object named **response** with hello following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="fa720-146">В **PowerShell**, получить значение заголовка hello из операции Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="fa720-146">In **PowerShell**, you retrieve hello header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="fa720-147">Или, если хотите toosee hello оставшихся запросов для отладки, вы можете предоставить hello **-Отладка** параметра в вашей **PowerShell** командлета.</span><span class="sxs-lookup"><span data-stu-id="fa720-147">Or, if want toosee hello remaining requests for debugging, you can provide hello **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="fa720-148">Возвращающий множество значений, включая следующие значения ответа hello:</span><span class="sxs-lookup"><span data-stu-id="fa720-148">Which returns many values, including hello following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="fa720-149">В **Azure CLI**, значение заголовка hello получить с помощью hello параметром более подробных сведений.</span><span class="sxs-lookup"><span data-stu-id="fa720-149">In **Azure CLI**, you retrieve hello header value by using hello more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="fa720-150">Выдаются много значений, включая hello следующий объект:</span><span class="sxs-lookup"><span data-stu-id="fa720-150">Which returns many values, including hello following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="fa720-151">Ожидание перед отправкой следующего запроса</span><span class="sxs-lookup"><span data-stu-id="fa720-151">Waiting before sending next request</span></span>
<span data-ttu-id="fa720-152">Когда будет достигнут предел количества запросов hello, диспетчер ресурсов возвращает hello **429** код состояния HTTP и **Retry-After** значение в заголовке hello.</span><span class="sxs-lookup"><span data-stu-id="fa720-152">When you reach hello request limit, Resource Manager returns hello **429** HTTP status code and a **Retry-After** value in hello header.</span></span> <span data-ttu-id="fa720-153">Hello **Retry-After** значение указывает hello количество секунд ожидания приложения (или спящего режима) до отправки следующего запроса hello.</span><span class="sxs-lookup"><span data-stu-id="fa720-153">hello **Retry-After** value specifies hello number of seconds your application should wait (or sleep) before sending hello next request.</span></span> <span data-ttu-id="fa720-154">При отправке запроса до истечения значение повтора hello, запрос не обрабатывается и возвращается новое значение "Повторить".</span><span class="sxs-lookup"><span data-stu-id="fa720-154">If you send a request before hello retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa720-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa720-155">Next steps</span></span>

* <span data-ttu-id="fa720-156">Дополнительные сведения об ограничениях и квотах см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="fa720-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="fa720-157">toolearn об обработке асинхронных запросов REST, в разделе [отслеживания асинхронных операций Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="fa720-157">toolearn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
