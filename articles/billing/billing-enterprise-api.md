---
title: "Выставление счетов Enterprise API-интерфейсы aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="78fc7-103">Обзор API- интерфейсов отчетов для корпоративных клиентов</span><span class="sxs-lookup"><span data-stu-id="78fc7-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="78fc7-104">Hello Reporting API позволяют корпоративных клиентов tooprogrammatically запросу подписка Azure и выставления счетов в средства анализа предпочтительным.</span><span class="sxs-lookup"><span data-stu-id="78fc7-104">hello Reporting APIs enable Enterprise Azure customers tooprogrammatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-toohello-api"></a><span data-ttu-id="78fc7-105">Включение toohello API-Интерфейс</span><span class="sxs-lookup"><span data-stu-id="78fc7-105">Enabling data access toohello API</span></span>
* <span data-ttu-id="78fc7-106">**Создать или получить ключ hello API** - журнал toohello корпоративного портала и выполните hello учебника в разделе справки - API для сбора.</span><span class="sxs-lookup"><span data-stu-id="78fc7-106">**Generate or retrieve hello API key** - Log in toohello Enterprise portal and follow hello tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="78fc7-107">Hello первый раздел находится в этой справочной статье объясняется, как toogenerate или получить ключ hello API для hello указанном регистрации.</span><span class="sxs-lookup"><span data-stu-id="78fc7-107">hello first section under this help article explains how toogenerate or retrieve hello API key for hello specified enrollment.</span></span>
* <span data-ttu-id="78fc7-108">**Передача ключей в hello API** -hello API-ключ должен toobe, переданный для каждого вызова для проверки подлинности и авторизации.</span><span class="sxs-lookup"><span data-stu-id="78fc7-108">**Passing keys in hello API** - hello API key needs toobe passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="78fc7-109">Hello следующие свойства должны заголовки toohello HTTP toobe</span><span class="sxs-lookup"><span data-stu-id="78fc7-109">hello following property needs toobe toohello HTTP headers</span></span>

|<span data-ttu-id="78fc7-110">Ключ заголовка запроса</span><span class="sxs-lookup"><span data-stu-id="78fc7-110">Request Header Key</span></span> | <span data-ttu-id="78fc7-111">Значение</span><span class="sxs-lookup"><span data-stu-id="78fc7-111">Value</span></span>|
|-|-|
|<span data-ttu-id="78fc7-112">Авторизация</span><span class="sxs-lookup"><span data-stu-id="78fc7-112">Authorization</span></span>| <span data-ttu-id="78fc7-113">Укажите значение hello в следующем формате: **bearer {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="78fc7-113">Specify hello value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="78fc7-114">Пример: bearer eyr....09</span><span class="sxs-lookup"><span data-stu-id="78fc7-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="78fc7-115">Интерфейсы API потребления</span><span class="sxs-lookup"><span data-stu-id="78fc7-115">Consumption APIs</span></span>
<span data-ttu-id="78fc7-116">Доступен конечной точки Swagger [здесь](https://consumption.azure.com/swagger/ui/index) hello интерфейсов API, описанных ниже которого следует включить легко интроспекции hello API и hello возможность toogenerate клиентских SDK с помощью [AutoRest](https://github.com/Azure/AutoRest) или [ Swagger CodeGen](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="78fc7-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for hello APIs described below which should enable easy introspection of hello API and hello ability toogenerate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="78fc7-117">С 1 мая 2014 г. данные доступны через этот API.</span><span class="sxs-lookup"><span data-stu-id="78fc7-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="78fc7-118">**Сводка и баланс** - hello [баланс и Сводка API](billing-enterprise-api-balance-summary.md) предлагает ежемесячные сводку сведений о сальдо, новый покупок, плата за Azure Marketplace, корректировки и избыточные расходы.</span><span class="sxs-lookup"><span data-stu-id="78fc7-118">**Balance and Summary** - hello [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="78fc7-119">**Сведения об использовании** - hello [API сведений об использовании](billing-enterprise-api-usage-detail.md) предлагает ежедневного декомпозиция обрабатываемом количеств и оценка расходов по регистрации.</span><span class="sxs-lookup"><span data-stu-id="78fc7-119">**Usage Details** - hello [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="78fc7-120">результат Hello также содержатся сведения о экземпляров, показателей и отделах.</span><span class="sxs-lookup"><span data-stu-id="78fc7-120">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="78fc7-121">можно запрашивать Hello API периода выставления счетов или указанными датами начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="78fc7-121">hello API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="78fc7-122">**Издержки магазина Marketplace** - hello [API платы магазина Marketplace](billing-enterprise-api-marketplace-storecharge.md) возвращает декомпозиции расходов на основе использования marketplace hello за день для указанной hello период выставления счетов или даты начала и окончания (сборов за один раз, не включены) .</span><span class="sxs-lookup"><span data-stu-id="78fc7-122">**Marketplace Store Charge** - hello [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="78fc7-123">**Прайс-лист** - hello [цена лист API](billing-enterprise-api-pricesheet.md) предоставляет hello применимые скорость для каждого индикатора для регистрации и выставления счетов за период hello.</span><span class="sxs-lookup"><span data-stu-id="78fc7-123">**Price Sheet** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="78fc7-124">Интерфейсы API вспомогательного приложения</span><span class="sxs-lookup"><span data-stu-id="78fc7-124">Helper APIs</span></span>
 <span data-ttu-id="78fc7-125">**Список периодов выставления счетов** - hello [выставления счетов за периоды API](billing-enterprise-api-billing-periods.md) возвращает список периодов, которые имеют данные потребления для регистрации, указанной в обратном хронологическом порядке hello выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="78fc7-125">**List Billing Periods** - hello [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="78fc7-126">Для каждого периода содержит свойство, указывающее toohello API маршрута для hello четырех наборов данных - BalanceSummary, UsageDetails, о расходах в Marketplace и прайс-листа.</span><span class="sxs-lookup"><span data-stu-id="78fc7-126">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="78fc7-127">Коды ответов API</span><span class="sxs-lookup"><span data-stu-id="78fc7-127">API Response Codes</span></span>  
|<span data-ttu-id="78fc7-128">Код состояния отклика</span><span class="sxs-lookup"><span data-stu-id="78fc7-128">Response Status Code</span></span>|<span data-ttu-id="78fc7-129">Сообщение</span><span class="sxs-lookup"><span data-stu-id="78fc7-129">Message</span></span>|<span data-ttu-id="78fc7-130">Описание</span><span class="sxs-lookup"><span data-stu-id="78fc7-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="78fc7-131">200</span><span class="sxs-lookup"><span data-stu-id="78fc7-131">200</span></span>| <span data-ttu-id="78fc7-132">ОК</span><span class="sxs-lookup"><span data-stu-id="78fc7-132">OK</span></span>|<span data-ttu-id="78fc7-133">Без ошибок</span><span class="sxs-lookup"><span data-stu-id="78fc7-133">No error</span></span>|
|<span data-ttu-id="78fc7-134">401</span><span class="sxs-lookup"><span data-stu-id="78fc7-134">401</span></span>| <span data-ttu-id="78fc7-135">Не авторизовано</span><span class="sxs-lookup"><span data-stu-id="78fc7-135">Unauthorized</span></span>| <span data-ttu-id="78fc7-136">Ключ API не найден, недопустимый формат, срок действия истек и т. д.</span><span class="sxs-lookup"><span data-stu-id="78fc7-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="78fc7-137">404</span><span class="sxs-lookup"><span data-stu-id="78fc7-137">404</span></span>| <span data-ttu-id="78fc7-138">Рекомендации недоступны</span><span class="sxs-lookup"><span data-stu-id="78fc7-138">Unavailable</span></span>| <span data-ttu-id="78fc7-139">Не найдена конечная точка отчетов</span><span class="sxs-lookup"><span data-stu-id="78fc7-139">Report endpoint not found</span></span>|
|<span data-ttu-id="78fc7-140">400</span><span class="sxs-lookup"><span data-stu-id="78fc7-140">400</span></span>| <span data-ttu-id="78fc7-141">Ошибка запроса</span><span class="sxs-lookup"><span data-stu-id="78fc7-141">Bad Request</span></span>| <span data-ttu-id="78fc7-142">Недопустимые параметры — диапазоны дат, числа EA и т. д.</span><span class="sxs-lookup"><span data-stu-id="78fc7-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="78fc7-143">500</span><span class="sxs-lookup"><span data-stu-id="78fc7-143">500</span></span>| <span data-ttu-id="78fc7-144">Ошибка сервера</span><span class="sxs-lookup"><span data-stu-id="78fc7-144">Server Error</span></span>| <span data-ttu-id="78fc7-145">Непредвиденная ошибка при обработке запроса</span><span class="sxs-lookup"><span data-stu-id="78fc7-145">Unexoected error processing request</span></span>| 









