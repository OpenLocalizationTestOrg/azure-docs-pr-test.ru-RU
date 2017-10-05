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
# <a name="track-asynchronous-azure-operations"></a>Отслеживание асинхронных операций Azure
Некоторые операции REST выполняются в Azure асинхронно, поскольку не могут быть быстро завершены. Из этой статьи вы узнаете, как отслеживать состояние асинхронных операций, используя возвращаемые в ответе значения.  

## <a name="status-codes-for-asynchronous-operations"></a>Коды состояния для асинхронных операций
Изначально асинхронная операция возвращает один из следующих кодов состояния HTTP:

* 201 Created (создано);
* 202 Accepted (принято). 

После успешного завершения операции возвращаются следующие коды:

* 200 OK;
* 204 No Content (нет содержимого). 

Ответы по выполняемой операции описаны в [документации по REST API](/rest/api/). 

## <a name="monitor-status-of-operation"></a>Отслеживание состояния операции
Асинхронные операции REST возвращают в заголовке некоторые значения, с помощью которых можно контролировать состояние операции. Нужно проверять наличие в заголовке следующих трех значений:

* `Azure-AsyncOperation` — это URL-адрес для проверки текущего состояния операции. Если операция возвращает такое значение, для отслеживания состояния операции всегда используйте именно его, а не значение Location.
* `Location` — это URL-адрес для определения момента завершения операции. Используйте это значение только в том случае, если отсутствует значение Azure-AsyncOperation.
* `Retry-After` — это количество секунд ожидания перед проверкой состояния асинхронной операции.

Не каждая асинхронная операция возвращает все эти значения. Например, для некоторых операций нужно учитывать значение заголовка Azure-AsyncOperation, а для других — значение заголовка Location. 

Значения этих заголовков вы можете получить так же, как и любых других заголовков запроса. Например, приведенный ниже код C# извлекает значение заголовка из объекта `HttpWebResponse` с именем `response`.

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Запрос и ответ с использованием Azure-AsyncOperation

Чтобы получить состояние асинхронной операции, отправьте запрос GET на URL-адрес, указанный в заголовке Azure-AsyncOperation.

Текст ответа, полученного от операции, будет содержать сведения о ее выполнении. В примере ниже показаны возможные значения, возвращаемые операцией.

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

Только `status` будет присутствовать во всех ответах. Объект error возвращается в том случае, если операция находится в состоянии сбоя (Failed) или отмены (Canceled). Все остальные значения являются необязательными, поэтому полученный ответ может существенно отличаться от этого примера.

## <a name="provisioningstate-values"></a>Значения provisioningState

Операции, которые создают, обновляют или удаляют ресурсы (PUT, PATCH, DELETE), обычно возвращают значение `provisioningState`. После завершения операции возвращается одно из следующих трех значений: 

* Успешно
* Сбой
* Canceled

Любое другое значение означает, что операция еще выполняется. Поставщик ресурсов может возвращать настраиваемое значение, указывающее его состояние. Например, значение **Accepted** (Принято) может сигнализировать о том, что запрос успешно получен и выполняется.

## <a name="example-requests-and-responses"></a>Примеры запросов и ответов

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>Запуск виртуальной машины (код 202, значение Azure-AsyncOperation)
Здесь показано, как можно проверить состояние операции **Start** для виртуальных машин. Исходный запрос имеет следующий формат:

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

В ответ получен код состояния 202. Среди полученных в заголовке значений есть такое:

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

Чтобы проверить состояние асинхронной операции, отправьте запрос на полученный URL-адрес.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

Текст ответа содержит состояние операции:

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>Развертывание ресурсов (код 201, значение Azure-AsyncOperation)

Здесь показано, как можно проверить состояние операции **deployments** для развертывания ресурсов в Azure. Исходный запрос имеет следующий формат:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

В ответ получен код состояния 201. Текст ответа включает следующие данные:

```json
"provisioningState":"Accepted",
```

Среди полученных в заголовке значений есть такое:

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

Чтобы проверить состояние асинхронной операции, отправьте запрос на полученный URL-адрес.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

Текст ответа содержит состояние операции:

```json
{"status":"Running"}
```

После завершения развертывания возвращается ответ с такими данными:

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>Создание учетной записи хранения (код 202, значения Location и Retry-After)

Здесь показано, как можно проверить состояние операции **create** для учетных записей хранения. Исходный запрос имеет следующий формат:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

Кроме того, текст запроса содержит свойства учетной записи хранения:

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

В ответ получен код состояния 202. Среди полученных в заголовке значений есть такие:

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

Подождав указанное в значении Retry-After количество секунд, проверьте состояние асинхронной операции посредством отправки еще одного запроса на указанный URL-адрес.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

Если запрос все еще выполняется, вы получите код состояния 202. Если запрос завершен, вы получите код состояния 200, а в тексте ответа будут указаны свойства созданной учетной записи хранения.

## <a name="next-steps"></a>Дальнейшие действия

* Документацию по каждой операции REST см. в [справочнике по REST API](/rest/api/).
* Сведения об управлении ресурсами с помощью REST API в Resource Manager см. [здесь](resource-manager-rest-api.md).
* Сведения о развертывании шаблонов с помощью REST API в Resource Manager см. в статье [Развертывание ресурсов с использованием шаблонов и REST API Resource Manager](resource-group-template-deploy-rest.md).