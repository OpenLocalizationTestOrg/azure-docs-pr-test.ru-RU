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
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>Введение в Apache Kafka в HDInsight (предварительная версия)

[Apache Kafka](https://kafka.apache.org) с открытым исходным кодом распределенных потоковой передачи платформой может быть в режиме реального времени используется toobuild потоковой передаче конвейеры данных и приложений. Kafka предоставляет брокера сообщений функциональность аналогичные tooa очереди сообщений, где вы можете публиковать и подписываться toonamed потоки данных. Kafka на HDInsight предоставляет управляемый высокую степень масштабируемости и высокой доступности службы в облако Microsoft Azure hello.

## <a name="why-use-kafka-on-hdinsight"></a>Преимущества Apache Kafka в HDInsight

Kafka предоставляет hello следующие атрибуты:

* Шаблон обмена сообщениями публикации подписки: Kafka предоставляет API производителя для публикации записей tooa Kafka раздела. Hello потребителя API используется в том случае, если подписка tooa раздела.

* Потоковая обработка. Kafka часто используется с Apache Storm или Spark для потоковой обработки в режиме реального времени. Kafka 0.10.0.0 (HDInsight версии 3.5) появился потоковой передачи API, который позволяет вам toobuild потоковой передачи решений без необходимости ураган или Spark.

* Горизонтальное масштабирование: Kafka секции потоки для hello узлов кластера HDInsight hello. Потребитель процессы можно связать с отдельными секциями tooprovide балансировки нагрузки при использовании записей.

* Порядок доставки: В каждой секции хранятся записи в потоке hello в порядке hello, которой они были получены. Достаточно связать один процесс пользователя с секцией — и записи будут обрабатываться в определенном порядке.

* Отказоустойчивое: Секции могут быть реплицированы между узлами tooprovide устойчивость к сбоям.

* Интеграция с Azure управляемых дисков: управляемый дисков предоставляет выше масштабируемость и пропускную способность для hello дисков, используемых виртуальными машинами hello hello кластера HDInsight.

    Управляемый дисков включены по умолчанию для Kafka на HDInsight и hello количество дисков, используемые для каждого узла можно настроить во время создания HDInsight. См. дополнительные сведения об [управляемых дисках Azure](../virtual-machines/windows/managed-disks-overview.md).

    См. сведения о [настройке числа управляемых дисков и повышении степени масштабируемости для Kafka в HDInsight](hdinsight-apache-kafka-scalability.md).

## <a name="use-cases"></a>Варианты использования

* **Обмен сообщениями**: так как он поддерживает hello сообщение шаблон публикации подписки, Kafka часто используется в качестве брокер обмена сообщениями.

* **Отслеживание действий**: поскольку Kafka обеспечивает ведение журналов в порядке записей, его можно использовать tootrack и повторного создания действий. Например, действий пользователя на веб-сайте или в приложении.

* **Агрегат**: обработка потока можно объединять данные из разных потоков toocombine и централизовать сведения hello в рабочих данных.

* **Преобразование.** С помощью потоковой обработки можно объединять и дополнять данные из нескольких входных разделов в один или несколько выходных разделов.

## <a name="next-steps"></a>Дальнейшие действия

Используйте hello следующие ссылки toolearn как toouse Kafka Apache на HDInsight:

* [Get started with Apache Kafka on HDInsight (preview)](hdinsight-apache-kafka-get-started.md) (Приступая к работе с Apache Kafka в HDInsight (предварительная версия))

* [Используйте MirrorMaker toocreate реплику Kafka в HDInsight](hdinsight-apache-kafka-mirroring.md)

* [Совместное использование Apache Kafka (предварительная версия) и Storm в HDInsight](hdinsight-apache-storm-with-kafka.md)

* [Совместное использование Apache Spark и Kafka (предварительная версия) в HDInsight](hdinsight-apache-spark-with-kafka.md)

* [Подключение через виртуальную сеть Azure tooKafka](hdinsight-apache-kafka-connect-vpn-gateway.md)
