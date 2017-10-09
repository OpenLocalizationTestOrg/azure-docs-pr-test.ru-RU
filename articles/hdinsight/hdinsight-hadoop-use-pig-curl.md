---
title: "aaaUse Hadoop Pig с REST в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как кластер задания toouse REST toorun латиница Pig в Hadoop в Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="42c42-103">Выполнение заданий Pig с помощью REST с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="42c42-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="42c42-104">Узнайте, как toorun Pig латиница заданий, делая кластера Azure HDInsight tooan запросов REST.</span><span class="sxs-lookup"><span data-stu-id="42c42-104">Learn how toorun Pig Latin jobs by making REST requests tooan Azure HDInsight cluster.</span></span> <span data-ttu-id="42c42-105">Перелистывание — используется toodemonstrate взаимодействие с HDInsight с помощью API-интерфейса REST WebHCat hello.</span><span class="sxs-lookup"><span data-stu-id="42c42-105">Curl is used toodemonstrate how you can interact with HDInsight using hello WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="42c42-106">Если вы уже знакомы с использованием серверов под управлением Linux Hadoop, но являются новый tooHDInsight, см. раздел [советы HDInsight под управлением Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="42c42-106">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="42c42-107"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="42c42-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="42c42-108">Кластер Azure HDInsight (Hadoop в HDInsight) (на платформе Linux или Windows).</span><span class="sxs-lookup"><span data-stu-id="42c42-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="42c42-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="42c42-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="42c42-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="42c42-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="42c42-111">Curl</span><span class="sxs-lookup"><span data-stu-id="42c42-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="42c42-112">jq</span><span class="sxs-lookup"><span data-stu-id="42c42-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="42c42-113"><a id="curl"></a>Выполнение заданий Pig с помощью Curl</span><span class="sxs-lookup"><span data-stu-id="42c42-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="42c42-114">Hello API-интерфейса REST является защищен с помощью [базовая проверка подлинности доступа](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="42c42-114">hello REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="42c42-115">Всегда выполнять запросы, используя свои учетные данные безопасно отправляются серверу toohello tooensure безопасного HTTP (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="42c42-115">Always make requests by using Secure HTTP (HTTPS) tooensure that your credentials are securely sent toohello server.</span></span>
>
> <span data-ttu-id="42c42-116">При использовании команд hello в этом разделе, замените `USERNAME` tooauthenticate toohello hello пользователя кластера и заменить `PASSWORD` hello пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="42c42-116">When using hello commands in this section, replace `USERNAME` with hello user tooauthenticate toohello cluster, and replace `PASSWORD` with hello password for hello user account.</span></span> <span data-ttu-id="42c42-117">Замените `CLUSTERNAME` с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="42c42-117">Replace `CLUSTERNAME` with hello name of your cluster.</span></span>
>


1. <span data-ttu-id="42c42-118">Из командной строки используйте следующие команды tooverify, возможность подключения кластера HDInsight tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="42c42-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="42c42-119">Должно появиться после ответа JSON hello.</span><span class="sxs-lookup"><span data-stu-id="42c42-119">You should receive hello following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="42c42-120">Ниже приведены параметры Hello, использованный в этой команде.</span><span class="sxs-lookup"><span data-stu-id="42c42-120">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="42c42-121">**-u**: hello имя пользователя и пароль используются tooauthenticate hello запроса</span><span class="sxs-lookup"><span data-stu-id="42c42-121">**-u**: hello user name and password used tooauthenticate hello request</span></span>
    * <span data-ttu-id="42c42-122">**-G** — указывает, что этот запрос является запросом GET.</span><span class="sxs-lookup"><span data-stu-id="42c42-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="42c42-123">Здравствуйте, начало hello URL-адрес, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello одинаково для всех запросов.</span><span class="sxs-lookup"><span data-stu-id="42c42-123">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="42c42-124">путь Hello **параметр/Status**, указывает, этот запрос hello состояние hello tooreturn WebHCat (также известный как Templeton) для сервера hello.</span><span class="sxs-lookup"><span data-stu-id="42c42-124">hello path, **/status**, indicates that hello request is tooreturn hello status of WebHCat (also known as Templeton) for hello server.</span></span>

2. <span data-ttu-id="42c42-125">Используйте следующий код toosubmit кластера toohello задания Pig латиница hello.</span><span class="sxs-lookup"><span data-stu-id="42c42-125">Use hello following code toosubmit a Pig Latin job toohello cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="42c42-126">Ниже приведены параметры Hello, использованный в этой команде.</span><span class="sxs-lookup"><span data-stu-id="42c42-126">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="42c42-127">**-d**: поскольку `-G` не используется, hello запроса по умолчанию используется метод POST toohello.</span><span class="sxs-lookup"><span data-stu-id="42c42-127">**-d**: Because `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="42c42-128">`-d`Указывает hello значения данных, отправляемых с запросом hello.</span><span class="sxs-lookup"><span data-stu-id="42c42-128">`-d` specifies hello data values that are sent with hello request.</span></span>

    * <span data-ttu-id="42c42-129">**User.Name**: hello пользователь, выполняющий команду hello</span><span class="sxs-lookup"><span data-stu-id="42c42-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="42c42-130">**выполнение**: hello tooexecute инструкций Латинская Pig</span><span class="sxs-lookup"><span data-stu-id="42c42-130">**execute**: hello Pig Latin statements tooexecute</span></span>
    * <span data-ttu-id="42c42-131">**statusdir**: hello, hello состояния для этого задания является записи в каталог</span><span class="sxs-lookup"><span data-stu-id="42c42-131">**statusdir**: hello directory that hello status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="42c42-132">Обратите внимание, что пробелы hello в инструкциях латиница Pig заменяются hello `+` символов при использовании с Curl.</span><span class="sxs-lookup"><span data-stu-id="42c42-132">Notice that hello spaces in Pig Latin statements are replaced by hello `+` character when used with Curl.</span></span>

    <span data-ttu-id="42c42-133">Эта команда должна возвращать идентификатора задания, который может быть используется toocheck hello состояние задания hello, например:</span><span class="sxs-lookup"><span data-stu-id="42c42-133">This command should return a job ID that can be used toocheck hello status of hello job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="42c42-134">состояние hello toocheck задания hello, hello используйте следующую команду</span><span class="sxs-lookup"><span data-stu-id="42c42-134">toocheck hello status of hello job, use hello following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="42c42-135">Замените `JOBID` с hello значение, возвращенное в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="42c42-135">Replace `JOBID` with hello value returned in hello previous step.</span></span> <span data-ttu-id="42c42-136">Например, если hello, возвращают значение было `{"id":"job_1415651640909_0026"}`, затем `JOBID` — `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="42c42-136">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="42c42-137">Если задание hello завершена, он имеет состояние hello **успешно**.</span><span class="sxs-lookup"><span data-stu-id="42c42-137">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="42c42-138">Этот запрос перелистывание возвращает документ JavaScript Object Notation (JSON) с сведения о задании hello и jq tooretrieve используется только hello значение состояния.</span><span class="sxs-lookup"><span data-stu-id="42c42-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job, and jq is used tooretrieve only hello state value.</span></span>

## <span data-ttu-id="42c42-139"><a id="results"></a>Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="42c42-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="42c42-140">При изменении состояния hello hello задания слишком**успешно**, можно получить результаты задания hello hello.</span><span class="sxs-lookup"><span data-stu-id="42c42-140">When hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job.</span></span> <span data-ttu-id="42c42-141">Hello `statusdir` параметр, передаваемый с запросом hello содержит расположение hello hello выходного файла; в данном случае `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="42c42-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="42c42-142">HDInsight можно использовать в качестве хранилища данных по умолчанию hello хранилища Azure или хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="42c42-142">HDInsight can use either Azure Storage or Azure Data Lake Store as hello default data store.</span></span> <span data-ttu-id="42c42-143">Существуют различные способы tooget hello данных, в зависимости от того, какой из них использовать.</span><span class="sxs-lookup"><span data-stu-id="42c42-143">There are various ways tooget at hello data depending on which one you use.</span></span> <span data-ttu-id="42c42-144">Дополнительные сведения см. раздел хранилища hello hello [HDInsight под управлением Linux сведения](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) документа.</span><span class="sxs-lookup"><span data-stu-id="42c42-144">For more information, see hello storage section of hello [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="42c42-145"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="42c42-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="42c42-146">Как показано в этом документе, можно использовать необработанные toorun запроса HTTP, монитор и просмотреть результаты hello задания Pig в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="42c42-146">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="42c42-147">Дополнительные сведения о hello интерфейс REST, используемые в этой статье в разделе hello [WebHCat ссылка](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="42c42-147">For more information about hello REST interface used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="42c42-148"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="42c42-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="42c42-149">Общая информация о Pig в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="42c42-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="42c42-150">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="42c42-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="42c42-151">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="42c42-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="42c42-152">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="42c42-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="42c42-153">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="42c42-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
