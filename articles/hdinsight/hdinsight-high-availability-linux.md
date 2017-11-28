---
title: "Высокая доступность для Hadoop в Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как использование дополнительного головного узла позволяет повысить надежность и доступность кластеров HDInsight. Узнайте, как это влияет на службы Hadoop, такие как Ambari и Hive, и научитесь подключаться к каждому отдельному головному узлу с помощью SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "Высокая доступность Hadoop"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: e66ba67a36fc48d1762ba302d708e060489fdc71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="0316a-105">Доступность и надежность кластеров Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0316a-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="0316a-106">В кластерах HDInsight предусмотрены два головных узла, повышающие доступность и надежность выполняемых служб и заданий Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0316a-106">HDInsight clusters provide two head nodes to increase the availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="0316a-107">Платформа Hadoop обеспечивает высокий уровень доступности и надежности, реплицируя службы и данные на нескольких узлах в кластере.</span><span class="sxs-lookup"><span data-stu-id="0316a-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="0316a-108">Однако стандартные дистрибутивы Hadoop обычно имеют один головной узел.</span><span class="sxs-lookup"><span data-stu-id="0316a-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="0316a-109">Любой сбой такого узла может вызвать прекращение работы кластера.</span><span class="sxs-lookup"><span data-stu-id="0316a-109">Any outage of the single head node can cause the cluster to stop working.</span></span> <span data-ttu-id="0316a-110">HDInsight предоставляет два головных узла для повышения доступности и надежности Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0316a-110">HDInsight provides two headnodes to improve Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0316a-111">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="0316a-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0316a-112">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0316a-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="0316a-113">Доступность и надежность узлов</span><span class="sxs-lookup"><span data-stu-id="0316a-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="0316a-114">Узлы в кластере HDInsight реализуются с помощью виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="0316a-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="0316a-115">В следующих разделах рассматриваются отдельные типы узлов, которые используются с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0316a-115">The following sections discuss the individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="0316a-116">Не все типы узлов используются для определенного типа кластера.</span><span class="sxs-lookup"><span data-stu-id="0316a-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="0316a-117">Например, тип кластера Hadoop не содержит узлы Nimbus.</span><span class="sxs-lookup"><span data-stu-id="0316a-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="0316a-118">Дополнительные сведения об узлах, используемых типами кластеров HDInsight, см. в разделе "Типы кластеров" статьи [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="0316a-118">For more information on nodes used by HDInsight cluster types, see the Cluster types section of the [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="0316a-119">Головные узлы</span><span class="sxs-lookup"><span data-stu-id="0316a-119">Head nodes</span></span>

<span data-ttu-id="0316a-120">Для обеспечения высокого уровня доступности службы Hadoop HDInsight предоставляет два головных узла.</span><span class="sxs-lookup"><span data-stu-id="0316a-120">To ensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="0316a-121">Оба головных узла активны и работают в кластере HDInsight одновременно.</span><span class="sxs-lookup"><span data-stu-id="0316a-121">Both head nodes are active and running within the HDInsight cluster simultaneously.</span></span> <span data-ttu-id="0316a-122">Некоторые службы, например HDFS или YARN, в любой момент времени активны только на одном головном узле.</span><span class="sxs-lookup"><span data-stu-id="0316a-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="0316a-123">Другие службы, например HiveServer2 или Hive MetaStore, активны одновременно на обоих головных узлах.</span><span class="sxs-lookup"><span data-stu-id="0316a-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at the same time.</span></span>

<span data-ttu-id="0316a-124">Головные узлы (и другие узлы в HDInsight) содержат в своем имени числовое значение.</span><span class="sxs-lookup"><span data-stu-id="0316a-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of the hostname of the node.</span></span> <span data-ttu-id="0316a-125">Например, `hn0-CLUSTERNAME` или `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="0316a-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0316a-126">Не воспринимайте это числовое значение как обозначение приоритета узла (первичный или вторичный).</span><span class="sxs-lookup"><span data-stu-id="0316a-126">Do not associate the numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="0316a-127">Единственная функция этого значения — обеспечение уникальности имен для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="0316a-127">The numeric value is only present to provide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="0316a-128">Узлы Nimbus</span><span class="sxs-lookup"><span data-stu-id="0316a-128">Nimbus Nodes</span></span>

<span data-ttu-id="0316a-129">Узлы Nimbus доступны с кластерами Storm.</span><span class="sxs-lookup"><span data-stu-id="0316a-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="0316a-130">Узлы Nimbus предоставляют Hadoop JobTracker похожие функциональные возможности путем распределения и мониторинга обработки на рабочих узлах.</span><span class="sxs-lookup"><span data-stu-id="0316a-130">The Nimbus nodes provide similar functionality to the Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="0316a-131">HDInsight предоставляет два узла Nimbus для кластеров Storm.</span><span class="sxs-lookup"><span data-stu-id="0316a-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="0316a-132">Узлы Zookeeper</span><span class="sxs-lookup"><span data-stu-id="0316a-132">Zookeeper nodes</span></span>

<span data-ttu-id="0316a-133">Узлы [ZooKeeper](http://zookeeper.apache.org/) используются для выбора лидера главных служб на головных узлах,</span><span class="sxs-lookup"><span data-stu-id="0316a-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="0316a-134">а также для уведомления служб, узлов данных (рабочих узлов) и шлюзов о том, на каком головном узле активна главная служба.</span><span class="sxs-lookup"><span data-stu-id="0316a-134">They are also used to insure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="0316a-135">По умолчанию в кластере HDInsight предусмотрено три узла ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="0316a-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="0316a-136">Рабочие узлы</span><span class="sxs-lookup"><span data-stu-id="0316a-136">Worker nodes</span></span>

<span data-ttu-id="0316a-137">Рабочие узлы выполняют анализ данных при отправке задания в кластер.</span><span class="sxs-lookup"><span data-stu-id="0316a-137">Worker nodes perform the actual data analysis when a job is submitted to the cluster.</span></span> <span data-ttu-id="0316a-138">Если происходит сбой рабочего узла, выполняемая задача отправляется на другой рабочий узел.</span><span class="sxs-lookup"><span data-stu-id="0316a-138">If a worker node fails, the task that it was performing is submitted to another worker node.</span></span> <span data-ttu-id="0316a-139">По умолчанию HDInsight создает четыре рабочих узла.</span><span class="sxs-lookup"><span data-stu-id="0316a-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="0316a-140">Вы можете изменить это количество по своему усмотрению как во время создания кластера, так и позднее.</span><span class="sxs-lookup"><span data-stu-id="0316a-140">You can change this number to suit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="0316a-141">Граничный узел</span><span class="sxs-lookup"><span data-stu-id="0316a-141">Edge node</span></span>

<span data-ttu-id="0316a-142">Граничный узел не принимает активного участия в анализе данных в пределах кластера.</span><span class="sxs-lookup"><span data-stu-id="0316a-142">An edge node does not actively participate in data analysis within the cluster.</span></span> <span data-ttu-id="0316a-143">Разработчики или специалисты по обработке и анализу данных используют его при работе с Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0316a-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="0316a-144">Граничный узел находится в той же виртуальной сети Azure, что и другие узлы в кластере, и может получать непосредственный доступ ко всем остальным узлам.</span><span class="sxs-lookup"><span data-stu-id="0316a-144">The edge node lives in the same Azure Virtual Network as the other nodes in the cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="0316a-145">Его можно использовать без опасения отнять ресурсы у критически важных служб или заданий анализа Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0316a-145">The edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="0316a-146">В настоящее время R Server в HDInsight является единственным типом кластера, который по умолчанию предоставляет граничный узел.</span><span class="sxs-lookup"><span data-stu-id="0316a-146">Currently, R Server on HDInsight is the only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="0316a-147">В R Server в HDInsight граничный узел используется для локального тестирования кода R на узле перед его отправкой в кластер для распределенной обработки.</span><span class="sxs-lookup"><span data-stu-id="0316a-147">For R Server on HDInsight, the edge node is used test R code locally on the node before submitting it to the cluster for distributed processing.</span></span>

<span data-ttu-id="0316a-148">Сведения об использовании граничного узла с типами кластеров, отличными от R Server, см. в статье [Использование пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="0316a-148">For information on using an edge node with cluster types other than R Server, see the [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-the-nodes"></a><span data-ttu-id="0316a-149">Доступ к узлам</span><span class="sxs-lookup"><span data-stu-id="0316a-149">Accessing the nodes</span></span>

<span data-ttu-id="0316a-150">Доступ к кластеру из Интернета предоставляется через общедоступный шлюз.</span><span class="sxs-lookup"><span data-stu-id="0316a-150">Access to the cluster over the internet is provided through a public gateway.</span></span> <span data-ttu-id="0316a-151">Этот режим доступа позволяет подключаться только к головным узлам и граничному узлу (если он существует).</span><span class="sxs-lookup"><span data-stu-id="0316a-151">Access is limited to connecting to the head nodes and (if one exists) the edge node.</span></span> <span data-ttu-id="0316a-152">Наличие нескольких головных узлов никак не влияет на доступ к службам, работающим на головных узлах.</span><span class="sxs-lookup"><span data-stu-id="0316a-152">Access to services running on the head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="0316a-153">Общедоступный шлюз просто направляет запросы к тому головному узлу, на котором размещается запрашиваемая служба.</span><span class="sxs-lookup"><span data-stu-id="0316a-153">The public gateway routes requests to the head node that hosts the requested service.</span></span> <span data-ttu-id="0316a-154">Например, если служба Ambari размещена на вторичном головном узле, шлюз будет направлять на этот узел все входящие запросы к службе Ambari.</span><span class="sxs-lookup"><span data-stu-id="0316a-154">For example, if Ambari is currently hosted on the secondary head node, the gateway routes incoming requests for Ambari to that node.</span></span>

<span data-ttu-id="0316a-155">Доступ через общедоступный шлюз ограничен портами 443 (HTTPS), 22 и 23.</span><span class="sxs-lookup"><span data-stu-id="0316a-155">Access over the public gateway is limited to port 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="0316a-156">Порт __443__ используется для доступа к Ambari и другим пользовательским веб-интерфейсам или интерфейсам REST API, размещенным на головных узлах.</span><span class="sxs-lookup"><span data-stu-id="0316a-156">Port __443__ is used to access Ambari and other web UI or REST APIs hosted on the head nodes.</span></span>

* <span data-ttu-id="0316a-157">Порт __22__ используется для доступа к первичному головному узлу или граничному узлу по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="0316a-157">Port __22__ is used to access the primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="0316a-158">Порт __23__ используется для доступа ко вторичному головному узлу по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="0316a-158">Port __23__ is used to access the secondary head node with SSH.</span></span> <span data-ttu-id="0316a-159">Например, `ssh username@mycluster-ssh.azurehdinsight.net` подключается к основному головному узлу кластера с именем **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="0316a-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects to the primary head node of the cluster named **mycluster**.</span></span>

<span data-ttu-id="0316a-160">Дополнительные сведения об использовании SSH см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0316a-160">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="0316a-161">Внутренние полные доменные имена (FQDN)</span><span class="sxs-lookup"><span data-stu-id="0316a-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="0316a-162">Каждый узел в кластере HDInsight имеет внутренний IP-адрес и полное доменное имя, доступ к которым возможен только из этого кластера.</span><span class="sxs-lookup"><span data-stu-id="0316a-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from the cluster.</span></span> <span data-ttu-id="0316a-163">При доступе к службам в кластере с помощью внутреннего FQDN или IP-адреса следует использовать Ambari для проверки IP-адреса или FQDN, которые будут использоваться для доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="0316a-163">When accessing services on the cluster using the internal FQDN or IP address, you should use Ambari to verify the IP or FQDN to use when accessing the service.</span></span>

<span data-ttu-id="0316a-164">Например, служба Oozie может выполняться только на одном головном узле, и при использовании команды `oozie` в сеансе SSH требуется URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="0316a-164">For example, the Oozie service can only run on one head node, and using the `oozie` command from an SSH session requires the URL to the service.</span></span> <span data-ttu-id="0316a-165">Этот адрес можно получить из Ambari с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="0316a-165">This URL can be retrieved from Ambari by using the following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="0316a-166">Команда возвращает примерно следующее значение, содержащее внутренний URL-адрес для использования с командой `oozie`:</span><span class="sxs-lookup"><span data-stu-id="0316a-166">This command returns a value similar to the following command, which contains the internal URL to use with the `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="0316a-167">Дополнительные сведения о работе с REST API службы Ambari см. в статье [Управление кластерами HDInsight с помощью REST API Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="0316a-167">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="0316a-168">Доступ к узлам других типов</span><span class="sxs-lookup"><span data-stu-id="0316a-168">Accessing other node types</span></span>

<span data-ttu-id="0316a-169">К узлам, которые недоступны напрямую через Интернет, можно подключаться следующими способами.</span><span class="sxs-lookup"><span data-stu-id="0316a-169">You can connect to nodes that are not directly accessible over the internet by using the following methods:</span></span>

* <span data-ttu-id="0316a-170">**SSH.** После подключения к головному узлу с помощью SSH можно затем использовать SSH с головного узла для подключения к другим узлам в кластере.</span><span class="sxs-lookup"><span data-stu-id="0316a-170">**SSH**: Once connected to a head node using SSH, you can then use SSH from the head node to connect to other nodes in the cluster.</span></span> <span data-ttu-id="0316a-171">Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0316a-171">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="0316a-172">**Туннель SSH.** Если вам нужен доступ к веб-службе, размещенной на узле, к которому нет доступа из Интернета, следует использовать туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="0316a-172">**SSH Tunnel**: If you need to access a web service hosted on one of the nodes that is not exposed to the internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="0316a-173">Дополнительные сведения см. в статье [Использование туннелирования SSH для доступа к веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим веб-интерфейсам](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="0316a-173">For more information, see the [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="0316a-174">**Виртуальная сеть Azure.** Если кластер HDInsight входит в состав виртуальной сети Azure, любой ресурс в той же виртуальной сети может напрямую получать доступ ко всем узлам в кластере.</span><span class="sxs-lookup"><span data-stu-id="0316a-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on the same Virtual Network can directly access all nodes in the cluster.</span></span> <span data-ttu-id="0316a-175">Дополнительные сведения см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="0316a-175">For more information, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-to-check-on-a-service-status"></a><span data-ttu-id="0316a-176">Проверка состояния службы</span><span class="sxs-lookup"><span data-stu-id="0316a-176">How to check on a service status</span></span>

<span data-ttu-id="0316a-177">Состояние служб, работающих на головных узлах, можно проверить с помощью веб-интерфейса Ambari или REST API Ambari.</span><span class="sxs-lookup"><span data-stu-id="0316a-177">To check the status of services that run on the head nodes, use the Ambari Web UI or the Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="0316a-178">Веб-интерфейс Ambari</span><span class="sxs-lookup"><span data-stu-id="0316a-178">Ambari Web UI</span></span>

<span data-ttu-id="0316a-179">Веб-интерфейс Ambari можно просмотреть по ссылке https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="0316a-179">The Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="0316a-180">Замените **CLUSTERNAME** именем кластера.</span><span class="sxs-lookup"><span data-stu-id="0316a-180">Replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="0316a-181">При появлении запроса введите учетные данные пользователя HTTP для кластера.</span><span class="sxs-lookup"><span data-stu-id="0316a-181">If prompted, enter the HTTP user credentials for your cluster.</span></span> <span data-ttu-id="0316a-182">По умолчанию используются имя пользователя HTTP **admin** и пароль, который вы ввели при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="0316a-182">The default HTTP user name is **admin** and the password is the password you entered when creating the cluster.</span></span>

<span data-ttu-id="0316a-183">Открыв страницу Ambari, слева вы увидите список установленных служб.</span><span class="sxs-lookup"><span data-stu-id="0316a-183">When you arrive on the Ambari page, the installed services are listed on the left of the page.</span></span>

![Установленные службы](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="0316a-185">Существует ряд значков, которые могут отображаться рядом со службой и указывать ее состояние.</span><span class="sxs-lookup"><span data-stu-id="0316a-185">There are a series of icons that may appear next to a service to indicate status.</span></span> <span data-ttu-id="0316a-186">Все оповещения, связанные с той или иной службой, можно просмотреть, щелкнув ссылку **Оповещения** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0316a-186">Any alerts related to a service can be viewed using the **Alerts** link at the top of the page.</span></span> <span data-ttu-id="0316a-187">Чтобы просмотреть дополнительные сведения о службе, выберите ее.</span><span class="sxs-lookup"><span data-stu-id="0316a-187">You can select each service to view more information on it.</span></span>

<span data-ttu-id="0316a-188">На странице службы содержатся сведения о состоянии и конфигурации каждой службы, но не указывается, на каком головном узле она работает.</span><span class="sxs-lookup"><span data-stu-id="0316a-188">While the service page provides information on the status and configuration of each service, it does not provide information on which head node the service is running on.</span></span> <span data-ttu-id="0316a-189">Чтобы просмотреть эти сведения, щелкните ссылку **Узлы** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0316a-189">To view this information, use the **Hosts** link at the top of the page.</span></span> <span data-ttu-id="0316a-190">На странице отобразятся все узлы кластера, включая головные узлы.</span><span class="sxs-lookup"><span data-stu-id="0316a-190">This page displays hosts within the cluster, including the head nodes.</span></span>

![список узлов](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="0316a-192">Выберите ссылку на один из головных узлов, чтобы отобразить работающие на нем службы и компоненты.</span><span class="sxs-lookup"><span data-stu-id="0316a-192">Selecting the link for one of the head nodes displays the services and components running on that node.</span></span>

![Состояние компонента](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="0316a-194">Подробные сведения об использовании Ambari см. в статье [Управление кластерами HDInsight с помощью веб-интерфейса Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="0316a-194">For more information on using Ambari, see [Monitor and manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="0316a-195">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="0316a-195">Ambari REST API</span></span>

<span data-ttu-id="0316a-196">Ambari REST API доступен в Интернете.</span><span class="sxs-lookup"><span data-stu-id="0316a-196">The Ambari REST API is available over the internet.</span></span> <span data-ttu-id="0316a-197">Открытый шлюз HDInsight обрабатывает запросы маршрутизации к головному узлу, на котором в настоящее время размещается REST API.</span><span class="sxs-lookup"><span data-stu-id="0316a-197">The HDInsight public gateway handles routing requests to the head node that is currently hosting the REST API.</span></span>

<span data-ttu-id="0316a-198">Чтобы проверить состояние службы с помощью интерфейса Ambari REST API, можно воспользоваться следующей командой:</span><span class="sxs-lookup"><span data-stu-id="0316a-198">You can use the following command to check the state of a service through the Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="0316a-199">Замените **PASSWORD** паролем учетной записи пользователя (администратора) HTTP.</span><span class="sxs-lookup"><span data-stu-id="0316a-199">Replace **PASSWORD** with the HTTP user (admin) account password.</span></span>
* <span data-ttu-id="0316a-200">Замените **CLUSTERNAME** именем кластера.</span><span class="sxs-lookup"><span data-stu-id="0316a-200">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
* <span data-ttu-id="0316a-201">Замените **SERVICENAME** именем службы, состояние которой вы хотите проверить.</span><span class="sxs-lookup"><span data-stu-id="0316a-201">Replace **SERVICENAME** with the name of the service you want to check the status of.</span></span>

<span data-ttu-id="0316a-202">Например, чтобы проверить состояние службы **HDFS** в кластере с именем **mycluster** и паролем **password**, нужно выполнить следующую команду.</span><span class="sxs-lookup"><span data-stu-id="0316a-202">For example, to check the status of the **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use the following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="0316a-203">В ответ вы получите примерно такой код JSON:</span><span class="sxs-lookup"><span data-stu-id="0316a-203">The response is similar to the following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="0316a-204">URL-адрес указывает, что сейчас служба работает на узле с именем **hn0-CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="0316a-204">The URL tells us that the service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="0316a-205">Состояние указывает, что служба в настоящий момент запущена ( **STARTED**).</span><span class="sxs-lookup"><span data-stu-id="0316a-205">The state tells us that the service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="0316a-206">Если вам неизвестно, какие службы установлены в кластере, их список можно получить с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="0316a-206">If you do not know what services are installed on the cluster, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="0316a-207">Дополнительные сведения о работе с REST API службы Ambari см. в статье [Управление кластерами HDInsight с помощью REST API Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="0316a-207">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="0316a-208">Компоненты служб</span><span class="sxs-lookup"><span data-stu-id="0316a-208">Service components</span></span>

<span data-ttu-id="0316a-209">Иногда службы содержат компоненты, состояние которых может потребоваться проверить по отдельности.</span><span class="sxs-lookup"><span data-stu-id="0316a-209">Services may contain components that you wish to check the status of individually.</span></span> <span data-ttu-id="0316a-210">Например, служба HDFS содержит компонент NameNode.</span><span class="sxs-lookup"><span data-stu-id="0316a-210">For example, HDFS contains the NameNode component.</span></span> <span data-ttu-id="0316a-211">Чтобы просмотреть сведения о компоненте, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0316a-211">To view information on a component, the command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="0316a-212">Если вам неизвестно, какие компоненты содержатся в службе, их список можно получить с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="0316a-212">If you do not know what components are provided by a service, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-to-access-log-files-on-the-head-nodes"></a><span data-ttu-id="0316a-213">Доступ к файлам журнала на головных узлах</span><span class="sxs-lookup"><span data-stu-id="0316a-213">How to access log files on the head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="0316a-214">SSH</span><span class="sxs-lookup"><span data-stu-id="0316a-214">SSH</span></span>

<span data-ttu-id="0316a-215">Если подключение к головному узлу установлено через SSH, файлы журнала можно найти в папке **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="0316a-215">While connected to a head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="0316a-216">Например, в папке **/var/log/hadoop-yarn/yarn** содержатся журналы для YARN.</span><span class="sxs-lookup"><span data-stu-id="0316a-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="0316a-217">Каждый головной узел может иметь уникальные записи журнала, поэтому следует проверить журналы на обоих узлах.</span><span class="sxs-lookup"><span data-stu-id="0316a-217">Each head node can have unique log entries, so you should check the logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="0316a-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="0316a-218">SFTP</span></span>

<span data-ttu-id="0316a-219">Кроме того, к головному узлу можно подключаться с помощью протокола передачи файлов SSH или безопасного протокола передачи файлов (SFTP) и напрямую загружать файлы журналов.</span><span class="sxs-lookup"><span data-stu-id="0316a-219">You can also connect to the head node using the SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download the log files directly.</span></span>

<span data-ttu-id="0316a-220">Как и при использовании клиента SSH, при подключении к кластеру необходимо указать имя учетной записи пользователя SSH и адрес SSH кластера.</span><span class="sxs-lookup"><span data-stu-id="0316a-220">Similar to using an SSH client, when connecting to the cluster you must provide the SSH user account name and the SSH address of the cluster.</span></span> <span data-ttu-id="0316a-221">Например, `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="0316a-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="0316a-222">Предоставьте пароль для учетной записи, когда отобразится соответствующий запрос, или передайте открытый ключ через параметр `-i`.</span><span class="sxs-lookup"><span data-stu-id="0316a-222">Provide the password for the account when prompted, or provide a public key using the `-i` parameter.</span></span>

<span data-ttu-id="0316a-223">После подключения отобразится строка `sftp>` .</span><span class="sxs-lookup"><span data-stu-id="0316a-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="0316a-224">С помощью этой строки можно переходить в другие каталоги, отправлять и скачивать файлы.</span><span class="sxs-lookup"><span data-stu-id="0316a-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="0316a-225">Например, следующие команды изменяют каталоги на каталог **/var/log/hadoop/hdfs** , а затем загружают все файлы в каталоге.</span><span class="sxs-lookup"><span data-stu-id="0316a-225">For example, the following commands change directories to the **/var/log/hadoop/hdfs** directory and then download all files in the directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="0316a-226">Для просмотра списка доступных команд введите `help` в строке `sftp>`.</span><span class="sxs-lookup"><span data-stu-id="0316a-226">For a list of available commands, enter `help` at the `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="0316a-227">Некоторые графические интерфейсы позволяют визуализировать файловую систему при подключении по протоколу SFTP.</span><span class="sxs-lookup"><span data-stu-id="0316a-227">There are also graphical interfaces that allow you to visualize the file system when connected using SFTP.</span></span> <span data-ttu-id="0316a-228">Например, [MobaXTerm](http://mobaxterm.mobatek.net/) позволяет просматривать файловую систему с помощью интерфейса, похожего на проводник Windows.</span><span class="sxs-lookup"><span data-stu-id="0316a-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you to browse the file system using an interface similar to Windows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="0316a-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="0316a-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="0316a-230">Чтобы получить доступ к файлам журнала с помощью Ambari, используйте туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="0316a-230">To access log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="0316a-231">К веб-интерфейсам для отдельных служб не предоставляется открытый доступ через Интернет.</span><span class="sxs-lookup"><span data-stu-id="0316a-231">The web interfaces for the individual services are not exposed publicly on the Internet.</span></span> <span data-ttu-id="0316a-232">Дополнительные сведения об использовании туннеля SSH см. в документе [Использование туннелирования SSH для доступа к веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим веб-интерфейсам](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="0316a-232">For information on using an SSH tunnel, see the [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="0316a-233">Через веб-Интерфейс Ambari выберите службу, для которой вы хотите просмотреть журналы (например, YARN).</span><span class="sxs-lookup"><span data-stu-id="0316a-233">From the Ambari Web UI, select the service you wish to view logs for (for example, YARN).</span></span> <span data-ttu-id="0316a-234">Затем в разделе **Быстрые ссылки** выберите головной узел, для которого нужно просмотреть журналы.</span><span class="sxs-lookup"><span data-stu-id="0316a-234">Then use **Quick Links** to select which head node to view the logs for.</span></span>

![Использование быстрых ссылок для просмотра журналов](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-to-configure-the-node-size"></a><span data-ttu-id="0316a-236">Настройка размера узла</span><span class="sxs-lookup"><span data-stu-id="0316a-236">How to configure the node size</span></span>

<span data-ttu-id="0316a-237">Размер узла можно выбрать только во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="0316a-237">The size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="0316a-238">Список различных размеров виртуальных машин, доступных для HDInsight, можно найти на [странице цен на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0316a-238">You can find a list of the different VM sizes available for HDInsight on the [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="0316a-239">При создании кластера можно указать размер узлов.</span><span class="sxs-lookup"><span data-stu-id="0316a-239">When creating a cluster, you can specify the size of the nodes.</span></span> <span data-ttu-id="0316a-240">Далее приведены сведения о том, как указать размер узла с помощью [портала Azure][preview-portal], [Azure PowerShell][azure-powershell] и [Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="0316a-240">The following information provides guidance on how to specify the size using the [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and the [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="0316a-241">**Портал Azure.** При создании кластера можно задать размер для узлов этого кластера:</span><span class="sxs-lookup"><span data-stu-id="0316a-241">**Azure portal**: When creating a cluster, you can set the size of the nodes used by the cluster:</span></span>

    ![Изображение мастера создания кластера с выбором размера узла](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="0316a-243">**Azure CLI.** При использовании команды `azure hdinsight cluster create` можно задать размер головного, рабочего узла и узла ZooKeeper с помощью параметров `--headNodeSize`, `--workerNodeSize` и `--zookeeperNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="0316a-243">**Azure CLI**: When using the `azure hdinsight cluster create` command, you can set the size of the head, worker, and ZooKeeper nodes by using the `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="0316a-244">**Azure PowerShell.** При использовании командлета `New-AzureRmHDInsightCluster` можно задать размер головного и рабочего узлов и узла ZooKeeper с помощью параметров `-HeadNodeVMSize`, `-WorkerNodeSize` и `-ZookeeperNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="0316a-244">**Azure PowerShell**: When using the `New-AzureRmHDInsightCluster` cmdlet, you can set the size of the head, worker, and ZooKeeper nodes by using the `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0316a-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0316a-245">Next steps</span></span>

<span data-ttu-id="0316a-246">Чтобы получить дополнительные сведения о вопросах, упомянутых в этой статье, используйте следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0316a-246">Use the following links to learn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="0316a-247">Справочник по REST Ambari</span><span class="sxs-lookup"><span data-stu-id="0316a-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="0316a-248">Установка и настройка CLI Azure</span><span class="sxs-lookup"><span data-stu-id="0316a-248">Install and configure the Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="0316a-249">Установка и настройка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0316a-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="0316a-250">Управление кластерами HDInsight с помощью Ambari</span><span class="sxs-lookup"><span data-stu-id="0316a-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="0316a-251">«Подготовка кластеров HDInsight на основе Linux»</span><span class="sxs-lookup"><span data-stu-id="0316a-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
