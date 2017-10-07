---
title: "функции шаблонов диспетчера ресурсов aaaAzure - ресурсы | Документы Microsoft"
description: "Описывает toouse функции hello значения tooretrieve шаблона диспетчера ресурсов Azure о ресурсах."
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
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="7c8e2-103">Функции для работы с ресурсами в шаблонах Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7c8e2-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="7c8e2-104">Диспетчер ресурсов предоставляет следующие функции для получения значений ресурсов hello:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="7c8e2-105">listKeys и list{Value}</span><span class="sxs-lookup"><span data-stu-id="7c8e2-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="7c8e2-106">providers</span><span class="sxs-lookup"><span data-stu-id="7c8e2-106">providers</span></span>](#providers)
* [<span data-ttu-id="7c8e2-107">reference</span><span class="sxs-lookup"><span data-stu-id="7c8e2-107">reference</span></span>](#reference)
* [<span data-ttu-id="7c8e2-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="7c8e2-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="7c8e2-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="7c8e2-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="7c8e2-110">subscription</span><span class="sxs-lookup"><span data-stu-id="7c8e2-110">subscription</span></span>](#subscription)

<span data-ttu-id="7c8e2-111">tooget значения из параметров, переменные или hello текущего развертывания, в разделе [функции развертывания значение](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e2-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="7c8e2-112">listKeys и list{Value}</span><span class="sxs-lookup"><span data-stu-id="7c8e2-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="7c8e2-113">Возвращает hello значения для любого типа ресурсов, которая поддерживает операции вывода списка hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="7c8e2-114">Hello наиболее распространенным вариантом применения является `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="7c8e2-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="7c8e2-115">Parameters</span></span>

| <span data-ttu-id="7c8e2-116">Параметр</span><span class="sxs-lookup"><span data-stu-id="7c8e2-116">Parameter</span></span> | <span data-ttu-id="7c8e2-117">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7c8e2-117">Required</span></span> | <span data-ttu-id="7c8e2-118">Тип</span><span class="sxs-lookup"><span data-stu-id="7c8e2-118">Type</span></span> | <span data-ttu-id="7c8e2-119">Описание</span><span class="sxs-lookup"><span data-stu-id="7c8e2-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7c8e2-120">имя_ресурса или идентификатор_ресурса</span><span class="sxs-lookup"><span data-stu-id="7c8e2-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="7c8e2-121">Да</span><span class="sxs-lookup"><span data-stu-id="7c8e2-121">Yes</span></span> |<span data-ttu-id="7c8e2-122">string</span><span class="sxs-lookup"><span data-stu-id="7c8e2-122">string</span></span> |<span data-ttu-id="7c8e2-123">Уникальный идентификатор для ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="7c8e2-124">версия_API</span><span class="sxs-lookup"><span data-stu-id="7c8e2-124">apiVersion</span></span> |<span data-ttu-id="7c8e2-125">Да</span><span class="sxs-lookup"><span data-stu-id="7c8e2-125">Yes</span></span> |<span data-ttu-id="7c8e2-126">string</span><span class="sxs-lookup"><span data-stu-id="7c8e2-126">string</span></span> |<span data-ttu-id="7c8e2-127">Версия API для состояния среды выполнения ресурса.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-127">API version of resource runtime state.</span></span> <span data-ttu-id="7c8e2-128">Как правило, в формате hello **гггг мм дд**.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7c8e2-129">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7c8e2-129">Return value</span></span>

<span data-ttu-id="7c8e2-130">Hello вернуть объект из listKeys существует hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-130">hello returned object from listKeys has hello following format:</span></span>

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

<span data-ttu-id="7c8e2-131">Другие функции list возвращают данные в других форматах.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-131">Other list functions have different return formats.</span></span> <span data-ttu-id="7c8e2-132">Формат hello toosee функции, включите ее в разделе выходы hello как показано в примере шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="7c8e2-133">Примечания</span><span class="sxs-lookup"><span data-stu-id="7c8e2-133">Remarks</span></span>

<span data-ttu-id="7c8e2-134">Любая операция, которая начинается с **list**, может быть использована в шаблоне как функция.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="7c8e2-135">Hello доступные операции включают не только listKeys, но также операции, такие как `list`, `listAdminKeys`, и `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="7c8e2-136">Однако нельзя использовать **списка** операции, требующие значения в hello текст запроса.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="7c8e2-137">Здравствуйте, например, [список учетных записей SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) операция требует параметров текста запроса, например *signedExpiry*, поэтому его нельзя использовать внутри шаблона.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="7c8e2-138">toodetermine операция списка имеют типы ресурсов, имеются следующие варианты hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="7c8e2-139">Представление hello [операции REST API](/rest/api/) для поставщика ресурсов и найти список операций.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="7c8e2-140">Например, учетные записи хранилища имеют hello [listKeys операции](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="7c8e2-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="7c8e2-141">Используйте hello [Get AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="7c8e2-142">Hello следующий пример возвращает все операции списка учетных записей хранилища:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="7c8e2-143">Используйте следующую команду Azure CLI toofilter только hello операции списка hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="7c8e2-144">Укажите ресурс hello, используя либо hello [функции resourceId](#resourceid), или в формате hello `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="7c8e2-145">Пример</span><span class="sxs-lookup"><span data-stu-id="7c8e2-145">Example</span></span>

<span data-ttu-id="7c8e2-146">Hello следующем примере показано, как tooreturn hello первичный и вторичный ключи из учетной записи хранения в hello выводит раздел.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

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

## <a name="providers"></a><span data-ttu-id="7c8e2-147">providers</span><span class="sxs-lookup"><span data-stu-id="7c8e2-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="7c8e2-148">Возвращает сведения о поставщике ресурсов и поддерживаемых типах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="7c8e2-149">Если тип ресурса не указано, функция hello возвращает все типы hello поддерживается для поставщика ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="7c8e2-150">Параметры</span><span class="sxs-lookup"><span data-stu-id="7c8e2-150">Parameters</span></span>

| <span data-ttu-id="7c8e2-151">Параметр</span><span class="sxs-lookup"><span data-stu-id="7c8e2-151">Parameter</span></span> | <span data-ttu-id="7c8e2-152">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7c8e2-152">Required</span></span> | <span data-ttu-id="7c8e2-153">Тип</span><span class="sxs-lookup"><span data-stu-id="7c8e2-153">Type</span></span> | <span data-ttu-id="7c8e2-154">Описание</span><span class="sxs-lookup"><span data-stu-id="7c8e2-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7c8e2-155">пространство_имен_поставщика</span><span class="sxs-lookup"><span data-stu-id="7c8e2-155">providerNamespace</span></span> |<span data-ttu-id="7c8e2-156">Да</span><span class="sxs-lookup"><span data-stu-id="7c8e2-156">Yes</span></span> |<span data-ttu-id="7c8e2-157">string</span><span class="sxs-lookup"><span data-stu-id="7c8e2-157">string</span></span> |<span data-ttu-id="7c8e2-158">Пространство имен поставщика hello</span><span class="sxs-lookup"><span data-stu-id="7c8e2-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="7c8e2-159">тип_ресурса</span><span class="sxs-lookup"><span data-stu-id="7c8e2-159">resourceType</span></span> |<span data-ttu-id="7c8e2-160">Нет</span><span class="sxs-lookup"><span data-stu-id="7c8e2-160">No</span></span> |<span data-ttu-id="7c8e2-161">string</span><span class="sxs-lookup"><span data-stu-id="7c8e2-161">string</span></span> |<span data-ttu-id="7c8e2-162">Hello тип ресурса в пределах hello указано пространство имен.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7c8e2-163">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7c8e2-163">Return value</span></span>

<span data-ttu-id="7c8e2-164">Каждый поддерживаемый тип возвращается в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="7c8e2-165">Массив упорядочение hello возвращаемые значения не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="7c8e2-166">Пример</span><span class="sxs-lookup"><span data-stu-id="7c8e2-166">Example</span></span>

<span data-ttu-id="7c8e2-167">Hello в следующем примере показано, как toouse hello функция поставщика:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-167">hello following example shows how toouse hello provider function:</span></span>

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

<span data-ttu-id="7c8e2-168">Hello предыдущий пример возвращает объект в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-168">hello preceding example returns an object in hello following format:</span></span>

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

## <a name="reference"></a><span data-ttu-id="7c8e2-169">reference</span><span class="sxs-lookup"><span data-stu-id="7c8e2-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="7c8e2-170">Возвращает объект, представляющий состояние среды выполнения ресурса.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="7c8e2-171">Параметры</span><span class="sxs-lookup"><span data-stu-id="7c8e2-171">Parameters</span></span>

| <span data-ttu-id="7c8e2-172">Параметр</span><span class="sxs-lookup"><span data-stu-id="7c8e2-172">Parameter</span></span> | <span data-ttu-id="7c8e2-173">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7c8e2-173">Required</span></span> | <span data-ttu-id="7c8e2-174">Тип</span><span class="sxs-lookup"><span data-stu-id="7c8e2-174">Type</span></span> | <span data-ttu-id="7c8e2-175">Описание</span><span class="sxs-lookup"><span data-stu-id="7c8e2-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7c8e2-176">имя_ресурса или идентификатор_ресурса</span><span class="sxs-lookup"><span data-stu-id="7c8e2-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="7c8e2-177">Да</span><span class="sxs-lookup"><span data-stu-id="7c8e2-177">Yes</span></span> |<span data-ttu-id="7c8e2-178">string</span><span class="sxs-lookup"><span data-stu-id="7c8e2-178">string</span></span> |<span data-ttu-id="7c8e2-179">Имя или уникальный идентификатор ресурса.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="7c8e2-180">версия_API</span><span class="sxs-lookup"><span data-stu-id="7c8e2-180">apiVersion</span></span> |<span data-ttu-id="7c8e2-181">Нет</span><span class="sxs-lookup"><span data-stu-id="7c8e2-181">No</span></span> |<span data-ttu-id="7c8e2-182">string</span><span class="sxs-lookup"><span data-stu-id="7c8e2-182">string</span></span> |<span data-ttu-id="7c8e2-183">Версии API-интерфейса hello указанный ресурс.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-183">API version of hello specified resource.</span></span> <span data-ttu-id="7c8e2-184">Включите этот параметр, когда ресурс hello не подготовлен в пределах того же шаблона.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="7c8e2-185">Как правило, в формате hello **гггг мм дд**.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7c8e2-186">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7c8e2-186">Return value</span></span>

<span data-ttu-id="7c8e2-187">Каждый тип ресурса возвращает различные параметры для функции hello ссылки.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="7c8e2-188">функция Hello не возвращает предварительно определенного формата.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="7c8e2-189">hello объекта в hello выводит раздела, как показано в примере hello возвращаемое toosee hello свойства для типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="7c8e2-190">Примечания</span><span class="sxs-lookup"><span data-stu-id="7c8e2-190">Remarks</span></span>

<span data-ttu-id="7c8e2-191">ссылка функции Hello значения из состояния среды выполнения и таким образом, не может использоваться в разделе переменные hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="7c8e2-192">Она может использоваться в разделе выходных данных шаблона.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="7c8e2-193">С помощью функции hello ссылку, вы неявно объявляют зависимость одного ресурса на другой ресурс при hello ссылка на ресурс, предоставляется в рамках того же шаблона.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="7c8e2-194">Hello dependsOn tooalso используйте свойство не обязательно.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="7c8e2-195">Hello функции не вычисляется до hello ресурс ссылки на них завершения развертывания.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="7c8e2-196">toosee hello имена и значения свойств для типа ресурса, создать шаблон, который возвращает объект hello в разделе hello выходные данные.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="7c8e2-197">Если у вас есть существующий ресурс этого типа, шаблон возвращает hello объекта без развертывания никаких новых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="7c8e2-198">Как правило, использовать hello **ссылки** функции tooreturn определенное значение из объекта, например hello BLOB-объект URI конечной точки или полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

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

### <a name="example"></a><span data-ttu-id="7c8e2-199">Пример</span><span class="sxs-lookup"><span data-stu-id="7c8e2-199">Example</span></span>

<span data-ttu-id="7c8e2-200">Справочник и toodeploy ресурс hello в hello того же шаблона, используйте:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-200">toodeploy and reference hello resource in hello same template, use:</span></span>

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

<span data-ttu-id="7c8e2-201">Hello предыдущий пример возвращает объект в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-201">hello preceding example returns an object in hello following format:</span></span>

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

<span data-ttu-id="7c8e2-202">Hello следующий пример ссылается на учетную запись хранилища, который не развернут в этом шаблоне.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="7c8e2-203">Hello учетной записи хранения уже существует в пределах hello же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-203">hello storage account already exists within hello same resource group.</span></span>

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

## <a name="resourcegroup"></a><span data-ttu-id="7c8e2-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="7c8e2-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="7c8e2-205">Возвращает объект, представляющий hello текущей группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="7c8e2-206">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7c8e2-206">Return value</span></span>

<span data-ttu-id="7c8e2-207">Hello вернул объект находится в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-207">hello returned object is in hello following format:</span></span>

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

### <a name="remarks"></a><span data-ttu-id="7c8e2-208">Примечания</span><span class="sxs-lookup"><span data-stu-id="7c8e2-208">Remarks</span></span>

<span data-ttu-id="7c8e2-209">Обычно группа ресурсов функции hello используется toocreate ресурсы hello местоположения hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="7c8e2-210">Hello следующий пример использует расположение hello tooassign расположение группы ресурсов hello веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

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

### <a name="example"></a><span data-ttu-id="7c8e2-211">Пример</span><span class="sxs-lookup"><span data-stu-id="7c8e2-211">Example</span></span>

<span data-ttu-id="7c8e2-212">Hello следующий шаблон возвращает hello свойства группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-212">hello following template returns hello properties of hello resource group.</span></span>

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

<span data-ttu-id="7c8e2-213">Hello предыдущий пример возвращает объект в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-213">hello preceding example returns an object in hello following format:</span></span>

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

## <a name="resourceid"></a><span data-ttu-id="7c8e2-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="7c8e2-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="7c8e2-215">Возвращает hello уникальный идентификатор ресурса.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="7c8e2-216">Эта функция используется, когда имя ресурса hello является неоднозначным или не инициализировано внутри hello того же шаблона.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="7c8e2-217">Параметры</span><span class="sxs-lookup"><span data-stu-id="7c8e2-217">Parameters</span></span>

| <span data-ttu-id="7c8e2-218">Параметр</span><span class="sxs-lookup"><span data-stu-id="7c8e2-218">Parameter</span></span> | <span data-ttu-id="7c8e2-219">Обязательно</span><span class="sxs-lookup"><span data-stu-id="7c8e2-219">Required</span></span> | <span data-ttu-id="7c8e2-220">Тип</span><span class="sxs-lookup"><span data-stu-id="7c8e2-220">Type</span></span> | <span data-ttu-id="7c8e2-221">Описание</span><span class="sxs-lookup"><span data-stu-id="7c8e2-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7c8e2-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7c8e2-222">subscriptionId</span></span> |<span data-ttu-id="7c8e2-223">Нет</span><span class="sxs-lookup"><span data-stu-id="7c8e2-223">No</span></span> |<span data-ttu-id="7c8e2-224">строка (в формате GUID)</span><span class="sxs-lookup"><span data-stu-id="7c8e2-224">string (In GUID format)</span></span> |<span data-ttu-id="7c8e2-225">Значение по умолчанию — hello текущей подписки.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-225">Default value is hello current subscription.</span></span> <span data-ttu-id="7c8e2-226">Задайте это значение, когда требуется tooretrieve ресурс в другую подписку.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="7c8e2-227">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="7c8e2-227">resourceGroupName</span></span> |<span data-ttu-id="7c8e2-228">Нет</span><span class="sxs-lookup"><span data-stu-id="7c8e2-228">No</span></span> |<span data-ttu-id="7c8e2-229">string</span><span class="sxs-lookup"><span data-stu-id="7c8e2-229">string</span></span> |<span data-ttu-id="7c8e2-230">Значение по умолчанию — текущая группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-230">Default value is current resource group.</span></span> <span data-ttu-id="7c8e2-231">Задайте это значение, когда требуется tooretrieve ресурсов в другой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="7c8e2-232">тип_ресурса</span><span class="sxs-lookup"><span data-stu-id="7c8e2-232">resourceType</span></span> |<span data-ttu-id="7c8e2-233">Да</span><span class="sxs-lookup"><span data-stu-id="7c8e2-233">Yes</span></span> |<span data-ttu-id="7c8e2-234">string</span><span class="sxs-lookup"><span data-stu-id="7c8e2-234">string</span></span> |<span data-ttu-id="7c8e2-235">Тип ресурса, включая пространство имен поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="7c8e2-236">имя_ресурса1</span><span class="sxs-lookup"><span data-stu-id="7c8e2-236">resourceName1</span></span> |<span data-ttu-id="7c8e2-237">Да</span><span class="sxs-lookup"><span data-stu-id="7c8e2-237">Yes</span></span> |<span data-ttu-id="7c8e2-238">string</span><span class="sxs-lookup"><span data-stu-id="7c8e2-238">string</span></span> |<span data-ttu-id="7c8e2-239">Имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-239">Name of resource.</span></span> |
| <span data-ttu-id="7c8e2-240">имя_ресурса2</span><span class="sxs-lookup"><span data-stu-id="7c8e2-240">resourceName2</span></span> |<span data-ttu-id="7c8e2-241">Нет</span><span class="sxs-lookup"><span data-stu-id="7c8e2-241">No</span></span> |<span data-ttu-id="7c8e2-242">string</span><span class="sxs-lookup"><span data-stu-id="7c8e2-242">string</span></span> |<span data-ttu-id="7c8e2-243">Имя следующего ресурса, если ресурс является вложенным.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="7c8e2-244">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7c8e2-244">Return value</span></span>

<span data-ttu-id="7c8e2-245">возвращается идентификатор Hello в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="7c8e2-246">Примечания</span><span class="sxs-lookup"><span data-stu-id="7c8e2-246">Remarks</span></span>

<span data-ttu-id="7c8e2-247">Hello указать значения параметров зависят от того, является ли ресурс hello в hello же группу ресурса и подписки, что текущее развертывание hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="7c8e2-248">Идентификатор ресурса hello tooget учетной записи на hello же подписке и группе ресурсов, используйте:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7c8e2-249">Идентификатор ресурса hello tooget для учетной записи хранения в hello ту же подписку, но другой группе ресурсов, используйте:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7c8e2-250">Используйте идентификатор ресурса hello tooget для учетной записи хранения в другой подписке и группе ресурсов:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="7c8e2-251">Идентификатор ресурса hello tooget базы данных в другой группе ресурсов, используйте:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="7c8e2-252">Часто требуется toouse эту функцию при использовании учетной записи хранилища или виртуальной сети в группе ресурсов альтернативный.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="7c8e2-253">Hello следующем примере показано, как ресурс из группы внешних ресурсов можно легко использовать:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

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

### <a name="example"></a><span data-ttu-id="7c8e2-254">Пример</span><span class="sxs-lookup"><span data-stu-id="7c8e2-254">Example</span></span>

<span data-ttu-id="7c8e2-255">Hello следующий пример возвращает идентификатор ресурса hello для учетной записи хранилища в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

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

<span data-ttu-id="7c8e2-256">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="7c8e2-257">Имя</span><span class="sxs-lookup"><span data-stu-id="7c8e2-257">Name</span></span> | <span data-ttu-id="7c8e2-258">Тип</span><span class="sxs-lookup"><span data-stu-id="7c8e2-258">Type</span></span> | <span data-ttu-id="7c8e2-259">Значение</span><span class="sxs-lookup"><span data-stu-id="7c8e2-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="7c8e2-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="7c8e2-260">sameRGOutput</span></span> | <span data-ttu-id="7c8e2-261">Строка</span><span class="sxs-lookup"><span data-stu-id="7c8e2-261">String</span></span> | <span data-ttu-id="7c8e2-262">/subscriptions/{ИД_текущей_подписки}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7c8e2-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7c8e2-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="7c8e2-263">differentRGOutput</span></span> | <span data-ttu-id="7c8e2-264">Строка</span><span class="sxs-lookup"><span data-stu-id="7c8e2-264">String</span></span> | <span data-ttu-id="7c8e2-265">/subscriptions/{ИД_текущей_подписки}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7c8e2-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7c8e2-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="7c8e2-266">differentSubOutput</span></span> | <span data-ttu-id="7c8e2-267">Строка</span><span class="sxs-lookup"><span data-stu-id="7c8e2-267">String</span></span> | <span data-ttu-id="7c8e2-268">/subscriptions/{ИД_другой_подписки}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="7c8e2-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="7c8e2-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="7c8e2-269">nestedResourceOutput</span></span> | <span data-ttu-id="7c8e2-270">Строка</span><span class="sxs-lookup"><span data-stu-id="7c8e2-270">String</span></span> | <span data-ttu-id="7c8e2-271">/subscriptions/{ИД_текущей_подписки}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="7c8e2-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="7c8e2-272">Подписка</span><span class="sxs-lookup"><span data-stu-id="7c8e2-272">subscription</span></span>
`subscription()`

<span data-ttu-id="7c8e2-273">Возвращает сведения о подписке hello для текущего развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="7c8e2-274">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7c8e2-274">Return value</span></span>

<span data-ttu-id="7c8e2-275">функция Hello возвращает hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="7c8e2-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="7c8e2-276">Пример</span><span class="sxs-lookup"><span data-stu-id="7c8e2-276">Example</span></span>

<span data-ttu-id="7c8e2-277">Hello пример hello подписки функцию с именем раздела hello выходные данные.</span><span class="sxs-lookup"><span data-stu-id="7c8e2-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="7c8e2-278">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c8e2-278">Next steps</span></span>
* <span data-ttu-id="7c8e2-279">Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e2-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7c8e2-280">toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e2-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="7c8e2-281">tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e2-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="7c8e2-282">toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7c8e2-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

