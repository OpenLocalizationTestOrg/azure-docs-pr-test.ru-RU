---
title: "Учебник по службам Azure Analysis Services: занятие 12 \"Анализ в Excel\" | Документы Майкрософт"
description: "Описывает анализ данных в Excel в учебном проекте служб Azure Analysis Services."
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
ms.openlocfilehash: 6f47de43ff8d94de22f8b7c12fa0707a8d7ffbbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-12-analyze-in-excel"></a><span data-ttu-id="44d55-103">Занятие 12. Анализ в Excel</span><span class="sxs-lookup"><span data-stu-id="44d55-103">Lesson 12: Analyze in Excel</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="44d55-104">В этом занятии вы воспользуетесь функцией "Анализ в Excel", чтобы открыть Microsoft Excel, автоматически создать подключение к рабочей области модели и автоматически добавить сводную таблицу на лист.</span><span class="sxs-lookup"><span data-stu-id="44d55-104">In this lesson, you use the Analyze in Excel feature to open Microsoft Excel, automatically create a connection to the model workspace, and automatically add a PivotTable to the worksheet.</span></span> <span data-ttu-id="44d55-105">Функция "Анализ в Excel" предназначена для быстрого и удобного тестирования эффективности модели до ее развертывания.</span><span class="sxs-lookup"><span data-stu-id="44d55-105">The Analyze in Excel feature is meant to provide a quick and easy way to test the efficacy of your model design prior to deploying your model.</span></span> <span data-ttu-id="44d55-106">В этом занятии выполнять анализ данных не нужно.</span><span class="sxs-lookup"><span data-stu-id="44d55-106">You do not perform any data analysis in this lesson.</span></span> <span data-ttu-id="44d55-107">Оно призвано познакомить вас как автора модели со средствами для проверки модели.</span><span class="sxs-lookup"><span data-stu-id="44d55-107">The purpose of this lesson is to familiarize you, the model author, with the tools you can use to test your model design.</span></span>   
  
<span data-ttu-id="44d55-108">Для этого занятия нужно установить Excel на том же компьютере, где находится SSDT.</span><span class="sxs-lookup"><span data-stu-id="44d55-108">To complete this lesson, Excel must be installed on the same computer as SSDT.</span></span>
  
<span data-ttu-id="44d55-109">Предполагаемое время выполнения этого занятия: **5 минут**</span><span class="sxs-lookup"><span data-stu-id="44d55-109">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="44d55-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44d55-110">Prerequisites</span></span>  
<span data-ttu-id="44d55-111">Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке.</span><span class="sxs-lookup"><span data-stu-id="44d55-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="44d55-112">Прежде чем выполнять задачи в этом разделе, нужно завершить предыдущее занятие: [Занятие 11. Создание ролей](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="44d55-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).</span></span>  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a><span data-ttu-id="44d55-113">Просмотр с помощью перспективы по умолчанию и перспективы Internet Sales</span><span class="sxs-lookup"><span data-stu-id="44d55-113">Browse using the Default and Internet Sales perspectives</span></span>  
<span data-ttu-id="44d55-114">В этих первых задачах вам нужно просмотреть модель как с помощью перспективы по умолчанию, включающей в себя все объекты модели, так и с помощью созданной ранее перспективы Internet Sales.</span><span class="sxs-lookup"><span data-stu-id="44d55-114">In these first tasks, you browse your model by using both the default perspective, which includes all model objects, and also by using the Internet Sales perspective you earlier.</span></span> <span data-ttu-id="44d55-115">Перспектива Internet Sales исключает объект таблицы Customer.</span><span class="sxs-lookup"><span data-stu-id="44d55-115">The Internet Sales perspective excludes the Customer table object.</span></span>  
  
#### <a name="to-browse-by-using-the-default-perspective"></a><span data-ttu-id="44d55-116">Просмотр с использованием перспективы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="44d55-116">To browse by using the Default perspective</span></span>  
  
1.  <span data-ttu-id="44d55-117">Откройте меню **Модель** и выберите **Анализ в Excel**.</span><span class="sxs-lookup"><span data-stu-id="44d55-117">Click the **Model** menu > **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="44d55-118">В диалоговом окне **Анализ в Excel** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="44d55-118">In the **Analyze in Excel** dialog box, click **OK**.</span></span>  
  
    <span data-ttu-id="44d55-119">В Excel открывается новая книга.</span><span class="sxs-lookup"><span data-stu-id="44d55-119">Excel opens with a new workbook.</span></span> <span data-ttu-id="44d55-120">Создается подключение к источнику данных с использованием текущей учетной записи пользователя, и с помощью перспективы по умолчанию определяются доступные для просмотра поля.</span><span class="sxs-lookup"><span data-stu-id="44d55-120">A data source connection is created using the current user account and the Default perspective is used to define viewable fields.</span></span> <span data-ttu-id="44d55-121">На лист автоматически добавляется сводная таблица.</span><span class="sxs-lookup"><span data-stu-id="44d55-121">A PivotTable is automatically added to the worksheet.</span></span>  
  
3.  <span data-ttu-id="44d55-122">В Excel в **списке полей сводной таблицы** отображаются группы мер **DimDate** и **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="44d55-122">In Excel, in the **PivotTable Field List**, notice the **DimDate** and **FactInternetSales** measure groups appear.</span></span> <span data-ttu-id="44d55-123">Также отображаются следующие таблицы со связанными столбцами: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** и **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="44d55-123">The **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.</span></span>  
  
4.  <span data-ttu-id="44d55-124">Закройте Excel без сохранения книги.</span><span class="sxs-lookup"><span data-stu-id="44d55-124">Close Excel without saving the workbook.</span></span>  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a><span data-ttu-id="44d55-125">Просмотр с использованием перспективы Internet Sales</span><span class="sxs-lookup"><span data-stu-id="44d55-125">To browse by using the Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="44d55-126">Откройте меню **Модель** и выберите **Анализ в Excel**.</span><span class="sxs-lookup"><span data-stu-id="44d55-126">Click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="44d55-127">В диалоговом окне **Анализ в Excel** оставьте параметр **Текущий пользователь Windows** выбранным, а затем в раскрывающемся списке **Перспектива** выберите **Internet Sales** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="44d55-127">In the **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in the **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**.</span></span> 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  <span data-ttu-id="44d55-129">В области **Поля сводной таблицы** Excel обратите внимание на то, что таблица DimCustomer исключена из списка полей.</span><span class="sxs-lookup"><span data-stu-id="44d55-129">In Excel, in **PivotTable Fields**, notice the DimCustomer table is excluded from the field list.</span></span>  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  <span data-ttu-id="44d55-131">Закройте Excel без сохранения книги.</span><span class="sxs-lookup"><span data-stu-id="44d55-131">Close Excel without saving the workbook.</span></span>  
  
## <a name="browse-by-using-roles"></a><span data-ttu-id="44d55-132">Просмотр с помощью ролей</span><span class="sxs-lookup"><span data-stu-id="44d55-132">Browse by using roles</span></span>  
<span data-ttu-id="44d55-133">Роли — это неотъемлемая часть любой табличной модели.</span><span class="sxs-lookup"><span data-stu-id="44d55-133">Roles are an important part of any tabular model.</span></span> <span data-ttu-id="44d55-134">Если пользователям не назначить хотя бы одну роль, они не смогут использовать и анализировать данные с помощью вашей модели.</span><span class="sxs-lookup"><span data-stu-id="44d55-134">Without at least one role to which users are added as members, users cannot access and analyze data using your model.</span></span> <span data-ttu-id="44d55-135">Функция "Анализ в Excel" позволяет тестировать заданные роли.</span><span class="sxs-lookup"><span data-stu-id="44d55-135">The Analyze in Excel feature provides a way for you to test the roles you have defined.</span></span>  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a><span data-ttu-id="44d55-136">Просмотр с помощью роли пользователя Sales Manager</span><span class="sxs-lookup"><span data-stu-id="44d55-136">To browse by using the Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="44d55-137">В SSDT откройте меню **Модель** и выберите **Анализ в Excel**.</span><span class="sxs-lookup"><span data-stu-id="44d55-137">In SSDT, click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="44d55-138">В поле **Укажите имя пользователя или роль для подключения к модели** щелкните **Роль** и выберите **Менеджер по продажам** в раскрывающемся списке. Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="44d55-138">In **Specify the user name or role to use to connect to the model**, select **Role**, and then in the drop-down listbox, select **Sales Manager**, and then click **OK**.</span></span>  
  
    <span data-ttu-id="44d55-139">В Excel открывается новая книга.</span><span class="sxs-lookup"><span data-stu-id="44d55-139">Excel opens with a new workbook.</span></span> <span data-ttu-id="44d55-140">Автоматически создается сводная таблица.</span><span class="sxs-lookup"><span data-stu-id="44d55-140">A PivotTable is automatically created.</span></span> <span data-ttu-id="44d55-141">Список полей сводной таблицы включает все поля данных, доступные в новой модели.</span><span class="sxs-lookup"><span data-stu-id="44d55-141">The Pivot Table Field List includes all the data fields available in your new model.</span></span>  
      
3.  <span data-ttu-id="44d55-142">Закройте Excel без сохранения книги.</span><span class="sxs-lookup"><span data-stu-id="44d55-142">Close Excel without saving the workbook.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="44d55-143">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="44d55-143">What's next?</span></span>
<span data-ttu-id="44d55-144">Перейдите к следующему разделу: [Занятие 13. Развертывание](../tutorials/aas-lesson-13-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="44d55-144">Go to the next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).</span></span>

  
  
  
