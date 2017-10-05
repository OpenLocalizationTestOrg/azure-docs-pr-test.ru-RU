---
title: "Использование Hadoop Pig с SSH в кластере HDInsight — Azure | Документы Майкрософт"
description: "Узнайте, как подключиться к кластеру Hadoop под управлением Linux с помощью SSH, а затем использовать команду Pig для выполнения операторов Pig Latin в интерактивном режиме или в виде пакетного задания."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e4c893ef4bfa573dd9fbc9c9b0ae296720769842
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a><span data-ttu-id="a8a69-103">Выполнение заданий Pig в кластере под управлением Linux с помощью команды Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="a8a69-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="a8a69-104">Узнайте, как в интерактивном режиме выполнять задания Pig с помощью SSH-подключения к кластеру HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8a69-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span></span> <span data-ttu-id="a8a69-105">Язык программирования Pig Latin позволяет описывать преобразования, применяемые к входным данным для получения требуемых выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a8a69-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8a69-106">Для выполнения действий, описанных в этом документе, необходим кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="a8a69-106">The steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a8a69-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a8a69-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a8a69-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a8a69-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="a8a69-109"><a id="ssh"></a>Подключение по SSH</span><span class="sxs-lookup"><span data-stu-id="a8a69-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="a8a69-110">Подключитесь к кластеру HDInsight с помощью протокола SSH.</span><span class="sxs-lookup"><span data-stu-id="a8a69-110">Use SSH to connect to your HDInsight cluster.</span></span> <span data-ttu-id="a8a69-111">Следующий пример подключается к кластеру **myhdinsight** с учетной записью **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="a8a69-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="a8a69-112">**Если указан ключ сертификата для аутентификации SSH** , возможно, при создании кластера HDInsight потребуется указать расположение закрытого ключа в клиентской системе.</span><span class="sxs-lookup"><span data-stu-id="a8a69-112">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="a8a69-113">Если при создании кластера HDInsight **для аутентификации SSH был задан пароль**, введите его при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="a8a69-113">**If you provided a password for SSH authentication** when you created the HDInsight cluster, provide the password when prompted.</span></span>

<span data-ttu-id="a8a69-114">Дополнительные сведения об использовании протокола SSH с HDInsight см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a8a69-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="a8a69-115"><a id="pig"></a>Использование команды Pig</span><span class="sxs-lookup"><span data-stu-id="a8a69-115"><a id="pig"></a>Use the Pig command</span></span>

1. <span data-ttu-id="a8a69-116">После установления подключения запустите интерфейс командной строки Pig с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="a8a69-116">Once connected, start the Pig command-line interface (CLI) by using the following command:</span></span>

        pig

    <span data-ttu-id="a8a69-117">Через некоторое время отобразится командная строка `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="a8a69-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="a8a69-118">Введите следующий оператор:</span><span class="sxs-lookup"><span data-stu-id="a8a69-118">Enter the following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="a8a69-119">Эта команда загружает содержимое файла sample.log в LOGS.</span><span class="sxs-lookup"><span data-stu-id="a8a69-119">This command loads the contents of the sample.log file into LOGS.</span></span> <span data-ttu-id="a8a69-120">Вы можете просмотреть содержимое файла с помощью следующей инструкции.</span><span class="sxs-lookup"><span data-stu-id="a8a69-120">You can view the contents of the file by using the following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="a8a69-121">Затем преобразуйте данные приведенной ниже инструкцией, применив регулярное выражение для извлечения из каждой записи только информации об уровне ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="a8a69-121">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="a8a69-122">Вы можете использовать **DUMP** , чтобы просмотреть данные после преобразования.</span><span class="sxs-lookup"><span data-stu-id="a8a69-122">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="a8a69-123">В этом случае используйте `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="a8a69-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="a8a69-124">Продолжайте применение преобразований с помощью приведенных инструкций в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="a8a69-124">Continue applying transformations by using the statements in the following table:</span></span>

    | <span data-ttu-id="a8a69-125">Инструкция Pig Latin</span><span class="sxs-lookup"><span data-stu-id="a8a69-125">Pig Latin statement</span></span> | <span data-ttu-id="a8a69-126">Функция инструкции</span><span class="sxs-lookup"><span data-stu-id="a8a69-126">What the statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="a8a69-127">Удаляет строки, содержащие значение NULL для уровня ведения журнала, и сохраняет результаты в `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="a8a69-127">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="a8a69-128">Группирует строки по уровню ведения журнала и сохраняет результаты в `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="a8a69-128">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="a8a69-129">Создает набор данных, который содержит каждое уникальное значение уровня ведения журнала и количество его вхождений.</span><span class="sxs-lookup"><span data-stu-id="a8a69-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="a8a69-130">Набор данных сохраняется в `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="a8a69-130">The data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="a8a69-131">Упорядочивает уровни ведения журнала по количеству (по убыванию) и сохраняет данные в `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="a8a69-131">Orders the log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="a8a69-132">Используйте `DUMP` для просмотра результатов преобразования после каждого шага.</span><span class="sxs-lookup"><span data-stu-id="a8a69-132">Use `DUMP` to view the result of the transformation after each step.</span></span>

5. <span data-ttu-id="a8a69-133">Можно также сохранить результаты преобразования с помощью оператора `STORE` .</span><span class="sxs-lookup"><span data-stu-id="a8a69-133">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="a8a69-134">Например, следующая инструкция сохраняет `RESULT` в каталог `/example/data/pigout` в используемом по умолчанию хранилище для кластера.</span><span class="sxs-lookup"><span data-stu-id="a8a69-134">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="a8a69-135">Данные хранятся в указанном каталоге в файлах с именем `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="a8a69-135">The data is stored in the specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="a8a69-136">Если каталог уже существует, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="a8a69-136">If the directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="a8a69-137">Чтобы выйти из командной строки grunt, введите следующую инструкцию.</span><span class="sxs-lookup"><span data-stu-id="a8a69-137">To exit the grunt prompt, enter the following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="a8a69-138">Пакетные файлы Pig Latin</span><span class="sxs-lookup"><span data-stu-id="a8a69-138">Pig Latin batch files</span></span>

<span data-ttu-id="a8a69-139">Вы также можете использовать команду Pig для выполнения кода Pig Latin, содержащегося в файле.</span><span class="sxs-lookup"><span data-stu-id="a8a69-139">You can also use the Pig command to run Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="a8a69-140">После выхода из командной строки grunt используйте следующую команду, чтобы направить канал STDIN в файл `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="a8a69-140">After exiting the grunt prompt, use the following command to pipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="a8a69-141">Этот файл создан в корневом каталоге учетной записи пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="a8a69-141">This file is created in the home directory for the SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="a8a69-142">Введите или вставьте следующие строки, а когда все будет готово, используйте клавиши CTRL+D.</span><span class="sxs-lookup"><span data-stu-id="a8a69-142">Type or paste the following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="a8a69-143">Используйте следующую команду, чтобы запустить файл `pigbatch.pig` с помощью команды Pig.</span><span class="sxs-lookup"><span data-stu-id="a8a69-143">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="a8a69-144">После завершения пакетного задания можно увидеть результаты следующего вида.</span><span class="sxs-lookup"><span data-stu-id="a8a69-144">Once the batch job finishes, you see the following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="a8a69-145"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8a69-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="a8a69-146">Дополнительные общие сведения об использовании Pig в HDInsight см. в следующем документе:</span><span class="sxs-lookup"><span data-stu-id="a8a69-146">For general information on Pig in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="a8a69-147">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8a69-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="a8a69-148">Дополнительные сведения о способах работы с Hadoop в HDInsight см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="a8a69-148">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="a8a69-149">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8a69-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a8a69-150">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8a69-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
