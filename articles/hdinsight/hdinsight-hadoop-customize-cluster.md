---
title: "aaaCustomize кластеров HDInsight с помощью сценария действий - Azure | Документы Microsoft"
description: "Узнайте, как toocustomize HDInsight кластеры, использующие действие сценария."
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
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="9dbe4-103">Настройка кластеров HDInsight под управлением Windows с помощью действия сценария</span><span class="sxs-lookup"><span data-stu-id="9dbe4-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="9dbe4-104">**Записать действие в скрипт** может быть используется tooinvoke [пользовательские сценарии](hdinsight-hadoop-script-actions.md) во время создания кластера hello для установки дополнительного программного обеспечения в кластере.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-104">**Script Action** can be used tooinvoke [custom scripts](hdinsight-hadoop-script-actions.md) during hello cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="9dbe4-105">Hello сведения в этой статье — конкретных tooWindows основе кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-105">hello information in this article is specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="9dbe4-106">О кластерах под управлением Linux читайте в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9dbe4-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9dbe4-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9dbe4-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9dbe4-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="9dbe4-109">Кластеров HDInsight могут быть настроены в различных других целей, такие как включение дополнительных учетных записей хранилища Azure, изменение hello Hadoop (core-site.xml, hive-site.xml, т. д.), файлы конфигурации и добавление общие библиотеки (например, Hive, Oozie) в стандартных расположениях в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing hello Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in hello cluster.</span></span> <span data-ttu-id="9dbe4-110">Эти настройки можно сделать с помощью Azure PowerShell, hello Azure HDInsight .NET SDK или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-110">These customizations can be done through Azure PowerShell, hello Azure HDInsight .NET SDK, or hello Azure portal.</span></span> <span data-ttu-id="9dbe4-111">Дополнительные сведения см. в статье [Создание кластеров Hadoop в HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="9dbe4-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="9dbe4-112">Действие сценария в процессе создания кластера hello</span><span class="sxs-lookup"><span data-stu-id="9dbe4-112">Script Action in hello cluster creation process</span></span>
<span data-ttu-id="9dbe4-113">Действие сценария используется только в том случае, пока кластер находится в процессе создания hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-113">Script Action is only used while a cluster is in hello process of being created.</span></span> <span data-ttu-id="9dbe4-114">Hello следующей схеме показана при выполнении сценария действия во время создания hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-114">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="9dbe4-115">![Настройка кластера HDInsight и этапы создания кластера][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="9dbe4-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="9dbe4-116">При выполнении скрипта hello, кластер hello вводит hello **ClusterCustomization** рабочей области.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-116">When hello script is running, hello cluster enters hello **ClusterCustomization** stage.</span></span> <span data-ttu-id="9dbe4-117">На этом этапе сценария hello запускается под учетной записью администратора системы hello, параллельно на всех hello указан узлов в кластере hello и предоставляет права полного администратора на узлах hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-117">At this stage, hello script is run under hello system admin account, in parallel on all hello specified nodes in hello cluster, and provides full admin privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="9dbe4-118">Если у вас права администратора на узлах кластера hello во время **ClusterCustomization** рабочей области, можно использовать hello сценария tooperform операции, такие как остановка и запуск служб, включая службы, связанные с Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-118">Because you have admin privileges on hello cluster nodes during the **ClusterCustomization** stage, you can use hello script tooperform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="9dbe4-119">Так как часть сценария hello, необходимо убедиться, hello Ambari службы и другие службы, связанные с Hadoop доступны и запущены перед hello сценарий завершает работу.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-119">So, as part of hello script, you must ensure that hello Ambari services and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="9dbe4-120">Эти службы необходимы toosuccessfully выяснить hello работоспособности и состояние кластера hello во время создания.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-120">These services are required toosuccessfully ascertain hello health and state of hello cluster while it is being created.</span></span> <span data-ttu-id="9dbe4-121">Если изменить какой-либо настройки в кластере, который влияет на эти службы, необходимо использовать hello вспомогательные функции, которые предоставляются.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-121">If you change any configuration on the cluster that affects these services, you must use hello helper functions that are provided.</span></span> <span data-ttu-id="9dbe4-122">Подробнее о вспомогательных функциях см. в статье [Разработка скриптов действия сценария для HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="9dbe4-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="9dbe4-123">Вывод Hello и hello журналы ошибок для скрипта hello хранятся в учетной записи хранилища hello по умолчанию, заданные для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-123">hello output and hello error logs for hello script are stored in hello default Storage account you specified for hello cluster.</span></span> <span data-ttu-id="9dbe4-124">Hello журналы хранятся в таблице с именем hello **u < \cluster-name-fragment >< \time-stamp > setuplog**.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-124">hello logs are stored in a table with hello name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="9dbe4-125">Это совокупное журналы из hello сценариев, запускаемых на всех узлах hello (головного узла и рабочих узлов) в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-125">These are aggregate logs from hello script run on all hello nodes (head node and worker nodes) in hello cluster.</span></span>

<span data-ttu-id="9dbe4-126">Каждый кластер может принимать несколько действий скрипта, которые вызываются в порядке hello, в котором они указаны.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-126">Each cluster can accept multiple script actions that are invoked in hello order in which they are specified.</span></span> <span data-ttu-id="9dbe4-127">Сценарий можно работали на головном узле hello и hello рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-127">A script can be ran on hello head node, hello worker nodes, or both.</span></span>

<span data-ttu-id="9dbe4-128">HDInsight предоставляет несколько сценариев tooinstall hello, следующие компоненты в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-128">HDInsight provides several scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="9dbe4-129">Имя</span><span class="sxs-lookup"><span data-stu-id="9dbe4-129">Name</span></span> | <span data-ttu-id="9dbe4-130">Скрипт</span><span class="sxs-lookup"><span data-stu-id="9dbe4-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="9dbe4-131">**Установка Spark**</span><span class="sxs-lookup"><span data-stu-id="9dbe4-131">**Install Spark**</span></span> |<span data-ttu-id="9dbe4-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="9dbe4-133">Ознакомьтесь со статьей [Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="9dbe4-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="9dbe4-134">**Установка R**</span><span class="sxs-lookup"><span data-stu-id="9dbe4-134">**Install R**</span></span> |<span data-ttu-id="9dbe4-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="9dbe4-136">Ознакомьтесь со статьей [Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="9dbe4-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="9dbe4-137">**Установка Solr**</span><span class="sxs-lookup"><span data-stu-id="9dbe4-137">**Install Solr**</span></span> |<span data-ttu-id="9dbe4-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="9dbe4-139">Ознакомьтесь со статьей [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="9dbe4-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="9dbe4-140">- **Установка Giraph**</span><span class="sxs-lookup"><span data-stu-id="9dbe4-140">- **Install Giraph**</span></span> |<span data-ttu-id="9dbe4-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="9dbe4-142">Ознакомьтесь со статьей [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="9dbe4-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="9dbe4-143">**Предварительная загрузка библиотек Hive**</span><span class="sxs-lookup"><span data-stu-id="9dbe4-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="9dbe4-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="9dbe4-145">Ознакомьтесь со статьей [Добавление библиотек Hive в кластеры HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="9dbe4-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-hello-azure-portal"></a><span data-ttu-id="9dbe4-146">Вызов сценариев с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="9dbe4-146">Call scripts using hello Azure portal</span></span>
<span data-ttu-id="9dbe4-147">**Из портала Azure hello**</span><span class="sxs-lookup"><span data-stu-id="9dbe4-147">**From hello Azure portal**</span></span>

1. <span data-ttu-id="9dbe4-148">Начните создание кластера, как описано в разделе [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9dbe4-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="9dbe4-149">В разделе дополнительной конфигурации hello **действия скрипта** колонке нажмите кнопку **добавьте действия скрипта** tooprovide сведений о hello действие скрипта, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="9dbe4-149">Under Optional Configuration, for hello **Script Actions** blade, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="9dbe4-150">![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize действия скрипта для использования кластера")</span><span class="sxs-lookup"><span data-stu-id="9dbe4-150">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="9dbe4-151">Свойство</span><span class="sxs-lookup"><span data-stu-id="9dbe4-151">Property</span></span></th><th><span data-ttu-id="9dbe4-152">Значение</span><span class="sxs-lookup"><span data-stu-id="9dbe4-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="9dbe4-153">Имя</span><span class="sxs-lookup"><span data-stu-id="9dbe4-153">Name</span></span></td>
            <td><span data-ttu-id="9dbe4-154">Укажите имя для действия сценария hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-154">Specify a name for hello script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="9dbe4-155">URI-адрес сценария</span><span class="sxs-lookup"><span data-stu-id="9dbe4-155">Script URI</span></span></td>
            <td><span data-ttu-id="9dbe4-156">Укажите сценарий toohello URI hello, вызванный toocustomize hello кластера.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-156">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="9dbe4-157">s</span><span class="sxs-lookup"><span data-stu-id="9dbe4-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="9dbe4-158">Головной/рабочий</span><span class="sxs-lookup"><span data-stu-id="9dbe4-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="9dbe4-159">Укажите узлы hello (**Head** или **рабочих**) на какие hello настройки выполнения скрипта.</b>.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-159">Specify hello nodes (**Head** or **Worker**) on which hello customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="9dbe4-160">Параметры</span><span class="sxs-lookup"><span data-stu-id="9dbe4-160">Parameters</span></span></td>
            <td><span data-ttu-id="9dbe4-161">Укажите параметры hello, если это требуется для сценария hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-161">Specify hello parameters, if required by hello script.</span></span></td></tr>
    </table>

    <span data-ttu-id="9dbe4-162">Нажмите клавишу ВВОД tooadd больше, чем один скрипт действие tooinstall несколько компонентов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-162">Press ENTER tooadd more than one script action tooinstall multiple components on hello cluster.</span></span>
3. <span data-ttu-id="9dbe4-163">Нажмите кнопку **выберите** toosave hello скрипт конфигурации действия и продолжите создание кластера.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-163">Click **Select** toosave hello script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="9dbe4-164">Вызов сценариев с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dbe4-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="9dbe4-165">Это следующий сценарий PowerShell показано, как tooinstall Spark в Windows на основе кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-165">This following PowerShell script demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
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

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
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


<span data-ttu-id="9dbe4-166">tooinstall другого программного обеспечения, вам потребуется файл сценария tooreplace hello в скрипте hello:</span><span class="sxs-lookup"><span data-stu-id="9dbe4-166">tooinstall other software, you will need tooreplace hello script file in hello script:</span></span>

<span data-ttu-id="9dbe4-167">При появлении запроса введите учетные данные hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-167">When prompted, enter hello credentials for hello cluster.</span></span> <span data-ttu-id="9dbe4-168">Он может занять несколько минут, перед созданием кластера hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-168">It can take several minutes before hello cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="9dbe4-169">Вызов сценариев с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="9dbe4-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="9dbe4-170">Hello следующий пример демонстрирует, как tooinstall Spark в Windows на основе кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-170">hello following sample demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="9dbe4-171">tooinstall другого программного обеспечения, вам потребуется файл сценария tooreplace hello в коде hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-171">tooinstall other software, you will need tooreplace hello script file in hello code.</span></span>

<span data-ttu-id="9dbe4-172">**кластер HDInsight с Spark toocreate**</span><span class="sxs-lookup"><span data-stu-id="9dbe4-172">**toocreate an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="9dbe4-173">Создайте в Visual Studio консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="9dbe4-174">Запустите следующую команду hello из hello консоль диспетчера пакетов Nuget.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-174">From hello Nuget Package Manager Console, run hello following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="9dbe4-175">Используйте hello после с помощью инструкций в файле Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="9dbe4-175">Use hello following using statements in hello Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="9dbe4-176">Поместите код hello в классе hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="9dbe4-176">Place hello code in hello class with hello following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
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
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
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
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="9dbe4-177">Нажмите клавишу **F5** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-177">Press **F5** toorun hello application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="9dbe4-178">Поддержка программного обеспечения с открытым исходным кодом, используемого в кластере HDInsight</span><span class="sxs-lookup"><span data-stu-id="9dbe4-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="9dbe4-179">Hello службы Microsoft Azure HDInsight — это гибкая платформа, обеспечивающий toobuild больших данных приложений в облаке hello с помощью экосистему технологий открытым исходным кодом, сформированный вокруг Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-179">hello Microsoft Azure HDInsight service is a flexible platform that enables you toobuild big-data applications in hello cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="9dbe4-180">Microsoft Azure предоставляет общие уровень поддержки для технологий с открытым исходным кодом, как описано в hello **область поддерживает** раздел hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">веб-сайта Azure поддерживают часто задаваемые вопросы о</a>.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in hello **Support Scope** section of hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="9dbe4-181">Hello службы HDInsight предоставляет дополнительный уровень поддержки для некоторых компонентов hello, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-181">hello HDInsight service provides an additional level of support for some of hello components, as described below.</span></span>

<span data-ttu-id="9dbe4-182">Существует два типа компонентов открытым исходным кодом, доступных в hello службы HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9dbe4-182">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="9dbe4-183">**Встроенные компоненты** -эти компоненты предустановлен в кластерах HDInsight и предоставляют основные функциональные возможности кластера hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="9dbe4-184">Например YARN ResourceManager, язык запросов Hive hello (HiveQL) и библиотеку Mahout hello принадлежать toothis категории.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-184">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="9dbe4-185">Полный список компонентов кластера доступен в [новые возможности, предоставляемые HDInsight версиями кластеров Hadoop hello?](hdinsight-component-versioning.md) </a>.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-185">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="9dbe4-186">**Пользовательские компоненты** -, как пользователь кластера hello, можно установить или использовать любой компонент, доступные в сообществе hello или созданный вами в рабочей нагрузке.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-186">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

<span data-ttu-id="9dbe4-187">Встроенные компоненты, полностью поддерживаются и поддержки Майкрософт способствуют tooisolate и разрешить проблемы toothese связанные компоненты.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-187">Built-in components are fully supported, and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>

> [!WARNING]
> <span data-ttu-id="9dbe4-188">Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются и поддержки Майкрософт способствуют tooisolate и разрешить проблемы toothese связанные компоненты.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-188">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="9dbe4-189">Пользовательские компоненты получают toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-189">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="9dbe4-190">Это может привести к устранению проблемы hello и без tooengage доступных каналов для hello открытии источника технологий, которых находится глубокие знания для данной технологии.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-190">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="9dbe4-191">Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, проекты Apache можно просмотреть на соответствующих сайтах по адресу [http://apache.org](http://apache.org), например для [Hadoop](http://hadoop.apache.org/) и [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="9dbe4-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="9dbe4-192">Служба HDInsight Hello предоставляет несколько способов toouse пользовательские компоненты.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-192">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="9dbe4-193">Независимо от того, как компонент используется, или установлена на кластере hello hello же уровнем поддержки применяется.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-193">Regardless of how a component is used or installed on hello cluster, hello same level of support applies.</span></span> <span data-ttu-id="9dbe4-194">Ниже приведен список наиболее распространенными способами hello, что пользовательские компоненты можно использовать в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-194">Below is a list of hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="9dbe4-195">Отправки заданий - Hadoop или других типов заданий, обрабатываемых или использовать пользовательские компоненты может быть отправлено toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-195">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>
2. <span data-ttu-id="9dbe4-196">Настройка кластера - во время создания кластера можно указать дополнительные параметры и пользовательские компоненты, которые будут устанавливаться на узлах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-196">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on hello cluster nodes.</span></span>
3. <span data-ttu-id="9dbe4-197">Примеры — для популярных пользовательские компоненты, корпорация Майкрософт и другие могут предоставлять примеры использования этих компонентов в кластерах HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-197">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="9dbe4-198">Эти примеры представляются без поддержки.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-198">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="9dbe4-199">Разработка скрипта действия сценария</span><span class="sxs-lookup"><span data-stu-id="9dbe4-199">Develop Script Action scripts</span></span>
<span data-ttu-id="9dbe4-200">Ознакомьтесь со статьей [Разработка скриптов действия сценария для HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="9dbe4-200">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="9dbe4-201">См. также</span><span class="sxs-lookup"><span data-stu-id="9dbe4-201">See also</span></span>
* <span data-ttu-id="9dbe4-202">[Создание кластеров Hadoop в HDInsight] [ hdinsight-provision-cluster] описано, как toocreate HDInsight кластер с помощью другие настраиваемые параметры.</span><span class="sxs-lookup"><span data-stu-id="9dbe4-202">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="9dbe4-203">[Разработка скриптов действия сценария для HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="9dbe4-203">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="9dbe4-204">[Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="9dbe4-204">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="9dbe4-205">[Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="9dbe4-205">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="9dbe4-206">[Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="9dbe4-206">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="9dbe4-207">[Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="9dbe4-207">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Этапы создания кластера"
