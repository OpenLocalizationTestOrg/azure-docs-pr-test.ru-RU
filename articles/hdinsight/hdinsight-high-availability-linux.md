---
title: "доступность aaaHigh для Hadoop - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как использование дополнительного головного узла позволяет повысить надежность и доступность кластеров HDInsight. Узнайте, как это влияет на службам Hadoop, например, Ambari и Hive, также как tooindividually подключения tooeach головного узла с помощью SSH."
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
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="09968-105">Доступность и надежность кластеров Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="09968-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="09968-106">Кластеры HDInsight предоставляют два головного узла tooincrease hello доступность и надежность Hadoop служб и заданий, выполняемых.</span><span class="sxs-lookup"><span data-stu-id="09968-106">HDInsight clusters provide two head nodes tooincrease hello availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="09968-107">Платформа Hadoop обеспечивает высокий уровень доступности и надежности, реплицируя службы и данные на нескольких узлах в кластере.</span><span class="sxs-lookup"><span data-stu-id="09968-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="09968-108">Однако стандартные дистрибутивы Hadoop обычно имеют один головной узел.</span><span class="sxs-lookup"><span data-stu-id="09968-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="09968-109">Любой сбой одного головного узла hello может привести к работе toostop кластера hello.</span><span class="sxs-lookup"><span data-stu-id="09968-109">Any outage of hello single head node can cause hello cluster toostop working.</span></span> <span data-ttu-id="09968-110">HDInsight обеспечивает доступность и надежность два headnodes tooimprove Hadoop.</span><span class="sxs-lookup"><span data-stu-id="09968-110">HDInsight provides two headnodes tooimprove Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09968-111">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="09968-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="09968-112">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="09968-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="09968-113">Доступность и надежность узлов</span><span class="sxs-lookup"><span data-stu-id="09968-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="09968-114">Узлы в кластере HDInsight реализуются с помощью виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="09968-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="09968-115">Hello следующих разделах рассматриваются типы hello отдельный узел, используемый с HDInsight.</span><span class="sxs-lookup"><span data-stu-id="09968-115">hello following sections discuss hello individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="09968-116">Не все типы узлов используются для определенного типа кластера.</span><span class="sxs-lookup"><span data-stu-id="09968-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="09968-117">Например, тип кластера Hadoop не содержит узлы Nimbus.</span><span class="sxs-lookup"><span data-stu-id="09968-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="09968-118">Дополнительные сведения об узлах, используемые типами кластера HDInsight см раздел типы кластера hello hello [кластеров под управлением Linux, создать Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) документа.</span><span class="sxs-lookup"><span data-stu-id="09968-118">For more information on nodes used by HDInsight cluster types, see hello Cluster types section of hello [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="09968-119">Головные узлы</span><span class="sxs-lookup"><span data-stu-id="09968-119">Head nodes</span></span>

<span data-ttu-id="09968-120">tooensure высокую доступность служб Hadoop, HDInsight предоставляет два головного узла.</span><span class="sxs-lookup"><span data-stu-id="09968-120">tooensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="09968-121">Оба головного узла и запущен в пределах кластера HDInsight hello одновременно.</span><span class="sxs-lookup"><span data-stu-id="09968-121">Both head nodes are active and running within hello HDInsight cluster simultaneously.</span></span> <span data-ttu-id="09968-122">Некоторые службы, например HDFS или YARN, в любой момент времени активны только на одном головном узле.</span><span class="sxs-lookup"><span data-stu-id="09968-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="09968-123">Другие службы, например HiveServer2 или Метахранилища Hive активны на оба головного узла на hello то же время.</span><span class="sxs-lookup"><span data-stu-id="09968-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at hello same time.</span></span>

<span data-ttu-id="09968-124">Головные узлы (и другие узлы в HDInsight) имеют числовое значение как часть имени узла hello hello узла.</span><span class="sxs-lookup"><span data-stu-id="09968-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of hello hostname of hello node.</span></span> <span data-ttu-id="09968-125">Например, `hn0-CLUSTERNAME` или `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="09968-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09968-126">Не связывайте hello числовое значение с ли узел является первичной или вторичной.</span><span class="sxs-lookup"><span data-stu-id="09968-126">Do not associate hello numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="09968-127">Hello числовое значение равно только присутствует tooprovide уникальное имя для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="09968-127">hello numeric value is only present tooprovide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="09968-128">Узлы Nimbus</span><span class="sxs-lookup"><span data-stu-id="09968-128">Nimbus Nodes</span></span>

<span data-ttu-id="09968-129">Узлы Nimbus доступны с кластерами Storm.</span><span class="sxs-lookup"><span data-stu-id="09968-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="09968-130">узлы Nimbus Hello предоставляют аналогичные функциональные возможности toohello Hadoop JobTracker, распространение и наблюдение за обработкой между узлами рабочих.</span><span class="sxs-lookup"><span data-stu-id="09968-130">hello Nimbus nodes provide similar functionality toohello Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="09968-131">HDInsight предоставляет два узла Nimbus для кластеров Storm.</span><span class="sxs-lookup"><span data-stu-id="09968-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="09968-132">Узлы Zookeeper</span><span class="sxs-lookup"><span data-stu-id="09968-132">Zookeeper nodes</span></span>

<span data-ttu-id="09968-133">Узлы [ZooKeeper](http://zookeeper.apache.org/) используются для выбора лидера главных служб на головных узлах,</span><span class="sxs-lookup"><span data-stu-id="09968-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="09968-134">Они также могут использовать tooinsure, что службы, узлы данных (рабочая) и шлюзы знают, какие головного узла не активна на главной службой.</span><span class="sxs-lookup"><span data-stu-id="09968-134">They are also used tooinsure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="09968-135">По умолчанию в кластере HDInsight предусмотрено три узла ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="09968-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="09968-136">Рабочие узлы</span><span class="sxs-lookup"><span data-stu-id="09968-136">Worker nodes</span></span>

<span data-ttu-id="09968-137">Рабочих узлов анализ hello фактические данные после задания отправленной toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="09968-137">Worker nodes perform hello actual data analysis when a job is submitted toohello cluster.</span></span> <span data-ttu-id="09968-138">В случае отказа рабочий узел hello задачу, которая его выполнением могут отправленной tooanother рабочий узел.</span><span class="sxs-lookup"><span data-stu-id="09968-138">If a worker node fails, hello task that it was performing is submitted tooanother worker node.</span></span> <span data-ttu-id="09968-139">По умолчанию HDInsight создает четыре рабочих узла.</span><span class="sxs-lookup"><span data-stu-id="09968-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="09968-140">Можно изменить этот номер toosuit потребностей во время и после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="09968-140">You can change this number toosuit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="09968-141">Граничный узел</span><span class="sxs-lookup"><span data-stu-id="09968-141">Edge node</span></span>

<span data-ttu-id="09968-142">Граничного узла не активно участвует в анализе данных в пределах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="09968-142">An edge node does not actively participate in data analysis within hello cluster.</span></span> <span data-ttu-id="09968-143">Разработчики или специалисты по обработке и анализу данных используют его при работе с Hadoop.</span><span class="sxs-lookup"><span data-stu-id="09968-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="09968-144">Hello edge узел находится в hello одной виртуальной сети Azure как hello другие узлы в кластере hello и прямой доступ к всех остальных узлов.</span><span class="sxs-lookup"><span data-stu-id="09968-144">hello edge node lives in hello same Azure Virtual Network as hello other nodes in hello cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="09968-145">Hello граничного узла можно использовать без учета ресурсов от критических служб Hadoop или задания анализа.</span><span class="sxs-lookup"><span data-stu-id="09968-145">hello edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="09968-146">В настоящее время сервер R на HDInsight является hello только кластера тип, предоставляющий граничного узла по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="09968-146">Currently, R Server on HDInsight is hello only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="09968-147">Сервер R в HDInsight, используется hello граничного узла код теста R локально на узле hello перед его отправкой toohello кластера для распределенной обработки.</span><span class="sxs-lookup"><span data-stu-id="09968-147">For R Server on HDInsight, hello edge node is used test R code locally on hello node before submitting it toohello cluster for distributed processing.</span></span>

<span data-ttu-id="09968-148">Сведения об использовании граничного узла с типами кластера, отличном от сервера R см. в разделе hello [использовать краевым узлам в HDInsight](hdinsight-apps-use-edge-node.md) документа.</span><span class="sxs-lookup"><span data-stu-id="09968-148">For information on using an edge node with cluster types other than R Server, see hello [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-hello-nodes"></a><span data-ttu-id="09968-149">Доступ к узлам hello</span><span class="sxs-lookup"><span data-stu-id="09968-149">Accessing hello nodes</span></span>

<span data-ttu-id="09968-150">Кластер toohello доступ через hello Интернет обеспечивается через открытые шлюза.</span><span class="sxs-lookup"><span data-stu-id="09968-150">Access toohello cluster over hello internet is provided through a public gateway.</span></span> <span data-ttu-id="09968-151">Доступ к ограниченной tooconnecting toohello головного узла и (если он существует) hello граничного узла.</span><span class="sxs-lookup"><span data-stu-id="09968-151">Access is limited tooconnecting toohello head nodes and (if one exists) hello edge node.</span></span> <span data-ttu-id="09968-152">Наличие нескольких головного узла tooservices доступ, работающих на узлах головного hello не влияют.</span><span class="sxs-lookup"><span data-stu-id="09968-152">Access tooservices running on hello head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="09968-153">Hello открытый шлюза маршруты запросов toohello головного узла, на котором размещена hello Запрошенная служба.</span><span class="sxs-lookup"><span data-stu-id="09968-153">hello public gateway routes requests toohello head node that hosts hello requested service.</span></span> <span data-ttu-id="09968-154">Например если Ambari в настоящий момент размещен на hello дополнительного головного узла, hello шлюза направляет входящие запросы для узла toothat Ambari.</span><span class="sxs-lookup"><span data-stu-id="09968-154">For example, if Ambari is currently hosted on hello secondary head node, hello gateway routes incoming requests for Ambari toothat node.</span></span>

<span data-ttu-id="09968-155">Доступ через шлюз открытый hello является ограниченной tooport 443 (HTTPS), 22 и 23.</span><span class="sxs-lookup"><span data-stu-id="09968-155">Access over hello public gateway is limited tooport 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="09968-156">Порт __443__ — используется tooaccess Ambari и других веб-интерфейса пользователя или интерфейсов API REST, размещенных на hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="09968-156">Port __443__ is used tooaccess Ambari and other web UI or REST APIs hosted on hello head nodes.</span></span>

* <span data-ttu-id="09968-157">Порт __22__ используется tooaccess hello основного головного узла или граничного узла с SSH.</span><span class="sxs-lookup"><span data-stu-id="09968-157">Port __22__ is used tooaccess hello primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="09968-158">Порт __23__ — используется tooaccess hello получателей головной узел с SSH.</span><span class="sxs-lookup"><span data-stu-id="09968-158">Port __23__ is used tooaccess hello secondary head node with SSH.</span></span> <span data-ttu-id="09968-159">Например `ssh username@mycluster-ssh.azurehdinsight.net` подключается toohello первичного головного узла с именем кластера hello **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="09968-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects toohello primary head node of hello cluster named **mycluster**.</span></span>

<span data-ttu-id="09968-160">Дополнительные сведения об использовании SSH см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.</span><span class="sxs-lookup"><span data-stu-id="09968-160">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="09968-161">Внутренние полные доменные имена (FQDN)</span><span class="sxs-lookup"><span data-stu-id="09968-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="09968-162">Узлы в кластере HDInsight имеют внутренний IP-адрес и полное доменное имя, может осуществляться только из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="09968-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from hello cluster.</span></span> <span data-ttu-id="09968-163">При обращении к службам на кластере hello hello внутренней полное доменное имя или IP-адрес, Ambari tooverify hello IP-адрес или полное доменное имя toouse следует использовать при доступе к службе hello.</span><span class="sxs-lookup"><span data-stu-id="09968-163">When accessing services on hello cluster using hello internal FQDN or IP address, you should use Ambari tooverify hello IP or FQDN toouse when accessing hello service.</span></span>

<span data-ttu-id="09968-164">Например, hello Oozie службы могут выполняться только на один головной узел и используя hello `oozie` команды из сеанса SSH требуется служба toohello hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="09968-164">For example, hello Oozie service can only run on one head node, and using hello `oozie` command from an SSH session requires hello URL toohello service.</span></span> <span data-ttu-id="09968-165">Этот URL-адрес можно получить из Ambari с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="09968-165">This URL can be retrieved from Ambari by using hello following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="09968-166">Эта команда возвращает значение аналогичные toohello, выполнив команду, которая содержит URL-адрес toouse hello для внутренних с hello `oozie` команды:</span><span class="sxs-lookup"><span data-stu-id="09968-166">This command returns a value similar toohello following command, which contains hello internal URL toouse with hello `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="09968-167">Дополнительные сведения о работе с Ambari REST API hello см. в разделе [монитор и управлять HDInsight с помощью API-интерфейса REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="09968-167">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="09968-168">Доступ к узлам других типов</span><span class="sxs-lookup"><span data-stu-id="09968-168">Accessing other node types</span></span>

<span data-ttu-id="09968-169">Можно подключиться toonodes, которые не напрямую доступны через Интернет hello с помощью hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="09968-169">You can connect toonodes that are not directly accessible over hello internet by using hello following methods:</span></span>

* <span data-ttu-id="09968-170">**SSH**: после подключения tooa головного узла с помощью SSH, можно использовать SSH от узлов tooother tooconnect hello головного узла в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="09968-170">**SSH**: Once connected tooa head node using SSH, you can then use SSH from hello head node tooconnect tooother nodes in hello cluster.</span></span> <span data-ttu-id="09968-171">Дополнительные сведения см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.</span><span class="sxs-lookup"><span data-stu-id="09968-171">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="09968-172">**Туннель SSH**: при необходимости tooaccess веб-службы, размещенной на один из узлов hello, которые не предоставляются toohello Интернета, необходимо использовать туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="09968-172">**SSH Tunnel**: If you need tooaccess a web service hosted on one of hello nodes that is not exposed toohello internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="09968-173">Дополнительные сведения см. в разделе hello [использовать туннель SSH с HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) документа.</span><span class="sxs-lookup"><span data-stu-id="09968-173">For more information, see hello [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="09968-174">**Виртуальная сеть Azure**: Если кластера является частью виртуальной сети Azure, любой ресурс на HDInsight hello же виртуальной сети можно получить доступ всем узлам в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="09968-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on hello same Virtual Network can directly access all nodes in hello cluster.</span></span> <span data-ttu-id="09968-175">Дополнительные сведения см. в разделе hello [HDInsight, расширять и с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md) документа.</span><span class="sxs-lookup"><span data-stu-id="09968-175">For more information, see hello [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-toocheck-on-a-service-status"></a><span data-ttu-id="09968-176">Как toocheck на состояние службы</span><span class="sxs-lookup"><span data-stu-id="09968-176">How toocheck on a service status</span></span>

<span data-ttu-id="09968-177">toocheck hello состояния служб, работающих на hello головного узла, используйте hello Ambari веб-интерфейса или hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="09968-177">toocheck hello status of services that run on hello head nodes, use hello Ambari Web UI or hello Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="09968-178">Веб-интерфейс Ambari</span><span class="sxs-lookup"><span data-stu-id="09968-178">Ambari Web UI</span></span>

<span data-ttu-id="09968-179">Hello Ambari веб-интерфейс пользователя может быть просмотрен на https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="09968-179">hello Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="09968-180">Замените **CLUSTERNAME** с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="09968-180">Replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="09968-181">Если необходимо, введите учетные данные пользователя hello HTTP для кластера.</span><span class="sxs-lookup"><span data-stu-id="09968-181">If prompted, enter hello HTTP user credentials for your cluster.</span></span> <span data-ttu-id="09968-182">имя пользователя HTTP по умолчанию Hello **администратора** hello пароль — hello пароль при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="09968-182">hello default HTTP user name is **admin** and hello password is hello password you entered when creating hello cluster.</span></span>

<span data-ttu-id="09968-183">При поступлении на странице приветствия Ambari, перечислены услуги hello установлен hello левой стороны страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="09968-183">When you arrive on hello Ambari page, hello installed services are listed on hello left of hello page.</span></span>

![Установленные службы](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="09968-185">Существует набор значков, которые могут появиться Далее состояние tooindicate tooa службы.</span><span class="sxs-lookup"><span data-stu-id="09968-185">There are a series of icons that may appear next tooa service tooindicate status.</span></span> <span data-ttu-id="09968-186">Все оповещения, связанные с tooa службы можно просмотреть при помощи hello **оповещения** ссылку вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="09968-186">Any alerts related tooa service can be viewed using hello **Alerts** link at hello top of hello page.</span></span> <span data-ttu-id="09968-187">Дополнительные сведения о его можно выбрать tooview каждой службы.</span><span class="sxs-lookup"><span data-stu-id="09968-187">You can select each service tooview more information on it.</span></span>

<span data-ttu-id="09968-188">Страница службы hello предоставляет информацию о hello состояние и конфигурация каждой службы, он не предоставляет сведения, на котором выполняется служба hello головного узла на.</span><span class="sxs-lookup"><span data-stu-id="09968-188">While hello service page provides information on hello status and configuration of each service, it does not provide information on which head node hello service is running on.</span></span> <span data-ttu-id="09968-189">tooview этой информации, используйте hello **узлов** ссылку вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="09968-189">tooview this information, use hello **Hosts** link at hello top of hello page.</span></span> <span data-ttu-id="09968-190">На этой странице отображаются узлы, находящиеся в кластере hello, в том числе hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="09968-190">This page displays hosts within hello cluster, including hello head nodes.</span></span>

![список узлов](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="09968-192">Выбор hello ссылку для одного из головного узла hello отображает hello служб и компонентов, работающих на этом узле.</span><span class="sxs-lookup"><span data-stu-id="09968-192">Selecting hello link for one of hello head nodes displays hello services and components running on that node.</span></span>

![Состояние компонента](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="09968-194">Дополнительные сведения об использовании Ambari см. в разделе [мониторинг и управление ими HDInsight с помощью hello Ambari веб-интерфейса](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="09968-194">For more information on using Ambari, see [Monitor and manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="09968-195">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="09968-195">Ambari REST API</span></span>

<span data-ttu-id="09968-196">Hello Ambari REST API доступен через hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="09968-196">hello Ambari REST API is available over hello internet.</span></span> <span data-ttu-id="09968-197">открытые шлюза Hello HDInsight обрабатывает маршрутизации запросов toohello головного узла, на котором в настоящее время размещается hello REST API.</span><span class="sxs-lookup"><span data-stu-id="09968-197">hello HDInsight public gateway handles routing requests toohello head node that is currently hosting hello REST API.</span></span>

<span data-ttu-id="09968-198">Можно использовать следующие команды toocheck hello состояния службы через API-Интерфейс REST Ambari hello hello:</span><span class="sxs-lookup"><span data-stu-id="09968-198">You can use hello following command toocheck hello state of a service through hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="09968-199">Замените **пароль** с паролем учетной записи пользователя (администратор) hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="09968-199">Replace **PASSWORD** with hello HTTP user (admin) account password.</span></span>
* <span data-ttu-id="09968-200">Замените **CLUSTERNAME** с именем hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="09968-200">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
* <span data-ttu-id="09968-201">Замените **SERVICENAME** именем hello hello службы требуется toocheck hello состояние.</span><span class="sxs-lookup"><span data-stu-id="09968-201">Replace **SERVICENAME** with hello name of hello service you want toocheck hello status of.</span></span>

<span data-ttu-id="09968-202">Например, toocheck hello состояние hello **HDFS** на кластер с именем **mycluster**, с паролем **пароль**, следует использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="09968-202">For example, toocheck hello status of hello **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use hello following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="09968-203">Hello ответ — примерно toohello следующие JSON:</span><span class="sxs-lookup"><span data-stu-id="09968-203">hello response is similar toohello following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="09968-204">Hello URL-адрес показывает, что служба hello в данный момент запущена на головной узел с именем **hn0 CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="09968-204">hello URL tells us that hello service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="09968-205">Hello состояние показывает, что выполняется служба hello, или **STARTED**.</span><span class="sxs-lookup"><span data-stu-id="09968-205">hello state tells us that hello service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="09968-206">Если вы не знаете, на кластере hello установленных служб, можно использовать hello, следующая команда tooretrieve списка:</span><span class="sxs-lookup"><span data-stu-id="09968-206">If you do not know what services are installed on hello cluster, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="09968-207">Дополнительные сведения о работе с Ambari REST API hello см. в разделе [монитор и управлять HDInsight с помощью API-интерфейса REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="09968-207">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="09968-208">Компоненты служб</span><span class="sxs-lookup"><span data-stu-id="09968-208">Service components</span></span>

<span data-ttu-id="09968-209">Службы могут включать компоненты, которые нужно состояние hello toocheck по отдельности.</span><span class="sxs-lookup"><span data-stu-id="09968-209">Services may contain components that you wish toocheck hello status of individually.</span></span> <span data-ttu-id="09968-210">Например HDFS содержит компонент NameNode hello.</span><span class="sxs-lookup"><span data-stu-id="09968-210">For example, HDFS contains hello NameNode component.</span></span> <span data-ttu-id="09968-211">tooview сведения о компоненте, hello команда будет выглядеть:</span><span class="sxs-lookup"><span data-stu-id="09968-211">tooview information on a component, hello command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="09968-212">Если вы не знаете, какие компоненты, предоставляемые службой, можно использовать hello, следующая команда tooretrieve списка:</span><span class="sxs-lookup"><span data-stu-id="09968-212">If you do not know what components are provided by a service, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a><span data-ttu-id="09968-213">Как tooaccess файлы журнала на hello головного узла</span><span class="sxs-lookup"><span data-stu-id="09968-213">How tooaccess log files on hello head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="09968-214">SSH</span><span class="sxs-lookup"><span data-stu-id="09968-214">SSH</span></span>

<span data-ttu-id="09968-215">При подключенном tooa головного узла через SSH, файлы журнала можно найти в разделе **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="09968-215">While connected tooa head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="09968-216">Например, в папке **/var/log/hadoop-yarn/yarn** содержатся журналы для YARN.</span><span class="sxs-lookup"><span data-stu-id="09968-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="09968-217">Каждый головной узел может привести уникальный журнал, поэтому следует проверить журналы на обоих hello.</span><span class="sxs-lookup"><span data-stu-id="09968-217">Each head node can have unique log entries, so you should check hello logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="09968-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="09968-218">SFTP</span></span>

<span data-ttu-id="09968-219">Можно подключиться с помощью SSH File Transfer Protocol hello или защиты файла передачи протокол SFTP головного узла toohello и загрузки файлов журнала hello напрямую.</span><span class="sxs-lookup"><span data-stu-id="09968-219">You can also connect toohello head node using hello SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download hello log files directly.</span></span>

<span data-ttu-id="09968-220">Аналогичные toousing клиент SSH, при подключении toohello кластера, необходимо указать hello SSH учетной записи имя пользователя и hello SSH адрес кластера hello.</span><span class="sxs-lookup"><span data-stu-id="09968-220">Similar toousing an SSH client, when connecting toohello cluster you must provide hello SSH user account name and hello SSH address of hello cluster.</span></span> <span data-ttu-id="09968-221">Например, `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="09968-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="09968-222">Указать hello пароль для учетной записи hello при появлении запроса или предоставить открытый ключ, с помощью hello `-i` параметра.</span><span class="sxs-lookup"><span data-stu-id="09968-222">Provide hello password for hello account when prompted, or provide a public key using hello `-i` parameter.</span></span>

<span data-ttu-id="09968-223">После подключения отобразится строка `sftp>` .</span><span class="sxs-lookup"><span data-stu-id="09968-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="09968-224">С помощью этой строки можно переходить в другие каталоги, отправлять и скачивать файлы.</span><span class="sxs-lookup"><span data-stu-id="09968-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="09968-225">Следующие команды hello изменить toohello каталогов, например, **/var/log/hadoop/hdfs** каталог и затем загрузить все файлы в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="09968-225">For example, hello following commands change directories toohello **/var/log/hadoop/hdfs** directory and then download all files in hello directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="09968-226">Список доступных команд, введите `help` в hello `sftp>` строки.</span><span class="sxs-lookup"><span data-stu-id="09968-226">For a list of available commands, enter `help` at hello `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="09968-227">Существуют также графические интерфейсы, позволяющие toovisualize hello файловой системы при подключении с помощью SFTP.</span><span class="sxs-lookup"><span data-stu-id="09968-227">There are also graphical interfaces that allow you toovisualize hello file system when connected using SFTP.</span></span> <span data-ttu-id="09968-228">Например [MobaXTerm](http://mobaxterm.mobatek.net/) позволяет toobrowse hello файловой системы, с помощью примерно tooWindows интерфейс обозревателя.</span><span class="sxs-lookup"><span data-stu-id="09968-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you toobrowse hello file system using an interface similar tooWindows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="09968-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="09968-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="09968-230">файлы, с помощью Ambari журнала tooaccess, необходимо использовать туннель SSH.</span><span class="sxs-lookup"><span data-stu-id="09968-230">tooaccess log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="09968-231">Hello веб-интерфейсы для отдельных служб hello не предоставляются открыто на hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="09968-231">hello web interfaces for hello individual services are not exposed publicly on hello Internet.</span></span> <span data-ttu-id="09968-232">Сведения об использовании туннель SSH см. в разделе hello [использование SSH туннелирование](hdinsight-linux-ambari-ssh-tunnel.md) документа.</span><span class="sxs-lookup"><span data-stu-id="09968-232">For information on using an SSH tunnel, see hello [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="09968-233">Hello Ambari веб-интерфейса выберите службу hello, вы хотите tooview журналы (например, YARN).</span><span class="sxs-lookup"><span data-stu-id="09968-233">From hello Ambari Web UI, select hello service you wish tooview logs for (for example, YARN).</span></span> <span data-ttu-id="09968-234">Затем с помощью **быстрые ссылки** tooselect какие hello tooview головного узла в журналах.</span><span class="sxs-lookup"><span data-stu-id="09968-234">Then use **Quick Links** tooselect which head node tooview hello logs for.</span></span>

![Использование быстрого связывает tooview журналы](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a><span data-ttu-id="09968-236">Как tooconfigure hello размер узла</span><span class="sxs-lookup"><span data-stu-id="09968-236">How tooconfigure hello node size</span></span>

<span data-ttu-id="09968-237">размер Hello узла может быть выбран только во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="09968-237">hello size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="09968-238">Можно найти список hello различных размеров виртуальных Машин для HDInsight на hello [HDInsight странице цен](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="09968-238">You can find a list of hello different VM sizes available for HDInsight on hello [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="09968-239">При создании кластера, можно указать размер hello hello узлов.</span><span class="sxs-lookup"><span data-stu-id="09968-239">When creating a cluster, you can specify hello size of hello nodes.</span></span> <span data-ttu-id="09968-240">Hello следующее руководство по как с помощью размер hello toospecify hello [портал Azure][preview-portal], [Azure PowerShell][azure-powershell], и hello [Azure CLI][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="09968-240">hello following information provides guidance on how toospecify hello size using hello [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and hello [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="09968-241">**Портал Azure**: при создании кластера, можно задать размер hello hello кластере узлов hello:</span><span class="sxs-lookup"><span data-stu-id="09968-241">**Azure portal**: When creating a cluster, you can set hello size of hello nodes used by hello cluster:</span></span>

    ![Изображение мастера создания кластера с выбором размера узла](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="09968-243">**Azure CLI**: при использовании hello `azure hdinsight cluster create` команды можно задать размер hello hello head, рабочего процесса и ZooKeeper узлов с помощью hello `--headNodeSize`, `--workerNodeSize`, и `--zookeeperNodeSize` параметров.</span><span class="sxs-lookup"><span data-stu-id="09968-243">**Azure CLI**: When using hello `azure hdinsight cluster create` command, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="09968-244">**Azure PowerShell**: при использовании hello `New-AzureRmHDInsightCluster` командлета, можно задать размер hello hello head, рабочий и ZooKeeper узлов с помощью hello `-HeadNodeVMSize`, `-WorkerNodeSize`, и `-ZookeeperNodeSize` параметров.</span><span class="sxs-lookup"><span data-stu-id="09968-244">**Azure PowerShell**: When using hello `New-AzureRmHDInsightCluster` cmdlet, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09968-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09968-245">Next steps</span></span>

<span data-ttu-id="09968-246">Используйте следующие ссылки toolearn больше о действиях, упомянутые в этом документе hello.</span><span class="sxs-lookup"><span data-stu-id="09968-246">Use hello following links toolearn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="09968-247">Справочник по REST Ambari</span><span class="sxs-lookup"><span data-stu-id="09968-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="09968-248">Установка и настройка hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="09968-248">Install and configure hello Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="09968-249">Установка и настройка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="09968-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="09968-250">Управление кластерами HDInsight с помощью Ambari</span><span class="sxs-lookup"><span data-stu-id="09968-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="09968-251">«Подготовка кластеров HDInsight на основе Linux»</span><span class="sxs-lookup"><span data-stu-id="09968-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
