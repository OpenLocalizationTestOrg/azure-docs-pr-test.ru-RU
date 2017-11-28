---
title: "Установка или обновление Mono в HDInsight — Azure | Документы Майкрософт"
description: "Сведения об использовании конкретной версии Mono с кластером HDInsight. Mono используется для запуска приложений .NET в кластерах HDInsight под управлением Linux."
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
ms.openlocfilehash: fd284542e1de65f323f1e3a092689f847e025be6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="8339d-104">Установка или обновление Mono в HDInsight</span><span class="sxs-lookup"><span data-stu-id="8339d-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="8339d-105">Сведения об установке конкретной версии [Mono](https://www.mono-project.com) в HDInsight версии 3.4 или выше.</span><span class="sxs-lookup"><span data-stu-id="8339d-105">Learn how to install a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="8339d-106">Mono устанавливается на HDInsight версии 3.4 и выше и используется для запуска приложений .NET.</span><span class="sxs-lookup"><span data-stu-id="8339d-106">Mono is installed on HDInsight 3.4 and higher, and is used to run .NET applications.</span></span> <span data-ttu-id="8339d-107">Сведения о версии Mono, которая входит в состав каждой версии HDInsight, см. в статье [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="8339d-107">For information on the version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="8339d-108">Чтобы установить разные версии в кластере, используйте действия скрипта, рассматриваемые в этом документе.</span><span class="sxs-lookup"><span data-stu-id="8339d-108">To install a different version on your cluster, use the script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="8339d-109">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="8339d-109">How it works</span></span>

<span data-ttu-id="8339d-110">Этот скрипт принимает следующий параметр.</span><span class="sxs-lookup"><span data-stu-id="8339d-110">This script accepts the following parameter:</span></span>

* <span data-ttu-id="8339d-111">__Номер версии Mono.__ Версия Mono, которую необходимо установить.</span><span class="sxs-lookup"><span data-stu-id="8339d-111">__Mono version number__: The version of Mono to install.</span></span> <span data-ttu-id="8339d-112">Версия должна быть доступна по адресу [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="8339d-112">The version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="8339d-113">С помощью скрипта можно установить следующие пакеты Mono:</span><span class="sxs-lookup"><span data-stu-id="8339d-113">The script installs the following Mono packages:</span></span>

* <span data-ttu-id="8339d-114">__mono-complete__;</span><span class="sxs-lookup"><span data-stu-id="8339d-114">__mono-complete__</span></span>

* <span data-ttu-id="8339d-115">__ca-certificates-mono__.</span><span class="sxs-lookup"><span data-stu-id="8339d-115">__ca-certificates-mono__</span></span>

## <a name="the-script"></a><span data-ttu-id="8339d-116">Сценарий</span><span class="sxs-lookup"><span data-stu-id="8339d-116">The script</span></span>

<span data-ttu-id="8339d-117">__Расположение скрипта:__ [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="8339d-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="8339d-118">__Требования__</span><span class="sxs-lookup"><span data-stu-id="8339d-118">__Requirements__:</span></span>

* <span data-ttu-id="8339d-119">Скрипт должен применяться к __головным узлам__ и __рабочим узлам__.</span><span class="sxs-lookup"><span data-stu-id="8339d-119">The script must be applied on the __head nodes__ and __worker nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="8339d-120">Использование скрипта</span><span class="sxs-lookup"><span data-stu-id="8339d-120">To use the script</span></span>

<span data-ttu-id="8339d-121">Сведения об использовании этого скрипта с HDInsight см. в документе [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster).</span><span class="sxs-lookup"><span data-stu-id="8339d-121">For information on how to use this script with HDInsight, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="8339d-122">Вы можете использовать скрипт с помощью портала Azure, Azure PowerShell или интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="8339d-122">You can use the script through the Azure portal, Azure PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="8339d-123">При выполнении документа со сведениями о действиях скрипта используйте следующий универсальный код ресурса (URI):</span><span class="sxs-lookup"><span data-stu-id="8339d-123">While following the script action document, use the following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="8339d-124">Чтобы настроить HDInsight с помощью этого скрипта, пометьте скрипт как __сохраненный__.</span><span class="sxs-lookup"><span data-stu-id="8339d-124">When configuring HDInsight with this script, mark the script as __Persisted__.</span></span> <span data-ttu-id="8339d-125">Этот параметр позволяет HDInsight применять скрипт к рабочим узлам, добавленным с помощью операций масштабирования.</span><span class="sxs-lookup"><span data-stu-id="8339d-125">This setting allows HDInsight to apply the script to worker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8339d-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8339d-126">Next steps</span></span>

<span data-ttu-id="8339d-127">Вы узнали, как обновить или установить конкретную версию Mono в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8339d-127">You have learned how to upgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="8339d-128">Дополнительные сведения об использовании приложений .NET в HDInsight см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="8339d-128">For more information on using .NET applications with Mono on HDInsight, see the following documents:</span></span>

* <span data-ttu-id="8339d-129">[Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md);</span><span class="sxs-lookup"><span data-stu-id="8339d-129">[Use .NET for streaming MapReduce on HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)</span></span>
* <span data-ttu-id="8339d-130">[Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md);</span><span class="sxs-lookup"><span data-stu-id="8339d-130">[Use .NET with Hive and Pig on HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)</span></span>
* <span data-ttu-id="8339d-131">[Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md);</span><span class="sxs-lookup"><span data-stu-id="8339d-131">[Develop C# solutions with Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md)</span></span>
* <span data-ttu-id="8339d-132">[Перенос решений .NET из HDInsight под управлением Windows в HDInsight под управлением Linux](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8339d-132">[Migrate .NET solutions to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)</span></span>

<span data-ttu-id="8339d-133">Дополнительные сведения об использовании действий скрипта см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8339d-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>