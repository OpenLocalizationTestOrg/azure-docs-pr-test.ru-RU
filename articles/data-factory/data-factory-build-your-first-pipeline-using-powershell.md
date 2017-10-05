---
title: "Создание первой фабрики данных (PowerShell) | Документация Майкрософт"
description: "В этом руководстве вы создадите образец конвейера фабрики данных Azure с помощью Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 40a63339be90d0c5d972605c7f6fa029ca1e2ba4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="fda0b-103">Руководство. Создание первой фабрики данных Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fda0b-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fda0b-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fda0b-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="fda0b-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="fda0b-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="fda0b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fda0b-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="fda0b-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fda0b-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="fda0b-108">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fda0b-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="fda0b-109">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="fda0b-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="fda0b-110">Из этой статьи вы узнаете, как создать свою первую фабрику данных с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fda0b-110">In this article, you use Azure PowerShell to create your first Azure data factory.</span></span> <span data-ttu-id="fda0b-111">Чтобы выполнить приведенные здесь инструкции с помощью других средств или пакетов SDK, выберите в раскрывающемся списке один из доступных вариантов.</span><span class="sxs-lookup"><span data-stu-id="fda0b-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="fda0b-112">В этом руководстве конвейеру доступно одно действие — **действие Hive HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="fda0b-113">Это действие запускает сценарий Hive в кластере HDInsight Azure, который преобразует входные данные в выходные.</span><span class="sxs-lookup"><span data-stu-id="fda0b-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="fda0b-114">Конвейер запускается раз в месяц по расписанию. Время начала и окончания запуска также указаны.</span><span class="sxs-lookup"><span data-stu-id="fda0b-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="fda0b-115">В этом руководстве конвейер данных преобразовывает входные данные в выходные.</span><span class="sxs-lookup"><span data-stu-id="fda0b-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="fda0b-116">Он не копирует данные из исходного хранилища данных в целевое.</span><span class="sxs-lookup"><span data-stu-id="fda0b-116">It does not copy data from a source data store to a destination data store.</span></span> <span data-ttu-id="fda0b-117">Инструкции по копированию данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных Azure см. в [этой статье](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="fda0b-117">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="fda0b-118">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="fda0b-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="fda0b-119">Два действия можно объединить в цепочку (выполнить одно действие вслед за другим), настроив выходной набор данных одного действия как входной набор данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="fda0b-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="fda0b-120">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="fda0b-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fda0b-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fda0b-121">Prerequisites</span></span>
* <span data-ttu-id="fda0b-122">Прочтите [обзорную статью](data-factory-build-your-first-pipeline.md) и выполните **предварительные требования** .</span><span class="sxs-lookup"><span data-stu-id="fda0b-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="fda0b-123">Чтобы установить последнюю версию Azure PowerShell на локальном компьютере, следуйте инструкциям в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="fda0b-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="fda0b-124">В этой статье рассматриваются не все командлеты фабрики данных (необязательный раздел).</span><span class="sxs-lookup"><span data-stu-id="fda0b-124">(optional) This article does not cover all the Data Factory cmdlets.</span></span> <span data-ttu-id="fda0b-125">Полную документацию по командлетам фабрики данных см. в [этом справочнике](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="fda0b-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="fda0b-126">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="fda0b-126">Create data factory</span></span>
<span data-ttu-id="fda0b-127">На этом этапе с помощью Azure PowerShell создается фабрика данных Azure с именем **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-127">In this step, you use Azure PowerShell to create an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="fda0b-128">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="fda0b-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="fda0b-129">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="fda0b-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="fda0b-130">Это может быть, например, действие копирования данных из исходного хранилища в целевое или действие HDInsight Hive для выполнения скрипта Hive, преобразующего входные данные.</span><span class="sxs-lookup"><span data-stu-id="fda0b-130">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span></span> <span data-ttu-id="fda0b-131">Начнем с создания фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-131">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="fda0b-132">Откройте Azure PowerShell и выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="fda0b-132">Start Azure PowerShell and run the following command.</span></span> <span data-ttu-id="fda0b-133">Не закрывайте Azure PowerShell, пока выполняются описанные в учебнике инструкции.</span><span class="sxs-lookup"><span data-stu-id="fda0b-133">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="fda0b-134">Если закрыть и снова открыть это окно, то придется вновь выполнять эти команды.</span><span class="sxs-lookup"><span data-stu-id="fda0b-134">If you close and reopen, you need to run these commands again.</span></span>
   * <span data-ttu-id="fda0b-135">Выполните следующую команду и введите имя пользователя и пароль, которые используются для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fda0b-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="fda0b-136">Выполните следующую команду, чтобы просмотреть все подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="fda0b-136">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="fda0b-137">Выполните следующую команду, чтобы выбрать подписку, с которой вы собираетесь работать.</span><span class="sxs-lookup"><span data-stu-id="fda0b-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="fda0b-138">Эта подписка должна совпадать с той, которая используется на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="fda0b-138">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="fda0b-139">Создайте группу ресурсов Azure с именем **ADFTutorialResourceGroup** , выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fda0b-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="fda0b-140">Некоторые действия, описанные в этом учебнике, предполагают, что вы используете группу ресурсов с именем ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="fda0b-140">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="fda0b-141">Если вы используете другую группу ресурсов, укажите ее вместо ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="fda0b-141">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="fda0b-142">Выполните командлет **New-AzureRmDataFactory**, чтобы создать фабрику данных с именем **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-142">Run the **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="fda0b-143">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="fda0b-143">Note the following points:</span></span>

* <span data-ttu-id="fda0b-144">Имя фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="fda0b-144">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="fda0b-145">Если появится сообщение об ошибке **Имя FirstDataFactoryPSH фабрики данных недоступно**измените это имя (например, на ваше_имя_FirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="fda0b-145">If you receive the error **Data factory name “FirstDataFactoryPSH” is not available**, change the name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="fda0b-146">Используйте это имя вместо ADFTutorialFactoryPSH при выполнении шагов в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="fda0b-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="fda0b-147">Ознакомьтесь с разделом [Фабрика данных — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="fda0b-148">Чтобы создать экземпляры фабрики данных, вы должны быть администратором или участником подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="fda0b-148">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="fda0b-149">В будущем имя фабрики данных может быть зарегистрировано в качестве DNS-имени и, следовательно, стать отображаемым.</span><span class="sxs-lookup"><span data-stu-id="fda0b-149">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
* <span data-ttu-id="fda0b-150">Если появится сообщение об ошибке**Подписка не зарегистрирована для использования пространства имен Microsoft.DataFactory**, выполните одно из следующих действий и повторите попытку публикации.</span><span class="sxs-lookup"><span data-stu-id="fda0b-150">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="fda0b-151">Чтобы зарегистрировать поставщик фабрики данных Azure, выполните следующую команду в Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fda0b-151">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="fda0b-152">Чтобы убедиться, что поставщик фабрики данных зарегистрирован, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fda0b-152">You can run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="fda0b-153">Войдите на [портал Azure](https://portal.azure.com) с использованием подписки Azure и откройте колонку фабрики данных или создайте на портале фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-153">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="fda0b-154">Поставщик будет зарегистрирован автоматически.</span><span class="sxs-lookup"><span data-stu-id="fda0b-154">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="fda0b-155">Прежде чем создавать конвейер, необходимо создать несколько сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-155">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="fda0b-156">Сначала создайте связанные службы, чтобы связать хранилища данных и вычисления со своим хранилищем данных, и определите входные и выходные наборы данных, которые будут представлять входные и выходные данные в связанных хранилищах. Затем создайте конвейер с действием, в котором используются эти наборы данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-156">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="fda0b-157">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="fda0b-157">Create linked services</span></span>
<span data-ttu-id="fda0b-158">На этом шаге вы свяжете учетную запись службы хранилища Azure и используемый по запросу кластер Azure HDInsight с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="fda0b-159">В этом примере учетная запись хранения Azure содержит входные и выходные данные для конвейера.</span><span class="sxs-lookup"><span data-stu-id="fda0b-159">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="fda0b-160">Для выполнения скрипта Hive, указанного в действии конвейера, в этом примере используется связанная служба HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fda0b-160">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="fda0b-161">Определите, какие данные хранилища и службы вычислений используются в сценарии, и свяжите эти службы с фабрикой данных, создав связанные службы.</span><span class="sxs-lookup"><span data-stu-id="fda0b-161">Identify what data store/compute services are used in your scenario and link those services to the data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="fda0b-162">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="fda0b-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="fda0b-163">На этом шаге вы свяжете учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-163">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="fda0b-164">Используйте одну и ту же учетную запись хранения Azure для хранения входных и выходных данных и файла скрипта HQL.</span><span class="sxs-lookup"><span data-stu-id="fda0b-164">You use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="fda0b-165">Создайте в папке C:\ADFGetStarted JSON-файл с именем StorageLinkedService.json со следующим содержимым.</span><span class="sxs-lookup"><span data-stu-id="fda0b-165">Create a JSON file named StorageLinkedService.json in the C:\ADFGetStarted folder with the following content.</span></span> <span data-ttu-id="fda0b-166">Создайте папку ADFGetStarted, если она еще не существует.</span><span class="sxs-lookup"><span data-stu-id="fda0b-166">Create the folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="fda0b-167">Замените **account name** именем своей учетной записи хранения Azure, а **account key** — ключом доступа к ней.</span><span class="sxs-lookup"><span data-stu-id="fda0b-167">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="fda0b-168">Сведения о получении, просмотре, копировании и повторном создании ключей доступа к хранилищу см. в разделе [Управление учетной записью хранения](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="fda0b-168">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="fda0b-169">В Azure PowerShell перейдите в папку ADFGetStarted.</span><span class="sxs-lookup"><span data-stu-id="fda0b-169">In Azure PowerShell, switch to the ADFGetStarted folder.</span></span>
3. <span data-ttu-id="fda0b-170">Создать связанную службу можно с помощью командлета **New-AzureRmDataFactoryLinkedService** .</span><span class="sxs-lookup"><span data-stu-id="fda0b-170">You can use the **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="fda0b-171">В этом командлете и в других командлетах фабрики данных, которые используются в этом руководстве, требуется передача значений для параметров *ResourceGroupName* и *DataFactoryName*.</span><span class="sxs-lookup"><span data-stu-id="fda0b-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you to pass values for the *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="fda0b-172">Кроме того, можно использовать командлет **Get-AzureRmDataFactory**, чтобы получить объект **DataFactory** и передать этот объект без необходимости ввода параметров *ResourceGroupName* и *DataFactoryName* при каждом запуске командлета.</span><span class="sxs-lookup"><span data-stu-id="fda0b-172">Alternatively, you can use **Get-AzureRmDataFactory** to get a **DataFactory** object and pass the object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="fda0b-173">Выполните следующую команду, чтобы назначить выходные данные командлета **Get-AzureRmDataFactory** переменной **$df**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-173">Run the following command to assign the output of the **Get-AzureRmDataFactory** cmdlet to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="fda0b-174">Теперь выполните командлет **New-AzureRmDataFactoryLinkedService**, чтобы создать связанную службу **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-174">Now, run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="fda0b-175">Если вы не выполнили командлет **Get-AzureRmDataFactory** и не присвоили выходные данные переменной **$df**, вам нужно указать значения параметров *ResourceGroupName* и *DataFactoryName* следующим образом.</span><span class="sxs-lookup"><span data-stu-id="fda0b-175">If you hadn't run the **Get-AzureRmDataFactory** cmdlet and assigned the output to the **$df** variable, you would have to specify values for the *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="fda0b-176">Если вы закроете Azure PowerShell, не завершив выполнение описанных в руководстве инструкций, при следующем запуске Azure PowerShell вам нужно будет запустить командлет **Get-AzureRmDataFactory** , чтобы выполнить эти инструкции.</span><span class="sxs-lookup"><span data-stu-id="fda0b-176">If you close Azure PowerShell in the middle of the tutorial, you have to run the **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell to complete the tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="fda0b-177">Создание связанной службы Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="fda0b-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="fda0b-178">На этом шаге вы свяжете используемый по запросу кластер HDInsight с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-178">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="fda0b-179">Кластер HDInsight автоматически создается в среде выполнения и удаляется после завершения обработки и простоя в течение указанного времени.</span><span class="sxs-lookup"><span data-stu-id="fda0b-179">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="fda0b-180">Вместо используемого по запросу кластера HDInsight можно использовать собственный кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fda0b-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="fda0b-181">Дополнительные сведения см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="fda0b-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="fda0b-182">Создайте в папке **C:\ADFGetStarted** JSON-файл **HDInsightOnDemandLinkedService**.json со следующим содержимым.</span><span class="sxs-lookup"><span data-stu-id="fda0b-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in the **C:\ADFGetStarted** folder with the following content.</span></span>

    ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    <span data-ttu-id="fda0b-183">В следующей таблице приведены описания свойств JSON, используемых в этом фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="fda0b-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="fda0b-184">Свойство</span><span class="sxs-lookup"><span data-stu-id="fda0b-184">Property</span></span> | <span data-ttu-id="fda0b-185">Описание</span><span class="sxs-lookup"><span data-stu-id="fda0b-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="fda0b-186">ClusterSize (размер кластера)</span><span class="sxs-lookup"><span data-stu-id="fda0b-186">ClusterSize</span></span> |<span data-ttu-id="fda0b-187">Указывает размер кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fda0b-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="fda0b-188">TimeToLive (срок жизни)</span><span class="sxs-lookup"><span data-stu-id="fda0b-188">TimeToLive</span></span> |<span data-ttu-id="fda0b-189">Указывает, сколько времени может простаивать кластер HDInsight, прежде чем он будет удален.</span><span class="sxs-lookup"><span data-stu-id="fda0b-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="fda0b-190">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="fda0b-190">linkedServiceName</span></span> |<span data-ttu-id="fda0b-191">Указывает имя учетной записи хранения, в которой будут храниться журналы, создаваемые HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fda0b-191">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="fda0b-192">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="fda0b-192">Note the following points:</span></span>

   * <span data-ttu-id="fda0b-193">С помощью JSON-файла фабрика данных создает кластер HDInsight **под управлением Linux**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="fda0b-194">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="fda0b-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="fda0b-195">Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="fda0b-196">См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="fda0b-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="fda0b-197">Кластер HDInsight создает **контейнер по умолчанию** в хранилище BLOB-объектов, указанном в коде JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="fda0b-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="fda0b-198">При удалении кластера HDInsight этот контейнер не удаляется.</span><span class="sxs-lookup"><span data-stu-id="fda0b-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="fda0b-199">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="fda0b-199">This behavior is by design.</span></span> <span data-ttu-id="fda0b-200">Если используется связанная служба HDInsight по запросу, кластер HDInsight создается при каждой обработке среза данных (если не используется динамический кластер**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="fda0b-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="fda0b-201">После завершения обработки кластер автоматически удаляется.</span><span class="sxs-lookup"><span data-stu-id="fda0b-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="fda0b-202">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="fda0b-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="fda0b-203">Если эти контейнеры не используются для устранения неполадок с заданиями, удалите их — это позволит сократить расходы на хранение.</span><span class="sxs-lookup"><span data-stu-id="fda0b-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="fda0b-204">Имена контейнеров указаны в формате adf**имя_фабрики_данных**-**имя_связанной_службы**-метка_даты_и_времени.</span><span class="sxs-lookup"><span data-stu-id="fda0b-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="fda0b-205">Для удаления контейнеров в хранилище BLOB-объектов Azure используйте такие инструменты, как [Microsoft Storage Explorer](http://storageexplorer.com/) .</span><span class="sxs-lookup"><span data-stu-id="fda0b-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="fda0b-206">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="fda0b-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="fda0b-207">Выполните командлет **New-AzureRmDataFactoryLinkedService** , чтобы создать связанную службу с именем HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="fda0b-207">Run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="fda0b-208">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="fda0b-208">Create datasets</span></span>
<span data-ttu-id="fda0b-209">На этом шаге вы создадите наборы данных, которые представляют входные и выходные данные для обработки Hive.</span><span class="sxs-lookup"><span data-stu-id="fda0b-209">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="fda0b-210">Эти наборы данных ссылаются на службу **StorageLinkedService** , созданную ранее в ходе работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="fda0b-210">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="fda0b-211">Точки связанной службы указывают на учетную запись хранения Azure, а наборы данных указывают контейнер, папку и имя файла в хранилище, в котором содержатся входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="fda0b-211">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="fda0b-212">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="fda0b-212">Create input dataset</span></span>
1. <span data-ttu-id="fda0b-213">Создайте в папке **C:\ADFGetStarted** JSON-файл **InputTable.json** со следующим содержимым.</span><span class="sxs-lookup"><span data-stu-id="fda0b-213">Create a JSON file named **InputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    <span data-ttu-id="fda0b-214">Приведенный выше JSON-файл определяет набор данных с именем **AzureBlobInput**, представляющий входные данные для действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="fda0b-214">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="fda0b-215">Кроме того, файл указывает, что входные данные размещаются в контейнере больших двоичных объектов **adfgetstarted** и в папке **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-215">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    <span data-ttu-id="fda0b-216">В следующей таблице приведены описания свойств JSON, используемых в этом фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="fda0b-216">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="fda0b-217">Свойство</span><span class="sxs-lookup"><span data-stu-id="fda0b-217">Property</span></span> | <span data-ttu-id="fda0b-218">Описание</span><span class="sxs-lookup"><span data-stu-id="fda0b-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="fda0b-219">type</span><span class="sxs-lookup"><span data-stu-id="fda0b-219">type</span></span> |<span data-ttu-id="fda0b-220">Для свойства типа задано значение AzureBlob, так как данные хранятся в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="fda0b-220">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="fda0b-221">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="fda0b-221">linkedServiceName</span></span> |<span data-ttu-id="fda0b-222">Ссылается на созданную ранее службу StorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="fda0b-222">refers to the StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="fda0b-223">fileName</span><span class="sxs-lookup"><span data-stu-id="fda0b-223">fileName</span></span> |<span data-ttu-id="fda0b-224">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="fda0b-224">This property is optional.</span></span> <span data-ttu-id="fda0b-225">Если это свойство не указано, выбираются все файлы из папки folderPath.</span><span class="sxs-lookup"><span data-stu-id="fda0b-225">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="fda0b-226">В этом случае обрабатывается только файл input.log.</span><span class="sxs-lookup"><span data-stu-id="fda0b-226">In this case, only the input.log is processed.</span></span> |
   | <span data-ttu-id="fda0b-227">type</span><span class="sxs-lookup"><span data-stu-id="fda0b-227">type</span></span> |<span data-ttu-id="fda0b-228">Файлы журнала представлены в текстовом формате, поэтому мы используем значение TextFormat.</span><span class="sxs-lookup"><span data-stu-id="fda0b-228">The log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="fda0b-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="fda0b-229">columnDelimiter</span></span> |<span data-ttu-id="fda0b-230">Столбцы в файлах журнала разделяются запятыми (,).</span><span class="sxs-lookup"><span data-stu-id="fda0b-230">columns in the log files are delimited by the comma character (,).</span></span> |
   | <span data-ttu-id="fda0b-231">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="fda0b-231">frequency/interval</span></span> |<span data-ttu-id="fda0b-232">Для свойства frequency задано значение Month, а для свойства interval — значение 1. Это означает, что срезы входных данных доступны ежемесячно.</span><span class="sxs-lookup"><span data-stu-id="fda0b-232">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="fda0b-233">external</span><span class="sxs-lookup"><span data-stu-id="fda0b-233">external</span></span> |<span data-ttu-id="fda0b-234">Это свойство имеет значение true, если входные данные не создаются службой фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-234">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |
2. <span data-ttu-id="fda0b-235">Чтобы создать набор данных фабрики данных, выполните следующую команду в Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fda0b-235">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="fda0b-236">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="fda0b-236">Create output dataset</span></span>
<span data-ttu-id="fda0b-237">Теперь создайте выходной набор данных, представляющий выходные данные, которые хранятся в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="fda0b-237">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="fda0b-238">Создайте в папке **C:\ADFGetStarted** JSON-файл **OutputTable.json** со следующим содержимым.</span><span class="sxs-lookup"><span data-stu-id="fda0b-238">Create a JSON file named **OutputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    <span data-ttu-id="fda0b-239">JSON-файл определяет набор данных с именем **AzureBlobOutput**, представляющий выходные данные для действия в конвейере.</span><span class="sxs-lookup"><span data-stu-id="fda0b-239">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="fda0b-240">Кроме того, файл указывает, что результаты хранятся в контейнере больших двоичных объектов **adfgetstarted** и в папке **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-240">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="fda0b-241">В разделе **availability** указывается частота, с которой будет создаваться выходной набор данных (ежемесячно).</span><span class="sxs-lookup"><span data-stu-id="fda0b-241">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="fda0b-242">Чтобы создать набор данных фабрики данных, выполните следующую команду в Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fda0b-242">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="fda0b-243">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="fda0b-243">Create pipeline</span></span>
<span data-ttu-id="fda0b-244">На этом шаге вы создадите свой первый конвейер с действием **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="fda0b-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="fda0b-245">Срез входных данных создается ежемесячно (frequency: Month, interval: 1), срез выходных данных создается ежемесячно, свойство scheduler для действия также указывается ежемесячно.</span><span class="sxs-lookup"><span data-stu-id="fda0b-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="fda0b-246">Параметры выходного набора данных (outputs) и планировщика действия (scheduler) должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="fda0b-246">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="fda0b-247">В настоящее время расписание активируется с помощью выходного набора данных, поэтому его необходимо создать, даже если действие не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-247">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="fda0b-248">Если действие не принимает никаких входных данных, входной набор данных можно не создавать.</span><span class="sxs-lookup"><span data-stu-id="fda0b-248">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="fda0b-249">Свойства, используемые в следующем фрагменте JSON, описаны в конце этого раздела.</span><span class="sxs-lookup"><span data-stu-id="fda0b-249">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="fda0b-250">Создайте в папке C:\ADFGetStarted JSON-файл MyFirstPipelinePSH.json со следующим содержимым.</span><span class="sxs-lookup"><span data-stu-id="fda0b-250">Create a JSON file named MyFirstPipelinePSH.json in the C:\ADFGetStarted folder with the following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="fda0b-251">В JSON-файле замените свойство **storageaccountname** именем своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fda0b-251">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    <span data-ttu-id="fda0b-252">Этот фрагмент создает конвейер из одного действия, использующего Hive для обработки данных в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fda0b-252">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="fda0b-253">Файл **partitionweblogs.hql** скрипта Hive хранится в учетной записи хранения Azure (указывается с помощью свойства scriptLinkedService с именем **StorageLinkedService**) в папке **script** в контейнере **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-253">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="fda0b-254">Раздел **defines** используется для настройки параметров среды выполнения, которые будут переданы в скрипт Hive в качестве значений конфигурации Hive (например, ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="fda0b-254">The **defines** section is used to specify the runtime settings that be passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="fda0b-255">Активный период конвейера задается с помощью свойств **start** и **end**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-255">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="fda0b-256">В действии JSON укажите, что скрипт Hive будет выполняться в среде вычислений, указанной в свойстве **linkedServiceName**, — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-256">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fda0b-257">Сведения о свойствах JSON, используемых в этом примере, см. в разделе "Конвейер JSON" статьи [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="fda0b-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in the example.</span></span>

2. <span data-ttu-id="fda0b-258">Убедитесь, что файл **input.log** отображается в папке **adfgetstarted/inputdata** в хранилище BLOB-объектов Azure, и выполните следующую команду, чтобы развернуть конвейер.</span><span class="sxs-lookup"><span data-stu-id="fda0b-258">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="fda0b-259">Так как время в свойствах **start** и **end** задано в прошлом, а для свойства **isPaused** задано значение false, конвейер (действие в конвейере) запускается сразу после развертывания.</span><span class="sxs-lookup"><span data-stu-id="fda0b-259">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="fda0b-260">Поздравляем! Вы создали свой первый конвейер с помощью Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="fda0b-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="fda0b-261">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="fda0b-261">Monitor pipeline</span></span>
<span data-ttu-id="fda0b-262">На этом шаге Azure PowerShell будет использоваться для мониторинга процессов в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fda0b-262">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="fda0b-263">Выполните командлет **Get-AzureRmDataFactory** и назначьте выходные данные переменной **$df**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-263">Run **Get-AzureRmDataFactory** and assign the output to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="fda0b-264">Выполните командлет **Get-AzureRmDataFactorySlice** для получения сведений обо всех срезах в таблице **EmpSQLTable**, которая является выходной таблицей конвейера.</span><span class="sxs-lookup"><span data-stu-id="fda0b-264">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **EmpSQLTable**, which is the output table of the pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="fda0b-265">Обратите внимание, здесь указывается то же значение StartDateTime, что и в JSON конвейера.</span><span class="sxs-lookup"><span data-stu-id="fda0b-265">Notice that the StartDateTime you specify here is the same start time specified in the pipeline JSON.</span></span> <span data-ttu-id="fda0b-266">Пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="fda0b-266">Here is the sample output:</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="fda0b-267">Выполните командлет **Get-AzureRmDataFactoryRun** , чтобы получить сведения о действиях, выполняемых для конкретного среза.</span><span class="sxs-lookup"><span data-stu-id="fda0b-267">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="fda0b-268">Пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="fda0b-268">Here is the sample output:</span></span> 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="fda0b-269">Вы можете выполнять этот командлет до тех пор, пока не увидите срез с состоянием **Готово** или **Сбой**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-269">You can keep running this cmdlet until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="fda0b-270">Когда срез перейдет в состояние "Готово", проверьте выходные данные в папке **partitioneddata** контейнера **adfgetstarted** в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="fda0b-270">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="fda0b-271">Создание кластера HDInsight по требованию занимает некоторое время.</span><span class="sxs-lookup"><span data-stu-id="fda0b-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![выходные данные](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="fda0b-273">Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут).</span><span class="sxs-lookup"><span data-stu-id="fda0b-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="fda0b-274">Таким образом, конвейер обработает срез **примерно через 30 минут** .</span><span class="sxs-lookup"><span data-stu-id="fda0b-274">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
>
> <span data-ttu-id="fda0b-275">В случае успешной обработки среза входной файл удаляется.</span><span class="sxs-lookup"><span data-stu-id="fda0b-275">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="fda0b-276">Если вы хотите повторно обработать срез или еще раз выполнить инструкции из руководства, передайте входной файл (input.log) в папку inputdata в контейнере adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="fda0b-276">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="fda0b-277">Сводка</span><span class="sxs-lookup"><span data-stu-id="fda0b-277">Summary</span></span>
<span data-ttu-id="fda0b-278">Следуя инструкциям из этого руководства, вы создали фабрику данных Azure для обработки данных путем выполнения сценария Hive в кластере Hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fda0b-278">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="fda0b-279">Вы использовали редактор фабрики данных на портале Azure для выполнения следующих действий:</span><span class="sxs-lookup"><span data-stu-id="fda0b-279">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="fda0b-280">создание **фабрики данных Azure**;</span><span class="sxs-lookup"><span data-stu-id="fda0b-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="fda0b-281">создание двух **связанных служб**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="fda0b-282">**Служба хранилища Azure** — связанная служба для связывания хранилища BLOB-объектов Azure, которое содержит входные и выходные файлы, с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-282">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="fda0b-283">**Azure HDInsight** — связанная служба по запросу для связывания кластера HDInsight Hadoop с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-283">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="fda0b-284">Фабрика данных Azure своевременно создает кластер HDInsight Hadoop для обработки входных данных и генерирования выходных данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="fda0b-285">Создание двух **наборов данных**, которые описывают входные и выходные данные для действия HDInsight Hive в конвейере.</span><span class="sxs-lookup"><span data-stu-id="fda0b-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="fda0b-286">Создание **конвейера** с действием **HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="fda0b-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fda0b-287">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fda0b-287">Next steps</span></span>
<span data-ttu-id="fda0b-288">В этой статье описывается создание конвейера с помощью действия преобразования (действие HDInsight), которое по требованию выполняет сценарий Hive в кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fda0b-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="fda0b-289">Сведения о том, как копировать данные из хранилища BLOB-объектов Azure в SQL Azure с помощью действия копирования, см. в статье [Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="fda0b-289">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fda0b-290">См. также</span><span class="sxs-lookup"><span data-stu-id="fda0b-290">See Also</span></span>
| <span data-ttu-id="fda0b-291">Раздел</span><span class="sxs-lookup"><span data-stu-id="fda0b-291">Topic</span></span> | <span data-ttu-id="fda0b-292">Описание</span><span class="sxs-lookup"><span data-stu-id="fda0b-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="fda0b-293">Справочник по командлетам фабрики данных</span><span class="sxs-lookup"><span data-stu-id="fda0b-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="fda0b-294">См. полную документацию по командлетам фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="fda0b-295">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="fda0b-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="fda0b-296">Эта статья поможет вам понять сущность конвейеров и действий в фабрике данных Azure, а также научиться с их помощью создавать комплексные рабочие процессы, управляемые данными, для конкретных бизнес-сценариев.</span><span class="sxs-lookup"><span data-stu-id="fda0b-296">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="fda0b-297">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="fda0b-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="fda0b-298">Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fda0b-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="fda0b-299">Планирование и выполнение</span><span class="sxs-lookup"><span data-stu-id="fda0b-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="fda0b-300">Здесь объясняются аспекты планирования и исполнения в модели приложений фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fda0b-300">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="fda0b-301">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="fda0b-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="fda0b-302">В этой статье описывается мониторинг и отладка конвейеров, а также управление ими с помощью приложения мониторинга и управления.</span><span class="sxs-lookup"><span data-stu-id="fda0b-302">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
