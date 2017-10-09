---
title: "aaaLoad данных в хранилище данных SQL Azure — фабрики данных | Документы Microsoft"
description: "Этот учебник загружает данные в хранилище данных SQL Azure с помощью фабрики данных Azure и использует базы данных SQL Server в качестве источника данных hello."
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
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="afdb6-103">Загрузка данных в хранилище данных SQL с помощью фабрики данных</span><span class="sxs-lookup"><span data-stu-id="afdb6-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="afdb6-104">Можно использовать данные tooload фабрики данных Azure в хранилище данных SQL Azure из любого hello [поддерживается хранилищ данных источника](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="afdb6-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="afdb6-105">Например, с помощью фабрики данных можно загрузить данные из базы данных SQL Azure или базы данных Oracle в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="afdb6-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="afdb6-106">Учебник, в этой статье показано, как tooload данных с сервера SQL в локальной базы данных в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="afdb6-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="afdb6-107">**Примерное время**: учебником занимает около 10 – 15 минут toocomplete после hello предварительных условий.</span><span class="sxs-lookup"><span data-stu-id="afdb6-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afdb6-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="afdb6-108">Prerequisites</span></span>

- <span data-ttu-id="afdb6-109">Требуется **базы данных SQL Server** с таблицами, содержащими данные hello toobe копируются toohello хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="afdb6-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="afdb6-110">**Хранилище данных SQL.**</span><span class="sxs-lookup"><span data-stu-id="afdb6-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="afdb6-111">Если вы еще нет в хранилище данных, узнайте, как слишком[создать хранилище данных SQL Azure](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="afdb6-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="afdb6-112">**Учетная запись хранения Azure.**</span><span class="sxs-lookup"><span data-stu-id="afdb6-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="afdb6-113">Если у вас еще нет учетной записи хранилища, узнайте, как слишком[создать учетную запись хранилища](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="afdb6-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="afdb6-114">Для наилучшей производительности, найдите учетную запись хранилища hello и хранилища данных hello в hello же регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="afdb6-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="afdb6-115">Настройка фабрики данных</span><span class="sxs-lookup"><span data-stu-id="afdb6-115">Configure a data factory</span></span>
1. <span data-ttu-id="afdb6-116">Войдите в toohello [портал Azure][].</span><span class="sxs-lookup"><span data-stu-id="afdb6-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="afdb6-117">Найдите хранилищем данных и щелкните tooopen его.</span><span class="sxs-lookup"><span data-stu-id="afdb6-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="afdb6-118">В главной колонке hello щелкните **загрузки данных** > **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Запуск мастера загрузки данных](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="afdb6-120">Если у вас фабрики данных в вашей подписке Azure, вы увидите **новую фабрику данных** диалоговое на отдельной вкладке браузера hello.</span><span class="sxs-lookup"><span data-stu-id="afdb6-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="afdb6-121">Заполните hello запрошенных сведения и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="afdb6-122">После создания фабрики данных hello hello **новую фабрику данных** диалоговое окно закрывается, и вы видите hello **выберите фабрики данных** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="afdb6-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="afdb6-123">Если у вас есть один или несколько фабрик данных уже находится в hello подписки Azure, вы увидите hello **выберите фабрики данных** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="afdb6-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="afdb6-124">В этом диалоговом окне можно выбрать существующую фабрику данных или нажмите кнопку **создать новую фабрику данных** toocreate новый.</span><span class="sxs-lookup"><span data-stu-id="afdb6-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![Настройка фабрики данных](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="afdb6-126">В hello **выберите фабрики данных** диалоговое окно, hello **загрузки данных** параметр выбран по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="afdb6-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="afdb6-127">Нажмите кнопку **Далее** toostart создание данных при загрузке задачи.</span><span class="sxs-lookup"><span data-stu-id="afdb6-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="afdb6-128">Настройка свойств фабрики данных hello</span><span class="sxs-lookup"><span data-stu-id="afdb6-128">Configure hello data factory properties</span></span>
<span data-ttu-id="afdb6-129">После создания фабрики данных hello следующим шагом является загрузка расписание tooconfigure hello данных.</span><span class="sxs-lookup"><span data-stu-id="afdb6-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="afdb6-130">В качестве **имени задачи** введите **DWLoadData-fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="afdb6-131">Использовать значение по умолчанию hello **запустить один раз сейчас** , нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![Настройка расписания загрузки](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="afdb6-133">Настройка хранилища данных источника hello и шлюза</span><span class="sxs-lookup"><span data-stu-id="afdb6-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="afdb6-134">Теперь вы указываете фабрики данных о базе данных SQL Server в локальной среде hello tooload данные из которого нужно получить.</span><span class="sxs-lookup"><span data-stu-id="afdb6-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="afdb6-135">Выберите **SQL Server** из исходных данных поддерживается hello хранения каталога и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![Выбор источника SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="afdb6-137">Объект **базы данных SQL Server укажите hello локальной** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="afdb6-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="afdb6-138">Здравствуйте, сначала **имя подключения** поле будет заполнено автоматически.</span><span class="sxs-lookup"><span data-stu-id="afdb6-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="afdb6-139">Второе поле Hello запрашивает имя hello hello **шлюза**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="afdb6-140">При использовании существующей фабрики данных, уже содержит шлюз можно повторно использовать hello шлюза, выбрав необходимую из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="afdb6-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="afdb6-141">Нажмите кнопку hello **создать шлюз** связать toocreate шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="afdb6-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="afdb6-142">Если хранилище данных источника hello локально или на виртуальной машине Azure IaaS требуется шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="afdb6-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="afdb6-143">Шлюз связан с фабрикой данных по схеме "один к одному".</span><span class="sxs-lookup"><span data-stu-id="afdb6-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="afdb6-144">Не может использоваться из другого фабрики данных, но он может использоваться несколько загрузки задач с hello данных же фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="afdb6-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="afdb6-145">Шлюз может быть хранилищ данных toomultiple tooconnect используется при выполнении задачи загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="afdb6-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="afdb6-146">Подробные сведения о шлюзе hello. в разделе [шлюз управления данными](../data-factory/data-factory-data-management-gateway.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="afdb6-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="afdb6-147">Откроется диалоговое окно **Создание шлюза**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="afdb6-148">В качестве имени введите **GatewayForDWLoading** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="afdb6-149">Откроется диалоговое окно **Настройка шлюза**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="afdb6-150">Нажмите кнопку **запуска экспресс-установку на этом компьютере** tooautomatically загрузить, установить и зарегистрировать шлюз управления данными на текущем компьютере.</span><span class="sxs-lookup"><span data-stu-id="afdb6-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="afdb6-151">во всплывающем окне отображается ход выполнения Hello.</span><span class="sxs-lookup"><span data-stu-id="afdb6-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="afdb6-152">Hello компьютера не удается подключиться toohello хранилища данных, можно вручную [скачать и установить шлюз hello](https://www.microsoft.com/download/details.aspx?id=39717) на компьютере, который можно подключить данные toohello хранения, а затем использовать ключа tooregister hello.</span><span class="sxs-lookup"><span data-stu-id="afdb6-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="afdb6-153">экспресс-установку Hello изначально работает с Microsoft Edge и Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="afdb6-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="afdb6-154">При использовании Google Chrome сначала установите расширение ClickOnce hello из Chrome веб-хранилища.</span><span class="sxs-lookup"><span data-stu-id="afdb6-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![Запуск экспресс-установки](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="afdb6-156">Дождитесь установки toocomplete hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="afdb6-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="afdb6-157">После hello шлюз успешно зарегистрирован и находится в оперативном режиме, hello всплывающее окно закрывается, а новый шлюз hello отображается в hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="afdb6-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="afdb6-158">Затем заполните hello остальные обязательные поля следующим образом, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="afdb6-159">**Имя сервера**: hello имя локального SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afdb6-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="afdb6-160">**Имя базы**: имя базы данных сервера SQL.</span><span class="sxs-lookup"><span data-stu-id="afdb6-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="afdb6-161">**Учетными данными шифрования**: используется по умолчанию hello «веб-браузер».</span><span class="sxs-lookup"><span data-stu-id="afdb6-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="afdb6-162">**Тип проверки подлинности**: выберите тип проверки подлинности, вы используете hello.</span><span class="sxs-lookup"><span data-stu-id="afdb6-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="afdb6-163">**Имя пользователя** и **пароль**: Введите hello имя пользователя и пароль для пользователя, имеющего разрешение toocopy hello данных.</span><span class="sxs-lookup"><span data-stu-id="afdb6-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![Запуск экспресс-установки](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="afdb6-165">Hello следующим шагом является toochoose hello таблиц, из которых данные toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="afdb6-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="afdb6-166">Можно фильтровать hello таблицы с помощью ключевых слов.</span><span class="sxs-lookup"><span data-stu-id="afdb6-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="afdb6-167">И вы можете просмотреть схему таблицы и данным hello hello нижней панели.</span><span class="sxs-lookup"><span data-stu-id="afdb6-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="afdb6-168">Выбрав нужные элементы, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-168">After you finish your selection, click **Next**.</span></span>

    ![Выбор таблиц](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="afdb6-170">Настройка назначения «hello» в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="afdb6-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="afdb6-171">Теперь вы указываете фабрики данных о сведения о назначении hello.</span><span class="sxs-lookup"><span data-stu-id="afdb6-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="afdb6-172">Сведения о подключении к хранилищу данных SQL будут заполнены автоматически.</span><span class="sxs-lookup"><span data-stu-id="afdb6-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="afdb6-173">Введите hello пароль для имени пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="afdb6-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="afdb6-174">а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-174">and click **Next**.</span></span>

    ![Настройка назначения](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="afdb6-176">Сопоставление интеллектуальной таблицы появляется соответствие исходных toodestination таблиц на основе имен таблиц.</span><span class="sxs-lookup"><span data-stu-id="afdb6-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="afdb6-177">Если таблица hello не существует в месте назначения hello, по умолчанию ADF создаст с hello таким же именем (применяется tooSQL сервера или базы данных SQL Azure в качестве источника).</span><span class="sxs-lookup"><span data-stu-id="afdb6-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="afdb6-178">Также можно выбрать существующую таблицу tooan toomap.</span><span class="sxs-lookup"><span data-stu-id="afdb6-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="afdb6-179">Просмотрите результат и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-179">Review and click **Next**.</span></span>

    ![Сопоставление таблиц](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="afdb6-181">Проверьте соответствие схемы hello и проверьте наличие ошибок или предупреждений.</span><span class="sxs-lookup"><span data-stu-id="afdb6-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="afdb6-182">Интеллектуальное сопоставление основано на имени столбца.</span><span class="sxs-lookup"><span data-stu-id="afdb6-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="afdb6-183">Если преобразование типов данных не поддерживается между исходной и целевой столбец hello, вы видите сообщение об ошибке наряду с соответствующей таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="afdb6-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="afdb6-184">При выборе toolet фабрики данных автоматически создать таблицу hello, правильное преобразование типов может произойти при необходимости toofix hello несовместимости между хранилищами источника и назначения.</span><span class="sxs-lookup"><span data-stu-id="afdb6-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![Сопоставление схем](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="afdb6-186">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="afdb6-187">Настройка параметров производительности hello</span><span class="sxs-lookup"><span data-stu-id="afdb6-187">Configure hello performance settings</span></span>
<span data-ttu-id="afdb6-188">В конфигурациях производительности hello, настройте учетную запись хранилища Azure, используемую для промежуточных hello данных перед загрузкой в хранилище данных SQL с помощью performantly [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="afdb6-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="afdb6-189">После завершения копирования hello hello промежуточных данных в хранилище будут очищены автоматически.</span><span class="sxs-lookup"><span data-stu-id="afdb6-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="afdb6-190">Выберите существующую учетную запись хранения Azure и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Настройка промежуточного BLOB-объекта](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="afdb6-192">Просмотрите сводные данные и развертывание конвейера hello</span><span class="sxs-lookup"><span data-stu-id="afdb6-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="afdb6-193">Проверьте конфигурацию hello и нажмите кнопку **Готово** кнопку toodeploy hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="afdb6-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![Развертывание фабрики данных](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="afdb6-195">Мониторинг загрузки данных</span><span class="sxs-lookup"><span data-stu-id="afdb6-195">Monitor data loading progress</span></span>

<span data-ttu-id="afdb6-196">Можно просмотреть ход выполнения развертывания hello и результаты в hello **развертывания** страницы.</span><span class="sxs-lookup"><span data-stu-id="afdb6-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="afdb6-197">После завершения развертывания hello по ссылке hello потребовал **щелкните здесь конвейера копирования toomonitor** загрузки выполняется toomonitor данных.</span><span class="sxs-lookup"><span data-stu-id="afdb6-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![Отслеживание конвейера](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="afdb6-199">вновь созданные Hello **DWLoadData fromSQLServer** конвейера загрузки данных выбирается автоматически из левой hello **обозреватель ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![Представление конвейера](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="afdb6-201">Щелкните в конвейер hello в середине hello hello toosee панель, сведения о состоянии для каждой таблицы, которая сопоставляет tooan действия.</span><span class="sxs-lookup"><span data-stu-id="afdb6-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![Просмотр действия таблицы](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="afdb6-203">Далее щелкните в действие и позволяет просматривать данные hello загрузка сведений о hello правой панели, включая размер данных, строки, пропускной способности, и т. д.</span><span class="sxs-lookup"><span data-stu-id="afdb6-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![Просмотр сведений о действии таблицы](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="afdb6-205">toolaunch этого мониторинга представление более поздней версии, выберите tooyour хранилище данных SQL, щелкните **загрузки данных > фабрики данных Azure**выберите фабрики и выберите **отслеживать существующие задачи загрузки**.</span><span class="sxs-lookup"><span data-stu-id="afdb6-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afdb6-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="afdb6-206">Next steps</span></span>

<span data-ttu-id="afdb6-207">toomigrate tooSQL вашей базы данных хранилища данных, в разделе [Общие сведения о миграции](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="afdb6-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="afdb6-208">toolearn Дополнительные сведения о фабрики данных Azure и его возможности перемещения данных, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="afdb6-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="afdb6-209">Введение tooAzure фабрики данных</span><span class="sxs-lookup"><span data-stu-id="afdb6-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="afdb6-210">Перемещение данных с помощью действия копирования</span><span class="sxs-lookup"><span data-stu-id="afdb6-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="afdb6-211">Tooand перемещения данных из хранилища данных SQL Azure, с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="afdb6-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="afdb6-212">tooexplore данные в хранилище данных SQL, в разделе hello следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="afdb6-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="afdb6-213">Подключиться с помощью Visual Studio и SSDT tooSQL хранилища данных</span><span class="sxs-lookup"><span data-stu-id="afdb6-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="afdb6-214">[Визуализация данных с помощью Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="afdb6-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[портал Azure]: https://portal.azure.com
