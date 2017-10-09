---
title: "aaaDevelop Python потоковой передачи MapReduce заданий с HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toouse Python в потоковой передачи задания MapReduce. Hadoop предоставляет интерфейс API потоковой передачи для MapReduce с целью написания заданий на языках, отличных от Java."
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a>Разработка программ MapReduce с потоковой передачей Python для HDInsight

Узнайте, как toouse Python в потоковой передачи MapReduce операций. Hadoop предоставляет потоковой передачи API для MapReduce, которая позволяет toowrite карты и уменьшить функциям в языках, отличных от Java. Hello действия, описанные в этом документе реализовать hello карты и уменьшить компонентов в Python.

## <a name="prerequisites"></a>Предварительные требования

* Hadoop в кластере HDInsight на платформе Linux

  > [!IMPORTANT]
  > Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Текстовый редактор

  > [!IMPORTANT]
  > редактор текста Hello необходимо использовать LF как hello завершения строк. С помощью завершения строк из CRLF приводит к ошибкам при запуске задания MapReduce hello в кластерах HDInsight под управлением Linux.

* Hello `ssh` и `scp` команды, или [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)

## <a name="word-count"></a>Статистика

В этом примере реализуется простая функция подсчета слов, реализованная в модулях сопоставления и сжатия в Python. сопоставления Hello разбивает предложения на отдельные слова и редуктора hello объединяет слова hello и подсчитывает tooproduce hello вывода.

Hello следующая блок-схема иллюстрирует, что происходит во время сопоставления hello и снижения этапов.

![Иллюстрация процесса mapreduce hello](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a>Потоковая передача MapReduce

Hadoop позволяет toospecify файл, который содержит схему hello и снижения логику, используемую в рамках задания. Hello особые требования к hello сопоставления и уменьшения логику являются:

* **Входной**: hello карты и снижения компоненты должны считать входные данные из стандартного ввода.
* **Выходные данные**: hello карты и снижения компонентов необходимо написать tooSTDOUT вывода данных.
* **Формат данных**: hello данные, а оно создается должны быть пара ключ значение, разделенные символом табуляции.

Python может легко обрабатывать эти требования с помощью hello `sys` tooread модуля с помощью стандартного ввода, а `print` tooprint tooSTDOUT. Hello оставшихся задач просто форматирование hello данных символом табуляции (`\t`) символ между hello ключ и значение.

## <a name="create-hello-mapper-and-reducer"></a>Создание hello сопоставления и редуктора

1. Создайте файл с именем `mapper.py` и hello используйте следующий код в качестве содержимого hello:

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. Создайте файл с именем **reducer.py** и hello используйте следующий код в качестве содержимого hello:

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a>Запуск с помощью PowerShell

у файлов завершение вправо строк hello tooensure hello используйте следующий сценарий PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

Используйте следующие файлы hello tooupload сценария PowerShell hello, запустите задание hello и просмотр выходных данных hello:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a>Запуск из сеанса SSH

1. Из среды разработки в hello же каталоге, что и `mapper.py` и `reducer.py` файлы, используют hello следующую команду:

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    Замените `username` с именем пользователя hello SSH для кластера, и `clustername` с hello имя кластера.

    Эта команда копирует файлы hello из hello локальной системы toohello головного узла.

    > [!NOTE]
    > Если вы использовали toosecure пароль учетной записи SSH, запрашивается пароль hello. При использовании ключа SSH, возможно, toouse hello `-i` параметр и hello путь toohello закрытого ключа. Например, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.

2. Подключение toohello кластера с помощью SSH:

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

3. tooensure hello mapper.py и reducer.py имеют hello исправить символ конца строки, используйте hello, следующие команды:

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. Используйте следующие задания MapReduce hello toostart команда hello.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    Эта команда имеет hello следующие части:

   * **hadoop streaming.jar**— используется при выполнении операций потоковой передачи MapReduce. Hadoop он взаимодействует с внешнего MapReduce кода hello вами.

   * **-файлы**: Добавляет указанный hello задания MapReduce toohello файлов.

   * **-сопоставления**: Hadoop указывает файл toouse как hello сопоставления, в котором.

   * **-редуктора**: сообщает Hadoop, в которой файл toouse как hello редуктора.

   * **-ввода**: hello входной файл, нам необходимо подсчитать слова из.

   * **-Вывод**: hello, hello выходные данные записи в каталог.

    Как работает задания MapReduce hello, hello процесса отображаются в виде процентов.

        15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%


5. Вывод tooview hello, hello используйте следующую команду:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Эта команда отображает список ключевых слов и сколько раз слово hello произошла.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, каким образом задания потоковой передачи MapRedcue toouse с HDInsight, используйте следующие ссылки tooexplore hello других способов toowork с Azure HDInsight.

* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование заданий MapReduce с HDInsight](hdinsight-use-mapreduce.md)
