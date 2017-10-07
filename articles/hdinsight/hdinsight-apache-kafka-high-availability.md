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
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a>Высокий уровень доступности данных с Apache Kafka (предварительная версия) в HDInsight

Узнайте, как tooconfigure реплики разделов для Kafka разделы tootake преимуществами аппаратным обеспечением стойка конфигурации. Такая конфигурация обеспечивает доступность данных, хранящихся в Apache Kafka на HDInsight hello.

## <a name="fault-and-update-domains-with-kafka"></a>Домены сбоя и обновления с Kafka

Домен сбоя — это логическое объединение базового оборудования в центре обработки данных Azure. Все домены сбоя используют общий источник питания и сетевой коммутатор. в этих доменах сбоя распределения Hello виртуальных машин и управляемых дисков, которые реализуют hello узлы в кластер HDInsight. Эта архитектура ограничивает hello потенциальное воздействие сбоев физического оборудования.

В каждом регионе Azure есть определенное количество доменов сбоя. Список доменов и hello количество доменов сбоя, они содержат см. в разделе hello [задает доступности](../virtual-machines/linux/regions-and-availability.md#availability-sets) документации.

> [!IMPORTANT]
> В Kafka нет сведений о доменах сбоя. При создании раздела в Kafka, он может хранить все реплики разделов в hello одного домена. toosolve эту проблему, мы предоставляем hello [Kafka секции измените баланс средство](https://github.com/hdinsight/hdinsight-kafka-tools).

## <a name="when-toorebalance-partition-replicas"></a>Когда toorebalance секции реплики

tooensure hello максимальную доступность данных Kafka следует балансирования hello реплики разделов для раздела в следующий раз hello:

* при создании раздела или секции;

* при масштабировании кластера.

## <a name="replication-factor"></a>Коэффициент репликации

> [!IMPORTANT]
> Мы рекомендуем использовать регион Azure с тремя доменами сбоя и коэффициент репликации 3.

Если необходимо использовать область, которая содержит только два домена сбоя, следует используйте репликации коэффициент 4 реплик hello toospread равномерно в двух доменах отказоустойчивости hello.

Пример создания разделов и коэффициент репликации hello параметр см. в разделе hello [начинаться с Kafka на HDInsight](hdinsight-apache-kafka-get-started.md) документа.

## <a name="how-toorebalance-partition-replicas"></a>Как toorebalance секции реплики

Используйте hello [Kafka секции измените баланс средство](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance выбранных разделов. Это средство необходимо запускали с SSH сеанса toohello головного узла кластера Kafka.

Дополнительные сведения о подключении с помощью SSH tooHDInsight см. в разделе [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.

## <a name="next-steps"></a>Дальнейшие действия

* [Масштабируемость Kafka в HDInsight](hdinsight-apache-kafka-scalability.md)
* [Зеркальное отображение Kafka в HDInsight](hdinsight-apache-kafka-mirroring.md)