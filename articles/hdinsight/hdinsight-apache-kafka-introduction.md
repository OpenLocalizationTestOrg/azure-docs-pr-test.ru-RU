---
title: "Основные сведения об Apache Kafka в Azure HDInsight | Документация Майкрософт"
description: "Данные об Apache Kafka в HDInsight: предназначение, выполняемые функции, а также сведения о том, где найти примеры и информацию по началу работы."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1976c52bd7fa56bb07104e205ab3699b2dfa4c50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="59c2c-103">Введение в Apache Kafka в HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="59c2c-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="59c2c-104">[Apache Kafka](https://kafka.apache.org) — это распределенная платформа потоковой передачи с открытым исходным кодом, которую можно использовать для создания конвейеров и приложений потоковой передачи данных в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="59c2c-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="59c2c-105">Kafka также предоставляет функцию брокера сообщений, подобную очереди сообщений, с помощью которой можно выполнять публикацию и подписываться на именованные потоки данных.</span><span class="sxs-lookup"><span data-stu-id="59c2c-105">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span></span> <span data-ttu-id="59c2c-106">Kafka в HDInsight предоставляет управляемую, высокомасштабируемую службу с высоким уровнем доступности в облаке Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="59c2c-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in the Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="59c2c-107">Преимущества Apache Kafka в HDInsight</span><span class="sxs-lookup"><span data-stu-id="59c2c-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="59c2c-108">Kafka предоставляет следующие возможности.</span><span class="sxs-lookup"><span data-stu-id="59c2c-108">Kafka provides the following features:</span></span>

* <span data-ttu-id="59c2c-109">Модель обмена сообщениями по схеме "публикация — подписка". Kafka предоставляет API производителя для публикации записей в разделе Kafka.</span><span class="sxs-lookup"><span data-stu-id="59c2c-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records to a Kafka topic.</span></span> <span data-ttu-id="59c2c-110">При подписке на раздел используется API пользователя.</span><span class="sxs-lookup"><span data-stu-id="59c2c-110">The Consumer API is used when subscribing to a topic.</span></span>

* <span data-ttu-id="59c2c-111">Потоковая обработка. Kafka часто используется с Apache Storm или Spark для потоковой обработки в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="59c2c-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="59c2c-112">В Kafka 0.10.0.0 (HDInsight версии 3.5) представлен API, позволяющий создавать решения для потоковой передачи без использования Storm или Spark.</span><span class="sxs-lookup"><span data-stu-id="59c2c-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you to build streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="59c2c-113">Горизонтальное масштабирование. В Kafka потоки разделяются между узлами в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59c2c-113">Horizontal scale: Kafka partitions streams across the nodes in the HDInsight cluster.</span></span> <span data-ttu-id="59c2c-114">Процессы пользователя можно связать с отдельными секциями для обеспечения балансировки нагрузки при использовании записей.</span><span class="sxs-lookup"><span data-stu-id="59c2c-114">Consumer processes can be associated with individual partitions to provide load balancing when consuming records.</span></span>

* <span data-ttu-id="59c2c-115">Порядок доставки. В каждой секции записи сохраняются в потоке в том порядке, в котором они были получены.</span><span class="sxs-lookup"><span data-stu-id="59c2c-115">In-order delivery: Within each partition, records are stored in the stream in the order that they were received.</span></span> <span data-ttu-id="59c2c-116">Достаточно связать один процесс пользователя с секцией — и записи будут обрабатываться в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="59c2c-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="59c2c-117">Отказоустойчивость. Для обеспечения отказоустойчивости секции могут реплицироваться между узлами.</span><span class="sxs-lookup"><span data-stu-id="59c2c-117">Fault-tolerant: Partitions can be replicated between nodes to provide fault tolerance.</span></span>

* <span data-ttu-id="59c2c-118">Интеграция с управляемыми дисками Azure: управляемые диски обеспечивают высокие показатели масштабируемости и пропускной способности для дисков, используемых виртуальными машинами в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59c2c-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for the disks used by the virtual machines in the HDInsight cluster.</span></span>

    <span data-ttu-id="59c2c-119">Управляемые диски по умолчанию включены для Kafka в HDInsight. Число используемых для каждого узла дисков можно настроить во время создания HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59c2c-119">Managed disks are enabled by default for Kafka on HDInsight, and the number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="59c2c-120">См. дополнительные сведения об [управляемых дисках Azure](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59c2c-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="59c2c-121">См. сведения о [настройке числа управляемых дисков и повышении степени масштабируемости для Kafka в HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="59c2c-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="59c2c-122">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="59c2c-122">Use cases</span></span>

* <span data-ttu-id="59c2c-123">**Обмен сообщениями.** Благодаря поддержке модели обмена сообщениями по схеме "публикация — подписка" Kafka часто используется как брокер сообщений.</span><span class="sxs-lookup"><span data-stu-id="59c2c-123">**Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="59c2c-124">**Отслеживание действий.** Kafka предоставляет возможность ведения журнала записей в определенном порядке, поэтому его можно использовать для отслеживания и повторного создания действий.</span><span class="sxs-lookup"><span data-stu-id="59c2c-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities.</span></span> <span data-ttu-id="59c2c-125">Например, действий пользователя на веб-сайте или в приложении.</span><span class="sxs-lookup"><span data-stu-id="59c2c-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="59c2c-126">**Агрегирование.** С помощью потоковой обработки можно объединить информацию из разных потоков для ее централизации в качестве оперативных данных.</span><span class="sxs-lookup"><span data-stu-id="59c2c-126">**Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span></span>

* <span data-ttu-id="59c2c-127">**Преобразование.** С помощью потоковой обработки можно объединять и дополнять данные из нескольких входных разделов в один или несколько выходных разделов.</span><span class="sxs-lookup"><span data-stu-id="59c2c-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59c2c-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59c2c-128">Next steps</span></span>

<span data-ttu-id="59c2c-129">Ниже приведены ссылки на статьи об использовании Apache Kafka в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59c2c-129">Use the following links to learn how to use Apache Kafka on HDInsight:</span></span>

* <span data-ttu-id="59c2c-130">[Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="59c2c-130">[Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)</span></span>

* <span data-ttu-id="59c2c-131">[Use MirrorMaker to create a replica of a Kafka on HDInsight cluster (preview)](hdinsight-apache-kafka-mirroring.md) (Создание реплики Kafka в кластере HDInsight с помощью MirrorMaker (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="59c2c-131">[Use MirrorMaker to create a replica of Kafka on HDInsight](hdinsight-apache-kafka-mirroring.md)</span></span>

* [<span data-ttu-id="59c2c-132">Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="59c2c-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="59c2c-133">Совместное использование Apache Spark и Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="59c2c-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="59c2c-134">Подключение к Kafka через виртуальную сеть Azure</span><span class="sxs-lookup"><span data-stu-id="59c2c-134">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)