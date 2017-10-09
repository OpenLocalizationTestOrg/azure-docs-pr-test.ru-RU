---
title: "aaaInstall или обновить Mono на HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toouse конкретной версии моно с кластером HDInsight. Моно — используется toorun приложений .NET в кластерах HDInsight под управлением Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="f26a0-104">Установка или обновление Mono в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f26a0-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="f26a0-105">Узнайте, как tooinstall конкретную версию из [моно](https://www.mono-project.com) на HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f26a0-105">Learn how tooinstall a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="f26a0-106">Моно установлена в HDInsight 3.4 и выше и используется toorun приложений .NET.</span><span class="sxs-lookup"><span data-stu-id="f26a0-106">Mono is installed on HDInsight 3.4 and higher, and is used toorun .NET applications.</span></span> <span data-ttu-id="f26a0-107">Сведения о версии hello Mono, входящий в состав каждой версии HDInsight см. в разделе [управление версиями компонента HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f26a0-107">For information on hello version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="f26a0-108">tooinstall другой версии в кластере, используйте действие скрипта hello в этом документе.</span><span class="sxs-lookup"><span data-stu-id="f26a0-108">tooinstall a different version on your cluster, use hello script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="f26a0-109">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="f26a0-109">How it works</span></span>

<span data-ttu-id="f26a0-110">Этот сценарий принимает hello следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="f26a0-110">This script accepts hello following parameter:</span></span>

* <span data-ttu-id="f26a0-111">__Номер версии моно__: hello версии моно tooinstall.</span><span class="sxs-lookup"><span data-stu-id="f26a0-111">__Mono version number__: hello version of Mono tooinstall.</span></span> <span data-ttu-id="f26a0-112">Hello версии должны быть доступны из [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="f26a0-112">hello version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="f26a0-113">Hello скрипт устанавливает следующие пакеты моно hello:</span><span class="sxs-lookup"><span data-stu-id="f26a0-113">hello script installs hello following Mono packages:</span></span>

* <span data-ttu-id="f26a0-114">__mono-complete__;</span><span class="sxs-lookup"><span data-stu-id="f26a0-114">__mono-complete__</span></span>

* <span data-ttu-id="f26a0-115">__ca-certificates-mono__.</span><span class="sxs-lookup"><span data-stu-id="f26a0-115">__ca-certificates-mono__</span></span>

## <a name="hello-script"></a><span data-ttu-id="f26a0-116">сценарий Hello</span><span class="sxs-lookup"><span data-stu-id="f26a0-116">hello script</span></span>

<span data-ttu-id="f26a0-117">__Расположение скрипта:__ [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="f26a0-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="f26a0-118">__Требования__</span><span class="sxs-lookup"><span data-stu-id="f26a0-118">__Requirements__:</span></span>

* <span data-ttu-id="f26a0-119">сценарий Hello должен применяться hello __head узлы__ и __рабочих узлов__.</span><span class="sxs-lookup"><span data-stu-id="f26a0-119">hello script must be applied on hello __head nodes__ and __worker nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="f26a0-120">сценарий toouse hello</span><span class="sxs-lookup"><span data-stu-id="f26a0-120">toouse hello script</span></span>

<span data-ttu-id="f26a0-121">Сведения о toouse этот сценарий с HDInsight, в статье hello [HDInsight под управлением Linux, настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) документа.</span><span class="sxs-lookup"><span data-stu-id="f26a0-121">For information on how toouse this script with HDInsight, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="f26a0-122">Можно использовать сценарий hello hello портал Azure, Azure PowerShell или hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f26a0-122">You can use hello script through hello Azure portal, Azure PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="f26a0-123">Во время следующих hello документ действие скрипта, используйте hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="f26a0-123">While following hello script action document, use hello following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="f26a0-124">При настройке HDInsight с помощью этого сценария необходимо пометить hello скрипта как __Persisted__.</span><span class="sxs-lookup"><span data-stu-id="f26a0-124">When configuring HDInsight with this script, mark hello script as __Persisted__.</span></span> <span data-ttu-id="f26a0-125">Этот параметр позволяет HDInsight tooapply hello скрипт tooworker узлы, добавленные с помощью операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="f26a0-125">This setting allows HDInsight tooapply hello script tooworker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f26a0-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f26a0-126">Next steps</span></span>

<span data-ttu-id="f26a0-127">Вы узнали, как tooupgrade или установить определенную версию Mono на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f26a0-127">You have learned how tooupgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="f26a0-128">См. Дополнительные сведения об использовании приложений .NET с моно на HDInsight hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="f26a0-128">For more information on using .NET applications with Mono on HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="f26a0-129">[Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md);</span><span class="sxs-lookup"><span data-stu-id="f26a0-129">[Use .NET for streaming MapReduce on HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)</span></span>
* <span data-ttu-id="f26a0-130">[Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md);</span><span class="sxs-lookup"><span data-stu-id="f26a0-130">[Use .NET with Hive and Pig on HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)</span></span>
* <span data-ttu-id="f26a0-131">[Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md);</span><span class="sxs-lookup"><span data-stu-id="f26a0-131">[Develop C# solutions with Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md)</span></span>
* [<span data-ttu-id="f26a0-132">Перенос решений .NET на основе tooLinux HDInsight</span><span class="sxs-lookup"><span data-stu-id="f26a0-132">Migrate .NET solutions tooLinux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="f26a0-133">Дополнительные сведения об использовании действий скрипта см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f26a0-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>