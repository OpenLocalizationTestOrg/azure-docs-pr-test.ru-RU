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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a>Создание списка рекомендуемых фильмов с помощью Apache Mahout и Hadoop в HDInsight (PowerShell)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Узнайте, как toouse hello [Apache Mahout](http://mahout.apache.org) библиотека обучения компьютера рекомендации фильмов toogenerate Azure HDInsight. Hello в этом документе примере задания Mahout toorun Azure PowerShell.

## <a name="prerequisites"></a>Предварительные требования

* Кластер HDInsight под управлением Linux. Дополнительные сведения о создании кластера см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][getstarted].

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Azure PowerShell](/powershell/azure/overview)

## <a name="recommendations"></a>Создание рекомендаций с использованием Azure PowerShell

> [!WARNING]
> с помощью Azure PowerShell работает Hello задания в этом разделе. В настоящее время многие hello классов, предоставляемых с Mahout не работают с помощью Azure PowerShell. Список классов, которые не поддерживают работу с Azure PowerShell см. в разделе hello [Устранение неполадок](#troubleshooting) раздела.
>
> Пример использования SSH tooconnect tooHDInsight и примеры выполнения Mahout непосредственно в кластере hello см [сформировать рекомендации фильмов с использованием Mahout и HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

Одна из функций hello, предоставляемых Mahout является ядро рекомендаций. Этот модуль принимает данные в формат hello `userID`, `itemId`, и `prefValue` (hello предпочтений пользователей для hello элемента). Mahout использует hello данных toodetermine пользователей с like элемент предпочтения, которые можно использовать toomake рекомендации.

Hello ниже приведен упрощенный Пошаговое руководство о принципах работы процесса hello рекомендации:

* **сопутствующего вхождения**: Joe, Анна и Виктор все популярные *звезда эту*, *hello обратно случится Empire*, и *возврат hello Джедай*. Mahout определяет, что пользователи, как и любого из этих фильмов также hello два других.

* **совместное вхождения**: Боб и Анна также понравилось *hello фантомных угроза*, *Атака клонов hello*, и *Revenge из hello Sith*. Mahout определяет пользователей, которые также понравилось hello предыдущих трех фильмы, такие как этих фильмов.

* **Рекомендация подобия**: поскольку Joe понравилось hello первые три фильмы, Mahout просматривает фильмы, другим пользователям, имеющим аналогичные предпочтения понравилось, но Joe имеет не просматривались (понравилось и оценкой). В этом случае рекомендует Mahout *hello фантомных угроза*, *Атака клонов hello*, и *Revenge из hello Sith*.

### <a name="understanding-hello-data"></a>Основные сведения о данных hello

Компания [GroupLens Research][movielens] предоставляет данные о рейтинге фильмов в формате, совместимом с Mahout. Эти данные окажутся доступными на hello хранилища по умолчанию для кластера на `/HdiSamples//HdiSamples/MahoutMovieData`.

Существуют два файла `moviedb.txt` (сведения о фильмах hello) и `user-ratings.txt`. Hello `user-ratings.txt` файла используется во время анализа. Hello `moviedb.txt` файл является понятный текст tooprovide используется при отображении hello результаты анализа hello.

Hello данные, содержащиеся в ratings.txt пользователь имеет структуру `userID`, `movieID`, `userRating`, и `timestamp`, который сообщает, как высокая оценка фильм в каждого пользователя. Ниже приведен пример hello данных:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a>Запустить задание hello

Используйте следующий сценарий Windows PowerShell toorun задания, использующего ядро рекомендаций hello Mahout с данным фильма hello hello.

> [!NOTE]
> Этот файл запросит сведения, используемые tooconnect кластера HDInsight tooyour и выполнения заданий. Он может занять несколько минут для задания toocomplete hello и загрузите файл output.txt hello.

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> Mahout заданий не удаляйте временных данных, которые созданы при обработке задания hello. Hello `--tempDir` параметр указан в hello примере задание tooisolate hello временные файлы в заданный каталог.

Задание Mahout Hello не возвращать tooSTDOUT hello выходных данных. Вместо этого он сохраняет в указанный выходной каталог hello как **часть r-00000**. сценарий Hello загружает этот файл слишком**output.txt** в текущем каталоге hello на рабочей станции.

Hello следующий текст является примером hello содержимое этого файла:

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

Первый столбец Hello — hello `userID`. Здравствуйте, значения, содержащиеся в "[" и "]", `movieId`:`recommendationScore`.

сценарий Hello также загружает hello `moviedb.txt` и `user-ratings.txt` , где находятся файлы, необходимые tooformat hello вывода toobe более удобном для чтения.

### <a name="view-hello-output"></a>Просмотр выходных данных hello

Несмотря на то, что hello созданные выходные данные могут быть ОК для использования в приложении, не удобной для пользователей. Hello `moviedb.txt` из hello server можно использовать tooresolve hello `movieId` tooa названия фильма. Используйте следующие рекомендации toodisplay сценария PowerShell с именами фильма hello.

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

Используйте hello рекомендации команда toodisplay hello в понятном формате. 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

Hello выходных данных аналогичные toohello следующий текст:

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

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="cannot-overwrite-files"></a>Отсутствие возможности перезаписи файлов

Задания Mahout не удаляют временные файлы, созданные во время обработки. Кроме того задания hello не перезаписывать существующий выходной файл.

tooavoid ошибки при выполнении задания Mahout удалить временные файлы и файлы вывода между запусками. tooremove hello файлы, созданные по hello более ранних скриптах в этом документе, используют hello следующий сценарий PowerShell:

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

### <a name="nopowershell"></a>Классы, которые не работают с Azure PowerShell

Mahout заданий, использующих следующие классы hello возвращают различные сообщения об ошибках при использовании из Windows PowerShell:

* org.apache.mahout.utils.clustering.ClusterDumper
* org.apache.mahout.utils.SequenceFileDumper
* org.apache.mahout.utils.vectors.lucene.Driver
* org.apache.mahout.utils.vectors.arff.Driver
* org.apache.mahout.text.WikipediaToSequenceFile
* org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles
* org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer
* org.apache.mahout.classifier.sgd.TrainLogistic
* org.apache.mahout.classifier.sgd.RunLogistic
* org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic
* org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic
* org.apache.mahout.classifier.sgd.RunAdaptiveLogistic
* org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer
* org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator
* org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator
* org.apache.mahout.classifier.df.tools.Describe

toorun задания, использующие эти классы подключиться с помощью SSH кластера HDInsight toohello и запустите задания hello из командной строки hello. Пример использования SSH toorun Mahout заданий см. в разделе [сформировать рекомендации фильмов с использованием Mahout и HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как toouse Mahout, обнаружить другие способы работы с данными в HDInsight:

* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с HDInsight](hdinsight-use-mapreduce.md)

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
