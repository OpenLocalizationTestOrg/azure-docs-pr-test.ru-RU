---
title: "Использование Hadoop Pig с помощью PowerShell в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте, как отправлять задания Pig в кластер Hadoop в HDInsight с помощью Azure PowerShell."
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
ms.openlocfilehash: 28904b07609ffb40a8195278fd1afd3957896733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="cdb16-103">Использование Azure PowerShell для выполнения заданий Pig в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cdb16-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="cdb16-104">В этом документе приведен пример использования Azure PowerShell для отправки заданий Pig в Hadoop в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cdb16-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="cdb16-105">Pig позволяет написать задания MapReduce с использованием языка (Pig Latin), который моделирует преобразования данных, а не функции сопоставления и приведения.</span><span class="sxs-lookup"><span data-stu-id="cdb16-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="cdb16-106">В этом документе не приводится подробное описание процессов, которые выполняют операторы Pig Latin, используемые в примерах.</span><span class="sxs-lookup"><span data-stu-id="cdb16-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="cdb16-107">Информацию об операторах Pig Latin, используемых в данном примере, см. в статье [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="cdb16-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="cdb16-108"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cdb16-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="cdb16-109">**Кластер Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cdb16-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cdb16-110">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="cdb16-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cdb16-111">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cdb16-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="cdb16-112"><seg>
  **Рабочая станция с Azure PowerShell**.</seg></span><span class="sxs-lookup"><span data-stu-id="cdb16-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="cdb16-113"><a id="powershell"></a>Выполнение заданий Pig с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdb16-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="cdb16-114">Azure PowerShell предоставляет *командлеты* , позволяющие удаленно запускать задания Pig в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cdb16-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="cdb16-115">Во внутренних процессах PowerShell использует вызовы REST к [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat), выполняющемуся на кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cdb16-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="cdb16-116">При выполнении заданий Pig на удаленном кластере HDInsight используются следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="cdb16-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="cdb16-117">**Login-AzureRmAccount**— выполняет аутентификацию Azure PowerShell для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb16-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span></span>
* <span data-ttu-id="cdb16-118">**New-AzureRmHDInsightPigJobDefinition** — создает *определение задания* с использованием заданных операторов Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="cdb16-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span></span>
* <span data-ttu-id="cdb16-119">**Start-AzureRmHDInsightJob**— отправляет определение задания в HDInsight, запускает задание и возвращает объект- *задание* , который можно использовать для проверки состояния задания.</span><span class="sxs-lookup"><span data-stu-id="cdb16-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="cdb16-120">**Wait-AzureRmHDInsightJob**— использует объект-задание для проверки состояния задания.</span><span class="sxs-lookup"><span data-stu-id="cdb16-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="cdb16-121">Он ждет завершения задания или превышения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="cdb16-121">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="cdb16-122">**Get-AzureRmHDInsightJobOutput**— используется для получения выходных данных задания.</span><span class="sxs-lookup"><span data-stu-id="cdb16-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>

<span data-ttu-id="cdb16-123">Следующие шаги показывают, как использовать эти командлеты для выполнения задания в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cdb16-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="cdb16-124">С помощью редактора сохраните следующий код как **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="cdb16-124">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    <span data-ttu-id="cdb16-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span><span class="sxs-lookup"><span data-stu-id="cdb16-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span></span>

1. <span data-ttu-id="cdb16-126">Откройте командную строку Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cdb16-126">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="cdb16-127">Перейдите к расположению файла **pigjob.ps1** , а затем используйте следующую команду для запуска сценария:</span><span class="sxs-lookup"><span data-stu-id="cdb16-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="cdb16-128">Вам будет предложено войти в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb16-128">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="cdb16-129">Затем вам будет предложено ввести данные HTTPS, имя и пароль учетной записи администратора для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cdb16-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="cdb16-130">После завершения задания должна быть возвращена информация следующего вида.</span><span class="sxs-lookup"><span data-stu-id="cdb16-130">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="cdb16-131"><a id="troubleshooting"></a>Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="cdb16-131"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="cdb16-132">Если данные не возвращаются по завершении задания, возможно, во время обработки произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="cdb16-132">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="cdb16-133">Чтобы просмотреть информацию об ошибке для данного задания, добавьте следующую команду в конец файла **pigjob.ps1** , сохраните его, а затем запустите снова.</span><span class="sxs-lookup"><span data-stu-id="cdb16-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="cdb16-134">Будет возвращена информация, которая записывается в STDERR на сервере при запуске задания и может помочь определить причину сбоя задания.</span><span class="sxs-lookup"><span data-stu-id="cdb16-134">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="cdb16-135"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="cdb16-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="cdb16-136">Как можно видеть, Azure PowerShell позволяет с легкостью выполнять задания Pig в кластере HDInsight, отслеживать состояние задания и получать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="cdb16-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="cdb16-137"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cdb16-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="cdb16-138">Общая информация о Pig в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cdb16-138">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="cdb16-139">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cdb16-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="cdb16-140">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cdb16-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="cdb16-141">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cdb16-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="cdb16-142">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cdb16-142">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
