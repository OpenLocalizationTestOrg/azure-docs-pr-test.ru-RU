---
title: "кластеры Hadoop aaaCreate с помощью PowerShell, Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Hadoop, HBase, ураган или Spark кластеров в Linux для HDInsight с помощью Azure PowerShell."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="aa3b6-103">Создание кластеров под управлением Linux в HDInsight с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa3b6-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="aa3b6-104">Azure PowerShell — это мощная среда сценариев, можно использовать toocontrol и автоматизации развертывания hello и управления ими в Microsoft Azure рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="aa3b6-105">Этот документ содержит сведения о как кластер toocreate HDInsight под управлением Linux с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-105">This document provides information about how toocreate a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="aa3b6-106">а также приведен пример скрипта.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="aa3b6-107">Оболочка Azure PowerShell доступна только для клиентов Windows.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="aa3b6-108">Если вы используете клиент Linux, Unix или Mac OS X, см. раздел [создание кластера HDInsight под управлением Linux с помощью Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) сведения об использовании hello Azure CLI toocreate кластера.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using hello Azure CLI toocreate a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa3b6-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="aa3b6-109">Prerequisites</span></span>
<span data-ttu-id="aa3b6-110">Необходимо иметь следующие hello перед началом этой процедуры.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-110">You must have hello following before starting this procedure:</span></span>

* <span data-ttu-id="aa3b6-111">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-111">An Azure subscription.</span></span> <span data-ttu-id="aa3b6-112">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="aa3b6-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="aa3b6-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa3b6-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="aa3b6-114">Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="aa3b6-115">шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-115">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="aa3b6-116">Выполните шаги hello в [установите Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello последнюю версию Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-116">Please follow hello steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="aa3b6-117">При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-117">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="aa3b6-118">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="aa3b6-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="aa3b6-119">toocreate кластер HDInsight с помощью Azure PowerShell, необходимо выполнить hello следующих процедур:</span><span class="sxs-lookup"><span data-stu-id="aa3b6-119">toocreate an HDInsight cluster by using Azure PowerShell, you must complete hello following procedures:</span></span>

* <span data-ttu-id="aa3b6-120">создание группы ресурсов Azure;</span><span class="sxs-lookup"><span data-stu-id="aa3b6-120">Create an Azure resource group</span></span>
* <span data-ttu-id="aa3b6-121">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="aa3b6-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="aa3b6-122">Создание контейнера BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="aa3b6-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="aa3b6-123">Создание кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa3b6-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="aa3b6-124">Hello следующий сценарий демонстрирует, каким образом toocreate нового кластера:</span><span class="sxs-lookup"><span data-stu-id="aa3b6-124">hello following script demonstrates how toocreate a new cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

<span data-ttu-id="aa3b6-125">Hello значения, указываемые для имени входа кластера hello: hello используется toocreate учетной записи пользователя Hadoop для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-125">hello values you specify for hello cluster login are used toocreate hello Hadoop user account for hello cluster.</span></span> <span data-ttu-id="aa3b6-126">С помощью этой учетной записи tooservices tooconnect, размещенных в кластере hello, например веб-интерфейсы пользователя или API REST.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-126">Use this account tooconnect tooservices hosted on hello cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="aa3b6-127">значения Hello, указать для пользователя SSH hello, используется toocreate hello SSH пользователя для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-127">hello values you specify for hello SSH user are used toocreate hello SSH user for hello cluster.</span></span> <span data-ttu-id="aa3b6-128">Этот метод следует использовать учетную запись toostart удаленный сеанс SSH на кластере hello и запуска заданий.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-128">Use this account toostart a remote SSH session on hello cluster and run jobs.</span></span> <span data-ttu-id="aa3b6-129">Дополнительные сведения см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-129">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa3b6-130">Если планируется toouse более 32 рабочих узлов (или при создании кластера масштабирования hello кластера после создания), необходимо также указать размер головного узла с по крайней мере 8 ядер, 14 ГБ ОЗУ.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-130">If you plan toouse more than 32 worker nodes (either at cluster creation or by scaling hello cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="aa3b6-131">Дополнительные сведения о размерах узлов и их стоимости см. на странице с [ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="aa3b6-131">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="aa3b6-132">Он может занять toocreate минут too20 кластера.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-132">It can take up too20 minutes toocreate a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="aa3b6-133">Создание кластера: объект конфигурации</span><span class="sxs-lookup"><span data-stu-id="aa3b6-133">Create cluster: Configuration object</span></span>

<span data-ttu-id="aa3b6-134">Можно также создать объект конфигурации HDInsight с помощью командлета `New-AzureRmHDInsightClusterConfig`.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-134">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="aa3b6-135">Затем можно изменить этот конфигурации объекта tooenable Дополнительные параметры конфигурации для кластера.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-135">You can then modify this configuration object tooenable additional configuration options for your cluster.</span></span> <span data-ttu-id="aa3b6-136">Наконец, используйте hello `-Config` параметр hello `New-AzureRmHDInsightCluster` конфигурации hello toouse командлета.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-136">Finally, use hello `-Config` parameter of hello `New-AzureRmHDInsightCluster` cmdlet toouse hello configuration.</span></span>

<span data-ttu-id="aa3b6-137">Hello следующий скрипт создает tooconfigure объекта конфигурации сервера R на тип кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-137">hello following script creates a configuration object tooconfigure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="aa3b6-138">Hello настройку граничного узла, RStudio и дополнительная учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-138">hello configuration enables an edge node, RStudio, and an additional storage account.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> <span data-ttu-id="aa3b6-139">Использование учетной записи хранилища в другом месте, чем hello кластера HDInsight не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-139">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span> <span data-ttu-id="aa3b6-140">При использовании в этом примере, создать hello дополнительная учетная запись хранения в hello местоположения сервера hello.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-140">When using this example, create hello additional storage account in hello same location as hello server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="aa3b6-141">Настройка кластеров</span><span class="sxs-lookup"><span data-stu-id="aa3b6-141">Customize clusters</span></span>

* <span data-ttu-id="aa3b6-142">Ознакомьтесь с разделом [Настройка кластеров HDInsight с помощью службы начальной загрузки](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="aa3b6-142">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="aa3b6-143">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="aa3b6-143">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="aa3b6-144">Удалить кластер hello</span><span class="sxs-lookup"><span data-stu-id="aa3b6-144">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="aa3b6-145">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="aa3b6-145">Troubleshoot</span></span>

<span data-ttu-id="aa3b6-146">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="aa3b6-146">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa3b6-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aa3b6-147">Next steps</span></span>

<span data-ttu-id="aa3b6-148">Теперь, когда вы успешно создали кластер HDInsight, используйте следующие ресурсы toolearn как hello toowork с кластером.</span><span class="sxs-lookup"><span data-stu-id="aa3b6-148">Now that you have successfully created an HDInsight cluster, use hello following resources toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="aa3b6-149">Кластеры Hadoop</span><span class="sxs-lookup"><span data-stu-id="aa3b6-149">Hadoop clusters</span></span>

* [<span data-ttu-id="aa3b6-150">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa3b6-150">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="aa3b6-151">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa3b6-151">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="aa3b6-152">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa3b6-152">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="aa3b6-153">Кластеры HBase</span><span class="sxs-lookup"><span data-stu-id="aa3b6-153">HBase clusters</span></span>

* [<span data-ttu-id="aa3b6-154">Начало работы с HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa3b6-154">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="aa3b6-155">Разработка приложений Java для HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa3b6-155">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="aa3b6-156">Кластеры Storm</span><span class="sxs-lookup"><span data-stu-id="aa3b6-156">Storm clusters</span></span>

* [<span data-ttu-id="aa3b6-157">Разработка приложений Java для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa3b6-157">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="aa3b6-158">Использование компонентов Python в Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa3b6-158">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="aa3b6-159">Развертывание и мониторинг топологий с помощью Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa3b6-159">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="aa3b6-160">Кластеры Spark</span><span class="sxs-lookup"><span data-stu-id="aa3b6-160">Spark clusters</span></span>

* [<span data-ttu-id="aa3b6-161">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="aa3b6-161">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="aa3b6-162">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="aa3b6-162">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="aa3b6-163">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="aa3b6-163">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="aa3b6-164">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="aa3b6-164">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="aa3b6-165">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="aa3b6-165">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

