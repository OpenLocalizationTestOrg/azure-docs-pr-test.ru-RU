---
title: "Сетка событий Azure: безопасность и проверка подлинности"
description: "В статье описываются сетка событий Azure и ее основные понятия."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: b6e1c7587c0b47d04862b4850741aaa3b7d191a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="0fcd6-103">Сетка событий: безопасность и проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="0fcd6-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="0fcd6-104">В сетке событий Azure предусмотрено три типа проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="0fcd6-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="0fcd6-105">Подписки на события</span><span class="sxs-lookup"><span data-stu-id="0fcd6-105">Event subscriptions</span></span>
* <span data-ttu-id="0fcd6-106">Публикация событий</span><span class="sxs-lookup"><span data-stu-id="0fcd6-106">Event publishing</span></span>
* <span data-ttu-id="0fcd6-107">Доставка событий веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="0fcd6-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="0fcd6-108">Доставка событий веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="0fcd6-108">WebHook Event delivery</span></span>

<span data-ttu-id="0fcd6-109">Веб-перехватчики — это один из многих способов получения событий в режиме реального времени из сетки событий Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-109">Webhooks are one of many ways to receive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="0fcd6-110">Каждый раз, когда имеется новое событие, готовое к доставке, сетка событий отправляет в веб-перехватчик HTTP-запрос, в теле которого находится событие.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-110">Every time there is a new event ready to be delivered, Event Grid sends an HTTP request with to your WebHook with the event in the body.</span></span>

<span data-ttu-id="0fcd6-111">При регистрации собственной конечной точки веб-перехватчика с сеткой событий он отправляет запрос POST с кодом простой проверки для подтверждения владения конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order to prove endpoint ownership.</span></span> <span data-ttu-id="0fcd6-112">В ответ приложение должно вернуть код проверки.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-112">Your app needs to respond by echoing back the validation code.</span></span> <span data-ttu-id="0fcd6-113">Сетка событий не доставляет события на конечные точки веб-перехватчика, которые не прошли проверку.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-113">Event Grid will not deliver events to WebHook endpoints that have not passed the validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="0fcd6-114">Сведения о проверке:</span><span class="sxs-lookup"><span data-stu-id="0fcd6-114">Validation details:</span></span>

* <span data-ttu-id="0fcd6-115">Во время создания или обновления подписки на событие сетка событий публикует на целевой конечной точке событие "SubscriptionValidationEvent".</span><span class="sxs-lookup"><span data-stu-id="0fcd6-115">At the time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event to the target endpoint.</span></span>
* <span data-ttu-id="0fcd6-116">В качестве заголовка событие содержит значение "Event-Type: Validation".</span><span class="sxs-lookup"><span data-stu-id="0fcd6-116">The event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="0fcd6-117">Текст события имеет ту же схему, что и другие события сетки событий.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-117">The event body has the same schema as other Event Grid events.</span></span>
* <span data-ttu-id="0fcd6-118">В данных события содержится свойство ValidationCode со строкой, сгенерированной случайным образом (например, ValidationCode: acb13…).</span><span class="sxs-lookup"><span data-stu-id="0fcd6-118">The event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="0fcd6-119">Чтобы подтвердить владение конечной точкой, возвращается код проверки (например, validation_response: acb13…).</span><span class="sxs-lookup"><span data-stu-id="0fcd6-119">In order to prove endpoint ownership, echo back the validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="0fcd6-120">Наконец, необходимо отметить, что сетка событий Azure поддерживает только конечные точки веб-перехватчиков HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-120">Finally, it is important to note that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="0fcd6-121">Подписка на события</span><span class="sxs-lookup"><span data-stu-id="0fcd6-121">Event subscription</span></span>

<span data-ttu-id="0fcd6-122">Чтобы подписаться на событие, необходимо иметь разрешение **Microsoft.EventGrid/EventSubscriptions/Write** для требуемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-122">To subscribe to an event, you must have the **Microsoft.EventGrid/EventSubscriptions/Write** permission on the required resource.</span></span> <span data-ttu-id="0fcd6-123">Это разрешение необходимо, так как вы записываете новую подписку в области действия ресурса.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-123">You need this permission because you are writing a new subscription at the scope of the resource.</span></span> <span data-ttu-id="0fcd6-124">Требуемый ресурс зависит от того, оформляется ли подписка на системный или пользовательский раздел.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-124">The required resource differs based on whether you are subscribing to a system topic or custom topic.</span></span> <span data-ttu-id="0fcd6-125">В этом разделе описываются оба типа подписки.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="0fcd6-126">Системные разделы (издатели служб Azure)</span><span class="sxs-lookup"><span data-stu-id="0fcd6-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="0fcd6-127">Для системных разделов необходимо разрешение на запись новой подписки на события в области действия ресурса, публикующего событие.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-127">For system topics, you need permission to write a new event subscription at the scope of the resource publishing the event.</span></span> <span data-ttu-id="0fcd6-128">Ресурс имеет следующий формат: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="0fcd6-128">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="0fcd6-129">Например, чтобы подписаться на событие в учетной записи хранения с именем **myacct**, требуется разрешение Microsoft.EventGrid/EventSubscriptions/Write для следующего ресурса: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="0fcd6-129">For example, to subscribe to an event on a storage account named **myacct**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="0fcd6-130">Пользовательские разделы</span><span class="sxs-lookup"><span data-stu-id="0fcd6-130">Custom topics</span></span>

<span data-ttu-id="0fcd6-131">Для пользовательских разделов необходимо разрешение на запись новой подписки на события в области действия сетки событий.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-131">For custom topics, you need permission to write a new event subscription at the scope of the Event Grid topic.</span></span> <span data-ttu-id="0fcd6-132">Ресурс имеет следующий формат: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="0fcd6-132">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="0fcd6-133">Например, чтобы подписаться на пользовательский раздел с именем **mytopic**, требуется разрешение Microsoft.EventGrid/EventSubscriptions/Write для следующего ресурса: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="0fcd6-133">For example, to subscribe to a custom topic named **mytopic**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="0fcd6-134">Публикация разделов</span><span class="sxs-lookup"><span data-stu-id="0fcd6-134">Topic publishing</span></span>

<span data-ttu-id="0fcd6-135">Для разделов используется либо подписанный URL-адрес (SAS), либо проверка подлинности с использованием ключа.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="0fcd6-136">Рекомендуется использовать SAS, но проверка подлинности с использованием ключа обеспечивает простое программирование, а также совместима со множеством существующих издателей веб-перехватчиков.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="0fcd6-137">Значение проверки подлинности следует включить в заголовок HTTP.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-137">You include the authentication value in the HTTP header.</span></span> <span data-ttu-id="0fcd6-138">Для SAS в качестве значения заголовка используйте **aeg-sas-token**.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-138">For SAS, use **aeg-sas-token** for the header value.</span></span> <span data-ttu-id="0fcd6-139">Для подлинности с использованием ключа в качестве значения заголовка следует использовать **aeg-sas-key**.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-139">For key authentication, use **aeg-sas-key** for the header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="0fcd6-140">Проверка подлинности с использованием ключа</span><span class="sxs-lookup"><span data-stu-id="0fcd6-140">Key authentication</span></span>

<span data-ttu-id="0fcd6-141">Проверка подлинности с использованием ключа — самая простая форма проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-141">Key authentication is the simplest form of authentication.</span></span> <span data-ttu-id="0fcd6-142">Используйте следующий формат: `aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="0fcd6-142">Use the format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="0fcd6-143">Например, для передачи ключа можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0fcd6-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="0fcd6-144">Маркеры SAS</span><span class="sxs-lookup"><span data-stu-id="0fcd6-144">SAS tokens</span></span>

<span data-ttu-id="0fcd6-145">Маркеры SAS для сетки события включают ресурс, срок его действия и подпись.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-145">SAS tokens for Event Grid include the resource, an expiration time, and a signature.</span></span> <span data-ttu-id="0fcd6-146">Маркер SAS имеет следующий формат: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-146">The format of the SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="0fcd6-147">Ресурс — это путь для раздела, в который вы отправляете события.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-147">The resource is the path for the topic to which you are sending events.</span></span> <span data-ttu-id="0fcd6-148">Вот пример допустимого пути к ресурсу: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="0fcd6-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="0fcd6-149">Вы создаете подпись на основе ключа.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-149">You generate the signature from a key.</span></span>

<span data-ttu-id="0fcd6-150">Например, допустимое значение **aeg-sas-token** выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0fcd6-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="0fcd6-151">В следующем примере создается маркер SAS для использования с сеткой событий:</span><span class="sxs-lookup"><span data-stu-id="0fcd6-151">The following example creates a SAS token for use with Event Grid:</span></span>

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a><span data-ttu-id="0fcd6-152">Контроль доступа к управлению</span><span class="sxs-lookup"><span data-stu-id="0fcd6-152">Management Access Control</span></span>

<span data-ttu-id="0fcd6-153">Сетка событий Azure позволяет контролировать уровень доступа, предоставленного разным пользователям для выполнения различных операций управления, таких как создание списка подписок на события, создание новых подписок и генерирование ключей.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-153">Azure Event Grid allows you to control the level of access given to different users to do various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="0fcd6-154">Для этих целей сетка событий использует проверку доступа на основе ролей Azure (RBAC).</span><span class="sxs-lookup"><span data-stu-id="0fcd6-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="0fcd6-155">Типы операций</span><span class="sxs-lookup"><span data-stu-id="0fcd6-155">Operation types</span></span>

<span data-ttu-id="0fcd6-156">Сетка событий Azure поддерживает следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0fcd6-156">Azure event grid supports the following actions:</span></span>

* <span data-ttu-id="0fcd6-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="0fcd6-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="0fcd6-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="0fcd6-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="0fcd6-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="0fcd6-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="0fcd6-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="0fcd6-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="0fcd6-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="0fcd6-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="0fcd6-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="0fcd6-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="0fcd6-163">Последние три операции возвращают потенциально секретную информацию, которая отфильтровывается из обычных операций чтения.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-163">The last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="0fcd6-164">Это наилучший способ ограничить доступ к этим операциям.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-164">It is best practice for you to restrict access to these operations.</span></span> <span data-ttu-id="0fcd6-165">Настраиваемые роли можно создавать с помощью [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [интерфейса командной строки (CLI) Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md) и интерфейса [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="0fcd6-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and the [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="0fcd6-166">Применение проверки доступа на основе ролей (RBAC)</span><span class="sxs-lookup"><span data-stu-id="0fcd6-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="0fcd6-167">Чтобы принудительно применить RBAC для разных пользователей, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0fcd6-167">Use the following steps to enforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="0fcd6-168">Создание файла определения пользовательской роли (.json)</span><span class="sxs-lookup"><span data-stu-id="0fcd6-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="0fcd6-169">Вот пример определений роли сетки событий, которые позволяют пользователям выполнять разные действия.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-169">The following are sample Event Grid role definitions which allow users to perform different sets of actions.</span></span>

<span data-ttu-id="0fcd6-170">**EventGridReadOnlyRole.json**: разрешено только чтение.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

<span data-ttu-id="0fcd6-171">**EventGridNoDeleteListKeysRole.json**: разрешен ограниченный набор действий по публикации и запрещены действия удаления.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
<span data-ttu-id="0fcd6-172">**EventGridContributorRole.json**: разрешено выполнять все действия сетки событий.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-to-azure-cli"></a><span data-ttu-id="0fcd6-173">Установка интерфейса командной строки Azure и вход в него</span><span class="sxs-lookup"><span data-stu-id="0fcd6-173">Install and login to Azure CLI</span></span>

* <span data-ttu-id="0fcd6-174">Интерфейс командной строки Azure версии 0.8.8 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="0fcd6-175">Чтобы установить последнюю версию и связать ее со своей подпиской Azure, см. статью [Установка Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0fcd6-175">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="0fcd6-176">Azure Resource Manager в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0fcd6-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="0fcd6-177">Дополнительные сведения см. в статье [Управление ресурсами и группами ресурсов Azure с помощью интерфейса командной строки Azure](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0fcd6-177">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="0fcd6-178">Создание настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="0fcd6-178">Create a custom role</span></span>

<span data-ttu-id="0fcd6-179">Чтобы создать настраиваемую роль, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0fcd6-179">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-the-role-to-a-user"></a><span data-ttu-id="0fcd6-180">Назначение роли пользователю</span><span class="sxs-lookup"><span data-stu-id="0fcd6-180">Assign the role to a user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="0fcd6-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0fcd6-181">Next steps</span></span>

* <span data-ttu-id="0fcd6-182">Общие сведения о сетке событий см. в статье [Сведения о сетке событий](overview.md)</span><span class="sxs-lookup"><span data-stu-id="0fcd6-182">For an introduction to Event Grid, see [About Event Grid](overview.md)</span></span>
