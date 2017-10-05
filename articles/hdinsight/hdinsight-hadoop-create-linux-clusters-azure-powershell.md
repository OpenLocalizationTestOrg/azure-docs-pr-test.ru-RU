---
title: "Создание кластеров Hadoop с помощью PowerShell в Azure HDInsight | Документы Майкрософт"
description: "Узнайте, как создавать кластеры Hadoop, HBase, Storm или Spark на платформе Linux для HDInsight с помощью Azure PowerShell."
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
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="029da-103">Создание кластеров под управлением Linux в HDInsight с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="029da-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="029da-104">Azure PowerShell — это полнофункциональная среда сценариев, которую можно использовать для контроля и автоматизации развертывания и управления вашей рабочей нагрузкой в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="029da-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="029da-105">В этой статье содержится информация о том, как создать кластер HDInsight под управлением Linux с помощью Azure PowerShell,</span><span class="sxs-lookup"><span data-stu-id="029da-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="029da-106">а также приведен пример скрипта.</span><span class="sxs-lookup"><span data-stu-id="029da-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="029da-107">Оболочка Azure PowerShell доступна только для клиентов Windows.</span><span class="sxs-lookup"><span data-stu-id="029da-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="029da-108">Если вы используете клиент Linux, Unix или Mac OS X, сведения об использовании интерфейса командной строки Azure для создания кластера см. в статье [Создание кластеров под управлением Linux в HDInsight с помощью Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="029da-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="029da-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="029da-109">Prerequisites</span></span>
<span data-ttu-id="029da-110">Прежде чем следовать инструкциям в этой статье, необходимо подготовить следующее.</span><span class="sxs-lookup"><span data-stu-id="029da-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="029da-111">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="029da-111">An Azure subscription.</span></span> <span data-ttu-id="029da-112">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="029da-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="029da-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="029da-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="029da-114">Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="029da-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="029da-115">В описанных в этом документе инструкциях используются новые командлеты HDInsight, которые работают с Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="029da-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="029da-116">Чтобы установить последнюю версию Azure PowerShell, выполните действия из статьи [Установка и настройка Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="029da-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="029da-117">Если у вас есть сценарии, в которые нужно добавить новые командлеты, работающие с Azure Resource Manager, см. статью [Переход к средствам разработки на основе Azure Resource Manager для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="029da-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="029da-118">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="029da-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="029da-119">Для создания кластера HDInsight с помощью Azure PowerShell необходимо выполнить следующие процедуры:</span><span class="sxs-lookup"><span data-stu-id="029da-119">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="029da-120">создание группы ресурсов Azure;</span><span class="sxs-lookup"><span data-stu-id="029da-120">Create an Azure resource group</span></span>
* <span data-ttu-id="029da-121">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="029da-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="029da-122">Создание контейнера BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="029da-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="029da-123">Создание кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="029da-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="029da-124">Следующий сценарий демонстрирует создание нового кластера.</span><span class="sxs-lookup"><span data-stu-id="029da-124">The following script demonstrates how to create a new cluster:</span></span>

<span data-ttu-id="029da-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span><span class="sxs-lookup"><span data-stu-id="029da-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span></span>

<span data-ttu-id="029da-126">Значения, указываемые для входа в кластер, используются для создания учетной записи пользователя Hadoop в кластере.</span><span class="sxs-lookup"><span data-stu-id="029da-126">The values you specify for the cluster login are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="029da-127">Используйте эту учетную запись для подключения к службам, размещенным в кластере, например веб-интерфейсам пользователя или REST API.</span><span class="sxs-lookup"><span data-stu-id="029da-127">Use this account to connect to services hosted on the cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="029da-128">Значения, указываемые для пользователя SSH, используются для создания пользователя SSH в кластере.</span><span class="sxs-lookup"><span data-stu-id="029da-128">The values you specify for the SSH user are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="029da-129">Используйте эту учетную запись для запуска удаленного сеанса SSH в кластере и выполнения заданий.</span><span class="sxs-lookup"><span data-stu-id="029da-129">Use this account to start a remote SSH session on the cluster and run jobs.</span></span> <span data-ttu-id="029da-130">Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="029da-130">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="029da-131">Если вы планируете использовать более 32 узлов рабочей роли (при создании кластера или в ходе масштабирования после создания кластера), для головного узла потребуется минимум 8-ядерный процессор и 14 ГБ ОЗУ.</span><span class="sxs-lookup"><span data-stu-id="029da-131">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="029da-132">Дополнительные сведения о размерах узлов и их стоимости см. на странице с [ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="029da-132">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="029da-133">Операция создания кластера может занять до 20 минут.</span><span class="sxs-lookup"><span data-stu-id="029da-133">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="029da-134">Создание кластера: объект конфигурации</span><span class="sxs-lookup"><span data-stu-id="029da-134">Create cluster: Configuration object</span></span>

<span data-ttu-id="029da-135">Можно также создать объект конфигурации HDInsight с помощью командлета `New-AzureRmHDInsightClusterConfig`.</span><span class="sxs-lookup"><span data-stu-id="029da-135">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="029da-136">Затем можно изменить этот объект конфигурации, чтобы включить дополнительные параметры конфигурации для кластера.</span><span class="sxs-lookup"><span data-stu-id="029da-136">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="029da-137">Наконец, используйте параметр `-Config` командлета `New-AzureRmHDInsightCluster`, чтобы использовать эту конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="029da-137">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="029da-138">Приведенный ниже сценарий создает объект конфигурации для настройки R Server для типа кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="029da-138">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="029da-139">Конфигурация включает граничный узел, RStudio и дополнительную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="029da-139">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

<span data-ttu-id="029da-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span><span class="sxs-lookup"><span data-stu-id="029da-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span></span>

> [!WARNING]
> <span data-ttu-id="029da-141">Использование учетной записи хранения, расположение которой отличается от расположения кластера HDInsight, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="029da-141">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="029da-142">При использовании этого примера создайте дополнительную учетную запись хранения в том же расположении, что и сервер.</span><span class="sxs-lookup"><span data-stu-id="029da-142">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="029da-143">Настройка кластеров</span><span class="sxs-lookup"><span data-stu-id="029da-143">Customize clusters</span></span>

* <span data-ttu-id="029da-144">Ознакомьтесь с разделом [Настройка кластеров HDInsight с помощью службы начальной загрузки](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="029da-144">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="029da-145">См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="029da-145">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="029da-146">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="029da-146">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="029da-147">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="029da-147">Troubleshoot</span></span>

<span data-ttu-id="029da-148">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="029da-148">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="029da-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="029da-149">Next steps</span></span>

<span data-ttu-id="029da-150">Теперь, когда вы успешно создали кластер HDInsight, обратитесь к следующим ресурсам, чтобы научиться с ним работать.</span><span class="sxs-lookup"><span data-stu-id="029da-150">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="029da-151">Кластеры Hadoop</span><span class="sxs-lookup"><span data-stu-id="029da-151">Hadoop clusters</span></span>

* [<span data-ttu-id="029da-152">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="029da-152">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="029da-153">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="029da-153">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="029da-154">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="029da-154">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="029da-155">Кластеры HBase</span><span class="sxs-lookup"><span data-stu-id="029da-155">HBase clusters</span></span>

* [<span data-ttu-id="029da-156">Начало работы с HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="029da-156">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="029da-157">Разработка приложений Java для HBase в HDInsight</span><span class="sxs-lookup"><span data-stu-id="029da-157">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="029da-158">Кластеры Storm</span><span class="sxs-lookup"><span data-stu-id="029da-158">Storm clusters</span></span>

* [<span data-ttu-id="029da-159">Разработка приложений Java для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="029da-159">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="029da-160">Использование компонентов Python в Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="029da-160">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="029da-161">Развертывание и мониторинг топологий с помощью Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="029da-161">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="029da-162">Кластеры Spark</span><span class="sxs-lookup"><span data-stu-id="029da-162">Spark clusters</span></span>

* [<span data-ttu-id="029da-163">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="029da-163">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="029da-164">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="029da-164">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="029da-165">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="029da-165">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="029da-166">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="029da-166">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="029da-167">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="029da-167">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

