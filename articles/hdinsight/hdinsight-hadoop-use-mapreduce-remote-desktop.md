---
title: "aaaMapReduce и удаленного рабочего стола с Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как tooHadoop tooconnect toouse удаленного рабочего стола на HDInsight и выполнения заданий MapReduce."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a>Использование MapReduce в Hadoop в HDInsight с помощью удаленного рабочего стола
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

В этой статье будет узнать, как кластер tooconnect tooa Hadoop в HDInsight с помощью удаленного рабочего стола и запустите задания MapReduce с помощью команды Hadoop hello.

> [!IMPORTANT]
> Удаленный рабочий стол доступен только в кластерах HDInsight на платформе Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Для HDInsight 3.4 или выше в разделе [используйте MapReduce с SSH](hdinsight-hadoop-use-mapreduce-ssh.md) сведения о подключении кластера HDInsight toohello и выполнения заданий MapReduce.

## <a id="prereq"></a>Предварительные требования
в этой статье инструкциям toocomplete hello, вам потребуется hello следующие:

* Кластер HDInsight на платформе Windows (Hadoop в HDInsight).
* Клиентский компьютер под управлением Windows 10, Windows 8 или Windows 7.

## <a id="connect"></a>Подключение к удаленному рабочему столу
Включить удаленный рабочий стол для кластера HDInsight hello, а затем соедините tooit в соответствии с инструкциями hello в [tooHDInsight кластерами, с помощью протокола удаленного рабочего СТОЛА подключиться](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hadoop"></a>Команда Hadoop hello
Подключенных toohello рабочий стол для кластера HDInsight hello, используйте следующие шаги toorun задание MapReduce с помощью команды Hadoop hello hello:

1. С рабочего стола HDInsight hello, запустите hello **командной строки Hadoop**. Это открывает новую командную строку в hello **c:\apps\dist\hadoop-&lt;номер версии >** каталога.

   > [!NOTE]
   > номер версии Hello изменяются по мере обновления Hadoop. Hello **HADOOP_HOME** переменной среды может быть путь используется toofind hello. Например `cd %HADOOP_HOME%` изменения каталоги toohello Hadoop в каталоге, не требуя номер версии tooknow hello.
   >
   >
2. toouse hello **Hadoop** toorun задание MapReduce пример команды, используйте hello следующую команду:

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    Запустится hello **wordcount** класс, который содержится в hello **mapreduce-hadoop-examples.jar** файл в текущем каталоге hello. В качестве входного, он использует hello **wasb://example/data/gutenberg/davinci.txt** хранится документ и выход по: **wasb: / / / пример/данных/WordCountOutput**.

   > [!NOTE]
   > Дополнительные сведения о MapReduce задания и hello данными из этого примера см. в разделе <a href="hdinsight-use-mapreduce.md">используйте MapReduce в HDInsight Hadoop</a>.
   >
   >
3. Задание Hello выдает сведения, как его обработки, и возвращает аналогичные toohello следующие сведения при завершении задания hello:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. По завершении задания hello использовать hello, следующая команда toolist hello выходные файлы, хранящиеся в **wasb://example/data/WordCountOutput**:

        hadoop fs -ls wasb:///example/data/WordCountOutput

    Должно отобразиться два файла: **_SUCCESS** и **part-r-00000**. Hello **часть r-00000** файл содержит hello выходные данные для этого задания.

   > [!NOTE]
   > Некоторые задания MapReduce может разделить результаты hello в нескольких **часть r-###** файлов. Если Да, использовать hello ### суффикс tooindicate hello порядок файлов hello.
   >
   >
5. Вывод tooview hello, hello используйте следующую команду:

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    Это список hello слов, которые содержатся в hello **wasb://example/data/gutenberg/davinci.txt** файла вместе с hello число возникновений каждого слова. Hello ниже приведен пример hello данных, которые будут содержаться в файле hello:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Сводка
Как видите, hello команда Hadoop, посвященная toorun простой способ задания MapReduce кластер HDInsight и просмотр выходных данных задания hello.

## <a id="nextsteps"></a>Дальнейшие действия
Общая информация о заданиях MapReduce в HDInsight:

* [Использование MapReduce в Hadoop в HDInsight](hdinsight-use-mapreduce.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)
