---
title: "aaaGenerate рекомендаций, с помощью Mahout HDInsight из PowerShell, Azure | Документы Microsoft"
description: "Узнайте, как toouse hello машины Apache Mahout обучения рекомендации фильмов toogenerate библиотеки с HDInsight (Hadoop) с помощью сценария PowerShell запущена на клиентском компьютере."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="77b52-103">Создание списка рекомендуемых фильмов с помощью Apache Mahout и Hadoop в HDInsight (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="77b52-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="77b52-104">Узнайте, как toouse hello [Apache Mahout](http://mahout.apache.org) библиотека обучения компьютера рекомендации фильмов toogenerate Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77b52-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span> <span data-ttu-id="77b52-105">Hello в этом документе примере задания Mahout toorun Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77b52-105">hello example in this document uses Azure PowerShell toorun Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77b52-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="77b52-106">Prerequisites</span></span>

* <span data-ttu-id="77b52-107">Кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="77b52-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="77b52-108">Дополнительные сведения о создании кластера см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][getstarted].</span><span class="sxs-lookup"><span data-stu-id="77b52-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77b52-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="77b52-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="77b52-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="77b52-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="77b52-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77b52-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="77b52-112"><a name="recommendations"></a>Создание рекомендаций с использованием Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77b52-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="77b52-113">с помощью Azure PowerShell работает Hello задания в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="77b52-113">hello job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="77b52-114">В настоящее время многие hello классов, предоставляемых с Mahout не работают с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77b52-114">Many of hello classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="77b52-115">Список классов, которые не поддерживают работу с Azure PowerShell см. в разделе hello [Устранение неполадок](#troubleshooting) раздела.</span><span class="sxs-lookup"><span data-stu-id="77b52-115">For a list of classes that do not work with Azure PowerShell, see hello [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="77b52-116">Пример использования SSH tooconnect tooHDInsight и примеры выполнения Mahout непосредственно в кластере hello см [сформировать рекомендации фильмов с использованием Mahout и HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="77b52-116">For an example of using SSH tooconnect tooHDInsight and run Mahout examples directly on hello cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="77b52-117">Одна из функций hello, предоставляемых Mahout является ядро рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="77b52-117">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="77b52-118">Этот модуль принимает данные в формат hello `userID`, `itemId`, и `prefValue` (hello предпочтений пользователей для hello элемента).</span><span class="sxs-lookup"><span data-stu-id="77b52-118">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello users preference for hello item).</span></span> <span data-ttu-id="77b52-119">Mahout использует hello данных toodetermine пользователей с like элемент предпочтения, которые можно использовать toomake рекомендации.</span><span class="sxs-lookup"><span data-stu-id="77b52-119">Mahout uses hello data toodetermine users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="77b52-120">Hello ниже приведен упрощенный Пошаговое руководство о принципах работы процесса hello рекомендации:</span><span class="sxs-lookup"><span data-stu-id="77b52-120">hello following example is a simplified walk-through of how hello recommendation process works:</span></span>

* <span data-ttu-id="77b52-121">**сопутствующего вхождения**: Joe, Анна и Виктор все популярные *звезда эту*, *hello обратно случится Empire*, и *возврат hello Джедай*.</span><span class="sxs-lookup"><span data-stu-id="77b52-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="77b52-122">Mahout определяет, что пользователи, как и любого из этих фильмов также hello два других.</span><span class="sxs-lookup"><span data-stu-id="77b52-122">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="77b52-123">**совместное вхождения**: Боб и Анна также понравилось *hello фантомных угроза*, *Атака клонов hello*, и *Revenge из hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="77b52-123">**co-occurrence**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="77b52-124">Mahout определяет пользователей, которые также понравилось hello предыдущих трех фильмы, такие как этих фильмов.</span><span class="sxs-lookup"><span data-stu-id="77b52-124">Mahout determines that users who liked hello previous three movies also like these movies.</span></span>

* <span data-ttu-id="77b52-125">**Рекомендация подобия**: поскольку Joe понравилось hello первые три фильмы, Mahout просматривает фильмы, другим пользователям, имеющим аналогичные предпочтения понравилось, но Joe имеет не просматривались (понравилось и оценкой).</span><span class="sxs-lookup"><span data-stu-id="77b52-125">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="77b52-126">В этом случае рекомендует Mahout *hello фантомных угроза*, *Атака клонов hello*, и *Revenge из hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="77b52-126">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="77b52-127">Основные сведения о данных hello</span><span class="sxs-lookup"><span data-stu-id="77b52-127">Understanding hello data</span></span>

<span data-ttu-id="77b52-128">Компания [GroupLens Research][movielens] предоставляет данные о рейтинге фильмов в формате, совместимом с Mahout.</span><span class="sxs-lookup"><span data-stu-id="77b52-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="77b52-129">Эти данные окажутся доступными на hello хранилища по умолчанию для кластера на `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="77b52-129">This data is available on hello default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="77b52-130">Существуют два файла `moviedb.txt` (сведения о фильмах hello) и `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="77b52-130">There are two files, `moviedb.txt` (information about hello movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="77b52-131">Hello `user-ratings.txt` файла используется во время анализа.</span><span class="sxs-lookup"><span data-stu-id="77b52-131">hello `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="77b52-132">Hello `moviedb.txt` файл является понятный текст tooprovide используется при отображении hello результаты анализа hello.</span><span class="sxs-lookup"><span data-stu-id="77b52-132">hello `moviedb.txt` file is used tooprovide user-friendly text when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="77b52-133">Hello данные, содержащиеся в ratings.txt пользователь имеет структуру `userID`, `movieID`, `userRating`, и `timestamp`, который сообщает, как высокая оценка фильм в каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="77b52-133">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="77b52-134">Ниже приведен пример hello данных:</span><span class="sxs-lookup"><span data-stu-id="77b52-134">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a><span data-ttu-id="77b52-135">Запустить задание hello</span><span class="sxs-lookup"><span data-stu-id="77b52-135">Run hello job</span></span>

<span data-ttu-id="77b52-136">Используйте следующий сценарий Windows PowerShell toorun задания, использующего ядро рекомендаций hello Mahout с данным фильма hello hello.</span><span class="sxs-lookup"><span data-stu-id="77b52-136">Use hello following Windows PowerShell script toorun a job that uses hello Mahout recommendation engine with hello movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="77b52-137">Этот файл запросит сведения, используемые tooconnect кластера HDInsight tooyour и выполнения заданий.</span><span class="sxs-lookup"><span data-stu-id="77b52-137">This file prompts you for information that is used tooconnect tooyour HDInsight cluster and run jobs.</span></span> <span data-ttu-id="77b52-138">Он может занять несколько минут для задания toocomplete hello и загрузите файл output.txt hello.</span><span class="sxs-lookup"><span data-stu-id="77b52-138">It may take several minutes for hello jobs toocomplete and download hello output.txt file.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> <span data-ttu-id="77b52-139">Mahout заданий не удаляйте временных данных, которые созданы при обработке задания hello.</span><span class="sxs-lookup"><span data-stu-id="77b52-139">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="77b52-140">Hello `--tempDir` параметр указан в hello примере задание tooisolate hello временные файлы в заданный каталог.</span><span class="sxs-lookup"><span data-stu-id="77b52-140">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific directory.</span></span>

<span data-ttu-id="77b52-141">Задание Mahout Hello не возвращать tooSTDOUT hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="77b52-141">hello Mahout job does not return hello output tooSTDOUT.</span></span> <span data-ttu-id="77b52-142">Вместо этого он сохраняет в указанный выходной каталог hello как **часть r-00000**.</span><span class="sxs-lookup"><span data-stu-id="77b52-142">Instead, it stores it in hello specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="77b52-143">сценарий Hello загружает этот файл слишком**output.txt** в текущем каталоге hello на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="77b52-143">hello script downloads this file too**output.txt** in hello current directory on your workstation.</span></span>

<span data-ttu-id="77b52-144">Hello следующий текст является примером hello содержимое этого файла:</span><span class="sxs-lookup"><span data-stu-id="77b52-144">hello following text is an example of hello content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="77b52-145">Первый столбец Hello — hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="77b52-145">hello first column is hello `userID`.</span></span> <span data-ttu-id="77b52-146">Здравствуйте, значения, содержащиеся в "[" и "]", `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="77b52-146">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="77b52-147">сценарий Hello также загружает hello `moviedb.txt` и `user-ratings.txt` , где находятся файлы, необходимые tooformat hello вывода toobe более удобном для чтения.</span><span class="sxs-lookup"><span data-stu-id="77b52-147">hello script also downloads hello `moviedb.txt` and `user-ratings.txt` files, which are needed tooformat hello output toobe more readable.</span></span>

### <a name="view-hello-output"></a><span data-ttu-id="77b52-148">Просмотр выходных данных hello</span><span class="sxs-lookup"><span data-stu-id="77b52-148">View hello output</span></span>

<span data-ttu-id="77b52-149">Несмотря на то, что hello созданные выходные данные могут быть ОК для использования в приложении, не удобной для пользователей.</span><span class="sxs-lookup"><span data-stu-id="77b52-149">Although hello generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="77b52-150">Hello `moviedb.txt` из hello server можно использовать tooresolve hello `movieId` tooa названия фильма.</span><span class="sxs-lookup"><span data-stu-id="77b52-150">hello `moviedb.txt` from hello server can be used tooresolve hello `movieId` tooa movie name.</span></span> <span data-ttu-id="77b52-151">Используйте следующие рекомендации toodisplay сценария PowerShell с именами фильма hello.</span><span class="sxs-lookup"><span data-stu-id="77b52-151">Use hello following PowerShell script toodisplay recommendations with movie names:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

<span data-ttu-id="77b52-152">Используйте hello рекомендации команда toodisplay hello в понятном формате.</span><span class="sxs-lookup"><span data-stu-id="77b52-152">Use hello following command toodisplay hello recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="77b52-153">Hello выходных данных аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="77b52-153">hello output is similar toohello following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="77b52-154"><a name="troubleshooting"></a>Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="77b52-154"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="77b52-155">Отсутствие возможности перезаписи файлов</span><span class="sxs-lookup"><span data-stu-id="77b52-155">Cannot overwrite files</span></span>

<span data-ttu-id="77b52-156">Задания Mahout не удаляют временные файлы, созданные во время обработки.</span><span class="sxs-lookup"><span data-stu-id="77b52-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="77b52-157">Кроме того задания hello не перезаписывать существующий выходной файл.</span><span class="sxs-lookup"><span data-stu-id="77b52-157">In addition, hello jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="77b52-158">tooavoid ошибки при выполнении задания Mahout удалить временные файлы и файлы вывода между запусками.</span><span class="sxs-lookup"><span data-stu-id="77b52-158">tooavoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="77b52-159">tooremove hello файлы, созданные по hello более ранних скриптах в этом документе, используют hello следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="77b52-159">tooremove hello files created by hello earlier scripts in this document, use hello following PowerShell script:</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="77b52-160"><a name="nopowershell"></a>Классы, которые не работают с Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77b52-160"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="77b52-161">Mahout заданий, использующих следующие классы hello возвращают различные сообщения об ошибках при использовании из Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="77b52-161">Mahout jobs that use hello following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="77b52-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="77b52-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="77b52-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="77b52-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="77b52-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="77b52-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="77b52-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="77b52-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="77b52-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="77b52-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="77b52-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="77b52-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="77b52-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="77b52-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="77b52-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="77b52-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="77b52-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="77b52-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="77b52-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="77b52-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="77b52-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="77b52-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="77b52-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="77b52-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="77b52-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="77b52-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="77b52-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="77b52-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="77b52-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="77b52-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="77b52-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="77b52-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="77b52-178">toorun задания, использующие эти классы подключиться с помощью SSH кластера HDInsight toohello и запустите задания hello из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="77b52-178">toorun jobs that use these classes, connect toohello HDInsight cluster using SSH and run hello jobs from hello command line.</span></span> <span data-ttu-id="77b52-179">Пример использования SSH toorun Mahout заданий см. в разделе [сформировать рекомендации фильмов с использованием Mahout и HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="77b52-179">For an example of using SSH toorun Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="77b52-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="77b52-180">Next steps</span></span>

<span data-ttu-id="77b52-181">Теперь, когда вы узнали, как toouse Mahout, обнаружить другие способы работы с данными в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77b52-181">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="77b52-182">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="77b52-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="77b52-183">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="77b52-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="77b52-184">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="77b52-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
