---
title: "Просмотр помесячной тенденции изменения оценочной стоимости в Azure DevTest Labs | Документация Майкрософт"
description: "Узнайте о диаграмме Azure DevTest Labs \"Помесячная тенденция изменения оценочной стоимости\"."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: b3ad1ead522908d4b41b7cca98d20ac91664998e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="5c3f7-103">Просмотр помесячной тенденции изменения оценочной стоимости в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5c3f7-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="5c3f7-104">Функция управления затратами в лаборатории для разработки и тестирования помогает отслеживать расходы на лабораторию.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="5c3f7-105">В этой статье демонстрируется, как использовать диаграмму **Помесячная тенденция изменения оценочной стоимости** для просмотра оценочной стоимости на данный момент для текущего календарного месяца, а также прогнозируемой стоимости на конец текущего календарного месяца.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="5c3f7-106">В этой статье вы узнаете, как просмотреть диаграмму "Помесячная тенденция изменения оценочной стоимости" на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="5c3f7-107">Просмотр диаграммы "Помесячная тенденция изменения расчетной стоимости"</span><span class="sxs-lookup"><span data-stu-id="5c3f7-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="5c3f7-108">Для просмотра диаграммы "Помесячная тенденция изменения оценочной стоимости" выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="5c3f7-109">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5c3f7-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="5c3f7-110">Щелкните **Больше служб**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="5c3f7-111">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-111">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="5c3f7-112">В колонке лаборатории выберите **Cost settings**(Параметры стоимости).</span><span class="sxs-lookup"><span data-stu-id="5c3f7-112">On the lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="5c3f7-113">В колонке **Настройки затрат** лаборатории выберите **Тренд затрат на лабораторию**.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="5c3f7-114">На снимке экрана ниже показан пример диаграммы стоимости.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-114">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![Диаграмма стоимости](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="5c3f7-116">Значение **Оценочная стоимость** — это стоимость на данный момент в текущем календарном месяце.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="5c3f7-117">А значение **Плановые затраты** — это оценочная стоимость за весь текущий календарный месяц, рассчитанная исходя из затрат лаборатории за предыдущие пять дней.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="5c3f7-118">Обратите внимание, что суммы затрат округляются до ближайшего целого числа.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-118">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="5c3f7-119">Например:</span><span class="sxs-lookup"><span data-stu-id="5c3f7-119">For example:</span></span> 

* <span data-ttu-id="5c3f7-120">5.01 округляется до 6</span><span class="sxs-lookup"><span data-stu-id="5c3f7-120">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="5c3f7-121">5.50 округляется до 6</span><span class="sxs-lookup"><span data-stu-id="5c3f7-121">5.50 rounds up to 6</span></span>
* <span data-ttu-id="5c3f7-122">5.99 округляется до 6</span><span class="sxs-lookup"><span data-stu-id="5c3f7-122">5.99 rounds up to 6</span></span>

<span data-ttu-id="5c3f7-123">Как указано над диаграммой, приведенные в ней затраты *рассчитываются* согласно тарифам с [оплатой по мере использования](https://azure.microsoft.com/offers/ms-azr-0003p/) .</span><span class="sxs-lookup"><span data-stu-id="5c3f7-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="5c3f7-124">Кроме того, при расчете стоимости *не* учитываются следующие данные:</span><span class="sxs-lookup"><span data-stu-id="5c3f7-124">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="5c3f7-125">подписки CSP и Dreamspark в настоящее время не поддерживаются, так как для расчета затрат лаборатории Azure DevTest Labs использует [интерфейсы API Azure для выставления счетов](../billing/billing-usage-rate-card-overview.md) , а они не поддерживают указанные подписки;</span><span class="sxs-lookup"><span data-stu-id="5c3f7-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="5c3f7-126">индивидуальные тарифы —</span><span class="sxs-lookup"><span data-stu-id="5c3f7-126">Your offer rates.</span></span> <span data-ttu-id="5c3f7-127">в настоящее время мы не можем учитывать ваши индивидуальные тарифы (указанные под подпиской), согласованные с корпорацией Майкрософт или ее партнерами;</span><span class="sxs-lookup"><span data-stu-id="5c3f7-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="5c3f7-128">мы используем тарифы с оплатой по мере использования;</span><span class="sxs-lookup"><span data-stu-id="5c3f7-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="5c3f7-129">налоги;</span><span class="sxs-lookup"><span data-stu-id="5c3f7-129">Your taxes</span></span>
* <span data-ttu-id="5c3f7-130">скидки;</span><span class="sxs-lookup"><span data-stu-id="5c3f7-130">Your discounts</span></span>
* <span data-ttu-id="5c3f7-131">валюта выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-131">Your billing currency.</span></span> <span data-ttu-id="5c3f7-132">В настоящее время затраты на лабораторию приводятся только в долларах США.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-132">Currently, the lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="5c3f7-133">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="5c3f7-133">Related blog posts</span></span>
* [<span data-ttu-id="5c3f7-134">Two more things to keep your cost on track in DevTest Labs (Два дополнительных действия для отслеживания затрат в DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="5c3f7-134">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="5c3f7-135">Why Cost Thresholds? (Зачем нужны стоимостные пороги?)</span><span class="sxs-lookup"><span data-stu-id="5c3f7-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="5c3f7-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c3f7-136">Next steps</span></span>
<span data-ttu-id="5c3f7-137">Далее можно выполнить перечисленные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-137">Here are some things to try next:</span></span>

* <span data-ttu-id="5c3f7-138">[Определение политик лаборатории.](devtest-lab-set-lab-policy.md) Узнайте, как настроить различные политики управления, которые используются лабораторией и ее виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="5c3f7-139">[Создание пользовательского образа.](devtest-lab-create-template.md) При создании виртуальной машины необходимо указать базовый образ виртуальной машины, который может представлять собой пользовательский образ или образ из Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="5c3f7-140">В этой статье показано, как создать настраиваемый образ из VHD-файла.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-140">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="5c3f7-141">[Настройка образов Marketplace.](devtest-lab-configure-marketplace-images.md) DevTest Labs поддерживает создание виртуальных машин на основе образов Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="5c3f7-142">В этой статье показано, как определить, какие образы Azure Marketplace (если таковые имеются) можно использовать при создании виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="5c3f7-143">[Добавление виртуальной машины с артефактами в лабораторию.](devtest-lab-add-vm-with-artifacts.md) В этой статье рассказывается, как создать виртуальную машину из базового образа (пользовательского или из Marketplace) и работать с артефактами виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5c3f7-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

