---
title: "aaaUse MapReduce и Curl на Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как tooremotely запуска задания MapReduce с Hadoop в HDInsight с помощью Перелистывание."
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
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="cca95-103">Выполнение заданий MapReduce с помощью REST в Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cca95-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="cca95-104">Узнайте, как toouse hello WebHCat REST API toorun MapReduce заданий на Hadoop в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cca95-104">Learn how toouse hello WebHCat REST API toorun MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="cca95-105">Перелистывание — используется toodemonstrate о взаимодействии с HDInsight с помощью необработанных задания MapReduce toorun запросов HTTP.</span><span class="sxs-lookup"><span data-stu-id="cca95-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="cca95-106">Если вы уже знакомы с использованием серверов под управлением Linux Hadoop, но существует новый tooHDInsight, см. раздел hello [необходимые tooknow о под управлением Linux Hadoop в HDInsight](hdinsight-hadoop-linux-information.md) документа.</span><span class="sxs-lookup"><span data-stu-id="cca95-106">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see hello [What you need tooknow about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="cca95-107"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cca95-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="cca95-108">Hadoop в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cca95-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="cca95-109">Curl</span><span class="sxs-lookup"><span data-stu-id="cca95-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="cca95-110">jq</span><span class="sxs-lookup"><span data-stu-id="cca95-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="cca95-111"><a id="curl"></a>Выполнение заданий MapReduce с помощью Curl</span><span class="sxs-lookup"><span data-stu-id="cca95-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="cca95-112">При использовании с WebHCat перелистывания или любые другие связи REST должен пройти проверку подлинности запросы hello, указав имя пользователя администратора кластера HDInsight hello и пароль.</span><span class="sxs-lookup"><span data-stu-id="cca95-112">When you use Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="cca95-113">Имя кластера hello необходимо использовать как часть URI, который является сервером toohello запросы hello используется toosend hello.</span><span class="sxs-lookup"><span data-stu-id="cca95-113">You must use hello cluster name as part of hello URI that is used toosend hello requests toohello server.</span></span>
>
> <span data-ttu-id="cca95-114">Hello команды в этом разделе, замените **USERNAME** с кластером toohello tooauthenticate hello пользователя, и **пароль** hello пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="cca95-114">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="cca95-115">Замените **CLUSTERNAME** с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="cca95-115">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="cca95-116">Hello REST API обеспечивается с помощью [базовая проверка подлинности доступа](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="cca95-116">hello REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="cca95-117">Всегда должны выполнять запросы, используя свои учетные данные безопасно отправляются серверу toohello tooensure HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cca95-117">You should always make requests by using HTTPS tooensure that your credentials are securely sent toohello server.</span></span>


1. <span data-ttu-id="cca95-118">Из командной строки используйте следующие команды tooverify, возможность подключения кластера HDInsight tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="cca95-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="cca95-119">Должно появиться примерно toohello ответа, следуя JSON.</span><span class="sxs-lookup"><span data-stu-id="cca95-119">You should receive a response similar toohello following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="cca95-120">Ниже приведены параметры Hello, использованный в этой команде.</span><span class="sxs-lookup"><span data-stu-id="cca95-120">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="cca95-121">**-u**: указывает hello имя пользователя и пароль используются tooauthenticate hello запроса</span><span class="sxs-lookup"><span data-stu-id="cca95-121">**-u**: Indicates hello user name and password used tooauthenticate hello request</span></span>
   * <span data-ttu-id="cca95-122">**-G**: указывает, что это запрос GET.</span><span class="sxs-lookup"><span data-stu-id="cca95-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="cca95-123">Здравствуйте, начало hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello одинаково для всех запросов.</span><span class="sxs-lookup"><span data-stu-id="cca95-123">hello beginning of hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span>

2. <span data-ttu-id="cca95-124">toosubmit задание MapReduce hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cca95-124">toosubmit a MapReduce job, use hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="cca95-125">конец Hello hello URI (/ mapreduce и jar) сообщает WebHCat, этот запрос запускает задание MapReduce из класса в jar-файл.</span><span class="sxs-lookup"><span data-stu-id="cca95-125">hello end of hello URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="cca95-126">Ниже приведены параметры Hello, использованный в этой команде.</span><span class="sxs-lookup"><span data-stu-id="cca95-126">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="cca95-127">**-d**: `-G` не используется, поэтому hello запроса по умолчанию используется метод POST toohello.</span><span class="sxs-lookup"><span data-stu-id="cca95-127">**-d**: `-G` is not used, so hello request defaults toohello POST method.</span></span> <span data-ttu-id="cca95-128">`-d`Указывает hello значения данных, отправляемых с запросом hello.</span><span class="sxs-lookup"><span data-stu-id="cca95-128">`-d` specifies hello data values that are sent with hello request.</span></span>
    * <span data-ttu-id="cca95-129">**User.Name**: hello пользователь, выполняющий команду hello</span><span class="sxs-lookup"><span data-stu-id="cca95-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="cca95-130">**JAR**: hello расположение hello jar-файл, содержащий класс toobe выполнялись</span><span class="sxs-lookup"><span data-stu-id="cca95-130">**jar**: hello location of hello jar file that contains class toobe ran</span></span>
    * <span data-ttu-id="cca95-131">**Класс**: hello класса, содержащего логику MapReduce hello</span><span class="sxs-lookup"><span data-stu-id="cca95-131">**class**: hello class that contains hello MapReduce logic</span></span>
    * <span data-ttu-id="cca95-132">**arg**: hello аргументы toobe передан toohello задания MapReduce.</span><span class="sxs-lookup"><span data-stu-id="cca95-132">**arg**: hello arguments toobe passed toohello MapReduce job.</span></span> <span data-ttu-id="cca95-133">В этом случае hello входной текстовый файл и hello каталог, которые используются для вывода hello</span><span class="sxs-lookup"><span data-stu-id="cca95-133">In this case, hello input text file and hello directory that are used for hello output</span></span>

     <span data-ttu-id="cca95-134">Эта команда должна возвращать идентификатора задания, который может быть состояние hello используется toocheck hello задания:</span><span class="sxs-lookup"><span data-stu-id="cca95-134">This command should return a job ID that can be used toocheck hello status of hello job:</span></span>

       <span data-ttu-id="cca95-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="cca95-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="cca95-136">состояние hello toocheck задания hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cca95-136">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="cca95-137">Замените hello **JOBID** с hello значение, возвращенное в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="cca95-137">Replace hello **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="cca95-138">Например, если hello, возвращают значение было `{"id":"job_1415651640909_0026"}`, затем hello JOBID бы `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="cca95-138">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then hello JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="cca95-139">При задании hello hello состояние возвращается `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="cca95-139">If hello job is complete, hello state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cca95-140">Этот запрос перелистывание возвращает документ JSON с сведения о задании hello.</span><span class="sxs-lookup"><span data-stu-id="cca95-140">This Curl request returns a JSON document with information about hello job.</span></span> <span data-ttu-id="cca95-141">Используется Jq tooretrieve только hello значение состояния.</span><span class="sxs-lookup"><span data-stu-id="cca95-141">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="cca95-142">При изменении состояния hello hello задания слишком`SUCCEEDED`, можно получить результаты задания hello hello из хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="cca95-142">When hello state of hello job has changed too`SUCCEEDED`, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="cca95-143">Hello `statusdir` параметр, передаваемый с запросом hello содержит расположение hello hello выходного файла.</span><span class="sxs-lookup"><span data-stu-id="cca95-143">hello `statusdir` parameter that is passed with hello query contains hello location of hello output file.</span></span> <span data-ttu-id="cca95-144">В этом примере — расположение hello `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="cca95-144">In this example, hello location is `/example/curl`.</span></span> <span data-ttu-id="cca95-145">Этот адрес сохраняет hello выходные данные задания hello в хранилище по умолчанию hello кластеров в `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="cca95-145">This address stores hello output of hello job in hello clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="cca95-146">Можно перечислить и загрузить эти файлы с помощью hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cca95-146">You can list and download these files by using hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="cca95-147">Дополнительные сведения о работе с большими двоичными объектами из hello Azure CLI см. в разделе hello [использование hello Azure CLI 2.0 со службой хранилища Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs) документа.</span><span class="sxs-lookup"><span data-stu-id="cca95-147">For more information on working with blobs from hello Azure CLI, see hello [Using hello Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="cca95-148"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cca95-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="cca95-149">Общая информация о заданиях MapReduce в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cca95-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="cca95-150">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cca95-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="cca95-151">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cca95-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="cca95-152">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cca95-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="cca95-153">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cca95-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="cca95-154">Дополнительные сведения о hello интерфейс REST, который используется в этой статье в разделе hello [WebHCat ссылка](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="cca95-154">For more information about hello REST interface that is used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
