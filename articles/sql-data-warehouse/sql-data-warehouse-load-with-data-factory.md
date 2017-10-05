---
title: "Загрузка данных в хранилище данных SQL Azure (фабрика данных) | Документация Майкрософт"
description: "В этом руководстве вы загрузите данные в хранилище данных SQL Azure, используя фабрику данных Azure и базу данных SQL Server в качестве источника данных."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 12a35213e07ff16bdc1c27be106792bcc032ac80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="a73e4-103">Загрузка данных в хранилище данных SQL с помощью фабрики данных</span><span class="sxs-lookup"><span data-stu-id="a73e4-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="a73e4-104">Фабрику данных Azure можно использовать для загрузки данных в хранилище данных SQL Azure из любых [поддерживаемых исходных хранилищ данных](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="a73e4-104">You can use Azure Data Factory to load data into Azure SQL Data Warehouse from any of the [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="a73e4-105">Например, с помощью фабрики данных можно загрузить данные из базы данных SQL Azure или базы данных Oracle в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a73e4-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="a73e4-106">В руководстве в этой статье показано, как загрузить данные из локальной базы данных SQL Server в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a73e4-106">Tutorial in this article shows you how to load data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="a73e4-107">**Оценка времени**. Для работы с этим руководством потребуется около 10–15 минут (при условии, что предварительные требования уже выполнены).</span><span class="sxs-lookup"><span data-stu-id="a73e4-107">**Time estimate**: This tutorial takes about 10-15 minutes to complete once the prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a73e4-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a73e4-108">Prerequisites</span></span>

- <span data-ttu-id="a73e4-109">**База данных SQL Server** с таблицами, содержащими данные, которые требуется скопировать в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a73e4-109">You need a **SQL Server database** with tables that contain the data to be copied over to the SQL data warehouse.</span></span>  

- <span data-ttu-id="a73e4-110">**Хранилище данных SQL.**</span><span class="sxs-lookup"><span data-stu-id="a73e4-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="a73e4-111">Если у вас еще нет хранилища данных, создайте его, как описано в статье [Создание хранилища данных SQL Azure](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="a73e4-111">If you do not already have a data warehouse, learn how to [Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="a73e4-112">**Учетная запись хранения Azure.**</span><span class="sxs-lookup"><span data-stu-id="a73e4-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="a73e4-113">Если у вас еще нет учетной записи хранения, узнайте, как [ее создать](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a73e4-113">If you do not already have a storage account, learn how to [Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="a73e4-114">Чтобы оптимизировать производительность, разместите учетную запись хранения и хранилище данных в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="a73e4-114">For best performance, locate the storage account and the data warehouse in the same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="a73e4-115">Настройка фабрики данных</span><span class="sxs-lookup"><span data-stu-id="a73e4-115">Configure a data factory</span></span>
1. <span data-ttu-id="a73e4-116">Войдите на [портал Azure][].</span><span class="sxs-lookup"><span data-stu-id="a73e4-116">Log in to the [Azure portal][].</span></span>
2. <span data-ttu-id="a73e4-117">Найдите хранилище данных и щелкните, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="a73e4-117">Locate your data warehouse and click to open it.</span></span>
3. <span data-ttu-id="a73e4-118">В главной колонке щелкните **Загрузка данных** > **Фабрика данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-118">In the main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Запуск мастера загрузки данных](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="a73e4-120">Если в вашей подписке Azure нет фабрики данных, то вы увидите диалоговое окно **Новая фабрика данных** на отдельной вкладке браузера.</span><span class="sxs-lookup"><span data-stu-id="a73e4-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of the browser.</span></span> <span data-ttu-id="a73e4-121">Введите требуемые данные и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-121">Fill in the requested information, and click **Create**.</span></span> <span data-ttu-id="a73e4-122">После создания фабрики данных диалоговое окно **Новая фабрика данных** закроется, и вы увидите диалоговое окно **Select Data Factory** (Выбор фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="a73e4-122">After the data factory is created, the **New Data Factory** dialog box closes, and you see the **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="a73e4-123">Если в вашей подписке Azure уже есть одна или несколько фабрик данных, то, вы увидите диалоговое окно **Select Data Factory** (Выбор фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="a73e4-123">If you have one or more data factories already in the Azure subscription, you see the **Select Data Factory** dialog box.</span></span> <span data-ttu-id="a73e4-124">В этом диалоговом окне можно выбрать существующую фабрику данных или щелкнуть **Create new data factory** (Создать новую фабрику данных), чтобы создать новую.</span><span class="sxs-lookup"><span data-stu-id="a73e4-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** to create a new one.</span></span>

    ![Настройка фабрики данных](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="a73e4-126">В диалоговом окне **Выбор фабрики данных** параметр **Загрузить данные** выбран по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a73e4-126">In the **Select Data Factory** dialog box, the **Load data** option is selected by default.</span></span> <span data-ttu-id="a73e4-127">Щелкните **Далее**, чтобы начать создание задачи загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="a73e4-127">Click **Next** to start creating a data loading task.</span></span>

## <a name="configure-the-data-factory-properties"></a><span data-ttu-id="a73e4-128">Настройка свойств фабрики данных</span><span class="sxs-lookup"><span data-stu-id="a73e4-128">Configure the data factory properties</span></span>
<span data-ttu-id="a73e4-129">Создав фабрику данных, переходите к настройке расписания загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="a73e4-129">Now that you have created a data factory, the next step is to configure the data loading schedule.</span></span>

1. <span data-ttu-id="a73e4-130">В качестве **имени задачи** введите **DWLoadData-fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="a73e4-131">Используйте параметр по умолчанию **Запустить один раз** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-131">Use the default **Run once now** option, click **Next**.</span></span>

    ![Настройка расписания загрузки](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-the-source-data-store-and-gateway"></a><span data-ttu-id="a73e4-133">Настройка исходного хранилища данных и шлюза</span><span class="sxs-lookup"><span data-stu-id="a73e4-133">Configure the source data store and gateway</span></span>
<span data-ttu-id="a73e4-134">Теперь для фабрики данных нужно указать локальную базу данных SQL Server для загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="a73e4-134">Now you tell Data Factory about the on-premises SQL Server database from which you want to load data.</span></span>

1. <span data-ttu-id="a73e4-135">Выберите **SQL Server** в каталоге хранилищ данных, поддерживаемых в качестве источника данных, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-135">Choose **SQL Server** from the supported source data store catalog, and click **Next**.</span></span>

    ![Выбор источника SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="a73e4-137">Откроется диалоговое окно **Выбор локальной базы данных SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-137">A **Specify the on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="a73e4-138">Первое поле **Имя подключения** заполнено автоматически.</span><span class="sxs-lookup"><span data-stu-id="a73e4-138">The first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="a73e4-139">Во втором поле нужно указать имя **шлюза**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-139">The second field asks for the name of the **Gateway**.</span></span> <span data-ttu-id="a73e4-140">При использовании существующей фабрики данных, у которой уже имеется шлюз, можно повторно использовать его, выбрав этот шлюз из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="a73e4-140">If you are using an existing data factory that already has a gateway, you can reuse the gateway by selecting it from the drop-down list.</span></span> <span data-ttu-id="a73e4-141">Щелкните ссылку **Создать шлюз**, чтобы создать шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="a73e4-141">Click the **Create Gateway** link to create a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="a73e4-142">Если исходное хранилище данных расположено в локальной среде или в виртуальной машине IaaS Azure, то шлюз управления данными указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="a73e4-142">If the source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="a73e4-143">Шлюз связан с фабрикой данных по схеме "один к одному".</span><span class="sxs-lookup"><span data-stu-id="a73e4-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="a73e4-144">Он не может использоваться другой фабрикой данных, но может использоваться несколькими задачами загрузки в одной фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="a73e4-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in the same data factory.</span></span> <span data-ttu-id="a73e4-145">Шлюз можно использовать для подключения к нескольким хранилищам данных при выполнении задач загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="a73e4-145">A gateway can be used to connect to multiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="a73e4-146">Дополнительные сведения о шлюзе см. в статье [Шлюз управления данными](../data-factory/data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a73e4-146">For detailed information about the gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="a73e4-147">Откроется диалоговое окно **Создание шлюза**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="a73e4-148">В качестве имени введите **GatewayForDWLoading** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="a73e4-149">Откроется диалоговое окно **Настройка шлюза**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="a73e4-150">Щелкните ссылку **Launch express setup on this computer** (Запустить экспресс-установку на этом компьютере), чтобы автоматически скачать, установить и зарегистрировать шлюз управления данными на текущем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a73e4-150">Click **Launch express setup on this computer** to automatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="a73e4-151">Ход выполнения отображается во всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="a73e4-151">The progress is shown in a pop-up window.</span></span> <span data-ttu-id="a73e4-152">Если этот компьютер не может подключиться к хранилищу данных, то можно вручную [скачать и установить шлюз](https://www.microsoft.com/download/details.aspx?id=39717) на компьютере, который может подключиться к хранилищу данных, а затем использовать ключ для регистрации.</span><span class="sxs-lookup"><span data-stu-id="a73e4-152">If the machine cannot connect to the data store, you can manually [download and install the gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect to the data store, and then use the key to register.</span></span>
    > [!NOTE]
    > <span data-ttu-id="a73e4-153">Экспресс-установка по умолчанию выполняется с помощью Microsoft Edge и Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="a73e4-153">The express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="a73e4-154">Если вы используете Google Chrome, сначала установите расширение ClickOnce из интернет-магазина Chrome.</span><span class="sxs-lookup"><span data-stu-id="a73e4-154">If you are using Google Chrome, first install the ClickOnce extension from Chrome web store.</span></span>

    ![Запуск экспресс-установки](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="a73e4-156">Дождитесь завершения установки шлюза.</span><span class="sxs-lookup"><span data-stu-id="a73e4-156">Wait for the gateway setup to complete.</span></span> <span data-ttu-id="a73e4-157">После регистрации и подключения шлюза всплывающее окно закроется, а новый шлюз отобразится в поле шлюза.</span><span class="sxs-lookup"><span data-stu-id="a73e4-157">Once the gateway is successfully registered and is online, the pop-up window closes and the new gateway appears in the gateway field.</span></span> <span data-ttu-id="a73e4-158">Заполните остальные обязательные поля, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-158">Then fill in the rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="a73e4-159">**Имя сервера**: имя локального сервера SQL.</span><span class="sxs-lookup"><span data-stu-id="a73e4-159">**Server name**: Name of the on-premises SQL Server.</span></span>
    - <span data-ttu-id="a73e4-160">**Имя базы**: имя базы данных сервера SQL.</span><span class="sxs-lookup"><span data-stu-id="a73e4-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="a73e4-161">**Credential encryption** (Шифрование учетных данных). Используйте значение по умолчанию (By web browser (В браузере)).</span><span class="sxs-lookup"><span data-stu-id="a73e4-161">**Credential encryption**: Use the default "By web browser".</span></span>
    - <span data-ttu-id="a73e4-162">**Тип проверки подлинности**: выберите тип проверки подлинности, который вы используете.</span><span class="sxs-lookup"><span data-stu-id="a73e4-162">**Authentication type**: Choose the type of authentication you are using.</span></span>
    - <span data-ttu-id="a73e4-163">**Имя пользователя** и **пароль**: введите имя и пароль для пользователя с правами на копирование данных.</span><span class="sxs-lookup"><span data-stu-id="a73e4-163">**User name** and **password**: Enter the user name and password for a user who has permission to copy the data.</span></span>

    ![Запуск экспресс-установки](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="a73e4-165">Затем вам нужно выбрать таблицы, из которых будут копироваться данные.</span><span class="sxs-lookup"><span data-stu-id="a73e4-165">The next step is to choose the tables from which to copy the data.</span></span> <span data-ttu-id="a73e4-166">Эти таблицы можно отфильтровать с помощью ключевых слов.</span><span class="sxs-lookup"><span data-stu-id="a73e4-166">You can filter the tables by using keywords.</span></span> <span data-ttu-id="a73e4-167">Кроме того, на нижней панели доступен предварительный просмотр схемы таблиц и данных.</span><span class="sxs-lookup"><span data-stu-id="a73e4-167">And you can preview the data and table schema in the bottom panel.</span></span> <span data-ttu-id="a73e4-168">Выбрав нужные элементы, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-168">After you finish your selection, click **Next**.</span></span>

    ![Выбор таблиц](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-the-destination-your-sql-data-warehouse"></a><span data-ttu-id="a73e4-170">Настройка целевого расположения — хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="a73e4-170">Configure the destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="a73e4-171">Теперь для фабрики данных нужно указать сведения о назначении.</span><span class="sxs-lookup"><span data-stu-id="a73e4-171">Now you tell Data Factory about the destination information.</span></span>

1. <span data-ttu-id="a73e4-172">Сведения о подключении к хранилищу данных SQL будут заполнены автоматически.</span><span class="sxs-lookup"><span data-stu-id="a73e4-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="a73e4-173">Введите пароль для этого имени пользователя,</span><span class="sxs-lookup"><span data-stu-id="a73e4-173">Enter the password for the user name.</span></span> <span data-ttu-id="a73e4-174">а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-174">and click **Next**.</span></span>

    ![Настройка назначения](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="a73e4-176">Отобразится интеллектуальное сопоставление таблиц, которое позволяет связать исходные и целевые таблицы на основе имен таблиц.</span><span class="sxs-lookup"><span data-stu-id="a73e4-176">An intelligent table mapping appears that maps source to destination tables based on table names.</span></span> <span data-ttu-id="a73e4-177">Если в целевом расположении отсутствует таблица, ADF по умолчанию создаст ее с тем же именем (если в качестве исходного хранилища используется SQL Server или база данных Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="a73e4-177">If the table does not exist in the destination, by default ADF will create one with the same name (this applies to SQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="a73e4-178">Вы также можете сопоставить имеющуюся таблицу.</span><span class="sxs-lookup"><span data-stu-id="a73e4-178">You can also choose to map to an existing table.</span></span> <span data-ttu-id="a73e4-179">Просмотрите результат и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-179">Review and click **Next**.</span></span>

    ![Сопоставление таблиц](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="a73e4-181">Просмотрите сопоставление схем и проверьте наличие сообщений об ошибке.</span><span class="sxs-lookup"><span data-stu-id="a73e4-181">Review the schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="a73e4-182">Интеллектуальное сопоставление основано на имени столбца.</span><span class="sxs-lookup"><span data-stu-id="a73e4-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="a73e4-183">Если между исходным и целевым столбцами обнаружится преобразование неподдерживаемого типа данных, появится сообщение об ошибке с указанием на соответствующую таблицу.</span><span class="sxs-lookup"><span data-stu-id="a73e4-183">If there is an unsupported data type conversion between the source and destination column, you see an error message alongside the corresponding table.</span></span> <span data-ttu-id="a73e4-184">Если включить функцию автоматического создания таблиц, в фабрике данных может выполняться преобразование типов данных. Это позволяет устранить несовместимость между исходными и целевыми хранилищами.</span><span class="sxs-lookup"><span data-stu-id="a73e4-184">If you choose to let Data Factory auto create the tables, proper data type conversion may happen if needed to fix the incompatibility between source and destination stores.</span></span>

    ![Сопоставление схем](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="a73e4-186">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-186">Click **Next**.</span></span>

## <a name="configure-the-performance-settings"></a><span data-ttu-id="a73e4-187">Настройка параметров производительности</span><span class="sxs-lookup"><span data-stu-id="a73e4-187">Configure the performance settings</span></span>
<span data-ttu-id="a73e4-188">В параметрах производительности настройте учетную запись хранения Azure для промежуточного хранения данных перед их загрузкой в хранилище данных SQL, используя [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="a73e4-188">In the Performance configurations, you configure an Azure storage account used for staging the data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="a73e4-189">После завершения копирования промежуточные данные в хранилище будут удалены автоматически.</span><span class="sxs-lookup"><span data-stu-id="a73e4-189">After the copy is done, the interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="a73e4-190">Выберите существующую учетную запись хранения Azure и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Настройка промежуточного BLOB-объекта](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-the-pipeline"></a><span data-ttu-id="a73e4-192">Просмотр сводных данных и развертывание конвейера</span><span class="sxs-lookup"><span data-stu-id="a73e4-192">Review summary information and deploy the pipeline</span></span>

<span data-ttu-id="a73e4-193">Проверьте конфигурацию и нажмите кнопку **Готово**, чтобы развернуть конвейер.</span><span class="sxs-lookup"><span data-stu-id="a73e4-193">Review the configuration and click **Finish** button to deploy the pipeline.</span></span>

![Развертывание фабрики данных](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="a73e4-195">Мониторинг загрузки данных</span><span class="sxs-lookup"><span data-stu-id="a73e4-195">Monitor data loading progress</span></span>

<span data-ttu-id="a73e4-196">На странице **развертывания** можно увидеть ход выполнения развертывания и его результаты.</span><span class="sxs-lookup"><span data-stu-id="a73e4-196">You can see the deployment progress and results in the **Deployment** page.</span></span>

1. <span data-ttu-id="a73e4-197">После развертывания для мониторинга загрузки данных щелкните ссылку **Click here to monitor copy pipeline** (Щелкните здесь для мониторинга конвейера копирования).</span><span class="sxs-lookup"><span data-stu-id="a73e4-197">Once the deployment is done, click the link that says **Click here to monitor copy pipeline** to monitor data loading progress.</span></span>

    ![Отслеживание конвейера](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="a73e4-199">Созданный конвейер загрузки данных **DWLoadData-fromSQLServer** будет выбран автоматически слева в **обозревателе ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="a73e4-199">The newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from the left-hand **Resource Explorer**.</span></span>

    ![Представление конвейера](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="a73e4-201">Щелкните конвейер в центральной области, чтобы просмотреть подробные сведения о состоянии каждой таблицы, связанной с действием.</span><span class="sxs-lookup"><span data-stu-id="a73e4-201">Click into the pipeline in the middle panel to see the detailed status for each table that maps to an Activity.</span></span>

    ![Просмотр действия таблицы](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="a73e4-203">Вы также можете щелкнуть действие, чтобы просмотреть данные о загрузке на панели справа, включая размер данных, строки, пропускную способность и т. д.</span><span class="sxs-lookup"><span data-stu-id="a73e4-203">Further click into an activity and you see the data loading details in the right panel including data size, rows, throughput, etc.</span></span>

    ![Просмотр сведений о действии таблицы](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="a73e4-205">Чтобы запустить это представление мониторинга позже, в хранилище данных SQL щелкните **Загрузить данные > Фабрика данных Azure**, выберите свою фабрику и щелкните **Monitor existing loading tasks** (Отслеживать существующие задачи загрузки).</span><span class="sxs-lookup"><span data-stu-id="a73e4-205">To launch this monitoring view later, go to your SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a73e4-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a73e4-206">Next steps</span></span>

<span data-ttu-id="a73e4-207">Инструкции по переносу базы данных в хранилище данных SQL см. в статье [Перенос решения в хранилище данных SQL](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="a73e4-207">To migrate your database to SQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="a73e4-208">Чтобы узнать больше о фабрике данных Azure и ее возможностях по перемещению данных, ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="a73e4-208">To learn more about Azure Data Factory and its data movement capabilities, see the following articles:</span></span>

- [<span data-ttu-id="a73e4-209">Общие сведения о службе фабрики данных Azure, службе интеграции данных в облаке</span><span class="sxs-lookup"><span data-stu-id="a73e4-209">Introduction to Azure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="a73e4-210">Перемещение данных с помощью действия копирования</span><span class="sxs-lookup"><span data-stu-id="a73e4-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="a73e4-211">Перемещение данных в хранилище данных Azure SQL и из него с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="a73e4-211">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="a73e4-212">Чтобы узнать, как просматривать данные в хранилище данных SQL, ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="a73e4-212">To explore your data in SQL Data Warehouse, see the following articles:</span></span>

- [<span data-ttu-id="a73e4-213">Подключение к хранилищу данных SQL с помощью Visual Studio и SSDT</span><span class="sxs-lookup"><span data-stu-id="a73e4-213">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="a73e4-214">[Визуализация данных с помощью Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="a73e4-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[портал Azure]: https://portal.azure.com
