---
title: "AAA» служб Azure Analysis Services Adventure Works учебника | Документы Microsoft»"
description: "Предоставляет учебник hello Adventure Works для Azure Analysis Services"
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
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a><span data-ttu-id="abf93-103">Azure Analysis Services — учебник по Adventure Works</span><span class="sxs-lookup"><span data-stu-id="abf93-103">Azure Analysis Services - Adventure Works tutorial</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="abf93-104">О том, как в этом учебнике содержатся занятия toocreate и развертывание с помощью табличной модели на уровне совместимости hello 1400 [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span><span class="sxs-lookup"><span data-stu-id="abf93-104">This tutorial provides lessons on how toocreate and deploy a tabular model at hello 1400 compatibility level by using [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  

<span data-ttu-id="abf93-105">Если вы новые службы tooAnalysis и табличного моделирования, изучения этого учебника является быстрым способом toolearn hello как toocreate и развертывание табличной модели.</span><span class="sxs-lookup"><span data-stu-id="abf93-105">If you're new tooAnalysis Services and tabular modeling, completing this tutorial is hello quickest way toolearn how toocreate and deploy a basic tabular model.</span></span> <span data-ttu-id="abf93-106">При наличии необходимых компонентов hello в месте, он должен принимать между двумя toocomplete toothree часов.</span><span class="sxs-lookup"><span data-stu-id="abf93-106">Once you have hello prerequisites in-place, it should take between two toothree hours toocomplete.</span></span>  
  
## <a name="what-you-learn"></a><span data-ttu-id="abf93-107">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="abf93-107">What you learn</span></span>   
  
-   <span data-ttu-id="abf93-108">Как toocreate новой табличной модели проекта в hello **уровень совместимости 1400** в SSDT.</span><span class="sxs-lookup"><span data-stu-id="abf93-108">How toocreate a new tabular model project at hello **1400 compatibility level** in SSDT.</span></span>
  
-   <span data-ttu-id="abf93-109">Как tooimport данных из реляционной базы данных в проект табличной модели.</span><span class="sxs-lookup"><span data-stu-id="abf93-109">How tooimport data from a relational database into a tabular model project.</span></span>  
  
-   <span data-ttu-id="abf93-110">Как toocreate связей между таблицами в модели hello и управление ими.</span><span class="sxs-lookup"><span data-stu-id="abf93-110">How toocreate and manage relationships between tables in hello model.</span></span>  
  
-   <span data-ttu-id="abf93-111">Как toocreate вычисляемые столбцы, меры и ключевые индикаторы производительности, которые помогут пользователям анализировать показатели критически важные для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="abf93-111">How toocreate calculated columns, measures, and Key Performance Indicators that help users analyze critical business metrics.</span></span>  
  
-   <span data-ttu-id="abf93-112">Как toocreate и управление перспективами и иерархиями, которые помогут пользователям более легко просматривать данные модели, предоставляя бизнеса и точки зрения конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="abf93-112">How toocreate and manage perspectives and hierarchies that help users more easily browse model data by providing business and application-specific viewpoints.</span></span>  
  
-   <span data-ttu-id="abf93-113">Как toocreate секций, разделяющих табличные данные на более мелкие логические части, которые могут быть обработаны независимо от других секций.</span><span class="sxs-lookup"><span data-stu-id="abf93-113">How toocreate partitions that divide table data into smaller logical parts that can be processed independent from other partitions.</span></span>  
  
-   <span data-ttu-id="abf93-114">Как toosecure модели объектов и данных путем создания ролей с членами пользователя.</span><span class="sxs-lookup"><span data-stu-id="abf93-114">How toosecure model objects and data by creating roles with user members.</span></span>  
  
-   <span data-ttu-id="abf93-115">Как toodeploy tooan табличной модели **Azure Analysis Services** сервера или локального сервера служб Analysis Services SQL Server 2017 г.</span><span class="sxs-lookup"><span data-stu-id="abf93-115">How toodeploy a tabular model tooan **Azure Analysis Services** server or an on-premises SQL Server 2017 Analysis Services server.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="abf93-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="abf93-116">Prerequisites</span></span>  
<span data-ttu-id="abf93-117">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="abf93-117">toocomplete this tutorial, you need:</span></span>  
  
-   <span data-ttu-id="abf93-118">Azure Analysis Services или служб аналитики SQL Server 2017 г экземпляра toodeploy для модели.</span><span class="sxs-lookup"><span data-stu-id="abf93-118">An Azure Analysis Services or SQL Server 2017 Analysis Services instance toodeploy your model to.</span></span> <span data-ttu-id="abf93-119">Подпишитесь для получения бесплатной [пробной версии служб Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) и [создайте сервер](../analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="abf93-119">Sign up for a free [Azure Analysis Services trial](https://azure.microsoft.com/services/analysis-services/) and [create a server](../analysis-services-create-server.md).</span></span> <span data-ttu-id="abf93-120">Либо зарегистрируйтесь и скачайте [ознакомительную версию для сообщества SQL Server 2017](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span><span class="sxs-lookup"><span data-stu-id="abf93-120">Or, sign up and download [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span></span> 

-   <span data-ttu-id="abf93-121">Хранилище данных SQL Server или хранилище данных SQL Azure с hello [AdventureWorksDW2014 образца базы данных](http://go.microsoft.com/fwlink/?LinkID=335807).</span><span class="sxs-lookup"><span data-stu-id="abf93-121">A SQL Server Data Warehouse or Azure SQL Data Warehouse with hello [AdventureWorksDW2014 sample database](http://go.microsoft.com/fwlink/?LinkID=335807).</span></span> <span data-ttu-id="abf93-122">Этот образец базы данных включает в себя необходимые toocomplete hello данных этого учебника.</span><span class="sxs-lookup"><span data-stu-id="abf93-122">This sample database includes hello data necessary toocomplete this tutorial.</span></span> <span data-ttu-id="abf93-123">Скачайте [бесплатные выпуски SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).</span><span class="sxs-lookup"><span data-stu-id="abf93-123">Download [SQL Server free editions](https://www.microsoft.com/sql-server/sql-server-downloads).</span></span> <span data-ttu-id="abf93-124">Либо зарегистрируйтесь для получения бесплатной [пробной версии базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="abf93-124">Or, sign up for a free [Azure SQL Database trial](https://azure.microsoft.com/services/sql-database/).</span></span> 

    <span data-ttu-id="abf93-125">**Важно:** при установке образца hello базы данных на локальном сервере SQL, и развертывание сервера служб Analysis Services Azure tooan модели, [локального шлюза данных](../analysis-services-gateway.md) является обязательным.</span><span class="sxs-lookup"><span data-stu-id="abf93-125">**Important:** If you install hello sample database on an on-premises SQL Server, and you deploy your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>

-   <span data-ttu-id="abf93-126">Hello последнюю версию [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span><span class="sxs-lookup"><span data-stu-id="abf93-126">hello latest version of [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>

-   <span data-ttu-id="abf93-127">Hello последнюю версию [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="abf93-127">hello latest version of [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>    

-   <span data-ttu-id="abf93-128">Клиентское приложение, например [Power BI Desktop](https://powerbi.microsoft.com/desktop/) или Excel.</span><span class="sxs-lookup"><span data-stu-id="abf93-128">A client application such as [Power BI Desktop](https://powerbi.microsoft.com/desktop/) or Excel.</span></span> 

## <a name="scenario"></a><span data-ttu-id="abf93-129">Сценарий</span><span class="sxs-lookup"><span data-stu-id="abf93-129">Scenario</span></span>  
<span data-ttu-id="abf93-130">В этом учебнике используется вымышленная компания Adventure Works Cycles.</span><span class="sxs-lookup"><span data-stu-id="abf93-130">This tutorial is based on Adventure Works Cycles, a fictitious company.</span></span> <span data-ttu-id="abf93-131">Adventure Works — это большой, многонациональная производственная компания, производящая и реализующая велосипедов, элементы и стандартные toocommercial рынках Северной Америки, Европы и Азии.</span><span class="sxs-lookup"><span data-stu-id="abf93-131">Adventure Works is a large, multinational manufacturing company that produces and distributes bicycles, parts, and accessories toocommercial markets in North America, Europe, and Asia.</span></span> <span data-ttu-id="abf93-132">ней работают 500 сотрудников компании Hello.</span><span class="sxs-lookup"><span data-stu-id="abf93-132">hello company employs 500 workers.</span></span> <span data-ttu-id="abf93-133">Кроме того, на Adventure Works работает несколько региональных групп, относящихся к разным ее рынкам сбыта.</span><span class="sxs-lookup"><span data-stu-id="abf93-133">Additionally, Adventure Works employs several regional sales teams throughout its market base.</span></span> <span data-ttu-id="abf93-134">Проект является toocreate табличную модель для пользователей, отделов продаж и маркетинга tooanalyze данных Интернет-продаж в базы данных AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="abf93-134">Your project is toocreate a tabular model for sales and marketing users tooanalyze Internet sales data in hello AdventureWorksDW database.</span></span>  
  
<span data-ttu-id="abf93-135">toocomplete hello учебника, необходимо выполнить различные занятий.</span><span class="sxs-lookup"><span data-stu-id="abf93-135">toocomplete hello tutorial, you must complete various lessons.</span></span> <span data-ttu-id="abf93-136">каждое из которых содержит определенную задачу.</span><span class="sxs-lookup"><span data-stu-id="abf93-136">In each lesson, there are tasks.</span></span> <span data-ttu-id="abf93-137">Выполнение каждой задачи в порядке является обязательным для завершения занятия hello.</span><span class="sxs-lookup"><span data-stu-id="abf93-137">Completing each task in order is necessary for completing hello lesson.</span></span> <span data-ttu-id="abf93-138">Хотя в определенном занятии может присутствовать несколько задач, дающих схожий результат, решаться они будут несколько разными способами.</span><span class="sxs-lookup"><span data-stu-id="abf93-138">While in a particular lesson there may be several tasks that accomplish a similar outcome, but how you complete each task is slightly different.</span></span> <span data-ttu-id="abf93-139">В этом показан метод часто больше, чем один из способов toocomplete задачи и toochallenge, можно использовать навыки вы узнали в предыдущих уроках и задачах.</span><span class="sxs-lookup"><span data-stu-id="abf93-139">This method shows there is often more than one way toocomplete a task, and toochallenge you by using skills you've learned in previous lessons and tasks.</span></span>  
  
<span data-ttu-id="abf93-140">Hello занятий hello предназначен tooguide через создание простой табличной модели с использованием разных функций hello включены в SSDT.</span><span class="sxs-lookup"><span data-stu-id="abf93-140">hello purpose of hello lessons is tooguide you through authoring a basic tabular model by using many of hello features included in SSDT.</span></span> <span data-ttu-id="abf93-141">Поскольку каждое занятие строится на предыдущем занятии hello, следует выполнить hello по порядку.</span><span class="sxs-lookup"><span data-stu-id="abf93-141">Because each lesson builds upon hello previous lesson, you should complete hello lessons in order.</span></span>
  
<span data-ttu-id="abf93-142">Этот учебник не предоставляет уроки по управлению сервером на портале Azure, управление сервера или базы данных с помощью SSMS или с помощью клиента приложения toobrowse модели данных.</span><span class="sxs-lookup"><span data-stu-id="abf93-142">This tutorial does not provide lessons about managing a server in Azure portal, managing a server or database by using SSMS, or using a client application toobrowse model data.</span></span> 


## <a name="lessons"></a><span data-ttu-id="abf93-143">Занятия</span><span class="sxs-lookup"><span data-stu-id="abf93-143">Lessons</span></span>  
<span data-ttu-id="abf93-144">Этот учебник содержит следующие занятия hello:</span><span class="sxs-lookup"><span data-stu-id="abf93-144">This tutorial includes hello following lessons:</span></span>  
  
|<span data-ttu-id="abf93-145">Занятие</span><span class="sxs-lookup"><span data-stu-id="abf93-145">Lesson</span></span>|<span data-ttu-id="abf93-146">Предполагаемое время toocomplete</span><span class="sxs-lookup"><span data-stu-id="abf93-146">Estimated time toocomplete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="abf93-147">1. Создание проекта табличной модели</span><span class="sxs-lookup"><span data-stu-id="abf93-147">1 - Create a new tabular model project</span></span>](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|<span data-ttu-id="abf93-148">10 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-148">10 minutes</span></span>|  
|[<span data-ttu-id="abf93-149">2. Получение данных</span><span class="sxs-lookup"><span data-stu-id="abf93-149">2 - Get data</span></span>](../tutorials/aas-lesson-2-get-data.md)|<span data-ttu-id="abf93-150">10 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-150">10 minutes</span></span>|  
|[<span data-ttu-id="abf93-151">3. Обозначение таблицы дат</span><span class="sxs-lookup"><span data-stu-id="abf93-151">3 - Mark as Date Table</span></span>](../tutorials/aas-lesson-3-mark-as-date-table.md)|<span data-ttu-id="abf93-152">3 минуты</span><span class="sxs-lookup"><span data-stu-id="abf93-152">3 minutes</span></span>|  
|[<span data-ttu-id="abf93-153">4. Создание связей</span><span class="sxs-lookup"><span data-stu-id="abf93-153">4 - Create relationships</span></span>](../tutorials/aas-lesson-4-create-relationships.md)|<span data-ttu-id="abf93-154">10 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-154">10 minutes</span></span>|  
|[<span data-ttu-id="abf93-155">5. Создание вычисляемых столбцов</span><span class="sxs-lookup"><span data-stu-id="abf93-155">5 - Create calculated columns</span></span>](../tutorials/aas-lesson-5-create-calculated-columns.md)|<span data-ttu-id="abf93-156">15 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-156">15 minutes</span></span>|
|[<span data-ttu-id="abf93-157">6. Создание мер</span><span class="sxs-lookup"><span data-stu-id="abf93-157">6 - Create measures</span></span>](../tutorials/aas-lesson-6-create-measures.md)|<span data-ttu-id="abf93-158">30 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-158">30 minutes</span></span>|  
|[<span data-ttu-id="abf93-159">7. Создание ключевых показателей эффективности (KPI)</span><span class="sxs-lookup"><span data-stu-id="abf93-159">7 - Create Key Performance Indicators (KPI)</span></span>](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|<span data-ttu-id="abf93-160">15 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-160">15 minutes</span></span>|  
|[<span data-ttu-id="abf93-161">8. Создание перспектив</span><span class="sxs-lookup"><span data-stu-id="abf93-161">8 - Create perspectives</span></span>](../tutorials/aas-lesson-8-create-perspectives.md)|<span data-ttu-id="abf93-162">5 мин</span><span class="sxs-lookup"><span data-stu-id="abf93-162">5 minutes</span></span>|  
|[<span data-ttu-id="abf93-163">9. Создание иерархий</span><span class="sxs-lookup"><span data-stu-id="abf93-163">9 - Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)|<span data-ttu-id="abf93-164">20 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-164">20 minutes</span></span>|  
|[<span data-ttu-id="abf93-165">10. Создание секций</span><span class="sxs-lookup"><span data-stu-id="abf93-165">10 - Create partitions</span></span>](../tutorials/aas-lesson-10-create-partitions.md)|<span data-ttu-id="abf93-166">15 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-166">15 minutes</span></span>|  
|[<span data-ttu-id="abf93-167">11. Создание ролей</span><span class="sxs-lookup"><span data-stu-id="abf93-167">11 - Create roles</span></span>](../tutorials/aas-lesson-11-create-roles.md)|<span data-ttu-id="abf93-168">15 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-168">15 minutes</span></span>|  
|[<span data-ttu-id="abf93-169">12. Анализ в Excel</span><span class="sxs-lookup"><span data-stu-id="abf93-169">12 - Analyze in Excel</span></span>](../tutorials/aas-lesson-12-analyze-in-excel.md)|<span data-ttu-id="abf93-170">5 мин</span><span class="sxs-lookup"><span data-stu-id="abf93-170">5 minutes</span></span>| 
|[<span data-ttu-id="abf93-171">13. Развертывание</span><span class="sxs-lookup"><span data-stu-id="abf93-171">13 - Deploy</span></span>](../tutorials/aas-lesson-13-deploy.md)|<span data-ttu-id="abf93-172">5 мин</span><span class="sxs-lookup"><span data-stu-id="abf93-172">5 minutes</span></span>|  
  
## <a name="supplemental-lessons"></a><span data-ttu-id="abf93-173">Дополнительные занятия</span><span class="sxs-lookup"><span data-stu-id="abf93-173">Supplemental lessons</span></span>  
<span data-ttu-id="abf93-174">Эти занятия не требуется toocomplete hello учебника, но могут быть полезны для улучшения понимания расширенной табличной моделью функции.</span><span class="sxs-lookup"><span data-stu-id="abf93-174">These lessons are not required toocomplete hello tutorial, but can be helpful in better understanding advanced tabular model authoring features.</span></span>  
  
|<span data-ttu-id="abf93-175">Занятие</span><span class="sxs-lookup"><span data-stu-id="abf93-175">Lesson</span></span>|<span data-ttu-id="abf93-176">Предполагаемое время toocomplete</span><span class="sxs-lookup"><span data-stu-id="abf93-176">Estimated time toocomplete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="abf93-177">Строки детализации</span><span class="sxs-lookup"><span data-stu-id="abf93-177">Detail Rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)|<span data-ttu-id="abf93-178">10 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-178">10 minutes</span></span>|
|[<span data-ttu-id="abf93-179">Динамическая безопасность</span><span class="sxs-lookup"><span data-stu-id="abf93-179">Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)|<span data-ttu-id="abf93-180">30 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-180">30 minutes</span></span>|
|[<span data-ttu-id="abf93-181">Неоднородные иерархии</span><span class="sxs-lookup"><span data-stu-id="abf93-181">Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|<span data-ttu-id="abf93-182">20 минут</span><span class="sxs-lookup"><span data-stu-id="abf93-182">20 minutes</span></span>| 

  
## <a name="next-steps"></a><span data-ttu-id="abf93-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="abf93-183">Next steps</span></span>  
<span data-ttu-id="abf93-184">tooget работы см. в разделе [занятия 1: Создание нового проекта табличной модели](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="abf93-184">tooget started, see [Lesson 1: Create a New Tabular Model Project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
  
  

