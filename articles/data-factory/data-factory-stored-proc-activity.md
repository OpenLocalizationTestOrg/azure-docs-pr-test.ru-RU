---
title: "Действие \"Хранимая процедура SQL Server\""
description: "Узнайте, как с помощью действия хранимой процедуры SQL Server можно вызвать хранимую процедуру в Базе данных SQL Azure или хранилище данных SQL Azure из конвейера фабрики данных."
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
ms.openlocfilehash: 6505d9aa2c7ae003bd928e2fa82cd923a9615394
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="fc053-103">Действие "Хранимая процедура SQL Server"</span><span class="sxs-lookup"><span data-stu-id="fc053-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="fc053-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="fc053-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="fc053-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="fc053-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="fc053-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="fc053-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="fc053-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="fc053-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="fc053-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="fc053-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="fc053-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="fc053-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="fc053-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="fc053-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="fc053-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="fc053-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="fc053-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="fc053-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="fc053-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="fc053-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="fc053-114">Обзор</span><span class="sxs-lookup"><span data-stu-id="fc053-114">Overview</span></span>
<span data-ttu-id="fc053-115">Действия преобразования данных в [конвейере](data-factory-create-pipelines.md) фабрики данных позволяют преобразовать необработанные данные и переработать их в прогнозы и аналитику.</span><span class="sxs-lookup"><span data-stu-id="fc053-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="fc053-116">Действие хранимой процедуры — это одно из действий преобразования данных, которые поддерживает фабрика данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-116">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="fc053-117">Данная статья основана на материалах статьи о [действиях преобразования данных](data-factory-data-transformation-activities.md), в которой приведен общий обзор преобразования данных и список поддерживаемых действий преобразования в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="fc053-118">C его помощью можно вызвать хранимую процедуру в одном из следующих хранилищ данных вашего предприятия или на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="fc053-118">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="fc053-119">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="fc053-119">Azure SQL Database</span></span>
- <span data-ttu-id="fc053-120">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="fc053-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="fc053-121">База данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fc053-121">SQL Server Database.</span></span>  <span data-ttu-id="fc053-122">Если вы используете SQL Server, установите шлюз управления данными на том же компьютере, на котором размещена база данных, или на отдельном компьютере, имеющем доступ к базе данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-122">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="fc053-123">Шлюз управления данными — это компонент, который обеспечивает безопасное и управляемое подключение локальных источников данных или данных виртуальной машины Azure к облачным службам.</span><span class="sxs-lookup"><span data-stu-id="fc053-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="fc053-124">Дополнительные сведения см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="fc053-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc053-125">При копировании данных в базу данных SQL Azure или SQL Server можно настроить класс **SqlSink** в действии копирования для вызова хранимой процедуры с помощью свойства **sqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="fc053-125">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="fc053-126">Дополнительные сведения см. в статье [Вызов хранимой процедуры из действия копирования в фабрике данных Azure](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="fc053-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="fc053-127">Дополнительные сведения о свойствах см. в следующих статьях о соединителях: [Перемещение данных в базу данных SQL Azure и из нее с помощью фабрики данных Azure](data-factory-azure-sql-connector.md#copy-activity-properties) и [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fc053-127">For details about the property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="fc053-128">Вызов хранимой процедуры во время копирования данных в хранилище данных SQL Azure с помощью операции копирования не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="fc053-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="fc053-129">Однако действие хранимой процедуры можно использовать для вызова хранимой процедуры в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fc053-129">But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="fc053-130">При копировании данных из базы данных SQL Azure, SQL Server или хранилища данных SQL Azure можно настроить **SqlSource** в действии копирования, чтобы вызвать хранимую процедуру для считывания данных из исходной базы данных с помощью свойства **sqlReaderStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="fc053-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="fc053-131">Дополнительные сведения см. в разделе "Свойства действия копирования" следующих статей о соединителях: [Перемещение данных в базу данных SQL Azure и из нее с помощью фабрики данных Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-sqlserver-connector.md#copy-activity-properties), [Перемещение данных в хранилище данных Azure SQL и из него с помощью фабрики данных Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fc053-131">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="fc053-132">В следующем пошаговом руководстве используется действие "Хранимая процедура SQL Server" в конвейере для вызова хранимой процедуры в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fc053-132">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="fc053-133">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="fc053-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="fc053-134">Образец таблицы и хранимая процедура</span><span class="sxs-lookup"><span data-stu-id="fc053-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="fc053-135">Создайте следующую **таблицу** в базе данных SQL Azure с помощью SQL Server Management Studio или другого подходящего инструмента.</span><span class="sxs-lookup"><span data-stu-id="fc053-135">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="fc053-136">Столбец datetimestamp содержит дату и время создания соответствующего идентификатора.</span><span class="sxs-lookup"><span data-stu-id="fc053-136">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

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
    <span data-ttu-id="fc053-137">Id — уникальный идентификатор, а столбец datetimestamp содержит дату и время создания соответствующего идентификатора.</span><span class="sxs-lookup"><span data-stu-id="fc053-137">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![Пример данных](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="fc053-139">В этом примере хранимая процедура находится в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fc053-139">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="fc053-140">Если хранимая процедура находится в хранилище данных SQL Azure и базе данных SQL Server, используется аналогичный подход.</span><span class="sxs-lookup"><span data-stu-id="fc053-140">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="fc053-141">В случае с базой данных SQL Server необходимо установить [шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="fc053-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="fc053-142">Создайте следующую **хранимую процедуру**, вставляющую данные в таблицу **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="fc053-142">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="fc053-143">**Имя** и **регистр** параметра (в этом примере — DateTime) должны соответствовать имени и регистру параметра, указанного в конвейере или действии JSON.</span><span class="sxs-lookup"><span data-stu-id="fc053-143">**Name** and **casing** of the parameter (DateTime in this example) must match that of parameter specified in the pipeline/activity JSON.</span></span> <span data-ttu-id="fc053-144">Убедитесь, что в определении хранимой процедуры в качестве префикса для параметра используется символ **@** .</span><span class="sxs-lookup"><span data-stu-id="fc053-144">In the stored procedure definition, ensure that **@** is used as a prefix for the parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="fc053-145">Создать фабрику данных</span><span class="sxs-lookup"><span data-stu-id="fc053-145">Create a data factory</span></span>
1. <span data-ttu-id="fc053-146">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fc053-146">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fc053-147">Щелкните **Создать** в меню слева, выберите **Аналитика** и щелкните **Фабрика данных**.</span><span class="sxs-lookup"><span data-stu-id="fc053-147">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Новая фабрика данных](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="fc053-149">В колонке **Новая фабрика данных** введите **SProcDF** в поле "Имя".</span><span class="sxs-lookup"><span data-stu-id="fc053-149">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="fc053-150">Имена фабрики данных Azure являются **глобально уникальными**.</span><span class="sxs-lookup"><span data-stu-id="fc053-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="fc053-151">Для успешного создания фабрики добавьте свое имя в качестве префикса имени фабрики.</span><span class="sxs-lookup"><span data-stu-id="fc053-151">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![Новая фабрика данных](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="fc053-153">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="fc053-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="fc053-154">Для **группы ресурсов** выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="fc053-154">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="fc053-155">Щелкните **Создать** и введите имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fc053-155">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="fc053-156">Щелкните **Использовать существующий** и укажите имеющуюся группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fc053-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="fc053-157">Укажите **расположение** фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-157">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="fc053-158">Выберите **Закрепить на панели мониторинга**, чтобы при следующем входе фабрика данных отобразилась на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="fc053-158">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="fc053-159">В колонке **Создание фабрики данных** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fc053-159">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="fc053-160">Созданная фабрика данных появится на **панели мониторинга** портала Azure.</span><span class="sxs-lookup"><span data-stu-id="fc053-160">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="fc053-161">Ее содержимое отобразится на соответствующей странице.</span><span class="sxs-lookup"><span data-stu-id="fc053-161">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Домашняя страница фабрики данных](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="fc053-163">Создание связанной службы SQL Azure</span><span class="sxs-lookup"><span data-stu-id="fc053-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="fc053-164">После создания фабрики данных создайте связанную службу SQL Azure, которая связывает базу данных SQL Azure, содержащую упомянутую таблицу и хранимую процедуру, с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-164">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span></span>

1. <span data-ttu-id="fc053-165">В колонке **Фабрика данных** щелкните **Создать и развернуть** для **SProcDF**, чтобы запустить редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-165">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="fc053-166">Щелкните **Новое хранилище данных** в командной строке и выберите **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="fc053-166">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="fc053-167">В редакторе отобразится сценарий JSON для создания связанной службы SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fc053-167">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![Новое хранилище данных](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="fc053-169">Внесите следующие изменения в сценарий JSON:</span><span class="sxs-lookup"><span data-stu-id="fc053-169">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="fc053-170">Замените `<servername>` именем сервера базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fc053-170">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="fc053-171">Замените `<databasename>` базой данных, в которой создана таблица и хранимая процедура.</span><span class="sxs-lookup"><span data-stu-id="fc053-171">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="fc053-172">Замените `<username@servername>` учетной записью пользователя, у которой есть доступ к базе данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-172">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="fc053-173">Замените `<password>` паролем к учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="fc053-173">Replace `<password>` with the password for the user account.</span></span>

      ![Новое хранилище данных](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="fc053-175">Чтобы развернуть связанную службу, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="fc053-175">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="fc053-176">Экземпляр AzureSqlLinkedService должен отображаться в иерархическом представлении слева.</span><span class="sxs-lookup"><span data-stu-id="fc053-176">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![иерархическое представление со связанными службами](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="fc053-178">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="fc053-178">Create an output dataset</span></span>
<span data-ttu-id="fc053-179">Необходимо указать набор выходных данных для действия хранимой процедуры, даже если хранимая процедура не возвращает данные.</span><span class="sxs-lookup"><span data-stu-id="fc053-179">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span></span> <span data-ttu-id="fc053-180">Это связано с тем, что набор выходных данных управляет расписанием действия (то, как часто запускается действие: ежечасно, ежедневно и т. д.).</span><span class="sxs-lookup"><span data-stu-id="fc053-180">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="fc053-181">Выходной набор данных должен использовать **связанную службу**, ссылающуюся на Базу данных SQL Azure, хранилище данных SQL Azure или базу данных SQL Server, в которых следует запускать хранимую процедуру.</span><span class="sxs-lookup"><span data-stu-id="fc053-181">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="fc053-182">Выходной набор данных может использоваться для передачи результатов хранимой процедуры для дальнейшей обработки с помощью другого действия ([цепочки действий](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)) в конвейере.</span><span class="sxs-lookup"><span data-stu-id="fc053-182">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="fc053-183">Тем не менее фабрика данных не записывает выходные данные хранимой процедуры в этот набор данных автоматически.</span><span class="sxs-lookup"><span data-stu-id="fc053-183">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="fc053-184">Выходные данные записывает сама хранимая процедура в таблицу SQL, на которую указывает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-184">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="fc053-185">В некоторых случаях набор выходных данных может быть **фиктивным** (набор данных, указывающий на таблицу, которая не содержит выходные данные хранимой процедуры).</span><span class="sxs-lookup"><span data-stu-id="fc053-185">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span></span> <span data-ttu-id="fc053-186">Такой набор данных используется, только чтобы задать расписание выполнения действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="fc053-186">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span></span> 

1. <span data-ttu-id="fc053-187">Нажмите **... Дополнительно** на панели инструментов, щелкните **Новый набор данных** и выберите **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="fc053-187">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="fc053-188">**Новый набор данных** на панели команд и выберите **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="fc053-188">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![иерархическое представление со связанными службами](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="fc053-190">Скопируйте и вставьте следующий скрипт JSON в редактор JSON.</span><span class="sxs-lookup"><span data-stu-id="fc053-190">Copy/paste the following JSON script in to the JSON editor.</span></span>

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
3. <span data-ttu-id="fc053-191">Чтобы развернуть набор данных, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="fc053-191">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="fc053-192">Набор данных должен отображаться в иерархическом представлении.</span><span class="sxs-lookup"><span data-stu-id="fc053-192">Confirm that you see the dataset in the tree view.</span></span>

    ![иерархическое представление со связанными службами](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="fc053-194">Создание конвейера с помощью действия SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="fc053-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="fc053-195">Теперь создадим конвейер с помощью действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="fc053-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="fc053-196">Обратите внимание на следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="fc053-196">Notice the following properties:</span></span> 

- <span data-ttu-id="fc053-197">Свойству **type** присвоено значение **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="fc053-197">The **type** property is set to **SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="fc053-198">Параметру **storedProcedureName** в свойствах типа присвоено значение **sp_sample** (имя хранимой процедуры).</span><span class="sxs-lookup"><span data-stu-id="fc053-198">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span></span>
- <span data-ttu-id="fc053-199">Раздел **storedProcedureParameters** содержит один параметр с именем **DataTime**.</span><span class="sxs-lookup"><span data-stu-id="fc053-199">The **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="fc053-200">Имя и регистр параметра в формате JSON должны совпадать с именем и регистром параметра в определении хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="fc053-200">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span></span> <span data-ttu-id="fc053-201">Если для параметра необходимо передать значение null, используйте синтаксис `"param1": null` (все символы в нижнем регистре).</span><span class="sxs-lookup"><span data-stu-id="fc053-201">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="fc053-202">Нажмите **... Дополнительно** на панели команд и выберите **Новый конвейер**.</span><span class="sxs-lookup"><span data-stu-id="fc053-202">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="fc053-203">Скопируйте и вставьте следующий фрагмент JSON.</span><span class="sxs-lookup"><span data-stu-id="fc053-203">Copy/paste the following JSON snippet:</span></span>   

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
3. <span data-ttu-id="fc053-204">Чтобы развернуть конвейер, щелкните **Развернуть** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="fc053-204">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="fc053-205">Мониторинг конвейера</span><span class="sxs-lookup"><span data-stu-id="fc053-205">Monitor the pipeline</span></span>
1. <span data-ttu-id="fc053-206">Щелкните **X**, чтобы закрыть колонки редактора фабрики данных и вернуться в колонку фабрики данных. Затем щелкните **Схема**.</span><span class="sxs-lookup"><span data-stu-id="fc053-206">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![плитка "Схема"](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="fc053-208">В **представлении схемы**вы увидите все конвейеры и наборы данных, используемые в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="fc053-208">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![плитка "Схема"](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="fc053-210">В представлении схемы дважды щелкните набор данных `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="fc053-210">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="fc053-211">Отобразятся срезы в состоянии "Готово".</span><span class="sxs-lookup"><span data-stu-id="fc053-211">You see the slices in Ready state.</span></span> <span data-ttu-id="fc053-212">Должно отобразиться пять срезов, так как из JSON срез создается каждый час в периоде между временем начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="fc053-212">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![плитка "Схема"](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="fc053-214">Если срез находится в состоянии **Готово**, выполните запрос `select * from sampletable` к базе данных SQL Azure, чтобы убедиться, что хранимая процедура вставила данные в таблицу.</span><span class="sxs-lookup"><span data-stu-id="fc053-214">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![Выходные данные](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="fc053-216">В разделе [Мониторинг конвейера](data-factory-monitor-manage-pipelines.md) представлены подробные сведения о мониторинге конвейеров фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fc053-216">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="fc053-217">Указание набора входных данных</span><span class="sxs-lookup"><span data-stu-id="fc053-217">Specify an input dataset</span></span>
<span data-ttu-id="fc053-218">В этом руководстве действие хранимой процедуры не содержит наборы входных данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-218">In the walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="fc053-219">При указании набора входных данных действие хранимой процедуры не выполняется, пока не стает доступен срез набора входных данных (в состоянии "Готово").</span><span class="sxs-lookup"><span data-stu-id="fc053-219">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="fc053-220">Набор данных может быть внешним (который не был создан с помощью другого действия в одном конвейере) или внутренним, созданным с помощью вышестоящего действия (действие, которое выполняется перед этим действием).</span><span class="sxs-lookup"><span data-stu-id="fc053-220">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span></span> <span data-ttu-id="fc053-221">Для действия хранимой процедуры можно указать несколько наборов входных данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-221">You can specify multiple input datasets for the stored procedure activity.</span></span> <span data-ttu-id="fc053-222">В таком случае действие хранимой процедуры выполняется только в том случае, когда доступны все срезы набора входных данных (в состоянии "Готово").</span><span class="sxs-lookup"><span data-stu-id="fc053-222">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="fc053-223">Входной набор данных не может потребляться в хранимой процедуре в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="fc053-223">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="fc053-224">Он используется только для проверки зависимости перед запуском действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="fc053-224">It is only used to check the dependency before starting the stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="fc053-225">Объединение с другими действиями</span><span class="sxs-lookup"><span data-stu-id="fc053-225">Chaining with other activities</span></span>
<span data-ttu-id="fc053-226">Если необходимо объединить вышестоящее действие с этим действием, укажите выходные данные вышестоящего действия в качестве входных данных этого действия.</span><span class="sxs-lookup"><span data-stu-id="fc053-226">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span></span> <span data-ttu-id="fc053-227">При этом действие хранимой процедуры не выполняется, пока не завершится вышестоящее действие и набор выходных данных вышестоящего действия не станет доступен (в состоянии "Готово").</span><span class="sxs-lookup"><span data-stu-id="fc053-227">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span></span> <span data-ttu-id="fc053-228">В качестве наборов входных данных действия хранимой процедуры можно указать наборы выходных данных нескольких вышестоящих действий.</span><span class="sxs-lookup"><span data-stu-id="fc053-228">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span></span> <span data-ttu-id="fc053-229">В таком случае действие хранимой процедуры выполняется только в том случае, когда доступны все срезы набора входных данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-229">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span></span>  

<span data-ttu-id="fc053-230">В следующем примере выходными данными действия копирования является набор OutputDataset, который представляет собой входные данные действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="fc053-230">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span></span> <span data-ttu-id="fc053-231">Таким образом, действие хранимой процедуры не выполняется, пока не завершится действие копирования и срез набора данных OutputDataset не станет доступен (в состоянии "Готово").</span><span class="sxs-lookup"><span data-stu-id="fc053-231">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="fc053-232">При указании нескольких наборов входных данных действие хранимой процедуры не выполняется, пока не станет доступен срез набора входных данных (в состоянии "Готово").</span><span class="sxs-lookup"><span data-stu-id="fc053-232">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="fc053-233">Наборы входных данных нельзя использовать непосредственно в качестве параметров действия хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="fc053-233">The input datasets cannot be used directly as parameters to the stored procedure activity.</span></span> 

<span data-ttu-id="fc053-234">Дополнительные сведения о цепочках действий см. в разделе [Несколько действий в конвейере](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="fc053-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob to blob",
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

<span data-ttu-id="fc053-235">Аналогичным образом, чтобы связать действие хранимой процедуры с **нижестоящими действиями** (действия, которые выполняются после завершения действия хранимой процедуры), укажите набор выходных данных действия хранимой процедуры в качестве входных данных нижестоящего действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="fc053-235">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc053-236">При копировании данных в базу данных SQL Azure или SQL Server можно настроить класс **SqlSink** в действии копирования для вызова хранимой процедуры с помощью свойства **sqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="fc053-236">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="fc053-237">Дополнительные сведения см. в статье [Вызов хранимой процедуры из действия копирования в фабрике данных Azure](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="fc053-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="fc053-238">Дополнительные сведения о свойствах см. в следующих статьях о соединителях: [Перемещение данных в базу данных SQL Azure и из нее с помощью фабрики данных Azure](data-factory-azure-sql-connector.md#copy-activity-properties) и [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fc053-238">For details about the property, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="fc053-239">При копировании данных из базы данных SQL Azure, SQL Server или хранилища данных SQL Azure можно настроить **SqlSource** в действии копирования, чтобы вызвать хранимую процедуру для считывания данных из исходной базы данных с помощью свойства **sqlReaderStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="fc053-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="fc053-240">Дополнительные сведения см. в разделе "Свойства действия копирования" следующих статей о соединителях: [Перемещение данных в базу данных SQL Azure и из нее с помощью фабрики данных Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-sqlserver-connector.md#copy-activity-properties), [Перемещение данных в хранилище данных Azure SQL и из него с помощью фабрики данных Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fc053-240">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="fc053-241">Формат JSON</span><span class="sxs-lookup"><span data-stu-id="fc053-241">JSON format</span></span>
<span data-ttu-id="fc053-242">Ниже приведен формат JSON для определения действия хранимой процедуры:</span><span class="sxs-lookup"><span data-stu-id="fc053-242">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of the stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="fc053-243">В следующей таблице описаны эти свойства JSON:</span><span class="sxs-lookup"><span data-stu-id="fc053-243">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="fc053-244">Свойство</span><span class="sxs-lookup"><span data-stu-id="fc053-244">Property</span></span> | <span data-ttu-id="fc053-245">Описание</span><span class="sxs-lookup"><span data-stu-id="fc053-245">Description</span></span> | <span data-ttu-id="fc053-246">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fc053-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc053-247">name</span><span class="sxs-lookup"><span data-stu-id="fc053-247">name</span></span> | <span data-ttu-id="fc053-248">Имя действия.</span><span class="sxs-lookup"><span data-stu-id="fc053-248">Name of the activity</span></span> |<span data-ttu-id="fc053-249">Да</span><span class="sxs-lookup"><span data-stu-id="fc053-249">Yes</span></span> |
| <span data-ttu-id="fc053-250">Описание</span><span class="sxs-lookup"><span data-stu-id="fc053-250">description</span></span> |<span data-ttu-id="fc053-251">Текст, описывающий, для чего используется действие</span><span class="sxs-lookup"><span data-stu-id="fc053-251">Text describing what the activity is used for</span></span> |<span data-ttu-id="fc053-252">Нет</span><span class="sxs-lookup"><span data-stu-id="fc053-252">No</span></span> |
| <span data-ttu-id="fc053-253">type</span><span class="sxs-lookup"><span data-stu-id="fc053-253">type</span></span> | <span data-ttu-id="fc053-254">Нужно задать значение **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="fc053-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="fc053-255">Да</span><span class="sxs-lookup"><span data-stu-id="fc053-255">Yes</span></span> |
| <span data-ttu-id="fc053-256">inputs</span><span class="sxs-lookup"><span data-stu-id="fc053-256">inputs</span></span> | <span data-ttu-id="fc053-257">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="fc053-257">Optional.</span></span> <span data-ttu-id="fc053-258">При указании входного набора данных он должен быть доступен (в состоянии "Готово") для выполнения действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="fc053-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="fc053-259">Входной набор данных не может потребляться в хранимой процедуре в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="fc053-259">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="fc053-260">Он используется только для проверки зависимости перед запуском действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="fc053-260">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="fc053-261">Нет</span><span class="sxs-lookup"><span data-stu-id="fc053-261">No</span></span> |
| <span data-ttu-id="fc053-262">outputs</span><span class="sxs-lookup"><span data-stu-id="fc053-262">outputs</span></span> | <span data-ttu-id="fc053-263">Для действия хранимой процедуры необходимо указать выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="fc053-264">Выходной набор данных указывает **расписание** для действия хранимой процедуры (ежечасно, еженедельно, ежемесячно и т. д.).</span><span class="sxs-lookup"><span data-stu-id="fc053-264">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="fc053-265">Выходной набор данных должен использовать **связанную службу**, ссылающуюся на Базу данных SQL Azure, хранилище данных SQL Azure или базу данных SQL Server, в которых следует запускать хранимую процедуру.</span><span class="sxs-lookup"><span data-stu-id="fc053-265">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="fc053-266">Выходной набор данных может использоваться для передачи результатов хранимой процедуры для дальнейшей обработки с помощью другого действия ([цепочки действий](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)) в конвейере.</span><span class="sxs-lookup"><span data-stu-id="fc053-266">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="fc053-267">Тем не менее фабрика данных не записывает выходные данные хранимой процедуры в этот набор данных автоматически.</span><span class="sxs-lookup"><span data-stu-id="fc053-267">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="fc053-268">Выходные данные записывает сама хранимая процедура в таблицу SQL, на которую указывает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="fc053-268">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="fc053-269">В некоторых случаях выходной набор данных может быть **фиктивным набором данных**. Он используется, только чтобы задать расписание выполнения действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="fc053-269">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="fc053-270">Да</span><span class="sxs-lookup"><span data-stu-id="fc053-270">Yes</span></span> |
| <span data-ttu-id="fc053-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="fc053-271">storedProcedureName</span></span> |<span data-ttu-id="fc053-272">Укажите имя хранимой процедуры в базе данных SQL Azure, хранилище данных SQL Azure или в базе данных SQL Server, представленной связанной службой, которую использует выходная таблица.</span><span class="sxs-lookup"><span data-stu-id="fc053-272">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="fc053-273">Да</span><span class="sxs-lookup"><span data-stu-id="fc053-273">Yes</span></span> |
| <span data-ttu-id="fc053-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="fc053-274">storedProcedureParameters</span></span> |<span data-ttu-id="fc053-275">Указываемые значения для параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="fc053-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="fc053-276">Если для параметра необходимо передать значение null, используйте синтаксис param1: null (все символы в нижнем регистре).</span><span class="sxs-lookup"><span data-stu-id="fc053-276">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="fc053-277">Чтобы научиться использовать это свойство, см. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="fc053-277">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="fc053-278">Нет</span><span class="sxs-lookup"><span data-stu-id="fc053-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="fc053-279">Передача статического значения</span><span class="sxs-lookup"><span data-stu-id="fc053-279">Passing a static value</span></span>
<span data-ttu-id="fc053-280">Теперь давайте рассмотрим добавление другого столбца с именем "Scenario" в таблицу, содержащую статическое значение с именем "Document sample".</span><span class="sxs-lookup"><span data-stu-id="fc053-280">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![Пример данных 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="fc053-282">**Таблица:**</span><span class="sxs-lookup"><span data-stu-id="fc053-282">**Table:**</span></span>

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

<span data-ttu-id="fc053-283">**Хранимая процедура:**</span><span class="sxs-lookup"><span data-stu-id="fc053-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="fc053-284">Теперь передайте параметр **Scenario** и значение из действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="fc053-284">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="fc053-285">Раздел **typeProperties** в предыдущем примере выглядит как следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="fc053-285">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

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

<span data-ttu-id="fc053-286">**Набор данных фабрики данных:**</span><span class="sxs-lookup"><span data-stu-id="fc053-286">**Data Factory dataset:**</span></span>

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

<span data-ttu-id="fc053-287">**Конвейер фабрики данных**</span><span class="sxs-lookup"><span data-stu-id="fc053-287">**Data Factory pipeline**</span></span>

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