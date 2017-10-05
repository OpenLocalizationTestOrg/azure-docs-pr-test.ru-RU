---
title: "Загрузка терабайтов данных в хранилище данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: c29f1f01b660c4eb780e178a68036327fafa9ba6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="cb2d3-103">Загрузка 1 ТБ в хранилище данных SQL Azure с помощью фабрики данных менее чем за 15 минут</span><span class="sxs-lookup"><span data-stu-id="cb2d3-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="cb2d3-104">[Хранилище данных SQL Azure](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) — это развернутая в облаке база данных, способная обрабатывать большие объемы реляционных и нереляционных данных.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="cb2d3-105">Благодаря реализованной архитектуре вычислений с массовым параллелизмом (MPP) хранилище данных SQL оптимизировано для рабочих нагрузок хранилища корпоративных данных.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="cb2d3-106">Оно предоставляет эластичность облака и гибкие возможности масштабирования хранилища и вычислительной мощности независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="cb2d3-107">Приступить к работе с хранилищем данных SQL Azure теперь проще, чем когда-либо, с помощью **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="cb2d3-108">Фабрика данных Azure — это полностью управляемая облачная служба интеграции данных, которую можно использовать для заполнения хранилища данных SQL данными из существующей системы, экономя ценное время при оценке хранилища данных SQL и создании решений на основе его аналитики.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="cb2d3-109">Ниже приведены ключевые преимущества загрузки данных в хранилище данных SQL Azure с помощью фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-109">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="cb2d3-110">**Простота настройки**: вам доступен 5-этапный интуитивно понятный мастер без необходимости создавать сценарии.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-110">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="cb2d3-111">**Расширенная поддержка хранилищ данных**: встроенная поддержка обширного набора локальных и облачных хранилищ.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="cb2d3-112">**Безопасность и совместимость**: данные передаются по протоколу HTTPS или ExpressRoute, а наличие глобальной службы гарантирует, что ваши данные никогда не покинут заданных географических границ.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span></span>
* <span data-ttu-id="cb2d3-113">**Беспрецедентная производительность благодаря PolyBase**: применение Polybase является наиболее эффективным способом перемещения данных в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-113">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="cb2d3-114">Используя функцию промежуточных больших двоичных объектов, можно достичь высокой скорости загрузки данных из хранилищ всех типов, а не только из хранилища BLOB-объектов Azure, которое по умолчанию поддерживается Polybase.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-114">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span></span>

<span data-ttu-id="cb2d3-115">В этой статье показано, как использовать мастер копирования фабрики данных для загрузки 1 ТБ данных из хранилища BLOB-объектов Azure в хранилище данных SQL Azure менее чем за 15 минут с пропускной способностью более 1,2 Гбит/с.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-115">This article shows you how to use Data Factory Copy Wizard to load 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="cb2d3-116">Кроме того, статья содержит пошаговые инструкции по перемещению данных в хранилище данных SQL Azure с помощью мастера копирования.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="cb2d3-117">В статье [Перемещение данных в хранилище данных Azure SQL и из него с помощью фабрики данных Azure](data-factory-azure-sql-data-warehouse-connector.md) приведены общие сведения о возможностях фабрики данных по перемещению данных в хранилище данных SQL Azure и из него.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="cb2d3-118">Можно также создавать конвейеры с помощью портала Azure, Visual Studio PowerShell и т. д. Краткое пошаговое руководство с инструкциями по использованию действия копирования в фабрике данных Azure см. в статье [Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="cb2d3-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="cb2d3-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cb2d3-119">Prerequisites</span></span>
* <span data-ttu-id="cb2d3-120">Хранилище BLOB-объектов Azure: в этом эксперименте хранилище BLOB-объектов Azure (GRS) используется для хранения тестового набора данных TPC-H.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="cb2d3-121">Если у вас нет учетной записи хранения Azure, узнайте, как [создать учетную запись хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cb2d3-121">If you do not have an Azure storage account, learn [how to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="cb2d3-122">Данные [TPC-H](http://www.tpc.org/tpch/): в качестве тестового набора данных мы будем использовать TPC-H.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span></span>  <span data-ttu-id="cb2d3-123">Для этого необходимо использовать `dbgen` из набора средств TPC-H. Это поможет создать набор данных.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-123">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span></span>  <span data-ttu-id="cb2d3-124">Можно скачать исходный код `dbgen` из [инструментов TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) и скомпилировать его или скачать скомпилированный двоичный файл с сайта [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="cb2d3-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="cb2d3-125">Выполните dbgen.exe с приведенными ниже командами, чтобы создать неструктурированный файл размером в 1 ТБ для таблицы `lineitem`, распределенной на 10 файлов.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-125">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="cb2d3-126">…</span><span class="sxs-lookup"><span data-stu-id="cb2d3-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="cb2d3-127">Теперь скопируйте созданные файлы в большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-127">Now copy the generated files to Azure Blob.</span></span>  <span data-ttu-id="cb2d3-128">Ознакомьтесь с разделом [Перемещение данных в локальную файловую систему или из нее с помощью фабрики данных Azure](data-factory-onprem-file-system-connector.md), чтобы узнать, как это можно сделать с помощью фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-128">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span></span>    
* <span data-ttu-id="cb2d3-129">Хранилище данных SQL Azure: в ходе этого эксперимента данные загружаются в хранилище данных SQL Azure, созданное с 6000 DWU.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="cb2d3-130">В разделе [Создание хранилища данных SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) представлены подробные инструкции о том, как создать базу данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-130">Refer to [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span></span>  <span data-ttu-id="cb2d3-131">Чтобы обеспечить максимально возможную производительность загрузки в хранилище данных SQL с помощью Polybase, мы выбираем максимальное число единиц использования хранилища данных, допустимое для параметра производительности — 6000 DWU.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-131">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="cb2d3-132">Производительность загрузки из большого двоичного объекта Azure прямо пропорциональна количеству DWU, заданному для хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-132">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="cb2d3-133">Загрузка 1 ТБ в 1000 DWU хранилища данных SQL занимает 87 минут (при пропускной способности около 200 Мбит/с). Загрузка 1 ТБ в 2000 DWU хранилища данных SQL занимает 46 минут (при пропускной способности около 380 Мбит/с). Загрузка 1 ТБ в 6000 DWU хранилища данных SQL занимает 14 минут (при пропускной способности около 1,2 Гбит/с).</span><span class="sxs-lookup"><span data-stu-id="cb2d3-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="cb2d3-134">Чтобы создать хранилище данных SQL с 6000 DWU, сдвиньте ползунок "Производительность" вправо до конца.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-134">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span></span>

    ![Ползунок "Производительность"](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="cb2d3-136">В случае, если для существующей базы данных не настроено 6000 DWU, ее можно масштабировать с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="cb2d3-137">Перейдите к базе данных на портале Azure. На панели **Обзор** имеется кнопка **Масштаб**, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-137">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span></span>

    ![Кнопка "Масштаб"](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="cb2d3-139">Нажмите кнопку **Масштаб**, чтобы открыть приведенную ниже панель, передвиньте ползунок до максимального значения и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-139">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span></span>

    ![Диалоговое окно "Масштаб"](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="cb2d3-141">В этом эксперименте данные загружаются в хранилище данных SQL Azure с помощью класса ресурсов `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="cb2d3-142">Для получения наилучшей пропускной способности копирование нужно выполнить с помощью пользователя хранилища данных SQL, относящегося к классу ресурсов `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-142">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span></span>  <span data-ttu-id="cb2d3-143">Узнайте, как это сделать, ознакомившись с [примером изменения класса ресурсов пользователя](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="cb2d3-143">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="cb2d3-144">Создайте схему целевой таблицы в базе данных хранилища данных SQL Azure, выполнив следующую инструкцию DDL.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-144">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span></span>

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
<span data-ttu-id="cb2d3-145">Мы выполнили необходимые предварительные действия и готовы к настройке действия копирования с помощью мастера копирования.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-145">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="cb2d3-146">Запуск мастера копирования</span><span class="sxs-lookup"><span data-stu-id="cb2d3-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="cb2d3-147">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cb2d3-147">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cb2d3-148">Нажмите кнопку **+ Создать** в верхнем левом углу, выберите **Аналитика** и щелкните **Фабрика данных**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-148">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="cb2d3-149">В колонке **Создать фабрику данных** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-149">In the **New data factory** blade:</span></span>

   1. <span data-ttu-id="cb2d3-150">В поле **Имя** введите **LoadIntoSQLDWDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-150">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span></span>
       <span data-ttu-id="cb2d3-151">Имя фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-151">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="cb2d3-152">При возникновении ошибки **Имя фабрики данных LoadIntoSQLDWDataFactory недоступно** измените имя этой фабрики данных (например, на <ваше_имя>LoadIntoSQLDWDataFactory) и попробуйте создать ее снова.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-152">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="cb2d3-153">Ознакомьтесь с разделом [Фабрика данных — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="cb2d3-154">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="cb2d3-155">Для группы ресурсов выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-155">For Resource Group, do one of the following steps:</span></span>
      1. <span data-ttu-id="cb2d3-156">а) выберите **Использовать существующую** и укажите имеющуюся группу ресурсов;</span><span class="sxs-lookup"><span data-stu-id="cb2d3-156">Select **Use existing** to select an existing resource group.</span></span>
      2. <span data-ttu-id="cb2d3-157">выберите **Создать** и введите имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-157">Select **Create new** to enter a name for a resource group.</span></span>
   4. <span data-ttu-id="cb2d3-158">Укажите **расположение** фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-158">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="cb2d3-159">Установите флажок **Закрепить на панели мониторинга** в нижней части колонки.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-159">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="cb2d3-160">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-160">Click **Create**.</span></span>
4. <span data-ttu-id="cb2d3-161">После создания вы увидите колонку **Фабрика данных**, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-161">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>

   ![Домашняя страница фабрики данных](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="cb2d3-163">Чтобы запустить **мастер копирования**, на домашней странице фабрики данных щелкните **Копирование данных**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-163">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb2d3-164">Если веб-браузер завис на действии "Авторизация...", отключите параметр или снимите флажок **Block third party cookies and site data** (Блокировать сторонние файлы cookie и данные сайта). Либо оставьте флажок и создайте исключение для адреса **login.microsoftonline.com**, а затем попробуйте запустить мастер еще раз.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-164">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="cb2d3-165">Шаг 1. Настройка расписания загрузки данных</span><span class="sxs-lookup"><span data-stu-id="cb2d3-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="cb2d3-166">Первым шагом является настройка расписания загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-166">The first step is to configure the data loading schedule.</span></span>  

<span data-ttu-id="cb2d3-167">Вот что нужно сделать на странице **Свойства** :</span><span class="sxs-lookup"><span data-stu-id="cb2d3-167">In the **Properties** page:</span></span>

1. <span data-ttu-id="cb2d3-168">В качестве **имени задачи** введите **CopyFromBlobToAzureSqlDataWarehouse**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="cb2d3-169">Выберите параметр **Run once now** (Запустить сейчас один раз).</span><span class="sxs-lookup"><span data-stu-id="cb2d3-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="cb2d3-170">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-170">Click **Next**.</span></span>  

    ![Мастер копирования — страница "Свойства"](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="cb2d3-172">Шаг 2. Настройка источника</span><span class="sxs-lookup"><span data-stu-id="cb2d3-172">Step 2: Configure source</span></span>
<span data-ttu-id="cb2d3-173">В этом разделе описываются шаги для настройки источника: большого двоичного объекта Azure, содержащего файлы размером в 1 ТБ с элементами строк TPC-H.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-173">This section shows you the steps to configure the source: Azure Blob containing the 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="cb2d3-174">Выберите **хранилище BLOB-объектов Azure** в качестве хранилища и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-174">Select the **Azure Blob Storage** as the data store and click **Next**.</span></span>

    ![Мастер копирования — страница "Выбрать источник"](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="cb2d3-176">Укажите сведения о подключении для учетной записи хранения BLOB-объектов Azure и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-176">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span></span>

    ![Мастер копирования — сведения о подключении к источнику](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="cb2d3-178">Выберите **папку**, содержащую файлы с элементами строк TPC-H, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-178">Choose the **folder** containing the TPC-H line item files and click **Next**.</span></span>

    ![Мастер копирования — выбор папки входных данных](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="cb2d3-180">После нажатия кнопки **Далее** параметры формата файлов определяются автоматически.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-180">Upon clicking **Next**, the file format settings are detected automatically.</span></span>  <span data-ttu-id="cb2d3-181">Убедитесь, что разделителем столбцов является "|", а не запятая ",", используемая умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-181">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span></span>  <span data-ttu-id="cb2d3-182">Просмотрев данные, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-182">Click **Next** after you have previewed the data.</span></span>

    ![Мастер копирования — параметры формата файлов](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="cb2d3-184">Шаг 3. Настройка назначения</span><span class="sxs-lookup"><span data-stu-id="cb2d3-184">Step 3: Configure destination</span></span>
<span data-ttu-id="cb2d3-185">В этом разделе показано, как настроить назначение: таблицу `lineitem` в базе данных хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-185">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="cb2d3-186">Выберите **хранилище данных SQL Azure** в качестве назначения и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-186">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span></span>

    ![Мастер копирования — выбор целевого хранилища данных](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="cb2d3-188">Введите сведения о подключении для хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-188">Fill in the connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="cb2d3-189">Обязательно укажите пользователя, который является участником роли `xlargerc` (подробные инструкции приведены в разделе **предварительных требований**), и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-189">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Мастер копирования — сведения о подключении к целевому хранилищу](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="cb2d3-191">Выберите целевую таблицу и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-191">Choose the destination table and click **Next**.</span></span>

    ![Мастер копирования — страница сопоставления таблиц](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="cb2d3-193">На странице сопоставления схемы оставьте флажок "Apply column mapping" (Применить сопоставление столбцов) снятым и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="cb2d3-194">Шаг 4. Настройки производительности</span><span class="sxs-lookup"><span data-stu-id="cb2d3-194">Step 4: Performance settings</span></span>

<span data-ttu-id="cb2d3-195">Флажок **Allow polybase** (Разрешить использование PolyBase) установлен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="cb2d3-196">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-196">Click **Next**.</span></span>

![Мастер копирования — страница сопоставления столбцов](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="cb2d3-198">Шаг 5. Развертывание и мониторинг результатов нагрузки</span><span class="sxs-lookup"><span data-stu-id="cb2d3-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="cb2d3-199">Нажмите кнопку **Готово**, чтобы осуществить развертывание.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-199">Click **Finish** button to deploy.</span></span>

    ![Мастер копирования — страница сводки](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="cb2d3-201">После завершения развертывания щелкните `Click here to monitor copy pipeline`, чтобы отслеживать ход выполнения копирования.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-201">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span></span> <span data-ttu-id="cb2d3-202">Выберите конвейер копирования, созданный при работе со списком **Окна действий**.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-202">Select the copy pipeline you created in the **Activity Windows** list.</span></span>

    ![Мастер копирования — страница сводки](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="cb2d3-204">Можно просмотреть сведения о выполнении копирования в **Activity Window Explorer** в правой панели, в том числе объем данных, считанных из источника и записанных в назначение, продолжительность и среднюю пропускную способность копирования.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-204">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span></span>

    <span data-ttu-id="cb2d3-205">Как видно на следующем снимке экрана, копирование 1 ТБ из хранилища BLOB-объектов Azure в хранилище данных SQL занимает 14 минут, то есть фактическая пропускная способность составила 1,22 Гбит/с!</span><span class="sxs-lookup"><span data-stu-id="cb2d3-205">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Мастер копирования — диалоговое окно успешного выполнения](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="cb2d3-207">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="cb2d3-207">Best practices</span></span>
<span data-ttu-id="cb2d3-208">Ниже приведены некоторые советы и рекомендации по выполнению базы данных хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="cb2d3-209">При загрузке в кластеризованный индекс columnstore используйте класс ресурсов большего размера.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="cb2d3-210">Чтобы повысить эффективность соединений, рассмотрите возможность использования хэш-распределения по выбранному столбцу вместо используемого по умолчанию циклического распределения.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="cb2d3-211">Чтобы ускорить загрузку, рекомендуется использовать кучу для хранения временных данных.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="cb2d3-212">Сформируйте статистику после окончания загрузки хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="cb2d3-213">Дополнительные сведения см. в разделе [Рекомендации по использованию хранилища данных SQL Azure](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="cb2d3-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb2d3-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb2d3-214">Next steps</span></span>
* <span data-ttu-id="cb2d3-215">[Мастер копирования фабрики данных](data-factory-copy-wizard.md). В этой статье приведены сведения о мастере копирования.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span></span>
* <span data-ttu-id="cb2d3-216">[Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md). Эта статья содержит эталонные измерения производительности и руководство по настройке.</span><span class="sxs-lookup"><span data-stu-id="cb2d3-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span></span>
