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
# <a name="event-hubs-authentication-and-security-model-overview"></a>Обзор проверки подлинности концентраторов событий и модели безопасности
модель безопасности концентраторов событий Azure Hello соответствует hello следующие требования:

* Только клиенты, предоставляющие допустимые учетные данные можно отправить концентратора событий tooan данных.
* Клиент не может действовать от имени другого клиента.
* Незаконный клиент можно запретить отправку данных концентратора событий tooan.

## <a name="client-authentication"></a>Аутентификация клиента
модель безопасности концентраторов событий Hello основан на сочетание [подписи общего доступа (SAS)](../service-bus-messaging/service-bus-sas.md) маркеры и *издатели событий*. Издатель событий определяет виртуальную конечную точку для концентратора событий. концентратор событий tooan используется toosend сообщения можно только издателю Hello. Это не tooreceive возможные сообщения от издателя.

Как правило, концентратор событий использует один издатель на клиент. Все сообщения, отправляемые tooany hello издателей концентратора событий, ставятся в очередь в этот концентратор событий. Издатели обеспечивают точный контроль доступа и регулирование.

Каждый клиент концентраторов событий назначается уникальный токен, который является toohello отправленный клиентом. Hello токены создаются таким образом, что каждый уникальный токен предоставляет доступ tooa отдельному уникальному издателю. Клиент, обладающие токеном можно отправлять только tooone publisher, но не другие издателя. Если несколько клиентов общей папки hello же токен, то каждое из них совместно используют издателя.

Несмотря на то, что не рекомендуется, это возможно tooequip устройства токенами, предоставляющими концентратора событий tooan прямой доступ. Любое устройство с этим маркером может отправлять сообщения непосредственно в концентратор событий. Такое устройство не будет toothrottling субъекта. Кроме того устройство hello нельзя заблокировать отправку сообщений toothat концентратора событий.

Все маркеры подписаны с помощью ключа SAS. Как правило, все токены подписываются с hello таким же ключом. Клиенты не поддерживают hello ключом. Это предотвращает производство маркеров других клиентов.

### <a name="create-hello-sas-key"></a>Создание ключа SAS hello

При создании имен концентраторов событий, служба hello создает 256-разрядный ключ SAS с именем **RootManageSharedAccessKey**. Этот ключ предоставляет отправки, прослушивания и управления пространством имен toohello права. Кроме того, можно создать дополнительные ключи. Рекомендуется создать ключ, отправки, предоставление разрешения toohello конкретного события концентратора. Hello оставшейся части этого раздела, предполагается имя этого ключа **EventHubSendKey**.

Следующий пример Hello создается ключ только для отправки при создании концентратора событий hello:

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

### <a name="generate-tokens"></a>Создание маркеров

Вы можете создать маркеры с помощью ключа SAS hello. Следует создавать только один маркер на клиент. Маркеры затем могут быть созданы с помощью hello следующий метод. Все токены создаются с помощью hello **EventHubSendKey** ключа. Каждому маркеру назначается уникальный URI.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

При вызове этого метода, hello URI должно быть указано как `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`. Для всех токенов hello URI идентичен, за исключением hello объекта `PUBLISHER_NAME`, который должен отличаться для каждого токена. В идеальном случае `PUBLISHER_NAME` представляет hello идентификатор hello клиента, который получит этот токен.

Этот метод создает маркер с hello следующие структуры:

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

Срок действия токена Hello указывается в секундах от 1 января 1970 г. Hello ниже приведен пример токена:

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

Как правило hello токены имеют время существования, вида или превышает время существования hello hello клиента. Если клиент hello имеет возможность tooobtain hello новый маркер, можно использовать токены с более коротким временем существования.

### <a name="sending-data"></a>Отправка данных
После создания токенов hello каждому клиенту предоставляется со своим собственным уникальным токеном.

Когда клиент hello отправляет данные в концентратор событий, он теги отправки запроса с токеном hello. tooprevent злоумышленник перехвата и кражи токена hello, hello обмен данными между клиентом hello и hello концентратора событий должно выполняться по зашифрованному каналу.

### <a name="blacklisting-clients"></a>Добавление клиентов в черный список
Если токен украден злоумышленником, hello злоумышленник может выполнить олицетворение клиента hello кражи, токен. Добавление клиента в черный список означает, что этот клиент не сможет работать, пока не получит новый маркер, использующий другой издатель.

## <a name="authentication-of-back-end-applications"></a>Проверка подлинности серверных приложений

tooauthenticate серверных приложений, использующих данные hello клиентов концентраторов событий, концентраторы событий использует модель безопасности, аналогичной модели toohello, используемый для разделов Service Bus. Группа потребителей концентраторов событий — раздел служебной шины tooa эквивалентные tooa подписки. Клиент можно создать группу потребителей, если запрос toocreate hello hello-группа потребителей сопровождается токен, что предоставляет права для концентратора событий hello управления или для пространства имен toowhich hello принадлежит концентратор событий hello. Клиент разрешен tooconsume данных из группы потребителей Если hello запроса на получение сопровождается токен предоставляет получают прав для этой группы потребителей, hello концентратора событий или концентратор событий hello toowhich имен hello принадлежит.

Текущая версия шины обслуживания Hello не поддерживает правила SAS для отдельных подписок. Здравствуйте, справедливо и для групп потребителей концентраторов событий. Поддержка SAS будет добавлена для обоих компонентов в будущем hello.

В отсутствие проверки подлинности SAS для отдельных групп потребителей hello можно использовать toosecure ключи SAS всех групп потребителей с общим ключом. Такой подход дает данных tooconsume приложения из любого hello групп потребителей концентратора событий.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о концентраторах событий посетите hello следующие вопросы:

* [Обзор концентраторов событий]
* [Обзор подписанных URL-адресов]
* [Примеры приложений, использующих концентраторы событий]

[Обзор концентраторов событий]: event-hubs-what-is-event-hubs.md
[Примеры приложений, использующих концентраторы событий]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Обзор подписанных URL-адресов]: ../service-bus-messaging/service-bus-sas.md

