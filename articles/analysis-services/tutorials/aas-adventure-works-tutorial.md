---
title: "Учебник по Adventure Works для служб Azure Analysis Services | Документы Майкрософт"
description: "Здесь представлен учебник по Adventure Works для служб Analysis Services Azure"
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
ms.openlocfilehash: 257e0bc442f29bfe6683fb0511deac50d92c1720
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a><span data-ttu-id="9563a-103">Azure Analysis Services — учебник по Adventure Works</span><span class="sxs-lookup"><span data-stu-id="9563a-103">Azure Analysis Services - Adventure Works tutorial</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="9563a-104">Этот учебник состоит из занятий по созданию и развертыванию табличной модели на уровне совместимости 1400 с помощью [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span><span class="sxs-lookup"><span data-stu-id="9563a-104">This tutorial provides lessons on how to create and deploy a tabular model at the 1400 compatibility level by using [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  

<span data-ttu-id="9563a-105">Если ранее вы не работали со службами Analysis Services и табличным моделированием, с помощью этого руководства вы быстро научитесь создавать и развертывать простые табличные модели.</span><span class="sxs-lookup"><span data-stu-id="9563a-105">If you're new to Analysis Services and tabular modeling, completing this tutorial is the quickest way to learn how to create and deploy a basic tabular model.</span></span> <span data-ttu-id="9563a-106">После установки всех необходимых компонентов прохождение руководства займет около 2–3 часов.</span><span class="sxs-lookup"><span data-stu-id="9563a-106">Once you have the prerequisites in-place, it should take between two to three hours to complete.</span></span>  
  
## <a name="what-you-learn"></a><span data-ttu-id="9563a-107">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="9563a-107">What you learn</span></span>   
  
-   <span data-ttu-id="9563a-108">Создание проекта табличной модели на **уровне совместимости 1400** в SSDT.</span><span class="sxs-lookup"><span data-stu-id="9563a-108">How to create a new tabular model project at the **1400 compatibility level** in SSDT.</span></span>
  
-   <span data-ttu-id="9563a-109">Импорт данных из реляционной базы данных в проекте табличной модели.</span><span class="sxs-lookup"><span data-stu-id="9563a-109">How to import data from a relational database into a tabular model project.</span></span>  
  
-   <span data-ttu-id="9563a-110">Способы создания связей между таблицами в модели и управления ими.</span><span class="sxs-lookup"><span data-stu-id="9563a-110">How to create and manage relationships between tables in the model.</span></span>  
  
-   <span data-ttu-id="9563a-111">Создание вычисляемых столбцов, мер и ключевых показателей эффективности, помогающих пользователям анализировать критические бизнес-метрики.</span><span class="sxs-lookup"><span data-stu-id="9563a-111">How to create calculated columns, measures, and Key Performance Indicators that help users analyze critical business metrics.</span></span>  
  
-   <span data-ttu-id="9563a-112">Создание перспектив и иерархий, которые помогают пользователям просматривать данные в модели, предоставляя точки наблюдения для конкретного бизнеса и приложения, а также управление ими.</span><span class="sxs-lookup"><span data-stu-id="9563a-112">How to create and manage perspectives and hierarchies that help users more easily browse model data by providing business and application-specific viewpoints.</span></span>  
  
-   <span data-ttu-id="9563a-113">Создание секций, разбивающих данные таблицы на более мелкие логические части, которые можно обрабатывать независимо от других секций.</span><span class="sxs-lookup"><span data-stu-id="9563a-113">How to create partitions that divide table data into smaller logical parts that can be processed independent from other partitions.</span></span>  
  
-   <span data-ttu-id="9563a-114">Защита объектов и данных посредством создания ролей с членами в виде пользователей.</span><span class="sxs-lookup"><span data-stu-id="9563a-114">How to secure model objects and data by creating roles with user members.</span></span>  
  
-   <span data-ttu-id="9563a-115">Развертывание табличной модели на сервере **служб Azure Analysis Services** или на локальном сервере SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="9563a-115">How to deploy a tabular model to an **Azure Analysis Services** server or an on-premises SQL Server 2017 Analysis Services server.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="9563a-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9563a-116">Prerequisites</span></span>  
<span data-ttu-id="9563a-117">Для работы с этим руководством необходимы указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="9563a-117">To complete this tutorial, you need:</span></span>  
  
-   <span data-ttu-id="9563a-118">Экземпляр служб Azure Analysis Services или SQL Server 2017 Analysis Services для развертывания модели.</span><span class="sxs-lookup"><span data-stu-id="9563a-118">An Azure Analysis Services or SQL Server 2017 Analysis Services instance to deploy your model to.</span></span> <span data-ttu-id="9563a-119">Подпишитесь для получения бесплатной [пробной версии служб Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) и [создайте сервер](../analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="9563a-119">Sign up for a free [Azure Analysis Services trial](https://azure.microsoft.com/services/analysis-services/) and [create a server](../analysis-services-create-server.md).</span></span> <span data-ttu-id="9563a-120">Либо зарегистрируйтесь и скачайте [ознакомительную версию для сообщества SQL Server 2017](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span><span class="sxs-lookup"><span data-stu-id="9563a-120">Or, sign up and download [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span></span> 

-   <span data-ttu-id="9563a-121">Хранилище данных SQL Server или хранилище данных SQL Azure с [примером базы данных AdventureWorksDW2014](http://go.microsoft.com/fwlink/?LinkID=335807).</span><span class="sxs-lookup"><span data-stu-id="9563a-121">A SQL Server Data Warehouse or Azure SQL Data Warehouse with the [AdventureWorksDW2014 sample database](http://go.microsoft.com/fwlink/?LinkID=335807).</span></span> <span data-ttu-id="9563a-122">Этот пример базы данных содержит данные, необходимые для работы с настоящим учебником.</span><span class="sxs-lookup"><span data-stu-id="9563a-122">This sample database includes the data necessary to complete this tutorial.</span></span> <span data-ttu-id="9563a-123">Скачайте [бесплатные выпуски SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).</span><span class="sxs-lookup"><span data-stu-id="9563a-123">Download [SQL Server free editions](https://www.microsoft.com/sql-server/sql-server-downloads).</span></span> <span data-ttu-id="9563a-124">Либо зарегистрируйтесь для получения бесплатной [пробной версии базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="9563a-124">Or, sign up for a free [Azure SQL Database trial](https://azure.microsoft.com/services/sql-database/).</span></span> 

    <span data-ttu-id="9563a-125">**Важно!** При установке примера базы данных на SQL Server и развертывании модели на сервере служб Azure Analysis Services [локальный шлюз данных](../analysis-services-gateway.md) является обязательным.</span><span class="sxs-lookup"><span data-stu-id="9563a-125">**Important:** If you install the sample database on an on-premises SQL Server, and you deploy your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>

-   <span data-ttu-id="9563a-126">Последняя версия [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span><span class="sxs-lookup"><span data-stu-id="9563a-126">The latest version of [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>

-   <span data-ttu-id="9563a-127">Последняя версия [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="9563a-127">The latest version of [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>    

-   <span data-ttu-id="9563a-128">Клиентское приложение, например [Power BI Desktop](https://powerbi.microsoft.com/desktop/) или Excel.</span><span class="sxs-lookup"><span data-stu-id="9563a-128">A client application such as [Power BI Desktop](https://powerbi.microsoft.com/desktop/) or Excel.</span></span> 

## <a name="scenario"></a><span data-ttu-id="9563a-129">Сценарий</span><span class="sxs-lookup"><span data-stu-id="9563a-129">Scenario</span></span>  
<span data-ttu-id="9563a-130">В этом учебнике используется вымышленная компания Adventure Works Cycles.</span><span class="sxs-lookup"><span data-stu-id="9563a-130">This tutorial is based on Adventure Works Cycles, a fictitious company.</span></span> <span data-ttu-id="9563a-131">Adventure Works — это большая международная производственная компания, выпускающая и реализующая велосипеды, запчасти и аксессуары для рынков Северной Америки, Европы и Азии.</span><span class="sxs-lookup"><span data-stu-id="9563a-131">Adventure Works is a large, multinational manufacturing company that produces and distributes bicycles, parts, and accessories to commercial markets in North America, Europe, and Asia.</span></span> <span data-ttu-id="9563a-132">Штат компании насчитывает 500 сотрудников.</span><span class="sxs-lookup"><span data-stu-id="9563a-132">The company employs 500 workers.</span></span> <span data-ttu-id="9563a-133">Кроме того, на Adventure Works работает несколько региональных групп, относящихся к разным ее рынкам сбыта.</span><span class="sxs-lookup"><span data-stu-id="9563a-133">Additionally, Adventure Works employs several regional sales teams throughout its market base.</span></span> <span data-ttu-id="9563a-134">В рамках проекта вы создадите табличную модель для пользователей, специализирующихся на продажах и маркетинге, чтобы проанализировать в базе данных AdventureWorksDW данные об интернет-продажах.</span><span class="sxs-lookup"><span data-stu-id="9563a-134">Your project is to create a tabular model for sales and marketing users to analyze Internet sales data in the AdventureWorksDW database.</span></span>  
  
<span data-ttu-id="9563a-135">Это руководство содержит несколько занятий,</span><span class="sxs-lookup"><span data-stu-id="9563a-135">To complete the tutorial, you must complete various lessons.</span></span> <span data-ttu-id="9563a-136">каждое из которых содержит определенную задачу.</span><span class="sxs-lookup"><span data-stu-id="9563a-136">In each lesson, there are tasks.</span></span> <span data-ttu-id="9563a-137">Чтобы завершить занятие, вам нужно решить соответствующую задачу.</span><span class="sxs-lookup"><span data-stu-id="9563a-137">Completing each task in order is necessary for completing the lesson.</span></span> <span data-ttu-id="9563a-138">Хотя в определенном занятии может присутствовать несколько задач, дающих схожий результат, решаться они будут несколько разными способами.</span><span class="sxs-lookup"><span data-stu-id="9563a-138">While in a particular lesson there may be several tasks that accomplish a similar outcome, but how you complete each task is slightly different.</span></span> <span data-ttu-id="9563a-139">Такой подход не только помогает понять, что в большинстве случаев есть несколько способов решения определенной задачи, но и стимулирует вас применять полученные ранее знания.</span><span class="sxs-lookup"><span data-stu-id="9563a-139">This method shows there is often more than one way to complete a task, and to challenge you by using skills you've learned in previous lessons and tasks.</span></span>  
  
<span data-ttu-id="9563a-140">Эти занятия помогут вам создать простую табличную модель с использованием разных функций, доступных в SSDT.</span><span class="sxs-lookup"><span data-stu-id="9563a-140">The purpose of the lessons is to guide you through authoring a basic tabular model by using many of the features included in SSDT.</span></span> <span data-ttu-id="9563a-141">Поскольку каждое из занятий основывается на предыдущем, их следует выполнять по порядку.</span><span class="sxs-lookup"><span data-stu-id="9563a-141">Because each lesson builds upon the previous lesson, you should complete the lessons in order.</span></span>
  
<span data-ttu-id="9563a-142">Это руководство не обучает управлению сервером на портале Azure, а также управлению сервером или базой данных с помощью SSMS или клиентского приложения для просмотра данных модели.</span><span class="sxs-lookup"><span data-stu-id="9563a-142">This tutorial does not provide lessons about managing a server in Azure portal, managing a server or database by using SSMS, or using a client application to browse model data.</span></span> 


## <a name="lessons"></a><span data-ttu-id="9563a-143">Занятия</span><span class="sxs-lookup"><span data-stu-id="9563a-143">Lessons</span></span>  
<span data-ttu-id="9563a-144">Учебник включает в себя следующие занятия:</span><span class="sxs-lookup"><span data-stu-id="9563a-144">This tutorial includes the following lessons:</span></span>  
  
|<span data-ttu-id="9563a-145">Занятие</span><span class="sxs-lookup"><span data-stu-id="9563a-145">Lesson</span></span>|<span data-ttu-id="9563a-146">Предполагаемое время выполнения</span><span class="sxs-lookup"><span data-stu-id="9563a-146">Estimated time to complete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="9563a-147">1. Создание проекта табличной модели</span><span class="sxs-lookup"><span data-stu-id="9563a-147">1 - Create a new tabular model project</span></span>](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|<span data-ttu-id="9563a-148">10 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-148">10 minutes</span></span>|  
|[<span data-ttu-id="9563a-149">2. Получение данных</span><span class="sxs-lookup"><span data-stu-id="9563a-149">2 - Get data</span></span>](../tutorials/aas-lesson-2-get-data.md)|<span data-ttu-id="9563a-150">10 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-150">10 minutes</span></span>|  
|[<span data-ttu-id="9563a-151">3. Обозначение таблицы дат</span><span class="sxs-lookup"><span data-stu-id="9563a-151">3 - Mark as Date Table</span></span>](../tutorials/aas-lesson-3-mark-as-date-table.md)|<span data-ttu-id="9563a-152">3 минуты</span><span class="sxs-lookup"><span data-stu-id="9563a-152">3 minutes</span></span>|  
|[<span data-ttu-id="9563a-153">4. Создание связей</span><span class="sxs-lookup"><span data-stu-id="9563a-153">4 - Create relationships</span></span>](../tutorials/aas-lesson-4-create-relationships.md)|<span data-ttu-id="9563a-154">10 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-154">10 minutes</span></span>|  
|[<span data-ttu-id="9563a-155">5. Создание вычисляемых столбцов</span><span class="sxs-lookup"><span data-stu-id="9563a-155">5 - Create calculated columns</span></span>](../tutorials/aas-lesson-5-create-calculated-columns.md)|<span data-ttu-id="9563a-156">15 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-156">15 minutes</span></span>|
|[<span data-ttu-id="9563a-157">6. Создание мер</span><span class="sxs-lookup"><span data-stu-id="9563a-157">6 - Create measures</span></span>](../tutorials/aas-lesson-6-create-measures.md)|<span data-ttu-id="9563a-158">30 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-158">30 minutes</span></span>|  
|[<span data-ttu-id="9563a-159">7. Создание ключевых показателей эффективности (KPI)</span><span class="sxs-lookup"><span data-stu-id="9563a-159">7 - Create Key Performance Indicators (KPI)</span></span>](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|<span data-ttu-id="9563a-160">15 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-160">15 minutes</span></span>|  
|[<span data-ttu-id="9563a-161">8. Создание перспектив</span><span class="sxs-lookup"><span data-stu-id="9563a-161">8 - Create perspectives</span></span>](../tutorials/aas-lesson-8-create-perspectives.md)|<span data-ttu-id="9563a-162">5 мин</span><span class="sxs-lookup"><span data-stu-id="9563a-162">5 minutes</span></span>|  
|[<span data-ttu-id="9563a-163">9. Создание иерархий</span><span class="sxs-lookup"><span data-stu-id="9563a-163">9 - Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)|<span data-ttu-id="9563a-164">20 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-164">20 minutes</span></span>|  
|[<span data-ttu-id="9563a-165">10. Создание секций</span><span class="sxs-lookup"><span data-stu-id="9563a-165">10 - Create partitions</span></span>](../tutorials/aas-lesson-10-create-partitions.md)|<span data-ttu-id="9563a-166">15 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-166">15 minutes</span></span>|  
|[<span data-ttu-id="9563a-167">11. Создание ролей</span><span class="sxs-lookup"><span data-stu-id="9563a-167">11 - Create roles</span></span>](../tutorials/aas-lesson-11-create-roles.md)|<span data-ttu-id="9563a-168">15 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-168">15 minutes</span></span>|  
|[<span data-ttu-id="9563a-169">12. Анализ в Excel</span><span class="sxs-lookup"><span data-stu-id="9563a-169">12 - Analyze in Excel</span></span>](../tutorials/aas-lesson-12-analyze-in-excel.md)|<span data-ttu-id="9563a-170">5 мин</span><span class="sxs-lookup"><span data-stu-id="9563a-170">5 minutes</span></span>| 
|[<span data-ttu-id="9563a-171">13. Развертывание</span><span class="sxs-lookup"><span data-stu-id="9563a-171">13 - Deploy</span></span>](../tutorials/aas-lesson-13-deploy.md)|<span data-ttu-id="9563a-172">5 мин</span><span class="sxs-lookup"><span data-stu-id="9563a-172">5 minutes</span></span>|  
  
## <a name="supplemental-lessons"></a><span data-ttu-id="9563a-173">Дополнительные занятия</span><span class="sxs-lookup"><span data-stu-id="9563a-173">Supplemental lessons</span></span>  
<span data-ttu-id="9563a-174">Эти занятия не требуются для работы с учебником, но могут оказаться полезными при получении более общих сведений о функциях расширенной табличной модели.</span><span class="sxs-lookup"><span data-stu-id="9563a-174">These lessons are not required to complete the tutorial, but can be helpful in better understanding advanced tabular model authoring features.</span></span>  
  
|<span data-ttu-id="9563a-175">Занятие</span><span class="sxs-lookup"><span data-stu-id="9563a-175">Lesson</span></span>|<span data-ttu-id="9563a-176">Предполагаемое время выполнения</span><span class="sxs-lookup"><span data-stu-id="9563a-176">Estimated time to complete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="9563a-177">Строки детализации</span><span class="sxs-lookup"><span data-stu-id="9563a-177">Detail Rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)|<span data-ttu-id="9563a-178">10 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-178">10 minutes</span></span>|
|[<span data-ttu-id="9563a-179">Динамическая безопасность</span><span class="sxs-lookup"><span data-stu-id="9563a-179">Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)|<span data-ttu-id="9563a-180">30 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-180">30 minutes</span></span>|
|[<span data-ttu-id="9563a-181">Неоднородные иерархии</span><span class="sxs-lookup"><span data-stu-id="9563a-181">Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|<span data-ttu-id="9563a-182">20 минут</span><span class="sxs-lookup"><span data-stu-id="9563a-182">20 minutes</span></span>| 

  
## <a name="next-steps"></a><span data-ttu-id="9563a-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9563a-183">Next steps</span></span>  
<span data-ttu-id="9563a-184">Для начала работы см. [Занятие 1. Создание нового проекта табличной модели](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="9563a-184">To get started, see [Lesson 1: Create a New Tabular Model Project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
  
  

