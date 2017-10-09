---
title: "aaaLoad данных в хранилище данных SQL Azure | Документы Microsoft"
description: "Узнайте hello распространенные сценарии загрузку данных в хранилище данных SQL. Они включают использование PolyBase, хранилища BLOB-объектов Azure, неструктурированных файлов и доставки диска. Кроме того, можно использовать сторонние средства."
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
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="14959-105">Загрузка данных в хранилище данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="14959-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="14959-106">Сводка параметров сценария hello и рекомендации для загрузки данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="14959-106">A summary of hello scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="14959-107">Hello сложнее всего загрузки данных обычно готовится данных hello hello нагрузки.</span><span class="sxs-lookup"><span data-stu-id="14959-107">hello hardest part of loading data is usually preparing hello data for hello load.</span></span> <span data-ttu-id="14959-108">Azure упрощает загрузку с помощью хранилища BLOB-объектов Azure как общее хранилище данных для многих служб hello и фабрики данных Azure с помощью перемещения tooorchestrate связью и обменом данными между hello служб Azure.</span><span class="sxs-lookup"><span data-stu-id="14959-108">Azure simplifies loading by using Azure blob storage as a common data store for many of hello services, and using Azure Data Factory tooorchestrate communication and data movement between hello Azure services.</span></span> <span data-ttu-id="14959-109">Эти процессы интегрированы с технологией PolyBase, которая использует расширенной параллельной обработки данных (MPP) tooload в параллельном режиме из хранилища BLOB-объектов Azure в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="14959-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) tooload data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="14959-110">Инструкции по загрузке образцов баз данных в хранилище данных SQL см. в [этой статье][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="14959-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="14959-111">Загрузка из хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="14959-111">Load from Azure blob storage</span></span>
<span data-ttu-id="14959-112">Hello самый быстрый способ tooimport данные в хранилище данных SQL — toouse PolyBase tooload данные из хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="14959-112">hello fastest way tooimport data into SQL Data Warehouse is toouse PolyBase tooload data from Azure blob storage.</span></span> <span data-ttu-id="14959-113">PolyBase использует хранилище данных SQL в расширенной параллельной обработки (MPP) разработки tooload данные в параллельном режиме из хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="14959-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design tooload data in parallel from Azure blob storage.</span></span> <span data-ttu-id="14959-114">toouse PolyBase, можно использовать команды T-SQL или конвейера фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="14959-114">toouse PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="14959-115">1. Использование PolyBase и T-SQL</span><span class="sxs-lookup"><span data-stu-id="14959-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="14959-116">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="14959-116">Summary of loading process:</span></span>

1. <span data-ttu-id="14959-117">Переместить в хранилище больших двоичных объектов tooAzure данных или хранилища Озера данных Azure и их сохранения в текстовых файлах.</span><span class="sxs-lookup"><span data-stu-id="14959-117">Move your data tooAzure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="14959-118">Настройка внешних объектов в хранилище данных SQL toodefine hello расположение и формат данных hello</span><span class="sxs-lookup"><span data-stu-id="14959-118">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data</span></span>
3. <span data-ttu-id="14959-119">Параллельное выполнение данных hello tooload команды T-SQL в новую таблицу базы данных.</span><span class="sxs-lookup"><span data-stu-id="14959-119">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="14959-120">См. в разделе [загрузки данных из хранилища BLOB-объектов Azure tooSQL хранилище данных (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="14959-120">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="14959-121">2. Использование фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="14959-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="14959-122">Для более простой способ toouse PolyBase можно создать конвейера фабрики данных Azure, использующей данные tooload PolyBase из хранилища BLOB-объектов Azure в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="14959-122">For a simpler way toouse PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase tooload data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="14959-123">Это быстрый tooconfigure, поскольку объекты T-SQL toodefine hello не требуется.</span><span class="sxs-lookup"><span data-stu-id="14959-123">This is fast tooconfigure since you don't need toodefine hello T-SQL objects.</span></span> <span data-ttu-id="14959-124">Если вам требуется tooquery hello внешних данных без их импорта, используйте T-SQL.</span><span class="sxs-lookup"><span data-stu-id="14959-124">If you need tooquery hello external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="14959-125">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="14959-125">Summary of loading process:</span></span>

1. <span data-ttu-id="14959-126">Переместить хранилище данных tooAzure BLOB-объектов и их сохранения в текстовых файлах.</span><span class="sxs-lookup"><span data-stu-id="14959-126">Move your data tooAzure blob storage and store it in text files.</span></span> <span data-ttu-id="14959-127">Сейчас фабрика данных Azure не поддерживает подключение к ADLS с использованием PolyBase.</span><span class="sxs-lookup"><span data-stu-id="14959-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="14959-128">Создайте данных hello tooingest конвейера фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="14959-128">Create an Azure Data Factory pipeline tooingest hello data.</span></span> <span data-ttu-id="14959-129">Используйте параметр PolyBase hello.</span><span class="sxs-lookup"><span data-stu-id="14959-129">Use hello PolyBase option.</span></span>
4. <span data-ttu-id="14959-130">Планирование и выполнение конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="14959-130">Schedule and run hello pipeline.</span></span>

<span data-ttu-id="14959-131">См. в разделе [загрузки данных из хранилища BLOB-объектов Azure tooSQL хранилище данных (фабрики данных Azure)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="14959-131">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="14959-132">Загрузка из SQL Server</span><span class="sxs-lookup"><span data-stu-id="14959-132">Load from SQL Server</span></span>
<span data-ttu-id="14959-133">tooload tooSQL SQL Server Integration Services (SSIS) можно использовать хранилище данных передачи плоских файлов или поставлен tooMicrosoft дисков.</span><span class="sxs-lookup"><span data-stu-id="14959-133">tooload data from SQL Server tooSQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks tooMicrosoft.</span></span> <span data-ttu-id="14959-134">Чтение toosee Сводка hello различных загрузке tootutorials процессы и ссылки.</span><span class="sxs-lookup"><span data-stu-id="14959-134">Read on toosee a summary of hello different loading processes and links tootutorials.</span></span>

<span data-ttu-id="14959-135">tooplan перехода полного набора данных с SQL Server tooSQL хранилища данных. в разделе hello [Общие сведения о миграции][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="14959-135">tooplan a full data migration from SQL Server tooSQL Data Warehouse, see hello [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="14959-136">Использование служб интеграции (SSIS)</span><span class="sxs-lookup"><span data-stu-id="14959-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="14959-137">Если вы уже используете tooload пакеты Integration Services (SSIS) в SQL Server, можно обновить toouse вашей пакетов SQL Server, как исходный hello и хранилище данных SQL в качестве назначения hello.</span><span class="sxs-lookup"><span data-stu-id="14959-137">If you are already using Integration Services (SSIS) packages tooload into SQL Server, you can update your packages toouse SQL Server as hello source and SQL Data Warehouse as hello destination.</span></span> <span data-ttu-id="14959-138">Это быстрый и простой toodo и является хорошим выбором, если вы не пытаетесь toomigrate вашей загрузки обработки данных toouse уже в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="14959-138">This is quick and easy toodo, and is a good choice if you are not trying toomigrate your loading process toouse data already in hello cloud.</span></span> <span data-ttu-id="14959-139">компромисс Hello является hello нагрузки будет работать медленнее, чем с помощью PolyBase, так как это служб SSIS не нагрузки hello параллельного выполнения.</span><span class="sxs-lookup"><span data-stu-id="14959-139">hello tradeoff is hello load will be slower than using PolyBase because this SSIS does not perform hello load in parallel.</span></span>

<span data-ttu-id="14959-140">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="14959-140">Summary of loading process:</span></span>

1. <span data-ttu-id="14959-141">Измените экземпляр службы интеграции пакета toopoint toohello SQL Server для hello источника и базы данных хранилища данных SQL hello для назначения hello.</span><span class="sxs-lookup"><span data-stu-id="14959-141">Revise your Integration Services package toopoint toohello SQL Server instance for hello source and hello SQL Data Warehouse database for hello destination.</span></span>
2. <span data-ttu-id="14959-142">Перенос вашей tooSQL схемы хранилища данных, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="14959-142">Migrate your schema tooSQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="14959-143">Изменить сопоставление hello в пакеты используют только hello типы данных, поддерживаемые хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="14959-143">Change hello mapping in your packages use only hello data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="14959-144">Планирование и запуск пакета hello.</span><span class="sxs-lookup"><span data-stu-id="14959-144">Schedule and run hello package.</span></span>

<span data-ttu-id="14959-145">См. в разделе [загрузки данных из SQL Server tooAzure хранилища данных SQL (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="14959-145">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="14959-146">Использование AZCopy (рекомендуется при объеме данных меньше 10 ТБ)</span><span class="sxs-lookup"><span data-stu-id="14959-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="14959-147">Если размер данных < 10 ТБ, можно экспортировать hello данные из файлов tooflat SQL Server, скопируйте хранилища больших двоичных объектов tooAzure hello файлы и затем использовать PolyBase tooload hello данных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="14959-147">If your data size is < 10 TB, you can export hello data from SQL Server tooflat files, copy hello files tooAzure blob storage, and then use PolyBase tooload hello data into SQL Data Warehouse</span></span>

<span data-ttu-id="14959-148">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="14959-148">Summary of loading process:</span></span>

1. <span data-ttu-id="14959-149">Используйте hello bcp программы командной строки tooexport данные из файлов tooflat SQL Server.</span><span class="sxs-lookup"><span data-stu-id="14959-149">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="14959-150">Используйте hello AZCopy программы командной строки toocopy данные из хранилища больших двоичных объектов tooAzure неструктурированных файлов.</span><span class="sxs-lookup"><span data-stu-id="14959-150">Use hello AZCopy command-line utility toocopy data from flat files tooAzure blob storage.</span></span>
3. <span data-ttu-id="14959-151">Используйте PolyBase tooload в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="14959-151">Use PolyBase tooload into SQL Data Warehouse.</span></span>

<span data-ttu-id="14959-152">См. в разделе [загрузки данных из хранилища BLOB-объектов Azure tooSQL хранилище данных (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="14959-152">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="14959-153">Использование программы bcp</span><span class="sxs-lookup"><span data-stu-id="14959-153">Use bcp</span></span>
<span data-ttu-id="14959-154">Если у вас есть небольшой объем данных bcp tooload можно использовать непосредственно в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="14959-154">If you have a small amount of data you can use bcp tooload directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="14959-155">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="14959-155">Summary of loading process:</span></span>

1. <span data-ttu-id="14959-156">Используйте hello bcp программы командной строки tooexport данные из файлов tooflat SQL Server.</span><span class="sxs-lookup"><span data-stu-id="14959-156">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="14959-157">Использовать bcp tooload данные из неструктурированных файлов непосредственно tooSQL хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="14959-157">Use bcp tooload data from flat files directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="14959-158">См. в разделе [загрузки данных из SQL Server tooAzure хранилище данных SQL (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="14959-158">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="14959-159">Использование импорта и экспорта (рекомендуется при объеме данных меньше 10 ТБ)</span><span class="sxs-lookup"><span data-stu-id="14959-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="14959-160">Если размер данных > 10 ТБ и предполагается toomove его tooAzure, мы рекомендуем использовать наши диска доставки службы [импорта и экспорта][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="14959-160">If your data size is > 10 TB and you want toomove it tooAzure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="14959-161">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="14959-161">Summary of loading process</span></span>

1. <span data-ttu-id="14959-162">Используйте hello bcp программы командной строки tooexport данные из файлов tooflat SQL Server на переносимые дисков.</span><span class="sxs-lookup"><span data-stu-id="14959-162">Use hello bcp command-line utility tooexport data from SQL Server tooflat files on transferrable disks.</span></span>
2. <span data-ttu-id="14959-163">Поставка tooMicrosoft диски hello.</span><span class="sxs-lookup"><span data-stu-id="14959-163">Ship hello disks tooMicrosoft.</span></span>
3. <span data-ttu-id="14959-164">Microsoft загружает hello данные в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="14959-164">Microsoft loads hello data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="14959-165">Загрузка из HDInsight</span><span class="sxs-lookup"><span data-stu-id="14959-165">Load from HDInsight</span></span>
<span data-ttu-id="14959-166">Хранилище данных SQL поддерживает загрузку данных из HDInsight через PolyBase.</span><span class="sxs-lookup"><span data-stu-id="14959-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="14959-167">процесс Hello hello такой же, как загрузка данных из хранилища больших двоичных объектов — с помощью PolyBase tooconnect tooHDInsight tooload данных.</span><span class="sxs-lookup"><span data-stu-id="14959-167">hello process is hello same as loading data from Azure Blob Storage - using PolyBase tooconnect tooHDInsight tooload data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="14959-168">1. Использование PolyBase и T-SQL</span><span class="sxs-lookup"><span data-stu-id="14959-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="14959-169">Процесс загрузки:</span><span class="sxs-lookup"><span data-stu-id="14959-169">Summary of loading process:</span></span>

1. <span data-ttu-id="14959-170">Перемещение вашей tooHDInsight данных и сохранить ее в текстовых файлах, формат ORC или Parquet.</span><span class="sxs-lookup"><span data-stu-id="14959-170">Move your data tooHDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="14959-171">Настройка внешних объектов в хранилище данных SQL toodefine hello расположение и формат данных hello.</span><span class="sxs-lookup"><span data-stu-id="14959-171">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data.</span></span>
3. <span data-ttu-id="14959-172">Параллельное выполнение данных hello tooload команды T-SQL в новую таблицу базы данных.</span><span class="sxs-lookup"><span data-stu-id="14959-172">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<span data-ttu-id="14959-173">См. в разделе [загрузки данных из хранилища BLOB-объектов Azure tooSQL хранилище данных (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="14959-173">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="14959-174">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="14959-174">Recommendations</span></span>
<span data-ttu-id="14959-175">Многие из наших партнеров предлагают решения для загрузки.</span><span class="sxs-lookup"><span data-stu-id="14959-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="14959-176">toofind подробные сведения, см. список наших [решения партнеров][solution partners].</span><span class="sxs-lookup"><span data-stu-id="14959-176">toofind out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="14959-177">Если будут поступать данные из источника нереляционных tooload его в данных SQL в хранилище вам потребуется tootransform его в виде строк и столбцов перед их загрузкой.</span><span class="sxs-lookup"><span data-stu-id="14959-177">If your data is coming from a non-relational source and you want tooload it into SQL Data Warehouse you will need tootransform it into rows and columns before you load it.</span></span> <span data-ttu-id="14959-178">Hello преобразования данных не должны toobe в базе данных, могут храниться в текстовых файлах.</span><span class="sxs-lookup"><span data-stu-id="14959-178">hello transformed data doesn't need toobe stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="14959-179">Создание статистики для вновь загруженных данных</span><span class="sxs-lookup"><span data-stu-id="14959-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="14959-180">Хранилище данных SQL Azure пока не поддерживает автоматическое создание или автоматическое обновление статистики.</span><span class="sxs-lookup"><span data-stu-id="14959-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="14959-181">В порядке tooget hello наилучшей производительности запросов очень важно сначала загрузите toocreate статистику для всех столбцов всех таблиц после hello или любые существенные изменения происходят в данных hello.</span><span class="sxs-lookup"><span data-stu-id="14959-181">In order tooget hello best performance from your queries, it's important toocreate statistics on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="14959-182">Дополнительные сведения см. в статье [Управление статистикой таблиц в хранилище данных SQL][Statistics].</span><span class="sxs-lookup"><span data-stu-id="14959-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="14959-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="14959-183">Next steps</span></span>
<span data-ttu-id="14959-184">Дополнительные советы по разработке в разделе hello [Общие сведения о разработке][development overview].</span><span class="sxs-lookup"><span data-stu-id="14959-184">For more development tips, see hello [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
