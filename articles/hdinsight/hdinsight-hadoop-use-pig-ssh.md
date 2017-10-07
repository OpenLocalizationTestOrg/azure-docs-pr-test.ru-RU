---
title: "aaaUse Hadoop Pig с SSH в кластере HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как подключать кластер Hadoop под управлением Linux tooa SSH, и затем использовать hello Pig команды toorun Pig латиница инструкции в интерактивном режиме или в виде пакета задания."
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
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="f06b4-103">Выполнять задания Pig в кластере под управлением Linux с hello команда Pig (SSH)</span><span class="sxs-lookup"><span data-stu-id="f06b4-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="f06b4-104">Узнайте, как toointeractively запуска задания Pig из кластера HDInsight tooyour подключения SSH.</span><span class="sxs-lookup"><span data-stu-id="f06b4-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="f06b4-105">Hello латиница Pig язык программирования позволяет toodescribe преобразования, вывод hello требуемого tooproduce примененных toohello входных данных.</span><span class="sxs-lookup"><span data-stu-id="f06b4-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f06b4-106">Hello в данном пошаговом руководстве требуется кластер HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="f06b4-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="f06b4-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="f06b4-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f06b4-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f06b4-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="f06b4-109"><a id="ssh"></a>Подключение по SSH</span><span class="sxs-lookup"><span data-stu-id="f06b4-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="f06b4-110">Используйте кластер HDInsight tooyour tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="f06b4-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="f06b4-111">Hello следующий пример соединяет tooa кластер с именем **myhdinsight** как hello учетной записи с именем **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="f06b4-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="f06b4-112">**При указании ключа сертификата для проверки подлинности SSH** при создании кластера HDInsight hello, может потребоваться toospecify расположение hello hello закрытого ключа на компьютере клиента.</span><span class="sxs-lookup"><span data-stu-id="f06b4-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="f06b4-113">**Если задан пароль для проверки подлинности SSH** при создании кластера HDInsight hello предоставляют hello пароль при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="f06b4-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="f06b4-114">Дополнительные сведения об использовании протокола SSH с HDInsight см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f06b4-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="f06b4-115"><a id="pig"></a>Команда Pig hello</span><span class="sxs-lookup"><span data-stu-id="f06b4-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="f06b4-116">После установления соединения, запустите hello Pig командной строки (CLI) с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f06b4-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="f06b4-117">Через некоторое время отобразится командная строка `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="f06b4-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="f06b4-118">Введите hello следующей инструкцией:</span><span class="sxs-lookup"><span data-stu-id="f06b4-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="f06b4-119">Эта команда загружает содержимое файла sample.log hello hello в ЖУРНАЛЫ.</span><span class="sxs-lookup"><span data-stu-id="f06b4-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="f06b4-120">Hello содержимое файла hello можно просмотреть с помощью hello следующей инструкцией:</span><span class="sxs-lookup"><span data-stu-id="f06b4-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="f06b4-121">Затем преобразуйте hello данных путем применения регулярное выражение tooextract только hello уровень ведения журнала из каждой записи с помощью hello следующей инструкцией:</span><span class="sxs-lookup"><span data-stu-id="f06b4-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="f06b4-122">Можно использовать **ДАМПА** tooview hello данных после преобразования «hello».</span><span class="sxs-lookup"><span data-stu-id="f06b4-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="f06b4-123">В этом случае используйте `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="f06b4-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="f06b4-124">Продолжить применение преобразований с помощью инструкций hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="f06b4-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="f06b4-125">Инструкция Pig Latin</span><span class="sxs-lookup"><span data-stu-id="f06b4-125">Pig Latin statement</span></span> | <span data-ttu-id="f06b4-126">Какие оператор hello</span><span class="sxs-lookup"><span data-stu-id="f06b4-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="f06b4-127">Удаляет строки, содержащие значение null для уровня ведения журнала hello и сохраняет результаты hello в `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="f06b4-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="f06b4-128">Hello групп строк, уровень ведения журнала и сохраняет результаты hello в `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="f06b4-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="f06b4-129">Создает набор данных, который содержит каждое уникальное значение уровня ведения журнала и количество его вхождений.</span><span class="sxs-lookup"><span data-stu-id="f06b4-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="f06b4-130">Hello набор данных хранится в `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="f06b4-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="f06b4-131">Упорядочивает уровни журнала hello по количеству (по убыванию) и сохраняет в `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="f06b4-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="f06b4-132">Используйте `DUMP` tooview hello результат преобразования hello после каждого шага.</span><span class="sxs-lookup"><span data-stu-id="f06b4-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="f06b4-133">Можно также сохранить результаты hello преобразования с помощью hello `STORE` инструкции.</span><span class="sxs-lookup"><span data-stu-id="f06b4-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="f06b4-134">Например, следующем за инструкцией hello сохраняет hello `RESULT` toohello `/example/data/pigout` на hello хранилища по умолчанию для кластера:</span><span class="sxs-lookup"><span data-stu-id="f06b4-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="f06b4-135">Hello данные хранятся в указанном каталоге hello в файлах с именем `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="f06b4-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="f06b4-136">Если hello каталог уже существует, возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="f06b4-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="f06b4-137">tooexit hello grunt приглашении введите hello следующей инструкцией:</span><span class="sxs-lookup"><span data-stu-id="f06b4-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="f06b4-138">Пакетные файлы Pig Latin</span><span class="sxs-lookup"><span data-stu-id="f06b4-138">Pig Latin batch files</span></span>

<span data-ttu-id="f06b4-139">Также можно использовать hello Pig команда toorun латиница Pig, содержащиеся в файле.</span><span class="sxs-lookup"><span data-stu-id="f06b4-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="f06b4-140">После выхода из строки grunt hello, используйте hello следующая команда toopipe STDIN в файл с именем `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="f06b4-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="f06b4-141">Этот файл создается в корневом каталоге hello для hello учетной записи пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="f06b4-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="f06b4-142">Введите или вставьте следующие строки hello и затем использовать сочетание клавиш Ctrl + D, после завершения.</span><span class="sxs-lookup"><span data-stu-id="f06b4-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="f06b4-143">Используйте hello следующая команда toorun hello `pigbatch.pig` файл с помощью команды Pig hello.</span><span class="sxs-lookup"><span data-stu-id="f06b4-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="f06b4-144">После завершения выполнения пакетного задания hello, вы видите hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="f06b4-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="f06b4-145"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f06b4-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="f06b4-146">Общие сведения о Pig в HDInsight см. следующий документ hello.</span><span class="sxs-lookup"><span data-stu-id="f06b4-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="f06b4-147">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f06b4-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="f06b4-148">Дополнительные сведения о других способах toowork с Hadoop в HDInsight см hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="f06b4-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="f06b4-149">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f06b4-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f06b4-150">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f06b4-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
