---
title: "aaaApache Kafka увеличение масштаба - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как tooconfigure управление дисков для кластера Apache Kafka на масштабируемость tooincrease Azure HDInsight."
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
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="caf0c-103">Настройка объема хранилища и уровня масштабируемости для Apache Kafka в HDInsight</span><span class="sxs-lookup"><span data-stu-id="caf0c-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="caf0c-104">Дополнительные сведения, способ использования tooconfigure hello количество дисков, управляемых Apache Kafka на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="caf0c-104">Learn how tooconfigure hello number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="caf0c-105">Kafka на HDInsight использует локальный диск hello hello виртуальных машин в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="caf0c-105">Kafka on HDInsight uses hello local disk of hello virtual machines in hello HDInsight cluster.</span></span> <span data-ttu-id="caf0c-106">Поскольку Kafka является очень ввода-вывода большого объема, [управляемых дисков Azure](../virtual-machines/windows/managed-disks-overview.md) — используется tooprovide высокой пропускной способностью и выделить дополнительное хранилище для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="caf0c-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used tooprovide high throughput and provide more storage per node.</span></span> <span data-ttu-id="caf0c-107">Если для Kafka традиционных виртуальных жестких дисков (VHD), каждый узел имеет ограниченный too1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="caf0c-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited too1 TB.</span></span> <span data-ttu-id="caf0c-108">В управляемых дисков можно использовать несколько дисков tooachieve 16 ТБ для каждого узла в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="caf0c-108">With managed disks, you can use multiple disks tooachieve 16 TB for each node in hello cluster.</span></span>

<span data-ttu-id="caf0c-109">Hello следующей схеме представлено сравнение Kafka на HDInsight перед управляемых дисков и Kafka на HDInsight с управляемых дисков:</span><span class="sxs-lookup"><span data-stu-id="caf0c-109">hello following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Схема: Kafka в HDInsight с одним виртуальным жестким диском для каждой виртуальной машины и с несколькими управляемыми дисками для каждой виртуальной машины](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="caf0c-111">Настройка управляемых дисков на портале Azure</span><span class="sxs-lookup"><span data-stu-id="caf0c-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="caf0c-112">Следуйте указаниям hello hello [создать кластер HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello общих шагов toocreate кластера с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="caf0c-112">Follow hello steps in hello [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello common steps toocreate a cluster using hello portal.</span></span> <span data-ttu-id="caf0c-113">Не завершить процесс создания портала hello.</span><span class="sxs-lookup"><span data-stu-id="caf0c-113">Do not complete hello portal creation process.</span></span>

2. <span data-ttu-id="caf0c-114">Из hello __размер кластера__ колонки, используйте hello __дисков на рабочий узел__ поле tooconfigure hello число дисков.</span><span class="sxs-lookup"><span data-stu-id="caf0c-114">From hello __Cluster size__ blade, use hello __Disks per worker node__ field tooconfigure hello number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="caf0c-115">Hello тип управляемого диска может быть либо __Стандартная__ (HDD) или __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="caf0c-115">hello type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="caf0c-116">Диски категории "Премиум" используются с виртуальными машинами серий DS и GS.</span><span class="sxs-lookup"><span data-stu-id="caf0c-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="caf0c-117">Для всех остальных виртуальных машин используются стандартные управляемые диски.</span><span class="sxs-lookup"><span data-stu-id="caf0c-117">All other VM types use standard.</span></span>

    ![Изображение hello колонка размер кластера с hello дисков на рабочий узел выделен](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="caf0c-119">Настройка управляемых дисков с использованием шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="caf0c-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="caf0c-120">toocontrol число hello диски, используемые hello рабочих узлов в кластере Kafka hello используйте следующий раздел hello шаблона:</span><span class="sxs-lookup"><span data-stu-id="caf0c-120">toocontrol hello number of disks used by hello worker nodes in a Kafka cluster, use hello following section of hello template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="caf0c-121">Полный шаблон, который демонстрирует, как tooconfigure Управление дисками можно найти [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="caf0c-121">You can find a complete template that demonstrates how tooconfigure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="caf0c-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="caf0c-122">Next steps</span></span>

<span data-ttu-id="caf0c-123">См. Дополнительные сведения о работе с Kafka на HDInsight hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="caf0c-123">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="caf0c-124">Используйте MirrorMaker toocreate реплику Kafka в HDInsight</span><span class="sxs-lookup"><span data-stu-id="caf0c-124">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="caf0c-125">Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="caf0c-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="caf0c-126">Совместное использование Apache Spark и Kafka (предварительная версия) в HDInsight</span><span class="sxs-lookup"><span data-stu-id="caf0c-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="caf0c-127">Подключение через виртуальную сеть Azure tooKafka</span><span class="sxs-lookup"><span data-stu-id="caf0c-127">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="caf0c-128">Блог HDInsight об управляемых дисках в Kafka</span><span class="sxs-lookup"><span data-stu-id="caf0c-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)