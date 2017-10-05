---
title: "Использование Interactive Hive в HDInsight — Azure | Документы Майкрософт"
description: "Сведения об использовании Interactive Hive (Hive в LLAP) в HDInsight."
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
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="c8e04-103">Использование Interactive Hive в HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="c8e04-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="c8e04-104">Interactive Hive (также называемый</span><span class="sxs-lookup"><span data-stu-id="c8e04-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="c8e04-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) является новым [типом кластера](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c8e04-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="c8e04-106">Interactive Hive обеспечивает кэширование в памяти, благодаря чему запросы Hive становятся более интерактивными и быстрыми.</span><span class="sxs-lookup"><span data-stu-id="c8e04-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="c8e04-107">Эта новая функция делает HDInsight одним из самых производительных, гибких и открытых решений для работы с большими данными в облаке с кэш-памятью (с использованием Hive и Spark). Она также предоставляет расширенную аналитику благодаря тесной интеграции со службами R.</span><span class="sxs-lookup"><span data-stu-id="c8e04-107">This new feature makes HDInsight one of the world’s most performant, flexible, and open Big Data solutions on the cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="c8e04-108">Кластер Interactive Hive отличается от кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c8e04-108">The Interactive Hive cluster is different from the Hadoop cluster.</span></span> <span data-ttu-id="c8e04-109">Он содержит только службу Hive.</span><span class="sxs-lookup"><span data-stu-id="c8e04-109">It only contains the Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="c8e04-110">MapReduce, Pig, Sqoop, Oozie и другие службы скоро будут удалены из кластера этого типа.</span><span class="sxs-lookup"><span data-stu-id="c8e04-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="c8e04-111">Служба Hive в кластере Interactive Hive доступна только через представление Ambari Hive, Beeline и Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="c8e04-111">The Hive service in the Interactive Hive cluster is only accessible via the Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="c8e04-112">К ней невозможно получить доступ через консоль Hive, Templeton, интерфейс командной строки Azure и Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8e04-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="c8e04-113">Создание кластера Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="c8e04-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="c8e04-114">Кластер Interactive Hive поддерживается только на кластерах под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="c8e04-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="c8e04-115">Дополнительные сведения о создании кластеров HDInsight см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c8e04-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="c8e04-116">Выполнение Hive из Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="c8e04-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="c8e04-117">Существуют различные варианты выполнения запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="c8e04-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="c8e04-118">Запуск Hive с помощью представления Ambari Hive.</span><span class="sxs-lookup"><span data-stu-id="c8e04-118">Run Hive using the Ambari Hive view</span></span>
  
    <span data-ttu-id="c8e04-119">Сведения об использовании представления Hive см. в статье [Использование представления Hive с Hadoop в HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="c8e04-119">For the information about using the Hive View, see [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="c8e04-120">Запуск Hive с помощью Beeline.</span><span class="sxs-lookup"><span data-stu-id="c8e04-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="c8e04-121">Дополнительные сведения об использовании Beeline в HDInsight см. в статье [Использование Hive с Hadoop в HDInsight с применением Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="c8e04-121">For the information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="c8e04-122">Используйте Beeline на головном узле или на пустом граничном узле.</span><span class="sxs-lookup"><span data-stu-id="c8e04-122">You use Beeline from either the headnode or an empty edge node.</span></span>  <span data-ttu-id="c8e04-123">Рекомендуется использовать Beeline на пустом граничном узле.</span><span class="sxs-lookup"><span data-stu-id="c8e04-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="c8e04-124">Дополнительные сведения о создании кластера HDInsight с пустым граничным узлом см. в статье [Использование пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="c8e04-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="c8e04-125">Запуск Hive с помощью Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="c8e04-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="c8e04-126">Дополнительные сведения об использовании Hive ODBC см. в статье [Подключение Excel к Hadoop с помощью драйвера Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="c8e04-126">For the information on using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="c8e04-127">**Чтобы узнать строку подключения JDBC:**</span><span class="sxs-lookup"><span data-stu-id="c8e04-127">**To find the JDBC connection string:**</span></span>

1. <span data-ttu-id="c8e04-128">Войдите в Ambari, используя следующий URL-адрес: https://<ClusterName>. AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="c8e04-128">Sign on to Ambari using the following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="c8e04-129">Щелкните **Hive** в меню слева.</span><span class="sxs-lookup"><span data-stu-id="c8e04-129">Click **Hive** from the left menu.</span></span>
3. <span data-ttu-id="c8e04-130">Щелкните выделенный значок, чтобы скопировать URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="c8e04-130">Click the highlighted icon to copy the URL:</span></span>
   
   ![JDBC для HDInsight Hadoop типа Interactive Hive на LLAP](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="c8e04-132">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="c8e04-132">See also</span></span>
* <span data-ttu-id="c8e04-133">[Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="c8e04-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how to create Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="c8e04-134">[Использование Hive с Hadoop в HDInsight с применением Beeline](hdinsight-hadoop-use-hive-beeline.md)</span><span class="sxs-lookup"><span data-stu-id="c8e04-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how to use Beeline to submit Hive queries.</span></span>
* <span data-ttu-id="c8e04-135">[Подключение Excel к Hadoop с помощью драйвера Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="c8e04-135">[Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how to connect Excel to Hive.</span></span>

