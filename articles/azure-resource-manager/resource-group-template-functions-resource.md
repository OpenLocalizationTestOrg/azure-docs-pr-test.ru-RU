---
title: "Функции шаблонов Azure Resource Manager для работы с ресурсами | Документация Майкрософт"
description: "Описывает функции, используемые в шаблоне Azure Resource Manager для получения значений ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: 494ade55f21c19d9c68d5cc52756528401d9bb77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="7ec9a-103">Функции для работы с ресурсами в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7ec9a-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="7ec9a-104">Диспетчер ресурсов предоставляет следующие функции для получения значений ресурсов:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-104">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="7ec9a-105">listKeys и list{Value}</span><span class="sxs-lookup"><span data-stu-id="7ec9a-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="7ec9a-106">providers</span><span class="sxs-lookup"><span data-stu-id="7ec9a-106">providers</span></span>](#providers)
* [<span data-ttu-id="7ec9a-107">reference</span><span class="sxs-lookup"><span data-stu-id="7ec9a-107">reference</span></span>](#reference)
* [<span data-ttu-id="7ec9a-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="7ec9a-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="7ec9a-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="7ec9a-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="7ec9a-110">subscription</span><span class="sxs-lookup"><span data-stu-id="7ec9a-110">subscription</span></span>](#subscription)

<span data-ttu-id="7ec9a-111">Получение значений параметров, переменных или текущего развертывания описано в разделе [Функции для параметров развертывания](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7ec9a-111">To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="7ec9a-112">listKeys и list{Value}</span><span class="sxs-lookup"><span data-stu-id="7ec9a-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="7ec9a-113">Возвращает значения для любого типа ресурса, который поддерживает операцию list.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-113">Returns the values for any resource type that supports the list operation.</span></span> <span data-ttu-id="7ec9a-114">Наиболее распространенным вариантом применения является `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-114">The most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="7ec9a-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="7ec9a-115">Parameters</span></span>

| <span data-ttu-id="7ec9a-116">Параметр</span><span class="sxs-lookup"><span data-stu-id="7ec9a-116">Parameter</span></span> | <span data-ttu-id="7ec9a-117">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7ec9a-117">Required</span></span> | <span data-ttu-id="7ec9a-118">Тип</span><span class="sxs-lookup"><span data-stu-id="7ec9a-118">Type</span></span> | <span data-ttu-id="7ec9a-119">Описание</span><span class="sxs-lookup"><span data-stu-id="7ec9a-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7ec9a-120">имя_ресурса или идентификатор_ресурса</span><span class="sxs-lookup"><span data-stu-id="7ec9a-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="7ec9a-121">Да</span><span class="sxs-lookup"><span data-stu-id="7ec9a-121">Yes</span></span> |<span data-ttu-id="7ec9a-122">string</span><span class="sxs-lookup"><span data-stu-id="7ec9a-122">string</span></span> |<span data-ttu-id="7ec9a-123">Уникальный идентификатор ресурса.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-123">Unique identifier for the resource.</span></span> |
| <span data-ttu-id="7ec9a-124">версия_API</span><span class="sxs-lookup"><span data-stu-id="7ec9a-124">apiVersion</span></span> |<span data-ttu-id="7ec9a-125">Да</span><span class="sxs-lookup"><span data-stu-id="7ec9a-125">Yes</span></span> |<span data-ttu-id="7ec9a-126">string</span><span class="sxs-lookup"><span data-stu-id="7ec9a-126">string</span></span> |<span data-ttu-id="7ec9a-127">Версия API для состояния среды выполнения ресурса.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-127">API version of resource runtime state.</span></span> <span data-ttu-id="7ec9a-128">Как правило, указывается в формате **гггг-мм-дд**.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-128">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7ec9a-129">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7ec9a-129">Return value</span></span>

<span data-ttu-id="7ec9a-130">Возвращаемый функцией listKeys объект имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-130">The returned object from listKeys has the following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="7ec9a-131">Другие функции list возвращают данные в других форматах.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-131">Other list functions have different return formats.</span></span> <span data-ttu-id="7ec9a-132">Чтобы просмотреть формат функции, включите ее в раздел outputs, как показано в примере шаблона.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-132">To see the format of a function, include it in the outputs section as shown in the example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="7ec9a-133">Примечания</span><span class="sxs-lookup"><span data-stu-id="7ec9a-133">Remarks</span></span>

<span data-ttu-id="7ec9a-134">Любая операция, которая начинается с **list**, может быть использована в шаблоне как функция.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="7ec9a-135">Это относится не только к listKeys, но и к таким операциям, как `list`, `listAdminKeys` и `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-135">The available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="7ec9a-136">Но нельзя использовать операции **list**, требующие значения в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-136">However, you cannot use **list** operations that require values in the request body.</span></span> <span data-ttu-id="7ec9a-137">Например, для операции [перечисления SAS учетной записи](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) требуются параметры текста запроса, такие как *signedExpiry*, поэтому ее нельзя использовать внутри шаблона.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-137">For example, the [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="7ec9a-138">Чтобы определить, какие типы ресурсов поддерживают операцию list, можно использовать следующие варианты:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-138">To determine which resource types have a list operation, you have the following options:</span></span>

* <span data-ttu-id="7ec9a-139">Просмотрите [операции REST API](/rest/api/) для поставщика ресурсов и найдите операции list.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-139">View the [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="7ec9a-140">Например, в учетных записях хранения есть [операция listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="7ec9a-140">For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="7ec9a-141">Воспользуйтесь командлетом PowerShell [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation).</span><span class="sxs-lookup"><span data-stu-id="7ec9a-141">Use the [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="7ec9a-142">В следующем примере извлекаются все операции list для учетных записей хранения:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-142">The following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="7ec9a-143">Используйте следующую команду Azure CLI, чтобы отфильтровать только операции list:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-143">Use the following Azure CLI command to filter only the list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="7ec9a-144">Укажите ресурс с помощью [функции resourceId](#resourceid) или формата `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-144">Specify the resource by using either the [resourceId function](#resourceid), or the format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="7ec9a-145">Пример</span><span class="sxs-lookup"><span data-stu-id="7ec9a-145">Example</span></span>

<span data-ttu-id="7ec9a-146">В следующем примере показано, как получить в разделе выходных данных первичный и вторичный ключи из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-146">The following example shows how to return the primary and secondary keys from a storage account in the outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="7ec9a-147">providers</span><span class="sxs-lookup"><span data-stu-id="7ec9a-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="7ec9a-148">Возвращает сведения о поставщике ресурсов и поддерживаемых типах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="7ec9a-149">Если тип ресурса не указан, функция возвращает все типы, поддерживаемые для поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-149">If you do not provide a resource type, the function returns all the supported types for the resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="7ec9a-150">Параметры</span><span class="sxs-lookup"><span data-stu-id="7ec9a-150">Parameters</span></span>

| <span data-ttu-id="7ec9a-151">Параметр</span><span class="sxs-lookup"><span data-stu-id="7ec9a-151">Parameter</span></span> | <span data-ttu-id="7ec9a-152">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7ec9a-152">Required</span></span> | <span data-ttu-id="7ec9a-153">Тип</span><span class="sxs-lookup"><span data-stu-id="7ec9a-153">Type</span></span> | <span data-ttu-id="7ec9a-154">Описание</span><span class="sxs-lookup"><span data-stu-id="7ec9a-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7ec9a-155">пространство_имен_поставщика</span><span class="sxs-lookup"><span data-stu-id="7ec9a-155">providerNamespace</span></span> |<span data-ttu-id="7ec9a-156">Да</span><span class="sxs-lookup"><span data-stu-id="7ec9a-156">Yes</span></span> |<span data-ttu-id="7ec9a-157">string</span><span class="sxs-lookup"><span data-stu-id="7ec9a-157">string</span></span> |<span data-ttu-id="7ec9a-158">Пространство имен поставщика.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-158">Namespace of the provider</span></span> |
| <span data-ttu-id="7ec9a-159">тип_ресурса</span><span class="sxs-lookup"><span data-stu-id="7ec9a-159">resourceType</span></span> |<span data-ttu-id="7ec9a-160">Нет</span><span class="sxs-lookup"><span data-stu-id="7ec9a-160">No</span></span> |<span data-ttu-id="7ec9a-161">string</span><span class="sxs-lookup"><span data-stu-id="7ec9a-161">string</span></span> |<span data-ttu-id="7ec9a-162">Тип ресурса в указанном пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-162">The type of resource within the specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7ec9a-163">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7ec9a-163">Return value</span></span>

<span data-ttu-id="7ec9a-164">Все поддерживаемые типы возвращаются в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-164">Each supported type is returned in the following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="7ec9a-165">Упорядочение массива возвращаемых значений не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-165">Array ordering of the returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="7ec9a-166">Пример</span><span class="sxs-lookup"><span data-stu-id="7ec9a-166">Example</span></span>

<span data-ttu-id="7ec9a-167">Следующий пример показывает, как использовать функцию provider:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-167">The following example shows how to use the provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="7ec9a-168">В предыдущем примере возвращается объект в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-168">The preceding example returns an object in the following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="7ec9a-169">reference</span><span class="sxs-lookup"><span data-stu-id="7ec9a-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="7ec9a-170">Возвращает объект, представляющий состояние среды выполнения ресурса.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="7ec9a-171">Параметры</span><span class="sxs-lookup"><span data-stu-id="7ec9a-171">Parameters</span></span>

| <span data-ttu-id="7ec9a-172">Параметр</span><span class="sxs-lookup"><span data-stu-id="7ec9a-172">Parameter</span></span> | <span data-ttu-id="7ec9a-173">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7ec9a-173">Required</span></span> | <span data-ttu-id="7ec9a-174">Тип</span><span class="sxs-lookup"><span data-stu-id="7ec9a-174">Type</span></span> | <span data-ttu-id="7ec9a-175">Описание</span><span class="sxs-lookup"><span data-stu-id="7ec9a-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7ec9a-176">имя_ресурса или идентификатор_ресурса</span><span class="sxs-lookup"><span data-stu-id="7ec9a-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="7ec9a-177">Да</span><span class="sxs-lookup"><span data-stu-id="7ec9a-177">Yes</span></span> |<span data-ttu-id="7ec9a-178">string</span><span class="sxs-lookup"><span data-stu-id="7ec9a-178">string</span></span> |<span data-ttu-id="7ec9a-179">Имя или уникальный идентификатор ресурса.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="7ec9a-180">версия_API</span><span class="sxs-lookup"><span data-stu-id="7ec9a-180">apiVersion</span></span> |<span data-ttu-id="7ec9a-181">Нет</span><span class="sxs-lookup"><span data-stu-id="7ec9a-181">No</span></span> |<span data-ttu-id="7ec9a-182">string</span><span class="sxs-lookup"><span data-stu-id="7ec9a-182">string</span></span> |<span data-ttu-id="7ec9a-183">Версия API для указанного ресурса.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-183">API version of the specified resource.</span></span> <span data-ttu-id="7ec9a-184">Если ресурс не предоставляется в рамках того же шаблона, необходимо включить этот параметр.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-184">Include this parameter when the resource is not provisioned within same template.</span></span> <span data-ttu-id="7ec9a-185">Как правило, указывается в формате **гггг-мм-дд**.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-185">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7ec9a-186">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7ec9a-186">Return value</span></span>

<span data-ttu-id="7ec9a-187">Каждый тип ресурса возвращает для функции reference разные свойства.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-187">Every resource type returns different properties for the reference function.</span></span> <span data-ttu-id="7ec9a-188">Функция не возвращает данные в едином предварительно заданном формате.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-188">The function does not return a single, predefined format.</span></span> <span data-ttu-id="7ec9a-189">Чтобы просмотреть свойства для типа ресурса, возвратите объект в разделе outputs, как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-189">To see the properties for a resource type, return the object in the outputs section as shown in the example.</span></span>

### <a name="remarks"></a><span data-ttu-id="7ec9a-190">Примечания</span><span class="sxs-lookup"><span data-stu-id="7ec9a-190">Remarks</span></span>

<span data-ttu-id="7ec9a-191">Функция reference получает свое значение из состояния среды выполнения, и поэтому ее невозможно использовать в разделе переменных.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-191">The reference function derives its value from a runtime state, and therefore cannot be used in the variables section.</span></span> <span data-ttu-id="7ec9a-192">Она может использоваться в разделе выходных данных шаблона.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="7ec9a-193">С помощью функции reference вы прямо объявляете, что один ресурс зависит от другого, если ресурс, на который указывает ссылка, предоставляется в том же шаблоне.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-193">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template.</span></span> <span data-ttu-id="7ec9a-194">При этом свойство dependsOn использовать не нужно.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-194">You do not need to also use the dependsOn property.</span></span> <span data-ttu-id="7ec9a-195">Расчет функции выполняется только после развертывания ресурса, на который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-195">The function is not evaluated until the referenced resource has completed deployment.</span></span>

<span data-ttu-id="7ec9a-196">Чтобы просмотреть имена и значения свойств для типа ресурса, создайте в разделе outputs шаблон, который возвращает объект.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-196">To see the property names and values for a resource type, create a template that returns the object in the outputs section.</span></span> <span data-ttu-id="7ec9a-197">Если ресурс этого типа уже существует, то шаблон возвращает объект, не развертывая новых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-197">If you have an existing resource of that type, your template returns the object without deploying any new resources.</span></span> 

<span data-ttu-id="7ec9a-198">Обычно функция **reference** используется, чтобы получить определенное значение из объекта, например универсальный код ресурса (URI) конечной точки большого двоичного объекта или полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-198">Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="7ec9a-199">Пример</span><span class="sxs-lookup"><span data-stu-id="7ec9a-199">Example</span></span>

<span data-ttu-id="7ec9a-200">Чтобы развернуть ресурс и сослаться на него в одном шаблоне, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-200">To deploy and reference the resource in the same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="7ec9a-201">В предыдущем примере возвращается объект в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-201">The preceding example returns an object in the following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="7ec9a-202">Следующий пример ссылается на учетную запись хранения, которая не развертывается в этом шаблоне.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-202">The following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="7ec9a-203">Учетная запись хранения уже существует в той же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-203">The storage account already exists within the same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="7ec9a-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="7ec9a-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="7ec9a-205">Возвращает объект, который представляет текущую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-205">Returns an object that represents the current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="7ec9a-206">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7ec9a-206">Return value</span></span>

<span data-ttu-id="7ec9a-207">Возвращаемый объект имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-207">The returned object is in the following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="7ec9a-208">Примечания</span><span class="sxs-lookup"><span data-stu-id="7ec9a-208">Remarks</span></span>

<span data-ttu-id="7ec9a-209">Как правило, функция resourceGroup используется для создания ресурсов в одном расположении с группой ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-209">A common use of the resourceGroup function is to create resources in the same location as the resource group.</span></span> <span data-ttu-id="7ec9a-210">В следующем примере расположение группы ресурсов используется для назначения расположения веб-сайту.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-210">The following example uses the resource group location to assign the location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="7ec9a-211">Пример</span><span class="sxs-lookup"><span data-stu-id="7ec9a-211">Example</span></span>

<span data-ttu-id="7ec9a-212">Следующий шаблон возвращает свойства группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-212">The following template returns the properties of the resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="7ec9a-213">В предыдущем примере возвращается объект в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-213">The preceding example returns an object in the following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="7ec9a-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="7ec9a-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="7ec9a-215">Возвращает уникальный идентификатор ресурса.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-215">Returns the unique identifier of a resource.</span></span> <span data-ttu-id="7ec9a-216">Используйте эту функцию в том случае, когда имя ресурса является неоднозначным или не было предоставлено в пределах того же шаблона.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-216">You use this function when the resource name is ambiguous or not provisioned within the same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="7ec9a-217">Параметры</span><span class="sxs-lookup"><span data-stu-id="7ec9a-217">Parameters</span></span>

| <span data-ttu-id="7ec9a-218">Параметр</span><span class="sxs-lookup"><span data-stu-id="7ec9a-218">Parameter</span></span> | <span data-ttu-id="7ec9a-219">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7ec9a-219">Required</span></span> | <span data-ttu-id="7ec9a-220">Тип</span><span class="sxs-lookup"><span data-stu-id="7ec9a-220">Type</span></span> | <span data-ttu-id="7ec9a-221">Описание</span><span class="sxs-lookup"><span data-stu-id="7ec9a-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7ec9a-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7ec9a-222">subscriptionId</span></span> |<span data-ttu-id="7ec9a-223">Нет</span><span class="sxs-lookup"><span data-stu-id="7ec9a-223">No</span></span> |<span data-ttu-id="7ec9a-224">строка (в формате GUID)</span><span class="sxs-lookup"><span data-stu-id="7ec9a-224">string (In GUID format)</span></span> |<span data-ttu-id="7ec9a-225">Значение по умолчанию — текущая подписка.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-225">Default value is the current subscription.</span></span> <span data-ttu-id="7ec9a-226">Укажите это значение, если нужно получить ресурс из другой подписки.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-226">Specify this value when you need to retrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="7ec9a-227">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="7ec9a-227">resourceGroupName</span></span> |<span data-ttu-id="7ec9a-228">Нет</span><span class="sxs-lookup"><span data-stu-id="7ec9a-228">No</span></span> |<span data-ttu-id="7ec9a-229">string</span><span class="sxs-lookup"><span data-stu-id="7ec9a-229">string</span></span> |<span data-ttu-id="7ec9a-230">Значение по умолчанию — текущая группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-230">Default value is current resource group.</span></span> <span data-ttu-id="7ec9a-231">Укажите это значение, если нужно получить ресурс из другой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-231">Specify this value when you need to retrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="7ec9a-232">тип_ресурса</span><span class="sxs-lookup"><span data-stu-id="7ec9a-232">resourceType</span></span> |<span data-ttu-id="7ec9a-233">Да</span><span class="sxs-lookup"><span data-stu-id="7ec9a-233">Yes</span></span> |<span data-ttu-id="7ec9a-234">string</span><span class="sxs-lookup"><span data-stu-id="7ec9a-234">string</span></span> |<span data-ttu-id="7ec9a-235">Тип ресурса, включая пространство имен поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="7ec9a-236">имя_ресурса1</span><span class="sxs-lookup"><span data-stu-id="7ec9a-236">resourceName1</span></span> |<span data-ttu-id="7ec9a-237">Да</span><span class="sxs-lookup"><span data-stu-id="7ec9a-237">Yes</span></span> |<span data-ttu-id="7ec9a-238">string</span><span class="sxs-lookup"><span data-stu-id="7ec9a-238">string</span></span> |<span data-ttu-id="7ec9a-239">Имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-239">Name of resource.</span></span> |
| <span data-ttu-id="7ec9a-240">имя_ресурса2</span><span class="sxs-lookup"><span data-stu-id="7ec9a-240">resourceName2</span></span> |<span data-ttu-id="7ec9a-241">Нет</span><span class="sxs-lookup"><span data-stu-id="7ec9a-241">No</span></span> |<span data-ttu-id="7ec9a-242">string</span><span class="sxs-lookup"><span data-stu-id="7ec9a-242">string</span></span> |<span data-ttu-id="7ec9a-243">Имя следующего ресурса, если ресурс является вложенным.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7ec9a-244">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7ec9a-244">Return value</span></span>

<span data-ttu-id="7ec9a-245">Идентификатор возвращается в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-245">The identifier is returned in the following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="7ec9a-246">Примечания</span><span class="sxs-lookup"><span data-stu-id="7ec9a-246">Remarks</span></span>

<span data-ttu-id="7ec9a-247">Указанные значения параметров зависят от того, находится ли ресурс в той же подписке и группе ресурсов, что и текущее развертывание.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-247">The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment.</span></span>

<span data-ttu-id="7ec9a-248">Чтобы получить идентификатор ресурса для учетной записи хранения в одной подписке и группе ресурсов, используйте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-248">To get the resource ID for a storage account in the same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7ec9a-249">Чтобы получить идентификатор ресурса для учетной записи хранения в той же подписке, но другой группе ресурсов, используйте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-249">To get the resource ID for a storage account in the same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7ec9a-250">Чтобы получить идентификатор ресурса для учетной записи хранения в других подписке и группе ресурсов, используйте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-250">To get the resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7ec9a-251">Чтобы получить идентификатор ресурса для базы данных в другой группе ресурсов, используйте команду ниже:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-251">To get the resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="7ec9a-252">Эта функция часто необходима при использовании учетной записи хранения или виртуальной сети в альтернативной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-252">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="7ec9a-253">В следующем примере показано, как ресурс из внешней группы ресурсов можно легко использовать:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-253">The following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="7ec9a-254">Пример</span><span class="sxs-lookup"><span data-stu-id="7ec9a-254">Example</span></span>

<span data-ttu-id="7ec9a-255">Следующий пример возвращает идентификатор ресурса для учетной записи хранения в группе ресурсов:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-255">The following example returns the resource ID for a storage account in the resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="7ec9a-256">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-256">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="7ec9a-257">Имя</span><span class="sxs-lookup"><span data-stu-id="7ec9a-257">Name</span></span> | <span data-ttu-id="7ec9a-258">Тип</span><span class="sxs-lookup"><span data-stu-id="7ec9a-258">Type</span></span> | <span data-ttu-id="7ec9a-259">Значение</span><span class="sxs-lookup"><span data-stu-id="7ec9a-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7ec9a-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="7ec9a-260">sameRGOutput</span></span> | <span data-ttu-id="7ec9a-261">Строка</span><span class="sxs-lookup"><span data-stu-id="7ec9a-261">String</span></span> | <span data-ttu-id="7ec9a-262">/subscriptions/{ИД_текущей_подписки}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7ec9a-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7ec9a-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="7ec9a-263">differentRGOutput</span></span> | <span data-ttu-id="7ec9a-264">Строка</span><span class="sxs-lookup"><span data-stu-id="7ec9a-264">String</span></span> | <span data-ttu-id="7ec9a-265">/subscriptions/{ИД_текущей_подписки}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7ec9a-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7ec9a-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="7ec9a-266">differentSubOutput</span></span> | <span data-ttu-id="7ec9a-267">Строка</span><span class="sxs-lookup"><span data-stu-id="7ec9a-267">String</span></span> | <span data-ttu-id="7ec9a-268">/subscriptions/{ИД_другой_подписки}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7ec9a-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7ec9a-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="7ec9a-269">nestedResourceOutput</span></span> | <span data-ttu-id="7ec9a-270">Строка</span><span class="sxs-lookup"><span data-stu-id="7ec9a-270">String</span></span> | <span data-ttu-id="7ec9a-271">/subscriptions/{ИД_текущей_подписки}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="7ec9a-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="7ec9a-272">Подписка</span><span class="sxs-lookup"><span data-stu-id="7ec9a-272">subscription</span></span>
`subscription()`

<span data-ttu-id="7ec9a-273">Возвращает сведения о подписке для текущего развертывания.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-273">Returns details about the subscription for the current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="7ec9a-274">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7ec9a-274">Return value</span></span>

<span data-ttu-id="7ec9a-275">Функция возвращает значение в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="7ec9a-275">The function returns the following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="7ec9a-276">Пример</span><span class="sxs-lookup"><span data-stu-id="7ec9a-276">Example</span></span>

<span data-ttu-id="7ec9a-277">В следующем примере показана функция subscription, вызываемая в разделе выходных данных.</span><span class="sxs-lookup"><span data-stu-id="7ec9a-277">The following example shows the subscription function called in the outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="7ec9a-278">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ec9a-278">Next steps</span></span>
* <span data-ttu-id="7ec9a-279">Описание разделов в шаблоне Azure Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7ec9a-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7ec9a-280">Инструкции по объединению нескольких шаблонов см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7ec9a-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="7ec9a-281">Указания по выполнению заданного количества циклов итерации при создании типа ресурса см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="7ec9a-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="7ec9a-282">Указания по развертыванию созданного шаблона см. в статье, посвященной [развертыванию приложения с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7ec9a-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

