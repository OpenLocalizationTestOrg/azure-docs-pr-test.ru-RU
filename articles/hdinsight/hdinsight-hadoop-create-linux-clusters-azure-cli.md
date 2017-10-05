---
title: "Создание кластеров Hadoop с помощью командной строки в Azure HDInsight | Документы Майкрософт"
description: "Узнайте, как создавать кластеры HDInsight с кроссплатформенного Azure CLI 1.0."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 8f2fcb46789d000cd66164508f1159338dcae5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-using-the-azure-cli"></a><span data-ttu-id="7dd5a-103">Создание кластеров HDInsight с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="7dd5a-103">Create HDInsight clusters using the Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="7dd5a-104">Это пошаговое руководство содержит инструкции по созданию кластера HDInsight 3.5 с помощью Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7dd5a-105">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7dd5a-106">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7dd5a-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7dd5a-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7dd5a-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="7dd5a-108">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-108">**An Azure subscription**.</span></span> <span data-ttu-id="7dd5a-109">См. страницу [бесплатной пробной версии Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7dd5a-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="7dd5a-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-110">**Azure CLI**.</span></span> <span data-ttu-id="7dd5a-111">Действия, описанные в этом документе, проверены с помощью Azure CLI версии 0.10.14.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-111">The steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7dd5a-112">Инструкции, приведенные в этом документе, не подходят для Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-112">The steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="7dd5a-113">Azure CLI 2.0 не поддерживает создание кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="7dd5a-114">Вход в подписку Azure</span><span class="sxs-lookup"><span data-stu-id="7dd5a-114">Log in to your Azure subscription</span></span>

<span data-ttu-id="7dd5a-115">Выполните действия, описанные в статье [Подключение к среде Azure с использованием интерфейса командной строки Azure (Azure CLI)](../xplat-cli-connect.md) , и подключитесь к подписке с помощью метода **login** .</span><span class="sxs-lookup"><span data-stu-id="7dd5a-115">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="7dd5a-116">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="7dd5a-116">Create a cluster</span></span>

<span data-ttu-id="7dd5a-117">Описанные ниже действия следует выполнять в командной строке, например PowerShell или Bash.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-117">The following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="7dd5a-118">Выполните следующую команду для аутентификации в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-118">Use the following command to authenticate to your Azure subscription:</span></span>

        azure login

    <span data-ttu-id="7dd5a-119">Вам будет предложено указать имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-119">You are prompted to provide your name and password.</span></span> <span data-ttu-id="7dd5a-120">Если подписок Azure несколько, укажите, какую подписку должны использовать команды Azure CLI, с помощью метода `azure account set <subscriptionname>` .</span><span class="sxs-lookup"><span data-stu-id="7dd5a-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span></span>

2. <span data-ttu-id="7dd5a-121">Переключитесь в режим диспетчера ресурсов Azure с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="7dd5a-121">Switch to Azure Resource Manager mode using the following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="7dd5a-122">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-122">Create a resource group.</span></span> <span data-ttu-id="7dd5a-123">Эта группа ресурсов будет содержать кластер HDInsight и соответствующую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-123">This resource group contains the HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="7dd5a-124">Замените `groupname` на уникальное имя группы.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-124">Replace `groupname` with a unique name for the group.</span></span>

    * <span data-ttu-id="7dd5a-125">Замените `location` на географический регион, в котором нужно создать группу.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-125">Replace `location` with the geographic region that you want to create the group in.</span></span>

       <span data-ttu-id="7dd5a-126">Для получения списка допустимых расположений выполните команду `azure location list`, а затем воспользуйтесь одним из расположений из столбца `Name`.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-126">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the `Name` column.</span></span>

4. <span data-ttu-id="7dd5a-127">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-127">Create a storage account.</span></span> <span data-ttu-id="7dd5a-128">Эта учетная запись хранения будет использоваться как хранилище по умолчанию для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-128">This storage account is used as the default storage for the HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="7dd5a-129">Замените `groupname` на имя группы, созданной на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-129">Replace `groupname` with the name of the group created in the previous step.</span></span>

    * <span data-ttu-id="7dd5a-130">Замените `location` на расположение, которое использовалось на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-130">Replace `location` with the same location used in the previous step.</span></span>

    * <span data-ttu-id="7dd5a-131">Замените `storagename` на уникальное имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-131">Replace `storagename` with a unique name for the storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="7dd5a-132">Дополнительные сведения о параметрах, используемых в этой команде, используйте `azure storage account create -h`, чтобы открыть справку по этой команде.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-132">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span></span>

5. <span data-ttu-id="7dd5a-133">Извлеките ключ для доступа к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-133">Retrieve the key used to access the storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="7dd5a-134">Замените `groupname` на имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-134">Replace `groupname` with the resource group name.</span></span>
    * <span data-ttu-id="7dd5a-135">Замените `storagename` на имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-135">Replace `storagename` with the name of the storage account.</span></span>

     <span data-ttu-id="7dd5a-136">Из полученных данных сохраните значение `key` параметра `key1`.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-136">In the data that is returned, save the `key` value for `key1`.</span></span>

6. <span data-ttu-id="7dd5a-137">Создание кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="7dd5a-138">Замените `groupname` на имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-138">Replace `groupname` with the resource group name.</span></span>

    * <span data-ttu-id="7dd5a-139">Замените `Hadoop` типом кластера, который хотите создать.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-139">Replace `Hadoop` with the cluster type that you wish to create.</span></span> <span data-ttu-id="7dd5a-140">Примеры: `Hadoop`, `HBase`, `Kafka`, `Spark` или `Storm`.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="7dd5a-141">Кластеры HDInsight бывают разных типов, которые соответствуют рабочей нагрузке или технологии, для которой предназначен кластер.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-141">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="7dd5a-142">Создать кластер, в котором бы объединились несколько типов, например Storm и HBase, нельзя.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-142">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="7dd5a-143">Замените `location` на расположение, которое использовалось на предыдущих этапах.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-143">Replace `location` with the same location used in previous steps.</span></span>

    * <span data-ttu-id="7dd5a-144">Замените `storagename` на имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-144">Replace `storagename` with the storage account name.</span></span>

    * <span data-ttu-id="7dd5a-145">Замените `storagekey` на ключ, полученный на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-145">Replace `storagekey` with the key obtained in the previous step.</span></span>

    * <span data-ttu-id="7dd5a-146">Для параметра `--defaultStorageContainer` используйте то же имя, что и для кластера.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-146">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span></span>

    * <span data-ttu-id="7dd5a-147">Замените `admin` и `httppassword` именем и паролем, которые нужно использовать для доступа к кластеру по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-147">Replace `admin` and `httppassword` with the name and password you wish to use when accessing the cluster through HTTPS.</span></span>

    * <span data-ttu-id="7dd5a-148">Замените `sshuser` и `sshuserpassword` именем пользователя и паролем, которые нужно использовать для доступа к кластеру по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-148">Replace `sshuser` and `sshuserpassword` with the username and password you wish to use when accessing the cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7dd5a-149">Этот пример создает кластер с 2 рабочими узлами.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="7dd5a-150">После создания кластера можно изменить число рабочих узлов, выполнив операцию масштабирования.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-150">You can also change the number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="7dd5a-151">Если вы планируете использовать более 32 рабочих узлов, для головного узла необходимо выбрать по крайней мере 8-ядерный процессор и 14 ГБ ОЗУ.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="7dd5a-152">Настроить размер головного узла можно с помощью параметра `--headNodeSize` во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-152">You can set the head node size by using the `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="7dd5a-153">Дополнительные сведения о размерах узлов и их стоимости см. на странице с [ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7dd5a-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="7dd5a-154">Создание кластера требует времени,</span><span class="sxs-lookup"><span data-stu-id="7dd5a-154">It may take several minutes for the cluster creation process to finish.</span></span> <span data-ttu-id="7dd5a-155">обычно около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="7dd5a-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="7dd5a-156">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="7dd5a-156">Troubleshoot</span></span>

<span data-ttu-id="7dd5a-157">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="7dd5a-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7dd5a-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7dd5a-158">Next steps</span></span>

<span data-ttu-id="7dd5a-159">Теперь, когда вы успешно создали кластер HDInsight с помощью интерфейса командной строки Azure, обратитесь к следующим статьям, чтобы научиться работать с кластером:</span><span class="sxs-lookup"><span data-stu-id="7dd5a-159">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="7dd5a-160">Кластеры Hadoop</span><span class="sxs-lookup"><span data-stu-id="7dd5a-160">Hadoop clusters</span></span>

* [<span data-ttu-id="7dd5a-161">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dd5a-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7dd5a-162">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dd5a-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7dd5a-163">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dd5a-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="7dd5a-164">Кластеры HBase</span><span class="sxs-lookup"><span data-stu-id="7dd5a-164">HBase clusters</span></span>

* [<span data-ttu-id="7dd5a-165">Начало работы с HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dd5a-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="7dd5a-166">Разработка приложений Java для HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dd5a-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="7dd5a-167">Кластеры Storm</span><span class="sxs-lookup"><span data-stu-id="7dd5a-167">Storm clusters</span></span>

* [<span data-ttu-id="7dd5a-168">Разработка приложений Java для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dd5a-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="7dd5a-169">Использование компонентов Python в Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dd5a-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="7dd5a-170">Развертывание и мониторинг топологий с помощью Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="7dd5a-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
