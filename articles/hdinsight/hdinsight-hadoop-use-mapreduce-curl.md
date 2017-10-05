---
title: "Использование MapReduce и Curl с Hadoop в HDInsight — Azure | Документы Майкрософт"
description: "Информация об удаленном выполнении заданий MapReduce с помощью Curl с использованием Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8238bb829df95dcb8c99c0b7fff53c627a56f47c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="28d2b-103">Выполнение заданий MapReduce с помощью REST в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="28d2b-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="28d2b-104">Узнайте, как с помощью REST API WebHCat выполнять задания MapReduce в Hadoop в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28d2b-104">Learn how to use the WebHCat REST API to run MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="28d2b-105">Curl используется для демонстрации возможностей взаимодействия с HDInsight с помощью необработанных HTTP-запросов для выполнения заданий MapReduce, их мониторинга и получения их результатов.</span><span class="sxs-lookup"><span data-stu-id="28d2b-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="28d2b-106">Если вы уже знакомы с использованием серверов Hadoop на платформе Linux, но не знакомы с HDInsight, ознакомьтесь с документом [Сведения об использовании HDInsight в Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="28d2b-106">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see the [What you need to know about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="28d2b-107"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="28d2b-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="28d2b-108">Hadoop в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28d2b-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="28d2b-109">Curl</span><span class="sxs-lookup"><span data-stu-id="28d2b-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="28d2b-110">jq</span><span class="sxs-lookup"><span data-stu-id="28d2b-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="28d2b-111"><a id="curl"></a>Выполнение заданий MapReduce с помощью Curl</span><span class="sxs-lookup"><span data-stu-id="28d2b-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="28d2b-112">При использовании Curl или любых других средств связи REST с WebHCat нужно проводить аутентификацию запросов с помощью пароля и имени пользователя администратора кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28d2b-112">When you use Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="28d2b-113">Имя кластера необходимо использовать в составе универсального кода ресурса (URI), используемого для отправки запросов на сервер.</span><span class="sxs-lookup"><span data-stu-id="28d2b-113">You must use the cluster name as part of the URI that is used to send the requests to the server.</span></span>
>
> <span data-ttu-id="28d2b-114">В командах, описанных в этом разделе, **USERNAME** нужно заменить именем пользователя для аутентификации в кластере, а **PASSWORD** — паролем учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="28d2b-114">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="28d2b-115">Замените **CLUSTERNAME** именем кластера.</span><span class="sxs-lookup"><span data-stu-id="28d2b-115">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="28d2b-116">API-интерфейс REST защищается с помощью [обычной проверки подлинности доступа](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="28d2b-116">The REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="28d2b-117">Чтобы обеспечить безопасную отправку учетных данных на сервер, все запросы следует отправлять с помощью протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="28d2b-117">You should always make requests by using HTTPS to ensure that your credentials are securely sent to the server.</span></span>


1. <span data-ttu-id="28d2b-118">Используйте следующую команду в командной строке, чтобы проверить возможность подключения к кластеру HDInsight:</span><span class="sxs-lookup"><span data-stu-id="28d2b-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="28d2b-119">Вы должны получить ответ, аналогичный показанному ниже фрагменту JSON.</span><span class="sxs-lookup"><span data-stu-id="28d2b-119">You should receive a response similar to the following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="28d2b-120">Ниже приведены параметры, используемые в этой команде:</span><span class="sxs-lookup"><span data-stu-id="28d2b-120">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="28d2b-121">**-u**: имя пользователя и пароль, используемые для аутентификации запроса.</span><span class="sxs-lookup"><span data-stu-id="28d2b-121">**-u**: Indicates the user name and password used to authenticate the request</span></span>
   * <span data-ttu-id="28d2b-122">**-G**: указывает, что это запрос GET.</span><span class="sxs-lookup"><span data-stu-id="28d2b-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="28d2b-123">Начало URI **https://CLUSTERNAME.azurehdinsight.net/templeton/v1** одинаковое для всех запросов.</span><span class="sxs-lookup"><span data-stu-id="28d2b-123">The beginning of the URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span>

2. <span data-ttu-id="28d2b-124">Чтобы отправить задание MapReduce, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="28d2b-124">To submit a MapReduce job, use the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="28d2b-125">Конец универсального кода ресурса (/mapreduce/jar) сообщает WebHCat, что этот запрос запускает задание MapReduce из класса в JAR-файле.</span><span class="sxs-lookup"><span data-stu-id="28d2b-125">The end of the URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="28d2b-126">Ниже приведены параметры, используемые в этой команде:</span><span class="sxs-lookup"><span data-stu-id="28d2b-126">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="28d2b-127">**-d**: `-G` не используется, поэтому в запросе по умолчанию используется метод POST.</span><span class="sxs-lookup"><span data-stu-id="28d2b-127">**-d**: `-G` is not used, so the request defaults to the POST method.</span></span> <span data-ttu-id="28d2b-128">`-d` задает значения данных, отправляемые в запросе.</span><span class="sxs-lookup"><span data-stu-id="28d2b-128">`-d` specifies the data values that are sent with the request.</span></span>
    * <span data-ttu-id="28d2b-129">**user.name**: пользователь, выполняющий команду.</span><span class="sxs-lookup"><span data-stu-id="28d2b-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="28d2b-130">**jar**: расположение JAR-файла, содержащего класс для запуска.</span><span class="sxs-lookup"><span data-stu-id="28d2b-130">**jar**: The location of the jar file that contains class to be ran</span></span>
    * <span data-ttu-id="28d2b-131">**class**: класс, содержащий логику MapReduce.</span><span class="sxs-lookup"><span data-stu-id="28d2b-131">**class**: The class that contains the MapReduce logic</span></span>
    * <span data-ttu-id="28d2b-132">**arg**: аргументы, передаваемые в задание MapReduce.</span><span class="sxs-lookup"><span data-stu-id="28d2b-132">**arg**: The arguments to be passed to the MapReduce job.</span></span> <span data-ttu-id="28d2b-133">В данном случае это входной текстовый файл и каталог, который используется для вывода.</span><span class="sxs-lookup"><span data-stu-id="28d2b-133">In this case, the input text file and the directory that are used for the output</span></span>

     <span data-ttu-id="28d2b-134">Эта команда должна возвращать идентификатор задания, который может использоваться для проверки состояния задания:</span><span class="sxs-lookup"><span data-stu-id="28d2b-134">This command should return a job ID that can be used to check the status of the job:</span></span>

       <span data-ttu-id="28d2b-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="28d2b-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="28d2b-136">Чтобы проверить состояние задания, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="28d2b-136">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="28d2b-137">Замените **JOBID** значением, возвращенным на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="28d2b-137">Replace the **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="28d2b-138">Например, если возвращено значение `{"id":"job_1415651640909_0026"}`, то JOBID будет `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="28d2b-138">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then the JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="28d2b-139">Если задание завершено, то возвращается состояние `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="28d2b-139">If the job is complete, the state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="28d2b-140">Этот запрос Curl возвращает документ JSON с информацией о задании.</span><span class="sxs-lookup"><span data-stu-id="28d2b-140">This Curl request returns a JSON document with information about the job.</span></span> <span data-ttu-id="28d2b-141">При этом jq используется только для получения значения состояния.</span><span class="sxs-lookup"><span data-stu-id="28d2b-141">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="28d2b-142">После изменения состояния задания на `SUCCEEDED` результаты задания можно получить из хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="28d2b-142">When the state of the job has changed to `SUCCEEDED`, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="28d2b-143">Параметр `statusdir`, передаваемый в запросе, содержит расположение выходного файла.</span><span class="sxs-lookup"><span data-stu-id="28d2b-143">The `statusdir` parameter that is passed with the query contains the location of the output file.</span></span> <span data-ttu-id="28d2b-144">В данном случае это `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="28d2b-144">In this example, the location is `/example/curl`.</span></span> <span data-ttu-id="28d2b-145">Этот адрес задает каталог `/example/curl` для сохранения выходных данных задания, который размещен в хранилище по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="28d2b-145">This address stores the output of the job in the clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="28d2b-146">Вы можете вывести список этих файлов и скачать их с помощью [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="28d2b-146">You can list and download these files by using the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="28d2b-147">Дополнительные сведения о работе с большими двоичными объектами с помощью Azure CLI см. в документе [Использование Azure CLI 2.0 со службой хранилища Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs).</span><span class="sxs-lookup"><span data-stu-id="28d2b-147">For more information on working with blobs from the Azure CLI, see the [Using the Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="28d2b-148"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28d2b-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="28d2b-149">Общая информация о заданиях MapReduce в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="28d2b-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="28d2b-150">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="28d2b-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="28d2b-151">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="28d2b-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="28d2b-152">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="28d2b-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="28d2b-153">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="28d2b-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="28d2b-154">Дополнительные сведения об интерфейсе REST, используемом в этой статье, см. в [справочнике по WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="28d2b-154">For more information about the REST interface that is used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>