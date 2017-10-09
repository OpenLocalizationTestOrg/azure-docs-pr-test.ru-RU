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
# <a name="track-asynchronous-azure-operations"></a>Отслеживание асинхронных операций Azure
Некоторые операции Azure REST выполняются асинхронно, так как быстро невозможно выполнить операцию hello. В этом разделе описывается, как tootrack hello состояние асинхронной операции с помощью значения возвращаются в ответе hello.  

## <a name="status-codes-for-asynchronous-operations"></a>Коды состояния для асинхронных операций
Изначально асинхронная операция возвращает один из следующих кодов состояния HTTP:

* 201 Created (создано);
* 202 Accepted (принято). 

После успешного завершения операции hello возвращает либо:

* 200 OK;
* 204 No Content (нет содержимого). 

См. toohello [документация по REST API](/rest/api/) toosee hello ответы для выполнении операции hello. 

## <a name="monitor-status-of-operation"></a>Отслеживание состояния операции
Hello асинхронные REST операций заголовок возврата значений, которые использовать состояние toodetermine hello hello операции. Существует потенциально tooexamine заголовок три значения:

* `Azure-AsyncOperation`-URL-адрес для проверки текущего состояния операции hello hello. Если операция возвращает это значение, всегда используйте ИТ (а не местоположение) tootrack hello состояние операции hello.
* `Location` — это URL-адрес для определения момента завершения операции. Используйте это значение только в том случае, если отсутствует значение Azure-AsyncOperation.
* `Retry-After`-hello число toowait секунд перед проверкой hello состояние асинхронной операции hello.

Не каждая асинхронная операция возвращает все эти значения. Например может потребоваться значение заголовка tooevaluate hello асинхронных операций Azure для одной операции, а значение заголовка расположения hello для другой операции. 

Получить значения заголовка hello, как бы получить любое значение заголовка запроса. Например, в C# можно извлечь значение заголовка hello из `HttpWebResponse` объект с именем `response` с hello, следующий код:

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Запрос и ответ с использованием Azure-AsyncOperation

состояние hello tooget hello асинхронной операции, отправлять запрос GET toohello URL-адрес в заголовке асинхронных операций Azure.

текст Hello hello ответа от этой операции содержит сведения об операции hello. Hello ниже приведен пример hello возможные значения возвращаются из операции hello.

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

Только `status` будет присутствовать во всех ответах. Hello объекта error возвращается в том случае, если состояние hello сбой или отменено. Все остальные значения являются необязательными; Таким образом может выглядеть иначе, чем hello пример hello ответ, полученный.

## <a name="provisioningstate-values"></a>Значения provisioningState

Операции, которые создают, обновляют или удаляют ресурсы (PUT, PATCH, DELETE), обычно возвращают значение `provisioningState`. После завершения операции возвращается одно из следующих трех значений: 

* Успешно
* Сбой
* Canceled

Все другие значения указывают, что по-прежнему выполняется операция hello. поставщик ресурсов Hello может возвращать настраиваемые значение, указывающее, его состояние. Например, может появиться **принято** при hello запрос получен и запущена.

## <a name="example-requests-and-responses"></a>Примеры запросов и ответов

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>Запуск виртуальной машины (код 202, значение Azure-AsyncOperation)
В этом примере показано, как toodetermine hello состояние **запустить** операции для виртуальных машин. первоначальный запрос Hello имеет hello следующий формат:

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

В ответ получен код состояния 202. Среди значений заголовка hello см.

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

состояние hello toocheck hello асинхронной операции отправки другой URL-адрес запроса toothat.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

Hello текст ответа содержит состояние hello hello операции:

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>Развертывание ресурсов (код 201, значение Azure-AsyncOperation)

В этом примере показано, как toodetermine hello состояние **развертываний** операция развертывания ресурсов tooAzure. первоначальный запрос Hello имеет hello следующий формат:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

В ответ получен код состояния 201. текст Hello hello ответа включает:

```json
"provisioningState":"Accepted",
```

Среди значений заголовка hello см.

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

состояние hello toocheck hello асинхронной операции отправки другой URL-адрес запроса toothat.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

Hello текст ответа содержит состояние hello hello операции:

```json
{"status":"Running"}
```

После завершения развертывания hello hello ответ содержит:

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>Создание учетной записи хранения (код 202, значения Location и Retry-After)

В этом примере показано, как toodetermine hello состояние hello **создания** операции для учетных записей хранения. первоначальный запрос Hello имеет hello следующий формат:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

И текст hello запроса содержит свойства для учетной записи хранения hello:

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

В ответ получен код состояния 202. Среди значений заголовка hello можно увидеть hello, следующие два значения:

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

После ожидания в течение число секунд, указанное в Retry-After, проверьте состояние hello hello асинхронной операции, отправляя другой URL-адрес запроса toothat.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

Если запрос hello по-прежнему запущен, вы получите код состояния 202. Если запрос hello завершен, ваш получать код состояния 200 и текст hello hello ответа содержит свойства hello hello учетной записи хранилища, который был создан.

## <a name="next-steps"></a>Дальнейшие действия

* Документацию по каждой операции REST см. в [справочнике по REST API](/rest/api/).
* Сведения об управлении ресурсами через hello REST API диспетчера ресурсов см. в разделе [hello с помощью REST API диспетчера ресурсов](resource-manager-rest-api.md).
* сведения о развертывании шаблонов через hello REST API диспетчера ресурсов см. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и REST API диспетчера ресурсов](resource-group-template-deploy-rest.md).
