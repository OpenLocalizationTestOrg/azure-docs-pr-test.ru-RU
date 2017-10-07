---
title: "aaaAzure интерфейсы API Enterprise выставления счетов — сведения об использовании | Документы Microsoft"
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>API-интерфейсы отчетов для корпоративных клиентов: сведения об использовании

Hello API сведений об использовании предлагает ежедневного декомпозиция обрабатываемом количеств и оценка расходов по регистрации. результат Hello также содержатся сведения о экземпляров, показателей и отделах. можно запрашивать Hello API периода выставления счетов или указанными датами начала и окончания. 
## <a name="consumption-apis"></a>Интерфейсы API потребления


##<a name="request"></a>Запрос 
Задаются общие свойства заголовка, которые необходимо добавить toobe [здесь](billing-enterprise-api.md). Если периода выставления счетов не указан, данные для выставления счетов hello для текущего периода возвращается. Пользовательские временных диапазонов могут быть заданы с начала hello и окончания параметры даты, которые находятся в hello формат гггг мм-дд. Hello максимальное время, поддерживаемый диапазон: 36 месяцев.  

|Метод | URI запроса|
|-|-|
|ПОЛУЧЕНИЕ|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails 
|ПОЛУЧЕНИЕ|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails|
|ПОЛУЧЕНИЕ|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> toouse hello предварительную версию API, замените v2 v1 в hello выше URL-адрес.
>

## <a name="response"></a>Ответ

> Из-за toohello потенциально большого объема данных hello результирующий набор разбиении на страницы. Свойство nextLink Hello, при их наличии указывает ссылку hello hello следующую страницу данных. Если ссылка hello пуст, это указывает, что это последняя страница приветствия. 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/>
**Определения свойств ответа**

|Имя свойства| Тип| Описание
|-|-|-|
|id| string| Hello уникальный идентификатор для вызова hello API. |
|data| Массив JSON| Здравствуйте, массив ежедневные подробные сведения об использовании каждого instance\meter.|
|nextLink| string| При наличии нескольких страниц данных hello nextLink точки toohello URL-адрес tooreturn hello следующей страницы данных. |
|accountId| int| Устаревшее поле. Сохранено для обратной совместимости. |
|productId| int| Устаревшее поле. Сохранено для обратной совместимости. |
|resourceLocationId| int| Устаревшее поле. Сохранено для обратной совместимости. |
|consumedServiceID| int| Устаревшее поле. Сохранено для обратной совместимости. |
|departmentId| int| Устаревшее поле. Сохранено для обратной совместимости. |
|accountOwnerEmail| string| Учетная запись электронной почты владельца учетной записи hello. |
|accountName| string| Клиент введено имя учетной записи hello. |
|serviceAdministratorId| string| Адрес электронной почты администратора службы. |
|subscriptionId| int| Устаревшее поле. Сохранено для обратной совместимости. |
|subscriptionGuid| string| Глобальный уникальный идентификатор для подписки hello. |
|subscriptionName| string| Имя подписки hello. |
|дата| string| Дата Hello, в котором произошло потребления. |
|product| string| Дополнительные сведения о индикатор hello. Пример: виртуальная машина A1 Windows — восток Азиатско-тихоокеанского региона|
|meterId| string| Идентификатор Hello индикатор hello которого создается использования. |
|meterCategory| string| Здравствуйте, службы платформы Azure, который был использован. |
|meterSubCategory| string| Определяет тип службы Azure hello, которые могут повлиять на скорость hello. Пример: виртуальная машина A1 (не Windows)|
|meterRegion| string| Определяет местоположение hello hello центра обработки данных для определенных служб, которые оцениваются на основе расположения центра обработки данных. |
|meterName| string| Имя индикатора hello. |
|consumedQuantity| double| объем индикатор hello, отработанной Hello. |
|resourceRate| double| Hello тарифу, применимому оплачиваемых единицы. |
|cost| double| Hello издержек, выполненным индикатор hello. |
|resourceLocation| string| Идентифицирует hello центра обработки данных, где запущен индикатор hello. |
|consumedService| string| Здравствуйте, службы платформы Azure, который был использован. |
|instanceId| string| Этот идентификатор является hello имя ресурса hello или hello полный идентификатор ресурса. Подробные сведения см. на странице, посвященной [API Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). |
|serviceInfo1| string| Метаданные внутренней службы Azure. |
|serviceInfo2| string| Например, тип образа для виртуальной машины и имя поставщика услуг Интернета для ExpressRoute. |
|additionalInfo| string| Метаданные определенных служб. Например, тип образа для виртуальной машины. |
|Теги| string| Добавляемые клиентом теги. Дополнительные сведения см. в статье [Использование тегов для организации ресурсов в Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags). |
|storeServiceIdentifier| string| Этот столбец не используется. Сохранен для обратной совместимости. |
|departmentName| string| Имя подразделения hello. |
|costCenter| string| Центр затрат Hello, связанный с использованием hello. |
|unitOfMeasure| string| Определяет единицу hello, служба hello плата взимается за. Например: гигабайты, часы, десятки тысяч секунд. |
|resourceGroup| string| в какой hello развернутой индикатор работает в группе ресурсов Hello. Дополнительные сведения см. в [обзоре Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
<br/>
## <a name="see-also"></a>См. также

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды](billing-enterprise-api-billing-periods.md)

* [Интерфейсы API отчетов для корпоративных клиентов: баланс и сводка](billing-enterprise-api-balance-summary.md)

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace](billing-enterprise-api-marketplace-storecharge.md) 

* [Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант](billing-enterprise-api-pricesheet.md)
