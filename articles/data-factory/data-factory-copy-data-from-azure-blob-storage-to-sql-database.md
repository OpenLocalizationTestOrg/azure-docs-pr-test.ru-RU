---
title: "aaaCopy данные из хранилища больших двоичных объектов tooSQL база данных — Azure | Документы Microsoft"
description: "Этот учебник показывает, как toouse действие копирования в фабрике данных Azure конвейера toocopy данные из базы данных tooSQL хранилища Blob."
keywords: "BLOB-объект, SQL, хранилище BLOB-объектов, копирование данных"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a><span data-ttu-id="0882a-104">Учебник: Копирование данных из хранилища больших двоичных объектов tooSQL базы данных с помощью фабрики данных</span><span class="sxs-lookup"><span data-stu-id="0882a-104">Tutorial: Copy data from Blob Storage tooSQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0882a-105">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0882a-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="0882a-106">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="0882a-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="0882a-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="0882a-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="0882a-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0882a-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="0882a-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0882a-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="0882a-110">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0882a-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="0882a-111">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="0882a-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="0882a-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="0882a-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="0882a-113">В этом учебнике создать фабрику данных данными конвейера toocopy из базы данных tooSQL хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="0882a-113">In this tutorial, you create a data factory with a pipeline toocopy data from Blob storage tooSQL database.</span></span>

<span data-ttu-id="0882a-114">Действие копирования Hello выполняет перемещение данных hello в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0882a-114">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="0882a-115">Это действие выполняется с помощью глобально доступной службы, обеспечивающей безопасное, надежное и масштабируемое копирование данных между разными хранилищами.</span><span class="sxs-lookup"><span data-stu-id="0882a-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="0882a-116">В разделе [действия перемещения данных](data-factory-data-movement-activities.md) статьи приведены сведения о действии копирования hello.</span><span class="sxs-lookup"><span data-stu-id="0882a-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="0882a-117">Подробный обзор hello служба фабрики данных см. в разделе hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0882a-117">For a detailed overview of hello Data Factory service, see hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="0882a-118">Необходимые условия для учебника hello</span><span class="sxs-lookup"><span data-stu-id="0882a-118">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="0882a-119">Прежде чем начать работу с учебником, необходимо иметь hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="0882a-119">Before you begin this tutorial, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="0882a-120">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="0882a-120">**Azure subscription**.</span></span>  <span data-ttu-id="0882a-121">Если у вас нет подписки, вы можете создать бесплатную пробную версию учетной записи всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0882a-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0882a-122">В разделе hello [бесплатной пробной версии](http://azure.microsoft.com/pricing/free-trial/) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="0882a-122">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="0882a-123">**исходного**хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="0882a-123">**Azure Storage Account**.</span></span> <span data-ttu-id="0882a-124">Использовать хранилище больших двоичных объектов hello как **источника** хранилище данных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0882a-124">You use hello blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="0882a-125">При отсутствии учетной записи хранилища Azure в разделе hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи для действия toocreate один.</span><span class="sxs-lookup"><span data-stu-id="0882a-125">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="0882a-126">**База данных SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="0882a-126">**Azure SQL Database**.</span></span> <span data-ttu-id="0882a-127">В этом учебнике используется база данных SQL Azure в качестве **конечного** хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="0882a-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="0882a-128">Если у вас нет базы данных Azure SQL, можно использовать в hello учебника, см. в разделе [как toocreate и настроить базу данных SQL Azure](../sql-database/sql-database-get-started.md) toocreate один.</span><span class="sxs-lookup"><span data-stu-id="0882a-128">If you don't have an Azure SQL database that you can use in hello tutorial, See [How toocreate and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate one.</span></span>
* <span data-ttu-id="0882a-129">**SQL Server 2012/2014 или Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="0882a-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="0882a-130">Используйте SQL Server Management Studio или Visual Studio toocreate образца базы данных и tooview hello результирующие данные в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="0882a-130">You use SQL Server Management Studio or Visual Studio toocreate a sample database and tooview hello result data in hello database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="0882a-131">Получение имени и ключа учетной записи хранения BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="0882a-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="0882a-132">Требуется учетная запись hello, имя и ключ учетной записи хранилища Azure учетной записи toodo этого учебника.</span><span class="sxs-lookup"><span data-stu-id="0882a-132">You need hello account name and account key of your Azure storage account toodo this tutorial.</span></span> <span data-ttu-id="0882a-133">Запишите **имя** и **ключ учетной записи** для своей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="0882a-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="0882a-134">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0882a-134">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0882a-135">Нажмите кнопку **дополнительные службы** на hello слева и выбрать пункт **учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="0882a-135">Click **More services** on hello left menu and select **Storage Accounts**.</span></span>

    !["Обзор" — "Учетные записи хранения"](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="0882a-137">В hello **учетные записи хранения** колонки, выберите hello **учетной записи хранилища Azure** требуется toouse в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0882a-137">In hello **Storage Accounts** blade, select hello **Azure storage account** that you want toouse in this tutorial.</span></span>
4. <span data-ttu-id="0882a-138">В разделе **Параметры** выберите ссылку **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="0882a-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="0882a-139">Нажмите кнопку **копирования** (изображение) рядом слишком**имя учетной записи хранения** текста поле, сохранить и вставка его где-нибудь (например: в текстовом файле).</span><span class="sxs-lookup"><span data-stu-id="0882a-139">Click **copy** (image) button next too**Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="0882a-140">Повторите предыдущие шаг toocopy hello или запишите hello **key1**.</span><span class="sxs-lookup"><span data-stu-id="0882a-140">Repeat hello previous step toocopy or note down hello **key1**.</span></span>

    ![Ключ доступа к хранилищу](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="0882a-142">Закройте все колонках hello, нажав кнопку **X**.</span><span class="sxs-lookup"><span data-stu-id="0882a-142">Close all hello blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="0882a-143">Получение имени сервера SQL, имени базы данных и имени пользователя</span><span class="sxs-lookup"><span data-stu-id="0882a-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="0882a-144">Должны иметь имена hello Azure SQL server, базы данных и toodo пользователя этого учебника.</span><span class="sxs-lookup"><span data-stu-id="0882a-144">You need hello names of Azure SQL server, database, and user toodo this tutorial.</span></span> <span data-ttu-id="0882a-145">Запишите имена **сервера**, **базы данных** и **пользователя** базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0882a-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="0882a-146">В hello **портал Azure**, нажмите кнопку **дополнительные службы** на hello слева и выберите **баз данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="0882a-146">In hello **Azure portal**, click **More services** on hello left and select **SQL databases**.</span></span>
2. <span data-ttu-id="0882a-147">В hello **колонки баз данных SQL**выберите hello **базы данных** требуется toouse в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0882a-147">In hello **SQL databases blade**, select hello **database** that you want toouse in this tutorial.</span></span> <span data-ttu-id="0882a-148">Запишите hello **имя базы данных**.</span><span class="sxs-lookup"><span data-stu-id="0882a-148">Note down hello **database name**.</span></span>  
3. <span data-ttu-id="0882a-149">В hello **базы данных SQL** колонка, щелкните **свойства** под **параметры**.</span><span class="sxs-lookup"><span data-stu-id="0882a-149">In hello **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="0882a-150">Запишите значения hello **имя сервера** и **имя входа АДМИНИСТРАТОРА сервера**.</span><span class="sxs-lookup"><span data-stu-id="0882a-150">Note down hello values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="0882a-151">Закройте все колонках hello, нажав кнопку **X**.</span><span class="sxs-lookup"><span data-stu-id="0882a-151">Close all hello blades by clicking **X**.</span></span>

## <a name="allow-azure-services-tooaccess-sql-server"></a><span data-ttu-id="0882a-152">Разрешить службам Azure tooaccess SQL server</span><span class="sxs-lookup"><span data-stu-id="0882a-152">Allow Azure services tooaccess SQL server</span></span>
<span data-ttu-id="0882a-153">Убедитесь, что **разрешить доступ службы tooAzure** включен параметр **ON** для вашего сервера Azure SQL, так что hello служба фабрики данных можно получить доступ к серверу Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="0882a-153">Ensure that **Allow access tooAzure services** setting turned **ON** for your Azure SQL server so that hello Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="0882a-154">tooverify и включение этого параметра hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0882a-154">tooverify and turn on this setting, do hello following steps:</span></span>

1. <span data-ttu-id="0882a-155">Нажмите кнопку **дополнительные службы** концентратора hello слева и щелкните **серверов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0882a-155">Click **More services** hub on hello left and click **SQL servers**.</span></span>
2. <span data-ttu-id="0882a-156">Выберите сервер и щелкните **Брандмауэр** в разделе **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="0882a-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="0882a-157">В hello **параметры брандмауэра** колонка, щелкните **ON** для **разрешить доступ службы tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="0882a-157">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
4. <span data-ttu-id="0882a-158">Закройте все колонках hello, нажав кнопку **X**.</span><span class="sxs-lookup"><span data-stu-id="0882a-158">Close all hello blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="0882a-159">Подготовка хранилища BLOB-объектов и базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="0882a-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="0882a-160">Теперь Подготовьте хранилище больших двоичных объектов и базы данных Azure SQL для учебника hello, выполнив следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0882a-160">Now, prepare your Azure blob storage and Azure SQL database for hello tutorial by performing hello following steps:</span></span>  

1. <span data-ttu-id="0882a-161">Запустите Блокнот.</span><span class="sxs-lookup"><span data-stu-id="0882a-161">Launch Notepad.</span></span> <span data-ttu-id="0882a-162">Скопируйте следующий текст hello и сохраните его как **emp.txt** слишком**C:\ADFGetStarted** папку на жестком диске.</span><span class="sxs-lookup"><span data-stu-id="0882a-162">Copy hello following text and save it as **emp.txt** too**C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="0882a-163">Использовать инструменты, такие как [обозреватель хранилищ Azure](http://storageexplorer.com/) toocreate hello **adftutorial** hello контейнера и tooupload **emp.txt** toohello файла контейнера.</span><span class="sxs-lookup"><span data-stu-id="0882a-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** container and tooupload hello **emp.txt** file toohello container.</span></span>

    ![Обозреватель хранилищ Azure](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="0882a-166">Используйте hello, следуя hello toocreate скрипт SQL **emp** таблицы в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0882a-166">Use hello following SQL script toocreate hello **emp** table in your Azure SQL Database.</span></span>  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    <span data-ttu-id="0882a-167">**Если у вас есть SQL Server 2012 и 2014 установлены на компьютере:** следуйте инструкциям из [управление базой данных SQL Azure с помощью SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL и запустите hello скрипт SQL.</span><span class="sxs-lookup"><span data-stu-id="0882a-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server and run hello SQL script.</span></span> <span data-ttu-id="0882a-168">В этой статье используется hello [классический портал Azure](http://manage.windowsazure.com), не hello [новый портал Azure](https://portal.azure.com), tooconfigure брандмауэра для сервера Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="0882a-168">This article uses hello [classic Azure portal](http://manage.windowsazure.com), not hello [new Azure portal](https://portal.azure.com), tooconfigure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="0882a-169">Если клиент не может быть tooaccess hello Azure SQL server, необходимо tooconfigure брандмауэра для Azure SQL server tooallow доступ с вашего компьютера (IP-адрес).</span><span class="sxs-lookup"><span data-stu-id="0882a-169">If your client is not allowed tooaccess hello Azure SQL server, you need tooconfigure firewall for your Azure SQL server tooallow access from your machine (IP Address).</span></span> <span data-ttu-id="0882a-170">В разделе [в этой статье](../sql-database/sql-database-configure-firewall-settings.md) действия tooconfigure hello брандмауэра для сервера Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="0882a-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps tooconfigure hello firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="0882a-171">Создать фабрику данных</span><span class="sxs-lookup"><span data-stu-id="0882a-171">Create a data factory</span></span>
<span data-ttu-id="0882a-172">Предварительные требования hello завершена.</span><span class="sxs-lookup"><span data-stu-id="0882a-172">You have completed hello prerequisites.</span></span> <span data-ttu-id="0882a-173">Можно создать фабрику данных, с помощью одного из следующих способов hello.</span><span class="sxs-lookup"><span data-stu-id="0882a-173">You can create a data factory using one of hello following ways.</span></span> <span data-ttu-id="0882a-174">Выберите один из вариантов hello в hello раскрывающегося списка в верхней hello или hello следующие ссылки tooperform hello учебника.</span><span class="sxs-lookup"><span data-stu-id="0882a-174">Click one of hello options in hello drop-down list at hello top or hello following links tooperform hello tutorial.</span></span>     

* [<span data-ttu-id="0882a-175">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="0882a-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="0882a-176">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="0882a-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="0882a-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0882a-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="0882a-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0882a-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="0882a-179">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0882a-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="0882a-180">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="0882a-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="0882a-181">API .NET</span><span class="sxs-lookup"><span data-stu-id="0882a-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="0882a-182">конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="0882a-182">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="0882a-183">Он не выполняет преобразование входных данных tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="0882a-183">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="0882a-184">Учебник о том, как tootransform данных с помощью фабрики данных Azure, см. [учебника: построение первые данные конвейера tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="0882a-184">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="0882a-185">Вы можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="0882a-185">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="0882a-186">Подробные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="0882a-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
