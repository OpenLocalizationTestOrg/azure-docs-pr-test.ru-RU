---
title: "Обзор аутентификации концентраторов событий Azure и модели безопасности | Документация Майкрософт"
description: "Обзор проверки подлинности концентраторов событий и модели безопасности."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 5abdbf70d4fdb2c7feb0f3537ecc0f2abf0775a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="1f2bb-103">Обзор проверки подлинности концентраторов событий и модели безопасности</span><span class="sxs-lookup"><span data-stu-id="1f2bb-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="1f2bb-104">Модель безопасности концентраторов событий Azure соответствует следующим требованиям.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="1f2bb-105">Только клиенты, предоставляющие действительные учетные данные, могут передать данные в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="1f2bb-106">Клиент не может действовать от имени другого клиента.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="1f2bb-107">Постороннему клиенту можно запретить отправку данных в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="1f2bb-108">Аутентификация клиента</span><span class="sxs-lookup"><span data-stu-id="1f2bb-108">Client authentication</span></span>
<span data-ttu-id="1f2bb-109">В основе модели безопасности концентраторов событий лежит сочетание [издателей событий](../service-bus-messaging/service-bus-sas.md) и маркеров *подписанных URL-адресов (SAS)*.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="1f2bb-110">Издатель событий определяет виртуальную конечную точку для концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="1f2bb-111">Издатель можно использовать только для отправки сообщений в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="1f2bb-112">Получать сообщения от издателя невозможно.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="1f2bb-113">Как правило, концентратор событий использует один издатель на клиент.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="1f2bb-114">Все сообщения, отправленные любому из издателей концентратора событий, добавляются в очередь этого концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="1f2bb-115">Издатели обеспечивают точный контроль доступа и регулирование.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="1f2bb-116">Каждому клиенту концентраторов событий назначается уникальный маркер, который передается в клиент.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="1f2bb-117">Маркеры созданы таким образом, что каждый уникальный маркер предоставляет доступ к одному уникальному издателю.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="1f2bb-118">Клиент, обладающий маркером, может отправлять данные только в один издатель, но не в другие издатели.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="1f2bb-119">Если несколько клиентов совместно используют один маркер, они также совместно используют издатель.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="1f2bb-120">Хотя это и не рекомендуется, можно предоставить устройствам маркеры, которые обеспечивают прямой доступ к концентратору событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="1f2bb-121">Любое устройство с этим маркером может отправлять сообщения непосредственно в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="1f2bb-122">Такие устройства не подвергаются регулированию.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="1f2bb-123">Кроме того, устройство нельзя внести в черный список, чтобы запретить отправку данных в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="1f2bb-124">Все маркеры подписаны с помощью ключа SAS.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="1f2bb-125">Как правило, все маркеры должны быть подписаны тем же ключом.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="1f2bb-126">Клиенты не имеют сведений о ключе. Это не позволяет другим клиентам создавать маркеры.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="1f2bb-127">Создание ключа SAS</span><span class="sxs-lookup"><span data-stu-id="1f2bb-127">Create the SAS key</span></span>

<span data-ttu-id="1f2bb-128">При создании пространства имен концентраторов событий служба создает 256-битный ключ SAS с именем **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-128">When creating an Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="1f2bb-129">Этот ключ дает пространству имен право на отправку, прослушивание и управление.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="1f2bb-130">Кроме того, можно создать дополнительные ключи.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-130">You can also create additional keys.</span></span> <span data-ttu-id="1f2bb-131">Рекомендуется создать ключ, дающий разрешения на отправку в конкретный концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="1f2bb-132">Далее в этом разделе предполагается, что вы дали ключу имя **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="1f2bb-133">В следующем примере при создании концентратора событий создается ключ только для отправки.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-133">The following example creates a send-only key when creating the event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="1f2bb-134">Создание маркеров</span><span class="sxs-lookup"><span data-stu-id="1f2bb-134">Generate tokens</span></span>

<span data-ttu-id="1f2bb-135">Маркеры можно создать с помощью ключа SAS.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="1f2bb-136">Следует создавать только один маркер на клиент.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-136">You must produce only one token per client.</span></span> <span data-ttu-id="1f2bb-137">Маркеры можно создать с помощью следующего метода.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="1f2bb-138">Все маркеры создаются с помощью ключа **EventHubSendKey** .</span><span class="sxs-lookup"><span data-stu-id="1f2bb-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="1f2bb-139">Каждому маркеру назначается уникальный URI.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="1f2bb-140">При вызове этого метода URI должен быть указан как `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="1f2bb-141">URI идентичен для всех маркеров за исключением класса `PUBLISHER_NAME`, который должен быть уникальным для каждого маркера.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="1f2bb-142">В идеальном случае `PUBLISHER_NAME` представляет идентификатор клиента, который получает маркер.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="1f2bb-143">Этот метод создает маркер со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="1f2bb-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="1f2bb-144">Срок действия маркера указывается в секундах от 1 января 1970 г.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="1f2bb-145">Ниже приведен пример маркера:</span><span class="sxs-lookup"><span data-stu-id="1f2bb-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="1f2bb-146">Как правило, срок существования маркера соответствует времени существования клиента или превышает его.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="1f2bb-147">Если клиент имеет возможность получить новый маркер, можно использовать маркеры с более коротким временем существования.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="1f2bb-148">Отправка данных</span><span class="sxs-lookup"><span data-stu-id="1f2bb-148">Sending data</span></span>
<span data-ttu-id="1f2bb-149">После создания маркеров каждому клиенту присваивается собственный уникальный маркер.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="1f2bb-150">Когда клиент отправляет данные в концентратор событий, к запросу на отправку прикрепляется специальный маркер.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-150">When the client sends data into an event hub, it tags its send request with the token.</span></span> <span data-ttu-id="1f2bb-151">Во избежание перехвата и кражи маркера злоумышленником связь между клиентом и концентратором событий должна выполняться по зашифрованному каналу.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="1f2bb-152">Добавление клиентов в черный список</span><span class="sxs-lookup"><span data-stu-id="1f2bb-152">Blacklisting clients</span></span>
<span data-ttu-id="1f2bb-153">Если маркер украден злоумышленником, злоумышленник может действовать от имени клиента, маркер которого был украден.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="1f2bb-154">Добавление клиента в черный список означает, что этот клиент не сможет работать, пока не получит новый маркер, использующий другой издатель.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="1f2bb-155">Проверка подлинности серверных приложений</span><span class="sxs-lookup"><span data-stu-id="1f2bb-155">Authentication of back-end applications</span></span>

<span data-ttu-id="1f2bb-156">Для аутентификации серверных приложений, которые используют данные, созданные клиентами концентраторов событий, концентраторы событий применяют модель безопасности, похожую на модель, используемую для разделов служебной шины.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="1f2bb-157">Группа потребителей концентраторов событий соответствует подписке на раздел служебной шины.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="1f2bb-158">Клиент может создать группу потребителей, если запрос на ее создание содержит маркер, который предоставляет права управления для концентратора событий или для пространства имен, которому принадлежит этот концентратор.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub, or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="1f2bb-159">Клиент может получать данные от группы потребителей, если запрос на получение сопровождается маркером, который предоставляет права на получение для этой группы потребителей, концентратора событий или пространства имен, которому принадлежит концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>

<span data-ttu-id="1f2bb-160">Текущая версия служебной шины не поддерживает правила SAS для отдельных подписок.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="1f2bb-161">Это же справедливо и для групп потребителей концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="1f2bb-162">В будущем планируется добавить поддержку SAS для обоих компонентов.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="1f2bb-163">В отсутствие проверки подлинности SAS для отдельных групп потребителей можно использовать ключи SAS для защиты всех групп потребителей общим ключом.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="1f2bb-164">Такой подход позволяет приложению получать данные от любых групп потребителей концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="1f2bb-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f2bb-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f2bb-165">Next steps</span></span>
<span data-ttu-id="1f2bb-166">Чтобы узнать больше о концентраторах событий, посетите следующие разделы:</span><span class="sxs-lookup"><span data-stu-id="1f2bb-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="1f2bb-167">[Обзор концентраторов событий]</span><span class="sxs-lookup"><span data-stu-id="1f2bb-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="1f2bb-168">[Обзор подписанных URL-адресов]</span><span class="sxs-lookup"><span data-stu-id="1f2bb-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="1f2bb-169">[Примеры приложений, использующих концентраторы событий]</span><span class="sxs-lookup"><span data-stu-id="1f2bb-169">[Sample applications that use Event Hubs]</span></span>

<span data-ttu-id="1f2bb-170">[Обзор концентраторов событий]: event-hubs-what-is-event-hubs.md</span><span class="sxs-lookup"><span data-stu-id="1f2bb-170">[Event Hubs overview]: event-hubs-what-is-event-hubs.md</span></span>
<span data-ttu-id="1f2bb-171">[Примеры приложений, использующих концентраторы событий]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="1f2bb-171">[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span></span>
<span data-ttu-id="1f2bb-172">[Обзор подписанных URL-адресов]: ../service-bus-messaging/service-bus-sas.md</span><span class="sxs-lookup"><span data-stu-id="1f2bb-172">[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md</span></span>

