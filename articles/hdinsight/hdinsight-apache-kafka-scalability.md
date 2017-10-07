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
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>Настройка объема хранилища и уровня масштабируемости для Apache Kafka в HDInsight

Дополнительные сведения, способ использования tooconfigure hello количество дисков, управляемых Apache Kafka на HDInsight.

Kafka на HDInsight использует локальный диск hello hello виртуальных машин в кластере HDInsight hello. Поскольку Kafka является очень ввода-вывода большого объема, [управляемых дисков Azure](../virtual-machines/windows/managed-disks-overview.md) — используется tooprovide высокой пропускной способностью и выделить дополнительное хранилище для каждого узла. Если для Kafka традиционных виртуальных жестких дисков (VHD), каждый узел имеет ограниченный too1 ТБ. В управляемых дисков можно использовать несколько дисков tooachieve 16 ТБ для каждого узла в кластере hello.

Hello следующей схеме представлено сравнение Kafka на HDInsight перед управляемых дисков и Kafka на HDInsight с управляемых дисков:

![Схема: Kafka в HDInsight с одним виртуальным жестким диском для каждой виртуальной машины и с несколькими управляемыми дисками для каждой виртуальной машины](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>Настройка управляемых дисков на портале Azure

1. Следуйте указаниям hello hello [создать кластер HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello общих шагов toocreate кластера с помощью портала hello. Не завершить процесс создания портала hello.

2. Из hello __размер кластера__ колонки, используйте hello __дисков на рабочий узел__ поле tooconfigure hello число дисков.

    > [!NOTE]
    > Hello тип управляемого диска может быть либо __Стандартная__ (HDD) или __Premium__ (SSD). Диски категории "Премиум" используются с виртуальными машинами серий DS и GS. Для всех остальных виртуальных машин используются стандартные управляемые диски.

    ![Изображение hello колонка размер кластера с hello дисков на рабочий узел выделен](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>Настройка управляемых дисков с использованием шаблона Resource Manager

toocontrol число hello диски, используемые hello рабочих узлов в кластере Kafka hello используйте следующий раздел hello шаблона:

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

Полный шаблон, который демонстрирует, как tooconfigure Управление дисками можно найти [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).

## <a name="next-steps"></a>Дальнейшие действия

См. Дополнительные сведения о работе с Kafka на HDInsight hello следующие документы:

* [Используйте MirrorMaker toocreate реплику Kafka в HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Совместное использование Apache Spark и Kafka (предварительная версия) в HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Подключение через виртуальную сеть Azure tooKafka](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [Блог HDInsight об управляемых дисках в Kafka](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)