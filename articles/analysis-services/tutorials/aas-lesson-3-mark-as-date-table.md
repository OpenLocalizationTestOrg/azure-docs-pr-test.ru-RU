---
title: "Учебник по службам Azure Analysis Services: занятие 3 \"Обозначение таблицы дат\" | Документы Майкрософт"
description: "Описывает обозначение таблицы дат в учебном проекте служб Azure Analysis Services."
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
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: c62f2726fef5219155a08b70c61162c914600d1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-3-mark-as-date-table"></a><span data-ttu-id="9b6a9-103">Занятие 3. Обозначение таблицы дат</span><span class="sxs-lookup"><span data-stu-id="9b6a9-103">Lesson 3: Mark as Date Table</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="9b6a9-104">В занятии 2 "Получение данных" вы импортировали таблицу измерения DimDate.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-104">In Lesson 2: Get data, you imported a dimension table named DimDate.</span></span> <span data-ttu-id="9b6a9-105">Хотя в вашей модели эта таблица имеет имя DimDate, она также может называться *таблицей дат*, так как содержит данные о датах и времени.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-105">While in your model this table is named DimDate, it can also be known as a *Date table*, in that it contains date and time data.</span></span>  
  
<span data-ttu-id="9b6a9-106">Каждый раз при использовании функций логики операций со временем DAX (вы займетесь этим чуть позже при создании мер) нужно указывать такие свойства, как *Таблица дат* и уникальный идентификатор *Столбец даты* в ней.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-106">Whenever you use DAX time-intelligence functions, like when you create measures later, you must specify properties which include a *Date table* and a unique identifier *Date column* in that table.</span></span>
  
<span data-ttu-id="9b6a9-107">На этом занятии вы пометите таблицу DimDate как *таблицу дат*, а столбец даты как *Столбец даты* (уникальный идентификатор).</span><span class="sxs-lookup"><span data-stu-id="9b6a9-107">In this lesson, you mark the DimDate table as the *Date table* and the Date column (in the Date table) as the *Date column* (unique identifier).</span></span>  

<span data-ttu-id="9b6a9-108">Прежде чем помечать таблицу дат и столбец дат, рекомендуется выполнить несколько служебных действий, чтобы упростить восприятие модели.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-108">Before you mark the date table and date column, it's a good time to do a little housekeeping to make your model easier to understand.</span></span> <span data-ttu-id="9b6a9-109">Обратите внимание на столбец с именем **FullDateAlternateKey** в таблице DimDate.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-109">Notice in the DimDate table a column named **FullDateAlternateKey**.</span></span> <span data-ttu-id="9b6a9-110">Он содержит по одной строке для каждого дня каждого календарного года, включенного в таблицу.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-110">This column contains one row for every day in each calendar year included in the table.</span></span> <span data-ttu-id="9b6a9-111">Этот столбец часто используется в формулах мер и отчетах.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-111">You use this column a lot in measure formulas and in reports.</span></span> <span data-ttu-id="9b6a9-112">Однако FullDateAlternateKey нельзя назвать уместным идентификатором для этого столбца.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-112">But, FullDateAlternateKey isn't really a good identifier for this column.</span></span> <span data-ttu-id="9b6a9-113">Его имя следует изменить на **Date**, чтобы упростить поиск и использование в формулах.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-113">You rename it to **Date**, making it easier to identify and include in formulas.</span></span> <span data-ttu-id="9b6a9-114">По возможности рекомендуется переименовывать такие объекты, как таблицы и столбцы, чтобы упростить их поиск в SSDT и клиентских приложениях, таких как Power BI и Excel.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-114">Whenever possible, it's a good idea to rename objects like tables and columns to make them easier to identify in SSDT and client reporting applications like Power BI and Excel.</span></span> 
  
<span data-ttu-id="9b6a9-115">Предполагаемое время выполнения этого занятия: **3 минуты**</span><span class="sxs-lookup"><span data-stu-id="9b6a9-115">Estimated time to complete this lesson: **Three minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="9b6a9-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9b6a9-116">Prerequisites</span></span>  
<span data-ttu-id="9b6a9-117">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-117">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="9b6a9-118">Прежде чем выполнять задачи в этом разделе, нужно завершить предыдущее занятие: [Занятие 2. Получение данных](../tutorials/aas-lesson-2-get-data.md).</span><span class="sxs-lookup"><span data-stu-id="9b6a9-118">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span></span> 

### <a name="to-rename-the-fulldatealternatekey-column"></a><span data-ttu-id="9b6a9-119">Чтобы переименовать столбец FullDateAlternateKey, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9b6a9-119">To rename the FullDateAlternateKey column</span></span>

1.  <span data-ttu-id="9b6a9-120">В конструкторе моделей щелкните таблицу **DimDate**.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-120">In the model designer, click the **DimDate** table.</span></span>

2.  <span data-ttu-id="9b6a9-121">Дважды щелкните заголовок для столбца **FullDateAlternateKey** и измените имя на **Date**.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-121">Double-click the header for the **FullDateAlternateKey** column, and then rename it to **Date**.</span></span>

  
### <a name="to-set-mark-as-date-table"></a><span data-ttu-id="9b6a9-122">Чтобы обозначить таблицу дат, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9b6a9-122">To set Mark as Date Table</span></span>  
  
1.  <span data-ttu-id="9b6a9-123">Выберите столбец **Date** и затем в разделе **Тип данных** окна **Свойства** выберите параметр **Date**.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-123">Select the **Date** column, and then in the **Properties** window, under **Data Type**, make sure  **Date** is selected.</span></span>  
  
2.  <span data-ttu-id="9b6a9-124">Щелкните меню **Таблица**, а затем выберите **Date** и **Пометить как таблицу дат**.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-124">Click the **Table** menu, then click **Date**, and then click **Mark as Date Table**.</span></span>  
  
3.  <span data-ttu-id="9b6a9-125">В списке **Date** диалогового окна **Пометить как таблицу дат** выберите столбец **Date** в качестве уникального идентификатора.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-125">In the **Mark as Date Table** dialog box, in the **Date** listbox, select the **Date** column as the unique identifier.</span></span> <span data-ttu-id="9b6a9-126">Обычно он уже выбран по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-126">It's usually selected by default.</span></span> <span data-ttu-id="9b6a9-127">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9b6a9-127">Click **OK**.</span></span> 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a><span data-ttu-id="9b6a9-129">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="9b6a9-129">What's next?</span></span>
<span data-ttu-id="9b6a9-130">[Занятие 4. Создание связей](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="9b6a9-130">[Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span>
  
