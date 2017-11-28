---
title: "aaaHigh доступности с помощью Apache Kafka - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как высокий уровень доступности tooensure Kafka Apache на Azure HDInsight. Узнайте, как секционирование toorebalance реплик в Kafka так, чтобы они находятся в разных доменах сбоя в hello регионе Azure, которая содержит HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="2bc7d-104">Высокий уровень доступности данных с Apache Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2bc7d-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="2bc7d-105">Узнайте, как tooconfigure реплики разделов для Kafka разделы tootake преимуществами аппаратным обеспечением стойка конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-105">Learn how tooconfigure partition replicas for Kafka topics tootake advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="2bc7d-106">Такая конфигурация обеспечивает доступность данных, хранящихся в Apache Kafka на HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-106">This configuration ensures hello availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="2bc7d-107">Домены сбоя и обновления с Kafka</span><span class="sxs-lookup"><span data-stu-id="2bc7d-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="2bc7d-108">Домен сбоя — это логическое объединение базового оборудования в центре обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="2bc7d-109">Все домены сбоя используют общий источник питания и сетевой коммутатор.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="2bc7d-110">в этих доменах сбоя распределения Hello виртуальных машин и управляемых дисков, которые реализуют hello узлы в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-110">hello virtual machines and managed disks that implement hello nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="2bc7d-111">Эта архитектура ограничивает hello потенциальное воздействие сбоев физического оборудования.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-111">This architecture limits hello potential impact of physical hardware failures.</span></span>

<span data-ttu-id="2bc7d-112">В каждом регионе Azure есть определенное количество доменов сбоя.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="2bc7d-113">Список доменов и hello количество доменов сбоя, они содержат см. в разделе hello [задает доступности](../virtual-machines/linux/regions-and-availability.md#availability-sets) документации.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-113">For a list of domains and hello number of fault domains they contain, see hello [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bc7d-114">В Kafka нет сведений о доменах сбоя.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="2bc7d-115">При создании раздела в Kafka, он может хранить все реплики разделов в hello одного домена.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-115">When you create a topic in Kafka, it may store all partition replicas in hello same fault domain.</span></span> <span data-ttu-id="2bc7d-116">toosolve эту проблему, мы предоставляем hello [Kafka секции измените баланс средство](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="2bc7d-116">toosolve this problem, we provide hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-toorebalance-partition-replicas"></a><span data-ttu-id="2bc7d-117">Когда toorebalance секции реплики</span><span class="sxs-lookup"><span data-stu-id="2bc7d-117">When toorebalance partition replicas</span></span>

<span data-ttu-id="2bc7d-118">tooensure hello максимальную доступность данных Kafka следует балансирования hello реплики разделов для раздела в следующий раз hello:</span><span class="sxs-lookup"><span data-stu-id="2bc7d-118">tooensure hello highest availability of your Kafka data, you should rebalance hello partition replicas for your topic at hello following times:</span></span>

* <span data-ttu-id="2bc7d-119">при создании раздела или секции;</span><span class="sxs-lookup"><span data-stu-id="2bc7d-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="2bc7d-120">при масштабировании кластера.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="2bc7d-121">Коэффициент репликации</span><span class="sxs-lookup"><span data-stu-id="2bc7d-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bc7d-122">Мы рекомендуем использовать регион Azure с тремя доменами сбоя и коэффициент репликации 3.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="2bc7d-123">Если необходимо использовать область, которая содержит только два домена сбоя, следует используйте репликации коэффициент 4 реплик hello toospread равномерно в двух доменах отказоустойчивости hello.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-123">If you must use a region that contains only two fault domains, use a replication factor of 4 toospread hello replicas evenly across hello two fault domains.</span></span>

<span data-ttu-id="2bc7d-124">Пример создания разделов и коэффициент репликации hello параметр см. в разделе hello [начинаться с Kafka на HDInsight](hdinsight-apache-kafka-get-started.md) документа.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-124">For an example of creating topics and setting hello replication factor, see hello [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-toorebalance-partition-replicas"></a><span data-ttu-id="2bc7d-125">Как toorebalance секции реплики</span><span class="sxs-lookup"><span data-stu-id="2bc7d-125">How toorebalance partition replicas</span></span>

<span data-ttu-id="2bc7d-126">Используйте hello [Kafka секции измените баланс средство](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance выбранных разделов.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-126">Use hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selected topics.</span></span> <span data-ttu-id="2bc7d-127">Это средство необходимо запускали с SSH сеанса toohello головного узла кластера Kafka.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-127">This tool must be ran from an SSH session toohello head node of your Kafka cluster.</span></span>

<span data-ttu-id="2bc7d-128">Дополнительные сведения о подключении с помощью SSH tooHDInsight см. в разделе [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.</span><span class="sxs-lookup"><span data-stu-id="2bc7d-128">For more information on connecting tooHDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bc7d-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2bc7d-129">Next steps</span></span>

* [<span data-ttu-id="2bc7d-130">Масштабируемость Kafka в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2bc7d-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="2bc7d-131">Зеркальное отображение Kafka в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2bc7d-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)