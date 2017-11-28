---
title: "Использование Hadoop Pig с помощью REST в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте, как с помощью REST выполнять задания Pig Latin в кластере Hadoop в Azure HDInsight."
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
ms.openlocfilehash: a86864a779b0de1c6d5669cfbba0f3e1a27f1ff1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="77233-103">Выполнение заданий Pig с помощью REST с использованием Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="77233-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="77233-104">Узнайте, как выполнять задания Pig Latin с помощью запросов REST к кластеру Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77233-104">Learn how to run Pig Latin jobs by making REST requests to an Azure HDInsight cluster.</span></span> <span data-ttu-id="77233-105">Curl используется для демонстрации возможностей взаимодействия с HDInsight с помощью REST API WebHCat.</span><span class="sxs-lookup"><span data-stu-id="77233-105">Curl is used to demonstrate how you can interact with HDInsight using the WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="77233-106">Если вы уже знаете, как использовать серверы Hadoop на платформе Linux, но не знакомы с HDInsight, ознакомьтесь со статьей [Советы по использованию HDInsight на платформе Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="77233-106">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="77233-107"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="77233-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="77233-108">Кластер Azure HDInsight (Hadoop в HDInsight) (на платформе Linux или Windows).</span><span class="sxs-lookup"><span data-stu-id="77233-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="77233-109">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="77233-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="77233-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="77233-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="77233-111">Curl</span><span class="sxs-lookup"><span data-stu-id="77233-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="77233-112">jq</span><span class="sxs-lookup"><span data-stu-id="77233-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="77233-113"><a id="curl"></a>Выполнение заданий Pig с помощью Curl</span><span class="sxs-lookup"><span data-stu-id="77233-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="77233-114">REST API защищается с помощью [обычной проверки подлинности](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="77233-114">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="77233-115">Чтобы обеспечить безопасную отправку учетных данных на сервер, запросы всегда следует отправлять с помощью протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="77233-115">Always make requests by using Secure HTTP (HTTPS) to ensure that your credentials are securely sent to the server.</span></span>
>
> <span data-ttu-id="77233-116">При использовании команд, описанных в этом разделе, замените `USERNAME` на имя пользователя для выполнения проверки подлинности в кластере, а `PASSWORD` — на пароль учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="77233-116">When using the commands in this section, replace `USERNAME` with the user to authenticate to the cluster, and replace `PASSWORD` with the password for the user account.</span></span> <span data-ttu-id="77233-117">Замените `CLUSTERNAME` именем кластера.</span><span class="sxs-lookup"><span data-stu-id="77233-117">Replace `CLUSTERNAME` with the name of your cluster.</span></span>
>


1. <span data-ttu-id="77233-118">Используйте следующую команду в командной строке, чтобы проверить возможность подключения к кластеру HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77233-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="77233-119">Вы получите следующий ответ JSON:</span><span class="sxs-lookup"><span data-stu-id="77233-119">You should receive the following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="77233-120">Ниже приведены параметры, используемые в этой команде:</span><span class="sxs-lookup"><span data-stu-id="77233-120">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="77233-121">**-u**— имя пользователя и пароль, используемый для аутентификации запроса.</span><span class="sxs-lookup"><span data-stu-id="77233-121">**-u**: The user name and password used to authenticate the request</span></span>
    * <span data-ttu-id="77233-122">**-G** — указывает, что этот запрос является запросом GET.</span><span class="sxs-lookup"><span data-stu-id="77233-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="77233-123">Начало URL-адреса **https://CLUSTERNAME.azurehdinsight.net/templeton/v1** одинаковое для всех запросов.</span><span class="sxs-lookup"><span data-stu-id="77233-123">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="77233-124">Путь **/status** указывает, что по запросу серверу должно быть возвращено состояние WebHCat (другое название — Templeton).</span><span class="sxs-lookup"><span data-stu-id="77233-124">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span></span>

2. <span data-ttu-id="77233-125">Чтобы отправить задание Pig Latin в кластер, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="77233-125">Use the following code to submit a Pig Latin job to the cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="77233-126">Ниже приведены параметры, используемые в этой команде:</span><span class="sxs-lookup"><span data-stu-id="77233-126">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="77233-127">**-d** — так как `-G` не используется, в запросе по умолчанию используется метод POST.</span><span class="sxs-lookup"><span data-stu-id="77233-127">**-d**: Because `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="77233-128">`-d` задает значения данных, отправляемые в запросе.</span><span class="sxs-lookup"><span data-stu-id="77233-128">`-d` specifies the data values that are sent with the request.</span></span>

    * <span data-ttu-id="77233-129">**user.name**— пользователь, выполняющий команду.</span><span class="sxs-lookup"><span data-stu-id="77233-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="77233-130">**execute**— оператор Pig Latin, который необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="77233-130">**execute**: The Pig Latin statements to execute</span></span>
    * <span data-ttu-id="77233-131">**statusdir** — каталог, в который будет записано состояние этого задания.</span><span class="sxs-lookup"><span data-stu-id="77233-131">**statusdir**: The directory that the status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="77233-132">Обратите внимание, что при использовании Curl пробелы в операторах Pig Latin заменяются знаком `+`.</span><span class="sxs-lookup"><span data-stu-id="77233-132">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span></span>

    <span data-ttu-id="77233-133">Эта команда должна возвращать идентификатор задания, который может использоваться для проверки состояния задания. Пример:</span><span class="sxs-lookup"><span data-stu-id="77233-133">This command should return a job ID that can be used to check the status of the job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="77233-134">Чтобы проверить состояние задания, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="77233-134">To check the status of the job, use the following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="77233-135">Замените `JOBID` значением, возвращенным на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="77233-135">Replace `JOBID` with the value returned in the previous step.</span></span> <span data-ttu-id="77233-136">Например, если возвращено значение `{"id":"job_1415651640909_0026"}`, то `JOBID` равно `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="77233-136">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="77233-137">Если задание завершено, оно будет в состоянии **SUCCEEDED** (Успешно).</span><span class="sxs-lookup"><span data-stu-id="77233-137">If the job has finished, the state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="77233-138">Этот запрос Curl возвращает документ JSON с информацией о задании. При этом jq используется только для получения значения состояния.</span><span class="sxs-lookup"><span data-stu-id="77233-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span></span>

## <span data-ttu-id="77233-139"><a id="results"></a>Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="77233-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="77233-140">Когда состояние задания изменится на **SUCCEEDED**, вы можете получить результаты задания.</span><span class="sxs-lookup"><span data-stu-id="77233-140">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job.</span></span> <span data-ttu-id="77233-141">Параметр `statusdir`, передаваемый с помощью запроса, содержит расположение выходного файла. В данном случае это `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="77233-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="77233-142">В качестве хранилища данных по умолчанию HDInsight может использовать хранилище Azure или Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="77233-142">HDInsight can use either Azure Storage or Azure Data Lake Store as the default data store.</span></span> <span data-ttu-id="77233-143">Существуют различные способы получения данных в зависимости от их используемого типа.</span><span class="sxs-lookup"><span data-stu-id="77233-143">There are various ways to get at the data depending on which one you use.</span></span> <span data-ttu-id="77233-144">Дополнительные сведения см. в разделе о хранилище в документе [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) (Сведения о HDInsight на базе Linux).</span><span class="sxs-lookup"><span data-stu-id="77233-144">For more information, see the storage section of the [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="77233-145"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="77233-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="77233-146">Как показано в этом документе, для запуска, мониторинга и просмотра результатов выполнения заданий Pig в кластере HDInsight можно использовать необработанные HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="77233-146">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="77233-147">Дополнительные сведения об интерфейсе REST, используемом в этой статье, см. в [справочнике по WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="77233-147">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="77233-148"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="77233-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="77233-149">Общая информация о Pig в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77233-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="77233-150">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="77233-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="77233-151">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77233-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="77233-152">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="77233-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="77233-153">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="77233-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
