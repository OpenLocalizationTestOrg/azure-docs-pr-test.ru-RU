---
title: "Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace | Документация Майкрософт"
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
ms.openlocfilehash: 5539623f7ae35e14b6dafe6fdf9efe4bcaba4fd3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="435ae-103">API-интерфейсы отчетов для корпоративных клиентов: платежи в Marketplace</span><span class="sxs-lookup"><span data-stu-id="435ae-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="435ae-104">Интерфейс API платежей в Marketplace предоставляет сводку о расходах в Marketplace с разбивкой по дням. Данные основаны на фактическом использовании и отображаются для указанного расчетного периода или дат начала и окончания (однократные сборы не включаются).</span><span class="sxs-lookup"><span data-stu-id="435ae-104">The Marketplace Store Charge API returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="435ae-105">Запрос</span><span class="sxs-lookup"><span data-stu-id="435ae-105">Request</span></span> 
<span data-ttu-id="435ae-106">Общие свойства заголовка, которые необходимо добавить, указываются [здесь](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="435ae-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="435ae-107">Если расчетный период не указан, то возвращаются данные за текущий расчетный период.</span><span class="sxs-lookup"><span data-stu-id="435ae-107">If a billing period is not specified, then data for the current billing period is returned.</span></span> <span data-ttu-id="435ae-108">Настраиваемые диапазоны времени можно указать с помощью параметров даты начала и окончания, которые вводятся в формате гггг-ММ-дд. Максимальный поддерживаемый диапазон времени — 36 месяцев.</span><span class="sxs-lookup"><span data-stu-id="435ae-108">Custom time ranges can be specified with the start and end date parameters that are in the format yyyy-MM-dd, the maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="435ae-109">Метод</span><span class="sxs-lookup"><span data-stu-id="435ae-109">Method</span></span> | <span data-ttu-id="435ae-110">URI запроса</span><span class="sxs-lookup"><span data-stu-id="435ae-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="435ae-111">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="435ae-111">GET</span></span>|<span data-ttu-id="435ae-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="435ae-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="435ae-113">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="435ae-113">GET</span></span>|<span data-ttu-id="435ae-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="435ae-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="435ae-115">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="435ae-115">GET</span></span>|<span data-ttu-id="435ae-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="435ae-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="435ae-117">Чтобы использовать предварительную версию API, измените v2 на v1 в URL-адресе выше.</span><span class="sxs-lookup"><span data-stu-id="435ae-117">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="435ae-118">Ответ</span><span class="sxs-lookup"><span data-stu-id="435ae-118">Response</span></span>
 
    
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
    

<span data-ttu-id="435ae-119">**Определения свойств ответа**</span><span class="sxs-lookup"><span data-stu-id="435ae-119">**Response property definitions**</span></span>

|<span data-ttu-id="435ae-120">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="435ae-120">Property Name</span></span>| <span data-ttu-id="435ae-121">Тип</span><span class="sxs-lookup"><span data-stu-id="435ae-121">Type</span></span>| <span data-ttu-id="435ae-122">Описание</span><span class="sxs-lookup"><span data-stu-id="435ae-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="435ae-123">id</span><span class="sxs-lookup"><span data-stu-id="435ae-123">id</span></span>|<span data-ttu-id="435ae-124">string</span><span class="sxs-lookup"><span data-stu-id="435ae-124">string</span></span>|<span data-ttu-id="435ae-125">Уникальный идентификатор для элемента платежа в Marketplace</span><span class="sxs-lookup"><span data-stu-id="435ae-125">Unique Id for the marketplace charge item</span></span>|
|<span data-ttu-id="435ae-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="435ae-126">subscriptionGuid</span></span>|<span data-ttu-id="435ae-127">Guid</span><span class="sxs-lookup"><span data-stu-id="435ae-127">Guid</span></span>|<span data-ttu-id="435ae-128">Идентификатор GUID подписки</span><span class="sxs-lookup"><span data-stu-id="435ae-128">The Subscription Guid</span></span>|
|<span data-ttu-id="435ae-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="435ae-129">subscriptionName</span></span>|<span data-ttu-id="435ae-130">string</span><span class="sxs-lookup"><span data-stu-id="435ae-130">string</span></span>|<span data-ttu-id="435ae-131">Имя подписки</span><span class="sxs-lookup"><span data-stu-id="435ae-131">The Subscription Name</span></span>|
|<span data-ttu-id="435ae-132">meterId</span><span class="sxs-lookup"><span data-stu-id="435ae-132">meterId</span></span>|<span data-ttu-id="435ae-133">string</span><span class="sxs-lookup"><span data-stu-id="435ae-133">string</span></span>|<span data-ttu-id="435ae-134">Идентификатор для генерируемой метрики</span><span class="sxs-lookup"><span data-stu-id="435ae-134">Id for the emitted Meter</span></span>|
|<span data-ttu-id="435ae-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="435ae-135">usageStartDate</span></span>|<span data-ttu-id="435ae-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="435ae-136">DateTime</span></span>|<span data-ttu-id="435ae-137">Время начала записи использования</span><span class="sxs-lookup"><span data-stu-id="435ae-137">Start time for the usage record</span></span>|
|<span data-ttu-id="435ae-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="435ae-138">usageEndDate</span></span>|<span data-ttu-id="435ae-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="435ae-139">DateTime</span></span>|<span data-ttu-id="435ae-140">Время окончания записи использования</span><span class="sxs-lookup"><span data-stu-id="435ae-140">End time for the usage record</span></span>|
|<span data-ttu-id="435ae-141">offerName</span><span class="sxs-lookup"><span data-stu-id="435ae-141">offerName</span></span>|<span data-ttu-id="435ae-142">string</span><span class="sxs-lookup"><span data-stu-id="435ae-142">string</span></span>|<span data-ttu-id="435ae-143">Название предложения</span><span class="sxs-lookup"><span data-stu-id="435ae-143">The Offer name</span></span>|
|<span data-ttu-id="435ae-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="435ae-144">resourceGroup</span></span>|<span data-ttu-id="435ae-145">string</span><span class="sxs-lookup"><span data-stu-id="435ae-145">string</span></span>|<span data-ttu-id="435ae-146">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="435ae-146">The resource Group</span></span>|
|<span data-ttu-id="435ae-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="435ae-147">instanceId</span></span>|<span data-ttu-id="435ae-148">string</span><span class="sxs-lookup"><span data-stu-id="435ae-148">string</span></span>|<span data-ttu-id="435ae-149">Идентификатор экземпляра</span><span class="sxs-lookup"><span data-stu-id="435ae-149">Instance Id</span></span>|
|<span data-ttu-id="435ae-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="435ae-150">additionalInfo</span></span>|<span data-ttu-id="435ae-151">string</span><span class="sxs-lookup"><span data-stu-id="435ae-151">string</span></span>|<span data-ttu-id="435ae-152">Строка JSON с дополнительной информацией</span><span class="sxs-lookup"><span data-stu-id="435ae-152">Additional info JSON string</span></span>|
|<span data-ttu-id="435ae-153">tags</span><span class="sxs-lookup"><span data-stu-id="435ae-153">tags</span></span>|<span data-ttu-id="435ae-154">string</span><span class="sxs-lookup"><span data-stu-id="435ae-154">string</span></span>|<span data-ttu-id="435ae-155">Строка JSON с тегами</span><span class="sxs-lookup"><span data-stu-id="435ae-155">Tag JSON string</span></span>|
|<span data-ttu-id="435ae-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="435ae-156">orderNumber</span></span>|<span data-ttu-id="435ae-157">string</span><span class="sxs-lookup"><span data-stu-id="435ae-157">string</span></span>|<span data-ttu-id="435ae-158">Порядковый номер</span><span class="sxs-lookup"><span data-stu-id="435ae-158">The order number</span></span>|
|<span data-ttu-id="435ae-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="435ae-159">unitOfMeasure</span></span>|<span data-ttu-id="435ae-160">string</span><span class="sxs-lookup"><span data-stu-id="435ae-160">string</span></span>|<span data-ttu-id="435ae-161">Единица измерения метрики</span><span class="sxs-lookup"><span data-stu-id="435ae-161">Unit of measure for the meter</span></span>|
|<span data-ttu-id="435ae-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="435ae-162">costCenter</span></span>|<span data-ttu-id="435ae-163">string</span><span class="sxs-lookup"><span data-stu-id="435ae-163">string</span></span>|<span data-ttu-id="435ae-164">Место возникновения затрат</span><span class="sxs-lookup"><span data-stu-id="435ae-164">The cost center</span></span>|
|<span data-ttu-id="435ae-165">accountId</span><span class="sxs-lookup"><span data-stu-id="435ae-165">accountId</span></span>|<span data-ttu-id="435ae-166">int</span><span class="sxs-lookup"><span data-stu-id="435ae-166">int</span></span>|<span data-ttu-id="435ae-167">Идентификатор учетной записи</span><span class="sxs-lookup"><span data-stu-id="435ae-167">The account Id</span></span>|
|<span data-ttu-id="435ae-168">accountName</span><span class="sxs-lookup"><span data-stu-id="435ae-168">accountName</span></span>|<span data-ttu-id="435ae-169">string</span><span class="sxs-lookup"><span data-stu-id="435ae-169">string</span></span> |<span data-ttu-id="435ae-170">Имя учетной записи</span><span class="sxs-lookup"><span data-stu-id="435ae-170">The Account Name</span></span>|
|<span data-ttu-id="435ae-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="435ae-171">accountOwnerId</span></span>|<span data-ttu-id="435ae-172">string</span><span class="sxs-lookup"><span data-stu-id="435ae-172">string</span></span>|<span data-ttu-id="435ae-173">Идентификатор владельца учетной записи</span><span class="sxs-lookup"><span data-stu-id="435ae-173">The Account Owner Id</span></span>|
|<span data-ttu-id="435ae-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="435ae-174">departmentId</span></span>|<span data-ttu-id="435ae-175">int</span><span class="sxs-lookup"><span data-stu-id="435ae-175">int</span></span>|<span data-ttu-id="435ae-176">Идентификатор отдела</span><span class="sxs-lookup"><span data-stu-id="435ae-176">The department Id</span></span>|
|<span data-ttu-id="435ae-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="435ae-177">departmentName</span></span>|<span data-ttu-id="435ae-178">string</span><span class="sxs-lookup"><span data-stu-id="435ae-178">string</span></span>|<span data-ttu-id="435ae-179">Название отдела</span><span class="sxs-lookup"><span data-stu-id="435ae-179">The department name</span></span>|
|<span data-ttu-id="435ae-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="435ae-180">publisherName</span></span>|<span data-ttu-id="435ae-181">string</span><span class="sxs-lookup"><span data-stu-id="435ae-181">string</span></span>|<span data-ttu-id="435ae-182">Имя издателя</span><span class="sxs-lookup"><span data-stu-id="435ae-182">The publisher name</span></span>|
|<span data-ttu-id="435ae-183">planName</span><span class="sxs-lookup"><span data-stu-id="435ae-183">planName</span></span>|<span data-ttu-id="435ae-184">string</span><span class="sxs-lookup"><span data-stu-id="435ae-184">string</span></span>|<span data-ttu-id="435ae-185">Имя плана</span><span class="sxs-lookup"><span data-stu-id="435ae-185">The Plan name</span></span>|
|<span data-ttu-id="435ae-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="435ae-186">consumedQuantity</span></span>|<span data-ttu-id="435ae-187">decimal</span><span class="sxs-lookup"><span data-stu-id="435ae-187">decimal</span></span>|<span data-ttu-id="435ae-188">Потребленный объем за этот период времени</span><span class="sxs-lookup"><span data-stu-id="435ae-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="435ae-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="435ae-189">resourceRate</span></span>|<span data-ttu-id="435ae-190">decimal</span><span class="sxs-lookup"><span data-stu-id="435ae-190">decimal</span></span>|<span data-ttu-id="435ae-191">Цена единицы для метрики</span><span class="sxs-lookup"><span data-stu-id="435ae-191">Unit price for the meter</span></span>|
|<span data-ttu-id="435ae-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="435ae-192">extendedCost</span></span>|<span data-ttu-id="435ae-193">decimal</span><span class="sxs-lookup"><span data-stu-id="435ae-193">decimal</span></span>|<span data-ttu-id="435ae-194">Оценка расходов на основе потребленного объема и расширенных затрат</span><span class="sxs-lookup"><span data-stu-id="435ae-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="435ae-195">См. также</span><span class="sxs-lookup"><span data-stu-id="435ae-195">See also</span></span>

* [<span data-ttu-id="435ae-196">Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды</span><span class="sxs-lookup"><span data-stu-id="435ae-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="435ae-197">Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="435ae-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="435ae-198">Интерфейсы API отчетов для корпоративных клиентов: баланс и сводка</span><span class="sxs-lookup"><span data-stu-id="435ae-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="435ae-199">Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант</span><span class="sxs-lookup"><span data-stu-id="435ae-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)