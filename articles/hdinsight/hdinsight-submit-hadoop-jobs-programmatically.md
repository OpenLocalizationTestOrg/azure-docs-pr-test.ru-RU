---
title: "Отправка заданий Hadoop в HDInsight | Документация Майкрософт"
description: "Вы узнаете, как отправлять задания Hadoop в HDInsight для платформы Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 50430b96-2329-4775-9713-19c5795b775f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 6829ff82afc7fcea9e027ad14ec7ed0c8015a5fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="submit-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="66b8a-103">Отправка заданий Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="66b8a-103">Submit Hadoop jobs in HDInsight</span></span>

<span data-ttu-id="66b8a-104">Задания Hadoop можно отправлять с помощью пакета SDK для .NET, Curl и Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="66b8a-104">You can submit Hadoop jobs using .NET SDK, Curl, and Azure PowerShell:</span></span>

- <span data-ttu-id="66b8a-105">Использование пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="66b8a-105">Use .NET SDK</span></span>

  - [<span data-ttu-id="66b8a-106">Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="66b8a-106">Create non-interactive authentication .NET applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)
  - [<span data-ttu-id="66b8a-107">Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET</span><span class="sxs-lookup"><span data-stu-id="66b8a-107">Run Hive queries using HDInsight .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
  - [<span data-ttu-id="66b8a-108">Выполнение заданий Pig с помощью пакета SDK для .NET для Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="66b8a-108">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md)
  - [<span data-ttu-id="66b8a-109">Выполнение заданий Sqoop с помощью пакета SDK для .NET для Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="66b8a-109">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)
  - [<span data-ttu-id="66b8a-110">Выполнение заданий MapReduce с использованием пакета SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="66b8a-110">Run MapReduce jobs using HDInsight .NET SDK</span></span>](hdinsight-hadoop-use-mapreduce-dotnet-sdk.md)

- <span data-ttu-id="66b8a-111">CURL</span><span class="sxs-lookup"><span data-stu-id="66b8a-111">CURL</span></span>

  - [<span data-ttu-id="66b8a-112">Выполнение запросов Hive с Hadoop в HDInsight с помощью Curl</span><span class="sxs-lookup"><span data-stu-id="66b8a-112">Run Hive queries with Hadoop in HDInsight with Curl</span></span>](hdinsight-hadoop-use-hive-curl.md)
  - [<span data-ttu-id="66b8a-113">Выполнение заданий Pig с помощью Curl с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="66b8a-113">Run Pig jobs with Hadoop on HDInsight by using Curl</span></span>](hdinsight-hadoop-use-pig-curl.md)
  - [<span data-ttu-id="66b8a-114">Выполнение заданий Sqoop с Hadoop в HDInsight с помощью Curl</span><span class="sxs-lookup"><span data-stu-id="66b8a-114">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>](hdinsight-hadoop-use-sqoop-curl.md)
  - [<span data-ttu-id="66b8a-115">Выполнение заданий MapReduce с помощью Curl с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="66b8a-115">Run MapReduce jobs with Hadoop on HDInsight using Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)

- <span data-ttu-id="66b8a-116">PowerShell</span><span class="sxs-lookup"><span data-stu-id="66b8a-116">PowerShell</span></span>

  - [<span data-ttu-id="66b8a-117">Выполнение запросов Hive с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="66b8a-117">Run Hive queries using PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md)
  - [<span data-ttu-id="66b8a-118">Выполнение заданий Pig с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="66b8a-118">Run Pig jobs using PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md)
  - [<span data-ttu-id="66b8a-119">Выполнение заданий Sqoop с помощью Azure PowerShell для Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="66b8a-119">Use Sqoop with Hadoop in HDInsight</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)
  - [<span data-ttu-id="66b8a-120">Выполнение заданий MapReduce с помощью PowerShell с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="66b8a-120">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md)

## <a name="see-also"></a><span data-ttu-id="66b8a-121">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="66b8a-121">See also</span></span>

- [<span data-ttu-id="66b8a-122">Документация по Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="66b8a-122">Azure HDInsight Documentation</span></span>](https://docs.microsoft.com/azure/hdinsight/)