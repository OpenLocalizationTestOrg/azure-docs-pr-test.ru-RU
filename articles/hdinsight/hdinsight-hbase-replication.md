---
title: "репликация кластер HBase aaaConfigure внутри виртуальных сетей - Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure HBase репликации для балансировки нагрузки, высокий уровень доступности, миграция или обновление простоев из одного tooanother версии HDInsight и аварийного восстановления."
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
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="c4b72-103">Настройка репликации кластера HBase в виртуальных сетях</span><span class="sxs-lookup"><span data-stu-id="c4b72-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="c4b72-104">Узнайте, как tooconfigure HBase репликации в одной виртуальной сети (VNet) или между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="c4b72-104">Learn how tooconfigure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="c4b72-105">Репликация кластера использует методологию source-push.</span><span class="sxs-lookup"><span data-stu-id="c4b72-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="c4b72-106">Кластер HBase может быть исходным, кластером назначения или выполнять обе роли одновременно.</span><span class="sxs-lookup"><span data-stu-id="c4b72-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="c4b72-107">Репликация выполняется асинхронно, а целью hello репликации является окончательной согласованности.</span><span class="sxs-lookup"><span data-stu-id="c4b72-107">Replication is asynchronous, and hello goal of replication is eventual consistency.</span></span> <span data-ttu-id="c4b72-108">Получив исходный hello семейство изменить tooa столбца с включенной репликацией, изменению — распространенный tooall конечных кластеров.</span><span class="sxs-lookup"><span data-stu-id="c4b72-108">When hello source receives an edit tooa column family with replication enabled, that edit is propagated tooall destination clusters.</span></span> <span data-ttu-id="c4b72-109">При репликации данных из одного кластера tooanother hello исходного кластера и всех кластеров, которые уже потреблено hello данных являются отслеживаемых tooprevent циклов репликации.</span><span class="sxs-lookup"><span data-stu-id="c4b72-109">When data is replicated from one cluster tooanother, hello source cluster and all clusters that have already consumed hello data are tracked tooprevent replication loops.</span></span>

<span data-ttu-id="c4b72-110">В этом руководстве показано, как настроить репликацию "источник — назначение".</span><span class="sxs-lookup"><span data-stu-id="c4b72-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="c4b72-111">Другие топологии кластеров см. в документе [Справочное руководство по Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="c4b72-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="c4b72-112">Примеры использования репликации HBase для одной виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="c4b72-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="c4b72-113">Балансировка нагрузки — например, выполнение проверки одного или нескольких заданий MapReduce hello целевом кластере и передаче данных на исходном кластере hello</span><span class="sxs-lookup"><span data-stu-id="c4b72-113">Load balancing--for example, running scans or MapReduce jobs on hello destination cluster and ingesting data on hello source cluster</span></span>
* <span data-ttu-id="c4b72-114">высокую доступность;</span><span class="sxs-lookup"><span data-stu-id="c4b72-114">High availability</span></span>
* <span data-ttu-id="c4b72-115">Перенос данных из одного tooanother кластер HBase</span><span class="sxs-lookup"><span data-stu-id="c4b72-115">Migrating data from one HBase cluster tooanother</span></span>
* <span data-ttu-id="c4b72-116">Обновление кластера Azure HDInsight с одной версии tooanother</span><span class="sxs-lookup"><span data-stu-id="c4b72-116">Upgrading an Azure HDInsight cluster from one version tooanother</span></span>

<span data-ttu-id="c4b72-117">Примеры использования репликации HBase для двух виртуальных сетей:</span><span class="sxs-lookup"><span data-stu-id="c4b72-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="c4b72-118">Аварийное восстановление</span><span class="sxs-lookup"><span data-stu-id="c4b72-118">Disaster recovery</span></span>
* <span data-ttu-id="c4b72-119">Балансировка нагрузки и секционирования приложения hello</span><span class="sxs-lookup"><span data-stu-id="c4b72-119">Load balancing and partitioning hello application</span></span>
* <span data-ttu-id="c4b72-120">высокую доступность;</span><span class="sxs-lookup"><span data-stu-id="c4b72-120">High availability</span></span>

<span data-ttu-id="c4b72-121">Репликация кластеров осуществляется с помощью скриптов [действий сценария](hdinsight-hadoop-customize-cluster-linux.md), которые можно найти на веб-сайте [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="c4b72-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4b72-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c4b72-122">Prerequisites</span></span>
<span data-ttu-id="c4b72-123">Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b72-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="c4b72-124">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c4b72-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-hello-environments"></a><span data-ttu-id="c4b72-125">Настройка сред hello</span><span class="sxs-lookup"><span data-stu-id="c4b72-125">Configure hello environments</span></span>

<span data-ttu-id="c4b72-126">Доступны три варианта конфигурации:</span><span class="sxs-lookup"><span data-stu-id="c4b72-126">There are three possible configurations:</span></span>

- <span data-ttu-id="c4b72-127">два кластера HBase в одной виртуальной сети Azure;</span><span class="sxs-lookup"><span data-stu-id="c4b72-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="c4b72-128">Два HBase кластеров в двух разных виртуальных сетей в hello одного региона</span><span class="sxs-lookup"><span data-stu-id="c4b72-128">Two HBase clusters in two different virtual networks in hello same region</span></span>
- <span data-ttu-id="c4b72-129">два кластера HBase в двух виртуальных сетях в двух регионах (георепликация).</span><span class="sxs-lookup"><span data-stu-id="c4b72-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="c4b72-130">toomake его проще tooconfigure hello средах, мы создали некоторые [шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4b72-130">toomake it easier tooconfigure hello environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="c4b72-131">Если вы предпочитаете tooconfigure hello сред с помощью других методов, см.:</span><span class="sxs-lookup"><span data-stu-id="c4b72-131">If you prefer tooconfigure hello environments by using other methods, see:</span></span>

- [<span data-ttu-id="c4b72-132">Создание кластеров Hadoop под управлением Linux в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4b72-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="c4b72-133">Создание кластеров HBase в виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="c4b72-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="c4b72-134">Настройка одной виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="c4b72-134">Configure one virtual network</span></span>

<span data-ttu-id="c4b72-135">Выберите следующие изображения toocreate HBase кластерами в hello hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c4b72-135">Click hello following image toocreate two HBase clusters in hello same virtual network.</span></span> <span data-ttu-id="c4b72-136">Hello шаблон хранится в [шаблоны быстрый запуск Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="c4b72-136">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a><span data-ttu-id="c4b72-137">Настройка двух виртуальных сетей в hello одного региона</span><span class="sxs-lookup"><span data-stu-id="c4b72-137">Configure two virtual networks in hello same region</span></span>

<span data-ttu-id="c4b72-138">Выберите следующие изображения toocreate двух виртуальных сетей с пиринга виртуальной сети и два кластера HBase в hello hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="c4b72-138">Click hello following image toocreate two virtual networks with VNet peering and two HBase clusters in hello same region.</span></span> <span data-ttu-id="c4b72-139">Hello шаблон хранится в [шаблоны быстрый запуск Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="c4b72-139">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



<span data-ttu-id="c4b72-140">В этом случае необходима [пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4b72-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="c4b72-141">Hello шаблон позволяет пиринг виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c4b72-141">hello template enables VNet peering.</span></span>   

<span data-ttu-id="c4b72-142">Репликация HBase использует IP-адреса виртуальных машин ZooKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-142">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="c4b72-143">Необходимо настроить статические IP-адреса для узлов HBase ZooKeeper hello назначения.</span><span class="sxs-lookup"><span data-stu-id="c4b72-143">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="c4b72-144">**tooconfigure статические IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="c4b72-144">**tooconfigure static IP addresses**</span></span>

1. <span data-ttu-id="c4b72-145">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4b72-145">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c4b72-146">Hello в левом меню, щелкните **групп ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-146">From hello left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="c4b72-147">Выберите группу ресурсов, содержащий hello целевой кластер HBase.</span><span class="sxs-lookup"><span data-stu-id="c4b72-147">Click your resource group that contains hello destination HBase cluster.</span></span> <span data-ttu-id="c4b72-148">Это группа ресурсов hello, указанный вами при использовании среды hello toocreate шаблонов диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-148">This is hello resource group that you specified when you used hello Resource Manager template toocreate hello environment.</span></span> <span data-ttu-id="c4b72-149">Можно использовать toonarrow фильтра hello списку hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-149">You can use hello filter toonarrow down hello list.</span></span> <span data-ttu-id="c4b72-150">Вы увидите список ресурсов, содержащий hello двух виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="c4b72-150">You can see a list of resources that contains hello two virtual networks.</span></span>
4. <span data-ttu-id="c4b72-151">Щелкните hello виртуальной сети, содержащей hello целевой кластер HBase.</span><span class="sxs-lookup"><span data-stu-id="c4b72-151">Click hello virtual network that contains hello destination HBase cluster.</span></span> <span data-ttu-id="c4b72-152">Например, щелкните **xxxx-vnet2**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="c4b72-153">Вы увидите три устройства с именами, которые начинаются с **nic-zookeepermode -**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="c4b72-154">Эти устройства, hello трех ZooKeeper ВМ.</span><span class="sxs-lookup"><span data-stu-id="c4b72-154">Those devices are hello three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="c4b72-155">Выберите один из виртуальных машин ZooKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-155">Click one of hello ZooKeeper VMs.</span></span>
6. <span data-ttu-id="c4b72-156">Щелкните **IP configurations** (Конфигурации IP).</span><span class="sxs-lookup"><span data-stu-id="c4b72-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="c4b72-157">Нажмите кнопку **ipConfig1** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-157">Click **ipConfig1** from hello list.</span></span>
8. <span data-ttu-id="c4b72-158">Нажмите кнопку **статических**и запишите hello фактический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c4b72-158">Click **Static**, and write down hello actual IP address.</span></span> <span data-ttu-id="c4b72-159">Необходимо будет hello IP-адрес при запуске действия tooenable hello сценария репликации.</span><span class="sxs-lookup"><span data-stu-id="c4b72-159">You will need hello IP address when you run hello script action tooenable replication.</span></span>

  ![репликация HDInsight HBase, статический IP-адрес узла ZooKeeper](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="c4b72-161">Повторите шаг 6 tooset hello статический IP-адрес для hello двух остальных узлов ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="c4b72-161">Repeat step 6 tooset hello static IP address for hello other two ZooKeeper nodes.</span></span>

<span data-ttu-id="c4b72-162">Для сценария виртуальной сети между hello, необходимо использовать hello **- ip** переключение при вызове hello **hdi_enable_replication.sh** записать действие в скрипт.</span><span class="sxs-lookup"><span data-stu-id="c4b72-162">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="c4b72-163">Настройка двух виртуальных сетей в двух регионах</span><span class="sxs-lookup"><span data-stu-id="c4b72-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="c4b72-164">Щелкните hello после изображения toocreate двух виртуальных сетей в двух разных регионах.</span><span class="sxs-lookup"><span data-stu-id="c4b72-164">Click hello following image toocreate two virtual networks in two different regions.</span></span> <span data-ttu-id="c4b72-165">Hello шаблон хранится в открытый контейнер больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b72-165">hello template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

<span data-ttu-id="c4b72-166">Создайте шлюз VPN между двумя виртуальными сетями hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-166">Create a VPN gateway between hello two virtual networks.</span></span> <span data-ttu-id="c4b72-167">Инструкции см. в статье [Создание виртуальной сети с подключением типа "сеть — сеть" с помощью портала Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4b72-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="c4b72-168">Репликация HBase использует IP-адреса виртуальных машин ZooKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-168">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="c4b72-169">Необходимо настроить статические IP-адреса для узлов HBase ZooKeeper hello назначения.</span><span class="sxs-lookup"><span data-stu-id="c4b72-169">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="c4b72-170">tooconfigure статический IP-адрес см. раздел «Настройка двух виртуальных сетей в hello одного региона» hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c4b72-170">tooconfigure static IP, see hello "Configure two virtual networks in hello same region" section in this article.</span></span>

<span data-ttu-id="c4b72-171">Для сценария виртуальной сети между hello, необходимо использовать hello **- ip** переключение при вызове hello **hdi_enable_replication.sh** записать действие в скрипт.</span><span class="sxs-lookup"><span data-stu-id="c4b72-171">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="c4b72-172">Загрузка тестовых данных</span><span class="sxs-lookup"><span data-stu-id="c4b72-172">Load test data</span></span>

<span data-ttu-id="c4b72-173">При репликации кластера, необходимо указать tooreplicate таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-173">When you replicate a cluster, you must specify hello tables tooreplicate.</span></span> <span data-ttu-id="c4b72-174">В этом разделе будет загружать некоторые данные в исходном кластере hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-174">In this section, you will load some data into hello source cluster.</span></span> <span data-ttu-id="c4b72-175">В следующем разделе hello будет включить репликацию между двумя кластерами hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-175">In hello next section, you will enable replication between hello two clusters.</span></span>

<span data-ttu-id="c4b72-176">Следуйте инструкциям в разделе hello [учебника HBase: начало работы с Apache HBase на основе Linux Hadoop в HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate **контактов** таблицы и вставить некоторые данные в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-176">Follow hello instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate a **Contacts** table and insert some data into hello table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="c4b72-177">Включение репликации</span><span class="sxs-lookup"><span data-stu-id="c4b72-177">Enable replication</span></span>

<span data-ttu-id="c4b72-178">Привет, следующие шаги показывают, как toocall hello сценарий действия сценария из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b72-178">hello following steps show how toocall hello script action script from hello Azure portal.</span></span> <span data-ttu-id="c4b72-179">Выполняется действие скрипта с помощью Azure PowerShell и hello Azure командной строки (CLI), в разделе [HDInsight под управлением Linux, настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c4b72-179">For running a script action by using Azure PowerShell and hello Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="c4b72-180">**репликация HBase tooenable из hello портал Azure**</span><span class="sxs-lookup"><span data-stu-id="c4b72-180">**tooenable HBase replication from hello Azure portal**</span></span>

1. <span data-ttu-id="c4b72-181">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4b72-181">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c4b72-182">Откройте hello исходного HBase кластера.</span><span class="sxs-lookup"><span data-stu-id="c4b72-182">Open hello source HBase cluster.</span></span>
3. <span data-ttu-id="c4b72-183">Меню hello кластера, нажмите кнопку **действия скрипта**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-183">From hello cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="c4b72-184">Нажмите кнопку **отправить новый** из hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-184">Click **Submit New** from hello top of hello blade.</span></span>
5. <span data-ttu-id="c4b72-185">Выберите или введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="c4b72-185">Select or enter hello following information:</span></span>

  - <span data-ttu-id="c4b72-186">**Имя:** введите **Включение репликации**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="c4b72-187">**URL-адрес bash-скрипта:** введите **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="c4b72-188">**Головной узел:** выбран.</span><span class="sxs-lookup"><span data-stu-id="c4b72-188">**Head**: Selected.</span></span> <span data-ttu-id="c4b72-189">Здравствуйте, снимите флажок для других типов узлов.</span><span class="sxs-lookup"><span data-stu-id="c4b72-189">Clear hello other node types.</span></span>
  - <span data-ttu-id="c4b72-190">**Параметры**: hello следующие образцы параметры Включение репликации для всех существующих таблиц hello и скопируйте все данные hello из hello источника toohello назначения кластера:</span><span class="sxs-lookup"><span data-stu-id="c4b72-190">**Parameters**: hello following sample parameters enable replication for all hello existing tables and copy all hello data from hello source cluster toohello destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="c4b72-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-191">Click **Create**.</span></span> <span data-ttu-id="c4b72-192">Hello скрипт может занять некоторое время, особенно при использовании аргумента - copydata hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-192">hello script can take some time, especially when hello -copydata argument is used.</span></span>

<span data-ttu-id="c4b72-193">Ниже приведены обязательные аргументы.</span><span class="sxs-lookup"><span data-stu-id="c4b72-193">Required arguments:</span></span>

|<span data-ttu-id="c4b72-194">Имя</span><span class="sxs-lookup"><span data-stu-id="c4b72-194">Name</span></span>|<span data-ttu-id="c4b72-195">Описание</span><span class="sxs-lookup"><span data-stu-id="c4b72-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="c4b72-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="c4b72-196">-s, --src-cluster</span></span> | <span data-ttu-id="c4b72-197">Укажите DNS-имя кластера HBase источника hello hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-197">Specify hello DNS name of hello source HBase cluster.</span></span> <span data-ttu-id="c4b72-198">например -s hbsrccluster, --src-cluster=hbsrccluster.</span><span class="sxs-lookup"><span data-stu-id="c4b72-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="c4b72-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="c4b72-199">-d, --dst-cluster</span></span> | <span data-ttu-id="c4b72-200">Укажите DNS-имя hello назначения «hello» (реплики) HBase кластера.</span><span class="sxs-lookup"><span data-stu-id="c4b72-200">Specify hello DNS name of hello destination (replica) HBase cluster.</span></span> <span data-ttu-id="c4b72-201">например -s dsthbcluster, --src-cluster=dsthbcluster.</span><span class="sxs-lookup"><span data-stu-id="c4b72-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="c4b72-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="c4b72-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="c4b72-203">Укажите пароль администратора hello для Ambari на кластер HBase источника hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-203">Specify hello admin password for Ambari on hello source HBase cluster.</span></span> |
|<span data-ttu-id="c4b72-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="c4b72-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="c4b72-205">Укажите пароль администратора hello для Ambari hello целевом кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="c4b72-205">Specify hello admin password for Ambari on hello destination HBase cluster.</span></span>|

<span data-ttu-id="c4b72-206">Необязательные аргументы для этой команды.</span><span class="sxs-lookup"><span data-stu-id="c4b72-206">Optional arguments:</span></span>

|<span data-ttu-id="c4b72-207">Имя</span><span class="sxs-lookup"><span data-stu-id="c4b72-207">Name</span></span>|<span data-ttu-id="c4b72-208">Описание</span><span class="sxs-lookup"><span data-stu-id="c4b72-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="c4b72-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="c4b72-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="c4b72-210">Укажите имя пользователя администратора hello для Ambari hello источника HBase кластере.</span><span class="sxs-lookup"><span data-stu-id="c4b72-210">Specify hello admin username for Ambari on hello source HBase cluster.</span></span> <span data-ttu-id="c4b72-211">значение по умолчанию Hello — **администратора**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-211">hello default value is **admin**.</span></span> |
|<span data-ttu-id="c4b72-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="c4b72-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="c4b72-213">Укажите имя пользователя администратора hello для Ambari hello целевом кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="c4b72-213">Specify hello admin username for Ambari on hello destination HBase cluster.</span></span> <span data-ttu-id="c4b72-214">значение по умолчанию Hello — **администратора**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-214">hello default value is **admin**.</span></span> |
|<span data-ttu-id="c4b72-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="c4b72-215">-t, --table-list</span></span> | <span data-ttu-id="c4b72-216">Укажите toobe таблиц hello репликации.</span><span class="sxs-lookup"><span data-stu-id="c4b72-216">Specify hello tables toobe replicated.</span></span> <span data-ttu-id="c4b72-217">например --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="c4b72-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="c4b72-218">Если не указать таблицы, будут реплицированы все существующие таблицы HBase.</span><span class="sxs-lookup"><span data-stu-id="c4b72-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="c4b72-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="c4b72-219">-m, --machine</span></span> | <span data-ttu-id="c4b72-220">Укажите hello головной узел, где будет выполняться действие сценария hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-220">Specify hello head node where hello script action will run.</span></span> <span data-ttu-id="c4b72-221">значение Hello — hn1 или hn0.</span><span class="sxs-lookup"><span data-stu-id="c4b72-221">hello value is either hn1 or hn0.</span></span> <span data-ttu-id="c4b72-222">Так как узел hn0 обычно более загружен, рекомендуется использовать hn1.</span><span class="sxs-lookup"><span data-stu-id="c4b72-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="c4b72-223">Используйте этот параметр при запуске сценария hello $0 как действие сценария с портала HDInsight hello или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4b72-223">You use this option when you're running hello $0 script as a script action from hello HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="c4b72-224">-ip</span><span class="sxs-lookup"><span data-stu-id="c4b72-224">-ip</span></span> | <span data-ttu-id="c4b72-225">Этот аргумент является обязательным, если вы включаете репликацию между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="c4b72-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="c4b72-226">Данный аргумент действует как переключатель toouse hello статические IP-адреса ZooKeeper узлы из кластеров реплики, а не полные ДОМЕННЫЕ имена.</span><span class="sxs-lookup"><span data-stu-id="c4b72-226">This argument acts as a switch toouse hello static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="c4b72-227">Hello статического IP-адреса должны toobe, заранее настроенный перед включением репликации.</span><span class="sxs-lookup"><span data-stu-id="c4b72-227">hello static IPs need toobe preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="c4b72-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="c4b72-228">-cp, -copydata</span></span> | <span data-ttu-id="c4b72-229">Включите hello миграцию существующих данных в таблицах hello, где включена репликация.</span><span class="sxs-lookup"><span data-stu-id="c4b72-229">Enable hello migration of existing data on hello tables where replication is enabled.</span></span> |
|<span data-ttu-id="c4b72-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="c4b72-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="c4b72-231">Включает репликацию для системных таблиц Phoenix.</span><span class="sxs-lookup"><span data-stu-id="c4b72-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="c4b72-232">*Используйте этот параметр с осторожностью.*</span><span class="sxs-lookup"><span data-stu-id="c4b72-232">*Use this option with caution.*</span></span> <span data-ttu-id="c4b72-233">Рекомендуется повторно создать таблицы Phoenix в реплицированных кластерах перед использованием этого скрипта.</span><span class="sxs-lookup"><span data-stu-id="c4b72-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="c4b72-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="c4b72-234">-h, --help</span></span> | <span data-ttu-id="c4b72-235">Отображает сведения об использовании.</span><span class="sxs-lookup"><span data-stu-id="c4b72-235">Display usage information.</span></span> |

<span data-ttu-id="c4b72-236">Здравствуйте, раздел print_usage() hello [сценарий](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) дано подробное описание параметров.</span><span class="sxs-lookup"><span data-stu-id="c4b72-236">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="c4b72-237">После hello скрипт действии успешно развернута, можно использовать кластер HBase назначения toohello tooconnect SSH и убедитесь, что были реплицированы данные hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-237">After hello script action is successfully deployed, you can use SSH tooconnect toohello destination HBase cluster, and verify hello data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="c4b72-238">Сценарии репликации</span><span class="sxs-lookup"><span data-stu-id="c4b72-238">Replication scenarios</span></span>

<span data-ttu-id="c4b72-239">Hello следующем списке перечислены некоторые общие способы применения и настройки их параметров.</span><span class="sxs-lookup"><span data-stu-id="c4b72-239">hello following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="c4b72-240">**Включение репликации для всех таблиц между кластерами hello двух**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-240">**Enable replication on all tables between hello two clusters**.</span></span> <span data-ttu-id="c4b72-241">В этом сценарии требуется копировать hello/миграции существующих данных в таблицах hello и не использует Финиксе таблиц.</span><span class="sxs-lookup"><span data-stu-id="c4b72-241">This scenario does not require hello copy/migration of existing data on hello tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="c4b72-242">Используйте hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c4b72-242">Use hello following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="c4b72-243">**Включение репликации для отдельных таблиц.**</span><span class="sxs-lookup"><span data-stu-id="c4b72-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="c4b72-244">Используйте следующие параметры репликации tooenable на table1, table2 и Таблица3 hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-244">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="c4b72-245">**Включение репликации для отдельных таблиц и копировать существующие данные hello**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-245">**Enable replication on specific tables and copy hello existing data**.</span></span> <span data-ttu-id="c4b72-246">Используйте следующие параметры репликации tooenable на table1, table2 и Таблица3 hello.</span><span class="sxs-lookup"><span data-stu-id="c4b72-246">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="c4b72-247">**Включение репликации для всех таблиц с помощью репликации Финиксе метаданных из источника toodestination**.</span><span class="sxs-lookup"><span data-stu-id="c4b72-247">**Enable replication on all tables with replicating phoenix metadata from source toodestination**.</span></span> <span data-ttu-id="c4b72-248">Репликация метаданных Phoenix работает не идеально, ее следует использовать с осторожностью.</span><span class="sxs-lookup"><span data-stu-id="c4b72-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="c4b72-249">Копирование и перенос данных</span><span class="sxs-lookup"><span data-stu-id="c4b72-249">Copy and migrate data</span></span>

<span data-ttu-id="c4b72-250">Существует два отдельных скрипта действия сценария для копирования или переноса данных после включения репликации:</span><span class="sxs-lookup"><span data-stu-id="c4b72-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="c4b72-251">[Скрипт для небольших таблиц](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (несколько гигабайт копирования размер, а также общем — ожидаемое toofinish менее чем за один час)</span><span class="sxs-lookup"><span data-stu-id="c4b72-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected toofinish in less than one hour)</span></span>

- <span data-ttu-id="c4b72-252">[Скрипт для больших таблиц](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (требуется больше времени, чем один час toocopy tootake)</span><span class="sxs-lookup"><span data-stu-id="c4b72-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected tootake longer than one hour toocopy)</span></span>

<span data-ttu-id="c4b72-253">Можно выполнить hello же процедуру в [включить репликацию](#enable-replication) действие сценария hello toocall с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c4b72-253">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="c4b72-254">Здравствуйте, раздел print_usage() hello [сценарий](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) содержит подробное описание параметров.</span><span class="sxs-lookup"><span data-stu-id="c4b72-254">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="c4b72-255">Сценарии</span><span class="sxs-lookup"><span data-stu-id="c4b72-255">Scenarios</span></span>

- <span data-ttu-id="c4b72-256">**Копирование определенных таблиц (test1, test2 и test3) для всех строк, измененных до настоящего момента (текущая отметка времени):**</span><span class="sxs-lookup"><span data-stu-id="c4b72-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="c4b72-257">или</span><span class="sxs-lookup"><span data-stu-id="c4b72-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="c4b72-258">**Копирование определенных таблиц с указанным интервалом времени:**</span><span class="sxs-lookup"><span data-stu-id="c4b72-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="c4b72-259">Отключение репликации</span><span class="sxs-lookup"><span data-stu-id="c4b72-259">Disable replication</span></span>

<span data-ttu-id="c4b72-260">репликация toodisable, используйте другой сценарий действия сценария, расположенный в [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="c4b72-260">toodisable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="c4b72-261">Можно выполнить hello же процедуру в [включить репликацию](#enable-replication) действие сценария hello toocall с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c4b72-261">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="c4b72-262">Здравствуйте, раздел print_usage() hello [сценарий](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) дано подробное описание параметров.</span><span class="sxs-lookup"><span data-stu-id="c4b72-262">hello print_usage() section of hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="c4b72-263">Сценарии</span><span class="sxs-lookup"><span data-stu-id="c4b72-263">Scenarios</span></span>

- <span data-ttu-id="c4b72-264">**Отключение репликации для всех таблиц:**</span><span class="sxs-lookup"><span data-stu-id="c4b72-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="c4b72-265">или</span><span class="sxs-lookup"><span data-stu-id="c4b72-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="c4b72-266">**Отключение репликации для определенных таблиц (table1, table2 и table3):**</span><span class="sxs-lookup"><span data-stu-id="c4b72-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="c4b72-267">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c4b72-267">Next steps</span></span>

<span data-ttu-id="c4b72-268">В этом учебнике вы узнали, как tooconfigure HBase репликации между двумя центрами обработки данных.</span><span class="sxs-lookup"><span data-stu-id="c4b72-268">In this tutorial, you learned how tooconfigure HBase replication across two datacenters.</span></span> <span data-ttu-id="c4b72-269">toolearn Дополнительные сведения о HDInsight и HBase, см.:</span><span class="sxs-lookup"><span data-stu-id="c4b72-269">toolearn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="c4b72-270">[Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Windows в HDInsight][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="c4b72-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="c4b72-271">[Что такое HBase в HDInsight: база данных NoSQL, которая предоставляет возможности, схожие с BigTable, для Hadoop][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="c4b72-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="c4b72-272">[Создание кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="c4b72-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="c4b72-273">[Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="c4b72-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="c4b72-274">[Анализ полученных с датчиков данных с использованием Apache Storm, концентратора событий и базы данных HBase в службе HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="c4b72-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

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
