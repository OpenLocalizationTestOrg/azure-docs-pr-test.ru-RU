---
title: "aaaVisualize данных хранилища данных SQL с помощью Power BI Microsoft Azure"
description: "Визуализация данных хранилища данных SQL с помощью Power BI"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="67caa-103">Визуализация данных с помощью Power BI</span><span class="sxs-lookup"><span data-stu-id="67caa-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67caa-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="67caa-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="67caa-105">машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="67caa-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="67caa-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="67caa-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="67caa-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="67caa-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="67caa-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="67caa-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="67caa-109">В этом учебнике показано как toouse Power BI tooconnect tooSQL хранилища данных и создать базовый визуализации.</span><span class="sxs-lookup"><span data-stu-id="67caa-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="67caa-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="67caa-110">Prerequisites</span></span>
<span data-ttu-id="67caa-111">toostep изучения этого руководства требуется:</span><span class="sxs-lookup"><span data-stu-id="67caa-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="67caa-112">Хранилище данных SQL предварительно загружен с базы данных AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="67caa-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="67caa-113">tooprovision это, см. в разделе [создать хранилище данных SQL] [ Create a SQL Data Warehouse] и выберите образец hello tooload данных.</span><span class="sxs-lookup"><span data-stu-id="67caa-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="67caa-114">Если хранилище данных уже существует, но в нем нет демонстрационных данных, вы можете [загрузить их вручную][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="67caa-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="67caa-115">1. Подключение базы данных tooyour</span><span class="sxs-lookup"><span data-stu-id="67caa-115">1. Connect tooyour database</span></span>
<span data-ttu-id="67caa-116">tooopen Power BI и подключение базы данных AdventureWorksDW tooyour:</span><span class="sxs-lookup"><span data-stu-id="67caa-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="67caa-117">Вход в hello [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="67caa-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="67caa-118">Щелкните **Базы данных SQL** и выберите базу данных хранилища данных SQL AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="67caa-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Поиск базы данных][1]
3. <span data-ttu-id="67caa-120">Нажмите кнопку «Открыть в Power BI» hello.</span><span class="sxs-lookup"><span data-stu-id="67caa-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Кнопка Power BI][2]
4. <span data-ttu-id="67caa-122">Теперь должна появиться страница подключения хранилища данных SQL hello, отображение веб-адресом базы данных.</span><span class="sxs-lookup"><span data-stu-id="67caa-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="67caa-123">Нажмите кнопку «Далее».</span><span class="sxs-lookup"><span data-stu-id="67caa-123">Click next.</span></span>
   
    ![Power BI: подключение][3]
5. <span data-ttu-id="67caa-125">Введите имя сервера Azure SQL и пароль пользователя и будет базы данных полностью соединенными tooyour хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="67caa-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Power BI: вход][4]
6. <span data-ttu-id="67caa-127">После входа в Power BI, щелкните набор данных AdventureWorksDW hello левой колонке hello.</span><span class="sxs-lookup"><span data-stu-id="67caa-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="67caa-128">Будет открыта hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="67caa-128">This will open hello database.</span></span>
   
    ![Power BI: открытие AdventureWorksDW][5]

## <a name="2-create-a-report"></a><span data-ttu-id="67caa-130">2) Создание отчета</span><span class="sxs-lookup"><span data-stu-id="67caa-130">2. Create a report</span></span>
<span data-ttu-id="67caa-131">Вы являются tooanalyze Power BI теперь готовы toouse образцы данных AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="67caa-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="67caa-132">Анализ tooperform hello, AdventureWorksDW имеет представление с именем AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="67caa-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="67caa-133">Это представление содержит несколько hello основные метрики для анализа продаж компании hello hello.</span><span class="sxs-lookup"><span data-stu-id="67caa-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="67caa-134">hello tooexpand AggregateSales представление, нажмите кнопку toocreate карту объем продаж, toopostal код, в области справа поля hello, в соответствии с его.</span><span class="sxs-lookup"><span data-stu-id="67caa-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="67caa-135">Выберите столбцы tooselect hello PostalCode и SalesAmount их.</span><span class="sxs-lookup"><span data-stu-id="67caa-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![Power BI: выбор AggregateSales][6]
   
    <span data-ttu-id="67caa-137">Power BI в автоматическом режиме распознает географические данные и наносит их на карту.</span><span class="sxs-lookup"><span data-stu-id="67caa-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Карта Power BI][7]
2. <span data-ttu-id="67caa-139">На этом этапе создается линейчатая диаграмма, на которой отображается сумма продаж в зависимости от доходов клиентов.</span><span class="sxs-lookup"><span data-stu-id="67caa-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="67caa-140">toocreate этого перейдите toohello расширенный AggregateSales вид.</span><span class="sxs-lookup"><span data-stu-id="67caa-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="67caa-141">Щелкните поле SalesAmount hello.</span><span class="sxs-lookup"><span data-stu-id="67caa-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="67caa-142">Перетащите поле toohello hello доход клиента влево и вставьте его в оси.</span><span class="sxs-lookup"><span data-stu-id="67caa-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![Power BI: выбор оси][8]
   
    <span data-ttu-id="67caa-144">Мы перешли hello линейчатой диаграммы по левой hello.</span><span class="sxs-lookup"><span data-stu-id="67caa-144">We moved hello bar chart over hello left.</span></span>
   
    ![Гистограмма Power BI][9]
3. <span data-ttu-id="67caa-146">На этом этапе создается график, на котором отображены продажи по дате заказа.</span><span class="sxs-lookup"><span data-stu-id="67caa-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="67caa-147">toocreate этого перейдите toohello расширенный AggregateSales вид.</span><span class="sxs-lookup"><span data-stu-id="67caa-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="67caa-148">Щелкните SalesAmount и OrderDate.</span><span class="sxs-lookup"><span data-stu-id="67caa-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="67caa-149">В столбце визуализации hello выберите значок графика hello; Это первый значок hello вторую строку hello в визуализации.</span><span class="sxs-lookup"><span data-stu-id="67caa-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![Power BI: выбор графика][10]
   
    <span data-ttu-id="67caa-151">Теперь у вас есть отчет, показывающий трех различных вариантах визуализации данных hello.</span><span class="sxs-lookup"><span data-stu-id="67caa-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![График Power BI][11]

<span data-ttu-id="67caa-153">Ход выполнения можно сохранить в любой момент, выбрав в меню **Файл** пункт **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="67caa-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67caa-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67caa-154">Next steps</span></span>
<span data-ttu-id="67caa-155">Мы предоставили вам toowarm некоторое время с образцами данных hello, см. статью как слишком[разработки][develop], [загрузить][load], или [ Перенос][migrate].</span><span class="sxs-lookup"><span data-stu-id="67caa-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="67caa-156">Или просмотрите hello [веб-сайт Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="67caa-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
