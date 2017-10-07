---
title: "API использования ресурсов aaaProvider | Документы Microsoft"
description: "Ссылку для использования ресурсов API, которая получить сведения об использовании Azure стека."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b6055923-b6a6-45f0-8979-225b713150ae
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: alfredop
ms.openlocfilehash: 7cc2d7af27e6abc86e247b2ed0ab1bc236fdb1af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provider-resource-usage-api"></a>Использование поставщика ресурсов API
Поставщик термин Hello применяет toohello администратор службы и поставщики tooany делегированными полномочиями. Администраторы службы и делегированные поставщики могут использовать использование API использования поставщика tooview hello их прямых клиентов. Например P0 можно вызвать P1 и P2 в прямом использовании сведения об использовании tooget API-Интерфейс поставщика hello и P1 можно вызвать для получения сведений об использовании на P3 и P4.

![Концептуальная модель поставщика иерархии](media/azure-stack-provider-resource-api/image1.png)

## <a name="api-call-reference"></a>Вызов API-ссылка
### <a name="request"></a>Запрос
Hello сведения о потреблении запрос возвращает для hello запрашивается подписки и для hello запрошен промежуток времени. Нет текста запроса нет.

Такое использование API является API-Интерфейс поставщика, поэтому вызывающий объект hello должна быть назначена владельца, участника или чтения в подписке hello поставщика.

| **Метод** | **URI запроса** |
| --- | --- |
| ПОЛУЧЕНИЕ |https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}& subscriberId = {sub1.1} & api-version = 2015-06-01-preview & continuationToken = {значение маркера} |

### <a name="arguments"></a>Аргументы
| **Аргумент** | **Описание** |
| --- | --- |
| *armendpoint* |Конечная точка Azure диспетчер ресурсов среды Azure стека. Hello соглашение стек Azure — имя этого hello диспетчера ресурсов Azure конечная точка находится в формате hello `https://adminmanagement.{domain-name}`. Например, если hello доменное имя local.azurestack.external, то конечная точка диспетчера ресурсов hello `https://adminmanagement.local.azurestack.external`. |
| *subId* |Идентификатор подписки hello пользователя, который выполняет вызов hello. |
| *reportedStartTime* |Запуск запроса hello. Здравствуйте, значение для *DateTime* должно быть в формате UTC и в начале hello hello час, 13:00. Для ежедневного статистической обработки значение полуночи tooUTC это значение. Формат Hello *escape-последовательность* ISO 8601, например, 2015-06-16T18% 3a53% 3a11% 2b00% 3a00Z, где двоеточие escape-последовательность слишком % 3a и плюс экранируется слишком 2b %, чтобы оно было понятное URI. |
| *reportedEndTime* |Время окончания запроса hello. Здравствуйте, ограничения, применяемые слишком*reportedStartTime* справедливы toothis аргумент. Здравствуйте, значение для *reportedEndTime* не может быть в будущем hello или hello текущую дату. Если это так, hello результирующий набор слишком «обработка не полный.» |
| *aggregationGranularity* |Необязательный параметр, который имеет два дискретных возможные значения: дням или часам. Предложить значения hello, одно возвращает данные hello в дням и hello других является почасовой разрешение. параметр ежедневной Hello — по умолчанию hello. |
| *subscriberId* |Идентификатор подписки. tooget отфильтрованных данных, требуется идентификатор подписки hello прямой клиент hello поставщика. Если задано ни одного параметра идентификатор подписки, hello вызов возвращает данные об использовании для прямых клиентов все hello поставщика. |
| *версия API* |Версия протокола hello, используемые toomake этого запроса. Это значение too2015-06-01-preview. |
| *continuationToken* |Маркер извлекается из hello последнего вызова toohello использования API поставщика. Этот токен необходим в том случае, когда ответ больше 1 000 строк и он действует в качестве закладки для hello хода выполнения. Если он отсутствует, данные извлекаются из hello начало hello день или час, в зависимости от гранулярности hello, переданный приветствия. |

### <a name="response"></a>Ответ
ПОЛУЧИТЬ /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00 & reportedEndTime = 2015-06-01T00% 3a00% 3a00% 2b00% 3a00 & aggregationGranularity = ежедневно & subscriberId = sub1.1 & api-version = 1,0

{

«значение»:\[

{

«Идентификатор»: «/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-

meterID1»,

«Имя»: «sub1.1-meterID1»

«Тип»: «Microsoft.Commerce/UsageAggregate»

"properties": {

«subscriptionId»: «sub1.1»

«usageStartTime»: «2015-03-03T00:00:00 + 00:00»,

«usageEndTime»: «2015-03-04T00:00:00 + 00:00»,

«instanceData»: «{\\» Microsoft.Resources\\«: {\\» resourceUri\\»:\\» resourceUri1\\»,\\«местоположение\\

«:\\«Аляска\\»,\\«теги\\»: имеет значение null,\\» additionalInfo\\«: null}}»,

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
| *subscriptionId* |Идентификатор подписки hello стек Azure |
| *usageStartTime* |Время hello использование контейнеров toowhich, к которому относится это статистическое выражение использования начала UTC |
| *usageEndTime* |Время hello использование контейнеров toowhich, к которому относится это статистическое выражение использования завершения UTC |
| *instanceData* |Подробные сведения об экземпляре (в новом формате) пар ключ значение:<br> *resourceUri*: полный идентификатор ресурса, включая группы ресурсов hello и имя экземпляра hello <br> *расположение*: область, в котором эта служба была запущена <br> *теги*: теги ресурсов, указанных пользователем hello <br> *additionalInfo*: более подробные сведения о ресурсе hello, которое было получено, например, тип версии или образа ОС |
| *количество* |Объем потребления ресурсов, возникшее в этот промежуток времени |
| *meterId* |Уникальный идентификатор ресурса hello, которое было получено (также называемый *ResourceID*) |

## <a name="next-steps"></a>Дальнейшие действия
[Использование ресурсов клиента Справочник по API](azure-stack-tenant-resource-usage-api.md)

[Часто задаваемые вопросы, относящиеся к использованию](azure-stack-usage-related-faq.md)

