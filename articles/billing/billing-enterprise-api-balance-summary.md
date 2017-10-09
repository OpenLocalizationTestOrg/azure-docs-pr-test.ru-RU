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
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="d367a-103">API-интерфейсы отчетов для корпоративных клиентов: баланс и сводка</span><span class="sxs-lookup"><span data-stu-id="d367a-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="d367a-104">Hello баланс и Сводка API предоставляет ежемесячные сводку сведений о сальдо, новый покупок, плата за Azure Marketplace, корректировки и избыточные расходы.</span><span class="sxs-lookup"><span data-stu-id="d367a-104">hello Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="d367a-105">Запрос</span><span class="sxs-lookup"><span data-stu-id="d367a-105">Request</span></span> 
<span data-ttu-id="d367a-106">Задаются общие свойства заголовка, которые необходимо добавить toobe [здесь](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="d367a-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="d367a-107">Если периода выставления счетов не указан, данные для выставления счетов hello для текущего периода возвращается.</span><span class="sxs-lookup"><span data-stu-id="d367a-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="d367a-108">Метод</span><span class="sxs-lookup"><span data-stu-id="d367a-108">Method</span></span> | <span data-ttu-id="d367a-109">URI запроса</span><span class="sxs-lookup"><span data-stu-id="d367a-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="d367a-110">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="d367a-110">GET</span></span>| <span data-ttu-id="d367a-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="d367a-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="d367a-112">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="d367a-112">GET</span></span>| <span data-ttu-id="d367a-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="d367a-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="d367a-114">toouse hello предварительную версию API, замените v2 v1 в hello выше URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d367a-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="d367a-115">Ответ</span><span class="sxs-lookup"><span data-stu-id="d367a-115">Response</span></span>

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


<span data-ttu-id="d367a-116">**Определения свойств ответа**</span><span class="sxs-lookup"><span data-stu-id="d367a-116">**Response property definitions**</span></span>

|<span data-ttu-id="d367a-117">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="d367a-117">Property Name</span></span>| <span data-ttu-id="d367a-118">Тип</span><span class="sxs-lookup"><span data-stu-id="d367a-118">Type</span></span>| <span data-ttu-id="d367a-119">Описание</span><span class="sxs-lookup"><span data-stu-id="d367a-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="d367a-120">id</span><span class="sxs-lookup"><span data-stu-id="d367a-120">id</span></span>|<span data-ttu-id="d367a-121">string</span><span class="sxs-lookup"><span data-stu-id="d367a-121">string</span></span>|<span data-ttu-id="d367a-122">Hello уникальный идентификатор для определенного периода выставления счетов и регистрации</span><span class="sxs-lookup"><span data-stu-id="d367a-122">hello unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="d367a-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="d367a-123">billingPeriodId</span></span>|<span data-ttu-id="d367a-124">string</span><span class="sxs-lookup"><span data-stu-id="d367a-124">string</span></span> |<span data-ttu-id="d367a-125">Привет, код периода выставления счетов</span><span class="sxs-lookup"><span data-stu-id="d367a-125">hello billing period Id</span></span>|
|<span data-ttu-id="d367a-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="d367a-126">currencyCode</span></span>|<span data-ttu-id="d367a-127">string</span><span class="sxs-lookup"><span data-stu-id="d367a-127">string</span></span> |<span data-ttu-id="d367a-128">Код валюты Hello</span><span class="sxs-lookup"><span data-stu-id="d367a-128">hello currency code</span></span>|
|<span data-ttu-id="d367a-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="d367a-129">beginningBalance</span></span>|<span data-ttu-id="d367a-130">decimal</span><span class="sxs-lookup"><span data-stu-id="d367a-130">decimal</span></span>| <span data-ttu-id="d367a-131">Начальное сальдо Hello hello цикл выставления счетов</span><span class="sxs-lookup"><span data-stu-id="d367a-131">hello beginning balance for hello billing period</span></span>|
|<span data-ttu-id="d367a-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="d367a-132">endingBalance</span></span>|<span data-ttu-id="d367a-133">decimal</span><span class="sxs-lookup"><span data-stu-id="d367a-133">decimal</span></span>| <span data-ttu-id="d367a-134">Привет, конечное сальдо периода выставления счетов hello (для открытых периодов, это будет обновляться ежедневно)</span><span class="sxs-lookup"><span data-stu-id="d367a-134">hello ending balance for hello billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="d367a-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="d367a-135">newPurchases</span></span>|<span data-ttu-id="d367a-136">decimal</span><span class="sxs-lookup"><span data-stu-id="d367a-136">decimal</span></span>| <span data-ttu-id="d367a-137">Общая сумма новой покупки</span><span class="sxs-lookup"><span data-stu-id="d367a-137">Total new purchase amount</span></span>|
|<span data-ttu-id="d367a-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="d367a-138">adjustments</span></span>|<span data-ttu-id="d367a-139">decimal</span><span class="sxs-lookup"><span data-stu-id="d367a-139">decimal</span></span>| <span data-ttu-id="d367a-140">Общая сумма корректировки</span><span class="sxs-lookup"><span data-stu-id="d367a-140">Total adjustment amount</span></span>|
|<span data-ttu-id="d367a-141">utilized</span><span class="sxs-lookup"><span data-stu-id="d367a-141">utilized</span></span>|<span data-ttu-id="d367a-142">decimal</span><span class="sxs-lookup"><span data-stu-id="d367a-142">decimal</span></span>| <span data-ttu-id="d367a-143">Общая сумма обязательств</span><span class="sxs-lookup"><span data-stu-id="d367a-143">Total Commitment usage</span></span>|
|<span data-ttu-id="d367a-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="d367a-144">serviceOverage</span></span>|<span data-ttu-id="d367a-145">decimal</span><span class="sxs-lookup"><span data-stu-id="d367a-145">decimal</span></span>| <span data-ttu-id="d367a-146">Превышение использования служб Azure</span><span class="sxs-lookup"><span data-stu-id="d367a-146">Overage for Azure services</span></span>|
|<span data-ttu-id="d367a-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="d367a-147">chargesBilledSeparately</span></span>|<span data-ttu-id="d367a-148">decimal</span><span class="sxs-lookup"><span data-stu-id="d367a-148">decimal</span></span>| <span data-ttu-id="d367a-149">Счета, выставляемые отдельно</span><span class="sxs-lookup"><span data-stu-id="d367a-149">Charges Billed separately</span></span>|
|<span data-ttu-id="d367a-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="d367a-150">totalOverage</span></span>|<span data-ttu-id="d367a-151">decimal</span><span class="sxs-lookup"><span data-stu-id="d367a-151">decimal</span></span>| <span data-ttu-id="d367a-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="d367a-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="d367a-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="d367a-153">totalUsage</span></span>|<span data-ttu-id="d367a-154">decimal</span><span class="sxs-lookup"><span data-stu-id="d367a-154">decimal</span></span>| <span data-ttu-id="d367a-155">Обязательства по службам Azure + totalOverage</span><span class="sxs-lookup"><span data-stu-id="d367a-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="d367a-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="d367a-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="d367a-157">decimal</span><span class="sxs-lookup"><span data-stu-id="d367a-157">decimal</span></span>| <span data-ttu-id="d367a-158">Общая сумма платежей за использование Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="d367a-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="d367a-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="d367a-159">newPurchasesDetails</span></span>|<span data-ttu-id="d367a-160">Массив строк JSON из пар "имя-значение"</span><span class="sxs-lookup"><span data-stu-id="d367a-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="d367a-161">Список новых покупок</span><span class="sxs-lookup"><span data-stu-id="d367a-161">List of new purchases</span></span>|
|<span data-ttu-id="d367a-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="d367a-162">adjustmentDetails</span></span>|<span data-ttu-id="d367a-163">Массив строк JSON из пар "имя-значение"</span><span class="sxs-lookup"><span data-stu-id="d367a-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="d367a-164">Список корректировок (акционный кредит, кредит SIE и т. д.)</span><span class="sxs-lookup"><span data-stu-id="d367a-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="d367a-165">См. также</span><span class="sxs-lookup"><span data-stu-id="d367a-165">See also</span></span>

* [<span data-ttu-id="d367a-166">Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды</span><span class="sxs-lookup"><span data-stu-id="d367a-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="d367a-167">Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="d367a-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="d367a-168">Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace</span><span class="sxs-lookup"><span data-stu-id="d367a-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="d367a-169">Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант</span><span class="sxs-lookup"><span data-stu-id="d367a-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)