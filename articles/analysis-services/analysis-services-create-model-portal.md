---
title: "aaaCreate табличной модели с помощью конструктора веб-Azure Analysis Services hello | Документы Microsoft"
description: "Узнайте, как toocreate табличной модели служб Azure Analysis Services с помощью hello Web designer на портале Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="6b94c-103">Создание модели на портале Azure</span><span class="sxs-lookup"><span data-stu-id="6b94c-103">Create a model in Azure portal</span></span>

<span data-ttu-id="6b94c-104">Hello Azure Analysis Services web designer (Предварительная версия) на портале Azure дает toocreate легко и быстро и редактирование табличных моделей и запрос модели данных прямо в браузере.</span><span class="sxs-lookup"><span data-stu-id="6b94c-104">hello Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way toocreate and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="6b94c-105">Помните, является веб-дизайнера hello **предварительной версии**.</span><span class="sxs-lookup"><span data-stu-id="6b94c-105">Keep in mind, hello web designer is **preview**.</span></span> <span data-ttu-id="6b94c-106">Во время добавления новых функций все время hello, во время предварительного просмотра ограничена функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="6b94c-106">While new functionality is being added all hello time, in preview, functionality is limited.</span></span> <span data-ttu-id="6b94c-107">Для более сложных модель разработки и тестирования это лучший toouse Visual Studio (SSDT) и SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="6b94c-107">For more advanced model development and testing, it's best toouse Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b94c-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6b94c-108">Prerequisites</span></span>

- <span data-ttu-id="6b94c-109">Сервер служб Analysis Services Azure на уровне Standard или разработчика hello.</span><span class="sxs-lookup"><span data-stu-id="6b94c-109">An Azure Analysis Services server at hello Standard or Developer tier.</span></span> <span data-ttu-id="6b94c-110">Новые модели, созданные с помощью веб-дизайнера hello, DirectQuery, поддерживаемое только эти уровни.</span><span class="sxs-lookup"><span data-stu-id="6b94c-110">New models created by using hello Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="6b94c-111">База данных SQL Azure, хранилище данных SQL Azure или PBIX-файл Power BI Desktop в качестве источника данных.</span><span class="sxs-lookup"><span data-stu-id="6b94c-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="6b94c-112">Новые модели, созданные из файлов Power BI Desktop, поддерживают в качестве источников данных Базу данных SQL Azure, хранилище данных SQL Azure, Oracle и Teradata.</span><span class="sxs-lookup"><span data-stu-id="6b94c-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="6b94c-113">Учетная запись SQL Server и пароль для подключения tooAzure источники данных базы данных SQL или хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6b94c-113">A SQL Server account and password for connecting tooAzure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="toocreate-a-new-tabular-model"></a><span data-ttu-id="6b94c-114">toocreate новой табличной модели</span><span class="sxs-lookup"><span data-stu-id="6b94c-114">toocreate a new tabular model</span></span>

1. <span data-ttu-id="6b94c-115">В колонке сервера **Обзор** выберите **Web designer** (Конструктор веб-приложений) и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="6b94c-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Создание модели на портале Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="6b94c-117">Выбрав **Web designer** (Конструктор веб-приложений)  >  **Модели**, нажмите кнопку **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6b94c-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Создание модели на портале Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="6b94c-119">В диалоговом окне **Новая модель** введите имя модели и выберите источник данных.</span><span class="sxs-lookup"><span data-stu-id="6b94c-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Диалоговое окно "Новая модель" на портале Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="6b94c-121">В **Connect**, введите hello свойства соединения.</span><span class="sxs-lookup"><span data-stu-id="6b94c-121">In **Connect**, enter hello connection properties.</span></span> <span data-ttu-id="6b94c-122">Необходимо указать имя пользователя и пароль учетной записи SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6b94c-122">Username and password must be a SQL Server account.</span></span>

     ![Диалоговое окно "Подключение" на портале Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="6b94c-124">В **таблиц и представлений**, выберите tooinclude hello таблиц в модели и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="6b94c-124">In **Tables and views**, select hello tables tooinclude in your model, and then click **Create**.</span></span> <span data-ttu-id="6b94c-125">Связи между таблицами создаются автоматически с помощью пары ключей.</span><span class="sxs-lookup"><span data-stu-id="6b94c-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Выбор таблиц и представлений](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="6b94c-127">Новая модель отобразится в браузере.</span><span class="sxs-lookup"><span data-stu-id="6b94c-127">Your new model appears in your browser.</span></span> <span data-ttu-id="6b94c-128">На данном этапе можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="6b94c-128">From here, you can:</span></span>   

- <span data-ttu-id="6b94c-129">Запрос данных модели, перетаскивая поля конструктор запросов toohello и добавления фильтров.</span><span class="sxs-lookup"><span data-stu-id="6b94c-129">Query model data by dragging fields toohello query designer and adding filters.</span></span>
- <span data-ttu-id="6b94c-130">Создавать новые меры в таблицах.</span><span class="sxs-lookup"><span data-stu-id="6b94c-130">Create new measures in tables.</span></span>
- <span data-ttu-id="6b94c-131">Изменение метаданных модели с помощью редактора json hello.</span><span class="sxs-lookup"><span data-stu-id="6b94c-131">Edit model metadata by using hello json editor.</span></span>
- <span data-ttu-id="6b94c-132">Откройте модель hello в Visual Studio (SSDT), Power BI Desktop или Excel.</span><span class="sxs-lookup"><span data-stu-id="6b94c-132">Open hello model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Выбор таблиц и представлений](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="6b94c-134">При попытке создать новые меры в браузере или изменить метаданные модели, модели tooyour эти изменения сохраняются в Azure.</span><span class="sxs-lookup"><span data-stu-id="6b94c-134">When you edit model metadata or create new measures in your browser, you're saving those changes tooyour model in Azure.</span></span> <span data-ttu-id="6b94c-135">Если вы также работаете с моделью в SSDT, Power BI Desktop или Excel, то она может оказаться несинхронизированной.</span><span class="sxs-lookup"><span data-stu-id="6b94c-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6b94c-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b94c-136">Next steps</span></span> 
[<span data-ttu-id="6b94c-137">Управление ролями и пользователями базы данных</span><span class="sxs-lookup"><span data-stu-id="6b94c-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="6b94c-138">Подключение с помощью Excel</span><span class="sxs-lookup"><span data-stu-id="6b94c-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


