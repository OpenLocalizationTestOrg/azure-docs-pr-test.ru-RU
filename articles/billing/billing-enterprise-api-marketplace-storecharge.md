---
title: "aaaAzure выставления счетов Enterprise API-интерфейсов - о расходах в Marketplace | Документы Microsoft"
description: "Дополнительные сведения о hello API отчетов, которые программным образом включить корпоративных клиентов toopull потребления данных Azure."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>API-интерфейсы отчетов для корпоративных клиентов: платежи в Marketplace

Hello декомпозиции API платы магазина Marketplace возвращает hello marketplace с учетом использования расходов по дням для hello указан период выставления счетов или даты начала и окончания (сборов за один раз, не включены).

##<a name="request"></a>Запрос 
Задаются общие свойства заголовка, которые необходимо добавить toobe [здесь](billing-enterprise-api.md). Если периода выставления счетов не указан, данные для выставления счетов hello для текущего периода возвращается. Пользовательские временных диапазонов могут быть заданы с начала hello и окончания параметры даты, которые находятся в hello формат гггг мм дд максимальное hello поддерживается время диапазон: 36 месяцев.  

|Метод | URI запроса|
|-|-|
|ПОЛУЧЕНИЕ|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges|
|ПОЛУЧЕНИЕ|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges|
|ПОЛУЧЕНИЕ|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> toouse hello предварительную версию API, замените v2 v1 в hello выше URL-адрес.
>

## <a name="response"></a>Ответ
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

**Определения свойств ответа**

|Имя свойства| Тип| Описание
|-|-|-|
|id|string|Уникальный идентификатор для элемента платы hello marketplace|
|subscriptionGuid|Guid|Hello Guid подписки|
|subscriptionName|string|Hello имя подписки|
|meterId|string|Идентификатор для hello создается индикатора|
|usageStartDate|DateTime|Время начала для записи об использовании hello|
|usageEndDate|DateTime|Время окончания для записи об использовании hello|
|offerName|string|имя предложения Hello|
|resourceGroup|string|Hello ресурсов группы|
|instanceId|string|Идентификатор экземпляра|
|additionalInfo|string|Строка JSON с дополнительной информацией|
|tags|string|Строка JSON с тегами|
|orderNumber|string|Номер заказа Hello|
|unitOfMeasure|string|Единица измерения для индикатора hello|
|costCenter|string|Центр затрат Hello|
|accountId|int|Учетная запись Hello идентификатор|
|accountName|string |Hello имя учетной записи|
|accountOwnerId|string|Hello идентификатор владельца учетной записи|
|departmentId|int|отдел Hello идентификатор|
|departmentName|string|Название отдела Hello|
|publisherName|string|Имя издателя Hello|
|planName|string|Имя плана Hello|
|consumedQuantity|decimal|Потребленный объем за этот период времени|
|resourceRate|decimal|Цена единицы для индикатора hello|
|extendedCost|decimal|Оценка расходов на основе потребленного объема и расширенных затрат|
<br/>
## <a name="see-also"></a>См. также

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды](billing-enterprise-api-billing-periods.md)

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании](billing-enterprise-api-usage-detail.md) 

* [Интерфейсы API отчетов для корпоративных клиентов: баланс и сводка](billing-enterprise-api-balance-summary.md)

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант](billing-enterprise-api-pricesheet.md)