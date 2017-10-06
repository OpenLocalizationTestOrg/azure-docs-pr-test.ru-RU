---
title: "Введение aaaAn tooApache Kafka на HDInsight - Azure | Документы Microsoft"
description: "Дополнительные сведения о Kafka Apache на HDInsight: что это такое, действие и начала примеры toofind и получение сведений."
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
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="ad3ca-103">Введение в Apache Kafka в HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="ad3ca-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="ad3ca-104">[Apache Kafka](https://kafka.apache.org) с открытым исходным кодом распределенных потоковой передачи платформой может быть в режиме реального времени используется toobuild потоковой передаче конвейеры данных и приложений.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="ad3ca-105">Kafka предоставляет брокера сообщений функциональность аналогичные tooa очереди сообщений, где вы можете публиковать и подписываться toonamed потоки данных.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-105">Kafka also provides message broker functionality similar tooa message queue, where you can publish and subscribe toonamed data streams.</span></span> <span data-ttu-id="ad3ca-106">Kafka на HDInsight предоставляет управляемый высокую степень масштабируемости и высокой доступности службы в облако Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in hello Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="ad3ca-107">Преимущества Apache Kafka в HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad3ca-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="ad3ca-108">Kafka предоставляет hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="ad3ca-108">Kafka provides hello following features:</span></span>

* <span data-ttu-id="ad3ca-109">Шаблон обмена сообщениями публикации подписки: Kafka предоставляет API производителя для публикации записей tooa Kafka раздела.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records tooa Kafka topic.</span></span> <span data-ttu-id="ad3ca-110">Hello потребителя API используется в том случае, если подписка tooa раздела.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-110">hello Consumer API is used when subscribing tooa topic.</span></span>

* <span data-ttu-id="ad3ca-111">Потоковая обработка. Kafka часто используется с Apache Storm или Spark для потоковой обработки в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="ad3ca-112">Kafka 0.10.0.0 (HDInsight версии 3.5) появился потоковой передачи API, который позволяет вам toobuild потоковой передачи решений без необходимости ураган или Spark.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you toobuild streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="ad3ca-113">Горизонтальное масштабирование: Kafka секции потоки для hello узлов кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-113">Horizontal scale: Kafka partitions streams across hello nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="ad3ca-114">Потребитель процессы можно связать с отдельными секциями tooprovide балансировки нагрузки при использовании записей.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-114">Consumer processes can be associated with individual partitions tooprovide load balancing when consuming records.</span></span>

* <span data-ttu-id="ad3ca-115">Порядок доставки: В каждой секции хранятся записи в потоке hello в порядке hello, которой они были получены.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-115">In-order delivery: Within each partition, records are stored in hello stream in hello order that they were received.</span></span> <span data-ttu-id="ad3ca-116">Достаточно связать один процесс пользователя с секцией — и записи будут обрабатываться в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="ad3ca-117">Отказоустойчивое: Секции могут быть реплицированы между узлами tooprovide устойчивость к сбоям.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-117">Fault-tolerant: Partitions can be replicated between nodes tooprovide fault tolerance.</span></span>

* <span data-ttu-id="ad3ca-118">Интеграция с Azure управляемых дисков: управляемый дисков предоставляет выше масштабируемость и пропускную способность для hello дисков, используемых виртуальными машинами hello hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for hello disks used by hello virtual machines in hello HDInsight cluster.</span></span>

    <span data-ttu-id="ad3ca-119">Управляемый дисков включены по умолчанию для Kafka на HDInsight и hello количество дисков, используемые для каждого узла можно настроить во время создания HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-119">Managed disks are enabled by default for Kafka on HDInsight, and hello number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="ad3ca-120">См. дополнительные сведения об [управляемых дисках Azure](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad3ca-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="ad3ca-121">См. сведения о [настройке числа управляемых дисков и повышении степени масштабируемости для Kafka в HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="ad3ca-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="ad3ca-122">Варианты использования</span><span class="sxs-lookup"><span data-stu-id="ad3ca-122">Use cases</span></span>

* <span data-ttu-id="ad3ca-123">**Обмен сообщениями**: так как он поддерживает hello сообщение шаблон публикации подписки, Kafka часто используется в качестве брокер обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-123">**Messaging**: Since it supports hello publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="ad3ca-124">**Отслеживание действий**: поскольку Kafka обеспечивает ведение журналов в порядке записей, его можно использовать tootrack и повторного создания действий.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used tootrack and re-create activities.</span></span> <span data-ttu-id="ad3ca-125">Например, действий пользователя на веб-сайте или в приложении.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="ad3ca-126">**Агрегат**: обработка потока можно объединять данные из разных потоков toocombine и централизовать сведения hello в рабочих данных.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-126">**Aggregation**: Using stream processing, you can aggregate information from different streams toocombine and centralize hello information into operational data.</span></span>

* <span data-ttu-id="ad3ca-127">**Преобразование.** С помощью потоковой обработки можно объединять и дополнять данные из нескольких входных разделов в один или несколько выходных разделов.</span><span class="sxs-lookup"><span data-stu-id="ad3ca-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad3ca-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad3ca-128">Next steps</span></span>

<span data-ttu-id="ad3ca-129">Используйте hello следующие ссылки toolearn как toouse Kafka Apache на HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ad3ca-129">Use hello following links toolearn how toouse Apache Kafka on HDInsight:</span></span>

* <span data-ttu-id="ad3ca-130">[Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))</span><span class="sxs-lookup"><span data-stu-id="ad3ca-130">[Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)</span></span>

* [<span data-ttu-id="ad3ca-131">Используйте MirrorMaker toocreate реплику Kafka в HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad3ca-131">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="ad3ca-132">Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad3ca-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="ad3ca-133">Совместное использование Apache Spark и Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad3ca-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="ad3ca-134">Подключение через виртуальную сеть Azure tooKafka</span><span class="sxs-lookup"><span data-stu-id="ad3ca-134">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
