---
title: "Интерактивный Hive в HDInsight - Azure aaaUse | Документы Microsoft"
description: "Узнайте, как интерактивный Hive (Hive на LLAP) в HDInsight toouse."
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="f74ab-103">Использование Interactive Hive в HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="f74ab-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="f74ab-104">Interactive Hive (также называемый</span><span class="sxs-lookup"><span data-stu-id="f74ab-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="f74ab-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) является новым [типом кластера](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f74ab-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="f74ab-106">Interactive Hive обеспечивает кэширование в памяти, благодаря чему запросы Hive становятся более интерактивными и быстрыми.</span><span class="sxs-lookup"><span data-stu-id="f74ab-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="f74ab-107">Эта новая возможность делает HDInsight один hello мире большинство производительными, гибкий и открытый больших данных решений в облаке hello с кэшем в памяти (с помощью Hive и Spark) и advanced analytics через глубокую интеграцию со службами R Services.</span><span class="sxs-lookup"><span data-stu-id="f74ab-107">This new feature makes HDInsight one of hello world’s most performant, flexible, and open Big Data solutions on hello cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="f74ab-108">Интерактивный Hive кластера Hello отличается от кластера Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="f74ab-108">hello Interactive Hive cluster is different from hello Hadoop cluster.</span></span> <span data-ttu-id="f74ab-109">Он содержит только службы Hive hello.</span><span class="sxs-lookup"><span data-stu-id="f74ab-109">It only contains hello Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="f74ab-110">MapReduce, Pig, Sqoop, Oozie и другие службы скоро будут удалены из кластера этого типа.</span><span class="sxs-lookup"><span data-stu-id="f74ab-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="f74ab-111">Hello службы Hive в кластере интерактивный Hive hello доступен только через hello представление Ambari Hive, Beeline и Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="f74ab-111">hello Hive service in hello Interactive Hive cluster is only accessible via hello Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="f74ab-112">К ней невозможно получить доступ через консоль Hive, Templeton, интерфейс командной строки Azure и Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f74ab-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="f74ab-113">Создание кластера Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="f74ab-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="f74ab-114">Кластер Interactive Hive поддерживается только на кластерах под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="f74ab-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="f74ab-115">Дополнительные сведения о создании кластеров HDInsight см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="f74ab-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="f74ab-116">Выполнение Hive из Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="f74ab-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="f74ab-117">Существуют различные варианты выполнения запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="f74ab-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="f74ab-118">Запустите Hive с помощью hello куст Ambari представление</span><span class="sxs-lookup"><span data-stu-id="f74ab-118">Run Hive using hello Ambari Hive view</span></span>
  
    <span data-ttu-id="f74ab-119">Hello сведения об использовании hello Hive представления см. в разделе [hello используйте представление Hive с Hadoop в HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="f74ab-119">For hello information about using hello Hive View, see [Use hello Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="f74ab-120">Запуск Hive с помощью Beeline.</span><span class="sxs-lookup"><span data-stu-id="f74ab-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="f74ab-121">Hello сведения об использовании Beeline на HDInsight см. в разделе [используйте Hive в с Hadoop в HDInsight с Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="f74ab-121">For hello information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="f74ab-122">Используйте Beeline из головному узлу hello или пустой граничного узла.</span><span class="sxs-lookup"><span data-stu-id="f74ab-122">You use Beeline from either hello headnode or an empty edge node.</span></span>  <span data-ttu-id="f74ab-123">Рекомендуется использовать Beeline на пустом граничном узле.</span><span class="sxs-lookup"><span data-stu-id="f74ab-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="f74ab-124">Дополнительные сведения о создании кластера HDInsight с пустым граничным узлом см. в статье [Использование пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="f74ab-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="f74ab-125">Запуск Hive с помощью Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="f74ab-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="f74ab-126">Hello сведения об использовании Hive ODBC см. в разделе [tooHadoop Excel подключиться с помощью драйвера Microsoft Hive ODBC hello](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="f74ab-126">For hello information on using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="f74ab-127">**hello toofind строку подключения JDBC:**</span><span class="sxs-lookup"><span data-stu-id="f74ab-127">**toofind hello JDBC connection string:**</span></span>

1. <span data-ttu-id="f74ab-128">Вход с помощью URL-адреса hello tooAmbari: https://<ClusterName>. AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="f74ab-128">Sign on tooAmbari using hello following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="f74ab-129">Нажмите кнопку **Hive** из меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="f74ab-129">Click **Hive** from hello left menu.</span></span>
3. <span data-ttu-id="f74ab-130">Щелкните URL-адрес toocopy значок hello выделяются hello:</span><span class="sxs-lookup"><span data-stu-id="f74ab-130">Click hello highlighted icon toocopy hello URL:</span></span>
   
   ![JDBC для HDInsight Hadoop типа Interactive Hive на LLAP](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="f74ab-132">См. также</span><span class="sxs-lookup"><span data-stu-id="f74ab-132">See also</span></span>
* <span data-ttu-id="f74ab-133">[Создавать кластеры под управлением Linux Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Узнайте, как кластеры toocreate интерактивного Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f74ab-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how toocreate Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="f74ab-134">[Используйте Hive в с Hadoop в HDInsight с Beeline](hdinsight-hadoop-use-hive-beeline.md): Узнайте, как запросы Hive toosubmit Beeline toouse.</span><span class="sxs-lookup"><span data-stu-id="f74ab-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how toouse Beeline toosubmit Hive queries.</span></span>
* <span data-ttu-id="f74ab-135">[Подключение Excel tooHadoop с помощью драйвера Microsoft Hive ODBC hello](hdinsight-connect-excel-hive-odbc-driver.md): Узнайте, как tooconnect Excel tooHive.</span><span class="sxs-lookup"><span data-stu-id="f74ab-135">[Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how tooconnect Excel tooHive.</span></span>

