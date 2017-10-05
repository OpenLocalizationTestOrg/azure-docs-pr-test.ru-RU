---
title: "Дополнительное занятие для учебника по службам Azure Analysis Services: \"Неоднородные иерархии\" | Документы Майкрософт"
description: "Описывает исправление неоднородных иерархий в учебном проекте служб Azure Analysis Services."
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
ms.openlocfilehash: 0f02ff73eb126cc397312e87bde50b3ee2d6ce53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="b0ca0-103">Дополнительное занятие. Неоднородные иерархии</span><span class="sxs-lookup"><span data-stu-id="b0ca0-103">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b0ca0-104">В этом дополнительном занятии вы устраните распространенную проблему, которая возникает при сведении иерархий, содержащих пустые значения (члены) на различных уровнях.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-104">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="b0ca0-105">Например, организация, где прямыми подчиненными высокопоставленного руководителя являются как руководители подразделений, так и не руководящие работники.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-105">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="b0ca0-106">Или географические иерархии, состоящие из комбинации страна+регион+город, где некоторые города не относятся к конкретному штату или конкретной провинции, например Вашингтон, округ Колумбия, или Ватикан.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-106">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="b0ca0-107">Когда иерархия содержит пустые члены, она часто опускается на другие — или неоднородные — уровни.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-107">When a hierarchy has blank members, it often descends to different, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="b0ca0-109">Табличные модели на уровне совместимости 1400 имеют дополнительное свойство **Скрыть члены** для иерархий.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-109">Tabular models at the 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="b0ca0-110">Значение **По умолчанию** предполагает отсутствие пустых членов на всех уровнях.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-110">The **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="b0ca0-111">Значение **Скрыть пустые члены** исключает пустые члены из иерархии при добавлении в сводную таблицу или отчет.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-111">The **Hide blank members** setting excludes blank members from the hierarchy when added to a PivotTable or report.</span></span>  
  
<span data-ttu-id="b0ca0-112">Предполагаемое время выполнения этого занятия: **20 минут**</span><span class="sxs-lookup"><span data-stu-id="b0ca0-112">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b0ca0-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b0ca0-113">Prerequisites</span></span>  
<span data-ttu-id="b0ca0-114">Это дополнительное занятие входит в учебник по табличному моделированию.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-114">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="b0ca0-115">Прежде чем выполнять задачи из этого дополнительного занятия, следует завершить все предыдущие занятия или располагать готовым учебным проектом модели интернет-продаж Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-115">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="b0ca0-116">Если вы создали проект AW Internet Sales во время прохождения этого учебника, то ваша модель еще не содержит неоднородные иерархии или данные.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-116">If you've created the AW Internet Sales project as part of the tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="b0ca0-117">Для выполнения этого дополнительного занятия нужно сначала создать проблему, добавив несколько дополнительных таблиц, создать связи, вычисляемые столбцы, меры и новую иерархию "Organization".</span><span class="sxs-lookup"><span data-stu-id="b0ca0-117">To complete this supplemental lesson, you first have to create the problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="b0ca0-118">Эта часть займет около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-118">That part takes about 15 minutes.</span></span> <span data-ttu-id="b0ca0-119">Затем вам потребуется решить проблему за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-119">Then, you get to solve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="b0ca0-120">Добавление таблиц и объектов</span><span class="sxs-lookup"><span data-stu-id="b0ca0-120">Add tables and objects</span></span>
  
### <a name="to-add-new-tables-to-your-model"></a><span data-ttu-id="b0ca0-121">Порядок добавления таблиц в модель</span><span class="sxs-lookup"><span data-stu-id="b0ca0-121">To add new tables to your model</span></span>
  
1.  <span data-ttu-id="b0ca0-122">В обозревателе табличных моделей разверните пункт **Источники данных**, щелкните правой кнопкой мыши подключение и выберите элемент **Импортировать новые таблицы**.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-122">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="b0ca0-123">В навигаторе выберите **DimEmployee** и **FactResellerSales**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-123">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="b0ca0-124">В редакторе запросов щелкните элемент **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-124">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="b0ca0-125">Создайте следующие [связи](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="b0ca0-125">Create the following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="b0ca0-126">Таблица 1</span><span class="sxs-lookup"><span data-stu-id="b0ca0-126">Table 1</span></span>           | <span data-ttu-id="b0ca0-127">столбец</span><span class="sxs-lookup"><span data-stu-id="b0ca0-127">Column</span></span>       | <span data-ttu-id="b0ca0-128">Направление фильтра</span><span class="sxs-lookup"><span data-stu-id="b0ca0-128">Filter Direction</span></span>   | <span data-ttu-id="b0ca0-129">Таблица 2</span><span class="sxs-lookup"><span data-stu-id="b0ca0-129">Table 2</span></span>     | <span data-ttu-id="b0ca0-130">столбец</span><span class="sxs-lookup"><span data-stu-id="b0ca0-130">Column</span></span>      | <span data-ttu-id="b0ca0-131">Активна</span><span class="sxs-lookup"><span data-stu-id="b0ca0-131">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="b0ca0-132">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b0ca0-132">FactResellerSales</span></span> | <span data-ttu-id="b0ca0-133">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="b0ca0-133">OrderDateKey</span></span> | <span data-ttu-id="b0ca0-134">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b0ca0-134">Default</span></span>            | <span data-ttu-id="b0ca0-135">DimDate</span><span class="sxs-lookup"><span data-stu-id="b0ca0-135">DimDate</span></span>     | <span data-ttu-id="b0ca0-136">Дата</span><span class="sxs-lookup"><span data-stu-id="b0ca0-136">Date</span></span>        | <span data-ttu-id="b0ca0-137">Да</span><span class="sxs-lookup"><span data-stu-id="b0ca0-137">Yes</span></span>    |
    | <span data-ttu-id="b0ca0-138">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b0ca0-138">FactResellerSales</span></span> | <span data-ttu-id="b0ca0-139">DueDate</span><span class="sxs-lookup"><span data-stu-id="b0ca0-139">DueDate</span></span>      | <span data-ttu-id="b0ca0-140">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b0ca0-140">Default</span></span>            | <span data-ttu-id="b0ca0-141">DimDate</span><span class="sxs-lookup"><span data-stu-id="b0ca0-141">DimDate</span></span>     | <span data-ttu-id="b0ca0-142">Дата</span><span class="sxs-lookup"><span data-stu-id="b0ca0-142">Date</span></span>        | <span data-ttu-id="b0ca0-143">Нет</span><span class="sxs-lookup"><span data-stu-id="b0ca0-143">No</span></span>     |
    | <span data-ttu-id="b0ca0-144">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b0ca0-144">FactResellerSales</span></span> | <span data-ttu-id="b0ca0-145">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="b0ca0-145">ShipDateKey</span></span>  | <span data-ttu-id="b0ca0-146">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b0ca0-146">Default</span></span>            | <span data-ttu-id="b0ca0-147">DimDate</span><span class="sxs-lookup"><span data-stu-id="b0ca0-147">DimDate</span></span>     | <span data-ttu-id="b0ca0-148">Дата</span><span class="sxs-lookup"><span data-stu-id="b0ca0-148">Date</span></span>        | <span data-ttu-id="b0ca0-149">Нет</span><span class="sxs-lookup"><span data-stu-id="b0ca0-149">No</span></span>     |
    | <span data-ttu-id="b0ca0-150">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b0ca0-150">FactResellerSales</span></span> | <span data-ttu-id="b0ca0-151">ProductKey</span><span class="sxs-lookup"><span data-stu-id="b0ca0-151">ProductKey</span></span>   | <span data-ttu-id="b0ca0-152">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b0ca0-152">Default</span></span>            | <span data-ttu-id="b0ca0-153">DimProduct</span><span class="sxs-lookup"><span data-stu-id="b0ca0-153">DimProduct</span></span>  | <span data-ttu-id="b0ca0-154">ProductKey</span><span class="sxs-lookup"><span data-stu-id="b0ca0-154">ProductKey</span></span>  | <span data-ttu-id="b0ca0-155">Да</span><span class="sxs-lookup"><span data-stu-id="b0ca0-155">Yes</span></span>    |
    | <span data-ttu-id="b0ca0-156">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="b0ca0-156">FactResellerSales</span></span> | <span data-ttu-id="b0ca0-157">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="b0ca0-157">EmployeeKey</span></span>  | <span data-ttu-id="b0ca0-158">В обе таблицы</span><span class="sxs-lookup"><span data-stu-id="b0ca0-158">To Both Tables</span></span> | <span data-ttu-id="b0ca0-159">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="b0ca0-159">DimEmployee</span></span> | <span data-ttu-id="b0ca0-160">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="b0ca0-160">EmployeeKey</span></span> | <span data-ttu-id="b0ca0-161">Да</span><span class="sxs-lookup"><span data-stu-id="b0ca0-161">Yes</span></span>    |

5. <span data-ttu-id="b0ca0-162">В таблице **DimEmployee** создайте следующие [вычисляемые столбцы](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="b0ca0-162">In the **DimEmployee** table, create the following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="b0ca0-163">**Путь**</span><span class="sxs-lookup"><span data-stu-id="b0ca0-163">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="b0ca0-164">**FullName**</span><span class="sxs-lookup"><span data-stu-id="b0ca0-164">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="b0ca0-165">**Level1**</span><span class="sxs-lookup"><span data-stu-id="b0ca0-165">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="b0ca0-166">**Level2**</span><span class="sxs-lookup"><span data-stu-id="b0ca0-166">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="b0ca0-167">**Level3**</span><span class="sxs-lookup"><span data-stu-id="b0ca0-167">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="b0ca0-168">**Level4**</span><span class="sxs-lookup"><span data-stu-id="b0ca0-168">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="b0ca0-169">**Level5**</span><span class="sxs-lookup"><span data-stu-id="b0ca0-169">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="b0ca0-170">В таблице **DimEmployee** создайте [иерархию](../tutorials/aas-lesson-9-create-hierarchies.md) с именем **Organization**.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-170">In the **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="b0ca0-171">Добавьте следующие столбцы в указанном порядке: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-171">Add the following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="b0ca0-172">В таблице **FactResellerSales** создайте следующую [меру](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="b0ca0-172">In the **FactResellerSales** table, create the following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="b0ca0-173">Используйте функцию [Анализ в Excel](../tutorials/aas-lesson-12-analyze-in-excel.md), чтобы открыть Excel и автоматически создать сводную таблицу.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-173">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) to open Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="b0ca0-174">В области **Поля сводной таблицы** добавьте иерархию **Organization** из таблицы **DimEmployee** в поле **Строки** и меру **ResellerTotalSales** из таблицы **FactResellerSales** в поле **Значения**.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-174">In **PivotTable Fields**, add the **Organization** hierarchy from the **DimEmployee** table to **Rows**, and the **ResellerTotalSales** measure from the **FactResellerSales**  table to **Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="b0ca0-176">Как можно видеть в сводной таблице, иерархия отображает неоднородные строки.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-176">As you can see in the PivotTable, the hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="b0ca0-177">Имеется множество строк с пустыми членами.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-177">There are many rows where blank members are shown.</span></span>

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a><span data-ttu-id="b0ca0-178">Исправление неоднородной иерархии с помощью установки свойства "Скрыть члены"</span><span class="sxs-lookup"><span data-stu-id="b0ca0-178">To fix the ragged hierarchy by setting the Hide members property</span></span>

1.  <span data-ttu-id="b0ca0-179">В **обозревателе табличных моделей** разверните пункт **Таблицы** > **DimEmployee** > **Иерархии** > **Organization**.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-179">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="b0ca0-180">В области **Свойства** > **Скрыть члены** выберите **Скрыть пустые члены**.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-180">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="b0ca0-182">Вернитесь в Excel и обновите сводную таблицу.</span><span class="sxs-lookup"><span data-stu-id="b0ca0-182">Back in Excel, refresh the PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="b0ca0-184">Теперь все выглядит гораздо лучше!</span><span class="sxs-lookup"><span data-stu-id="b0ca0-184">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="b0ca0-185">См. также</span><span class="sxs-lookup"><span data-stu-id="b0ca0-185">See Also</span></span>   
[<span data-ttu-id="b0ca0-186">Занятие 9. Создание иерархий</span><span class="sxs-lookup"><span data-stu-id="b0ca0-186">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="b0ca0-187">Дополнительное занятие. Динамическая безопасность</span><span class="sxs-lookup"><span data-stu-id="b0ca0-187">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="b0ca0-188">Дополнительное занятие. Строки детализации</span><span class="sxs-lookup"><span data-stu-id="b0ca0-188">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  