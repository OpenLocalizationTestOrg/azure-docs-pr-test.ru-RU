---
title: "Интерфейсы API для выставления счетов Azure корпоративным клиентам: баланс и сводка | Документация Майкрософт"
description: "Сведения об интерфейсах API использования и RateCard для выставления счетов Azure, которые применяются для получения ценных сведений о потреблении ресурсов Azure и соответствующих тенденциях."
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
ms.openlocfilehash: f6b149f0e656d2263705048aa5b644f5bb4a5712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="7f9c9-103">API-интерфейсы отчетов для корпоративных клиентов: баланс и сводка</span><span class="sxs-lookup"><span data-stu-id="7f9c9-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="7f9c9-104">API-интерфейс для управления балансом предоставляет ежемесячную сводку о состоянии баланса, новых покупках, расходах на службы Azure Marketplace, корректировках и взимании платы за превышение.</span><span class="sxs-lookup"><span data-stu-id="7f9c9-104">The Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="7f9c9-105">Запрос</span><span class="sxs-lookup"><span data-stu-id="7f9c9-105">Request</span></span> 
<span data-ttu-id="7f9c9-106">Общие свойства заголовка, которые необходимо добавить, указываются [здесь](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="7f9c9-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="7f9c9-107">Если расчетный период не указан, то возвращаются данные за текущий расчетный период.</span><span class="sxs-lookup"><span data-stu-id="7f9c9-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="7f9c9-108">Метод</span><span class="sxs-lookup"><span data-stu-id="7f9c9-108">Method</span></span> | <span data-ttu-id="7f9c9-109">URI запроса</span><span class="sxs-lookup"><span data-stu-id="7f9c9-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="7f9c9-110">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="7f9c9-110">GET</span></span>| <span data-ttu-id="7f9c9-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="7f9c9-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="7f9c9-112">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="7f9c9-112">GET</span></span>| <span data-ttu-id="7f9c9-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="7f9c9-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="7f9c9-114">Чтобы использовать предварительную версию API, измените v2 на v1 в URL-адресе выше.</span><span class="sxs-lookup"><span data-stu-id="7f9c9-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="7f9c9-115">Ответ</span><span class="sxs-lookup"><span data-stu-id="7f9c9-115">Response</span></span>

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


<span data-ttu-id="7f9c9-116">**Определения свойств ответа**</span><span class="sxs-lookup"><span data-stu-id="7f9c9-116">**Response property definitions**</span></span>

|<span data-ttu-id="7f9c9-117">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="7f9c9-117">Property Name</span></span>| <span data-ttu-id="7f9c9-118">Тип</span><span class="sxs-lookup"><span data-stu-id="7f9c9-118">Type</span></span>| <span data-ttu-id="7f9c9-119">Описание</span><span class="sxs-lookup"><span data-stu-id="7f9c9-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="7f9c9-120">id</span><span class="sxs-lookup"><span data-stu-id="7f9c9-120">id</span></span>|<span data-ttu-id="7f9c9-121">string</span><span class="sxs-lookup"><span data-stu-id="7f9c9-121">string</span></span>|<span data-ttu-id="7f9c9-122">Уникальный идентификатор для определенного расчетного периода и регистрации</span><span class="sxs-lookup"><span data-stu-id="7f9c9-122">The unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="7f9c9-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="7f9c9-123">billingPeriodId</span></span>|<span data-ttu-id="7f9c9-124">string</span><span class="sxs-lookup"><span data-stu-id="7f9c9-124">string</span></span> |<span data-ttu-id="7f9c9-125">Идентификатор расчетного периода</span><span class="sxs-lookup"><span data-stu-id="7f9c9-125">The billing period Id</span></span>|
|<span data-ttu-id="7f9c9-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="7f9c9-126">currencyCode</span></span>|<span data-ttu-id="7f9c9-127">string</span><span class="sxs-lookup"><span data-stu-id="7f9c9-127">string</span></span> |<span data-ttu-id="7f9c9-128">Код валюты</span><span class="sxs-lookup"><span data-stu-id="7f9c9-128">The currency code</span></span>|
|<span data-ttu-id="7f9c9-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="7f9c9-129">beginningBalance</span></span>|<span data-ttu-id="7f9c9-130">decimal</span><span class="sxs-lookup"><span data-stu-id="7f9c9-130">decimal</span></span>| <span data-ttu-id="7f9c9-131">Начальный баланс для расчетного периода</span><span class="sxs-lookup"><span data-stu-id="7f9c9-131">The beginning balance for the billing period</span></span>|
|<span data-ttu-id="7f9c9-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="7f9c9-132">endingBalance</span></span>|<span data-ttu-id="7f9c9-133">decimal</span><span class="sxs-lookup"><span data-stu-id="7f9c9-133">decimal</span></span>| <span data-ttu-id="7f9c9-134">Конечное сальдо для расчетного периода (для открытых периодов это значение обновляется ежедневно)</span><span class="sxs-lookup"><span data-stu-id="7f9c9-134">The ending balance for the billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="7f9c9-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="7f9c9-135">newPurchases</span></span>|<span data-ttu-id="7f9c9-136">decimal</span><span class="sxs-lookup"><span data-stu-id="7f9c9-136">decimal</span></span>| <span data-ttu-id="7f9c9-137">Общая сумма новой покупки</span><span class="sxs-lookup"><span data-stu-id="7f9c9-137">Total new purchase amount</span></span>|
|<span data-ttu-id="7f9c9-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="7f9c9-138">adjustments</span></span>|<span data-ttu-id="7f9c9-139">decimal</span><span class="sxs-lookup"><span data-stu-id="7f9c9-139">decimal</span></span>| <span data-ttu-id="7f9c9-140">Общая сумма корректировки</span><span class="sxs-lookup"><span data-stu-id="7f9c9-140">Total adjustment amount</span></span>|
|<span data-ttu-id="7f9c9-141">utilized</span><span class="sxs-lookup"><span data-stu-id="7f9c9-141">utilized</span></span>|<span data-ttu-id="7f9c9-142">decimal</span><span class="sxs-lookup"><span data-stu-id="7f9c9-142">decimal</span></span>| <span data-ttu-id="7f9c9-143">Общая сумма обязательств</span><span class="sxs-lookup"><span data-stu-id="7f9c9-143">Total Commitment usage</span></span>|
|<span data-ttu-id="7f9c9-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="7f9c9-144">serviceOverage</span></span>|<span data-ttu-id="7f9c9-145">decimal</span><span class="sxs-lookup"><span data-stu-id="7f9c9-145">decimal</span></span>| <span data-ttu-id="7f9c9-146">Превышение использования служб Azure</span><span class="sxs-lookup"><span data-stu-id="7f9c9-146">Overage for Azure services</span></span>|
|<span data-ttu-id="7f9c9-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="7f9c9-147">chargesBilledSeparately</span></span>|<span data-ttu-id="7f9c9-148">decimal</span><span class="sxs-lookup"><span data-stu-id="7f9c9-148">decimal</span></span>| <span data-ttu-id="7f9c9-149">Счета, выставляемые отдельно</span><span class="sxs-lookup"><span data-stu-id="7f9c9-149">Charges Billed separately</span></span>|
|<span data-ttu-id="7f9c9-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="7f9c9-150">totalOverage</span></span>|<span data-ttu-id="7f9c9-151">decimal</span><span class="sxs-lookup"><span data-stu-id="7f9c9-151">decimal</span></span>| <span data-ttu-id="7f9c9-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="7f9c9-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="7f9c9-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="7f9c9-153">totalUsage</span></span>|<span data-ttu-id="7f9c9-154">decimal</span><span class="sxs-lookup"><span data-stu-id="7f9c9-154">decimal</span></span>| <span data-ttu-id="7f9c9-155">Обязательства по службам Azure + totalOverage</span><span class="sxs-lookup"><span data-stu-id="7f9c9-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="7f9c9-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="7f9c9-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="7f9c9-157">decimal</span><span class="sxs-lookup"><span data-stu-id="7f9c9-157">decimal</span></span>| <span data-ttu-id="7f9c9-158">Общая сумма платежей за использование Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="7f9c9-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="7f9c9-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="7f9c9-159">newPurchasesDetails</span></span>|<span data-ttu-id="7f9c9-160">Массив строк JSON из пар "имя-значение"</span><span class="sxs-lookup"><span data-stu-id="7f9c9-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="7f9c9-161">Список новых покупок</span><span class="sxs-lookup"><span data-stu-id="7f9c9-161">List of new purchases</span></span>|
|<span data-ttu-id="7f9c9-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="7f9c9-162">adjustmentDetails</span></span>|<span data-ttu-id="7f9c9-163">Массив строк JSON из пар "имя-значение"</span><span class="sxs-lookup"><span data-stu-id="7f9c9-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="7f9c9-164">Список корректировок (акционный кредит, кредит SIE и т. д.)</span><span class="sxs-lookup"><span data-stu-id="7f9c9-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="7f9c9-165">См. также</span><span class="sxs-lookup"><span data-stu-id="7f9c9-165">See also</span></span>

* [<span data-ttu-id="7f9c9-166">Интерфейсы API для выставления счетов Azure корпоративным клиентам: расчетные периоды</span><span class="sxs-lookup"><span data-stu-id="7f9c9-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="7f9c9-167">Интерфейсы API для выставления счетов Azure корпоративным клиентам: сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="7f9c9-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="7f9c9-168">Интерфейсы API для выставления счетов Azure корпоративным клиентам: платежи в Marketplace</span><span class="sxs-lookup"><span data-stu-id="7f9c9-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="7f9c9-169">Интерфейсы API для выставления счетов Azure корпоративным клиентам: прейскурант</span><span class="sxs-lookup"><span data-stu-id="7f9c9-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)