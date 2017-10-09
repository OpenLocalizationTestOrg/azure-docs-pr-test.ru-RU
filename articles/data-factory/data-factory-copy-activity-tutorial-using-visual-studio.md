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
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="9390e-103">Руководство. Создание конвейера с действием копирования с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9390e-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9390e-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9390e-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="9390e-105">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="9390e-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="9390e-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="9390e-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="9390e-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9390e-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="9390e-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9390e-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="9390e-109">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9390e-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="9390e-110">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="9390e-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="9390e-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="9390e-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="9390e-112">В этой статье вы узнаете, как toouse hello toocreate Microsoft Visual Studio фабрики данных с конвейером, который копирует данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="9390e-112">In this article, you learn how toouse hello Microsoft Visual Studio toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="9390e-113">Если новый tooAzure фабрики данных, прочтите hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи, прежде чем выполнять задания этого учебника.</span><span class="sxs-lookup"><span data-stu-id="9390e-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="9390e-114">В этом руководстве описывается создание конвейера с одним действием — действием копирования.</span><span class="sxs-lookup"><span data-stu-id="9390e-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="9390e-115">Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="9390e-116">Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9390e-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="9390e-117">Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы.</span><span class="sxs-lookup"><span data-stu-id="9390e-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="9390e-118">Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="9390e-119">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="9390e-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="9390e-120">Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="9390e-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="9390e-121">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="9390e-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="9390e-122">конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="9390e-123">Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9390e-124">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9390e-124">Prerequisites</span></span>
1. <span data-ttu-id="9390e-125">Прочтите [Обзор учебника](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) статьи и завершения hello **необходимого компонента** действия.</span><span class="sxs-lookup"><span data-stu-id="9390e-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete hello **prerequisite** steps.</span></span>       
2. <span data-ttu-id="9390e-126">экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.</span><span class="sxs-lookup"><span data-stu-id="9390e-126">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
3. <span data-ttu-id="9390e-127">Необходимо иметь следующие hello, установленной на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9390e-127">You must have hello following installed on your computer:</span></span> 
   * <span data-ttu-id="9390e-128">Visual Studio 2013 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9390e-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="9390e-129">Загрузите пакет SDK Azure для Visual Studio 2013 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9390e-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="9390e-130">Перейдите в слишком[странице загрузки Azure](https://azure.microsoft.com/downloads/) и нажмите кнопку **VS 2013** или **VS 2015** в hello **.NET** раздела.</span><span class="sxs-lookup"><span data-stu-id="9390e-130">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="9390e-131">Загрузите hello последнюю фабрики данных Azure, подключаемый модуль для Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) или [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="9390e-131">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="9390e-132">Можно также обновить hello подключаемого модуля, выполнив следующие шаги hello: hello меню **средства** -> **расширения и обновления** -> **Online**  ->  **Коллекции visual Studio** -> **средства фабрики данных Microsoft Azure для Visual Studio** -> **обновление**.</span><span class="sxs-lookup"><span data-stu-id="9390e-132">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="9390e-133">Действия</span><span class="sxs-lookup"><span data-stu-id="9390e-133">Steps</span></span>
<span data-ttu-id="9390e-134">Ниже приведены hello действий, выполняемых в рамках этого учебника.</span><span class="sxs-lookup"><span data-stu-id="9390e-134">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="9390e-135">Создание **связанные службы** в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-135">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="9390e-136">На этом этапе вы создадите две связанные службы — службу хранилища Azure и базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9390e-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="9390e-137">Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9390e-137">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="9390e-138">Создан контейнер и загруженные в рамках учетной записи хранения данных toothis [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-138">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="9390e-139">AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9390e-139">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="9390e-140">Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-140">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="9390e-141">Вы создали таблицу SQL в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="9390e-142">Создать входной и выходной **наборы данных** в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-142">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="9390e-143">Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9390e-143">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="9390e-144">И входного BLOB-объекта dataset hello указывает контейнер hello и hello папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-144">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="9390e-145">Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения.</span><span class="sxs-lookup"><span data-stu-id="9390e-145">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="9390e-146">И SQL таблицы hello выходной набор данных указывает, что таблица hello в данных hello toowhich hello базы данных из хранилища больших двоичных объектов hello копируется.</span><span class="sxs-lookup"><span data-stu-id="9390e-146">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
3. <span data-ttu-id="9390e-147">Создание **конвейера** в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-147">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="9390e-148">На этом этапе вы создадите конвейер с действием копирования.</span><span class="sxs-lookup"><span data-stu-id="9390e-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="9390e-149">Действие копирования Hello копирует данные из большого двоичного объекта в таблице tooa хранилища BLOB-объектов Azure hello в базе данных Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-149">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="9390e-150">Действие копирования можно использовать в конвейер toocopy данных из любого места назначения tooany поддерживается поддерживаемой исходной.</span><span class="sxs-lookup"><span data-stu-id="9390e-150">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="9390e-151">Список поддерживаемых хранилищ данных см. в [этом разделе](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9390e-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="9390e-152">Создайте **фабрику данных** Azure при развертывании сущностей фабрики данных (связанные службы, наборы данных, таблицы и конвейеры).</span><span class="sxs-lookup"><span data-stu-id="9390e-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="9390e-153">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9390e-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="9390e-154">Запустите **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="9390e-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="9390e-155">Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="9390e-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="9390e-156">Вы увидите hello **новый проект** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="9390e-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="9390e-157">В hello **новый проект** диалоговое окно, выберите hello **DataFactory** шаблона и нажмите кнопку **пустой проект фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="9390e-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Диалоговое окно "Новый проект"](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="9390e-159">Укажите имя проекта hello, местоположение для решения hello hello и имя решения hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9390e-159">Specify hello name of hello project, location for hello solution, and name of hello solution, and then click **OK**.</span></span>
   
    ![Обозреватель решений](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="9390e-161">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="9390e-161">Create linked services</span></span>
<span data-ttu-id="9390e-162">Создания связанных служб в toolink фабрики данных, хранит и вычислений фабрики данных toohello службы данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-162">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="9390e-163">В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9390e-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="9390e-164">Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище).</span><span class="sxs-lookup"><span data-stu-id="9390e-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="9390e-165">Вы создадите две связанные службы — AzureStorage и AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="9390e-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="9390e-166">Hello хранилища Azure связанные ссылки на службу фабрики данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9390e-166">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="9390e-167">Эта учетная запись хранения является hello один в котором можно создать контейнер и загруженные данные hello в рамках [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-167">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="9390e-168">Azure SQL связанные ссылки на службу фабрики данных toohello базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9390e-168">Azure SQL linked service links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="9390e-169">Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-169">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="9390e-170">Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-170">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="9390e-171">Связанные службы связывание хранилищ данных или фабрики данных Azure tooan службы вычислений.</span><span class="sxs-lookup"><span data-stu-id="9390e-171">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="9390e-172">В разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) для всех hello источники и приемники, поддерживаемые действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="9390e-173">В разделе [связанные службы вычислений](data-factory-compute-linked-services.md) список hello вычислительных служб, поддерживаемые фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-173">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span> <span data-ttu-id="9390e-174">В этом руководстве не рассматривается использование служб вычислений.</span><span class="sxs-lookup"><span data-stu-id="9390e-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-hello-azure-storage-linked-service"></a><span data-ttu-id="9390e-175">Создание hello связанной службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="9390e-175">Create hello Azure Storage linked service</span></span>
1. <span data-ttu-id="9390e-176">В **обозревателе решений**, щелкните правой кнопкой мыши **связанные службы**, слишком точки**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="9390e-176">In **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="9390e-177">В hello **Добавление нового элемента** выберите **связанной службы хранилища Azure** hello списка и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="9390e-177">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span> 
   
    ![Новая связанная служба](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="9390e-179">Замените `<accountname>` и `<accountkey>`* hello имя вашей учетной записи хранилища Azure и ее ключа.</span><span class="sxs-lookup"><span data-stu-id="9390e-179">Replace `<accountname>` and `<accountkey>`* with hello name of your Azure storage account and its key.</span></span> 
   
    ![Связанная служба хранилища Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="9390e-181">Сохранить hello **AzureStorageLinkedService1.json** файла.</span><span class="sxs-lookup"><span data-stu-id="9390e-181">Save hello **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="9390e-182">Дополнительные сведения о свойствах JSON в определении службы hello связаны см. в разделе [соединителя хранилища больших двоичных объектов](data-factory-azure-blob-connector.md#linked-service-properties) статьи.</span><span class="sxs-lookup"><span data-stu-id="9390e-182">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-hello-azure-sql-linked-service"></a><span data-ttu-id="9390e-183">Создание hello связанной службой Azure SQL</span><span class="sxs-lookup"><span data-stu-id="9390e-183">Create hello Azure SQL linked service</span></span>
1. <span data-ttu-id="9390e-184">Щелкните правой кнопкой мыши **связанные службы** узел в hello **обозревателе решений** снова точки слишком**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="9390e-184">Right-click on **Linked Services** node in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="9390e-185">На этот раз выберите **Azure SQL Linked Service** (Связанная служба SQL Azure) и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9390e-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="9390e-186">В hello **файл AzureSqlLinkedService1.json**, замените `<servername>`, `<databasename>`, `<username@servername>`, и `<password>` с именами Azure SQL server, базы данных, учетная запись пользователя, и пароль.</span><span class="sxs-lookup"><span data-stu-id="9390e-186">In hello **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="9390e-187">Сохранить hello **AzureSqlLinkedService1.json** файла.</span><span class="sxs-lookup"><span data-stu-id="9390e-187">Save hello **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="9390e-188">Дополнительные сведения об этих свойствах JSON см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9390e-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="9390e-189">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="9390e-189">Create datasets</span></span>
<span data-ttu-id="9390e-190">В предыдущем шаге hello создать связанные службы toolink вашей учетной записи хранилища Azure и фабрику данных tooyour базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9390e-190">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="9390e-191">На этом шаге можно определить два набора данных с именем InputDataset и OutputDataset, представляющие входные данные и выходные данные, которые хранятся в хранилищах данных hello, на которые ссылается AzureStorageLinkedService1 и AzureSqlLinkedService1 соответственно.</span><span class="sxs-lookup"><span data-stu-id="9390e-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="9390e-192">Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9390e-192">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="9390e-193">И hello входного BLOB-объекта dataset (InputDataset) указывает контейнер hello и hello папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-193">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="9390e-194">Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения.</span><span class="sxs-lookup"><span data-stu-id="9390e-194">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="9390e-195">И hello выходной набор данных таблицы SQL (OututDataset) указывает таблицу hello в hello базы данных toowhich hello и копирования данных из хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-195">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="9390e-196">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="9390e-196">Create input dataset</span></span>
<span data-ttu-id="9390e-197">На этом шаге создается набор данных с именем InputDataset, который указывает файл tooa больших двоичных объектов (emp.txt) в корневой папке hello контейнер больших двоичных объектов (adftutorial) в hello представленный hello AzureStorageLinkedService1 связанной службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9390e-197">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="9390e-198">Если не указать значение для имени файла hello (или пропустить его), данные из всех больших двоичных объектов в папке входной hello, скопированный toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="9390e-198">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="9390e-199">В этом учебнике укажите значение для имени файла hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-199">In this tutorial, you specify a value for hello fileName.</span></span> 

<span data-ttu-id="9390e-200">Здесь используется hello термин «таблицы» вместо «наборы данных».</span><span class="sxs-lookup"><span data-stu-id="9390e-200">Here, you use hello term "tables" rather than "datasets".</span></span> <span data-ttu-id="9390e-201">Таблица представляет собой прямоугольный набор данных и представляет единственный тип hello набора данных, поддерживаемые в данный момент.</span><span class="sxs-lookup"><span data-stu-id="9390e-201">A table is a rectangular dataset and is hello only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="9390e-202">Щелкните правой кнопкой мыши **таблиц** в hello **обозревателе решений**, слишком точки**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="9390e-202">Right-click **Tables** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="9390e-203">В hello **Добавление нового элемента** выберите **больших двоичных объектов Azure**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="9390e-203">In hello **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="9390e-204">Заменить текст JSON hello после текста hello и сохранить hello **AzureBlobLocation1.json** файла.</span><span class="sxs-lookup"><span data-stu-id="9390e-204">Replace hello JSON text with hello following text and save hello **AzureBlobLocation1.json** file.</span></span> 

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
    <span data-ttu-id="9390e-205">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-205">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="9390e-206">Свойство</span><span class="sxs-lookup"><span data-stu-id="9390e-206">Property</span></span> | <span data-ttu-id="9390e-207">Описание</span><span class="sxs-lookup"><span data-stu-id="9390e-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="9390e-208">type</span><span class="sxs-lookup"><span data-stu-id="9390e-208">type</span></span> | <span data-ttu-id="9390e-209">Hello свойство type установлено слишком**AzureBlob** , так как данные находятся в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="9390e-209">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="9390e-210">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="9390e-210">linkedServiceName</span></span> | <span data-ttu-id="9390e-211">Указывает toohello **AzureStorageLinkedService** , созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="9390e-211">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="9390e-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="9390e-212">folderPath</span></span> | <span data-ttu-id="9390e-213">Указывает hello blob **контейнера** и hello **папки** , содержащий входного BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="9390e-213">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="9390e-214">В этом учебнике adftutorial — контейнер больших двоичных объектов hello и папка является корневой папкой hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-214">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="9390e-215">fileName</span><span class="sxs-lookup"><span data-stu-id="9390e-215">fileName</span></span> | <span data-ttu-id="9390e-216">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="9390e-216">This property is optional.</span></span> <span data-ttu-id="9390e-217">Если это свойство не указан, извлекаются все файлы из hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="9390e-217">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="9390e-218">В этом учебнике **emp.txt** задается для hello имя файла, поэтому только этот файл будет выбрано для обработки.</span><span class="sxs-lookup"><span data-stu-id="9390e-218">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="9390e-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="9390e-219">format -> type</span></span> |<span data-ttu-id="9390e-220">Hello входной файл имеет текстовый формат hello, поэтому мы используем **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="9390e-220">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="9390e-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="9390e-221">columnDelimiter</span></span> | <span data-ttu-id="9390e-222">Hello столбцов во входном файле hello разделяются **запятая (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="9390e-222">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="9390e-223">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="9390e-223">frequency/interval</span></span> | <span data-ttu-id="9390e-224">частота Hello задано слишком**час** и интервала задано слишком**1**, это означает, что hello ввода доступны срезы **каждый час**.</span><span class="sxs-lookup"><span data-stu-id="9390e-224">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="9390e-225">Другими словами, hello служба фабрики данных ищет входных данных каждый час в корневой папке hello контейнер больших двоичных объектов (**adftutorial**) было задано.</span><span class="sxs-lookup"><span data-stu-id="9390e-225">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="9390e-226">Выполняет поиск данных hello в hello конвейера начального и конечного времени, не до или после этих значений времени.</span><span class="sxs-lookup"><span data-stu-id="9390e-226">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="9390e-227">external</span><span class="sxs-lookup"><span data-stu-id="9390e-227">external</span></span> | <span data-ttu-id="9390e-228">Это свойство задано слишком**true** Если hello данных в этом конвейере не создается.</span><span class="sxs-lookup"><span data-stu-id="9390e-228">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="9390e-229">в файле emp.txt hello, который создается в этом конвейере не, поэтому мы задали это свойство tootrue — Hello входных данных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9390e-229">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="9390e-230">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9390e-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="9390e-231">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="9390e-231">Create output dataset</span></span>
<span data-ttu-id="9390e-232">На этом этапе мы создадим выходной набор данных с именем **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="9390e-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="9390e-233">Этот набор данных указывает tooa SQL таблицы в базе данных Azure SQL hello, представленного **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="9390e-233">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="9390e-234">Щелкните правой кнопкой мыши **таблиц** в hello **обозревателе решений** снова точки слишком**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="9390e-234">Right-click **Tables** in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="9390e-235">В hello **Добавление нового элемента** выберите **Azure SQL**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="9390e-235">In hello **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="9390e-236">Заменить текст JSON hello hello, следуя JSON и сохранить hello **AzureSqlTableLocation1.json** файла.</span><span class="sxs-lookup"><span data-stu-id="9390e-236">Replace hello JSON text with hello following JSON and save hello **AzureSqlTableLocation1.json** file.</span></span>

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
    <span data-ttu-id="9390e-237">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-237">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="9390e-238">Свойство</span><span class="sxs-lookup"><span data-stu-id="9390e-238">Property</span></span> | <span data-ttu-id="9390e-239">Описание</span><span class="sxs-lookup"><span data-stu-id="9390e-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="9390e-240">type</span><span class="sxs-lookup"><span data-stu-id="9390e-240">type</span></span> | <span data-ttu-id="9390e-241">Hello свойство type установлено слишком**AzureSqlTable** из-за данных скопированный tooa таблицы в базе данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9390e-241">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="9390e-242">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="9390e-242">linkedServiceName</span></span> | <span data-ttu-id="9390e-243">Указывает toohello **AzureSqlLinkedService** , созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="9390e-243">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="9390e-244">tableName</span><span class="sxs-lookup"><span data-stu-id="9390e-244">tableName</span></span> | <span data-ttu-id="9390e-245">Указанный hello **таблицы** toowhich hello данные копируются.</span><span class="sxs-lookup"><span data-stu-id="9390e-245">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="9390e-246">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="9390e-246">frequency/interval</span></span> | <span data-ttu-id="9390e-247">Hello задана слишком**час** и интервал — **1**, это означает, что hello срезы выходных данных создаются **каждый час** между hello конвейера начала и время окончания, не до или После этих значений времени.</span><span class="sxs-lookup"><span data-stu-id="9390e-247">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="9390e-248">Имеются три столбца — **идентификатор**, **FirstName**, и **LastName** — в таблице emp hello в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-248">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="9390e-249">Идентификатор является столбцом идентификаторов, поэтому вам необходимо только toospecify **FirstName** и **LastName** здесь.</span><span class="sxs-lookup"><span data-stu-id="9390e-249">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="9390e-250">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9390e-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="9390e-251">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="9390e-251">Create pipeline</span></span>
<span data-ttu-id="9390e-252">На этом этапе вы создадите конвейер с **действием копирования**, которое использует **InputDataset** в качестве входных данных и **OutputDataset** в качестве выходных.</span><span class="sxs-lookup"><span data-stu-id="9390e-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="9390e-253">В настоящее время выходной набор данных — того, какие диски hello расписания.</span><span class="sxs-lookup"><span data-stu-id="9390e-253">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="9390e-254">В этом учебнике выходной набор данных является настроенным tooproduce срез один раз в час.</span><span class="sxs-lookup"><span data-stu-id="9390e-254">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="9390e-255">конвейер Hello содержит время начала и время окончания, которые однажды друг от друга, что составляет 24 часа.</span><span class="sxs-lookup"><span data-stu-id="9390e-255">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="9390e-256">Таким образом 24 фрагменты выходной набор данных создают hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="9390e-256">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="9390e-257">Щелкните правой кнопкой мыши **конвейеры** в hello **обозревателе решений**, слишком точки**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="9390e-257">Right-click **Pipelines** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="9390e-258">Выберите **конвейера данных копирования** в hello **Добавление нового элемента** диалоговое окно и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="9390e-258">Select **Copy Data Pipeline** in hello **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="9390e-259">Замените следующие JSON hello hello JSON и сохраните hello **CopyActivity1.json** файла.</span><span class="sxs-lookup"><span data-stu-id="9390e-259">Replace hello JSON with hello following JSON and save hello **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
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
    - <span data-ttu-id="9390e-260">В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**копирования**.</span><span class="sxs-lookup"><span data-stu-id="9390e-260">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="9390e-261">Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-261">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="9390e-262">В решениях фабрики данных можно также использовать [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="9390e-263">Входных данных для действия hello установлено слишком**InputDataset** и вывода для hello действия установлено слишком**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="9390e-263">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="9390e-264">В hello **typeProperties** разделе **BlobSource** указан в качестве типа источника hello и **SqlSink** указан как тип приемника hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-264">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="9390e-265">Перечень хранилищ данных, поддерживаемые действием копирования hello как источники и приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9390e-265">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="9390e-266">как сохранить toouse конкретных поддерживаемые данные в качестве источника и приемника, toolearn по ссылке hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-266">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="9390e-267">Замените значение hello hello **запустить** свойство с hello текущего дня и **окончания** значение с hello следующего дня.</span><span class="sxs-lookup"><span data-stu-id="9390e-267">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="9390e-268">Можно указать только часть даты hello и пропустить hello время hello Дата и время.</span><span class="sxs-lookup"><span data-stu-id="9390e-268">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="9390e-269">Например, «2016-02-03», который является эквивалентом "2016-02-03T00:00:00Z»</span><span class="sxs-lookup"><span data-stu-id="9390e-269">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="9390e-270">Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="9390e-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="9390e-271">Например, 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="9390e-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="9390e-272">Hello **окончания** времени является необязательным, но мы используем в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9390e-272">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="9390e-273">Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов**».</span><span class="sxs-lookup"><span data-stu-id="9390e-273">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="9390e-274">конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство.</span><span class="sxs-lookup"><span data-stu-id="9390e-274">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="9390e-275">В предыдущих пример hello существует 24 срезы данных, как каждый срез данных создается каждый час.</span><span class="sxs-lookup"><span data-stu-id="9390e-275">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="9390e-276">Описание свойств JSON в определении конвейера см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9390e-277">Описание свойств JSON в определении действия копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="9390e-278">Описание свойств JSON, поддерживаемых BlobSource, см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="9390e-279">Описание свойств JSON, поддерживаемых SqlSink, см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="9390e-280">Публикация и развертывание сущностей фабрики данных</span><span class="sxs-lookup"><span data-stu-id="9390e-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="9390e-281">На этом этапе вы опубликуете созданные ранее сущности фабрики данных (связанные службы, наборы данных и конвейеры).</span><span class="sxs-lookup"><span data-stu-id="9390e-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="9390e-282">Также следует определять имя hello hello новых данных фабрики toobe созданного toohold этих сущностей.</span><span class="sxs-lookup"><span data-stu-id="9390e-282">You also specify hello name of hello new data factory toobe created toohold these entities.</span></span>  

1. <span data-ttu-id="9390e-283">Щелкните правой кнопкой мыши проект в обозревателе решений hello и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="9390e-283">Right-click project in hello Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="9390e-284">Если вы видите **входа в учетную запись Майкрософт tooyour** диалоговое окно, введите свои учетные данные для hello учетной записи, имеющей подписку Azure и нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="9390e-284">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="9390e-285">Вы должны увидеть следующие диалоговое окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="9390e-285">You should see hello following dialog box:</span></span>
   
   ![Диалоговое окно "Опубликовать"](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="9390e-287">На странице фабрики данных Настройка hello hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9390e-287">In hello Configure data factory page, do hello following steps:</span></span> 
   
   1. <span data-ttu-id="9390e-288">Выберите **Создать новую фабрику данных** .</span><span class="sxs-lookup"><span data-stu-id="9390e-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="9390e-289">Введите **VSTutorialFactory** в качестве **имени** фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="9390e-290">Имя фабрики данных Azure hello Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="9390e-290">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="9390e-291">Если появляется ошибка об hello имя фабрики данных при публикации, измените имя hello hello фабрики данных (например, yournameVSTutorialFactory) и повторите попытку публикации.</span><span class="sxs-lookup"><span data-stu-id="9390e-291">If you receive an error about hello name of data factory when publishing, change hello name of hello data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="9390e-292">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="9390e-293">Выберите подписку Azure для hello **подписки** поля.</span><span class="sxs-lookup"><span data-stu-id="9390e-293">Select your Azure subscription for hello **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="9390e-294">Если вы не видите любую подписку, убедитесь, что вы вошли в учетную запись, которая является администратором или соадминистратором подписки hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="9390e-295">Выберите hello **группы ресурсов** для hello данных фабрики toobe создан.</span><span class="sxs-lookup"><span data-stu-id="9390e-295">Select hello **resource group** for hello data factory toobe created.</span></span> 
   5. <span data-ttu-id="9390e-296">Выберите hello **область** для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-296">Select hello **region** for hello data factory.</span></span> <span data-ttu-id="9390e-297">В раскрывающемся списке hello отображаются только регионов, поддерживаемых hello служба фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-297">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   6. <span data-ttu-id="9390e-298">Нажмите кнопку **Далее** tooswitch toohello **публиковать элементы** страницы.</span><span class="sxs-lookup"><span data-stu-id="9390e-298">Click **Next** tooswitch toohello **Publish Items** page.</span></span>
      
       ![Страница Configure data factory (Настройка фабрики данных)](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="9390e-300">В hello **публиковать элементы** убедитесь, что все hello фабрик данных сущностей установлены и нажмите кнопку **Далее** tooswitch toohello **Сводка** страницы.</span><span class="sxs-lookup"><span data-stu-id="9390e-300">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>
   
   ![Страница Publish items (Публикация элементов)](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="9390e-302">Просмотрите hello сводки и нажмите кнопку **Далее** toostart hello развертывания процесса и представление hello **состояние развертывания**.</span><span class="sxs-lookup"><span data-stu-id="9390e-302">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>
   
   ![Страница "Сводка публикации"](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="9390e-304">В hello **состояние развертывания** страницы, вы увидите hello состояние процесса развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-304">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="9390e-305">После завершения развертывания hello, нажмите кнопку "Готово".</span><span class="sxs-lookup"><span data-stu-id="9390e-305">Click Finish after hello deployment is done.</span></span>
 
   ![Страница "Состояние развертывания"](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="9390e-307">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="9390e-307">Note hello following points:</span></span> 

* <span data-ttu-id="9390e-308">Если ошибка hello: «этой подписки не зарегистрированного toouse имен Microsoft.DataFactory», выполните одно из следующих hello и повторите попытку публикации:</span><span class="sxs-lookup"><span data-stu-id="9390e-308">If you receive hello error: "This subscription is not registered toouse namespace Microsoft.DataFactory", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="9390e-309">В Azure PowerShell запустите hello, следующая команда tooregister hello фабрики данных поставщика.</span><span class="sxs-lookup"><span data-stu-id="9390e-309">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="9390e-310">Следующая команда tooconfirm hello можно запустить, hello зарегистрирован поставщик фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-310">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="9390e-311">Имя входа с помощью hello подписки Azure в hello [портал Azure](https://portal.azure.com) и перейдите в колонку tooa фабрики данных (или) создать фабрику данных в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9390e-311">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="9390e-312">Это действие автоматически регистрирует поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-312">This action automatically registers hello provider for you.</span></span>
* <span data-ttu-id="9390e-313">Имя фабрики данных hello Hello может зарегистрирован как DNS-имя в будущем hello и таким образом становятся общедоступен.</span><span class="sxs-lookup"><span data-stu-id="9390e-313">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9390e-314">экземпляры toocreate фабрики данных, необходимо toobe администратором или соадминистратором hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="9390e-314">toocreate Data Factory instances, you need toobe a admin/co-admin of hello Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="9390e-315">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="9390e-315">Monitor pipeline</span></span>
<span data-ttu-id="9390e-316">Перемещаться toohello домашней страницы для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-316">Navigate toohello home page for your data factory:</span></span>

1. <span data-ttu-id="9390e-317">Войдите в слишком[портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9390e-317">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9390e-318">Нажмите кнопку **дополнительные службы** hello в левом меню и нажмите кнопку **фабрик данных**.</span><span class="sxs-lookup"><span data-stu-id="9390e-318">Click **More services** on hello left menu, and click **Data factories**.</span></span>

    ![Обзор фабрик данных](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="9390e-320">Начните вводить имя hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-320">Start typing hello name of your data factory.</span></span>

    ![Имя фабрики данных](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="9390e-322">Щелкните фабрики данных в hello результаты toosee hello домашней страницы списка для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-322">Click your data factory in hello results list toosee hello home page for your data factory.</span></span>

    ![Домашняя страница фабрики данных](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="9390e-324">Следуйте инструкциям из [отслеживать наборы данных и конвейера](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello конвейера и наборы данных создан в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9390e-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="9390e-325">Сейчас Visual Studio не поддерживает мониторинг конвейеров фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="9390e-326">Сводка</span><span class="sxs-lookup"><span data-stu-id="9390e-326">Summary</span></span>
<span data-ttu-id="9390e-327">В этом учебнике вы создали данных toocopy фабрики данных Azure из базы данных Azure SQL tooan BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="9390e-327">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="9390e-328">Вы использовали фабрики данных hello toocreate Visual Studio, связанные службы, наборы данных и конвейера.</span><span class="sxs-lookup"><span data-stu-id="9390e-328">You used Visual Studio toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="9390e-329">Ниже приведены hello высокоуровневые действия, выполняемые в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9390e-329">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="9390e-330">Создание **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="9390e-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="9390e-331">Создание **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="9390e-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="9390e-332">**Хранилища Azure** связанные toolink службы учетной записи хранилища Azure, содержащий входные данные.</span><span class="sxs-lookup"><span data-stu-id="9390e-332">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="9390e-333">**Azure SQL** связанные toolink службы базы данных Azure SQL, которое содержит hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-333">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="9390e-334">Создание **наборов данных**, описывающих входные и выходные данные для конвейеров.</span><span class="sxs-lookup"><span data-stu-id="9390e-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="9390e-335">Создание **конвейера** с **BlobSource** в качестве источника и **SqlSink** в качестве приемника с помощью **действия копирования**.</span><span class="sxs-lookup"><span data-stu-id="9390e-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="9390e-336">toosee toouse tootransform данных Hive действие HDInsight с помощью кластера Azure HDInsight. в статье [ учебника: построение первые данные конвейера tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-336">toosee how toouse a HDInsight Hive Activity tootransform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="9390e-337">Вы можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="9390e-337">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="9390e-338">Подробные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="9390e-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="9390e-339">Просмотр фабрик данных в обозревателе серверов</span><span class="sxs-lookup"><span data-stu-id="9390e-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="9390e-340">В этом разделе описывается toouse hello обозреватель серверов в Visual Studio tooview всех фабрик данных hello в вашей подписке Azure и Создание проекта Visual Studio, в зависимости от существующей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-340">This section describes how toouse hello Server Explorer in Visual Studio tooview all hello data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="9390e-341">В **Visual Studio**, нажмите кнопку **представление** hello меню и нажмите кнопку **обозревателя серверов**.</span><span class="sxs-lookup"><span data-stu-id="9390e-341">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="9390e-342">Разверните в окне обозревателя серверов hello **Azure** и разверните **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="9390e-342">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="9390e-343">Если вы видите **входа tooVisual Studio**, введите hello **учетной записи** связанный с подпиской Azure и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="9390e-343">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="9390e-344">Введите **пароль** и нажмите кнопку **Войти**.</span><span class="sxs-lookup"><span data-stu-id="9390e-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="9390e-345">Visual Studio предпринимает tooget сведения о всех фабрик данных Azure в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="9390e-345">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="9390e-346">Состояние данной операции в hello hello **список задач фабрики данных** окна.</span><span class="sxs-lookup"><span data-stu-id="9390e-346">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Обозреватель серверов](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="9390e-348">Создание проекта Visual Studio для имеющейся фабрики данных</span><span class="sxs-lookup"><span data-stu-id="9390e-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="9390e-349">Щелкните правой кнопкой мыши фабрики данных в обозревателе серверов и выберите **tooNew экспорта фабрики данных проекта** toocreate проект Visual Studio основан на существующей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-349">Right-click a data factory in Server Explorer, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Экспорт проекта Visual STUDIO tooa фабрики данных](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="9390e-351">Обновление средств фабрик данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9390e-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="9390e-352">средства tooupdate фабрики данных Azure для Visual Studio hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9390e-352">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="9390e-353">Нажмите кнопку **средства** hello меню и выберите пункт **расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="9390e-353">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="9390e-354">Выберите **обновления** в hello левой панели, а затем выберите **коллекции Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="9390e-354">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="9390e-355">Выберите **Azure Data Factory tools for Visual Studio** (Средства фабрики данных Azure для Visual Studio) и нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="9390e-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="9390e-356">Если эта запись отсутствует, уже hello последнюю версию средств hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-356">If you do not see this entry, you already have hello latest version of hello tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="9390e-357">Использование файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="9390e-357">Use configuration files</span></span>
<span data-ttu-id="9390e-358">Файлы конфигурации в свойствах tooconfigure Visual Studio можно использовать для связанной службы, таблицы и конвейеры по-разному для каждой среды.</span><span class="sxs-lookup"><span data-stu-id="9390e-358">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="9390e-359">Рассмотрим следующие определения JSON для связанной службой хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-359">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="9390e-360">toospecify **connectionString** с различными значениями для accountname и accountkey в зависимости от среды (разработки или тестирования и рабочего) toowhich hello развертывании сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-360">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="9390e-361">Это можно сделать с помощью отдельного файла конфигурации для каждой среды.</span><span class="sxs-lookup"><span data-stu-id="9390e-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="9390e-362">Добавление файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="9390e-362">Add a configuration file</span></span>
<span data-ttu-id="9390e-363">Добавьте файл конфигурации для каждой среды, выполнив следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-363">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="9390e-364">Щелкните правой кнопкой мыши hello фабрики данных проекта в решении Visual Studio, выберите пункт слишком**добавить**и нажмите кнопку **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="9390e-364">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="9390e-365">Выберите **Config** выберите из списка установленных шаблонов слева hello hello **файла конфигурации**, введите **имя** для hello конфигурации файла и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9390e-365">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Добавление файла конфигурации](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="9390e-367">Добавление параметров конфигурации и их значений в кодировке hello:</span><span class="sxs-lookup"><span data-stu-id="9390e-367">Add configuration parameters and their values in hello following format:</span></span>

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

    <span data-ttu-id="9390e-368">В этом примере настраивается свойство connectionString связанной службы хранилища Azure и связанной службы Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9390e-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="9390e-369">Обратите внимание, что hello синтаксис для указания имени [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="9390e-369">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="9390e-370">Если JSON имеет свойство, которое содержит массив значений, как показано на hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="9390e-370">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

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

    <span data-ttu-id="9390e-371">Настройте свойства, как показано в hello следующий файл конфигурации (Используйте индексацию с нуля).</span><span class="sxs-lookup"><span data-stu-id="9390e-371">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="9390e-372">Имена свойств c пробелами</span><span class="sxs-lookup"><span data-stu-id="9390e-372">Property names with spaces</span></span>
<span data-ttu-id="9390e-373">Если имя свойства содержит пробелы, используйте квадратные скобки, как показано в hello в следующем примере (имя сервера базы данных):</span><span class="sxs-lookup"><span data-stu-id="9390e-373">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="9390e-374">Развертывание решения с помощью конфигурации</span><span class="sxs-lookup"><span data-stu-id="9390e-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="9390e-375">При публикации сущностей фабрики данных Azure в Visual STUDIO, можно указать hello конфигурации требуется toouse для этой операции публикации.</span><span class="sxs-lookup"><span data-stu-id="9390e-375">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="9390e-376">toopublish сущности в проекте фабрики данных Azure, с помощью файла конфигурации:</span><span class="sxs-lookup"><span data-stu-id="9390e-376">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="9390e-377">Щелкните правой кнопкой мыши проект в фабрике данных и нажмите кнопку **публикации** toosee hello **публиковать элементы** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="9390e-377">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="9390e-378">Выберите существующую фабрику данных или указать значения для создания фабрики данных hello **фабрики данных Настройка** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9390e-378">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="9390e-379">На hello **публиковать элементы** страницы: отображается список раскрывающегося списка с конфигурации для hello **выбора конфигурации развертывания** поля.</span><span class="sxs-lookup"><span data-stu-id="9390e-379">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Выбор файла конфигурации](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="9390e-381">Выберите hello **файла конфигурации** , необходимо будет toouse и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9390e-381">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="9390e-382">Убедитесь, что это имя hello файла JSON в hello **Сводка** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9390e-382">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="9390e-383">Нажмите кнопку **Готово** после завершения операции развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-383">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="9390e-384">При развертывании, hello значения из файла конфигурации hello: используется tooset значения свойств в файлах JSON hello, прежде чем сущностей hello развернутой tooAzure служба фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-384">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="9390e-385">Использование хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="9390e-385">Use Azure Key Vault</span></span>
<span data-ttu-id="9390e-386">Это не рекомендуется и часто безопасности политики toocommit конфиденциальных данных, таких как репозиторий кода toohello строки подключения.</span><span class="sxs-lookup"><span data-stu-id="9390e-386">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="9390e-387">В разделе [ADF Secure публикации](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) на GitHub toolearn о хранение конфиденциальных сведений в хранилище ключей Azure и его использования при публикации сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="9390e-388">Hello Secure публикации расширения для Visual Studio позволяет toobe hello секретные данные, хранящиеся в хранилище ключей и только ссылки на toothem указываются в связанных служб или конфигураций развертывания.</span><span class="sxs-lookup"><span data-stu-id="9390e-388">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="9390e-389">Эти ссылки разрешаются во время публикации tooAzure сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-389">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="9390e-390">Эти файлы затем могут быть зафиксированы toosource репозитория без предоставления никакую конфиденциальную информацию.</span><span class="sxs-lookup"><span data-stu-id="9390e-390">These files can then be committed toosource repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9390e-391">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9390e-391">Next steps</span></span>
<span data-ttu-id="9390e-392">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="9390e-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="9390e-393">Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения:</span><span class="sxs-lookup"><span data-stu-id="9390e-393">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="9390e-394">toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="9390e-394">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
