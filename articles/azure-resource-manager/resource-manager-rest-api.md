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
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="a1d76-103">API-интерфейсы REST диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="a1d76-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1d76-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1d76-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="a1d76-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="a1d76-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="a1d76-106">Портал</span><span class="sxs-lookup"><span data-stu-id="a1d76-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="a1d76-107">REST API</span><span class="sxs-lookup"><span data-stu-id="a1d76-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="a1d76-108">За каждый вызов tooAzure диспетчера ресурсов, за каждого развернутого шаблона за каждые настроенная учетная запись хранилища существует один или несколько вызовов toohello диспетчера ресурсов Azure в API RESTful.</span><span class="sxs-lookup"><span data-stu-id="a1d76-108">Behind every call tooAzure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls toohello Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="a1d76-109">Этот раздел является выделяемых toothose API-интерфейсы и как их можно вызывать без использования во всех любых SDK.</span><span class="sxs-lookup"><span data-stu-id="a1d76-109">This topic is devoted toothose APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="a1d76-110">Этот подход полезен, если требуется полный контроль над tooAzure запросы или hello пакета SDK для предпочитаемого языка недоступна или не поддерживает операцию hello, что нужно.</span><span class="sxs-lookup"><span data-stu-id="a1d76-110">This approach is useful if you want full control of requests tooAzure, or if hello SDK for your preferred language is not available or doesn't support hello operations you need.</span></span>

<span data-ttu-id="a1d76-111">В этой статье не проходят через каждый API, который предоставляется в Azure, но вместо этого использует некоторые операции в подключении toothem примеры.</span><span class="sxs-lookup"><span data-stu-id="a1d76-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect toothem.</span></span> <span data-ttu-id="a1d76-112">Поняв основы hello, можно прочитать hello [Справочник по API REST диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/resources/) toofind подробные сведения о как остальные hello toouse hello API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="a1d76-112">After you understand hello basics, you can read hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind detailed information on how toouse hello rest of hello APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="a1d76-113">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="a1d76-113">Authentication</span></span>
<span data-ttu-id="a1d76-114">Проверка подлинности для Resource Manager осуществляется с помощью Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="a1d76-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="a1d76-115">tooconnect tooany API, необходимо сначала tooauthenticate с Azure AD tooreceive маркер проверки подлинности, который можно передать на tooevery запроса.</span><span class="sxs-lookup"><span data-stu-id="a1d76-115">tooconnect tooany API, you first need tooauthenticate with Azure AD tooreceive an authentication token that you can pass on tooevery request.</span></span> <span data-ttu-id="a1d76-116">Как здесь описывается вызов чисто напрямую toohello API-интерфейс REST, предполагается, что вы не хотите tooauthenticate по необходимости вводить имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a1d76-116">As we are describing a pure call directly toohello REST APIs, we assume that you don't want tooauthenticate by being prompted for a username and password.</span></span> <span data-ttu-id="a1d76-117">Кроме того, мы предполагаем, что двухфакторная проверка подлинности не используется.</span><span class="sxs-lookup"><span data-stu-id="a1d76-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="a1d76-118">Таким образом мы создания приложения Azure AD и субъекта-службы, используемые toolog в.</span><span class="sxs-lookup"><span data-stu-id="a1d76-118">Therefore, we create what is called an Azure AD Application and a service principal that are used toolog in.</span></span> <span data-ttu-id="a1d76-119">Но следует помнить, что Azure AD поддерживает несколько процедур проверки подлинности и все они могут быть используется tooretrieve этот маркер проверки подлинности, необходимую для последующих запросов API.</span><span class="sxs-lookup"><span data-stu-id="a1d76-119">But remember that Azure AD support several authentication procedures and all of them could be used tooretrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="a1d76-120">Пошаговые инструкции см. в статье [Создание приложения Active Directory и субъекта-службы с доступом к ресурсам с помощью портала](resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a1d76-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="a1d76-121">Создание маркера доступа</span><span class="sxs-lookup"><span data-stu-id="a1d76-121">Generating an Access Token</span></span>
<span data-ttu-id="a1d76-122">Выполняя запрос tooAzure AD, расположенный в login.microsoftonline.com выполняется проверка подлинности в Azure AD. tooauthenticate, требуется hello toohave следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a1d76-122">Authentication against Azure AD is done by calling out tooAzure AD, located at login.microsoftonline.com. tooauthenticate, you need toohave hello following information:</span></span>

* <span data-ttu-id="a1d76-123">Идентификатор клиента Azure AD (hello, Azure AD, вы используете toolog в имя, часто hello то же, что ваша компания, но не обязательно)</span><span class="sxs-lookup"><span data-stu-id="a1d76-123">Azure AD Tenant ID (hello name of that Azure AD you are using toolog in, often hello same as your company but not necessary)</span></span>
* <span data-ttu-id="a1d76-124">Идентификатор приложения (предпринятые во время шага создания приложения hello Azure AD)</span><span class="sxs-lookup"><span data-stu-id="a1d76-124">Application ID (taken during hello Azure AD application creation step)</span></span>
* <span data-ttu-id="a1d76-125">Пароль (который был выбран при создании hello приложения Azure AD)</span><span class="sxs-lookup"><span data-stu-id="a1d76-125">Password (that you selected while creating hello Azure AD Application)</span></span>

<span data-ttu-id="a1d76-126">В hello, выполнив HTTP-запроса чтобы убедиться, что tooreplace «Azure AD клиента ID», «Идентификатор приложения» и «Пароль» с правильными значениями hello.</span><span class="sxs-lookup"><span data-stu-id="a1d76-126">In hello following HTTP request, make sure tooreplace "Azure AD Tenant ID", "Application ID" and "Password" with hello correct values.</span></span>

<span data-ttu-id="a1d76-127">**Базовый HTTP-запрос:**</span><span class="sxs-lookup"><span data-stu-id="a1d76-127">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="a1d76-128">... будет (если проверка подлинности успешно пройдена) привести аналогичные toohello ответа, следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="a1d76-128">... will (if authentication succeeds) result in a response similar toohello following response:</span></span>

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
<span data-ttu-id="a1d76-129">(access_token hello в предшествующих ответа hello было сокращенный tooincrease удобства чтения)</span><span class="sxs-lookup"><span data-stu-id="a1d76-129">(hello access_token in hello preceding response have been shortened tooincrease readability)</span></span>

<span data-ttu-id="a1d76-130">**Создание маркера доступа с помощью Bash:**</span><span class="sxs-lookup"><span data-stu-id="a1d76-130">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="a1d76-131">**Создание маркера доступа с помощью PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="a1d76-131">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="a1d76-132">Hello ответ содержит токен доступа, сведения о как долго этот маркер является допустимым и сведения о какой ресурс можно использовать этот маркер для.</span><span class="sxs-lookup"><span data-stu-id="a1d76-132">hello response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="a1d76-133">маркер доступа Hello, полученный в предыдущем вызове HTTP hello должны передаваться в для всех запросов toohello API диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a1d76-133">hello access token you received in hello previous HTTP call must be passed in for all request toohello Resource Manager API.</span></span> <span data-ttu-id="a1d76-134">Передайте его в качестве значение заголовка «Авторизации» с именем hello значение «YOUR_ACCESS_TOKEN носителя».</span><span class="sxs-lookup"><span data-stu-id="a1d76-134">You pass it as a header value named "Authorization" with hello value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="a1d76-135">Обратите внимание, hello пробел между «Bearer» и маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="a1d76-135">Notice hello space between "Bearer" and your access token.</span></span>

<span data-ttu-id="a1d76-136">Как видно из hello выше результат HTTP hello маркер действителен за определенный период времени, во время которого следует кэшировать и повторно использовать этот же токен.</span><span class="sxs-lookup"><span data-stu-id="a1d76-136">As you can see from hello above HTTP Result, hello token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="a1d76-137">Даже если это возможно tooauthenticate от Azure AD для каждого вызова API будет крайне неэффективно.</span><span class="sxs-lookup"><span data-stu-id="a1d76-137">Even if it is possible tooauthenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="a1d76-138">Вызов интерфейсов REST API в Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a1d76-138">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="a1d76-139">В этом разделе использует только несколько интерфейсов API tooexplain hello базовое использование операций REST hello.</span><span class="sxs-lookup"><span data-stu-id="a1d76-139">This topic only uses a few APIs tooexplain hello basic usage of hello REST operations.</span></span> <span data-ttu-id="a1d76-140">Сведения обо всех операциях hello см. в разделе [API REST диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="a1d76-140">For information about all hello operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="a1d76-141">Вывод списка всех подписок</span><span class="sxs-lookup"><span data-stu-id="a1d76-141">List all subscriptions</span></span>
<span data-ttu-id="a1d76-142">Одна из hello простой операции, которые можно сделать — доступные подписки hello toolist, которые можно открыть.</span><span class="sxs-lookup"><span data-stu-id="a1d76-142">One of hello simplest operations you can do is toolist hello available subscriptions that you can access.</span></span> <span data-ttu-id="a1d76-143">Привет, следующий запрос вы видите, как маркер доступа hello передаются в качестве заголовка:</span><span class="sxs-lookup"><span data-stu-id="a1d76-143">In hello following request, you see how hello access token is passed in as a header:</span></span>

<span data-ttu-id="a1d76-144">(Замените YOUR_ACCESS_TOKEN фактическим маркером доступа.)</span><span class="sxs-lookup"><span data-stu-id="a1d76-144">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="a1d76-145">… и в результате получить список подписок, допустимость tooaccess участника-службы</span><span class="sxs-lookup"><span data-stu-id="a1d76-145">... and as a result, you get a list of subscriptions that this service principal is allowed tooaccess</span></span>

<span data-ttu-id="a1d76-146">Идентификаторы подписок сокращены для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="a1d76-146">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="a1d76-147">Вывод списка всех групп ресурсов в конкретной подписке</span><span class="sxs-lookup"><span data-stu-id="a1d76-147">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="a1d76-148">Все ресурсы, доступные с hello API диспетчера ресурсов являются вложенными внутри группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a1d76-148">All resources available with hello Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="a1d76-149">Вы можете запрашивать диспетчера ресурсов для существующих групп ресурсов в подписке, используя hello, выполнив запрос HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="a1d76-149">You can query Resource Manager for existing resource groups in your subscription using hello following HTTP GET request.</span></span> <span data-ttu-id="a1d76-150">Обратите внимание на то, как идентификатор подписки hello передаются в составе hello URL-адрес этого времени.</span><span class="sxs-lookup"><span data-stu-id="a1d76-150">Notice how hello subscription ID is passed in as part of hello URL this time.</span></span>

<span data-ttu-id="a1d76-151">Замените YOUR_ACCESS_TOKEN фактическим маркером доступа, а SUBSCRIPTION_ID — идентификатором подписки.</span><span class="sxs-lookup"><span data-stu-id="a1d76-151">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="a1d76-152">Hello вы получите ответ зависит от наличия ни одной группы ресурсов и если да, сколько.</span><span class="sxs-lookup"><span data-stu-id="a1d76-152">hello response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="a1d76-153">Идентификаторы подписок сокращены для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="a1d76-153">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="a1d76-154">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="a1d76-154">Create a resource group</span></span>
<span data-ttu-id="a1d76-155">Таким образом мы только запрос hello API диспетчера ресурсов сведения.</span><span class="sxs-lookup"><span data-stu-id="a1d76-155">So far, we've only been querying hello Resource Manager APIs for information.</span></span> <span data-ttu-id="a1d76-156">Пришло время создания некоторые ресурсы и начнем с простой из них все группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="a1d76-156">It's time we create some resources, and let's start by hello simplest of them all, a resource group.</span></span> <span data-ttu-id="a1d76-157">Hello следующий запрос HTTP создает группу ресурсов в регионе или место по своему усмотрению и добавляет tooit тег.</span><span class="sxs-lookup"><span data-stu-id="a1d76-157">hello following HTTP request creates a resource group in a region/location of your choice, and adds a tag tooit.</span></span>

<span data-ttu-id="a1d76-158">(Замените YOUR_ACCESS_TOKEN, ИД_ПОДПИСКИ, RESOURCE_GROUP_NAME фактическое токен доступа, Идентификатором подписки, а имя группы ресурсов, которые вы хотите toocreate hello)</span><span class="sxs-lookup"><span data-stu-id="a1d76-158">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of hello Resource Group you want toocreate)</span></span>

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

<span data-ttu-id="a1d76-159">В случае успешного выполнения вы получаете ответ, который имеет аналогичные toohello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="a1d76-159">If successful, you get a response that is similar toohello following response:</span></span>

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

<span data-ttu-id="a1d76-160">Вы успешно создали группу ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="a1d76-160">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="a1d76-161">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="a1d76-161">Congratulations!</span></span>

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="a1d76-162">Развертывание группы ресурсов tooa ресурсов, с помощью шаблона диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="a1d76-162">Deploy resources tooa resource group using a Resource Manager Template</span></span>
<span data-ttu-id="a1d76-163">При работе с Resource Manager ресурсы можно развертывать с помощью шаблонов.</span><span class="sxs-lookup"><span data-stu-id="a1d76-163">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="a1d76-164">Шаблон определяет несколько ресурсов и соответствующие зависимости.</span><span class="sxs-lookup"><span data-stu-id="a1d76-164">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="a1d76-165">Для этого раздела предполагается вы знакомы с шаблоны диспетчера ресурсов, и мы просто показано, как toomake hello API вызвать toostart развертывания.</span><span class="sxs-lookup"><span data-stu-id="a1d76-165">For this section, we assume you are familiar with Resource Manager templates, and we just show you how toomake hello API call toostart deployment.</span></span> <span data-ttu-id="a1d76-166">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a1d76-166">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="a1d76-167">Развертывание шаблона не отличаются много toohow вызывать другие API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="a1d76-167">Deployment of a template doesn't differ much toohow you call other APIs.</span></span> <span data-ttu-id="a1d76-168">Но важной особенностью является то, что развертывание шаблона может занять много времени.</span><span class="sxs-lookup"><span data-stu-id="a1d76-168">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="a1d76-169">Hello API вызов просто возвращает, а именно tooyou как разработчик tooquery состоянии toofind развертывания hello out при развертывании hello.</span><span class="sxs-lookup"><span data-stu-id="a1d76-169">hello API call just returns, and it's up tooyou as developer tooquery for status of hello deployment toofind out when hello deployment is done.</span></span> <span data-ttu-id="a1d76-170">Дополнительные сведения см. в разделе [Отслеживание асинхронных операций Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a1d76-170">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="a1d76-171">В этом примере используется общедоступный шаблон из репозитория [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a1d76-171">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="a1d76-172">шаблон Hello, мы используем развертывает область виртуальных Машин Linux toohello Запад США.</span><span class="sxs-lookup"><span data-stu-id="a1d76-172">hello template we use deploys a Linux VM toohello West US region.</span></span> <span data-ttu-id="a1d76-173">Несмотря на то, что в этом примере используется шаблон доступным в открытый репозитория GitHub, вместо этого можно передать полный шаблон hello как часть запроса hello.</span><span class="sxs-lookup"><span data-stu-id="a1d76-173">Even though this example uses a template available in a public repository like GitHub, you can instead pass hello full template as part of hello request.</span></span> <span data-ttu-id="a1d76-174">Обратите внимание, что мы предоставляем значения параметров в запросе hello, используемые внутри hello развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="a1d76-174">Note that we provide parameter values in hello request that are used inside hello deployed template.</span></span>

<span data-ttu-id="a1d76-175">(Замените ИД_ПОДПИСКИ, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD и DNS_NAME_FOR_PUBLIC_IP toovalues, соответствующих вашему запросу)</span><span class="sxs-lookup"><span data-stu-id="a1d76-175">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP toovalues appropriate for your request)</span></span>

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

<span data-ttu-id="a1d76-176">Hello долгих ответов JSON для данного запроса был опущен tooimprove удобочитаемость этой документации.</span><span class="sxs-lookup"><span data-stu-id="a1d76-176">hello long JSON response for this request has been omitted tooimprove readability of this documentation.</span></span> <span data-ttu-id="a1d76-177">Hello ответ содержит сведения о развертывании шаблонного hello, созданный вами.</span><span class="sxs-lookup"><span data-stu-id="a1d76-177">hello response contains information about hello templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1d76-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1d76-178">Next steps</span></span>

- <span data-ttu-id="a1d76-179">toolearn об обработке асинхронных операций REST, в разделе [отслеживания асинхронных операций Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a1d76-179">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
