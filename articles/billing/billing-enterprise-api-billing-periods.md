---
title: "Выставление счетов Enterprise API-интерфейсов - выставления счетов за периоды aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>Интерфейсы API отчетов для корпоративных клиентов: расчетные периоды

Выставление счетов API периодов Привет возвращает список выставления счетов за периоды данных об энергопотреблении для hello указанных регистрации в обратном хронологическом порядке. Для каждого периода содержит свойство, указывающее toohello API маршрута для четырех наборов данных - BalanceSummary, UsageDetails, Marktplace расходы и PriceSheet hello. Если период hello не имеет данных, hello соответствующее свойство имеет значение null. 


##<a name="request"></a>Запрос 
Задаются общие свойства заголовка, которые необходимо добавить toobe [здесь](billing-enterprise-api.md). 

|Метод | URI запроса|
|-|-|
|ПОЛУЧЕНИЕ| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods|

> [!Note]
> toouse hello предварительную версию API, замените v2 v1 в hello выше URL-адрес.
>

## <a name="response"></a>Ответ
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

**Определения свойств ответа**

|Имя свойства| Тип| Описание
|-|-|-|
|billingPeriodId| string| Hello уникальный идентификатор, представляющий определенного периода выставления счетов|
|billingStart| datetime;| ISO 8601 строка, представляющая дату начала периода hello|
|billingEnd| datetime;| ISO 8601 строка, представляющая дату окончания периода hello|
|balanceSummary| string| Hello URL-пути, направляет toohello баланс сводные данные за этот период|
|usageDetails| string| Hello URL-пути, передает данные, сведения об использовании toohello за этот период|
|marketplaceCharges| string| Hello URL-адрес, который передает данные о расходах в Marketplace, toohello за этот период|
|priceSheet| string| URL-адрес Hello, при котором toohello PriceSheet данные за этот период|

<br/>
## <a name="see-also"></a>См. также

* [Интерфейсы API отчетов для корпоративных клиентов: баланс и сводка](billing-enterprise-api-balance-summary.md)

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании](billing-enterprise-api-usage-detail.md) 

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace](billing-enterprise-api-marketplace-storecharge.md) 

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант](billing-enterprise-api-pricesheet.md)