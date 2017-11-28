---
title: "Настройка кластеров HDInsight с помощью действий скрипта — Azure | Документы Майкрософт"
description: "Дополнительные сведения о настройке кластеров HDInsight с помощью действия скрипта."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: ec95b6d66c71b4278dd1e16807fcc75f5e8b1c36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="00d8f-103">Настройка кластеров HDInsight под управлением Windows с помощью действия сценария</span><span class="sxs-lookup"><span data-stu-id="00d8f-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="00d8f-104">**действий сценария** можно вызывать [пользовательские сценарии](hdinsight-hadoop-script-actions.md) во время создания кластера для установки в нем дополнительного программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="00d8f-104">**Script Action** can be used to invoke [custom scripts](hdinsight-hadoop-script-actions.md) during the cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="00d8f-105">Информация, приведенная в этой статье, относится только к кластерам HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="00d8f-105">The information in this article is specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="00d8f-106">О кластерах под управлением Linux читайте в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="00d8f-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00d8f-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="00d8f-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="00d8f-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="00d8f-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="00d8f-109">Кластеры HDInsight можно настраивать множеством других способов, например включая дополнительные учетные записи хранения Azure, изменяя файлы конфигурации Hadoop (core-site.xml, hive-site.xml и т. д.) или добавляя общие библиотеки (например, Hive, Oozie) в стандартные расположения в кластере.</span><span class="sxs-lookup"><span data-stu-id="00d8f-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing the Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in the cluster.</span></span> <span data-ttu-id="00d8f-110">Эти настройки можно выполнить с помощью Azure PowerShell, пакета SDK для Azure для HDInsight .NET или на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="00d8f-110">These customizations can be done through Azure PowerShell, the Azure HDInsight .NET SDK, or the Azure portal.</span></span> <span data-ttu-id="00d8f-111">Дополнительные сведения см. в статье [Создание кластеров Hadoop в HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="00d8f-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="00d8f-112">Действие сценария в процессе создания кластера</span><span class="sxs-lookup"><span data-stu-id="00d8f-112">Script Action in the cluster creation process</span></span>
<span data-ttu-id="00d8f-113">Действие сценария используется только в том случае, если кластеры находятся в процессе создания.</span><span class="sxs-lookup"><span data-stu-id="00d8f-113">Script Action is only used while a cluster is in the process of being created.</span></span> <span data-ttu-id="00d8f-114">На следующей схеме показано, когда выполняется действие сценария в процессе создания.</span><span class="sxs-lookup"><span data-stu-id="00d8f-114">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="00d8f-115">![Настройка кластера HDInsight и этапы создания кластера][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="00d8f-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="00d8f-116">При выполнении сценария кластер переходит к этапу **ClusterCustomization** .</span><span class="sxs-lookup"><span data-stu-id="00d8f-116">When the script is running, the cluster enters the **ClusterCustomization** stage.</span></span> <span data-ttu-id="00d8f-117">На этой стадии скрипт выполняется под учетной записью администратора системы, параллельно на всех указанных узлах в кластере и предоставляет права администратора на узлах в полном объеме.</span><span class="sxs-lookup"><span data-stu-id="00d8f-117">At this stage, the script is run under the system admin account, in parallel on all the specified nodes in the cluster, and provides full admin privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="00d8f-118">Так как у вас есть права администратора в узлах кластера на этапе **ClusterCustomization**, вы можете использовать скрипт для выполнения таких операций, как остановка и запуск служб, в том числе служб, связанных с Hadoop.</span><span class="sxs-lookup"><span data-stu-id="00d8f-118">Because you have admin privileges on the cluster nodes during the **ClusterCustomization** stage, you can use the script to perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="00d8f-119">Таким образом, перед завершением работы сценария необходимо запустить службы Ambari и другие службы, связанные с Hadoop.</span><span class="sxs-lookup"><span data-stu-id="00d8f-119">So, as part of the script, you must ensure that the Ambari services and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="00d8f-120">Эти службы нужны для определения работоспособности и состояния кластера при его создании.</span><span class="sxs-lookup"><span data-stu-id="00d8f-120">These services are required to successfully ascertain the health and state of the cluster while it is being created.</span></span> <span data-ttu-id="00d8f-121">При изменении любых настроек в кластере, затрагивающих эти службы, необходимо использовать указанные вспомогательные функции.</span><span class="sxs-lookup"><span data-stu-id="00d8f-121">If you change any configuration on the cluster that affects these services, you must use the helper functions that are provided.</span></span> <span data-ttu-id="00d8f-122">Подробнее о вспомогательных функциях см. в статье [Разработка скриптов действия сценария для HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="00d8f-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="00d8f-123">Выходные данные и журналы ошибок сценария хранятся в учетной записи хранения, заданной по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="00d8f-123">The output and the error logs for the script are stored in the default Storage account you specified for the cluster.</span></span> <span data-ttu-id="00d8f-124">Журналы хранятся в таблице с именем **u<фрагмент-имени-кластера><\метка-времени>setuplog**.</span><span class="sxs-lookup"><span data-stu-id="00d8f-124">The logs are stored in a table with the name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="00d8f-125">Это сводные журналы сценария, выполняемого на всех узлах (на головном и рабочих) в кластере.</span><span class="sxs-lookup"><span data-stu-id="00d8f-125">These are aggregate logs from the script run on all the nodes (head node and worker nodes) in the cluster.</span></span>

<span data-ttu-id="00d8f-126">В каждом кластере можно использовать несколько действий сценариев, которые вызываются в том порядке, в котором они указаны.</span><span class="sxs-lookup"><span data-stu-id="00d8f-126">Each cluster can accept multiple script actions that are invoked in the order in which they are specified.</span></span> <span data-ttu-id="00d8f-127">Сценарий может выполняться на головном узле, на рабочем узле или на обоих.</span><span class="sxs-lookup"><span data-stu-id="00d8f-127">A script can be ran on the head node, the worker nodes, or both.</span></span>

<span data-ttu-id="00d8f-128">HDInsight предоставляет несколько скриптов для установки следующих компонентов в кластерах HDInsight:</span><span class="sxs-lookup"><span data-stu-id="00d8f-128">HDInsight provides several scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="00d8f-129">Имя</span><span class="sxs-lookup"><span data-stu-id="00d8f-129">Name</span></span> | <span data-ttu-id="00d8f-130">Скрипт</span><span class="sxs-lookup"><span data-stu-id="00d8f-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="00d8f-131">**Установка Spark**</span><span class="sxs-lookup"><span data-stu-id="00d8f-131">**Install Spark**</span></span> |<span data-ttu-id="00d8f-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="00d8f-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="00d8f-133">Ознакомьтесь со статьей [Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="00d8f-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="00d8f-134">**Установка R**</span><span class="sxs-lookup"><span data-stu-id="00d8f-134">**Install R**</span></span> |<span data-ttu-id="00d8f-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="00d8f-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="00d8f-136">Ознакомьтесь со статьей [Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="00d8f-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="00d8f-137">**Установка Solr**</span><span class="sxs-lookup"><span data-stu-id="00d8f-137">**Install Solr**</span></span> |<span data-ttu-id="00d8f-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="00d8f-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="00d8f-139">Ознакомьтесь со статьей [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="00d8f-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="00d8f-140">- **Установка Giraph**</span><span class="sxs-lookup"><span data-stu-id="00d8f-140">- **Install Giraph**</span></span> |<span data-ttu-id="00d8f-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="00d8f-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="00d8f-142">Ознакомьтесь со статьей [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="00d8f-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="00d8f-143">**Предварительная загрузка библиотек Hive**</span><span class="sxs-lookup"><span data-stu-id="00d8f-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="00d8f-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="00d8f-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="00d8f-145">Ознакомьтесь со статьей [Добавление библиотек Hive в кластеры HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="00d8f-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-the-azure-portal"></a><span data-ttu-id="00d8f-146">Вызов сценариев с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="00d8f-146">Call scripts using the Azure portal</span></span>
<span data-ttu-id="00d8f-147">**На портале Azure**</span><span class="sxs-lookup"><span data-stu-id="00d8f-147">**From the Azure portal**</span></span>

1. <span data-ttu-id="00d8f-148">Начните создание кластера, как описано в разделе [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="00d8f-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="00d8f-149">В разделе "Необязательная настройка" в колонке **Действия скрипта** щелкните **Добавить действие скрипта**, чтобы указать сведения об этом действии скрипта.</span><span class="sxs-lookup"><span data-stu-id="00d8f-149">Under Optional Configuration, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="00d8f-150">![Использование действия сценария для настройки кластера](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Использование действия сценария для настройки кластера")</span><span class="sxs-lookup"><span data-stu-id="00d8f-150">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="00d8f-151">Свойство</span><span class="sxs-lookup"><span data-stu-id="00d8f-151">Property</span></span></th><th><span data-ttu-id="00d8f-152">Значение</span><span class="sxs-lookup"><span data-stu-id="00d8f-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="00d8f-153">Имя</span><span class="sxs-lookup"><span data-stu-id="00d8f-153">Name</span></span></td>
            <td><span data-ttu-id="00d8f-154">Укажите имя для действия сценария.</span><span class="sxs-lookup"><span data-stu-id="00d8f-154">Specify a name for the script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="00d8f-155">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="00d8f-155">Script URI</span></span></td>
            <td><span data-ttu-id="00d8f-156">Укажите URI для сценария, который вызывается для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="00d8f-156">Specify the URI to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="00d8f-157">s</span><span class="sxs-lookup"><span data-stu-id="00d8f-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="00d8f-158">Головной/рабочий</span><span class="sxs-lookup"><span data-stu-id="00d8f-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="00d8f-159">Укажите узлы (**Головной** или **Рабочий**), на которых выполняется скрипт настройки</b>.</span><span class="sxs-lookup"><span data-stu-id="00d8f-159">Specify the nodes (**Head** or **Worker**) on which the customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="00d8f-160">Параметры</span><span class="sxs-lookup"><span data-stu-id="00d8f-160">Parameters</span></span></td>
            <td><span data-ttu-id="00d8f-161">Укажите параметры, если они требуются для сценария.</span><span class="sxs-lookup"><span data-stu-id="00d8f-161">Specify the parameters, if required by the script.</span></span></td></tr>
    </table>

    <span data-ttu-id="00d8f-162">Нажмите клавишу ВВОД, чтобы добавить несколько действий сценария для установки нескольких компонентов в кластере.</span><span class="sxs-lookup"><span data-stu-id="00d8f-162">Press ENTER to add more than one script action to install multiple components on the cluster.</span></span>
3. <span data-ttu-id="00d8f-163">Щелкните **Выбрать** , чтобы сохранить конфигурацию действия сценария и продолжить создание кластера.</span><span class="sxs-lookup"><span data-stu-id="00d8f-163">Click **Select** to save the script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="00d8f-164">Вызов сценариев с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="00d8f-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="00d8f-165">Этот сценарий PowerShell показывает, как установить Spark в кластере HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="00d8f-165">This following PowerShell script demonstrates how to install Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" to list IDs.

    $nameToken = "<Enter A Name Token>"  # The token is use to create Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect to Azure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare the dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify the configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action to the cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="00d8f-166">Чтобы установить другое программное обеспечение, необходимо заменить файл скрипта в сценарии:</span><span class="sxs-lookup"><span data-stu-id="00d8f-166">To install other software, you will need to replace the script file in the script:</span></span>

<span data-ttu-id="00d8f-167">При появлении запроса введите учетные данные для кластера.</span><span class="sxs-lookup"><span data-stu-id="00d8f-167">When prompted, enter the credentials for the cluster.</span></span> <span data-ttu-id="00d8f-168">Создание кластера может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="00d8f-168">It can take several minutes before the cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="00d8f-169">Вызов сценариев с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="00d8f-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="00d8f-170">В следующем примере показано, как установить Spark на кластер HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="00d8f-170">The following sample demonstrates how to install Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="00d8f-171">Чтобы установить другое программное обеспечение, необходимо заменить файл скрипта в коде.</span><span class="sxs-lookup"><span data-stu-id="00d8f-171">To install other software, you will need to replace the script file in the code.</span></span>

<span data-ttu-id="00d8f-172">**Создание кластера HDInsight с использованием Spark**</span><span class="sxs-lookup"><span data-stu-id="00d8f-172">**To create an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="00d8f-173">Создайте в Visual Studio консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="00d8f-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="00d8f-174">Введите следующую команду в окне консоли диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="00d8f-174">From the Nuget Package Manager Console, run the following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="00d8f-175">Используйте следующие инструкции using в файле Program.cs:</span><span class="sxs-lookup"><span data-stu-id="00d8f-175">Use the following using statements in the Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="00d8f-176">Замените существующий код в файле класса следующим:</span><span class="sxs-lookup"><span data-stu-id="00d8f-176">Place the code in the class with the following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is the GUID for the PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate to an Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">The AAD tenant ID</param>
        /// <param name="ClientId">The AAD client ID</param>
        /// <param name="SubscriptionId">The Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for the Resource manager and set the subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register the HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="00d8f-177">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="00d8f-177">Press **F5** to run the application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="00d8f-178">Поддержка программного обеспечения с открытым исходным кодом, используемого в кластере HDInsight</span><span class="sxs-lookup"><span data-stu-id="00d8f-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="00d8f-179">Служба Microsoft Azure HDInsight — это гибкая платформа, которая позволяет создавать приложения для работы с данными большого размера в облаке, используя сформированную вокруг Hadoop экосистему технологий с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="00d8f-179">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="00d8f-180">Microsoft Azure предоставляет общий уровень поддержки для технологий с открытым исходным кодом, как описано в статье **Объем поддержки** на <a href="http://azure.microsoft.com/support/faq/" target="_blank">веб-сайте часто задаваемых вопросов о поддержке Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="00d8f-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="00d8f-181">Служба HDInsight предоставляет дополнительный уровень поддержки для некоторых описанных ниже компонентов.</span><span class="sxs-lookup"><span data-stu-id="00d8f-181">The HDInsight service provides an additional level of support for some of the components, as described below.</span></span>

<span data-ttu-id="00d8f-182">В службе HDInsight доступно два типа компонентов с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="00d8f-182">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="00d8f-183">**Встроенные компоненты.** Эти компоненты предварительно установлены в кластерах HDInsight и предоставляют его базовые функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="00d8f-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="00d8f-184">Например, к этой категории относится диспетчер ресурсов YARN, язык запросов Hive (HiveQL) и библиотека Mahout.</span><span class="sxs-lookup"><span data-stu-id="00d8f-184">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="00d8f-185">Полный список компонентов кластера доступен в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</a></span><span class="sxs-lookup"><span data-stu-id="00d8f-185">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="00d8f-186">**Настраиваемые компоненты.** Как пользователь кластера вы можете установить или использовать в рабочей нагрузке любой компонент, полученный из сообщества или созданный самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="00d8f-186">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

<span data-ttu-id="00d8f-187">Встроенные компоненты полностью поддерживаются, и служба поддержки корпорации Майкрософт поможет выявить и устранить проблемы, связанные с этими компонентами.</span><span class="sxs-lookup"><span data-stu-id="00d8f-187">Built-in components are fully supported, and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>

> [!WARNING]
> <span data-ttu-id="00d8f-188">Компоненты, предоставляемые вместе с кластером HDInsight, поддерживаются в полном объеме. Служба поддержки Майкрософт поможет вам выявить и устранить проблемы, связанные с этими компонентами.</span><span class="sxs-lookup"><span data-stu-id="00d8f-188">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="00d8f-189">Настраиваемые компоненты получают ограниченную коммерчески оправданную поддержку, способствующую дальнейшей диагностике проблемы.</span><span class="sxs-lookup"><span data-stu-id="00d8f-189">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="00d8f-190">В результате проблема может быть устранена, либо вас могут попросить воспользоваться доступными каналами по технологиям с открытым исходным кодом, чтобы связаться с экспертами в данной области.</span><span class="sxs-lookup"><span data-stu-id="00d8f-190">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="00d8f-191">Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="00d8f-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="00d8f-192">Кроме того, проекты Apache можно просмотреть на соответствующих сайтах по адресу [http://apache.org](http://apache.org), например для [Hadoop](http://hadoop.apache.org/) и [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="00d8f-192">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="00d8f-193">Служба HDInsight позволяет использовать настраиваемые компоненты несколькими разными способами.</span><span class="sxs-lookup"><span data-stu-id="00d8f-193">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="00d8f-194">Уровень поддержки не зависит от того, как компонент используется или устанавливается в кластере.</span><span class="sxs-lookup"><span data-stu-id="00d8f-194">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span></span> <span data-ttu-id="00d8f-195">Ниже приведен список самых распространенных способов использования настраиваемых компонентов в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00d8f-195">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="00d8f-196">Отправка задания. В кластер можно отправлять задания Hadoop или другие типы заданий, выполняющие или использующие настраиваемые компоненты.</span><span class="sxs-lookup"><span data-stu-id="00d8f-196">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>
2. <span data-ttu-id="00d8f-197">Настройка кластера. Во время создания кластера можно указать дополнительные параметры и настраиваемые компоненты, которые будут установлены в узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="00d8f-197">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on the cluster nodes.</span></span>
3. <span data-ttu-id="00d8f-198">Примеры. Для популярных настраиваемых компонентов корпорация Майкрософт и другие компании могут предоставлять примеры использования таких компонентов в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00d8f-198">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="00d8f-199">Эти примеры представляются без поддержки.</span><span class="sxs-lookup"><span data-stu-id="00d8f-199">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="00d8f-200">Разработка скрипта действия сценария</span><span class="sxs-lookup"><span data-stu-id="00d8f-200">Develop Script Action scripts</span></span>
<span data-ttu-id="00d8f-201">Ознакомьтесь со статьей [Разработка скриптов действия сценария для HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="00d8f-201">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="00d8f-202">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="00d8f-202">See also</span></span>
* <span data-ttu-id="00d8f-203">В статье [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision-cluster] приведены указания по созданию кластера HDInsight с использованием других настраиваемых параметров.</span><span class="sxs-lookup"><span data-stu-id="00d8f-203">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="00d8f-204">[Разработка скриптов действия сценария для HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="00d8f-204">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="00d8f-205">[Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="00d8f-205">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="00d8f-206">[Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="00d8f-206">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="00d8f-207">[Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="00d8f-207">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="00d8f-208">[Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="00d8f-208">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="00d8f-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Этапы создания кластера"</span><span class="sxs-lookup"><span data-stu-id="00d8f-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
