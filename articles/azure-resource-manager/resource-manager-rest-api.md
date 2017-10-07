---
title: "интерфейсы API REST диспетчера aaaResource | Документы Microsoft"
description: "Обзор проверки подлинности API REST диспетчера ресурсов hello и примеры использования"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a>API-интерфейсы REST диспетчера ресурсов
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Интерфейс командной строки Azure](xplat-cli-azure-resource-manager.md)
> * [Портал](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

За каждый вызов tooAzure диспетчера ресурсов, за каждого развернутого шаблона за каждые настроенная учетная запись хранилища существует один или несколько вызовов toohello диспетчера ресурсов Azure в API RESTful. Этот раздел является выделяемых toothose API-интерфейсы и как их можно вызывать без использования во всех любых SDK. Этот подход полезен, если требуется полный контроль над tooAzure запросы или hello пакета SDK для предпочитаемого языка недоступна или не поддерживает операцию hello, что нужно.

В этой статье не проходят через каждый API, который предоставляется в Azure, но вместо этого использует некоторые операции в подключении toothem примеры. Поняв основы hello, можно прочитать hello [Справочник по API REST диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/resources/) toofind подробные сведения о как остальные hello toouse hello API-интерфейсы.

## <a name="authentication"></a>Аутентификация
Проверка подлинности для Resource Manager осуществляется с помощью Azure Active Directory (AD). tooconnect tooany API, необходимо сначала tooauthenticate с Azure AD tooreceive маркер проверки подлинности, который можно передать на tooevery запроса. Как здесь описывается вызов чисто напрямую toohello API-интерфейс REST, предполагается, что вы не хотите tooauthenticate по необходимости вводить имя пользователя и пароль. Кроме того, мы предполагаем, что двухфакторная проверка подлинности не используется. Таким образом мы создания приложения Azure AD и субъекта-службы, используемые toolog в. Но следует помнить, что Azure AD поддерживает несколько процедур проверки подлинности и все они могут быть используется tooretrieve этот маркер проверки подлинности, необходимую для последующих запросов API.
Пошаговые инструкции см. в статье [Создание приложения Active Directory и субъекта-службы с доступом к ресурсам с помощью портала](resource-group-create-service-principal-portal.md).

### <a name="generating-an-access-token"></a>Создание маркера доступа
Выполняя запрос tooAzure AD, расположенный в login.microsoftonline.com выполняется проверка подлинности в Azure AD. tooauthenticate, требуется hello toohave следующую информацию:

* Идентификатор клиента Azure AD (hello, Azure AD, вы используете toolog в имя, часто hello то же, что ваша компания, но не обязательно)
* Идентификатор приложения (предпринятые во время шага создания приложения hello Azure AD)
* Пароль (который был выбран при создании hello приложения Azure AD)

В hello, выполнив HTTP-запроса чтобы убедиться, что tooreplace «Azure AD клиента ID», «Идентификатор приложения» и «Пароль» с правильными значениями hello.

**Базовый HTTP-запрос:**

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

... будет (если проверка подлинности успешно пройдена) привести аналогичные toohello ответа, следующий ответ:

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
(access_token hello в предшествующих ответа hello было сокращенный tooincrease удобства чтения)

**Создание маркера доступа с помощью Bash:**

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

**Создание маркера доступа с помощью PowerShell:**

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

Hello ответ содержит токен доступа, сведения о как долго этот маркер является допустимым и сведения о какой ресурс можно использовать этот маркер для.
маркер доступа Hello, полученный в предыдущем вызове HTTP hello должны передаваться в для всех запросов toohello API диспетчера ресурсов. Передайте его в качестве значение заголовка «Авторизации» с именем hello значение «YOUR_ACCESS_TOKEN носителя». Обратите внимание, hello пробел между «Bearer» и маркер доступа.

Как видно из hello выше результат HTTP hello маркер действителен за определенный период времени, во время которого следует кэшировать и повторно использовать этот же токен. Даже если это возможно tooauthenticate от Azure AD для каждого вызова API будет крайне неэффективно.

## <a name="calling-resource-manager-rest-apis"></a>Вызов интерфейсов REST API в Resource Manager
В этом разделе использует только несколько интерфейсов API tooexplain hello базовое использование операций REST hello. Сведения обо всех операциях hello см. в разделе [API REST диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/resources/).

### <a name="list-all-subscriptions"></a>Вывод списка всех подписок
Одна из hello простой операции, которые можно сделать — доступные подписки hello toolist, которые можно открыть. Привет, следующий запрос вы видите, как маркер доступа hello передаются в качестве заголовка:

(Замените YOUR_ACCESS_TOKEN фактическим маркером доступа.)

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

… и в результате получить список подписок, допустимость tooaccess участника-службы

Идентификаторы подписок сокращены для удобства чтения.

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a>Вывод списка всех групп ресурсов в конкретной подписке
Все ресурсы, доступные с hello API диспетчера ресурсов являются вложенными внутри группы ресурсов. Вы можете запрашивать диспетчера ресурсов для существующих групп ресурсов в подписке, используя hello, выполнив запрос HTTP GET. Обратите внимание на то, как идентификатор подписки hello передаются в составе hello URL-адрес этого времени.

Замените YOUR_ACCESS_TOKEN фактическим маркером доступа, а SUBSCRIPTION_ID — идентификатором подписки.

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

Hello вы получите ответ зависит от наличия ни одной группы ресурсов и если да, сколько.

Идентификаторы подписок сокращены для удобства чтения.

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a>Создание группы ресурсов
Таким образом мы только запрос hello API диспетчера ресурсов сведения. Пришло время создания некоторые ресурсы и начнем с простой из них все группы ресурсов hello. Hello следующий запрос HTTP создает группу ресурсов в регионе или место по своему усмотрению и добавляет tooit тег.

(Замените YOUR_ACCESS_TOKEN, ИД_ПОДПИСКИ, RESOURCE_GROUP_NAME фактическое токен доступа, Идентификатором подписки, а имя группы ресурсов, которые вы хотите toocreate hello)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

В случае успешного выполнения вы получаете ответ, который имеет аналогичные toohello следующий ответ:

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

Вы успешно создали группу ресурсов в Azure. Поздравляем!

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a>Развертывание группы ресурсов tooa ресурсов, с помощью шаблона диспетчера ресурсов
При работе с Resource Manager ресурсы можно развертывать с помощью шаблонов. Шаблон определяет несколько ресурсов и соответствующие зависимости. Для этого раздела предполагается вы знакомы с шаблоны диспетчера ресурсов, и мы просто показано, как toomake hello API вызвать toostart развертывания. Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).

Развертывание шаблона не отличаются много toohow вызывать другие API-интерфейсы. Но важной особенностью является то, что развертывание шаблона может занять много времени. Hello API вызов просто возвращает, а именно tooyou как разработчик tooquery состоянии toofind развертывания hello out при развертывании hello. Дополнительные сведения см. в разделе [Отслеживание асинхронных операций Azure](resource-manager-async-operations.md).

В этом примере используется общедоступный шаблон из репозитория [GitHub](https://github.com/Azure/azure-quickstart-templates). шаблон Hello, мы используем развертывает область виртуальных Машин Linux toohello Запад США. Несмотря на то, что в этом примере используется шаблон доступным в открытый репозитория GitHub, вместо этого можно передать полный шаблон hello как часть запроса hello. Обратите внимание, что мы предоставляем значения параметров в запросе hello, используемые внутри hello развертывания шаблона.

(Замените ИД_ПОДПИСКИ, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD и DNS_NAME_FOR_PUBLIC_IP toovalues, соответствующих вашему запросу)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

Hello долгих ответов JSON для данного запроса был опущен tooimprove удобочитаемость этой документации. Hello ответ содержит сведения о развертывании шаблонного hello, созданный вами.

## <a name="next-steps"></a>Дальнейшие действия

- toolearn об обработке асинхронных операций REST, в разделе [отслеживания асинхронных операций Azure](resource-manager-async-operations.md).
