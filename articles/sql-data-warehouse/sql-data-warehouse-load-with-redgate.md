---
title: "Загрузка данных в хранилище данных Azure с помощью Redgate | Документация Майкрософт"
description: "Сведения об использовании партнерского решения Redgate Data Platform Studio в сценариях хранения данных."
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
ms.openlocfilehash: a38b237d5bfc0450c1ca79b53a5784dbb9bf8602
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="0bf82-103">Загрузка данных с помощью Redgate Data Platform Studio</span><span class="sxs-lookup"><span data-stu-id="0bf82-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0bf82-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="0bf82-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="0bf82-105">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="0bf82-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="0bf82-106">PolyBase;</span><span class="sxs-lookup"><span data-stu-id="0bf82-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="0bf82-107">BCP</span><span class="sxs-lookup"><span data-stu-id="0bf82-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="0bf82-108">В этом руководстве приведены сведения о том, как переместить данные из локальной базы данных SQL Server в хранилище данных SQL Azure с помощью партнерского решения [Redgate Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS).</span><span class="sxs-lookup"><span data-stu-id="0bf82-108">This tutorial shows you how to use [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) to move data from an on-premises SQL Server to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="0bf82-109">Так как к Data Platform Studio применены наиболее подходящие оптимизации и исправления совместимости, это самый быстрый способ начать работу с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="0bf82-109">Data Platform Studio applies the most appropriate compatibility fixes and optimizations, so it's the quickest way to get started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="0bf82-110">Компания [Redgate](http://www.red-gate.com) — это многолетний партнер корпорации Майкрософт, который предоставляет различные средства для базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0bf82-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="0bf82-111">Решение Data Platform Studio доступно бесплатно для коммерческого и некоммерческого использования.</span><span class="sxs-lookup"><span data-stu-id="0bf82-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="0bf82-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="0bf82-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="0bf82-113">Создание или определение ресурсов</span><span class="sxs-lookup"><span data-stu-id="0bf82-113">Create or identify resources</span></span>
<span data-ttu-id="0bf82-114">Для работы с этим руководством потребуется:</span><span class="sxs-lookup"><span data-stu-id="0bf82-114">Before starting this tutorial, you need to have:</span></span>

* <span data-ttu-id="0bf82-115">**Локальная база данных SQL Server.** Данные, которые нужно импортировать в хранилище данных SQL, должны храниться в локальной базе данных SQL Server (версии 2008R2 или более поздней).</span><span class="sxs-lookup"><span data-stu-id="0bf82-115">**on-premises SQL Server Database**: The data you want to import to SQL Data Warehouse needs to come from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="0bf82-116">Data Platform Studio не может импортировать данные напрямую из базы данных SQL Azure или из текстовых файлов.</span><span class="sxs-lookup"><span data-stu-id="0bf82-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="0bf82-117">**Учетная запись хранения Azure.** Перед отправкой данных в хранилище данных SQL средство Data Platform Studio размещает данные в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf82-117">**Azure Storage Account**: Data Platform Studio stages the data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="0bf82-118">Учетная запись хранения должна быть развернута с использование модели Resource Manager (по умолчанию), а не с помощью классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="0bf82-118">The storage account must be using the “Resource Manager” deployment model (the default) rather than the “Classic” deployment model.</span></span> <span data-ttu-id="0bf82-119">Если у вас нет учетной записи хранения, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="0bf82-119">If you don't have a storage account, learn how to Create a storage account.</span></span> 
* <span data-ttu-id="0bf82-120">**Хранилище данных SQL.** В этом руководстве мы будем перемещать данные из локальной базы данных SQL Server в хранилище данных SQL. Для этого нам потребуется интернет-хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="0bf82-120">**SQL Data Warehouse**: This tutorial moves the data from on-premises SQL Server to SQL Data Warehouse, so you need to have a data warehouse online.</span></span> <span data-ttu-id="0bf82-121">Если у вас еще нет хранилища данных, создайте его.</span><span class="sxs-lookup"><span data-stu-id="0bf82-121">If you do not already have a data warehouse, learn how to Create an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="0bf82-122">Чтобы оптимизировать производительность, учетную запись хранения и хранилище данных необходимо создать в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="0bf82-122">Performance is improved if the storage account and the data warehouse are created in the same region.</span></span>
> 
> 

## <a name="step-1-sign-in-to-data-platform-studio-with-your-azure-account"></a><span data-ttu-id="0bf82-123">Шаг 1. Вход в Data Platform Studio с помощью учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="0bf82-123">Step 1: Sign in to Data Platform Studio with your Azure account</span></span>
<span data-ttu-id="0bf82-124">Откройте браузер и перейдите на веб-сайт [Data Platform Studio](https://www.dataplatformstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="0bf82-124">Open your web browser and navigate to the [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="0bf82-125">Войдите в систему с помощью учетной записи Azure, используемой для создания учетной записи хранения и хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="0bf82-125">Sign in with the same Azure account that you used to create the storage account and data warehouse.</span></span> <span data-ttu-id="0bf82-126">Если адрес электронной почты связан с рабочей или учебной учетной записью и учетной записью Майкрософт, выберите учетную запись с доступом к своим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="0bf82-126">If your email address is associated with both a work or school account and a Microsoft account, be sure to choose the account that has access to your resources.</span></span>

> [!NOTE]
> <span data-ttu-id="0bf82-127">При первом использовании Data Platform Studio появится запрос на предоставление приложению разрешений на управление ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf82-127">If this is your first time using Data Platform Studio, you are asked to grant the application permission to manage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-the-import-wizard"></a><span data-ttu-id="0bf82-128">Шаг 2. Запуск мастера импорта</span><span class="sxs-lookup"><span data-stu-id="0bf82-128">Step 2: Start the Import Wizard</span></span>
<span data-ttu-id="0bf82-129">В главном окне DPS щелкните ссылку Import to Azure SQL Data Warehouse (Импортировать в хранилище данных SQL Azure), чтобы запустить мастер импорта.</span><span class="sxs-lookup"><span data-stu-id="0bf82-129">From the DPS main screen, select the Import to Azure SQL Data Warehouse link to start the import wizard.</span></span>

![][1]

## <a name="step-3-install-the-data-platform-studio-gateway"></a><span data-ttu-id="0bf82-130">Шаг 3. Установка шлюза Data Platform Studio</span><span class="sxs-lookup"><span data-stu-id="0bf82-130">Step 3: Install the Data Platform Studio Gateway</span></span>
<span data-ttu-id="0bf82-131">Чтобы подключиться к локальной базе данных SQL Server, необходимо установить шлюз DPS.</span><span class="sxs-lookup"><span data-stu-id="0bf82-131">To connect to your on-premises SQL Server database, you need to install the DPS Gateway.</span></span> <span data-ttu-id="0bf82-132">Шлюз — это агент клиента, который обеспечивает доступ к локальной среде, извлекает данные и отправляет их в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="0bf82-132">The gateway is a client agent that provides access to your on-premises environment, extracts the data, and uploads it to your storage account.</span></span> <span data-ttu-id="0bf82-133">Данные никогда не проходят через серверы Redgate.</span><span class="sxs-lookup"><span data-stu-id="0bf82-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="0bf82-134">Чтобы установить шлюз, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="0bf82-134">To install the Gateway:</span></span>

1. <span data-ttu-id="0bf82-135">Щелкните ссылку **Create Gateway** (Создать шлюз).</span><span class="sxs-lookup"><span data-stu-id="0bf82-135">Click the **Create Gateway** link</span></span>
2. <span data-ttu-id="0bf82-136">Скачайте и установите шлюз с помощью предоставленного установщика.</span><span class="sxs-lookup"><span data-stu-id="0bf82-136">Download and install the Gateway using the provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="0bf82-137">Шлюз можно установить на любой машине с сетевым доступом к базе данных-источнику SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0bf82-137">The Gateway can be installed on any machine with network access to the source SQL Server database.</span></span> <span data-ttu-id="0bf82-138">При доступе к базе данных SQL Server выполняется проверка подлинности Windows на основе учетных данных текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="0bf82-138">It accesses the SQL Server database using Windows authentication with the credentials of the current user.</span></span>
> 
> 

<span data-ttu-id="0bf82-139">После установки состояние шлюза изменится на Connected (Подключен). Нажмите кнопку Next (Далее).</span><span class="sxs-lookup"><span data-stu-id="0bf82-139">Once installed, the Gateway status changes to Connected and you can select Next.</span></span>

## <a name="step-4-identify-the-source-database"></a><span data-ttu-id="0bf82-140">Шаг 4. Определение базы данных-источника</span><span class="sxs-lookup"><span data-stu-id="0bf82-140">Step 4: Identify the source database</span></span>
<span data-ttu-id="0bf82-141">В текстовом поле *Enter Server Name* (Введите имя сервера) введите имя сервера, на котором размещены базы данных, и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="0bf82-141">In the *Enter Server Name* textbox, enter the name of the server that hosts your database and select **Next**.</span></span> <span data-ttu-id="0bf82-142">В раскрывающемся меню выберите базу данных, из которой нужно импортировать данные.</span><span class="sxs-lookup"><span data-stu-id="0bf82-142">Then, from the drop-down menu, select the database you want to import data from.</span></span>

![][3]

<span data-ttu-id="0bf82-143">DPS проверяет таблицы для импорта в выбранной базе данных.</span><span class="sxs-lookup"><span data-stu-id="0bf82-143">DPS inspects the selected database for tables to import.</span></span> <span data-ttu-id="0bf82-144">По умолчанию DPS импортирует все таблицы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="0bf82-144">By default, DPS imports all the tables in the database.</span></span> <span data-ttu-id="0bf82-145">Чтобы выбрать таблицы или отменить их выбор, щелкните ссылку All Tables (Все таблицы).</span><span class="sxs-lookup"><span data-stu-id="0bf82-145">You can select or deselect tables by expanding the All Tables link.</span></span> <span data-ttu-id="0bf82-146">Нажмите кнопку Next (Далее), чтобы перейти к следующему окну.</span><span class="sxs-lookup"><span data-stu-id="0bf82-146">Select the Next button to move forward.</span></span>

## <a name="step-5-choose-a-storage-account-to-stage-the-data"></a><span data-ttu-id="0bf82-147">Шаг 5. Выбор учетной записи хранения для размещения данных</span><span class="sxs-lookup"><span data-stu-id="0bf82-147">Step 5: Choose a storage account to stage the data</span></span>
<span data-ttu-id="0bf82-148">DPS запрашивает расположение для размещения данных.</span><span class="sxs-lookup"><span data-stu-id="0bf82-148">DPS prompts you for a location to stage the data.</span></span> <span data-ttu-id="0bf82-149">Выберите имеющуюся учетную запись хранения в подписке и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="0bf82-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="0bf82-150">DPS создаст в выбранной учетной записи хранения контейнер больших двоичных объектов. Для каждой операции импорта будет использоваться отдельная папка.</span><span class="sxs-lookup"><span data-stu-id="0bf82-150">DPS will create a new blob container in the chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="0bf82-151">Шаг 6. Выбор хранилища данных</span><span class="sxs-lookup"><span data-stu-id="0bf82-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="0bf82-152">Далее выберите интернет-базу данных в [хранилище данных SQL Azure](http://aka.ms/sqldw), в которую нужно импортировать данные.</span><span class="sxs-lookup"><span data-stu-id="0bf82-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database to import the data into.</span></span> <span data-ttu-id="0bf82-153">Выбрав базу данных, введите учетные данные, чтобы подключиться к ней, и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="0bf82-153">Once you've selected your database, you need to enter the credentials to connect to the database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="0bf82-154">DPS объединяет исходные таблицы данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="0bf82-154">DPS merges the source data tables into the data warehouse.</span></span> <span data-ttu-id="0bf82-155">Если из-за именования таблицы нужно перезаписать имеющиеся таблицы в хранилище данных, DPS выводит предупреждение.</span><span class="sxs-lookup"><span data-stu-id="0bf82-155">DPS warns you if the table name requires it to overwrite existing tables in the data warehouse.</span></span> <span data-ttu-id="0bf82-156">При необходимости из хранилища данных можно удалить любые имеющиеся объекты. Для этого перед импортом установите флажок Delete all existing objects (Удалить все имеющиеся объекты).</span><span class="sxs-lookup"><span data-stu-id="0bf82-156">You may optionally delete any existing objects in the data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-the-data"></a><span data-ttu-id="0bf82-157">Шаг 7. Импорт данных</span><span class="sxs-lookup"><span data-stu-id="0bf82-157">Step 7: Import the data</span></span>
<span data-ttu-id="0bf82-158">В DPS появится запрос на подтверждение импорта данных.</span><span class="sxs-lookup"><span data-stu-id="0bf82-158">DPS confirms that you would like to import the data.</span></span> <span data-ttu-id="0bf82-159">Чтобы начать импорт данных, просто нажмите кнопку Start import (Начать импорт).</span><span class="sxs-lookup"><span data-stu-id="0bf82-159">Simply click the Start import button to begin the data import.</span></span>

![][6]

<span data-ttu-id="0bf82-160">В DPS ход выполнения извлечения и передачи данных из локальной базы данных SQL Server, а также их импорта в хранилище данных SQL, визуализирован.</span><span class="sxs-lookup"><span data-stu-id="0bf82-160">DPS displays a visualization that shows the progress of extracting and uploading the data from the on-premises SQL Server and the progress of the import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="0bf82-161">После завершения импорта DPS отображает сводку по импорту данных и отчет об изменениях на основе выполненных исправлений совместимости.</span><span class="sxs-lookup"><span data-stu-id="0bf82-161">Once the import is complete, DPS displays a summary of the data import and a change report of the compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="0bf82-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0bf82-162">Next steps</span></span>
<span data-ttu-id="0bf82-163">Дополнительные сведения о просмотре данных в хранилище данных SQL см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="0bf82-163">To explore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="0bf82-164">[Запросы к хранилищу данных SQL Azure (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="0bf82-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="0bf82-165">[Визуализация данных с помощью Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="0bf82-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="0bf82-166">Дополнительные сведения о решении Redgate Data Platform Studio см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="0bf82-166">To learn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="0bf82-167">Домашняя страница DPS</span><span class="sxs-lookup"><span data-stu-id="0bf82-167">Visit the DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="0bf82-168">Демонстрационное видео DPS на Channel 9</span><span class="sxs-lookup"><span data-stu-id="0bf82-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="0bf82-169">Общие сведения о других способах переноса и отправки данных в хранилище данных SQL см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="0bf82-169">For an overview of other ways to migrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="0bf82-170">[Перенос решения в хранилище данных SQL][Migrate your solution to SQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="0bf82-170">[Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span></span>
* [<span data-ttu-id="0bf82-171">Загрузка данных в хранилище данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="0bf82-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="0bf82-172">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="0bf82-172">For more development tips, see the [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

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
[Migrate your solution to SQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
