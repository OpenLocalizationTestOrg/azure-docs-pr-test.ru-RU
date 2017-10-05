---
title: "Ограничения запросов Azure Resource Manager | Документация Майкрософт"
description: "В данной статье описывается использование регулирования запросов Azure Resource Manager при достижении ограничений подписки."
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
ms.openlocfilehash: 6d7eeaf460674c3ab98425a5412ffa465b9ffd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="0db7a-103">Регулирование запросов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0db7a-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="0db7a-104">Для каждой подписки и клиента Resource Manager ограничивает число запросов на чтение до 15 000 и запросов на запись — до 1200 в час.</span><span class="sxs-lookup"><span data-stu-id="0db7a-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="0db7a-105">Эти ограничения применяются к каждому экземпляру Azure Resource Manager. В каждом регионе Azure существует несколько экземпляров, а Azure Resource Manager развертывается во всех регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="0db7a-105">These limits apply to each Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed to all Azure regions.</span></span>  <span data-ttu-id="0db7a-106">На практике ограничений гораздо больше, чем указано выше, так как запросы пользователя обычно обслуживаются многими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="0db7a-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="0db7a-107">Если приложение или сценарий достигает этих предельных значений, то требуется регулировать запросы.</span><span class="sxs-lookup"><span data-stu-id="0db7a-107">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="0db7a-108">В этом разделе показано, как определить, сколько осталось запросов до достижения ограничения, и как реагировать на достижение этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="0db7a-108">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="0db7a-109">По достижении ограничения отображается код состояния HTTP **429 — слишком много запросов**.</span><span class="sxs-lookup"><span data-stu-id="0db7a-109">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="0db7a-110">Число запросов ограничивается либо подпиской, либо клиентом.</span><span class="sxs-lookup"><span data-stu-id="0db7a-110">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="0db7a-111">Если в вашей подписке имеется несколько приложений, одновременно выполняющих запросы, то количество этих запросов суммируется, после чего определяется количество оставшихся запросов.</span><span class="sxs-lookup"><span data-stu-id="0db7a-111">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="0db7a-112">Запросы, ограничиваемые подпиской, это запросы, включающие в себя передачу идентификатора подписки (например, извлечение ресурсов в подписке).</span><span class="sxs-lookup"><span data-stu-id="0db7a-112">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="0db7a-113">Запросы, ограничиваемые клиентом, не включают в себя идентификатор подписки (например, извлечение действительных расположений Azure).</span><span class="sxs-lookup"><span data-stu-id="0db7a-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="0db7a-114">Количество оставшихся запросов</span><span class="sxs-lookup"><span data-stu-id="0db7a-114">Remaining requests</span></span>
<span data-ttu-id="0db7a-115">Количество оставшихся запросов можно определить, проверяя заголовки ответов.</span><span class="sxs-lookup"><span data-stu-id="0db7a-115">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="0db7a-116">Каждый запрос содержит значения количества оставшихся запросов на чтение и запись.</span><span class="sxs-lookup"><span data-stu-id="0db7a-116">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="0db7a-117">В приведенной ниже таблице описаны заголовки ответов, в которых можно проверить эти значения.</span><span class="sxs-lookup"><span data-stu-id="0db7a-117">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="0db7a-118">Заголовок ответа</span><span class="sxs-lookup"><span data-stu-id="0db7a-118">Response header</span></span> | <span data-ttu-id="0db7a-119">Описание</span><span class="sxs-lookup"><span data-stu-id="0db7a-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0db7a-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="0db7a-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="0db7a-121">Оставшееся количество запросов на чтение для подписки.</span><span class="sxs-lookup"><span data-stu-id="0db7a-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="0db7a-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="0db7a-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="0db7a-123">Оставшееся количество запросов на запись для подписки.</span><span class="sxs-lookup"><span data-stu-id="0db7a-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="0db7a-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="0db7a-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="0db7a-125">Оставшееся количество запросов на чтение для клиента.</span><span class="sxs-lookup"><span data-stu-id="0db7a-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="0db7a-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="0db7a-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="0db7a-127">Оставшееся количество запросов на запись для клиента.</span><span class="sxs-lookup"><span data-stu-id="0db7a-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="0db7a-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="0db7a-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="0db7a-129">Оставшееся количество запросов для типа ресурса для подписки.</span><span class="sxs-lookup"><span data-stu-id="0db7a-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="0db7a-130">Это значение заголовка возвращается только в том случае, если служба переопределила ограничение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0db7a-130">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="0db7a-131">Resource Manager добавляет это значение вместо ограничения подписки на запросы на чтение или запись.</span><span class="sxs-lookup"><span data-stu-id="0db7a-131">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="0db7a-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="0db7a-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="0db7a-133">Оставшееся количество запросов коллекции типов ресурсов для подписки.</span><span class="sxs-lookup"><span data-stu-id="0db7a-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="0db7a-134">Это значение заголовка возвращается только в том случае, если служба переопределила ограничение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0db7a-134">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="0db7a-135">Это значение содержит число оставшихся запросов коллекции (вывод ресурсов).</span><span class="sxs-lookup"><span data-stu-id="0db7a-135">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="0db7a-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="0db7a-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="0db7a-137">Оставшееся количество запросов для типа ресурса для клиента.</span><span class="sxs-lookup"><span data-stu-id="0db7a-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="0db7a-138">Этот заголовок добавляется только для запросов уровня клиента и только в том случае, если служба переопределила ограничение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0db7a-138">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="0db7a-139">Resource Manager добавляет это значение вместо ограничения клиента на запросы на чтение или запись.</span><span class="sxs-lookup"><span data-stu-id="0db7a-139">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="0db7a-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="0db7a-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="0db7a-141">Оставшееся количество запросов коллекции типов ресурсов для клиента.</span><span class="sxs-lookup"><span data-stu-id="0db7a-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="0db7a-142">Этот заголовок добавляется только для запросов уровня клиента и только в том случае, если служба переопределила ограничение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0db7a-142">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="0db7a-143">Получение значений заголовков</span><span class="sxs-lookup"><span data-stu-id="0db7a-143">Retrieving the header values</span></span>
<span data-ttu-id="0db7a-144">Получение этих значений заголовков в коде или сценарии ничем не отличается от извлечения любого другого значения заголовка.</span><span class="sxs-lookup"><span data-stu-id="0db7a-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="0db7a-145">Например, приведенный ниже код **C#** извлекает значение заголовка из объекта **HttpWebResponse** с именем **response**.</span><span class="sxs-lookup"><span data-stu-id="0db7a-145">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="0db7a-146">В **PowerShell** извлечь значение заголовка можно с помощью операции Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="0db7a-146">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="0db7a-147">Или, если требуется узнать количество оставшихся запросов для отладки, можно указать параметр **-Debug** в командлете **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0db7a-147">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="0db7a-148">Он возвращает массу значений, включая следующее значение ответа.</span><span class="sxs-lookup"><span data-stu-id="0db7a-148">Which returns many values, including the following response value:</span></span>

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

<span data-ttu-id="0db7a-149">В **интерфейсе командной строки Azure** извлечь значение заголовка можно с помощью параметра подробного вывода.</span><span class="sxs-lookup"><span data-stu-id="0db7a-149">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="0db7a-150">Он возвращает массу значений, включая следующий объект.</span><span class="sxs-lookup"><span data-stu-id="0db7a-150">Which returns many values, including the following object:</span></span>

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

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="0db7a-151">Ожидание перед отправкой следующего запроса</span><span class="sxs-lookup"><span data-stu-id="0db7a-151">Waiting before sending next request</span></span>
<span data-ttu-id="0db7a-152">По достижении предельного количества запросов Resource Manager возвращает в заголовке код состояния HTTP **429** и значение **Retry-After**.</span><span class="sxs-lookup"><span data-stu-id="0db7a-152">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="0db7a-153">Значение **Retry-After** указывает период времени в секундах, в течение которого приложение ожидает (или находится в спящем режиме), прежде чем отправить следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="0db7a-153">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="0db7a-154">Если отправить запрос до истечения значения Retry-After, этот запрос не будет обработан, и будет возвращено новое значение Retry-After.</span><span class="sxs-lookup"><span data-stu-id="0db7a-154">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0db7a-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0db7a-155">Next steps</span></span>

* <span data-ttu-id="0db7a-156">Дополнительные сведения об ограничениях и квотах см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="0db7a-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="0db7a-157">Сведения об обработке асинхронных запросов REST см. в статье [Track asynchronous Azure operations](resource-manager-async-operations.md) (Отслеживание асинхронных операций Azure).</span><span class="sxs-lookup"><span data-stu-id="0db7a-157">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
