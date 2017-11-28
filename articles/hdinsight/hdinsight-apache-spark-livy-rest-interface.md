---
title: "aaaUse Livy Spark toosubmit заданий tooSpark кластера Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toosubmit toouse API-интерфейса REST Spark Apache Spark удаленно заданий tooan кластера Azure HDInsight."
keywords: apache spark rest api,livy spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a><span data-ttu-id="02924-104">Используйте API-интерфейса REST Apache Spark toosubmit заданий удаленного tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="02924-104">Use Apache Spark REST API toosubmit remote jobs tooan HDInsight Spark cluster</span></span>

<span data-ttu-id="02924-105">Узнайте, как toouse Livy hello Apache Spark REST API, который будет использоваться toosubmit удаленного задания tooan кластера Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="02924-105">Learn how toouse Livy, hello Apache Spark REST API, which is used toosubmit remote jobs tooan Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="02924-106">Подробную документацию см. в статье о [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="02924-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="02924-107">Можно использовать интерактивный оболочках Spark Livy toorun или отправки пакетных заданий toobe проведение Spark.</span><span class="sxs-lookup"><span data-stu-id="02924-107">You can use Livy toorun interactive Spark shells or submit batch jobs toobe run on Spark.</span></span> <span data-ttu-id="02924-108">В данной статье рассмотрен с использованием Livy toosubmit пакетных заданий.</span><span class="sxs-lookup"><span data-stu-id="02924-108">This article talks about using Livy toosubmit batch jobs.</span></span> <span data-ttu-id="02924-109">фрагменты кода Hello в этой статье использовать toomake перелистывание конечной Livy Spark toohello вызовы REST API.</span><span class="sxs-lookup"><span data-stu-id="02924-109">hello snippets in this article use cURL toomake REST API calls toohello Livy Spark endpoint.</span></span>

<span data-ttu-id="02924-110">**Предварительные требования:**</span><span class="sxs-lookup"><span data-stu-id="02924-110">**Prerequisites:**</span></span>

* <span data-ttu-id="02924-111">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02924-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="02924-112">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="02924-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="02924-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="02924-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="02924-114">В этой статье используется toodemonstrate перелистывание как вызывает toomake API-интерфейса REST для кластера HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="02924-114">This article uses cURL toodemonstrate how toomake REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="02924-115">Отправка пакетного задания Livy Spark</span><span class="sxs-lookup"><span data-stu-id="02924-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="02924-116">Прежде чем отправлять пакетного задания, необходимо передать jar приложения hello в хранилище кластера hello, связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="02924-116">Before you submit a batch job, you must upload hello application jar on hello cluster storage associated with hello cluster.</span></span> <span data-ttu-id="02924-117">Можно использовать [ **AzCopy**](../storage/common/storage-use-azcopy.md), программы командной строки, toodo так.</span><span class="sxs-lookup"><span data-stu-id="02924-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, toodo so.</span></span> <span data-ttu-id="02924-118">Существуют различные клиенты, можно использовать tooupload данные.</span><span class="sxs-lookup"><span data-stu-id="02924-118">There are various other clients you can use tooupload data.</span></span> <span data-ttu-id="02924-119">Дополнительные сведения о них см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="02924-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="02924-120">**Примеры**:</span><span class="sxs-lookup"><span data-stu-id="02924-120">**Examples**:</span></span>

* <span data-ttu-id="02924-121">Если hello jar-файл для хранения данных кластера hello (WASB)</span><span class="sxs-lookup"><span data-stu-id="02924-121">If hello jar file is on hello cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="02924-122">Toopass hello jar filename и hello classname как часть входного файла (в этом примере input.txt)</span><span class="sxs-lookup"><span data-stu-id="02924-122">If you want toopass hello jar filename and hello classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a><span data-ttu-id="02924-123">Получить сведения о пакетах Livy Spark на кластере hello</span><span class="sxs-lookup"><span data-stu-id="02924-123">Get information on Livy Spark batches running on hello cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="02924-124">**Примеры**:</span><span class="sxs-lookup"><span data-stu-id="02924-124">**Examples**:</span></span>

* <span data-ttu-id="02924-125">Если нужно tooretrieve все пакеты Livy Spark hello, работающих в кластере hello:</span><span class="sxs-lookup"><span data-stu-id="02924-125">If you want tooretrieve all hello Livy Spark batches running on hello cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="02924-126">Если требуется, чтобы tooretrieve конкретному пакету с ИД данного пакета</span><span class="sxs-lookup"><span data-stu-id="02924-126">If you want tooretrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="02924-127">Удаление пакетного задания Livy Spark</span><span class="sxs-lookup"><span data-stu-id="02924-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="02924-128">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="02924-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="02924-129">Livy Spark и высокая доступность</span><span class="sxs-lookup"><span data-stu-id="02924-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="02924-130">Livy предоставляет высокого уровня доступности для задания Spark на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="02924-130">Livy provides high-availability for Spark jobs running on hello cluster.</span></span> <span data-ttu-id="02924-131">Вот несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="02924-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="02924-132">Если hello Livy служба перестает работать после отправки задания удаленно tooa Spark кластер, hello задания toorun продолжается в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="02924-132">If hello Livy service goes down after you have submitted a job remotely tooa Spark cluster, hello job continues toorun in hello background.</span></span> <span data-ttu-id="02924-133">Когда Livy резервное копирование, он восстанавливает hello состояние задания hello и отчеты, его обратно.</span><span class="sxs-lookup"><span data-stu-id="02924-133">When Livy is back up, it restores hello status of hello job and reports it back.</span></span>
* <span data-ttu-id="02924-134">Записные книжки Jupyter для HDInsight берутся из Livy в серверном hello.</span><span class="sxs-lookup"><span data-stu-id="02924-134">Jupyter notebooks for HDInsight are powered by Livy in hello backend.</span></span> <span data-ttu-id="02924-135">Если записной книжке выполняется задание Spark и возвращает перезапуска службы Livy hello, hello ноутбук продолжает toorun hello кода ячейки.</span><span class="sxs-lookup"><span data-stu-id="02924-135">If a notebook is running a Spark job and hello Livy service gets restarted, hello notebook continues toorun hello code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="02924-136">Показать пример</span><span class="sxs-lookup"><span data-stu-id="02924-136">Show me an example</span></span>
<span data-ttu-id="02924-137">В этом разделе мы рассмотрим примеры toouse Livy Spark toosubmit пакетное задание, отслеживать ход выполнения hello hello задания и затем удалите его.</span><span class="sxs-lookup"><span data-stu-id="02924-137">In this section, we look at examples toouse Livy Spark toosubmit batch job, monitor hello progress of hello job, and then delete it.</span></span> <span data-ttu-id="02924-138">Hello приложение, мы используем в этом примере — hello один разработан в статье hello [Создание Scala автономное приложение и toorun в кластере HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="02924-138">hello application we use in this example is hello one developed in hello article [Create a standalone Scala application and toorun on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="02924-139">Hello при выполнении шагов предполагается, что:</span><span class="sxs-lookup"><span data-stu-id="02924-139">hello steps here assume that:</span></span>

* <span data-ttu-id="02924-140">Вы уже скопировали через hello приложения jar toohello хранилища учетной записи, связанной с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="02924-140">You have already copied over hello application jar toohello storage account associated with hello cluster.</span></span>
* <span data-ttu-id="02924-141">У вас есть перелистывания, установленных на компьютере hello, которого вы пытаетесь следующие действия.</span><span class="sxs-lookup"><span data-stu-id="02924-141">You have CuRL installed on hello computer where you are trying these steps.</span></span>

<span data-ttu-id="02924-142">Выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="02924-142">Perform hello following steps:</span></span>

1. <span data-ttu-id="02924-143">Сообщите нам сначала убедитесь, что Livy Spark работает на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="02924-143">Let us first verify that Livy Spark is running on hello cluster.</span></span> <span data-ttu-id="02924-144">Для этого получите список выполняемых пакетов.</span><span class="sxs-lookup"><span data-stu-id="02924-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="02924-145">При запуске задания, первый раз с помощью Livy для hello hello вывода должен возвращать ноль.</span><span class="sxs-lookup"><span data-stu-id="02924-145">If you are running a job using Livy for hello first time, hello output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="02924-146">Вы должны получить выходные данные примерно toohello следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="02924-146">You should get an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="02924-147">Обратите внимание на то, как последняя строка hello в выходных данных hello говорит **итог: 0**, который предлагает нет запущенных пакетов.</span><span class="sxs-lookup"><span data-stu-id="02924-147">Notice how hello last line in hello output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="02924-148">Теперь отправим пакетное задание.</span><span class="sxs-lookup"><span data-stu-id="02924-148">Let us now submit a batch job.</span></span> <span data-ttu-id="02924-149">Следующий фрагмент кода Hello использует имя входного файла (input.txt) toopass hello jar и имя класса hello в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="02924-149">hello following snippet uses an input file (input.txt) toopass hello jar name and hello class name as parameters.</span></span> <span data-ttu-id="02924-150">Если на компьютере следующие действия на компьютере Windows с помощью входного файла — hello, рекомендованный подход.</span><span class="sxs-lookup"><span data-stu-id="02924-150">If you are running these steps from a Windows computer, using an input file is hello recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="02924-151">Здравствуйте, параметры в файле hello **input.txt** определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="02924-151">hello parameters in hello file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="02924-152">Вы увидите примерно toohello выходные данные, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="02924-152">You should see an output similar toohello  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="02924-153">Обратите внимание на то, как последняя строка выходных данных hello hello говорит **состояние: запуск**.</span><span class="sxs-lookup"><span data-stu-id="02924-153">Notice how hello last line of hello output says **state:starting**.</span></span> <span data-ttu-id="02924-154">Кроме того, она включает параметр **id:0** —</span><span class="sxs-lookup"><span data-stu-id="02924-154">It also says, **id:0**.</span></span> <span data-ttu-id="02924-155">Здесь **0** — идентификатор пакета hello.</span><span class="sxs-lookup"><span data-stu-id="02924-155">Here, **0** is hello batch ID.</span></span>

3. <span data-ttu-id="02924-156">Теперь можно извлечь состояние hello этого конкретного пакета, используя идентификатор hello пакета.</span><span class="sxs-lookup"><span data-stu-id="02924-156">You can now retrieve hello status of this specific batch using hello batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="02924-157">Вы увидите примерно toohello выходные данные, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="02924-157">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="02924-158">Hello выходных данных теперь указывается **состояние: успех**, который предлагает hello задания успешно завершена.</span><span class="sxs-lookup"><span data-stu-id="02924-158">hello output now shows **state:success**, which suggests that hello job was successfully completed.</span></span>

4. <span data-ttu-id="02924-159">Если требуется, теперь можно удалить пакет hello.</span><span class="sxs-lookup"><span data-stu-id="02924-159">If you want, you can now delete hello batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="02924-160">Вы увидите примерно toohello выходные данные, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="02924-160">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="02924-161">Последняя строка Hello hello выходных данных показаны hello пакета успешно удален.</span><span class="sxs-lookup"><span data-stu-id="02924-161">hello last line of hello output shows that hello batch was successfully deleted.</span></span> <span data-ttu-id="02924-162">Удаление задания, пока она запущена, также разрывает hello задания.</span><span class="sxs-lookup"><span data-stu-id="02924-162">Deleting a job, while it is running, also kills hello job.</span></span> <span data-ttu-id="02924-163">При удалении завершенного задания, успешно или нет, она полностью удаляется сведения о задании hello.</span><span class="sxs-lookup"><span data-stu-id="02924-163">If you delete a job that has completed, successfully or otherwise, it deletes hello job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="02924-164">Использование Livy Spark в кластерах HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="02924-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="02924-165">Кластер HDInsight 3.5 по умолчанию запрещает использование файлы образцов данных tooaccess пути к локальному файлу или JAR-файлов.</span><span class="sxs-lookup"><span data-stu-id="02924-165">HDInsight 3.5 cluster, by default, disables use of local file paths tooaccess sample data files or jars.</span></span> <span data-ttu-id="02924-166">Мы рекомендуем вам toouse hello `wasb://` путь вместо tooaccess JAR-файлов и создавать образец данных файлов из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="02924-166">We encourage you toouse hello `wasb://` path instead tooaccess jars or sample data files from hello cluster.</span></span> <span data-ttu-id="02924-167">Если вы хотите toouse локальный путь, необходимо обновить конфигурации Ambari hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="02924-167">If you do want toouse local path, you must update hello Ambari configuration accordingly.</span></span> <span data-ttu-id="02924-168">toodo так:</span><span class="sxs-lookup"><span data-stu-id="02924-168">toodo so:</span></span>

1. <span data-ttu-id="02924-169">Откройте портал Ambari toohello для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="02924-169">Go toohello Ambari portal for hello cluster.</span></span> <span data-ttu-id="02924-170">Hello Ambari веб-интерфейса можно найти в кластер HDInsight адресу https://**ИМЯ_КЛАСТЕРА**. azurehdidnsight.net, где ИМЯ_КЛАСТЕРА hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="02924-170">hello Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is hello name of your cluster.</span></span>

2. <span data-ttu-id="02924-171">Hello навигации слева, щелкните **Livy**, а затем нажмите кнопку **Configs**.</span><span class="sxs-lookup"><span data-stu-id="02924-171">From hello left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="02924-172">В разделе **по умолчанию livy** добавьте имя свойства hello `livy.file.local-dir-whitelist` и задать его значение слишком**«/»** Если требуется, чтобы система toofile tooallow полный доступ.</span><span class="sxs-lookup"><span data-stu-id="02924-172">Under **livy-default** add hello property name `livy.file.local-dir-whitelist` and set it's value too**"/"** if you want tooallow full access toofile system.</span></span> <span data-ttu-id="02924-173">Если требуется tooallow доступ только tooa конкретного каталога, предоставляют hello путь toothat каталог в качестве значений hello.</span><span class="sxs-lookup"><span data-stu-id="02924-173">If you want tooallow access only tooa specific directory, provide hello path toothat directory as hello value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="02924-174">Отправка задания Livy для кластера в пределах виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="02924-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="02924-175">При подключении tooan кластер HDInsight Spark из в виртуальной сети Azure, могут напрямую подключаться tooLivy на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="02924-175">If you connect tooan HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect tooLivy on hello cluster.</span></span> <span data-ttu-id="02924-176">В этом случае hello URL-адрес конечной точки Livy `http://<IP address of hello headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="02924-176">In such a case, hello URL for Livy endpoint is `http://<IP address of hello headnode>:8998/batches`.</span></span> <span data-ttu-id="02924-177">Здесь **8998** hello порт, на котором выполняется Livy на головному узлу кластера hello.</span><span class="sxs-lookup"><span data-stu-id="02924-177">Here, **8998** is hello port on which Livy runs on hello cluster headnode.</span></span> <span data-ttu-id="02924-178">Дополнительные сведения о доступе к службам через порты, не являющиеся общедоступными, см. в разделе [Порты, используемые службами Hadoop в HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="02924-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="02924-179">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="02924-179">Troubleshooting</span></span>

<span data-ttu-id="02924-180">Ниже приведены некоторые проблемы, которые вы можете столкнуться при использовании Livy для удаленного задания отправки tooSpark кластеров.</span><span class="sxs-lookup"><span data-stu-id="02924-180">Here are some issues that you might run into while using Livy for remote job submission tooSpark clusters.</span></span>

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a><span data-ttu-id="02924-181">Использование внешних jar из дополнительного хранилища hello не поддерживается</span><span class="sxs-lookup"><span data-stu-id="02924-181">Using an external jar from hello additional storage is not supported</span></span>

<span data-ttu-id="02924-182">**Проблема:** при Livy Spark задания ссылается на внешние JAR-файл из учетной записи hello дополнительное хранилище, связанное с кластером hello, hello задание завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="02924-182">**Problem:** If your Livy Spark job references an external jar from hello additional storage account associated with hello cluster, hello job fails.</span></span>

<span data-ttu-id="02924-183">**Решение:** убедитесь в том, что jar hello toouse доступно в хранилище по умолчанию hello, связанное с кластером HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="02924-183">**Resolution:** Make sure that hello jar you want toouse is available in hello default storage associated with hello HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="02924-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02924-184">Next step</span></span>

* [<span data-ttu-id="02924-185">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="02924-185">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="02924-186">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="02924-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

