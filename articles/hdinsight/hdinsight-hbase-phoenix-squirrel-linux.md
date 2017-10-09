---
title: "aaaUse Финиксе Apache & белка с HBase - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Финиксе Apache в HDInsight и как tooinstall и настройте белка на кластер рабочей станции tooconnect tooan HBase на HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="a44af-103">Использование Apache Phoenix с кластерами HBase под управлением Linux в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a44af-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="a44af-104">Узнайте, как toouse [Финиксе Apache](http://phoenix.apache.org/) в HDInsight и как toouse SQLLine.</span><span class="sxs-lookup"><span data-stu-id="a44af-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how toouse SQLLine.</span></span> <span data-ttu-id="a44af-105">Дополнительные сведения о Phoenix см. в статье [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html) (Phoenix за 15 минут или меньше).</span><span class="sxs-lookup"><span data-stu-id="a44af-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="a44af-106">Hello Финиксе грамматики. в разделе [грамматики Финиксе](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="a44af-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="a44af-107">Hello Финиксе сведения о версии в HDInsight, в разделе [новые возможности, предоставляемые HDInsight версиями кластеров Hadoop hello?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a44af-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="a44af-108">Использование SQLLine</span><span class="sxs-lookup"><span data-stu-id="a44af-108">Use SQLLine</span></span>
<span data-ttu-id="a44af-109">[SQLLine](http://sqlline.sourceforge.net/) является tooexecute программы командной строки SQL.</span><span class="sxs-lookup"><span data-stu-id="a44af-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a44af-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a44af-110">Prerequisites</span></span>
<span data-ttu-id="a44af-111">Прежде чем использовать SQLLine, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="a44af-111">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="a44af-112">**Кластер HBase в HDInsight.**</span><span class="sxs-lookup"><span data-stu-id="a44af-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="a44af-113">Сведения о подготовке кластера HBase см. в статье [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Windows в HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="a44af-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="a44af-114">**Подключите кластер HBase toohello посредством протокола удаленного рабочего стола hello**.</span><span class="sxs-lookup"><span data-stu-id="a44af-114">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="a44af-115">Инструкции см. в разделе [кластеров управление Hadoop в HDInsight с помощью hello портал Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="a44af-115">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="a44af-116">При подключении tooan HBase кластера необходимо tooone tooconnect из hello Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="a44af-116">When you connect tooan HBase cluster, you need tooconnect tooone of hello Zookeepers.</span></span> <span data-ttu-id="a44af-117">Каждый кластер HDInsight содержит три узла Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="a44af-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="a44af-118">**toofind имя узла Zookeeper hello**</span><span class="sxs-lookup"><span data-stu-id="a44af-118">**toofind out hello Zookeeper host name**</span></span>

1. <span data-ttu-id="a44af-119">Откройте Ambari перейдя слишком**https://<ClusterName>. azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="a44af-119">Open Ambari by browsing too**https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="a44af-120">Введите имя пользователя и пароль toologin hello HTTP (кластер).</span><span class="sxs-lookup"><span data-stu-id="a44af-120">Enter hello HTTP (cluster) username and password toologin.</span></span>
3. <span data-ttu-id="a44af-121">Нажмите кнопку **ZooKeeper** из меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="a44af-121">Click **ZooKeeper** from hello left menu.</span></span> <span data-ttu-id="a44af-122">В списке будет три сервера **ZooKeeper Server**.</span><span class="sxs-lookup"><span data-stu-id="a44af-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="a44af-123">Выберите один из hello **ZooKeeper сервера** в списке.</span><span class="sxs-lookup"><span data-stu-id="a44af-123">Click one of hello **ZooKeeper Server** listed.</span></span> <span data-ttu-id="a44af-124">На сводной панели hello найти hello **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="a44af-124">On hello Summary pane, find hello **Hostname**.</span></span> <span data-ttu-id="a44af-125">Это аналогично слишком*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="a44af-125">It is similar too*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="a44af-126">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="a44af-126">**toouse SQLLine**</span></span>

1. <span data-ttu-id="a44af-127">Подключите кластер toohello с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="a44af-127">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="a44af-128">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a44af-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a44af-129">В SSH выполните следующие команды toorun SQLLine hello.</span><span class="sxs-lookup"><span data-stu-id="a44af-129">From SSH, run hello following commands toorun SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="a44af-130">Запустите следующие команды toocreate hello таблице HBase и вставить некоторые данные.</span><span class="sxs-lookup"><span data-stu-id="a44af-130">Run hello following commands toocreate a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="a44af-131">Дополнительные сведения см. в разделе [SQLLine manual](http://sqlline.sourceforge.net/#manual) (Руководство по SQLLine) и [Phoenix Grammar](http://phoenix.apache.org/language/index.html) (Грамматика Phoenix).</span><span class="sxs-lookup"><span data-stu-id="a44af-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a44af-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a44af-132">Next steps</span></span>
<span data-ttu-id="a44af-133">В этой статье вы узнали как toouse Финиксе Apache в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a44af-133">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="a44af-134">toolearn более, см.:</span><span class="sxs-lookup"><span data-stu-id="a44af-134">toolearn more, see:</span></span>

* <span data-ttu-id="a44af-135">[Что такое HBase в HDInsight][hdinsight-hbase-overview]. HBase — это база данных NoSQL с открытым исходным кодом Apache, разработанная в рамках проекта Hadoop, которая обеспечивает произвольный доступ и строгую согласованность больших объемов неструктурированных и частично структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="a44af-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="a44af-136">[Подготовка кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet]: С интеграцией виртуальной сети кластеров HBase может быть развернутой toohello виртуальных сетевых как приложения таким образом, приложения могут взаимодействовать с HBase напрямую.</span><span class="sxs-lookup"><span data-stu-id="a44af-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="a44af-137">[Настройка репликации HBase HDInsight](hdinsight-hbase-replication.md): Узнайте, как tooconfigure HBase репликации между двумя центрами обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a44af-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="a44af-138">[Анализ мнений Twitter с HBase в HDInsight][hbase-twitter-sentiment]: Узнайте, как toodo в режиме реального времени [анализ мнений](http://en.wikipedia.org/wiki/Sentiment_analysis) больших данных с помощью кластера Hadoop в HDInsight HBase.</span><span class="sxs-lookup"><span data-stu-id="a44af-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
