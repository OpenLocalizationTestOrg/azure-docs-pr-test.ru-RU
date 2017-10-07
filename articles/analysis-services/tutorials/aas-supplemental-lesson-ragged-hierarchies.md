---
<span data-ttu-id="4242a-101">Заголовок: aaa» Azure Analysis Services tutorial дополнительного занятия: неоднородные иерархии | Документы Microsoft» Описание: описание, как toofix неоднородные иерархии в учебнике hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="4242a-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs" description: Describes how toofix ragged hierarchies in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="4242a-102">службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''</span><span class="sxs-lookup"><span data-stu-id="4242a-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="4242a-103">MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="4242a-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="4242a-104">Дополнительное занятие. Неоднородные иерархии</span><span class="sxs-lookup"><span data-stu-id="4242a-104">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="4242a-105">В этом дополнительном занятии вы устраните распространенную проблему, которая возникает при сведении иерархий, содержащих пустые значения (члены) на различных уровнях.</span><span class="sxs-lookup"><span data-stu-id="4242a-105">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="4242a-106">Например, организация, где прямыми подчиненными высокопоставленного руководителя являются как руководители подразделений, так и не руководящие работники.</span><span class="sxs-lookup"><span data-stu-id="4242a-106">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="4242a-107">Или географические иерархии, состоящие из комбинации страна+регион+город, где некоторые города не относятся к конкретному штату или конкретной провинции, например Вашингтон, округ Колумбия, или Ватикан.</span><span class="sxs-lookup"><span data-stu-id="4242a-107">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="4242a-108">Если пустые элементы иерархии, его часто заканчиваются toodifferent или неоднородной, уровни.</span><span class="sxs-lookup"><span data-stu-id="4242a-108">When a hierarchy has blank members, it often descends toodifferent, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="4242a-110">Табличные модели на уровне совместимости hello 1400 имеют дополнительный **скрыть элементы** свойство для иерархии.</span><span class="sxs-lookup"><span data-stu-id="4242a-110">Tabular models at hello 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="4242a-111">Hello **по умолчанию** предполагается нет пустой членов на любом уровне.</span><span class="sxs-lookup"><span data-stu-id="4242a-111">hello **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="4242a-112">Hello **скрыть пустые элементы** позволяет исключить пустые элементы из иерархии hello при добавлении tooa сводной таблице или отчете.</span><span class="sxs-lookup"><span data-stu-id="4242a-112">hello **Hide blank members** setting excludes blank members from hello hierarchy when added tooa PivotTable or report.</span></span>  
  
<span data-ttu-id="4242a-113">Предполагаемое время toocomplete на этом занятии: **20 минут**</span><span class="sxs-lookup"><span data-stu-id="4242a-113">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="4242a-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4242a-114">Prerequisites</span></span>  
<span data-ttu-id="4242a-115">Это дополнительное занятие входит в учебник по табличному моделированию.</span><span class="sxs-lookup"><span data-stu-id="4242a-115">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="4242a-116">Перед выполнением задачи hello в этом дополнительном занятии, необходимо завершить все предыдущие занятия или иметь завершенный проект образце модели Интернет-продаж Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="4242a-116">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="4242a-117">При создании проекта Интернет-продаж AW hello hello учебника по модели не еще содержит любые данные или неровными иерархиями.</span><span class="sxs-lookup"><span data-stu-id="4242a-117">If you've created hello AW Internet Sales project as part of hello tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="4242a-118">toocomplete этого дополнительного занятия необходимо определить toocreate Здравствуйте проблему, добавив некоторые дополнительные таблицы, создавать связи, вычисляемые столбцы, меры и новую иерархию организации.</span><span class="sxs-lookup"><span data-stu-id="4242a-118">toocomplete this supplemental lesson, you first have toocreate hello problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="4242a-119">Эта часть займет около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="4242a-119">That part takes about 15 minutes.</span></span> <span data-ttu-id="4242a-120">После этого вы получаете toosolve его через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4242a-120">Then, you get toosolve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="4242a-121">Добавление таблиц и объектов</span><span class="sxs-lookup"><span data-stu-id="4242a-121">Add tables and objects</span></span>
  
### <a name="tooadd-new-tables-tooyour-model"></a><span data-ttu-id="4242a-122">tooadd новой таблицы tooyour модели</span><span class="sxs-lookup"><span data-stu-id="4242a-122">tooadd new tables tooyour model</span></span>
  
1.  <span data-ttu-id="4242a-123">В обозревателе табличных моделей разверните пункт **Источники данных**, щелкните правой кнопкой мыши подключение и выберите элемент **Импортировать новые таблицы**.</span><span class="sxs-lookup"><span data-stu-id="4242a-123">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="4242a-124">В навигаторе выберите **DimEmployee** и **FactResellerSales**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4242a-124">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="4242a-125">В редакторе запросов щелкните элемент **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="4242a-125">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="4242a-126">Создайте ниже hello [связи](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="4242a-126">Create hello following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="4242a-127">Таблица 1</span><span class="sxs-lookup"><span data-stu-id="4242a-127">Table 1</span></span>           | <span data-ttu-id="4242a-128">столбец</span><span class="sxs-lookup"><span data-stu-id="4242a-128">Column</span></span>       | <span data-ttu-id="4242a-129">Направление фильтра</span><span class="sxs-lookup"><span data-stu-id="4242a-129">Filter Direction</span></span>   | <span data-ttu-id="4242a-130">Таблица 2</span><span class="sxs-lookup"><span data-stu-id="4242a-130">Table 2</span></span>     | <span data-ttu-id="4242a-131">столбец</span><span class="sxs-lookup"><span data-stu-id="4242a-131">Column</span></span>      | <span data-ttu-id="4242a-132">Активна</span><span class="sxs-lookup"><span data-stu-id="4242a-132">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="4242a-133">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="4242a-133">FactResellerSales</span></span> | <span data-ttu-id="4242a-134">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="4242a-134">OrderDateKey</span></span> | <span data-ttu-id="4242a-135">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4242a-135">Default</span></span>            | <span data-ttu-id="4242a-136">DimDate</span><span class="sxs-lookup"><span data-stu-id="4242a-136">DimDate</span></span>     | <span data-ttu-id="4242a-137">Дата</span><span class="sxs-lookup"><span data-stu-id="4242a-137">Date</span></span>        | <span data-ttu-id="4242a-138">Да</span><span class="sxs-lookup"><span data-stu-id="4242a-138">Yes</span></span>    |
    | <span data-ttu-id="4242a-139">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="4242a-139">FactResellerSales</span></span> | <span data-ttu-id="4242a-140">DueDate</span><span class="sxs-lookup"><span data-stu-id="4242a-140">DueDate</span></span>      | <span data-ttu-id="4242a-141">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4242a-141">Default</span></span>            | <span data-ttu-id="4242a-142">DimDate</span><span class="sxs-lookup"><span data-stu-id="4242a-142">DimDate</span></span>     | <span data-ttu-id="4242a-143">Дата</span><span class="sxs-lookup"><span data-stu-id="4242a-143">Date</span></span>        | <span data-ttu-id="4242a-144">Нет</span><span class="sxs-lookup"><span data-stu-id="4242a-144">No</span></span>     |
    | <span data-ttu-id="4242a-145">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="4242a-145">FactResellerSales</span></span> | <span data-ttu-id="4242a-146">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="4242a-146">ShipDateKey</span></span>  | <span data-ttu-id="4242a-147">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4242a-147">Default</span></span>            | <span data-ttu-id="4242a-148">DimDate</span><span class="sxs-lookup"><span data-stu-id="4242a-148">DimDate</span></span>     | <span data-ttu-id="4242a-149">Дата</span><span class="sxs-lookup"><span data-stu-id="4242a-149">Date</span></span>        | <span data-ttu-id="4242a-150">Нет</span><span class="sxs-lookup"><span data-stu-id="4242a-150">No</span></span>     |
    | <span data-ttu-id="4242a-151">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="4242a-151">FactResellerSales</span></span> | <span data-ttu-id="4242a-152">ProductKey</span><span class="sxs-lookup"><span data-stu-id="4242a-152">ProductKey</span></span>   | <span data-ttu-id="4242a-153">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4242a-153">Default</span></span>            | <span data-ttu-id="4242a-154">DimProduct</span><span class="sxs-lookup"><span data-stu-id="4242a-154">DimProduct</span></span>  | <span data-ttu-id="4242a-155">ProductKey</span><span class="sxs-lookup"><span data-stu-id="4242a-155">ProductKey</span></span>  | <span data-ttu-id="4242a-156">Да</span><span class="sxs-lookup"><span data-stu-id="4242a-156">Yes</span></span>    |
    | <span data-ttu-id="4242a-157">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="4242a-157">FactResellerSales</span></span> | <span data-ttu-id="4242a-158">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="4242a-158">EmployeeKey</span></span>  | <span data-ttu-id="4242a-159">tooBoth таблиц</span><span class="sxs-lookup"><span data-stu-id="4242a-159">tooBoth Tables</span></span> | <span data-ttu-id="4242a-160">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="4242a-160">DimEmployee</span></span> | <span data-ttu-id="4242a-161">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="4242a-161">EmployeeKey</span></span> | <span data-ttu-id="4242a-162">Да</span><span class="sxs-lookup"><span data-stu-id="4242a-162">Yes</span></span>    |

5. <span data-ttu-id="4242a-163">В hello **DimEmployee** таблице, создайте следующие hello [вычисляемых столбцов](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="4242a-163">In hello **DimEmployee** table, create hello following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="4242a-164">**Путь**</span><span class="sxs-lookup"><span data-stu-id="4242a-164">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="4242a-165">**FullName**</span><span class="sxs-lookup"><span data-stu-id="4242a-165">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="4242a-166">**Level1**</span><span class="sxs-lookup"><span data-stu-id="4242a-166">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="4242a-167">**Level2**</span><span class="sxs-lookup"><span data-stu-id="4242a-167">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="4242a-168">**Level3**</span><span class="sxs-lookup"><span data-stu-id="4242a-168">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="4242a-169">**Level4**</span><span class="sxs-lookup"><span data-stu-id="4242a-169">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="4242a-170">**Level5**</span><span class="sxs-lookup"><span data-stu-id="4242a-170">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="4242a-171">В hello **DimEmployee** , куда вводится [иерархии](../tutorials/aas-lesson-9-create-hierarchies.md) с именем **организации**.</span><span class="sxs-lookup"><span data-stu-id="4242a-171">In hello **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="4242a-172">Добавьте следующие столбцы в порядке hello: **Level1**, **Level2**, **Level3**, **Level4**, **уровень 5**.</span><span class="sxs-lookup"><span data-stu-id="4242a-172">Add hello following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="4242a-173">В hello **FactResellerSales** таблице, создайте следующие hello [мер](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="4242a-173">In hello **FactResellerSales** table, create hello following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="4242a-174">Используйте [анализ в Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel и автоматически создать сводную таблицу.</span><span class="sxs-lookup"><span data-stu-id="4242a-174">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="4242a-175">В **полей сводной таблицы**, добавить hello **организации** иерархии из hello **DimEmployee** таблице слишком**строк**и hello **ResellerTotalSales** меру из hello **FactResellerSales** таблице слишком**значения**.</span><span class="sxs-lookup"><span data-stu-id="4242a-175">In **PivotTable Fields**, add hello **Organization** hierarchy from hello **DimEmployee** table too**Rows**, and hello **ResellerTotalSales** measure from hello **FactResellerSales**  table too**Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="4242a-177">Как видно в сводной таблице hello hello иерархии отображаются строки, без выравнивания.</span><span class="sxs-lookup"><span data-stu-id="4242a-177">As you can see in hello PivotTable, hello hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="4242a-178">Имеется множество строк с пустыми членами.</span><span class="sxs-lookup"><span data-stu-id="4242a-178">There are many rows where blank members are shown.</span></span>

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a><span data-ttu-id="4242a-179">toofix hello неоднородные иерархии, присвоив свойству hello скрытие членов</span><span class="sxs-lookup"><span data-stu-id="4242a-179">toofix hello ragged hierarchy by setting hello Hide members property</span></span>

1.  <span data-ttu-id="4242a-180">В **обозревателе табличных моделей** разверните пункт **Таблицы** > **DimEmployee** > **Иерархии** > **Organization**.</span><span class="sxs-lookup"><span data-stu-id="4242a-180">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="4242a-181">В области **Свойства** > **Скрыть члены** выберите **Скрыть пустые члены**.</span><span class="sxs-lookup"><span data-stu-id="4242a-181">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="4242a-183">Обратно в Excel обновите hello сводной таблицы.</span><span class="sxs-lookup"><span data-stu-id="4242a-183">Back in Excel, refresh hello PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="4242a-185">Теперь все выглядит гораздо лучше!</span><span class="sxs-lookup"><span data-stu-id="4242a-185">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="4242a-186">См. также</span><span class="sxs-lookup"><span data-stu-id="4242a-186">See Also</span></span>   
[<span data-ttu-id="4242a-187">Занятие 9. Создание иерархий</span><span class="sxs-lookup"><span data-stu-id="4242a-187">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="4242a-188">Дополнительное занятие. Динамическая безопасность</span><span class="sxs-lookup"><span data-stu-id="4242a-188">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="4242a-189">Дополнительное занятие. Строки детализации</span><span class="sxs-lookup"><span data-stu-id="4242a-189">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  