---
title: "aaaDebug и анализировать службам Hadoop с дампы кучи - Azure | Документы Microsoft"
description: "Автоматически собирать дампы кучи для службы Hadoop и поместить внутрь hello учетной записи хранилища больших двоичных объектов Azure для отладки и анализа."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a>Собирать дампы кучи в toodebug хранилища больших двоичных объектов и анализировать службам Hadoop
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Файлы дампа кучи содержат снимок памяти приложения hello, включая hello значения переменных во время создания дампа hello hello. Поэтому они полезны для диагностики проблем, возникающих во время выполнения. Автоматически собираются для служб Hadoop и помещен внутрь hello учетной записи хранилища больших двоичных объектов Azure пользователя в группе HDInsightHeapDumps дампы кучи или.

Коллекция Hello дампов кучи для различных служб необходимо включить для служб на отдельных кластерах. по умолчанию Hello эта возможность отключена toobe для кластера. Эти файлы дампа кучи могут быть большими, поэтому его учетной записи хранилища больших двоичных объектов hello рекомендуется toomonitor они являются был сохранен после включения коллекции hello.

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement). Hello сведения в этой статье применяется только на основе tooWindows HDInsight. Сведения о HDInsight под управлением Linux см. в статье [Включение дампов кучи для служб Hadoop в HDInsight, работающей под управлением Linux (предварительная версия)](hdinsight-hadoop-collect-debug-heap-dump-linux.md).


## <a name="eligible-services-for-heap-dumps"></a>Службы с возможностью включения дампов кучи
Можно включить дампы кучи для hello следующие службы:

* **Hcatalog** — tempelton;
* **Hive** — hiveserver2, metastore, derbyserver;
* **Mapreduce** — jobhistoryserver;
* **Yarn** — resourcemanager, nodemanager, timelineserver;
* **HDFS** — datanode, secondarynamenode, namenode.

## <a name="configuration-elements-that-enable-heap-dumps"></a>Элементы конфигурации, активирующие дампы кучи
tooturn о дампах кучи для службы необходимы tooset hello соответствующей конфигурации элементы в разделе "hello" для этой службы, которая задана в **service_name**.

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

Здравствуйте, значение **service_name** может быть любой из перечисленных ниже служб hello: tempelton hiveserver2, метахранилище, derbyserver, jobhistoryserver, диспетчер ресурсов, nodemanager, timelineserver, datanode secondarynamenode, или namenode.

## <a name="enable-using-azure-powershell"></a>Включить при помощи Azure PowerShell
Например при tooturn о дампах кучи с помощью Azure PowerShell для jobhistoryserver можно использовать следующий скрипт hello:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a>Включить при помощи пакета SDK для .NET
Например tooturn о дампах кучи с помощью hello Azure HDInsight .NET SDK для jobhistoryserver используется hello, следующий код:

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
