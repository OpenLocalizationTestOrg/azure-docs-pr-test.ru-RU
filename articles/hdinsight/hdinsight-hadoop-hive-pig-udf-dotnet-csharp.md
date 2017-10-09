---
title: "aaaUse C# с Hive и Pig в Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toouse C# определяемой пользователем функции (UDF) с Hive и Pig потоковой передачей в Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a>Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight.

Узнайте, как toouse C# пользовательские функции (UDF) с Apache Hive и Pig в HDInsight.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве работы с кластерами HDInsight в Linux и Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)

Оба Hive и Pig можно передать данные tooexternal приложения для обработки. Этот процесс называется _потоковой передачей_. При использовании приложения .NET, hello данных передается на STDIN toohello приложения, и приложение hello возвращает hello результаты на стандартный ВЫВОД. tooread записи из STDIN и STDOUT, вы можете использовать `Console.ReadLine()` и `Console.WriteLine()` в консольном приложении.

## <a name="prerequisites"></a>Предварительные требования

* Опыт написания и выполнения сборки кода C#, предназначенного для платформы .NET Framework 4.5.

    * Используйте любую интегрированную среду разработки. Мы рекомендуем использовать [Visual Studio](https://www.visualstudio.com/vs) 2015, Visual Studio 2017 или [Visual Studio Code](https://code.visualstudio.com/). Hello шаги в этом документе используется Visual Studio 2017 г.

* .exe tooupload способом файлы toohello кластера и выполнения заданий Pig и Hive. Мы рекомендуем hello данных Озера средства для Visual Studio, Azure PowerShell и Azure CLI. Hello в данном пошаговом руководстве используйте средства Озера данных hello файлов hello tooupload Visual Studio и выполните запрос Hive пример hello.

    Сведения о других способов toorun Hive запросы и задания Pig в разделе hello следующие документы:

    * [Использование Hive и HiveQL с Hadoop в HDInsight для анализа примера файла Apache log4j](hdinsight-use-hive.md)

    * [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)

* Hadoop в кластере HDInsight. Дополнительные сведения о создании кластера см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-provision-clusters.md).

## <a name="net-on-hdinsight"></a>.NET в HDInsight

* __HDInsight под управлением Linux__ кластеры, использующие [моно (https://mono-project.com)](https://mono-project.com) toorun приложений .NET. Mono версии 4.2.1 входит в состав HDInsight версии 3.5.

    Дополнительные сведения о совместимости Mono с различными версиями платформы .NET Framework см. в разделе [Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) (Совместимость).

    toouse моно, определенную версию в разделе hello [установку или обновление моно](hdinsight-hadoop-install-mono.md) документа.

* __HDInsight под управлением Windows__ кластеры использовать приложений .NET toorun hello Microsoft .NET CLR.

Дополнительные сведения о версии hello hello .NET framework и Mono, входящий в состав версий HDInsight см. в разделе [версий компонента HDInsight](hdinsight-component-versioning.md).

## <a name="create-hello-c-projects"></a>Создать hello C\# проектов

### <a name="hive-udf"></a>Определяемая пользователем функция Hive

1. Откройте Visual Studio и создайте решение. Выберите тип проекта hello **консольного приложения (.NET Framework)**и новый проект hello имя **HiveCSharp**.

    > [!IMPORTANT]
    > Если используется кластер HDInsight под управлением Linux, выберите __.NET Framework 4.5__. Дополнительные сведения о совместимости Mono с различными версиями платформы .NET Framework см. в разделе [Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) (Совместимость).

2. Замените содержимое hello **Program.cs** hello следующее:

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. Построение проекта hello.

### <a name="pig-udf"></a>Определяемая пользователем функция Pig

1. Откройте Visual Studio и создайте решение. Выберите тип проекта hello **консольное приложение**и новый проект hello имя **PigUDF**.

2. Замените содержимое hello hello **Program.cs** файл с hello, следующий код:

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    Это приложение выполняет синтаксический анализ строки hello, отправленные из Pig и переформатирование строки, начинающиеся с `java.lang.Exception`.

3. Сохранить **Program.cs**, а затем постройте проект hello.

## <a name="upload-toostorage"></a>Отправить toostorage

1. В Visual Studio в откройте **обозреватель сервера**.

2. Разверните пункт **Azure**, а затем — **HDInsight**.

3. При появлении запроса введите учетные данные подписки Azure и щелкните **Войти**.

4. Разверните кластер HDInsight hello, на котором необходимо toodeploy для данного приложения. Запись с текстом hello __(по умолчанию учетная запись хранилища)__ указан.

    ![Обозреватель сервера, отображающий hello учетной записи хранилища для кластера hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Если эта запись могут быть развернуты, вы используете __учетной записи хранилища Azure__ хранения по умолчанию для кластера hello. файлы tooview hello в хранилище по умолчанию hello hello кластер, разверните запись hello, а затем дважды щелкните hello __(по умолчанию контейнер)__.

    * Если эта запись не могут быть развернуты, вы используете __хранилища Озера данных Azure__ hello хранения по умолчанию для кластера hello. файлы tooview hello в хранилище по умолчанию hello кластер hello, дважды щелкните hello __(учетной записи хранения по умолчанию)__ входа.

6. файлы .exe tooupload hello, используйте один из следующих методов hello.

    * При использовании __учетной записи хранилища Azure__, щелкните значок передачи hello и найдите toohello **bin\debug** папку для hello **HiveCSharp** проекта. Наконец, выберите hello **HiveCSharp.exe** файла и нажмите кнопку **ОК**.

        ![значок отправки](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * При использовании __хранилища Озера данных Azure__, щелкните правой кнопкой мыши пустую область в списке файл hello и выберите __отправить__. Наконец, выберите hello **HiveCSharp.exe** файла и нажмите кнопку **откройте**.

    Здравствуйте, один раз __HiveCSharp.exe__ завершения отправки, процесс отправки повторов hello hello __PigUDF.exe__ файла.

## <a name="run-a-hive-query"></a>Выполнение запроса Hive

1. В Visual Studio в откройте **обозреватель сервера**.

2. Разверните пункт **Azure**, а затем — **HDInsight**.

3. Щелкните правой кнопкой мыши кластер hello, развернутым hello **HiveCSharp** приложение, а затем выберите **написать запрос Hive**.

4. Используйте следующий текст для запроса Hive hello hello.

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > Раскомментируйте hello `add file` инструкции, соответствующий типу hello хранения по умолчанию, используемый для кластера.

    Этот запрос выбирает hello `clientid`, `devicemake`, и `devicemodel` поля из `hivesampletable`и передает toohello HiveCSharp.exe приложения hello поля. Hello запрос ожидает hello приложения tooreturn три поля, которые хранятся в виде `clientid`, `phoneLabel`, и `phoneHash`. Hello запрос ожидает toofind HiveCSharp.exe в hello корневого контейнера хранилища по умолчанию hello.

5. Нажмите кнопку **отправить** toosubmit hello задания toohello HDInsight кластера. Hello **Hive Сводка заданий** открывается окно.

6. Нажмите кнопку **обновление** toorefresh hello сводки до **состояние задания** изменяет слишком**завершено**. выходные данные задания tooview hello, нажмите кнопку **выходные данные задания**.

## <a name="run-a-pig-job"></a>Выполнение задания Pig

1. Используйте один из hello следующие методы tooconnect tooyour HDInsight кластера.

    * Если используется кластер HDInsight под управлением __Linux__, примените протокол SSH. Например, `ssh sshuser@mycluster-ssh.azurehdinsight.net`. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).
    
    * Если вы используете __под управлением Windows__ кластера HDInsight [кластера toohello подключение с помощью удаленного рабочего стола](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)

2. Используйте один hello, следующая команда toostart hello Pig командной строки:

        pig

    > [!IMPORTANT]
    > При использовании кластера под управлением Windows используйте следующие команды вместо hello:
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    Откроется командная строка `grunt>`.

3. Введите hello следующие toorun задания Pig, использующий hello приложения .NET Framework:

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    Hello `DEFINE` инструкция создает псевдоним `streamer` для hello pigudf.exe приложений и `CACHE` загружает его из хранилища по умолчанию для кластера hello. Позже `streamer` используется с hello `STREAM` tooprocess оператор hello одиночных строк из ЖУРНАЛОВ и данных возвращаемого hello как ряд столбцов.

    > [!NOTE]
    > Имя приложения Hello, который используется для потоковой передачи должно быть заключено в hello \` (обратный апостроф) символов при псевдонимами, и ' (одинарная кавычка) при использовании с `SHIP`.

4. После ввода последней строкой hello, будет запущено задание hello. Он возвращает выходные данные примерно toohello после текста:

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a>Дальнейшие действия

В этом документе вы узнали как toouse приложения .NET Framework из Hive и Pig в HDInsight. При желании в статье toouse Python с Hive и Pig, toolearn [использование Python с Hive и Pig в HDInsight](hdinsight-python.md).

Другие способы toouse Pig и Hive и toolearn об использовании MapReduce в разделе hello следующие документы:

* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с HDInsight](hdinsight-use-mapreduce.md)
