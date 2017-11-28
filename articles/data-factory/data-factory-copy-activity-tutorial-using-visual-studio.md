---
title: "Руководство. Создание конвейера с действием копирования с помощью Visual Studio | Документация Майкрософт"
description: "С помощью этого руководства вы, используя Visual Studio, создадите конвейер фабрики данных Azure с действием копирования."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: f90b158e45a3679210685765b23c8299eb76ed50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="199cd-103">Руководство. Создание конвейера с действием копирования с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="199cd-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="199cd-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="199cd-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="199cd-105">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="199cd-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="199cd-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="199cd-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="199cd-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="199cd-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="199cd-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="199cd-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="199cd-109">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="199cd-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="199cd-110">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="199cd-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="199cd-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="199cd-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="199cd-112">В этом руководстве показано, как создать фабрику данных c конвейером, который копирует данные из хранилища BLOB-объектов Azure, с помощью Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="199cd-112">In this article, you learn how to use the Microsoft Visual Studio to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="199cd-113">Если вы еще не работали с фабрикой данных Azure, перед выполнением действий, описанных в этом руководстве, ознакомьтесь со статьей [Введение в фабрику данных Azure](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="199cd-114">В этом руководстве описывается создание конвейера с одним действием — действием копирования.</span><span class="sxs-lookup"><span data-stu-id="199cd-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="199cd-115">Действие копирования копирует данные из поддерживаемого хранилища данных в поддерживаемое хранилище данных-приемник.</span><span class="sxs-lookup"><span data-stu-id="199cd-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="199cd-116">Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="199cd-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="199cd-117">Это действие выполняется с помощью глобально доступной службы, обеспечивающей безопасное, надежное и масштабируемое копирование данных между разными хранилищами.</span><span class="sxs-lookup"><span data-stu-id="199cd-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="199cd-118">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="199cd-119">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="199cd-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="199cd-120">Два действия можно объединить в цепочку (выполнить одно действие вслед за другим), настроив выходной набор данных одного действия как входной набор данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="199cd-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="199cd-121">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="199cd-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="199cd-122">В этом руководстве конвейер данных копирует данные из исходного хранилища данных в целевое.</span><span class="sxs-lookup"><span data-stu-id="199cd-122">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="199cd-123">Инструкции по преобразованию данных с помощью фабрики данных Azure см. в [руководстве по созданию конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-123">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="199cd-124">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="199cd-124">Prerequisites</span></span>
1. <span data-ttu-id="199cd-125">Прочтите [обзорную статью](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) и выполните **предварительные требования** .</span><span class="sxs-lookup"><span data-stu-id="199cd-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete the **prerequisite** steps.</span></span>       
2. <span data-ttu-id="199cd-126">Создавать экземпляры фабрики данных может пользователь с ролью [Участник фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) на уровне подписки или группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="199cd-126">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
3. <span data-ttu-id="199cd-127">На вашем компьютере должны быть установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="199cd-127">You must have the following installed on your computer:</span></span> 
   * <span data-ttu-id="199cd-128">Visual Studio 2013 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="199cd-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="199cd-129">Загрузите пакет SDK Azure для Visual Studio 2013 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="199cd-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="199cd-130">Перейдите на [cтраницу загрузки Azure](https://azure.microsoft.com/downloads/) и щелкните **VS 2013** или **VS2015** в разделе **.NET**.</span><span class="sxs-lookup"><span data-stu-id="199cd-130">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="199cd-131">Скачайте последнюю версию подключаемого модуля фабрики данных Azure для Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) или [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="199cd-131">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="199cd-132">Вы также можете обновить подключаемый модуль, выполнив следующие действия. В меню выберите **Сервис** -> **Расширения и обновления** -> **В сети** -> **Галерея Visual Studio** -> **Microsoft Azure Data Factory Tools for Visual Studio**(Средства фабрики данных Microsoft Azure для Visual Studio) -> **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="199cd-132">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="199cd-133">Действия</span><span class="sxs-lookup"><span data-stu-id="199cd-133">Steps</span></span>
<span data-ttu-id="199cd-134">Ниже приведены шаги, которые вы выполните в процессе работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="199cd-134">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="199cd-135">Создайте в этой фабрике данных **связанные службы**.</span><span class="sxs-lookup"><span data-stu-id="199cd-135">Create **linked services** in the data factory.</span></span> <span data-ttu-id="199cd-136">На этом этапе вы создадите две связанные службы — службу хранилища Azure и базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="199cd-137">Связанная служба хранилища Azure связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-137">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="199cd-138">Вы создали контейнер и отправили данные в эту учетную запись хранения в ходе выполнения предварительных [требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-138">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="199cd-139">Связанная служба SQL Azure связывает базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-139">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="199cd-140">В этой базе данных хранятся данные, скопированные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="199cd-140">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="199cd-141">Вы создали таблицу SQL в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="199cd-142">Создайте в фабрике данных входные и выходные **наборы данных**.</span><span class="sxs-lookup"><span data-stu-id="199cd-142">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="199cd-143">Связанная служба хранилища Azure указывает строку подключения, которую фабрика данных использует во время выполнения, чтобы подключиться к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-143">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="199cd-144">А входной набор данных больших двоичных объектов определяет контейнер и папку с входными данными.</span><span class="sxs-lookup"><span data-stu-id="199cd-144">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="199cd-145">Аналогичным образом связанная служба базы данных SQL Azure указывает строку подключения, которую служба фабрики данных использует во время выполнения, чтобы подключиться к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-145">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="199cd-146">А выходной набор данных таблицы SQL определяет таблицу в базе данных, в которую копируются данные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="199cd-146">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
3. <span data-ttu-id="199cd-147">Создайте **конвейер** в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-147">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="199cd-148">На этом этапе вы создадите конвейер с действием копирования.</span><span class="sxs-lookup"><span data-stu-id="199cd-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="199cd-149">Действие копирования копирует данные из большого двоичного объекта из хранилища BLOB-объектов Azure в таблицу в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-149">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="199cd-150">Его можно использовать, чтобы копировать данные из любого поддерживаемого источника в любое расположение.</span><span class="sxs-lookup"><span data-stu-id="199cd-150">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="199cd-151">Список поддерживаемых хранилищ данных см. в [этом разделе](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="199cd-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="199cd-152">Создайте **фабрику данных** Azure при развертывании сущностей фабрики данных (связанные службы, наборы данных, таблицы и конвейеры).</span><span class="sxs-lookup"><span data-stu-id="199cd-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="199cd-153">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="199cd-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="199cd-154">Запустите **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="199cd-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="199cd-155">Щелкните **Файл**, наведите указатель мыши на пункт **Создать** и щелкните **Проект**.</span><span class="sxs-lookup"><span data-stu-id="199cd-155">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="199cd-156">Откроется диалоговое окно **Новый проект** .</span><span class="sxs-lookup"><span data-stu-id="199cd-156">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="199cd-157">В диалоговом окне **Новый проект** выберите шаблон **DataFactory** и щелкните **Empty Data Factory Project** (Пустой проект фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="199cd-157">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Диалоговое окно "Новый проект"](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="199cd-159">Укажите имя проекта, расположение и имя решения и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="199cd-159">Specify the name of the project, location for the solution, and name of the solution, and then click **OK**.</span></span>
   
    ![Обозреватель решений](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="199cd-161">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="199cd-161">Create linked services</span></span>
<span data-ttu-id="199cd-162">Связанная служба в фабрике данных связывает хранилища данных и службы вычислений с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-162">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="199cd-163">В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="199cd-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="199cd-164">Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище).</span><span class="sxs-lookup"><span data-stu-id="199cd-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="199cd-165">Вы создадите две связанные службы — AzureStorage и AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="199cd-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="199cd-166">Связанная служба хранилища Azure связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-166">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="199cd-167">В этой учетной записи хранения вы создали контейнер и отправили в нее данные в ходе выполнения предварительных [требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-167">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="199cd-168">Связанная служба Azure SQL связывает базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-168">Azure SQL linked service links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="199cd-169">В этой базе данных хранятся данные, скопированные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="199cd-169">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="199cd-170">Вы создали пустую таблицу в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-170">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="199cd-171">Связанные службы связывают хранилища данных или службы вычислений с фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-171">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="199cd-172">См. список [поддерживаемых хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) для всех источников и приемников, которые поддерживаются действием копирования.</span><span class="sxs-lookup"><span data-stu-id="199cd-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="199cd-173">См. список [связанных служб вычислений](data-factory-compute-linked-services.md), поддерживаемых фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-173">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span> <span data-ttu-id="199cd-174">В этом руководстве не рассматривается использование служб вычислений.</span><span class="sxs-lookup"><span data-stu-id="199cd-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-the-azure-storage-linked-service"></a><span data-ttu-id="199cd-175">Создание связанных служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="199cd-175">Create the Azure Storage linked service</span></span>
1. <span data-ttu-id="199cd-176">В **обозревателе решений** щелкните правой кнопкой мыши **Связанные службы**, наведите указатель на пункт **Добавить** и выберите **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="199cd-176">In **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="199cd-177">В диалоговом окне **Добавление нового элемента** выберите в списке пункт **Azure Storage Linked Service** (Связанная служба хранилища Azure) и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="199cd-177">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span> 
   
    ![Новая связанная служба](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="199cd-179">Замените `<accountname>` и `<accountkey>`* именем и ключом учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-179">Replace `<accountname>` and `<accountkey>`* with the name of your Azure storage account and its key.</span></span> 
   
    ![Связанная служба хранилища Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="199cd-181">Сохраните файл **AzureStorageLinkedService1.json** .</span><span class="sxs-lookup"><span data-stu-id="199cd-181">Save the **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="199cd-182">Дополнительные сведения о свойствах JSON см. в статье о [соединителе хранилища BLOB-объектов Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="199cd-182">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-the-azure-sql-linked-service"></a><span data-ttu-id="199cd-183">Создание связанной службы SQL Azure</span><span class="sxs-lookup"><span data-stu-id="199cd-183">Create the Azure SQL linked service</span></span>
1. <span data-ttu-id="199cd-184">Щелкните правой кнопкой мыши узел **Связанные службы** в **обозревателе решений**, выберите **Добавить** и щелкните **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="199cd-184">Right-click on **Linked Services** node in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="199cd-185">На этот раз выберите **Azure SQL Linked Service** (Связанная служба SQL Azure) и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="199cd-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="199cd-186">В файле **AzureSqlLinkedService1.json** замените `<servername>`, `<databasename>`, `<username@servername>` и `<password>` именем сервера Azure SQL Server, именем базы данных, именем учетной записи пользователя и паролем соответственно.</span><span class="sxs-lookup"><span data-stu-id="199cd-186">In the **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="199cd-187">Сохраните файл **AzureSqlLinkedService1.json** .</span><span class="sxs-lookup"><span data-stu-id="199cd-187">Save the **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="199cd-188">Дополнительные сведения об этих свойствах JSON см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="199cd-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="199cd-189">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="199cd-189">Create datasets</span></span>
<span data-ttu-id="199cd-190">На предыдущем шаге вы создали связанные службы, связывающие учетную запись хранения Azure и базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-190">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="199cd-191">На этом шаге будут определены два набора данных, InputDataset и OutputDataset, представляющие входные и выходные данные в хранилищах данных, на которые ссылаются службы AzureStorageLinkedService1 и AzureSqlLinkedService1 соответственно.</span><span class="sxs-lookup"><span data-stu-id="199cd-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="199cd-192">Связанная служба хранилища Azure указывает строку подключения, которую фабрика данных использует во время выполнения, чтобы подключиться к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-192">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="199cd-193">А входной набор данных больших двоичных объектов (InputDataset) определяет контейнер и папку с входными данными.</span><span class="sxs-lookup"><span data-stu-id="199cd-193">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="199cd-194">Аналогичным образом связанная служба базы данных SQL Azure указывает строку подключения, которую служба фабрики данных использует во время выполнения, чтобы подключиться к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-194">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="199cd-195">А выходной набор данных таблицы SQL (OututDataset) определяет таблицу в базе данных, в которую копируются данные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="199cd-195">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="199cd-196">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="199cd-196">Create input dataset</span></span>
<span data-ttu-id="199cd-197">На этом шаге создается набор данных с именем InputDataset. Он указывает на файл большого двоичного объекта (emp.txt) в корневой папке контейнера больших двоичных объектов в службе хранилища Azure, которая представлена связанной службой AzureStorageLinkedService1.</span><span class="sxs-lookup"><span data-stu-id="199cd-197">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="199cd-198">Если не указать значение fileName (или пропустить его), данные из всех больших двоичных объектов в папке входных данных копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="199cd-198">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="199cd-199">В этом руководстве вы укажете значение параметра fileName.</span><span class="sxs-lookup"><span data-stu-id="199cd-199">In this tutorial, you specify a value for the fileName.</span></span> 

<span data-ttu-id="199cd-200">Здесь используется термин "таблицы", а не "наборы данных".</span><span class="sxs-lookup"><span data-stu-id="199cd-200">Here, you use the term "tables" rather than "datasets".</span></span> <span data-ttu-id="199cd-201">Таблица — это прямоугольный набор данных. Это единственный тип набора данных, который сейчас поддерживается.</span><span class="sxs-lookup"><span data-stu-id="199cd-201">A table is a rectangular dataset and is the only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="199cd-202">Щелкните правой кнопкой мыши **Таблицы** в **обозревателе решений**, выберите **Добавить** и щелкните **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="199cd-202">Right-click **Tables** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="199cd-203">В диалоговом окне **Добавление нового элемента** выберите **BLOB-объект Azure** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="199cd-203">In the **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="199cd-204">Замените текст JSON приведенным далее текстом и сохраните файл **AzureBlobLocation1.json** .</span><span class="sxs-lookup"><span data-stu-id="199cd-204">Replace the JSON text with the following text and save the **AzureBlobLocation1.json** file.</span></span> 

  ```json   
  {
    "name": "InputDataset",
    "properties": {
      "structure": [
        {
          "name": "FirstName",
          "type": "String"
        },
        {
          "name": "LastName",
          "type": "String"
        }
      ],
      "type": "AzureBlob",
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
        "format": {
          "type": "TextFormat",
          "columnDelimiter": ","
        }
      },
      "external": true,
      "availability": {
        "frequency": "Hour",
        "interval": 1
      }
    }
  }
  ``` 
    <span data-ttu-id="199cd-205">В следующей таблице приведены описания свойств JSON, используемых в этом фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="199cd-205">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="199cd-206">Свойство</span><span class="sxs-lookup"><span data-stu-id="199cd-206">Property</span></span> | <span data-ttu-id="199cd-207">Описание</span><span class="sxs-lookup"><span data-stu-id="199cd-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="199cd-208">type</span><span class="sxs-lookup"><span data-stu-id="199cd-208">type</span></span> | <span data-ttu-id="199cd-209">Для свойства типа задано значение **AzureBlob**, так как данные хранятся в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-209">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="199cd-210">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="199cd-210">linkedServiceName</span></span> | <span data-ttu-id="199cd-211">Ссылается на созданную ранее службу **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="199cd-211">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="199cd-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="199cd-212">folderPath</span></span> | <span data-ttu-id="199cd-213">Определяет **контейнер** больших двоичных объектов и **папку**, которая содержит входные большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="199cd-213">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="199cd-214">В этом руководстве adftutorial — это контейнер больших двоичных объектов, а созданная папка является корневой.</span><span class="sxs-lookup"><span data-stu-id="199cd-214">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="199cd-215">fileName</span><span class="sxs-lookup"><span data-stu-id="199cd-215">fileName</span></span> | <span data-ttu-id="199cd-216">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="199cd-216">This property is optional.</span></span> <span data-ttu-id="199cd-217">Если это свойство не указано, выбираются все файлы из папки folderPath.</span><span class="sxs-lookup"><span data-stu-id="199cd-217">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="199cd-218">В этом руководстве для свойства fileName указывается значение **emp.txt**, чтобы обрабатывался только этот файл.</span><span class="sxs-lookup"><span data-stu-id="199cd-218">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="199cd-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="199cd-219">format -> type</span></span> |<span data-ttu-id="199cd-220">Входной файл имеет текстовый формат, поэтому укажите значение **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="199cd-220">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="199cd-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="199cd-221">columnDelimiter</span></span> | <span data-ttu-id="199cd-222">Столбцы во входном файле разделяются **запятыми (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="199cd-222">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="199cd-223">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="199cd-223">frequency/interval</span></span> | <span data-ttu-id="199cd-224">Для свойства frequency задано значение **Hour**, а для свойства interval — значение **1**. Это означает, что срезы входных данных будут создаваться **каждый час**.</span><span class="sxs-lookup"><span data-stu-id="199cd-224">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="199cd-225">Иными словами, служба фабрики данных будет искать входные данные в корневой папке указанного контейнера BLOB-объектов (**adftutorial**) каждый час.</span><span class="sxs-lookup"><span data-stu-id="199cd-225">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="199cd-226">Поиск данных осуществляется в пределах времени начала и времени окончания для конвейера, но не перед этим периодом или после него.</span><span class="sxs-lookup"><span data-stu-id="199cd-226">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="199cd-227">external</span><span class="sxs-lookup"><span data-stu-id="199cd-227">external</span></span> | <span data-ttu-id="199cd-228">Это свойство имеет значение **true**, если этот конвейер не создает данные.</span><span class="sxs-lookup"><span data-stu-id="199cd-228">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="199cd-229">В этом руководстве входные данные находятся в файле emp.txt, который не создается этим конвейером, поэтому мы присвоим этому свойству значение true.</span><span class="sxs-lookup"><span data-stu-id="199cd-229">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="199cd-230">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="199cd-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="199cd-231">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="199cd-231">Create output dataset</span></span>
<span data-ttu-id="199cd-232">На этом этапе мы создадим выходной набор данных с именем **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="199cd-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="199cd-233">Этот набор данных указывает на таблицу SQL в базе данных SQL Azure (представлена значением **AzureSqlLinkedService1**).</span><span class="sxs-lookup"><span data-stu-id="199cd-233">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="199cd-234">Снова щелкните правой кнопкой мыши **Таблицы** в **обозревателе решений**, выберите **Добавить** и щелкните **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="199cd-234">Right-click **Tables** in the **Solution Explorer** again, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="199cd-235">В диалоговом окне **Добавление нового элемента** выберите **SQL Azure**  и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="199cd-235">In the **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="199cd-236">Замените текст JSON приведенным далее кодом JSON и сохраните файл **AzureSqlTableLocation1.json** .</span><span class="sxs-lookup"><span data-stu-id="199cd-236">Replace the JSON text with the following JSON and save the **AzureSqlTableLocation1.json** file.</span></span>

  ```json
    {
     "name": "OutputDataset",
     "properties": {
       "structure": [
         {
           "name": "FirstName",
           "type": "String"
         },
         {
           "name": "LastName",
           "type": "String"
         }
       ],
       "type": "AzureSqlTable",
       "linkedServiceName": "AzureSqlLinkedService1",
       "typeProperties": {
         "tableName": "emp"
       },
       "availability": {
         "frequency": "Hour",
         "interval": 1
       }
     }
    }
    ```
    <span data-ttu-id="199cd-237">В следующей таблице приведены описания свойств JSON, используемых в этом фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="199cd-237">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="199cd-238">Свойство</span><span class="sxs-lookup"><span data-stu-id="199cd-238">Property</span></span> | <span data-ttu-id="199cd-239">Описание</span><span class="sxs-lookup"><span data-stu-id="199cd-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="199cd-240">type</span><span class="sxs-lookup"><span data-stu-id="199cd-240">type</span></span> | <span data-ttu-id="199cd-241">Свойство type имеет значение **AzureSqlTable**, так как данные копируются в таблицу в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-241">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="199cd-242">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="199cd-242">linkedServiceName</span></span> | <span data-ttu-id="199cd-243">Ссылается на созданную ранее службу **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="199cd-243">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="199cd-244">tableName</span><span class="sxs-lookup"><span data-stu-id="199cd-244">tableName</span></span> | <span data-ttu-id="199cd-245">Указывает **таблицу**, в которую копируются данные.</span><span class="sxs-lookup"><span data-stu-id="199cd-245">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="199cd-246">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="199cd-246">frequency/interval</span></span> | <span data-ttu-id="199cd-247">Для свойства frequency задано значение **Hour**, а для interval — **1**. Это означает, что срезы выходных данных создаются **каждый час** в пределах времени начала и времени окончания для конвейера, но не перед этим периодом или после него.</span><span class="sxs-lookup"><span data-stu-id="199cd-247">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="199cd-248">В таблице emp в базе данных есть три столбца: **ID**, **FirstName** и **LastName**.</span><span class="sxs-lookup"><span data-stu-id="199cd-248">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="199cd-249">ID — это столбец для идентификаторов, поэтому здесь вам нужно указать только значения **FirstName** и **LastName**.</span><span class="sxs-lookup"><span data-stu-id="199cd-249">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="199cd-250">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="199cd-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="199cd-251">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="199cd-251">Create pipeline</span></span>
<span data-ttu-id="199cd-252">На этом этапе вы создадите конвейер с **действием копирования**, которое использует **InputDataset** в качестве входных данных и **OutputDataset** в качестве выходных.</span><span class="sxs-lookup"><span data-stu-id="199cd-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="199cd-253">Сейчас на основе этого набора настраивается расписание.</span><span class="sxs-lookup"><span data-stu-id="199cd-253">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="199cd-254">В этом руководстве выходной набор данных создает срез раз в час.</span><span class="sxs-lookup"><span data-stu-id="199cd-254">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="199cd-255">Для конвейера настроено время начала и время окончания с разницей в сутки.</span><span class="sxs-lookup"><span data-stu-id="199cd-255">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="199cd-256">Таким образом, конвейер создает 24 среза для выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-256">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="199cd-257">Щелкните правой кнопкой мыши **Конвейеры** в **обозревателе решений**, выберите **Добавить** и щелкните **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="199cd-257">Right-click **Pipelines** in the **Solution Explorer**, point to **Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="199cd-258">В диалоговом окне **Добавление нового элемента** выберите **Конвейер копирования данных** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="199cd-258">Select **Copy Data Pipeline** in the **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="199cd-259">Замените JSON приведенным далее кодом JSON и сохраните файл **CopyActivity1.json** .</span><span class="sxs-lookup"><span data-stu-id="199cd-259">Replace the JSON with the following JSON and save the **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob to Azure SQL table",
       "activities": [
         {
           "name": "CopyFromBlobToSQL",
           "type": "Copy",
           "inputs": [
             {
               "name": "InputDataset"
             }
           ],
           "outputs": [
             {
               "name": "OutputDataset"
             }
           ],
           "typeProperties": {
             "source": {
               "type": "BlobSource"
             },
             "sink": {
               "type": "SqlSink",
               "writeBatchSize": 10000,
               "writeBatchTimeout": "60:00:00"
             }
           },
           "Policy": {
             "concurrency": 1,
             "executionPriorityOrder": "NewestFirst",
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="199cd-260">В разделе действий доступно только одно действие, параметр **type** которого имеет значение **Copy**.</span><span class="sxs-lookup"><span data-stu-id="199cd-260">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="199cd-261">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-261">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="199cd-262">В решениях фабрики данных можно также использовать [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="199cd-263">Для этого действия параметру input присвоено значение **InputDataset**, а параметру output — значение **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="199cd-263">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="199cd-264">В разделе **typeProperties** в качестве типа источника указано **BlobSource**, а в качестве типа приемника — **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="199cd-264">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="199cd-265">Список хранилищ данных, поддерживаемых действием копирования в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="199cd-265">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="199cd-266">Чтобы узнать, как использовать конкретное хранилище данных в качестве источника или приемника, щелкните ссылку в таблице.</span><span class="sxs-lookup"><span data-stu-id="199cd-266">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="199cd-267">Замените значение свойства **start** текущей датой, а значение свойства **end** — датой следующего дня.</span><span class="sxs-lookup"><span data-stu-id="199cd-267">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="199cd-268">Можно указать только часть даты и пропустить временную часть указанной даты и времени.</span><span class="sxs-lookup"><span data-stu-id="199cd-268">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="199cd-269">Например, 2016-02-03, что эквивалентно 2016-02-03T00:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="199cd-269">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="199cd-270">Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="199cd-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="199cd-271">Например, 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="199cd-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="199cd-272">Время **окончания** указывать не обязательно, однако в этом примере мы будем его использовать.</span><span class="sxs-lookup"><span data-stu-id="199cd-272">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="199cd-273">Если не указать значение свойства **end**, оно вычисляется по формуле "**время начала + 48 часов**".</span><span class="sxs-lookup"><span data-stu-id="199cd-273">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="199cd-274">Чтобы запустить конвейер в течение неопределенного срока, укажите значение **9999-09-09** в качестве значения свойства **end**.</span><span class="sxs-lookup"><span data-stu-id="199cd-274">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="199cd-275">В примере выше получено 24 среза данных, так как они создаются каждый час.</span><span class="sxs-lookup"><span data-stu-id="199cd-275">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="199cd-276">Описание свойств JSON в определении конвейера см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="199cd-277">Описание свойств JSON в определении действия копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="199cd-278">Описание свойств JSON, поддерживаемых BlobSource, см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="199cd-279">Описание свойств JSON, поддерживаемых SqlSink, см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="199cd-280">Публикация и развертывание сущностей фабрики данных</span><span class="sxs-lookup"><span data-stu-id="199cd-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="199cd-281">На этом этапе вы опубликуете созданные ранее сущности фабрики данных (связанные службы, наборы данных и конвейеры).</span><span class="sxs-lookup"><span data-stu-id="199cd-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="199cd-282">Вы также укажете имя новой фабрики данных, которая будет создана для хранения этих сущностей.</span><span class="sxs-lookup"><span data-stu-id="199cd-282">You also specify the name of the new data factory to be created to hold these entities.</span></span>  

1. <span data-ttu-id="199cd-283">В обозревателе решений щелкните проект правой кнопкой мыши и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="199cd-283">Right-click project in the Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="199cd-284">Когда отобразится диалоговое окно **Вход в учетную запись Майкрософт**, введите данные учетной записи с подпиской Azure и нажмите кнопку **Войти**.</span><span class="sxs-lookup"><span data-stu-id="199cd-284">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="199cd-285">Вы должны увидеть следующее диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="199cd-285">You should see the following dialog box:</span></span>
   
   ![Диалоговое окно "Опубликовать"](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="199cd-287">На странице Configure data factory (Настройка фабрики данных) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="199cd-287">In the Configure data factory page, do the following steps:</span></span> 
   
   1. <span data-ttu-id="199cd-288">Выберите **Создать новую фабрику данных** .</span><span class="sxs-lookup"><span data-stu-id="199cd-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="199cd-289">Введите **VSTutorialFactory** в качестве **имени** фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="199cd-290">Имя фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="199cd-290">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="199cd-291">Если во время публикации отобразится ошибка об имени фабрики данных, измените имя фабрики данных (например, на ваше_имяVSTutorialFactory) и повторите попытку публикации.</span><span class="sxs-lookup"><span data-stu-id="199cd-291">If you receive an error about the name of data factory when publishing, change the name of the data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="199cd-292">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="199cd-293">Выберите свою подписку в Azure в поле **Подписка** .</span><span class="sxs-lookup"><span data-stu-id="199cd-293">Select your Azure subscription for the **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="199cd-294">Если подписки не отображаются, проверьте, выполнен ли вход с использованием учетной записи администратора или соадминистратора подписки.</span><span class="sxs-lookup"><span data-stu-id="199cd-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="199cd-295">Выберите **группу ресурсов** для создаваемой фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-295">Select the **resource group** for the data factory to be created.</span></span> 
   5. <span data-ttu-id="199cd-296">Выберите **регион** для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-296">Select the **region** for the data factory.</span></span> <span data-ttu-id="199cd-297">В раскрывающемся списке отображаются только те регионы, которые поддерживаются службой фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-297">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   6. <span data-ttu-id="199cd-298">Нажмите кнопку **Далее**, чтобы перейти на страницу **Publish Items** (Публикация элементов).</span><span class="sxs-lookup"><span data-stu-id="199cd-298">Click **Next** to switch to the **Publish Items** page.</span></span>
      
       ![Страница Configure data factory (Настройка фабрики данных)](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="199cd-300">На странице **Publish Items** (Публикация элементов) выберите все сущности фабрик данных и нажмите кнопку **Далее**, чтобы перейти на страницу **Сводка**.</span><span class="sxs-lookup"><span data-stu-id="199cd-300">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>
   
   ![Страница Publish items (Публикация элементов)](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="199cd-302">Просмотрите сводку и нажмите кнопку **Далее** для запуска процесса развертывания и просмотра **состояния развертывания**.</span><span class="sxs-lookup"><span data-stu-id="199cd-302">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>
   
   ![Страница "Сводка публикации"](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="199cd-304">На странице **Состояние развертывания** вы увидите состояние процесса развертывания.</span><span class="sxs-lookup"><span data-stu-id="199cd-304">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="199cd-305">После завершения развертывания нажмите кнопку "Готово".</span><span class="sxs-lookup"><span data-stu-id="199cd-305">Click Finish after the deployment is done.</span></span>
 
   ![Страница "Состояние развертывания"](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="199cd-307">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="199cd-307">Note the following points:</span></span> 

* <span data-ttu-id="199cd-308">Если появится сообщение об ошибке: "Подписка не зарегистрирована для использования пространства имен Microsoft.DataFactory", выполните одно из следующих действий и повторите попытку публикации.</span><span class="sxs-lookup"><span data-stu-id="199cd-308">If you receive the error: "This subscription is not registered to use namespace Microsoft.DataFactory", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="199cd-309">В Azure PowerShell выполните следующую команду, чтобы зарегистрировать поставщик фабрики данных Azure:</span><span class="sxs-lookup"><span data-stu-id="199cd-309">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="199cd-310">Чтобы убедиться, что поставщик фабрики данных зарегистрирован, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="199cd-310">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="199cd-311">Войдите на [портал Azure](https://portal.azure.com) с использованием подписки Azure и откройте колонку фабрики данных или создайте на портале фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-311">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="199cd-312">Поставщик будет зарегистрирован автоматически.</span><span class="sxs-lookup"><span data-stu-id="199cd-312">This action automatically registers the provider for you.</span></span>
* <span data-ttu-id="199cd-313">В будущем имя фабрики данных может быть зарегистрировано в качестве DNS-имени и, следовательно, стать отображаемым.</span><span class="sxs-lookup"><span data-stu-id="199cd-313">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="199cd-314">Чтобы создать экземпляры фабрики данных, необходимо быть администратором или соадминистратором подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-314">To create Data Factory instances, you need to be a admin/co-admin of the Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="199cd-315">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="199cd-315">Monitor pipeline</span></span>
<span data-ttu-id="199cd-316">Перейдите на домашнюю страницу своей фабрики:</span><span class="sxs-lookup"><span data-stu-id="199cd-316">Navigate to the home page for your data factory:</span></span>

1. <span data-ttu-id="199cd-317">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="199cd-317">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="199cd-318">В меню слева щелкните **Больше служб** и выберите **Фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="199cd-318">Click **More services** on the left menu, and click **Data factories**.</span></span>

    ![Обзор фабрик данных](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="199cd-320">Начните вводить имя фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-320">Start typing the name of your data factory.</span></span>

    ![Имя фабрики данных](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="199cd-322">Щелкните свою фабрику данных в списке результатов, чтобы увидеть ее домашнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="199cd-322">Click your data factory in the results list to see the home page for your data factory.</span></span>

    ![Домашняя страница фабрики данных](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="199cd-324">Следуйте инструкциям из раздела [Отслеживание конвейера](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) для мониторинга конвейера и баз данных, созданных при работе с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="199cd-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="199cd-325">Сейчас Visual Studio не поддерживает мониторинг конвейеров фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="199cd-326">Сводка</span><span class="sxs-lookup"><span data-stu-id="199cd-326">Summary</span></span>
<span data-ttu-id="199cd-327">В этом учебнике вы создали фабрику данных Azure для копирования данных из большого двоичного объекта Azure в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-327">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="199cd-328">Вы использовали Visual Studio для создания фабрики данных, связанных служб, наборов данных и конвейера.</span><span class="sxs-lookup"><span data-stu-id="199cd-328">You used Visual Studio to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="199cd-329">Вот обобщенные действия, которые вы выполнили в этом руководстве:</span><span class="sxs-lookup"><span data-stu-id="199cd-329">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="199cd-330">Создание **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="199cd-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="199cd-331">Создание **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="199cd-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="199cd-332">**Служба хранилища Azure** — связанная служба для связи с учетной записью хранения Azure, которая содержит входные данные.</span><span class="sxs-lookup"><span data-stu-id="199cd-332">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="199cd-333">**SQL Azure** — связанная служба для связи с базой данных SQL Azure, которая содержит выходные данные.</span><span class="sxs-lookup"><span data-stu-id="199cd-333">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="199cd-334">Создание **наборов данных**, описывающих входные и выходные данные для конвейеров.</span><span class="sxs-lookup"><span data-stu-id="199cd-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="199cd-335">Создание **конвейера** с **BlobSource** в качестве источника и **SqlSink** в качестве приемника с помощью **действия копирования**.</span><span class="sxs-lookup"><span data-stu-id="199cd-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="199cd-336">Инструкции по преобразованию данных с помощью действия Hive HDInsight см. в [руководстве по созданию первого конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-336">To see how to use a HDInsight Hive Activity to transform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="199cd-337">Можно объединить в цепочку два действия (выполнить одно действие вслед за другим), настроив выходной набор данных одного действия как входной набор данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="199cd-337">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="199cd-338">Подробные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="199cd-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="199cd-339">Просмотр фабрик данных в обозревателе серверов</span><span class="sxs-lookup"><span data-stu-id="199cd-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="199cd-340">В этом разделе описывается, как просматривать фабрики данных в подписке Azure и создать проект Visual Studio на основе имеющейся фабрики данных с помощью обозревателя серверов в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="199cd-340">This section describes how to use the Server Explorer in Visual Studio to view all the data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="199cd-341">В **Visual Studio** щелкните **Вид** в меню и выберите **Обозреватель серверов**.</span><span class="sxs-lookup"><span data-stu-id="199cd-341">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="199cd-342">В окне обозревателя серверов разверните элементы **Azure** и **Фабрика данных**.</span><span class="sxs-lookup"><span data-stu-id="199cd-342">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="199cd-343">Когда отобразится окно **Выполните вход в Visual Studio**, введите данные **учетной записи**, связанной с вашей подпиской Azure, и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="199cd-343">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="199cd-344">Введите **пароль** и нажмите кнопку **Войти**.</span><span class="sxs-lookup"><span data-stu-id="199cd-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="199cd-345">Visual Studio пытается получить сведения обо всех фабриках данных Azure в подписке.</span><span class="sxs-lookup"><span data-stu-id="199cd-345">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="199cd-346">В окне **Data Factory Task List** (Список задач фабрики данных) будет отображено состояние операции.</span><span class="sxs-lookup"><span data-stu-id="199cd-346">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Обозреватель серверов](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="199cd-348">Создание проекта Visual Studio для имеющейся фабрики данных</span><span class="sxs-lookup"><span data-stu-id="199cd-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="199cd-349">Щелкните фабрику данных правой кнопкой мыши в обозревателе серверов и выберите пункт **Export Data Factory to New Project** (Экспорт фабрики данных в новый проект), чтобы создать проект Visual Studio на основе имеющейся фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-349">Right-click a data factory in Server Explorer, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![Экспорт фабрики данных для проекта VS](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="199cd-351">Обновление средств фабрик данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="199cd-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="199cd-352">Чтобы обновить средства фабрики данных Azure для Visual Studio, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="199cd-352">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="199cd-353">Щелкните в меню пункт **Сервис** и выберите **Расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="199cd-353">Click **Tools** on the menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="199cd-354">Выберите пункт **Обновления** слева, а затем — **Галерея Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="199cd-354">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="199cd-355">Выберите **Azure Data Factory tools for Visual Studio** (Средства фабрики данных Azure для Visual Studio) и нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="199cd-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="199cd-356">Если эта запись отсутствует, у вас уже установлена последняя версия средства.</span><span class="sxs-lookup"><span data-stu-id="199cd-356">If you do not see this entry, you already have the latest version of the tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="199cd-357">Использование файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="199cd-357">Use configuration files</span></span>
<span data-ttu-id="199cd-358">Файлы конфигурации в Visual Studio можно использовать для индивидуальной настройки свойств связанных служб, таблиц и конвейеров для каждой среды.</span><span class="sxs-lookup"><span data-stu-id="199cd-358">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="199cd-359">Рассмотрим следующее определение JSON для связанной службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-359">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="199cd-360">В нем нужно указать свойство **connectionString**. В зависимости от того, в какую среду вы развертываете сущности фабрики данных (среда разработки, среда тестирования или рабочая среда), значения accountname и accountkey будут разными.</span><span class="sxs-lookup"><span data-stu-id="199cd-360">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="199cd-361">Это можно сделать с помощью отдельного файла конфигурации для каждой среды.</span><span class="sxs-lookup"><span data-stu-id="199cd-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a><span data-ttu-id="199cd-362">Добавление файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="199cd-362">Add a configuration file</span></span>
<span data-ttu-id="199cd-363">Добавьте файл конфигурации для каждой среды, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="199cd-363">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="199cd-364">Щелкните правой кнопкой мыши проект фабрики данных в решении Visual Studio и последовательно выберите **Добавить** и **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="199cd-364">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="199cd-365">В левой части окна в списке установленных шаблонов последовательно выберите пункты **Конфигурация** и **Файл конфигурации**, укажите **имя** файла конфигурации и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="199cd-365">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![Добавление файла конфигурации](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="199cd-367">Добавьте параметры конфигурации и их значения в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="199cd-367">Add configuration parameters and their values in the following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="199cd-368">В этом примере настраивается свойство connectionString связанной службы хранилища Azure и связанной службы Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="199cd-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="199cd-369">Обратите внимание, что имя указывается с использованием синтаксиса [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="199cd-369">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="199cd-370">Если JSON-файл содержит свойство, которое имеет массив значений (см. ниже):</span><span class="sxs-lookup"><span data-stu-id="199cd-370">If JSON has a property that has an array of values as shown in the following code:</span></span>  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    <span data-ttu-id="199cd-371">Настройте свойства, как показано в следующем файле конфигурации (используйте индекс, начинающийся с нуля).</span><span class="sxs-lookup"><span data-stu-id="199cd-371">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="199cd-372">Имена свойств c пробелами</span><span class="sxs-lookup"><span data-stu-id="199cd-372">Property names with spaces</span></span>
<span data-ttu-id="199cd-373">Если имя свойства содержит пробелы, используйте квадратные скобки, как показано в следующем примере (имя сервера базы данных):</span><span class="sxs-lookup"><span data-stu-id="199cd-373">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="199cd-374">Развертывание решения с помощью конфигурации</span><span class="sxs-lookup"><span data-stu-id="199cd-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="199cd-375">Во время публикации сущностей фабрики данных Azure в Visual Studio можно указать конфигурацию, которая будет использоваться для этой операции публикации.</span><span class="sxs-lookup"><span data-stu-id="199cd-375">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="199cd-376">Чтобы опубликовать сущности в проекте фабрики данных Azure с помощью файла конфигурации, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="199cd-376">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="199cd-377">Щелкните правой кнопкой мыши проект фабрики данных и выберите пункт **Publish** (Опубликовать). Откроется диалоговое окно **Publish Items** (Публикация элементов).</span><span class="sxs-lookup"><span data-stu-id="199cd-377">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="199cd-378">На странице **Configure data factory** (Настройка фабрики данных) выберите имеющуюся фабрику данных или укажите значения для создания новой, а затем нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="199cd-378">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="199cd-379">На странице **Publish Items** (Публикация элементов) вы найдете раскрывающийся список **Select Deployment Config** (Выбор конфигурации развертывания) с доступными конфигурациями.</span><span class="sxs-lookup"><span data-stu-id="199cd-379">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![Выбор файла конфигурации](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="199cd-381">Выберите нужный **файл конфигурации** и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="199cd-381">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="199cd-382">Убедитесь, что на странице **Summary** (Сводка) отображается имя нужного JSON-файла, и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="199cd-382">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="199cd-383">По завершении развертывания нажмите кнопку **Готово** .</span><span class="sxs-lookup"><span data-stu-id="199cd-383">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="199cd-384">При развертывании значения из файла конфигурации используются, чтобы задать значения свойств в JSON-файлах, после чего сущности будут развернуты в службе фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-384">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="199cd-385">Использование хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="199cd-385">Use Azure Key Vault</span></span>
<span data-ttu-id="199cd-386">Фиксировать конфиденциальные данные, например строки подключения, в репозитории кода не рекомендуется и часто противоречит политике безопасности.</span><span class="sxs-lookup"><span data-stu-id="199cd-386">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="199cd-387">См. пример [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) на портале GitHub, чтобы узнать о хранении конфиденциальных сведений в Azure Key Vault и их использовании при публикации сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="199cd-388">Расширение Secure Publish для Visual Studio позволяет хранить секреты в службе Key Vault, определяя в конфигурациях связанных служб и развертываний только ссылки на них.</span><span class="sxs-lookup"><span data-stu-id="199cd-388">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="199cd-389">Эти ссылки разрешаются при публикации сущностей фабрики данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="199cd-389">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="199cd-390">Эти файлы затем можно зафиксировать в репозитории, не раскрывая конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="199cd-390">These files can then be committed to source repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="199cd-391">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="199cd-391">Next steps</span></span>
<span data-ttu-id="199cd-392">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="199cd-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="199cd-393">В следующей таблице приведен список хранилищ данных, которые поддерживаются в качестве источников и целевых расположений для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="199cd-393">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="199cd-394">Чтобы получить дополнительные сведения о том, как скопировать данные в хранилище данных или из него, щелкните ссылку для хранилища данных в таблице.</span><span class="sxs-lookup"><span data-stu-id="199cd-394">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>