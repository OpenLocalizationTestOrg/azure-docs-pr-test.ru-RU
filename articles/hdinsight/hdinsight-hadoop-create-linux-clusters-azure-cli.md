---
title: "с помощью командной строки - hello Azure HDInsight кластеров Hadoop aaaCreate | Документы Microsoft"
description: "Узнайте, как с помощью кластеров HDInsight toocreate hello кросс платформенных Azure CLI 1.0."
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
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a><span data-ttu-id="a1424-103">Создать кластеры HDInsight с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a1424-103">Create HDInsight clusters using hello Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="a1424-104">Hello шагов этого пошагового руководства документа, для создания кластера HDInsight 3.5 с помощью hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="a1424-104">hello steps in this document walk-through creating a HDInsight 3.5 cluster using hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1424-105">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a1424-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a1424-106">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a1424-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a1424-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a1424-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="a1424-108">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="a1424-108">**An Azure subscription**.</span></span> <span data-ttu-id="a1424-109">См. страницу [бесплатной пробной версии Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a1424-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="a1424-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="a1424-110">**Azure CLI**.</span></span> <span data-ttu-id="a1424-111">Hello в данном пошаговом руководстве последнего были протестированы с Azure CLI версии 0.10.14.</span><span class="sxs-lookup"><span data-stu-id="a1424-111">hello steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a1424-112">Hello в данном пошаговом руководстве не работают с Azure CLI версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="a1424-112">hello steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="a1424-113">Azure CLI 2.0 не поддерживает создание кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a1424-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="a1424-114">Войдите в tooyour подписки Azure</span><span class="sxs-lookup"><span data-stu-id="a1424-114">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="a1424-115">Выполните hello шагов, описанных в [подключение tooan подписки Azure из hello Azure командной строки (CLI Azure)](../xplat-cli-connect.md) и подключите tooyour подписку, используя hello **входа** метод.</span><span class="sxs-lookup"><span data-stu-id="a1424-115">Follow hello steps documented in [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect tooyour subscription using hello **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="a1424-116">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="a1424-116">Create a cluster</span></span>

<span data-ttu-id="a1424-117">Привет, следующие шаги необходимо выполнить из командной строки, например PowerShell или Bash.</span><span class="sxs-lookup"><span data-stu-id="a1424-117">hello following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="a1424-118">Используйте hello следующая команда tooauthenticate tooyour подписки Azure:</span><span class="sxs-lookup"><span data-stu-id="a1424-118">Use hello following command tooauthenticate tooyour Azure subscription:</span></span>

        azure login

    <span data-ttu-id="a1424-119">Вы являются запрашиваемые tooprovide свое имя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a1424-119">You are prompted tooprovide your name and password.</span></span> <span data-ttu-id="a1424-120">Если у вас несколько подписок Azure, используйте `azure account set <subscriptionname>` tooset hello подписку, которая hello Azure CLI команды используют.</span><span class="sxs-lookup"><span data-stu-id="a1424-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` tooset hello subscription that hello Azure CLI commands use.</span></span>

2. <span data-ttu-id="a1424-121">Переключение режима tooAzure диспетчера ресурсов, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a1424-121">Switch tooAzure Resource Manager mode using hello following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="a1424-122">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a1424-122">Create a resource group.</span></span> <span data-ttu-id="a1424-123">Эта группа ресурсов содержит кластер HDInsight hello и соответствующие учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="a1424-123">This resource group contains hello HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="a1424-124">Замените `groupname` уникальное имя для группы hello.</span><span class="sxs-lookup"><span data-stu-id="a1424-124">Replace `groupname` with a unique name for hello group.</span></span>

    * <span data-ttu-id="a1424-125">Замените `location` с hello географический регион, вы должны быть toocreate hello группы.</span><span class="sxs-lookup"><span data-stu-id="a1424-125">Replace `location` with hello geographic region that you want toocreate hello group in.</span></span>

       <span data-ttu-id="a1424-126">Список допустимых местах, использовать hello `azure location list` команды, а затем использовать одно из местоположений hello из hello `Name` столбца.</span><span class="sxs-lookup"><span data-stu-id="a1424-126">For a list of valid locations, use hello `azure location list` command, and then use one of hello locations from hello `Name` column.</span></span>

4. <span data-ttu-id="a1424-127">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a1424-127">Create a storage account.</span></span> <span data-ttu-id="a1424-128">Эта учетная запись хранения служит hello хранилища по умолчанию для кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="a1424-128">This storage account is used as hello default storage for hello HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="a1424-129">Замените `groupname` с именем hello hello группы, созданной в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="a1424-129">Replace `groupname` with hello name of hello group created in hello previous step.</span></span>

    * <span data-ttu-id="a1424-130">Замените `location` с hello местоположения, используемый в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="a1424-130">Replace `location` with hello same location used in hello previous step.</span></span>

    * <span data-ttu-id="a1424-131">Замените `storagename` уникальное имя для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="a1424-131">Replace `storagename` with a unique name for hello storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="a1424-132">Дополнительные сведения о параметрах hello, использованный в этой команде используется `azure storage account create -h` tooview справку для этой команды.</span><span class="sxs-lookup"><span data-stu-id="a1424-132">For more information on hello parameters used in this command, use `azure storage account create -h` tooview help for this command.</span></span>

5. <span data-ttu-id="a1424-133">Получить учетную запись хранения hello ключа используется tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="a1424-133">Retrieve hello key used tooaccess hello storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="a1424-134">Замените `groupname` с hello имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a1424-134">Replace `groupname` with hello resource group name.</span></span>
    * <span data-ttu-id="a1424-135">Замените `storagename` с именем hello hello учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a1424-135">Replace `storagename` with hello name of hello storage account.</span></span>

     <span data-ttu-id="a1424-136">В возвращаемых данных hello, сохранить hello `key` значение `key1`.</span><span class="sxs-lookup"><span data-stu-id="a1424-136">In hello data that is returned, save hello `key` value for `key1`.</span></span>

6. <span data-ttu-id="a1424-137">Создание кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a1424-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="a1424-138">Замените `groupname` с hello имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a1424-138">Replace `groupname` with hello resource group name.</span></span>

    * <span data-ttu-id="a1424-139">Замените `Hadoop` с типом кластера hello, что вы хотите toocreate.</span><span class="sxs-lookup"><span data-stu-id="a1424-139">Replace `Hadoop` with hello cluster type that you wish toocreate.</span></span> <span data-ttu-id="a1424-140">Примеры: `Hadoop`, `HBase`, `Kafka`, `Spark` или `Storm`.</span><span class="sxs-lookup"><span data-stu-id="a1424-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="a1424-141">HDInsight кластеров поставляются в различных типов, которые соответствуют toohello рабочей нагрузки или технология, которая hello кластера настроена для работы.</span><span class="sxs-lookup"><span data-stu-id="a1424-141">HDInsight clusters come in various types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="a1424-142">Нет не поддерживаемый метод toocreate кластера, которая объединяет несколько типов, таких как Storm и HBase на один кластер.</span><span class="sxs-lookup"><span data-stu-id="a1424-142">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="a1424-143">Замените `location` с hello местоположения, используемый в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="a1424-143">Replace `location` with hello same location used in previous steps.</span></span>

    * <span data-ttu-id="a1424-144">Замените `storagename` на имя учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="a1424-144">Replace `storagename` with hello storage account name.</span></span>

    * <span data-ttu-id="a1424-145">Замените `storagekey` с hello ключ, полученный в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="a1424-145">Replace `storagekey` with hello key obtained in hello previous step.</span></span>

    * <span data-ttu-id="a1424-146">Для hello `--defaultStorageContainer` параметр, используйте hello точно такое же имя, как вы используете для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="a1424-146">For hello `--defaultStorageContainer` parameter, use hello same name as you are using for hello cluster.</span></span>

    * <span data-ttu-id="a1424-147">Замените `admin` и `httppassword` hello имя и пароль вы хотите toouse при доступе к hello кластера по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a1424-147">Replace `admin` and `httppassword` with hello name and password you wish toouse when accessing hello cluster through HTTPS.</span></span>

    * <span data-ttu-id="a1424-148">Замените `sshuser` и `sshuserpassword` hello имя пользователя и пароль при доступе к hello кластера с помощью SSH требуется toouse</span><span class="sxs-lookup"><span data-stu-id="a1424-148">Replace `sshuser` and `sshuserpassword` with hello username and password you wish toouse when accessing hello cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a1424-149">Этот пример создает кластер с 2 рабочими узлами.</span><span class="sxs-lookup"><span data-stu-id="a1424-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="a1424-150">После создания кластера можно также изменить hello число рабочих узлов, выполняя операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="a1424-150">You can also change hello number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="a1424-151">Если вы планируете использовать более 32 рабочих узлов, для головного узла необходимо выбрать по крайней мере 8-ядерный процессор и 14 ГБ ОЗУ.</span><span class="sxs-lookup"><span data-stu-id="a1424-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="a1424-152">Можно задать размер hello головного узла с помощью hello `--headNodeSize` параметра во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="a1424-152">You can set hello head node size by using hello `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="a1424-153">Дополнительные сведения о размерах узлов и их стоимости см. на странице с [ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a1424-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="a1424-154">Он может занять несколько минут для toofinish процесса создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="a1424-154">It may take several minutes for hello cluster creation process toofinish.</span></span> <span data-ttu-id="a1424-155">обычно около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="a1424-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="a1424-156">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="a1424-156">Troubleshoot</span></span>

<span data-ttu-id="a1424-157">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="a1424-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1424-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1424-158">Next steps</span></span>

<span data-ttu-id="a1424-159">Теперь, когда кластер HDInsight с помощью Azure CLI hello успешно создана, использовать как следующая toolearn hello toowork с кластером:</span><span class="sxs-lookup"><span data-stu-id="a1424-159">Now that you have successfully created an HDInsight cluster using hello Azure CLI, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="a1424-160">Кластеры Hadoop</span><span class="sxs-lookup"><span data-stu-id="a1424-160">Hadoop clusters</span></span>

* [<span data-ttu-id="a1424-161">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1424-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a1424-162">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1424-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a1424-163">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1424-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="a1424-164">Кластеры HBase</span><span class="sxs-lookup"><span data-stu-id="a1424-164">HBase clusters</span></span>

* [<span data-ttu-id="a1424-165">Начало работы с HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1424-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="a1424-166">Разработка приложений Java для HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1424-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="a1424-167">Кластеры Storm</span><span class="sxs-lookup"><span data-stu-id="a1424-167">Storm clusters</span></span>

* [<span data-ttu-id="a1424-168">Разработка приложений Java для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1424-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="a1424-169">Использование компонентов Python в Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1424-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="a1424-170">Развертывание и мониторинг топологий с помощью Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1424-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
