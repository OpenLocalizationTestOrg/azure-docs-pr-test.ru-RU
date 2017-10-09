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
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="d33f6-103">Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d33f6-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="d33f6-104">Узнайте, как toouse C# пользовательские функции (UDF) с Apache Hive и Pig в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d33f6-104">Learn how toouse C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d33f6-105">Hello в данном пошаговом руководстве работы с кластерами HDInsight в Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="d33f6-105">hello steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="d33f6-106">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="d33f6-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d33f6-107">Дополнительные сведения см. в разделе [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="d33f6-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="d33f6-108">Оба Hive и Pig можно передать данные tooexternal приложения для обработки.</span><span class="sxs-lookup"><span data-stu-id="d33f6-108">Both Hive and Pig can pass data tooexternal applications for processing.</span></span> <span data-ttu-id="d33f6-109">Этот процесс называется _потоковой передачей_.</span><span class="sxs-lookup"><span data-stu-id="d33f6-109">This process is known as _streaming_.</span></span> <span data-ttu-id="d33f6-110">При использовании приложения .NET, hello данных передается на STDIN toohello приложения, и приложение hello возвращает hello результаты на стандартный ВЫВОД.</span><span class="sxs-lookup"><span data-stu-id="d33f6-110">When using a .NET applciation, hello data is passed toohello application on STDIN, and hello application returns hello results on STDOUT.</span></span> <span data-ttu-id="d33f6-111">tooread записи из STDIN и STDOUT, вы можете использовать `Console.ReadLine()` и `Console.WriteLine()` в консольном приложении.</span><span class="sxs-lookup"><span data-stu-id="d33f6-111">tooread and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d33f6-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d33f6-112">Prerequisites</span></span>

* <span data-ttu-id="d33f6-113">Опыт написания и выполнения сборки кода C#, предназначенного для платформы .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d33f6-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="d33f6-114">Используйте любую интегрированную среду разработки.</span><span class="sxs-lookup"><span data-stu-id="d33f6-114">Use whatever IDE you want.</span></span> <span data-ttu-id="d33f6-115">Мы рекомендуем использовать [Visual Studio](https://www.visualstudio.com/vs) 2015, Visual Studio 2017 или [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="d33f6-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="d33f6-116">Hello шаги в этом документе используется Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="d33f6-116">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="d33f6-117">.exe tooupload способом файлы toohello кластера и выполнения заданий Pig и Hive.</span><span class="sxs-lookup"><span data-stu-id="d33f6-117">A way tooupload .exe files toohello cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="d33f6-118">Мы рекомендуем hello данных Озера средства для Visual Studio, Azure PowerShell и Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d33f6-118">We recommend hello Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="d33f6-119">Hello в данном пошаговом руководстве используйте средства Озера данных hello файлов hello tooupload Visual Studio и выполните запрос Hive пример hello.</span><span class="sxs-lookup"><span data-stu-id="d33f6-119">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files and run hello example Hive query.</span></span>

    <span data-ttu-id="d33f6-120">Сведения о других способов toorun Hive запросы и задания Pig в разделе hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="d33f6-120">For information on other ways toorun Hive queries and Pig jobs, see hello following documents:</span></span>

    * [<span data-ttu-id="d33f6-121">Использование Hive и HiveQL с Hadoop в HDInsight для анализа примера файла Apache log4j</span><span class="sxs-lookup"><span data-stu-id="d33f6-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="d33f6-122">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d33f6-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="d33f6-123">Hadoop в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d33f6-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="d33f6-124">Дополнительные сведения о создании кластера см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d33f6-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="d33f6-125">.NET в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d33f6-125">.NET on HDInsight</span></span>

* <span data-ttu-id="d33f6-126">__HDInsight под управлением Linux__ кластеры, использующие [моно (https://mono-project.com)](https://mono-project.com) toorun приложений .NET.</span><span class="sxs-lookup"><span data-stu-id="d33f6-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="d33f6-127">Mono версии 4.2.1 входит в состав HDInsight версии 3.5.</span><span class="sxs-lookup"><span data-stu-id="d33f6-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="d33f6-128">Дополнительные сведения о совместимости Mono с различными версиями платформы .NET Framework см. в разделе [Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) (Совместимость).</span><span class="sxs-lookup"><span data-stu-id="d33f6-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="d33f6-129">toouse моно, определенную версию в разделе hello [установку или обновление моно](hdinsight-hadoop-install-mono.md) документа.</span><span class="sxs-lookup"><span data-stu-id="d33f6-129">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="d33f6-130">__HDInsight под управлением Windows__ кластеры использовать приложений .NET toorun hello Microsoft .NET CLR.</span><span class="sxs-lookup"><span data-stu-id="d33f6-130">__Windows-based HDInsight__ clusters use hello Microsoft .NET CLR toorun .NET applications.</span></span>

<span data-ttu-id="d33f6-131">Дополнительные сведения о версии hello hello .NET framework и Mono, входящий в состав версий HDInsight см. в разделе [версий компонента HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d33f6-131">For more information on hello version of hello .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-hello-c-projects"></a><span data-ttu-id="d33f6-132">Создать hello C\# проектов</span><span class="sxs-lookup"><span data-stu-id="d33f6-132">Create hello C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="d33f6-133">Определяемая пользователем функция Hive</span><span class="sxs-lookup"><span data-stu-id="d33f6-133">Hive UDF</span></span>

1. <span data-ttu-id="d33f6-134">Откройте Visual Studio и создайте решение.</span><span class="sxs-lookup"><span data-stu-id="d33f6-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="d33f6-135">Выберите тип проекта hello **консольного приложения (.NET Framework)**и новый проект hello имя **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-135">For hello project type, select **Console App (.NET Framework)**, and name hello new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d33f6-136">Если используется кластер HDInsight под управлением Linux, выберите __.NET Framework 4.5__.</span><span class="sxs-lookup"><span data-stu-id="d33f6-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d33f6-137">Дополнительные сведения о совместимости Mono с различными версиями платформы .NET Framework см. в разделе [Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) (Совместимость).</span><span class="sxs-lookup"><span data-stu-id="d33f6-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="d33f6-138">Замените содержимое hello **Program.cs** hello следующее:</span><span class="sxs-lookup"><span data-stu-id="d33f6-138">Replace hello contents of **Program.cs** with hello following:</span></span>

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

3. <span data-ttu-id="d33f6-139">Построение проекта hello.</span><span class="sxs-lookup"><span data-stu-id="d33f6-139">Build hello project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="d33f6-140">Определяемая пользователем функция Pig</span><span class="sxs-lookup"><span data-stu-id="d33f6-140">Pig UDF</span></span>

1. <span data-ttu-id="d33f6-141">Откройте Visual Studio и создайте решение.</span><span class="sxs-lookup"><span data-stu-id="d33f6-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="d33f6-142">Выберите тип проекта hello **консольное приложение**и новый проект hello имя **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-142">For hello project type, select **Console Application**, and name hello new project **PigUDF**.</span></span>

2. <span data-ttu-id="d33f6-143">Замените содержимое hello hello **Program.cs** файл с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="d33f6-143">Replace hello contents of hello **Program.cs** file with hello following code:</span></span>

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

    <span data-ttu-id="d33f6-144">Это приложение выполняет синтаксический анализ строки hello, отправленные из Pig и переформатирование строки, начинающиеся с `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="d33f6-144">This application parses hello lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="d33f6-145">Сохранить **Program.cs**, а затем постройте проект hello.</span><span class="sxs-lookup"><span data-stu-id="d33f6-145">Save **Program.cs**, and then build hello project.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="d33f6-146">Отправить toostorage</span><span class="sxs-lookup"><span data-stu-id="d33f6-146">Upload toostorage</span></span>

1. <span data-ttu-id="d33f6-147">В Visual Studio в откройте **обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="d33f6-148">Разверните пункт **Azure**, а затем — **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="d33f6-149">При появлении запроса введите учетные данные подписки Azure и щелкните **Войти**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="d33f6-150">Разверните кластер HDInsight hello, на котором необходимо toodeploy для данного приложения.</span><span class="sxs-lookup"><span data-stu-id="d33f6-150">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="d33f6-151">Запись с текстом hello __(по умолчанию учетная запись хранилища)__ указан.</span><span class="sxs-lookup"><span data-stu-id="d33f6-151">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Обозреватель сервера, отображающий hello учетной записи хранилища для кластера hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="d33f6-153">Если эта запись могут быть развернуты, вы используете __учетной записи хранилища Azure__ хранения по умолчанию для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="d33f6-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="d33f6-154">файлы tooview hello в хранилище по умолчанию hello hello кластер, разверните запись hello, а затем дважды щелкните hello __(по умолчанию контейнер)__.</span><span class="sxs-lookup"><span data-stu-id="d33f6-154">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="d33f6-155">Если эта запись не могут быть развернуты, вы используете __хранилища Озера данных Azure__ hello хранения по умолчанию для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="d33f6-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="d33f6-156">файлы tooview hello в хранилище по умолчанию hello кластер hello, дважды щелкните hello __(учетной записи хранения по умолчанию)__ входа.</span><span class="sxs-lookup"><span data-stu-id="d33f6-156">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="d33f6-157">файлы .exe tooupload hello, используйте один из следующих методов hello.</span><span class="sxs-lookup"><span data-stu-id="d33f6-157">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="d33f6-158">При использовании __учетной записи хранилища Azure__, щелкните значок передачи hello и найдите toohello **bin\debug** папку для hello **HiveCSharp** проекта.</span><span class="sxs-lookup"><span data-stu-id="d33f6-158">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **HiveCSharp** project.</span></span> <span data-ttu-id="d33f6-159">Наконец, выберите hello **HiveCSharp.exe** файла и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-159">Finally, select hello **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![значок отправки](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="d33f6-161">При использовании __хранилища Озера данных Azure__, щелкните правой кнопкой мыши пустую область в списке файл hello и выберите __отправить__.</span><span class="sxs-lookup"><span data-stu-id="d33f6-161">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="d33f6-162">Наконец, выберите hello **HiveCSharp.exe** файла и нажмите кнопку **откройте**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-162">Finally, select hello **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="d33f6-163">Здравствуйте, один раз __HiveCSharp.exe__ завершения отправки, процесс отправки повторов hello hello __PigUDF.exe__ файла.</span><span class="sxs-lookup"><span data-stu-id="d33f6-163">Once hello __HiveCSharp.exe__ upload has finished, repeat hello upload process for hello __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="d33f6-164">Выполнение запроса Hive</span><span class="sxs-lookup"><span data-stu-id="d33f6-164">Run a Hive query</span></span>

1. <span data-ttu-id="d33f6-165">В Visual Studio в откройте **обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="d33f6-166">Разверните пункт **Azure**, а затем — **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="d33f6-167">Щелкните правой кнопкой мыши кластер hello, развернутым hello **HiveCSharp** приложение, а затем выберите **написать запрос Hive**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-167">Right-click hello cluster that you deployed hello **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="d33f6-168">Используйте следующий текст для запроса Hive hello hello.</span><span class="sxs-lookup"><span data-stu-id="d33f6-168">Use hello following text for hello Hive query:</span></span>

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
    > <span data-ttu-id="d33f6-169">Раскомментируйте hello `add file` инструкции, соответствующий типу hello хранения по умолчанию, используемый для кластера.</span><span class="sxs-lookup"><span data-stu-id="d33f6-169">Uncomment hello `add file` statement that matches hello type of default storage used for your cluster.</span></span>

    <span data-ttu-id="d33f6-170">Этот запрос выбирает hello `clientid`, `devicemake`, и `devicemodel` поля из `hivesampletable`и передает toohello HiveCSharp.exe приложения hello поля.</span><span class="sxs-lookup"><span data-stu-id="d33f6-170">This query selects hello `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes hello fields toohello HiveCSharp.exe application.</span></span> <span data-ttu-id="d33f6-171">Hello запрос ожидает hello приложения tooreturn три поля, которые хранятся в виде `clientid`, `phoneLabel`, и `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="d33f6-171">hello query expects hello application tooreturn three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="d33f6-172">Hello запрос ожидает toofind HiveCSharp.exe в hello корневого контейнера хранилища по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d33f6-172">hello query also expects toofind HiveCSharp.exe in hello root of hello default storage container.</span></span>

5. <span data-ttu-id="d33f6-173">Нажмите кнопку **отправить** toosubmit hello задания toohello HDInsight кластера.</span><span class="sxs-lookup"><span data-stu-id="d33f6-173">Click **Submit** toosubmit hello job toohello HDInsight cluster.</span></span> <span data-ttu-id="d33f6-174">Hello **Hive Сводка заданий** открывается окно.</span><span class="sxs-lookup"><span data-stu-id="d33f6-174">hello **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="d33f6-175">Нажмите кнопку **обновление** toorefresh hello сводки до **состояние задания** изменяет слишком**завершено**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-175">Click **Refresh** toorefresh hello summary until **Job Status** changes too**Completed**.</span></span> <span data-ttu-id="d33f6-176">выходные данные задания tooview hello, нажмите кнопку **выходные данные задания**.</span><span class="sxs-lookup"><span data-stu-id="d33f6-176">tooview hello job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="d33f6-177">Выполнение задания Pig</span><span class="sxs-lookup"><span data-stu-id="d33f6-177">Run a Pig job</span></span>

1. <span data-ttu-id="d33f6-178">Используйте один из hello следующие методы tooconnect tooyour HDInsight кластера.</span><span class="sxs-lookup"><span data-stu-id="d33f6-178">Use one of hello following methods tooconnect tooyour HDInsight cluster:</span></span>

    * <span data-ttu-id="d33f6-179">Если используется кластер HDInsight под управлением __Linux__, примените протокол SSH.</span><span class="sxs-lookup"><span data-stu-id="d33f6-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="d33f6-180">Например, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="d33f6-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="d33f6-181">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d33f6-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="d33f6-182">Если вы используете __под управлением Windows__ кластера HDInsight [кластера toohello подключение с помощью удаленного рабочего стола](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="d33f6-182">If you are using a __Windows-based__ HDInsight cluster, [Connect toohello cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="d33f6-183">Используйте один hello, следующая команда toostart hello Pig командной строки:</span><span class="sxs-lookup"><span data-stu-id="d33f6-183">Use one hello following command toostart hello Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="d33f6-184">При использовании кластера под управлением Windows используйте следующие команды вместо hello:</span><span class="sxs-lookup"><span data-stu-id="d33f6-184">If you are using a Windows-based cluster, use hello following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="d33f6-185">Откроется командная строка `grunt>`.</span><span class="sxs-lookup"><span data-stu-id="d33f6-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="d33f6-186">Введите hello следующие toorun задания Pig, использующий hello приложения .NET Framework:</span><span class="sxs-lookup"><span data-stu-id="d33f6-186">Enter hello following toorun a Pig job that uses hello .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="d33f6-187">Hello `DEFINE` инструкция создает псевдоним `streamer` для hello pigudf.exe приложений и `CACHE` загружает его из хранилища по умолчанию для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="d33f6-187">hello `DEFINE` statement creates an alias of `streamer` for hello pigudf.exe applications, and `CACHE` loads it from default storage for hello cluster.</span></span> <span data-ttu-id="d33f6-188">Позже `streamer` используется с hello `STREAM` tooprocess оператор hello одиночных строк из ЖУРНАЛОВ и данных возвращаемого hello как ряд столбцов.</span><span class="sxs-lookup"><span data-stu-id="d33f6-188">Later, `streamer` is used with hello `STREAM` operator tooprocess hello single lines contained in LOG and return hello data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d33f6-189">Имя приложения Hello, который используется для потоковой передачи должно быть заключено в hello \` (обратный апостроф) символов при псевдонимами, и ' (одинарная кавычка) при использовании с `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="d33f6-189">hello application name that is used for streaming must be surrounded by hello \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="d33f6-190">После ввода последней строкой hello, будет запущено задание hello.</span><span class="sxs-lookup"><span data-stu-id="d33f6-190">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="d33f6-191">Он возвращает выходные данные примерно toohello после текста:</span><span class="sxs-lookup"><span data-stu-id="d33f6-191">It returns output similar toohello following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="d33f6-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d33f6-192">Next steps</span></span>

<span data-ttu-id="d33f6-193">В этом документе вы узнали как toouse приложения .NET Framework из Hive и Pig в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d33f6-193">In this document, you have learned how toouse a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="d33f6-194">При желании в статье toouse Python с Hive и Pig, toolearn [использование Python с Hive и Pig в HDInsight](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="d33f6-194">If you would like toolearn how toouse Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="d33f6-195">Другие способы toouse Pig и Hive и toolearn об использовании MapReduce в разделе hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="d33f6-195">For other ways toouse Pig and Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="d33f6-196">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="d33f6-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d33f6-197">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="d33f6-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d33f6-198">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="d33f6-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
