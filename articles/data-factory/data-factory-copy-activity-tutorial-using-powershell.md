---
title: "Учебник: Создание конвейера toomove данных с помощью Azure PowerShell | Документы Microsoft"
description: "В этом руководстве вы создадите конвейер фабрики данных Azure с действием копирования с помощью Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="c3a43-103">Руководство по созданию конвейера фабрики данных для переноса данных с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3a43-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3a43-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c3a43-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="c3a43-105">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="c3a43-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="c3a43-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c3a43-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="c3a43-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c3a43-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="c3a43-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3a43-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="c3a43-109">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c3a43-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="c3a43-110">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="c3a43-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="c3a43-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="c3a43-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="c3a43-112">В этой статье вы узнаете, как toocreate toouse PowerShell фабрики данных с конвейером, который копирует данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-112">In this article, you learn how toouse PowerShell toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="c3a43-113">Если новый tooAzure фабрики данных, прочтите hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи, прежде чем выполнять задания этого учебника.</span><span class="sxs-lookup"><span data-stu-id="c3a43-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="c3a43-114">В этом руководстве описывается создание конвейера с одним действием — действием копирования.</span><span class="sxs-lookup"><span data-stu-id="c3a43-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="c3a43-115">Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="c3a43-116">Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c3a43-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c3a43-117">Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы.</span><span class="sxs-lookup"><span data-stu-id="c3a43-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="c3a43-118">Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="c3a43-119">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="c3a43-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c3a43-120">Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="c3a43-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c3a43-121">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c3a43-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="c3a43-122">Данная статья не охватывает все командлеты фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-122">This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="c3a43-123">Полную документацию по этим командлетам см. в [справочнике](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="c3a43-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="c3a43-124">конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="c3a43-125">Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3a43-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c3a43-126">Prerequisites</span></span>
- <span data-ttu-id="c3a43-127">Выполните предварительные требования, перечисленные в hello [предварительных требованиях для учебников](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="c3a43-127">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="c3a43-128">Установите **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="c3a43-129">Следуйте инструкциям в разделе hello [как tooinstall и настройка Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-129">Follow hello instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="c3a43-130">Действия</span><span class="sxs-lookup"><span data-stu-id="c3a43-130">Steps</span></span>
<span data-ttu-id="c3a43-131">Ниже приведены hello действий, выполняемых в рамках этого учебника.</span><span class="sxs-lookup"><span data-stu-id="c3a43-131">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="c3a43-132">Создайте **фабрику данных** Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="c3a43-133">На этом этапе вы создадите фабрику данных Azure с именем ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="c3a43-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="c3a43-134">Создание **связанные службы** в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-134">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="c3a43-135">На этом этапе вы создадите две связанные службы — службу хранилища Azure и базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="c3a43-136">Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-136">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="c3a43-137">Создан контейнер и загруженные в рамках учетной записи хранения данных toothis [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-137">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="c3a43-138">AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c3a43-138">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="c3a43-139">Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-139">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="c3a43-140">Вы создали таблицу SQL в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="c3a43-141">Создать входной и выходной **наборы данных** в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-141">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="c3a43-142">Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-142">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c3a43-143">И входного BLOB-объекта dataset hello указывает контейнер hello и hello папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-143">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="c3a43-144">Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c3a43-144">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="c3a43-145">И SQL таблицы hello выходной набор данных указывает, что таблица hello в данных hello toowhich hello базы данных из хранилища больших двоичных объектов hello копируется.</span><span class="sxs-lookup"><span data-stu-id="c3a43-145">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="c3a43-146">Создание **конвейера** в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-146">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="c3a43-147">На этом этапе вы создадите конвейер с действием копирования.</span><span class="sxs-lookup"><span data-stu-id="c3a43-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="c3a43-148">Действие копирования Hello копирует данные из большого двоичного объекта в таблице tooa хранилища BLOB-объектов Azure hello в базе данных Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-148">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="c3a43-149">Действие копирования можно использовать в конвейер toocopy данных из любого места назначения tooany поддерживается поддерживаемой исходной.</span><span class="sxs-lookup"><span data-stu-id="c3a43-149">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="c3a43-150">Список поддерживаемых хранилищ данных см. в [этом разделе](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c3a43-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="c3a43-151">Монитор hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="c3a43-151">Monitor hello pipeline.</span></span> <span data-ttu-id="c3a43-152">На этом шаге вы **монитор** hello фрагменты наборов входных и выходных данных с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c3a43-152">In this step, you **monitor** hello slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="c3a43-153">Создать фабрику данных</span><span class="sxs-lookup"><span data-stu-id="c3a43-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c3a43-154">Полный [необходимых компонентов для учебника hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="c3a43-154">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="c3a43-155">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="c3a43-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c3a43-156">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="c3a43-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c3a43-157">Например toocopy действие копирования данных из целевое хранилище данных источника tooa и toorun действие Hive в HDInsight tootransform скрипт Hive входных данных tooproduct выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-157">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="c3a43-158">Давайте начнем с создания фабрики данных hello на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="c3a43-158">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="c3a43-159">Запустите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-159">Launch **PowerShell**.</span></span> <span data-ttu-id="c3a43-160">Не закрывайте Azure PowerShell до завершения этого учебника hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-160">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="c3a43-161">Если закрыть и снова открыть понадобятся toorun hello команд.</span><span class="sxs-lookup"><span data-stu-id="c3a43-161">If you close and reopen, you need toorun hello commands again.</span></span>

    <span data-ttu-id="c3a43-162">Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-162">Run hello following command, and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="c3a43-163">Выполните следующие команды tooview hello все hello подписки для этой учетной записи:</span><span class="sxs-lookup"><span data-stu-id="c3a43-163">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="c3a43-164">Следующая команда tooselect hello подписки на toowork с выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-164">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="c3a43-165">Замените  **&lt;NameOfAzureSubscription** &gt; с именем hello подписки Azure:</span><span class="sxs-lookup"><span data-stu-id="c3a43-165">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="c3a43-166">Создание группы ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c3a43-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="c3a43-167">Некоторые шаги hello в этом учебнике предполагается использовать с именем группы ресурсов hello **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-167">Some of hello steps in this tutorial assume that you use hello resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="c3a43-168">Если вы используете другой группе ресурсов, необходимо toouse его вместо ADFTutorialResourceGroup в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c3a43-168">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="c3a43-169">Запустите hello **New AzureRmDataFactory** toocreate командлет фабрики данных с именем **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="c3a43-169">Run hello **New-AzureRmDataFactory** cmdlet toocreate a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="c3a43-170">Это имя уже может использоваться.</span><span class="sxs-lookup"><span data-stu-id="c3a43-170">This name may already have been taken.</span></span> <span data-ttu-id="c3a43-171">Таким образом, чтобы hello имя фабрики данных hello уникальными путем добавления префикса или суффикса (например: ADFTutorialDataFactoryPSH05152017) и снова выполните команду hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-171">Therefore, make hello name of hello data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run hello command again.</span></span>  

<span data-ttu-id="c3a43-172">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="c3a43-172">Note hello following points:</span></span>

* <span data-ttu-id="c3a43-173">Имя фабрики данных Azure hello Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="c3a43-173">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="c3a43-174">Если появляется следующая ошибка hello, измените имя hello (например, yournameADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="c3a43-174">If you receive hello following error, change hello name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="c3a43-175">Используйте это имя вместо ADFTutorialFactoryPSH при выполнении шагов в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="c3a43-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="c3a43-176">Ознакомьтесь с [правилами именования](data-factory-naming-rules.md) артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="c3a43-177">экземпляры toocreate фабрики данных, вы должны быть участника или администратор hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-177">toocreate Data Factory instances, you must be a contributor or administrator of hello Azure subscription.</span></span>
* <span data-ttu-id="c3a43-178">Hello имя фабрики данных hello быть зарегистрировано как DNS-имя в будущем hello и поэтому становятся публично видимых.</span><span class="sxs-lookup"><span data-stu-id="c3a43-178">hello name of hello data factory may be registered as a DNS name in hello future, and hence become publicly visible.</span></span>
* <span data-ttu-id="c3a43-179">Может появиться следующая ошибка hello: «**этой подписки не является пространством имен зарегистрированных toouse Microsoft.DataFactory.**»</span><span class="sxs-lookup"><span data-stu-id="c3a43-179">You may receive hello following error: "**This subscription is not registered toouse namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="c3a43-180">Выполните одно из следующих hello и повторите попытку публикации:</span><span class="sxs-lookup"><span data-stu-id="c3a43-180">Do one of hello following, and try publishing again:</span></span>

  * <span data-ttu-id="c3a43-181">В Azure PowerShell выполните hello, следующая команда tooregister hello фабрики данных поставщика.</span><span class="sxs-lookup"><span data-stu-id="c3a43-181">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="c3a43-182">Выполните следующие команды tooconfirm hello, hello зарегистрирован поставщик фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="c3a43-182">Run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="c3a43-183">Вход с помощью hello подписки Azure toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c3a43-183">Sign in by using hello Azure subscription toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c3a43-184">Перейдите в колонку tooa фабрики данных или создать фабрику данных в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-184">Go tooa Data Factory blade, or create a data factory in hello Azure portal.</span></span> <span data-ttu-id="c3a43-185">Это действие автоматически регистрирует поставщик hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-185">This action automatically registers hello provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="c3a43-186">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="c3a43-186">Create linked services</span></span>
<span data-ttu-id="c3a43-187">Создания связанных служб в toolink фабрики данных, хранит и вычислений фабрики данных toohello службы данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-187">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="c3a43-188">В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c3a43-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="c3a43-189">Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище).</span><span class="sxs-lookup"><span data-stu-id="c3a43-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="c3a43-190">Поэтому нужно создать две связанные службы: служба хранилища Azure с именем AzureStorageLinkedService и база данных SQL Azure с именем AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="c3a43-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="c3a43-191">Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-191">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="c3a43-192">Эта учетная запись хранения является hello один в котором можно создать контейнер и загруженные данные hello в рамках [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-192">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="c3a43-193">AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c3a43-193">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="c3a43-194">Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-194">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="c3a43-195">Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-195">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="c3a43-196">Создание связанной службы для учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="c3a43-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="c3a43-197">На этом шаге связать фабрики данных tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-197">In this step, you link your Azure storage account tooyour data factory.</span></span>

1. <span data-ttu-id="c3a43-198">Создайте JSON-файл с именем **AzureStorageLinkedService.json** в **C:\ADFGetStartedPSH** папка с hello после содержимого: (Создание hello папки ADFGetStartedPSH, если он еще не существует.)</span><span class="sxs-lookup"><span data-stu-id="c3a43-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with hello following content: (Create hello folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c3a43-199">Замените &lt;accountname&gt; и &lt;accountkey&gt; с именем и ключом вашей учетной записи хранилища Azure, прежде чем сохранять файл hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving hello file.</span></span> 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. <span data-ttu-id="c3a43-200">В **Azure PowerShell**, переключение toohello **ADFGetStartedPSH** папки.</span><span class="sxs-lookup"><span data-stu-id="c3a43-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="c3a43-201">Запустите hello **New AzureRmDataFactoryLinkedService** toocreate hello командлет связанной службы: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-201">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="c3a43-202">Этот командлет и другие командлеты фабрики данных, используемый в этом учебнике требуется toopass значения для hello **ResourceGroupName** и **с именем DataFactoryName** параметров.</span><span class="sxs-lookup"><span data-stu-id="c3a43-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="c3a43-203">Кроме того можно передать объект DataFactory hello, возвращаемых командлетом New-AzureRmDataFactory hello без ввода ResourceGroupName и с именем DataFactoryName каждый раз при запуске командлета.</span><span class="sxs-lookup"><span data-stu-id="c3a43-203">Alternatively, you can pass hello DataFactory object returned by hello New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="c3a43-204">Вот пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-204">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="c3a43-205">Второй способ создания эта связанная служба — имя группы ресурсов toospecify и имя фабрики данных вместо указания hello объекта DataFactory.</span><span class="sxs-lookup"><span data-stu-id="c3a43-205">Other way of creating this linked service is toospecify resource group name and data factory name instead of specifying hello DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="c3a43-206">Создание связанной службы для Базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c3a43-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="c3a43-207">На этом шаге связать фабрики данных tooyour базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c3a43-207">In this step, you link your Azure SQL database tooyour data factory.</span></span>

1. <span data-ttu-id="c3a43-208">Создайте JSON-файл с именем AzureSqlLinkedService.json в папке C:\ADFGetStartedPSH и hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="c3a43-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with hello following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c3a43-209">Вместо &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; и &lt;password&gt; укажите имя своего сервера Azure SQL Server, имя базы данных, имя учетной записи пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="c3a43-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. <span data-ttu-id="c3a43-210">Выполните следующие команды toocreate hello связанной службы:</span><span class="sxs-lookup"><span data-stu-id="c3a43-210">Run hello following command toocreate a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="c3a43-211">Вот пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-211">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="c3a43-212">Убедитесь, что **разрешить доступ службы tooAzure** будет включена для базы данных SQL server.</span><span class="sxs-lookup"><span data-stu-id="c3a43-212">Confirm that **Allow access tooAzure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="c3a43-213">tooverify и включите его, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c3a43-213">tooverify and turn it on, do hello following steps:</span></span>

    1. <span data-ttu-id="c3a43-214">Войдите в toohello [портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="c3a43-214">Log in toohello [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="c3a43-215">Нажмите кнопку **дополнительные службы >** hello слева, а затем нажмите **серверов SQL Server** в hello **баз данных** категории.</span><span class="sxs-lookup"><span data-stu-id="c3a43-215">Click **More services >** on hello left, and click **SQL servers** in hello **DATABASES** category.</span></span>
    3. <span data-ttu-id="c3a43-216">Выберите сервер в список серверов SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-216">Select your server in hello list of SQL servers.</span></span>
    4. <span data-ttu-id="c3a43-217">В колонке hello SQL server выберите **Показать параметры брандмауэра** ссылку.</span><span class="sxs-lookup"><span data-stu-id="c3a43-217">On hello SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="c3a43-218">В hello **параметры брандмауэра** колонка, щелкните **ON** для **разрешить доступ службы tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-218">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
    6. <span data-ttu-id="c3a43-219">Нажмите кнопку **Сохранить** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-219">Click **Save** on hello toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="c3a43-220">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="c3a43-220">Create datasets</span></span>
<span data-ttu-id="c3a43-221">В предыдущем шаге hello создать связанные службы toolink вашей учетной записи хранилища Azure и фабрику данных tooyour базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c3a43-221">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="c3a43-222">На этом шаге можно определить два набора данных с именем InputDataset и OutputDataset, представляющие входные данные и выходные данные, которые хранятся в хранилищах данных hello, на которые ссылается AzureStorageLinkedService и AzureSqlLinkedService соответственно.</span><span class="sxs-lookup"><span data-stu-id="c3a43-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="c3a43-223">Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-223">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c3a43-224">И hello входного BLOB-объекта dataset (InputDataset) указывает контейнер hello и hello папку, содержащую hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-224">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="c3a43-225">Аналогичным образом hello связана база данных SQL Azure службы указывает hello строку подключения, использующее служба фабрики данных в базе данных Azure SQL tooyour tooconnect время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c3a43-225">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="c3a43-226">И hello выходной набор данных таблицы SQL (OututDataset) указывает таблицу hello в hello базы данных toowhich hello и копирования данных из хранилища больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-226">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="c3a43-227">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="c3a43-227">Create an input dataset</span></span>
<span data-ttu-id="c3a43-228">На этом шаге создается набор данных с именем InputDataset, который указывает файл tooa больших двоичных объектов (emp.txt) в корневой папке hello контейнер больших двоичных объектов (adftutorial) в hello представленный hello AzureStorageLinkedService связанной службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-228">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="c3a43-229">Если не указать значение для имени файла hello (или пропустить его), данные из всех больших двоичных объектов в папке входной hello, скопированный toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="c3a43-229">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="c3a43-230">В этом учебнике укажите значение для имени файла hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-230">In this tutorial, you specify a value for hello fileName.</span></span>  

1. <span data-ttu-id="c3a43-231">Создайте JSON-файл с именем **InputDataset.json** в hello **C:\ADFGetStartedPSH** папке с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="c3a43-231">Create a JSON file named **InputDataset.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
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

    <span data-ttu-id="c3a43-232">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-232">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="c3a43-233">Свойство</span><span class="sxs-lookup"><span data-stu-id="c3a43-233">Property</span></span> | <span data-ttu-id="c3a43-234">Описание</span><span class="sxs-lookup"><span data-stu-id="c3a43-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="c3a43-235">type</span><span class="sxs-lookup"><span data-stu-id="c3a43-235">type</span></span> | <span data-ttu-id="c3a43-236">Hello свойство type установлено слишком**AzureBlob** , так как данные находятся в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c3a43-236">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="c3a43-237">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="c3a43-237">linkedServiceName</span></span> | <span data-ttu-id="c3a43-238">Указывает toohello **AzureStorageLinkedService** , созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="c3a43-238">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="c3a43-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="c3a43-239">folderPath</span></span> | <span data-ttu-id="c3a43-240">Указывает hello blob **контейнера** и hello **папки** , содержащий входного BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="c3a43-240">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="c3a43-241">В этом учебнике adftutorial — контейнер больших двоичных объектов hello и папка является корневой папкой hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-241">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="c3a43-242">fileName</span><span class="sxs-lookup"><span data-stu-id="c3a43-242">fileName</span></span> | <span data-ttu-id="c3a43-243">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="c3a43-243">This property is optional.</span></span> <span data-ttu-id="c3a43-244">Если это свойство не указан, извлекаются все файлы из hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="c3a43-244">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="c3a43-245">В этом учебнике **emp.txt** задается для hello имя файла, поэтому только этот файл будет выбрано для обработки.</span><span class="sxs-lookup"><span data-stu-id="c3a43-245">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="c3a43-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="c3a43-246">format -> type</span></span> |<span data-ttu-id="c3a43-247">Hello входной файл имеет текстовый формат hello, поэтому мы используем **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-247">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="c3a43-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c3a43-248">columnDelimiter</span></span> | <span data-ttu-id="c3a43-249">Hello столбцов во входном файле hello разделяются **запятая (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-249">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="c3a43-250">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="c3a43-250">frequency/interval</span></span> | <span data-ttu-id="c3a43-251">частота Hello задано слишком**час** и интервала задано слишком**1**, это означает, что hello ввода доступны срезы **каждый час**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-251">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="c3a43-252">Другими словами, hello служба фабрики данных ищет входных данных каждый час в корневой папке hello контейнер больших двоичных объектов (**adftutorial**) было задано.</span><span class="sxs-lookup"><span data-stu-id="c3a43-252">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="c3a43-253">Выполняет поиск данных hello в hello конвейера начального и конечного времени, не до или после этих значений времени.</span><span class="sxs-lookup"><span data-stu-id="c3a43-253">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="c3a43-254">external</span><span class="sxs-lookup"><span data-stu-id="c3a43-254">external</span></span> | <span data-ttu-id="c3a43-255">Это свойство задано слишком**true** Если hello данных в этом конвейере не создается.</span><span class="sxs-lookup"><span data-stu-id="c3a43-255">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="c3a43-256">в файле emp.txt hello, который создается в этом конвейере не, поэтому мы задали это свойство tootrue — Hello входных данных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c3a43-256">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="c3a43-257">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c3a43-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="c3a43-258">Запустите hello, следующая команда toocreate hello фабрики данных dataset.</span><span class="sxs-lookup"><span data-stu-id="c3a43-258">Run hello following command toocreate hello Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="c3a43-259">Вот пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-259">Here is hello sample output:</span></span>

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="c3a43-260">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="c3a43-260">Create an output dataset</span></span>
<span data-ttu-id="c3a43-261">В этой части hello шаг создания выходной набор данных с именем **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-261">In this part of hello step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="c3a43-262">Этот набор данных указывает tooa SQL таблицы в базе данных Azure SQL hello, представленного **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-262">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="c3a43-263">Создайте JSON-файл с именем **OutputDataset.json** в hello **C:\ADFGetStartedPSH** папка с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="c3a43-263">Create a JSON file named **OutputDataset.json** in hello **C:\ADFGetStartedPSH** folder with hello following content:</span></span>

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
            "linkedServiceName": "AzureSqlLinkedService",
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

    <span data-ttu-id="c3a43-264">Hello следующей таблице содержатся описания свойств JSON hello, используемых в фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-264">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="c3a43-265">Свойство</span><span class="sxs-lookup"><span data-stu-id="c3a43-265">Property</span></span> | <span data-ttu-id="c3a43-266">Описание</span><span class="sxs-lookup"><span data-stu-id="c3a43-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="c3a43-267">type</span><span class="sxs-lookup"><span data-stu-id="c3a43-267">type</span></span> | <span data-ttu-id="c3a43-268">Hello свойство type установлено слишком**AzureSqlTable** из-за данных скопированный tooa таблицы в базе данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c3a43-268">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="c3a43-269">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="c3a43-269">linkedServiceName</span></span> | <span data-ttu-id="c3a43-270">Указывает toohello **AzureSqlLinkedService** , созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="c3a43-270">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="c3a43-271">tableName</span><span class="sxs-lookup"><span data-stu-id="c3a43-271">tableName</span></span> | <span data-ttu-id="c3a43-272">Указанный hello **таблицы** toowhich hello данные копируются.</span><span class="sxs-lookup"><span data-stu-id="c3a43-272">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="c3a43-273">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="c3a43-273">frequency/interval</span></span> | <span data-ttu-id="c3a43-274">Hello задана слишком**час** и интервал — **1**, это означает, что hello срезы выходных данных создаются **каждый час** между hello конвейера начала и время окончания, не до или После этих значений времени.</span><span class="sxs-lookup"><span data-stu-id="c3a43-274">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="c3a43-275">Имеются три столбца — **идентификатор**, **FirstName**, и **LastName** — в таблице emp hello в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-275">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="c3a43-276">Идентификатор является столбцом идентификаторов, поэтому вам необходимо только toospecify **FirstName** и **LastName** здесь.</span><span class="sxs-lookup"><span data-stu-id="c3a43-276">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="c3a43-277">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c3a43-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="c3a43-278">Запустите следующий набор данных hello данных команды toocreate фабрики hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-278">Run hello following command toocreate hello data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="c3a43-279">Вот пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-279">Here is hello sample output:</span></span>

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="c3a43-280">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="c3a43-280">Create a pipeline</span></span>
<span data-ttu-id="c3a43-281">На этом этапе вы создадите конвейер с **действием копирования**, которое использует **InputDataset** в качестве входных данных и **OutputDataset** в качестве выходных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="c3a43-282">В настоящее время выходной набор данных — того, какие диски hello расписания.</span><span class="sxs-lookup"><span data-stu-id="c3a43-282">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="c3a43-283">В этом учебнике выходной набор данных является настроенным tooproduce срез один раз в час.</span><span class="sxs-lookup"><span data-stu-id="c3a43-283">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="c3a43-284">конвейер Hello содержит время начала и время окончания, которые однажды друг от друга, что составляет 24 часа.</span><span class="sxs-lookup"><span data-stu-id="c3a43-284">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="c3a43-285">Таким образом 24 фрагменты выходной набор данных создают hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="c3a43-285">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 


1. <span data-ttu-id="c3a43-286">Создайте JSON-файл с именем **ADFTutorialPipeline.json** в hello **C:\ADFGetStartedPSH** папке с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="c3a43-286">Create a JSON file named **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```
    <span data-ttu-id="c3a43-287">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="c3a43-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="c3a43-288">В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**копирования**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="c3a43-289">Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="c3a43-290">В решениях фабрики данных можно также использовать [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="c3a43-291">Входных данных для действия hello установлено слишком**InputDataset** и вывода для hello действия установлено слишком**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="c3a43-292">В hello **typeProperties** разделе **BlobSource** указан в качестве типа источника hello и **SqlSink** указан как тип приемника hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="c3a43-293">Перечень хранилищ данных, поддерживаемые действием копирования hello как источники и приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c3a43-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c3a43-294">как сохранить toouse конкретных поддерживаемые данные в качестве источника и приемника, toolearn по ссылке hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="c3a43-295">Замените значение hello hello **запустить** свойство с hello текущего дня и **окончания** значение с hello следующего дня.</span><span class="sxs-lookup"><span data-stu-id="c3a43-295">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="c3a43-296">Можно указать только часть даты hello и пропустить hello время hello Дата и время.</span><span class="sxs-lookup"><span data-stu-id="c3a43-296">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="c3a43-297">Например, «2016-02-03», который является эквивалентом "2016-02-03T00:00:00Z»</span><span class="sxs-lookup"><span data-stu-id="c3a43-297">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="c3a43-298">Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="c3a43-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="c3a43-299">Например, 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="c3a43-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="c3a43-300">Hello **окончания** времени является необязательным, но мы используем в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c3a43-300">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="c3a43-301">Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов**».</span><span class="sxs-lookup"><span data-stu-id="c3a43-301">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="c3a43-302">конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство.</span><span class="sxs-lookup"><span data-stu-id="c3a43-302">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="c3a43-303">В предыдущих пример hello существует 24 срезы данных, как каждый срез данных создается каждый час.</span><span class="sxs-lookup"><span data-stu-id="c3a43-303">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="c3a43-304">Описание свойств JSON в определении конвейера см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c3a43-305">Описание свойств JSON в определении действия копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="c3a43-306">Описание свойств JSON, поддерживаемых BlobSource, см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="c3a43-307">Описание свойств JSON, поддерживаемых SqlSink, см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="c3a43-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="c3a43-308">Выполнения hello следующая команда таблицу фабрики данных toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-308">Run hello following command toocreate hello data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="c3a43-309">Вот пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-309">Here is hello sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="c3a43-310">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="c3a43-310">**Congratulations!**</span></span> <span data-ttu-id="c3a43-311">Успешно создана фабрикой данных Azure с toocopy конвейера данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-311">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

## <a name="monitor-hello-pipeline"></a><span data-ttu-id="c3a43-312">Монитор hello конвейера</span><span class="sxs-lookup"><span data-stu-id="c3a43-312">Monitor hello pipeline</span></span>
<span data-ttu-id="c3a43-313">На этом шаге используется Azure PowerShell toomonitor происходящем в фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-313">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="c3a43-314">Замените &lt;с именем DataFactoryName&gt; с именем hello фабрику данных и выполнения **Get AzureRmDataFactory**и назначить переменной $df tooa hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-314">Replace &lt;DataFactoryName&gt; with hello name of your data factory and run **Get-AzureRmDataFactory**, and assign hello output tooa variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="c3a43-315">Например:</span><span class="sxs-lookup"><span data-stu-id="c3a43-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="c3a43-316">Затем выполните содержимое Здравствуй, мир hello toosee $df следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c3a43-316">Then, run print hello contents of $df toosee hello following output:</span></span> 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. <span data-ttu-id="c3a43-317">Запустите **Get AzureRmDataFactorySlice** tooget сведения о всех фрагментов hello **OutputDataset**, являющееся hello выходной набор данных конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-317">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **OutputDataset**, which is hello output dataset of hello pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="c3a43-318">Это значение должно соответствовать hello **запустить** значение hello конвейера JSON.</span><span class="sxs-lookup"><span data-stu-id="c3a43-318">This setting should match hello **Start** value in hello pipeline JSON.</span></span> <span data-ttu-id="c3a43-319">Вы увидите 24 срезов, один для каждого часа с 00: 00 для too12 текущий день hello AM из hello следующего дня.</span><span class="sxs-lookup"><span data-stu-id="c3a43-319">You should see 24 slices, one for each hour from 12 AM of hello current day too12 AM of hello next day.</span></span>

   <span data-ttu-id="c3a43-320">Ниже приведены три фрагмента образец hello в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-320">Here are three sample slices from hello output:</span></span> 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="c3a43-321">Запустите **Get AzureRmDataFactoryRun** tooget сведения hello действия выполняется для **конкретных** среза.</span><span class="sxs-lookup"><span data-stu-id="c3a43-321">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="c3a43-322">Скопируйте значение даты времени hello из выходных данных hello hello предыдущей команды toospecify hello значения для параметра StartDateTime hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-322">Copy hello date-time value from hello output of hello previous command toospecify hello value for hello StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="c3a43-323">Вот пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-323">Here is hello sample output:</span></span> 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

<span data-ttu-id="c3a43-324">Полную документацию по командлетам фабрики данных см. в [этом справочнике](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="c3a43-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="c3a43-325">Сводка</span><span class="sxs-lookup"><span data-stu-id="c3a43-325">Summary</span></span>
<span data-ttu-id="c3a43-326">В этом учебнике вы создали данных toocopy фабрики данных Azure из базы данных Azure SQL tooan BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a43-326">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="c3a43-327">Вы использовали фабрики данных hello toocreate PowerShell, связанные службы, наборы данных и конвейера.</span><span class="sxs-lookup"><span data-stu-id="c3a43-327">You used PowerShell toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="c3a43-328">Ниже приведены hello высокоуровневые действия, выполняемые в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c3a43-328">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="c3a43-329">Создание **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c3a43-330">Создание **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="c3a43-330">Created **linked services**:</span></span>

   <span data-ttu-id="c3a43-331">а.</span><span class="sxs-lookup"><span data-stu-id="c3a43-331">a.</span></span> <span data-ttu-id="c3a43-332">**Хранилища Azure** связанные службы toolink вашей учетной записи хранилища Azure, который содержит входные данные.</span><span class="sxs-lookup"><span data-stu-id="c3a43-332">An **Azure Storage** linked service toolink your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="c3a43-333">b.</span><span class="sxs-lookup"><span data-stu-id="c3a43-333">b.</span></span> <span data-ttu-id="c3a43-334">**Azure SQL** связанные toolink службы базы данных SQL, содержащий hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-334">An **Azure SQL** linked service toolink your SQL database that holds hello output data.</span></span>
3. <span data-ttu-id="c3a43-335">Создание **наборов данных** , которые описывают входные и выходные данные для конвейеров.</span><span class="sxs-lookup"><span data-stu-id="c3a43-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="c3a43-336">Создан **конвейера** с **действие копирования**, с **BlobSource** как источник hello и **SqlSink** как приемник hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as hello source and **SqlSink** as hello sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3a43-337">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3a43-337">Next steps</span></span>
<span data-ttu-id="c3a43-338">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="c3a43-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="c3a43-339">Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения:</span><span class="sxs-lookup"><span data-stu-id="c3a43-339">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="c3a43-340">toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="c3a43-340">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span> 

