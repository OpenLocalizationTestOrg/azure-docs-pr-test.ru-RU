---
title: "aaaUse Hadoop Sqoop с перелистывание в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как tooremotely передан tooHDInsight Sqoop заданий, с помощью Curl."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="0703c-103">Выполнение заданий Sqoop с Hadoop в HDInsight с помощью Curl</span><span class="sxs-lookup"><span data-stu-id="0703c-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="0703c-104">Узнайте, как кластер toouse Curl toorun Sqoop заданий на Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0703c-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="0703c-105">Перелистывание — используется toodemonstrate о взаимодействии с HDInsight с помощью необработанных toorun запросов HTTP, монитор и получить результаты hello Sqoop заданий.</span><span class="sxs-lookup"><span data-stu-id="0703c-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="0703c-106">Это работает с использованием hello WebHCat API-Интерфейсу REST (прежнее название — Templeton) с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0703c-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="0703c-107">Если вы уже знакомы с использованием серверов под управлением Linux Hadoop, но являются новый tooHDInsight, см. раздел [сведения об использовании HDInsight в Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="0703c-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0703c-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0703c-108">Prerequisites</span></span>
<span data-ttu-id="0703c-109">в этой статье инструкциям toocomplete hello, вам потребуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0703c-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="0703c-110">Hadoop в кластере HDInsight (на платформе Linux или Windows)</span><span class="sxs-lookup"><span data-stu-id="0703c-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="0703c-111">Curl</span><span class="sxs-lookup"><span data-stu-id="0703c-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="0703c-112">jq</span><span class="sxs-lookup"><span data-stu-id="0703c-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="0703c-113">Отправка заданий Sqoop с помощью Curl</span><span class="sxs-lookup"><span data-stu-id="0703c-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="0703c-114">При использовании перелистывания или любые другие связи REST с WebHCat, должен пройти проверку подлинности запросы hello, предоставляя hello имя пользователя и пароль администратора кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="0703c-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="0703c-115">Как использовать запросы toohello toosend hello server часть hello универсальный код ресурса (URI), необходимо также использовать имя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="0703c-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="0703c-116">Hello команды в этом разделе, замените **USERNAME** tooauthenticate toohello hello пользователя кластера и заменить **пароль** hello пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="0703c-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="0703c-117">Замените **CLUSTERNAME** с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="0703c-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="0703c-118">Hello API-интерфейса REST является защищен с помощью [обычной проверки подлинности](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="0703c-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="0703c-119">Всегда должны выполнять запросы с помощью безопасного HTTP (HTTPS) toohelp убедитесь, что учетные данные безопасно отправляются toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="0703c-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="0703c-120">Из командной строки используйте следующие команды tooverify, возможность подключения кластера HDInsight tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="0703c-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="0703c-121">Должно появиться ответа аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="0703c-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="0703c-122">Ниже приведены параметры Hello, использованный в этой команде.</span><span class="sxs-lookup"><span data-stu-id="0703c-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="0703c-123">**-u** -hello имя пользователя и пароль используются tooauthenticate hello запроса.</span><span class="sxs-lookup"><span data-stu-id="0703c-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="0703c-124">**-G** — указывает, что это запрос GET.</span><span class="sxs-lookup"><span data-stu-id="0703c-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="0703c-125">Здравствуйте, начало hello URL-адрес, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, будет hello одинаково для всех запросов.</span><span class="sxs-lookup"><span data-stu-id="0703c-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="0703c-126">путь Hello **параметр/Status**, указывает, что hello запрос tooreturn состояние WebHCat (также известный как Templeton) для сервера hello.</span><span class="sxs-lookup"><span data-stu-id="0703c-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="0703c-127">Используйте следующие toosubmit задание sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="0703c-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="0703c-128">Ниже приведены параметры Hello, использованный в этой команде.</span><span class="sxs-lookup"><span data-stu-id="0703c-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="0703c-129">**-d** — с момента `-G` не используется, hello запроса по умолчанию используется метод POST toohello.</span><span class="sxs-lookup"><span data-stu-id="0703c-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="0703c-130">`-d`Указывает hello значения данных, отправляемых с запросом hello.</span><span class="sxs-lookup"><span data-stu-id="0703c-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="0703c-131">**User.Name** -hello пользователя, на котором выполняется команда hello.</span><span class="sxs-lookup"><span data-stu-id="0703c-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="0703c-132">**команда** -hello tooexecute команда Sqoop.</span><span class="sxs-lookup"><span data-stu-id="0703c-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="0703c-133">**statusdir** -будет записан hello каталог, в котором hello состояния для данного задания.</span><span class="sxs-lookup"><span data-stu-id="0703c-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="0703c-134">Эта команда должна возвращать идентификатора задания, который может быть используется toocheck hello состояние задания hello.</span><span class="sxs-lookup"><span data-stu-id="0703c-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="0703c-135">состояние hello toocheck задания hello, hello используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="0703c-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="0703c-136">Замените **JOBID** с hello значение, возвращенное в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="0703c-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="0703c-137">Например, если hello, возвращают значение было `{"id":"job_1415651640909_0026"}`, затем **JOBID** бы `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="0703c-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="0703c-138">Если задание hello завершена, будет иметь состояние hello **успешно**.</span><span class="sxs-lookup"><span data-stu-id="0703c-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0703c-139">Этот запрос перелистывание возвращает документ нотации объектов JavaScript (JSON) с сведения о задании hello; используется jq tooretrieve только hello значение состояния.</span><span class="sxs-lookup"><span data-stu-id="0703c-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="0703c-140">После hello состояние задания hello изменилось слишком**успешно**, результаты hello hello задания можно получить из хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0703c-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="0703c-141">Hello `statusdir` параметр, передаваемый с запросом hello содержит расположение hello hello выходного файла; в данном случае **wasb: / / / пример/перелистывание**.</span><span class="sxs-lookup"><span data-stu-id="0703c-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="0703c-142">Этот адрес сохраняет выходные данные hello задания hello в hello **примере/перелистывание** на контейнера хранилища по умолчанию hello, используемого кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0703c-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="0703c-143">Можно перечислить и загрузить эти файлы с помощью hello [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0703c-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="0703c-144">Например, файлы toolist в **примере/перелистывание**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0703c-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="0703c-145">toodownload файл, используйте hello ниже:</span><span class="sxs-lookup"><span data-stu-id="0703c-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="0703c-146">Необходимо указать имя учетной записи хранения hello, содержащее hello blob с помощью hello `-a` и `-k` параметры или набор hello **AZURE\_ХРАНЕНИЯ\_учетную запись** и **AZURE\_ХРАНЕНИЯ\_доступа\_ключ** переменные среды.</span><span class="sxs-lookup"><span data-stu-id="0703c-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="0703c-147">См. также: <a href="hdinsight-upload-data.md" target="_blank".</span><span class="sxs-lookup"><span data-stu-id="0703c-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="0703c-148">Ограничения</span><span class="sxs-lookup"><span data-stu-id="0703c-148">Limitations</span></span>
* <span data-ttu-id="0703c-149">Для массового экспорта — под управлением Linux с HDInsight, hello Sqoop соединитель, используемый tooexport данных tooMicrosoft SQL Server или база данных SQL Azure в настоящее время не поддерживает операции массовой вставки.</span><span class="sxs-lookup"><span data-stu-id="0703c-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="0703c-150">Пакетное выполнение — с hdinsight под управлением Linux, при использовании hello `-batch` переход при выполнении вставки, Sqoop будет выполнять вставку нескольких вместо Пакетная обработка операций вставки hello.</span><span class="sxs-lookup"><span data-stu-id="0703c-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="0703c-151">Сводка</span><span class="sxs-lookup"><span data-stu-id="0703c-151">Summary</span></span>
<span data-ttu-id="0703c-152">Как показано в этом документе, можно использовать необработанные toorun запроса HTTP, монитор и просмотр результатов hello Sqoop заданий в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0703c-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="0703c-153">Дополнительные сведения о hello интерфейс REST, используемые в этой статье в разделе hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">руководство по Sqoop REST API</a>.</span><span class="sxs-lookup"><span data-stu-id="0703c-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0703c-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0703c-154">Next steps</span></span>
<span data-ttu-id="0703c-155">Общая информация об использовании Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0703c-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="0703c-156">Использование Sqoop с Hadoop в HDInsight (Windows)</span><span class="sxs-lookup"><span data-stu-id="0703c-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="0703c-157">Дополнительная информация о других способах работы с Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0703c-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="0703c-158">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0703c-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0703c-159">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0703c-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0703c-160">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0703c-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


