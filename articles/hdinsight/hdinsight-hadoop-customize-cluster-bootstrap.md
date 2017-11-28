---
title: "aaaCustomize кластерами HDInsight с помощью начальной загрузки — Azure | Документы Microsoft"
description: "Узнайте, как toocustomize HDInsight кластеры, использующие начальной загрузки."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ab2ebf0c-e961-4e95-8151-9724ee22d769
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0029680fd1aa0e9e6aa9cdf667256c31b7ddc565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="8c1ef-103">Настройка кластеров HDInsight с помощью начальной загрузки</span><span class="sxs-lookup"><span data-stu-id="8c1ef-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="8c1ef-104">В некоторых случаях требуется, чтобы файлы конфигурации tooconfigure hello, которые включают:</span><span class="sxs-lookup"><span data-stu-id="8c1ef-104">Sometimes, you want tooconfigure hello configuration files, which include:</span></span>

* <span data-ttu-id="8c1ef-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="8c1ef-106">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-106">core-site.xml</span></span>
* <span data-ttu-id="8c1ef-107">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-107">gateway.xml</span></span>
* <span data-ttu-id="8c1ef-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-108">hbase-env.xml</span></span>
* <span data-ttu-id="8c1ef-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-109">hbase-site.xml</span></span>
* <span data-ttu-id="8c1ef-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-110">hdfs-site.xml</span></span>
* <span data-ttu-id="8c1ef-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-111">hive-env.xml</span></span>
* <span data-ttu-id="8c1ef-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-112">hive-site.xml</span></span>
* <span data-ttu-id="8c1ef-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="8c1ef-113">mapred-site</span></span>
* <span data-ttu-id="8c1ef-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-114">oozie-site.xml</span></span>
* <span data-ttu-id="8c1ef-115">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-115">oozie-env.xml</span></span>
* <span data-ttu-id="8c1ef-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-116">storm-site.xml</span></span>
* <span data-ttu-id="8c1ef-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-117">tez-site.xml</span></span>
* <span data-ttu-id="8c1ef-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-118">webhcat-site.xml</span></span>
* <span data-ttu-id="8c1ef-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="8c1ef-119">yarn-site.xml</span></span>

<span data-ttu-id="8c1ef-120">Существует три toouse методы начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-120">There are three methods toouse bootstrap:</span></span>

* <span data-ttu-id="8c1ef-121">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c1ef-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="8c1ef-122">Использование пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="8c1ef-122">Use .NET SDK</span></span>
* <span data-ttu-id="8c1ef-123">Использование шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8c1ef-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="8c1ef-124">Сведения об установке дополнительных компонентов в кластере HDInsight во время создания hello см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="8c1ef-124">For information on installing additional components on HDInsight cluster during hello creation time, see:</span></span>

* [<span data-ttu-id="8c1ef-125">Настройка кластеров HDInsight с помощью действия скрипта (Linux)</span><span class="sxs-lookup"><span data-stu-id="8c1ef-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="8c1ef-126">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c1ef-126">Use Azure PowerShell</span></span>
<span data-ttu-id="8c1ef-127">Следующий код PowerShell Hello настраивает конфигурации Hive:</span><span class="sxs-lookup"><span data-stu-id="8c1ef-127">hello following PowerShell code customizes a Hive configuration:</span></span>

    # hive-site.xml configuration
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $existingResourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -Config $config 

<span data-ttu-id="8c1ef-128">Полный рабочий сценарий PowerShell можно найти в [Приложении A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="8c1ef-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="8c1ef-129">**Изменение hello tooverify:**</span><span class="sxs-lookup"><span data-stu-id="8c1ef-129">**tooverify hello change:**</span></span>

1. <span data-ttu-id="8c1ef-130">Войдите на toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c1ef-130">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8c1ef-131">Hello в левом меню, щелкните **кластеров HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-131">From hello left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="8c1ef-132">Если вы не видите этот пункт, сначала щелкните **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="8c1ef-133">Щелкните кластер hello, созданный с помощью сценария PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-133">Click hello cluster you just created using hello PowerShell script.</span></span>
4. <span data-ttu-id="8c1ef-134">Нажмите кнопку **мониторинга** hello верхней части колонки tooopen hello hello Ambari пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-134">Click **Dashboard** from hello top of hello blade tooopen hello Ambari UI.</span></span>
5. <span data-ttu-id="8c1ef-135">Нажмите кнопку **Hive** из меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-135">Click **Hive** from hello left menu.</span></span>
6. <span data-ttu-id="8c1ef-136">Щелкните **HiveServer2** в разделе **Сводка**.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="8c1ef-137">Нажмите кнопку hello **Configs** вкладки.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-137">Click hello **Configs** tab.</span></span>
8. <span data-ttu-id="8c1ef-138">Нажмите кнопку **Hive** из меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-138">Click **Hive** from hello left menu.</span></span>
9. <span data-ttu-id="8c1ef-139">Нажмите кнопку hello **Дополнительно** вкладки.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-139">Click hello **Advanced** tab.</span></span>
10. <span data-ttu-id="8c1ef-140">Прокрутите вниз и разверните раздел **Advanced hive-site**(Расширенный сайт Hive).</span><span class="sxs-lookup"><span data-stu-id="8c1ef-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="8c1ef-141">Найдите **hive.metastore.client.socket.timeout** в разделе "hello".</span><span class="sxs-lookup"><span data-stu-id="8c1ef-141">Look for **hive.metastore.client.socket.timeout** in hello section.</span></span>

<span data-ttu-id="8c1ef-142">Вот еще несколько примеров изменения других файлов конфигурации:</span><span class="sxs-lookup"><span data-stu-id="8c1ef-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="8c1ef-143">Дополнительные сведения см. в статье Азима Уддина (Azim Uddin) [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx) (Дополнительная настройка при подготовке кластера HDInsight).</span><span class="sxs-lookup"><span data-stu-id="8c1ef-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="8c1ef-144">Использование пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="8c1ef-144">Use .NET SDK</span></span>
<span data-ttu-id="8c1ef-145">В разделе [под управлением Linux, создание кластеров HDInsight с помощью hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span><span class="sxs-lookup"><span data-stu-id="8c1ef-145">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="8c1ef-146">Использование шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8c1ef-146">Use Resource Manager template</span></span>
<span data-ttu-id="8c1ef-147">В шаблоне Resource Manager можно использовать начальную загрузку:</span><span class="sxs-lookup"><span data-stu-id="8c1ef-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![Настройка шаблона Azure Resource Manager для начальной загрузки кластера с помощью HDInsight Hadoop](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="8c1ef-149">См. также</span><span class="sxs-lookup"><span data-stu-id="8c1ef-149">See also</span></span>
* <span data-ttu-id="8c1ef-150">[Создание кластеров Hadoop в HDInsight] [ hdinsight-provision-cluster] описано, как toocreate HDInsight кластер с помощью другие настраиваемые параметры.</span><span class="sxs-lookup"><span data-stu-id="8c1ef-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="8c1ef-151">[Разработка скриптов действия сценария для HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="8c1ef-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="8c1ef-152">[Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="8c1ef-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="8c1ef-153">[Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="8c1ef-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="8c1ef-154">[Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="8c1ef-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="8c1ef-155">[Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="8c1ef-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Этапы создания кластера"

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="8c1ef-157">Приложение A. Пример PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c1ef-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="8c1ef-158">Этот сценарий PowerShell создает кластер HDInsight и настраивает параметр Hive:</span><span class="sxs-lookup"><span data-stu-id="8c1ef-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

    ####################################
    # Set these variables
    ####################################
    #region - used for creating Azure service names
    $nameToken = "<ENTER AN ALIAS>" 
    #endregion

    #region - cluster user accounts
    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

    $sshUserName = "sshuser" #HDInsight ssh user name
    $sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
    #endregion

    ####################################
    # Service names and varialbes
    ####################################
    #region - service names
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    $location = "East US 2"
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    ####################################
    # Connect tooAzure
    ####################################
    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an HDInsight cluster
    ####################################
    # Create dependent components
    ####################################
    Write-Host "Creating a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Creating hello default storage account and default blob container ..."  -ForegroundColor Green
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS

    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageContext #use hello cluster name as hello container name

    ####################################
    # Create a configuration object
    ####################################
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    ####################################
    # Create an HDInsight cluster
    ####################################
    $httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

    $sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
    $sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -Location $location `
        -ClusterSizeInNodes 1 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -SshCredential $sshCredential `
        -Config $config

    ####################################
    # Verify hello cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
