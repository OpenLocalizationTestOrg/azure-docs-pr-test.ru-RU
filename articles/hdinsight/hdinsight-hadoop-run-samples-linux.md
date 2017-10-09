---
title: "Примеры aaaRun Hadoop MapReduce в HDInsight - Azure | Документы Microsoft"
description: "Начало работы с образцами MapReduce в файлах JAR, включенных в HDInsight. Использование кластера toohello tooconnect SSH, а затем использовать hello Hadoop команда toorun образец задания."
keywords: "пример jar-файла hadoop,примеры jar-файлов hadoop,примеры hadoop mapreduce,примеры mapreduce"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a>Запустить примеры hello MapReduce, включенные в HDInsight

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Узнайте, как включенные примеры MapReduce hello toorun с Hadoop в HDInsight.

## <a name="prerequisites"></a>Предварительные требования

* **Кластер HDInsight**. См. статью [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

    > [!IMPORTANT]
    > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **SSH-клиент**. Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="hello-mapreduce-examples"></a>Примеры MapReduce Hello

**Расположение**: hello образцы расположены на hello в кластер HDInsight `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.

**Содержимое**: hello следующие образцы находятся в этом архиве:

* `aggregatewordcount`: Статистического выражения на основе программу mapreduce, которая подсчитывает слова hello во входных файлах hello.
* `aggregatewordhist`: Статистического выражения на основе программу mapreduce, которая вычисляет гистограмму hello слова hello во входных файлах hello.
* `bbp`: Mapreduce программа, использующая п-в Бейли-Borwein-Plouffe toocompute точные цифры числа пи.
* `dbcount`: Задание пример, который подсчитывает hello pageview журналов, хранящихся в базе данных.
* `distbbp`: Mapreduce программа, использующая точное bits BBP тип формулы toocompute пи.
* `grep`: Mapreduce программу, которая подсчитывает hello соответствует регулярного выражения во входном файле hello.
* `join`: задание для объединения сортированных наборов данных одного размера.
* `multifilewc`: задание для подсчета слов в нескольких файлах.
* `pentomino`: Mapreduce плитки размещение программы toofind решения toopentomino проблем.
* `pi`: программа MapReduce для расчета числа π по методу квази-Монте-Карло.
* `randomtextwriter`: программа MapReduce для записи 10 ГБ случайных текстовых данных на узел.
* `randomwriter`: программа MapReduce для записи 10 ГБ случайных данных на узел.
* `secondarysort`: Пример определения toohello дополнительной сортировки уменьшить этап.
* `sort`: Mapreduce программа, которая сортирует данные hello, записываемых модулем записи случайных hello.
* `sudoku`: программа решения судоку.
* `teragen`: Создать данные для hello terasort.
* `terasort`: Запустите hello terasort.
* `teravalidate`: проверка результатов выполнения программы TeraSort.
* `wordcount`: Mapreduce программа, которая подсчитывает слова hello во входных файлах hello.
* `wordmean`: Mapreduce программа, которая подсчитывает hello среднюю длину слова hello во входных файлах hello.
* `wordmedian`: Mapreduce программа, которая подсчитывает hello медианы длина слова hello во входных файлах hello.
* `wordstandarddeviation`: Mapreduce программа, которая подсчитывает стандартное отклонение hello hello длины слова hello во входных файлах hello.

**Исходный код**: исходный код этих образцов включен в кластер HDInsight на hello `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.

> [!NOTE]
> Hello `2.2.4.9-1` в hello путь — версия hello hello платформы Hortonworks Data Platform для кластера HDInsight hello и может быть разным для кластера.

## <a name="run-hello-wordcount-example"></a>Выполнить пример счетчика слов hello

1. Подключиться с помощью SSH tooHDInsight. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Из hello `username@#######:~$` запрос, используйте следующие примеры hello toolist команд hello:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    Эта команда создает список hello образец hello в предыдущем разделе этого документа.

3. Используйте hello следующая команда tooget справки по определенной выборке. В этом случае hello **wordcount** образца:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    Появляется после сообщения hello:

        Usage: wordcount <in> [<in>...] <out>

    Это сообщение означает, что вы можете задать несколько путей ввода hello исходные документы. конечный путь Hello здесь хранятся hello вывода (число слов в документах источника hello).

4. Используйте следующие toocount hello все слова в hello портативные компьютеры из Леонардо да Винчи, которой будут предоставлены кластера в качестве данных выборки:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    Для этого задания считываются входные данные из файла `/example/data/gutenberg/davinci.txt`. Выходные данные для этого примера сохраняются в `/example/data/davinciwordcount`. Оба пути находились в хранилище по умолчанию hello кластер, не hello локальной файловой системе.

   > [!NOTE]
   > Как уже отмечалось в справке hello для образца wordcount hello, можно также указать несколько входных файлов. Например, команда `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` позволит подсчитать слова в файлах davinci.txt и ulysses.txt.

5. После завершения задания hello, используйте следующие выходные данные команды tooview hello hello:

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    Эта команда объединяет все hello выходные файлы, созданные задания hello. Он отображает hello вывода toohello консоли. Hello выходных данных аналогичные toohello следующий текст:

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    Каждая строка представляет слова и сколько раз она произошла в hello входные данные.

## <a name="hello-sudoku-example"></a>Пример Судоку Hello

[Судоку](https://en.wikipedia.org/wiki/Sudoku) — это логическая головоломка, которая состоит из девяти полей размером 3 x 3 клетки. Некоторые ячейки в сетке hello есть цифры, тогда как другие пусты, а задача hello — toosolve пустым ячейкам hello. предыдущая ссылка Hello содержит дополнительные сведения о головоломки hello, но цель этого образца hello toosolve пустым ячейкам hello. Поэтому наши входных данных должен быть файлом в кодировке hello:

* Девять строк и девять столбцов
* Каждый столбец может содержать число или знак `?` (означает пустую ячейку).
* Ячейки разделяются пробелами

Нет определенных tooconstruct способом головоломки Судоку; Невозможно повторно число в столбце или строке. Кластер HDInsight hello, правильно ли построено приводится пример. Он находится в `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` и содержит hello следующий текст:

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

Используйте эту проблему пример hello примере Судоку toorun hello следующую команду:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

Hello результаты отображаются как toohello следующий текст:

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a>Пример "Пи" (π)

Образец Hello pi использует статистические (реализация Монте Carlo) метод tooestimate hello число пи. Точки в произвольном порядке помещаются внутри единичного квадрата. квадрат Hello также содержит круг. Hello вероятность точек hello подпадающих hello круг, равно toohello области hello circle pi/4. на основе значения hello 4R можно оценить Hello число пи. R — отношение hello hello количество точек, которые находятся внутри hello круг toohello общего количества точек, расположенных внутри квадратных hello. Hello большего образец hello точек, используемых, является hello лучшую оценку hello.

Использование этого образца hello, выполнив команду toorun. Эта команда использует 16 maps с 10 000 000 образцы tooestimate hello число пи:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

Hello значение, возвращаемое этой командой аналогично слишком**3.14159155000000000000**. Для ссылок hello первые 10 десятичных разрядов числа пи являются 3.1415926535.

## <a name="10-gb-greysort-example"></a>Пример Greysort для 10 ГБ данных

GraySort — это измерение производительности сортировки. Hello метрика скорость сортировки hello (ТБ в минуту), достигается при сортировке больших объемов данных, обычно 100 ТБ минимальное.

В этом примере используется небольшой объем данных, 10 ГБ, чтобы можно было выполнить сортировку достаточно быстро. Она использует hello MapReduce приложения, разработанные с Owen O'Malley и Arun Murthy. Эти приложения hello годовой общего назначения («daytona») терабайт сортировки тестирования выигрыш в 2009 г., с частотой 0.578 ТБ/мин (100 ТБ 173 минут). Дополнительные сведения об этом и других сортировки тестов производительности см. в разделе hello [Sortbenchmark](http://sortbenchmark.org/) сайта.

В этом примере используются три набора программ MapReduce.

* **TeraGen**: программу MapReduce, которая приводит к возникновению ряда данных toosort

* **TeraSort**: образцы hello входных данных и использует данные hello toosort MapReduce в сумма заказа

    TeraSort представляет собой стандартную сортировку MapReduce, за исключением настраиваемого разделителя. разделитель Hello использует отсортированный список ключей выборки n-1, определяющие hello диапазона ключей для каждого редукции. В частности, все ключи такого, образец [i-1] < = ключ < образец [i] отправляются tooreduce я. Этот разделитель гарантии, что выходные данные hello уменьшить i, меньше, чем выходные данные hello уменьшить i + 1.

* **TeraValidate**: глобально сортируется программу MapReduce, которая проверяет hello выходного файла

    Он создает одно сопоставление каждого файла в выходной каталог hello, и каждая карта гарантирует, что каждый ключ меньше или равно toohello предыдущий. Функция сопоставления Hello сначала создает записи hello и последний ключи каждого файла. Hello reduce-функция гарантирует, что hello первый ключ файла i больше, чем последний ключ файла i-1 hello. Проблемы выводятся как выход hello уменьшение этапе hello ключей, которые выходят за пределы.

Используйте hello следующие шаги данных toogenerate сортировки, а затем проверять hello выходные данные:

1. Создать 10 ГБ данных, которая является хранилищем по умолчанию кластер HDInsight хранимых toohello на `/example/data/10GB-sort-input`:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    Hello `-Dmapred.map.tasks` сообщает, сколько toouse карты задач для этого задания Hadoop. Hello две последних параметра означают, что задание toocreate hello 10 ГБ данных и toostore его в параметре `/example/data/10GB-sort-input`.

2. Используйте следующие команды toosort hello данные hello.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    Hello `-Dmapred.reduce.tasks` Hadoop сообщает, сколько уменьшить toouse задачи для задания hello. Параметры Hello две последних просто hello ввода и вывода ячейки данных.

3. Используйте следующие созданные hello сортировать данные hello toovalidate hello.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a>Дальнейшие действия

Из этой статьи вы узнали, как образцы hello toorun входящий в состав hello кластеры HDInsight под управлением Linux. Руководства об использовании с HDInsight Pig, Hive и MapReduce см hello следующие вопросы:

* [Использование Pig с Hadoop в HDInsight][hdinsight-use-pig]
* [Использование Hive с Hadoop в HDInsight][hdinsight-use-hive]
* [Использование MapReduce в Hadoop в HDInsight][hdinsight-use-mapreduce]

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
