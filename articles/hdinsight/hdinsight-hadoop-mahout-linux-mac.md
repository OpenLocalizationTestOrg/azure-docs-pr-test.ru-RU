---
title: "с помощью Mahout и HDInsight (SSH) - Azure рекомендации aaaGenerate | Документы Microsoft"
description: "Узнайте, как toouse hello Apache Mahout машинного обучения рекомендации фильмов toogenerate библиотеки с HDInsight (Hadoop)."
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
ms.openlocfilehash: fedac9ceb4268f8421bce4623a5ad271041b8b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="149c4-103">Создание списка рекомендуемых фильмов с помощью Apache Mahout и Hadoop в HDInsight (SSH) на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="149c4-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="149c4-104">Узнайте, как toouse hello [Apache Mahout](http://mahout.apache.org) библиотека обучения компьютера рекомендации фильмов toogenerate Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="149c4-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span>

<span data-ttu-id="149c4-105">Mahout — это библиотека [машинного обучения][ml] для Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="149c4-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="149c4-106">Mahout содержит алгоритмы для обработки данных, такие как фильтрация, классификация и кластеризация.</span><span class="sxs-lookup"><span data-stu-id="149c4-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="149c4-107">В этой статье используйте рекомендации фильмов рекомендация engine toogenerate, основанные на ранее увидели ваши друзья.</span><span class="sxs-lookup"><span data-stu-id="149c4-107">In this article, you use a recommendation engine toogenerate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="149c4-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="149c4-108">Prerequisites</span></span>

* <span data-ttu-id="149c4-109">Кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="149c4-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="149c4-110">Дополнительные сведения о создании кластера см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][getstarted].</span><span class="sxs-lookup"><span data-stu-id="149c4-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="149c4-111">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="149c4-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="149c4-112">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="149c4-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="149c4-113">Клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="149c4-113">An SSH client.</span></span> <span data-ttu-id="149c4-114">Дополнительные сведения см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.</span><span class="sxs-lookup"><span data-stu-id="149c4-114">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="149c4-115">Управление версиями Mahout</span><span class="sxs-lookup"><span data-stu-id="149c4-115">Mahout versioning</span></span>

<span data-ttu-id="149c4-116">Дополнительные сведения о версии hello Mahout в HDInsight см. в разделе [HDInsight версии и компоненты Hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="149c4-116">For more information about hello version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="149c4-117"><a name="recommendations"></a>Общие сведения о рекомендациях</span><span class="sxs-lookup"><span data-stu-id="149c4-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="149c4-118">Одна из функций hello, предоставляемых Mahout является ядро рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="149c4-118">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="149c4-119">Этот модуль принимает данные в формат hello `userID`, `itemId`, и `prefValue` (hello предпочтения для hello элемента).</span><span class="sxs-lookup"><span data-stu-id="149c4-119">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello preference for hello item).</span></span> <span data-ttu-id="149c4-120">Mahout, а затем выполнять toodetermine анализ сопутствующего экземпляры: *пользователей, имеющих предпочтение элемент также имеется предпочтение эти другие элементы*.</span><span class="sxs-lookup"><span data-stu-id="149c4-120">Mahout can then perform co-occurance analysis toodetermine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="149c4-121">Затем mahout определяет пользователей с like элемент предпочтения, которые можно использовать toomake рекомендации.</span><span class="sxs-lookup"><span data-stu-id="149c4-121">Mahout then determines users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="149c4-122">Hello следующий рабочий процесс — упрощенный пример, использующий данные фильма:</span><span class="sxs-lookup"><span data-stu-id="149c4-122">hello following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="149c4-123">**Экземпляры совместно**: Joe, Анна и Виктор все популярные *звезда эту*, *hello случится Empire обратно*, и *возврат hello Джедай*.</span><span class="sxs-lookup"><span data-stu-id="149c4-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="149c4-124">Mahout определяет, что пользователи, как и любого из этих фильмов также hello два других.</span><span class="sxs-lookup"><span data-stu-id="149c4-124">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="149c4-125">**Экземпляры совместно**: Боб и Анна также понравилось *hello фантомных угроза*, *Атака клонов hello*, и *Revenge из hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="149c4-125">**Co-occurance**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="149c4-126">Mahout определяет пользователей, которые также понравилось hello предыдущих трех фильмы, такие как эти три фильмов.</span><span class="sxs-lookup"><span data-stu-id="149c4-126">Mahout determines that users who liked hello previous three movies also like these three movies.</span></span>

* <span data-ttu-id="149c4-127">**Рекомендация подобия**: поскольку Joe понравилось hello первые три фильмы, Mahout просматривает фильмы, другим пользователям, имеющим аналогичные предпочтения понравилось, но Joe имеет не просматривались (понравилось и оценкой).</span><span class="sxs-lookup"><span data-stu-id="149c4-127">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="149c4-128">В этом случае рекомендует Mahout *hello фантомных угроза*, *Атака клонов hello*, и *Revenge из hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="149c4-128">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="149c4-129">Основные сведения о данных hello</span><span class="sxs-lookup"><span data-stu-id="149c4-129">Understanding hello data</span></span>

<span data-ttu-id="149c4-130">Очень кстати, что компания [GroupLens Research][movielens] предоставляет данные о рейтинге фильмов в формате, совместимом с Mahout.</span><span class="sxs-lookup"><span data-stu-id="149c4-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="149c4-131">Эти данные можно найти в хранилище по умолчанию вашего кластера по адресу `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="149c4-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="149c4-132">Вы увидите два файла, `moviedb.txt` и `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="149c4-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="149c4-133">файл пользователя ratings.txt Hello используется во время анализа, пока moviedb.txt сведения понятный текст используется tooprovide при отображении hello результаты анализа hello.</span><span class="sxs-lookup"><span data-stu-id="149c4-133">hello user-ratings.txt file is used during analysis, while moviedb.txt is used tooprovide user-friendly text information when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="149c4-134">Hello данные, содержащиеся в ratings.txt пользователь имеет структуру `userID`, `movieID`, `userRating`, и `timestamp`, который сообщает, как высокая оценка фильм в каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="149c4-134">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="149c4-135">Ниже приведен пример hello данных:</span><span class="sxs-lookup"><span data-stu-id="149c4-135">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a><span data-ttu-id="149c4-136">Запуск анализа hello</span><span class="sxs-lookup"><span data-stu-id="149c4-136">Run hello analysis</span></span>

<span data-ttu-id="149c4-137">В кластере toohello подключения SSH используйте hello, следующая команда toorun hello рекомендация задания:</span><span class="sxs-lookup"><span data-stu-id="149c4-137">From an SSH connection toohello cluster, use hello following command toorun hello recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="149c4-138">Hello задания может занять несколько минут toocomplete и выполнения нескольких заданий MapReduce.</span><span class="sxs-lookup"><span data-stu-id="149c4-138">hello job may take several minutes toocomplete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-hello-output"></a><span data-ttu-id="149c4-139">Просмотр выходных данных hello</span><span class="sxs-lookup"><span data-stu-id="149c4-139">View hello output</span></span>

1. <span data-ttu-id="149c4-140">После завершения задания hello hello используется следующая команда tooview hello порождаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="149c4-140">Once hello job completes, use hello following command tooview hello generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="149c4-141">Hello вывод выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="149c4-141">hello output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="149c4-142">Первый столбец Hello — hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="149c4-142">hello first column is hello `userID`.</span></span> <span data-ttu-id="149c4-143">Здравствуйте, значения, содержащиеся в "[" и "]", `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="149c4-143">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="149c4-144">Можно использовать дополнительные сведения hello выходные данные, вместе с hello moviedb.txt, tooprovide рекомендациям hello.</span><span class="sxs-lookup"><span data-stu-id="149c4-144">You can use hello output, along with hello moviedb.txt, tooprovide more information on hello recommendations.</span></span> <span data-ttu-id="149c4-145">Во-первых мы должны toocopy hello файлы локально с помощью следующих команд hello.</span><span class="sxs-lookup"><span data-stu-id="149c4-145">First, we need toocopy hello files locally using hello following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="149c4-146">Эта команда копирует hello выходного файла tooa данных с именем **recommendations.txt** в текущем каталоге hello вместе с файлами данных фильма hello.</span><span class="sxs-lookup"><span data-stu-id="149c4-146">This command copies hello output data tooa file named **recommendations.txt** in hello current directory, along with hello movie data files.</span></span>

3. <span data-ttu-id="149c4-147">Используйте hello, следующая команда toocreate сценарий Python, выполняющее поиск имен фильма для данных hello в выходных данных hello рекомендации:</span><span class="sxs-lookup"><span data-stu-id="149c4-147">Use hello following command toocreate a Python script that looks up movie names for hello data in hello recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="149c4-148">Когда откроется окно редактора hello, используйте hello после текста как hello содержимое файла hello:</span><span class="sxs-lookup"><span data-stu-id="149c4-148">When hello editor opens, use hello following text as hello contents of hello file:</span></span>

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

    <span data-ttu-id="149c4-149">Нажмите клавишу **Ctrl-X**, **Y**и, наконец, **ввод** toosave hello данных.</span><span class="sxs-lookup"><span data-stu-id="149c4-149">Press **Ctrl-X**, **Y**, and finally **Enter** toosave hello data.</span></span>

4. <span data-ttu-id="149c4-150">Запустите сценарий Python hello.</span><span class="sxs-lookup"><span data-stu-id="149c4-150">Run hello Python script.</span></span> <span data-ttu-id="149c4-151">Hello следующая команда предполагает, что вы находитесь в каталоге hello, где были загружены все файлы hello:</span><span class="sxs-lookup"><span data-stu-id="149c4-151">hello following command assumes you are in hello directory where all hello files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="149c4-152">Эта команда просматривает hello рекомендации для 4 идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="149c4-152">This command looks at hello recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="149c4-153">Hello **ratings.txt пользователя** файл является используется tooretrieve фильмы, которые были оценены.</span><span class="sxs-lookup"><span data-stu-id="149c4-153">hello **user-ratings.txt** file is used tooretrieve movies that have been rated.</span></span>

    * <span data-ttu-id="149c4-154">Hello **moviedb.txt** файла — имена hello используется tooretrieve hello фильмов.</span><span class="sxs-lookup"><span data-stu-id="149c4-154">hello **moviedb.txt** file is used tooretrieve hello names of hello movies.</span></span>

    * <span data-ttu-id="149c4-155">Hello **recommendations.txt** — используется tooretrieve рекомендации фильмов hello для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="149c4-155">hello **recommendations.txt** is used tooretrieve hello movie recommendations for this user.</span></span>

     <span data-ttu-id="149c4-156">Hello выходные данные этой команды будет примерно toohello после текста:</span><span class="sxs-lookup"><span data-stu-id="149c4-156">hello output from this command is similar toohello following text:</span></span>

        <span data-ttu-id="149c4-157">Оценка семь лет в Tibet (1997) = 5.0 Джонс Индиане и hello последнего Crusade (1989 г.), оценка = 5.0 Jaws (1975 г.), оценка = 5.0 смысле и Sensibility (1995 г.), оценка = 5.0 день независимости (ID4) (1996), оценка = 5.0 Мой лучший друг Свадьба (1997), оценка = 5.0 Джерри Maguire (1996 ), оценка = 5.0 Scream 2 (1997), оценка = 5.0 оценки времени tooKill, (1996 г) = 5.0</span><span class="sxs-lookup"><span data-stu-id="149c4-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and hello Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time tooKill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="149c4-158">Удаление временных данных</span><span class="sxs-lookup"><span data-stu-id="149c4-158">Delete temporary data</span></span>

<span data-ttu-id="149c4-159">Mahout заданий не удаляйте временных данных, которые созданы при обработке задания hello.</span><span class="sxs-lookup"><span data-stu-id="149c4-159">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="149c4-160">Hello `--tempDir` параметр указан в hello примере задание tooisolate hello временные файлы в определенный путь для удаления легко.</span><span class="sxs-lookup"><span data-stu-id="149c4-160">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="149c4-161">tooremove hello временных файлов, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="149c4-161">tooremove hello temp files, use hello following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="149c4-162">Если требуется команда toorun hello, также необходимо удалить hello выходной каталог.</span><span class="sxs-lookup"><span data-stu-id="149c4-162">If you want toorun hello command again, you must also delete hello output directory.</span></span> <span data-ttu-id="149c4-163">Используйте следующие toodelete hello этот каталог:</span><span class="sxs-lookup"><span data-stu-id="149c4-163">Use hello following toodelete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="149c4-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="149c4-164">Next steps</span></span>

<span data-ttu-id="149c4-165">Теперь, когда вы узнали, как toouse Mahout, обнаружить другие способы работы с данными в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="149c4-165">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="149c4-166">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="149c4-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="149c4-167">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="149c4-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="149c4-168">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="149c4-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
