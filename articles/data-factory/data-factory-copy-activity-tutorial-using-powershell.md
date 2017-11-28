---
title: "Руководство по созданию конвейера для переноса данных с помощью Azure PowerShell | Документация Майкрософт"
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
ms.openlocfilehash: 81efe7c6af29af778686e1f6bcf62fedc9711052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="41e5a-103">Руководство по созданию конвейера фабрики данных для переноса данных с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="41e5a-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41e5a-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="41e5a-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="41e5a-105">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="41e5a-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="41e5a-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="41e5a-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="41e5a-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="41e5a-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="41e5a-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="41e5a-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="41e5a-109">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="41e5a-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="41e5a-110">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="41e5a-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="41e5a-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="41e5a-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="41e5a-112">В этом руководстве показано, как создать фабрику данных c конвейером, который копирует данные из хранилища BLOB-объектов Azure, с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41e5a-112">In this article, you learn how to use PowerShell to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="41e5a-113">Если вы еще не работали с фабрикой данных Azure, перед выполнением действий, описанных в этом руководстве, ознакомьтесь со статьей [Введение в фабрику данных Azure](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="41e5a-114">В этом руководстве описывается создание конвейера с одним действием — действием копирования.</span><span class="sxs-lookup"><span data-stu-id="41e5a-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="41e5a-115">Действие копирования копирует данные из поддерживаемого хранилища данных в поддерживаемое хранилище данных-приемник.</span><span class="sxs-lookup"><span data-stu-id="41e5a-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="41e5a-116">Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="41e5a-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="41e5a-117">Это действие выполняется с помощью глобально доступной службы, обеспечивающей безопасное, надежное и масштабируемое копирование данных между разными хранилищами.</span><span class="sxs-lookup"><span data-stu-id="41e5a-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="41e5a-118">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="41e5a-119">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="41e5a-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="41e5a-120">Два действия можно объединить в цепочку (выполнить одно действие вслед за другим), настроив выходной набор данных одного действия как входной набор данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="41e5a-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="41e5a-121">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="41e5a-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="41e5a-122">В этой статье рассматриваются не все командлеты фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-122">This article does not cover all the Data Factory cmdlets.</span></span> <span data-ttu-id="41e5a-123">Полную документацию по этим командлетам см. в [справочнике](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="41e5a-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="41e5a-124">В этом руководстве конвейер данных копирует данные из исходного хранилища данных в целевое.</span><span class="sxs-lookup"><span data-stu-id="41e5a-124">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="41e5a-125">Инструкции по преобразованию данных с помощью фабрики данных Azure см. в [руководстве по созданию конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-125">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41e5a-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="41e5a-126">Prerequisites</span></span>
- <span data-ttu-id="41e5a-127">Выполните предварительные требования, перечисленные в [этом руководстве](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-127">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="41e5a-128">Установите **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="41e5a-129">Следуйте инструкциям по [установке и настройке Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-129">Follow the instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="41e5a-130">Действия</span><span class="sxs-lookup"><span data-stu-id="41e5a-130">Steps</span></span>
<span data-ttu-id="41e5a-131">Ниже приведены шаги, которые вы выполните в процессе работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="41e5a-131">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="41e5a-132">Создайте **фабрику данных** Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="41e5a-133">На этом этапе вы создадите фабрику данных Azure с именем ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="41e5a-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="41e5a-134">Создайте в этой фабрике данных **связанные службы**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-134">Create **linked services** in the data factory.</span></span> <span data-ttu-id="41e5a-135">На этом этапе вы создадите две связанные службы — службу хранилища Azure и базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="41e5a-136">Связанная служба хранилища Azure связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-136">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="41e5a-137">Вы создали контейнер и отправили данные в эту учетную запись хранения в ходе выполнения предварительных [требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-137">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="41e5a-138">Связанная служба SQL Azure связывает базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-138">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="41e5a-139">В этой базе данных хранятся данные, скопированные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="41e5a-139">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="41e5a-140">Вы создали таблицу SQL в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="41e5a-141">Создайте в фабрике данных входные и выходные **наборы данных**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-141">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="41e5a-142">Связанная служба хранилища Azure указывает строку подключения, которую фабрика данных использует во время выполнения, чтобы подключиться к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-142">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="41e5a-143">А входной набор данных больших двоичных объектов определяет контейнер и папку с входными данными.</span><span class="sxs-lookup"><span data-stu-id="41e5a-143">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="41e5a-144">Аналогичным образом связанная служба базы данных SQL Azure указывает строку подключения, которую служба фабрики данных использует во время выполнения, чтобы подключиться к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-144">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="41e5a-145">А выходной набор данных таблицы SQL определяет таблицу в базе данных, в которую копируются данные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="41e5a-145">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
4. <span data-ttu-id="41e5a-146">Создайте **конвейер** в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-146">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="41e5a-147">На этом этапе вы создадите конвейер с действием копирования.</span><span class="sxs-lookup"><span data-stu-id="41e5a-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="41e5a-148">Действие копирования копирует данные из большого двоичного объекта из хранилища BLOB-объектов Azure в таблицу в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-148">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="41e5a-149">Его можно использовать, чтобы копировать данные из любого поддерживаемого источника в любое расположение.</span><span class="sxs-lookup"><span data-stu-id="41e5a-149">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="41e5a-150">Список поддерживаемых хранилищ данных см. в [этом разделе](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="41e5a-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="41e5a-151">Выполните мониторинг конвейера.</span><span class="sxs-lookup"><span data-stu-id="41e5a-151">Monitor the pipeline.</span></span> <span data-ttu-id="41e5a-152">На этом этапе вы **отследите** срезы входных и выходных наборов данных с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41e5a-152">In this step, you **monitor** the slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="41e5a-153">Создать фабрику данных</span><span class="sxs-lookup"><span data-stu-id="41e5a-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="41e5a-154">Выполните [предварительные требования, необходимые для работы с этим руководством](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="41e5a-154">Complete [prerequisites for the tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="41e5a-155">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="41e5a-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="41e5a-156">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="41e5a-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="41e5a-157">Это может быть, например, действие копирования данных из исходного хранилища в целевое или действие HDInsight Hive для выполнения скрипта Hive, преобразующего входные данные в выходные данные продукта.</span><span class="sxs-lookup"><span data-stu-id="41e5a-157">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="41e5a-158">Начнем с создания фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-158">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="41e5a-159">Запустите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-159">Launch **PowerShell**.</span></span> <span data-ttu-id="41e5a-160">Не закрывайте Azure PowerShell, пока выполняются описанные в учебнике инструкции.</span><span class="sxs-lookup"><span data-stu-id="41e5a-160">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="41e5a-161">Если закрыть и снова открыть это окно, то придется вновь выполнять эти команды.</span><span class="sxs-lookup"><span data-stu-id="41e5a-161">If you close and reopen, you need to run the commands again.</span></span>

    <span data-ttu-id="41e5a-162">Выполните следующую команду и введите имя пользователя и пароль, которые используются для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-162">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="41e5a-163">Чтобы просмотреть все подписки для этой учетной записи, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="41e5a-163">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="41e5a-164">Выполните следующую команду, чтобы выбрать подписку, с которой вы собираетесь работать.</span><span class="sxs-lookup"><span data-stu-id="41e5a-164">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="41e5a-165">Замените **&lt;NameOfAzureSubscription**&gt; именем своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-165">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="41e5a-166">Создайте группу ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="41e5a-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="41e5a-167">Некоторые действия, описанные в этом учебнике, предполагают, что вы используете группу ресурсов с именем **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-167">Some of the steps in this tutorial assume that you use the resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="41e5a-168">Если вы используете другую группу ресурсов, укажите ее вместо ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="41e5a-168">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="41e5a-169">Выполните командлет **New-AzureRmDataFactory**, чтобы создать фабрику данных с именем **ADFTutorialDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-169">Run the **New-AzureRmDataFactory** cmdlet to create a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="41e5a-170">Это имя уже может использоваться.</span><span class="sxs-lookup"><span data-stu-id="41e5a-170">This name may already have been taken.</span></span> <span data-ttu-id="41e5a-171">В этом случае присвойте фабрике данных уникальное имя, добавив к нему префикс или суффикс (например, ADFTutorialDataFactoryPSH05152017), и выполните команду еще раз.</span><span class="sxs-lookup"><span data-stu-id="41e5a-171">Therefore, make the name of the data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run the command again.</span></span>  

<span data-ttu-id="41e5a-172">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="41e5a-172">Note the following points:</span></span>

* <span data-ttu-id="41e5a-173">Имя фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="41e5a-173">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="41e5a-174">При возникновении следующей ошибки измените имя (например, на ваше_имя_ADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="41e5a-174">If you receive the following error, change the name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="41e5a-175">Используйте это имя вместо ADFTutorialFactoryPSH при выполнении шагов в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="41e5a-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="41e5a-176">Ознакомьтесь с [правилами именования](data-factory-naming-rules.md) артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="41e5a-177">Чтобы создавать экземпляры фабрики данных, вы должны быть участником или администратором подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-177">To create Data Factory instances, you must be a contributor or administrator of the Azure subscription.</span></span>
* <span data-ttu-id="41e5a-178">В будущем имя фабрики данных может быть зарегистрировано в качестве DNS-имени и, следовательно, стать отображаемым.</span><span class="sxs-lookup"><span data-stu-id="41e5a-178">The name of the data factory may be registered as a DNS name in the future, and hence become publicly visible.</span></span>
* <span data-ttu-id="41e5a-179">Может появиться сообщение об ошибке **Подписка не зарегистрирована для использования пространства имен "Microsoft.DataFactory"**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-179">You may receive the following error: "**This subscription is not registered to use namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="41e5a-180">В этом случае выполните одно из следующих действий и повторите попытку публикации.</span><span class="sxs-lookup"><span data-stu-id="41e5a-180">Do one of the following, and try publishing again:</span></span>

  * <span data-ttu-id="41e5a-181">Чтобы зарегистрировать поставщик фабрики данных Azure, выполните следующую команду в Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="41e5a-181">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="41e5a-182">Чтобы убедиться, что поставщик фабрики данных зарегистрирован, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="41e5a-182">Run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="41e5a-183">Войдите на [портал Azure](https://portal.azure.com), используя свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-183">Sign in by using the Azure subscription to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="41e5a-184">Откройте колонку фабрики данных или создайте фабрику данных на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-184">Go to a Data Factory blade, or create a data factory in the Azure portal.</span></span> <span data-ttu-id="41e5a-185">Поставщик будет зарегистрирован автоматически.</span><span class="sxs-lookup"><span data-stu-id="41e5a-185">This action automatically registers the provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="41e5a-186">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="41e5a-186">Create linked services</span></span>
<span data-ttu-id="41e5a-187">Связанная служба в фабрике данных связывает хранилища данных и службы вычислений с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-187">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="41e5a-188">В этом руководстве не используются службы вычислений, например Azure HDInsight или Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="41e5a-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="41e5a-189">Вы используете два хранилища данных — служба хранилища Azure (источник) и база данных SQL Azure (конечное хранилище).</span><span class="sxs-lookup"><span data-stu-id="41e5a-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="41e5a-190">Поэтому нужно создать две связанные службы: служба хранилища Azure с именем AzureStorageLinkedService и база данных SQL Azure с именем AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="41e5a-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="41e5a-191">Связанная служба хранилища Azure связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-191">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="41e5a-192">В этой учетной записи хранения вы создали контейнер и отправили в нее данные в ходе выполнения предварительных [требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-192">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="41e5a-193">Связанная служба SQL Azure связывает базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-193">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="41e5a-194">В этой базе данных хранятся данные, скопированные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="41e5a-194">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="41e5a-195">Вы создали пустую таблицу в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-195">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="41e5a-196">Создание связанной службы для учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="41e5a-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="41e5a-197">На этом шаге вы свяжете учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-197">In this step, you link your Azure storage account to your data factory.</span></span>

1. <span data-ttu-id="41e5a-198">Создайте JSON-файл с именем **AzureStorageLinkedService.json** в папке **C:\ADFGetStartedPSH** и добавьте в него приведенное ниже содержимое. Если папка ADFGetStartedPSH отсутствует, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="41e5a-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with the following content: (Create the folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="41e5a-199">Перед сохранением файла замените значения &lt;accountname&gt; и &lt;accountkey&gt; на имя вашей учетной записи хранения Azure и ее ключ.</span><span class="sxs-lookup"><span data-stu-id="41e5a-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving the file.</span></span> 

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
2. <span data-ttu-id="41e5a-200">В **Azure PowerShell** перейдите в папку **ADFGetStartedPSH**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-200">In **Azure PowerShell**, switch to the **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="41e5a-201">Выполните командлет **New-AzureRmDataFactoryLinkedService**, чтобы создать связанную службу **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-201">Run the **New-AzureRmDataFactoryLinkedService** cmdlet to create the linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="41e5a-202">В этом и в других командлетах фабрики данных, которые используются в этом руководстве, требуется передача значений для параметров **ResourceGroupName** и **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you to pass values for the **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="41e5a-203">Кроме того, вы можете передать объект DataFactory, возвращенный командлетом New-AzureRmDataFactory, не вводя параметры ResourceGroupName и DataFactoryName при каждом запуске командлета.</span><span class="sxs-lookup"><span data-stu-id="41e5a-203">Alternatively, you can pass the DataFactory object returned by the New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="41e5a-204">Пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="41e5a-204">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="41e5a-205">Связанную службу можно создать и другим способом. Вместо объекта DataFactory укажите имя группы ресурсов и фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-205">Other way of creating this linked service is to specify resource group name and data factory name instead of specifying the DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="41e5a-206">Создание связанной службы для Базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="41e5a-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="41e5a-207">На этом шаге вы свяжете базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-207">In this step, you link your Azure SQL database to your data factory.</span></span>

1. <span data-ttu-id="41e5a-208">Создайте в папке C:\ADFGetStartedPSH файл JSON с именем AzureSqlLinkedService.json и добавьте в него приведенное ниже содержимое.</span><span class="sxs-lookup"><span data-stu-id="41e5a-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with the following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="41e5a-209">Вместо &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; и &lt;password&gt; укажите имя своего сервера Azure SQL Server, имя базы данных, имя учетной записи пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="41e5a-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
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
2. <span data-ttu-id="41e5a-210">Чтобы создать связанную службу, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="41e5a-210">Run the following command to create a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="41e5a-211">Пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="41e5a-211">Here is the sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="41e5a-212">Убедитесь, что для сервера базы данных SQL включен параметр **Разрешить доступ к службам Azure**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-212">Confirm that **Allow access to Azure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="41e5a-213">Чтобы проверить и при необходимости включить этот параметр, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="41e5a-213">To verify and turn it on, do the following steps:</span></span>

    1. <span data-ttu-id="41e5a-214">Войдите на [портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="41e5a-214">Log in to the [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="41e5a-215">Щелкните **Больше служб** слева и выберите **Серверы SQL** в категории **Базы данных**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-215">Click **More services >** on the left, and click **SQL servers** in the **DATABASES** category.</span></span>
    3. <span data-ttu-id="41e5a-216">Выберите в списке свой сервер SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41e5a-216">Select your server in the list of SQL servers.</span></span>
    4. <span data-ttu-id="41e5a-217">В колонке SQL Server щелкните ссылку **Показать параметры брандмауэра**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-217">On the SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="41e5a-218">В колонке **Параметры брандмауэра** щелкните **ВКЛ** для параметра **Разрешить доступ к службам Azure**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-218">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
    6. <span data-ttu-id="41e5a-219">Нажмите кнопку **Сохранить** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="41e5a-219">Click **Save** on the toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="41e5a-220">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="41e5a-220">Create datasets</span></span>
<span data-ttu-id="41e5a-221">На предыдущем шаге вы создали связанные службы, связывающие учетную запись хранения Azure и базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-221">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="41e5a-222">На этом этапе вы определите два набора данных (InputDataset и OutputDataset), представляющие входные и выходные данные в хранилищах данных, на которые ссылаются службы AzureStorageLinkedService и AzureSqlLinkedService соответственно.</span><span class="sxs-lookup"><span data-stu-id="41e5a-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="41e5a-223">Связанная служба хранилища Azure указывает строку подключения, которую фабрика данных использует во время выполнения, чтобы подключиться к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-223">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="41e5a-224">А входной набор данных больших двоичных объектов (InputDataset) определяет контейнер и папку с входными данными.</span><span class="sxs-lookup"><span data-stu-id="41e5a-224">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="41e5a-225">Аналогичным образом связанная служба базы данных SQL Azure указывает строку подключения, которую служба фабрики данных использует во время выполнения, чтобы подключиться к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-225">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="41e5a-226">А выходной набор данных таблицы SQL (OututDataset) определяет таблицу в базе данных, в которую копируются данные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="41e5a-226">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="41e5a-227">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="41e5a-227">Create an input dataset</span></span>
<span data-ttu-id="41e5a-228">На этом этапе вы создадите набор данных с именем InputDataset. Он указывает на файл большого двоичного объекта (emp.txt) в корневой папке контейнера больших двоичных объектов в службе хранилища Azure, которая представлена связанной службой AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="41e5a-228">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="41e5a-229">Если не указать значение fileName (или пропустить его), данные из всех больших двоичных объектов в папке входных данных копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="41e5a-229">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="41e5a-230">В этом руководстве вы укажете значение параметра fileName.</span><span class="sxs-lookup"><span data-stu-id="41e5a-230">In this tutorial, you specify a value for the fileName.</span></span>  

1. <span data-ttu-id="41e5a-231">Создайте файл JSON с именем **InputDataset.json** в папке **C:\ADFGetStartedPSH** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="41e5a-231">Create a JSON file named **InputDataset.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

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

    <span data-ttu-id="41e5a-232">В следующей таблице приведены описания свойств JSON, используемых в этом фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="41e5a-232">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="41e5a-233">Свойство</span><span class="sxs-lookup"><span data-stu-id="41e5a-233">Property</span></span> | <span data-ttu-id="41e5a-234">Описание</span><span class="sxs-lookup"><span data-stu-id="41e5a-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="41e5a-235">type</span><span class="sxs-lookup"><span data-stu-id="41e5a-235">type</span></span> | <span data-ttu-id="41e5a-236">Для свойства типа задано значение **AzureBlob**, так как данные хранятся в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-236">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="41e5a-237">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="41e5a-237">linkedServiceName</span></span> | <span data-ttu-id="41e5a-238">Ссылается на созданную ранее службу **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-238">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="41e5a-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="41e5a-239">folderPath</span></span> | <span data-ttu-id="41e5a-240">Определяет **контейнер** больших двоичных объектов и **папку**, которая содержит входные большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="41e5a-240">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="41e5a-241">В этом руководстве adftutorial — это контейнер больших двоичных объектов, а созданная папка является корневой.</span><span class="sxs-lookup"><span data-stu-id="41e5a-241">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="41e5a-242">fileName</span><span class="sxs-lookup"><span data-stu-id="41e5a-242">fileName</span></span> | <span data-ttu-id="41e5a-243">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="41e5a-243">This property is optional.</span></span> <span data-ttu-id="41e5a-244">Если это свойство не указано, выбираются все файлы из папки folderPath.</span><span class="sxs-lookup"><span data-stu-id="41e5a-244">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="41e5a-245">В этом руководстве для свойства fileName указывается значение **emp.txt**, чтобы обрабатывался только этот файл.</span><span class="sxs-lookup"><span data-stu-id="41e5a-245">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="41e5a-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="41e5a-246">format -> type</span></span> |<span data-ttu-id="41e5a-247">Входной файл имеет текстовый формат, поэтому укажите значение **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-247">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="41e5a-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="41e5a-248">columnDelimiter</span></span> | <span data-ttu-id="41e5a-249">Столбцы во входном файле разделяются **запятыми (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-249">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="41e5a-250">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="41e5a-250">frequency/interval</span></span> | <span data-ttu-id="41e5a-251">Для свойства frequency задано значение **Hour**, а для свойства interval — значение **1**. Это означает, что срезы входных данных будут создаваться **каждый час**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-251">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="41e5a-252">Иными словами, служба фабрики данных будет искать входные данные в корневой папке указанного контейнера BLOB-объектов (**adftutorial**) каждый час.</span><span class="sxs-lookup"><span data-stu-id="41e5a-252">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="41e5a-253">Поиск данных осуществляется в пределах времени начала и времени окончания для конвейера, но не перед этим периодом или после него.</span><span class="sxs-lookup"><span data-stu-id="41e5a-253">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="41e5a-254">external</span><span class="sxs-lookup"><span data-stu-id="41e5a-254">external</span></span> | <span data-ttu-id="41e5a-255">Это свойство имеет значение **true**, если этот конвейер не создает данные.</span><span class="sxs-lookup"><span data-stu-id="41e5a-255">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="41e5a-256">В этом руководстве входные данные находятся в файле emp.txt, который не создается этим конвейером, поэтому мы присвоим этому свойству значение true.</span><span class="sxs-lookup"><span data-stu-id="41e5a-256">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="41e5a-257">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="41e5a-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="41e5a-258">Выполните следующую команду для создания набора данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-258">Run the following command to create the Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="41e5a-259">Пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="41e5a-259">Here is the sample output:</span></span>

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

### <a name="create-an-output-dataset"></a><span data-ttu-id="41e5a-260">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="41e5a-260">Create an output dataset</span></span>
<span data-ttu-id="41e5a-261">На этом этапе мы создадим выходной набор данных с именем **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-261">In this part of the step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="41e5a-262">Этот набор данных указывает на таблицу SQL в базе данных SQL Azure (представлена значением **AzureSqlLinkedService**).</span><span class="sxs-lookup"><span data-stu-id="41e5a-262">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="41e5a-263">Создайте файл JSON с именем **OutputDataset.json** в папке **C:\ADFGetStartedPSH** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="41e5a-263">Create a JSON file named **OutputDataset.json** in the **C:\ADFGetStartedPSH** folder with the following content:</span></span>

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

    <span data-ttu-id="41e5a-264">В следующей таблице приведены описания свойств JSON, используемых в этом фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="41e5a-264">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="41e5a-265">Свойство</span><span class="sxs-lookup"><span data-stu-id="41e5a-265">Property</span></span> | <span data-ttu-id="41e5a-266">Описание</span><span class="sxs-lookup"><span data-stu-id="41e5a-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="41e5a-267">type</span><span class="sxs-lookup"><span data-stu-id="41e5a-267">type</span></span> | <span data-ttu-id="41e5a-268">Свойство type имеет значение **AzureSqlTable**, так как данные копируются в таблицу в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-268">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="41e5a-269">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="41e5a-269">linkedServiceName</span></span> | <span data-ttu-id="41e5a-270">Ссылается на созданную ранее службу **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-270">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="41e5a-271">tableName</span><span class="sxs-lookup"><span data-stu-id="41e5a-271">tableName</span></span> | <span data-ttu-id="41e5a-272">Указывает **таблицу**, в которую копируются данные.</span><span class="sxs-lookup"><span data-stu-id="41e5a-272">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="41e5a-273">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="41e5a-273">frequency/interval</span></span> | <span data-ttu-id="41e5a-274">Для свойства frequency задано значение **Hour**, а для interval — **1**. Это означает, что срезы выходных данных создаются **каждый час** в пределах времени начала и времени окончания для конвейера, но не перед этим периодом или после него.</span><span class="sxs-lookup"><span data-stu-id="41e5a-274">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="41e5a-275">В таблице emp в базе данных есть три столбца: **ID**, **FirstName** и **LastName**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-275">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="41e5a-276">ID — это столбец для идентификаторов, поэтому здесь вам нужно указать только значения **FirstName** и **LastName**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-276">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="41e5a-277">Дополнительные сведения об этих свойствах JSON см. в [этом разделе](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="41e5a-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="41e5a-278">Выполните следующую команду для создания набора данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-278">Run the following command to create the data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="41e5a-279">Пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="41e5a-279">Here is the sample output:</span></span>

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

## <a name="create-a-pipeline"></a><span data-ttu-id="41e5a-280">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="41e5a-280">Create a pipeline</span></span>
<span data-ttu-id="41e5a-281">На этом этапе вы создадите конвейер с **действием копирования**, которое использует **InputDataset** в качестве входных данных и **OutputDataset** в качестве выходных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="41e5a-282">Сейчас на основе этого набора настраивается расписание.</span><span class="sxs-lookup"><span data-stu-id="41e5a-282">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="41e5a-283">В этом руководстве выходной набор данных создает срез раз в час.</span><span class="sxs-lookup"><span data-stu-id="41e5a-283">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="41e5a-284">Для конвейера настроено время начала и время окончания с разницей в сутки.</span><span class="sxs-lookup"><span data-stu-id="41e5a-284">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="41e5a-285">Таким образом, конвейер создает 24 среза для выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-285">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 


1. <span data-ttu-id="41e5a-286">Создайте файл JSON с именем **ADFTutorialPipeline.json** в папке **C:\ADFGetStartedPSH** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="41e5a-286">Create a JSON file named **ADFTutorialPipeline.json** in the **C:\ADFGetStartedPSH** folder, with the following content:</span></span>

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
    <span data-ttu-id="41e5a-287">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="41e5a-287">Note the following points:</span></span>
   
    - <span data-ttu-id="41e5a-288">В разделе действий доступно только одно действие, параметр **type** которого имеет значение **Copy**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="41e5a-289">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-289">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="41e5a-290">В решениях фабрики данных можно также использовать [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="41e5a-291">Для этого действия параметру input присвоено значение **InputDataset**, а параметру output — значение **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-291">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="41e5a-292">В разделе **typeProperties** в качестве типа источника указано **BlobSource**, а в качестве типа приемника — **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-292">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="41e5a-293">Список хранилищ данных, поддерживаемых действием копирования в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="41e5a-293">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="41e5a-294">Чтобы узнать, как использовать конкретное хранилище данных в качестве источника или приемника, щелкните ссылку в таблице.</span><span class="sxs-lookup"><span data-stu-id="41e5a-294">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
     
    <span data-ttu-id="41e5a-295">Замените значение свойства **start** текущей датой, а значение свойства **end** — датой следующего дня.</span><span class="sxs-lookup"><span data-stu-id="41e5a-295">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="41e5a-296">Можно указать только часть даты и пропустить временную часть указанной даты и времени.</span><span class="sxs-lookup"><span data-stu-id="41e5a-296">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="41e5a-297">Например, 2016-02-03, что эквивалентно 2016-02-03T00:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="41e5a-297">For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="41e5a-298">Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="41e5a-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="41e5a-299">Например, 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="41e5a-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="41e5a-300">Время **окончания** указывать не обязательно, однако в этом примере мы будем его использовать.</span><span class="sxs-lookup"><span data-stu-id="41e5a-300">The **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="41e5a-301">Если не указать значение свойства **end**, оно вычисляется по формуле "**время начала + 48 часов**".</span><span class="sxs-lookup"><span data-stu-id="41e5a-301">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="41e5a-302">Чтобы запустить конвейер в течение неопределенного срока, укажите значение **9999-09-09** в качестве значения свойства **end**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-302">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="41e5a-303">В примере выше получено 24 среза данных, так как они создаются каждый час.</span><span class="sxs-lookup"><span data-stu-id="41e5a-303">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="41e5a-304">Описание свойств JSON в определении конвейера см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="41e5a-305">Описание свойств JSON в определении действия копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="41e5a-306">Описание свойств JSON, поддерживаемых BlobSource, см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="41e5a-307">Описание свойств JSON, поддерживаемых SqlSink, см. в статье о [соединителе базы данных SQL Azure](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="41e5a-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="41e5a-308">Выполните следующую команду для создания таблицы фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-308">Run the following command to create the data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="41e5a-309">Пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="41e5a-309">Here is the sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="41e5a-310">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="41e5a-310">**Congratulations!**</span></span> <span data-ttu-id="41e5a-311">Фабрика данных Azure с конвейером, который копирует данные из хранилища BLOB-объектов Azure в базу данных SQL Azure, успешно создана.</span><span class="sxs-lookup"><span data-stu-id="41e5a-311">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

## <a name="monitor-the-pipeline"></a><span data-ttu-id="41e5a-312">Мониторинг конвейера</span><span class="sxs-lookup"><span data-stu-id="41e5a-312">Monitor the pipeline</span></span>
<span data-ttu-id="41e5a-313">На этом шаге Azure PowerShell будет использоваться для мониторинга процессов в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-313">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="41e5a-314">Замените &lt;DataFactoryName&gt; именем своей фабрики данных. Выполните командлет **Get-AzureRmDataFactory** и назначьте выходные данные переменной $df.</span><span class="sxs-lookup"><span data-stu-id="41e5a-314">Replace &lt;DataFactoryName&gt; with the name of your data factory and run **Get-AzureRmDataFactory**, and assign the output to a variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="41e5a-315">Например:</span><span class="sxs-lookup"><span data-stu-id="41e5a-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="41e5a-316">Затем выведите содержимое $df и просмотрите следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="41e5a-316">Then, run print the contents of $df to see the following output:</span></span> 
    
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
2. <span data-ttu-id="41e5a-317">Выполните командлет **Get-AzureRmDataFactorySlice**, чтобы получить сведения обо всех срезах набора данных **OutputDataset**, который является выходным набором конвейера.</span><span class="sxs-lookup"><span data-stu-id="41e5a-317">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **OutputDataset**, which is the output dataset of the pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="41e5a-318">Это значение должно соответствовать значению параметра **Start** в JSON-файле конвейера.</span><span class="sxs-lookup"><span data-stu-id="41e5a-318">This setting should match the **Start** value in the pipeline JSON.</span></span> <span data-ttu-id="41e5a-319">Вы увидите 24 среза — по одному для каждого часа с 00:00 текущего дня до 00:00 следующего дня.</span><span class="sxs-lookup"><span data-stu-id="41e5a-319">You should see 24 slices, one for each hour from 12 AM of the current day to 12 AM of the next day.</span></span>

   <span data-ttu-id="41e5a-320">Ниже приведены три примера срезов из выходных данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-320">Here are three sample slices from the output:</span></span> 

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
3. <span data-ttu-id="41e5a-321">Выполните командлет **Get-AzureRmDataFactoryRun**, чтобы получить сведения о действиях, выполняемых для **конкретного** среза.</span><span class="sxs-lookup"><span data-stu-id="41e5a-321">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="41e5a-322">Скопируйте значение даты и времени в выходных данных предыдущей команды, чтобы задать значение параметра StartDateTime.</span><span class="sxs-lookup"><span data-stu-id="41e5a-322">Copy the date-time value from the output of the previous command to specify the value for the StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="41e5a-323">Пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="41e5a-323">Here is the sample output:</span></span> 

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

<span data-ttu-id="41e5a-324">Полную документацию по командлетам фабрики данных см. в [этом справочнике](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="41e5a-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="41e5a-325">Сводка</span><span class="sxs-lookup"><span data-stu-id="41e5a-325">Summary</span></span>
<span data-ttu-id="41e5a-326">В этом учебнике вы создали фабрику данных Azure для копирования данных из большого двоичного объекта Azure в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="41e5a-326">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="41e5a-327">Вы использовали PowerShell для создания фабрики данных, связанных служб, наборов данных и конвейера.</span><span class="sxs-lookup"><span data-stu-id="41e5a-327">You used PowerShell to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="41e5a-328">Вот обобщенные действия, которые вы выполнили в этом руководстве:</span><span class="sxs-lookup"><span data-stu-id="41e5a-328">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="41e5a-329">Создание **фабрики данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="41e5a-330">Создание **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-330">Created **linked services**:</span></span>

   <span data-ttu-id="41e5a-331">а.</span><span class="sxs-lookup"><span data-stu-id="41e5a-331">a.</span></span> <span data-ttu-id="41e5a-332">**Служба хранилища Azure** — создание связанной службы для связи с учетной записью хранения Azure, которая содержит входные данные.</span><span class="sxs-lookup"><span data-stu-id="41e5a-332">An **Azure Storage** linked service to link your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="41e5a-333">b.</span><span class="sxs-lookup"><span data-stu-id="41e5a-333">b.</span></span> <span data-ttu-id="41e5a-334">**SQL Azure** — создание связанной службы для связи с Базой данных SQL Azure, которая содержит выходные данные.</span><span class="sxs-lookup"><span data-stu-id="41e5a-334">An **Azure SQL** linked service to link your SQL database that holds the output data.</span></span>
3. <span data-ttu-id="41e5a-335">Создание **наборов данных** , которые описывают входные и выходные данные для конвейеров.</span><span class="sxs-lookup"><span data-stu-id="41e5a-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="41e5a-336">Создание **конвейера** с **BlobSource** в качестве источника и **SqlSink** в качестве приемника с помощью **действия копирования**.</span><span class="sxs-lookup"><span data-stu-id="41e5a-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as the source and **SqlSink** as the sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41e5a-337">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41e5a-337">Next steps</span></span>
<span data-ttu-id="41e5a-338">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="41e5a-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="41e5a-339">В следующей таблице приведен список хранилищ данных, которые поддерживаются в качестве источников и целевых расположений для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="41e5a-339">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="41e5a-340">Чтобы получить дополнительные сведения о том, как скопировать данные в хранилище данных или из него, щелкните ссылку для хранилища данных в таблице.</span><span class="sxs-lookup"><span data-stu-id="41e5a-340">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span> 

