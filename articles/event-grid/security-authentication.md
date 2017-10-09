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
# <a name="event-grid-security-and-authentication"></a>Сетка событий: безопасность и проверка подлинности 

В сетке событий Azure предусмотрено три типа проверки подлинности:

* Подписки на события
* Публикация событий
* Доставка событий веб-перехватчика

## <a name="webhook-event-delivery"></a>Доставка событий веб-перехватчика

Веб-перехватчиков являются одним из многих событий tooreceive способами, в режиме реального времени из сетки событий Azure.

Каждый раз, имеется новое событие готовности toobe доставки, сетка события отправляет запрос HTTP с tooyour веб-перехватчик с событием hello в тексте hello.

При регистрации конечной точки веб-перехватчик с сеткой событий, она отправляет запрос POST с кодом простую проверку права собственности конечной точки tooprove заказа. Приложение должно toorespond, возвращая код проверки назад hello. Событие сетки не доставляет события tooWebHook конечных точек, которые не прошли проверку hello.
 
### <a name="validation-details"></a>Сведения о проверке:

* Во время hello подписки события создания или обновления сетки событий сообщений конечной точки целевого toohello события «SubscriptionValidationEvent».
* Hello событие содержит заголовок значение «Тип события: проверка».
* текст Hello событий имеет hello одной схеме с другими событиями сетки событий.
* данные события Hello включают свойство «ValidationCode» со строкой случайным, например ValidationCode: acb13…).

В владение конечной точки tooprove заказа, echo пример кода проверки назад hello» ValidationResponse: acb13...».

Наконец это важно toonote сетки событий Azure поддерживает только конечные точки веб-перехватчика HTTPS.
## <a name="event-subscription"></a>Подписка на события

событие tooan toosubscribe, должно иметь hello **Microsoft.EventGrid/EventSubscriptions/Write** ресурсов требуется разрешение на hello. Это разрешение требуется использовать, поскольку при написании новую подписку можно в области hello hello ресурса. Hello требуемый ресурс зависит от подписка раздела системы tooa или пользовательский раздел. В этом разделе описываются оба типа подписки.

### <a name="system-topics-azure-service-publishers"></a>Системные разделы (издатели служб Azure)

Разделы, системы необходимо разрешение toowrite новой подписки на события в области видимости hello публикации события hello hello ресурсов. Hello ресурса hello выглядит следующим образом:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

Например, событие toosubscribe tooan на учетную запись хранения с именем **myacct**, требуется разрешение Microsoft.EventGrid/EventSubscriptions/Write hello на:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>Пользовательские разделы

Настраиваемые разделы необходимо разрешение toowrite новой подписки на события в области видимости hello hello сетки события раздела. Hello ресурса hello выглядит следующим образом:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

Например, toosubscribe tooa пользовательский раздел с именем **mytopic**, требуется разрешение Microsoft.EventGrid/EventSubscriptions/Write hello на:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>Публикация разделов

Для разделов используется либо подписанный URL-адрес (SAS), либо проверка подлинности с использованием ключа. Рекомендуется использовать SAS, но проверка подлинности с использованием ключа обеспечивает простое программирование, а также совместима со множеством существующих издателей веб-перехватчиков. 

Значение проверки подлинности hello включаются в заголовок HTTP hello. SAS, используйте **aeg маркер sas** для hello значение заголовка. Для проверки подлинности с ключом, используйте **aeg ключ sas** для hello значение заголовка.

### <a name="key-authentication"></a>Проверка подлинности с использованием ключа

Проверка подлинности с ключом является hello простая форма проверки подлинности. Используйте формат hello:`aeg-sas-key: <your key>`

Например, для передачи ключа можно использовать следующую команду: 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>Маркеры SAS

Маркеры SAS для сетки события включают ресурсов hello, срок его действия и подписи. Hello маркер SAS hello имеет формат: `r={resource}&e={expiration}&s={signature}`.

Hello ресурсов — hello путь для hello разделе toowhich можно отправлять события. Вот пример допустимого пути к ресурсу: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

Вы создаете ключ подписи hello.

Например, допустимое значение **aeg-sas-token** выглядит следующим образом:

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

Следующий пример Hello создает маркер SAS для использования с сеткой событий:

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

## <a name="management-access-control"></a>Контроль доступа к управлению

Azure сетки событий позволяет вам toocontrol hello уровень доступа, предоставленный toodifferent пользователей toodo различные операции управления, такие как список подписки на события, создавать новые и формирования ключей. Для этих целей сетка событий использует проверку доступа на основе ролей Azure (RBAC).

### <a name="operation-types"></a>Типы операций

Сетка событий Azure поддерживает hello, следующие действия:

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

Здравствуйте, последние три операции возврата потенциально секретные сведения которой возвращает отфильтрованы из обычных операций чтения. Рекомендуется для вас операции toothese toorestrict доступа. Можно создать настраиваемые роли с помощью [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure интерфейс командной строки (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)и hello [API-интерфейса REST](../active-directory/role-based-access-control-manage-access-rest.md).

### <a name="enforcing-role-based-access-check-rbac"></a>Применение проверки доступа на основе ролей (RBAC)

Используйте следующие шаги tooenforce RBAC для разных пользователей hello.

#### <a name="create-a-custom-role-definition-file-json"></a>Создание файла определения пользовательской роли (.json)

Здесь представлены Hello определения ролей сетки событий образца, дающие пользователям различные наборы tooperform действий.

**EventGridReadOnlyRole.json**: разрешено только чтение.
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

**EventGridNoDeleteListKeysRole.json**: разрешен ограниченный набор действий по публикации и запрещены действия удаления.
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
 
**EventGridContributorRole.json**: разрешено выполнять все действия сетки событий.  
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

#### <a name="install-and-login-tooazure-cli"></a>Установка и входа tooAzure CLI

* Интерфейс командной строки Azure версии 0.8.8 или более поздней. последнюю версию tooinstall hello и связывание его с подпиской Azure. в разделе [Установка и настройка hello Azure CLI](../cli-install-nodejs.md).
* Azure Resource Manager в Azure CLI. Go слишком[использование hello Azure CLI с hello диспетчера ресурсов](../xplat-cli-azure-resource-manager.md) для получения дополнительных сведений.

#### <a name="create-a-custom-role"></a>Создание настраиваемой роли

Используйте toocreate пользовательской роли:

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Назначить пользователя tooa роли hello


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>Дальнейшие действия

* Введение tooEvent сетки. в разделе [о сетки событий](overview.md)
