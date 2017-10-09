---
title: "aaaAzure выставления счетов Enterprise API-интерфейсов - PriceSheet | Документы Microsoft"
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>API-интерфейсы отчетов для корпоративных клиентов: прейскурант

Hello цена лист API предоставляет соответствующему курсу hello для каждого индикатора для регистрации и выставления счетов за период hello.

##<a name="request"></a>Запрос
Задаются общие свойства заголовка, которые необходимо добавить toobe [здесь](billing-enterprise-api.md). Если периода выставления счетов не указан, данные для выставления счетов hello для текущего периода возвращается.

|Метод | URI запроса|
|-|-|
|ПОЛУЧЕНИЕ|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet|
|ПОЛУЧЕНИЕ|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet|

> [!Note]
> toouse hello предварительную версию API, замените v2 v1 в hello выше URL-адрес.
>

## <a name="response"></a>Ответ

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
>Если вы используете hello API предварительной версии, meterId поле недоступно.
>

**Определения свойств ответа**

|Имя свойства| Тип| Описание
|-|-|-|
|id| string| Hello уникальный идентификатор, представляющий определенный элемент PriceSheet (индикатор, расчетный период)|
|billingPeriodId| string| Hello уникальный идентификатор, представляющий определенного периода выставления счетов|
|meterId| string| Идентификатор Hello индикатор hello. Это может быть meterId сопоставленных toohello использования.|
|meterName| string| имя индикатора Hello|
|unitOfMeasure| string| Hello единица измерения для измерения службы hello|
|includedQuantity| decimal| Количество, которое включено |
|partNumber| string| Номер части Hello, связанный с hello индикатора|
|unitPrice| decimal| Hello цену за единицу для индикатора hello|
|currencyCode| string| Код валюты Hello hello unitPrice|
<br/>
## <a name="see-also"></a>См. также

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды](billing-enterprise-api-billing-periods.md)

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании](billing-enterprise-api-usage-detail.md)

* [Интерфейсы API отчетов для корпоративных клиентов: баланс и сводка](billing-enterprise-api-balance-summary.md)

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace](billing-enterprise-api-marketplace-storecharge.md)
