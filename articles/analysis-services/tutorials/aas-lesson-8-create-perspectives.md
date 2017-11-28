---
title: "aaa \"Создание перспектив Azure Analysis Services занятие учебника 8 | Документы Microsoft»"
description: "Описывает, как toocreate перспективы в hello проекта tutorial служб Azure Analysis Services."
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
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="ebe6b-103">Занятие 8. Создание перспектив</span><span class="sxs-lookup"><span data-stu-id="ebe6b-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ebe6b-104">В этом занятии вы создадите перспективу Internet Sales.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="ebe6b-105">Перспектива определяет просматриваемое подмножество модели, предоставляющее точки наблюдения, сосредоточенные на определенном объекте, аспекте бизнеса или приложении.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="ebe6b-106">Когда пользователь подключается tooa модели с помощью перспективы, они видят только те объекты модели (таблицы, столбцы, меры, иерархии и ключевые показатели эффективности) как поля, определенные в перспективе.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="ebe6b-107">toolearn более, в разделе [перспективы](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="ebe6b-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="ebe6b-108">Hello перспективы Internet Sales, создаваемая на этом занятии исключает объект таблицы DimCustomer hello.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="ebe6b-109">При создании перспективы, которая исключает из представления определенные объекты, объекты продолжают существовать в модели hello.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="ebe6b-110">но не отображаются в списке полей для клиента отчетов.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="ebe6b-111">Вычисляемые столбцы и меры, как включенные, так и не включенные в перспективу, по-прежнему могут проводить расчеты на основе исключенных данных.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="ebe6b-112">Hello цель этого занятия — toodescribe как toocreate перспектив и ознакомиться со средствами разработки табличных моделей hello.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="ebe6b-113">Если потом развернуть дополнительные таблицы tooinclude этой модели, можно создать дополнительные перспективы toodefine разных точек обзора модели hello, например, инвентаризации и продажи.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="ebe6b-114">Предполагаемое время toocomplete на этом занятии: **пять минут**</span><span class="sxs-lookup"><span data-stu-id="ebe6b-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ebe6b-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ebe6b-115">Prerequisites</span></span>  
<span data-ttu-id="ebe6b-116">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ebe6b-117">Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятии 7: Создание ключевых показателей эффективности](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="ebe6b-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="ebe6b-118">Создание перспектив</span><span class="sxs-lookup"><span data-stu-id="ebe6b-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="ebe6b-119">toocreate перспективы Internet Sales</span><span class="sxs-lookup"><span data-stu-id="ebe6b-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="ebe6b-120">Нажмите кнопку hello **модель** меню > **перспективы** > **Создание и управление**.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="ebe6b-121">В hello **перспективы** диалоговое окно, нажмите кнопку **новую перспективу**.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="ebe6b-122">Дважды щелкните hello **новую перспективу** заголовок столбца и переименовать **продажи через Интернет**.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="ebe6b-123">Здравствуйте, выберите все таблицы hello *за исключением* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="ebe6b-125">В одном из следующих занятий вы использовать hello анализ в Excel функции tootest этой перспективы.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="ebe6b-126">Hello список полей сводной таблицы Excel включает в себя все таблицы, кроме таблица DimCustomer hello.</span><span class="sxs-lookup"><span data-stu-id="ebe6b-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="ebe6b-127">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="ebe6b-127">What's next?</span></span>
<span data-ttu-id="ebe6b-128">[Занятие 9. Создание иерархий](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="ebe6b-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
