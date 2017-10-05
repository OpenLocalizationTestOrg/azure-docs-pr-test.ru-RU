---
title: "Отладка и анализ служб Hadoop с помощью дампов кучи в Azure | Документы Майкрософт"
description: "Автоматически собирайте дампы кучи для служб Hadoop и размещайте их в учетной записи хранения BLOB-объектов Azure для отладки и анализа."
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
ms.openlocfilehash: 6d1d4d47d279eb7a1f0bf1f587445683f0ace7a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="collect-heap-dumps-in-blob-storage-to-debug-and-analyze-hadoop-services"></a><span data-ttu-id="14b33-103">Сбор дампов кучи в хранилище больших двоичных объектов для отладки и анализа служб Hadoop</span><span class="sxs-lookup"><span data-stu-id="14b33-103">Collect heap dumps in Blob storage to debug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="14b33-104">Дампы кучи содержат снимок памяти приложения, включая значения переменных на момент создания дампа.</span><span class="sxs-lookup"><span data-stu-id="14b33-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="14b33-105">Поэтому они полезны для диагностики проблем, возникающих во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="14b33-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="14b33-106">Сборка дампов кучи для служб Hadoop может выполняться автоматически, после чего они помещаются в учетную запись хранилища больших двоичных объектов Azure в раздел HDInsightHeapDumps/.</span><span class="sxs-lookup"><span data-stu-id="14b33-106">Heap dumps can be automatically collected for Hadoop services and placed inside the Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="14b33-107">Сбор дампов кучи для различных служб нужно включать на отдельных кластерах.</span><span class="sxs-lookup"><span data-stu-id="14b33-107">The collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="14b33-108">По умолчанию эта функция отключена.</span><span class="sxs-lookup"><span data-stu-id="14b33-108">The default for this feature is to be off for a cluster.</span></span> <span data-ttu-id="14b33-109">Размер дампов кучи может быть большим, поэтому мы советуем следить за учетной записью хранилища больших двоичных объектов после включения сбора.</span><span class="sxs-lookup"><span data-stu-id="14b33-109">These heap dumps can be large, so it is advisable to monitor the Blob storage account where they are being saved once the collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14b33-110">Linux — единственная операционная система, используемая для работы с HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="14b33-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="14b33-111">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="14b33-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="14b33-112">Сведения в этой статье применимы только к HDInsight, работающей под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="14b33-112">The information in this article only applies to Windows-based HDInsight.</span></span> <span data-ttu-id="14b33-113">Сведения о HDInsight под управлением Linux см. в статье [Включение дампов кучи для служб Hadoop в HDInsight, работающей под управлением Linux (предварительная версия)](hdinsight-hadoop-collect-debug-heap-dump-linux.md).</span><span class="sxs-lookup"><span data-stu-id="14b33-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="14b33-114">Службы с возможностью включения дампов кучи</span><span class="sxs-lookup"><span data-stu-id="14b33-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="14b33-115">Вы можете включить дампы кучи для следующих служб:</span><span class="sxs-lookup"><span data-stu-id="14b33-115">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="14b33-116">**Hcatalog** — tempelton;</span><span class="sxs-lookup"><span data-stu-id="14b33-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="14b33-117">**Hive** — hiveserver2, metastore, derbyserver;</span><span class="sxs-lookup"><span data-stu-id="14b33-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="14b33-118">**Mapreduce** — jobhistoryserver;</span><span class="sxs-lookup"><span data-stu-id="14b33-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="14b33-119">**Yarn** — resourcemanager, nodemanager, timelineserver;</span><span class="sxs-lookup"><span data-stu-id="14b33-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="14b33-120">**HDFS** — datanode, secondarynamenode, namenode.</span><span class="sxs-lookup"><span data-stu-id="14b33-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="14b33-121">Элементы конфигурации, активирующие дампы кучи</span><span class="sxs-lookup"><span data-stu-id="14b33-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="14b33-122">Чтобы включить дампы кучи для службы, необходимо задать необходимые элементы конфигурации в разделе для этой службы, обозначенном аргументом **service_name**.</span><span class="sxs-lookup"><span data-stu-id="14b33-122">To turn on heap dumps for a service, you need to set the appropriate configuration elements in the section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="14b33-123">Значением **service_name** может быть любая из следующих служб: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode или namenode.</span><span class="sxs-lookup"><span data-stu-id="14b33-123">The value of **service_name** can be any of the services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="14b33-124">Включить при помощи Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="14b33-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="14b33-125">Например, чтобы включить дампы кучи с помощью Azure PowerShell для jobhistoryserver, можно использовать следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="14b33-125">For example, to turn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use the following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="14b33-126">Включить при помощи пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="14b33-126">Enable using .NET SDK</span></span>
<span data-ttu-id="14b33-127">Например, чтобы включить дампы кучи с помощью пакета SDK .NET для Azure HDInsight для jobhistoryserver, можно использовать следующий код:</span><span class="sxs-lookup"><span data-stu-id="14b33-127">For example, to turn on heap dumps by using the Azure HDInsight .NET SDK for jobhistoryserver, you can use the following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
