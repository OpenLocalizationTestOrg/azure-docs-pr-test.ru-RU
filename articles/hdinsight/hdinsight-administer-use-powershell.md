---
title: "Управление кластерами Hadoop в HDInsight с помощью PowerShell — Azure | Документы Майкрософт"
description: "Узнайте, как осуществлять управление кластерами Hadoop в HDInsight с использованием Azure PowerShell."
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
ms.openlocfilehash: c47dabd7c4aa4ba0be08c419989e536711f03677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="1239d-103">Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1239d-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="1239d-104">Azure PowerShell — это полнофункциональная среда сценариев, которую можно использовать для контроля и автоматизации развертывания и управления вашей рабочей нагрузкой в Azure.</span><span class="sxs-lookup"><span data-stu-id="1239d-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="1239d-105">В этой статье вы узнаете, как управлять кластерами Hadoop в Azure HDInsight с помощью локальной консоли Azure PowerShell, используя Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1239d-105">In this article, you will learn how to manage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through the use of Windows PowerShell.</span></span> <span data-ttu-id="1239d-106">Список командлетов HDInsight PowerShell см. в [справочнике по командлетам HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="1239d-106">For the list of the HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="1239d-107">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="1239d-107">**Prerequisites**</span></span>

<span data-ttu-id="1239d-108">Перед началом работы с этой статьей необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="1239d-108">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="1239d-109">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="1239d-109">**An Azure subscription**.</span></span> <span data-ttu-id="1239d-110">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1239d-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="1239d-111">Установка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1239d-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="1239d-112">Если вы установили Azure PowerShell версии 0.9x, то перед установкой новой версии ее необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="1239d-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="1239d-113">Проверка версии установленной оболочки PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1239d-113">To check the version of the installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="1239d-114">Для удаления старой версии запустите "Программы и компоненты" в панели управления.</span><span class="sxs-lookup"><span data-stu-id="1239d-114">To uninstall the older version, run Programs and Features in the control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="1239d-115">Создание кластеров</span><span class="sxs-lookup"><span data-stu-id="1239d-115">Create clusters</span></span>
<span data-ttu-id="1239d-116">Ознакомьтесь с разделом [Создание кластеров под управлением Linux в HDInsight с помощью Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="1239d-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="1239d-117">Получение списка кластеров</span><span class="sxs-lookup"><span data-stu-id="1239d-117">List clusters</span></span>
<span data-ttu-id="1239d-118">Чтобы получить список всех кластеров в текущей подписке, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1239d-118">Use the following command to list all clusters in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="1239d-119">Отображение кластеров</span><span class="sxs-lookup"><span data-stu-id="1239d-119">Show cluster</span></span>
<span data-ttu-id="1239d-120">Чтобы отобразить сведения о конкретном кластере в текущей подписке, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1239d-120">Use the following command to show details of a specific cluster in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="1239d-121">Удаление кластеров</span><span class="sxs-lookup"><span data-stu-id="1239d-121">Delete clusters</span></span>
<span data-ttu-id="1239d-122">Используйте следующую команду для удаления кластера:</span><span class="sxs-lookup"><span data-stu-id="1239d-122">Use the following command to delete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="1239d-123">Можно также удалить кластер, удалив группу ресурсов, которая содержит этот кластер.</span><span class="sxs-lookup"><span data-stu-id="1239d-123">You can also delete a cluster by removing the resource group that contains the cluster.</span></span> <span data-ttu-id="1239d-124">Обратите внимание, это приведет к удалению всех ресурсов в группе, включая учетную запись хранения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1239d-124">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="1239d-125">Масштабирование кластеров</span><span class="sxs-lookup"><span data-stu-id="1239d-125">Scale clusters</span></span>
<span data-ttu-id="1239d-126">Масштабирование кластера позволяет изменить количество рабочих узлов в кластере, который работает под управлением Azure HDInsight. При этом не требуется повторно создавать кластер.</span><span class="sxs-lookup"><span data-stu-id="1239d-126">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="1239d-127">Поддерживаются только кластеры HDInsight версии 3.1.3 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="1239d-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="1239d-128">Если вы не знаете версию кластера, см. страницу «Свойства».</span><span class="sxs-lookup"><span data-stu-id="1239d-128">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="1239d-129">См. раздел [Отображение кластеров](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="1239d-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="1239d-130">Ниже представлены возможности, связанные с изменением количества узлов данных в кластере каждого типа, поддерживаемого в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1239d-130">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="1239d-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="1239d-131">Hadoop</span></span>

    <span data-ttu-id="1239d-132">Вы можете легко увеличить количество рабочих узлов в работающем кластере Hadoop. Это не помешает обработке заданий в состоянии ожидания и выполнения.</span><span class="sxs-lookup"><span data-stu-id="1239d-132">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="1239d-133">В ходе выполнения операции можно также отправлять новые задания.</span><span class="sxs-lookup"><span data-stu-id="1239d-133">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="1239d-134">Сбои операции масштабирования обрабатываются корректно, поэтому кластер всегда пребывает в функциональном состоянии.</span><span class="sxs-lookup"><span data-stu-id="1239d-134">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="1239d-135">Если уменьшить масштаб кластера Hadoop, сократив количество узлов данных, некоторые службы в нем будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="1239d-135">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="1239d-136">Это приведет к сбою всех выполняющихся и ожидающих заданий при завершении операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="1239d-136">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="1239d-137">Однако после завершения операции вы можете повторно отправить задания.</span><span class="sxs-lookup"><span data-stu-id="1239d-137">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="1239d-138">HBase</span><span class="sxs-lookup"><span data-stu-id="1239d-138">HBase</span></span>

    <span data-ttu-id="1239d-139">Вы можете с легкостью добавлять и удалять узлы данных в работающем кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="1239d-139">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="1239d-140">Балансировка региональных серверов выполняется автоматически в течение нескольких минут после завершения операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="1239d-140">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="1239d-141">Но их также можно сбалансировать вручную, выполнив вход в головной узел кластера и выполнив следующие команды в окне командной строки:</span><span class="sxs-lookup"><span data-stu-id="1239d-141">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="1239d-142">Storm</span><span class="sxs-lookup"><span data-stu-id="1239d-142">Storm</span></span>

    <span data-ttu-id="1239d-143">Вы можете с легкостью добавлять и удалять узлы данных в работающем кластере Storm.</span><span class="sxs-lookup"><span data-stu-id="1239d-143">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="1239d-144">Но после успешного завершения операции масштабирования потребуется повторная балансировка топологии.</span><span class="sxs-lookup"><span data-stu-id="1239d-144">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="1239d-145">Повторную балансировку можно выполнить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="1239d-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="1239d-146">с помощью веб-интерфейса Storm;</span><span class="sxs-lookup"><span data-stu-id="1239d-146">Storm web UI</span></span>
  * <span data-ttu-id="1239d-147">с помощью программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="1239d-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="1239d-148">Дополнительные сведения см. в [документации по Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="1239d-148">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="1239d-149">В кластере HDInsight доступен веб-интерфейс Storm.</span><span class="sxs-lookup"><span data-stu-id="1239d-149">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight, storm, масштабирование, перераспределение](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="1239d-151">Ниже приведен пример использования команды CLI для повторной балансировки топологии Storm:</span><span class="sxs-lookup"><span data-stu-id="1239d-151">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="1239d-152">Чтобы изменить размер кластера Hadoop с помощью Azure PowerShell, выполните следующую команду с клиентского компьютера:</span><span class="sxs-lookup"><span data-stu-id="1239d-152">To change the Hadoop cluster size by using Azure PowerShell, run the following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="1239d-153">Предоставление и отмена доступа</span><span class="sxs-lookup"><span data-stu-id="1239d-153">Grant/revoke access</span></span>
<span data-ttu-id="1239d-154">В кластерах HDInsight имеются следующие веб-службы HTTP (все эти службы имеют конечные точки RESTful):</span><span class="sxs-lookup"><span data-stu-id="1239d-154">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="1239d-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="1239d-155">ODBC</span></span>
* <span data-ttu-id="1239d-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="1239d-156">JDBC</span></span>
* <span data-ttu-id="1239d-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="1239d-157">Ambari</span></span>
* <span data-ttu-id="1239d-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="1239d-158">Oozie</span></span>
* <span data-ttu-id="1239d-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="1239d-159">Templeton</span></span>

<span data-ttu-id="1239d-160">По умолчанию эти службы предоставляются для доступа.</span><span class="sxs-lookup"><span data-stu-id="1239d-160">By default, these services are granted for access.</span></span> <span data-ttu-id="1239d-161">Вы можете отменить или предоставить доступ.</span><span class="sxs-lookup"><span data-stu-id="1239d-161">You can revoke/grant the access.</span></span> <span data-ttu-id="1239d-162">Для отмены:</span><span class="sxs-lookup"><span data-stu-id="1239d-162">To revoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="1239d-163">Для предоставления:</span><span class="sxs-lookup"><span data-stu-id="1239d-163">To grant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter the Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter the HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="1239d-164">Предоставляя или отменяя доступ, вы сбрасываете имя пользователя и пароль кластера.</span><span class="sxs-lookup"><span data-stu-id="1239d-164">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="1239d-165">Это также можно сделать через портал.</span><span class="sxs-lookup"><span data-stu-id="1239d-165">This can also be done via the Portal.</span></span> <span data-ttu-id="1239d-166">Ознакомьтесь с разделом [Администрирование HDInsight с помощью портала Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="1239d-166">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="1239d-167">Обновление учетных данных пользователя HTTP</span><span class="sxs-lookup"><span data-stu-id="1239d-167">Update HTTP user credentials</span></span>
<span data-ttu-id="1239d-168">Эта процедура аналогична [предоставлению или запрету доступа HTTP](#grant/revoke-access). Если кластеру был предоставлен доступ по протоколу HTTP, необходимо сначала отменить его.</span><span class="sxs-lookup"><span data-stu-id="1239d-168">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="1239d-169">После этого предоставьте доступ с новыми учетными данными пользователя HTTP.</span><span class="sxs-lookup"><span data-stu-id="1239d-169">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="1239d-170">Поиск учетной записи хранения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1239d-170">Find the default storage account</span></span>
<span data-ttu-id="1239d-171">В следующем сценарии Powershell показано получение имени учетной записи хранения по умолчанию и ключа учетной записи хранения по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="1239d-171">The following Powershell script demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-the-resource-group"></a><span data-ttu-id="1239d-172">Поиск группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="1239d-172">Find the resource group</span></span>
<span data-ttu-id="1239d-173">В режиме Resource Manager каждый кластер HDInsight относится к группе ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="1239d-173">In the Resource Manager mode, each HDInsight cluster belongs to an Azure resource group.</span></span>  <span data-ttu-id="1239d-174">Поиск группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="1239d-174">To find the resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="1239d-175">Отправка заданий</span><span class="sxs-lookup"><span data-stu-id="1239d-175">Submit jobs</span></span>
<span data-ttu-id="1239d-176">**Отправка заданий MapReduce**</span><span class="sxs-lookup"><span data-stu-id="1239d-176">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="1239d-177">См. статью [Выполнение примеров Hadoop MapReduce в HDInsight на базе Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1239d-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="1239d-178">**Отправка заданий Hive**</span><span class="sxs-lookup"><span data-stu-id="1239d-178">**To submit Hive jobs**</span></span>

<span data-ttu-id="1239d-179">См. статью [Выполнение запросов Hive с помощью PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1239d-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="1239d-180">**Отправка заданий Pig**</span><span class="sxs-lookup"><span data-stu-id="1239d-180">**To submit Pig jobs**</span></span>

<span data-ttu-id="1239d-181">См. статью [Выполнение заданий Pig с помощью PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1239d-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="1239d-182">**Отправка заданий Sqoop**</span><span class="sxs-lookup"><span data-stu-id="1239d-182">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="1239d-183">См. статью [Использование Sqoop с Hadoop в HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="1239d-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="1239d-184">**Отправка заданий Oozie**</span><span class="sxs-lookup"><span data-stu-id="1239d-184">**To submit Oozie jobs**</span></span>

<span data-ttu-id="1239d-185">См. статью [Использование Oozie с Hadoop для определения и выполнения рабочего процесса в HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="1239d-185">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="1239d-186">Отправка данных в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="1239d-186">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="1239d-187">Ознакомьтесь со статьей [Отправка данных в HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="1239d-187">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="1239d-188">См. также</span><span class="sxs-lookup"><span data-stu-id="1239d-188">See Also</span></span>
* <span data-ttu-id="1239d-189">[Справочная документация по командлетам HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="1239d-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="1239d-190">[Администрирование HDInsight с помощью портала Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="1239d-190">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="1239d-191">[Администрирование HDInsight с помощью интерфейса командной строки][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="1239d-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="1239d-192">[Создание кластеров Hadoop в HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="1239d-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="1239d-193">[Отправка данных в HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="1239d-193">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="1239d-194">[Отправка заданий Hadoop в HDInsight][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="1239d-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="1239d-195">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="1239d-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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
