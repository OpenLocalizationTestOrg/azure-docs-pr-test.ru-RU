---
title: "Создание рекомендаций с помощью Mahout и HDInsight (SSH) — Azure | Документы Майкрософт"
description: "Узнайте, как использовать библиотеку машинного обучения Apache Mahout для создания списка рекомендуемых фильмов с помощью HDInsight (Hadoop)."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c78ec37c-9a8c-4bb6-9e38-0bdb9e89fbd7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 28450d72f19a5467d88bc787d11f6c37c5afbf9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="965e9-103">Создание списка рекомендуемых фильмов с помощью Apache Mahout и Hadoop в HDInsight (SSH) на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="965e9-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="965e9-104">Узнайте, как использовать библиотеку машинного обучения [Apache Mahout](http://mahout.apache.org) для создания списка рекомендуемых к просмотру фильмов с помощью Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="965e9-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span>

<span data-ttu-id="965e9-105">Mahout — это библиотека [машинного обучения][ml] для Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="965e9-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="965e9-106">Mahout содержит алгоритмы для обработки данных, такие как фильтрация, классификация и кластеризация.</span><span class="sxs-lookup"><span data-stu-id="965e9-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="965e9-107">В этой статье описано, как создать список рекомендуемых фильмов на основе фильмов, уже просмотренных вашими друзьями, используя подсистему рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="965e9-107">In this article, you use a recommendation engine to generate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="965e9-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="965e9-108">Prerequisites</span></span>

* <span data-ttu-id="965e9-109">Кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="965e9-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="965e9-110">Дополнительные сведения о создании кластера см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][getstarted].</span><span class="sxs-lookup"><span data-stu-id="965e9-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="965e9-111">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="965e9-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="965e9-112">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="965e9-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="965e9-113">Клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="965e9-113">An SSH client.</span></span> <span data-ttu-id="965e9-114">Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="965e9-114">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="965e9-115">Управление версиями Mahout</span><span class="sxs-lookup"><span data-stu-id="965e9-115">Mahout versioning</span></span>

<span data-ttu-id="965e9-116">Дополнительные сведения о версии Mahout, входящей в состав кластера HDInsight, см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="965e9-116">For more information about the version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="965e9-117"><a name="recommendations"></a>Общие сведения о рекомендациях</span><span class="sxs-lookup"><span data-stu-id="965e9-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="965e9-118">Одной из функций, предоставляемой Mahout, является подсистема рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="965e9-118">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="965e9-119">Она принимает данные в формате `userID`, `itemId` и `prefValue` (предпочтения для элемента).</span><span class="sxs-lookup"><span data-stu-id="965e9-119">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the preference for the item).</span></span> <span data-ttu-id="965e9-120">Затем Mahout может провести анализ совместной встречаемости, чтобы определить: *пользователи с предпочтениями к одному элементу также имеют их и к определенным другим элементам*.</span><span class="sxs-lookup"><span data-stu-id="965e9-120">Mahout can then perform co-occurance analysis to determine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="965e9-121">После этого Mahout определяет пользователей со сходными предпочтениями элементов, что можно использовать для создания рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="965e9-121">Mahout then determines users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="965e9-122">Ниже приведен простой пример рабочего процесса с использованием данных о фильме.</span><span class="sxs-lookup"><span data-stu-id="965e9-122">The following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="965e9-123">**Совместная встречаемость**: Джо, Алисе и Бобу нравятся фильмы *Звездные войны*, *Империя наносит ответный удар* и *Возвращение джедая*.</span><span class="sxs-lookup"><span data-stu-id="965e9-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="965e9-124">Mahout определяет, что пользователям, которым нравится любой из этих фильмов, также нравятся другие два.</span><span class="sxs-lookup"><span data-stu-id="965e9-124">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="965e9-125">**Совместная встречаемость**: Бобу и Алисе также нравятся фильмы *Призрачная угроза*, *Атака клонов* и *Месть ситхов*.</span><span class="sxs-lookup"><span data-stu-id="965e9-125">**Co-occurance**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="965e9-126">Mahout определяет, что пользователям, которым нравятся предыдущие три фильма, также нравятся и эти три.</span><span class="sxs-lookup"><span data-stu-id="965e9-126">Mahout determines that users who liked the previous three movies also like these three movies.</span></span>

* <span data-ttu-id="965e9-127">**Рекомендации на основе подобия:**так как Джо понравились первые три фильма, Mahout будет отбирать фильмы, которые нравились другим пользователям со схожими предпочтениями, но которые Джо еще не смотрел (по положительным отзывам и рейтингу).</span><span class="sxs-lookup"><span data-stu-id="965e9-127">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="965e9-128">В этом случае Mahout рекомендует посмотреть фильмы *Призрачная угроза*, *Атака клонов* и *Месть ситхов*.</span><span class="sxs-lookup"><span data-stu-id="965e9-128">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="965e9-129">Основные сведения о данных</span><span class="sxs-lookup"><span data-stu-id="965e9-129">Understanding the data</span></span>

<span data-ttu-id="965e9-130">Очень кстати, что компания [GroupLens Research][movielens] предоставляет данные о рейтинге фильмов в формате, совместимом с Mahout.</span><span class="sxs-lookup"><span data-stu-id="965e9-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="965e9-131">Эти данные можно найти в хранилище по умолчанию вашего кластера по адресу `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="965e9-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="965e9-132">Вы увидите два файла, `moviedb.txt` и `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="965e9-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="965e9-133">Файл user-ratings.txt используется во время анализа, а moviedb.txt — для отображения понятного текста в результатах анализа.</span><span class="sxs-lookup"><span data-stu-id="965e9-133">The user-ratings.txt file is used during analysis, while moviedb.txt is used to provide user-friendly text information when displaying the results of the analysis.</span></span>

<span data-ttu-id="965e9-134">Данные, содержащиеся файле user-ratings.txt, имеют структуру `userID`, `movieID`, `userRating` и `timestamp`, благодаря чему мы видим, насколько высоко каждый пользователь оценил фильм.</span><span class="sxs-lookup"><span data-stu-id="965e9-134">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="965e9-135">Вот пример данных:</span><span class="sxs-lookup"><span data-stu-id="965e9-135">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-the-analysis"></a><span data-ttu-id="965e9-136">Выполнение анализа</span><span class="sxs-lookup"><span data-stu-id="965e9-136">Run the analysis</span></span>

<span data-ttu-id="965e9-137">Чтобы запустить задание рекомендации, выполните из SSH-подключения к кластеру следующую команду:</span><span class="sxs-lookup"><span data-stu-id="965e9-137">From an SSH connection to the cluster, use the following command to run the recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="965e9-138">Выполнение задания может занять несколько минут; может выполняться несколько заданий MapReduce.</span><span class="sxs-lookup"><span data-stu-id="965e9-138">The job may take several minutes to complete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-the-output"></a><span data-ttu-id="965e9-139">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="965e9-139">View the output</span></span>

1. <span data-ttu-id="965e9-140">По завершении задания воспользуйтесь следующей командой, чтобы просмотреть результат:</span><span class="sxs-lookup"><span data-stu-id="965e9-140">Once the job completes, use the following command to view the generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="965e9-141">Результат выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="965e9-141">The output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="965e9-142">Первый столбец — `userID`.</span><span class="sxs-lookup"><span data-stu-id="965e9-142">The first column is the `userID`.</span></span> <span data-ttu-id="965e9-143">Значения, хранящиеся в скобках «[» и «]», — это `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="965e9-143">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="965e9-144">Выходные данные, а также файл moviedb.txt, можно использовать, чтобы отобразить более понятные сведения о рекомендациях.</span><span class="sxs-lookup"><span data-stu-id="965e9-144">You can use the output, along with the moviedb.txt, to provide more information on the recommendations.</span></span> <span data-ttu-id="965e9-145">Во-первых, необходимо скопировать файлы локально с помощью следующих команд.</span><span class="sxs-lookup"><span data-stu-id="965e9-145">First, we need to copy the files locally using the following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="965e9-146">Эта команда копирует выходные данные в файл **recommendations.txt** в текущем каталоге. В него также будут скопированы и файлы данных фильмов.</span><span class="sxs-lookup"><span data-stu-id="965e9-146">This command copies the output data to a file named **recommendations.txt** in the current directory, along with the movie data files.</span></span>

3. <span data-ttu-id="965e9-147">Чтобы создать сценарий Python, выполняющий поиск названий фильмов для данных в полученных рекомендациях, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="965e9-147">Use the following command to create a Python script that looks up movie names for the data in the recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="965e9-148">Когда откроется редактор, добавьте в файл следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="965e9-148">When the editor opens, use the following text as the contents of the file:</span></span>

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    <span data-ttu-id="965e9-149">Нажмите **CTRL+X**, **Y**, и, наконец, **ВВОД**, чтобы сохранить данные.</span><span class="sxs-lookup"><span data-stu-id="965e9-149">Press **Ctrl-X**, **Y**, and finally **Enter** to save the data.</span></span>

4. <span data-ttu-id="965e9-150">Запустите скрипт Python.</span><span class="sxs-lookup"><span data-stu-id="965e9-150">Run the Python script.</span></span> <span data-ttu-id="965e9-151">Следующая команда предполагает, что вы находитесь в каталоге со всеми скачанными файлами.</span><span class="sxs-lookup"><span data-stu-id="965e9-151">The following command assumes you are in the directory where all the files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="965e9-152">Она рассматривает рекомендации, созданные для пользователя ID 4.</span><span class="sxs-lookup"><span data-stu-id="965e9-152">This command looks at the recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="965e9-153">Файл **user-ratings.txt** используется для получения оцененных фильмов.</span><span class="sxs-lookup"><span data-stu-id="965e9-153">The **user-ratings.txt** file is used to retrieve movies that have been rated.</span></span>

    * <span data-ttu-id="965e9-154">Файл **moviedb.txt** используется для извлечения названий фильмов.</span><span class="sxs-lookup"><span data-stu-id="965e9-154">The **moviedb.txt** file is used to retrieve the names of the movies.</span></span>

    * <span data-ttu-id="965e9-155">Файл **recommendations.txt** используется для получения рекомендованных фильмов для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="965e9-155">The **recommendations.txt** is used to retrieve the movie recommendations for this user.</span></span>

     <span data-ttu-id="965e9-156">Результат этой команды аналогичен следующему:</span><span class="sxs-lookup"><span data-stu-id="965e9-156">The output from this command is similar to the following text:</span></span>

        <span data-ttu-id="965e9-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span><span class="sxs-lookup"><span data-stu-id="965e9-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="965e9-158">Удаление временных данных</span><span class="sxs-lookup"><span data-stu-id="965e9-158">Delete temporary data</span></span>

<span data-ttu-id="965e9-159">Задания Mahout не удаляют временные данные, созданные во время выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="965e9-159">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="965e9-160">В примере задания указан параметр `--tempDir` , чтобы выделить временные файлы в отдельный каталог для простоты последующего их удаления.</span><span class="sxs-lookup"><span data-stu-id="965e9-160">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="965e9-161">Чтобы удалить временные файлы, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="965e9-161">To remove the temp files, use the following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="965e9-162">Если вы хотите выполнить команду еще раз, необходимо удалить выходной каталог.</span><span class="sxs-lookup"><span data-stu-id="965e9-162">If you want to run the command again, you must also delete the output directory.</span></span> <span data-ttu-id="965e9-163">Используйте следующую команду для удаления этого каталога:</span><span class="sxs-lookup"><span data-stu-id="965e9-163">Use the following to delete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="965e9-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="965e9-164">Next steps</span></span>

<span data-ttu-id="965e9-165">Теперь, когда вы узнали, как использовать Mahout, откройте для себя другие способы работы с данными в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="965e9-165">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="965e9-166">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="965e9-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="965e9-167">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="965e9-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="965e9-168">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="965e9-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
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
