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
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a>Использование языка C# для потоковой передачи MapReduce в Hadoop в HDInsight

Узнайте, как toocreate toouse C# решения MapReduce в HDInsight.

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)

Потоковой передачи Hadoop — это программа, позволяющая toorun задания MapReduce, с помощью скрипта или исполняемого файла. В этом примере .NET — используется tooimplement hello сопоставления и редуктора для решения word count.

## <a name="net-on-hdinsight"></a>.NET в HDInsight

__HDInsight под управлением Linux__ кластеры используйте [моно (https://mono-project.com)](https://mono-project.com) toorun приложений .NET. Mono версии 4.2.1 входит в состав HDInsight версии 3.5. Дополнительные сведения о версии hello Mono, входящий в состав HDInsight см. в разделе [версий компонента HDInsight](hdinsight-component-versioning.md). toouse моно, определенную версию в разделе hello [установку или обновление моно](hdinsight-hadoop-install-mono.md) документа.

Дополнительные сведения о совместимости Mono с различными версиями платформы .NET Framework см. в разделе [Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) (Совместимость).

## <a name="how-hadoop-streaming-works"></a>Как работает потоковая передача Hadoop

процесс basic Hello, используемый для потоковой передачи в этом документе выглядит следующим образом:

1. Hadoop передает STDIN сопоставления данных toohello (mapper.exe в этом примере).
2. средство сопоставления Hello обрабатывает данные hello и выдает tooSTDOUT пары ключ значение с разделителями-знаками табуляции.
3. выходные данные Hello прочитан Hadoop и затем передается STDIN редуктора toohello (reducer.exe в этом примере).
4. Hello редуктора считывает пары ключ значение hello табуляцией, обрабатывает данные hello и затем передает результат hello парами ключей и значений с разделителями-знаками табуляции в STDOUT.
5. Hello выходных данных считывается, Hadoop и записанных toohello выходной каталог.

Дополнительные сведения о потоковой передаче см. в разделе [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html) (Потоковая передача Hadoop).

## <a name="prerequisites"></a>Предварительные требования

* Опыт написания и выполнения сборки кода C#, предназначенного для платформы .NET Framework 4.5. Hello шаги в этом документе используется Visual Studio 2017 г.

* Способ tooupload .exe файлы toohello кластер. Hello в данном пошаговом руководстве используйте hello данных Озера средства для Visual Studio tooupload hello файлы tooprimary хранилище для кластера hello.

* Azure PowerShell или SSH-клиент.

* Hadoop в кластере HDInsight. Дополнительные сведения о создании кластера см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-provision-clusters.md).

## <a name="create-hello-mapper"></a>Создание сопоставления hello

Создайте __консольное приложение__ в Visual Studio и назовите его __mapper__. Используйте следующий код для приложения hello hello.

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

После создания приложения hello, выполните его построение tooproduce hello `/bin/Debug/mapper.exe` файл в каталог проекта hello.

## <a name="create-hello-reducer"></a>Создание редуктора hello

Создайте __консольное приложение__ в Visual Studio и назовите его __reducer__. Используйте следующий код для приложения hello hello.

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

После создания приложения hello, выполните его построение tooproduce hello `/bin/Debug/reducer.exe` файл в каталог проекта hello.

## <a name="upload-toostorage"></a>Отправить toostorage

1. В Visual Studio в откройте **обозреватель сервера**.

2. Разверните пункт **Azure**, а затем — **HDInsight**.

3. При появлении запроса введите учетные данные подписки Azure и щелкните **Войти**.

4. Разверните кластер HDInsight hello, на котором необходимо toodeploy для данного приложения. Запись с текстом hello __(по умолчанию учетная запись хранилища)__ указан.

    ![Обозреватель сервера, отображающий hello учетной записи хранилища для кластера hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Если эта запись могут быть развернуты, вы используете __учетной записи хранилища Azure__ хранения по умолчанию для кластера hello. файлы tooview hello в хранилище по умолчанию hello hello кластер, разверните запись hello, а затем дважды щелкните hello __(по умолчанию контейнер)__.

    * Если эта запись не могут быть развернуты, вы используете __хранилища Озера данных Azure__ hello хранения по умолчанию для кластера hello. файлы tooview hello в хранилище по умолчанию hello кластер hello, дважды щелкните hello __(учетной записи хранения по умолчанию)__ входа.

5. файлы .exe tooupload hello, используйте один из следующих методов hello.

    * При использовании __учетной записи хранилища Azure__, щелкните значок передачи hello и найдите toohello **bin\debug** папку для hello **сопоставления** проекта. Наконец, выберите hello **mapper.exe** файла и нажмите кнопку **ОК**.

        ![значок отправки](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * При использовании __хранилища Озера данных Azure__, щелкните правой кнопкой мыши пустую область в списке файл hello и выберите __отправить__. Наконец, выберите hello **mapper.exe** файла и нажмите кнопку **откройте**.

    Здравствуйте, один раз __mapper.exe__ завершения отправки, процесс отправки повторов hello hello __reducer.exe__ файла.

## <a name="run-a-job-using-an-ssh-session"></a>Выполнение задания с помощью сеанса SSH

1. Используйте кластер HDInsight toohello tooconnect SSH. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Используйте один из hello после задания MapReduce hello toostart команды:

    * Если в качестве хранилища по умолчанию используется __Azure Data Lake Store__:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * Если в качестве хранилища по умолчанию используется __служба хранилища Azure__:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    Hello следующий список описывает, что делает каждый параметр:

    * `hadoop-streaming.jar`: hello jar-файл, содержащий hello MapReduce функции потоковой передачи.
    * `-files`: Добавляет hello `mapper.exe` и `reducer.exe` файлы toothis задания. Hello `adl:///` или `wasb:///` до корневого toohello hello путь хранения по умолчанию для кластера hello каждого файла.
    * `-mapper`: Указывает файл, который реализует hello сопоставления.
    * `-reducer`: Указывает файл, который реализует hello редуктора.
    * `-input`: hello входные данные.
    * `-output`: hello выходной каталог.

3. После завершения задания MapReduce hello, используйте следующие результаты hello tooview hello:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Hello следующий текст является примером hello данных, возвращаемых этой командой:

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a>Выполнение задания с помощью PowerShell

Используйте следующий сценарий PowerShell toorun задание MapReduce hello и загрузить результаты hello.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

Этот сценарий предложит hello кластера учетной записи имя входа и пароль, а также имя кластера HDInsight hello. После завершения задания hello hello выводится загруженный toohello `output.txt` файл в скрипте hello directory hello, запускали с. Hello следующий текст является примером данных hello в hello `output.txt` файла:

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об использовании MapReduce с HDInsight см. в разделе [Использование MapReduce в Hadoop в HDInsight](hdinsight-use-mapreduce.md).

Сведения об использовании языка C# с Hive и Pig см. в разделе [Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).

Сведения об использовании языка C# со Storm в HDInsight см. в разделе [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).