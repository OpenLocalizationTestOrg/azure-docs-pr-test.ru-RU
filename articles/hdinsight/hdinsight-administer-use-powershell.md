---
title: "кластеры aaaManage Hadoop в HDInsight с помощью PowerShell, Azure | Документы Microsoft"
description: "Узнайте, как tooperform административные задачи для hello кластеров Hadoop в HDInsight с помощью Azure PowerShell."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="afef0-103">Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="afef0-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="afef0-104">Azure PowerShell — это мощная среда сценариев, можно использовать toocontrol и автоматизации развертывания hello и управления ими рабочих нагрузок в Azure.</span><span class="sxs-lookup"><span data-stu-id="afef0-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="afef0-105">В этой статье вы узнаете, как использовать toomanage кластеров Hadoop в Azure HDInsight с помощью локальной консоли Azure PowerShell через hello оболочки Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afef0-105">In this article, you will learn how toomanage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through hello use of Windows PowerShell.</span></span> <span data-ttu-id="afef0-106">Список hello hello командлеты HDInsight PowerShell см. в разделе [Справочник по командлетам HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="afef0-106">For hello list of hello HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="afef0-107">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="afef0-107">**Prerequisites**</span></span>

<span data-ttu-id="afef0-108">Прежде чем приступать к этой статье, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="afef0-108">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="afef0-109">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="afef0-109">**An Azure subscription**.</span></span> <span data-ttu-id="afef0-110">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="afef0-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="afef0-111">Установка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="afef0-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="afef0-112">Если вы установили Azure PowerShell версии 0.9x, то перед установкой новой версии ее необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="afef0-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="afef0-113">toocheck hello hello версии PowerShell:</span><span class="sxs-lookup"><span data-stu-id="afef0-113">toocheck hello version of hello installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="afef0-114">старая версия hello toouninstall, запустить программы и компоненты панели управления hello.</span><span class="sxs-lookup"><span data-stu-id="afef0-114">toouninstall hello older version, run Programs and Features in hello control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="afef0-115">Создание кластеров</span><span class="sxs-lookup"><span data-stu-id="afef0-115">Create clusters</span></span>
<span data-ttu-id="afef0-116">Ознакомьтесь с разделом [Создание кластеров под управлением Linux в HDInsight с помощью Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="afef0-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="afef0-117">Получение списка кластеров</span><span class="sxs-lookup"><span data-stu-id="afef0-117">List clusters</span></span>
<span data-ttu-id="afef0-118">Используйте следующие команды toolist hello всех кластеров в текущей подписке hello:</span><span class="sxs-lookup"><span data-stu-id="afef0-118">Use hello following command toolist all clusters in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="afef0-119">Отображение кластеров</span><span class="sxs-lookup"><span data-stu-id="afef0-119">Show cluster</span></span>
<span data-ttu-id="afef0-120">Используйте приведенные ниже сведения tooshow команду к конкретному кластеру в текущей подписке hello hello.</span><span class="sxs-lookup"><span data-stu-id="afef0-120">Use hello following command tooshow details of a specific cluster in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="afef0-121">Удаление кластеров</span><span class="sxs-lookup"><span data-stu-id="afef0-121">Delete clusters</span></span>
<span data-ttu-id="afef0-122">Используйте следующие команды toodelete кластера hello:</span><span class="sxs-lookup"><span data-stu-id="afef0-122">Use hello following command toodelete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="afef0-123">Можно также удалить кластер, удалив hello группы ресурсов, содержащий hello кластера.</span><span class="sxs-lookup"><span data-stu-id="afef0-123">You can also delete a cluster by removing hello resource group that contains hello cluster.</span></span> <span data-ttu-id="afef0-124">Обратите внимание, это приведет к удалению всех ресурсов группы hello, включая учетную запись хранения по умолчанию hello hello.</span><span class="sxs-lookup"><span data-stu-id="afef0-124">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="afef0-125">Масштабирование кластеров</span><span class="sxs-lookup"><span data-stu-id="afef0-125">Scale clusters</span></span>
<span data-ttu-id="afef0-126">масштабирование функции кластера Hello позволяет toochange hello число рабочих узлов в кластере, который выполняется в Azure HDInsight без необходимости toore-создать кластер hello.</span><span class="sxs-lookup"><span data-stu-id="afef0-126">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="afef0-127">Поддерживаются только кластеры HDInsight версии 3.1.3 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="afef0-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="afef0-128">Если вы не знаете hello версии кластера, можно проверить свойства страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="afef0-128">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="afef0-129">См. раздел [Отображение кластеров](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="afef0-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="afef0-130">Hello последствия изменения hello количество узлов данных для каждого типа поддерживаемых HDInsight кластера:</span><span class="sxs-lookup"><span data-stu-id="afef0-130">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="afef0-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="afef0-131">Hadoop</span></span>

    <span data-ttu-id="afef0-132">Можно легко увеличить hello число рабочих узлов в кластере Hadoop, на котором выполняется без ущерба для все ожидающие или выполняемые задания.</span><span class="sxs-lookup"><span data-stu-id="afef0-132">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="afef0-133">Также можно отправлять новые задания, hello операции во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="afef0-133">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="afef0-134">Ошибки в операции масштабирования обрабатываются правильно, чтобы hello кластер всегда оставался в рабочем состоянии.</span><span class="sxs-lookup"><span data-stu-id="afef0-134">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="afef0-135">Когда кластер Hadoop уменьшено за счет уменьшения hello количество узлов данных, некоторые службы hello в кластере hello перезапускаются.</span><span class="sxs-lookup"><span data-stu-id="afef0-135">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="afef0-136">В результате все выполняющиеся и ожидающие задания toofail окончании hello hello операцию масштабирования.</span><span class="sxs-lookup"><span data-stu-id="afef0-136">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="afef0-137">Можно Однако повторно отправить задания hello после завершения операции hello.</span><span class="sxs-lookup"><span data-stu-id="afef0-137">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="afef0-138">HBase</span><span class="sxs-lookup"><span data-stu-id="afef0-138">HBase</span></span>

    <span data-ttu-id="afef0-139">Можно легко добавить или удалить узлы tooyour HBase кластера при выполнении.</span><span class="sxs-lookup"><span data-stu-id="afef0-139">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="afef0-140">Региональные серверы распределяются автоматически через несколько минут после завершения hello операция масштабирования.</span><span class="sxs-lookup"><span data-stu-id="afef0-140">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="afef0-141">Тем не менее можно также вручную сбалансировать региональные серверы hello войдите в систему в toohello головному узлу кластера, и выполнение hello, следующие команды из окна командной строки:</span><span class="sxs-lookup"><span data-stu-id="afef0-141">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="afef0-142">Storm</span><span class="sxs-lookup"><span data-stu-id="afef0-142">Storm</span></span>

    <span data-ttu-id="afef0-143">Можно легко добавить или удалить кластер Storm tooyour узлы данных при выполнении.</span><span class="sxs-lookup"><span data-stu-id="afef0-143">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="afef0-144">Однако после успешного завершения hello операция масштабирования потребуется toorebalance hello топологии.</span><span class="sxs-lookup"><span data-stu-id="afef0-144">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="afef0-145">Повторную балансировку можно выполнить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="afef0-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="afef0-146">с помощью веб-интерфейса Storm;</span><span class="sxs-lookup"><span data-stu-id="afef0-146">Storm web UI</span></span>
  * <span data-ttu-id="afef0-147">с помощью программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="afef0-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="afef0-148">См. toohello [документации Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="afef0-148">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="afef0-149">в кластере HDInsight hello доступен Hello Storm пользовательского веб-интерфейса:</span><span class="sxs-lookup"><span data-stu-id="afef0-149">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![HDInsight, storm, масштабирование, перераспределение](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="afef0-151">Ниже приведен пример как toouse hello CLI команды toorebalance hello Storm топологии:</span><span class="sxs-lookup"><span data-stu-id="afef0-151">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="afef0-152">hello toochange размер кластера Hadoop с помощью Azure PowerShell, запустите следующую команду с клиентского компьютера hello:</span><span class="sxs-lookup"><span data-stu-id="afef0-152">toochange hello Hadoop cluster size by using Azure PowerShell, run hello following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="afef0-153">Предоставление и отмена доступа</span><span class="sxs-lookup"><span data-stu-id="afef0-153">Grant/revoke access</span></span>
<span data-ttu-id="afef0-154">Кластеры HDInsight имеют hello следующие веб-службы HTTP (все эти службы имеют RESTful конечные точки):</span><span class="sxs-lookup"><span data-stu-id="afef0-154">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="afef0-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="afef0-155">ODBC</span></span>
* <span data-ttu-id="afef0-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="afef0-156">JDBC</span></span>
* <span data-ttu-id="afef0-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="afef0-157">Ambari</span></span>
* <span data-ttu-id="afef0-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="afef0-158">Oozie</span></span>
* <span data-ttu-id="afef0-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="afef0-159">Templeton</span></span>

<span data-ttu-id="afef0-160">По умолчанию эти службы предоставляются для доступа.</span><span class="sxs-lookup"><span data-stu-id="afef0-160">By default, these services are granted for access.</span></span> <span data-ttu-id="afef0-161">Вы можете revoke или предоставления доступа hello.</span><span class="sxs-lookup"><span data-stu-id="afef0-161">You can revoke/grant hello access.</span></span> <span data-ttu-id="afef0-162">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="afef0-162">toorevoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="afef0-163">toogrant:</span><span class="sxs-lookup"><span data-stu-id="afef0-163">toogrant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="afef0-164">Предоставление или Отмена доступа hello, восстановится hello кластера имя и пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="afef0-164">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="afef0-165">Это можно сделать через портал hello.</span><span class="sxs-lookup"><span data-stu-id="afef0-165">This can also be done via hello Portal.</span></span> <span data-ttu-id="afef0-166">В разделе [Здравствуйте, администрировать HDInsight с помощью портала Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="afef0-166">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="afef0-167">Обновление учетных данных пользователя HTTP</span><span class="sxs-lookup"><span data-stu-id="afef0-167">Update HTTP user credentials</span></span>
<span data-ttu-id="afef0-168">Это же hello процедуры как [доступа для предоставления или отзыва HTTP](#grant/revoke-access). Если кластер hello было предоставлено hello доступа по протоколу HTTP, то необходимо отозвать.</span><span class="sxs-lookup"><span data-stu-id="afef0-168">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="afef0-169">А затем предоставить доступ hello с новыми учетными данными пользователя HTTP.</span><span class="sxs-lookup"><span data-stu-id="afef0-169">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="afef0-170">Найти учетную запись хранения по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="afef0-170">Find hello default storage account</span></span>
<span data-ttu-id="afef0-171">Следующий сценарий Powershell Hello демонстрируется tooget hello имя учетной записи хранения по умолчанию и hello ключ учетной записи хранения по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="afef0-171">hello following Powershell script demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a><span data-ttu-id="afef0-172">Найти группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="afef0-172">Find hello resource group</span></span>
<span data-ttu-id="afef0-173">В режиме hello диспетчера ресурсов каждый кластер HDInsight принадлежит tooan группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="afef0-173">In hello Resource Manager mode, each HDInsight cluster belongs tooan Azure resource group.</span></span>  <span data-ttu-id="afef0-174">Группа ресурсов hello toofind:</span><span class="sxs-lookup"><span data-stu-id="afef0-174">toofind hello resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="afef0-175">Отправка заданий</span><span class="sxs-lookup"><span data-stu-id="afef0-175">Submit jobs</span></span>
<span data-ttu-id="afef0-176">**задания MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="afef0-176">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="afef0-177">См. статью [Выполнение примеров Hadoop MapReduce в HDInsight на базе Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="afef0-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="afef0-178">**задания Hive toosubmit**</span><span class="sxs-lookup"><span data-stu-id="afef0-178">**toosubmit Hive jobs**</span></span>

<span data-ttu-id="afef0-179">См. статью [Выполнение запросов Hive с помощью PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="afef0-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="afef0-180">**задания Pig toosubmit**</span><span class="sxs-lookup"><span data-stu-id="afef0-180">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="afef0-181">См. статью [Выполнение заданий Pig с помощью PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="afef0-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="afef0-182">**toosubmit Sqoop заданий**</span><span class="sxs-lookup"><span data-stu-id="afef0-182">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="afef0-183">См. статью [Использование Sqoop с Hadoop в HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="afef0-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="afef0-184">**toosubmit Oozie заданий**</span><span class="sxs-lookup"><span data-stu-id="afef0-184">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="afef0-185">В разделе [Oozie использования с Hadoop toodefine и выполнения рабочего процесса в HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="afef0-185">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="afef0-186">Отправка больших двоичных объектов хранилища данных tooAzure</span><span class="sxs-lookup"><span data-stu-id="afef0-186">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="afef0-187">В разделе [отправить данные tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="afef0-187">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="afef0-188">См. также</span><span class="sxs-lookup"><span data-stu-id="afef0-188">See Also</span></span>
* <span data-ttu-id="afef0-189">[Справочная документация по командлетам HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="afef0-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="afef0-190">[Администрирование с помощью hello портал Azure HDInsight][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="afef0-190">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="afef0-191">[Администрирование HDInsight с помощью интерфейса командной строки][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="afef0-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="afef0-192">[Создание кластеров Hadoop в HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="afef0-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="afef0-193">[Отправка данных tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="afef0-193">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="afef0-194">[Отправка заданий Hadoop в HDInsight][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="afef0-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="afef0-195">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="afef0-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
