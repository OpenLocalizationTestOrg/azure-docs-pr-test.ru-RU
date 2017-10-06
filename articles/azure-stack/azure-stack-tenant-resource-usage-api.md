---
title: "API использования ресурсов aaaTenant | Документы Microsoft"
description: "Ссылку для использования ресурсов API, которая получить сведения об использовании Azure стека."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b9d7c7ee-e906-4978-92a3-a2c52df16c36
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: eb826aba87b3b5b79155d9003162f2b5e6871f82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tenant-resource-usage-api"></a>Использование ресурсов API клиента
Клиент может использовать hello hello tooview API клиента клиента собственные данные об использовании ресурсов. Этот API согласуется с hello API использования Azure (в настоящее время в личной предварительной версии).

Можно использовать командлет Windows PowerShell hello **Get UsageAggregates** tooget данные об использовании, как в Azure.

## <a name="api-call"></a>Вызов API
### <a name="request"></a>Запрос
Hello сведения о потреблении запрос возвращает для hello запрашивается подписки и для hello запрошен промежуток времени. Нет текста запроса нет.

| **Метод** | **URI запроса** |
| --- | --- |
| ПОЛУЧЕНИЕ |https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version= 2015-06-01-preview & continuationToken = {значение маркера} |

### <a name="arguments"></a>Аргументы
| **Аргумент** | **Описание** |
| --- | --- |
| *Armendpoint* |Конечная точка Azure диспетчер ресурсов среды Azure стека. Hello соглашение стек Azure — имя этого hello диспетчера ресурсов Azure конечная точка находится в формате hello `https://management.{domain-name}`. Например, если hello доменное имя local.azurestack.external, то конечная точка диспетчера ресурсов hello `https://management.local.azurestack.external`. |
| *subId* |Идентификатор подписки hello пользователя, который выполняет вызов hello. Для использования одной подписке можно использовать только tooquery этого API. Поставщики могут использовать использования tooquery hello API использования поставщика ресурсов для всех клиентов. |
| *reportedStartTime* |Запуск запроса hello. Здравствуйте, значение для *DateTime* должно быть в формате UTC и в начале hello hello час, 13:00. Для ежедневного статистической обработки значение полуночи tooUTC это значение. Формат Hello *escape-последовательность* ISO 8601, например, 2015-06-16T18% 3a53% 3a11% 2b00% 3a00Z, где двоеточие escape-последовательность слишком % 3a и плюс экранируется слишком 2b %, чтобы оно было понятное URI. |
| *reportedEndTime* |Время окончания запроса hello. Здравствуйте, ограничения, применяемые слишком*reportedStartTime* справедливы toothis аргумент. Здравствуйте, значение для *reportedEndTime* не может быть в будущем hello. |
| *aggregationGranularity* |Необязательный параметр, который имеет два дискретных возможные значения: дням или часам. Предложить значения hello, одно возвращает данные hello в дням и hello других является почасовой разрешение. параметр ежедневной Hello — по умолчанию hello. |
| *версия API* |Версия протокола hello, используемые toomake этого запроса. Необходимо использовать 2015-06-01-preview. |
| *continuationToken* |Маркер извлекается из hello последнего вызова toohello использования API поставщика. Этот токен необходим в том случае, когда ответ больше 1 000 строк и он действует в качестве закладки для хода выполнения. Если он отсутствует, данные извлекаются из hello начало hello день или час, в зависимости от гранулярности hello, переданный приветствия. |

### <a name="response"></a>Ответ
ПОЛУЧИТЬ /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00 & reportedEndTime = 2015-06-01T00% 3a00% 3a00% 2b00% 3a00 & aggregationGranularity = ежедневно & api-version = 1,0

{

«значение»:\[

{

«Идентификатор»: «/ subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1»,

«Имя»: «sub1-meterID1»

«Тип»: «Microsoft.Commerce/UsageAggregate»

"properties": {

«subscriptionId»: «sub1»

«usageStartTime»: «2015-03-03T00:00:00 + 00:00»,

«usageEndTime»: «2015-03-04T00:00:00 + 00:00»,

«instanceData»: «{\\» Microsoft.Resources\\»: {\\» resourceUri\\»:\\» resourceUri1\\»,\\«расположение\\»:\\«Аляска \\»,\\«теги\\«: null,\\» additionalInfo\\«: null}}»,

:2.4000000000 «quantity»

«meterId»: «meterID1»

}

},

…

### <a name="response-details"></a>Сведения об ответе
| **Аргумент** | **Описание** |
| --- | --- |
| *id* |Уникальный идентификатор совокупное использование hello |
| *name* |Имя статистической использования hello |
| *type* |Определение ресурсов |
| *subscriptionId* |Идентификатор подписки hello Azure пользователя |
| *usageStartTime* |Время hello использование контейнеров toowhich, к которому относится это статистическое выражение использования начала UTC |
| *usageEndTime* |Время hello использование контейнеров toowhich, к которому относится это статистическое выражение использования завершения UTC |
| *instanceData* |Подробные сведения об экземпляре (в новом формате) пар ключ значение:<br>  *resourceUri*: полный идентификатор ресурса, включая группы ресурсов и имя экземпляра <br>  *расположение*: область, в котором эта служба была запущена <br>  *теги*: теги ресурсов этого пользователя hello указывает <br>  *additionalInfo*: более подробные сведения о ресурсе hello, которое было получено, например, тип версии или образа ОС |
| *количество* |Объем потребления ресурсов, возникшее в этот промежуток времени |
| *meterId* |Уникальный идентификатор ресурса hello, которое было получено (также называемый *ResourceID*) |

## <a name="next-steps"></a>Дальнейшие действия
[API использования ресурсов для поставщиков](azure-stack-provider-resource-api.md)

[Часто задаваемые вопросы, относящиеся к использованию](azure-stack-usage-related-faq.md)

