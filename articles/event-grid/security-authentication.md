---
title: "aaaAzure сетки событий безопасности и проверки подлинности"
description: "В статье описываются служба \"Сетка событий Azure\" и ее основные понятия."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="70b94-103">Сетка событий: безопасность и проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="70b94-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="70b94-104">В сетке событий Azure предусмотрено три типа проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="70b94-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="70b94-105">Подписки на события</span><span class="sxs-lookup"><span data-stu-id="70b94-105">Event subscriptions</span></span>
* <span data-ttu-id="70b94-106">Публикация событий</span><span class="sxs-lookup"><span data-stu-id="70b94-106">Event publishing</span></span>
* <span data-ttu-id="70b94-107">Доставка событий веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="70b94-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="70b94-108">Доставка событий веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="70b94-108">WebHook Event delivery</span></span>

<span data-ttu-id="70b94-109">Веб-перехватчиков являются одним из многих событий tooreceive способами, в режиме реального времени из сетки событий Azure.</span><span class="sxs-lookup"><span data-stu-id="70b94-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="70b94-110">Каждый раз, имеется новое событие готовности toobe доставки, сетка события отправляет запрос HTTP с tooyour веб-перехватчик с событием hello в тексте hello.</span><span class="sxs-lookup"><span data-stu-id="70b94-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="70b94-111">При регистрации конечной точки веб-перехватчик с сеткой событий, она отправляет запрос POST с кодом простую проверку права собственности конечной точки tooprove заказа.</span><span class="sxs-lookup"><span data-stu-id="70b94-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="70b94-112">Приложение должно toorespond, возвращая код проверки назад hello.</span><span class="sxs-lookup"><span data-stu-id="70b94-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="70b94-113">Событие сетки не доставляет события tooWebHook конечных точек, которые не прошли проверку hello.</span><span class="sxs-lookup"><span data-stu-id="70b94-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="70b94-114">Сведения о проверке:</span><span class="sxs-lookup"><span data-stu-id="70b94-114">Validation details:</span></span>

* <span data-ttu-id="70b94-115">Во время hello подписки события создания или обновления сетки событий сообщений конечной точки целевого toohello события «SubscriptionValidationEvent».</span><span class="sxs-lookup"><span data-stu-id="70b94-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="70b94-116">Hello событие содержит заголовок значение «Тип события: проверка».</span><span class="sxs-lookup"><span data-stu-id="70b94-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="70b94-117">текст Hello событий имеет hello одной схеме с другими событиями сетки событий.</span><span class="sxs-lookup"><span data-stu-id="70b94-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="70b94-118">данные события Hello включают свойство «ValidationCode» со строкой случайным, например ValidationCode: acb13…).</span><span class="sxs-lookup"><span data-stu-id="70b94-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="70b94-119">В владение конечной точки tooprove заказа, echo пример кода проверки назад hello» ValidationResponse: acb13...».</span><span class="sxs-lookup"><span data-stu-id="70b94-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="70b94-120">Наконец это важно toonote сетки событий Azure поддерживает только конечные точки веб-перехватчика HTTPS.</span><span class="sxs-lookup"><span data-stu-id="70b94-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="70b94-121">Подписка на события</span><span class="sxs-lookup"><span data-stu-id="70b94-121">Event subscription</span></span>

<span data-ttu-id="70b94-122">событие tooan toosubscribe, должно иметь hello **Microsoft.EventGrid/EventSubscriptions/Write** ресурсов требуется разрешение на hello.</span><span class="sxs-lookup"><span data-stu-id="70b94-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="70b94-123">Это разрешение требуется использовать, поскольку при написании новую подписку можно в области hello hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="70b94-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="70b94-124">Hello требуемый ресурс зависит от подписка раздела системы tooa или пользовательский раздел.</span><span class="sxs-lookup"><span data-stu-id="70b94-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="70b94-125">В этом разделе описываются оба типа подписки.</span><span class="sxs-lookup"><span data-stu-id="70b94-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="70b94-126">Системные разделы (издатели служб Azure)</span><span class="sxs-lookup"><span data-stu-id="70b94-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="70b94-127">Разделы, системы необходимо разрешение toowrite новой подписки на события в области видимости hello публикации события hello hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="70b94-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="70b94-128">Hello ресурса hello выглядит следующим образом:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="70b94-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="70b94-129">Например, событие toosubscribe tooan на учетную запись хранения с именем **myacct**, требуется разрешение Microsoft.EventGrid/EventSubscriptions/Write hello на:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="70b94-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="70b94-130">Пользовательские разделы</span><span class="sxs-lookup"><span data-stu-id="70b94-130">Custom topics</span></span>

<span data-ttu-id="70b94-131">Настраиваемые разделы необходимо разрешение toowrite новой подписки на события в области видимости hello hello сетки события раздела.</span><span class="sxs-lookup"><span data-stu-id="70b94-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="70b94-132">Hello ресурса hello выглядит следующим образом:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="70b94-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="70b94-133">Например, toosubscribe tooa пользовательский раздел с именем **mytopic**, требуется разрешение Microsoft.EventGrid/EventSubscriptions/Write hello на:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="70b94-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="70b94-134">Публикация разделов</span><span class="sxs-lookup"><span data-stu-id="70b94-134">Topic publishing</span></span>

<span data-ttu-id="70b94-135">Для разделов используется либо подписанный URL-адрес (SAS), либо проверка подлинности с использованием ключа.</span><span class="sxs-lookup"><span data-stu-id="70b94-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="70b94-136">Рекомендуется использовать SAS, но проверка подлинности с использованием ключа обеспечивает простое программирование, а также совместима со множеством существующих издателей веб-перехватчиков.</span><span class="sxs-lookup"><span data-stu-id="70b94-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="70b94-137">Значение проверки подлинности hello включаются в заголовок HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="70b94-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="70b94-138">SAS, используйте **aeg маркер sas** для hello значение заголовка.</span><span class="sxs-lookup"><span data-stu-id="70b94-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="70b94-139">Для проверки подлинности с ключом, используйте **aeg ключ sas** для hello значение заголовка.</span><span class="sxs-lookup"><span data-stu-id="70b94-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="70b94-140">Проверка подлинности с использованием ключа</span><span class="sxs-lookup"><span data-stu-id="70b94-140">Key authentication</span></span>

<span data-ttu-id="70b94-141">Проверка подлинности с ключом является hello простая форма проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="70b94-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="70b94-142">Используйте формат hello:`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="70b94-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="70b94-143">Например, для передачи ключа можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="70b94-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="70b94-144">Маркеры SAS</span><span class="sxs-lookup"><span data-stu-id="70b94-144">SAS tokens</span></span>

<span data-ttu-id="70b94-145">Маркеры SAS для сетки события включают ресурсов hello, срок его действия и подписи.</span><span class="sxs-lookup"><span data-stu-id="70b94-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="70b94-146">Hello маркер SAS hello имеет формат: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="70b94-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="70b94-147">Hello ресурсов — hello путь для hello разделе toowhich можно отправлять события.</span><span class="sxs-lookup"><span data-stu-id="70b94-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="70b94-148">Вот пример допустимого пути к ресурсу: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="70b94-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="70b94-149">Вы создаете ключ подписи hello.</span><span class="sxs-lookup"><span data-stu-id="70b94-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="70b94-150">Например, допустимое значение **aeg-sas-token** выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="70b94-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="70b94-151">Следующий пример Hello создает маркер SAS для использования с сеткой событий:</span><span class="sxs-lookup"><span data-stu-id="70b94-151">hello following example creates a SAS token for use with Event Grid:</span></span>

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

## <a name="management-access-control"></a><span data-ttu-id="70b94-152">Контроль доступа к управлению</span><span class="sxs-lookup"><span data-stu-id="70b94-152">Management Access Control</span></span>

<span data-ttu-id="70b94-153">Azure сетки событий позволяет вам toocontrol hello уровень доступа, предоставленный toodifferent пользователей toodo различные операции управления, такие как список подписки на события, создавать новые и формирования ключей.</span><span class="sxs-lookup"><span data-stu-id="70b94-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="70b94-154">Для этих целей сетка событий использует проверку доступа на основе ролей Azure (RBAC).</span><span class="sxs-lookup"><span data-stu-id="70b94-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="70b94-155">Типы операций</span><span class="sxs-lookup"><span data-stu-id="70b94-155">Operation types</span></span>

<span data-ttu-id="70b94-156">Сетка событий Azure поддерживает hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="70b94-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="70b94-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="70b94-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="70b94-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="70b94-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="70b94-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="70b94-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="70b94-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="70b94-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="70b94-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="70b94-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="70b94-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="70b94-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="70b94-163">Здравствуйте, последние три операции возврата потенциально секретные сведения которой возвращает отфильтрованы из обычных операций чтения.</span><span class="sxs-lookup"><span data-stu-id="70b94-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="70b94-164">Рекомендуется для вас операции toothese toorestrict доступа.</span><span class="sxs-lookup"><span data-stu-id="70b94-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="70b94-165">Можно создать настраиваемые роли с помощью [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure интерфейс командной строки (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)и hello [API-интерфейса REST](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="70b94-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="70b94-166">Применение проверки доступа на основе ролей (RBAC)</span><span class="sxs-lookup"><span data-stu-id="70b94-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="70b94-167">Используйте следующие шаги tooenforce RBAC для разных пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="70b94-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="70b94-168">Создание файла определения пользовательской роли (.json)</span><span class="sxs-lookup"><span data-stu-id="70b94-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="70b94-169">Здесь представлены Hello определения ролей сетки событий образца, дающие пользователям различные наборы tooperform действий.</span><span class="sxs-lookup"><span data-stu-id="70b94-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="70b94-170">**EventGridReadOnlyRole.json**: разрешено только чтение.</span><span class="sxs-lookup"><span data-stu-id="70b94-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
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

<span data-ttu-id="70b94-171">**EventGridNoDeleteListKeysRole.json**: разрешен ограниченный набор действий по публикации и запрещены действия удаления.</span><span class="sxs-lookup"><span data-stu-id="70b94-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
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
 
<span data-ttu-id="70b94-172">**EventGridContributorRole.json**: разрешено выполнять все действия сетки событий.</span><span class="sxs-lookup"><span data-stu-id="70b94-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
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

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="70b94-173">Установка и входа tooAzure CLI</span><span class="sxs-lookup"><span data-stu-id="70b94-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="70b94-174">Интерфейс командной строки Azure версии 0.8.8 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="70b94-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="70b94-175">последнюю версию tooinstall hello и связывание его с подпиской Azure. в разделе [Установка и настройка hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="70b94-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="70b94-176">Azure Resource Manager в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="70b94-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="70b94-177">Go слишком[использование hello Azure CLI с hello диспетчера ресурсов](../xplat-cli-azure-resource-manager.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="70b94-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="70b94-178">Создание настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="70b94-178">Create a custom role</span></span>

<span data-ttu-id="70b94-179">Используйте toocreate пользовательской роли:</span><span class="sxs-lookup"><span data-stu-id="70b94-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="70b94-180">Назначить пользователя tooa роли hello</span><span class="sxs-lookup"><span data-stu-id="70b94-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="70b94-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70b94-181">Next steps</span></span>

* <span data-ttu-id="70b94-182">Введение tooEvent сетки. в разделе [о сетки событий](overview.md)</span><span class="sxs-lookup"><span data-stu-id="70b94-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>
