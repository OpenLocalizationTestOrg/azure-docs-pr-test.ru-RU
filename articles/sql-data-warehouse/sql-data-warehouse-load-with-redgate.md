---
title: "хранилище данных Azure tooyour данных tooload aaaUse Redgate | Документы Microsoft"
description: "Узнайте, как toouse Redgate Studio платформы данных для сценариев хранилища данных."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="cd0fa-103">Загрузка данных с помощью Redgate Data Platform Studio</span><span class="sxs-lookup"><span data-stu-id="cd0fa-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd0fa-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="cd0fa-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="cd0fa-105">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="cd0fa-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="cd0fa-106">PolyBase;</span><span class="sxs-lookup"><span data-stu-id="cd0fa-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="cd0fa-107">BCP</span><span class="sxs-lookup"><span data-stu-id="cd0fa-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="cd0fa-108">В этом учебнике показано как toouse [Studio платформы данных Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) (диагностики) toomove данные из локального SQL Server tooAzure хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-108">This tutorial shows you how toouse [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) toomove data from an on-premises SQL Server tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="cd0fa-109">Studio платформы данных применяет исправления совместимости наиболее подходящий hello и оптимизации, поэтому он содержит быстрее других hello tooget способ работы с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-109">Data Platform Studio applies hello most appropriate compatibility fixes and optimizations, so it's hello quickest way tooget started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="cd0fa-110">Компания [Redgate](http://www.red-gate.com) — это многолетний партнер корпорации Майкрософт, который предоставляет различные средства для базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="cd0fa-111">Решение Data Platform Studio доступно бесплатно для коммерческого и некоммерческого использования.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="cd0fa-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="cd0fa-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="cd0fa-113">Создание или определение ресурсов</span><span class="sxs-lookup"><span data-stu-id="cd0fa-113">Create or identify resources</span></span>
<span data-ttu-id="cd0fa-114">Перед запуском этого учебника, необходимо toohave:</span><span class="sxs-lookup"><span data-stu-id="cd0fa-114">Before starting this tutorial, you need toohave:</span></span>

* <span data-ttu-id="cd0fa-115">**Локальная база данных SQL Server**: hello данные нужно tooimport tooSQL хранилища данных требуется toocome из локального SQL Server (версии 2008 R2 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="cd0fa-115">**on-premises SQL Server Database**: hello data you want tooimport tooSQL Data Warehouse needs toocome from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="cd0fa-116">Data Platform Studio не может импортировать данные напрямую из базы данных SQL Azure или из текстовых файлов.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="cd0fa-117">**Учетная запись хранения Azure**: Studio платформы данных готовит hello данных в хранилище больших двоичных объектов Azure перед загрузкой в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-117">**Azure Storage Account**: Data Platform Studio stages hello data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="cd0fa-118">Hello учетной записи хранилища необходимо использовать модель развертывания hello «диспетчер ресурсов» (по умолчанию hello) вместо модель развертывания «Классический» hello.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-118">hello storage account must be using hello “Resource Manager” deployment model (hello default) rather than hello “Classic” deployment model.</span></span> <span data-ttu-id="cd0fa-119">При отсутствии учетной записи хранилища, узнайте, как tooCreate учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-119">If you don't have a storage account, learn how tooCreate a storage account.</span></span> 
* <span data-ttu-id="cd0fa-120">**Хранилище данных SQL**: этого учебника перемещает hello данные из tooSQL в локальной среде SQL Server хранилища данных, поэтому требуется toohave хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-120">**SQL Data Warehouse**: This tutorial moves hello data from on-premises SQL Server tooSQL Data Warehouse, so you need toohave a data warehouse online.</span></span> <span data-ttu-id="cd0fa-121">Если у вас еще нет в хранилище данных, узнайте, как tooCreate хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-121">If you do not already have a data warehouse, learn how tooCreate an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="cd0fa-122">Повышение производительности, если учетная запись хранения hello и хранилище данных hello создаются в hello же области.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-122">Performance is improved if hello storage account and hello data warehouse are created in hello same region.</span></span>
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a><span data-ttu-id="cd0fa-123">Шаг 1: Войдите в tooData Studio платформы с учетной записью Azure</span><span class="sxs-lookup"><span data-stu-id="cd0fa-123">Step 1: Sign in tooData Platform Studio with your Azure account</span></span>
<span data-ttu-id="cd0fa-124">Откройте браузер и перейдите toohello [Studio платформы данных](https://www.dataplatformstudio.com/) веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-124">Open your web browser and navigate toohello [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="cd0fa-125">Вход с hello одной учетной записью Azure, то используется toocreate hello хранилища учетной записи и хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-125">Sign in with hello same Azure account that you used toocreate hello storage account and data warehouse.</span></span> <span data-ttu-id="cd0fa-126">Если ваш адрес электронной почты связан с рабочую или учебную учетную запись и учетную запись Майкрософт, будет убедиться, что hello toochoose учетную запись, которая имеет доступ к ресурсам tooyour.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-126">If your email address is associated with both a work or school account and a Microsoft account, be sure toochoose hello account that has access tooyour resources.</span></span>

> [!NOTE]
> <span data-ttu-id="cd0fa-127">Если вы впервые используете Studio платформы данных, задаваемые toomanage разрешений приложения hello toogrant ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-127">If this is your first time using Data Platform Studio, you are asked toogrant hello application permission toomanage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-hello-import-wizard"></a><span data-ttu-id="cd0fa-128">Шаг 2: Запуск мастера импорта hello</span><span class="sxs-lookup"><span data-stu-id="cd0fa-128">Step 2: Start hello Import Wizard</span></span>
<span data-ttu-id="cd0fa-129">Главный экран приветствия диагностики выберите hello импорта tooAzure хранилище данных SQL ссылку toostart приветствия мастера импорта.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-129">From hello DPS main screen, select hello Import tooAzure SQL Data Warehouse link toostart hello import wizard.</span></span>

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a><span data-ttu-id="cd0fa-130">Шаг 3: Установка hello шлюз Studio платформы данных</span><span class="sxs-lookup"><span data-stu-id="cd0fa-130">Step 3: Install hello Data Platform Studio Gateway</span></span>
<span data-ttu-id="cd0fa-131">База данных SQL Server в локальной tooyour tooconnect, необходимо tooinstall hello диагностики шлюза.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-131">tooconnect tooyour on-premises SQL Server database, you need tooinstall hello DPS Gateway.</span></span> <span data-ttu-id="cd0fa-132">шлюз Hello — агент клиента, который предоставляет доступ tooyour в локальную среду, извлекает данные hello и передает его tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-132">hello gateway is a client agent that provides access tooyour on-premises environment, extracts hello data, and uploads it tooyour storage account.</span></span> <span data-ttu-id="cd0fa-133">Данные никогда не проходят через серверы Redgate.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="cd0fa-134">hello tooinstall шлюз:</span><span class="sxs-lookup"><span data-stu-id="cd0fa-134">tooinstall hello Gateway:</span></span>

1. <span data-ttu-id="cd0fa-135">Нажмите кнопку hello **создать шлюз** ссылку</span><span class="sxs-lookup"><span data-stu-id="cd0fa-135">Click hello **Create Gateway** link</span></span>
2. <span data-ttu-id="cd0fa-136">Загрузка и установка hello шлюза с помощью hello предоставленный установщика</span><span class="sxs-lookup"><span data-stu-id="cd0fa-136">Download and install hello Gateway using hello provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="cd0fa-137">Hello шлюз можно установить на любом компьютере с базой данных SQL Server источника toohello доступа к сети.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-137">hello Gateway can be installed on any machine with network access toohello source SQL Server database.</span></span> <span data-ttu-id="cd0fa-138">Он обращается к hello базы данных SQL Server с помощью проверки подлинности Windows с учетными данными hello hello текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-138">It accesses hello SQL Server database using Windows authentication with hello credentials of hello current user.</span></span>
> 
> 

<span data-ttu-id="cd0fa-139">После установки hello tooConnected изменения состояния шлюза и выборе Далее.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-139">Once installed, hello Gateway status changes tooConnected and you can select Next.</span></span>

## <a name="step-4-identify-hello-source-database"></a><span data-ttu-id="cd0fa-140">Шаг 4: Определение hello базы данных-источника</span><span class="sxs-lookup"><span data-stu-id="cd0fa-140">Step 4: Identify hello source database</span></span>
<span data-ttu-id="cd0fa-141">В hello *введите имя сервера* текстовом поле введите имя hello hello сервера, на котором размещены базы данных и выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-141">In hello *Enter Server Name* textbox, enter hello name of hello server that hosts your database and select **Next**.</span></span> <span data-ttu-id="cd0fa-142">Hello раскрывающегося меню, выберите базу данных hello нужные данные tooimport из.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-142">Then, from hello drop-down menu, select hello database you want tooimport data from.</span></span>

![][3]

<span data-ttu-id="cd0fa-143">Проверяет hello выбранной базы данных для таблицы tooimport.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-143">DPS inspects hello selected database for tables tooimport.</span></span> <span data-ttu-id="cd0fa-144">По умолчанию диагностики импортирует все hello таблицы в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-144">By default, DPS imports all hello tables in hello database.</span></span> <span data-ttu-id="cd0fa-145">Можно выбрать или отменить выбор таблиц, развернув приветствия связывать все таблицы.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-145">You can select or deselect tables by expanding hello All Tables link.</span></span> <span data-ttu-id="cd0fa-146">Выберите hello далее кнопку toomove вперед.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-146">Select hello Next button toomove forward.</span></span>

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a><span data-ttu-id="cd0fa-147">Шаг 5: Выберите данные hello toostage учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="cd0fa-147">Step 5: Choose a storage account toostage hello data</span></span>
<span data-ttu-id="cd0fa-148">Диагностики запрашивает toostage hello расположения данных.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-148">DPS prompts you for a location toostage hello data.</span></span> <span data-ttu-id="cd0fa-149">Выберите имеющуюся учетную запись хранения в подписке и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="cd0fa-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="cd0fa-150">Диагностики будет создать новый контейнер больших двоичных объектов в выбранной учетной записи хранилища hello и использовать отдельные папки для каждого импорта.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-150">DPS will create a new blob container in hello chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="cd0fa-151">Шаг 6. Выбор хранилища данных</span><span class="sxs-lookup"><span data-stu-id="cd0fa-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="cd0fa-152">Затем выберите оперативного [хранилище данных SQL Azure](http://aka.ms/sqldw) tooimport hello данных в базы данных.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database tooimport hello data into.</span></span> <span data-ttu-id="cd0fa-153">После выбора базы данных, вам потребуется tooenter hello учетные данные tooconnect toohello базы данных и выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-153">Once you've selected your database, you need tooenter hello credentials tooconnect toohello database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="cd0fa-154">Диагностики объединяет таблицы с исходными данными hello в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-154">DPS merges hello source data tables into hello data warehouse.</span></span> <span data-ttu-id="cd0fa-155">Диагностики выдает предупреждение, если имя таблицы hello требует toooverwrite таблиц, существующих в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-155">DPS warns you if hello table name requires it toooverwrite existing tables in hello data warehouse.</span></span> <span data-ttu-id="cd0fa-156">Можно удалить все существующие объекты в хранилище данных hello, отсчет удалить все существующие объекты перед импортом.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-156">You may optionally delete any existing objects in hello data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-hello-data"></a><span data-ttu-id="cd0fa-157">Шаг 7: Импорт данных hello</span><span class="sxs-lookup"><span data-stu-id="cd0fa-157">Step 7: Import hello data</span></span>
<span data-ttu-id="cd0fa-158">Диагностики подтверждает, что хотелось бы tooimport hello данных.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-158">DPS confirms that you would like tooimport hello data.</span></span> <span data-ttu-id="cd0fa-159">Просто нажмите кнопку Пуск hello импорта toobegin кнопку hello импорта данных.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-159">Simply click hello Start import button toobegin hello data import.</span></span>

![][6]

<span data-ttu-id="cd0fa-160">Диагностики отображает представление, где отображается ход hello извлечение и передача данных hello с hello в локальной среде SQL Server и hello ход выполнения импорта hello в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-160">DPS displays a visualization that shows hello progress of extracting and uploading hello data from hello on-premises SQL Server and hello progress of hello import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="cd0fa-161">После завершения импорта hello диагностики отображается сводка по импорту данных hello и изменение отчета о hello исправления совместимости, которые были выполнены.</span><span class="sxs-lookup"><span data-stu-id="cd0fa-161">Once hello import is complete, DPS displays a summary of hello data import and a change report of hello compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="cd0fa-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd0fa-162">Next steps</span></span>
<span data-ttu-id="cd0fa-163">tooexplore ваши данные в хранилище данных SQL, начните с просмотра:</span><span class="sxs-lookup"><span data-stu-id="cd0fa-163">tooexplore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="cd0fa-164">[Запросы к хранилищу данных SQL Azure (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="cd0fa-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="cd0fa-165">[Визуализация данных с помощью Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="cd0fa-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="cd0fa-166">Дополнительные сведения о Studio платформы данных Redgate toolearn:</span><span class="sxs-lookup"><span data-stu-id="cd0fa-166">toolearn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="cd0fa-167">Посетите домашнюю страницу диагностики hello</span><span class="sxs-lookup"><span data-stu-id="cd0fa-167">Visit hello DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="cd0fa-168">Демонстрационное видео DPS на Channel 9</span><span class="sxs-lookup"><span data-stu-id="cd0fa-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="cd0fa-169">Общие сведения о других способах toomigrate и загрузка данных в хранилище данных SQL см.:</span><span class="sxs-lookup"><span data-stu-id="cd0fa-169">For an overview of other ways toomigrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="cd0fa-170">[Перенос tooSQL вашего решения хранилища данных][Migrate your solution tooSQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="cd0fa-170">[Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span></span>
* [<span data-ttu-id="cd0fa-171">Загрузка данных в хранилище данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="cd0fa-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="cd0fa-172">Дополнительные советы по разработке в разделе hello [Общие сведения о разработке хранилище данных SQL](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="cd0fa-172">For more development tips, see hello [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
