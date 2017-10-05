---
title: "Интерфейсы REST API Resource Manager | Документация Майкрософт"
description: "Обзор примеров проверки подлинности и использования API-интерфейсов REST диспетчера ресурсов"
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
ms.openlocfilehash: 2f7ba23775545637de865f9ef63680ae22c62164
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="02e4d-103">API-интерфейсы REST диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="02e4d-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="02e4d-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="02e4d-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="02e4d-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="02e4d-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="02e4d-106">Портал</span><span class="sxs-lookup"><span data-stu-id="02e4d-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="02e4d-107">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="02e4d-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="02e4d-108">Каждый вызов диспетчера ресурсов Azure, каждый развернутый шаблон, каждая настроенная учетная запись хранения связаны с одним или несколькими вызовами REST API в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02e4d-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="02e4d-109">Эта статья посвящена таким API-интерфейсам и возможностям их вызова без использования пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="02e4d-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="02e4d-110">Такой подход полезен, если требуется полный контроль всех запросов к Azure или если пакет SDK для предпочитаемого языка недоступен либо не поддерживает нужные операции.</span><span class="sxs-lookup"><span data-stu-id="02e4d-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span></span>

<span data-ttu-id="02e4d-111">В этой статье не будет рассматриваться каждый API, существующий в Azure, а только некоторые операции в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="02e4d-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span></span> <span data-ttu-id="02e4d-112">Ознакомившись с основами, переходите к [справочнику по REST API в Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/), который предоставит подробные сведения об использовании остальных API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="02e4d-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="02e4d-113">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="02e4d-113">Authentication</span></span>
<span data-ttu-id="02e4d-114">Проверка подлинности для Resource Manager осуществляется с помощью Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="02e4d-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="02e4d-115">Чтобы подключиться к любому API-интерфейсу, сначала нужно пройти аутентификацию в Azure AD для получения маркера аутентификации, который можно передавать в каждый запрос.</span><span class="sxs-lookup"><span data-stu-id="02e4d-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span></span> <span data-ttu-id="02e4d-116">Мы рассматриваем прямой вызов непосредственно к интерфейсам REST API, и в этом контексте вы вряд ли хотите видеть запрос на ввод имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="02e4d-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span></span> <span data-ttu-id="02e4d-117">Кроме того, мы предполагаем, что двухфакторная проверка подлинности не используется.</span><span class="sxs-lookup"><span data-stu-id="02e4d-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="02e4d-118">Поэтому мы создадим то, что называется приложением Azure AD, и субъект-службу, которые будут использоваться для входа.</span><span class="sxs-lookup"><span data-stu-id="02e4d-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span></span> <span data-ttu-id="02e4d-119">Помните, что Azure AD поддерживает несколько процедур проверки подлинности и все они могут использоваться для получения маркера проверки подлинности, необходимого для последующих запросов API.</span><span class="sxs-lookup"><span data-stu-id="02e4d-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="02e4d-120">Пошаговые инструкции см. в статье [Создание приложения Active Directory и субъекта-службы с доступом к ресурсам с помощью портала](resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="02e4d-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="02e4d-121">Создание маркера доступа</span><span class="sxs-lookup"><span data-stu-id="02e4d-121">Generating an Access Token</span></span>
<span data-ttu-id="02e4d-122">Проверка подлинности в Azure AD выполняется путем вызова службы Azure AD, находящейся по адресу login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="02e4d-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span></span> <span data-ttu-id="02e4d-123">Чтобы выполнить аутентификацию, требуются следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="02e4d-123">To authenticate, you need to have the following information:</span></span>

* <span data-ttu-id="02e4d-124">идентификатор клиента Azure AD (имя Azure AD, используемое для входа; обычно оно совпадает с названием компании, но не обязательно);</span><span class="sxs-lookup"><span data-stu-id="02e4d-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span></span>
* <span data-ttu-id="02e4d-125">идентификатор приложения (полученный на этапе создания приложения Azure AD);</span><span class="sxs-lookup"><span data-stu-id="02e4d-125">Application ID (taken during the Azure AD application creation step)</span></span>
* <span data-ttu-id="02e4d-126">пароль (выбранный при создании приложения Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02e4d-126">Password (that you selected while creating the Azure AD Application)</span></span>

<span data-ttu-id="02e4d-127">В следующем HTTP-запросе замените "Azure AD Tenant ID", "Application ID" и "Password" правильными значениями.</span><span class="sxs-lookup"><span data-stu-id="02e4d-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span></span>

<span data-ttu-id="02e4d-128">**Базовый HTTP-запрос:**</span><span class="sxs-lookup"><span data-stu-id="02e4d-128">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="02e4d-129">Если аутентификация пройдет успешно, на этот запрос будет возвращен ответ такого вида:</span><span class="sxs-lookup"><span data-stu-id="02e4d-129">... will (if authentication succeeds) result in a response similar to the following response:</span></span>

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
<span data-ttu-id="02e4d-130">Значение параметра access_token в ответе выше сокращено для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="02e4d-130">(The access_token in the preceding response have been shortened to increase readability)</span></span>

<span data-ttu-id="02e4d-131">**Создание маркера доступа с помощью Bash:**</span><span class="sxs-lookup"><span data-stu-id="02e4d-131">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="02e4d-132">**Создание маркера доступа с помощью PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="02e4d-132">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="02e4d-133">Ответ содержит маркер доступа, сведения о сроке его действия и о том, для каких ресурсов его можно использовать.</span><span class="sxs-lookup"><span data-stu-id="02e4d-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="02e4d-134">Маркер доступа, полученный в предыдущем вызове HTTP, следует передавать во всех запросах к API в Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02e4d-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span></span> <span data-ttu-id="02e4d-135">Он передается в заголовке с именем "Authorization", который должен иметь значение "Bearer полученный_маркер_доступа".</span><span class="sxs-lookup"><span data-stu-id="02e4d-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="02e4d-136">Обратите внимание на пробел между словом "Bearer" и маркером доступа.</span><span class="sxs-lookup"><span data-stu-id="02e4d-136">Notice the space between "Bearer" and your access token.</span></span>

<span data-ttu-id="02e4d-137">Как видно из приведенного выше ответа HTTP, для маркера определен период действия. Маркер следует сохранить в кэш и повторно использовать в течение всего этого периода.</span><span class="sxs-lookup"><span data-stu-id="02e4d-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="02e4d-138">Несмотря на то, что можно проверить подлинность каждого вызова API в Azure AD, это будет крайне неэффективно.</span><span class="sxs-lookup"><span data-stu-id="02e4d-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="02e4d-139">Вызов интерфейсов REST API в Resource Manager</span><span class="sxs-lookup"><span data-stu-id="02e4d-139">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="02e4d-140">В этом разделе упоминаются только несколько API-интерфейсов, на примере которых мы объясним основные принципы использования операций REST.</span><span class="sxs-lookup"><span data-stu-id="02e4d-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span></span> <span data-ttu-id="02e4d-141">Сведения о других операциях вы найдете в [справочнике по REST API в Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="02e4d-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="02e4d-142">Вывод списка всех подписок</span><span class="sxs-lookup"><span data-stu-id="02e4d-142">List all subscriptions</span></span>
<span data-ttu-id="02e4d-143">Одной из простейших операций является вывод списка доступных подписок, к которым вы можете обращаться.</span><span class="sxs-lookup"><span data-stu-id="02e4d-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span></span> <span data-ttu-id="02e4d-144">В следующем запросе можно увидеть, как маркер доступа передается в качестве заголовка.</span><span class="sxs-lookup"><span data-stu-id="02e4d-144">In the following request, you see how the access token is passed in as a header:</span></span>

<span data-ttu-id="02e4d-145">(Замените YOUR_ACCESS_TOKEN фактическим маркером доступа.)</span><span class="sxs-lookup"><span data-stu-id="02e4d-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="02e4d-146">В ответе вы получите список подписок, к которым может получать доступ этот субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="02e4d-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span></span>

<span data-ttu-id="02e4d-147">Идентификаторы подписок сокращены для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="02e4d-147">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="02e4d-148">Вывод списка всех групп ресурсов в конкретной подписке</span><span class="sxs-lookup"><span data-stu-id="02e4d-148">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="02e4d-149">Все ресурсы, доступные через API-интерфейсы Resource Manager, входят в группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="02e4d-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="02e4d-150">Список групп ресурсов, существующих в подписке, можно получить из Resource Manager с помощью приведенного ниже запроса HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="02e4d-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span></span> <span data-ttu-id="02e4d-151">Обратите внимание, что в этом запросе идентификатор подписки передается в составе URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="02e4d-151">Notice how the subscription ID is passed in as part of the URL this time.</span></span>

<span data-ttu-id="02e4d-152">Замените YOUR_ACCESS_TOKEN фактическим маркером доступа, а SUBSCRIPTION_ID — идентификатором подписки.</span><span class="sxs-lookup"><span data-stu-id="02e4d-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="02e4d-153">Ответ зависит от того, определены ли в подписке группы ресурсов, и сколько их.</span><span class="sxs-lookup"><span data-stu-id="02e4d-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="02e4d-154">Идентификаторы подписок сокращены для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="02e4d-154">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="02e4d-155">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="02e4d-155">Create a resource group</span></span>
<span data-ttu-id="02e4d-156">Пока мы обращались к API-интерфейсам Resource Manager только с запросами на получение информации.</span><span class="sxs-lookup"><span data-stu-id="02e4d-156">So far, we've only been querying the Resource Manager APIs for information.</span></span> <span data-ttu-id="02e4d-157">Теперь давайте попробуем создать какие-то ресурсы. Проще всего создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="02e4d-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span></span> <span data-ttu-id="02e4d-158">Следующий запрос HTTP создает группу ресурсов в указанном регионе или расположении и добавляет к ней тег.</span><span class="sxs-lookup"><span data-stu-id="02e4d-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span></span>

<span data-ttu-id="02e4d-159">Замените YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME фактическим маркером доступа, идентификатором подписки и именем группы ресурсов, которую вы планируете создать.</span><span class="sxs-lookup"><span data-stu-id="02e4d-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span></span>

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

<span data-ttu-id="02e4d-160">В случае успешного выполнения отобразится ответ, который выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="02e4d-160">If successful, you get a response that is similar to the following response:</span></span>

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

<span data-ttu-id="02e4d-161">Вы успешно создали группу ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="02e4d-161">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="02e4d-162">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="02e4d-162">Congratulations!</span></span>

### <a name="deploy-resources-to-a-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="02e4d-163">Развертывание ресурсов в группе ресурсов с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="02e4d-163">Deploy resources to a resource group using a Resource Manager Template</span></span>
<span data-ttu-id="02e4d-164">При работе с Resource Manager ресурсы можно развертывать с помощью шаблонов.</span><span class="sxs-lookup"><span data-stu-id="02e4d-164">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="02e4d-165">Шаблон определяет несколько ресурсов и соответствующие зависимости.</span><span class="sxs-lookup"><span data-stu-id="02e4d-165">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="02e4d-166">В этом разделе мы предполагаем, что вы уже знакомы с шаблонами Resource Manager, поэтому сразу перейдем к вызову API для запуска развертывания.</span><span class="sxs-lookup"><span data-stu-id="02e4d-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span></span> <span data-ttu-id="02e4d-167">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="02e4d-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="02e4d-168">Развертывание шаблона сильно не отличается от вызова других API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="02e4d-168">Deployment of a template doesn't differ much to how you call other APIs.</span></span> <span data-ttu-id="02e4d-169">Но важной особенностью является то, что развертывание шаблона может занять много времени.</span><span class="sxs-lookup"><span data-stu-id="02e4d-169">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="02e4d-170">Вызов API просто завершается, а дальше вы как разработчик можете реализовать проверку статуса развертывания, чтобы выяснить, когда оно завершится.</span><span class="sxs-lookup"><span data-stu-id="02e4d-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span></span> <span data-ttu-id="02e4d-171">Дополнительные сведения см. в разделе [Отслеживание асинхронных операций Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="02e4d-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="02e4d-172">В этом примере используется общедоступный шаблон из репозитория [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="02e4d-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="02e4d-173">Этот шаблон развертывает виртуальную машину Linux в западной части США.</span><span class="sxs-lookup"><span data-stu-id="02e4d-173">The template we use deploys a Linux VM to the West US region.</span></span> <span data-ttu-id="02e4d-174">В нашем примере используется ссылка на шаблон, размещенный в общедоступном репозитории, в данном случае GitHub. Вместо этого вы можете передать сам шаблон в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="02e4d-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span></span> <span data-ttu-id="02e4d-175">Обратите внимание, что в запросе мы передаем значения параметров, которые будут использоваться внутри шаблона.</span><span class="sxs-lookup"><span data-stu-id="02e4d-175">Note that we provide parameter values in the request that are used inside the deployed template.</span></span>

<span data-ttu-id="02e4d-176">Замените SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD и DNS_NAME_FOR_PUBLIC_IP значениями, соответствующими вашему запросу.</span><span class="sxs-lookup"><span data-stu-id="02e4d-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span></span>

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

<span data-ttu-id="02e4d-177">Для удобства чтения статьи мы опустили довольно длинный ответ JSON на данный запрос.</span><span class="sxs-lookup"><span data-stu-id="02e4d-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span></span> <span data-ttu-id="02e4d-178">Этот ответ содержит сведения о развертывании, созданном на основе шаблона.</span><span class="sxs-lookup"><span data-stu-id="02e4d-178">The response contains information about the templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02e4d-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02e4d-179">Next steps</span></span>

- <span data-ttu-id="02e4d-180">Сведения об обработке асинхронных операций REST см. в статье [Отслеживание асинхронных операций Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="02e4d-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
