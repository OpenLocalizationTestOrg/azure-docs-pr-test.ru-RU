---
title: "aaaLoad терабайт данных в хранилище данных SQL | Документы Microsoft"
description: "Демонстрируется загрузка 1 ТБ данных в хранилище данных SQL Azure с помощью фабрики данных Azure менее чем за 15 минут."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="c96dc-103">Загрузка 1 ТБ в хранилище данных SQL Azure с помощью фабрики данных менее чем за 15 минут</span><span class="sxs-lookup"><span data-stu-id="c96dc-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="c96dc-104">[Хранилище данных SQL Azure](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) — это развернутая в облаке база данных, способная обрабатывать большие объемы реляционных и нереляционных данных.</span><span class="sxs-lookup"><span data-stu-id="c96dc-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="c96dc-105">Благодаря реализованной архитектуре вычислений с массовым параллелизмом (MPP) хранилище данных SQL оптимизировано для рабочих нагрузок хранилища корпоративных данных.</span><span class="sxs-lookup"><span data-stu-id="c96dc-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="c96dc-106">Он предлагает облачных эластичности с хранилищем tooscale гибкость hello и вычислений независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="c96dc-106">It offers cloud elasticity with hello flexibility tooscale storage and compute independently.</span></span>

<span data-ttu-id="c96dc-107">Приступить к работе с хранилищем данных SQL Azure теперь проще, чем когда-либо, с помощью **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="c96dc-108">Фабрика данных Azure является полностью управляемая облачными данными интеграции службы, которая может быть toopopulate используется хранилище данных SQL с hello данных из существующей системы и сохранение вы ценное время при оценке хранилище данных SQL и построение аналитику решения.</span><span class="sxs-lookup"><span data-stu-id="c96dc-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used toopopulate a SQL Data Warehouse with hello data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="c96dc-109">Ниже приведены ключевые преимущества hello загрузки данных в хранилище данных SQL Azure, с помощью фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c96dc-109">Here are hello key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="c96dc-110">**Легко tooset копирование**: шаг 5 интуитивно понятный мастер с нет необходимости в сценариях.</span><span class="sxs-lookup"><span data-stu-id="c96dc-110">**Easy tooset up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="c96dc-111">**Расширенная поддержка хранилищ данных**: встроенная поддержка обширного набора локальных и облачных хранилищ.</span><span class="sxs-lookup"><span data-stu-id="c96dc-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="c96dc-112">**Безопасность и соответствие**: данные передаются по протоколу HTTPS или ExpressRoute и гарантирует наличие глобальной службы данных никогда не покидает hello географической границы</span><span class="sxs-lookup"><span data-stu-id="c96dc-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves hello geographical boundary</span></span>
* <span data-ttu-id="c96dc-113">**Несравненную производительности с помощью PolyBase** — с помощью Polybase — hello наиболее эффективный способ toomove данные в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c96dc-113">**Unparalleled performance by using PolyBase** – Using Polybase is hello most efficient way toomove data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="c96dc-114">Привет, промежуточного хранения больших двоичных этого можно добиться высокой нагрузки скорости из всех типов хранилищ данных, помимо хранения больших двоичных объектов Azure, которые hello Polybase поддерживает по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c96dc-114">Using hello staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which hello Polybase supports by default.</span></span>

<span data-ttu-id="c96dc-115">В этой статье показано, как toouse мастер копирования фабрики данных tooload 1 ТБ данных из хранилища больших двоичных объектов в хранилище данных SQL Azure в разделе 15 минут, в более 1,2 Гбит/с пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="c96dc-115">This article shows you how toouse Data Factory Copy Wizard tooload 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="c96dc-116">В этой статье содержит пошаговые инструкции по переносу данных в хранилище данных SQL Azure с помощью мастера копирования hello.</span><span class="sxs-lookup"><span data-stu-id="c96dc-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using hello Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="c96dc-117">Общие сведения о возможностях фабрики данных при перемещении данных в хранилище данных SQL Azure см. в разделе [перемещения tooand данные из хранилища данных SQL Azure, с помощью фабрики данных Azure](data-factory-azure-sql-data-warehouse-connector.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="c96dc-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="c96dc-118">Можно также создавать конвейеры с помощью портала Azure, Visual Studio PowerShell и т. д. В разделе [учебника: копирование данных из больших двоичных объектов Azure tooAzure базы данных SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) краткое Пошаговое руководство с пошаговыми инструкциями по использованию hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c96dc-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using hello Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="c96dc-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c96dc-119">Prerequisites</span></span>
* <span data-ttu-id="c96dc-120">Хранилище BLOB-объектов Azure: в этом эксперименте хранилище BLOB-объектов Azure (GRS) используется для хранения тестового набора данных TPC-H.</span><span class="sxs-lookup"><span data-stu-id="c96dc-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="c96dc-121">Если у вас учетная запись хранилища Azure, узнайте [как учетную запись хранения toocreate](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c96dc-121">If you do not have an Azure storage account, learn [how toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="c96dc-122">[TPC-H](http://www.tpc.org/tpch/) данных: мы будем toouse TPC-H как hello проверочного набора данных.</span><span class="sxs-lookup"><span data-stu-id="c96dc-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going toouse TPC-H as hello testing dataset.</span></span>  <span data-ttu-id="c96dc-123">потребуется toouse toodo `dbgen` из набора средств TPC-H, который поможет создать набор данных hello.</span><span class="sxs-lookup"><span data-stu-id="c96dc-123">toodo that, you need toouse `dbgen` from TPC-H toolkit, which helps you generate hello dataset.</span></span>  <span data-ttu-id="c96dc-124">Можно загрузить исходный код для `dbgen` из [средства TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) и скомпилируйте его самостоятельно, либо двоичный файл скомпилирован hello загрузки из [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="c96dc-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download hello compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="c96dc-125">Неструктурированный файл toogenerate 1 ТБ для команды выполнения dbgen.exe следующий hello `lineitem` таблицы разворота через 10 файлов:</span><span class="sxs-lookup"><span data-stu-id="c96dc-125">Run dbgen.exe with hello following commands toogenerate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="c96dc-126">…</span><span class="sxs-lookup"><span data-stu-id="c96dc-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="c96dc-127">Теперь hello копирования создается tooAzure файлов больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c96dc-127">Now copy hello generated files tooAzure Blob.</span></span>  <span data-ttu-id="c96dc-128">См. слишком[перемещение tooand данных из локальной файловой системы с помощью фабрики данных Azure](data-factory-onprem-file-system-connector.md) как toodo, с помощью копирования ADF.</span><span class="sxs-lookup"><span data-stu-id="c96dc-128">Refer too[Move data tooand from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how toodo that using ADF Copy.</span></span>    
* <span data-ttu-id="c96dc-129">Хранилище данных SQL Azure: в ходе этого эксперимента данные загружаются в хранилище данных SQL Azure, созданное с 6000 DWU.</span><span class="sxs-lookup"><span data-stu-id="c96dc-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="c96dc-130">См. слишком[создать хранилище данных SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) подробные инструкции о том, как toocreate хранилище данных SQL базы данных.</span><span class="sxs-lookup"><span data-stu-id="c96dc-130">Refer too[Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how toocreate a SQL Data Warehouse database.</span></span>  <span data-ttu-id="c96dc-131">tooget hello наилучшей возможную нагрузку производительности в хранилище данных SQL с помощью Polybase, мы выбираем максимальное число единиц хранилища данных (Dwu) допускается в производительности приветствия, являющийся 6000 Dwu.</span><span class="sxs-lookup"><span data-stu-id="c96dc-131">tooget hello best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in hello Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c96dc-132">При загрузке из больших двоичных объектов Azure, производительность загрузки данных hello — прямо пропорционально toohello количество Dwu настроить на hello хранилище данных SQL:</span><span class="sxs-lookup"><span data-stu-id="c96dc-132">When loading from Azure Blob, hello data loading performance is directly proportional toohello number of DWUs you configure on hello SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="c96dc-133">Загрузка 1 ТБ в 1000 DWU хранилища данных SQL занимает 87 минут (при пропускной способности около 200 Мбит/с). Загрузка 1 ТБ в 2000 DWU хранилища данных SQL занимает 46 минут (при пропускной способности около 380 Мбит/с). Загрузка 1 ТБ в 6000 DWU хранилища данных SQL занимает 14 минут (при пропускной способности около 1,2 Гбит/с).</span><span class="sxs-lookup"><span data-stu-id="c96dc-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="c96dc-134">Хранилище данных SQL с 6000 Dwu toocreate ползунок hello производительности всех toohello способом hello справа:</span><span class="sxs-lookup"><span data-stu-id="c96dc-134">toocreate a SQL Data Warehouse with 6,000 DWUs, move hello Performance slider all hello way toohello right:</span></span>

    ![Ползунок "Производительность"](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="c96dc-136">В случае, если для существующей базы данных не настроено 6000 DWU, ее можно масштабировать с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c96dc-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="c96dc-137">Перейдите toohello базы данных на портале Azure и **шкалы** кнопку в hello **Обзор** панели показано hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="c96dc-137">Navigate toohello database in Azure portal, and there is a **Scale** button in hello **Overview** panel shown in hello following image:</span></span>

    ![Кнопка "Масштаб"](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="c96dc-139">Нажмите кнопку hello **шкалы** следующие hello tooopen кнопку панели, переместите hello ползунок toohello максимальное значение и нажмите кнопку **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c96dc-139">Click hello **Scale** button tooopen hello following panel, move hello slider toohello maximum value, and click **Save** button.</span></span>

    ![Диалоговое окно "Масштаб"](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="c96dc-141">В этом эксперименте данные загружаются в хранилище данных SQL Azure с помощью класса ресурсов `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="c96dc-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="c96dc-142">tooachieve лучшие возможности пропускной способности копирования необходимо выполнить с помощью SQL хранилища данных пользователь, принадлежащий слишком toobe`xlargerc` класса ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c96dc-142">tooachieve best possible throughput, copy needs toobe performed using a SQL Data Warehouse user belonging too`xlargerc` resource class.</span></span>  <span data-ttu-id="c96dc-143">Узнайте, как toodo, выполнив следующие [измените пример класса ресурса для пользователя](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="c96dc-143">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="c96dc-144">Создание схемы целевой таблицы в базе данных хранилища данных SQL Azure, выполнив следующие инструкции DDL hello:</span><span class="sxs-lookup"><span data-stu-id="c96dc-144">Create destination table schema in Azure SQL Data Warehouse database, by running hello following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="c96dc-145">Обязательные шаги hello завершена мы становятся действие копирования hello готов tooconfigure, с помощью мастера копирования hello.</span><span class="sxs-lookup"><span data-stu-id="c96dc-145">With hello prerequisite steps completed, we are now ready tooconfigure hello copy activity using hello Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="c96dc-146">Запуск мастера копирования</span><span class="sxs-lookup"><span data-stu-id="c96dc-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="c96dc-147">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c96dc-147">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c96dc-148">Нажмите кнопку **+ создать** в левом верхнем углу hello, выберите **аналитики + аналитика**и нажмите кнопку **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-148">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="c96dc-149">В hello **новую фабрику данных** колонки:</span><span class="sxs-lookup"><span data-stu-id="c96dc-149">In hello **New data factory** blade:</span></span>

   1. <span data-ttu-id="c96dc-150">Введите **LoadIntoSQLDWDataFactory** для hello **имя**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-150">Enter **LoadIntoSQLDWDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="c96dc-151">Имя фабрики данных Azure hello Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="c96dc-151">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="c96dc-152">Если ошибка hello: **имя фабрики данных «LoadIntoSQLDWDataFactory» недоступен**, измените имя hello hello фабрики данных (например, yournameLoadIntoSQLDWDataFactory) и повторите попытку создания.</span><span class="sxs-lookup"><span data-stu-id="c96dc-152">If you receive hello error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change hello name of hello data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="c96dc-153">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c96dc-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="c96dc-154">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="c96dc-155">Для группы ресурсов выполните одно из действий hello.</span><span class="sxs-lookup"><span data-stu-id="c96dc-155">For Resource Group, do one of hello following steps:</span></span>
      1. <span data-ttu-id="c96dc-156">Выберите **использовать существующие** tooselect существующую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c96dc-156">Select **Use existing** tooselect an existing resource group.</span></span>
      2. <span data-ttu-id="c96dc-157">Выберите **создать новый** tooenter имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c96dc-157">Select **Create new** tooenter a name for a resource group.</span></span>
   4. <span data-ttu-id="c96dc-158">Выберите **расположение** для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="c96dc-158">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="c96dc-159">Выберите **toodashboard ПИН-код** флажок hello нижней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="c96dc-159">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="c96dc-160">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-160">Click **Create**.</span></span>
4. <span data-ttu-id="c96dc-161">После завершения создания hello, вы видите hello **фабрики данных** колонки, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="c96dc-161">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>

   ![Домашняя страница фабрики данных](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="c96dc-163">На домашней странице hello фабрики данных, нажмите кнопку hello **скопировать данные** плитки toolaunch **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-163">On hello Data Factory home page, click hello **Copy data** tile toolaunch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c96dc-164">При появлении этого веб-браузер hello застряла в «Авторизации...», отключить или снимите **блокировать сторонние файлы cookie и данным сайта** параметра (или) Оставьте включенным и создание исключения для **login.microsoftonline.com**, затем попытайтесь еще раз запустить мастер hello.</span><span class="sxs-lookup"><span data-stu-id="c96dc-164">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="c96dc-165">Шаг 1. Настройка расписания загрузки данных</span><span class="sxs-lookup"><span data-stu-id="c96dc-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="c96dc-166">Hello первым шагом является загрузка расписание tooconfigure hello данных.</span><span class="sxs-lookup"><span data-stu-id="c96dc-166">hello first step is tooconfigure hello data loading schedule.</span></span>  

<span data-ttu-id="c96dc-167">В hello **свойства** страницы:</span><span class="sxs-lookup"><span data-stu-id="c96dc-167">In hello **Properties** page:</span></span>

1. <span data-ttu-id="c96dc-168">В качестве **имени задачи** введите **CopyFromBlobToAzureSqlDataWarehouse**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="c96dc-169">Выберите параметр **Run once now** (Запустить сейчас один раз).</span><span class="sxs-lookup"><span data-stu-id="c96dc-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="c96dc-170">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-170">Click **Next**.</span></span>  

    ![Мастер копирования — страница "Свойства"](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="c96dc-172">Шаг 2. Настройка источника</span><span class="sxs-lookup"><span data-stu-id="c96dc-172">Step 2: Configure source</span></span>
<span data-ttu-id="c96dc-173">В этом разделе представлены hello действия tooconfigure hello источника: содержащий больших двоичных объектов Azure hello 1 ТБ TPC-H файлы элементов строки.</span><span class="sxs-lookup"><span data-stu-id="c96dc-173">This section shows you hello steps tooconfigure hello source: Azure Blob containing hello 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="c96dc-174">Выберите hello **хранилища больших двоичных объектов** как hello хранилище и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-174">Select hello **Azure Blob Storage** as hello data store and click **Next**.</span></span>

    ![Мастер копирования — страница "Выбрать источник"](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="c96dc-176">Заполните сведения о соединении hello для hello учетной записи хранилища больших двоичных объектов Azure и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-176">Fill in hello connection information for hello Azure Blob storage account, and click **Next**.</span></span>

    ![Мастер копирования — сведения о подключении к источнику](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="c96dc-178">Выберите hello **папки** содержащего строку hello TPC-H элемент файлы и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-178">Choose hello **folder** containing hello TPC-H line item files and click **Next**.</span></span>

    ![Мастер копирования — выбор папки входных данных](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="c96dc-180">После нажатия кнопки **Далее**, параметры формата файла hello обнаруживаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="c96dc-180">Upon clicking **Next**, hello file format settings are detected automatically.</span></span>  <span data-ttu-id="c96dc-181">Проверьте toomake убедиться, что разделителем столбцов является "| «вместо запятой по умолчанию hello»,".</span><span class="sxs-lookup"><span data-stu-id="c96dc-181">Check toomake sure that column delimiter is ‘|’ instead of hello default comma ‘,’.</span></span>  <span data-ttu-id="c96dc-182">Нажмите кнопку **Далее** после просмотрев hello данных.</span><span class="sxs-lookup"><span data-stu-id="c96dc-182">Click **Next** after you have previewed hello data.</span></span>

    ![Мастер копирования — параметры формата файлов](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="c96dc-184">Шаг 3. Настройка назначения</span><span class="sxs-lookup"><span data-stu-id="c96dc-184">Step 3: Configure destination</span></span>
<span data-ttu-id="c96dc-185">В этом разделе показано, как tooconfigure hello назначения: `lineitem` таблицы в базе данных хранилища данных SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c96dc-185">This section shows you how tooconfigure hello destination: `lineitem` table in hello Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="c96dc-186">Выберите **хранилище данных SQL Azure** как hello назначения хранилище и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-186">Choose **Azure SQL Data Warehouse** as hello destination store and click **Next**.</span></span>

    ![Мастер копирования — выбор целевого хранилища данных](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="c96dc-188">Заполните сведения о соединении hello для хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c96dc-188">Fill in hello connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="c96dc-189">Убедитесь, что указан hello пользователя, который является членом роли hello `xlargerc` (hello в разделе **необходимые компоненты** подробные инструкции в разделе) и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-189">Make sure you specify hello user that is a member of hello role `xlargerc` (see hello **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Мастер копирования — сведения о подключении к целевому хранилищу](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="c96dc-191">Выберите целевую таблицу hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-191">Choose hello destination table and click **Next**.</span></span>

    ![Мастер копирования — страница сопоставления таблиц](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="c96dc-193">На странице сопоставления схемы оставьте флажок "Apply column mapping" (Применить сопоставление столбцов) снятым и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="c96dc-194">Шаг 4. Настройки производительности</span><span class="sxs-lookup"><span data-stu-id="c96dc-194">Step 4: Performance settings</span></span>

<span data-ttu-id="c96dc-195">Флажок **Allow polybase** (Разрешить использование PolyBase) установлен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c96dc-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="c96dc-196">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c96dc-196">Click **Next**.</span></span>

![Мастер копирования — страница сопоставления столбцов](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="c96dc-198">Шаг 5. Развертывание и мониторинг результатов нагрузки</span><span class="sxs-lookup"><span data-stu-id="c96dc-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="c96dc-199">Нажмите кнопку **Готово** toodeploy кнопки.</span><span class="sxs-lookup"><span data-stu-id="c96dc-199">Click **Finish** button toodeploy.</span></span>

    ![Мастер копирования — страница сводки](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="c96dc-201">По завершении развертывания hello щелкните `Click here toomonitor copy pipeline` ход выполнения копирования hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="c96dc-201">After hello deployment is complete, click `Click here toomonitor copy pipeline` toomonitor hello copy run progress.</span></span> <span data-ttu-id="c96dc-202">Выберите hello копирования конвейера, созданный в hello **действия Windows** списка.</span><span class="sxs-lookup"><span data-stu-id="c96dc-202">Select hello copy pipeline you created in hello **Activity Windows** list.</span></span>

    ![Мастер копирования — страница сводки](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="c96dc-204">Можно просмотреть сведения о выполнении в hello копирования hello **действия окно обозревателя** hello правой панели, включая hello тома данных из источника для чтения и записи в назначения, продолжительность и hello Средняя пропускная способность для запуска hello.</span><span class="sxs-lookup"><span data-stu-id="c96dc-204">You can view hello copy run details in hello **Activity Window Explorer** in hello right panel, including hello data volume read from source and written into destination, duration, and hello average throughput for hello run.</span></span>

    <span data-ttu-id="c96dc-205">Как видно из hello следующий снимок экрана, копируя 1 ТБ из хранилища больших двоичных объектов в хранилище данных SQL занимает 14 минут, эффективно достижение 1,22 Гбит/с пропускной способности!</span><span class="sxs-lookup"><span data-stu-id="c96dc-205">As you can see from hello following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Мастер копирования — диалоговое окно успешного выполнения](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="c96dc-207">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="c96dc-207">Best practices</span></span>
<span data-ttu-id="c96dc-208">Ниже приведены некоторые советы и рекомендации по выполнению базы данных хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c96dc-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="c96dc-209">При загрузке в кластеризованный индекс columnstore используйте класс ресурсов большего размера.</span><span class="sxs-lookup"><span data-stu-id="c96dc-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="c96dc-210">Чтобы повысить эффективность соединений, рассмотрите возможность использования хэш-распределения по выбранному столбцу вместо используемого по умолчанию циклического распределения.</span><span class="sxs-lookup"><span data-stu-id="c96dc-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="c96dc-211">Чтобы ускорить загрузку, рекомендуется использовать кучу для хранения временных данных.</span><span class="sxs-lookup"><span data-stu-id="c96dc-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="c96dc-212">Сформируйте статистику после окончания загрузки хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c96dc-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="c96dc-213">Дополнительные сведения см. в разделе [Рекомендации по использованию хранилища данных SQL Azure](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="c96dc-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c96dc-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c96dc-214">Next steps</span></span>
* <span data-ttu-id="c96dc-215">[Мастер копирования фабрики данных](data-factory-copy-wizard.md) -Эта статья содержит сведения о приветствия мастера копирования.</span><span class="sxs-lookup"><span data-stu-id="c96dc-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about hello Copy Wizard.</span></span>
* <span data-ttu-id="c96dc-216">[Скопируйте действие производительности и руководство по настройке](data-factory-copy-activity-performance.md) -Эта статья содержит измерения производительности ссылка hello и руководство по настройке.</span><span class="sxs-lookup"><span data-stu-id="c96dc-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains hello reference performance measurements and tuning guide.</span></span>
