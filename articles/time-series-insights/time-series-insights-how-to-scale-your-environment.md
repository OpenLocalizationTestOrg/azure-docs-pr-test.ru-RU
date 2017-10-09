---
title: "aaaHow tooscale среды аналитики ряда времени Azure | Документы Microsoft"
description: "В этом учебнике описано как tooscale среды Azure Insights ряда времени"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a><span data-ttu-id="fb84b-103">Как tooscale среды времени серии аналитики</span><span class="sxs-lookup"><span data-stu-id="fb84b-103">How tooscale your Time Series Insights environment</span></span>

<span data-ttu-id="fb84b-104">В этом учебнике описано как tooscale среды аналитики ряда времени.</span><span class="sxs-lookup"><span data-stu-id="fb84b-104">This tutorial covers how tooscale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="fb84b-105">Увеличение масштаба в разных номерах SKU запрещено.</span><span class="sxs-lookup"><span data-stu-id="fb84b-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="fb84b-106">Среду с номером SKU S1 нельзя преобразовать в среду S2.</span><span class="sxs-lookup"><span data-stu-id="fb84b-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="fb84b-107">Скорость приема и емкость номера SKU S1</span><span class="sxs-lookup"><span data-stu-id="fb84b-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="fb84b-108">Емкость номера SKU S1</span><span class="sxs-lookup"><span data-stu-id="fb84b-108">S1 SKU Capacity</span></span> | <span data-ttu-id="fb84b-109">Скорость приема</span><span class="sxs-lookup"><span data-stu-id="fb84b-109">Ingress Rate</span></span> | <span data-ttu-id="fb84b-110">Максимальная емкость хранилища</span><span class="sxs-lookup"><span data-stu-id="fb84b-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="fb84b-111">1</span><span class="sxs-lookup"><span data-stu-id="fb84b-111">1</span></span> | <span data-ttu-id="fb84b-112">1 ГБ (1 млн событий)</span><span class="sxs-lookup"><span data-stu-id="fb84b-112">1 GB (1 million events)</span></span> | <span data-ttu-id="fb84b-113">30 ГБ в месяц (30 млн событий)</span><span class="sxs-lookup"><span data-stu-id="fb84b-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="fb84b-114">10</span><span class="sxs-lookup"><span data-stu-id="fb84b-114">10</span></span> | <span data-ttu-id="fb84b-115">10 ГБ (10 млн событий)</span><span class="sxs-lookup"><span data-stu-id="fb84b-115">10 GB (10 million events)</span></span> | <span data-ttu-id="fb84b-116">300 ГБ в месяц (300 млн событий)</span><span class="sxs-lookup"><span data-stu-id="fb84b-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="fb84b-117">Скорость приема и емкость номера SKU S2</span><span class="sxs-lookup"><span data-stu-id="fb84b-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="fb84b-118">Емкость номера SKU S2</span><span class="sxs-lookup"><span data-stu-id="fb84b-118">S2 SKU Capacity</span></span> | <span data-ttu-id="fb84b-119">Скорость приема</span><span class="sxs-lookup"><span data-stu-id="fb84b-119">Ingress Rate</span></span> | <span data-ttu-id="fb84b-120">Максимальная емкость хранилища</span><span class="sxs-lookup"><span data-stu-id="fb84b-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="fb84b-121">1</span><span class="sxs-lookup"><span data-stu-id="fb84b-121">1</span></span> | <span data-ttu-id="fb84b-122">10 ГБ (10 млн событий)</span><span class="sxs-lookup"><span data-stu-id="fb84b-122">10 GB (10 million events)</span></span> | <span data-ttu-id="fb84b-123">300 ГБ в месяц (300 млн событий)</span><span class="sxs-lookup"><span data-stu-id="fb84b-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="fb84b-124">10</span><span class="sxs-lookup"><span data-stu-id="fb84b-124">10</span></span> | <span data-ttu-id="fb84b-125">100 ГБ (100 млн событий)</span><span class="sxs-lookup"><span data-stu-id="fb84b-125">100 GB (100 million events)</span></span> | <span data-ttu-id="fb84b-126">3 ТБ в месяц (3 млрд событий)</span><span class="sxs-lookup"><span data-stu-id="fb84b-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="fb84b-127">Емкость масштабируется линейно, поэтому номер SKU S1 с емкостью 2 поддерживает скорость приема 2 ГБ (2 млн событий) в неделю и 60 ГБ (60 млн событий) в месяц.</span><span class="sxs-lookup"><span data-stu-id="fb84b-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-hello-capacity-of-your-environment"></a><span data-ttu-id="fb84b-128">Изменение емкости hello среды</span><span class="sxs-lookup"><span data-stu-id="fb84b-128">Changing hello capacity of your environment</span></span>

1. <span data-ttu-id="fb84b-129">В hello портал Azure, выберите hello среды, емкость которого вы хотите toochange.</span><span class="sxs-lookup"><span data-stu-id="fb84b-129">In hello Azure portal, select hello environment whose capacity you want toochange.</span></span>
1. <span data-ttu-id="fb84b-130">В разделе "Параметры" щелкните "Настроить".</span><span class="sxs-lookup"><span data-stu-id="fb84b-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="fb84b-131">Используйте hello емкость ползунок tooselect hello емкость, удовлетворяющий требованиям тарифы входящих сообщений hello и емкость хранилища.</span><span class="sxs-lookup"><span data-stu-id="fb84b-131">Use hello Capacity slider tooselect hello capacity that meets hello requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb84b-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb84b-132">Next steps</span></span>

* <span data-ttu-id="fb84b-133">Убедитесь, что достаточно hello новой емкости tooprevent регулирования.</span><span class="sxs-lookup"><span data-stu-id="fb84b-133">Verify that hello new capacity is sufficient tooprevent throttling.</span></span> <span data-ttu-id="fb84b-134">Дополнительные сведения см. в разделе hello *среды возможно получение регулироваться* раздел [здесь](time-series-insights-diagnose-and-solve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="fb84b-134">For more details, see hello *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>
