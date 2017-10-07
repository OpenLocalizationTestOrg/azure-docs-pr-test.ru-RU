---
title: "разделы Apache Kafka aaaMirror - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Apache Kafka зеркального отображения компонентов toomaintain Kafka в кластере HDInsight из реплики можно использовать зеркальное отображение разделов tooa вторичного кластера."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="06502-103">Подразделы MirrorMaker tooreplicate Apache Kafka с Kafka на HDInsight (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="06502-103">Use MirrorMaker tooreplicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="06502-104">Узнайте, как toouse Apache Kafka зеркального отображения компонента tooreplicate разделы tooa вторичного кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-104">Learn how toouse Apache Kafka's mirroring feature tooreplicate topics tooa secondary cluster.</span></span> <span data-ttu-id="06502-105">Зеркальное отображение может быть выполнялся как непрерывный процесс, или использован периодически как метод переноса данных из одного кластера tooanother.</span><span class="sxs-lookup"><span data-stu-id="06502-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster tooanother.</span></span>

<span data-ttu-id="06502-106">В этом примере зеркальное отображение — разделы используется tooreplicate между двумя кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06502-106">In this example, mirroring is used tooreplicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="06502-107">Оба кластеров находится в виртуальной сети Azure в hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="06502-107">Both clusters are in an Azure Virtual Network in hello same region.</span></span>

> [!WARNING]
> <span data-ttu-id="06502-108">Зеркальное отображение не может считаться означает tooachieve отказоустойчивости.</span><span class="sxs-lookup"><span data-stu-id="06502-108">Mirroring should not be considered as a means tooachieve fault-tolerance.</span></span> <span data-ttu-id="06502-109">смещения tooitems Hello в разделе различаются hello источника и назначения кластеров, поэтому клиенты не могут использовать два hello попеременно.</span><span class="sxs-lookup"><span data-stu-id="06502-109">hello offset tooitems within a topic are different between hello source and destination clusters, so clients cannot use hello two interchangeably.</span></span>
>
> <span data-ttu-id="06502-110">Если отказоустойчивость, следует настроить репликацию разделов hello в рамках кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-110">If you are concerned about fault tolerance, you should set replication for hello topics within your cluster.</span></span> <span data-ttu-id="06502-111">Дополнительные сведения см. в статье по [началу работы с Kafka в HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="06502-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="06502-112">Как работает зеркальное отображение Kafka</span><span class="sxs-lookup"><span data-stu-id="06502-112">How Kafka mirroring works</span></span>

<span data-ttu-id="06502-113">Работает зеркальное отображение с помощью средства (часть Apache Kafka) tooconsume hello MirrorMaker записывает сведения в разделах, посвященных hello исходного кластера, а затем создать локальную копию hello целевом кластере.</span><span class="sxs-lookup"><span data-stu-id="06502-113">Mirroring works by using hello MirrorMaker tool (part of Apache Kafka) tooconsume records from topics on hello source cluster and then create a local copy on hello destination cluster.</span></span> <span data-ttu-id="06502-114">MirrorMaker использует один (или более) *потребителей* считывания hello исходного кластера и *производитель* , который записывает toohello локальной (назначение) кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-114">MirrorMaker uses one (or more) *consumers* that read from hello source cluster, and a *producer* that writes toohello local (destination) cluster.</span></span>

<span data-ttu-id="06502-115">Привет, следующая схема иллюстрирует процесс hello зеркального отображения:</span><span class="sxs-lookup"><span data-stu-id="06502-115">hello following diagram illustrates hello Mirroring process:</span></span>

![Схема процесса зеркального отображения hello](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="06502-117">Kafka Apache на HDInsight не предоставляет доступа toohello Kafka службы через hello общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="06502-117">Apache Kafka on HDInsight does not provide access toohello Kafka service over hello public internet.</span></span> <span data-ttu-id="06502-118">Производители Kafka или потребители должны находиться в hello одной виртуальной сети Azure hello в виде узлов кластера Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="06502-118">Kafka producers or consumers must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="06502-119">В этом примере hello Kafka источника и назначения кластеров находятся в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="06502-119">For this example, both hello Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="06502-120">Hello следующей схеме показаны связи потоки между кластерами hello:</span><span class="sxs-lookup"><span data-stu-id="06502-120">hello following diagram shows how communication flows between hello clusters:</span></span>

![Схема исходного и целевого кластеров Kafka в виртуальной сети Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="06502-122">Hello источника и назначения кластеров могут быть разными в hello числа узлов и секций и смещения в пределах hello разделы также различаются.</span><span class="sxs-lookup"><span data-stu-id="06502-122">hello source and destination clusters can be different in hello number of nodes and partitions, and offsets within hello topics are different also.</span></span> <span data-ttu-id="06502-123">Зеркальное отображение поддерживает hello значение ключа, который используется для секционирования, поэтому порядок записей сохраняются отдельно для каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="06502-123">Mirroring maintains hello key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="06502-124">Зеркальное отображение в пределах сети</span><span class="sxs-lookup"><span data-stu-id="06502-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="06502-125">Если вам требуется toomirror между кластерами Kafka в разных сетях, существует hello следующие дополнительные вопросы:</span><span class="sxs-lookup"><span data-stu-id="06502-125">If you need toomirror between Kafka clusters in different networks, there are hello following additional considerations:</span></span>

* <span data-ttu-id="06502-126">**Шлюзы**: hello сети должны быть toocommunicate доступ на уровне TCPIP hello.</span><span class="sxs-lookup"><span data-stu-id="06502-126">**Gateways**: hello networks must be able toocommunicate at hello TCPIP level.</span></span>

* <span data-ttu-id="06502-127">**Разрешение имен**: hello Kafka кластеров в каждой сети должен быть другие возможности tooconnect tooeach с помощью имен узлов.</span><span class="sxs-lookup"><span data-stu-id="06502-127">**Name resolution**: hello Kafka clusters in each network must be able tooconnect tooeach other by using hostnames.</span></span> <span data-ttu-id="06502-128">Это может потребоваться на сервере доменных имен (DNS) в каждой сети, настроить toohello tooforward запросы других сетей.</span><span class="sxs-lookup"><span data-stu-id="06502-128">This may require a Domain Name System (DNS) server in each network that is configured tooforward requests toohello other networks.</span></span>

    <span data-ttu-id="06502-129">При создании виртуальной сети Azure, вместо hello, предоставленные автоматического DNS с hello сети, необходимо указать пользовательский DNS сервера и hello IP-адрес для сервера hello.</span><span class="sxs-lookup"><span data-stu-id="06502-129">When creating an Azure Virtual Network, instead of using hello automatic DNS provided with hello network, you must specify a custom DNS server and hello IP address for hello server.</span></span> <span data-ttu-id="06502-130">После hello создания виртуальной сети вы необходимо затем создания виртуальной машине Azure, который использует этот IP-адрес, а затем установить и настроить программное обеспечение DNS на нем.</span><span class="sxs-lookup"><span data-stu-id="06502-130">After hello Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="06502-131">Создайте и настройте hello пользовательского DNS-сервера, перед установкой HDInsight в hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="06502-131">Create and configure hello custom DNS server before installing HDInsight into hello Virtual Network.</span></span> <span data-ttu-id="06502-132">Нет никаких дополнительных настроек, необходимых для HDInsight toouse hello DNS-сервер настроен для hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="06502-132">There is no additional configuration required for HDInsight toouse hello DNS server configured for hello Virtual Network.</span></span>

<span data-ttu-id="06502-133">Дополнительные сведения о подключении двух виртуальных сетей Azure см. в статье [Настройка подключения между виртуальными сетями в развертывании Resource Manager с помощью PowerShell](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="06502-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="06502-134">Создание кластеров Kafka</span><span class="sxs-lookup"><span data-stu-id="06502-134">Create Kafka clusters</span></span>

<span data-ttu-id="06502-135">Можно создать виртуальную сеть Azure и Kafka кластеры вручную, но это проще toouse шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="06502-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="06502-136">Следующие шаги toodeploy hello виртуальной сети Azure и используйте два tooyour кластеры Kafka подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="06502-136">Use hello following steps toodeploy an Azure virtual network and two Kafka clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="06502-137">Используйте hello toosign кнопки в tooAzure и Привет открыть шаблон в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="06502-137">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="06502-138">Hello шаблона Azure Resource Manager находится в каталоге **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="06502-138">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="06502-139">доступность tooguarantee Kafka на HDInsight, кластер должен содержать по крайней мере три рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="06502-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="06502-140">Этот шаблон создает кластер Kafka, содержащий три рабочих узла.</span><span class="sxs-lookup"><span data-stu-id="06502-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="06502-141">После записи hello toopopulate сведений на hello hello используйте **развертывания пользовательского** колонки:</span><span class="sxs-lookup"><span data-stu-id="06502-141">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
    
    ![Настраиваемое развертывание в HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="06502-143">**Группа ресурсов.** Создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="06502-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="06502-144">Эта группа содержит кластер HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="06502-144">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="06502-145">**Расположение**: выберите расположение территориально закрыть tooyou.</span><span class="sxs-lookup"><span data-stu-id="06502-145">**Location**: Select a location geographically close tooyou.</span></span>
     
    * <span data-ttu-id="06502-146">**Базовые имена кластеров**: это значение используется в качестве hello базовое имя для hello Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="06502-146">**Base Cluster Name**: This value is used as hello base name for hello Kafka clusters.</span></span> <span data-ttu-id="06502-147">Например, введя значение **hdi**, вы создадите кластеры с именами **source-hdi** и **dest-hdi**.</span><span class="sxs-lookup"><span data-stu-id="06502-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="06502-148">**Имя входа пользователя кластера**: hello имя пользователя администратора для hello источника и назначения Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="06502-148">**Cluster Login User Name**: hello admin user name for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="06502-149">**Имя входа пароль кластера**: hello пароль пользователя admin для hello источника и назначения Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="06502-149">**Cluster Login Password**: hello admin user password for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="06502-150">**Имя пользователя SSH**: hello toocreate пользователя SSH для hello источника и назначения Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="06502-150">**SSH User Name**: hello SSH user toocreate for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="06502-151">**Пароль SSH**: hello пароль пользователя SSH hello для hello источника и назначения Kafka кластеров.</span><span class="sxs-lookup"><span data-stu-id="06502-151">**SSH Password**: hello password for hello SSH user for hello source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="06502-152">Hello чтения **условий**, а затем выберите **я принимаю условия toohello, указанных выше**.</span><span class="sxs-lookup"><span data-stu-id="06502-152">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="06502-153">Наконец, проверьте **toodashboard ПИН-код** , а затем выберите **покупки**.</span><span class="sxs-lookup"><span data-stu-id="06502-153">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="06502-154">Занимает около 20 минут toocreate hello кластеров.</span><span class="sxs-lookup"><span data-stu-id="06502-154">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="06502-155">После создания ресурсов hello предпринимается колонке перенаправленный tooa hello группы ресурсов, содержащий кластеров hello и панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="06502-155">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Колонки группы ресурсов для виртуальной сети hello и кластеров](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="06502-157">Обратите внимание, что имена hello hello кластеров HDInsight **базовое имя источника** и **базовым ИМЕНЕМ dest**, где базовое имя — имя hello указано toohello шаблона.</span><span class="sxs-lookup"><span data-stu-id="06502-157">Notice that hello names of hello HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="06502-158">Использовать эти имена на последующих этапах при подключении toohello кластеров.</span><span class="sxs-lookup"><span data-stu-id="06502-158">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="06502-159">Создание разделов</span><span class="sxs-lookup"><span data-stu-id="06502-159">Create topics</span></span>

1. <span data-ttu-id="06502-160">Подключение toohello **источника** кластера с помощью SSH:</span><span class="sxs-lookup"><span data-stu-id="06502-160">Connect toohello **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="06502-161">Замените **sshuser** с именем пользователя hello SSH, используемые при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="06502-161">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="06502-162">Замените **базовым ИМЕНЕМ** с базовым именем hello, используемый при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="06502-162">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="06502-163">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="06502-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="06502-164">Используйте hello следующими командами toofind hello Zookeeper узлов для hello исходного кластера:</span><span class="sxs-lookup"><span data-stu-id="06502-164">Use hello following commands toofind hello Zookeeper hosts for hello source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="06502-165">Следующая команда tooverify, hello разделе hello используйте был создан:</span><span class="sxs-lookup"><span data-stu-id="06502-165">Use hello following command tooverify that hello topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="06502-166">содержит ответ Hello `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="06502-166">hello response contains `testtopic`.</span></span>

4. <span data-ttu-id="06502-167">Hello используйте следующую информацию tooview hello Zookeeper узла для этого (hello **источника**) кластера:</span><span class="sxs-lookup"><span data-stu-id="06502-167">Use hello following tooview hello Zookeeper host information for this (hello **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="06502-168">Возвращает сведения аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="06502-168">This returns information similar toohello following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="06502-169">Сохраните эти сведения.</span><span class="sxs-lookup"><span data-stu-id="06502-169">Save this information.</span></span> <span data-ttu-id="06502-170">Он используется в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="06502-170">It is used in hello next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="06502-171">Настройка зеркального отображения</span><span class="sxs-lookup"><span data-stu-id="06502-171">Configure mirroring</span></span>

1. <span data-ttu-id="06502-172">Подключение toohello **назначения** кластера с помощью другого сеанса SSH:</span><span class="sxs-lookup"><span data-stu-id="06502-172">Connect toohello **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="06502-173">Замените **sshuser** с именем пользователя hello SSH, используемые при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="06502-173">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="06502-174">Замените **базовым ИМЕНЕМ** с базовым именем hello, используемый при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="06502-174">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="06502-175">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="06502-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="06502-176">Используйте hello следующая команда toocreate `consumer.properties` файл, который описывает способ toocommunicate с hello **источника** кластера:</span><span class="sxs-lookup"><span data-stu-id="06502-176">Use hello following command toocreate a `consumer.properties` file that describes how toocommunicate with hello **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="06502-177">Используйте hello после текста как содержимое hello hello `consumer.properties` файла:</span><span class="sxs-lookup"><span data-stu-id="06502-177">Use hello following text as hello contents of hello `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="06502-178">Замените **SOURCE_ZKHOSTS** к hello Zookeeper узлов сведения из hello **источника** кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-178">Replace **SOURCE_ZKHOSTS** with hello Zookeeper hosts information from hello **source** cluster.</span></span>

    <span data-ttu-id="06502-179">Этот файл описывает hello потребителя сведения toouse при чтении из источника hello Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-179">This file describes hello consumer information toouse when reading from hello source Kafka cluster.</span></span> <span data-ttu-id="06502-180">Дополнительные сведения о конфигурации получателя см. в [этом разделе](https://kafka.apache.org/documentation#consumerconfigs) на сайте kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="06502-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="06502-181">toosave hello файла, используйте **Ctrl + X**, **Y**, а затем **ввод**.</span><span class="sxs-lookup"><span data-stu-id="06502-181">toosave hello file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="06502-182">Прежде чем настраивать hello производитель, который обменивается данными с hello целевого кластера, необходимо найти hello broker узлов для hello **назначения** кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-182">Before configuring hello producer that communicates with hello destination cluster, you must find hello broker hosts for hello **destination** cluster.</span></span> <span data-ttu-id="06502-183">Используйте следующие команды tooretrieve hello эти сведения:</span><span class="sxs-lookup"><span data-stu-id="06502-183">Use hello following commands tooretrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="06502-184">Замените `$PASSWORD` с паролем учетной записи (администратор) hello входа для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-184">Replace `$PASSWORD` with hello login account (admin) password for hello cluster.</span></span>

    <span data-ttu-id="06502-185">Замените `$CLUSTERNAME` с именем hello hello целевого кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-185">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="06502-186">Эти команды возвращают аналогичные toohello следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="06502-186">These commands return information similar toohello following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="06502-187">Используйте hello, следуя toocreate `producer.properties` файл, который описывает как toocommunicate с hello **назначения** кластера:</span><span class="sxs-lookup"><span data-stu-id="06502-187">Use hello following toocreate a `producer.properties` file that describes how toocommunicate with hello **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="06502-188">Используйте hello после текста как содержимое hello hello `producer.properties` файла:</span><span class="sxs-lookup"><span data-stu-id="06502-188">Use hello following text as hello contents of hello `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="06502-189">Замените **DEST_BROKERS** hello broker данными из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="06502-189">Replace **DEST_BROKERS** with hello broker information from hello previous step.</span></span>

    <span data-ttu-id="06502-190">Дополнительные сведения о конфигурации производителя см. в [этом разделе](https://kafka.apache.org/documentation#producerconfigs) на сайте kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="06502-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="06502-191">Запуск MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="06502-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="06502-192">Из toohello подключения SSH hello **назначения** кластер, используйте hello, следуйте процедуре MirrorMaker hello toostart команды:</span><span class="sxs-lookup"><span data-stu-id="06502-192">From hello SSH connection toohello **destination** cluster, use hello following command toostart hello MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="06502-193">Hello параметры, используемые в данном примере это:</span><span class="sxs-lookup"><span data-stu-id="06502-193">hello parameters used in this example are:</span></span>

    * <span data-ttu-id="06502-194">**--consumer.config**: hello файл, содержащий свойства потребителя.</span><span class="sxs-lookup"><span data-stu-id="06502-194">**--consumer.config**: Specifies hello file that contains consumer properties.</span></span> <span data-ttu-id="06502-195">Эти свойства являются используется toocreate потребителя, который считывает данные из hello *источника* Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-195">These properties are used toocreate a consumer that reads from hello *source* Kafka cluster.</span></span>

    * <span data-ttu-id="06502-196">**--producer.config**: hello файл, содержащий свойства производителя.</span><span class="sxs-lookup"><span data-stu-id="06502-196">**--producer.config**: Specifies hello file that contains producer properties.</span></span> <span data-ttu-id="06502-197">Эти свойства являются используется toocreate производитель, который записывает toohello *назначения* Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-197">These properties are used toocreate a producer that writes toohello *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="06502-198">**--белого списка**: список разделов, которые MirrorMaker выполняется репликация из кластера toohello hello источник назначения.</span><span class="sxs-lookup"><span data-stu-id="06502-198">**--whitelist**: A list of topics that MirrorMaker replicates from hello source cluster toohello destination.</span></span>

    * <span data-ttu-id="06502-199">**--num.streams**: hello количество потоков toocreate потребителя.</span><span class="sxs-lookup"><span data-stu-id="06502-199">**--num.streams**: hello number of consumer threads toocreate.</span></span>

 <span data-ttu-id="06502-200">Во время запуска MirrorMaker возвращает сведения аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="06502-200">On startup, MirrorMaker returns information similar toohello following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="06502-201">Из toohello подключения SSH hello **источника** кластера, используется следующая команда toostart производитель hello и отправки сообщений toohello раздела:</span><span class="sxs-lookup"><span data-stu-id="06502-201">From hello SSH connection toohello **source** cluster, use hello following command toostart a producer and send messages toohello topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="06502-202">Замените `$PASSWORD` с пароль для входа (администратор) hello для hello исходного кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-202">Replace `$PASSWORD` with hello login (admin) password for hello source cluster.</span></span>

    <span data-ttu-id="06502-203">Замените `$CLUSTERNAME` с именем hello hello исходного кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-203">Replace `$CLUSTERNAME` with hello name of hello source cluster.</span></span>

     <span data-ttu-id="06502-204">При переходе в пустую строку с курсором введите несколько текстовых сообщений.</span><span class="sxs-lookup"><span data-stu-id="06502-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="06502-205">Раздел toohello отправляется на hello **источника** кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-205">These are sent toohello topic on hello **source** cluster.</span></span> <span data-ttu-id="06502-206">По завершении использования **сочетание клавиш Ctrl + C** tooend hello производитель процесса.</span><span class="sxs-lookup"><span data-stu-id="06502-206">When done, use **Ctrl + C** tooend hello producer process.</span></span>

3. <span data-ttu-id="06502-207">Из toohello подключения SSH hello **назначения** кластер, используйте **сочетание клавиш Ctrl + C** tooend hello MirrorMaker процесса.</span><span class="sxs-lookup"><span data-stu-id="06502-207">From hello SSH connection toohello **destination** cluster, use **Ctrl + C** tooend hello MirrorMaker process.</span></span> <span data-ttu-id="06502-208">Затем используйте hello следующими командами tooverify hello, `testtopic` разделе была создана, и эти данные в разделе hello была зеркальной реплицированных toothis:</span><span class="sxs-lookup"><span data-stu-id="06502-208">Then use hello following commands tooverify that hello `testtopic` topic was created, and that data in hello topic was replicated toothis mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="06502-209">Замените `$PASSWORD` с пароль для входа (администратор) hello для hello целевого кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-209">Replace `$PASSWORD` with hello login (admin) password for hello destination cluster.</span></span>

    <span data-ttu-id="06502-210">Замените `$CLUSTERNAME` с именем hello hello целевого кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-210">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="06502-211">Hello список разделов теперь включает `testtopic`, оно создается при MirrorMaster отражает hello раздел из кластера toohello hello источник назначения.</span><span class="sxs-lookup"><span data-stu-id="06502-211">hello list of topics now includes `testtopic`, which is created when MirrorMaster mirrors hello topic from hello source cluster toohello destination.</span></span> <span data-ttu-id="06502-212">Hello сообщения, полученные из раздела hello, так же, как введенные в исходном кластере hello hello.</span><span class="sxs-lookup"><span data-stu-id="06502-212">hello messages retrieved from hello topic are hello same as entered on hello source cluster.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="06502-213">Удалить кластер hello</span><span class="sxs-lookup"><span data-stu-id="06502-213">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="06502-214">С момента создания hello в данном пошаговом руководстве кластеров в Здравствуйте одной группе ресурсов Azure, можно удалить группу ресурсов hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="06502-214">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="06502-215">Удаление группы ресурсов hello удаляет все ресурсы, созданные после этого документа, hello виртуальной сети Azure и учетной записи хранения, используемые в кластерах hello.</span><span class="sxs-lookup"><span data-stu-id="06502-215">Deleting hello resource group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06502-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06502-216">Next Steps</span></span>

<span data-ttu-id="06502-217">В этом документе вы узнали, как toouse MirrorMaker toocreate реплику Kafka кластера.</span><span class="sxs-lookup"><span data-stu-id="06502-217">In this document, you learned how toouse MirrorMaker toocreate a replica of a Kafka cluster.</span></span> <span data-ttu-id="06502-218">Используйте следующие ссылки toodiscover hello других способов toowork с Kafka:</span><span class="sxs-lookup"><span data-stu-id="06502-218">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="06502-219">[Документация по Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) на сайте cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="06502-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* <span data-ttu-id="06502-220">[Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="06502-220">[Get started with Apache Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)</span></span>
* [<span data-ttu-id="06502-221">Совместное использование Apache Spark и Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="06502-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="06502-222">Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="06502-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="06502-223">Подключение через виртуальную сеть Azure tooKafka</span><span class="sxs-lookup"><span data-stu-id="06502-223">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
