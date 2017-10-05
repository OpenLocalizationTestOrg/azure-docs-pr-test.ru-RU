---
title: "Использование Hadoop Pig и удаленного рабочего стола в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте, использовать команду Pig для выполнения операторов Pig Latin через подключение к удаленному рабочему столу, установленное с кластером Hadoop под управлением Windows в HDInsight."
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
ms.openlocfilehash: 5e8d4fbd8afc54c8bbc1a9a71c66d7022a7d5986
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="4f081-103">Выполнение заданий Pig через подключение к удаленному рабочему столу</span><span class="sxs-lookup"><span data-stu-id="4f081-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="4f081-104">Этот документ содержит пошаговое руководство по использованию команды Pig для выполнения операторов Pig Latin через подключение к удаленному рабочему столу, установленное с кластером HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="4f081-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="4f081-105">Pig Latin позволяет создавать приложения MapReduce, описывая преобразования данных, а не функции сопоставления и приведения.</span><span class="sxs-lookup"><span data-stu-id="4f081-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f081-106">Удаленный рабочий стол доступен только в кластерах HDInsight под управлением операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="4f081-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="4f081-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="4f081-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4f081-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4f081-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="4f081-109">При использовании HDInsight 3.4 или более поздней версии см. сведения о выполнении интерактивных заданий Pig непосредственно в кластере из командной строки: [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) (Использование Pig в HDInsight с помощью SSH).</span><span class="sxs-lookup"><span data-stu-id="4f081-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="4f081-110"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4f081-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="4f081-111">Чтобы выполнить действия, описанные в этой статье, необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="4f081-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="4f081-112">Кластер HDInsight на платформе Windows (Hadoop в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="4f081-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="4f081-113">Клиентский компьютер под управлением Windows 10, Windows 8 или Windows 7.</span><span class="sxs-lookup"><span data-stu-id="4f081-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="4f081-114"><a id="connect"></a>Подключение к удаленному рабочему столу</span><span class="sxs-lookup"><span data-stu-id="4f081-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="4f081-115">Запустите протокол удаленного рабочего стола для кластера HDInsight, а затем выполните подключение, следуя инструкциям раздела [Подключение к кластерам HDInsight с использованием RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="4f081-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="4f081-116"><a id="pig"></a>Использование команды Pig</span><span class="sxs-lookup"><span data-stu-id="4f081-116"><a id="pig"></a>Use the Pig command</span></span>
1. <span data-ttu-id="4f081-117">Установив подключение к удаленному рабочему столу, запустите **командную строку Hadoop** с помощью значка на рабочем столе.</span><span class="sxs-lookup"><span data-stu-id="4f081-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="4f081-118">Для выполнения команды Pig используйте следующее:</span><span class="sxs-lookup"><span data-stu-id="4f081-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="4f081-119">Откроется командная строка `grunt>` .</span><span class="sxs-lookup"><span data-stu-id="4f081-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="4f081-120">Введите следующий оператор:</span><span class="sxs-lookup"><span data-stu-id="4f081-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="4f081-121">Эта команда загружает содержимое файла sample.log в файл LOGS.</span><span class="sxs-lookup"><span data-stu-id="4f081-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="4f081-122">Вы можете просмотреть содержимое файла с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="4f081-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="4f081-123">Преобразуйте данные, применив регулярное выражение для извлечения из каждой записи только информации об уровне ведения журнала:</span><span class="sxs-lookup"><span data-stu-id="4f081-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="4f081-124">Вы можете использовать **DUMP** , чтобы просмотреть данные после преобразования.</span><span class="sxs-lookup"><span data-stu-id="4f081-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="4f081-125">В этом случае — `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="4f081-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="4f081-126">Продолжайте применение преобразований с помощью следующих инструкций.</span><span class="sxs-lookup"><span data-stu-id="4f081-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="4f081-127">Используйте `DUMP` для просмотра результатов преобразования после каждого шага.</span><span class="sxs-lookup"><span data-stu-id="4f081-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="4f081-128">Инструкция</span><span class="sxs-lookup"><span data-stu-id="4f081-128">Statement</span></span></th><th><span data-ttu-id="4f081-129">Действие</span><span class="sxs-lookup"><span data-stu-id="4f081-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="4f081-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="4f081-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="4f081-131">Удаляет строки, содержащие значение NULL для уровня ведения журнала и сохраняет результаты в FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="4f081-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="4f081-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="4f081-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="4f081-133">Группирует строки по уровню ведения журнала и сохраняет результаты в GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="4f081-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="4f081-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="4f081-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="4f081-135">Создает новый набор данных, который содержит каждое уникальное значение уровня ведения журнала и количество его вхождений.</span><span class="sxs-lookup"><span data-stu-id="4f081-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="4f081-136">Он сохраняется в FREQUENCIES.</span><span class="sxs-lookup"><span data-stu-id="4f081-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="4f081-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="4f081-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="4f081-138">Упорядочивает уровни ведения журнала по количеству (по убыванию) и сохраняет данные в RESULT.</span><span class="sxs-lookup"><span data-stu-id="4f081-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="4f081-139">
6. Можно также сохранить результаты преобразования с помощью оператора `STORE`.</span><span class="sxs-lookup"><span data-stu-id="4f081-139">
6. You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="4f081-140">Например, следующий оператор сохраняет `RESULT` в каталог **/example/data/pigout** в используемом по умолчанию контейнере хранилища для кластера:</span><span class="sxs-lookup"><span data-stu-id="4f081-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="4f081-141">Данные хранятся в указанном каталоге в файлах с именем **part-№№№№№**.</span><span class="sxs-lookup"><span data-stu-id="4f081-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="4f081-142">Если каталог уже существует, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4f081-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="4f081-143">Чтобы выйти из командной строки grunt, введите следующий оператор.</span><span class="sxs-lookup"><span data-stu-id="4f081-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="4f081-144">Пакетные файлы Pig Latin</span><span class="sxs-lookup"><span data-stu-id="4f081-144">Pig Latin batch files</span></span>
<span data-ttu-id="4f081-145">Вы также можете использовать команду Pig для выполнения кода Pig Latin, содержащегося в файле.</span><span class="sxs-lookup"><span data-stu-id="4f081-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="4f081-146">После выхода из командной строки grunt откройте **Блокнот** и создайте новый файл с именем **pigbatch.pig** в каталоге **%PIG_HOME%**.</span><span class="sxs-lookup"><span data-stu-id="4f081-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="4f081-147">Введите или вставьте следующие строки в файл **pigbatch.pig** , а затем сохраните его:</span><span class="sxs-lookup"><span data-stu-id="4f081-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="4f081-148">Используйте следующую команду, чтобы запустить файл **pigbatch.pig** с помощью команды Pig.</span><span class="sxs-lookup"><span data-stu-id="4f081-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="4f081-149">После завершения пакетного задания вы должны увидеть следующий результат, который должен быть таким же, как при использовании `DUMP RESULT;` в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="4f081-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="4f081-150"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="4f081-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="4f081-151">Как вы видите, команда Pig позволяет интерактивно выполнять операции MapReduce или задания Pig Latin, хранимые в пакетном файле.</span><span class="sxs-lookup"><span data-stu-id="4f081-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="4f081-152"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f081-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="4f081-153">Общая информация о Pig в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4f081-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="4f081-154">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f081-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="4f081-155">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4f081-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="4f081-156">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f081-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4f081-157">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f081-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
