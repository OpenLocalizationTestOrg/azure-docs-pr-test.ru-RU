---
title: "Учебник по службам Azure Analysis Services: занятие 9 \"Создание иерархий\" | Документы Майкрософт"
description: 
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
ms.openlocfilehash: d628dc621335acf231342a6d9186079de16e85f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="e57f7-102">Занятие 9. Создание иерархий</span><span class="sxs-lookup"><span data-stu-id="e57f7-102">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="e57f7-103">На этом занятии мы создадим иерархии.</span><span class="sxs-lookup"><span data-stu-id="e57f7-103">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="e57f7-104">Иерархии — это группы столбцов, упорядоченных по уровням. Например, иерархия "География" может иметь подуровни для страны, области, района и города.</span><span class="sxs-lookup"><span data-stu-id="e57f7-104">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="e57f7-105">Иерархии могут отображаться отдельно от других столбцов в списке полей клиентского приложения отчетов, что упрощает для пользователей клиента навигацию и включение в отчет.</span><span class="sxs-lookup"><span data-stu-id="e57f7-105">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users to navigate and include in a report.</span></span> <span data-ttu-id="e57f7-106">Дополнительные сведения см. в статье [Иерархии](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="e57f7-106">To learn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="e57f7-107">Для создания иерархий используется конструктор моделей в *представлении схемы*.</span><span class="sxs-lookup"><span data-stu-id="e57f7-107">To create hierarchies, use the model designer in *Diagram View*.</span></span> <span data-ttu-id="e57f7-108">Создание иерархий и управление ими не поддерживается в представлении данных.</span><span class="sxs-lookup"><span data-stu-id="e57f7-108">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="e57f7-109">Предполагаемое время выполнения этого занятия: **20 минут**</span><span class="sxs-lookup"><span data-stu-id="e57f7-109">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="e57f7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e57f7-110">Prerequisites</span></span>  
<span data-ttu-id="e57f7-111">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="e57f7-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="e57f7-112">Прежде чем выполнять задачи в этом разделе, необходимо завершить предыдущее занятие: [Занятие 8. Создание перспектив](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="e57f7-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="e57f7-113">Создание иерархий</span><span class="sxs-lookup"><span data-stu-id="e57f7-113">Create hierarchies</span></span>  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a><span data-ttu-id="e57f7-114">Создание иерархии категорий в таблице DimProduct</span><span class="sxs-lookup"><span data-stu-id="e57f7-114">To create a Category hierarchy in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="e57f7-115">В конструкторе моделей (представление схемы) щелкните правой кнопкой мыши таблицу **DimProduct** и выберите пункт **Создать иерархию**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-115">In the model designer (diagram view), right-click the **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="e57f7-116">В нижней части окна таблицы появится новая иерархия.</span><span class="sxs-lookup"><span data-stu-id="e57f7-116">A new hierarchy appears at the bottom of the table window.</span></span> <span data-ttu-id="e57f7-117">Назовите иерархию **Category**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-117">Rename the hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="e57f7-118">Щелкните и перетащите столбец **ProductCategoryName** в новую иерархию **Category**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-118">Click and drag the **ProductCategoryName** column to the new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="e57f7-119">В иерархии **Category** щелкните правой кнопкой мыши столбец **ProductCategoryName** > **Переименовать**, а затем введите **Category**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-119">In the **Category** hierarchy, right-click the **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="e57f7-120">Переименование столбца в иерархии не приводит к переименованию этого столбца в таблице.</span><span class="sxs-lookup"><span data-stu-id="e57f7-120">Renaming a column in a hierarchy does not rename that column in the table.</span></span> <span data-ttu-id="e57f7-121">Столбец в иерархии — это просто представление столбца в таблице.</span><span class="sxs-lookup"><span data-stu-id="e57f7-121">A column in a hierarchy is just a representation of the column in the table.</span></span>  
  
4.  <span data-ttu-id="e57f7-122">Щелкните и перетащите столбец **ProductSubcategoryName** в иерархию **Category**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-122">Click and drag the **ProductSubcategoryName** column to the **Category** hierarchy.</span></span> <span data-ttu-id="e57f7-123">Назовите его **Subcategory**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-123">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="e57f7-124">Щелкните правой кнопкой мыши столбец **ModelName**, выберите **Добавить иерархию**, а затем **Category**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-124">Right-click the **ModelName** column > **Add to hierarchy**, and then select **Category**.</span></span> <span data-ttu-id="e57f7-125">Назовите его **Model**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-125">Rename it **Model**.</span></span>

6.  <span data-ttu-id="e57f7-126">Наконец, добавьте столбец **EnglishProductName** в иерархию категорий.</span><span class="sxs-lookup"><span data-stu-id="e57f7-126">Finally, add **EnglishProductName** to the Category hierarchy.</span></span> <span data-ttu-id="e57f7-127">Назовите его **Product**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-127">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a><span data-ttu-id="e57f7-129">Создание иерархий в таблице DimDate</span><span class="sxs-lookup"><span data-stu-id="e57f7-129">To create hierarchies in the DimDate table</span></span>  
  
1.  <span data-ttu-id="e57f7-130">В таблице **DimDate** создайте иерархию с именем **Calendar**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-130">In the **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="e57f7-131">Добавьте следующие столбцы по порядку:</span><span class="sxs-lookup"><span data-stu-id="e57f7-131">Add the following columns in-order:</span></span>

    *  <span data-ttu-id="e57f7-132">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="e57f7-132">CalendarYear</span></span>
    *  <span data-ttu-id="e57f7-133">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="e57f7-133">CalendarSemester</span></span>
    *  <span data-ttu-id="e57f7-134">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="e57f7-134">CalendarQuarter</span></span>
    *  <span data-ttu-id="e57f7-135">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="e57f7-135">MonthCalendar</span></span>
    *  <span data-ttu-id="e57f7-136">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="e57f7-136">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="e57f7-137">В таблице **DimDate** создайте иерархию **Fiscal**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-137">In the **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="e57f7-138">Включите следующие столбцы по порядку:</span><span class="sxs-lookup"><span data-stu-id="e57f7-138">Include the following columns in-order:</span></span>  
  
    *  <span data-ttu-id="e57f7-139">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="e57f7-139">FiscalYear</span></span>
    *  <span data-ttu-id="e57f7-140">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="e57f7-140">FiscalSemester</span></span>
    *  <span data-ttu-id="e57f7-141">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="e57f7-141">FiscalQuarter</span></span>
    *  <span data-ttu-id="e57f7-142">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="e57f7-142">MonthCalendar</span></span>
    *  <span data-ttu-id="e57f7-143">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="e57f7-143">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="e57f7-144">Наконец, в таблице **DimDate** создайте иерархию **ProductionCalendar**.</span><span class="sxs-lookup"><span data-stu-id="e57f7-144">Finally, in the **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="e57f7-145">Включите следующие столбцы по порядку:</span><span class="sxs-lookup"><span data-stu-id="e57f7-145">Include the following columns in-order:</span></span>  
    *  <span data-ttu-id="e57f7-146">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="e57f7-146">CalendarYear</span></span>
    *  <span data-ttu-id="e57f7-147">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="e57f7-147">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="e57f7-148">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="e57f7-148">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="e57f7-149">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="e57f7-149">What's next?</span></span>
<span data-ttu-id="e57f7-150">[Занятие 10. Создание разделов](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="e57f7-150">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
