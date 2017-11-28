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
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="5f9fd-103">Интерфейсы API отчетов для корпоративных клиентов: расчетные периоды</span><span class="sxs-lookup"><span data-stu-id="5f9fd-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="5f9fd-104">Выставление счетов API периодов Привет возвращает список выставления счетов за периоды данных об энергопотреблении для hello указанных регистрации в обратном хронологическом порядке.</span><span class="sxs-lookup"><span data-stu-id="5f9fd-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="5f9fd-105">Для каждого периода содержит свойство, указывающее toohello API маршрута для четырех наборов данных - BalanceSummary, UsageDetails, Marktplace расходы и PriceSheet hello.</span><span class="sxs-lookup"><span data-stu-id="5f9fd-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="5f9fd-106">Если период hello не имеет данных, hello соответствующее свойство имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="5f9fd-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="5f9fd-107">Запрос</span><span class="sxs-lookup"><span data-stu-id="5f9fd-107">Request</span></span> 
<span data-ttu-id="5f9fd-108">Задаются общие свойства заголовка, которые необходимо добавить toobe [здесь](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="5f9fd-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="5f9fd-109">Метод</span><span class="sxs-lookup"><span data-stu-id="5f9fd-109">Method</span></span> | <span data-ttu-id="5f9fd-110">URI запроса</span><span class="sxs-lookup"><span data-stu-id="5f9fd-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="5f9fd-111">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="5f9fd-111">GET</span></span>| <span data-ttu-id="5f9fd-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="5f9fd-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="5f9fd-113">toouse hello предварительную версию API, замените v2 v1 в hello выше URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="5f9fd-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="5f9fd-114">Ответ</span><span class="sxs-lookup"><span data-stu-id="5f9fd-114">Response</span></span>
 
    
    
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
    

<span data-ttu-id="5f9fd-115">**Определения свойств ответа**</span><span class="sxs-lookup"><span data-stu-id="5f9fd-115">**Response property definitions**</span></span>

|<span data-ttu-id="5f9fd-116">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="5f9fd-116">Property Name</span></span>| <span data-ttu-id="5f9fd-117">Тип</span><span class="sxs-lookup"><span data-stu-id="5f9fd-117">Type</span></span>| <span data-ttu-id="5f9fd-118">Описание</span><span class="sxs-lookup"><span data-stu-id="5f9fd-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="5f9fd-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="5f9fd-119">billingPeriodId</span></span>| <span data-ttu-id="5f9fd-120">string</span><span class="sxs-lookup"><span data-stu-id="5f9fd-120">string</span></span>| <span data-ttu-id="5f9fd-121">Hello уникальный идентификатор, представляющий определенного периода выставления счетов</span><span class="sxs-lookup"><span data-stu-id="5f9fd-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="5f9fd-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="5f9fd-122">billingStart</span></span>| <span data-ttu-id="5f9fd-123">datetime;</span><span class="sxs-lookup"><span data-stu-id="5f9fd-123">datetime</span></span>| <span data-ttu-id="5f9fd-124">ISO 8601 строка, представляющая дату начала периода hello</span><span class="sxs-lookup"><span data-stu-id="5f9fd-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="5f9fd-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="5f9fd-125">billingEnd</span></span>| <span data-ttu-id="5f9fd-126">datetime;</span><span class="sxs-lookup"><span data-stu-id="5f9fd-126">datetime</span></span>| <span data-ttu-id="5f9fd-127">ISO 8601 строка, представляющая дату окончания периода hello</span><span class="sxs-lookup"><span data-stu-id="5f9fd-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="5f9fd-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="5f9fd-128">balanceSummary</span></span>| <span data-ttu-id="5f9fd-129">string</span><span class="sxs-lookup"><span data-stu-id="5f9fd-129">string</span></span>| <span data-ttu-id="5f9fd-130">Hello URL-пути, направляет toohello баланс сводные данные за этот период</span><span class="sxs-lookup"><span data-stu-id="5f9fd-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="5f9fd-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="5f9fd-131">usageDetails</span></span>| <span data-ttu-id="5f9fd-132">string</span><span class="sxs-lookup"><span data-stu-id="5f9fd-132">string</span></span>| <span data-ttu-id="5f9fd-133">Hello URL-пути, передает данные, сведения об использовании toohello за этот период</span><span class="sxs-lookup"><span data-stu-id="5f9fd-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="5f9fd-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="5f9fd-134">marketplaceCharges</span></span>| <span data-ttu-id="5f9fd-135">string</span><span class="sxs-lookup"><span data-stu-id="5f9fd-135">string</span></span>| <span data-ttu-id="5f9fd-136">Hello URL-адрес, который передает данные о расходах в Marketplace, toohello за этот период</span><span class="sxs-lookup"><span data-stu-id="5f9fd-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="5f9fd-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="5f9fd-137">priceSheet</span></span>| <span data-ttu-id="5f9fd-138">string</span><span class="sxs-lookup"><span data-stu-id="5f9fd-138">string</span></span>| <span data-ttu-id="5f9fd-139">URL-адрес Hello, при котором toohello PriceSheet данные за этот период</span><span class="sxs-lookup"><span data-stu-id="5f9fd-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="5f9fd-140">См. также</span><span class="sxs-lookup"><span data-stu-id="5f9fd-140">See also</span></span>

* [<span data-ttu-id="5f9fd-141">Интерфейсы API отчетов для корпоративных клиентов: баланс и сводка</span><span class="sxs-lookup"><span data-stu-id="5f9fd-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="5f9fd-142">Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="5f9fd-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="5f9fd-143">Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace</span><span class="sxs-lookup"><span data-stu-id="5f9fd-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="5f9fd-144">Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант</span><span class="sxs-lookup"><span data-stu-id="5f9fd-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)