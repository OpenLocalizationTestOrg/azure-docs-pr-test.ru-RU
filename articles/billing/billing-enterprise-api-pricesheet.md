---
title: "Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант | Документация Майкрософт"
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
ms.openlocfilehash: 2e7d6e883abe4cee13bc5f684baf2a1ea9c6c397
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="2fe21-103">API-интерфейсы отчетов для корпоративных клиентов: прейскурант</span><span class="sxs-lookup"><span data-stu-id="2fe21-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="2fe21-104">API прейскуранта предоставляет соответствующий тариф для каждой метрики в отдельной регистрации и за определенный расчетный период.</span><span class="sxs-lookup"><span data-stu-id="2fe21-104">The Price Sheet API provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="2fe21-105">Запрос</span><span class="sxs-lookup"><span data-stu-id="2fe21-105">Request</span></span>
<span data-ttu-id="2fe21-106">Общие свойства заголовка, которые необходимо добавить, указываются [здесь](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="2fe21-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="2fe21-107">Если расчетный период не указан, то возвращаются данные за текущий расчетный период.</span><span class="sxs-lookup"><span data-stu-id="2fe21-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="2fe21-108">Метод</span><span class="sxs-lookup"><span data-stu-id="2fe21-108">Method</span></span> | <span data-ttu-id="2fe21-109">URI запроса</span><span class="sxs-lookup"><span data-stu-id="2fe21-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="2fe21-110">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="2fe21-110">GET</span></span>|<span data-ttu-id="2fe21-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="2fe21-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="2fe21-112">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="2fe21-112">GET</span></span>|<span data-ttu-id="2fe21-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="2fe21-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="2fe21-114">Чтобы использовать предварительную версию API, измените v2 на v1 в URL-адресе выше.</span><span class="sxs-lookup"><span data-stu-id="2fe21-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="2fe21-115">Ответ</span><span class="sxs-lookup"><span data-stu-id="2fe21-115">Response</span></span>

    
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
><span data-ttu-id="2fe21-116">Если вы используете API предварительной версии, поле meterId недоступно.</span><span class="sxs-lookup"><span data-stu-id="2fe21-116">If you are using the Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="2fe21-117">**Определения свойств ответа**</span><span class="sxs-lookup"><span data-stu-id="2fe21-117">**Response property definitions**</span></span>

|<span data-ttu-id="2fe21-118">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="2fe21-118">Property Name</span></span>| <span data-ttu-id="2fe21-119">Тип</span><span class="sxs-lookup"><span data-stu-id="2fe21-119">Type</span></span>| <span data-ttu-id="2fe21-120">Описание</span><span class="sxs-lookup"><span data-stu-id="2fe21-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="2fe21-121">id</span><span class="sxs-lookup"><span data-stu-id="2fe21-121">id</span></span>| <span data-ttu-id="2fe21-122">string</span><span class="sxs-lookup"><span data-stu-id="2fe21-122">string</span></span>| <span data-ttu-id="2fe21-123">Уникальный идентификатор, представляющий определенный элемент PriceSheet (метрика за расчетный период)</span><span class="sxs-lookup"><span data-stu-id="2fe21-123">The unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="2fe21-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="2fe21-124">billingPeriodId</span></span>| <span data-ttu-id="2fe21-125">string</span><span class="sxs-lookup"><span data-stu-id="2fe21-125">string</span></span>| <span data-ttu-id="2fe21-126">Уникальный идентификатор, представляющий определенный расчетный период</span><span class="sxs-lookup"><span data-stu-id="2fe21-126">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="2fe21-127">meterId</span><span class="sxs-lookup"><span data-stu-id="2fe21-127">meterId</span></span>| <span data-ttu-id="2fe21-128">string</span><span class="sxs-lookup"><span data-stu-id="2fe21-128">string</span></span>| <span data-ttu-id="2fe21-129">Идентификатор средства измерения.</span><span class="sxs-lookup"><span data-stu-id="2fe21-129">The identifier for the meter.</span></span> <span data-ttu-id="2fe21-130">Может сопоставляться с идентификатором meterId использования.</span><span class="sxs-lookup"><span data-stu-id="2fe21-130">It can be mapped to the usage meterId.</span></span>|
|<span data-ttu-id="2fe21-131">meterName</span><span class="sxs-lookup"><span data-stu-id="2fe21-131">meterName</span></span>| <span data-ttu-id="2fe21-132">string</span><span class="sxs-lookup"><span data-stu-id="2fe21-132">string</span></span>| <span data-ttu-id="2fe21-133">Имя метрики</span><span class="sxs-lookup"><span data-stu-id="2fe21-133">The meter name</span></span>|
|<span data-ttu-id="2fe21-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="2fe21-134">unitOfMeasure</span></span>| <span data-ttu-id="2fe21-135">string</span><span class="sxs-lookup"><span data-stu-id="2fe21-135">string</span></span>| <span data-ttu-id="2fe21-136">Единица измерения для измерения службы</span><span class="sxs-lookup"><span data-stu-id="2fe21-136">The Unit of Measure for measuring the service</span></span>|
|<span data-ttu-id="2fe21-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="2fe21-137">includedQuantity</span></span>| <span data-ttu-id="2fe21-138">decimal</span><span class="sxs-lookup"><span data-stu-id="2fe21-138">decimal</span></span>| <span data-ttu-id="2fe21-139">Количество, которое включено</span><span class="sxs-lookup"><span data-stu-id="2fe21-139">Quantity that is included</span></span> |
|<span data-ttu-id="2fe21-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="2fe21-140">partNumber</span></span>| <span data-ttu-id="2fe21-141">string</span><span class="sxs-lookup"><span data-stu-id="2fe21-141">string</span></span>| <span data-ttu-id="2fe21-142">Артикул, связанный со метрикой</span><span class="sxs-lookup"><span data-stu-id="2fe21-142">The part number associated with the Meter</span></span>|
|<span data-ttu-id="2fe21-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="2fe21-143">unitPrice</span></span>| <span data-ttu-id="2fe21-144">decimal</span><span class="sxs-lookup"><span data-stu-id="2fe21-144">decimal</span></span>| <span data-ttu-id="2fe21-145">Цена единицы измерения для метрики</span><span class="sxs-lookup"><span data-stu-id="2fe21-145">The unit price for the meter</span></span>|
|<span data-ttu-id="2fe21-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="2fe21-146">currencyCode</span></span>| <span data-ttu-id="2fe21-147">string</span><span class="sxs-lookup"><span data-stu-id="2fe21-147">string</span></span>| <span data-ttu-id="2fe21-148">Код валюты для unitPrice</span><span class="sxs-lookup"><span data-stu-id="2fe21-148">The currency code for the unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="2fe21-149">См. также</span><span class="sxs-lookup"><span data-stu-id="2fe21-149">See also</span></span>

* [<span data-ttu-id="2fe21-150">Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды</span><span class="sxs-lookup"><span data-stu-id="2fe21-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="2fe21-151">Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="2fe21-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="2fe21-152">Интерфейсы API отчетов для корпоративных клиентов: баланс и сводка</span><span class="sxs-lookup"><span data-stu-id="2fe21-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="2fe21-153">Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace</span><span class="sxs-lookup"><span data-stu-id="2fe21-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
