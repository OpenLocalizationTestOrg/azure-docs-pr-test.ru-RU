---
title: "aaaUse Pig для Hadoop с помощью PowerShell в HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как кластера tooa задания Pig toosubmit Hadoop в HDInsight с помощью Azure PowerShell."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a><span data-ttu-id="16c6d-103">Используйте задания Pig toorun Azure PowerShell с HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c6d-103">Use Azure PowerShell toorun Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="16c6d-104">Этот документ содержит пример использования tooa задания Hadoop для Azure PowerShell toosubmit Pig в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="16c6d-104">This document provides an example of using Azure PowerShell toosubmit Pig jobs tooa Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="16c6d-105">Pig позволяет задания MapReduce toowrite языке (Pig латиница) моделирует преобразования данных, вместо сопоставления и уменьшения функции.</span><span class="sxs-lookup"><span data-stu-id="16c6d-105">Pig allows you toowrite MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="16c6d-106">Этот документ не предоставляет подробное описание действий hello латиница Pig инструкций, используемых в примерах hello.</span><span class="sxs-lookup"><span data-stu-id="16c6d-106">This document does not provide a detailed description of what hello Pig Latin statements used in hello examples do.</span></span> <span data-ttu-id="16c6d-107">Сведения о hello латиница Pig, используемых в этом примере содержатся [использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="16c6d-107">For information about hello Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="16c6d-108"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="16c6d-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="16c6d-109">**Кластер Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="16c6d-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="16c6d-110">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="16c6d-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="16c6d-111">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="16c6d-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="16c6d-112"><seg>
  **Рабочая станция с Azure PowerShell**.</seg></span><span class="sxs-lookup"><span data-stu-id="16c6d-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="16c6d-113"><a id="powershell"></a>Выполнение заданий Pig с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="16c6d-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="16c6d-114">Azure PowerShell предоставляет *командлеты* , которые позволяют tooremotely запуска задания Pig в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="16c6d-114">Azure PowerShell provides *cmdlets* that allow you tooremotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="16c6d-115">На внутреннем уровне PowerShell использует вызовы REST слишком[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) работающих в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="16c6d-115">Internally, PowerShell uses REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="16c6d-116">Hello используются следующие командлеты для выполнения заданий Pig на удаленный кластер HDInsight:</span><span class="sxs-lookup"><span data-stu-id="16c6d-116">hello following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="16c6d-117">**AzureRmAccount входа**: tooyour Azure PowerShell выполняет проверку подлинности подписки Azure</span><span class="sxs-lookup"><span data-stu-id="16c6d-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure Subscription</span></span>
* <span data-ttu-id="16c6d-118">**Новый AzureRmHDInsightPigJobDefinition**: создает *определение задания* с помощью hello указан инструкций Латинская Pig</span><span class="sxs-lookup"><span data-stu-id="16c6d-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using hello specified Pig Latin statements</span></span>
* <span data-ttu-id="16c6d-119">**Начало AzureRmHDInsightJob**: отправляет tooHDInsight определение задания hello, запускает задание hello и возвращает *задания* объект, который может быть используется toocheck hello состояние задания hello</span><span class="sxs-lookup"><span data-stu-id="16c6d-119">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="16c6d-120">**Ожидание AzureRmHDInsightJob**: использует hello объекта toocheck hello состояния заданий hello задания.</span><span class="sxs-lookup"><span data-stu-id="16c6d-120">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="16c6d-121">Он ожидает завершения задания hello или превышения времени ожидания hello.</span><span class="sxs-lookup"><span data-stu-id="16c6d-121">It waits until hello job has completed, or hello wait time has been exceeded.</span></span>
* <span data-ttu-id="16c6d-122">**Get-AzureRmHDInsightJobOutput**: использовать tooretrieve hello выходные данные задания hello</span><span class="sxs-lookup"><span data-stu-id="16c6d-122">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>

<span data-ttu-id="16c6d-123">Hello следующие шаги показывают, как toouse toorun эти командлеты заданий в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="16c6d-123">hello following steps demonstrate how toouse these cmdlets toorun a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="16c6d-124">С помощью редактора, сохранить следующий код в виде hello **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="16c6d-124">Using an editor, save hello following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="16c6d-125">Откройте командную строку Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16c6d-125">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="16c6d-126">Изменить расположение каталогов toohello hello **pigjob.ps1** файла, а затем используйте следующий сценарий hello toorun hello:</span><span class="sxs-lookup"><span data-stu-id="16c6d-126">Change directories toohello location of hello **pigjob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="16c6d-127">Все запрашиваемые toolog в tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="16c6d-127">You are prompted toolog in tooyour Azure subscription.</span></span> <span data-ttu-id="16c6d-128">После этого появится для hello HTTPs/Admin учетную запись и пароль для кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="16c6d-128">Then, you are asked for hello HTTPs/Admin account name and password for hello HDInsight cluster.</span></span>

2. <span data-ttu-id="16c6d-129">После завершения задания hello, он должен возвращать сведения аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="16c6d-129">When hello job completes, it should return information similar toohello following text:</span></span>

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="16c6d-130"><a id="troubleshooting"></a>Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="16c6d-130"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="16c6d-131">Если данные не возвращаются при завершении задания hello, произошла ошибка во время обработки.</span><span class="sxs-lookup"><span data-stu-id="16c6d-131">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="16c6d-132">tooview сведения об ошибке для данного задания, добавить hello, следующая команда toohello конец hello **pigjob.ps1** файл, сохраните его и затем снова запустите ее.</span><span class="sxs-lookup"><span data-stu-id="16c6d-132">tooview error information for this job, add hello following command toohello end of hello **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="16c6d-133">Возвращает сведения hello, куда было записано tooSTDERR на сервере hello при выполнении задания hello и может помочь определить, почему происходит сбой задания hello.</span><span class="sxs-lookup"><span data-stu-id="16c6d-133">This returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="16c6d-134"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="16c6d-134"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="16c6d-135">Как видите, Azure PowerShell предоставляет toorun простой способ задания Pig в кластер HDInsight, состояние задания монитора hello и получить hello выход.</span><span class="sxs-lookup"><span data-stu-id="16c6d-135">As you can see, Azure PowerShell provides an easy way toorun Pig jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="16c6d-136"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16c6d-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="16c6d-137">Общая информация о Pig в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="16c6d-137">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="16c6d-138">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c6d-138">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="16c6d-139">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="16c6d-139">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="16c6d-140">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c6d-140">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="16c6d-141">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c6d-141">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
