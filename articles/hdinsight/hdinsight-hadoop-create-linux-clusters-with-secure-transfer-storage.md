---
title: "кластер aaaCreate Hadoop с безопасной передачи учетных записей хранения в Azure HDInsight | Документы Microsoft"
description: "Дополнительные сведения, включение toocreate кластеров HDInsight с безопасной передачи учетных записей хранилища Azure."
keywords: hadoop getting started,hadoop linux,hadoop quickstart,secure transfer,azure storage account
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="83bb4-104">Создание кластера Hadoop с помощью учетных записей хранения с безопасной передачей в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="83bb4-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="83bb4-105">Hello [Безопасная передача необходимые](../storage/common/storage-require-secure-transfer.md) функция усиливает hello безопасности вашей учетной записи хранилища Azure путем применения всех tooyour учетной записи запросов через безопасное соединение.</span><span class="sxs-lookup"><span data-stu-id="83bb4-105">hello [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances hello security of your Azure Storage account by enforcing all requests tooyour account through a secure connection.</span></span> <span data-ttu-id="83bb4-106">Этот компонент hello wasbs схему и поддерживаются только версия кластера HDInsight 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="83bb4-106">This feature and hello wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="83bb4-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="83bb4-107">Prerequisites</span></span>
<span data-ttu-id="83bb4-108">Для работы с этим руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="83bb4-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="83bb4-109">**Подписка Azure**: toocreate свободного один месяц пробную учетную запись, Обзор слишком[azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="83bb4-109">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="83bb4-110">**Учетная запись хранения Azure с включенной безопасной передачей**.</span><span class="sxs-lookup"><span data-stu-id="83bb4-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="83bb4-111">Hello инструкции см. в разделе [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) и [требуют безопасной передачи](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="83bb4-111">For hello instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="83bb4-112">**Контейнер больших двоичных объектов в учетной записи хранения hello**.</span><span class="sxs-lookup"><span data-stu-id="83bb4-112">**A Blob container on hello storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="83bb4-113">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="83bb4-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="83bb4-114">В этом разделе вы создадите в HDInsight кластер Hadoop, используя [шаблон Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="83bb4-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="83bb4-115">Hello шаблон находится в [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="83bb4-115">hello template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="83bb4-116">Знакомство с шаблонами Resource Manager не является обязательным для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="83bb4-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="83bb4-117">Для других методов создания кластера и общие сведения о свойствах hello, используемые в этом учебнике, см. [HDInsight, создания кластеров](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="83bb4-117">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="83bb4-118">Щелкните hello toosign образа в tooAzure и откройте hello шаблона диспетчера ресурсов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="83bb4-118">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="83bb4-119">Выполните hello инструкции toocreate hello кластера с hello следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="83bb4-119">Follow hello instructions toocreate hello cluster with hello following specifications:</span></span> 

    - <span data-ttu-id="83bb4-120">Укажите HDInsight версии 3.6.</span><span class="sxs-lookup"><span data-stu-id="83bb4-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="83bb4-121">версия по умолчанию Hello — 3.5.</span><span class="sxs-lookup"><span data-stu-id="83bb4-121">hello default version is 3.5.</span></span> <span data-ttu-id="83bb4-122">Требуется версия 3.6 или более новая.</span><span class="sxs-lookup"><span data-stu-id="83bb4-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="83bb4-123">Укажите учетную запись хранения с включенной безопасной передачей.</span><span class="sxs-lookup"><span data-stu-id="83bb4-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="83bb4-124">Используйте короткое имя для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="83bb4-124">Use short name for hello storage account.</span></span>
    - <span data-ttu-id="83bb4-125">Учетная запись хранения hello и hello контейнер больших двоичных объектов необходимо создать заранее.</span><span class="sxs-lookup"><span data-stu-id="83bb4-125">Both hello storage account and hello blob container must be created beforehand.</span></span> 

    <span data-ttu-id="83bb4-126">Hello инструкции см. в разделе [создать кластер](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="83bb4-126">For hello instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="83bb4-127">При использовании сценария действия tooprovide файлы конфигурации, необходимо использовать wasbs в hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="83bb4-127">If you use script action tooprovide your own configuration files, you must use wasbs in hello following settings:</span></span>

- <span data-ttu-id="83bb4-128">fs.defaultFS (core-site)</span><span class="sxs-lookup"><span data-stu-id="83bb4-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="83bb4-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="83bb4-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="83bb4-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="83bb4-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="83bb4-131">Добавление дополнительных учетных записей хранения</span><span class="sxs-lookup"><span data-stu-id="83bb4-131">Add additional storage accounts</span></span>

<span data-ttu-id="83bb4-132">Существует несколько вариантов tooadd включены дополнительные безопасной передачи учетных записей хранения:</span><span class="sxs-lookup"><span data-stu-id="83bb4-132">There are several options tooadd additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="83bb4-133">Изменение шаблона диспетчера ресурсов Azure hello в последнем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="83bb4-133">Modify hello Azure Resource Manager template in hello last section.</span></span>
- <span data-ttu-id="83bb4-134">Создание кластера с помощью hello [портал Azure](https://portal.azure.com) и укажите связанной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="83bb4-134">Create a cluster using hello [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="83bb4-135">Используйте сценарий действия tooadd дополнительных безопасной передачи включить существующий кластер HDInsight хранилища учетных записей tooan.</span><span class="sxs-lookup"><span data-stu-id="83bb4-135">Use script action tooadd additional secure transfer enabled storage accounts tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="83bb4-136">Дополнительные сведения см. в разделе [добавить дополнительное хранилище учетных записей tooHDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="83bb4-136">For more information, see [Add additional storage accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="83bb4-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83bb4-137">Next steps</span></span>
<span data-ttu-id="83bb4-138">В этом учебнике вы изучили, как toocreate кластер HDInsight и включить безопасной передачи toohello учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="83bb4-138">In this tutorial, you have learned how toocreate an HDInsight cluster, and enable secure transfer toohello storage accounts.</span></span>

<span data-ttu-id="83bb4-139">toolearn Дополнительные сведения об анализе данных с HDInsight, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="83bb4-139">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="83bb4-140">toolearn Подробнее об использовании Hive с HDInsight, включая как tooperform Hive запросы из Visual Studio, в разделе [используйте Hive с HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="83bb4-140">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="83bb4-141">использовать язык toolearn о Pig tootransform данных см. в разделе [использование Pig с HDInsight][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="83bb4-141">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="83bb4-142">в разделе toolearn о MapReduce программы toowrite способом обработки данных в Hadoop, [используйте MapReduce с HDInsight][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="83bb4-142">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="83bb4-143">в разделе toolearn об использовании hello средства HDInsight для Visual Studio tooanalyze данных на HDInsight, [приступить к работе со средствами Visual Studio Hadoop для HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83bb4-143">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="83bb4-144">Дополнительные сведения о хранением данных HDInsight toolearn или tooget данных в HDInsight, в статье hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="83bb4-144">toolearn more about how HDInsight stores data or how tooget data into HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="83bb4-145">Сведения о том, как HDInsight использует службу хранилища Azure, см. в статье [Использование HDFS-совместимой службы хранилища с Hadoop в HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="83bb4-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="83bb4-146">Сведения о том, как tooHDInsight tooupload данных, в разделе [отправить данные tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="83bb4-146">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="83bb4-147">toolearn Дополнительные сведения о создании и управлении кластер HDInsight см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="83bb4-147">toolearn more about creating or managing an HDInsight cluster, see hello following articles:</span></span>

* <span data-ttu-id="83bb4-148">toolearn об управлении кластера HDInsight под управлением Linux, в разделе [управления HDInsight кластеры, использующие Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="83bb4-148">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="83bb4-149">toolearn больше о параметрах hello, можно выбрать при создании кластера HDInsight, в разделе [Создание HDInsight в Linux с использованием пользовательских параметров](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="83bb4-149">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="83bb4-150">Если вы знакомы с Linux и Hadoop, но хотите tooknow подробные сведения о Hadoop в hello HDInsight, см. раздел [работу с HDInsight в Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="83bb4-150">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="83bb4-151">Эта статья содержит следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="83bb4-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="83bb4-152">URL-адреса для служб, размещенных в кластере hello, например, Ambari и WebHCat</span><span class="sxs-lookup"><span data-stu-id="83bb4-152">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="83bb4-153">Hello расположение файлов Hadoop и примеры hello локальной файловой системе</span><span class="sxs-lookup"><span data-stu-id="83bb4-153">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="83bb4-154">Hello использование служб Azure хранилища (WASB) вместо HDFS в качестве хранилища данных по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="83bb4-154">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


