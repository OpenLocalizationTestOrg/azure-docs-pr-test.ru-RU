---
title: "Использование Hadoop Sqoop с Curl в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте об удаленной отправке заданий Sqoop в HDInsight с помощью Curl."
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
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="216e0-103">Выполнение заданий Sqoop с Hadoop в HDInsight с помощью Curl</span><span class="sxs-lookup"><span data-stu-id="216e0-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="216e0-104">Узнайте, как с помощью Curl выполнять задания Sqoop в кластере Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="216e0-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="216e0-105">Curl используется для демонстрации возможностей взаимодействия с HDInsight с помощью необработанных HTTP-запросов для выполнения и мониторинга заданий Sqoop, а также получения их результатов.</span><span class="sxs-lookup"><span data-stu-id="216e0-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="216e0-106">Для этого используется REST API для WebHCat (прежнее название — Templeton), предоставляемый кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="216e0-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="216e0-107">Если вы уже знаете, как использовать серверы Hadoop на платформе Linux, но не знакомы с HDInsight, ознакомьтесь со статьей [Сведения об использовании HDInsight в Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="216e0-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="216e0-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="216e0-108">Prerequisites</span></span>
<span data-ttu-id="216e0-109">Чтобы выполнить действия, описанные в этой статье, необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="216e0-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="216e0-110">Hadoop в кластере HDInsight (на платформе Linux или Windows)</span><span class="sxs-lookup"><span data-stu-id="216e0-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="216e0-111">Curl</span><span class="sxs-lookup"><span data-stu-id="216e0-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="216e0-112">jq</span><span class="sxs-lookup"><span data-stu-id="216e0-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="216e0-113">Отправка заданий Sqoop с помощью Curl</span><span class="sxs-lookup"><span data-stu-id="216e0-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="216e0-114">При использовании Curl или любых других средств связи REST с WebHCat нужно выполнять аутентификацию запросов с помощью пароля и имени пользователя администратора кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="216e0-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="216e0-115">Имя кластера необходимо также использовать в составе универсального кода ресурса (URI), используемого для отправки запросов на сервер.</span><span class="sxs-lookup"><span data-stu-id="216e0-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="216e0-116">В командах, описанных в этом разделе, замените **USERNAME** на имя пользователя для выполнения проверки подлинности в кластере, а **PASSWORD** — на пароль учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="216e0-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="216e0-117">Замените **CLUSTERNAME** именем кластера.</span><span class="sxs-lookup"><span data-stu-id="216e0-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="216e0-118">REST API защищен с помощью [обычной проверки подлинности](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="216e0-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="216e0-119">Чтобы обеспечить безопасную отправку учетных данных на сервер, все запросы следует отправлять с помощью протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="216e0-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="216e0-120">Используйте следующую команду в командной строке, чтобы проверить возможность подключения к кластеру HDInsight:</span><span class="sxs-lookup"><span data-stu-id="216e0-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="216e0-121">Вы должны получить ответ, аналогичный показанному ниже:</span><span class="sxs-lookup"><span data-stu-id="216e0-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="216e0-122">Ниже приведены параметры, используемые в этой команде:</span><span class="sxs-lookup"><span data-stu-id="216e0-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="216e0-123">**-u** — имя пользователя и пароль, используемый для аутентификации запроса.</span><span class="sxs-lookup"><span data-stu-id="216e0-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="216e0-124">**-G** — указывает, что это запрос GET.</span><span class="sxs-lookup"><span data-stu-id="216e0-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="216e0-125">Начало URL-адреса **https://CLUSTERNAME.azurehdinsight.net/templeton/v1** будет одинаковым для всех запросов.</span><span class="sxs-lookup"><span data-stu-id="216e0-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="216e0-126">Путь **/status** указывает, что по запросу серверу должно быть возвращено состояние WebHCat (другое название — Templeton).</span><span class="sxs-lookup"><span data-stu-id="216e0-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="216e0-127">Чтобы отправить задание Sqoop, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="216e0-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="216e0-128">Ниже приведены параметры, используемые в этой команде:</span><span class="sxs-lookup"><span data-stu-id="216e0-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="216e0-129">**-d** — так как `-G` не используется, в запросе по умолчанию используется метод POST.</span><span class="sxs-lookup"><span data-stu-id="216e0-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="216e0-130">`-d` задает значения данных, отправляемые в запросе.</span><span class="sxs-lookup"><span data-stu-id="216e0-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="216e0-131">**user.name** — пользователь, выполняющий команду.</span><span class="sxs-lookup"><span data-stu-id="216e0-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="216e0-132">**command** — выполняемая команда Sqoop.</span><span class="sxs-lookup"><span data-stu-id="216e0-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="216e0-133">**statusdir** — каталог, в который будет записано состояние этого задания.</span><span class="sxs-lookup"><span data-stu-id="216e0-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="216e0-134">Эта команда должна возвращать идентификатор задания, который может использоваться для проверки состояния задания.</span><span class="sxs-lookup"><span data-stu-id="216e0-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="216e0-135">Чтобы проверить состояние задания, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="216e0-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="216e0-136">Замените **JOBID** значением, возвращенным на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="216e0-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="216e0-137">Например, если возвращено значение `{"id":"job_1415651640909_0026"}`, то **JOBID** будет `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="216e0-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="216e0-138">Если задание завершено, у него будет состояние **SUCCEEDED**(Успешно).</span><span class="sxs-lookup"><span data-stu-id="216e0-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="216e0-139">Этот запрос Curl возвращает документ нотации объектов JavaScript с информацией о задании. При этом jq используется только для получения значения состояния.</span><span class="sxs-lookup"><span data-stu-id="216e0-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="216e0-140">После изменения состояния задания на **SUCCEEDED** результаты задания можно получить из хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="216e0-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="216e0-141">Параметр `statusdir`, передаваемый с запросом, содержит расположение выходного файла. В нашем примере это **wasb:///example/curl**.</span><span class="sxs-lookup"><span data-stu-id="216e0-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="216e0-142">При использовании этого адреса выходные данные задания сохраняются в каталоге **example/curl** в контейнере хранилища, используемом по умолчанию кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="216e0-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="216e0-143">Вы можете вывести список этих файлов и скачать их с помощью [интерфейса командной строки Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="216e0-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="216e0-144">Например, для просмотра списка файлов в **example/curl**можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="216e0-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="216e0-145">Чтобы скачать файл:</span><span class="sxs-lookup"><span data-stu-id="216e0-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="216e0-146">Необходимо либо указать имя учетной записи хранения, содержащей большой двоичный объект, с помощью параметров `-a` и `-k`, либо задать переменные среды **AZURE\_STORAGE\_ACCOUNT** и **AZURE\_STORAGE\_ACCESS\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="216e0-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="216e0-147">См. также: <a href="hdinsight-upload-data.md" target="_blank".</span><span class="sxs-lookup"><span data-stu-id="216e0-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="216e0-148">Ограничения</span><span class="sxs-lookup"><span data-stu-id="216e0-148">Limitations</span></span>
* <span data-ttu-id="216e0-149">Массовый экспорт: при использовании HDInsight на основе Linux соединитель Sqoop, применяемый для экспорта данных в Microsoft SQL Server или базу данных SQL Azure, пока не поддерживает операции массовой вставки.</span><span class="sxs-lookup"><span data-stu-id="216e0-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="216e0-150">Пакетная обработка: при использовании HDInsight на основе Linux, когда для выполнения вставок применяется переключатель `-batch` , Sqoop выполняет несколько вставок вместо пакетной обработки операций вставки.</span><span class="sxs-lookup"><span data-stu-id="216e0-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="216e0-151">Сводка</span><span class="sxs-lookup"><span data-stu-id="216e0-151">Summary</span></span>
<span data-ttu-id="216e0-152">Как показано в этом документе, для запуска, мониторинга и просмотра результатов выполнения заданий Sqoop в кластере HDInsight можно использовать необработанные HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="216e0-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="216e0-153">Дополнительную информацию об интерфейсе REST, используемом в этой статье, см. в <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">справочнике по Sqoop REST API</a>.</span><span class="sxs-lookup"><span data-stu-id="216e0-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="216e0-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="216e0-154">Next steps</span></span>
<span data-ttu-id="216e0-155">Общая информация об использовании Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="216e0-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="216e0-156">Использование Sqoop с Hadoop в HDInsight (Windows)</span><span class="sxs-lookup"><span data-stu-id="216e0-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="216e0-157">Дополнительная информация о других способах работы с Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="216e0-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="216e0-158">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="216e0-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="216e0-159">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="216e0-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="216e0-160">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="216e0-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


