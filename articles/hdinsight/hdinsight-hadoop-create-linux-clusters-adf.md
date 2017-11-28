---
title: "по запросу Hadoop кластеры, использующие фабрика данных — Azure HDInsight aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate Hadoop по требованию кластеров в HDInsight с помощью фабрики данных Azure."
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
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="2e8f9-103">Создание кластеров Hadoop в HDInsight по запросу с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="2e8f9-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="2e8f9-104">[Фабрика данных Azure](../data-factory/data-factory-introduction.md) — служба интеграции данных на основе облака, которая координирует и автоматизирует процессы hello перемещения и преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="2e8f9-105">Его можно создать tooprocess just-in-time кластера HDInsight Hadoop срез входных данных и удалить hello кластера после завершения обработки hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-105">It can create a HDInsight Hadoop cluster just-in-time tooprocess an input data slice and delete hello cluster when hello processing is complete.</span></span> <span data-ttu-id="2e8f9-106">Ниже приведены некоторые преимущества hello кластера Hadoop в HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-106">Some of hello benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="2e8f9-107">Вы только оплаты для задания времени hello выполняется на hello кластера HDInsight Hadoop (а также краткое настраиваемое время простоя).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-107">You only pay for hello time job is running on hello HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="2e8f9-108">Hello выставления счетов для кластеров HDInsight пропорциональной в минуту, ли вы используете их, или нет.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-108">hello billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="2e8f9-109">При использовании по требованию связанной службы HDInsight в фабрике данных кластеров hello создаются по запросу.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-109">When you use an on-demand HDInsight linked service in Data Factory, hello clusters are created on-demand.</span></span> <span data-ttu-id="2e8f9-110">И кластеры hello автоматически удаляются по завершении задания hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-110">And hello clusters are deleted automatically when hello jobs are completed.</span></span> <span data-ttu-id="2e8f9-111">Таким образом вы платите только за hello задание, выполняющееся hello краткое время простоя (значение срока жизни) и времени.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-111">Therefore, you only pay for hello job running time and hello brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="2e8f9-112">С помощью конвейера фабрики данных можно создать рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="2e8f9-113">Например может иметь hello конвейера toocopy данные из локального SQL Server tooan хранилище больших двоичных объектов, обработка данных hello, запустив скрипт Hive и сценарий Pig в кластере HDInsight Hadoop по требованию.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-113">For example, you can have hello pipeline toocopy data from an on-premises SQL Server tooan Azure blob storage, process hello data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="2e8f9-114">Затем скопируйте результат hello данных tooan хранилище данных SQL Azure для tooconsume приложений бизнес-Аналитики.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-114">Then, copy hello result data tooan Azure SQL Data Warehouse for BI applications tooconsume.</span></span>
- <span data-ttu-id="2e8f9-115">Можно запланировать hello рабочего процесса toorun периодически (каждый час, день, неделю, месяц, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-115">You can schedule hello workflow toorun periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="2e8f9-116">В фабрике данных Azure фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="2e8f9-117">Конвейер данных включает одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="2e8f9-118">Существует два типа действий: [действия перемещения данных](../data-factory/data-factory-data-movement-activities.md) и [действия преобразования данных](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="2e8f9-119">Используйте toomove действия (в настоящее время только действие копирования) перемещения данных из источника данных хранилища tooa целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-119">You use data movement activities (currently, only Copy Activity) toomove data from a source data store tooa destination data store.</span></span> <span data-ttu-id="2e8f9-120">Используются данные tootransform или процесс действия преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-120">You use data transformation activities tootransform/process data.</span></span> <span data-ttu-id="2e8f9-121">Действие Hive в HDInsight является одним из действий hello преобразования, поддерживаемые фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-121">HDInsight Hive Activity is one of hello transformation activities supported by Data Factory.</span></span> <span data-ttu-id="2e8f9-122">В этом учебнике используется действие преобразования Hive hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-122">You use hello Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="2e8f9-123">Можно настроить toouse действие hive кластера HDInsight Hadoop или кластер Hadoop в HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-123">You can configure a hive activity toouse your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="2e8f9-124">В этом учебнике hello действие Hive в конвейере фабрики данных hello является настроенным toouse кластер HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-124">In this tutorial, hello Hive activity in hello data factory pipeline is configured toouse an on-demand HDInsight cluster.</span></span> <span data-ttu-id="2e8f9-125">Таким образом когда запускается действие hello tooprocess срез данных, происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-125">Therefore, when hello activity runs tooprocess a data slice, here is what happens:</span></span>

1. <span data-ttu-id="2e8f9-126">Кластер HDInsight Hadoop автоматически создается для вас tooprocess just-in-time hello среза.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-126">A HDInsight Hadoop cluster is automatically created for you just-in-time tooprocess hello slice.</span></span>  
2. <span data-ttu-id="2e8f9-127">Hello входные данные обрабатываются, выполнив сценарий HiveQL в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-127">hello input data is processed by running a HiveQL script on hello cluster.</span></span>
3. <span data-ttu-id="2e8f9-128">кластер HDInsight Hadoop Hello удаляется после завершения обработки hello и hello кластера используется в течение hello настроить количество времени (параметр timeToLive).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-128">hello HDInsight Hadoop cluster is deleted after hello processing is complete and hello cluster is idle for hello configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="2e8f9-129">Если для обработки с в это время простоя timeToLive hello следующий срез данных, hello одного кластера — используется tooprocess hello срез.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-129">If hello next data slice is available for processing with in this timeToLive idle time, hello same cluster is used tooprocess hello slice.</span></span>  

<span data-ttu-id="2e8f9-130">В этом учебнике hello сценарий HiveQL, связанный с действием hive hello выполняет hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-130">In this tutorial, hello HiveQL script associated with hello hive activity performs hello following actions:</span></span>

1. <span data-ttu-id="2e8f9-131">Создает внешнюю таблицу, которая ссылки hello необработанные веб-данных журнала, хранящиеся в службе хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-131">Creates an external table that references hello raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="2e8f9-132">Секции hello необработанные данные за год и месяц.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-132">Partitions hello raw data by year and month.</span></span>
3. <span data-ttu-id="2e8f9-133">Сохраняет hello секционированными данными в хранилище больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-133">Stores hello partitioned data in hello Azure blob storage.</span></span>

<span data-ttu-id="2e8f9-134">В этом учебнике hello сценарий HiveQL, связанный с действием hive hello создает внешнюю таблицу, которая ссылки hello необработанные web журнала данных, хранящихся в hello хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-134">In this tutorial, hello HiveQL script associated with hello hive activity creates an external table that references hello raw web log data stored in hello Azure Blob Storage.</span></span> <span data-ttu-id="2e8f9-135">Вот hello образцов строк для каждого месяца во входном файле hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-135">Here are hello sample rows for each month in hello input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="2e8f9-136">секции сценарий HiveQL Hello hello необработанные данные за год и месяц.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-136">hello HiveQL script partitions hello raw data by year and month.</span></span> <span data-ttu-id="2e8f9-137">Он создает три папки выходных данных, на основе предыдущих ввода hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-137">It creates three output folders based on hello previous input.</span></span> <span data-ttu-id="2e8f9-138">Каждая папка содержит файл с записями по каждому месяцу.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="2e8f9-139">Список действий преобразования данных фабрики данных в операции сложения tooHive см [преобразования и анализа с помощью фабрики данных Azure](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-139">For a list of Data Factory data transformation activities in addition tooHive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2e8f9-140">Сейчас в фабрике данных Azure можно создать только кластер HDInsight версии 3.2.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e8f9-141">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2e8f9-141">Prerequisites</span></span>
<span data-ttu-id="2e8f9-142">Прежде чем начать hello инструкции в этой статье, необходимо иметь hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-142">Before you begin hello instructions in this article, you must have hello following items:</span></span>

* <span data-ttu-id="2e8f9-143">[Подписка Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="2e8f9-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="2e8f9-145">Подготовка учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="2e8f9-145">Prepare storage account</span></span>
<span data-ttu-id="2e8f9-146">Воспользуйтесь toothree учетных записей хранения в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-146">You can use up toothree storage accounts in this scenario:</span></span>

- <span data-ttu-id="2e8f9-147">Учетная запись хранения по умолчанию для кластера HDInsight hello</span><span class="sxs-lookup"><span data-stu-id="2e8f9-147">default storage account for hello HDInsight cluster</span></span>
- <span data-ttu-id="2e8f9-148">Учетная запись хранения для hello входных данных</span><span class="sxs-lookup"><span data-stu-id="2e8f9-148">storage account for hello input data</span></span>
- <span data-ttu-id="2e8f9-149">Учетная запись хранения для hello выходных данных</span><span class="sxs-lookup"><span data-stu-id="2e8f9-149">storage account for hello output data</span></span>

<span data-ttu-id="2e8f9-150">Учебник toosimplify hello, использовать одну учетную запись tooserve hello трех целей хранения.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-150">toosimplify hello tutorial, you use one storage account tooserve hello three purposes.</span></span> <span data-ttu-id="2e8f9-151">Пример сценария Hello Azure PowerShell, представленные в этом разделе выполняет следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-151">hello Azure PowerShell sample script found in this section performs hello following tasks:</span></span>

1. <span data-ttu-id="2e8f9-152">Войдите в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-152">Log in tooAzure.</span></span>
2. <span data-ttu-id="2e8f9-153">Создание группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="2e8f9-154">Создание учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="2e8f9-155">Создать контейнер больших двоичных объектов в учетной записи хранения hello</span><span class="sxs-lookup"><span data-stu-id="2e8f9-155">Create a Blob container in hello storage account</span></span>
5. <span data-ttu-id="2e8f9-156">Скопируйте следующие два контейнера больших двоичных объектов toohello файлы hello:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-156">Copy hello following two files toohello Blob container:</span></span>

   * <span data-ttu-id="2e8f9-157">Файл входных данных: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="2e8f9-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="2e8f9-158">Сценарий HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="2e8f9-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="2e8f9-159">Оба файла хранятся в общедоступном контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="2e8f9-160">**tooprepare hello хранилища и скопируйте hello файлы с помощью Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="2e8f9-160">**tooprepare hello storage and copy hello files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2e8f9-161">Укажите имена для группы ресурсов Azure hello и hello учетной записи хранилища Azure, будет создан скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-161">Specify names for hello Azure resource group and hello Azure storage account that will be created by hello script.</span></span>
> <span data-ttu-id="2e8f9-162">Запишите **имя группы ресурсов**, **имя учетной записи хранения**, и **ключ учетной записи хранения** выдаваемые hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by hello script.</span></span> <span data-ttu-id="2e8f9-163">Они необходимы в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-163">You need them in hello next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="2e8f9-164">Если вам нужна помощь с помощью скрипта PowerShell hello, см. раздел [hello использование Azure PowerShell с хранилищем Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-164">If you need help with hello PowerShell script, see [Using hello Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="2e8f9-165">Если вы хотите toouse Azure CLI вместо этого разделе hello [приложение](#appendix) раздел для hello сценария Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-165">If you like toouse Azure CLI instead, see hello [Appendix](#appendix) section for hello Azure CLI script.</span></span>

<span data-ttu-id="2e8f9-166">**tooexamine hello хранилища учетной записи и hello содержимое**</span><span class="sxs-lookup"><span data-stu-id="2e8f9-166">**tooexamine hello storage account and hello contents**</span></span>

1. <span data-ttu-id="2e8f9-167">Войдите на toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-167">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2e8f9-168">Нажмите кнопку **групп ресурсов** на левой панели hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-168">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="2e8f9-169">Дважды щелкните имя группы ресурсов hello, созданный в скриптах PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-169">Double-click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="2e8f9-170">Используйте фильтр hello, при наличии слишком много групп ресурсов в списке.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-170">Use hello filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="2e8f9-171">На hello **ресурсов** плитки, должен иметь один ресурс, если группа ресурсов hello предоставить другие проекты в списке.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-171">On hello **Resources** tile, you shall have one resource listed unless you share hello resource group with other projects.</span></span> <span data-ttu-id="2e8f9-172">Этот ресурс является hello учетной записи хранилища с именем hello, указанного ранее.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-172">That resource is hello storage account with hello name you specified earlier.</span></span> <span data-ttu-id="2e8f9-173">Щелкните имя учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-173">Click hello storage account name.</span></span>
5. <span data-ttu-id="2e8f9-174">Нажмите кнопку hello **большие двоичные объекты** плитки.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-174">Click hello **Blobs** tiles.</span></span>
6. <span data-ttu-id="2e8f9-175">Нажмите кнопку hello **adfgetstarted** контейнера.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-175">Click hello **adfgetstarted** container.</span></span> <span data-ttu-id="2e8f9-176">Вы увидите две папки: **inputdata** и **script**.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="2e8f9-177">Откройте папку hello и проверьте hello файлы в папках hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-177">Open hello folder and check hello files in hello folders.</span></span> <span data-ttu-id="2e8f9-178">Hello inputdata файлом hello input.log с входными данными и hello скрипт папка содержит файл скрипта HiveQL hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-178">hello inputdata contains hello input.log file with input data and hello script folder contains hello HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="2e8f9-179">Создание фабрики данных с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e8f9-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="2e8f9-180">Hello учетной записи хранилища, hello входных данных и hello подготовить сценарий HiveQL будут готовы toocreate фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-180">With hello storage account, hello input data, and hello HiveQL script prepared, you are ready toocreate an Azure data factory.</span></span> <span data-ttu-id="2e8f9-181">Существует несколько способов создания фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="2e8f9-182">В этом учебнике создать фабрику данных путем развертывания шаблона Azure Resource Manager с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using hello Azure portal.</span></span> <span data-ttu-id="2e8f9-183">Вы также можете развернуть шаблон Resource Manager с помощью [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) или [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="2e8f9-184">Описание других способов создания фабрики данных вы найдете в [руководстве по созданию фабрики данных](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="2e8f9-185">Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-185">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> <span data-ttu-id="2e8f9-186">Hello шаблона находится в https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-186">hello template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="2e8f9-187">В разделе hello [фабрики данных сущности в шаблоне hello](#data-factory-entities-in-the-template) подробные сведения о сущности, определенные в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-187">See hello [Data Factory entities in hello template](#data-factory-entities-in-the-template) section for detailed information about entities defined in hello template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="2e8f9-188">Выберите **использовать существующие** параметр для hello **группы ресурсов** параметр и выберите hello имя группы ресурсов hello, созданный на предыдущем шаге hello (с помощью сценария PowerShell).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-188">Select **Use existing** option for hello **Resource group** setting, and select hello name of hello resource group you created in hello previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="2e8f9-189">Введите имя фабрики данных hello (**имя фабрики данных**).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-189">Enter a name for hello data factory (**Data Factory Name**).</span></span> <span data-ttu-id="2e8f9-190">Оно должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="2e8f9-191">Введите hello **имя учетной записи хранения** и **ключ учетной записи хранения** записанные на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-191">Enter hello **storage account name** and **storage account key** you wrote down in hello previous step.</span></span>
5. <span data-ttu-id="2e8f9-192">Выберите **я принимаю условия toohello** говорилось выше, после тщательного изучения **условий**.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-192">Select **I agree toohello terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="2e8f9-193">Выберите **toodashboard ПИН-код** параметр.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-193">Select **Pin toodashboard** option.</span></span>
6. <span data-ttu-id="2e8f9-194">Щелкните **Purchase/Create** (Купить или Создать).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="2e8f9-195">Вы видите плитку на панель мониторинга называется hello **развертывание шаблона-развертывания**.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-195">You see a tile on hello Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="2e8f9-196">Подождите, пока hello **группы ресурсов** открывает колонку для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-196">Wait until hello **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="2e8f9-197">Можно также щелкнуть плитку hello под названием как вашей группы имя tooopen hello ресурсов группы колонки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-197">You can also click hello tile titled as your resource group name tooopen hello resource group blade.</span></span>
6. <span data-ttu-id="2e8f9-198">Щелкните группу ресурсов hello tooopen плитки приветствия, если колонки группы ресурсов hello еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-198">Click hello tile tooopen hello resource group if hello resource group blade is not already open.</span></span> <span data-ttu-id="2e8f9-199">Теперь будет отображаться один дополнительные ресурсы фабрики данных, кроме перечисленных toohello ресурс учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-199">Now you shall see one more data factory resource listed in addition toohello storage account resource.</span></span>
7. <span data-ttu-id="2e8f9-200">Щелкните имя hello фабрики данных (значение, указанное для hello **имя фабрики данных** параметр).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-200">Click hello name of your data factory (value you specified for hello **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="2e8f9-201">В колонке hello фабрики данных, нажмите кнопку hello **схема** плитки.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-201">In hello Data Factory blade, click hello **Diagram** tile.</span></span> <span data-ttu-id="2e8f9-202">Hello схеме показано одно действие с входного набора данных и выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-202">hello diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Фабрика данных Azure: схема конвейера действий Hive в кластере HDInsight по запросу](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="2e8f9-204">имена Hello определены в шаблоне hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-204">hello names are defined in hello Resource Manager template.</span></span>
9. <span data-ttu-id="2e8f9-205">Дважды щелкните **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="2e8f9-206">На hello **последние обновления фрагменты**, вы увидите один срез.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-206">On hello **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="2e8f9-207">Если состояние hello **выполняется**, подождите, пока он изменяется слишком**готовности**.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-207">If hello status is **In progress**, wait until it is changed too**Ready**.</span></span> <span data-ttu-id="2e8f9-208">Обычно это занимает около **20 минут** toocreate кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-208">It usually takes about **20 minutes** toocreate an HDInsight cluster.</span></span>

### <a name="check-hello-data-factory-output"></a><span data-ttu-id="2e8f9-209">Проверьте выходные данные для фабрики данных hello</span><span class="sxs-lookup"><span data-stu-id="2e8f9-209">Check hello data factory output</span></span>

1. <span data-ttu-id="2e8f9-210">Используйте hello же процедуру, описанную в hello последнего сеанса toocheck hello контейнеров hello adfgetstarted контейнера.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-210">Use hello same procedure in hello last session toocheck hello containers of hello adfgetstarted container.</span></span> <span data-ttu-id="2e8f9-211">Существует два новых контейнеров в дополнение к этому слишком**adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-211">There are two new containers in addition too**adfgetsarted**:</span></span>

   * <span data-ttu-id="2e8f9-212">Контейнер с именем, hello шаблону: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-212">A container with name that follows hello pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="2e8f9-213">Этот контейнер — контейнер по умолчанию hello для кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-213">This container is hello default container for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="2e8f9-214">adfjobs: этот контейнер — контейнер hello для hello ADF. журналы заданий.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-214">adfjobs: This container is hello container for hello ADF job logs.</span></span>

     <span data-ttu-id="2e8f9-215">Вывод фабрики Hello данных хранится в **afgetstarted** , которые были настроены в шаблоне hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-215">hello data factory output is stored in **afgetstarted** as you configured in hello Resource Manager template.</span></span>
2. <span data-ttu-id="2e8f9-216">Щелкните **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="2e8f9-217">Дважды щелкните **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="2e8f9-218">Вы видите **год = 2014** папку, так как все веб-журналы hello датированные 2014 года.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-218">You see a **year=2014** folder because all hello web logs are dated in year 2014.</span></span>

    ![Фабрика данных Azure: выходные данные конвейера действия Hive в кластере HDInsight по запросу](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="2e8f9-220">Если детализация углублением список hello, будет отображаться три папки за январь, февраль и март.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-220">If you drill down hello list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="2e8f9-221">Для каждого месяца существует журнал.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-221">And there is a log for each month.</span></span>

    ![Фабрика данных Azure: выходные данные конвейера действия Hive в кластере HDInsight по запросу](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="2e8f9-223">Фабрика сущностями данных в шаблоне hello</span><span class="sxs-lookup"><span data-stu-id="2e8f9-223">Data Factory entities in hello template</span></span>
<span data-ttu-id="2e8f9-224">Вот, как выглядит hello верхнего уровня шаблона диспетчера ресурсов для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-224">Here is how hello top-level Resource Manager template for a data factory looks like:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="2e8f9-225">Определение фабрики данных</span><span class="sxs-lookup"><span data-stu-id="2e8f9-225">Define data factory</span></span>
<span data-ttu-id="2e8f9-226">Фабрика данных определить в шаблоне hello диспетчера ресурсов, как показано в следующих образец hello:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-226">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="2e8f9-227">с именем dataFactoryName Hello — имя hello hello фабрики данных, которые указываются при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-227">hello dataFactoryName is hello name of hello data factory you specify when you deploy hello template.</span></span> <span data-ttu-id="2e8f9-228">Фабрика данных — в настоящее время поддерживается только в регионах hello Восток США, Запад США и Северной Европе.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-228">Data factory is currently only supported in hello East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-hello-data-factory"></a><span data-ttu-id="2e8f9-229">Определение сущности в рамках фабрики данных hello</span><span class="sxs-lookup"><span data-stu-id="2e8f9-229">Defining entities within hello data factory</span></span>
<span data-ttu-id="2e8f9-230">Hello следующие сущности фабрики данных определены в шаблоне hello JSON:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-230">hello following Data Factory entities are defined in hello JSON template:</span></span>

* [<span data-ttu-id="2e8f9-231">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="2e8f9-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="2e8f9-232">Связанная служба кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="2e8f9-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="2e8f9-233">Входной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="2e8f9-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="2e8f9-234">Выходной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="2e8f9-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="2e8f9-235">Конвейер данных с действием копирования</span><span class="sxs-lookup"><span data-stu-id="2e8f9-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="2e8f9-236">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="2e8f9-236">Azure Storage linked service</span></span>
<span data-ttu-id="2e8f9-237">Hello хранилища Azure связанные ссылки на службу фабрики данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-237">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="2e8f9-238">В этом учебнике hello учетную запись хранения используется как учетная запись хранения HDInsight по умолчанию hello, входные данные и хранилищем вывода данных.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-238">In this tutorial, hello same storage account is used as hello default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="2e8f9-239">Таким образом, вы определяете только одну связанную службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="2e8f9-240">В определении службы hello связаны укажите имя hello и ключ учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-240">In hello linked service definition, you specify hello name and key of your Azure storage account.</span></span> <span data-ttu-id="2e8f9-241">В разделе [связанная служба хранилища Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) подробные сведения о JSON свойства, используемые toodefine связанная служба хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>

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
<span data-ttu-id="2e8f9-242">Hello **connectionString** использует hello storageAccountName и storageAccountKey параметров.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-242">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="2e8f9-243">Необходимо указать значения для этих параметров при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-243">You specify values for these parameters while deploying hello template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="2e8f9-244">Связанная служба кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="2e8f9-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="2e8f9-245">В hello HDInsight по требованию связанное определение службы, укажите значения для параметров конфигурации, используемых hello фабрики данных службы toocreate кластера HDInsight Hadoop во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-245">In hello on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by hello Data Factory service toocreate a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="2e8f9-246">В разделе [связанные службы вычислений](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) статьи для получения сведений об toodefine свойства, используемые JSON связанной службы HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="2e8f9-247">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-247">Note hello following points:</span></span>

* <span data-ttu-id="2e8f9-248">Hello фабрики данных создает **под управлением Linux** кластера HDInsight для вас.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-248">hello Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="2e8f9-249">Hello кластера HDInsight Hadoop создается в hello же регионе, что учетная запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-249">hello HDInsight Hadoop cluster is created in hello same region as hello storage account.</span></span>
* <span data-ttu-id="2e8f9-250">Обратите внимание hello *timeToLive* параметр.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-250">Notice hello *timeToLive* setting.</span></span> <span data-ttu-id="2e8f9-251">Фабрика данных Hello автоматически удаляет hello кластера после hello кластера простоя в течение 30 минут.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-251">hello data factory deletes hello cluster automatically after hello cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="2e8f9-252">Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-252">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="2e8f9-253">При удалении hello кластера HDInsight не удаляет этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-253">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="2e8f9-254">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-254">This behavior is by design.</span></span> <span data-ttu-id="2e8f9-255">С помощью по требованию связанной службы HDInsight, кластер HDInsight создается каждый раз фрагмент должен обработать, если нет существующего кластера динамической toobe (**timeToLive**) и удаляется при завершении обработки hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

<span data-ttu-id="2e8f9-256">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e8f9-257">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="2e8f9-258">Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-258">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="2e8f9-259">имена этих контейнеров Hello соответствуют шаблону: «adf**yourdatafactoryname**-**linkedservicename**- datetimestamp».</span><span class="sxs-lookup"><span data-stu-id="2e8f9-259">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="2e8f9-260">Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="2e8f9-261">Входной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="2e8f9-261">Azure blob input dataset</span></span>
<span data-ttu-id="2e8f9-262">В определении hello входного набора данных укажите имена hello контейнер больших двоичных объектов, папки и файла, содержащего входные данные hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-262">In hello input dataset definition, you specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="2e8f9-263">В разделе [свойства набора данных больших двоичных объектов Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>

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

<span data-ttu-id="2e8f9-264">Обратите внимание, следующие параметры в определении JSON hello hello:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-264">Notice hello following specific settings in hello JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="2e8f9-265">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="2e8f9-265">Azure Blob output dataset</span></span>
<span data-ttu-id="2e8f9-266">В определении набора данных для вывода hello укажите имена hello контейнер больших двоичных объектов и папке, содержащей hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-266">In hello output dataset definition, you specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="2e8f9-267">В разделе [свойства набора данных больших двоичных объектов Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="2e8f9-268">Hello folderPath указывает hello путь toohello папке, содержащей hello выходные данные:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-268">hello folderPath specifies hello path toohello folder that holds hello output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="2e8f9-269">Hello [доступности набора данных](../data-factory/data-factory-create-datasets.md#dataset-availability) задается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-269">hello [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="2e8f9-270">В фабрике данных Azure, выходной набор данных доступности дисков hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-270">In Azure Data Factory, output dataset availability drives hello pipeline.</span></span> <span data-ttu-id="2e8f9-271">В этом примере hello срез создается ежемесячно hello последний день месяца (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-271">In this example, hello slice is produced monthly on hello last day of month (EndOfInterval).</span></span> <span data-ttu-id="2e8f9-272">Дополнительные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="2e8f9-273">Конвейер данных</span><span class="sxs-lookup"><span data-stu-id="2e8f9-273">Data pipeline</span></span>
<span data-ttu-id="2e8f9-274">Здесь вы определите конвейер для преобразования данных. Для этого нужно запустить скрипт Hive в кластере HDInsight Azure по требованию.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="2e8f9-275">В разделе [конвейера JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) описания toodefine элементы, используемые JSON конвейера в этом примере.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span>

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

<span data-ttu-id="2e8f9-276">конвейер Hello содержит одно действие, действие HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-276">hello pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="2e8f9-277">Так как даты начала и окончания находятся в пределах января 2016 г., обрабатываются данные только за один месяц (срез).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="2e8f9-278">Оба *запустить* и *окончания* hello действия имеют прошедшую дату, поэтому hello фабрики данных обрабатывает данные за месяц hello немедленно.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-278">Both *start* and *end* of hello activity have a past date, so hello Data Factory processes data for hello month immediately.</span></span> <span data-ttu-id="2e8f9-279">Если конец hello дату в будущем, hello фабрики данных создает другой срез, когда наступает время hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-279">If hello end is a future date, hello data factory creates another slice when hello time comes.</span></span> <span data-ttu-id="2e8f9-280">Дополнительные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="2e8f9-281">Очистка hello учебника</span><span class="sxs-lookup"><span data-stu-id="2e8f9-281">Clean up hello tutorial</span></span>

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="2e8f9-282">Удаление контейнеров больших двоичных объектов hello, созданное кластером HDInsight по требованию</span><span class="sxs-lookup"><span data-stu-id="2e8f9-282">Delete hello blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="2e8f9-283">С помощью по требованию связанной службы HDInsight кластер HDInsight создается каждый раз фрагмент должен toobe обработки, если нет существующего кластера динамическая (timeToLive); и hello кластер будет удален после завершения обработки hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (timeToLive); and hello cluster is deleted when hello processing is done.</span></span> <span data-ttu-id="2e8f9-284">Для каждого кластера фабрики данных Azure создает контейнер больших двоичных объектов в хранилище больших двоичных объектов, используется в качестве учетной записи хранилища по умолчанию hello для кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-284">For each cluster, Azure Data Factory creates a blob container in hello Azure blob storage used as hello default stroage account for hello cluster.</span></span> <span data-ttu-id="2e8f9-285">Несмотря на то, что кластер HDInsight удален, контейнер хранилища больших двоичных объектов по умолчанию hello и учетной записи хранения связанных hello не удаляются.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-285">Even though HDInsight cluster is deleted, hello default blob storage container and hello associated storage account are not deleted.</span></span> <span data-ttu-id="2e8f9-286">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-286">This behavior is by design.</span></span> <span data-ttu-id="2e8f9-287">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="2e8f9-288">Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-288">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="2e8f9-289">имена этих контейнеров Hello соответствуют шаблону: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-289">hello names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="2e8f9-290">Удалить hello **adfjobs** и **adfyourdatafactoryname linkedservicename-datetimestamp** папки.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-290">Delete hello **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="2e8f9-291">контейнер adfjobs Hello содержит журналы заданий из фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-291">hello adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-hello-resource-group"></a><span data-ttu-id="2e8f9-292">Удаление группы ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="2e8f9-292">Delete hello resource group</span></span>
<span data-ttu-id="2e8f9-293">[Диспетчер ресурсов Azure](../azure-resource-manager/resource-group-overview.md) — используется toodeploy управлять и отслеживать ваше решение как группу.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used toodeploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="2e8f9-294">При удалении группы ресурсов удаляются все компоненты hello внутри группы hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-294">Deleting a resource group deletes all hello components inside hello group.</span></span>  

1. <span data-ttu-id="2e8f9-295">Войдите на toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-295">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2e8f9-296">Нажмите кнопку **групп ресурсов** на левой панели hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-296">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="2e8f9-297">Щелкните имя группы ресурсов hello, созданный в скриптах PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-297">Click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="2e8f9-298">Используйте фильтр hello, при наличии слишком много групп ресурсов в списке.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-298">Use hello filter if you have too many resource groups listed.</span></span> <span data-ttu-id="2e8f9-299">Группа ресурсов hello открывается новая колонка.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-299">It opens hello resource group in a new blade.</span></span>
4. <span data-ttu-id="2e8f9-300">На hello **ресурсов** плитки, должен иметь учетную запись хранения по умолчанию hello и hello фабрики данных, если группа ресурсов hello предоставить другие проекты в списке.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-300">On hello **Resources** tile, you shall have hello default storage account and hello data factory listed unless you share hello resource group with other projects.</span></span>
5. <span data-ttu-id="2e8f9-301">Нажмите кнопку **удалить** на hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-301">Click **Delete** on hello top of hello blade.</span></span> <span data-ttu-id="2e8f9-302">Таким образом Удаляет учетную запись хранения hello и hello данные, хранящиеся в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-302">Doing so deletes hello storage account and hello data stored in hello storage account.</span></span>
6. <span data-ttu-id="2e8f9-303">Введите удаление tooconfirm имя группы ресурсов hello и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-303">Enter hello resource group name tooconfirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="2e8f9-304">В случае, если вы не хотите учетной записи хранилища hello toodelete при удалении группы ресурсов hello, рассмотрите следующие архитектуры, разделяя hello бизнес-данных из учетной записи хранения по умолчанию hello hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-304">In case you don't want toodelete hello storage account when you delete hello resource group, consider hello following architecture by separating hello business data from hello default storage account.</span></span> <span data-ttu-id="2e8f9-305">В этом случае одну группу ресурсов для учетной записи хранения hello hello бизнес-данными и hello другой группе ресурсов для учетной записи хранения по умолчанию hello для HDInsight связанные службы и hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-305">In this case, you have one resource group for hello storage account with hello business data, and hello other resource group for hello default storage account for HDInsight linked service and hello data factory.</span></span> <span data-ttu-id="2e8f9-306">При удалении hello второй группы ресурсов, не мешая учетной записи хранилища данных предприятия hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-306">When you delete hello second resource group, it does not impact hello business data storage account.</span></span> <span data-ttu-id="2e8f9-307">toodo так:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-307">toodo so:</span></span>

* <span data-ttu-id="2e8f9-308">Добавьте hello, следуя toohello группы ресурсов верхнего уровня, а также hello Microsoft.DataFactory/datafactories ресурсов в шаблон диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-308">Add hello following toohello top-level resource group along with hello Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="2e8f9-309">При этом будет создана учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-309">It creates a storage account:</span></span>

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
* <span data-ttu-id="2e8f9-310">Добавление новой связанной службы toohello точки учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-310">Add a new linked service point toohello new storage account:</span></span>

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
* <span data-ttu-id="2e8f9-311">Настройте службу ondemand связанных hello HDInsight с дополнительных dependsOn и additionalLinkedServiceNames.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-311">Configure hello HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="2e8f9-312">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e8f9-312">Next steps</span></span>
<span data-ttu-id="2e8f9-313">В этой статье вы узнали как tooprocess кластера HDInsight toouse фабрики данных Azure toocreate по требованию задания Hive.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-313">In this article, you have learned how toouse Azure Data Factory toocreate on-demand HDInsight cluster tooprocess Hive jobs.</span></span> <span data-ttu-id="2e8f9-314">Дополнительные tooread:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-314">tooread more:</span></span>

* [<span data-ttu-id="2e8f9-315">Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2e8f9-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="2e8f9-316">Создание кластеров Hadoop под управлением Linux в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e8f9-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="2e8f9-317">Документация по HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e8f9-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="2e8f9-318">Документация по фабрике данных</span><span class="sxs-lookup"><span data-stu-id="2e8f9-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="2e8f9-319">Приложение</span><span class="sxs-lookup"><span data-stu-id="2e8f9-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="2e8f9-320">Скрипт Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2e8f9-320">Azure CLI script</span></span>
<span data-ttu-id="2e8f9-321">Вместо использования учебника hello toodo Azure PowerShell можно использовать Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-321">You can use Azure CLI instead of using Azure PowerShell toodo hello tutorial.</span></span> <span data-ttu-id="2e8f9-322">toouse Azure CLI, сначала следует установить Azure CLI согласно инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="2e8f9-322">toouse Azure CLI, first install Azure CLI as per hello following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a><span data-ttu-id="2e8f9-323">Использовать хранилище hello tooprepare Azure CLI и скопируйте файлы hello</span><span class="sxs-lookup"><span data-stu-id="2e8f9-323">Use Azure CLI tooprepare hello storage and copy hello files</span></span>

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

<span data-ttu-id="2e8f9-324">Имя контейнера Hello — *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-324">hello container name is *adfgetstarted*.</span></span> <span data-ttu-id="2e8f9-325">Не изменяйте его.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-325">Keep it as it is.</span></span> <span data-ttu-id="2e8f9-326">В противном случае необходимо tooupdate шаблона диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="2e8f9-326">Otherwise you need tooupdate hello Resource Manager template.</span></span> <span data-ttu-id="2e8f9-327">Если вам нужна помощь с помощью этого сценария CLI, см. раздел [использование hello Azure CLI со службой хранилища Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2e8f9-327">If you need help with this CLI script, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
