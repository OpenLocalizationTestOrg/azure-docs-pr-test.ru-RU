---
title: "Использование Hive Hadoop с помощью PowerShell в HDInsight — Azure | Документы Майкрософт"
description: "Использование PowerShell для выполнения запросов Hive в Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: e1cb2e4a1fc82fb43082e79a5feba71b81b3eaa8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="d370f-103">Выполнение запросов Hive с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d370f-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="d370f-104">В этом документе приведен пример использования Azure PowerShell в режиме группы ресурсов Azure для выполнения запросов Hive в Hadoop в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d370f-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d370f-105">В этом документе не приводится подробное описание процессов, которые выполняют инструкции HiveQL, используемые в примерах.</span><span class="sxs-lookup"><span data-stu-id="d370f-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span></span> <span data-ttu-id="d370f-106">Информацию об операторах HiveQL, используемых в данном примере, см. в статье [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="d370f-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="d370f-107">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="d370f-107">**Prerequisites**</span></span>

* <span data-ttu-id="d370f-108">**Кластер Azure HDInsight**. Не имеет значения, какой кластер используется — под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="d370f-108">**An Azure HDInsight cluster**: It does not matter whether the cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d370f-109">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="d370f-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d370f-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d370f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d370f-111">**Рабочая станция с Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d370f-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="d370f-112">Выполнение запросов Hive с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d370f-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="d370f-113">Azure PowerShell предоставляет *командлеты* , позволяющие удаленно запускать запросы Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d370f-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="d370f-114">Во внутренних командлет использует вызовы REST к [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d370f-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span></span>

<span data-ttu-id="d370f-115">При выполнении запросов Hive на удаленном кластере HDInsight используются следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="d370f-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="d370f-116">**Add-AzureRmAccount**— выполняет аутентификацию Azure PowerShell для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d370f-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription</span></span>
* <span data-ttu-id="d370f-117">**New-AzureRmHDInsightHiveJobDefinition**— создает *определение задания* с использованием заданных операторов HiveQL.</span><span class="sxs-lookup"><span data-stu-id="d370f-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using the specified HiveQL statements</span></span>
* <span data-ttu-id="d370f-118">**Start-AzureRmHDInsightJob**— отправляет определение задания в HDInsight, запускает задание и возвращает объект- *задание* , который можно использовать для проверки состояния задания.</span><span class="sxs-lookup"><span data-stu-id="d370f-118">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="d370f-119">**Wait-AzureRmHDInsightJob**— использует объект-задание для проверки состояния задания.</span><span class="sxs-lookup"><span data-stu-id="d370f-119">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="d370f-120">Он ожидает завершения задания или превышения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="d370f-120">It waits until the job completes or the wait time is exceeded.</span></span>
* <span data-ttu-id="d370f-121">**Get-AzureRmHDInsightJobOutput**— используется для получения выходных данных задания.</span><span class="sxs-lookup"><span data-stu-id="d370f-121">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>
* <span data-ttu-id="d370f-122">**Invoke-AzureRmHDInsightHiveJob**— используется для выполнения операторов HiveQL.</span><span class="sxs-lookup"><span data-stu-id="d370f-122">**Invoke-AzureRmHDInsightHiveJob**: Used to run HiveQL statements.</span></span> <span data-ttu-id="d370f-123">Этот командлет блокирует выполнение запроса, после чего возвращаются результаты.</span><span class="sxs-lookup"><span data-stu-id="d370f-123">This cmdlet blocks the query completes, then returns the results</span></span>
* <span data-ttu-id="d370f-124">**Use-AzureRmHDInsightCluster** — указывает, что при выполнении команды **Invoke-AzureRmHDInsightHiveJob** должен использоваться текущий кластер.</span><span class="sxs-lookup"><span data-stu-id="d370f-124">**Use-AzureRmHDInsightCluster**: Sets the current cluster to use for the **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="d370f-125">Следующие шаги показывают, как использовать эти командлеты для выполнения задания в кластере HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d370f-125">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="d370f-126">С помощью редактора сохраните следующий код как **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="d370f-126">Using an editor, save the following code as **hivejob.ps1**.</span></span>

    <span data-ttu-id="d370f-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span><span class="sxs-lookup"><span data-stu-id="d370f-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span></span>

2. <span data-ttu-id="d370f-128">Откройте новую командную строку **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="d370f-128">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="d370f-129">Перейдите к расположению файла **hivejob.ps1** , а затем используйте следующую команду для запуска сценария:</span><span class="sxs-lookup"><span data-stu-id="d370f-129">Change directories to the location of the **hivejob.ps1** file, then use the following command to run the script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="d370f-130">При запуске сценария будет предложено ввести имя кластера, данные HTTPS и учетной записи администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="d370f-130">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span></span> <span data-ttu-id="d370f-131">Вам также может быть предложено выполнить вход в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="d370f-131">You may also be prompted to log in to your Azure subscription.</span></span>

3. <span data-ttu-id="d370f-132">После завершения задания должна быть возвращена информация следующего вида.</span><span class="sxs-lookup"><span data-stu-id="d370f-132">When the job completes, it returns information similar to the following thext:</span></span>

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="d370f-133">Как уже упоминалось, **Invoke-Hive** можно использовать для отправки запроса и ожидания ответа.</span><span class="sxs-lookup"><span data-stu-id="d370f-133">As mentioned earlier, **Invoke-Hive** can be used to run a query and wait for the response.</span></span> <span data-ttu-id="d370f-134">Чтобы увидеть работу команды Invoke-Hive, используйте следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="d370f-134">Use the following script to see how Invoke-Hive works:</span></span>

    <span data-ttu-id="d370f-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span><span class="sxs-lookup"><span data-stu-id="d370f-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span></span>

    <span data-ttu-id="d370f-136">Выходные данные выглядят так:</span><span class="sxs-lookup"><span data-stu-id="d370f-136">The output looks like the following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="d370f-137">Для более длинных запросов HiveQL вы можете использовать командлет Azure PowerShell **Here-Strings** или файлы сценариев HiveQL.</span><span class="sxs-lookup"><span data-stu-id="d370f-137">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="d370f-138">В приведенном ниже отрывке кода показано, как использовать командлет **Invoke-Hive** для запуска файла сценария HiveQL.</span><span class="sxs-lookup"><span data-stu-id="d370f-138">The following snippet shows how to use the **Invoke-Hive** cmdlet to run a HiveQL script file.</span></span> <span data-ttu-id="d370f-139">Файл скрипта HiveQL необходимо передать в wasb://.</span><span class="sxs-lookup"><span data-stu-id="d370f-139">The HiveQL script file must be uploaded to wasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="d370f-140">Дополнительные сведения о командлете **Here-Strings** см. <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">здесь</a>.</span><span class="sxs-lookup"><span data-stu-id="d370f-140">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d370f-141">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="d370f-141">Troubleshooting</span></span>

<span data-ttu-id="d370f-142">Если данные не возвращаются по завершении задания, возможно, во время обработки произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="d370f-142">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="d370f-143">Чтобы просмотреть информацию об ошибке для данного задания, добавьте следующий текст в конце файла **hivejob.ps1** , сохраните его, а затем запустите снова.</span><span class="sxs-lookup"><span data-stu-id="d370f-143">To view error information for this job, add the following to the end of the **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="d370f-144">Этот командлет возвращает информацию, которая записывается в STDERR на сервере при запуске задания.</span><span class="sxs-lookup"><span data-stu-id="d370f-144">This cmdlet returns the information that is written to STDERR on the server when you ran the job.</span></span>

## <a name="summary"></a><span data-ttu-id="d370f-145">Сводка</span><span class="sxs-lookup"><span data-stu-id="d370f-145">Summary</span></span>

<span data-ttu-id="d370f-146">Как можно видеть, Azure PowerShell позволяет с легкостью выполнять запросы Hive в кластере HDInsight, отслеживать состояние задания и получать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="d370f-146">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d370f-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d370f-147">Next steps</span></span>

<span data-ttu-id="d370f-148">Общая информация о Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d370f-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="d370f-149">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d370f-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="d370f-150">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d370f-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="d370f-151">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d370f-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d370f-152">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d370f-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
