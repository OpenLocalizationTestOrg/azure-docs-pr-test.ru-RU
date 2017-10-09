---
title: "данные задержки рейсов aaaAnalyze на Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toouse один Windows PowerShell скрипт toocreate кластер HDInsight запуска задания Hive, запустите задание Sqoop и удалить кластер hello."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="0f164-103">Анализ данных о задержке рейсов с помощью Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f164-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="0f164-104">Hive предоставляет средства для выполнения заданий Hadoop MapReduce с помощью языка сценариев, аналогичного SQL, под названием *[HiveQL][hadoop-hiveql]*, который применяется для обобщения данных, создания запросов и анализа больших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="0f164-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f164-105">Hello в данном пошаговом руководстве требуется кластер HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="0f164-105">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="0f164-106">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="0f164-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0f164-107">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0f164-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="0f164-108">Инструкции по работе с кластерами под управлением Linux см. в статье [Анализ данных о задержке рейсов с помощью Hive в HDInsight в Linux](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0f164-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="0f164-109">Одно из главных преимуществ hello Azure HDInsight — разделение hello хранения данных и вычислений.</span><span class="sxs-lookup"><span data-stu-id="0f164-109">One of hello major benefits of Azure HDInsight is hello separation of data storage and compute.</span></span> <span data-ttu-id="0f164-110">HDInsight использует для хранения данных хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="0f164-111">Типичное задание состоит из 3 частей:</span><span class="sxs-lookup"><span data-stu-id="0f164-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="0f164-112">**Хранение данных в хранилище больших двоичных объектов Azure.**</span><span class="sxs-lookup"><span data-stu-id="0f164-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="0f164-113">Например, данные о погодных условиях, данные, получаемые от датчиков, журналы учета сетевой активности и, как в настоящем случае, данные о задержке авиарейсов сохраняются в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="0f164-114">**Выполнение заданий.**</span><span class="sxs-lookup"><span data-stu-id="0f164-114">**Run jobs.**</span></span> <span data-ttu-id="0f164-115">Когда данные hello tooprocess времени, запуска сценария Windows PowerShell (или клиентском приложении) toocreate кластер HDInsight выполнения заданий и удалить кластер hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-115">When it is time tooprocess hello data, you run a Windows PowerShell script (or a client application) toocreate an HDInsight cluster, run jobs, and delete hello cluster.</span></span> <span data-ttu-id="0f164-116">задания Hello сохранить tooAzure вывод данных хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="0f164-116">hello jobs save output data tooAzure Blob storage.</span></span> <span data-ttu-id="0f164-117">Hello выходных данных сохраняется даже после удаления кластера hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-117">hello output data is retained even after hello cluster is deleted.</span></span> <span data-ttu-id="0f164-118">Такой подход позволяет платить только за использованные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0f164-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="0f164-119">**Извлечение выходных данных hello из хранилища больших двоичных объектов Azure**, или в этом учебнике экспорта базы данных Azure SQL tooan данных hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-119">**Retrieve hello output from Azure Blob storage**, or in this tutorial, export hello data tooan Azure SQL database.</span></span>

<span data-ttu-id="0f164-120">Hello следующей диаграмме показан сценарий hello и структура hello данного учебника:</span><span class="sxs-lookup"><span data-stu-id="0f164-120">hello following diagram illustrates hello scenario and hello structure of this tutorial:</span></span>

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="0f164-122">Обратите внимание, что номера hello hello диаграмме соответствуют toohello названия разделов.</span><span class="sxs-lookup"><span data-stu-id="0f164-122">Note that hello numbers in hello diagram correspond toohello section titles.</span></span> <span data-ttu-id="0f164-123">**M** расшифровывается главный процесс hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-123">**M** stands for hello main process.</span></span> <span data-ttu-id="0f164-124">**Объект** расшифровывается hello содержимого в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-124">**A** stands for hello content in hello appendix.</span></span>

<span data-ttu-id="0f164-125">Hello основной части hello учебника показано, как toouse один Windows PowerShell скрипт tooperform hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="0f164-125">hello main portion of hello tutorial shows you how toouse one Windows PowerShell script tooperform hello following tasks:</span></span>

* <span data-ttu-id="0f164-126">Создание кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f164-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="0f164-127">Выполните задание куста hello кластера toocalculate Средняя задержка в аэропортах.</span><span class="sxs-lookup"><span data-stu-id="0f164-127">Run a Hive job on hello cluster toocalculate average delays at airports.</span></span> <span data-ttu-id="0f164-128">Hello рейса задержки данные хранятся в учетной записи хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-128">hello flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="0f164-129">Запустите Sqoop задания tooexport hello Hive задания вывода tooan базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="0f164-129">Run a Sqoop job tooexport hello Hive job output tooan Azure SQL database.</span></span>
* <span data-ttu-id="0f164-130">Удаление кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-130">Delete hello HDInsight cluster.</span></span>

<span data-ttu-id="0f164-131">В приложения hello hello инструкции можно найти для отправки данных задержки рейсов, создание и отправка строку запроса Hive и подготовка базы данных Azure SQL hello задание Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-131">In hello appendixes, you can find hello instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing hello Azure SQL database for hello Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="0f164-132">Hello действия в этом документе, определенных tooWindows основе кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f164-132">hello steps in this document are specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="0f164-133">Инструкции по работе с кластерами под управлением Linux см. в статье [Анализ данных о задержке рейсов с помощью Hive в HDInsight](hdinsight-analyze-flight-delay-data-linux.md) (для Linux).</span><span class="sxs-lookup"><span data-stu-id="0f164-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0f164-134">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0f164-134">Prerequisites</span></span>
<span data-ttu-id="0f164-135">Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0f164-135">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="0f164-136">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="0f164-136">**An Azure subscription**.</span></span> <span data-ttu-id="0f164-137">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0f164-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0f164-138"><seg>
  **Рабочая станция с Azure PowerShell**.</seg></span><span class="sxs-lookup"><span data-stu-id="0f164-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0f164-139">Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="0f164-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="0f164-140">шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-140">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="0f164-141">Выполните шаги hello в [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello последнюю версию Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f164-141">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="0f164-142">При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="0f164-142">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="0f164-143">**Файлы, используемые в этом учебнике**</span><span class="sxs-lookup"><span data-stu-id="0f164-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="0f164-144">В этом учебнике используется hello производительность на время данных рейса авиакомпании из [исследований и инновационных технологий администрирования, бюро статистики Транспортировка и РИТУ][rita-website].</span><span class="sxs-lookup"><span data-stu-id="0f164-144">This tutorial uses hello on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="0f164-145">Копия данных была hello загружен tooan контейнер хранилища больших двоичных объектов Azure с разрешения на доступ к большой двоичный объект открытого hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-145">A copy of hello data has been uploaded tooan Azure Blob storage container with hello Public Blob access permission.</span></span>
<span data-ttu-id="0f164-146">Часть скрипта PowerShell hello данных копируется из hello большой двоичный объект открытого контейнера toohello по умолчанию контейнер больших двоичных объектов кластера.</span><span class="sxs-lookup"><span data-stu-id="0f164-146">A part of your PowerShell script copies hello data from hello public blob container toohello default blob container of your cluster.</span></span> <span data-ttu-id="0f164-147">Hello HiveQL сценария можно скопировать toohello же контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="0f164-147">hello HiveQL script is also copied toohello same Blob container.</span></span>
<span data-ttu-id="0f164-148">Toolearn как tooyour данных hello tooget "или" отправлять рабочие учетной записи хранилища и как файл, toocreate "или" отправлять hello HiveQL скрипта. в разделе [приложение A](#appendix-a) и [приложении Б](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="0f164-148">If you want toolearn how tooget/upload hello data tooyour own Storage account, and how toocreate/upload hello HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="0f164-149">Hello следующей таблице перечислены файлы hello, используемые в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0f164-149">hello following table lists hello files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="0f164-150">Файлы</span><span class="sxs-lookup"><span data-stu-id="0f164-150">Files</span></span></th><th><span data-ttu-id="0f164-151">Описание</span><span class="sxs-lookup"><span data-stu-id="0f164-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="0f164-152">использовать файл сценария HiveQL Hello задания Hive hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-152">hello HiveQL script file used by hello Hive job.</span></span> <span data-ttu-id="0f164-153">Этот скрипт был загруженного tooan учетной записи хранилища больших двоичных объектов Azure с hello общего доступа.</span><span class="sxs-lookup"><span data-stu-id="0f164-153">This script has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="0f164-154"><a href="#appendix-b">Приложение Б</a> содержит инструкции по подготовке и загрузке файла tooyour собственные Azure BLOB-объектов учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0f164-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="0f164-155">Входные данные для задания Hive hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-155">Input data for hello Hive job.</span></span> <span data-ttu-id="0f164-156">Hello данные были отправленного tooan учетной записи хранилища больших двоичных объектов Azure с hello общего доступа.</span><span class="sxs-lookup"><span data-stu-id="0f164-156">hello data has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="0f164-157"><a href="#appendix-a">Приложение А</a> имеет инструкции на получение данных hello и передачи hello данных tooyour собственные Azure BLOB-объектов учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="0f164-157"><a href="#appendix-a">Appendix A</a> has instructions on getting hello data and uploading hello data tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="0f164-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="0f164-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="0f164-159">Hello выходной путь для задания Hive hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-159">hello output path for hello Hive job.</span></span> <span data-ttu-id="0f164-160">контейнер по умолчанию Hello используется для хранения выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-160">hello default container is used for storing hello output data.</span></span></td></tr>
<tr><td><span data-ttu-id="0f164-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="0f164-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="0f164-162">Hello Hive папка состояние задания на контейнер по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-162">hello Hive job status folder on hello default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="0f164-163">Создание кластера и выполнение заданий Hive и Sqoop</span><span class="sxs-lookup"><span data-stu-id="0f164-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="0f164-164">Hadoop MapReduce представляет из себя пакетную обработку данных.</span><span class="sxs-lookup"><span data-stu-id="0f164-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="0f164-165">Hello большинство toorun экономически эффективным способом задания Hive toocreate кластер состоит из задания hello и удалите hello задание после завершения задания hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-165">hello most cost-effective way toorun a Hive job is toocreate a cluster for hello job, and delete hello job after hello job is completed.</span></span> <span data-ttu-id="0f164-166">Hello следующий скрипт охватывает весь процесс hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-166">hello following script covers hello whole process.</span></span>
<span data-ttu-id="0f164-167">Дополнительные сведения о создании кластера HDInsight и выполнении заданий Hive см. в статьях [Создание кластеров Hadoop в HDInsight][hdinsight-provision] и [Использование Hive с HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="0f164-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="0f164-168">**запросы Hive hello toorun по Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0f164-168">**toorun hello Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="0f164-169">Создать таблицу базы данных и hello Azure SQL для выходных данных задания Sqoop hello с помощью инструкций hello в [приложении C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="0f164-169">Create an Azure SQL database and hello table for hello Sqoop job output by using hello instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="0f164-170">Откройте Windows PowerShell ISE и выполните следующий скрипт hello:</span><span class="sxs-lookup"><span data-stu-id="0f164-170">Open Windows PowerShell ISE, and run hello following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="0f164-171">База данных SQL tooyour подключиться и задержки рейсов среднее по городам в таблице AvgDelays hello:</span><span class="sxs-lookup"><span data-stu-id="0f164-171">Connect tooyour SQL database and see average flight delays by city in hello AvgDelays table:</span></span>

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="0f164-173"><a id="appendix-a"></a>Приложение А передачи рейса задержка данных tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="0f164-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data tooAzure Blob storage</span></span>
<span data-ttu-id="0f164-174">Отправка файла данных hello и файлы сценариев HiveQL hello (см. [приложении Б](#appendix-b)) требует решения некоторых вопросов.</span><span class="sxs-lookup"><span data-stu-id="0f164-174">Uploading hello data file and hello HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="0f164-175">Hello идея состоит, файлы данных toostore hello и hello HiveQL файла до создания кластера HDInsight и запуск задания Hive hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-175">hello idea is toostore hello data files and hello HiveQL file before creating an HDInsight cluster and running hello Hive job.</span></span> <span data-ttu-id="0f164-176">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="0f164-176">You have two options:</span></span>

* <span data-ttu-id="0f164-177">**Используйте hello же учетную запись хранилища Azure, который будет использоваться кластером HDInsight hello как файловой системы по умолчанию hello.**</span><span class="sxs-lookup"><span data-stu-id="0f164-177">**Use hello same Azure Storage account that will be used by hello HDInsight cluster as hello default file system.**</span></span> <span data-ttu-id="0f164-178">Так как кластер HDInsight hello будет ключ доступа учетной записи хранения hello, нет необходимости toomake дополнительные изменения.</span><span class="sxs-lookup"><span data-stu-id="0f164-178">Because hello HDInsight cluster will have hello Storage account access key, you don't need toomake any additional changes.</span></span>
* <span data-ttu-id="0f164-179">**Используйте другую учетную запись хранилища Azure hello HDInsight кластера по умолчанию файловой системы.**</span><span class="sxs-lookup"><span data-stu-id="0f164-179">**Use a different Azure Storage account from hello HDInsight cluster default file system.**</span></span> <span data-ttu-id="0f164-180">Если это так hello, необходимо изменить часть создания hello hello сценарий, найденных в Windows PowerShell [кластера HDInsight, создания и выполнения задания Hive и Sqoop](#runjob) toolink hello учетной записи хранилища, дополнительной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0f164-180">If this is hello case, you must modify hello creation part of hello Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) toolink hello Storage account as an additional Storage account.</span></span> <span data-ttu-id="0f164-181">Инструкции см. в статье [Создание кластеров Hadoop в HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="0f164-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="0f164-182">Затем кластер HDInsight Hello знает hello ключ доступа для учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-182">hello HDInsight cluster then knows hello access key for hello Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="0f164-183">Здравствуйте, путь к хранилищу BLOB-объекта для файла данных закодирована в файле сценария HiveQL hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="0f164-183">hello Blob storage path for hello data file is hard coded in hello HiveQL script file.</span></span> <span data-ttu-id="0f164-184">Его следует обновлять соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="0f164-184">You must update it accordingly.</span></span>

<span data-ttu-id="0f164-185">**toodownload hello рейса данных**</span><span class="sxs-lookup"><span data-stu-id="0f164-185">**toodownload hello flight data**</span></span>

1. <span data-ttu-id="0f164-186">Обзор слишком[исследования и инновационные технологии администрирования бюро статистики Транспортировка][rita-website].</span><span class="sxs-lookup"><span data-stu-id="0f164-186">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="0f164-187">На странице приветствия выберите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="0f164-187">On hello page, select hello following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="0f164-188">Имя</span><span class="sxs-lookup"><span data-stu-id="0f164-188">Name</span></span></th><th><span data-ttu-id="0f164-189">Значение</span><span class="sxs-lookup"><span data-stu-id="0f164-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="0f164-190">Фильтр года</span><span class="sxs-lookup"><span data-stu-id="0f164-190">Filter Year</span></span></td><td><span data-ttu-id="0f164-191">2013</span><span class="sxs-lookup"><span data-stu-id="0f164-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="0f164-192">Период фильтра</span><span class="sxs-lookup"><span data-stu-id="0f164-192">Filter Period</span></span></td><td><span data-ttu-id="0f164-193">Январь</span><span class="sxs-lookup"><span data-stu-id="0f164-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="0f164-194">Поля</span><span class="sxs-lookup"><span data-stu-id="0f164-194">Fields</span></span></td><td><span data-ttu-id="0f164-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (очистите остальные поля)</span><span class="sxs-lookup"><span data-stu-id="0f164-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="0f164-196">
3. Щелкните элемент **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="0f164-196">
3. Click **Download**.</span></span>
<span data-ttu-id="0f164-197">4.</span><span class="sxs-lookup"><span data-stu-id="0f164-197">4.</span></span> <span data-ttu-id="0f164-198">Распакуйте файл toohello hello **C:\Tutorials\FlightDelay\2013Data** папки.</span><span class="sxs-lookup"><span data-stu-id="0f164-198">Unzip hello file toohello **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="0f164-199">Каждый файл представляет собой CSV-файл и имеет размер около 60 ГБ.</span><span class="sxs-lookup"><span data-stu-id="0f164-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="0f164-200">5.</span><span class="sxs-lookup"><span data-stu-id="0f164-200">5.</span></span> <span data-ttu-id="0f164-201">Изменение имени toohello файла hello hello месяца с данными для.</span><span class="sxs-lookup"><span data-stu-id="0f164-201">Rename hello file toohello name of hello month that it contains data for.</span></span> <span data-ttu-id="0f164-202">Например, будет называться hello файл, содержащий данные за январь hello *January.csv*.</span><span class="sxs-lookup"><span data-stu-id="0f164-202">For example, hello file containing hello January data would be named *January.csv*.</span></span>
<span data-ttu-id="0f164-203">6.</span><span class="sxs-lookup"><span data-stu-id="0f164-203">6.</span></span> <span data-ttu-id="0f164-204">Повторите шаги 2 и 5 toodownload файл для каждого из hello 12 месяцев в 2013.</span><span class="sxs-lookup"><span data-stu-id="0f164-204">Repeat steps 2 and 5 toodownload a file for each of hello 12 months in 2013.</span></span> <span data-ttu-id="0f164-205">Вам потребуется как минимум один файл toorun hello учебника.</span><span class="sxs-lookup"><span data-stu-id="0f164-205">You will need a minimum of one file toorun hello tutorial.</span></span>

<span data-ttu-id="0f164-206">**tooAzure tooupload hello рейса задержка данных хранилища больших двоичных объектов**</span><span class="sxs-lookup"><span data-stu-id="0f164-206">**tooupload hello flight delay data tooAzure Blob storage**</span></span>

1. <span data-ttu-id="0f164-207">Подготовка параметров hello:</span><span class="sxs-lookup"><span data-stu-id="0f164-207">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="0f164-208">Имя переменной</span><span class="sxs-lookup"><span data-stu-id="0f164-208">Variable Name</span></span></th><th><span data-ttu-id="0f164-209">Примечания</span><span class="sxs-lookup"><span data-stu-id="0f164-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="0f164-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="0f164-210">$storageAccountName</span></span></td><td><span data-ttu-id="0f164-211">Здравствуйте, где вы хотите tooupload hello данные учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-211">hello Azure Storage account where you want tooupload hello data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="0f164-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="0f164-212">$blobContainerName</span></span></td><td><span data-ttu-id="0f164-213">Здравствуйте, контейнер больших двоичных объектов, где вы хотите tooupload hello данные.</span><span class="sxs-lookup"><span data-stu-id="0f164-213">hello Blob container where you want tooupload hello data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="0f164-214">Откройте интегрированную среду сценариев Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f164-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="0f164-215">3.</span><span class="sxs-lookup"><span data-stu-id="0f164-215">3.</span></span> <span data-ttu-id="0f164-216">Вставьте следующий сценарий в области сценариев hello hello:</span><span class="sxs-lookup"><span data-stu-id="0f164-216">Paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="0f164-217">Нажмите клавишу **F5** toorun hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="0f164-217">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="0f164-218">При выборе другого метода для передачи файлов hello toouse убедитесь, что путь к файлу hello учебники, данных или flightdelay.</span><span class="sxs-lookup"><span data-stu-id="0f164-218">If you choose toouse a different method for uploading hello files, please make sure hello file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="0f164-219">Hello для доступа к файлам hello используется синтаксис:</span><span class="sxs-lookup"><span data-stu-id="0f164-219">hello syntax for accessing hello files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="0f164-220">путь Hello учебники/flightdelay/данные — hello виртуальная папка, созданный при отправке файлов hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-220">hello path tutorials/flightdelay/data is hello virtual folder you created when you uploaded hello files.</span></span> <span data-ttu-id="0f164-221">Убедитесь, что присутствует 12 файлов — по одному для каждого месяца.</span><span class="sxs-lookup"><span data-stu-id="0f164-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="0f164-222">Необходимо обновить tooread запроса Hive hello в новом расположении hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-222">You must update hello Hive query tooread from hello new location.</span></span>
>
> <span data-ttu-id="0f164-223">Необходимо настроить hello контейнера доступа разрешение toobe public или привязать toohello учетной записи хранилища hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f164-223">You must either configure hello container access permission toobe public or bind hello Storage account toohello HDInsight cluster.</span></span> <span data-ttu-id="0f164-224">В противном случае строка запроса Hive hello не будут файлы данных могут tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-224">Otherwise, hello Hive query string will not be able tooaccess hello data files.</span></span>

- - -

## <span data-ttu-id="0f164-225"><a id="appendix-b"></a>Приложение Б. Создание и загрузка скрипта HiveQL</span><span class="sxs-lookup"><span data-stu-id="0f164-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="0f164-226">С помощью Azure PowerShell, можно выполнения нескольких инструкций HiveQL один во время или пакет hello HiveQL инструкции в файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="0f164-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="0f164-227">В этом разделе показано, как toocreate сценарий HiveQL и передачи hello скрипт tooAzure хранилища больших двоичных объектов с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f164-227">This section shows you how toocreate a HiveQL script and upload hello script tooAzure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="0f164-228">Куст требует toobe сценариев HiveQL hello, хранящиеся в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-228">Hive requires hello HiveQL scripts toobe stored in Azure Blob storage.</span></span>

<span data-ttu-id="0f164-229">сценарий HiveQL Hello выполнит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="0f164-229">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="0f164-230">**Удалить таблицу delays_raw hello**, в случае, если таблица hello уже существует.</span><span class="sxs-lookup"><span data-stu-id="0f164-230">**Drop hello delays_raw table**, in case hello table already exists.</span></span>
2. <span data-ttu-id="0f164-231">**Создайте внешнюю таблицу Hive hello delays_raw** указывает место хранения большого двоичного объекта toohello с файлами задержки рейсов hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-231">**Create hello delays_raw external Hive table** pointing toohello Blob storage location with hello flight delay files.</span></span> <span data-ttu-id="0f164-232">Этот запрос задает то, что поля разделяются с помощью "," и что строки завершаются с помощью "\n".</span><span class="sxs-lookup"><span data-stu-id="0f164-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="0f164-233">Это создает проблему, если значения полей содержать запятые, так как Hive не различает запятую, которая является разделителем полей и один, который является частью значения поля (бывает hello в значения полей для источника\_Город\_имя и DEST\_ Город\_имя).</span><span class="sxs-lookup"><span data-stu-id="0f164-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is hello case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="0f164-234">tooaddress hello, этот запрос создает столбцы TEMP toohold данных, который неправильно разбит на столбцы.</span><span class="sxs-lookup"><span data-stu-id="0f164-234">tooaddress this, hello query creates TEMP columns toohold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="0f164-235">**Удалить таблицу задержки hello**, в случае, если таблица hello уже существует.</span><span class="sxs-lookup"><span data-stu-id="0f164-235">**Drop hello delays table**, in case hello table already exists.</span></span>
4. <span data-ttu-id="0f164-236">**Создание таблицы задержек hello**.</span><span class="sxs-lookup"><span data-stu-id="0f164-236">**Create hello delays table**.</span></span> <span data-ttu-id="0f164-237">Это полезно tooclean hello данные перед дальнейшей обработкой.</span><span class="sxs-lookup"><span data-stu-id="0f164-237">It is helpful tooclean up hello data before further processing.</span></span> <span data-ttu-id="0f164-238">Этот запрос создает новую таблицу, *задержки*, из таблицы delays_raw hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-238">This query creates a new table, *delays*, from hello delays_raw table.</span></span> <span data-ttu-id="0f164-239">Примечание hello TEMP столбцов (как было упомянуто ранее), не копируются и что hello **подстроки** функция является используется tooremove кавычки из данных hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-239">Note that hello TEMP columns (as mentioned previously) are not copied, and that hello **substring** function is used tooremove quotation marks from hello data.</span></span>
5. <span data-ttu-id="0f164-240">**Hello среднее погоды задержки и группы hello результаты вычислений по названию города.**</span><span class="sxs-lookup"><span data-stu-id="0f164-240">**Compute hello average weather delay and groups hello results by city name.**</span></span> <span data-ttu-id="0f164-241">Он также будет выводить hello результаты tooBlob хранилища.</span><span class="sxs-lookup"><span data-stu-id="0f164-241">It will also output hello results tooBlob storage.</span></span> <span data-ttu-id="0f164-242">Обратите внимание, этот запрос hello апострофы приведет к удалению из данных hello и исключает строки, где значение hello **weather_delay** имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="0f164-242">Note that hello query will remove apostrophes from hello data and will exclude rows where hello value for **weather_delay** is null.</span></span> <span data-ttu-id="0f164-243">Это необходимо, так как Sqoop, используемый в этом руководстве, не обрабатывает эти значения надлежащим образом по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0f164-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="0f164-244">Полный список команд HiveQL hello см. в разделе [язык описания данных DDL Hive][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="0f164-244">For a full list of hello HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="0f164-245">Каждая команда HiveQL должна завершаться точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="0f164-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="0f164-246">**файл скрипта HiveQL toocreate**</span><span class="sxs-lookup"><span data-stu-id="0f164-246">**toocreate a HiveQL script file**</span></span>

1. <span data-ttu-id="0f164-247">Подготовка параметров hello:</span><span class="sxs-lookup"><span data-stu-id="0f164-247">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="0f164-248">Имя переменной</span><span class="sxs-lookup"><span data-stu-id="0f164-248">Variable Name</span></span></th><th><span data-ttu-id="0f164-249">Примечания</span><span class="sxs-lookup"><span data-stu-id="0f164-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="0f164-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="0f164-250">$storageAccountName</span></span></td><td><span data-ttu-id="0f164-251">Здравствуйте, место сценарий HiveQL hello tooupload для учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-251">hello Azure Storage account where you want tooupload hello HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="0f164-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="0f164-252">$blobContainerName</span></span></td><td><span data-ttu-id="0f164-253">Здравствуйте, место сценарий HiveQL tooupload hello в контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="0f164-253">hello Blob container where you want tooupload hello HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="0f164-254">Откройте интегрированную среду сценариев Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f164-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="0f164-255">3.</span><span class="sxs-lookup"><span data-stu-id="0f164-255">3.</span></span> <span data-ttu-id="0f164-256">Скопируйте и вставьте следующий сценарий в области сценариев hello hello:</span><span class="sxs-lookup"><span data-stu-id="0f164-256">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="0f164-257">Ниже приведены hello переменных, используемых в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-257">Here are hello variables used in hello script:</span></span>

   * <span data-ttu-id="0f164-258">**$hqlLocalFileName** -скрипт hello сохраняет файл сценария HiveQL hello локально перед передачей его tooBlob хранилища.</span><span class="sxs-lookup"><span data-stu-id="0f164-258">**$hqlLocalFileName** - hello script saves hello HiveQL script file locally before uploading it tooBlob storage.</span></span> <span data-ttu-id="0f164-259">Это имя файла hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-259">This is hello file name.</span></span> <span data-ttu-id="0f164-260">значение по умолчанию Hello — <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="0f164-260">hello default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="0f164-261">**$hqlBlobName** -это hello HiveQL имя файла скрипта BLOB-объект используется в hello хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-261">**$hqlBlobName** - This is hello HiveQL script file blob name used in hello Azure Blob storage.</span></span> <span data-ttu-id="0f164-262">значение по умолчанию Hello — tutorials/flightdelay/flightdelays.hql.</span><span class="sxs-lookup"><span data-stu-id="0f164-262">hello default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="0f164-263">Поскольку hello будет записан файл напрямую tooAzure хранилища больших двоичных объектов, не «/» в начале hello hello имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="0f164-263">Because hello file will be written directly tooAzure Blob storage, there is NOT a "/" at hello beginning of hello blob name.</span></span> <span data-ttu-id="0f164-264">Если требуется файл hello tooaccess из хранилища больших двоичных объектов, необходимо будет tooadd «/» в начале имени файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-264">If you want tooaccess hello file from Blob storage, you will need tooadd a "/" at hello beginning of hello file name.</span></span>
   * <span data-ttu-id="0f164-265">**$srcDataFolder** и **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span><span class="sxs-lookup"><span data-stu-id="0f164-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="0f164-266"><a id="appendix-c"></a>Приложение C — Подготовка базы данных Azure SQL для hello Sqoop выходные данные задания</span><span class="sxs-lookup"><span data-stu-id="0f164-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for hello Sqoop job output</span></span>
<span data-ttu-id="0f164-267">**База данных SQL tooprepare hello (слияние с hello Sqoop сценарий)**</span><span class="sxs-lookup"><span data-stu-id="0f164-267">**tooprepare hello SQL database (merge this with hello Sqoop script)**</span></span>

1. <span data-ttu-id="0f164-268">Подготовка параметров hello:</span><span class="sxs-lookup"><span data-stu-id="0f164-268">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="0f164-269">Имя переменной</span><span class="sxs-lookup"><span data-stu-id="0f164-269">Variable Name</span></span></th><th><span data-ttu-id="0f164-270">Примечания</span><span class="sxs-lookup"><span data-stu-id="0f164-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="0f164-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="0f164-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="0f164-272">Имя сервера базы данных Azure SQL hello Hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-272">hello name of hello Azure SQL database server.</span></span> <span data-ttu-id="0f164-273">Введите ничего не toocreate нового сервера.</span><span class="sxs-lookup"><span data-stu-id="0f164-273">Enter nothing toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="0f164-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="0f164-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="0f164-275">Hello имя входа для сервера базы данных Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-275">hello login name for hello Azure SQL database server.</span></span> <span data-ttu-id="0f164-276">Если $sqlDatabaseServerName существующий сервер, hello входа и пароль для входа, используется tooauthenticate с сервером hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-276">If $sqlDatabaseServerName is an existing server, hello login and login password are used tooauthenticate with hello server.</span></span> <span data-ttu-id="0f164-277">В противном случае они не используется toocreate нового сервера.</span><span class="sxs-lookup"><span data-stu-id="0f164-277">Otherwise they are used toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="0f164-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="0f164-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="0f164-279">пароль для входа для сервера базы данных Azure SQL hello Hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-279">hello login password for hello Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="0f164-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="0f164-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="0f164-281">Это значение используется только при создании нового сервера базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="0f164-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="0f164-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="0f164-283">База данных SQL Hello toocreate hello AvgDelays таблицы используется для задание Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-283">hello SQL database used toocreate hello AvgDelays table for hello Sqoop job.</span></span> <span data-ttu-id="0f164-284">Если это значение не задано, то будет создана база данных с именем HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="0f164-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="0f164-285">Имя таблицы Hello hello Sqoop выходные данные задания будет AvgDelays.</span><span class="sxs-lookup"><span data-stu-id="0f164-285">hello table name for hello Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="0f164-286">Откройте интегрированную среду сценариев Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f164-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="0f164-287">3.</span><span class="sxs-lookup"><span data-stu-id="0f164-287">3.</span></span> <span data-ttu-id="0f164-288">Скопируйте и вставьте следующий сценарий в области сценариев hello hello:</span><span class="sxs-lookup"><span data-stu-id="0f164-288">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="0f164-289">Hello скрипт использует службы передачи репрезентативного состояния (REST) передачи, http://bot.whatismyipaddress.com, tooretrieve внешнего IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="0f164-289">hello script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, tooretrieve your external IP address.</span></span> <span data-ttu-id="0f164-290">Hello IP-адрес используется для создания правила брандмауэра для сервера базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="0f164-290">hello IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="0f164-291">Ниже приведены некоторые переменные, используемые в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-291">Here are some variables used in hello script:</span></span>

   * <span data-ttu-id="0f164-292">**$ipAddressRestService** -hello значение по умолчанию — http://bot.whatismyipaddress.com. Это общедоступный IP-адрес службы REST для получения внешнего IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="0f164-292">**$ipAddressRestService** - hello default value is http://bot.whatismyipaddress.com. It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="0f164-293">При необходимости можно использовать и другие службы.</span><span class="sxs-lookup"><span data-stu-id="0f164-293">You can use other services if you want.</span></span> <span data-ttu-id="0f164-294">внешний IP-адрес Hello извлечь с помощью службы hello будет toocreate используется правило брандмауэра для сервера базы данных Azure SQL, можно доступа к базе данных hello с рабочей станции (с помощью сценария Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="0f164-294">hello external IP address retrieved through hello service will be used toocreate a firewall rule for your Azure SQL database server, so that you can access hello database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="0f164-295">**$fireWallRuleName** -это имя hello hello правила брандмауэра для сервера базы данных Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-295">**$fireWallRuleName** - This is hello name of hello firewall rule for hello Azure SQL database server.</span></span> <span data-ttu-id="0f164-296">имя по умолчанию Hello — <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="0f164-296">hello default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="0f164-297">При необходимости можно использовать другое имя.</span><span class="sxs-lookup"><span data-stu-id="0f164-297">You can rename it if you want.</span></span>
   * <span data-ttu-id="0f164-298">**$sqlDatabaseMaxSizeGB** — это значение используется только при создании нового сервера базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-298">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="0f164-299">значение по умолчанию Hello составляет 10 ГБ.</span><span class="sxs-lookup"><span data-stu-id="0f164-299">hello default value is 10GB.</span></span> <span data-ttu-id="0f164-300">Размера 10ГБ достаточно для примеров из данного учебника.</span><span class="sxs-lookup"><span data-stu-id="0f164-300">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="0f164-301">**$sqlDatabaseName** — это значение используется только при создании новой базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0f164-301">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="0f164-302">значение по умолчанию Hello — HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="0f164-302">hello default value is HDISqoop.</span></span> <span data-ttu-id="0f164-303">Если переименовать, необходимо соответствующим образом обновить сценарий Sqoop Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-303">If you rename it, you must update hello Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="0f164-304">Нажмите клавишу **F5** toorun hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="0f164-304">Press **F5** toorun hello script.</span></span>
5. <span data-ttu-id="0f164-305">Проверьте выходные данные сценария hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-305">Validate hello script output.</span></span> <span data-ttu-id="0f164-306">Убедитесь, что скрипт hello выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="0f164-306">Make sure hello script ran successfully.</span></span>

## <span data-ttu-id="0f164-307"><a id="nextsteps"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f164-307"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="0f164-308">Теперь вы понимаете как tooupload tooAzure файл хранилища больших двоичных объектов, как таблицы toopopulate куст, используя hello данные из хранилища больших двоичных объектов Azure, как toorun Hive запросы и как toouse Sqoop tooexport данные из базы данных Azure SQL tooan HDFS.</span><span class="sxs-lookup"><span data-stu-id="0f164-308">Now you understand how tooupload a file tooAzure Blob storage, how toopopulate a Hive table by using hello data from Azure Blob storage, how toorun Hive queries, and how toouse Sqoop tooexport data from HDFS tooan Azure SQL database.</span></span> <span data-ttu-id="0f164-309">toolearn более, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="0f164-309">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="0f164-310">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0f164-310">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="0f164-311">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="0f164-311">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="0f164-312">[Использование Oozie с HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="0f164-312">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="0f164-313">[Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="0f164-313">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="0f164-314">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="0f164-314">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="0f164-315">[Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="0f164-315">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
