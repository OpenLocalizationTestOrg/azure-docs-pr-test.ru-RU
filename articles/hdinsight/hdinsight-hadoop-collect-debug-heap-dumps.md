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
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a><span data-ttu-id="36bf2-103">Собирать дампы кучи в toodebug хранилища больших двоичных объектов и анализировать службам Hadoop</span><span class="sxs-lookup"><span data-stu-id="36bf2-103">Collect heap dumps in Blob storage toodebug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="36bf2-104">Файлы дампа кучи содержат снимок памяти приложения hello, включая hello значения переменных во время создания дампа hello hello.</span><span class="sxs-lookup"><span data-stu-id="36bf2-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="36bf2-105">Поэтому они полезны для диагностики проблем, возникающих во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="36bf2-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="36bf2-106">Автоматически собираются для служб Hadoop и помещен внутрь hello учетной записи хранилища больших двоичных объектов Azure пользователя в группе HDInsightHeapDumps дампы кучи или.</span><span class="sxs-lookup"><span data-stu-id="36bf2-106">Heap dumps can be automatically collected for Hadoop services and placed inside hello Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="36bf2-107">Коллекция Hello дампов кучи для различных служб необходимо включить для служб на отдельных кластерах.</span><span class="sxs-lookup"><span data-stu-id="36bf2-107">hello collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="36bf2-108">по умолчанию Hello эта возможность отключена toobe для кластера.</span><span class="sxs-lookup"><span data-stu-id="36bf2-108">hello default for this feature is toobe off for a cluster.</span></span> <span data-ttu-id="36bf2-109">Эти файлы дампа кучи могут быть большими, поэтому его учетной записи хранилища больших двоичных объектов hello рекомендуется toomonitor они являются был сохранен после включения коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="36bf2-109">These heap dumps can be large, so it is advisable toomonitor hello Blob storage account where they are being saved once hello collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36bf2-110">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="36bf2-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="36bf2-111">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="36bf2-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="36bf2-112">Hello сведения в этой статье применяется только на основе tooWindows HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36bf2-112">hello information in this article only applies tooWindows-based HDInsight.</span></span> <span data-ttu-id="36bf2-113">Сведения о HDInsight под управлением Linux см. в статье [Включение дампов кучи для служб Hadoop в HDInsight, работающей под управлением Linux (предварительная версия)](hdinsight-hadoop-collect-debug-heap-dump-linux.md).</span><span class="sxs-lookup"><span data-stu-id="36bf2-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="36bf2-114">Службы с возможностью включения дампов кучи</span><span class="sxs-lookup"><span data-stu-id="36bf2-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="36bf2-115">Можно включить дампы кучи для hello следующие службы:</span><span class="sxs-lookup"><span data-stu-id="36bf2-115">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="36bf2-116">**Hcatalog** — tempelton;</span><span class="sxs-lookup"><span data-stu-id="36bf2-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="36bf2-117">**Hive** — hiveserver2, metastore, derbyserver;</span><span class="sxs-lookup"><span data-stu-id="36bf2-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="36bf2-118">**Mapreduce** — jobhistoryserver;</span><span class="sxs-lookup"><span data-stu-id="36bf2-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="36bf2-119">**Yarn** — resourcemanager, nodemanager, timelineserver;</span><span class="sxs-lookup"><span data-stu-id="36bf2-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="36bf2-120">**HDFS** — datanode, secondarynamenode, namenode.</span><span class="sxs-lookup"><span data-stu-id="36bf2-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="36bf2-121">Элементы конфигурации, активирующие дампы кучи</span><span class="sxs-lookup"><span data-stu-id="36bf2-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="36bf2-122">tooturn о дампах кучи для службы необходимы tooset hello соответствующей конфигурации элементы в разделе "hello" для этой службы, которая задана в **service_name**.</span><span class="sxs-lookup"><span data-stu-id="36bf2-122">tooturn on heap dumps for a service, you need tooset hello appropriate configuration elements in hello section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="36bf2-123">Здравствуйте, значение **service_name** может быть любой из перечисленных ниже служб hello: tempelton hiveserver2, метахранилище, derbyserver, jobhistoryserver, диспетчер ресурсов, nodemanager, timelineserver, datanode secondarynamenode, или namenode.</span><span class="sxs-lookup"><span data-stu-id="36bf2-123">hello value of **service_name** can be any of hello services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="36bf2-124">Включить при помощи Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="36bf2-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="36bf2-125">Например при tooturn о дампах кучи с помощью Azure PowerShell для jobhistoryserver можно использовать следующий скрипт hello:</span><span class="sxs-lookup"><span data-stu-id="36bf2-125">For example, tooturn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use hello following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="36bf2-126">Включить при помощи пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="36bf2-126">Enable using .NET SDK</span></span>
<span data-ttu-id="36bf2-127">Например tooturn о дампах кучи с помощью hello Azure HDInsight .NET SDK для jobhistoryserver используется hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="36bf2-127">For example, tooturn on heap dumps by using hello Azure HDInsight .NET SDK for jobhistoryserver, you can use hello following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
