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
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="e2af1-104">Разработка программ MapReduce с потоковой передачей Python для HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2af1-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="e2af1-105">Узнайте, как toouse Python в потоковой передачи MapReduce операций.</span><span class="sxs-lookup"><span data-stu-id="e2af1-105">Learn how toouse Python in streaming MapReduce operations.</span></span> <span data-ttu-id="e2af1-106">Hadoop предоставляет потоковой передачи API для MapReduce, которая позволяет toowrite карты и уменьшить функциям в языках, отличных от Java.</span><span class="sxs-lookup"><span data-stu-id="e2af1-106">Hadoop provides a streaming API for MapReduce that enables you toowrite map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="e2af1-107">Hello действия, описанные в этом документе реализовать hello карты и уменьшить компонентов в Python.</span><span class="sxs-lookup"><span data-stu-id="e2af1-107">hello steps in this document implement hello Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2af1-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e2af1-108">Prerequisites</span></span>

* <span data-ttu-id="e2af1-109">Hadoop в кластере HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="e2af1-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e2af1-110">Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux.</span><span class="sxs-lookup"><span data-stu-id="e2af1-110">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="e2af1-111">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e2af1-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e2af1-112">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e2af1-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e2af1-113">Текстовый редактор</span><span class="sxs-lookup"><span data-stu-id="e2af1-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e2af1-114">редактор текста Hello необходимо использовать LF как hello завершения строк.</span><span class="sxs-lookup"><span data-stu-id="e2af1-114">hello text editor must use LF as hello line ending.</span></span> <span data-ttu-id="e2af1-115">С помощью завершения строк из CRLF приводит к ошибкам при запуске задания MapReduce hello в кластерах HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="e2af1-115">Using a line ending of CRLF causes errors when running hello MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="e2af1-116">Hello `ssh` и `scp` команды, или [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="e2af1-116">hello `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="e2af1-117">Статистика</span><span class="sxs-lookup"><span data-stu-id="e2af1-117">Word count</span></span>

<span data-ttu-id="e2af1-118">В этом примере реализуется простая функция подсчета слов, реализованная в модулях сопоставления и сжатия в Python.</span><span class="sxs-lookup"><span data-stu-id="e2af1-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="e2af1-119">сопоставления Hello разбивает предложения на отдельные слова и редуктора hello объединяет слова hello и подсчитывает tooproduce hello вывода.</span><span class="sxs-lookup"><span data-stu-id="e2af1-119">hello mapper breaks sentences into individual words, and hello reducer aggregates hello words and counts tooproduce hello output.</span></span>

<span data-ttu-id="e2af1-120">Hello следующая блок-схема иллюстрирует, что происходит во время сопоставления hello и снижения этапов.</span><span class="sxs-lookup"><span data-stu-id="e2af1-120">hello following flowchart illustrates what happens during hello map and reduce phases.</span></span>

![Иллюстрация процесса mapreduce hello](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="e2af1-122">Потоковая передача MapReduce</span><span class="sxs-lookup"><span data-stu-id="e2af1-122">Streaming MapReduce</span></span>

<span data-ttu-id="e2af1-123">Hadoop позволяет toospecify файл, который содержит схему hello и снижения логику, используемую в рамках задания.</span><span class="sxs-lookup"><span data-stu-id="e2af1-123">Hadoop allows you toospecify a file that contains hello map and reduce logic that is used by a job.</span></span> <span data-ttu-id="e2af1-124">Hello особые требования к hello сопоставления и уменьшения логику являются:</span><span class="sxs-lookup"><span data-stu-id="e2af1-124">hello specific requirements for hello map and reduce logic are:</span></span>

* <span data-ttu-id="e2af1-125">**Входной**: hello карты и снижения компоненты должны считать входные данные из стандартного ввода.</span><span class="sxs-lookup"><span data-stu-id="e2af1-125">**Input**: hello map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="e2af1-126">**Выходные данные**: hello карты и снижения компонентов необходимо написать tooSTDOUT вывода данных.</span><span class="sxs-lookup"><span data-stu-id="e2af1-126">**Output**: hello map and reduce components must write output data tooSTDOUT.</span></span>
* <span data-ttu-id="e2af1-127">**Формат данных**: hello данные, а оно создается должны быть пара ключ значение, разделенные символом табуляции.</span><span class="sxs-lookup"><span data-stu-id="e2af1-127">**Data format**: hello data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="e2af1-128">Python может легко обрабатывать эти требования с помощью hello `sys` tooread модуля с помощью стандартного ввода, а `print` tooprint tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="e2af1-128">Python can easily handle these requirements by using hello `sys` module tooread from STDIN and using `print` tooprint tooSTDOUT.</span></span> <span data-ttu-id="e2af1-129">Hello оставшихся задач просто форматирование hello данных символом табуляции (`\t`) символ между hello ключ и значение.</span><span class="sxs-lookup"><span data-stu-id="e2af1-129">hello remaining task is simply formatting hello data with a tab (`\t`) character between hello key and value.</span></span>

## <a name="create-hello-mapper-and-reducer"></a><span data-ttu-id="e2af1-130">Создание hello сопоставления и редуктора</span><span class="sxs-lookup"><span data-stu-id="e2af1-130">Create hello mapper and reducer</span></span>

1. <span data-ttu-id="e2af1-131">Создайте файл с именем `mapper.py` и hello используйте следующий код в качестве содержимого hello:</span><span class="sxs-lookup"><span data-stu-id="e2af1-131">Create a file named `mapper.py` and use hello following code as hello content:</span></span>

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

2. <span data-ttu-id="e2af1-132">Создайте файл с именем **reducer.py** и hello используйте следующий код в качестве содержимого hello:</span><span class="sxs-lookup"><span data-stu-id="e2af1-132">Create a file named **reducer.py** and use hello following code as hello content:</span></span>

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

## <a name="run-using-powershell"></a><span data-ttu-id="e2af1-133">Запуск с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2af1-133">Run using PowerShell</span></span>

<span data-ttu-id="e2af1-134">у файлов завершение вправо строк hello tooensure hello используйте следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e2af1-134">tooensure that your files have hello right line endings, use hello following PowerShell script:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

<span data-ttu-id="e2af1-135">Используйте следующие файлы hello tooupload сценария PowerShell hello, запустите задание hello и просмотр выходных данных hello:</span><span class="sxs-lookup"><span data-stu-id="e2af1-135">Use hello following PowerShell script tooupload hello files, run hello job, and view hello output:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="e2af1-136">Запуск из сеанса SSH</span><span class="sxs-lookup"><span data-stu-id="e2af1-136">Run from an SSH session</span></span>

1. <span data-ttu-id="e2af1-137">Из среды разработки в hello же каталоге, что и `mapper.py` и `reducer.py` файлы, используют hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e2af1-137">From your development environment, in hello same directory as `mapper.py` and `reducer.py` files, use hello following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="e2af1-138">Замените `username` с именем пользователя hello SSH для кластера, и `clustername` с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="e2af1-138">Replace `username` with hello SSH user name for your cluster, and `clustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="e2af1-139">Эта команда копирует файлы hello из hello локальной системы toohello головного узла.</span><span class="sxs-lookup"><span data-stu-id="e2af1-139">This command copies hello files from hello local system toohello head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2af1-140">Если вы использовали toosecure пароль учетной записи SSH, запрашивается пароль hello.</span><span class="sxs-lookup"><span data-stu-id="e2af1-140">If you used a password toosecure your SSH account, you are prompted for hello password.</span></span> <span data-ttu-id="e2af1-141">При использовании ключа SSH, возможно, toouse hello `-i` параметр и hello путь toohello закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="e2af1-141">If you used an SSH key, you may have toouse hello `-i` parameter and hello path toohello private key.</span></span> <span data-ttu-id="e2af1-142">Например, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="e2af1-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="e2af1-143">Подключение toohello кластера с помощью SSH:</span><span class="sxs-lookup"><span data-stu-id="e2af1-143">Connect toohello cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="e2af1-144">Дополнительные сведения см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e2af1-144">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="e2af1-145">tooensure hello mapper.py и reducer.py имеют hello исправить символ конца строки, используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e2af1-145">tooensure hello mapper.py and reducer.py have hello correct line endings, use hello following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="e2af1-146">Используйте следующие задания MapReduce hello toostart команда hello.</span><span class="sxs-lookup"><span data-stu-id="e2af1-146">Use hello following command toostart hello MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="e2af1-147">Эта команда имеет hello следующие части:</span><span class="sxs-lookup"><span data-stu-id="e2af1-147">This command has hello following parts:</span></span>

   * <span data-ttu-id="e2af1-148">**hadoop streaming.jar**— используется при выполнении операций потоковой передачи MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e2af1-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="e2af1-149">Hadoop он взаимодействует с внешнего MapReduce кода hello вами.</span><span class="sxs-lookup"><span data-stu-id="e2af1-149">It interfaces Hadoop with hello external MapReduce code you provide.</span></span>

   * <span data-ttu-id="e2af1-150">**-файлы**: Добавляет указанный hello задания MapReduce toohello файлов.</span><span class="sxs-lookup"><span data-stu-id="e2af1-150">**-files**: Adds hello specified files toohello MapReduce job.</span></span>

   * <span data-ttu-id="e2af1-151">**-сопоставления**: Hadoop указывает файл toouse как hello сопоставления, в котором.</span><span class="sxs-lookup"><span data-stu-id="e2af1-151">**-mapper**: Tells Hadoop which file toouse as hello mapper.</span></span>

   * <span data-ttu-id="e2af1-152">**-редуктора**: сообщает Hadoop, в которой файл toouse как hello редуктора.</span><span class="sxs-lookup"><span data-stu-id="e2af1-152">**-reducer**: Tells Hadoop which file toouse as hello reducer.</span></span>

   * <span data-ttu-id="e2af1-153">**-ввода**: hello входной файл, нам необходимо подсчитать слова из.</span><span class="sxs-lookup"><span data-stu-id="e2af1-153">**-input**: hello input file that we should count words from.</span></span>

   * <span data-ttu-id="e2af1-154">**-Вывод**: hello, hello выходные данные записи в каталог.</span><span class="sxs-lookup"><span data-stu-id="e2af1-154">**-output**: hello directory that hello output is written to.</span></span>

    <span data-ttu-id="e2af1-155">Как работает задания MapReduce hello, hello процесса отображаются в виде процентов.</span><span class="sxs-lookup"><span data-stu-id="e2af1-155">As hello MapReduce job works, hello process is displayed as percentages.</span></span>

        <span data-ttu-id="e2af1-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="e2af1-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="e2af1-157">Вывод tooview hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e2af1-157">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="e2af1-158">Эта команда отображает список ключевых слов и сколько раз слово hello произошла.</span><span class="sxs-lookup"><span data-stu-id="e2af1-158">This command displays a list of words and how many times hello word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2af1-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2af1-159">Next steps</span></span>

<span data-ttu-id="e2af1-160">Теперь, когда вы узнали, каким образом задания потоковой передачи MapRedcue toouse с HDInsight, используйте следующие ссылки tooexplore hello других способов toowork с Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e2af1-160">Now that you have learned how toouse streaming MapRedcue jobs with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="e2af1-161">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2af1-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e2af1-162">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2af1-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e2af1-163">Использование заданий MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2af1-163">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
