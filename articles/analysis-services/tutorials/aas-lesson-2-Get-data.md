---
<span data-ttu-id="b073c-101">Заголовок: aaa» Azure Analysis Services учебника lesson 2: получение данных | Документы Microsoft» Описание: описание, как tooget и импорта данных в hello проекта tutorial служб Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b073c-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="b073c-102">службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''</span><span class="sxs-lookup"><span data-stu-id="b073c-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="b073c-103">MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: н/д ms.workload: н/д ms.date: ms.author 06/01/2017 г.: owend</span><span class="sxs-lookup"><span data-stu-id="b073c-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="b073c-104">Занятие 2. Получение данных</span><span class="sxs-lookup"><span data-stu-id="b073c-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b073c-105">На этом занятии использовать получение данных в SSDT tooconnect toohello AdventureWorksDW2014 образца базы данных, выберите данные, просмотр и фильтрация и затем импортировать в рабочую область модели.</span><span class="sxs-lookup"><span data-stu-id="b073c-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="b073c-106">С помощью функции получения данных можно импортировать данные из самых разнообразных источников: базы данных SQL Azure, Oracle, Sybase, канала OData, Teradata, файлов и других.</span><span class="sxs-lookup"><span data-stu-id="b073c-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="b073c-107">Данные также можно запросить с помощью выражения формулы Power Query M.</span><span class="sxs-lookup"><span data-stu-id="b073c-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="b073c-108">Предполагаемое время toocomplete на этом занятии: **10 минут**</span><span class="sxs-lookup"><span data-stu-id="b073c-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b073c-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b073c-109">Prerequisites</span></span>  
<span data-ttu-id="b073c-110">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="b073c-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b073c-111">Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятия 1: Создание нового проекта табличной модели](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="b073c-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="b073c-112">Создание подключения</span><span class="sxs-lookup"><span data-stu-id="b073c-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="b073c-113">toocreate toohello AdventureWorksDW2014 подключения базы данных</span><span class="sxs-lookup"><span data-stu-id="b073c-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="b073c-114">В обозревателе табличных моделей щелкните правой кнопкой мыши **Источники данных** > **Импорт из источника данных**.</span><span class="sxs-lookup"><span data-stu-id="b073c-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="b073c-115">Получение данных, который поможет подключения источника данных tooa будет запущен.</span><span class="sxs-lookup"><span data-stu-id="b073c-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="b073c-116">Если вы не видите обозревателе табличной модели в **обозревателе решений**, дважды щелкните **Model.bim** tooopen hello модели в конструкторе hello.</span><span class="sxs-lookup"><span data-stu-id="b073c-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="b073c-118">В области функции получения данных щелкните **База данных** > **База данных SQL Server** > **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="b073c-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="b073c-119">В hello **базы данных SQL Server** диалоговое окно, в **сервера**, введите имя hello hello сервера, где установлен hello AdventureWorksDW2014 базы данных и нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="b073c-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="b073c-120">При появлении запроса учетных данных tooenter, необходимо иметь учетные данные hello toospecify, службы Analysis Services используют источник данных tooconnect toohello при импорте и обработке данных.</span><span class="sxs-lookup"><span data-stu-id="b073c-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="b073c-121">В области **Режим олицетворения** выберите **Олицетворить учетную запись**, а затем введите учетные данные и нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="b073c-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="b073c-122">Рекомендуется использовать учетную запись, где hello срок действия пароля не ограничен.</span><span class="sxs-lookup"><span data-stu-id="b073c-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="b073c-124">Использование учетной записи пользователя Windows и пароль обеспечивает наиболее безопасный метод подключения источника данных tooa hello.</span><span class="sxs-lookup"><span data-stu-id="b073c-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="b073c-125">Выберите в навигаторе hello **AdventureWorksDW2014** базы данных, а затем нажмите кнопку **ОК**. При этом создается подключение hello toohello к базе данных.</span><span class="sxs-lookup"><span data-stu-id="b073c-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="b073c-126">Выберите в навигаторе Здравствуйте, флажок для hello следующие таблицы: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, и **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="b073c-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="b073c-128">После нажатия кнопки "ОК" откроется редактор запросов.</span><span class="sxs-lookup"><span data-stu-id="b073c-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="b073c-129">В следующем разделе hello следует выбрать только те данные hello, которые вы хотите tooimport.</span><span class="sxs-lookup"><span data-stu-id="b073c-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="b073c-130">Фильтрация данных таблицы hello</span><span class="sxs-lookup"><span data-stu-id="b073c-130">Filter hello table data</span></span>  
<span data-ttu-id="b073c-131">Таблицы в образце базы данных hello AdventureWorksDW2014 имеют данных, не требуется tooinclude в модели.</span><span class="sxs-lookup"><span data-stu-id="b073c-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="b073c-132">Если это возможно, требуется toofilter места в памяти toosave ненужные данные, используемые моделью hello.</span><span class="sxs-lookup"><span data-stu-id="b073c-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="b073c-133">Вам отфильтровать hello столбцы из таблиц, поэтому их не импорта в базу данных модели hello hello база данных рабочей области, или после его развертывания.</span><span class="sxs-lookup"><span data-stu-id="b073c-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="b073c-134">данные таблицы hello toofilter перед импортом</span><span class="sxs-lookup"><span data-stu-id="b073c-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="b073c-135">В редакторе запросов выберите hello **DimCustomer** таблицы.</span><span class="sxs-lookup"><span data-stu-id="b073c-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="b073c-136">Откроется представление таблицы DimCustomer hello в источник данных hello (AdventureWorksDWQ2014 образца базы данных).</span><span class="sxs-lookup"><span data-stu-id="b073c-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="b073c-137">Выполните множественный выбор (CTRL+щелчок мышью) элементов **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, а затем щелкните правой кнопкой мыши и выберите пункт **Удалить столбцы**.</span><span class="sxs-lookup"><span data-stu-id="b073c-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="b073c-139">Поскольку hello значения для этих столбцов не применимо tooInternet анализа продаж, нет нет необходимости tooimport эти столбцы.</span><span class="sxs-lookup"><span data-stu-id="b073c-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="b073c-140">После удаления ненужных столбцов модель становится компактнее и эффективнее.</span><span class="sxs-lookup"><span data-stu-id="b073c-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="b073c-141">Отфильтруйте оставшиеся таблицы, удалив следующие столбцы в каждой таблице hello hello:</span><span class="sxs-lookup"><span data-stu-id="b073c-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="b073c-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="b073c-142">**DimDate**</span></span>
    
      |<span data-ttu-id="b073c-143">столбец</span><span class="sxs-lookup"><span data-stu-id="b073c-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="b073c-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="b073c-144">DateKey</span></span>|  
      |<span data-ttu-id="b073c-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="b073c-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="b073c-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="b073c-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="b073c-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="b073c-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="b073c-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="b073c-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="b073c-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="b073c-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="b073c-150">столбец</span><span class="sxs-lookup"><span data-stu-id="b073c-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="b073c-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="b073c-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="b073c-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="b073c-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="b073c-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="b073c-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="b073c-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="b073c-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="b073c-155">столбец</span><span class="sxs-lookup"><span data-stu-id="b073c-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="b073c-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="b073c-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="b073c-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="b073c-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="b073c-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="b073c-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="b073c-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="b073c-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="b073c-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="b073c-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="b073c-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="b073c-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="b073c-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="b073c-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="b073c-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="b073c-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="b073c-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="b073c-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="b073c-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="b073c-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="b073c-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="b073c-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="b073c-167">столбец</span><span class="sxs-lookup"><span data-stu-id="b073c-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="b073c-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="b073c-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="b073c-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="b073c-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="b073c-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="b073c-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="b073c-171">столбец</span><span class="sxs-lookup"><span data-stu-id="b073c-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="b073c-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="b073c-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="b073c-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="b073c-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="b073c-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="b073c-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="b073c-175">столбец</span><span class="sxs-lookup"><span data-stu-id="b073c-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="b073c-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="b073c-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="b073c-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="b073c-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="b073c-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="b073c-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="b073c-179"><a name="Import"></a>Импорт данных hello выбранных таблиц и столбцов</span><span class="sxs-lookup"><span data-stu-id="b073c-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="b073c-180">Предварительного просмотра и фильтрации ненужных данных, можно импортировать rest hello hello данных, которые требуется.</span><span class="sxs-lookup"><span data-stu-id="b073c-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="b073c-181">Hello мастер импортирует данные таблицы hello вместе со всеми связями между таблицами.</span><span class="sxs-lookup"><span data-stu-id="b073c-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="b073c-182">Новые таблицы и столбцы создаются в модели hello и не импортируется отфильтрованные ранее данные.</span><span class="sxs-lookup"><span data-stu-id="b073c-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="b073c-183">tooimport hello выбранных таблиц и столбцов данных</span><span class="sxs-lookup"><span data-stu-id="b073c-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="b073c-184">Просмотрите выбранные параметры.</span><span class="sxs-lookup"><span data-stu-id="b073c-184">Review your selections.</span></span> <span data-ttu-id="b073c-185">Если все настроено правильно, нажмите кнопку **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="b073c-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="b073c-186">диалоговое окно обработки данных Hello показывает состояние hello данные, импортированные из вашего источника данных в базу данных рабочей области.</span><span class="sxs-lookup"><span data-stu-id="b073c-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="b073c-188">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="b073c-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="b073c-189">Сохранение проекта модели</span><span class="sxs-lookup"><span data-stu-id="b073c-189">Save your model project</span></span>  
<span data-ttu-id="b073c-190">Очень важно toofrequently сохранять проект модели.</span><span class="sxs-lookup"><span data-stu-id="b073c-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="b073c-191">проект модели toosave hello</span><span class="sxs-lookup"><span data-stu-id="b073c-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="b073c-192">Щелкните **Файл** > **Сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="b073c-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="b073c-193">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="b073c-193">What's next?</span></span>
<span data-ttu-id="b073c-194">[Занятие 3. Обозначение таблицы дат](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="b073c-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
