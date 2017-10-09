---
title: "ограничения запросов диспетчера ресурсов aaaAzure | Документы Microsoft"
description: "Описывает, как toouse регулирования Azure Resource Manager запрашивает достижении ограничения подписки."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a>Регулирование запросов Resource Manager
Для каждой подписки и клиента ограничения диспетчера ресурсов чтения too15 запросы, 000 в час и записи too1 запросы, 200 в час. Эти ограничения относятся tooeach экземпляр диспетчера ресурсов Azure; Существует несколько экземпляров в каждом регионе Azure, и диспетчер ресурсов Azure — развернутой tooall Azure областей.  На практике ограничений гораздо больше, чем указано выше, так как запросы пользователя обычно обслуживаются многими экземплярами.

Если приложению или сценарию, достигает этих ограничений, вы должны toothrottle запросов. В этом разделе показано, как toodetermine hello оставшихся запрашивает у вас есть до достижения предела hello и как toorespond при достижении максимального hello.

По достижении предела hello появляется код состояния hello HTTP **429 слишком много запросов**.

Здравствуйте, число запросов является областью tooeither подписки или клиента. При наличии нескольких параллельных приложений, выполняющие запросы в вашей подписке hello запросы от этих приложений суммируются toodetermine hello число оставшихся запросов.

Запросы подписок область — это аргументы, hello включают передача идентификатором подписки, такие как извлечение hello групп ресурсов в вашей подписке. Запросы, ограничиваемые клиентом, не включают в себя идентификатор подписки (например, извлечение действительных расположений Azure).

## <a name="remaining-requests"></a>Количество оставшихся запросов
Можно определить hello число оставшихся запросов на основе заголовков ответа. Каждый запрос содержит значения для hello количества оставшихся чтения и записи запросов. Hello следующей таблице описаны заголовки ответа hello, можно изучить для этих значений.

| Заголовок ответа | Описание |
| --- | --- |
| x-ms-ratelimit-remaining-subscription-reads |Оставшееся количество запросов на чтение для подписки. |
| x-ms-ratelimit-remaining-subscription-writes |Оставшееся количество запросов на запись для подписки. |
| x-ms-ratelimit-remaining-tenant-reads |Оставшееся количество запросов на чтение для клиента. |
| x-ms-ratelimit-remaining-tenant-writes |Оставшееся количество запросов на запись для клиента. |
| x-ms-ratelimit-remaining-subscription-resource-requests |Оставшееся количество запросов для типа ресурса для подписки.<br /><br />Значение заголовка возвращается только в том случае, если служба переопределил ограничение по умолчанию hello. Диспетчер ресурсов добавляет это значение вместо hello подписки чтения или записи. |
| x-ms-ratelimit-remaining-subscription-resource-entities-read |Оставшееся количество запросов коллекции типов ресурсов для подписки.<br /><br />Значение заголовка возвращается только в том случае, если служба переопределил ограничение по умолчанию hello. Это значение предоставляет hello количество оставшихся сбора запросов (список ресурсы). |
| x-ms-ratelimit-remaining-tenant-resource-requests |Оставшееся количество запросов для типа ресурса для клиента.<br /><br />Этот заголовок добавляется только для запросов на уровне клиента и только в том случае, если служба переопределил ограничение по умолчанию hello. Диспетчер ресурсов добавляет это значение вместо приветствия клиента чтения или записи. |
| x-ms-ratelimit-remaining-tenant-resource-entities-read |Оставшееся количество запросов коллекции типов ресурсов для клиента.<br /><br />Этот заголовок добавляется только для запросов на уровне клиента и только в том случае, если служба переопределил ограничение по умолчанию hello. |

## <a name="retrieving-hello-header-values"></a>Извлечение значений из заголовка hello
Получение этих значений заголовков в коде или сценарии ничем не отличается от извлечения любого другого значения заголовка. 

Например, в **C#**, получить значение заголовка hello из **HttpWebResponse** объект с именем **ответ** с hello, следующий код:

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

В **PowerShell**, получить значение заголовка hello из операции Invoke-WebRequest.

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

Или, если хотите toosee hello оставшихся запросов для отладки, вы можете предоставить hello **-Отладка** параметра в вашей **PowerShell** командлета.

```powershell
Get-AzureRmResourceGroup -Debug
```

Возвращающий множество значений, включая следующие значения ответа hello:

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

В **Azure CLI**, значение заголовка hello получить с помощью hello параметром более подробных сведений.

```azurecli
azure group list -vv --json
```

Выдаются много значений, включая hello следующий объект:

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a>Ожидание перед отправкой следующего запроса
Когда будет достигнут предел количества запросов hello, диспетчер ресурсов возвращает hello **429** код состояния HTTP и **Retry-After** значение в заголовке hello. Hello **Retry-After** значение указывает hello количество секунд ожидания приложения (или спящего режима) до отправки следующего запроса hello. При отправке запроса до истечения значение повтора hello, запрос не обрабатывается и возвращается новое значение "Повторить".

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения об ограничениях и квотах см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md).
* toolearn об обработке асинхронных запросов REST, в разделе [отслеживания асинхронных операций Azure](resource-manager-async-operations.md).
