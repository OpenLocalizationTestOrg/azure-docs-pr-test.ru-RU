---
title: "топологии Apache Storm aaaExample на HDInsight | Документы Microsoft"
description: "Список примеров топологий Storm, созданных и протестированных с помощью Apache Storm в HDInsight, включая базовые топологии на C# и Java, а также работа с концентраторами событий."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f9b1bdff-5928-4705-a76d-52fd200917cb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: b20299112f6489b7c99360f0a539fc732703c64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>Примеры топологий и компонентов Storm для Apache Storm в HDInsight

Hello ниже приведен список примеров создаются и поддерживаются корпорацией Майкрософт для использования с Apache Storm на HDInsight. Эти примеры охватывают широкий набор разделов, создание основные C# и tooworking топологии на Java с помощью служб Azure, такие как концентраторы событий, БД Cosmos, Power BI, база данных SQL, HBase на HDInsight и хранилище Azure. Некоторые примеры также показывают, как toowork с технологиями, отличных от Azure, или даже Microsoft, например SignalR и Socket.IO.

| Описание | Что демонстрирует | Язык или платформа |
|:--- |:--- |:--- |
| [Запись tooAzure хранилища Озера данных из Apache Storm](hdinsight-storm-write-data-lake-store.md) |Написание tooAzure хранилища Озера данных |Java |
| [Источник воронки и сита концентратора событий](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |Источник для hello Spout концентратора событий и молнии |Java |
| [Создание топологии Apache Storm на языке Java][5797064f] |Maven |Java |
| [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio][16fce2d1] |Средства HDInsight для Visual Studio |C#, Java |
| [Create multiple data streams in a C# Storm topology][ec5a4064] (Создание нескольких потоков данных в топологии Storm на C#) |Несколько потоков |C# |
| [Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (C#)][844d1d81] |Концентраторы событий |C# и Java |
| [Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md) |Концентраторы событий |Java |
| [Использование Power Bi toovisualize данных из топологии Storm][94d15238] |Power BI |C# |
| [Анализ полученных с датчиков данных с использованием Apache Storm, концентратора событий и базы данных HBase в службе HDInsight (Hadoop)][ab894747] |Концентраторы событий, HBase, Socket.IO, веб-панель мониторинга |C#, Java, JavaScript, HTML |
| [Обработка данных с датчиков автомобилей из концентраторов событий Azure с использованием средств Apache Storm в HDInsight][246ee964] |Концентраторы событий, Cosmos DB, Azure Storage Blob (WASB) |C#, Java |
| [Извлечения, преобразования и загрузки (ETL) из tooHBase концентраторов событий Azure с помощью Storm в HDInsight][b4b68194] |Концентраторы событий, HBase |C# |
| [Template C# Storm topology project for working with Azure services from Storm on HDInsight][ce0c02a2] (Шаблон проекта топологии на C# и Storm для работы со службами Azure из Storm в HDInsight) |Концентраторы событий, Cosmos DB, база данных SQL, HBase, SignalR |C#, Java |
| [EventHubs scalability example (Java & SCP.Net Hybrid)][d6c540e3] (Пример масштабируемости концентраторов событий (Java и SCP.Net Hybrid)) |Скорость обработки сообщений, концентраторы событий, база данных SQL |C#, Java |
| [Сопоставление событий с помощью Storm и HBase в HDInsight](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [Использование Python со Storm в HDInsight](hdinsight-storm-develop-python-topology.md) |Компоненты Python с топологией Flux |Python |
| [Использование Kafka со Storm в HDInsight](hdinsight-apache-storm-with-kafka.md) | Apache Storm чтение и запись tooApache Kafka | Java |

### <a name="next-steps"></a>Дальнейшие действия

* [Начало работы с примерами Storm Starter для аналитики больших данных в HDInsight под управлением Linux][2b8c3488]
* [Узнайте, как toodeploy и управление ими Storm топологии с Storm в HDInsight][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "Узнайте, как toocreate Storm на кластер HDInsight и с помощью hello мониторинга Storm toodeploy примеры топологий."
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "Узнайте, как toodeploy и управления ими топологий с помощью hello веб-панели мониторинга Storm и Storm пользовательского интерфейса или hello средства HDInsight для Visual Studio."
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "Узнайте, как toocreate топологии Storm C# с помощью hello средства HDInsight для Visual Studio."
[5797064f]: hdinsight-storm-develop-java-topology.md "Узнайте, как toocreate Storm топологии Java, используя Maven, путем создания топологии основные wordcount."
[94d15238]: hdinsight-storm-power-bi-topology.md "Показано, как tooPower toowrite данных бизнес-Аналитики из топологии на C#, затем создать диаграммы и панели мониторинга на основе данных hello."
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "Демонстрация реализованной на языке C# простой топологии Storm для подсчета статистики. Это также показывает, как toocreate несколько потоков данных в топологии на C#."
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "Узнайте, как tooread и запись данных из концентраторов событий Azure с Storm на HDInsight."
[ab894747]: hdinsight-storm-sensor-data-analysis.md "Узнайте, как визуализации с помощью D3.js toouse Apache Storm на HDInsight tooprocess датчик, данные из концентраторов событий Azure и (необязательно), сохраните ее tooHBase."
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "Узнайте, как toouse сообщений tooread Storm топологии из концентраторов событий Azure, читать документы из базы данных Azure Cosmos для ссылки на данные и сохранить данные tooAzure хранилища."
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "Несколько топологий toodemonstrate пропускная способность при чтении из концентраторов событий Azure и хранения tooSQL базы данных с помощью Apache Storm на HDInsight."
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "Узнайте, как tooread данные из концентраторов событий Azure, статистическое выражение и преобразование hello данных, а затем сохранить ее tooHBase на HDInsight."
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "Этот проект содержит шаблоны для toointeract spouts, винты и топологии с различными службами Azure как концентраторы событий, БД Cosmos и базы данных SQL."

