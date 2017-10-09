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
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="fbfb8-103">API-интерфейсы отчетов для корпоративных клиентов: прейскурант</span><span class="sxs-lookup"><span data-stu-id="fbfb8-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="fbfb8-104">Hello цена лист API предоставляет соответствующему курсу hello для каждого индикатора для регистрации и выставления счетов за период hello.</span><span class="sxs-lookup"><span data-stu-id="fbfb8-104">hello Price Sheet API provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="fbfb8-105">Запрос</span><span class="sxs-lookup"><span data-stu-id="fbfb8-105">Request</span></span>
<span data-ttu-id="fbfb8-106">Задаются общие свойства заголовка, которые необходимо добавить toobe [здесь](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="fbfb8-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="fbfb8-107">Если периода выставления счетов не указан, данные для выставления счетов hello для текущего периода возвращается.</span><span class="sxs-lookup"><span data-stu-id="fbfb8-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="fbfb8-108">Метод</span><span class="sxs-lookup"><span data-stu-id="fbfb8-108">Method</span></span> | <span data-ttu-id="fbfb8-109">URI запроса</span><span class="sxs-lookup"><span data-stu-id="fbfb8-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="fbfb8-110">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="fbfb8-110">GET</span></span>|<span data-ttu-id="fbfb8-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="fbfb8-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="fbfb8-112">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="fbfb8-112">GET</span></span>|<span data-ttu-id="fbfb8-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="fbfb8-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="fbfb8-114">toouse hello предварительную версию API, замените v2 v1 в hello выше URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="fbfb8-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="fbfb8-115">Ответ</span><span class="sxs-lookup"><span data-stu-id="fbfb8-115">Response</span></span>

    
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
><span data-ttu-id="fbfb8-116">Если вы используете hello API предварительной версии, meterId поле недоступно.</span><span class="sxs-lookup"><span data-stu-id="fbfb8-116">If you are using hello Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="fbfb8-117">**Определения свойств ответа**</span><span class="sxs-lookup"><span data-stu-id="fbfb8-117">**Response property definitions**</span></span>

|<span data-ttu-id="fbfb8-118">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="fbfb8-118">Property Name</span></span>| <span data-ttu-id="fbfb8-119">Тип</span><span class="sxs-lookup"><span data-stu-id="fbfb8-119">Type</span></span>| <span data-ttu-id="fbfb8-120">Описание</span><span class="sxs-lookup"><span data-stu-id="fbfb8-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="fbfb8-121">id</span><span class="sxs-lookup"><span data-stu-id="fbfb8-121">id</span></span>| <span data-ttu-id="fbfb8-122">string</span><span class="sxs-lookup"><span data-stu-id="fbfb8-122">string</span></span>| <span data-ttu-id="fbfb8-123">Hello уникальный идентификатор, представляющий определенный элемент PriceSheet (индикатор, расчетный период)</span><span class="sxs-lookup"><span data-stu-id="fbfb8-123">hello unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="fbfb8-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="fbfb8-124">billingPeriodId</span></span>| <span data-ttu-id="fbfb8-125">string</span><span class="sxs-lookup"><span data-stu-id="fbfb8-125">string</span></span>| <span data-ttu-id="fbfb8-126">Hello уникальный идентификатор, представляющий определенного периода выставления счетов</span><span class="sxs-lookup"><span data-stu-id="fbfb8-126">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="fbfb8-127">meterId</span><span class="sxs-lookup"><span data-stu-id="fbfb8-127">meterId</span></span>| <span data-ttu-id="fbfb8-128">string</span><span class="sxs-lookup"><span data-stu-id="fbfb8-128">string</span></span>| <span data-ttu-id="fbfb8-129">Идентификатор Hello индикатор hello.</span><span class="sxs-lookup"><span data-stu-id="fbfb8-129">hello identifier for hello meter.</span></span> <span data-ttu-id="fbfb8-130">Это может быть meterId сопоставленных toohello использования.</span><span class="sxs-lookup"><span data-stu-id="fbfb8-130">It can be mapped toohello usage meterId.</span></span>|
|<span data-ttu-id="fbfb8-131">meterName</span><span class="sxs-lookup"><span data-stu-id="fbfb8-131">meterName</span></span>| <span data-ttu-id="fbfb8-132">string</span><span class="sxs-lookup"><span data-stu-id="fbfb8-132">string</span></span>| <span data-ttu-id="fbfb8-133">имя индикатора Hello</span><span class="sxs-lookup"><span data-stu-id="fbfb8-133">hello meter name</span></span>|
|<span data-ttu-id="fbfb8-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="fbfb8-134">unitOfMeasure</span></span>| <span data-ttu-id="fbfb8-135">string</span><span class="sxs-lookup"><span data-stu-id="fbfb8-135">string</span></span>| <span data-ttu-id="fbfb8-136">Hello единица измерения для измерения службы hello</span><span class="sxs-lookup"><span data-stu-id="fbfb8-136">hello Unit of Measure for measuring hello service</span></span>|
|<span data-ttu-id="fbfb8-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="fbfb8-137">includedQuantity</span></span>| <span data-ttu-id="fbfb8-138">decimal</span><span class="sxs-lookup"><span data-stu-id="fbfb8-138">decimal</span></span>| <span data-ttu-id="fbfb8-139">Количество, которое включено</span><span class="sxs-lookup"><span data-stu-id="fbfb8-139">Quantity that is included</span></span> |
|<span data-ttu-id="fbfb8-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="fbfb8-140">partNumber</span></span>| <span data-ttu-id="fbfb8-141">string</span><span class="sxs-lookup"><span data-stu-id="fbfb8-141">string</span></span>| <span data-ttu-id="fbfb8-142">Номер части Hello, связанный с hello индикатора</span><span class="sxs-lookup"><span data-stu-id="fbfb8-142">hello part number associated with hello Meter</span></span>|
|<span data-ttu-id="fbfb8-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="fbfb8-143">unitPrice</span></span>| <span data-ttu-id="fbfb8-144">decimal</span><span class="sxs-lookup"><span data-stu-id="fbfb8-144">decimal</span></span>| <span data-ttu-id="fbfb8-145">Hello цену за единицу для индикатора hello</span><span class="sxs-lookup"><span data-stu-id="fbfb8-145">hello unit price for hello meter</span></span>|
|<span data-ttu-id="fbfb8-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="fbfb8-146">currencyCode</span></span>| <span data-ttu-id="fbfb8-147">string</span><span class="sxs-lookup"><span data-stu-id="fbfb8-147">string</span></span>| <span data-ttu-id="fbfb8-148">Код валюты Hello hello unitPrice</span><span class="sxs-lookup"><span data-stu-id="fbfb8-148">hello currency code for hello unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="fbfb8-149">См. также</span><span class="sxs-lookup"><span data-stu-id="fbfb8-149">See also</span></span>

* [<span data-ttu-id="fbfb8-150">Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды</span><span class="sxs-lookup"><span data-stu-id="fbfb8-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="fbfb8-151">Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="fbfb8-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="fbfb8-152">Интерфейсы API отчетов для корпоративных клиентов: баланс и сводка</span><span class="sxs-lookup"><span data-stu-id="fbfb8-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="fbfb8-153">Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace</span><span class="sxs-lookup"><span data-stu-id="fbfb8-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
