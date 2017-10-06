---
title: "aaaUse MapReduce и PowerShell со Hadoop - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse PowerShell tooremotely запуск заданий MapReduce с Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="31f32-103">Выполнение заданий MapReduce с помощью PowerShell с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="31f32-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="31f32-104">Этот документ содержит пример использования Azure PowerShell toorun задания MapReduce в Hadoop кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31f32-104">This document provides an example of using Azure PowerShell toorun a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="31f32-105"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="31f32-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="31f32-106">**Кластер Azure HDInsight (Hadoop в HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="31f32-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="31f32-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="31f32-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="31f32-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="31f32-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="31f32-109"><seg>
  **Рабочая станция с Azure PowerShell**.</seg></span><span class="sxs-lookup"><span data-stu-id="31f32-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="31f32-110"><a id="powershell"></a>Выполнение задания MapReduce с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="31f32-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="31f32-111">Azure PowerShell предоставляет *командлеты* , которые позволяют выполнить tooremotely задания MapReduce в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31f32-111">Azure PowerShell provides *cmdlets* that allow you tooremotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="31f32-112">На внутреннем уровне это достигается с помощью вызовов REST слишком[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (ранее называвшиеся Templeton) под управлением hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31f32-112">Internally, this is accomplished by using REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="31f32-113">Hello используются следующие командлеты для выполнения заданий MapReduce в удаленном кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31f32-113">hello following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="31f32-114">**AzureRmAccount входа**: tooyour Azure PowerShell выполняет проверку подлинности подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="31f32-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription.</span></span>

* <span data-ttu-id="31f32-115">**Новый AzureRmHDInsightMapReduceJobDefinition**: создает новый *определение задания* с помощью hello определенные сведения о MapReduce.</span><span class="sxs-lookup"><span data-stu-id="31f32-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using hello specified MapReduce information.</span></span>

* <span data-ttu-id="31f32-116">**Начало AzureRmHDInsightJob**: отправляет tooHDInsight определение задания hello, запускает задание hello и возвращает *задания* объект, который может быть используется toocheck hello состояние задания hello.</span><span class="sxs-lookup"><span data-stu-id="31f32-116">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job.</span></span>

* <span data-ttu-id="31f32-117">**Ожидание AzureRmHDInsightJob**: использует hello объекта toocheck hello состояния заданий hello задания.</span><span class="sxs-lookup"><span data-stu-id="31f32-117">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="31f32-118">Он ожидает завершения задания hello или превышено время ожидания hello.</span><span class="sxs-lookup"><span data-stu-id="31f32-118">It waits until hello job completes or hello wait time is exceeded.</span></span>

* <span data-ttu-id="31f32-119">**Get-AzureRmHDInsightJobOutput**: использовать tooretrieve hello выходные данные задания hello.</span><span class="sxs-lookup"><span data-stu-id="31f32-119">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job.</span></span>

<span data-ttu-id="31f32-120">Hello следующие шаги показывают, как toouse toorun эти командлеты заданий в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31f32-120">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="31f32-121">С помощью редактора, сохранить следующий код в виде hello **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="31f32-121">Using an editor, save hello following code as **mapreducejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="31f32-122">Откройте новую командную строку **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="31f32-122">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="31f32-123">Изменить расположение каталогов toohello hello **mapreducejob.ps1** файла, а затем используйте следующий сценарий hello toorun hello:</span><span class="sxs-lookup"><span data-stu-id="31f32-123">Change directories toohello location of hello **mapreducejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="31f32-124">При запуске скрипта hello, появится для hello имя кластера HDInsight hello hello HTTPS/Admin учетной записи имя и пароль для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="31f32-124">When you run hello script, you are prompted for hello name of hello HDInsight cluster and hello HTTPS/Admin account name and password for hello cluster.</span></span> <span data-ttu-id="31f32-125">Также может быть запросом tooauthenticate tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="31f32-125">You may also be prompted tooauthenticate tooyour Azure subscription.</span></span>

3. <span data-ttu-id="31f32-126">По завершении заданий hello появляется примерно toohello выходных данных после текста:</span><span class="sxs-lookup"><span data-stu-id="31f32-126">When hello job completes, you receive output similar toohello following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="31f32-127">Это выходные данные показывают, заданием hello успешно завершена.</span><span class="sxs-lookup"><span data-stu-id="31f32-127">This output indicates that hello job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="31f32-128">Если hello **ExitCode** представляет собой значение отличное от 0, в разделе [Устранение неполадок](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="31f32-128">If hello **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="31f32-129">В этом примере также хранит tooan файлы загружаются hello **output.txt** файл в каталоге hello при запуске сценария, hello.</span><span class="sxs-lookup"><span data-stu-id="31f32-129">This example also stores hello downloaded files tooan **output.txt** file in hello directory that you run hello script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="31f32-130">Просмотр выходных данных</span><span class="sxs-lookup"><span data-stu-id="31f32-130">View output</span></span>

<span data-ttu-id="31f32-131">Откройте hello **output.txt** файла в текстовый редактор toosee hello слов и число созданных заданием hello.</span><span class="sxs-lookup"><span data-stu-id="31f32-131">Open hello **output.txt** file in a text editor toosee hello words and counts produced by hello job.</span></span>

> [!NOTE]
> <span data-ttu-id="31f32-132">Hello выходных файлов задания MapReduce являются неизменяемыми.</span><span class="sxs-lookup"><span data-stu-id="31f32-132">hello output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="31f32-133">Поэтому при повторном запуске этого образца, требуется имя hello toochange hello выходного файла.</span><span class="sxs-lookup"><span data-stu-id="31f32-133">So if you rerun this sample, you need toochange hello name of hello output file.</span></span>

## <span data-ttu-id="31f32-134"><a id="troubleshooting"></a>Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="31f32-134"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="31f32-135">Если данные не возвращаются при завершении задания hello, произошла ошибка во время обработки.</span><span class="sxs-lookup"><span data-stu-id="31f32-135">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="31f32-136">tooview сведения об ошибке для данного задания, добавить hello, следующая команда toohello конец hello **mapreducejob.ps1** файл, сохраните его и затем снова запустите ее.</span><span class="sxs-lookup"><span data-stu-id="31f32-136">tooview error information for this job, add hello following command toohello end of hello **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="31f32-137">Этот командлет возвращает сведения hello, куда было записано tooSTDERR на сервере hello при выполнении задания hello и может помочь определить, почему происходит сбой задания hello.</span><span class="sxs-lookup"><span data-stu-id="31f32-137">This cmdlet returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="31f32-138"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="31f32-138"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="31f32-139">Как видите, Azure PowerShell предоставляет простой способ toorun задания MapReduce на кластер HDInsight, состояние задания монитора hello и получить hello выход.</span><span class="sxs-lookup"><span data-stu-id="31f32-139">As you can see, Azure PowerShell provides an easy way toorun MapReduce jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="31f32-140"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31f32-140"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="31f32-141">Общая информация о заданиях MapReduce в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="31f32-141">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="31f32-142">Использование MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="31f32-142">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="31f32-143">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="31f32-143">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="31f32-144">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="31f32-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="31f32-145">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="31f32-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
