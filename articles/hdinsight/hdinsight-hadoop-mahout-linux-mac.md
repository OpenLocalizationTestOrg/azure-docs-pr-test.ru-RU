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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a>Создание списка рекомендуемых фильмов с помощью Apache Mahout и Hadoop в HDInsight (SSH) на платформе Linux

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Узнайте, как toouse hello [Apache Mahout](http://mahout.apache.org) библиотека обучения компьютера рекомендации фильмов toogenerate Azure HDInsight.

Mahout — это библиотека [машинного обучения][ml] для Apache Hadoop. Mahout содержит алгоритмы для обработки данных, такие как фильтрация, классификация и кластеризация. В этой статье используйте рекомендации фильмов рекомендация engine toogenerate, основанные на ранее увидели ваши друзья.

## <a name="prerequisites"></a>Предварительные требования

* Кластер HDInsight под управлением Linux. Дополнительные сведения о создании кластера см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][getstarted].

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Клиент SSH. Дополнительные сведения см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) документа.

## <a name="mahout-versioning"></a>Управление версиями Mahout

Дополнительные сведения о версии hello Mahout в HDInsight см. в разделе [HDInsight версии и компоненты Hadoop](hdinsight-component-versioning.md).

## <a name="recommendations"></a>Общие сведения о рекомендациях

Одна из функций hello, предоставляемых Mahout является ядро рекомендаций. Этот модуль принимает данные в формат hello `userID`, `itemId`, и `prefValue` (hello предпочтения для hello элемента). Mahout, а затем выполнять toodetermine анализ сопутствующего экземпляры: *пользователей, имеющих предпочтение элемент также имеется предпочтение эти другие элементы*. Затем mahout определяет пользователей с like элемент предпочтения, которые можно использовать toomake рекомендации.

Hello следующий рабочий процесс — упрощенный пример, использующий данные фильма:

* **Экземпляры совместно**: Joe, Анна и Виктор все популярные *звезда эту*, *hello случится Empire обратно*, и *возврат hello Джедай*. Mahout определяет, что пользователи, как и любого из этих фильмов также hello два других.

* **Экземпляры совместно**: Боб и Анна также понравилось *hello фантомных угроза*, *Атака клонов hello*, и *Revenge из hello Sith*. Mahout определяет пользователей, которые также понравилось hello предыдущих трех фильмы, такие как эти три фильмов.

* **Рекомендация подобия**: поскольку Joe понравилось hello первые три фильмы, Mahout просматривает фильмы, другим пользователям, имеющим аналогичные предпочтения понравилось, но Joe имеет не просматривались (понравилось и оценкой). В этом случае рекомендует Mahout *hello фантомных угроза*, *Атака клонов hello*, и *Revenge из hello Sith*.

### <a name="understanding-hello-data"></a>Основные сведения о данных hello

Очень кстати, что компания [GroupLens Research][movielens] предоставляет данные о рейтинге фильмов в формате, совместимом с Mahout. Эти данные можно найти в хранилище по умолчанию вашего кластера по адресу `/HdiSamples/HdiSamples/MahoutMovieData`.

Вы увидите два файла, `moviedb.txt` и `user-ratings.txt`. файл пользователя ratings.txt Hello используется во время анализа, пока moviedb.txt сведения понятный текст используется tooprovide при отображении hello результаты анализа hello.

Hello данные, содержащиеся в ratings.txt пользователь имеет структуру `userID`, `movieID`, `userRating`, и `timestamp`, который сообщает, как высокая оценка фильм в каждого пользователя. Ниже приведен пример hello данных:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a>Запуск анализа hello

В кластере toohello подключения SSH используйте hello, следующая команда toorun hello рекомендация задания:

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> Hello задания может занять несколько минут toocomplete и выполнения нескольких заданий MapReduce.

## <a name="view-hello-output"></a>Просмотр выходных данных hello

1. После завершения задания hello hello используется следующая команда tooview hello порождаемые выходные данные:

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    Hello вывод выглядит следующим образом:

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    Первый столбец Hello — hello `userID`. Здравствуйте, значения, содержащиеся в "[" и "]", `movieId`:`recommendationScore`.

2. Можно использовать дополнительные сведения hello выходные данные, вместе с hello moviedb.txt, tooprovide рекомендациям hello. Во-первых мы должны toocopy hello файлы локально с помощью следующих команд hello.

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    Эта команда копирует hello выходного файла tooa данных с именем **recommendations.txt** в текущем каталоге hello вместе с файлами данных фильма hello.

3. Используйте hello, следующая команда toocreate сценарий Python, выполняющее поиск имен фильма для данных hello в выходных данных hello рекомендации:

    ```bash
    nano show_recommendations.py
    ```

    Когда откроется окно редактора hello, используйте hello после текста как hello содержимое файла hello:

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

    Нажмите клавишу **Ctrl-X**, **Y**и, наконец, **ввод** toosave hello данных.

4. Запустите сценарий Python hello. Hello следующая команда предполагает, что вы находитесь в каталоге hello, где были загружены все файлы hello:

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    Эта команда просматривает hello рекомендации для 4 идентификатор пользователя.

    * Hello **ratings.txt пользователя** файл является используется tooretrieve фильмы, которые были оценены.

    * Hello **moviedb.txt** файла — имена hello используется tooretrieve hello фильмов.

    * Hello **recommendations.txt** — используется tooretrieve рекомендации фильмов hello для этого пользователя.

     Hello выходные данные этой команды будет примерно toohello после текста:

        Оценка семь лет в Tibet (1997) = 5.0 Джонс Индиане и hello последнего Crusade (1989 г.), оценка = 5.0 Jaws (1975 г.), оценка = 5.0 смысле и Sensibility (1995 г.), оценка = 5.0 день независимости (ID4) (1996), оценка = 5.0 Мой лучший друг Свадьба (1997), оценка = 5.0 Джерри Maguire (1996 ), оценка = 5.0 Scream 2 (1997), оценка = 5.0 оценки времени tooKill, (1996 г) = 5.0

## <a name="delete-temporary-data"></a>Удаление временных данных

Mahout заданий не удаляйте временных данных, которые созданы при обработке задания hello. Hello `--tempDir` параметр указан в hello примере задание tooisolate hello временные файлы в определенный путь для удаления легко. tooremove hello временных файлов, используйте hello следующую команду:

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> Если требуется команда toorun hello, также необходимо удалить hello выходной каталог. Используйте следующие toodelete hello этот каталог:
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как toouse Mahout, обнаружить другие способы работы с данными в HDInsight:

* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с HDInsight](hdinsight-use-mapreduce.md)

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
