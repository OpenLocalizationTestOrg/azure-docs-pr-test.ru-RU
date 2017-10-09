---
title: "aaaUse Hadoop Hive с помощью PowerShell в HDInsight — Azure | Документы Microsoft"
description: "Использование запросов Hive toorun PowerShell в Hadoop в HDInsight."
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
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="877ab-103">Выполнение запросов Hive с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="877ab-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="877ab-104">Этот документ содержит пример использования Azure PowerShell hello группы ресурсов Azure toorun Hive в запросы в режиме в кластере HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="877ab-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="877ab-105">Этот документ не предоставляет подробное описание действий hello HiveQL инструкции, которые используются в примерах hello.</span><span class="sxs-lookup"><span data-stu-id="877ab-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="877ab-106">Сведения о hello HiveQL, используемый в этом примере в разделе [используйте Hive в с Hadoop в HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="877ab-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="877ab-107">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="877ab-107">**Prerequisites**</span></span>

* <span data-ttu-id="877ab-108">**Кластер Azure HDInsight**: он не имеет значения, является ли hello кластера Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="877ab-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="877ab-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="877ab-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="877ab-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="877ab-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="877ab-111">**Рабочая станция с Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="877ab-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="877ab-112">Выполнение запросов Hive с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="877ab-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="877ab-113">Azure PowerShell предоставляет *командлеты* , которые позволяют запустить tooremotely запросов Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="877ab-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="877ab-114">На внутреннем уровне командлеты hello вызовов REST слишком[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="877ab-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="877ab-115">Hello следующие командлеты используются при выполнении запросов Hive в удаленном кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="877ab-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="877ab-116">**Добавить AzureRmAccount**: tooyour Azure PowerShell выполняет проверку подлинности подписки Azure</span><span class="sxs-lookup"><span data-stu-id="877ab-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="877ab-117">**Новый AzureRmHDInsightHiveJobDefinition**: создает *определение задания* с помощью hello указан операторы HiveQL</span><span class="sxs-lookup"><span data-stu-id="877ab-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="877ab-118">**Начало AzureRmHDInsightJob**: отправляет tooHDInsight определение задания hello, запускает задание hello и возвращает *задания* объект, который может быть используется toocheck hello состояние задания hello</span><span class="sxs-lookup"><span data-stu-id="877ab-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="877ab-119">**Ожидание AzureRmHDInsightJob**: использует hello объекта toocheck hello состояния заданий hello задания.</span><span class="sxs-lookup"><span data-stu-id="877ab-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="877ab-120">Он ожидает завершения задания hello или превышено время ожидания hello.</span><span class="sxs-lookup"><span data-stu-id="877ab-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="877ab-121">**Get-AzureRmHDInsightJobOutput**: использовать tooretrieve hello выходные данные задания hello</span><span class="sxs-lookup"><span data-stu-id="877ab-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="877ab-122">**Вызвать AzureRmHDInsightHiveJob**: использовать операторы HiveQL toorun.</span><span class="sxs-lookup"><span data-stu-id="877ab-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="877ab-123">Этот командлет блоки hello запрос завершается, а затем возвращает результаты hello</span><span class="sxs-lookup"><span data-stu-id="877ab-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="877ab-124">**Используйте AzureRmHDInsightCluster**: наборы hello текущего кластера toouse для hello **Invoke AzureRmHDInsightHiveJob** команды</span><span class="sxs-lookup"><span data-stu-id="877ab-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="877ab-125">Hello следующие шаги показывают, как toouse toorun эти командлеты заданий в кластере HDInsight:</span><span class="sxs-lookup"><span data-stu-id="877ab-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="877ab-126">С помощью редактора, сохранить следующий код в виде hello **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="877ab-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="877ab-127">Откройте новую командную строку **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="877ab-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="877ab-128">Изменить расположение каталогов toohello hello **hivejob.ps1** файла, а затем используйте следующий сценарий hello toorun hello:</span><span class="sxs-lookup"><span data-stu-id="877ab-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="877ab-129">При запуске сценария hello их запрашиваемые tooenter hello кластера имя и hello HTTPS или учетных данных администратора для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="877ab-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="877ab-130">Также может быть запросом toolog в tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="877ab-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="877ab-131">По завершении заданий hello возвращается toohello аналогичные сведения, следуя thext:</span><span class="sxs-lookup"><span data-stu-id="877ab-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="877ab-132">Как упоминалось ранее, **Invoke-Hive** можно использовать toorun запроса и ожидать ответа hello.</span><span class="sxs-lookup"><span data-stu-id="877ab-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="877ab-133">Используйте следующий сценарий toosee, как работает Invoke-Hive hello.</span><span class="sxs-lookup"><span data-stu-id="877ab-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="877ab-134">Hello вывод выглядит следующим образом после текста hello.</span><span class="sxs-lookup"><span data-stu-id="877ab-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="877ab-135">Hello Azure PowerShell можно использовать для более длинных запросов HiveQL **Here-строках** командлета или HiveQL файлы сценариев.</span><span class="sxs-lookup"><span data-stu-id="877ab-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="877ab-136">Привет, в следующем фрагменте кода показан способ toouse hello **Invoke-Hive** командлет toorun HiveQL файла скрипта.</span><span class="sxs-lookup"><span data-stu-id="877ab-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="877ab-137">Hello HiveQL, файл сценария должен быть отправлен toowasb: / /.</span><span class="sxs-lookup"><span data-stu-id="877ab-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="877ab-138">Дополнительные сведения о командлете **Here-Strings** см. <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">здесь</a>.</span><span class="sxs-lookup"><span data-stu-id="877ab-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="877ab-139">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="877ab-139">Troubleshooting</span></span>

<span data-ttu-id="877ab-140">Если данные не возвращаются при завершении задания hello, произошла ошибка во время обработки.</span><span class="sxs-lookup"><span data-stu-id="877ab-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="877ab-141">tooview сведения об ошибке для данного задания, добавить hello следующему toohello конца hello **hivejob.ps1** файл, сохраните его и затем снова запустите ее.</span><span class="sxs-lookup"><span data-stu-id="877ab-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="877ab-142">Этот командлет возвращает hello информации, которая записывается tooSTDERR на сервере hello при выполнении задания hello.</span><span class="sxs-lookup"><span data-stu-id="877ab-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="877ab-143">Сводка</span><span class="sxs-lookup"><span data-stu-id="877ab-143">Summary</span></span>

<span data-ttu-id="877ab-144">Как видите, Azure PowerShell предоставляет простой способ toorun запросов Hive в кластер HDInsight, монитор hello состояние задания и получение выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="877ab-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="877ab-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="877ab-145">Next steps</span></span>

<span data-ttu-id="877ab-146">Общая информация о Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="877ab-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="877ab-147">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="877ab-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="877ab-148">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="877ab-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="877ab-149">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="877ab-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="877ab-150">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="877ab-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
