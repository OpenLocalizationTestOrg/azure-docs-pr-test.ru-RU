---
title: "Настройка репликации кластера HBase в виртуальных сетях — Azure | Документы Майкрософт"
description: "Сведения о том, как настроить репликацию HBase для балансировки нагрузки, обеспечения высокого уровня доступности, переноса или обновления с одной версии HDInsight на другую без простоя и аварийного восстановления."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 895709391486acb4a9d7a54ef046956539913f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="a91d2-103">Настройка репликации кластера HBase в виртуальных сетях</span><span class="sxs-lookup"><span data-stu-id="a91d2-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="a91d2-104">В этой статье вы узнаете, как настроить репликацию HBase в одной или между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="a91d2-104">Learn how to configure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="a91d2-105">Репликация кластера использует методологию source-push.</span><span class="sxs-lookup"><span data-stu-id="a91d2-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="a91d2-106">Кластер HBase может быть исходным, кластером назначения или выполнять обе роли одновременно.</span><span class="sxs-lookup"><span data-stu-id="a91d2-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="a91d2-107">Репликация выполняется асинхронно, а целью репликации в конечном итоге является согласованность.</span><span class="sxs-lookup"><span data-stu-id="a91d2-107">Replication is asynchronous, and the goal of replication is eventual consistency.</span></span> <span data-ttu-id="a91d2-108">При получении источником изменения в семействе столбцов с включенной репликацией такое изменение распространяется на все кластеры назначения.</span><span class="sxs-lookup"><span data-stu-id="a91d2-108">When the source receives an edit to a column family with replication enabled, that edit is propagated to all destination clusters.</span></span> <span data-ttu-id="a91d2-109">При репликации данных с одного кластера на другой исходный кластер и все кластеры, которые уже потребили данные, отслеживаются для предотвращения циклических репликаций.</span><span class="sxs-lookup"><span data-stu-id="a91d2-109">When data is replicated from one cluster to another, the source cluster and all clusters that have already consumed the data are tracked to prevent replication loops.</span></span>

<span data-ttu-id="a91d2-110">В этом руководстве показано, как настроить репликацию "источник — назначение".</span><span class="sxs-lookup"><span data-stu-id="a91d2-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="a91d2-111">Другие топологии кластеров см. в документе [Справочное руководство по Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="a91d2-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="a91d2-112">Примеры использования репликации HBase для одной виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="a91d2-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="a91d2-113">Балансировка нагрузки, например выполнения проверки или заданий MapReduce в целевом кластере и приема данных на исходном кластере.</span><span class="sxs-lookup"><span data-stu-id="a91d2-113">Load balancing--for example, running scans or MapReduce jobs on the destination cluster and ingesting data on the source cluster</span></span>
* <span data-ttu-id="a91d2-114">высокую доступность;</span><span class="sxs-lookup"><span data-stu-id="a91d2-114">High availability</span></span>
* <span data-ttu-id="a91d2-115">Перенос данных из одного кластера HBase в другой.</span><span class="sxs-lookup"><span data-stu-id="a91d2-115">Migrating data from one HBase cluster to another</span></span>
* <span data-ttu-id="a91d2-116">Обновление кластера Azure HDInsight до другой версии.</span><span class="sxs-lookup"><span data-stu-id="a91d2-116">Upgrading an Azure HDInsight cluster from one version to another</span></span>

<span data-ttu-id="a91d2-117">Примеры использования репликации HBase для двух виртуальных сетей:</span><span class="sxs-lookup"><span data-stu-id="a91d2-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="a91d2-118">Аварийное восстановление</span><span class="sxs-lookup"><span data-stu-id="a91d2-118">Disaster recovery</span></span>
* <span data-ttu-id="a91d2-119">Балансировка нагрузки и секционирование приложения.</span><span class="sxs-lookup"><span data-stu-id="a91d2-119">Load balancing and partitioning the application</span></span>
* <span data-ttu-id="a91d2-120">высокую доступность;</span><span class="sxs-lookup"><span data-stu-id="a91d2-120">High availability</span></span>

<span data-ttu-id="a91d2-121">Репликация кластеров осуществляется с помощью скриптов [действий сценария](hdinsight-hadoop-customize-cluster-linux.md), которые можно найти на веб-сайте [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="a91d2-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a91d2-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a91d2-122">Prerequisites</span></span>
<span data-ttu-id="a91d2-123">Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="a91d2-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="a91d2-124">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a91d2-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-the-environments"></a><span data-ttu-id="a91d2-125">Настройка сред</span><span class="sxs-lookup"><span data-stu-id="a91d2-125">Configure the environments</span></span>

<span data-ttu-id="a91d2-126">Доступны три варианта конфигурации:</span><span class="sxs-lookup"><span data-stu-id="a91d2-126">There are three possible configurations:</span></span>

- <span data-ttu-id="a91d2-127">два кластера HBase в одной виртуальной сети Azure;</span><span class="sxs-lookup"><span data-stu-id="a91d2-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="a91d2-128">два кластера HBase в двух виртуальных сетях в одном регионе;</span><span class="sxs-lookup"><span data-stu-id="a91d2-128">Two HBase clusters in two different virtual networks in the same region</span></span>
- <span data-ttu-id="a91d2-129">два кластера HBase в двух виртуальных сетях в двух регионах (георепликация).</span><span class="sxs-lookup"><span data-stu-id="a91d2-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="a91d2-130">Чтобы упростить настройку сред, мы создали несколько [шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a91d2-130">To make it easier to configure the environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="a91d2-131">Если вы предпочитаете настраивать среды с помощью других методов, см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="a91d2-131">If you prefer to configure the environments by using other methods, see:</span></span>

- [<span data-ttu-id="a91d2-132">Создание кластеров Hadoop под управлением Linux в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a91d2-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="a91d2-133">Создание кластеров HBase в виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="a91d2-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="a91d2-134">Настройка одной виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="a91d2-134">Configure one virtual network</span></span>

<span data-ttu-id="a91d2-135">Чтобы создать два кластера HBase в одной виртуальной сети, нажмите расположенную ниже кнопку.</span><span class="sxs-lookup"><span data-stu-id="a91d2-135">Click the following image to create two HBase clusters in the same virtual network.</span></span> <span data-ttu-id="a91d2-136">Шаблон хранится среди [шаблонов быстрого запуска Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="a91d2-136">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

### <a name="configure-two-virtual-networks-in-the-same-region"></a><span data-ttu-id="a91d2-137">Настройка двух виртуальных сетей в одном регионе</span><span class="sxs-lookup"><span data-stu-id="a91d2-137">Configure two virtual networks in the same region</span></span>

<span data-ttu-id="a91d2-138">Чтобы создать две виртуальные сети с пиринговой связью и два кластера HBase в одном регионе, нажмите расположенную ниже кнопку.</span><span class="sxs-lookup"><span data-stu-id="a91d2-138">Click the following image to create two virtual networks with VNet peering and two HBase clusters in the same region.</span></span> <span data-ttu-id="a91d2-139">Шаблон хранится среди [шаблонов быстрого запуска Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="a91d2-139">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>



<span data-ttu-id="a91d2-140">В этом случае необходима [пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a91d2-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="a91d2-141">Этот шаблон включает пиринговую связь между виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="a91d2-141">The template enables VNet peering.</span></span>   

<span data-ttu-id="a91d2-142">Репликация HBase использует IP-адреса виртуальных машин ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="a91d2-142">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="a91d2-143">Необходимо настроить статические IP-адреса для узлов назначения ZooKeeper HBase.</span><span class="sxs-lookup"><span data-stu-id="a91d2-143">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="a91d2-144">**Настройка статических IP-адресов**</span><span class="sxs-lookup"><span data-stu-id="a91d2-144">**To configure static IP addresses**</span></span>

1. <span data-ttu-id="a91d2-145">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a91d2-145">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a91d2-146">В меню слева щелкните **Группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-146">From the left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="a91d2-147">Выберите группу ресурсов, содержащую кластер назначения HBase.</span><span class="sxs-lookup"><span data-stu-id="a91d2-147">Click your resource group that contains the destination HBase cluster.</span></span> <span data-ttu-id="a91d2-148">Это группа ресурсов, указанная при использовании шаблона Resource Manager для создания среды.</span><span class="sxs-lookup"><span data-stu-id="a91d2-148">This is the resource group that you specified when you used the Resource Manager template to create the environment.</span></span> <span data-ttu-id="a91d2-149">Для сужения списка можно использовать фильтр.</span><span class="sxs-lookup"><span data-stu-id="a91d2-149">You can use the filter to narrow down the list.</span></span> <span data-ttu-id="a91d2-150">Вы увидите список ресурсов, содержащий две виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="a91d2-150">You can see a list of resources that contains the two virtual networks.</span></span>
4. <span data-ttu-id="a91d2-151">Выберите виртуальную сеть, содержащую кластер назначения HBase.</span><span class="sxs-lookup"><span data-stu-id="a91d2-151">Click the virtual network that contains the destination HBase cluster.</span></span> <span data-ttu-id="a91d2-152">Например, щелкните **xxxx-vnet2**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="a91d2-153">Вы увидите три устройства с именами, которые начинаются с **nic-zookeepermode -**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="a91d2-154">Это три виртуальные машины ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="a91d2-154">Those devices are the three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="a91d2-155">Щелкните одну из виртуальных машин ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="a91d2-155">Click one of the ZooKeeper VMs.</span></span>
6. <span data-ttu-id="a91d2-156">Щелкните **IP configurations** (Конфигурации IP).</span><span class="sxs-lookup"><span data-stu-id="a91d2-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="a91d2-157">В списке выберите **ipConfig1**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-157">Click **ipConfig1** from the list.</span></span>
8. <span data-ttu-id="a91d2-158">Щелкните **Статический** и введите фактический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a91d2-158">Click **Static**, and write down the actual IP address.</span></span> <span data-ttu-id="a91d2-159">IP-адрес потребуется вам при выполнении действия сценария для включения репликации.</span><span class="sxs-lookup"><span data-stu-id="a91d2-159">You will need the IP address when you run the script action to enable replication.</span></span>

  ![репликация HDInsight HBase, статический IP-адрес узла ZooKeeper](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="a91d2-161">Повторите шаг 6, чтобы задать статический IP-адрес для двух остальных узлов ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="a91d2-161">Repeat step 6 to set the static IP address for the other two ZooKeeper nodes.</span></span>

<span data-ttu-id="a91d2-162">Для сценария между виртуальными сетями необходимо использовать параметр **-ip** при вызове действия сценария **hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-162">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="a91d2-163">Настройка двух виртуальных сетей в двух регионах</span><span class="sxs-lookup"><span data-stu-id="a91d2-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="a91d2-164">Чтобы создать две виртуальные сети в двух регионах, нажмите расположенную ниже кнопку.</span><span class="sxs-lookup"><span data-stu-id="a91d2-164">Click the following image to create two virtual networks in two different regions.</span></span> <span data-ttu-id="a91d2-165">Шаблон хранится в общедоступном контейнере больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="a91d2-165">The template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

<span data-ttu-id="a91d2-166">Создайте VPN-шлюз между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="a91d2-166">Create a VPN gateway between the two virtual networks.</span></span> <span data-ttu-id="a91d2-167">Инструкции см. в статье [Создание виртуальной сети с подключением типа "сеть — сеть" с помощью портала Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a91d2-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="a91d2-168">Репликация HBase использует IP-адреса виртуальных машин ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="a91d2-168">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="a91d2-169">Необходимо настроить статические IP-адреса для узлов назначения ZooKeeper HBase.</span><span class="sxs-lookup"><span data-stu-id="a91d2-169">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="a91d2-170">Сведения о настройке статического IP-адреса см. в разделе "Настройка двух виртуальных сетей в одном регионе" этой статьи.</span><span class="sxs-lookup"><span data-stu-id="a91d2-170">To configure static IP, see the "Configure two virtual networks in the same region" section in this article.</span></span>

<span data-ttu-id="a91d2-171">Для сценария между виртуальными сетями необходимо использовать параметр **-ip** при вызове действия сценария **hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-171">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="a91d2-172">Загрузка тестовых данных</span><span class="sxs-lookup"><span data-stu-id="a91d2-172">Load test data</span></span>

<span data-ttu-id="a91d2-173">При репликации кластера необходимо указать реплицируемые таблицы.</span><span class="sxs-lookup"><span data-stu-id="a91d2-173">When you replicate a cluster, you must specify the tables to replicate.</span></span> <span data-ttu-id="a91d2-174">В этом разделе вы загрузите данные в исходный кластер.</span><span class="sxs-lookup"><span data-stu-id="a91d2-174">In this section, you will load some data into the source cluster.</span></span> <span data-ttu-id="a91d2-175">В следующем разделе вы включите репликацию между двумя кластерами.</span><span class="sxs-lookup"><span data-stu-id="a91d2-175">In the next section, you will enable replication between the two clusters.</span></span>

<span data-ttu-id="a91d2-176">Чтобы создать таблицу **контактов** и вставить в нее данные, следуйте инструкциям, приведенным в статье [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Linux в HDInsight](hdinsight-hbase-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a91d2-176">Follow the instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) to create a **Contacts** table and insert some data into the table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="a91d2-177">Включение репликации</span><span class="sxs-lookup"><span data-stu-id="a91d2-177">Enable replication</span></span>

<span data-ttu-id="a91d2-178">Ниже показано, как вызвать скрипт действия сценария на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a91d2-178">The following steps show how to call the script action script from the Azure portal.</span></span> <span data-ttu-id="a91d2-179">Дополнительные сведения о том, как выполнить действие сценария с помощью Azure PowerShell и интерфейса командной строки Azure, см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a91d2-179">For running a script action by using Azure PowerShell and the Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="a91d2-180">**Включение репликации HBase на портале Azure**</span><span class="sxs-lookup"><span data-stu-id="a91d2-180">**To enable HBase replication from the Azure portal**</span></span>

1. <span data-ttu-id="a91d2-181">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a91d2-181">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a91d2-182">Откройте исходный кластер HBase.</span><span class="sxs-lookup"><span data-stu-id="a91d2-182">Open the source HBase cluster.</span></span>
3. <span data-ttu-id="a91d2-183">В меню кластера щелкните **Действия скрипта**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-183">From the cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="a91d2-184">В верхней части колонки щелкните **Отправить новое**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-184">Click **Submit New** from the top of the blade.</span></span>
5. <span data-ttu-id="a91d2-185">Выберите или введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="a91d2-185">Select or enter the following information:</span></span>

  - <span data-ttu-id="a91d2-186">**Имя:** введите **Включение репликации**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="a91d2-187">**URL-адрес bash-скрипта:** введите **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="a91d2-188">**Головной узел:** выбран.</span><span class="sxs-lookup"><span data-stu-id="a91d2-188">**Head**: Selected.</span></span> <span data-ttu-id="a91d2-189">Отмените выбор других типов узлов.</span><span class="sxs-lookup"><span data-stu-id="a91d2-189">Clear the other node types.</span></span>
  - <span data-ttu-id="a91d2-190">**Параметры:** параметры в следующем примере позволяют включить репликацию для всех существующих таблиц и копировать все данные из исходного кластера в целевой.</span><span class="sxs-lookup"><span data-stu-id="a91d2-190">**Parameters**: The following sample parameters enable replication for all the existing tables and copy all the data from the source cluster to the destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="a91d2-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-191">Click **Create**.</span></span> <span data-ttu-id="a91d2-192">Выполнение скрипта может занять некоторое время, особенно при использовании аргумента -copydata.</span><span class="sxs-lookup"><span data-stu-id="a91d2-192">The script can take some time, especially when the -copydata argument is used.</span></span>

<span data-ttu-id="a91d2-193">Ниже приведены обязательные аргументы.</span><span class="sxs-lookup"><span data-stu-id="a91d2-193">Required arguments:</span></span>

|<span data-ttu-id="a91d2-194">Имя</span><span class="sxs-lookup"><span data-stu-id="a91d2-194">Name</span></span>|<span data-ttu-id="a91d2-195">Описание</span><span class="sxs-lookup"><span data-stu-id="a91d2-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="a91d2-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="a91d2-196">-s, --src-cluster</span></span> | <span data-ttu-id="a91d2-197">Укажите DNS-имя исходного кластера HBase,</span><span class="sxs-lookup"><span data-stu-id="a91d2-197">Specify the DNS name of the source HBase cluster.</span></span> <span data-ttu-id="a91d2-198">например -s hbsrccluster, --src-cluster=hbsrccluster.</span><span class="sxs-lookup"><span data-stu-id="a91d2-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="a91d2-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="a91d2-199">-d, --dst-cluster</span></span> | <span data-ttu-id="a91d2-200">Укажите DNS-имя кластера назначения (реплики) HBase,</span><span class="sxs-lookup"><span data-stu-id="a91d2-200">Specify the DNS name of the destination (replica) HBase cluster.</span></span> <span data-ttu-id="a91d2-201">например -s dsthbcluster, --src-cluster=dsthbcluster.</span><span class="sxs-lookup"><span data-stu-id="a91d2-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="a91d2-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="a91d2-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="a91d2-203">Укажите пароль администратора для Ambari в исходном кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="a91d2-203">Specify the admin password for Ambari on the source HBase cluster.</span></span> |
|<span data-ttu-id="a91d2-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="a91d2-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="a91d2-205">Укажите пароль администратора для Ambari в целевом кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="a91d2-205">Specify the admin password for Ambari on the destination HBase cluster.</span></span>|

<span data-ttu-id="a91d2-206">Необязательные аргументы для этой команды.</span><span class="sxs-lookup"><span data-stu-id="a91d2-206">Optional arguments:</span></span>

|<span data-ttu-id="a91d2-207">Имя</span><span class="sxs-lookup"><span data-stu-id="a91d2-207">Name</span></span>|<span data-ttu-id="a91d2-208">Описание</span><span class="sxs-lookup"><span data-stu-id="a91d2-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="a91d2-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="a91d2-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="a91d2-210">Укажите имя пользователя-администратора для Ambari в исходном кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="a91d2-210">Specify the admin username for Ambari on the source HBase cluster.</span></span> <span data-ttu-id="a91d2-211">Значение по умолчанию — **admin**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-211">The default value is **admin**.</span></span> |
|<span data-ttu-id="a91d2-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="a91d2-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="a91d2-213">Укажите имя пользователя-администратора для Ambari в целевом кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="a91d2-213">Specify the admin username for Ambari on the destination HBase cluster.</span></span> <span data-ttu-id="a91d2-214">Значение по умолчанию — **admin**.</span><span class="sxs-lookup"><span data-stu-id="a91d2-214">The default value is **admin**.</span></span> |
|<span data-ttu-id="a91d2-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="a91d2-215">-t, --table-list</span></span> | <span data-ttu-id="a91d2-216">Укажите таблицы для репликации,</span><span class="sxs-lookup"><span data-stu-id="a91d2-216">Specify the tables to be replicated.</span></span> <span data-ttu-id="a91d2-217">например --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="a91d2-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="a91d2-218">Если не указать таблицы, будут реплицированы все существующие таблицы HBase.</span><span class="sxs-lookup"><span data-stu-id="a91d2-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="a91d2-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="a91d2-219">-m, --machine</span></span> | <span data-ttu-id="a91d2-220">Укажите головной узел, на котором будет выполняться действие сценария.</span><span class="sxs-lookup"><span data-stu-id="a91d2-220">Specify the head node where the script action will run.</span></span> <span data-ttu-id="a91d2-221">Значение должно быть hn1 или hn0.</span><span class="sxs-lookup"><span data-stu-id="a91d2-221">The value is either hn1 or hn0.</span></span> <span data-ttu-id="a91d2-222">Так как узел hn0 обычно более загружен, рекомендуется использовать hn1.</span><span class="sxs-lookup"><span data-stu-id="a91d2-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="a91d2-223">Используйте этот параметр при запуске скрипта $0 как действия сценария из портала HDInsight или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a91d2-223">You use this option when you're running the $0 script as a script action from the HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="a91d2-224">-ip</span><span class="sxs-lookup"><span data-stu-id="a91d2-224">-ip</span></span> | <span data-ttu-id="a91d2-225">Этот аргумент является обязательным, если вы включаете репликацию между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="a91d2-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="a91d2-226">Этот аргумент действует как переключатель на использование статических IP-адресов узлов ZooKeeper реплицированных кластеров вместо полных доменных имен.</span><span class="sxs-lookup"><span data-stu-id="a91d2-226">This argument acts as a switch to use the static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="a91d2-227">Статические IP-адреса должны быть предварительно настроены перед включением репликации.</span><span class="sxs-lookup"><span data-stu-id="a91d2-227">The static IPs need to be preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="a91d2-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="a91d2-228">-cp, -copydata</span></span> | <span data-ttu-id="a91d2-229">Включает перенос существующих данных для таблиц, где включена репликация.</span><span class="sxs-lookup"><span data-stu-id="a91d2-229">Enable the migration of existing data on the tables where replication is enabled.</span></span> |
|<span data-ttu-id="a91d2-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="a91d2-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="a91d2-231">Включает репликацию для системных таблиц Phoenix.</span><span class="sxs-lookup"><span data-stu-id="a91d2-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="a91d2-232">*Используйте этот параметр с осторожностью.*</span><span class="sxs-lookup"><span data-stu-id="a91d2-232">*Use this option with caution.*</span></span> <span data-ttu-id="a91d2-233">Рекомендуется повторно создать таблицы Phoenix в реплицированных кластерах перед использованием этого скрипта.</span><span class="sxs-lookup"><span data-stu-id="a91d2-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="a91d2-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="a91d2-234">-h, --help</span></span> | <span data-ttu-id="a91d2-235">Отображает сведения об использовании.</span><span class="sxs-lookup"><span data-stu-id="a91d2-235">Display usage information.</span></span> |

<span data-ttu-id="a91d2-236">Раздел [скрипта](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) print_usage() содержит подробное объяснение параметров.</span><span class="sxs-lookup"><span data-stu-id="a91d2-236">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="a91d2-237">После успешного развертывания действия сценария можно использовать протокол SSH, чтобы подключиться к кластеру назначения HBase и убедиться, что данные реплицированы.</span><span class="sxs-lookup"><span data-stu-id="a91d2-237">After the script action is successfully deployed, you can use SSH to connect to the destination HBase cluster, and verify the data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="a91d2-238">Сценарии репликации</span><span class="sxs-lookup"><span data-stu-id="a91d2-238">Replication scenarios</span></span>

<span data-ttu-id="a91d2-239">Ниже перечислены некоторые общие способы применения и используемые параметры.</span><span class="sxs-lookup"><span data-stu-id="a91d2-239">The following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="a91d2-240">**Включение репликации для всех таблиц между двумя кластерами.**</span><span class="sxs-lookup"><span data-stu-id="a91d2-240">**Enable replication on all tables between the two clusters**.</span></span> <span data-ttu-id="a91d2-241">Этот сценарий не требует копирования и переноса существующих данных в таблицах и не использует таблицы Phoenix.</span><span class="sxs-lookup"><span data-stu-id="a91d2-241">This scenario does not require the copy/migration of existing data on the tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="a91d2-242">Используйте следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="a91d2-242">Use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="a91d2-243">**Включение репликации для отдельных таблиц.**</span><span class="sxs-lookup"><span data-stu-id="a91d2-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="a91d2-244">Чтобы включить репликацию для table1, table2 и table3, используйте следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="a91d2-244">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="a91d2-245">**Включение репликации для отдельных таблиц и копирование существующих данных.**</span><span class="sxs-lookup"><span data-stu-id="a91d2-245">**Enable replication on specific tables and copy the existing data**.</span></span> <span data-ttu-id="a91d2-246">Чтобы включить репликацию для table1, table2 и table3, используйте следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="a91d2-246">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="a91d2-247">**Включение репликации для всех таблиц с репликацией метаданных Phoenix из источника в место назначения.**</span><span class="sxs-lookup"><span data-stu-id="a91d2-247">**Enable replication on all tables with replicating phoenix metadata from source to destination**.</span></span> <span data-ttu-id="a91d2-248">Репликация метаданных Phoenix работает не идеально, ее следует использовать с осторожностью.</span><span class="sxs-lookup"><span data-stu-id="a91d2-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="a91d2-249">Копирование и перенос данных</span><span class="sxs-lookup"><span data-stu-id="a91d2-249">Copy and migrate data</span></span>

<span data-ttu-id="a91d2-250">Существует два отдельных скрипта действия сценария для копирования или переноса данных после включения репликации:</span><span class="sxs-lookup"><span data-stu-id="a91d2-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="a91d2-251">[Скрипт для небольших таблиц](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (размером в несколько гигабайт, ожидаемое время копирования — менее часа).</span><span class="sxs-lookup"><span data-stu-id="a91d2-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected to finish in less than one hour)</span></span>

- <span data-ttu-id="a91d2-252">[Скрипт для больших таблиц](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (копирование занимает больше часа).</span><span class="sxs-lookup"><span data-stu-id="a91d2-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected to take longer than one hour to copy)</span></span>

<span data-ttu-id="a91d2-253">Можно выполнить процедуру, описанную в разделе [Включение репликации](#enable-replication), чтобы вызвать действие сценария со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="a91d2-253">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="a91d2-254">Раздел [скрипта](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) print_usage() содержит подробное описание параметров.</span><span class="sxs-lookup"><span data-stu-id="a91d2-254">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="a91d2-255">Сценарии</span><span class="sxs-lookup"><span data-stu-id="a91d2-255">Scenarios</span></span>

- <span data-ttu-id="a91d2-256">**Копирование определенных таблиц (test1, test2 и test3) для всех строк, измененных до настоящего момента (текущая отметка времени):**</span><span class="sxs-lookup"><span data-stu-id="a91d2-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="a91d2-257">или</span><span class="sxs-lookup"><span data-stu-id="a91d2-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="a91d2-258">**Копирование определенных таблиц с указанным интервалом времени:**</span><span class="sxs-lookup"><span data-stu-id="a91d2-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="a91d2-259">Отключение репликации</span><span class="sxs-lookup"><span data-stu-id="a91d2-259">Disable replication</span></span>

<span data-ttu-id="a91d2-260">Чтобы отключить репликацию, используйте другой скрипт действия сценария, расположенный на веб-сайте [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="a91d2-260">To disable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="a91d2-261">Можно выполнить процедуру, описанную в разделе [Включение репликации](#enable-replication), чтобы вызвать действие сценария со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="a91d2-261">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="a91d2-262">Раздел [скрипта](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) print_usage() содержит подробное объяснение параметров.</span><span class="sxs-lookup"><span data-stu-id="a91d2-262">The print_usage() section of the [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="a91d2-263">Сценарии</span><span class="sxs-lookup"><span data-stu-id="a91d2-263">Scenarios</span></span>

- <span data-ttu-id="a91d2-264">**Отключение репликации для всех таблиц:**</span><span class="sxs-lookup"><span data-stu-id="a91d2-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="a91d2-265">или</span><span class="sxs-lookup"><span data-stu-id="a91d2-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="a91d2-266">**Отключение репликации для определенных таблиц (table1, table2 и table3):**</span><span class="sxs-lookup"><span data-stu-id="a91d2-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="a91d2-267">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a91d2-267">Next steps</span></span>

<span data-ttu-id="a91d2-268">В этом руководстве вы изучили настройку репликации HBase между двумя центрами обработки данных.</span><span class="sxs-lookup"><span data-stu-id="a91d2-268">In this tutorial, you learned how to configure HBase replication across two datacenters.</span></span> <span data-ttu-id="a91d2-269">Для получения дополнительных сведений о HDInsight и HBase см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="a91d2-269">To learn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="a91d2-270">[Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Windows в HDInsight][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="a91d2-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="a91d2-271">[Что такое HBase в HDInsight: база данных NoSQL, которая предоставляет возможности, схожие с BigTable, для Hadoop][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="a91d2-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="a91d2-272">[Создание кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="a91d2-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="a91d2-273">[Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="a91d2-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="a91d2-274">[Анализ полученных с датчиков данных с использованием Apache Storm, концентратора событий и базы данных HBase в службе HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="a91d2-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
