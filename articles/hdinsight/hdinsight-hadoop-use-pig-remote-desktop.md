---
title: "aaaUse Pig для Hadoop с помощью удаленного рабочего стола в HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как toouse hello инструкций латиница Pig toorun Pig команд из кластера под управлением Windows Hadoop tooa подключения удаленного рабочего стола в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="801fb-103">Выполнение заданий Pig через подключение к удаленному рабочему столу</span><span class="sxs-lookup"><span data-stu-id="801fb-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="801fb-104">Этот документ содержит пошаговое руководство по использованию инструкций hello Pig команд toorun латиница Pig с кластера HDInsight под управлением Windows tooa подключения удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="801fb-104">This document provides a walkthrough for using hello Pig command toorun Pig Latin statements from a Remote Desktop connection tooa Windows-based HDInsight cluster.</span></span> <span data-ttu-id="801fb-105">Латинская pig позволяет приложениям toocreate MapReduce, описав преобразования данных, вместо сопоставления и уменьшения функции.</span><span class="sxs-lookup"><span data-stu-id="801fb-105">Pig Latin allows you toocreate MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="801fb-106">Удаленный рабочий стол доступен только в кластерах HDInsight, использование в качестве hello операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="801fb-106">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="801fb-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="801fb-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="801fb-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="801fb-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="801fb-109">Для HDInsight 3.4 или выше в разделе [использование Pig с HDInsight и SSH](hdinsight-hadoop-use-pig-ssh.md) сведения о запуске Pig интерактивного задания непосредственно на hello кластера из командной строки.</span><span class="sxs-lookup"><span data-stu-id="801fb-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="801fb-110"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="801fb-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="801fb-111">в этой статье инструкциям toocomplete hello, необходимо будет ниже hello.</span><span class="sxs-lookup"><span data-stu-id="801fb-111">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="801fb-112">Кластер HDInsight на платформе Windows (Hadoop в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="801fb-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="801fb-113">Клиентский компьютер под управлением Windows 10, Windows 8 или Windows 7.</span><span class="sxs-lookup"><span data-stu-id="801fb-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="801fb-114"><a id="connect"></a>Подключение к удаленному рабочему столу</span><span class="sxs-lookup"><span data-stu-id="801fb-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="801fb-115">Включить удаленный рабочий стол для кластера HDInsight hello, а затем соедините tooit в соответствии с инструкциями hello в [tooHDInsight кластерами, с помощью протокола удаленного рабочего СТОЛА подключиться](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="801fb-115">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="801fb-116"><a id="pig"></a>Команда Pig hello</span><span class="sxs-lookup"><span data-stu-id="801fb-116"><a id="pig"></a>Use hello Pig command</span></span>
1. <span data-ttu-id="801fb-117">После подключения удаленного рабочего стола, запустите hello **командной строки Hadoop** с помощью hello значка на рабочем столе hello.</span><span class="sxs-lookup"><span data-stu-id="801fb-117">After you have a Remote Desktop connection, start hello **Hadoop Command Line** by using hello icon on hello desktop.</span></span>
2. <span data-ttu-id="801fb-118">Используйте следующую команду Pig toostart hello hello.</span><span class="sxs-lookup"><span data-stu-id="801fb-118">Use hello following toostart hello Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="801fb-119">Откроется командная строка `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="801fb-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="801fb-120">Введите hello следующей инструкцией:</span><span class="sxs-lookup"><span data-stu-id="801fb-120">Enter hello following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="801fb-121">Эта команда загружает содержимое файла sample.log hello hello в файл ЖУРНАЛЫ hello.</span><span class="sxs-lookup"><span data-stu-id="801fb-121">This command loads hello contents of hello sample.log file into hello LOGS file.</span></span> <span data-ttu-id="801fb-122">Можно просмотреть содержимое hello hello файла с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="801fb-122">You can view hello contents of hello file by using hello following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="801fb-123">Преобразования данных hello, применяя регулярное выражение tooextract только hello уровень ведения журнала из каждой записи:</span><span class="sxs-lookup"><span data-stu-id="801fb-123">Transform hello data by applying a regular expression tooextract only hello logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="801fb-124">Можно использовать **ДАМПА** tooview hello данных после преобразования «hello».</span><span class="sxs-lookup"><span data-stu-id="801fb-124">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="801fb-125">В этом случае — `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="801fb-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="801fb-126">Продолжайте применение преобразований с помощью hello, следующие инструкции.</span><span class="sxs-lookup"><span data-stu-id="801fb-126">Continue applying transformations by using hello following statements.</span></span> <span data-ttu-id="801fb-127">Используйте `DUMP` tooview hello результат преобразования hello после каждого шага.</span><span class="sxs-lookup"><span data-stu-id="801fb-127">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="801fb-128">Инструкция</span><span class="sxs-lookup"><span data-stu-id="801fb-128">Statement</span></span></th><th><span data-ttu-id="801fb-129">Действие</span><span class="sxs-lookup"><span data-stu-id="801fb-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="801fb-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="801fb-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="801fb-131">Удаляет строки, содержащие значение null для уровня ведения журнала hello и сохраняет результаты hello в FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="801fb-131">Removes rows that contain a null value for hello log level and stores hello results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="801fb-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="801fb-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="801fb-133">Hello групп строк, уровень ведения журнала и сохраняет результаты hello в GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="801fb-133">Groups hello rows by log level and stores hello results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="801fb-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="801fb-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="801fb-135">Создает новый набор данных, который содержит каждое уникальное значение уровня ведения журнала и количество его вхождений.</span><span class="sxs-lookup"><span data-stu-id="801fb-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="801fb-136">Он сохраняется в FREQUENCIES.</span><span class="sxs-lookup"><span data-stu-id="801fb-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="801fb-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="801fb-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="801fb-138">Упорядочивает уровни журнала hello, count (по убыванию) и сохраняет в РЕЗУЛЬТАТ</span><span class="sxs-lookup"><span data-stu-id="801fb-138">Orders hello log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="801fb-139">
6.Можно также сохранить результаты hello преобразования с помощью hello `STORE` инструкции.</span><span class="sxs-lookup"><span data-stu-id="801fb-139">
6. You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="801fb-140">Например, следующая команда hello сохраняет hello `RESULT` toohello **/example/data/pigout** каталог в контейнере хранилища по умолчанию hello для кластера:</span><span class="sxs-lookup"><span data-stu-id="801fb-140">For example, hello following command saves hello `RESULT` toohello **/example/data/pigout** directory in hello default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="801fb-141">Hello данные хранятся в указанном каталоге hello в файлах с именем **nnnnn часть**.</span><span class="sxs-lookup"><span data-stu-id="801fb-141">hello data is stored in hello specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="801fb-142">Если hello каталог уже существует, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="801fb-142">If hello directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="801fb-143">tooexit hello grunt приглашении введите hello, следующем за инструкцией.</span><span class="sxs-lookup"><span data-stu-id="801fb-143">tooexit hello grunt prompt, enter hello following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="801fb-144">Пакетные файлы Pig Latin</span><span class="sxs-lookup"><span data-stu-id="801fb-144">Pig Latin batch files</span></span>
<span data-ttu-id="801fb-145">Также можно использовать hello Pig команда toorun латиница Pig, содержащийся в файле.</span><span class="sxs-lookup"><span data-stu-id="801fb-145">You can also use hello Pig command toorun Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="801fb-146">После выхода из строки grunt hello, откройте **Блокнот** и создайте новый файл с именем **pigbatch.pig** в hello **% PIG_HOME %** каталога.</span><span class="sxs-lookup"><span data-stu-id="801fb-146">After exiting hello grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in hello **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="801fb-147">Тип или вставить hello следующие строки в hello **pigbatch.pig** файл и сохраните его:</span><span class="sxs-lookup"><span data-stu-id="801fb-147">Type or paste hello following lines into hello **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="801fb-148">Используйте hello, следуя toorun hello **pigbatch.pig** файла с помощью команды pig hello.</span><span class="sxs-lookup"><span data-stu-id="801fb-148">Use hello following toorun hello **pigbatch.pig** file using hello pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="801fb-149">После завершения пакетного задания hello, вы увидите hello после выходных данных, который должен быть hello же, как при использовании `DUMP RESULT;` в предыдущих шагах hello:</span><span class="sxs-lookup"><span data-stu-id="801fb-149">When hello batch job completes, you should see hello following output, which should be hello same as when you used `DUMP RESULT;` in hello previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="801fb-150"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="801fb-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="801fb-151">Как видите, hello Pig команда позволяет toointeractively выполнения операций MapReduce или выполнение заданий латиница Pig, которые хранятся в пакетном файле.</span><span class="sxs-lookup"><span data-stu-id="801fb-151">As you can see, hello Pig command allows you toointeractively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="801fb-152"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="801fb-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="801fb-153">Общая информация о Pig в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="801fb-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="801fb-154">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="801fb-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="801fb-155">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="801fb-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="801fb-156">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="801fb-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="801fb-157">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="801fb-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
