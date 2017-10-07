---
title: "aaaSQL действия хранимой процедуры сервера"
description: "Дополнительные сведения об использовании tooinvoke действия хранимой процедуры SQL Server hello хранимой процедуры в базе данных SQL Azure или хранилище данных SQL Azure из конвейера фабрики данных."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="cf4ff-103">Действие "Хранимая процедура SQL Server"</span><span class="sxs-lookup"><span data-stu-id="cf4ff-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="cf4ff-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="cf4ff-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="cf4ff-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="cf4ff-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="cf4ff-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="cf4ff-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="cf4ff-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="cf4ff-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="cf4ff-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="cf4ff-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="cf4ff-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="cf4ff-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="cf4ff-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="cf4ff-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="cf4ff-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="cf4ff-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="cf4ff-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cf4ff-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="cf4ff-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="cf4ff-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="cf4ff-114">Обзор</span><span class="sxs-lookup"><span data-stu-id="cf4ff-114">Overview</span></span>
<span data-ttu-id="cf4ff-115">Используйте действия преобразования данных в фабрике данных [конвейера](data-factory-create-pipelines.md) tootransform и процесс необработанные данные в прогнозы и аналитики.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) tootransform and process raw data into predictions and insights.</span></span> <span data-ttu-id="cf4ff-116">Hello действия хранимой процедуры — одно из действий hello преобразования, которые поддерживает фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-116">hello Stored Procedure Activity is one of hello transformation activities that Data Factory supports.</span></span> <span data-ttu-id="cf4ff-117">Эта статья основана на hello [действия преобразования данных](data-factory-data-transformation-activities.md) статьи, в котором предоставляются общие сведения о преобразования данных и hello поддерживается преобразование действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="cf4ff-118">Можно использовать tooinvoke действия хранимой процедуры hello хранимой процедуры в одном hello следующие данные хранятся в вашей организации или на виртуальной машине Azure (ВМ):</span><span class="sxs-lookup"><span data-stu-id="cf4ff-118">You can use hello Stored Procedure Activity tooinvoke a stored procedure in one of hello following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="cf4ff-119">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cf4ff-119">Azure SQL Database</span></span>
- <span data-ttu-id="cf4ff-120">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cf4ff-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="cf4ff-121">База данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-121">SQL Server Database.</span></span>  <span data-ttu-id="cf4ff-122">Если вы используете SQL Server, установите шлюз управления данными на приветствия же компьютер, что узлы hello базы данных или на отдельном компьютере, который имеет доступ к базе данных toohello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-122">If you are using SQL Server, install Data Management Gateway on hello same machine that hosts hello database or on a separate machine that has access toohello database.</span></span> <span data-ttu-id="cf4ff-123">Шлюз управления данными — это компонент, который обеспечивает безопасное и управляемое подключение локальных источников данных или данных виртуальной машины Azure к облачным службам.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="cf4ff-124">Дополнительные сведения см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf4ff-125">При копировании данных в базе данных SQL Azure или SQL Server, можно настроить hello **SqlSink** в tooinvoke действия копирования хранимой процедуры с помощью hello **sqlWriterStoredProcedureName** свойство.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-125">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="cf4ff-126">Дополнительные сведения см. в статье [Вызов хранимой процедуры из действия копирования в фабрике данных Azure](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="cf4ff-127">Дополнительные сведения о свойстве hello см. следующие статьи соединителя: [базы данных SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-127">For details about hello property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="cf4ff-128">Вызов хранимой процедуры во время копирования данных в хранилище данных SQL Azure с помощью операции копирования не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="cf4ff-129">Однако можно использовать tooinvoke действие hello хранимой процедуры хранимой процедуры в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-129">But, you can use hello stored procedure activity tooinvoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="cf4ff-130">При копировании данных из базы данных SQL Azure или SQL Server или хранилище данных SQL Azure, можно настроить **SqlSource** в tooinvoke действия копирования данных tooread хранимой процедуры из базы данных-источника hello с помощью hello  **sqlReaderStoredProcedureName** свойство.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="cf4ff-131">Дополнительные сведения см. следующие статьи соединителя hello: [базы данных SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="cf4ff-131">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="cf4ff-132">Пошаговое руководство использует следующие Hello hello действия хранимой процедуры в конвейер tooinvoke хранимую процедуру в базе данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-132">hello following walkthrough uses hello Stored Procedure Activity in a pipeline tooinvoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="cf4ff-133">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="cf4ff-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="cf4ff-134">Образец таблицы и хранимая процедура</span><span class="sxs-lookup"><span data-stu-id="cf4ff-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="cf4ff-135">Создайте ниже hello **таблицы** в базе данных SQL Azure с помощью SQL Server Management Studio или любой другой инструмент, вы знакомы с.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-135">Create hello following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="cf4ff-136">столбец datetimestamp Hello является hello даты и времени, когда создается соответствующий идентификатор hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-136">hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="cf4ff-137">Идентификатор hello уникальный идентифицировать а hello datetimestamp очередь hello даты и времени, когда создается соответствующий идентификатор hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-137">Id is hello unique identified and hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>
    
    ![Пример данных](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="cf4ff-139">В этом образце hello хранимой процедуры находится в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-139">In this sample, hello stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="cf4ff-140">Если hello хранимая процедура находится в хранилище данных SQL Azure и базы данных SQL Server, hello подход аналогичен.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-140">If hello stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, hello approach is similar.</span></span> <span data-ttu-id="cf4ff-141">В случае с базой данных SQL Server необходимо установить [шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="cf4ff-142">Создайте ниже hello **хранимой процедуры** , вставляет данные в toohello **образец таблицы**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-142">Create hello following **stored procedure** that inserts data in toohello **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="cf4ff-143">**Имя** и **регистр** hello параметра (Дата и время в этом примере) должно совпадать, параметр, указанный в JSON конвейера hello и действия.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-143">**Name** and **casing** of hello parameter (DateTime in this example) must match that of parameter specified in hello pipeline/activity JSON.</span></span> <span data-ttu-id="cf4ff-144">В hello определение хранимой процедуры, убедитесь, что  **@**  используется в качестве префикса для параметра hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-144">In hello stored procedure definition, ensure that **@** is used as a prefix for hello parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="cf4ff-145">Создать фабрику данных</span><span class="sxs-lookup"><span data-stu-id="cf4ff-145">Create a data factory</span></span>
1. <span data-ttu-id="cf4ff-146">Войдите в слишком[портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-146">Log in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cf4ff-147">Нажмите кнопку **NEW** hello левого меню **аналитики + аналитика**и нажмите кнопку **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-147">Click **NEW** on hello left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Новая фабрика данных](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="cf4ff-149">В hello **новую фабрику данных** колонке введите **SProcDF** для hello имя.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-149">In hello **New data factory** blade, enter **SProcDF** for hello Name.</span></span> <span data-ttu-id="cf4ff-150">Имена фабрики данных Azure являются **глобально уникальными**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="cf4ff-151">Требуется имя hello tooprefix hello фабрики данных с вашим именем tooenable hello успешного создания фабрики hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-151">You need tooprefix hello name of hello data factory with your name, tooenable hello successful creation of hello factory.</span></span>

   ![Новая фабрика данных](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="cf4ff-153">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="cf4ff-154">Для **группы ресурсов**, выполните одно из hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="cf4ff-154">For **Resource Group**, do one of hello following steps:</span></span>
   1. <span data-ttu-id="cf4ff-155">Нажмите кнопку **создать новый** и введите имя для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-155">Click **Create new** and enter a name for hello resource group.</span></span>
   2. <span data-ttu-id="cf4ff-156">Щелкните **Использовать существующий** и укажите имеющуюся группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="cf4ff-157">Выберите hello **расположение** для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-157">Select hello **location** for hello data factory.</span></span>
7. <span data-ttu-id="cf4ff-158">Выберите **toodashboard ПИН-код** , чтобы увидеть hello фабрики данных на панели мониторинга hello следующем входе в систему.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-158">Select **Pin toodashboard** so that you can see hello data factory on hello dashboard next time you log in.</span></span>
8. <span data-ttu-id="cf4ff-159">Нажмите кнопку **создать** на hello **новую фабрику данных** колонку.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-159">Click **Create** on hello **New data factory** blade.</span></span>
9. <span data-ttu-id="cf4ff-160">Вы видите hello фабрики данных, создаваемого в hello **мониторинга** из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-160">You see hello data factory being created in hello **dashboard** of hello Azure portal.</span></span> <span data-ttu-id="cf4ff-161">После успешного создания фабрики данных hello, отображается страница фабрики данных hello, в котором отображается содержимое фабрики данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-161">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![Домашняя страница фабрики данных](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="cf4ff-163">Создание связанной службы SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cf4ff-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="cf4ff-164">После создания фабрики данных hello, создайте связанной службой SQL Azure, связывающий базы данных Azure SQL, содержащий таблицу hello образец таблицы и sp_sample хранимые процедуры, tooyour фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-164">After creating hello data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains hello sampletable table and sp_sample stored procedure, tooyour data factory.</span></span>

1. <span data-ttu-id="cf4ff-165">Нажмите кнопку **автор и развернуть** на hello **фабрики данных** колонке **SProcDF** toolaunch hello редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-165">Click **Author and deploy** on hello **Data Factory** blade for **SProcDF** toolaunch hello Data Factory Editor.</span></span>
2. <span data-ttu-id="cf4ff-166">Нажмите кнопку **новое хранилище данных** hello панели команд и выберите **базы данных SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-166">Click **New data store** on hello command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="cf4ff-167">Вы увидите hello скрипта JSON для создания Azure SQL связанные службы в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-167">You should see hello JSON script for creating an Azure SQL linked service in hello editor.</span></span>

   ![Новое хранилище данных](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="cf4ff-169">Убедитесь в hello скрипта JSON, hello следующие отличия.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-169">In hello JSON script, make hello following changes:</span></span>

   1. <span data-ttu-id="cf4ff-170">Замените `<servername>` с именем hello сервера базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-170">Replace `<servername>` with hello name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="cf4ff-171">Замените `<databasename>` с hello базы данных, в которой создана таблица hello и hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-171">Replace `<databasename>` with hello database in which you created hello table and hello stored procedure.</span></span>
   3. <span data-ttu-id="cf4ff-172">Замените `<username@servername>` с hello учетной записи пользователя, который имеет доступ к базе данных toohello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-172">Replace `<username@servername>` with hello user account that has access toohello database.</span></span>
   4. <span data-ttu-id="cf4ff-173">Замените `<password>` hello пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-173">Replace `<password>` with hello password for hello user account.</span></span>

      ![Новое хранилище данных](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="cf4ff-175">toodeploy Здравствуйте связанной службы, нажмите кнопку **развернуть** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-175">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="cf4ff-176">Подтвердите, что вы видите hello AzureSqlLinkedService hello дерева просмотра слева hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-176">Confirm that you see hello AzureSqlLinkedService in hello tree view on hello left.</span></span>

    ![иерархическое представление со связанными службами](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="cf4ff-178">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="cf4ff-178">Create an output dataset</span></span>
<span data-ttu-id="cf4ff-179">Необходимо указать выходной набор данных для действия "хранимая процедура" даже если hello хранимой процедуры не создаются все данные.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-179">You must specify an output dataset for a stored procedure activity even if hello stored procedure does not produce any data.</span></span> <span data-ttu-id="cf4ff-180">Это, так как его hello выходной набор данных, который управляет расписанием hello hello действия (частоту hello действие выполняется - ежечасно, ежедневно, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-180">That's because it's hello output dataset that drives hello schedule of hello activity (how often hello activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="cf4ff-181">Hello выходной набор данных необходимо использовать **связанная служба** , обозначающий tooan базы данных SQL Azure или хранилище данных SQL Azure или базе SQL Server, в котором нужно hello toorun хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-181">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="cf4ff-182">Hello выходной набор данных может служить результат hello toopass способом hello хранимые процедуры для последующей обработки другим действием ([цепочки действий](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-182">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="cf4ff-183">Однако фабрики данных вывода автоматически hello объекта dataset toothis хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-183">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="cf4ff-184">Это hello хранимая процедура записи таблицы tooa SQL, который hello указывает выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-184">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="cf4ff-185">В некоторых случаях может быть выходной набор данных hello **пустой набор данных** (набор данных, указывающий tooa таблицу, которая не удерживает действительно hello выходные данные хранимой процедуры).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-185">In some cases, hello output dataset can be a **dummy dataset** (a dataset that points tooa table that does not really hold output of hello stored procedure).</span></span> <span data-ttu-id="cf4ff-186">Этот пустой набор данных используется только для hello расписание hello toospecify действие хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-186">This dummy dataset is used only toospecify hello schedule for running hello stored procedure activity.</span></span> 

1. <span data-ttu-id="cf4ff-187">Нажмите **... Дополнительные** на hello инструментов щелкните **новый набор данных**и нажмите кнопку **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-187">Click **... More** on hello toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="cf4ff-188">**Новый набор данных** панели и выберите команду hello **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-188">**New dataset** on hello command bar and select **Azure SQL**.</span></span>

    ![иерархическое представление со связанными службами](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="cf4ff-190">Скопируйте и вставьте следующий скрипт JSON в редакторе JSON toohello hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-190">Copy/paste hello following JSON script in toohello JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="cf4ff-191">toodeploy Здравствуйте набора данных, нажмите кнопку **развернуть** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-191">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="cf4ff-192">Подтвердите, что вы видите hello набора данных в древовидном представлении hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-192">Confirm that you see hello dataset in hello tree view.</span></span>

    ![иерархическое представление со связанными службами](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="cf4ff-194">Создание конвейера с помощью действия SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="cf4ff-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="cf4ff-195">Теперь создадим конвейер с помощью действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="cf4ff-196">Обратите внимание, hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="cf4ff-196">Notice hello following properties:</span></span> 

- <span data-ttu-id="cf4ff-197">Hello **тип** задано слишком**SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-197">hello **type** property is set too**SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="cf4ff-198">Hello **storedProcedureName** в тип свойства заданы слишком**sp_sample** (имя hello хранимой процедуры).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-198">hello **storedProcedureName** in type properties is set too**sp_sample** (name of hello stored procedure).</span></span>
- <span data-ttu-id="cf4ff-199">Hello **storedProcedureParameters** раздел содержит один параметр с именем **DataTime**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-199">hello **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="cf4ff-200">Имя и регистра параметра hello в JSON должны совпадать с именем hello и регистр hello параметра в определении hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-200">Name and casing of hello parameter in JSON must match hello name and casing of hello parameter in hello stored procedure definition.</span></span> <span data-ttu-id="cf4ff-201">Если требуется передать значение null для параметра, используйте синтаксис hello: `"param1": null` (прописными буквами).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-201">If you need pass null for a parameter, use hello syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="cf4ff-202">Нажмите **... Дополнительные** hello панели команд и нажмите кнопку **новый конвейер**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-202">Click **... More** on hello command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="cf4ff-203">Скопируйте и вставьте следующий фрагмент JSON hello:</span><span class="sxs-lookup"><span data-stu-id="cf4ff-203">Copy/paste hello following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="cf4ff-204">toodeploy hello конвейера, нажмите кнопку **развернуть** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-204">toodeploy hello pipeline, click **Deploy** on hello toolbar.</span></span>  

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="cf4ff-205">Монитор hello конвейера</span><span class="sxs-lookup"><span data-stu-id="cf4ff-205">Monitor hello pipeline</span></span>
1. <span data-ttu-id="cf4ff-206">Нажмите кнопку **X** tooclose редактор фабрики данных колонках toonavigate резервное колонке toohello фабрики данных и нажмите кнопку **схема**.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-206">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![плитка "Схема"](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="cf4ff-208">В hello **представление диаграммы**, просмотреть обзор конвейеров hello и использовать наборы данных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-208">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![плитка "Схема"](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="cf4ff-210">В hello представление диаграммы, дважды щелкните набор данных hello `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-210">In hello Diagram View, double-click hello dataset `sprocsampleout`.</span></span> <span data-ttu-id="cf4ff-211">Вы увидите hello срезов в состоянии готовности.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-211">You see hello slices in Ready state.</span></span> <span data-ttu-id="cf4ff-212">Поскольку срезов каждый час между hello время начала и время окончания из hello JSON должно быть пять срезов.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-212">There should be five slices because a slice is produced for each hour between hello start time and end time from hello JSON.</span></span>

    ![плитка "Схема"](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="cf4ff-214">Если срез находится в **готовности** состояние, запустите `select * from sampletable` запрос к tooverify базы данных Azure SQL hello, hello данных была вставлена в таблицу toohello hello хранимой процедурой.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-214">When a slice is in **Ready** state, run a `select * from sampletable` query against hello Azure SQL database tooverify that hello data was inserted in toohello table by hello stored procedure.</span></span>

   ![Выходные данные](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="cf4ff-216">В разделе [конвейера hello монитор](data-factory-monitor-manage-pipelines.md) подробные сведения о мониторинге конвейеров фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-216">See [Monitor hello pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="cf4ff-217">Указание набора входных данных</span><span class="sxs-lookup"><span data-stu-id="cf4ff-217">Specify an input dataset</span></span>
<span data-ttu-id="cf4ff-218">В пошаговом руководстве hello действия хранимой процедуры нет любой входных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-218">In hello walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="cf4ff-219">При указании входного набора данных, hello действие хранимой процедуры не запускается до hello фрагмент из набора входных данных доступен (в состоянии готовности).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-219">If you specify an input dataset, hello stored procedure activity does not run until hello slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="cf4ff-220">Hello набором данных может быть внешнего набора данных (не был создан другим действием hello же конвейера) или внутренний набор данных, данным, созданным вышестоящего действие (действие hello, который выполняется перед этим действием).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-220">hello dataset can be an external dataset (that is not produced by another activity in hello same pipeline) or an internal dataset that is produced by an upstream activity (hello activity that runs before this activity).</span></span> <span data-ttu-id="cf4ff-221">Можно указать несколько входных наборов данных для действия hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-221">You can specify multiple input datasets for hello stored procedure activity.</span></span> <span data-ttu-id="cf4ff-222">Если сделать это, hello действие хранимой процедуры выполняется только в том случае, если доступны все срезы hello входного набора данных (в состоянии готовности).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-222">If you do so, hello stored procedure activity runs only when all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="cf4ff-223">Hello входного набора данных не может использоваться в hello хранимой процедуре как параметр.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-223">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="cf4ff-224">Это только используемые toocheck hello зависимостей, до начала hello действие хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-224">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="cf4ff-225">Объединение с другими действиями</span><span class="sxs-lookup"><span data-stu-id="cf4ff-225">Chaining with other activities</span></span>
<span data-ttu-id="cf4ff-226">Toochain восходящего действия с этим действием, укажите выходные данные hello восходящего действия hello, входным этого действия.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-226">If you want toochain an upstream activity with this activity, specify hello output of hello upstream activity as an input of this activity.</span></span> <span data-ttu-id="cf4ff-227">При этом hello действие хранимой процедуры не выполняется до завершения действия вышестоящего hello и hello выходного набора данных hello восходящего действия доступен (в состоянии готовности).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-227">When you do so, hello stored procedure activity does not run until hello upstream activity completes and hello output dataset of hello upstream activity is available (in Ready status).</span></span> <span data-ttu-id="cf4ff-228">Выходные наборы данных из нескольких действий вышестоящего можно указать в качестве входных наборов данных действия hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-228">You can specify output datasets of multiple upstream activities as input datasets of hello stored procedure activity.</span></span> <span data-ttu-id="cf4ff-229">После этого hello действие хранимой процедуры выполняется только в том случае, когда доступны все срезы hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-229">When you do so, hello stored procedure activity runs only when all hello input dataset slices are available.</span></span>  

<span data-ttu-id="cf4ff-230">В следующем примере hello, является hello выходным результатом действия копирования hello: OutputDataset, который является входным hello действие хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-230">In hello following example, hello output of hello copy activity is: OutputDataset, which is an input of hello stored procedure activity.</span></span> <span data-ttu-id="cf4ff-231">Таким образом hello действие хранимой процедуры не выполняется до завершения действия копирования hello и hello OutputDataset фрагмент доступен (в состоянии готовности).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-231">Therefore, hello stored procedure activity does not run until hello copy activity completes and hello OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="cf4ff-232">При указании нескольких входных наборов данных hello действие хранимой процедуры не запускается до доступны все срезы hello входного набора данных (в состоянии готовности).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-232">If you specify multiple input datasets, hello stored procedure activity does not run until all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="cf4ff-233">Hello входных наборов данных не может использоваться непосредственно в виде параметров toohello хранимой процедуры действия.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-233">hello input datasets cannot be used directly as parameters toohello stored procedure activity.</span></span> 

<span data-ttu-id="cf4ff-234">Дополнительные сведения о цепочках действий см. в разделе [Несколько действий в конвейере](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="cf4ff-235">Аналогичным образом toolink hello магазина действия процедуры с **нисходящие действия** (hello действия, выполняющие после hello хранимая процедура завершения действия), укажите hello выходного набора данных действие hello хранимой процедуры как входные данные hello нисходящие действия в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-235">Similarly, toolink hello store procedure activity with **downstream activities** (hello activities that run after hello stored procedure activity completes), specify hello output dataset of hello stored procedure activity as an input of hello downstream activity in hello pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf4ff-236">При копировании данных в базе данных SQL Azure или SQL Server, можно настроить hello **SqlSink** в tooinvoke действия копирования хранимой процедуры с помощью hello **sqlWriterStoredProcedureName** свойство.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-236">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="cf4ff-237">Дополнительные сведения см. в статье [Вызов хранимой процедуры из действия копирования в фабрике данных Azure](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="cf4ff-238">Дополнительные сведения о свойстве hello см. следующие статьи соединителя hello: [базы данных SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-238">For details about hello property, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="cf4ff-239">При копировании данных из базы данных SQL Azure или SQL Server или хранилище данных SQL Azure, можно настроить **SqlSource** в tooinvoke действия копирования данных tooread хранимой процедуры из базы данных-источника hello с помощью hello  **sqlReaderStoredProcedureName** свойство.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="cf4ff-240">Дополнительные сведения см. следующие статьи соединителя hello: [базы данных SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="cf4ff-240">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="cf4ff-241">Формат JSON</span><span class="sxs-lookup"><span data-stu-id="cf4ff-241">JSON format</span></span>
<span data-ttu-id="cf4ff-242">Вот hello формат JSON для определения действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-242">Here is hello JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="cf4ff-243">Привет, в следующей таблице описываются эти свойства JSON:</span><span class="sxs-lookup"><span data-stu-id="cf4ff-243">hello following table describes these JSON properties:</span></span>

| <span data-ttu-id="cf4ff-244">Свойство</span><span class="sxs-lookup"><span data-stu-id="cf4ff-244">Property</span></span> | <span data-ttu-id="cf4ff-245">Описание</span><span class="sxs-lookup"><span data-stu-id="cf4ff-245">Description</span></span> | <span data-ttu-id="cf4ff-246">Обязательно</span><span class="sxs-lookup"><span data-stu-id="cf4ff-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf4ff-247">name</span><span class="sxs-lookup"><span data-stu-id="cf4ff-247">name</span></span> | <span data-ttu-id="cf4ff-248">Имя действия hello</span><span class="sxs-lookup"><span data-stu-id="cf4ff-248">Name of hello activity</span></span> |<span data-ttu-id="cf4ff-249">Да</span><span class="sxs-lookup"><span data-stu-id="cf4ff-249">Yes</span></span> |
| <span data-ttu-id="cf4ff-250">Описание</span><span class="sxs-lookup"><span data-stu-id="cf4ff-250">description</span></span> |<span data-ttu-id="cf4ff-251">Текст, описывающий, какое действие hello используется для</span><span class="sxs-lookup"><span data-stu-id="cf4ff-251">Text describing what hello activity is used for</span></span> |<span data-ttu-id="cf4ff-252">Нет</span><span class="sxs-lookup"><span data-stu-id="cf4ff-252">No</span></span> |
| <span data-ttu-id="cf4ff-253">type</span><span class="sxs-lookup"><span data-stu-id="cf4ff-253">type</span></span> | <span data-ttu-id="cf4ff-254">Нужно задать значение **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="cf4ff-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="cf4ff-255">Да</span><span class="sxs-lookup"><span data-stu-id="cf4ff-255">Yes</span></span> |
| <span data-ttu-id="cf4ff-256">inputs</span><span class="sxs-lookup"><span data-stu-id="cf4ff-256">inputs</span></span> | <span data-ttu-id="cf4ff-257">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-257">Optional.</span></span> <span data-ttu-id="cf4ff-258">При указании входного набора данных, он должен быть доступен (в состояние «Готово») для hello хранимой процедуры toorun действия.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="cf4ff-259">Hello входного набора данных не может использоваться в hello хранимой процедуре как параметр.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-259">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="cf4ff-260">Это только используемые toocheck hello зависимостей, до начала hello действие хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-260">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> |<span data-ttu-id="cf4ff-261">Нет</span><span class="sxs-lookup"><span data-stu-id="cf4ff-261">No</span></span> |
| <span data-ttu-id="cf4ff-262">outputs</span><span class="sxs-lookup"><span data-stu-id="cf4ff-262">outputs</span></span> | <span data-ttu-id="cf4ff-263">Для действия хранимой процедуры необходимо указать выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="cf4ff-264">Выходной набор данных указывает hello **расписание** для hello действие хранимой процедуры (каждый час, еженедельно, ежемесячно, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-264">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="cf4ff-265">Hello выходной набор данных необходимо использовать **связанная служба** , обозначающий tooan базы данных SQL Azure или хранилище данных SQL Azure или базе SQL Server, в котором нужно hello toorun хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-265">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <br/><br/><span data-ttu-id="cf4ff-266">Hello выходной набор данных может служить результат hello toopass способом hello хранимые процедуры для последующей обработки другим действием ([цепочки действий](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-266">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="cf4ff-267">Однако фабрики данных вывода автоматически hello объекта dataset toothis хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-267">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="cf4ff-268">Это hello хранимая процедура записи таблицы tooa SQL, который hello указывает выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-268">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <br/><br/><span data-ttu-id="cf4ff-269">В некоторых случаях может быть выходной набор данных hello **пустой набор данных**, который используется только для hello расписание hello toospecify действие хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-269">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span> |<span data-ttu-id="cf4ff-270">Да</span><span class="sxs-lookup"><span data-stu-id="cf4ff-270">Yes</span></span> |
| <span data-ttu-id="cf4ff-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="cf4ff-271">storedProcedureName</span></span> |<span data-ttu-id="cf4ff-272">Укажите имя hello hello хранимой процедуры в базе данных Azure SQL hello или хранилище данных SQL Azure или SQL Server базы данных, представленного hello связаны службы, которая hello использования выходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-272">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="cf4ff-273">Да</span><span class="sxs-lookup"><span data-stu-id="cf4ff-273">Yes</span></span> |
| <span data-ttu-id="cf4ff-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="cf4ff-274">storedProcedureParameters</span></span> |<span data-ttu-id="cf4ff-275">Указываемые значения для параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="cf4ff-276">Если вам требуется toopass значение null для параметра, используйте синтаксис hello: «param1»: null (все строчные).</span><span class="sxs-lookup"><span data-stu-id="cf4ff-276">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="cf4ff-277">См. следующий пример toolearn об использовании этого свойства hello.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-277">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="cf4ff-278">Нет</span><span class="sxs-lookup"><span data-stu-id="cf4ff-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="cf4ff-279">Передача статического значения</span><span class="sxs-lookup"><span data-stu-id="cf4ff-279">Passing a static value</span></span>
<span data-ttu-id="cf4ff-280">Теперь давайте рассмотрим добавление другой столбец с именем «Сценарий» в таблице hello, содержащий статический значение с именем «Документа-пример».</span><span class="sxs-lookup"><span data-stu-id="cf4ff-280">Now, let’s consider adding another column named ‘Scenario’ in hello table containing a static value called ‘Document sample’.</span></span>

![Пример данных 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="cf4ff-282">**Таблица:**</span><span class="sxs-lookup"><span data-stu-id="cf4ff-282">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="cf4ff-283">**Хранимая процедура:**</span><span class="sxs-lookup"><span data-stu-id="cf4ff-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="cf4ff-284">Теперь, передавать hello **сценарий** значение параметра и hello из hello действие хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="cf4ff-284">Now, pass hello **Scenario** parameter and hello value from hello stored procedure activity.</span></span> <span data-ttu-id="cf4ff-285">Hello **typeProperties** раздела hello предшествующий выглядит пример hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="cf4ff-285">hello **typeProperties** section in hello preceding sample looks like hello following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="cf4ff-286">**Набор данных фабрики данных:**</span><span class="sxs-lookup"><span data-stu-id="cf4ff-286">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="cf4ff-287">**Конвейер фабрики данных**</span><span class="sxs-lookup"><span data-stu-id="cf4ff-287">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```