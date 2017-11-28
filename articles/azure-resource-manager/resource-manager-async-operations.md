---
title: "Асинхронные операции Azure | Документация Майкрософт"
description: "Описание действий по отслеживанию асинхронных операций в Azure."
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
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 9fe3d98cd345aae45722295b6c1b7fc3e9036e95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="3ab57-103">Отслеживание асинхронных операций Azure</span><span class="sxs-lookup"><span data-stu-id="3ab57-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="3ab57-104">Некоторые операции REST выполняются в Azure асинхронно, поскольку не могут быть быстро завершены.</span><span class="sxs-lookup"><span data-stu-id="3ab57-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span></span> <span data-ttu-id="3ab57-105">Из этой статьи вы узнаете, как отслеживать состояние асинхронных операций, используя возвращаемые в ответе значения.</span><span class="sxs-lookup"><span data-stu-id="3ab57-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="3ab57-106">Коды состояния для асинхронных операций</span><span class="sxs-lookup"><span data-stu-id="3ab57-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="3ab57-107">Изначально асинхронная операция возвращает один из следующих кодов состояния HTTP:</span><span class="sxs-lookup"><span data-stu-id="3ab57-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="3ab57-108">201 Created (создано);</span><span class="sxs-lookup"><span data-stu-id="3ab57-108">201 (Created)</span></span>
* <span data-ttu-id="3ab57-109">202 Accepted (принято).</span><span class="sxs-lookup"><span data-stu-id="3ab57-109">202 (Accepted)</span></span> 

<span data-ttu-id="3ab57-110">После успешного завершения операции возвращаются следующие коды:</span><span class="sxs-lookup"><span data-stu-id="3ab57-110">When the operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="3ab57-111">200 OK;</span><span class="sxs-lookup"><span data-stu-id="3ab57-111">200 (OK)</span></span>
* <span data-ttu-id="3ab57-112">204 No Content (нет содержимого).</span><span class="sxs-lookup"><span data-stu-id="3ab57-112">204 (No Content)</span></span> 

<span data-ttu-id="3ab57-113">Ответы по выполняемой операции описаны в [документации по REST API](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="3ab57-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="3ab57-114">Отслеживание состояния операции</span><span class="sxs-lookup"><span data-stu-id="3ab57-114">Monitor status of operation</span></span>
<span data-ttu-id="3ab57-115">Асинхронные операции REST возвращают в заголовке некоторые значения, с помощью которых можно контролировать состояние операции.</span><span class="sxs-lookup"><span data-stu-id="3ab57-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span></span> <span data-ttu-id="3ab57-116">Нужно проверять наличие в заголовке следующих трех значений:</span><span class="sxs-lookup"><span data-stu-id="3ab57-116">There are potentially three header values to examine:</span></span>

* <span data-ttu-id="3ab57-117">`Azure-AsyncOperation` — это URL-адрес для проверки текущего состояния операции.</span><span class="sxs-lookup"><span data-stu-id="3ab57-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span></span> <span data-ttu-id="3ab57-118">Если операция возвращает такое значение, для отслеживания состояния операции всегда используйте именно его, а не значение Location.</span><span class="sxs-lookup"><span data-stu-id="3ab57-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span></span>
* <span data-ttu-id="3ab57-119">`Location` — это URL-адрес для определения момента завершения операции.</span><span class="sxs-lookup"><span data-stu-id="3ab57-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="3ab57-120">Используйте это значение только в том случае, если отсутствует значение Azure-AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="3ab57-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="3ab57-121">`Retry-After` — это количество секунд ожидания перед проверкой состояния асинхронной операции.</span><span class="sxs-lookup"><span data-stu-id="3ab57-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span></span>

<span data-ttu-id="3ab57-122">Не каждая асинхронная операция возвращает все эти значения.</span><span class="sxs-lookup"><span data-stu-id="3ab57-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="3ab57-123">Например, для некоторых операций нужно учитывать значение заголовка Azure-AsyncOperation, а для других — значение заголовка Location.</span><span class="sxs-lookup"><span data-stu-id="3ab57-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span></span> 

<span data-ttu-id="3ab57-124">Значения этих заголовков вы можете получить так же, как и любых других заголовков запроса.</span><span class="sxs-lookup"><span data-stu-id="3ab57-124">You retrieve the header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="3ab57-125">Например, приведенный ниже код C# извлекает значение заголовка из объекта `HttpWebResponse` с именем `response`.</span><span class="sxs-lookup"><span data-stu-id="3ab57-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="3ab57-126">Запрос и ответ с использованием Azure-AsyncOperation</span><span class="sxs-lookup"><span data-stu-id="3ab57-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="3ab57-127">Чтобы получить состояние асинхронной операции, отправьте запрос GET на URL-адрес, указанный в заголовке Azure-AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="3ab57-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="3ab57-128">Текст ответа, полученного от операции, будет содержать сведения о ее выполнении.</span><span class="sxs-lookup"><span data-stu-id="3ab57-128">The body of the response from this operation contains information about the operation.</span></span> <span data-ttu-id="3ab57-129">В примере ниже показаны возможные значения, возвращаемые операцией.</span><span class="sxs-lookup"><span data-stu-id="3ab57-129">The following example shows the possible values returned from the operation:</span></span>

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

<span data-ttu-id="3ab57-130">Только `status` будет присутствовать во всех ответах.</span><span class="sxs-lookup"><span data-stu-id="3ab57-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="3ab57-131">Объект error возвращается в том случае, если операция находится в состоянии сбоя (Failed) или отмены (Canceled).</span><span class="sxs-lookup"><span data-stu-id="3ab57-131">The error object is returned when the status is Failed or Canceled.</span></span> <span data-ttu-id="3ab57-132">Все остальные значения являются необязательными, поэтому полученный ответ может существенно отличаться от этого примера.</span><span class="sxs-lookup"><span data-stu-id="3ab57-132">All other values are optional; therefore, the response you receive may look different than the example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="3ab57-133">Значения provisioningState</span><span class="sxs-lookup"><span data-stu-id="3ab57-133">provisioningState values</span></span>

<span data-ttu-id="3ab57-134">Операции, которые создают, обновляют или удаляют ресурсы (PUT, PATCH, DELETE), обычно возвращают значение `provisioningState`.</span><span class="sxs-lookup"><span data-stu-id="3ab57-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="3ab57-135">После завершения операции возвращается одно из следующих трех значений:</span><span class="sxs-lookup"><span data-stu-id="3ab57-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="3ab57-136">Успешно</span><span class="sxs-lookup"><span data-stu-id="3ab57-136">Succeeded</span></span>
* <span data-ttu-id="3ab57-137">Сбой</span><span class="sxs-lookup"><span data-stu-id="3ab57-137">Failed</span></span>
* <span data-ttu-id="3ab57-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="3ab57-138">Canceled</span></span>

<span data-ttu-id="3ab57-139">Любое другое значение означает, что операция еще выполняется.</span><span class="sxs-lookup"><span data-stu-id="3ab57-139">All other values indicate the operation is still running.</span></span> <span data-ttu-id="3ab57-140">Поставщик ресурсов может возвращать настраиваемое значение, указывающее его состояние.</span><span class="sxs-lookup"><span data-stu-id="3ab57-140">The resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="3ab57-141">Например, значение **Accepted** (Принято) может сигнализировать о том, что запрос успешно получен и выполняется.</span><span class="sxs-lookup"><span data-stu-id="3ab57-141">For example, you may receive **Accepted** when the request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="3ab57-142">Примеры запросов и ответов</span><span class="sxs-lookup"><span data-stu-id="3ab57-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="3ab57-143">Запуск виртуальной машины (код 202, значение Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="3ab57-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="3ab57-144">Здесь показано, как можно проверить состояние операции **Start** для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="3ab57-144">This example shows how to determine the status of **start** operation for virtual machines.</span></span> <span data-ttu-id="3ab57-145">Исходный запрос имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="3ab57-145">The initial request is in the following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="3ab57-146">В ответ получен код состояния 202.</span><span class="sxs-lookup"><span data-stu-id="3ab57-146">It returns status code 202.</span></span> <span data-ttu-id="3ab57-147">Среди полученных в заголовке значений есть такое:</span><span class="sxs-lookup"><span data-stu-id="3ab57-147">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="3ab57-148">Чтобы проверить состояние асинхронной операции, отправьте запрос на полученный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3ab57-148">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="3ab57-149">Текст ответа содержит состояние операции:</span><span class="sxs-lookup"><span data-stu-id="3ab57-149">The response body contains the status of the operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="3ab57-150">Развертывание ресурсов (код 201, значение Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="3ab57-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="3ab57-151">Здесь показано, как можно проверить состояние операции **deployments** для развертывания ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="3ab57-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span></span> <span data-ttu-id="3ab57-152">Исходный запрос имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="3ab57-152">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="3ab57-153">В ответ получен код состояния 201.</span><span class="sxs-lookup"><span data-stu-id="3ab57-153">It returns status code 201.</span></span> <span data-ttu-id="3ab57-154">Текст ответа включает следующие данные:</span><span class="sxs-lookup"><span data-stu-id="3ab57-154">The body of the response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="3ab57-155">Среди полученных в заголовке значений есть такое:</span><span class="sxs-lookup"><span data-stu-id="3ab57-155">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="3ab57-156">Чтобы проверить состояние асинхронной операции, отправьте запрос на полученный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3ab57-156">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="3ab57-157">Текст ответа содержит состояние операции:</span><span class="sxs-lookup"><span data-stu-id="3ab57-157">The response body contains the status of the operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="3ab57-158">После завершения развертывания возвращается ответ с такими данными:</span><span class="sxs-lookup"><span data-stu-id="3ab57-158">When the deployment is finished, the response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="3ab57-159">Создание учетной записи хранения (код 202, значения Location и Retry-After)</span><span class="sxs-lookup"><span data-stu-id="3ab57-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="3ab57-160">Здесь показано, как можно проверить состояние операции **create** для учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="3ab57-160">This example shows how to determine the status of the **create** operation for storage accounts.</span></span> <span data-ttu-id="3ab57-161">Исходный запрос имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="3ab57-161">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="3ab57-162">Кроме того, текст запроса содержит свойства учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="3ab57-162">And the request body contains properties for the storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="3ab57-163">В ответ получен код состояния 202.</span><span class="sxs-lookup"><span data-stu-id="3ab57-163">It returns status code 202.</span></span> <span data-ttu-id="3ab57-164">Среди полученных в заголовке значений есть такие:</span><span class="sxs-lookup"><span data-stu-id="3ab57-164">Among the header values, you see the following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="3ab57-165">Подождав указанное в значении Retry-After количество секунд, проверьте состояние асинхронной операции посредством отправки еще одного запроса на указанный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3ab57-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="3ab57-166">Если запрос все еще выполняется, вы получите код состояния 202.</span><span class="sxs-lookup"><span data-stu-id="3ab57-166">If the request is still running, you receive a status code 202.</span></span> <span data-ttu-id="3ab57-167">Если запрос завершен, вы получите код состояния 200, а в тексте ответа будут указаны свойства созданной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3ab57-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ab57-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ab57-168">Next steps</span></span>

* <span data-ttu-id="3ab57-169">Документацию по каждой операции REST см. в [справочнике по REST API](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="3ab57-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="3ab57-170">Сведения об управлении ресурсами с помощью REST API в Resource Manager см. [здесь](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="3ab57-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="3ab57-171">Сведения о развертывании шаблонов с помощью REST API в Resource Manager см. в статье [Развертывание ресурсов с использованием шаблонов и REST API Resource Manager](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="3ab57-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>