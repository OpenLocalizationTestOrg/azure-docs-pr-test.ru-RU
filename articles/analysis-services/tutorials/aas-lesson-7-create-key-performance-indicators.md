---
<span data-ttu-id="ed1f6-101">Заголовок: aaa «занятие учебника по Azure Analysis Services 7: Создание ключевых показателей эффективности | Документы Microsoft» Описание: описание, как toocreate ключевых показателей эффективности в hello проекта tutorial служб Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-101">title: aaa"Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs" description: Describes how toocreate Key Performance Indicators in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="ed1f6-102">службы: documentationcenter служб analysis services: '' Автор: диспетчер minewiskan: редактор erikre: '' теги: ''</span><span class="sxs-lookup"><span data-stu-id="ed1f6-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="ed1f6-103">MS.AssetId: ms.service: ms.devlang служб analysis services: н/д ms.topic: get-started-article ms.tgt_pltfrm: ms.workload н/д: н/д ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="ed1f6-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="ed1f6-104">Занятие 7. Создание ключевых показателей эффективности</span><span class="sxs-lookup"><span data-stu-id="ed1f6-104">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ed1f6-105">В этом занятии вы создадите ключевые показатели эффективности (КПЭ).</span><span class="sxs-lookup"><span data-stu-id="ed1f6-105">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="ed1f6-106">Ключевые показатели эффективности, используемые toogauge производительность значения, определенного *базы* измерения, от *целевой* значения, также определенного мерой или абсолютным значением.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-106">KPIs are used toogauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="ed1f6-107">В службах reporting клиентских приложений, ключевые показатели эффективности предоставляют бизнесменам быстрый и простой способ toounderstand сводку по бизнес-успех или tooidentify трендов.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-107">In reporting client applications, KPIs can provide business professionals a quick and easy way toounderstand a summary of business success or tooidentify trends.</span></span> <span data-ttu-id="ed1f6-108">toolearn более, в разделе [ключевые показатели эффективности](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="ed1f6-108">toolearn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="ed1f6-109">Предполагаемое время toocomplete на этом занятии: **15 минут**</span><span class="sxs-lookup"><span data-stu-id="ed1f6-109">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ed1f6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ed1f6-110">Prerequisites</span></span>  
<span data-ttu-id="ed1f6-111">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ed1f6-112">Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [Lesson 6: создание мер](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="ed1f6-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="ed1f6-113">Создание ключевых показателей эффективности</span><span class="sxs-lookup"><span data-stu-id="ed1f6-113">Create Key Performance Indicators</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="ed1f6-114">toocreate InternetCurrentQuarterSalesPerformance ключевого показателя Эффективности</span><span class="sxs-lookup"><span data-stu-id="ed1f6-114">toocreate an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="ed1f6-115">В конструкторе моделей hello щелкните hello **FactInternetSales** таблицы.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-115">In hello model designer, click hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="ed1f6-116">В сетке мер hello щелкните пустую ячейку.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-116">In hello measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="ed1f6-117">В строке формул hello над таблицей hello введите hello следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="ed1f6-117">In hello formula bar, above hello table, type hello following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="ed1f6-118">Эта мера служит hello базовой мерой для ключевого показателя Эффективности hello.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-118">This measure serves as hello Base measure for hello KPI.</span></span>  
  
4.  <span data-ttu-id="ed1f6-119">Щелкните правой кнопкой мыши **InternetCurrentQuarterSalesPerformance** > **Создать ключевой показатель эффективности**.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-119">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="ed1f6-120">В диалоговом окне ключевого индикатора производительности (KPI) hello в **целевой** выберите **абсолютное значение**, а затем введите **1.1**.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-120">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="ed1f6-121">Введите в поле слева (низкий) ползунок hello **1**, а затем в правом (верхнем) ползунок hello введите **1.07**.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-121">In hello left (low) slider field, type **1**, and then in hello right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="ed1f6-122">В **Выбор стиля значков**выберите hello ромб (красный), треугольник (желтый), круг (зеленый) значок типа.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-122">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="ed1f6-124">Расширяемый hello уведомление **описания** подпись под hello доступными стилями значков.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-124">Notice hello expandable **Descriptions** label below hello available icon styles.</span></span> <span data-ttu-id="ed1f6-125">Используйте для hello описания различных toomake элементы ключевого показателя Эффективности их идентификацию в клиентских приложениях.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-125">Use descriptions for hello various KPI elements toomake them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="ed1f6-126">Нажмите кнопку **ОК** toocomplete hello ключевого показателя Эффективности.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-126">Click **OK** toocomplete hello KPI.</span></span>  
  
    <span data-ttu-id="ed1f6-127">В сетке мер hello, обратите внимание, далее toohello hello значок **InternetCurrentQuarterSalesPerformance** мер.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-127">In hello measure grid, notice hello icon next toohello **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="ed1f6-128">Он указывает, что мера служит базовым значением для КПЭ.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-128">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="ed1f6-129">toocreate InternetCurrentQuarterMarginPerformance ключевого показателя Эффективности</span><span class="sxs-lookup"><span data-stu-id="ed1f6-129">toocreate an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="ed1f6-130">В сетке мер hello hello **FactInternetSales** таблицы, щелкните пустую ячейку.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-130">In hello measure grid for hello **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="ed1f6-131">В строке формул hello над таблицей hello введите hello следующую формулу:</span><span class="sxs-lookup"><span data-stu-id="ed1f6-131">In hello formula bar, above hello table, type hello following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="ed1f6-132">Щелкните правой кнопкой мыши **InternetCurrentQuarterMarginPerformance** > **Создать ключевой показатель эффективности**.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-132">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="ed1f6-133">В диалоговом окне ключевого индикатора производительности (KPI) hello в **целевой** выберите **абсолютное значение**, а затем введите **1.25**.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-133">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="ed1f6-134">В (hello левом нижнем) поле ползунка, слайдов, пока не отобразится поле hello **0,8**, и затем hello слайд правой поле ползунка (высокий), пока не отобразится поле hello **1.03**.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-134">In hello left (low) slider field, slide until hello field displays **0.8**, and then slide hello right (high) slider field, until hello field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="ed1f6-135">В **Выбор стиля значков**, выберите hello ромб (красный), треугольник (желтый), круг (зеленый) тип значка и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ed1f6-135">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="ed1f6-136">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="ed1f6-136">What's next?</span></span>
<span data-ttu-id="ed1f6-137">[Занятие 8. Создание перспектив](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="ed1f6-137">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
