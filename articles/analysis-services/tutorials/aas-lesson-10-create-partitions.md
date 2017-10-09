---
<span data-ttu-id="a9617-101">Заголовок: aaa «занятие учебника Azure Analysis Services 10: Создание разделов | Документы Microsoft» Описание: описание как toocreate секции в проект tutorial служб Azure Analysis Services hello.</span><span class="sxs-lookup"><span data-stu-id="a9617-101">title: aaa"Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs" description: Describes how toocreate partitions in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="a9617-102">службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''</span><span class="sxs-lookup"><span data-stu-id="a9617-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="a9617-103">MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="a9617-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="a9617-104">Занятие 10. Создание секций</span><span class="sxs-lookup"><span data-stu-id="a9617-104">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="a9617-105">На этом занятии создайте таблицу FactInternetSales hello toodivide секций на более мелкие логические части, которые могут быть обработан (Обновить) независимо от других секций.</span><span class="sxs-lookup"><span data-stu-id="a9617-105">In this lesson, you create partitions toodivide hello FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="a9617-106">По умолчанию каждая таблица, включить в модель имеет одну секцию, которая включает все таблицы hello столбцов и строк.</span><span class="sxs-lookup"><span data-stu-id="a9617-106">By default, every table you include in your model has one partition, which includes all hello table’s columns and rows.</span></span> <span data-ttu-id="a9617-107">Для таблицы FactInternetSales hello мы хотим toodivide hello данные по годам; одну секцию для каждой таблицы hello пять лет.</span><span class="sxs-lookup"><span data-stu-id="a9617-107">For hello FactInternetSales table, we want toodivide hello data by year; one partition for each of hello table’s five years.</span></span> <span data-ttu-id="a9617-108">После этого каждую секцию можно будет обрабатывать отдельно.</span><span class="sxs-lookup"><span data-stu-id="a9617-108">Each partition can then be processed independently.</span></span> <span data-ttu-id="a9617-109">toolearn более, в разделе [секций](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="a9617-109">toolearn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="a9617-110">Предполагаемое время toocomplete на этом занятии: **15 минут**</span><span class="sxs-lookup"><span data-stu-id="a9617-110">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="a9617-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a9617-111">Prerequisites</span></span>  
<span data-ttu-id="a9617-112">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="a9617-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="a9617-113">Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятии 9: создание иерархий](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="a9617-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="a9617-114">Создание секций</span><span class="sxs-lookup"><span data-stu-id="a9617-114">Create partitions</span></span>  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a><span data-ttu-id="a9617-115">toocreate секций таблицы FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="a9617-115">toocreate partitions in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="a9617-116">В обозревателе табличных моделей разверните пункт **Таблицы** и щелкните правой кнопкой мыши **FactInternetSales** > **Секции**.</span><span class="sxs-lookup"><span data-stu-id="a9617-116">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="a9617-117">Щелкните в диспетчере секций **копирования**, измените имя hello слишком**FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="a9617-117">In Partition Manager, click **Copy**, and then change hello name too**FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="a9617-118">Так как вы хотите tooinclude секции hello только те строки, в течение определенного периода, за год hello 2010, необходимо изменить выражение запроса hello.</span><span class="sxs-lookup"><span data-stu-id="a9617-118">Because you want hello partition tooinclude only those rows within a certain period, for hello year 2010, you must modify hello query expression.</span></span>
  
4.  <span data-ttu-id="a9617-119">Нажмите кнопку **разработки** tooopen редактор запросов, а затем нажмите кнопку hello **FactInternetSales2010** запроса.</span><span class="sxs-lookup"><span data-stu-id="a9617-119">Click **Design** tooopen Query Editor, and then click hello **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="a9617-120">В режиме предварительного просмотра, нажмите кнопку hello стрелки вниз в hello **OrderDate** заголовок столбца, а затем щелкните **фильтров даты и времени** > **между**.</span><span class="sxs-lookup"><span data-stu-id="a9617-120">In preview, click hello down arrow in hello **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="a9617-122">В диалоговом окне фильтр строк hello в **отображает строки, где: OrderDate**, оставьте **после или равно**и введите в поля «Дата» hello **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="a9617-122">In hello Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in hello date field, enter **1/1/2010**.</span></span> <span data-ttu-id="a9617-123">Оставьте hello **и** оператор выбран, выберите **перед**, введите в поля «Дата» hello **1/1/2011**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a9617-123">Leave hello **And** operator selected, then select **is before**, then in hello date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="a9617-125">В разделе "Примененные шаги" редактора запросов появится еще один шаг с именем "Строки с примененным фильтром".</span><span class="sxs-lookup"><span data-stu-id="a9617-125">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="a9617-126">Этот фильтр рекомендуется только даты заказа tooselect 2010.</span><span class="sxs-lookup"><span data-stu-id="a9617-126">This filter is tooselect only order dates from 2010.</span></span>

8.  <span data-ttu-id="a9617-127">Щелкните **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="a9617-127">Click **Import**.</span></span>

    <span data-ttu-id="a9617-128">В диспетчере секций Обратите внимание запросов hello, теперь выражение имеет дополнительное предложение фильтрации строк.</span><span class="sxs-lookup"><span data-stu-id="a9617-128">In Partition Manager, notice hello query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="a9617-130">Эта инструкция указывает, что эта секция должна включать только данные hello в этих строках, где hello OrderDate — в hello 2010 календарного года, как указано в предложении hello отфильтрованные строки.</span><span class="sxs-lookup"><span data-stu-id="a9617-130">This statement specifies this partition should include only hello data in those rows where hello OrderDate is in hello 2010 calendar year as specified in hello filtered rows clause.</span></span>  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a><span data-ttu-id="a9617-131">toocreate секции для hello 2011 года</span><span class="sxs-lookup"><span data-stu-id="a9617-131">toocreate a partition for hello 2011 year</span></span>  
  
1.  <span data-ttu-id="a9617-132">В списке секций hello выберите hello **FactInternetSales2010** секции был создан и нажмите кнопку **копирования**.</span><span class="sxs-lookup"><span data-stu-id="a9617-132">In hello partitions list, click hello **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="a9617-133">Изменить имя секции hello слишком**FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="a9617-133">Change hello partition name too**FactInternetSales2011**.</span></span> 

    <span data-ttu-id="a9617-134">Toouse редактор запросов toocreate предложение отфильтрованные строки не обязательно.</span><span class="sxs-lookup"><span data-stu-id="a9617-134">You do not need toouse Query Editor toocreate a new filtered rows clause.</span></span> <span data-ttu-id="a9617-135">Так как вы создали копию запроса hello 2010, все, что нужно toodo — убедиться в небольшое изменение в запросе hello для 2011.</span><span class="sxs-lookup"><span data-stu-id="a9617-135">Because you created a copy of hello query for 2010, all you need toodo is make a slight change in hello query for 2011.</span></span>
  
2.  <span data-ttu-id="a9617-136">В **выражение запроса**, в определенном порядке для этой секции tooinclude только те строки hello 2011 года, замените лет hello в предложении фильтрации строк hello с **2011** и **2012**соответственно, например:</span><span class="sxs-lookup"><span data-stu-id="a9617-136">In **Query Expression**, in-order for this partition tooinclude only those rows for hello 2011 year, replace hello years in hello Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="a9617-137">разделы toocreate для 2012, 2013 и 2014.</span><span class="sxs-lookup"><span data-stu-id="a9617-137">toocreate partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="a9617-138">Выполните действия предыдущего hello, создания разделов для 2012, 2013 и 2014, изменение годы hello в hello фильтрации строк предложения tooinclude только строк за этот год.</span><span class="sxs-lookup"><span data-stu-id="a9617-138">Follow hello previous steps, creating partitions for 2012, 2013, and 2014, changing hello years in hello Filtered Rows clause tooinclude only rows for that year.</span></span> 
  

## <a name="delete-hello-factinternetsales-partition"></a><span data-ttu-id="a9617-139">Удалить раздел FactInternetSales hello</span><span class="sxs-lookup"><span data-stu-id="a9617-139">Delete hello FactInternetSales partition</span></span>
<span data-ttu-id="a9617-140">Теперь, когда у вас есть секции для каждого года, можно удалить раздел FactInternetSales hello; Предотвращение перекрытия при выборе всех процесс при обработке секций.</span><span class="sxs-lookup"><span data-stu-id="a9617-140">Now that you have partitions for each year, you can delete hello FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="toodelete-hello-factinternetsales-partition"></a><span data-ttu-id="a9617-141">hello toodelete FactInternetSales секции</span><span class="sxs-lookup"><span data-stu-id="a9617-141">toodelete hello FactInternetSales partition</span></span>
-  <span data-ttu-id="a9617-142">Щелкните раздел FactInternetSales hello и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="a9617-142">Click hello FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="a9617-143">Обработка секций</span><span class="sxs-lookup"><span data-stu-id="a9617-143">Process partitions</span></span>  
<span data-ttu-id="a9617-144">Обратите внимание, в диспетчере секций hello **последней обработки** столбец для каждого из новых секций hello, вы создали показаны эти разделы никогда не будут обработаны.</span><span class="sxs-lookup"><span data-stu-id="a9617-144">In Partition Manager, notice hello **Last Processed** column for each of hello new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="a9617-145">При создании секций, следует запустить эти разделы обработки секций или процесса операции toorefresh hello данные таблицы.</span><span class="sxs-lookup"><span data-stu-id="a9617-145">When you create partitions, you should run a Process Partitions or Process Table operation toorefresh hello data in those partitions.</span></span>  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a><span data-ttu-id="a9617-146">FactInternetSales секций tooprocess hello</span><span class="sxs-lookup"><span data-stu-id="a9617-146">tooprocess hello FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="a9617-147">Нажмите кнопку **ОК** tooclose диспетчер секций.</span><span class="sxs-lookup"><span data-stu-id="a9617-147">Click **OK** tooclose Partition Manager.</span></span>  
  
2.  <span data-ttu-id="a9617-148">Нажмите кнопку hello **FactInternetSales** , а затем нажмите кнопку hello **модели** меню > **процесс** > **Обработка секций**.</span><span class="sxs-lookup"><span data-stu-id="a9617-148">Click hello **FactInternetSales** table, then click hello **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="a9617-149">В диалоговом окне Обработка секций hello, проверьте **режим** задано слишком**обработка по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="a9617-149">In hello Process Partitions dialog box, verify **Mode** is set too**Process Default**.</span></span>  
  
4.  <span data-ttu-id="a9617-150">Установите флажок hello в hello **процесс** столбец для каждого из пяти hello секции был создан, а затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a9617-150">Select hello checkbox in hello **Process** column for each of hello five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="a9617-152">При появлении запроса учетных данных олицетворения, введите имя пользователя Windows hello и пароль, которые указаны в занятии 2.</span><span class="sxs-lookup"><span data-stu-id="a9617-152">If you're prompted for Impersonation credentials, enter hello Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="a9617-153">Hello **обработки данных** диалогового окна и отобразит сведения обработки для каждой секции.</span><span class="sxs-lookup"><span data-stu-id="a9617-153">hello **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="a9617-154">Обратите внимание, что для каждой секции передается разное количество строк.</span><span class="sxs-lookup"><span data-stu-id="a9617-154">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="a9617-155">Каждая секция включает только те строки, для hello года, указанного в предложение WHERE в инструкции SQL hello hello.</span><span class="sxs-lookup"><span data-stu-id="a9617-155">Each partition includes only those rows for hello year specified in hello WHERE clause in hello SQL Statement.</span></span> <span data-ttu-id="a9617-156">После завершения обработки пойти дальше и закройте диалоговое окно приветствия обработки данных.</span><span class="sxs-lookup"><span data-stu-id="a9617-156">When processing is finished, go ahead and close hello Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="a9617-158">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="a9617-158">What's next?</span></span>
<span data-ttu-id="a9617-159">Последовательно выберите toohello занятию: [занятие 11: Создание ролей](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a9617-159">Go toohello next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
