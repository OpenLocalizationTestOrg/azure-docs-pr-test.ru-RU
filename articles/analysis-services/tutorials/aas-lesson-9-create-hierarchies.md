---
<span data-ttu-id="d6b2e-101">Заголовок: aaa «занятие учебника Azure Analysis Services 9: создание иерархий | Документы Microsoft» Описание: службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''</span><span class="sxs-lookup"><span data-stu-id="d6b2e-101">title: aaa"Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs" description: services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="d6b2e-102">MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="d6b2e-102">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="d6b2e-103">Занятие 9. Создание иерархий</span><span class="sxs-lookup"><span data-stu-id="d6b2e-103">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="d6b2e-104">На этом занятии мы создадим иерархии.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="d6b2e-105">Иерархии — это группы столбцов, упорядоченных по уровням. Например, иерархия "География" может иметь подуровни для страны, области, района и города.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-105">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="d6b2e-106">Иерархии могут отображаться отдельно от других столбцов в списке полей отчетов клиентского приложения, что упрощает для клиентов toonavigate пользователей и включения в отчет.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-106">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users toonavigate and include in a report.</span></span> <span data-ttu-id="d6b2e-107">toolearn более, в разделе [иерархий](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="d6b2e-107">toolearn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="d6b2e-108">toocreate иерархии, используйте конструктор моделей hello в *представление диаграммы*.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-108">toocreate hierarchies, use hello model designer in *Diagram View*.</span></span> <span data-ttu-id="d6b2e-109">Создание иерархий и управление ими не поддерживается в представлении данных.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-109">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="d6b2e-110">Предполагаемое время toocomplete на этом занятии: **20 минут**</span><span class="sxs-lookup"><span data-stu-id="d6b2e-110">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="d6b2e-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d6b2e-111">Prerequisites</span></span>  
<span data-ttu-id="d6b2e-112">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="d6b2e-113">Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятии 8: Создание перспектив](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="d6b2e-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="d6b2e-114">Создание иерархий</span><span class="sxs-lookup"><span data-stu-id="d6b2e-114">Create hierarchies</span></span>  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a><span data-ttu-id="d6b2e-115">toocreate иерархию категорий в таблице DimProduct hello</span><span class="sxs-lookup"><span data-stu-id="d6b2e-115">toocreate a Category hierarchy in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="d6b2e-116">В конструкторе моделей hello (представление диаграммы), щелкните правой кнопкой мыши hello **DimProduct** таблицы > **создать иерархию**.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-116">In hello model designer (diagram view), right-click hello **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="d6b2e-117">Появится новая иерархия hello нижней части окна таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-117">A new hierarchy appears at hello bottom of hello table window.</span></span> <span data-ttu-id="d6b2e-118">Переименовать иерархию hello **категории**.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-118">Rename hello hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="d6b2e-119">Щелкните и перетащите hello **ProductCategoryName** toohello столбца нового **категории** иерархии.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-119">Click and drag hello **ProductCategoryName** column toohello new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="d6b2e-120">В hello **категории** иерархии, щелкните правой кнопкой мыши hello **ProductCategoryName** > **переименование**, а затем введите **категории**.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-120">In hello **Category** hierarchy, right-click hello **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="d6b2e-121">Переименование столбца в иерархии не переименовать этот столбец в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-121">Renaming a column in a hierarchy does not rename that column in hello table.</span></span> <span data-ttu-id="d6b2e-122">Столбец в иерархии является просто представлением hello столбца в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-122">A column in a hierarchy is just a representation of hello column in hello table.</span></span>  
  
4.  <span data-ttu-id="d6b2e-123">Щелкните и перетащите hello **ProductSubcategoryName** toohello столбца **категории** иерархии.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-123">Click and drag hello **ProductSubcategoryName** column toohello **Category** hierarchy.</span></span> <span data-ttu-id="d6b2e-124">Назовите его **Subcategory**.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-124">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="d6b2e-125">Щелкните правой кнопкой мыши hello **ModelName** столбца > **добавить toohierarchy**и выберите **категории**.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-125">Right-click hello **ModelName** column > **Add toohierarchy**, and then select **Category**.</span></span> <span data-ttu-id="d6b2e-126">Назовите его **Model**.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-126">Rename it **Model**.</span></span>

6.  <span data-ttu-id="d6b2e-127">Наконец, добавьте **EnglishProductName** toohello иерархию категорий.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-127">Finally, add **EnglishProductName** toohello Category hierarchy.</span></span> <span data-ttu-id="d6b2e-128">Назовите его **Product**.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-128">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a><span data-ttu-id="d6b2e-130">toocreate иерархий в таблицы DimDate hello</span><span class="sxs-lookup"><span data-stu-id="d6b2e-130">toocreate hierarchies in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="d6b2e-131">В hello **DimDate** таблице, создайте иерархию с именем **календаря**.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-131">In hello **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="d6b2e-132">Добавьте следующие столбцы в порядке hello:</span><span class="sxs-lookup"><span data-stu-id="d6b2e-132">Add hello following columns in-order:</span></span>

    *  <span data-ttu-id="d6b2e-133">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="d6b2e-133">CalendarYear</span></span>
    *  <span data-ttu-id="d6b2e-134">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="d6b2e-134">CalendarSemester</span></span>
    *  <span data-ttu-id="d6b2e-135">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="d6b2e-135">CalendarQuarter</span></span>
    *  <span data-ttu-id="d6b2e-136">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="d6b2e-136">MonthCalendar</span></span>
    *  <span data-ttu-id="d6b2e-137">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="d6b2e-137">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="d6b2e-138">В hello **DimDate** , куда вводится **финансовом** иерархии.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-138">In hello **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="d6b2e-139">Следующие hello следующие столбцы в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-139">Include hello following columns in-order:</span></span>  
  
    *  <span data-ttu-id="d6b2e-140">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="d6b2e-140">FiscalYear</span></span>
    *  <span data-ttu-id="d6b2e-141">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="d6b2e-141">FiscalSemester</span></span>
    *  <span data-ttu-id="d6b2e-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="d6b2e-142">FiscalQuarter</span></span>
    *  <span data-ttu-id="d6b2e-143">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="d6b2e-143">MonthCalendar</span></span>
    *  <span data-ttu-id="d6b2e-144">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="d6b2e-144">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="d6b2e-145">Наконец, в hello **DimDate** , куда вводится **ProductionCalendar** иерархии.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-145">Finally, in hello **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="d6b2e-146">Следующие hello следующие столбцы в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="d6b2e-146">Include hello following columns in-order:</span></span>  
    *  <span data-ttu-id="d6b2e-147">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="d6b2e-147">CalendarYear</span></span>
    *  <span data-ttu-id="d6b2e-148">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="d6b2e-148">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="d6b2e-149">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="d6b2e-149">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="d6b2e-150">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="d6b2e-150">What's next?</span></span>
<span data-ttu-id="d6b2e-151">[Занятие 10. Создание разделов](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="d6b2e-151">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
