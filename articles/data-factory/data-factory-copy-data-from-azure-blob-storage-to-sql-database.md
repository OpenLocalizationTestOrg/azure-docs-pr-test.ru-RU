---
title: "Копирование данных из хранилища BLOB-объектов в Базу данных SQL Azure | Документация Майкрософт"
description: "В этом учебнике рассказывается, как использовать действие копирования в конвейере фабрики данных Azure для копирования данных из хранилища BLOB-объектов в базу данных SQL."
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
ms.openlocfilehash: 730140d15f4dec7ddc1280c2e4da1d247902fe4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="1b46f-104">Руководство. Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных</span><span class="sxs-lookup"><span data-stu-id="1b46f-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b46f-105">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1b46f-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="1b46f-106">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="1b46f-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="1b46f-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1b46f-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="1b46f-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1b46f-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="1b46f-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b46f-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="1b46f-110">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b46f-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="1b46f-111">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="1b46f-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="1b46f-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="1b46f-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="1b46f-113">В этом учебнике вы создадите фабрику данных с конвейером, чтобы скопировать данные из хранилища BLOB-объектов в базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1b46f-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="1b46f-114">Действие копирования перемещает данные в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="1b46f-114">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="1b46f-115">Это действие выполняется с помощью глобально доступной службы, обеспечивающей безопасное, надежное и масштабируемое копирование данных между разными хранилищами.</span><span class="sxs-lookup"><span data-stu-id="1b46f-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="1b46f-116">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1b46f-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="1b46f-117">Подробный обзор службы фабрики данных см. в статье [Общие сведения о службе фабрики данных Azure, службе интеграции данных в облаке](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1b46f-117">For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="1b46f-118">Предварительные требования для прохождения этого учебника</span><span class="sxs-lookup"><span data-stu-id="1b46f-118">Prerequisites for the tutorial</span></span>
<span data-ttu-id="1b46f-119">Для работы с этим учебником необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="1b46f-119">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="1b46f-120">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-120">**Azure subscription**.</span></span>  <span data-ttu-id="1b46f-121">Если у вас нет подписки, вы можете создать бесплатную пробную версию учетной записи всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1b46f-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1b46f-122">Дополнительные сведения см. в статье [Бесплатная пробная версия](http://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b46f-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="1b46f-123">**исходного**хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="1b46f-123">**Azure Storage Account**.</span></span> <span data-ttu-id="1b46f-124">В этом учебнике в качестве **источника** будет использоваться хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="1b46f-124">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="1b46f-125">в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="1b46f-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="1b46f-126">**База данных SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-126">**Azure SQL Database**.</span></span> <span data-ttu-id="1b46f-127">В этом учебнике используется база данных SQL Azure в качестве **конечного** хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="1b46f-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="1b46f-128">Если нет базы данных SQL Azure, которую можно использовать для изучения этого учебника, ознакомьтесь с разделом [Как создать и настроить базу данных SQL Azure](../sql-database/sql-database-get-started.md), чтобы создать такую базу данных.</span><span class="sxs-lookup"><span data-stu-id="1b46f-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="1b46f-129">**SQL Server 2012/2014 или Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="1b46f-130">Для создания образца базы данных и просмотра итоговых данных в базе данных используется SQL Server Management Studio или Visual Studio .</span><span class="sxs-lookup"><span data-stu-id="1b46f-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="1b46f-131">Получение имени и ключа учетной записи хранения BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="1b46f-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="1b46f-132">В ходе изучения этого учебника потребуются имя и ключ вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="1b46f-132">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="1b46f-133">Запишите **имя** и **ключ учетной записи** для своей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="1b46f-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="1b46f-134">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1b46f-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1b46f-135">Щелкните **Больше служб** в меню слева и выберите **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-135">Click **More services** on the left menu and select **Storage Accounts**.</span></span>

    !["Обзор" — "Учетные записи хранения"](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="1b46f-137">В колонке **Учетные записи хранения** выберите **учетную запись хранения Azure**, которая будет использоваться в ходе изучения этого учебника.</span><span class="sxs-lookup"><span data-stu-id="1b46f-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="1b46f-138">В разделе **Параметры** выберите ссылку **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="1b46f-139">Нажмите кнопку **Копировать** (изображение) рядом с текстовым полем **Имя учетной записи хранения**, вставьте скопированный текст, например, в текстовый файл, и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="1b46f-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="1b46f-140">Повторите предыдущий шаг для ключа **key1**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-140">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![Ключ доступа к хранилищу](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="1b46f-142">Закройте все колонки, нажав **X**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-142">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="1b46f-143">Получение имени сервера SQL, имени базы данных и имени пользователя</span><span class="sxs-lookup"><span data-stu-id="1b46f-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="1b46f-144">В ходе изучения этого учебника потребуются имена сервера Azure SQL Server, базы данных и пользователя.</span><span class="sxs-lookup"><span data-stu-id="1b46f-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="1b46f-145">Запишите имена **сервера**, **базы данных** и **пользователя** базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1b46f-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="1b46f-146">На **портале Azure** щелкните **Больше служб** слева и выберите **Базы данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="1b46f-147">В **колонке баз данных SQL** выберите **базу данных**, которую вы планируете использовать для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="1b46f-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="1b46f-148">Запишите **имя базы данных**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-148">Note down the **database name**.</span></span>  
3. <span data-ttu-id="1b46f-149">В колонке **База данных SQL** в разделе **Параметры** щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="1b46f-150">Запишите значения параметров **Имя сервера** и **Имя для входа администратора сервера**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="1b46f-151">Закройте все колонки, нажав **X**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-151">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="1b46f-152">Предоставление службам Azure доступа к серверу SQL</span><span class="sxs-lookup"><span data-stu-id="1b46f-152">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="1b46f-153">Убедитесь, что параметр **Разрешить доступ к службам Azure** имеет состояние **ВКЛ** для вашего сервера Azure SQL Server, чтобы служба фабрики данных могла иметь доступ к серверу Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1b46f-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="1b46f-154">Чтобы проверить и при необходимости включить этот параметр, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="1b46f-154">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="1b46f-155">Щелкните **Больше служб** слева и выберите **Серверы SQL**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-155">Click **More services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="1b46f-156">Выберите сервер и щелкните **Брандмауэр** в разделе **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="1b46f-157">В колонке **Параметры брандмауэра** щелкните **ВКЛ** для параметра **Разрешить доступ к службам Azure**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="1b46f-158">Закройте все колонки, нажав **X**.</span><span class="sxs-lookup"><span data-stu-id="1b46f-158">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="1b46f-159">Подготовка хранилища BLOB-объектов и базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="1b46f-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="1b46f-160">Теперь подготовьте хранилище больших двоичных объектов Azure и базу данных SQL Azure к изучению этого учебника, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1b46f-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="1b46f-161">Запустите Блокнот.</span><span class="sxs-lookup"><span data-stu-id="1b46f-161">Launch Notepad.</span></span> <span data-ttu-id="1b46f-162">Скопируйте следующий текст и сохраните его в файл **emp.txt** в папке **C:\ADFGetStarted** на диске.</span><span class="sxs-lookup"><span data-stu-id="1b46f-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="1b46f-163">При помощи таких инструментов, как [Azure Storage Explorer](http://storageexplorer.com/), создайте контейнер **adftutorial** и передайте файл **emp.txt** в этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="1b46f-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Обозреватель хранилищ Azure](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="1b46f-166">Используйте следующий скрипт SQL, чтобы создать таблицу **emp** в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1b46f-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="1b46f-167">**Если на вашем компьютере установлен SQL Server 2012 или 2014**, выполните инструкции в статье [Управление базой данных SQL Azure с помощью SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md), чтобы подключиться к серверу Azure SQL Server и запустить скрипт SQL.</span><span class="sxs-lookup"><span data-stu-id="1b46f-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> <span data-ttu-id="1b46f-168">В этой статье для настройки брандмауэра сервера Azure SQL Server используется [классический портал Azure](http://manage.windowsazure.com), а не [новый портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b46f-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="1b46f-169">Если клиенту не разрешен доступ к серверу Azure SQL Server, то следует настроить брандмауэр вашего сервера Azure SQL Server, чтобы разрешить доступ с вашей машины (IP-адрес).</span><span class="sxs-lookup"><span data-stu-id="1b46f-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="1b46f-170">В [этой статье](../sql-database/sql-database-configure-firewall-settings.md) описано, как настроить брандмауэр для сервера Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1b46f-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="1b46f-171">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="1b46f-171">Create a data factory</span></span>
<span data-ttu-id="1b46f-172">Необходимые условия выполнены.</span><span class="sxs-lookup"><span data-stu-id="1b46f-172">You have completed the prerequisites.</span></span> <span data-ttu-id="1b46f-173">Для создания фабрики данных можно использовать один из приведенных ниже способов.</span><span class="sxs-lookup"><span data-stu-id="1b46f-173">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="1b46f-174">Выберите в раскрывающемся списке в верхней части страницы один из вариантов или щелкните одну из следующих ссылок, чтобы изучить руководство.</span><span class="sxs-lookup"><span data-stu-id="1b46f-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="1b46f-175">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="1b46f-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="1b46f-176">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1b46f-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="1b46f-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1b46f-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="1b46f-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b46f-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="1b46f-179">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b46f-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="1b46f-180">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="1b46f-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="1b46f-181">API .NET</span><span class="sxs-lookup"><span data-stu-id="1b46f-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="1b46f-182">Описанный в этом руководстве конвейер данных копирует данные из исходного хранилища данных в целевое.</span><span class="sxs-lookup"><span data-stu-id="1b46f-182">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="1b46f-183">Он не преобразовывает входные данные в выходные.</span><span class="sxs-lookup"><span data-stu-id="1b46f-183">It does not transform input data to produce output data.</span></span> <span data-ttu-id="1b46f-184">Инструкции по преобразованию данных с помощью фабрики данных Azure см. в [учебнике по созданию первого конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="1b46f-184">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="1b46f-185">Можно объединить в цепочку два действия (выполнить одно действие вслед за другим), настроив выходной набор данных одного действия как входной набор данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="1b46f-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="1b46f-186">Подробные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="1b46f-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
