---
title: "Загрузка данных в хранилище данных SQL Azure | Документация Майкрософт"
description: "Распространенные сценарии загрузки данных в хранилище данных SQL. Они включают использование PolyBase, хранилища BLOB-объектов Azure, неструктурированных файлов и доставки диска. Кроме того, можно использовать сторонние средства."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: c4199a387f5cdbd477a5e348e48ba8e8b5900075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="9d2e2-105">Загрузка данных в хранилище данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="9d2e2-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="9d2e2-106">Сводка параметров сценария и рекомендаций по загрузке данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="9d2e2-107">Обычно самая сложная часть загрузки — это подготовка данных для загрузки.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-107">The hardest part of loading data is usually preparing the data for the load.</span></span> <span data-ttu-id="9d2e2-108">Azure упрощает загрузку за счет использования хранилища BLOB-объектов Azure как общего хранилища данных для многих служб и фабрики данных Azure для управления взаимодействием и перемещениям данных между службами Azure.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span></span> <span data-ttu-id="9d2e2-109">Эти процессы интегрированы в технологию PolyBase, которая загружает данные из хранилища BLOB-объектов Azure в хранилище данных SQL с массовой параллельной обработкой (MPP).</span><span class="sxs-lookup"><span data-stu-id="9d2e2-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="9d2e2-110">Инструкции по загрузке образцов баз данных в хранилище данных SQL см. в [этой статье][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="9d2e2-111">Загрузка из хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="9d2e2-111">Load from Azure blob storage</span></span>
<span data-ttu-id="9d2e2-112">Самый быстрый способ импорта данных в хранилище данных SQL — это использование PolyBase для загрузки данных из хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span></span> <span data-ttu-id="9d2e2-113">PolyBase использует структуру массовой параллельной обработки (MPP) в хранилище данных SQL для параллельной загрузки данных из хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span></span> <span data-ttu-id="9d2e2-114">Для работы с PolyBase можно использовать команды T-SQL или конвейер фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="9d2e2-115">1. Использование PolyBase и T-SQL</span><span class="sxs-lookup"><span data-stu-id="9d2e2-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="9d2e2-116">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="9d2e2-116">Summary of loading process:</span></span>

1. <span data-ttu-id="9d2e2-117">Перенесите данные в хранилище BLOB-объектов Azure или Azure Data Lake Store и сохраните их в виде текстовых файлов.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="9d2e2-118">Настройте внешние объекты в хранилище данных SQL, определив расположение и формат данных.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span></span>
3. <span data-ttu-id="9d2e2-119">Выполните команду T-SQL для параллельной загрузки данных в новую таблицу баз данных.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-119">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="9d2e2-120">Инструкции см. в статье [Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="9d2e2-121">2) Использование фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="9d2e2-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="9d2e2-122">Чтобы упростить работу с PolyBase, можно создать конвейер фабрики данных Azure, использующий PolyBase для загрузки данных из хранилища BLOB-объектов Azure в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="9d2e2-123">Он настраивается быстро, поскольку не требует определения команд T-SQL.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-123">This is fast to configure since you don't need to define the T-SQL objects.</span></span> <span data-ttu-id="9d2e2-124">Если требуется только запрос внешних данных без импорта, используйте T-SQL.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-124">If you need to query the external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="9d2e2-125">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="9d2e2-125">Summary of loading process:</span></span>

1. <span data-ttu-id="9d2e2-126">Перенесите данные в хранилище BLOB-объектов Azure и сохраните их в виде текстовых файлов.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-126">Move your data to Azure blob storage and store it in text files.</span></span> <span data-ttu-id="9d2e2-127">Сейчас фабрика данных Azure не поддерживает подключение к ADLS с использованием PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="9d2e2-128">Создайте конвейер фабрики данных Azure для приема данных.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-128">Create an Azure Data Factory pipeline to ingest the data.</span></span> <span data-ttu-id="9d2e2-129">Используйте параметр PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-129">Use the PolyBase option.</span></span>
4. <span data-ttu-id="9d2e2-130">Спланируйте и запустите конвейер.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-130">Schedule and run the pipeline.</span></span>

<span data-ttu-id="9d2e2-131">Инструкции см. в статье [Загрузка данных в хранилище данных SQL с помощью фабрики данных][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="9d2e2-132">Загрузка из SQL Server</span><span class="sxs-lookup"><span data-stu-id="9d2e2-132">Load from SQL Server</span></span>
<span data-ttu-id="9d2e2-133">Для загрузки данных из SQL Server в хранилище данных SQL можно использовать службы интеграции, передавать неструктурированные файлы или отправлять диски в корпорацию Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span></span> <span data-ttu-id="9d2e2-134">Далее в этой статье будут рассмотрены различные процессы загрузки и даны ссылки на соответствующие учебники.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-134">Read on to see a summary of the different loading processes and links to tutorials.</span></span>

<span data-ttu-id="9d2e2-135">Сведения о планировании полной миграции данных из SQL Server в хранилище данных SQL см. в статье [Перенос решения в хранилище данных SQL][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="9d2e2-136">Использование служб интеграции (SSIS)</span><span class="sxs-lookup"><span data-stu-id="9d2e2-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="9d2e2-137">Если вы уже используете пакеты служб интеграции (SSIS) для загрузки в SQL Server, эти пакеты можно обновить таким образом, чтобы SQL Server использовался как источник, а хранилище данных SQL — как конечный пункт.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span></span> <span data-ttu-id="9d2e2-138">Это делается быстро и легко и подходит, если вы не пытаетесь перенести процесс загрузки для использования данных, которые уже находится в облаке.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span></span> <span data-ttu-id="9d2e2-139">При этом загрузка осуществляется медленнее, чем при использовании PolyBase, поскольку SSIS не выполняет параллельную загрузку.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span></span>

<span data-ttu-id="9d2e2-140">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="9d2e2-140">Summary of loading process:</span></span>

1. <span data-ttu-id="9d2e2-141">Измените пакет служб интеграции таким образом, чтобы он указывал на экземпляр SQL Server как источник и на базу данных хранилища данных SQL как на конечный пункт.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span></span>
2. <span data-ttu-id="9d2e2-142">Перенесите схему в хранилище данных SQL, если вы это еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="9d2e2-143">Измените сопоставление в пакетах, используя только те типы данных, которые поддерживаются хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="9d2e2-144">Спланируйте и запустите пакет.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-144">Schedule and run the package.</span></span>

<span data-ttu-id="9d2e2-145">Инструкции см. в статье [Загрузка данных из SQL Server в хранилище данных SQL Azure (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="9d2e2-146">Использование AZCopy (рекомендуется при объеме данных меньше 10 ТБ)</span><span class="sxs-lookup"><span data-stu-id="9d2e2-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="9d2e2-147">Если объем данных меньше 10 ТБ, можно экспортировать данные из SQL Server в неструктурированные файлы, скопировать их в хранилище BLOB-объектов Azure, а затем загрузить данные в хранилище данных SQL с помощью PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span></span>

<span data-ttu-id="9d2e2-148">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="9d2e2-148">Summary of loading process:</span></span>

1. <span data-ttu-id="9d2e2-149">Экспортируйте данные из SQL Server в неструктурированные файлы с помощью служебной программы командной строки bcp.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="9d2e2-150">Скопируйте данные из неструктурированных файлов в хранилище BLOB-объектов Azure с помощью служебной программы командной строки AZCopy.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span></span>
3. <span data-ttu-id="9d2e2-151">Загрузите данные в хранилище данных SQL с помощью PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-151">Use PolyBase to load into SQL Data Warehouse.</span></span>

<span data-ttu-id="9d2e2-152">Инструкции см. в статье [Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="9d2e2-153">Использование программы bcp</span><span class="sxs-lookup"><span data-stu-id="9d2e2-153">Use bcp</span></span>
<span data-ttu-id="9d2e2-154">Если данных немного, их можно загрузить непосредственно в хранилище данных SQL с помощью bcp.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="9d2e2-155">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="9d2e2-155">Summary of loading process:</span></span>

1. <span data-ttu-id="9d2e2-156">Экспортируйте данные из SQL Server в неструктурированные файлы с помощью служебной программы командной строки bcp.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="9d2e2-157">Загрузите данные из неструктурированных файлов непосредственно в хранилище данных SQL с помощью bcp.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="9d2e2-158">Инструкции см. в статье [Загрузка данных из SQL Server в хранилище данных SQL Azure (неструктурированные файлы)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="9d2e2-159">Использование импорта и экспорта (рекомендуется при объеме данных меньше 10 ТБ)</span><span class="sxs-lookup"><span data-stu-id="9d2e2-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="9d2e2-160">Если объем данных превышает 10 ТБ и вы хотите перенести их в Azure, мы рекомендуем использовать для доставки дисков нашу службу [импорта и экспорта][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="9d2e2-161">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="9d2e2-161">Summary of loading process</span></span>

1. <span data-ttu-id="9d2e2-162">Экспортируйте данные из SQL Server в неструктурированные файлы на переносных дисках с помощью служебной программы командной строки bcp.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span></span>
2. <span data-ttu-id="9d2e2-163">Перешлите диски в корпорацию Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-163">Ship the disks to Microsoft.</span></span>
3. <span data-ttu-id="9d2e2-164">Майкрософт загружает данные в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="9d2e2-164">Microsoft loads the data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="9d2e2-165">Загрузка из HDInsight</span><span class="sxs-lookup"><span data-stu-id="9d2e2-165">Load from HDInsight</span></span>
<span data-ttu-id="9d2e2-166">Хранилище данных SQL поддерживает загрузку данных из HDInsight через PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="9d2e2-167">Процесс будет таким же, как при загрузке данных из хранилища BLOB-объектов Azure с использованием PolyBase для подключения к HDInsight и загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="9d2e2-168">1. Использование PolyBase и T-SQL</span><span class="sxs-lookup"><span data-stu-id="9d2e2-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="9d2e2-169">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="9d2e2-169">Summary of loading process:</span></span>

1. <span data-ttu-id="9d2e2-170">Переместите данные в HDInsight и сохраните их в текстовых файлах, формате ORC или Parquet.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="9d2e2-171">Настройте внешние объекты в хранилище данных SQL, определив расположение и формат данных.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span></span>
3. <span data-ttu-id="9d2e2-172">Выполните команду T-SQL для параллельной загрузки данных в новую таблицу баз данных.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-172">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<span data-ttu-id="9d2e2-173">Инструкции см. в статье [Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="9d2e2-174">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="9d2e2-174">Recommendations</span></span>
<span data-ttu-id="9d2e2-175">Многие из наших партнеров предлагают решения для загрузки.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="9d2e2-176">Дополнительные сведения см. в статье [Партнеры по бизнес-аналитике хранилища данных SQL][solution partners].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-176">To find out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="9d2e2-177">Если данные поступают из нереляционного источника и их необходимо загрузить в хранилище данных SQL, перед загрузкой их нужно преобразовать в строки и столбцы.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span></span> <span data-ttu-id="9d2e2-178">Преобразованные данные не обязательно должны храниться в базе данных, их можно хранить в текстовых файлах.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="9d2e2-179">Создание статистики для вновь загруженных данных</span><span class="sxs-lookup"><span data-stu-id="9d2e2-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="9d2e2-180">Чтобы добиться максимально высокой производительности запросов, крайне важно сформировать статистические данные для всех столбцов всех таблиц после первой загрузки или после любых значительных изменений в данных.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="9d2e2-181">Чтобы добиться максимально высокой производительности запросов, крайне важно сформировать статистические данные для всех столбцов всех таблиц после первой загрузки или после любых значительных изменений в данных.</span><span class="sxs-lookup"><span data-stu-id="9d2e2-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="9d2e2-182">Дополнительные сведения см. в статье [Управление статистикой таблиц в хранилище данных SQL][Statistics].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d2e2-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9d2e2-183">Next steps</span></span>
<span data-ttu-id="9d2e2-184">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="9d2e2-184">For more development tips, see the [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server to Azure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server to Azure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
