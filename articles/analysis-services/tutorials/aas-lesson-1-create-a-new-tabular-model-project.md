---
title: "Учебник по службам Azure Analysis Services: занятие 1 \"Создание проекта табличной модели\" | Документы Майкрософт"
description: "Описывает создание проекта для учебника по службам Azure Analysis Services."
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
ms.openlocfilehash: ebd160372fc75c6d0fc323be9e948fa2475b71cf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="lesson-1-create-a-tabular-model-project"></a><span data-ttu-id="b022b-103">Занятие 1. Создание проекта табличной модели</span><span class="sxs-lookup"><span data-stu-id="b022b-103">Lesson 1: Create a tabular model project</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b022b-104">На этом занятии вы создадите проект табличной модели на уровне совместимости 1400, используя SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="b022b-104">In this lesson, you use SQL Server Data Tools (SSDT) to create a new tabular model project at the 1400 compatibility level.</span></span> <span data-ttu-id="b022b-105">После этого можно приступать к добавлению данных и созданию модели.</span><span class="sxs-lookup"><span data-stu-id="b022b-105">Once your new project is created, you can begin adding data and authoring your model.</span></span> <span data-ttu-id="b022b-106">Кроме того, это занятие содержит краткое описание для среды создания табличных моделей в SSDT.</span><span class="sxs-lookup"><span data-stu-id="b022b-106">This lesson also gives you a brief introduction to the tabular model authoring environment in SSDT.</span></span>  
  
<span data-ttu-id="b022b-107">Предполагаемое время выполнения этого занятия: **10 минут**</span><span class="sxs-lookup"><span data-stu-id="b022b-107">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b022b-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b022b-108">Prerequisites</span></span>  
<span data-ttu-id="b022b-109">Это первый раздел в учебнике по созданию табличной модели.</span><span class="sxs-lookup"><span data-stu-id="b022b-109">This topic is the first lesson in a tabular model authoring tutorial.</span></span> <span data-ttu-id="b022b-110">Для прохождения этого занятия требуется выполнить несколько предварительных условий.</span><span class="sxs-lookup"><span data-stu-id="b022b-110">To complete this lesson, there are several prerequisites you need to have in-place.</span></span> <span data-ttu-id="b022b-111">Дополнительные сведения см. в разделе [Azure Analysis Services — учебник по Adventure Works](../tutorials/aas-adventure-works-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="b022b-111">To learn more, see [Azure Analysis Services - Adventure Works tutorial](../tutorials/aas-adventure-works-tutorial.md).</span></span>  
  
## <a name="create-a-new-tabular-model-project"></a><span data-ttu-id="b022b-112">Создание проекта табличной модели</span><span class="sxs-lookup"><span data-stu-id="b022b-112">Create a new tabular model project</span></span>  
  
#### <a name="to-create-a-new-tabular-model-project"></a><span data-ttu-id="b022b-113">Чтобы создать проект табличной модели, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b022b-113">To create a new tabular model project</span></span>  
  
1.  <span data-ttu-id="b022b-114">В меню **Файл** SSDT выберите пункты **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="b022b-114">In SSDT, on the **File** menu, click **New** > **Project**.</span></span>  
  
2.  <span data-ttu-id="b022b-115">В диалоговом окне **Новый проект** разверните пункты **Установленные** > **Business Intelligence** > **Analysis Services** и щелкните элемент **Табличный проект служб Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="b022b-115">In the **New Project** dialog box, expand **Installed** > **Business Intelligence** > **Analysis Services**, and then click **Analysis Services Tabular Project**.</span></span>  
  
3.  <span data-ttu-id="b022b-116">В поле **Имя** введите **AW Internet Sales** (Интернет-продажи Adventure Works) и укажите расположение для файлов проекта.</span><span class="sxs-lookup"><span data-stu-id="b022b-116">In  **Name**, type **AW Internet Sales**, and then specify a location for the project files.</span></span>  
  
    <span data-ttu-id="b022b-117">По умолчанию **имя решения** совпадает с именем проекта, но его можно изменить.</span><span class="sxs-lookup"><span data-stu-id="b022b-117">By default, **Solution Name** is the same as the project name; however, you can type a different solution name.</span></span>  
  
4.  <span data-ttu-id="b022b-118">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b022b-118">Click **OK**.</span></span>  
  
5.  <span data-ttu-id="b022b-119">В диалоговом окне **Конструктор табличных моделей** выберите **Интегрированная рабочая область**.</span><span class="sxs-lookup"><span data-stu-id="b022b-119">In the **Tabular model designer** dialog box, select **Integrated workspace**.</span></span>  
  
    <span data-ttu-id="b022b-120">Эта рабочая область содержит базу данных табличной модели с тем же именем, что и у проекта, при создании модели.</span><span class="sxs-lookup"><span data-stu-id="b022b-120">The workspace hosts a tabular model database with the same name as the project during model authoring.</span></span> <span data-ttu-id="b022b-121">Параметр "Интегрированная рабочая область" означает, что SSDT будет использовать встроенный экземпляр, избавляя пользователя от необходимости устанавливать отдельный экземпляр сервера служб Analysis Services для создания модели.</span><span class="sxs-lookup"><span data-stu-id="b022b-121">Integrated workspace means SSDT uses a built-in instance, eliminating the need to install a separate Analysis Services server instance just for model authoring.</span></span>
      
6.  <span data-ttu-id="b022b-122">В поле **Уровень совместимости** выберите **SQL Server 2017/Azure Analysis Services (1400)**.</span><span class="sxs-lookup"><span data-stu-id="b022b-122">In **Compatibility level**, select **SQL Server 2017 / Azure Analysis Services (1400)**.</span></span>   
 
    ![aas-lesson1-tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    <span data-ttu-id="b022b-124">Если вы не видите элемент "SQL Server 2017/Azure Analysis Services (1400)" в списке уровней совместимости, значит используется не последняя версия SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="b022b-124">If you don’t see SQL Server 2017 / Azure Analysis Services (1400) in the Compatibility level listbox, you’re not using the latest version of SQL Server Data Tools.</span></span> <span data-ttu-id="b022b-125">Сведения о получении последней версии см. в разделе [Установка SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span><span class="sxs-lookup"><span data-stu-id="b022b-125">To get the latest version, see [Install SQL Server Data tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a><span data-ttu-id="b022b-126">Общие сведения о среде для создания табличных моделей в SSDT</span><span class="sxs-lookup"><span data-stu-id="b022b-126">Understanding the SSDT tabular model authoring environment</span></span>  
<span data-ttu-id="b022b-127">Создав проект табличной модели, давайте кратко познакомимся со средой для создания табличных моделей в SSDT.</span><span class="sxs-lookup"><span data-stu-id="b022b-127">Now that you’ve created a new tabular model project, let’s take a moment to explore the tabular model authoring environment in SSDT.</span></span>  
  
<span data-ttu-id="b022b-128">После создания проект открывается в SSDT.</span><span class="sxs-lookup"><span data-stu-id="b022b-128">After your project is created, it opens in SSDT.</span></span> <span data-ttu-id="b022b-129">В области **Обозреватель табличных моделей** справа вы увидите представление объектов модели в виде дерева.</span><span class="sxs-lookup"><span data-stu-id="b022b-129">On the right side, in **Tabular Model Explorer**, you see a tree view of the objects in your model.</span></span> <span data-ttu-id="b022b-130">Так как данные еще не импортированы, эти папки пусты.</span><span class="sxs-lookup"><span data-stu-id="b022b-130">Since you haven't yet imported data, the folders are empty.</span></span> <span data-ttu-id="b022b-131">Вы можете щелкнуть правой кнопкой мыши папку объектов для выполнения действий, что аналогично работе со строкой меню.</span><span class="sxs-lookup"><span data-stu-id="b022b-131">You can right-click an object folder to perform actions, similar to the menu bar.</span></span> <span data-ttu-id="b022b-132">При прохождении этого руководства вы будете использовать обозреватель табличных моделей для перехода по различным объектам в проекте модели.</span><span class="sxs-lookup"><span data-stu-id="b022b-132">As you step through this tutorial, you use the Tabular Model Explorer to navigate different objects in your model project.</span></span>

![aas-lesson1-tme](../tutorials/media/aas-lesson1-tme.png)

<span data-ttu-id="b022b-134">Откройте вкладку **Обозреватель решений**. Здесь находится файл **Model.bim**.</span><span class="sxs-lookup"><span data-stu-id="b022b-134">Click the **Solution Explorer** tab. Here, you see your **Model.bim** file.</span></span> <span data-ttu-id="b022b-135">Если вы не видите окно конструктора (пустое окно с вкладкой Model.bim) слева в разделе **Проект AW Internet Sales** **обозревателя решений**, дважды щелкните файл **Model.bim**.</span><span class="sxs-lookup"><span data-stu-id="b022b-135">If you don’t see the designer window to the left (the empty window with the Model.bim tab), in **Solution Explorer**, under **AW Internet Sales Project**, double-click the **Model.bim** file.</span></span> <span data-ttu-id="b022b-136">Этот файл содержит метаданные для проекта модели.</span><span class="sxs-lookup"><span data-stu-id="b022b-136">The Model.bim file contains the metadata for your model project.</span></span> 

![aas-lesson1-se](../tutorials/media/aas-lesson1-se.png)
  
<span data-ttu-id="b022b-138">Щелкните **Model.bim**.</span><span class="sxs-lookup"><span data-stu-id="b022b-138">Click **Model.bim**.</span></span> <span data-ttu-id="b022b-139">В окне **Свойства** отображаются свойства модели, наиболее важное из которых — **Режим DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="b022b-139">In the **Properties** window, you see the model properties, most important of which is the **DirectQuery Mode** property.</span></span> <span data-ttu-id="b022b-140">Это свойство определяет, развертывается ли модель в режиме In-Memory ("Выкл.") или DirectQuery ("Вкл.").</span><span class="sxs-lookup"><span data-stu-id="b022b-140">This property specifies if the model is deployed in In-Memory mode (Off) or DirectQuery mode (On).</span></span> <span data-ttu-id="b022b-141">В этом руководстве вы создадите и развернете модель в режиме In-Memory.</span><span class="sxs-lookup"><span data-stu-id="b022b-141">For this tutorial, you author and deploy your model in In-Memory mode.</span></span>

![aas-lesson1-properties](../tutorials/media/aas-lesson1-properties.png)
  
<span data-ttu-id="b022b-143">При создании проекта модели некоторые свойства модели задаются автоматически в соответствии с параметрами моделирования данных, которые можно указать в диалоговом окне **Параметры** меню **Сервис**.</span><span class="sxs-lookup"><span data-stu-id="b022b-143">When you create a model project, certain model properties are set automatically according to the Data Modeling settings that can be specified in the **Tools** menu > **Options** dialog box.</span></span> <span data-ttu-id="b022b-144">Свойства "Резервная копия", "Сохранение рабочей области" и "Сервер рабочей области" указывают, как и где база данных рабочей области (база данных для создания модели) архивируется, сохраняется в памяти и формируется.</span><span class="sxs-lookup"><span data-stu-id="b022b-144">Data Backup, Workspace Retention, and Workspace Server properties specify how and where the workspace database (your model authoring database) is backed up, retained in-memory, and built.</span></span> <span data-ttu-id="b022b-145">При необходимости вы можете изменить эти параметры позже, а сейчас оставьте заданные значения.</span><span class="sxs-lookup"><span data-stu-id="b022b-145">You can change these settings later if necessary, but for now, leave these properties as they are.</span></span>  

<span data-ttu-id="b022b-146">В **обозревателе решений** щелкните правой кнопкой мыши **AW Internet Sales** (проект) и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="b022b-146">In **Solution Explorer**, right-click **AW Internet Sales** (project), and then click **Properties**.</span></span> <span data-ttu-id="b022b-147">Открывается диалоговое окно **Страницы свойств AW Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="b022b-147">The **AW Internet Sales Property Pages** dialog box appears.</span></span> <span data-ttu-id="b022b-148">Некоторые из них вы установите позднее при развертывании модели.</span><span class="sxs-lookup"><span data-stu-id="b022b-148">You set some of these properties later when you deploy your model.</span></span>  
  
<span data-ttu-id="b022b-149">При установке SSDT в среду Visual Studio было добавлено несколько новых пунктов меню.</span><span class="sxs-lookup"><span data-stu-id="b022b-149">When you installed SSDT, several new menu items were added to the Visual Studio environment.</span></span> <span data-ttu-id="b022b-150">Откройте меню **Модель**.</span><span class="sxs-lookup"><span data-stu-id="b022b-150">Click the **Model** menu.</span></span> <span data-ttu-id="b022b-151">Здесь можно импортировать данные, обновить данные рабочей области, просмотреть модель в Excel, создать перспективы и роли, выбрать представление модели и задать параметры вычислений.</span><span class="sxs-lookup"><span data-stu-id="b022b-151">From here, you can import data, refresh workspace data, browse your model in Excel, create perspectives and roles, select the model view, and set calculation options.</span></span> <span data-ttu-id="b022b-152">Откройте меню **Таблица**.</span><span class="sxs-lookup"><span data-stu-id="b022b-152">Click the **Table** menu.</span></span> <span data-ttu-id="b022b-153">Здесь можно создать связи и управлять ими, указать параметры таблицы дат, создать секции и изменить свойства таблицы.</span><span class="sxs-lookup"><span data-stu-id="b022b-153">From here, you can create and manage relationships, specify date table settings, create partitions, and edit table properties.</span></span> <span data-ttu-id="b022b-154">Открыв меню **Столбец**, можно добавить и удалить столбцы в таблице, закрепить столбцы, а также указать порядок сортировки.</span><span class="sxs-lookup"><span data-stu-id="b022b-154">If you click the **Column** menu, you can add and delete columns in a table, freeze columns, and specify sort order.</span></span> <span data-ttu-id="b022b-155">SSDT также добавляет на панель несколько кнопок.</span><span class="sxs-lookup"><span data-stu-id="b022b-155">SSDT also adds some buttons to the bar.</span></span> <span data-ttu-id="b022b-156">Наиболее полезной является функция "Автосумма", позволяющая создать стандартную меру агрегата для выбранного столбца.</span><span class="sxs-lookup"><span data-stu-id="b022b-156">Most useful is the AutoSum feature to create a standard aggregation measure for a selected column.</span></span> <span data-ttu-id="b022b-157">Другие кнопки на панели инструментов обеспечивают быстрый доступ к часто используемым функциям и командам.</span><span class="sxs-lookup"><span data-stu-id="b022b-157">Other toolbar buttons provide quick access to frequently used features and commands.</span></span>  
  
<span data-ttu-id="b022b-158">Просмотрите диалоговые окна и другие расположения на предмет различных функций, связанных с созданием табличных моделей.</span><span class="sxs-lookup"><span data-stu-id="b022b-158">Explore some of the dialogs and locations for various features specific to authoring tabular models.</span></span> <span data-ttu-id="b022b-159">Хотя некоторые элементы пока неактивны, вы сможете получить хорошее представление о среде для создания табличных моделей.</span><span class="sxs-lookup"><span data-stu-id="b022b-159">While some items are not yet active, you can get a good idea of the tabular model authoring environment.</span></span>  
  

## <a name="whats-next"></a><span data-ttu-id="b022b-160">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="b022b-160">What's next?</span></span>
<span data-ttu-id="b022b-161">[Занятие 2. Получение данных](../tutorials/aas-lesson-2-get-data.md).</span><span class="sxs-lookup"><span data-stu-id="b022b-161">[Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span></span>

  
  
  
