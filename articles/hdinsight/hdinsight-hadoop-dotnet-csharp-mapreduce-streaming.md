---
title: "Использование C# с MapReduce в Hadoop HDInsight в Azure | Документация Майкрософт"
description: "Узнайте, как использовать C# для создания решений MapReduce, использующих Hadoop в Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: adb454e56378a800c671614735aec78b6851aeb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="906cc-103">Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="906cc-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="906cc-104">Узнайте, как использовать C# для создания решения MapReduce в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="906cc-104">Learn how to use C# to create a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="906cc-105">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="906cc-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="906cc-106">Дополнительные сведения см. в разделе [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="906cc-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="906cc-107">Потоковая передача Hadoop обеспечивается служебной программой, которая позволяет запускать задания MapReduce с помощью сценария или исполняемого файла.</span><span class="sxs-lookup"><span data-stu-id="906cc-107">Hadoop streaming is a utility that allows you to run MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="906cc-108">В этом примере .NET используется для реализации модулей сопоставления и редукции для решения для подсчета слов.</span><span class="sxs-lookup"><span data-stu-id="906cc-108">In this example, .NET is used to implement the mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="906cc-109">.NET в HDInsight</span><span class="sxs-lookup"><span data-stu-id="906cc-109">.NET on HDInsight</span></span>

<span data-ttu-id="906cc-110">В кластерах __HDInsight под управлением Linux__ для запуска приложений .NET используется [Mono (https://mono-project.com)](https://mono-project.com).</span><span class="sxs-lookup"><span data-stu-id="906cc-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="906cc-111">Mono версии 4.2.1 входит в состав HDInsight версии 3.5.</span><span class="sxs-lookup"><span data-stu-id="906cc-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="906cc-112">Дополнительные сведения о версии Mono, которая входит в состав HDInsight, см. в разделе [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="906cc-112">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="906cc-113">Чтобы использовать определенную версию Mono, см. статью об [установке или обновлении Mono](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="906cc-113">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="906cc-114">Дополнительные сведения о совместимости Mono с различными версиями платформы .NET Framework см. в разделе [Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) (Совместимость).</span><span class="sxs-lookup"><span data-stu-id="906cc-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="906cc-115">Как работает потоковая передача Hadoop</span><span class="sxs-lookup"><span data-stu-id="906cc-115">How Hadoop streaming works</span></span>

<span data-ttu-id="906cc-116">Базовый процесс потоковой передачи в данном документе выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="906cc-116">The basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="906cc-117">Hadoop передает данные в модуль сопоставления (mapper.exe в этом примере) через канал STDIN.</span><span class="sxs-lookup"><span data-stu-id="906cc-117">Hadoop passes data to the mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="906cc-118">Модуль сопоставления обрабатывает эти данные и передает пары "ключ-значение", разделенные знаками табуляции, в канал STDOUT.</span><span class="sxs-lookup"><span data-stu-id="906cc-118">The mapper processes the data, and emits tab-delimited key/value pairs to STDOUT.</span></span>
3. <span data-ttu-id="906cc-119">Выходные данные считываются Hadoop и затем передаются в модуль редукции (reducer.exe в этом примере) на STDIN.</span><span class="sxs-lookup"><span data-stu-id="906cc-119">The output is read by Hadoop, and then passed to the reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="906cc-120">Модуль редукции считывает пары "ключ-значение", разделенные знаками табуляции, обрабатывает данные и передает результат в виде пар "ключ-значение", разделенные знаками табуляции, в канал STDOUT.</span><span class="sxs-lookup"><span data-stu-id="906cc-120">The reducer reads the tab-delimited key/value pairs, processes the data, and then emits the result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="906cc-121">Выходные данные считываются Hadoop и записываются в выходной каталог.</span><span class="sxs-lookup"><span data-stu-id="906cc-121">The output is read by Hadoop and written to the output directory.</span></span>

<span data-ttu-id="906cc-122">Дополнительные сведения о потоковой передаче см. в разделе [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html) (Потоковая передача Hadoop).</span><span class="sxs-lookup"><span data-stu-id="906cc-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="906cc-123">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="906cc-123">Prerequisites</span></span>

* <span data-ttu-id="906cc-124">Опыт написания и выполнения сборки кода C#, предназначенного для платформы .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="906cc-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="906cc-125">В этом руководстве используется Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="906cc-125">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="906cc-126">Способ передачи EXE-файлов в кластер.</span><span class="sxs-lookup"><span data-stu-id="906cc-126">A way to upload .exe files to the cluster.</span></span> <span data-ttu-id="906cc-127">В этом документе для передачи файлов в основное хранилище кластера используются средства Data Lake для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="906cc-127">The steps in this document use the Data Lake Tools for Visual Studio to upload the files to primary storage for the cluster.</span></span>

* <span data-ttu-id="906cc-128">Azure PowerShell или SSH-клиент.</span><span class="sxs-lookup"><span data-stu-id="906cc-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="906cc-129">Hadoop в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="906cc-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="906cc-130">Дополнительные сведения о создании кластера см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="906cc-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-the-mapper"></a><span data-ttu-id="906cc-131">Создание модуля сопоставления</span><span class="sxs-lookup"><span data-stu-id="906cc-131">Create the mapper</span></span>

<span data-ttu-id="906cc-132">Создайте __консольное приложение__ в Visual Studio и назовите его __mapper__.</span><span class="sxs-lookup"><span data-stu-id="906cc-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="906cc-133">Используйте для него следующий код.</span><span class="sxs-lookup"><span data-stu-id="906cc-133">Use the following code for the application:</span></span>

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data to the mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over the words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

<span data-ttu-id="906cc-134">После создания приложения выполните его сборку, чтобы создать файл `/bin/Debug/mapper.exe` в каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="906cc-134">After creating the application, build it to produce the `/bin/Debug/mapper.exe` file in the project directory.</span></span>

## <a name="create-the-reducer"></a><span data-ttu-id="906cc-135">Создание модуля редукции</span><span class="sxs-lookup"><span data-stu-id="906cc-135">Create the reducer</span></span>

<span data-ttu-id="906cc-136">Создайте __консольное приложение__ в Visual Studio и назовите его __reducer__.</span><span class="sxs-lookup"><span data-stu-id="906cc-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="906cc-137">Используйте для него следующий код.</span><span class="sxs-lookup"><span data-stu-id="906cc-137">Use the following code for the application:</span></span>

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get the word
                string word = sArr[0];
                // Get the count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for the word?
                if(words.ContainsKey(word))
                {
                    //If so, increment the count
                    words[word] += count;
                } else
                {
                    //Add the key to the collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

<span data-ttu-id="906cc-138">После создания приложения выполните его сборку, чтобы создать файл `/bin/Debug/reducer.exe` в каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="906cc-138">After creating the application, build it to produce the `/bin/Debug/reducer.exe` file in the project directory.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="906cc-139">Отправка в хранилище</span><span class="sxs-lookup"><span data-stu-id="906cc-139">Upload to storage</span></span>

1. <span data-ttu-id="906cc-140">В Visual Studio в откройте **обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="906cc-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="906cc-141">Разверните пункт **Azure**, а затем — **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="906cc-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="906cc-142">При появлении запроса введите учетные данные подписки Azure и щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="906cc-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="906cc-143">Разверните кластер HDInsight, в который нужно развернуть это приложение.</span><span class="sxs-lookup"><span data-stu-id="906cc-143">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="906cc-144">Отобразится запись с текстом __(Учетная запись хранения по умолчанию)__.</span><span class="sxs-lookup"><span data-stu-id="906cc-144">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![В обозревателе серверов отображается учетная запись хранения для кластера](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="906cc-146">Если эту запись можно развернуты, то для кластера в качестве хранилища по умолчанию используется __учетная запись хранения Azure__.</span><span class="sxs-lookup"><span data-stu-id="906cc-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="906cc-147">Чтобы просмотреть файлы в хранилище по умолчанию кластера, разверните эту запись, а затем дважды щелкните запись __(Контейнер по умолчанию)__.</span><span class="sxs-lookup"><span data-stu-id="906cc-147">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="906cc-148">Если эту запись невозможно развернуты, то для кластера в качестве хранилища по умолчанию используется __Azure Data Lake Store__.</span><span class="sxs-lookup"><span data-stu-id="906cc-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="906cc-149">Чтобы просмотреть файлы в хранилище по умолчанию кластера, дважды щелкните запись __(Контейнер по умолчанию)__.</span><span class="sxs-lookup"><span data-stu-id="906cc-149">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="906cc-150">Чтобы передать EXE-файлы, используйте один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="906cc-150">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="906cc-151">Если используется __учетная запись хранения Azure__, щелкните значок передачи и перейдите в папку **bin\debug** проекта **mapper**.</span><span class="sxs-lookup"><span data-stu-id="906cc-151">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **mapper** project.</span></span> <span data-ttu-id="906cc-152">Выберите файл **mapper.exe** и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="906cc-152">Finally, select the **mapper.exe** file and click **Ok**.</span></span>

        ![значок отправки](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="906cc-154">Если используется __Azure Data Lake Store__, щелкните правой кнопкой мыши пустое место в списке файлов и выберите __Отправить__.</span><span class="sxs-lookup"><span data-stu-id="906cc-154">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="906cc-155">Выберите файл **mapper.exe** и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="906cc-155">Finally, select the **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="906cc-156">После завершения передачи __mapper.exe__ повторите этот процесс для передачи файла __reducer.exe__.</span><span class="sxs-lookup"><span data-stu-id="906cc-156">Once the __mapper.exe__ upload has finished, repeat the upload process for the __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="906cc-157">Выполнение задания с помощью сеанса SSH</span><span class="sxs-lookup"><span data-stu-id="906cc-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="906cc-158">Подключитесь к кластеру HDInsight с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="906cc-158">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="906cc-159">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="906cc-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="906cc-160">Используйте одну из приведенных команд для запуска задания MapReduce.</span><span class="sxs-lookup"><span data-stu-id="906cc-160">Use one of the following command to start the MapReduce job:</span></span>

    * <span data-ttu-id="906cc-161">Если в качестве хранилища по умолчанию используется __Azure Data Lake Store__:</span><span class="sxs-lookup"><span data-stu-id="906cc-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="906cc-162">Если в качестве хранилища по умолчанию используется __служба хранилища Azure__:</span><span class="sxs-lookup"><span data-stu-id="906cc-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="906cc-163">Ниже перечислены функции каждого из параметров.</span><span class="sxs-lookup"><span data-stu-id="906cc-163">The following list describes what each parameter does:</span></span>

    * <span data-ttu-id="906cc-164">`hadoop-streaming.jar`: JAR-файл, содержащий функции потоковой передачи MapReduce.</span><span class="sxs-lookup"><span data-stu-id="906cc-164">`hadoop-streaming.jar`: The jar file that contains the streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="906cc-165">`-files`: добавляет файлы `mapper.exe` и `reducer.exe` в это задание.</span><span class="sxs-lookup"><span data-stu-id="906cc-165">`-files`: Adds the `mapper.exe` and `reducer.exe` files to this job.</span></span> <span data-ttu-id="906cc-166">`adl:///` или `wasb:///` перед именем файла — это путь к корню хранилища по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="906cc-166">The `adl:///` or `wasb:///` before each file is the path to the root of default storage for the cluster.</span></span>
    * <span data-ttu-id="906cc-167">`-mapper`: задает файл, который реализует модуль сопоставления.</span><span class="sxs-lookup"><span data-stu-id="906cc-167">`-mapper`: Specifies which file implements the mapper.</span></span>
    * <span data-ttu-id="906cc-168">`-reducer`: задает файл, который реализует модуль редукции.</span><span class="sxs-lookup"><span data-stu-id="906cc-168">`-reducer`: Specifies which file implements the reducer.</span></span>
    * <span data-ttu-id="906cc-169">`-input`: входные данные.</span><span class="sxs-lookup"><span data-stu-id="906cc-169">`-input`: The input data.</span></span>
    * <span data-ttu-id="906cc-170">`-output`: выходной каталог.</span><span class="sxs-lookup"><span data-stu-id="906cc-170">`-output`: The output directory.</span></span>

3. <span data-ttu-id="906cc-171">После завершения задания MapReduce просмотрите результаты с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="906cc-171">Once the MapReduce job completes, use the following to view the results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="906cc-172">Ниже приведен пример данных, возвращаемых этой командой.</span><span class="sxs-lookup"><span data-stu-id="906cc-172">The following text is an example of the data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="906cc-173">Выполнение задания с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="906cc-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="906cc-174">Используйте приведенный ниже сценарий PowerShell для запуска задания MapReduce и скачивания результатов.</span><span class="sxs-lookup"><span data-stu-id="906cc-174">Use the following PowerShell script to run a MapReduce job and download the results.</span></span>

<span data-ttu-id="906cc-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span><span class="sxs-lookup"><span data-stu-id="906cc-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span></span>

<span data-ttu-id="906cc-176">Этот сценарий предлагает ввести имя учетной записи для входа и пароль для кластера, а также имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="906cc-176">This script prompts you for the cluster login account name and password, along with the HDInsight cluster name.</span></span> <span data-ttu-id="906cc-177">После завершения задания выходные данные будут скачаны в файл `output.txt` в каталоге, в котором был выполнен сценарий.</span><span class="sxs-lookup"><span data-stu-id="906cc-177">Once the job completes, the output is downloaded to the `output.txt` file in the directory the script is ran from.</span></span> <span data-ttu-id="906cc-178">Ниже приведен пример выходных данных в файле `output.txt`.</span><span class="sxs-lookup"><span data-stu-id="906cc-178">The following text is an example of the data in the `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="906cc-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="906cc-179">Next steps</span></span>

<span data-ttu-id="906cc-180">Дополнительные сведения об использовании MapReduce с HDInsight см. в разделе [Использование MapReduce в Hadoop в HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="906cc-180">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="906cc-181">Сведения об использовании языка C# с Hive и Pig см. в разделе [Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="906cc-181">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="906cc-182">Сведения об использовании языка C# со Storm в HDInsight см. в разделе [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="906cc-182">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>