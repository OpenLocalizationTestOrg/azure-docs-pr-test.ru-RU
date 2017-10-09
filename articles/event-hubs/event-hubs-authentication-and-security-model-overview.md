---
title: "aaaOverview модели проверки подлинности и безопасности концентраторов событий Azure | Документы Microsoft"
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
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="f579b-103">Обзор проверки подлинности концентраторов событий и модели безопасности</span><span class="sxs-lookup"><span data-stu-id="f579b-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="f579b-104">модель безопасности концентраторов событий Azure Hello соответствует hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="f579b-104">hello Azure Event Hubs security model meets hello following requirements:</span></span>

* <span data-ttu-id="f579b-105">Только клиенты, предоставляющие допустимые учетные данные можно отправить концентратора событий tooan данных.</span><span class="sxs-lookup"><span data-stu-id="f579b-105">Only clients that present valid credentials can send data tooan event hub.</span></span>
* <span data-ttu-id="f579b-106">Клиент не может действовать от имени другого клиента.</span><span class="sxs-lookup"><span data-stu-id="f579b-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="f579b-107">Незаконный клиент можно запретить отправку данных концентратора событий tooan.</span><span class="sxs-lookup"><span data-stu-id="f579b-107">A rogue client can be blocked from sending data tooan event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="f579b-108">Аутентификация клиента</span><span class="sxs-lookup"><span data-stu-id="f579b-108">Client authentication</span></span>
<span data-ttu-id="f579b-109">модель безопасности концентраторов событий Hello основан на сочетание [подписи общего доступа (SAS)](../service-bus-messaging/service-bus-sas.md) маркеры и *издатели событий*.</span><span class="sxs-lookup"><span data-stu-id="f579b-109">hello Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="f579b-110">Издатель событий определяет виртуальную конечную точку для концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="f579b-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="f579b-111">концентратор событий tooan используется toosend сообщения можно только издателю Hello.</span><span class="sxs-lookup"><span data-stu-id="f579b-111">hello publisher can only be used toosend messages tooan event hub.</span></span> <span data-ttu-id="f579b-112">Это не tooreceive возможные сообщения от издателя.</span><span class="sxs-lookup"><span data-stu-id="f579b-112">It is not possible tooreceive messages from a publisher.</span></span>

<span data-ttu-id="f579b-113">Как правило, концентратор событий использует один издатель на клиент.</span><span class="sxs-lookup"><span data-stu-id="f579b-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="f579b-114">Все сообщения, отправляемые tooany hello издателей концентратора событий, ставятся в очередь в этот концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="f579b-114">All messages that are sent tooany of hello publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="f579b-115">Издатели обеспечивают точный контроль доступа и регулирование.</span><span class="sxs-lookup"><span data-stu-id="f579b-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="f579b-116">Каждый клиент концентраторов событий назначается уникальный токен, который является toohello отправленный клиентом.</span><span class="sxs-lookup"><span data-stu-id="f579b-116">Each Event Hubs client is assigned a unique token, which is uploaded toohello client.</span></span> <span data-ttu-id="f579b-117">Hello токены создаются таким образом, что каждый уникальный токен предоставляет доступ tooa отдельному уникальному издателю.</span><span class="sxs-lookup"><span data-stu-id="f579b-117">hello tokens are produced such that each unique token grants access tooa different unique publisher.</span></span> <span data-ttu-id="f579b-118">Клиент, обладающие токеном можно отправлять только tooone publisher, но не другие издателя.</span><span class="sxs-lookup"><span data-stu-id="f579b-118">A client that possesses a token can only send tooone publisher, but no other publisher.</span></span> <span data-ttu-id="f579b-119">Если несколько клиентов общей папки hello же токен, то каждое из них совместно используют издателя.</span><span class="sxs-lookup"><span data-stu-id="f579b-119">If multiple clients share hello same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="f579b-120">Несмотря на то, что не рекомендуется, это возможно tooequip устройства токенами, предоставляющими концентратора событий tooan прямой доступ.</span><span class="sxs-lookup"><span data-stu-id="f579b-120">Although not recommended, it is possible tooequip devices with tokens that grant direct access tooan event hub.</span></span> <span data-ttu-id="f579b-121">Любое устройство с этим маркером может отправлять сообщения непосредственно в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="f579b-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="f579b-122">Такое устройство не будет toothrottling субъекта.</span><span class="sxs-lookup"><span data-stu-id="f579b-122">Such a device will not be subject toothrottling.</span></span> <span data-ttu-id="f579b-123">Кроме того устройство hello нельзя заблокировать отправку сообщений toothat концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="f579b-123">Furthermore, hello device cannot be blacklisted from sending toothat event hub.</span></span>

<span data-ttu-id="f579b-124">Все маркеры подписаны с помощью ключа SAS.</span><span class="sxs-lookup"><span data-stu-id="f579b-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="f579b-125">Как правило, все токены подписываются с hello таким же ключом.</span><span class="sxs-lookup"><span data-stu-id="f579b-125">Typically, all tokens are signed with hello same key.</span></span> <span data-ttu-id="f579b-126">Клиенты не поддерживают hello ключом. Это предотвращает производство маркеров других клиентов.</span><span class="sxs-lookup"><span data-stu-id="f579b-126">Clients are not aware of hello key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-hello-sas-key"></a><span data-ttu-id="f579b-127">Создание ключа SAS hello</span><span class="sxs-lookup"><span data-stu-id="f579b-127">Create hello SAS key</span></span>

<span data-ttu-id="f579b-128">При создании имен концентраторов событий, служба hello создает 256-разрядный ключ SAS с именем **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="f579b-128">When creating an Event Hubs namespace, hello service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="f579b-129">Этот ключ предоставляет отправки, прослушивания и управления пространством имен toohello права.</span><span class="sxs-lookup"><span data-stu-id="f579b-129">This key grants send, listen, and manage rights toohello namespace.</span></span> <span data-ttu-id="f579b-130">Кроме того, можно создать дополнительные ключи.</span><span class="sxs-lookup"><span data-stu-id="f579b-130">You can also create additional keys.</span></span> <span data-ttu-id="f579b-131">Рекомендуется создать ключ, отправки, предоставление разрешения toohello конкретного события концентратора.</span><span class="sxs-lookup"><span data-stu-id="f579b-131">It is recommended that you produce a key that grants send permissions toohello specific event hub.</span></span> <span data-ttu-id="f579b-132">Hello оставшейся части этого раздела, предполагается имя этого ключа **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="f579b-132">For hello remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="f579b-133">Следующий пример Hello создается ключ только для отправки при создании концентратора событий hello:</span><span class="sxs-lookup"><span data-stu-id="f579b-133">hello following example creates a send-only key when creating hello event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="f579b-134">Создание маркеров</span><span class="sxs-lookup"><span data-stu-id="f579b-134">Generate tokens</span></span>

<span data-ttu-id="f579b-135">Вы можете создать маркеры с помощью ключа SAS hello.</span><span class="sxs-lookup"><span data-stu-id="f579b-135">You can generate tokens using hello SAS key.</span></span> <span data-ttu-id="f579b-136">Следует создавать только один маркер на клиент.</span><span class="sxs-lookup"><span data-stu-id="f579b-136">You must produce only one token per client.</span></span> <span data-ttu-id="f579b-137">Маркеры затем могут быть созданы с помощью hello следующий метод.</span><span class="sxs-lookup"><span data-stu-id="f579b-137">Tokens can then be produced using hello following method.</span></span> <span data-ttu-id="f579b-138">Все токены создаются с помощью hello **EventHubSendKey** ключа.</span><span class="sxs-lookup"><span data-stu-id="f579b-138">All tokens are generated using hello **EventHubSendKey** key.</span></span> <span data-ttu-id="f579b-139">Каждому маркеру назначается уникальный URI.</span><span class="sxs-lookup"><span data-stu-id="f579b-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="f579b-140">При вызове этого метода, hello URI должно быть указано как `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="f579b-140">When calling this method, hello URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="f579b-141">Для всех токенов hello URI идентичен, за исключением hello объекта `PUBLISHER_NAME`, который должен отличаться для каждого токена.</span><span class="sxs-lookup"><span data-stu-id="f579b-141">For all tokens, hello URI is identical, with hello exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="f579b-142">В идеальном случае `PUBLISHER_NAME` представляет hello идентификатор hello клиента, который получит этот токен.</span><span class="sxs-lookup"><span data-stu-id="f579b-142">Ideally, `PUBLISHER_NAME` represents hello ID of hello client that receives that token.</span></span>

<span data-ttu-id="f579b-143">Этот метод создает маркер с hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="f579b-143">This method generates a token with hello following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="f579b-144">Срок действия токена Hello указывается в секундах от 1 января 1970 г.</span><span class="sxs-lookup"><span data-stu-id="f579b-144">hello token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="f579b-145">Hello ниже приведен пример токена:</span><span class="sxs-lookup"><span data-stu-id="f579b-145">hello following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="f579b-146">Как правило hello токены имеют время существования, вида или превышает время существования hello hello клиента.</span><span class="sxs-lookup"><span data-stu-id="f579b-146">Typically, hello tokens have a lifespan that resembles or exceeds hello lifespan of hello client.</span></span> <span data-ttu-id="f579b-147">Если клиент hello имеет возможность tooobtain hello новый маркер, можно использовать токены с более коротким временем существования.</span><span class="sxs-lookup"><span data-stu-id="f579b-147">If hello client has hello capability tooobtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="f579b-148">Отправка данных</span><span class="sxs-lookup"><span data-stu-id="f579b-148">Sending data</span></span>
<span data-ttu-id="f579b-149">После создания токенов hello каждому клиенту предоставляется со своим собственным уникальным токеном.</span><span class="sxs-lookup"><span data-stu-id="f579b-149">Once hello tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="f579b-150">Когда клиент hello отправляет данные в концентратор событий, он теги отправки запроса с токеном hello.</span><span class="sxs-lookup"><span data-stu-id="f579b-150">When hello client sends data into an event hub, it tags its send request with hello token.</span></span> <span data-ttu-id="f579b-151">tooprevent злоумышленник перехвата и кражи токена hello, hello обмен данными между клиентом hello и hello концентратора событий должно выполняться по зашифрованному каналу.</span><span class="sxs-lookup"><span data-stu-id="f579b-151">tooprevent an attacker from eavesdropping and stealing hello token, hello communication between hello client and hello event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="f579b-152">Добавление клиентов в черный список</span><span class="sxs-lookup"><span data-stu-id="f579b-152">Blacklisting clients</span></span>
<span data-ttu-id="f579b-153">Если токен украден злоумышленником, hello злоумышленник может выполнить олицетворение клиента hello кражи, токен.</span><span class="sxs-lookup"><span data-stu-id="f579b-153">If a token is stolen by an attacker, hello attacker can impersonate hello client whose token has been stolen.</span></span> <span data-ttu-id="f579b-154">Добавление клиента в черный список означает, что этот клиент не сможет работать, пока не получит новый маркер, использующий другой издатель.</span><span class="sxs-lookup"><span data-stu-id="f579b-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="f579b-155">Проверка подлинности серверных приложений</span><span class="sxs-lookup"><span data-stu-id="f579b-155">Authentication of back-end applications</span></span>

<span data-ttu-id="f579b-156">tooauthenticate серверных приложений, использующих данные hello клиентов концентраторов событий, концентраторы событий использует модель безопасности, аналогичной модели toohello, используемый для разделов Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f579b-156">tooauthenticate back-end applications that consume hello data generated by Event Hubs clients, Event Hubs employs a security model that is similar toohello model that is used for Service Bus topics.</span></span> <span data-ttu-id="f579b-157">Группа потребителей концентраторов событий — раздел служебной шины tooa эквивалентные tooa подписки.</span><span class="sxs-lookup"><span data-stu-id="f579b-157">An Event Hubs consumer group is equivalent tooa subscription tooa Service Bus topic.</span></span> <span data-ttu-id="f579b-158">Клиент можно создать группу потребителей, если запрос toocreate hello hello-группа потребителей сопровождается токен, что предоставляет права для концентратора событий hello управления или для пространства имен toowhich hello принадлежит концентратор событий hello.</span><span class="sxs-lookup"><span data-stu-id="f579b-158">A client can create a consumer group if hello request toocreate hello consumer group is accompanied by a token that grants manage privileges for hello event hub, or for hello namespace toowhich hello event hub belongs.</span></span> <span data-ttu-id="f579b-159">Клиент разрешен tooconsume данных из группы потребителей Если hello запроса на получение сопровождается токен предоставляет получают прав для этой группы потребителей, hello концентратора событий или концентратор событий hello toowhich имен hello принадлежит.</span><span class="sxs-lookup"><span data-stu-id="f579b-159">A client is allowed tooconsume data from a consumer group if hello receive request is accompanied by a token that grants receive rights on that consumer group, hello event hub, or hello namespace toowhich hello event hub belongs.</span></span>

<span data-ttu-id="f579b-160">Текущая версия шины обслуживания Hello не поддерживает правила SAS для отдельных подписок.</span><span class="sxs-lookup"><span data-stu-id="f579b-160">hello current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="f579b-161">Здравствуйте, справедливо и для групп потребителей концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="f579b-161">hello same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="f579b-162">Поддержка SAS будет добавлена для обоих компонентов в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="f579b-162">SAS support will be added for both features in hello future.</span></span>

<span data-ttu-id="f579b-163">В отсутствие проверки подлинности SAS для отдельных групп потребителей hello можно использовать toosecure ключи SAS всех групп потребителей с общим ключом.</span><span class="sxs-lookup"><span data-stu-id="f579b-163">In hello absence of SAS authentication for individual consumer groups, you can use SAS keys toosecure all consumer groups with a common key.</span></span> <span data-ttu-id="f579b-164">Такой подход дает данных tooconsume приложения из любого hello групп потребителей концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="f579b-164">This approach enables an application tooconsume data from any of hello consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f579b-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f579b-165">Next steps</span></span>
<span data-ttu-id="f579b-166">toolearn Дополнительные сведения о концентраторах событий посетите hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="f579b-166">toolearn more about Event Hubs, visit hello following topics:</span></span>

* <span data-ttu-id="f579b-167">[Обзор концентраторов событий]</span><span class="sxs-lookup"><span data-stu-id="f579b-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="f579b-168">[Обзор подписанных URL-адресов]</span><span class="sxs-lookup"><span data-stu-id="f579b-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="f579b-169">[Примеры приложений, использующих концентраторы событий]</span><span class="sxs-lookup"><span data-stu-id="f579b-169">[Sample applications that use Event Hubs]</span></span>

[Обзор концентраторов событий]: event-hubs-what-is-event-hubs.md
[Примеры приложений, использующих концентраторы событий]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Обзор подписанных URL-адресов]: ../service-bus-messaging/service-bus-sas.md

