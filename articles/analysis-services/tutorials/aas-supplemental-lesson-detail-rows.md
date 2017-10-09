---
<span data-ttu-id="bbf87-101">Заголовок: aaa» Azure Analysis Services tutorial дополнительного занятия: строки детализации | Документы Microsoft» Описание: описание, как toocreate a выражение строки детализации в hello Azure Analysis Services tutorial.</span><span class="sxs-lookup"><span data-stu-id="bbf87-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="bbf87-102">службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''</span><span class="sxs-lookup"><span data-stu-id="bbf87-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="bbf87-103">MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="bbf87-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="bbf87-104">Дополнительное занятие. Строки детализации</span><span class="sxs-lookup"><span data-stu-id="bbf87-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="bbf87-105">В этом дополнительном занятии используется hello toodefine редактор DAX пользовательское выражение строки детализации.</span><span class="sxs-lookup"><span data-stu-id="bbf87-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="bbf87-106">Выражение строки детализации — это свойство измерения, предоставляя конечным пользователям Дополнительные сведения о результатах hello статистическую обработку меры.</span><span class="sxs-lookup"><span data-stu-id="bbf87-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="bbf87-107">Предполагаемое время toocomplete на этом занятии: **10 минут**</span><span class="sxs-lookup"><span data-stu-id="bbf87-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="bbf87-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bbf87-108">Prerequisites</span></span>  
<span data-ttu-id="bbf87-109">Это дополнительное занятие входит в учебник по табличному моделированию.</span><span class="sxs-lookup"><span data-stu-id="bbf87-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="bbf87-110">Перед выполнением задачи hello в этом дополнительном занятии, необходимо завершить все предыдущие занятия или иметь завершенный проект образце модели Интернет-продаж Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="bbf87-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="bbf87-111">Что делать нам нужно toosolve?</span><span class="sxs-lookup"><span data-stu-id="bbf87-111">What do we need toosolve?</span></span>
<span data-ttu-id="bbf87-112">Давайте взглянем на hello сведений о нашей меры InternetTotalSales, прежде чем добавлять выражение строки детализации.</span><span class="sxs-lookup"><span data-stu-id="bbf87-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="bbf87-113">В SSDT выберите hello **модель** меню > **анализ в Excel** tooopen Excel и создайте пустую сводную таблицу.</span><span class="sxs-lookup"><span data-stu-id="bbf87-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="bbf87-114">В **полей сводной таблицы**, добавить hello **InternetTotalSales** мер из таблицы FactInternetSales hello слишком**значения**, **CalendarYear**из hello DimDate таблице слишком**столбцы**, и **EnglishCountryRegionName** слишком**строк**.</span><span class="sxs-lookup"><span data-stu-id="bbf87-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="bbf87-115">Теперь наши сводной таблицы дает нам сводных результатов из мер InternetTotalSales hello, регионы и года.</span><span class="sxs-lookup"><span data-stu-id="bbf87-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="bbf87-117">Hello сводной таблицы дважды щелкните сводное значение для года, а имя области.</span><span class="sxs-lookup"><span data-stu-id="bbf87-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="bbf87-118">Здесь мы дважды щелкнули значение hello Австралия и hello 2014 года.</span><span class="sxs-lookup"><span data-stu-id="bbf87-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="bbf87-119">Открывается новый лист с данными, но это не те данные, которые нам требуются.</span><span class="sxs-lookup"><span data-stu-id="bbf87-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="bbf87-121">Что мы хотели бы toosee здесь является таблицей, содержащей столбцы и строки данных, которые влияют на результат toohello статистическую обработку меры InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="bbf87-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="bbf87-122">toodo, можно добавить выражение строки детализации как свойство измерения hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="bbf87-123">Добавление выражения строк детализации</span><span class="sxs-lookup"><span data-stu-id="bbf87-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="bbf87-124">toocreate выражение строк детализации</span><span class="sxs-lookup"><span data-stu-id="bbf87-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="bbf87-125">В SSDT, в сетке мер таблицы FactInternetSales hello, щелкните hello **InternetTotalSales** мер.</span><span class="sxs-lookup"><span data-stu-id="bbf87-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="bbf87-126">В **свойства** > **выражение строки детализации**, нажмите кнопку hello редактор кнопка tooopen hello редактор DAX.</span><span class="sxs-lookup"><span data-stu-id="bbf87-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="bbf87-128">В редакторе DAX введите hello, следующее выражение:</span><span class="sxs-lookup"><span data-stu-id="bbf87-128">In DAX Editor, enter hello following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="bbf87-129">Это выражение указывает имена столбцов и мер из таблицы FactInternetSales hello и связанные таблицы результатов при двойном щелчке результат статистической обработки в сводной таблице или отчете.</span><span class="sxs-lookup"><span data-stu-id="bbf87-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="bbf87-130">В Excel удалить лист hello, созданной на шаге 3, а затем дважды щелкните это статистическое выражение.</span><span class="sxs-lookup"><span data-stu-id="bbf87-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="bbf87-131">На этот раз со свойством выражение строки детализации, определенные для меры hello, новый лист открывается с гораздо более полезными данными.</span><span class="sxs-lookup"><span data-stu-id="bbf87-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="bbf87-133">Разверните модель заново.</span><span class="sxs-lookup"><span data-stu-id="bbf87-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="bbf87-134">См. также</span><span class="sxs-lookup"><span data-stu-id="bbf87-134">See Also</span></span>  
<span data-ttu-id="bbf87-135">[Функция SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="bbf87-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="bbf87-136">Дополнительное занятие. Динамическая безопасность</span><span class="sxs-lookup"><span data-stu-id="bbf87-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="bbf87-137">Дополнительное занятие. Неоднородные иерархии</span><span class="sxs-lookup"><span data-stu-id="bbf87-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
