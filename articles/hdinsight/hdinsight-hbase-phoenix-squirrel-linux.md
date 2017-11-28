---
title: "Использование Apache Phoenix и SQuirreL c HBase в Azure HDInsight | Документы Майкрософт"
description: "Узнайте о том, как использовать Apache Phoenix в HDInsight, а также как установить и настроить SQuirreL на рабочей станции для подключения к кластеру HBase в HDInsight."
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
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="9c7c2-103">Использование Apache Phoenix с кластерами HBase под управлением Linux в HDInsight</span><span class="sxs-lookup"><span data-stu-id="9c7c2-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="9c7c2-104">Узнайте, как использовать [Apache Phoenix](http://phoenix.apache.org/) в HDInsight, а также как использовать SQLLine.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="9c7c2-105">Дополнительные сведения о Phoenix см. в статье [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html) (Phoenix за 15 минут или меньше).</span><span class="sxs-lookup"><span data-stu-id="9c7c2-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="9c7c2-106">Информацию по грамматике Phoenix см. в разделе [Phoenix Grammar](http://phoenix.apache.org/language/index.html) (Грамматика Phoenix).</span><span class="sxs-lookup"><span data-stu-id="9c7c2-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="9c7c2-107">Сведения о версии Phoenix в HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9c7c2-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="9c7c2-108">Использование SQLLine</span><span class="sxs-lookup"><span data-stu-id="9c7c2-108">Use SQLLine</span></span>
<span data-ttu-id="9c7c2-109">[SQLLine](http://sqlline.sourceforge.net/) — это программа командной строки для выполнения SQL.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9c7c2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9c7c2-110">Prerequisites</span></span>
<span data-ttu-id="9c7c2-111">Перед использованием SQLLine необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="9c7c2-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="9c7c2-112">**Кластер HBase в HDInsight.**</span><span class="sxs-lookup"><span data-stu-id="9c7c2-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="9c7c2-113">Сведения о подготовке кластера HBase см. в статье [Руководство по HBase. Приступая к работе с Apache HBase на Hadoop под управлением Windows в HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="9c7c2-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="9c7c2-114">**Подключение к кластеру с помощью протокола удаленного рабочего стола.**</span><span class="sxs-lookup"><span data-stu-id="9c7c2-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="9c7c2-115">Инструкции см. в статье [Управление кластерами Hadoop в HDInsight с помощью портала Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="9c7c2-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="9c7c2-116">При подключении к кластеру HBase необходимо подключиться к одному из Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-116">When you connect to an HBase cluster, you need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="9c7c2-117">Каждый кластер HDInsight содержит три узла Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="9c7c2-118">**Определение имени узла Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="9c7c2-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="9c7c2-119">Откройте Ambari, перейдя по адресу **https://<ClusterName>.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-119">Open Ambari by browsing to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="9c7c2-120">Введите имя пользователя (кластера) HTTP и пароль для входа.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="9c7c2-121">В меню слева щелкните **Zookeeper** .</span><span class="sxs-lookup"><span data-stu-id="9c7c2-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="9c7c2-122">В списке будет три сервера **ZooKeeper Server**.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="9c7c2-123">Выберите один из серверов **ZooKeeper Server** .</span><span class="sxs-lookup"><span data-stu-id="9c7c2-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="9c7c2-124">На панели сводки найдите **Имя узла**.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="9c7c2-125">Оно аналогично *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="9c7c2-126">**Использование SQLLine**</span><span class="sxs-lookup"><span data-stu-id="9c7c2-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="9c7c2-127">Подключитесь к кластеру с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="9c7c2-128">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9c7c2-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="9c7c2-129">Из SSH выполните следующие команды для запуска SQLLine.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="9c7c2-130">Выполните следующие команды, чтобы создать таблицу HBase и вставить некоторые данные.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="9c7c2-131">Дополнительные сведения см. в разделе [SQLLine manual](http://sqlline.sourceforge.net/#manual) (Руководство по SQLLine) и [Phoenix Grammar](http://phoenix.apache.org/language/index.html) (Грамматика Phoenix).</span><span class="sxs-lookup"><span data-stu-id="9c7c2-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c7c2-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c7c2-132">Next steps</span></span>
<span data-ttu-id="9c7c2-133">В этой статье вы изучили использование Apache Phoenix в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="9c7c2-134">Дополнительные сведения см. на следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="9c7c2-134">To learn more, see:</span></span>

* <span data-ttu-id="9c7c2-135">[Что такое HBase в HDInsight][hdinsight-hbase-overview]. HBase — это база данных NoSQL с открытым исходным кодом Apache, разработанная в рамках проекта Hadoop, которая обеспечивает произвольный доступ и строгую согласованность больших объемов неструктурированных и частично структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="9c7c2-136">[Создание кластеров HBase в виртуальной сети Azure][hdinsight-hbase-provision-vnet]. Благодаря интеграции виртуальной сети кластеры HBase можно развернуть в той же виртуальной сети, что и приложения, поэтому эти приложения могут напрямую обмениваться данными с HBase.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="9c7c2-137">[Настройка репликации HBase в HDInsight](hdinsight-hbase-replication.md): узнайте, как настроить репликацию HBase между двумя центрами обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="9c7c2-138">[Анализ мнений пользователей Twitter в режиме реального времени с использованием HBase в HDInsight][hbase-twitter-sentiment]. Узнайте, как выполнять [анализ тональности](http://en.wikipedia.org/wiki/Sentiment_analysis) в режиме реального времени на основе больших данных, используя HBase в кластере Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c7c2-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
