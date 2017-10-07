---
title: "тенденции затрат aaaView hello ежемесячные предполагаемое лаборатории в Azure DevTest Labs | Документы Microsoft"
description: "Дополнительные сведения о hello Azure DevTest Labs ежемесячные расчетные затраты на график."
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
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="53e22-103">Тенденции затрат представление hello ежемесячные предполагаемое лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="53e22-103">View hello monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="53e22-104">функции управления стоимость Hello DevTest Labs помогает отслеживать стоимость hello лаборатории.</span><span class="sxs-lookup"><span data-stu-id="53e22-104">hello Cost Management feature of DevTest Labs helps you track hello cost of your lab.</span></span> <span data-ttu-id="53e22-105">В этой статье показано, как toouse hello **ежемесячные предполагаемое тенденции затрат** tooview диаграммы hello текущего календарного месяца Оценка затрат с начала и hello запланированные затраты на конец месяца для hello текущего календарного месяца.</span><span class="sxs-lookup"><span data-stu-id="53e22-105">This article illustrates how toouse hello **Monthly Estimated Cost Trend** chart tooview hello current calendar month's estimated cost-to-date and hello projected end-of-month cost for hello current calendar month.</span></span> <span data-ttu-id="53e22-106">В этой статье вы узнаете, как tooview hello ежемесячные диаграммы тренда Предполагаемая стоимость в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="53e22-106">In this article, you learn how tooview hello monthly estimated cost trend chart in hello Azure portal.</span></span>

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="53e22-107">Просмотр hello ежемесячные Предполагаемая стоимость график</span><span class="sxs-lookup"><span data-stu-id="53e22-107">Viewing hello Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="53e22-108">hello tooview ежемесячные Предполагаемая стоимость график, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="53e22-108">tooview hello Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="53e22-109">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="53e22-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="53e22-110">Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="53e22-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="53e22-111">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="53e22-111">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="53e22-112">В колонке hello лаборатории выберите **параметров**.</span><span class="sxs-lookup"><span data-stu-id="53e22-112">On hello lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="53e22-113">В лаборатории hello **параметров** колонке выберите **тенденции затрат лаборатории**.</span><span class="sxs-lookup"><span data-stu-id="53e22-113">On hello lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="53e22-114">Hello следующем снимке экрана показан пример диаграммы затрат.</span><span class="sxs-lookup"><span data-stu-id="53e22-114">hello following screen shot shows an example of a cost chart.</span></span> 
   
    ![Диаграмма стоимости](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="53e22-116">Hello **Предполагаемая стоимость** значение hello текущего календарного месяца Оценка затрат с начала.</span><span class="sxs-lookup"><span data-stu-id="53e22-116">hello **Estimated cost** value is hello current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="53e22-117">Hello **затрат** hello предполагаемые затраты на hello весь текущий календарный месяц вычисляется с помощью стоимости лаборатории hello для hello прошедшие пять дней.</span><span class="sxs-lookup"><span data-stu-id="53e22-117">hello **Projected cost** is hello estimated cost for hello entire current calendar month, calculated using hello lab cost for hello previous five days.</span></span>

<span data-ttu-id="53e22-118">суммы затрат Hello округляются toohello следующего целого числа.</span><span class="sxs-lookup"><span data-stu-id="53e22-118">hello cost amounts are rounded up toohello next whole number.</span></span> <span data-ttu-id="53e22-119">Например:</span><span class="sxs-lookup"><span data-stu-id="53e22-119">For example:</span></span> 

* <span data-ttu-id="53e22-120">5.01 округляет too6</span><span class="sxs-lookup"><span data-stu-id="53e22-120">5.01 rounds up too6</span></span> 
* <span data-ttu-id="53e22-121">5.50 округляет too6</span><span class="sxs-lookup"><span data-stu-id="53e22-121">5.50 rounds up too6</span></span>
* <span data-ttu-id="53e22-122">5.99 округляет too6</span><span class="sxs-lookup"><span data-stu-id="53e22-122">5.99 rounds up too6</span></span>

<span data-ttu-id="53e22-123">Как говорится в над диаграммой hello, затраты на hello видно из диаграммы hello, *предполагаемое* расходы с помощью [Оплата по мере использования](https://azure.microsoft.com/offers/ms-azr-0003p/) предлагаются скидки.</span><span class="sxs-lookup"><span data-stu-id="53e22-123">As it states above hello chart, hello costs you see in hello chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="53e22-124">Кроме того, представлены hello *не* включен в расчет стоимости hello:</span><span class="sxs-lookup"><span data-stu-id="53e22-124">Additionally, hello following are *not* included in hello cost calculation:</span></span>

* <span data-ttu-id="53e22-125">Подписки Dreamspark и поставщика служб Шифрования в настоящее время не поддерживаются как Azure DevTest Labs использует hello [Azure выставления счетов API-интерфейсы](../billing/billing-usage-rate-card-overview.md) лаборатории hello toocalculate стоимости, который не поддерживает подписки CSP или Dreamspark.</span><span class="sxs-lookup"><span data-stu-id="53e22-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses hello [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) toocalculate hello lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="53e22-126">индивидуальные тарифы —</span><span class="sxs-lookup"><span data-stu-id="53e22-126">Your offer rates.</span></span> <span data-ttu-id="53e22-127">В настоящее время мы не может toouse тарифы предложение (показаны в рамках подписки), согласованные с Майкрософт или партнерами.</span><span class="sxs-lookup"><span data-stu-id="53e22-127">Currently, we are not able toouse your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="53e22-128">мы используем тарифы с оплатой по мере использования;</span><span class="sxs-lookup"><span data-stu-id="53e22-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="53e22-129">налоги;</span><span class="sxs-lookup"><span data-stu-id="53e22-129">Your taxes</span></span>
* <span data-ttu-id="53e22-130">скидки;</span><span class="sxs-lookup"><span data-stu-id="53e22-130">Your discounts</span></span>
* <span data-ttu-id="53e22-131">валюта выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="53e22-131">Your billing currency.</span></span> <span data-ttu-id="53e22-132">В настоящее время стоимости лаборатории hello отображается только в валюте долл. США.</span><span class="sxs-lookup"><span data-stu-id="53e22-132">Currently, hello lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="53e22-133">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="53e22-133">Related blog posts</span></span>
* [<span data-ttu-id="53e22-134">Две дополнительные действия tookeep расходы на отслеживание в DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="53e22-134">Two more things tookeep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="53e22-135">Why Cost Thresholds? (Зачем нужны стоимостные пороги?)</span><span class="sxs-lookup"><span data-stu-id="53e22-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="53e22-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53e22-136">Next steps</span></span>
<span data-ttu-id="53e22-137">Ниже приведены некоторые вещи tootry Далее.</span><span class="sxs-lookup"><span data-stu-id="53e22-137">Here are some things tootry next:</span></span>

* <span data-ttu-id="53e22-138">[Определение политик лаборатории](devtest-lab-set-lab-policy.md) -Узнайте, как tooset hello различные политики применяются toogovern, как использовать эту лабораторную работу и его виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="53e22-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how tooset hello various policies used toogovern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="53e22-139">[Создание пользовательского образа.](devtest-lab-create-template.md) При создании виртуальной машины необходимо указать базовый образ виртуальной машины, который может представлять собой пользовательский образ или образ из Marketplace.</span><span class="sxs-lookup"><span data-stu-id="53e22-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="53e22-140">В этой статье показано, как toocreate пользовательского образа из VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="53e22-140">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="53e22-141">[Настройка образов Marketplace.](devtest-lab-configure-marketplace-images.md) DevTest Labs поддерживает создание виртуальных машин на основе образов Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="53e22-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="53e22-142">В этой статье показано, как toospecify, который, если таковые имеются, образы Azure Marketplace можно использовать при создании виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="53e22-142">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="53e22-143">[Создание виртуальной Машины в лабораторной среде](devtest-lab-add-vm-with-artifacts.md) -показано, как toocreate из базового образа виртуальной Машины (либо настраиваемый или Marketplace) и как toowork с артефактами в ВМ.</span><span class="sxs-lookup"><span data-stu-id="53e22-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

