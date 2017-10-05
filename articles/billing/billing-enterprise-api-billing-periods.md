---
title: "Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды | Документация Майкрософт"
description: "Узнайте, как с помощью интерфейсов API отчетов для корпоративных клиентов Azure извлекать данные о потреблении программным способом."
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
ms.openlocfilehash: c6880b79189e0683387a7aafbd6fa4805b3b42ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="614a8-103">Интерфейсы API отчетов для корпоративных клиентов: расчетные периоды</span><span class="sxs-lookup"><span data-stu-id="614a8-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="614a8-104">API расчетных периодов возвращает список расчетных периодов, которые содержат данные о потреблении для определенной регистрации, приведенные в обратном хронологическом порядке.</span><span class="sxs-lookup"><span data-stu-id="614a8-104">The Billing Periods API returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="614a8-105">Каждый период содержит свойство, указывающее на маршрут API к четырем наборам данных: BalanceSummary, UsageDetails, MarketplaceCharges и PriceSheet.</span><span class="sxs-lookup"><span data-stu-id="614a8-105">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="614a8-106">Если период не содержит данных, то соответствующее свойство имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="614a8-106">If the period does not have data, the corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="614a8-107">Запрос</span><span class="sxs-lookup"><span data-stu-id="614a8-107">Request</span></span> 
<span data-ttu-id="614a8-108">Общие свойства заголовка, которые необходимо добавить, указываются [здесь](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="614a8-108">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="614a8-109">Метод</span><span class="sxs-lookup"><span data-stu-id="614a8-109">Method</span></span> | <span data-ttu-id="614a8-110">URI запроса</span><span class="sxs-lookup"><span data-stu-id="614a8-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="614a8-111">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="614a8-111">GET</span></span>| <span data-ttu-id="614a8-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="614a8-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="614a8-113">Чтобы использовать предварительную версию API, измените v2 на v1 в приведенном выше URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="614a8-113">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="614a8-114">Ответ</span><span class="sxs-lookup"><span data-stu-id="614a8-114">Response</span></span>
 
    
    
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
    

<span data-ttu-id="614a8-115">**Определения свойств ответа**</span><span class="sxs-lookup"><span data-stu-id="614a8-115">**Response property definitions**</span></span>

|<span data-ttu-id="614a8-116">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="614a8-116">Property Name</span></span>| <span data-ttu-id="614a8-117">Тип</span><span class="sxs-lookup"><span data-stu-id="614a8-117">Type</span></span>| <span data-ttu-id="614a8-118">Описание</span><span class="sxs-lookup"><span data-stu-id="614a8-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="614a8-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="614a8-119">billingPeriodId</span></span>| <span data-ttu-id="614a8-120">string</span><span class="sxs-lookup"><span data-stu-id="614a8-120">string</span></span>| <span data-ttu-id="614a8-121">Уникальный идентификатор, представляющий определенный расчетный период</span><span class="sxs-lookup"><span data-stu-id="614a8-121">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="614a8-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="614a8-122">billingStart</span></span>| <span data-ttu-id="614a8-123">datetime;</span><span class="sxs-lookup"><span data-stu-id="614a8-123">datetime</span></span>| <span data-ttu-id="614a8-124">Строка в формате ISO 8601, представляющая дату начала периода</span><span class="sxs-lookup"><span data-stu-id="614a8-124">ISO 8601 string representing the period start date</span></span>|
|<span data-ttu-id="614a8-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="614a8-125">billingEnd</span></span>| <span data-ttu-id="614a8-126">datetime;</span><span class="sxs-lookup"><span data-stu-id="614a8-126">datetime</span></span>| <span data-ttu-id="614a8-127">Строка в формате ISO 8601, представляющая дату окончания периода</span><span class="sxs-lookup"><span data-stu-id="614a8-127">ISO 8601 string representing the period end date</span></span>|
|<span data-ttu-id="614a8-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="614a8-128">balanceSummary</span></span>| <span data-ttu-id="614a8-129">string</span><span class="sxs-lookup"><span data-stu-id="614a8-129">string</span></span>| <span data-ttu-id="614a8-130">URL-адрес, ведущий к сводным данным баланса за указанный период</span><span class="sxs-lookup"><span data-stu-id="614a8-130">The URL path that routes to the Balance Summary data for this period</span></span>|
|<span data-ttu-id="614a8-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="614a8-131">usageDetails</span></span>| <span data-ttu-id="614a8-132">string</span><span class="sxs-lookup"><span data-stu-id="614a8-132">string</span></span>| <span data-ttu-id="614a8-133">URL-адрес, ведущий к сведениям об использовании за указанный период</span><span class="sxs-lookup"><span data-stu-id="614a8-133">The URL path that routes to the Usage Details data for this period</span></span>|
|<span data-ttu-id="614a8-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="614a8-134">marketplaceCharges</span></span>| <span data-ttu-id="614a8-135">string</span><span class="sxs-lookup"><span data-stu-id="614a8-135">string</span></span>| <span data-ttu-id="614a8-136">URL-адрес, ведущий к сведениям о расходах на заказы Marketplace за указанный период</span><span class="sxs-lookup"><span data-stu-id="614a8-136">The URL path that routes to the Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="614a8-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="614a8-137">priceSheet</span></span>| <span data-ttu-id="614a8-138">string</span><span class="sxs-lookup"><span data-stu-id="614a8-138">string</span></span>| <span data-ttu-id="614a8-139">URL-адрес, ведущий к данным прейскурантов за указанный период</span><span class="sxs-lookup"><span data-stu-id="614a8-139">The URL path that routes to the PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="614a8-140">См. также</span><span class="sxs-lookup"><span data-stu-id="614a8-140">See also</span></span>

* [<span data-ttu-id="614a8-141">Интерфейсы API отчетов для корпоративных клиентов: баланс и сводка</span><span class="sxs-lookup"><span data-stu-id="614a8-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="614a8-142">Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="614a8-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="614a8-143">Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace</span><span class="sxs-lookup"><span data-stu-id="614a8-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="614a8-144">Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант</span><span class="sxs-lookup"><span data-stu-id="614a8-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)