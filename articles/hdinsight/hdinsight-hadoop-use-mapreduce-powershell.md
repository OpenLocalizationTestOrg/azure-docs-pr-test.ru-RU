---
title: "Использование MapReduce и PowerShell с Hadoop в Azure HDInsight | Документы Майкрософт"
description: "Информация об использовании PowerShell для удаленного выполнения заданий MapReduce с помощью Hadoop в HDInsight."
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
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="5e449-103">Выполнение заданий MapReduce с помощью PowerShell с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e449-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="5e449-104">В этом документе приведен пример использования Azure PowerShell для выполнения задания MapReduce в Hadoop на кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e449-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="5e449-105"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5e449-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="5e449-106">**Кластер Azure HDInsight (Hadoop в HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="5e449-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5e449-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="5e449-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5e449-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5e449-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="5e449-109"><seg>
  **Рабочая станция с Azure PowerShell**.</seg></span><span class="sxs-lookup"><span data-stu-id="5e449-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="5e449-110"><a id="powershell"></a>Выполнение задания MapReduce с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e449-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="5e449-111">Azure PowerShell предоставляет *командлеты* , позволяющие удаленно запускать задания MapReduce в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e449-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="5e449-112">Внутренне это достигается с помощью выполнения вызовов REST для [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (прежнее название — Templeton) на кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5e449-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="5e449-113">При выполнении заданий MapReduce в удаленном кластере HDInsight используются следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="5e449-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="5e449-114">**Login-AzureRmAccount** — выполняет аутентификацию Azure PowerShell для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="5e449-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="5e449-115">**New-AzureRmHDInsightMapReduceJobDefinition** — создает *определение задания*, используя заданную информацию MapReduce.</span><span class="sxs-lookup"><span data-stu-id="5e449-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="5e449-116">**Start-AzureRmHDInsightJob** — отправляет определение задания в HDInsight, запускает задание и возвращает объект *задание*, который можно использовать для проверки состояния задания.</span><span class="sxs-lookup"><span data-stu-id="5e449-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="5e449-117">**Wait-AzureRmHDInsightJob**— использует объект-задание для проверки состояния задания.</span><span class="sxs-lookup"><span data-stu-id="5e449-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="5e449-118">Он ожидает завершения задания или превышения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="5e449-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="5e449-119">**Get-AzureRmHDInsightJobOutput** — используется для получения выходных данных задания.</span><span class="sxs-lookup"><span data-stu-id="5e449-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="5e449-120">Следующие шаги показывают, как использовать эти командлеты для выполнения задания в кластере HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5e449-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="5e449-121">С помощью редактора сохраните следующий код как **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="5e449-121">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    <span data-ttu-id="5e449-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span><span class="sxs-lookup"><span data-stu-id="5e449-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span></span>

2. <span data-ttu-id="5e449-123">Откройте новую командную строку **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="5e449-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="5e449-124">Перейдите к расположению файла **mapreducejob.ps1** , а затем используйте следующую команду для запуска сценария:</span><span class="sxs-lookup"><span data-stu-id="5e449-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="5e449-125">При выполнении сценария вам будет предложено ввести имя кластера HDInsight, а также сведения HTTPS/имя и пароль учетной записи администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="5e449-125">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="5e449-126">Вам также может быть предложено аутентифицироваться в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="5e449-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="5e449-127">По завершении задания выходные данные будут иметь примерно следующий вид.</span><span class="sxs-lookup"><span data-stu-id="5e449-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="5e449-128">Такие выходные данные означают, что задание завершено успешно.</span><span class="sxs-lookup"><span data-stu-id="5e449-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e449-129">Если значение **ExitCode** не равно 0, см. сведения в разделе [Устранение неполадок](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="5e449-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="5e449-130">В этом примере скачанные файлы сохраняются в файле **output.txt** в каталоге, из которого запускается сценарий.</span><span class="sxs-lookup"><span data-stu-id="5e449-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="5e449-131">Просмотр выходных данных</span><span class="sxs-lookup"><span data-stu-id="5e449-131">View output</span></span>

<span data-ttu-id="5e449-132">Откройте файл **output.txt** в текстовом редакторе, чтобы просмотреть слова и статистику, полученные при выполнении задания.</span><span class="sxs-lookup"><span data-stu-id="5e449-132">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="5e449-133">Выходные файлы задания MapReduce являются неизменяемыми.</span><span class="sxs-lookup"><span data-stu-id="5e449-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="5e449-134">Поэтому при повторном выполнении этого примера потребуется изменить имя выходного файла.</span><span class="sxs-lookup"><span data-stu-id="5e449-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <span data-ttu-id="5e449-135"><a id="troubleshooting"></a>Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="5e449-135"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="5e449-136">Если данные не возвращаются по завершении задания, возможно, во время обработки произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="5e449-136">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="5e449-137">Чтобы просмотреть информацию об ошибке для данного задания, добавьте следующую команду в конец файла **mapreducejob.ps1** , сохраните его, а затем запустите снова.</span><span class="sxs-lookup"><span data-stu-id="5e449-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="5e449-138">Этот командлет возвращает информацию, которая записывается в STDERR на сервере при запуске задания и может помочь определить причину сбоя задания.</span><span class="sxs-lookup"><span data-stu-id="5e449-138">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="5e449-139"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="5e449-139"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="5e449-140">Как можно видеть, Azure PowerShell позволяет с легкостью выполнять задания MapReduce в кластере HDInsight, отслеживать состояние задания и получать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="5e449-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="5e449-141"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e449-141"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="5e449-142">Общая информация о заданиях MapReduce в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5e449-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="5e449-143">Использование MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e449-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="5e449-144">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5e449-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5e449-145">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e449-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5e449-146">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e449-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
