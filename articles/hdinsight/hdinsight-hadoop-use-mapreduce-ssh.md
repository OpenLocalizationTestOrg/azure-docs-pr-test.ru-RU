---
title: "aaaMapReduce и SSH-подключения на Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как SSH toouse toorun MapReduce заданий с помощью Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>Использование MapReduce с Hadoop в HDInsight с помощью SSH

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Узнайте, как задания toosubmit MapReduce tooHDInsight подключения Secure Shell (SSH).

> [!NOTE]
> Если вы уже знакомы с использованием Hadoop на основе Linux серверы, но — новый tooHDInsight см [HDInsight под управлением Linux советы](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Предварительные требования

* Кластер HDInsight на основе Linux (Hadoop в HDInsight).

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Клиент SSH. Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="ssh"></a>Подключение по SSH

Подключите кластер toohello с помощью SSH. Например, следующая команда hello подключается tooa кластер с именем **myhdinsight**:

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

**При использовании ключа сертификата для проверки подлинности SSH**, может потребоваться toospecify расположение hello hello закрытого ключа в системе клиента, например:

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

**Если использовать пароль для проверки подлинности SSH**, вам необходим пароль hello tooprovide при появлении запроса.

Дополнительные сведения об использовании протокола SSH с HDInsight см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="hadoop"></a>Использование команд Hadoop

1. После toohello подключенных кластера HDInsight, используйте hello следующая команда toostart задание MapReduce:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    Эта команда запускает hello `wordcount` класс, который содержится в hello `hadoop-mapreduce-examples.jar` файла. Она использует hello `/example/data/gutenberg/davinci.txt` документа в качестве входных и выходных данных хранится в `/example/data/WordCountOutput`.

    > [!NOTE]
    > Дополнительные сведения о MapReduce задания и hello данными из этого примера см. в разделе [используйте MapReduce в Hadoop в HDInsight](hdinsight-use-mapreduce.md).

2. Задание Hello выдает сведения при обработке, и возвращает сведения аналогичные toohello после текста, при завершении задания hello:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. По завершении заданий hello используйте hello следующая команда toolist hello выходных файлов:

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    Эта команда отображает два файла — `_SUCCESS` и `part-r-00000`. Hello `part-r-00000` файл содержит hello выходные данные для этого задания.

    > [!NOTE]
    > Некоторые задания MapReduce может разделить результаты hello в нескольких **часть r-###** файлов. Если Да, использовать hello ### суффикс tooindicate hello порядок файлов hello.

4. Вывод tooview hello, hello используйте следующую команду:

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    Эта команда отображает список слов hello, содержащиеся в hello **wasb://example/data/gutenberg/davinci.txt** файл и hello число возникновений каждого слова. Hello следующий текст является примером hello данные, содержащиеся в файле hello:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Сводка

Как видите, Hadoop команды предоставляют простой способ toorun задания MapReduce в кластер HDInsight и просмотр выходных данных задания hello.

## <a id="nextsteps"></a>Дальнейшие действия

Общая информация о заданиях MapReduce в HDInsight:

* [Использование MapReduce в Hadoop в HDInsight](hdinsight-use-mapreduce.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)
