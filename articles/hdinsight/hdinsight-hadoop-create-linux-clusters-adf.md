---
title: "Создание кластеров Hadoop по запросу с помощью фабрики данных — Azure HDInsight | Документы Майкрософт"
description: "Узнайте, как создавать кластеры Hadoop в HDInsight по запросу с помощью фабрики данных Azure."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: e68f1d72965d9516e0552c84d03d234c21739390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="e6a1b-103">Создание кластеров Hadoop в HDInsight по запросу с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="e6a1b-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="e6a1b-104">[Фабрика данных Azure](../data-factory/data-factory-introduction.md) представляет собой облачную службу интеграции информации, которая организует и автоматизирует перемещение и преобразование данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="e6a1b-105">С ее помощью вы можете создать кластер Hadoop в HDInsight, когда это требуется для обработки входящих срезов данных. После завершения обработки кластер можно удалить.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span></span> <span data-ttu-id="e6a1b-106">Ниже приведены некоторые преимущества использования кластера Hadoop HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="e6a1b-107">Вы платите только за время выполнения задания в кластере Hadoop HDInsight (и непродолжительное настраиваемое время простоя).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="e6a1b-108">Счета за кластеры HDInsight выставляются пропорционально за минуту независимо от их использования.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="e6a1b-109">При использовании связанной службы HDInsight по требованию в фабрике данных можно создать кластеры по требованию.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span></span> <span data-ttu-id="e6a1b-110">Кластеры автоматически удаляются по завершении задания.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-110">And the clusters are deleted automatically when the jobs are completed.</span></span> <span data-ttu-id="e6a1b-111">Таким образом, вы платите только за время выполнения задания и непродолжительное время простоя (параметр срока жизни).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="e6a1b-112">С помощью конвейера фабрики данных можно создать рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="e6a1b-113">Например, у вас может быть конвейер для копирования данных из локального сервера SQL Server в хранилище BLOB-объектов Azure, обработки данных с помощью скриптов Hive и Pig в кластере Hadoop HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="e6a1b-114">Скопируйте данные о результатах в хранилище данных SQL Azure для приложений бизнес-аналитики, необходимых для использования.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span></span>
- <span data-ttu-id="e6a1b-115">Вы можете запланировать периодическое выполнение рабочего процесса (каждый час, день, неделю, месяц и т. д.).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="e6a1b-116">В фабрике данных Azure фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="e6a1b-117">Конвейер данных включает одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="e6a1b-118">Существует два типа действий: [действия перемещения данных](../data-factory/data-factory-data-movement-activities.md) и [действия преобразования данных](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="e6a1b-119">Для перемещения данных из исходного хранилища данных в целевое используются действия перемещения данных (сейчас только действие копирования).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span></span> <span data-ttu-id="e6a1b-120">Для перемещения и обработки данных используются действия преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-120">You use data transformation activities to transform/process data.</span></span> <span data-ttu-id="e6a1b-121">Действие Hive HDInsight — одно из действий преобразования, которое поддерживает фабрика данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span></span> <span data-ttu-id="e6a1b-122">В этом руководстве используется действие преобразования Hive.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-122">You use the Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="e6a1b-123">Вы можете настроить действие Hive, чтобы использовать собственный кластер Hadoop HDInsight или кластер Hadoop HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="e6a1b-124">В этом руководстве описывается настройка действия Hive в конвейере фабрики данных для использования кластера HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span></span> <span data-ttu-id="e6a1b-125">При выполнении действия для обработки среза данных происходит следующее.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-125">Therefore, when the activity runs to process a data slice, here is what happens:</span></span>

1. <span data-ttu-id="e6a1b-126">Кластер Hadoop HDInsight автоматически создается для своевременной обработки среза.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span></span>  
2. <span data-ttu-id="e6a1b-127">Для обработки входных данных выполняется скрипт HiveQL в кластере.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-127">The input data is processed by running a HiveQL script on the cluster.</span></span>
3. <span data-ttu-id="e6a1b-128">По завершении обработки кластер Hadoop HDInsight удаляется и не используется в течение заданного времени (параметр timeToLive).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="e6a1b-129">Если во время простоя (параметр timeToLive) можно обработать следующий срез данных, для этого используется тот же кластер.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span></span>  

<span data-ttu-id="e6a1b-130">В этом руководстве описываются действия скрипта HiveQL, связанного с действием Hive.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span></span>

1. <span data-ttu-id="e6a1b-131">Создается внешняя таблица, которая ссылается на необработанные данные веб-журнала в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="e6a1b-132">Разделяются необработанные данные по году и месяцу.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-132">Partitions the raw data by year and month.</span></span>
3. <span data-ttu-id="e6a1b-133">Секционированные данные сохраняются в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-133">Stores the partitioned data in the Azure blob storage.</span></span>

<span data-ttu-id="e6a1b-134">В этом руководстве скрипт HiveQL, связанный с действием Hive, создает внешнюю таблицу, которая ссылается на необработанные данные веб-журнала в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span></span> <span data-ttu-id="e6a1b-135">Вот пример строк за каждый месяц во входном файле.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-135">Here are the sample rows for each month in the input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="e6a1b-136">Скрипт HiveQL разделяет необработанные данные по году и месяцу.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-136">The HiveQL script partitions the raw data by year and month.</span></span> <span data-ttu-id="e6a1b-137">Он создает три выходные папки на основе предыдущих входных данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-137">It creates three output folders based on the previous input.</span></span> <span data-ttu-id="e6a1b-138">Каждая папка содержит файл с записями по каждому месяцу.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="e6a1b-139">Сведения о преобразовании данных в фабрике данных см. в статье [Преобразование данных в фабрике данных Azure](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e6a1b-140">Сейчас в фабрике данных Azure можно создать только кластер HDInsight версии 3.2.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6a1b-141">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e6a1b-141">Prerequisites</span></span>
<span data-ttu-id="e6a1b-142">Прежде чем следовать указаниям в этой статье, необходимо подготовить следующее:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-142">Before you begin the instructions in this article, you must have the following items:</span></span>

* <span data-ttu-id="e6a1b-143">[Подписка Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e6a1b-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="e6a1b-145">Подготовка учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="e6a1b-145">Prepare storage account</span></span>
<span data-ttu-id="e6a1b-146">В этом сценарии можно использовать до трех учетных записей хранения:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-146">You can use up to three storage accounts in this scenario:</span></span>

- <span data-ttu-id="e6a1b-147">учетную запись хранения по умолчанию для кластера HDInsight;</span><span class="sxs-lookup"><span data-stu-id="e6a1b-147">default storage account for the HDInsight cluster</span></span>
- <span data-ttu-id="e6a1b-148">учетную запись хранения для входных данных;</span><span class="sxs-lookup"><span data-stu-id="e6a1b-148">storage account for the input data</span></span>
- <span data-ttu-id="e6a1b-149">учетную запись хранения для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-149">storage account for the output data</span></span>

<span data-ttu-id="e6a1b-150">Чтобы упростить работу с руководством, для всех трех задач мы будем использовать одну учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span></span> <span data-ttu-id="e6a1b-151">Ниже описаны действия для примера скрипта Azure PowerShell, приведенного в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-151">The Azure PowerShell sample script found in this section performs the following tasks:</span></span>

1. <span data-ttu-id="e6a1b-152">Войдите в Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-152">Log in to Azure.</span></span>
2. <span data-ttu-id="e6a1b-153">Создание группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="e6a1b-154">Создание учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="e6a1b-155">Создание контейнера больших двоичных объектов в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-155">Create a Blob container in the storage account</span></span>
5. <span data-ttu-id="e6a1b-156">Скопируйте следующие два файла в контейнер BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-156">Copy the following two files to the Blob container:</span></span>

   * <span data-ttu-id="e6a1b-157">Файл входных данных: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="e6a1b-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="e6a1b-158">Сценарий HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="e6a1b-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="e6a1b-159">Оба файла хранятся в общедоступном контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="e6a1b-160">**Подготовка хранилища и копирование файлов с помощью Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="e6a1b-160">**To prepare the storage and copy the files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e6a1b-161">Укажите имена для группы ресурсов Azure и учетную запись хранения Azure, которая будет создана с помощью скрипта.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span></span>
> <span data-ttu-id="e6a1b-162">Запишите **имя группы ресурсов**, **имя учетной записи хранения** и **ключ учетной записи хранения**, выводимые скриптом.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span></span> <span data-ttu-id="e6a1b-163">Они потребуются в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-163">You need them in the next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use the following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="e6a1b-164">Если вам необходима помощь в работе со скриптом PowerShell, необходимые сведения см. в статье [Использование Azure PowerShell со службой хранилища Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="e6a1b-165">Если же вы хотите использовать Azure CLI, дополнительные сведения для скрипта Azure CLI см. в разделе [Приложение](#appendix).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span></span>

<span data-ttu-id="e6a1b-166">**Проверка учетной записи хранения и содержимого**</span><span class="sxs-lookup"><span data-stu-id="e6a1b-166">**To examine the storage account and the contents**</span></span>

1. <span data-ttu-id="e6a1b-167">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-167">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e6a1b-168">Щелкните **Группы ресурсов** на левой панели.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-168">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="e6a1b-169">Дважды щелкните имя группы ресурсов, созданной в скрипте PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-169">Double-click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="e6a1b-170">Если отображается слишком много групп ресурсов, используйте фильтр.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-170">Use the filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="e6a1b-171">На плитке **Ресурсы** должен отображаться один ресурс, если только группа ресурсов не является общей для других проектов.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span></span> <span data-ttu-id="e6a1b-172">Этим ресурсом будет учетная запись хранения с именем, которое вы указали ранее.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-172">That resource is the storage account with the name you specified earlier.</span></span> <span data-ttu-id="e6a1b-173">Щелкните имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-173">Click the storage account name.</span></span>
5. <span data-ttu-id="e6a1b-174">Щелкните элемент **BLOB-объекты** .</span><span class="sxs-lookup"><span data-stu-id="e6a1b-174">Click the **Blobs** tiles.</span></span>
6. <span data-ttu-id="e6a1b-175">Щелкните контейнер **adfgetstarted** .</span><span class="sxs-lookup"><span data-stu-id="e6a1b-175">Click the **adfgetstarted** container.</span></span> <span data-ttu-id="e6a1b-176">Вы увидите две папки: **inputdata** и **script**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="e6a1b-177">Откройте папку и проверьте файлы в папках.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-177">Open the folder and check the files in the folders.</span></span> <span data-ttu-id="e6a1b-178">Папка inputdata содержит файл input.log с входными данными, а папка script — файл скрипта HiveQL.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="e6a1b-179">Создание фабрики данных с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e6a1b-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="e6a1b-180">При наличии учетной записи хранения, входных данных и подготовленного сценария HiveQL вы можете создать фабрику данных Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span></span> <span data-ttu-id="e6a1b-181">Существует несколько способов создания фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="e6a1b-182">Работая с этим руководством, вы создадите фабрику данных, развернув шаблон Resource Manager Azure на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span></span> <span data-ttu-id="e6a1b-183">Вы также можете развернуть шаблон Resource Manager с помощью [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) или [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="e6a1b-184">Описание других способов создания фабрики данных вы найдете в [руководстве по созданию фабрики данных](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="e6a1b-185">Щелкните следующее изображение, чтобы войти в Azure и открыть шаблон Resource Manager на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="e6a1b-186">Шаблон находится по адресу https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="e6a1b-187">Дополнительные сведения о сущностях, определенных в шаблоне, см. в этом [разделе](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="e6a1b-188">Для параметра **Группа ресурсов** выберите вариант **Использовать существующий**, а затем выберите имя группы ресурсов, созданной на предыдущем шаге (с использованием скрипта PowerShell).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="e6a1b-189">Введите имя для фабрики данных (в поле **Имя фабрики данных**).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-189">Enter a name for the data factory (**Data Factory Name**).</span></span> <span data-ttu-id="e6a1b-190">Оно должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="e6a1b-191">Введите записанные на предыдущем шаге **имя учетной записи хранения** и **ключ учетной записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span></span>
5. <span data-ttu-id="e6a1b-192">Ознакомившись с **условиями использования**, установите флажок **I agree to the terms and conditions** (Я принимаю указанные выше условия).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="e6a1b-193">Кроме того, выберите **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-193">Select **Pin to dashboard** option.</span></span>
6. <span data-ttu-id="e6a1b-194">Щелкните **Purchase/Create** (Купить или Создать).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="e6a1b-195">На панели мониторинга появится плитка **Развертывание шаблона развертывания**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="e6a1b-196">Подождите, пока для группы ресурсов откроется колонка **Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-196">Wait until the **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="e6a1b-197">Чтобы открыть колонку группы ресурсов, можно также щелкнуть элемент с таким же названием, как имя вашей группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-197">You can also click the tile titled as your resource group name to open the resource group blade.</span></span>
6. <span data-ttu-id="e6a1b-198">Щелкните элемент, чтобы открыть группу ресурсов, если колонка группы ресурсов еще не открылась.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-198">Click the tile to open the resource group if the resource group blade is not already open.</span></span> <span data-ttu-id="e6a1b-199">Теперь наряду с ресурсом учетной записи хранения должен отображаться еще один ресурс фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span></span>
7. <span data-ttu-id="e6a1b-200">Щелкните имя фабрики данных (значение, указанное для параметра **Имя фабрики данных**).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="e6a1b-201">В колонке фабрики данных щелкните элемент **Схема**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-201">In the Data Factory blade, click the **Diagram** tile.</span></span> <span data-ttu-id="e6a1b-202">На схеме отображается одно действие с входным набором данных и выходным набором данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-202">The diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Фабрика данных Azure: схема конвейера действий Hive в кластере HDInsight по запросу](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="e6a1b-204">Эти имена определяются в шаблоне Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-204">The names are defined in the Resource Manager template.</span></span>
9. <span data-ttu-id="e6a1b-205">Дважды щелкните **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="e6a1b-206">В разделе **Последние обновленные срезы**вы увидите один срез.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-206">On the **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="e6a1b-207">Если отображается состояние **Выполняется**, подождите, пока оно не изменится на **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-207">If the status is **In progress**, wait until it is changed to **Ready**.</span></span> <span data-ttu-id="e6a1b-208">Создание кластера HDInsight обычно занимает около **20 минут**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span></span>

### <a name="check-the-data-factory-output"></a><span data-ttu-id="e6a1b-209">Проверка выходных данных фабрики данных</span><span class="sxs-lookup"><span data-stu-id="e6a1b-209">Check the data factory output</span></span>

1. <span data-ttu-id="e6a1b-210">Для проверки содержимого контейнера adfgetstarted используйте процедуру из предыдущего сеанса.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span></span> <span data-ttu-id="e6a1b-211">Кроме контейнера **adfgetsarted**, существует два новых контейнера.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-211">There are two new containers in addition to **adfgetsarted**:</span></span>

   * <span data-ttu-id="e6a1b-212">Контейнер с именем, соответствующим шаблону: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="e6a1b-213">Этот контейнер для кластера HDInsight используется в качестве контейнера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-213">This container is the default container for the HDInsight cluster.</span></span>
   * <span data-ttu-id="e6a1b-214">Контейнер для журналов заданий ADF — adfjobs.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-214">adfjobs: This container is the container for the ADF job logs.</span></span>

     <span data-ttu-id="e6a1b-215">Выходные данные фабрики данных хранятся в контейнере **afgetstarted** в соответствии с настройками в шаблоне Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span></span>
2. <span data-ttu-id="e6a1b-216">Щелкните **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="e6a1b-217">Дважды щелкните **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="e6a1b-218">Вы увидите папку **year=2014**, так как все веб-журналы датированы 2014 годом.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span></span>

    ![Фабрика данных Azure: выходные данные конвейера действия Hive в кластере HDInsight по запросу](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="e6a1b-220">Если перейти вниз по списку, вы увидите 3 папки за январь, февраль и март.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-220">If you drill down the list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="e6a1b-221">Для каждого месяца существует журнал.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-221">And there is a log for each month.</span></span>

    ![Фабрика данных Azure: выходные данные конвейера действия Hive в кластере HDInsight по запросу](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="e6a1b-223">Сущности фабрики данных в шаблоне</span><span class="sxs-lookup"><span data-stu-id="e6a1b-223">Data Factory entities in the template</span></span>
<span data-ttu-id="e6a1b-224">Шаблон Resource Manager верхнего уровня для фабрики данных выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-224">Here is how the top-level Resource Manager template for a data factory looks like:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a><span data-ttu-id="e6a1b-225">Определение фабрики данных</span><span class="sxs-lookup"><span data-stu-id="e6a1b-225">Define data factory</span></span>
<span data-ttu-id="e6a1b-226">Фабрику данных следует определить в шаблоне Resource Manager, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-226">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="e6a1b-227">dataFactoryName — это имя фабрики данных, указанное при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span></span> <span data-ttu-id="e6a1b-228">Сейчас фабрика данных поддерживается только в восточной и западной частях США, а также в Северной Европе.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-the-data-factory"></a><span data-ttu-id="e6a1b-229">Определение сущностей в фабрике данных</span><span class="sxs-lookup"><span data-stu-id="e6a1b-229">Defining entities within the data factory</span></span>
<span data-ttu-id="e6a1b-230">В шаблоне JSON определены следующие сущности фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-230">The following Data Factory entities are defined in the JSON template:</span></span>

* [<span data-ttu-id="e6a1b-231">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="e6a1b-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="e6a1b-232">Связанная служба кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="e6a1b-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="e6a1b-233">Входной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="e6a1b-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="e6a1b-234">Выходной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="e6a1b-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="e6a1b-235">Конвейер данных с действием копирования</span><span class="sxs-lookup"><span data-stu-id="e6a1b-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="e6a1b-236">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="e6a1b-236">Azure Storage linked service</span></span>
<span data-ttu-id="e6a1b-237">Связанная служба хранилища Azure связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-237">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="e6a1b-238">В этом руководстве одна и та же учетная запись хранения используется в качестве учетной записи хранения HDInsight, хранилища входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="e6a1b-239">Таким образом, вы определяете только одну связанную службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="e6a1b-240">В определении связанной службы необходимо указать имя и ключ учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-240">In the linked service definition, you specify the name and key of your Azure storage account.</span></span> <span data-ttu-id="e6a1b-241">Дополнительные сведения о свойствах JSON для определения связанной службы хранилища Azure см. в разделе [Связанная служба хранилища Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="e6a1b-242">Для **connectionString** используются параметры storageAccountName и storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="e6a1b-243">Вам необходимо указать значения для этих параметров при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-243">You specify values for these parameters while deploying the template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="e6a1b-244">Связанная служба кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="e6a1b-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="e6a1b-245">В определении связанной службы HDInsight по требованию необходимо указать значения для параметров конфигурации, которые служба фабрики данных использует для создания кластера Hadoop HDInsight во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="e6a1b-246">Дополнительные сведения о свойствах JSON, используемых для определения связанной службы кластера HDInsight по запросу, см. в статье [Связанные службы вычислений](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="e6a1b-247">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-247">Note the following points:</span></span>

* <span data-ttu-id="e6a1b-248">Фабрика данных создает кластер HDInsight **под управлением Linux**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="e6a1b-249">Кластер Hadoop HDInsight создается в том же регионе, что и учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span></span>
* <span data-ttu-id="e6a1b-250">Обратите внимание на параметр *timeToLive* .</span><span class="sxs-lookup"><span data-stu-id="e6a1b-250">Notice the *timeToLive* setting.</span></span> <span data-ttu-id="e6a1b-251">Фабрика данных автоматически удалит кластер по истечении 30 минут времени простоя.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="e6a1b-252">Кластер HDInsight создает **контейнер по умолчанию** в хранилище BLOB-объектов, указанном в коде JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="e6a1b-253">При удалении кластера HDInsight этот контейнер не удаляется.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-253">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="e6a1b-254">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-254">This behavior is by design.</span></span> <span data-ttu-id="e6a1b-255">Если используется связанная служба HDInsight по запросу, кластер HDInsight создается всякий раз, когда нужно обработать срез данных (если не используется динамический кластер**timeToLive**), после чего кластер удаляется.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

<span data-ttu-id="e6a1b-256">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6a1b-257">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="e6a1b-258">Если эти контейнеры не используются для устранения неполадок с заданиями, удалите их — это позволит сократить расходы на хранение.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="e6a1b-259">Имена контейнеров указаны в формате adf**имя_фабрики_данных**-**имя_связанной_службы**-метка_даты_и_времени.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="e6a1b-260">Для удаления контейнеров в хранилище BLOB-объектов Azure используйте такие инструменты, как [Microsoft Storage Explorer](http://storageexplorer.com/) .</span><span class="sxs-lookup"><span data-stu-id="e6a1b-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="e6a1b-261">Входной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="e6a1b-261">Azure blob input dataset</span></span>
<span data-ttu-id="e6a1b-262">В определении входного набора данных укажите имена контейнера больших двоичных объектов, папки и файла, содержащего входные данные.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="e6a1b-263">Подробные сведения о свойствах JSON, которые используюся для определения набора данных большого двоичного объекта Azure, см. в разделе [Свойства типа "Набор данных большого двоичного объекта Azure"](../data-factory/data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
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

<span data-ttu-id="e6a1b-264">Обратите внимание на следующие характерные параметры в определении JSON:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-264">Notice the following specific settings in the JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="e6a1b-265">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="e6a1b-265">Azure Blob output dataset</span></span>
<span data-ttu-id="e6a1b-266">В определении выходного набора данных укажите имена контейнера больших двоичных объектов и папки, содержащей выходные данные.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="e6a1b-267">Подробные сведения о свойствах JSON, которые используюся для определения набора данных большого двоичного объекта Azure, см. в разделе [Свойства типа "Набор данных большого двоичного объекта Azure"](../data-factory/data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="e6a1b-268">FolderPath задает путь к папке, содержащей выходные данные.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-268">The folderPath specifies the path to the folder that holds the output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="e6a1b-269">Параметр [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="e6a1b-270">В фабрике данных Azure доступность выходного набора данных активирует конвейер.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-270">In Azure Data Factory, output dataset availability drives the pipeline.</span></span> <span data-ttu-id="e6a1b-271">В этом примере срез создается ежемесячно в последний день месяца (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span></span> <span data-ttu-id="e6a1b-272">Дополнительные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="e6a1b-273">Конвейер данных</span><span class="sxs-lookup"><span data-stu-id="e6a1b-273">Data pipeline</span></span>
<span data-ttu-id="e6a1b-274">Здесь вы определите конвейер для преобразования данных. Для этого нужно запустить скрипт Hive в кластере HDInsight Azure по требованию.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="e6a1b-275">В разделе [Конвейер JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) описаны элементы JSON, используемые для определения конвейера в этом примере.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span>

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
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
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="e6a1b-276">Конвейер содержит одно действие (действие HDInsightHive).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-276">The pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="e6a1b-277">Так как даты начала и окончания находятся в пределах января 2016 г., обрабатываются данные только за один месяц (срез).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="e6a1b-278">И в *начале*, и в *конце* действия указана прошедшая дата, поэтому фабрика данных обрабатывает данные сразу за месяц.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span></span> <span data-ttu-id="e6a1b-279">Если окончание приходится на дату в будущем, фабрика данных создаст другой срез, когда наступит заданное время.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-279">If the end is a future date, the data factory creates another slice when the time comes.</span></span> <span data-ttu-id="e6a1b-280">Дополнительные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-the-tutorial"></a><span data-ttu-id="e6a1b-281">Очистка учебника</span><span class="sxs-lookup"><span data-stu-id="e6a1b-281">Clean up the tutorial</span></span>

### <a name="delete-the-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="e6a1b-282">Удаление контейнеров больших двоичных объектов, созданных кластером HDInsight по требованию</span><span class="sxs-lookup"><span data-stu-id="e6a1b-282">Delete the blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="e6a1b-283">В случае связанной службы HDInsight по запросу кластер HDInsight создается для обработки каждого среза данных (если не используется динамический кластер (timeToLive)) и удаляется по завершении обработки.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span></span> <span data-ttu-id="e6a1b-284">Для каждого кластера фабрика данных Azure создает контейнер больших двоичных объектов в хранилище BLOB-объектов Azure, которое используется в качестве учетной записи хранения по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span></span> <span data-ttu-id="e6a1b-285">При удалении кластера HDInsight контейнер хранилища BLOB-объектов по умолчанию и соответствующая учетная запись не удаляются.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span></span> <span data-ttu-id="e6a1b-286">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-286">This behavior is by design.</span></span> <span data-ttu-id="e6a1b-287">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="e6a1b-288">Если эти контейнеры не используются для устранения неполадок с заданиями, удалите их — это позволит сократить расходы на хранение.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="e6a1b-289">Имена этих контейнеров указаны по шаблону `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="e6a1b-290">Удалите папки **adfjobs** и **adfyourdatafactoryname-linkedservicename-datetimestamp**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="e6a1b-291">Контейнер adfjobs содержит журналы заданий из фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-291">The adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-the-resource-group"></a><span data-ttu-id="e6a1b-292">удаление группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-292">Delete the resource group</span></span>
<span data-ttu-id="e6a1b-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) используется для развертывания, контроля и мониторинга решения в виде группы.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="e6a1b-294">Удаление группы ресурсов приведет к удалению всех компонентов внутри группы.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-294">Deleting a resource group deletes all the components inside the group.</span></span>  

1. <span data-ttu-id="e6a1b-295">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-295">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e6a1b-296">Щелкните **Группы ресурсов** на левой панели.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-296">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="e6a1b-297">Щелкните имя группы ресурсов, созданной в сценарии PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-297">Click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="e6a1b-298">Если отображается слишком много групп ресурсов, используйте фильтр.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-298">Use the filter if you have too many resource groups listed.</span></span> <span data-ttu-id="e6a1b-299">Он позволит открыть группу ресурсов в новой колонке.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-299">It opens the resource group in a new blade.</span></span>
4. <span data-ttu-id="e6a1b-300">В элементе **Ресурсы** должны отображаться учетная запись хранения по умолчанию и фабрика данных, если только группа ресурсов не является общей для других проектов.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span></span>
5. <span data-ttu-id="e6a1b-301">Нажмите кнопку **Удалить** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-301">Click **Delete** on the top of the blade.</span></span> <span data-ttu-id="e6a1b-302">При этом также будет удалена учетная запись хранения и данные, хранящиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-302">Doing so deletes the storage account and the data stored in the storage account.</span></span>
6. <span data-ttu-id="e6a1b-303">Введите имя группы ресурсов, чтобы подтвердить удаление, и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="e6a1b-304">Если вы не хотите удалять учетную запись хранения при удалении группы ресурсов, можно использовать следующую архитектуру, отделив бизнес-данные от учетной записи хранения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span></span> <span data-ttu-id="e6a1b-305">В этом случае у вас будет одна группа ресурсов для учетной записи хранения с бизнес-данными, а другая — для учетной записи хранения по умолчанию для связанной службы HDInsight и фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span></span> <span data-ttu-id="e6a1b-306">Удаление второй группы ресурсов не затронет учетную запись хранения бизнес-данных.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-306">When you delete the second resource group, it does not impact the business data storage account.</span></span> <span data-ttu-id="e6a1b-307">Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-307">To do so:</span></span>

* <span data-ttu-id="e6a1b-308">Вместе с ресурсом Microsoft.DataFactory/datafactories в шаблоне Resource Manager добавьте следующее в группу ресурсов верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="e6a1b-309">При этом будет создана учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="e6a1b-310">Добавьте новую точку связанной службы в новую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-310">Add a new linked service point to the new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="e6a1b-311">Настройте связанную службу HDInsight по запросу с дополнительными параметрами dependsOn и additionalLinkedServiceNames:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="e6a1b-312">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e6a1b-312">Next steps</span></span>
<span data-ttu-id="e6a1b-313">В этой статье вы узнали, как использовать фабрику данных Azure для создания кластера HDInsight по запросу для обработки заданий Hive.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span></span> <span data-ttu-id="e6a1b-314">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="e6a1b-314">To read more:</span></span>

* [<span data-ttu-id="e6a1b-315">Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="e6a1b-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="e6a1b-316">Создание кластеров Hadoop под управлением Linux в HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6a1b-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="e6a1b-317">Документация по HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6a1b-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="e6a1b-318">Документация по фабрике данных</span><span class="sxs-lookup"><span data-stu-id="e6a1b-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="e6a1b-319">Приложение</span><span class="sxs-lookup"><span data-stu-id="e6a1b-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="e6a1b-320">Скрипт Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e6a1b-320">Azure CLI script</span></span>
<span data-ttu-id="e6a1b-321">Для этого руководства вместо Azure PowerShell можно использовать Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span></span> <span data-ttu-id="e6a1b-322">Чтобы использовать Azure CLI, вам необходимо сначала выполнить установку:</span><span class="sxs-lookup"><span data-stu-id="e6a1b-322">To use Azure CLI, first install Azure CLI as per the following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-to-prepare-the-storage-and-copy-the-files"></a><span data-ttu-id="e6a1b-323">Подготовка хранилища и копирование файлов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e6a1b-323">Use Azure CLI to prepare the storage and copy the files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="e6a1b-324">Имя контейнера — *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-324">The container name is *adfgetstarted*.</span></span> <span data-ttu-id="e6a1b-325">Не изменяйте его.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-325">Keep it as it is.</span></span> <span data-ttu-id="e6a1b-326">В противном случае потребуется обновить шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6a1b-326">Otherwise you need to update the Resource Manager template.</span></span> <span data-ttu-id="e6a1b-327">Дополнительные сведения об этом сценарии CLI см. в статье [Использование интерфейса командной строки (CLI) Azure со службой хранилища Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e6a1b-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
