---
title: "Учебник по службам Azure Analysis Services: занятие 7 \"Создание ключевых показателей эффективности\" | Документы Майкрософт"
description: "Описывает создание ключевых показателей эффективности в учебном проекте служб Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: d78808421dd5acd907aa9e9000bb3b770a42c061
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="152b8-103">Занятие 7. Создание ключевых показателей эффективности</span><span class="sxs-lookup"><span data-stu-id="152b8-103">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="152b8-104">В этом занятии вы создадите ключевые показатели эффективности (КПЭ).</span><span class="sxs-lookup"><span data-stu-id="152b8-104">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="152b8-105">Ключевые показатели эффективности используются для оценки эффективности значения, определенного *базовой* мерой, по отношению к *целевому* значению, также определенному мерой или абсолютным значением.</span><span class="sxs-lookup"><span data-stu-id="152b8-105">KPIs are used to gauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="152b8-106">В клиентских приложениях по ведению отчетности ключевые показатели эффективности позволяют специалистам быстро и просто получить сводку по успешности бизнеса или выявить тенденции.</span><span class="sxs-lookup"><span data-stu-id="152b8-106">In reporting client applications, KPIs can provide business professionals a quick and easy way to understand a summary of business success or to identify trends.</span></span> <span data-ttu-id="152b8-107">Дополнительные сведения см. в разделе [Ключевые показатели эффективности](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="152b8-107">To learn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="152b8-108">Предполагаемое время выполнения этого занятия: **15 минут**</span><span class="sxs-lookup"><span data-stu-id="152b8-108">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="152b8-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="152b8-109">Prerequisites</span></span>  
<span data-ttu-id="152b8-110">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="152b8-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="152b8-111">Прежде чем выполнять задачи в этом разделе, нужно завершить предыдущее занятие: [Занятие 6. Создание мер](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="152b8-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="152b8-112">Создание ключевых показателей эффективности</span><span class="sxs-lookup"><span data-stu-id="152b8-112">Create Key Performance Indicators</span></span>  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="152b8-113">Создание ключевого показателя эффективности InternetCurrentQuarterSalesPerformance</span><span class="sxs-lookup"><span data-stu-id="152b8-113">To create an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="152b8-114">В конструкторе моделей выберите таблицу **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="152b8-114">In the model designer, click the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="152b8-115">Щелкните пустую ячейку в сетке мер.</span><span class="sxs-lookup"><span data-stu-id="152b8-115">In the measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="152b8-116">В строке формул над таблицей введите следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="152b8-116">In the formula bar, above the table, type the following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="152b8-117">Эта мера будет использоваться в качестве базовой для ключевого показателя эффективности.</span><span class="sxs-lookup"><span data-stu-id="152b8-117">This measure serves as the Base measure for the KPI.</span></span>  
  
4.  <span data-ttu-id="152b8-118">Щелкните правой кнопкой мыши **InternetCurrentQuarterSalesPerformance** > **Создать ключевой показатель эффективности**.</span><span class="sxs-lookup"><span data-stu-id="152b8-118">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="152b8-119">В поле **Цель** диалогового окна "Ключевой показатель эффективности" выберите **Абсолютное значение**, а затем введите **1.1**.</span><span class="sxs-lookup"><span data-stu-id="152b8-119">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="152b8-120">В левом (нижнем) поле с ползунком введите **1**, а в правом (верхнем) — **1.07**.</span><span class="sxs-lookup"><span data-stu-id="152b8-120">In the left (low) slider field, type **1**, and then in the right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="152b8-121">В области **Выберите стиль значка** выберите значок в виде ромба (красного цвета), треугольника (желтого цвета), круга (зеленого цвета).</span><span class="sxs-lookup"><span data-stu-id="152b8-121">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="152b8-123">Обратите внимание на развертываемую метку **Описания** под доступными стилями значков.</span><span class="sxs-lookup"><span data-stu-id="152b8-123">Notice the expandable **Descriptions** label below the available icon styles.</span></span> <span data-ttu-id="152b8-124">Используйте описания для разных элементов ключевых показателей эффективности, чтобы сделать их более понятными в клиентских приложениях.</span><span class="sxs-lookup"><span data-stu-id="152b8-124">Use descriptions for the various KPI elements to make them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="152b8-125">Нажмите кнопку **ОК**, чтобы завершить создание КПЭ.</span><span class="sxs-lookup"><span data-stu-id="152b8-125">Click **OK** to complete the KPI.</span></span>  
  
    <span data-ttu-id="152b8-126">В сетке мер обратите внимание на значок рядом с мерой **InternetCurrentQuarterSalesPerformance**.</span><span class="sxs-lookup"><span data-stu-id="152b8-126">In the measure grid, notice the icon next to the **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="152b8-127">Он указывает, что мера служит базовым значением для КПЭ.</span><span class="sxs-lookup"><span data-stu-id="152b8-127">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="152b8-128">Создание ключевого показателя эффективности InternetCurrentQuarterMarginPerformance</span><span class="sxs-lookup"><span data-stu-id="152b8-128">To create an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="152b8-129">Щелкните пустую ячейку в сетке мер для таблицы **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="152b8-129">In the measure grid for the **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="152b8-130">В строке формул над таблицей введите следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="152b8-130">In the formula bar, above the table, type the following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="152b8-131">Щелкните правой кнопкой мыши **InternetCurrentQuarterMarginPerformance** > **Создать ключевой показатель эффективности**.</span><span class="sxs-lookup"><span data-stu-id="152b8-131">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="152b8-132">В поле **Цель** диалогового окна "Ключевой показатель эффективности" выберите **Абсолютное значение**, а затем введите **1.25**.</span><span class="sxs-lookup"><span data-stu-id="152b8-132">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="152b8-133">В левом (нижнем) поле с ползунком прокрутите до значения **0.8**, а в правом (верхнем) — до значения **1.03**.</span><span class="sxs-lookup"><span data-stu-id="152b8-133">In the left (low) slider field, slide until the field displays **0.8**, and then slide the right (high) slider field, until the field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="152b8-134">В области **Выберите стиль значка** выберите значок в виде ромба (красного цвета), треугольника (желтого цвета), круга (зеленого цвета) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="152b8-134">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="152b8-135">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="152b8-135">What's next?</span></span>
<span data-ttu-id="152b8-136">[Занятие 8. Создание перспектив](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="152b8-136">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
