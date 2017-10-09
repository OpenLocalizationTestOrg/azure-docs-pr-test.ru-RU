---
title: "aaaAzure выставления счетов Enterprise API-интерфейсов - баланс и Сводка | Документы Microsoft"
description: "Дополнительные сведения об использовании выставления счетов Azure и RateCard API-интерфейсы, которые используется tooprovide анализировать потребление ресурсов Azure и тенденции."
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a>API-интерфейсы отчетов для корпоративных клиентов: баланс и сводка

Hello баланс и Сводка API предоставляет ежемесячные сводку сведений о сальдо, новый покупок, плата за Azure Marketplace, корректировки и избыточные расходы.


##<a name="request"></a>Запрос 
Задаются общие свойства заголовка, которые необходимо добавить toobe [здесь](billing-enterprise-api.md). Если периода выставления счетов не указан, данные для выставления счетов hello для текущего периода возвращается.

|Метод | URI запроса|
|-|-|
|ПОЛУЧЕНИЕ| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary|
|ПОЛУЧЕНИЕ| https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary|

> [!Note]
> toouse hello предварительную версию API, замените v2 v1 в hello выше URL-адрес.
>

## <a name="response"></a>Ответ

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


**Определения свойств ответа**

|Имя свойства| Тип| Описание
|-|-|-|
|id|string|Hello уникальный идентификатор для определенного периода выставления счетов и регистрации|
|billingPeriodId|string |Привет, код периода выставления счетов|
|currencyCode|string |Код валюты Hello|
|beginningBalance|decimal| Начальное сальдо Hello hello цикл выставления счетов|
|endingBalance|decimal| Привет, конечное сальдо периода выставления счетов hello (для открытых периодов, это будет обновляться ежедневно)|
|newPurchases|decimal| Общая сумма новой покупки|
|adjustments|decimal| Общая сумма корректировки|
|utilized|decimal| Общая сумма обязательств|
|serviceOverage|decimal| Превышение использования служб Azure|
|chargesBilledSeparately|decimal| Счета, выставляемые отдельно|
|totalOverage|decimal| serviceOverage + chargesBilledSeparately|
|totalUsage|decimal| Обязательства по службам Azure + totalOverage|
|azureMarketplaceServiceCharges|decimal| Общая сумма платежей за использование Azure Marketplace|
|newPurchasesDetails|Массив строк JSON из пар "имя-значение"|Список новых покупок|
|adjustmentDetails|Массив строк JSON из пар "имя-значение"|Список корректировок (акционный кредит, кредит SIE и т. д.) |


<br/>
## <a name="see-also"></a>См. также

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды](billing-enterprise-api-billing-periods.md)

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании](billing-enterprise-api-usage-detail.md) 

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace](billing-enterprise-api-marketplace-storecharge.md) 

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант](billing-enterprise-api-pricesheet.md)