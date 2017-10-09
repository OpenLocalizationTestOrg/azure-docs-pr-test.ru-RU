---
title: "асинхронные операции aaaAzure | Документы Microsoft"
description: "Описывает способ tootrack асинхронных операций в Azure."
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
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="8b362-103">Отслеживание асинхронных операций Azure</span><span class="sxs-lookup"><span data-stu-id="8b362-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="8b362-104">Некоторые операции Azure REST выполняются асинхронно, так как быстро невозможно выполнить операцию hello.</span><span class="sxs-lookup"><span data-stu-id="8b362-104">Some Azure REST operations run asynchronously because hello operation cannot be completed quickly.</span></span> <span data-ttu-id="8b362-105">В этом разделе описывается, как tootrack hello состояние асинхронной операции с помощью значения возвращаются в ответе hello.</span><span class="sxs-lookup"><span data-stu-id="8b362-105">This topic describes how tootrack hello status of asynchronous operations through values returned in hello response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="8b362-106">Коды состояния для асинхронных операций</span><span class="sxs-lookup"><span data-stu-id="8b362-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="8b362-107">Изначально асинхронная операция возвращает один из следующих кодов состояния HTTP:</span><span class="sxs-lookup"><span data-stu-id="8b362-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="8b362-108">201 Created (создано);</span><span class="sxs-lookup"><span data-stu-id="8b362-108">201 (Created)</span></span>
* <span data-ttu-id="8b362-109">202 Accepted (принято).</span><span class="sxs-lookup"><span data-stu-id="8b362-109">202 (Accepted)</span></span> 

<span data-ttu-id="8b362-110">После успешного завершения операции hello возвращает либо:</span><span class="sxs-lookup"><span data-stu-id="8b362-110">When hello operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="8b362-111">200 OK;</span><span class="sxs-lookup"><span data-stu-id="8b362-111">200 (OK)</span></span>
* <span data-ttu-id="8b362-112">204 No Content (нет содержимого).</span><span class="sxs-lookup"><span data-stu-id="8b362-112">204 (No Content)</span></span> 

<span data-ttu-id="8b362-113">См. toohello [документация по REST API](/rest/api/) toosee hello ответы для выполнении операции hello.</span><span class="sxs-lookup"><span data-stu-id="8b362-113">Refer toohello [REST API documentation](/rest/api/) toosee hello responses for hello operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="8b362-114">Отслеживание состояния операции</span><span class="sxs-lookup"><span data-stu-id="8b362-114">Monitor status of operation</span></span>
<span data-ttu-id="8b362-115">Hello асинхронные REST операций заголовок возврата значений, которые использовать состояние toodetermine hello hello операции.</span><span class="sxs-lookup"><span data-stu-id="8b362-115">hello asynchronous REST operations return header values, which you use toodetermine hello status of hello operation.</span></span> <span data-ttu-id="8b362-116">Существует потенциально tooexamine заголовок три значения:</span><span class="sxs-lookup"><span data-stu-id="8b362-116">There are potentially three header values tooexamine:</span></span>

* <span data-ttu-id="8b362-117">`Azure-AsyncOperation`-URL-адрес для проверки текущего состояния операции hello hello.</span><span class="sxs-lookup"><span data-stu-id="8b362-117">`Azure-AsyncOperation` - URL for checking hello ongoing status of hello operation.</span></span> <span data-ttu-id="8b362-118">Если операция возвращает это значение, всегда используйте ИТ (а не местоположение) tootrack hello состояние операции hello.</span><span class="sxs-lookup"><span data-stu-id="8b362-118">If your operation returns this value, always use it (instead of Location) tootrack hello status of hello operation.</span></span>
* <span data-ttu-id="8b362-119">`Location` — это URL-адрес для определения момента завершения операции.</span><span class="sxs-lookup"><span data-stu-id="8b362-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="8b362-120">Используйте это значение только в том случае, если отсутствует значение Azure-AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="8b362-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="8b362-121">`Retry-After`-hello число toowait секунд перед проверкой hello состояние асинхронной операции hello.</span><span class="sxs-lookup"><span data-stu-id="8b362-121">`Retry-After` - hello number of seconds toowait before checking hello status of hello asynchronous operation.</span></span>

<span data-ttu-id="8b362-122">Не каждая асинхронная операция возвращает все эти значения.</span><span class="sxs-lookup"><span data-stu-id="8b362-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="8b362-123">Например может потребоваться значение заголовка tooevaluate hello асинхронных операций Azure для одной операции, а значение заголовка расположения hello для другой операции.</span><span class="sxs-lookup"><span data-stu-id="8b362-123">For example, you may need tooevaluate hello Azure-AsyncOperation header value for one operation, and hello Location header value for another operation.</span></span> 

<span data-ttu-id="8b362-124">Получить значения заголовка hello, как бы получить любое значение заголовка запроса.</span><span class="sxs-lookup"><span data-stu-id="8b362-124">You retrieve hello header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="8b362-125">Например, в C# можно извлечь значение заголовка hello из `HttpWebResponse` объект с именем `response` с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="8b362-125">For example, in C#, you retrieve hello header value from an `HttpWebResponse` object named `response` with hello following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="8b362-126">Запрос и ответ с использованием Azure-AsyncOperation</span><span class="sxs-lookup"><span data-stu-id="8b362-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="8b362-127">состояние hello tooget hello асинхронной операции, отправлять запрос GET toohello URL-адрес в заголовке асинхронных операций Azure.</span><span class="sxs-lookup"><span data-stu-id="8b362-127">tooget hello status of hello asynchronous operation, send a GET request toohello URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="8b362-128">текст Hello hello ответа от этой операции содержит сведения об операции hello.</span><span class="sxs-lookup"><span data-stu-id="8b362-128">hello body of hello response from this operation contains information about hello operation.</span></span> <span data-ttu-id="8b362-129">Hello ниже приведен пример hello возможные значения возвращаются из операции hello.</span><span class="sxs-lookup"><span data-stu-id="8b362-129">hello following example shows hello possible values returned from hello operation:</span></span>

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

<span data-ttu-id="8b362-130">Только `status` будет присутствовать во всех ответах.</span><span class="sxs-lookup"><span data-stu-id="8b362-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="8b362-131">Hello объекта error возвращается в том случае, если состояние hello сбой или отменено.</span><span class="sxs-lookup"><span data-stu-id="8b362-131">hello error object is returned when hello status is Failed or Canceled.</span></span> <span data-ttu-id="8b362-132">Все остальные значения являются необязательными; Таким образом может выглядеть иначе, чем hello пример hello ответ, полученный.</span><span class="sxs-lookup"><span data-stu-id="8b362-132">All other values are optional; therefore, hello response you receive may look different than hello example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="8b362-133">Значения provisioningState</span><span class="sxs-lookup"><span data-stu-id="8b362-133">provisioningState values</span></span>

<span data-ttu-id="8b362-134">Операции, которые создают, обновляют или удаляют ресурсы (PUT, PATCH, DELETE), обычно возвращают значение `provisioningState`.</span><span class="sxs-lookup"><span data-stu-id="8b362-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="8b362-135">После завершения операции возвращается одно из следующих трех значений:</span><span class="sxs-lookup"><span data-stu-id="8b362-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="8b362-136">Успешно</span><span class="sxs-lookup"><span data-stu-id="8b362-136">Succeeded</span></span>
* <span data-ttu-id="8b362-137">Сбой</span><span class="sxs-lookup"><span data-stu-id="8b362-137">Failed</span></span>
* <span data-ttu-id="8b362-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="8b362-138">Canceled</span></span>

<span data-ttu-id="8b362-139">Все другие значения указывают, что по-прежнему выполняется операция hello.</span><span class="sxs-lookup"><span data-stu-id="8b362-139">All other values indicate hello operation is still running.</span></span> <span data-ttu-id="8b362-140">поставщик ресурсов Hello может возвращать настраиваемые значение, указывающее, его состояние.</span><span class="sxs-lookup"><span data-stu-id="8b362-140">hello resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="8b362-141">Например, может появиться **принято** при hello запрос получен и запущена.</span><span class="sxs-lookup"><span data-stu-id="8b362-141">For example, you may receive **Accepted** when hello request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="8b362-142">Примеры запросов и ответов</span><span class="sxs-lookup"><span data-stu-id="8b362-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="8b362-143">Запуск виртуальной машины (код 202, значение Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="8b362-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="8b362-144">В этом примере показано, как toodetermine hello состояние **запустить** операции для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8b362-144">This example shows how toodetermine hello status of **start** operation for virtual machines.</span></span> <span data-ttu-id="8b362-145">первоначальный запрос Hello имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="8b362-145">hello initial request is in hello following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="8b362-146">В ответ получен код состояния 202.</span><span class="sxs-lookup"><span data-stu-id="8b362-146">It returns status code 202.</span></span> <span data-ttu-id="8b362-147">Среди значений заголовка hello см.</span><span class="sxs-lookup"><span data-stu-id="8b362-147">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="8b362-148">состояние hello toocheck hello асинхронной операции отправки другой URL-адрес запроса toothat.</span><span class="sxs-lookup"><span data-stu-id="8b362-148">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="8b362-149">Hello текст ответа содержит состояние hello hello операции:</span><span class="sxs-lookup"><span data-stu-id="8b362-149">hello response body contains hello status of hello operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="8b362-150">Развертывание ресурсов (код 201, значение Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="8b362-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="8b362-151">В этом примере показано, как toodetermine hello состояние **развертываний** операция развертывания ресурсов tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8b362-151">This example shows how toodetermine hello status of **deployments** operation for deploying resources tooAzure.</span></span> <span data-ttu-id="8b362-152">первоначальный запрос Hello имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="8b362-152">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="8b362-153">В ответ получен код состояния 201.</span><span class="sxs-lookup"><span data-stu-id="8b362-153">It returns status code 201.</span></span> <span data-ttu-id="8b362-154">текст Hello hello ответа включает:</span><span class="sxs-lookup"><span data-stu-id="8b362-154">hello body of hello response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="8b362-155">Среди значений заголовка hello см.</span><span class="sxs-lookup"><span data-stu-id="8b362-155">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="8b362-156">состояние hello toocheck hello асинхронной операции отправки другой URL-адрес запроса toothat.</span><span class="sxs-lookup"><span data-stu-id="8b362-156">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="8b362-157">Hello текст ответа содержит состояние hello hello операции:</span><span class="sxs-lookup"><span data-stu-id="8b362-157">hello response body contains hello status of hello operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="8b362-158">После завершения развертывания hello hello ответ содержит:</span><span class="sxs-lookup"><span data-stu-id="8b362-158">When hello deployment is finished, hello response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="8b362-159">Создание учетной записи хранения (код 202, значения Location и Retry-After)</span><span class="sxs-lookup"><span data-stu-id="8b362-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="8b362-160">В этом примере показано, как toodetermine hello состояние hello **создания** операции для учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="8b362-160">This example shows how toodetermine hello status of hello **create** operation for storage accounts.</span></span> <span data-ttu-id="8b362-161">первоначальный запрос Hello имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="8b362-161">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="8b362-162">И текст hello запроса содержит свойства для учетной записи хранения hello:</span><span class="sxs-lookup"><span data-stu-id="8b362-162">And hello request body contains properties for hello storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="8b362-163">В ответ получен код состояния 202.</span><span class="sxs-lookup"><span data-stu-id="8b362-163">It returns status code 202.</span></span> <span data-ttu-id="8b362-164">Среди значений заголовка hello можно увидеть hello, следующие два значения:</span><span class="sxs-lookup"><span data-stu-id="8b362-164">Among hello header values, you see hello following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="8b362-165">После ожидания в течение число секунд, указанное в Retry-After, проверьте состояние hello hello асинхронной операции, отправляя другой URL-адрес запроса toothat.</span><span class="sxs-lookup"><span data-stu-id="8b362-165">After waiting for number of seconds specified in Retry-After, check hello status of hello asynchronous operation by sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="8b362-166">Если запрос hello по-прежнему запущен, вы получите код состояния 202.</span><span class="sxs-lookup"><span data-stu-id="8b362-166">If hello request is still running, you receive a status code 202.</span></span> <span data-ttu-id="8b362-167">Если запрос hello завершен, ваш получать код состояния 200 и текст hello hello ответа содержит свойства hello hello учетной записи хранилища, который был создан.</span><span class="sxs-lookup"><span data-stu-id="8b362-167">If hello request has completed, your receive a status code 200, and hello body of hello response contains hello properties of hello storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b362-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b362-168">Next steps</span></span>

* <span data-ttu-id="8b362-169">Документацию по каждой операции REST см. в [справочнике по REST API](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="8b362-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="8b362-170">Сведения об управлении ресурсами через hello REST API диспетчера ресурсов см. в разделе [hello с помощью REST API диспетчера ресурсов](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="8b362-170">For information about managing resources through hello Resource Manager REST API, see [Using hello Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="8b362-171">сведения о развертывании шаблонов через hello REST API диспетчера ресурсов см. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и REST API диспетчера ресурсов](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="8b362-171">for information about deploying templates through hello Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>
