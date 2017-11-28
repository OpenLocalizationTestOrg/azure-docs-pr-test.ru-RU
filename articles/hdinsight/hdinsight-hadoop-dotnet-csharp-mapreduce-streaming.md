---
title: "aaaUse C# с MapReduce в Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как решения MapReduce toocreate toouse C# с Hadoop в Azure HDInsight."
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
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="cd63e-103">Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd63e-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="cd63e-104">Узнайте, как toocreate toouse C# решения MapReduce в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd63e-104">Learn how toouse C# toocreate a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd63e-105">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="cd63e-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cd63e-106">Дополнительные сведения см. в разделе [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="cd63e-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="cd63e-107">Потоковой передачи Hadoop — это программа, позволяющая toorun задания MapReduce, с помощью скрипта или исполняемого файла.</span><span class="sxs-lookup"><span data-stu-id="cd63e-107">Hadoop streaming is a utility that allows you toorun MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="cd63e-108">В этом примере .NET — используется tooimplement hello сопоставления и редуктора для решения word count.</span><span class="sxs-lookup"><span data-stu-id="cd63e-108">In this example, .NET is used tooimplement hello mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="cd63e-109">.NET в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd63e-109">.NET on HDInsight</span></span>

<span data-ttu-id="cd63e-110">__HDInsight под управлением Linux__ кластеры используйте [моно (https://mono-project.com)](https://mono-project.com) toorun приложений .NET.</span><span class="sxs-lookup"><span data-stu-id="cd63e-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="cd63e-111">Mono версии 4.2.1 входит в состав HDInsight версии 3.5.</span><span class="sxs-lookup"><span data-stu-id="cd63e-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="cd63e-112">Дополнительные сведения о версии hello Mono, входящий в состав HDInsight см. в разделе [версий компонента HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="cd63e-112">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="cd63e-113">toouse моно, определенную версию в разделе hello [установку или обновление моно](hdinsight-hadoop-install-mono.md) документа.</span><span class="sxs-lookup"><span data-stu-id="cd63e-113">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="cd63e-114">Дополнительные сведения о совместимости Mono с различными версиями платформы .NET Framework см. в разделе [Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) (Совместимость).</span><span class="sxs-lookup"><span data-stu-id="cd63e-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="cd63e-115">Как работает потоковая передача Hadoop</span><span class="sxs-lookup"><span data-stu-id="cd63e-115">How Hadoop streaming works</span></span>

<span data-ttu-id="cd63e-116">процесс basic Hello, используемый для потоковой передачи в этом документе выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cd63e-116">hello basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="cd63e-117">Hadoop передает STDIN сопоставления данных toohello (mapper.exe в этом примере).</span><span class="sxs-lookup"><span data-stu-id="cd63e-117">Hadoop passes data toohello mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="cd63e-118">средство сопоставления Hello обрабатывает данные hello и выдает tooSTDOUT пары ключ значение с разделителями-знаками табуляции.</span><span class="sxs-lookup"><span data-stu-id="cd63e-118">hello mapper processes hello data, and emits tab-delimited key/value pairs tooSTDOUT.</span></span>
3. <span data-ttu-id="cd63e-119">выходные данные Hello прочитан Hadoop и затем передается STDIN редуктора toohello (reducer.exe в этом примере).</span><span class="sxs-lookup"><span data-stu-id="cd63e-119">hello output is read by Hadoop, and then passed toohello reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="cd63e-120">Hello редуктора считывает пары ключ значение hello табуляцией, обрабатывает данные hello и затем передает результат hello парами ключей и значений с разделителями-знаками табуляции в STDOUT.</span><span class="sxs-lookup"><span data-stu-id="cd63e-120">hello reducer reads hello tab-delimited key/value pairs, processes hello data, and then emits hello result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="cd63e-121">Hello выходных данных считывается, Hadoop и записанных toohello выходной каталог.</span><span class="sxs-lookup"><span data-stu-id="cd63e-121">hello output is read by Hadoop and written toohello output directory.</span></span>

<span data-ttu-id="cd63e-122">Дополнительные сведения о потоковой передаче см. в разделе [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html) (Потоковая передача Hadoop).</span><span class="sxs-lookup"><span data-stu-id="cd63e-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd63e-123">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cd63e-123">Prerequisites</span></span>

* <span data-ttu-id="cd63e-124">Опыт написания и выполнения сборки кода C#, предназначенного для платформы .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="cd63e-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="cd63e-125">Hello шаги в этом документе используется Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="cd63e-125">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="cd63e-126">Способ tooupload .exe файлы toohello кластер.</span><span class="sxs-lookup"><span data-stu-id="cd63e-126">A way tooupload .exe files toohello cluster.</span></span> <span data-ttu-id="cd63e-127">Hello в данном пошаговом руководстве используйте hello данных Озера средства для Visual Studio tooupload hello файлы tooprimary хранилище для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cd63e-127">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files tooprimary storage for hello cluster.</span></span>

* <span data-ttu-id="cd63e-128">Azure PowerShell или SSH-клиент.</span><span class="sxs-lookup"><span data-stu-id="cd63e-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="cd63e-129">Hadoop в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd63e-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="cd63e-130">Дополнительные сведения о создании кластера см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="cd63e-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-hello-mapper"></a><span data-ttu-id="cd63e-131">Создание сопоставления hello</span><span class="sxs-lookup"><span data-stu-id="cd63e-131">Create hello mapper</span></span>

<span data-ttu-id="cd63e-132">Создайте __консольное приложение__ в Visual Studio и назовите его __mapper__.</span><span class="sxs-lookup"><span data-stu-id="cd63e-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="cd63e-133">Используйте следующий код для приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="cd63e-133">Use hello following code for hello application:</span></span>

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
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
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

<span data-ttu-id="cd63e-134">После создания приложения hello, выполните его построение tooproduce hello `/bin/Debug/mapper.exe` файл в каталог проекта hello.</span><span class="sxs-lookup"><span data-stu-id="cd63e-134">After creating hello application, build it tooproduce hello `/bin/Debug/mapper.exe` file in hello project directory.</span></span>

## <a name="create-hello-reducer"></a><span data-ttu-id="cd63e-135">Создание редуктора hello</span><span class="sxs-lookup"><span data-stu-id="cd63e-135">Create hello reducer</span></span>

<span data-ttu-id="cd63e-136">Создайте __консольное приложение__ в Visual Studio и назовите его __reducer__.</span><span class="sxs-lookup"><span data-stu-id="cd63e-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="cd63e-137">Используйте следующий код для приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="cd63e-137">Use hello following code for hello application:</span></span>

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
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
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

<span data-ttu-id="cd63e-138">После создания приложения hello, выполните его построение tooproduce hello `/bin/Debug/reducer.exe` файл в каталог проекта hello.</span><span class="sxs-lookup"><span data-stu-id="cd63e-138">After creating hello application, build it tooproduce hello `/bin/Debug/reducer.exe` file in hello project directory.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="cd63e-139">Отправить toostorage</span><span class="sxs-lookup"><span data-stu-id="cd63e-139">Upload toostorage</span></span>

1. <span data-ttu-id="cd63e-140">В Visual Studio в откройте **обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="cd63e-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="cd63e-141">Разверните пункт **Azure**, а затем — **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cd63e-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="cd63e-142">При появлении запроса введите учетные данные подписки Azure и щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="cd63e-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="cd63e-143">Разверните кластер HDInsight hello, на котором необходимо toodeploy для данного приложения.</span><span class="sxs-lookup"><span data-stu-id="cd63e-143">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="cd63e-144">Запись с текстом hello __(по умолчанию учетная запись хранилища)__ указан.</span><span class="sxs-lookup"><span data-stu-id="cd63e-144">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Обозреватель сервера, отображающий hello учетной записи хранилища для кластера hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="cd63e-146">Если эта запись могут быть развернуты, вы используете __учетной записи хранилища Azure__ хранения по умолчанию для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cd63e-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="cd63e-147">файлы tooview hello в хранилище по умолчанию hello hello кластер, разверните запись hello, а затем дважды щелкните hello __(по умолчанию контейнер)__.</span><span class="sxs-lookup"><span data-stu-id="cd63e-147">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="cd63e-148">Если эта запись не могут быть развернуты, вы используете __хранилища Озера данных Azure__ hello хранения по умолчанию для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cd63e-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="cd63e-149">файлы tooview hello в хранилище по умолчанию hello кластер hello, дважды щелкните hello __(учетной записи хранения по умолчанию)__ входа.</span><span class="sxs-lookup"><span data-stu-id="cd63e-149">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="cd63e-150">файлы .exe tooupload hello, используйте один из следующих методов hello.</span><span class="sxs-lookup"><span data-stu-id="cd63e-150">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="cd63e-151">При использовании __учетной записи хранилища Azure__, щелкните значок передачи hello и найдите toohello **bin\debug** папку для hello **сопоставления** проекта.</span><span class="sxs-lookup"><span data-stu-id="cd63e-151">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **mapper** project.</span></span> <span data-ttu-id="cd63e-152">Наконец, выберите hello **mapper.exe** файла и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cd63e-152">Finally, select hello **mapper.exe** file and click **Ok**.</span></span>

        ![значок отправки](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="cd63e-154">При использовании __хранилища Озера данных Azure__, щелкните правой кнопкой мыши пустую область в списке файл hello и выберите __отправить__.</span><span class="sxs-lookup"><span data-stu-id="cd63e-154">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="cd63e-155">Наконец, выберите hello **mapper.exe** файла и нажмите кнопку **откройте**.</span><span class="sxs-lookup"><span data-stu-id="cd63e-155">Finally, select hello **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="cd63e-156">Здравствуйте, один раз __mapper.exe__ завершения отправки, процесс отправки повторов hello hello __reducer.exe__ файла.</span><span class="sxs-lookup"><span data-stu-id="cd63e-156">Once hello __mapper.exe__ upload has finished, repeat hello upload process for hello __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="cd63e-157">Выполнение задания с помощью сеанса SSH</span><span class="sxs-lookup"><span data-stu-id="cd63e-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="cd63e-158">Используйте кластер HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="cd63e-158">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="cd63e-159">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cd63e-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="cd63e-160">Используйте один из hello после задания MapReduce hello toostart команды:</span><span class="sxs-lookup"><span data-stu-id="cd63e-160">Use one of hello following command toostart hello MapReduce job:</span></span>

    * <span data-ttu-id="cd63e-161">Если в качестве хранилища по умолчанию используется __Azure Data Lake Store__:</span><span class="sxs-lookup"><span data-stu-id="cd63e-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="cd63e-162">Если в качестве хранилища по умолчанию используется __служба хранилища Azure__:</span><span class="sxs-lookup"><span data-stu-id="cd63e-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="cd63e-163">Hello следующий список описывает, что делает каждый параметр:</span><span class="sxs-lookup"><span data-stu-id="cd63e-163">hello following list describes what each parameter does:</span></span>

    * <span data-ttu-id="cd63e-164">`hadoop-streaming.jar`: hello jar-файл, содержащий hello MapReduce функции потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="cd63e-164">`hadoop-streaming.jar`: hello jar file that contains hello streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="cd63e-165">`-files`: Добавляет hello `mapper.exe` и `reducer.exe` файлы toothis задания.</span><span class="sxs-lookup"><span data-stu-id="cd63e-165">`-files`: Adds hello `mapper.exe` and `reducer.exe` files toothis job.</span></span> <span data-ttu-id="cd63e-166">Hello `adl:///` или `wasb:///` до корневого toohello hello путь хранения по умолчанию для кластера hello каждого файла.</span><span class="sxs-lookup"><span data-stu-id="cd63e-166">hello `adl:///` or `wasb:///` before each file is hello path toohello root of default storage for hello cluster.</span></span>
    * <span data-ttu-id="cd63e-167">`-mapper`: Указывает файл, который реализует hello сопоставления.</span><span class="sxs-lookup"><span data-stu-id="cd63e-167">`-mapper`: Specifies which file implements hello mapper.</span></span>
    * <span data-ttu-id="cd63e-168">`-reducer`: Указывает файл, который реализует hello редуктора.</span><span class="sxs-lookup"><span data-stu-id="cd63e-168">`-reducer`: Specifies which file implements hello reducer.</span></span>
    * <span data-ttu-id="cd63e-169">`-input`: hello входные данные.</span><span class="sxs-lookup"><span data-stu-id="cd63e-169">`-input`: hello input data.</span></span>
    * <span data-ttu-id="cd63e-170">`-output`: hello выходной каталог.</span><span class="sxs-lookup"><span data-stu-id="cd63e-170">`-output`: hello output directory.</span></span>

3. <span data-ttu-id="cd63e-171">После завершения задания MapReduce hello, используйте следующие результаты hello tooview hello:</span><span class="sxs-lookup"><span data-stu-id="cd63e-171">Once hello MapReduce job completes, use hello following tooview hello results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="cd63e-172">Hello следующий текст является примером hello данных, возвращаемых этой командой:</span><span class="sxs-lookup"><span data-stu-id="cd63e-172">hello following text is an example of hello data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="cd63e-173">Выполнение задания с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd63e-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="cd63e-174">Используйте следующий сценарий PowerShell toorun задание MapReduce hello и загрузить результаты hello.</span><span class="sxs-lookup"><span data-stu-id="cd63e-174">Use hello following PowerShell script toorun a MapReduce job and download hello results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="cd63e-175">Этот сценарий предложит hello кластера учетной записи имя входа и пароль, а также имя кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cd63e-175">This script prompts you for hello cluster login account name and password, along with hello HDInsight cluster name.</span></span> <span data-ttu-id="cd63e-176">После завершения задания hello hello выводится загруженный toohello `output.txt` файл в скрипте hello directory hello, запускали с.</span><span class="sxs-lookup"><span data-stu-id="cd63e-176">Once hello job completes, hello output is downloaded toohello `output.txt` file in hello directory hello script is ran from.</span></span> <span data-ttu-id="cd63e-177">Hello следующий текст является примером данных hello в hello `output.txt` файла:</span><span class="sxs-lookup"><span data-stu-id="cd63e-177">hello following text is an example of hello data in hello `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="cd63e-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd63e-178">Next steps</span></span>

<span data-ttu-id="cd63e-179">Дополнительные сведения об использовании MapReduce с HDInsight см. в разделе [Использование MapReduce в Hadoop в HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="cd63e-179">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="cd63e-180">Сведения об использовании языка C# с Hive и Pig см. в разделе [Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="cd63e-180">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="cd63e-181">Сведения об использовании языка C# со Storm в HDInsight см. в разделе [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cd63e-181">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>