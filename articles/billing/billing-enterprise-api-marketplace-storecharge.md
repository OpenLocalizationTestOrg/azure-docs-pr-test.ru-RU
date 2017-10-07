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
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="676e9-103">API-интерфейсы отчетов для корпоративных клиентов: платежи в Marketplace</span><span class="sxs-lookup"><span data-stu-id="676e9-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="676e9-104">Hello декомпозиции API платы магазина Marketplace возвращает hello marketplace с учетом использования расходов по дням для hello указан период выставления счетов или даты начала и окончания (сборов за один раз, не включены).</span><span class="sxs-lookup"><span data-stu-id="676e9-104">hello Marketplace Store Charge API returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="676e9-105">Запрос</span><span class="sxs-lookup"><span data-stu-id="676e9-105">Request</span></span> 
<span data-ttu-id="676e9-106">Задаются общие свойства заголовка, которые необходимо добавить toobe [здесь](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="676e9-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="676e9-107">Если периода выставления счетов не указан, данные для выставления счетов hello для текущего периода возвращается.</span><span class="sxs-lookup"><span data-stu-id="676e9-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="676e9-108">Пользовательские временных диапазонов могут быть заданы с начала hello и окончания параметры даты, которые находятся в hello формат гггг мм дд максимальное hello поддерживается время диапазон: 36 месяцев.</span><span class="sxs-lookup"><span data-stu-id="676e9-108">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd, hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="676e9-109">Метод</span><span class="sxs-lookup"><span data-stu-id="676e9-109">Method</span></span> | <span data-ttu-id="676e9-110">URI запроса</span><span class="sxs-lookup"><span data-stu-id="676e9-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="676e9-111">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="676e9-111">GET</span></span>|<span data-ttu-id="676e9-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="676e9-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="676e9-113">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="676e9-113">GET</span></span>|<span data-ttu-id="676e9-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="676e9-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="676e9-115">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="676e9-115">GET</span></span>|<span data-ttu-id="676e9-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="676e9-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="676e9-117">toouse hello предварительную версию API, замените v2 v1 в hello выше URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="676e9-117">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="676e9-118">Ответ</span><span class="sxs-lookup"><span data-stu-id="676e9-118">Response</span></span>
 
    
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
    

<span data-ttu-id="676e9-119">**Определения свойств ответа**</span><span class="sxs-lookup"><span data-stu-id="676e9-119">**Response property definitions**</span></span>

|<span data-ttu-id="676e9-120">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="676e9-120">Property Name</span></span>| <span data-ttu-id="676e9-121">Тип</span><span class="sxs-lookup"><span data-stu-id="676e9-121">Type</span></span>| <span data-ttu-id="676e9-122">Описание</span><span class="sxs-lookup"><span data-stu-id="676e9-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="676e9-123">id</span><span class="sxs-lookup"><span data-stu-id="676e9-123">id</span></span>|<span data-ttu-id="676e9-124">string</span><span class="sxs-lookup"><span data-stu-id="676e9-124">string</span></span>|<span data-ttu-id="676e9-125">Уникальный идентификатор для элемента платы hello marketplace</span><span class="sxs-lookup"><span data-stu-id="676e9-125">Unique Id for hello marketplace charge item</span></span>|
|<span data-ttu-id="676e9-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="676e9-126">subscriptionGuid</span></span>|<span data-ttu-id="676e9-127">Guid</span><span class="sxs-lookup"><span data-stu-id="676e9-127">Guid</span></span>|<span data-ttu-id="676e9-128">Hello Guid подписки</span><span class="sxs-lookup"><span data-stu-id="676e9-128">hello Subscription Guid</span></span>|
|<span data-ttu-id="676e9-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="676e9-129">subscriptionName</span></span>|<span data-ttu-id="676e9-130">string</span><span class="sxs-lookup"><span data-stu-id="676e9-130">string</span></span>|<span data-ttu-id="676e9-131">Hello имя подписки</span><span class="sxs-lookup"><span data-stu-id="676e9-131">hello Subscription Name</span></span>|
|<span data-ttu-id="676e9-132">meterId</span><span class="sxs-lookup"><span data-stu-id="676e9-132">meterId</span></span>|<span data-ttu-id="676e9-133">string</span><span class="sxs-lookup"><span data-stu-id="676e9-133">string</span></span>|<span data-ttu-id="676e9-134">Идентификатор для hello создается индикатора</span><span class="sxs-lookup"><span data-stu-id="676e9-134">Id for hello emitted Meter</span></span>|
|<span data-ttu-id="676e9-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="676e9-135">usageStartDate</span></span>|<span data-ttu-id="676e9-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="676e9-136">DateTime</span></span>|<span data-ttu-id="676e9-137">Время начала для записи об использовании hello</span><span class="sxs-lookup"><span data-stu-id="676e9-137">Start time for hello usage record</span></span>|
|<span data-ttu-id="676e9-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="676e9-138">usageEndDate</span></span>|<span data-ttu-id="676e9-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="676e9-139">DateTime</span></span>|<span data-ttu-id="676e9-140">Время окончания для записи об использовании hello</span><span class="sxs-lookup"><span data-stu-id="676e9-140">End time for hello usage record</span></span>|
|<span data-ttu-id="676e9-141">offerName</span><span class="sxs-lookup"><span data-stu-id="676e9-141">offerName</span></span>|<span data-ttu-id="676e9-142">string</span><span class="sxs-lookup"><span data-stu-id="676e9-142">string</span></span>|<span data-ttu-id="676e9-143">имя предложения Hello</span><span class="sxs-lookup"><span data-stu-id="676e9-143">hello Offer name</span></span>|
|<span data-ttu-id="676e9-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="676e9-144">resourceGroup</span></span>|<span data-ttu-id="676e9-145">string</span><span class="sxs-lookup"><span data-stu-id="676e9-145">string</span></span>|<span data-ttu-id="676e9-146">Hello ресурсов группы</span><span class="sxs-lookup"><span data-stu-id="676e9-146">hello resource Group</span></span>|
|<span data-ttu-id="676e9-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="676e9-147">instanceId</span></span>|<span data-ttu-id="676e9-148">string</span><span class="sxs-lookup"><span data-stu-id="676e9-148">string</span></span>|<span data-ttu-id="676e9-149">Идентификатор экземпляра</span><span class="sxs-lookup"><span data-stu-id="676e9-149">Instance Id</span></span>|
|<span data-ttu-id="676e9-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="676e9-150">additionalInfo</span></span>|<span data-ttu-id="676e9-151">string</span><span class="sxs-lookup"><span data-stu-id="676e9-151">string</span></span>|<span data-ttu-id="676e9-152">Строка JSON с дополнительной информацией</span><span class="sxs-lookup"><span data-stu-id="676e9-152">Additional info JSON string</span></span>|
|<span data-ttu-id="676e9-153">tags</span><span class="sxs-lookup"><span data-stu-id="676e9-153">tags</span></span>|<span data-ttu-id="676e9-154">string</span><span class="sxs-lookup"><span data-stu-id="676e9-154">string</span></span>|<span data-ttu-id="676e9-155">Строка JSON с тегами</span><span class="sxs-lookup"><span data-stu-id="676e9-155">Tag JSON string</span></span>|
|<span data-ttu-id="676e9-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="676e9-156">orderNumber</span></span>|<span data-ttu-id="676e9-157">string</span><span class="sxs-lookup"><span data-stu-id="676e9-157">string</span></span>|<span data-ttu-id="676e9-158">Номер заказа Hello</span><span class="sxs-lookup"><span data-stu-id="676e9-158">hello order number</span></span>|
|<span data-ttu-id="676e9-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="676e9-159">unitOfMeasure</span></span>|<span data-ttu-id="676e9-160">string</span><span class="sxs-lookup"><span data-stu-id="676e9-160">string</span></span>|<span data-ttu-id="676e9-161">Единица измерения для индикатора hello</span><span class="sxs-lookup"><span data-stu-id="676e9-161">Unit of measure for hello meter</span></span>|
|<span data-ttu-id="676e9-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="676e9-162">costCenter</span></span>|<span data-ttu-id="676e9-163">string</span><span class="sxs-lookup"><span data-stu-id="676e9-163">string</span></span>|<span data-ttu-id="676e9-164">Центр затрат Hello</span><span class="sxs-lookup"><span data-stu-id="676e9-164">hello cost center</span></span>|
|<span data-ttu-id="676e9-165">accountId</span><span class="sxs-lookup"><span data-stu-id="676e9-165">accountId</span></span>|<span data-ttu-id="676e9-166">int</span><span class="sxs-lookup"><span data-stu-id="676e9-166">int</span></span>|<span data-ttu-id="676e9-167">Учетная запись Hello идентификатор</span><span class="sxs-lookup"><span data-stu-id="676e9-167">hello account Id</span></span>|
|<span data-ttu-id="676e9-168">accountName</span><span class="sxs-lookup"><span data-stu-id="676e9-168">accountName</span></span>|<span data-ttu-id="676e9-169">string</span><span class="sxs-lookup"><span data-stu-id="676e9-169">string</span></span> |<span data-ttu-id="676e9-170">Hello имя учетной записи</span><span class="sxs-lookup"><span data-stu-id="676e9-170">hello Account Name</span></span>|
|<span data-ttu-id="676e9-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="676e9-171">accountOwnerId</span></span>|<span data-ttu-id="676e9-172">string</span><span class="sxs-lookup"><span data-stu-id="676e9-172">string</span></span>|<span data-ttu-id="676e9-173">Hello идентификатор владельца учетной записи</span><span class="sxs-lookup"><span data-stu-id="676e9-173">hello Account Owner Id</span></span>|
|<span data-ttu-id="676e9-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="676e9-174">departmentId</span></span>|<span data-ttu-id="676e9-175">int</span><span class="sxs-lookup"><span data-stu-id="676e9-175">int</span></span>|<span data-ttu-id="676e9-176">отдел Hello идентификатор</span><span class="sxs-lookup"><span data-stu-id="676e9-176">hello department Id</span></span>|
|<span data-ttu-id="676e9-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="676e9-177">departmentName</span></span>|<span data-ttu-id="676e9-178">string</span><span class="sxs-lookup"><span data-stu-id="676e9-178">string</span></span>|<span data-ttu-id="676e9-179">Название отдела Hello</span><span class="sxs-lookup"><span data-stu-id="676e9-179">hello department name</span></span>|
|<span data-ttu-id="676e9-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="676e9-180">publisherName</span></span>|<span data-ttu-id="676e9-181">string</span><span class="sxs-lookup"><span data-stu-id="676e9-181">string</span></span>|<span data-ttu-id="676e9-182">Имя издателя Hello</span><span class="sxs-lookup"><span data-stu-id="676e9-182">hello publisher name</span></span>|
|<span data-ttu-id="676e9-183">planName</span><span class="sxs-lookup"><span data-stu-id="676e9-183">planName</span></span>|<span data-ttu-id="676e9-184">string</span><span class="sxs-lookup"><span data-stu-id="676e9-184">string</span></span>|<span data-ttu-id="676e9-185">Имя плана Hello</span><span class="sxs-lookup"><span data-stu-id="676e9-185">hello Plan name</span></span>|
|<span data-ttu-id="676e9-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="676e9-186">consumedQuantity</span></span>|<span data-ttu-id="676e9-187">decimal</span><span class="sxs-lookup"><span data-stu-id="676e9-187">decimal</span></span>|<span data-ttu-id="676e9-188">Потребленный объем за этот период времени</span><span class="sxs-lookup"><span data-stu-id="676e9-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="676e9-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="676e9-189">resourceRate</span></span>|<span data-ttu-id="676e9-190">decimal</span><span class="sxs-lookup"><span data-stu-id="676e9-190">decimal</span></span>|<span data-ttu-id="676e9-191">Цена единицы для индикатора hello</span><span class="sxs-lookup"><span data-stu-id="676e9-191">Unit price for hello meter</span></span>|
|<span data-ttu-id="676e9-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="676e9-192">extendedCost</span></span>|<span data-ttu-id="676e9-193">decimal</span><span class="sxs-lookup"><span data-stu-id="676e9-193">decimal</span></span>|<span data-ttu-id="676e9-194">Оценка расходов на основе потребленного объема и расширенных затрат</span><span class="sxs-lookup"><span data-stu-id="676e9-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="676e9-195">См. также</span><span class="sxs-lookup"><span data-stu-id="676e9-195">See also</span></span>

* [<span data-ttu-id="676e9-196">Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды</span><span class="sxs-lookup"><span data-stu-id="676e9-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="676e9-197">Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="676e9-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="676e9-198">Интерфейсы API отчетов для корпоративных клиентов: баланс и сводка</span><span class="sxs-lookup"><span data-stu-id="676e9-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="676e9-199">Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант</span><span class="sxs-lookup"><span data-stu-id="676e9-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)