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
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a>Используйте API-интерфейса REST Apache Spark toosubmit заданий удаленного tooan кластера HDInsight Spark

Узнайте, как toouse Livy hello Apache Spark REST API, который будет использоваться toosubmit удаленного задания tooan кластера Azure HDInsight Spark. Подробную документацию см. в статье о [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).

Можно использовать интерактивный оболочках Spark Livy toorun или отправки пакетных заданий toobe проведение Spark. В данной статье рассмотрен с использованием Livy toosubmit пакетных заданий. фрагменты кода Hello в этой статье использовать toomake перелистывание конечной Livy Spark toohello вызовы REST API.

**Предварительные требования:**

* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

* [cURL](http://curl.haxx.se/). В этой статье используется toodemonstrate перелистывание как вызывает toomake API-интерфейса REST для кластера HDInsight Spark.

## <a name="submit-a-livy-spark-batch-job"></a>Отправка пакетного задания Livy Spark
Прежде чем отправлять пакетного задания, необходимо передать jar приложения hello в хранилище кластера hello, связанные с кластером hello. Можно использовать [ **AzCopy**](../storage/common/storage-use-azcopy.md), программы командной строки, toodo так. Существуют различные клиенты, можно использовать tooupload данные. Дополнительные сведения о них см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

**Примеры**:

* Если hello jar-файл для хранения данных кластера hello (WASB)
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Toopass hello jar filename и hello classname как часть входного файла (в этом примере input.txt)
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a>Получить сведения о пакетах Livy Spark на кластере hello
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

**Примеры**:

* Если нужно tooretrieve все пакеты Livy Spark hello, работающих в кластере hello:
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Если требуется, чтобы tooretrieve конкретному пакету с ИД данного пакета
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a>Удаление пакетного задания Livy Spark
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

**Пример**:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a>Livy Spark и высокая доступность
Livy предоставляет высокого уровня доступности для задания Spark на кластере hello. Вот несколько примеров.

* Если hello Livy служба перестает работать после отправки задания удаленно tooa Spark кластер, hello задания toorun продолжается в фоновом режиме hello. Когда Livy резервное копирование, он восстанавливает hello состояние задания hello и отчеты, его обратно.
* Записные книжки Jupyter для HDInsight берутся из Livy в серверном hello. Если записной книжке выполняется задание Spark и возвращает перезапуска службы Livy hello, hello ноутбук продолжает toorun hello кода ячейки. 

## <a name="show-me-an-example"></a>Показать пример
В этом разделе мы рассмотрим примеры toouse Livy Spark toosubmit пакетное задание, отслеживать ход выполнения hello hello задания и затем удалите его. Hello приложение, мы используем в этом примере — hello один разработан в статье hello [Создание Scala автономное приложение и toorun в кластере HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md). Hello при выполнении шагов предполагается, что:

* Вы уже скопировали через hello приложения jar toohello хранилища учетной записи, связанной с кластером hello.
* У вас есть перелистывания, установленных на компьютере hello, которого вы пытаетесь следующие действия.

Выполните следующие шаги hello.

1. Сообщите нам сначала убедитесь, что Livy Spark работает на кластере hello. Для этого получите список выполняемых пакетов. При запуске задания, первый раз с помощью Livy для hello hello вывода должен возвращать ноль.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Вы должны получить выходные данные примерно toohello следующий фрагмент кода:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Обратите внимание на то, как последняя строка hello в выходных данных hello говорит **итог: 0**, который предлагает нет запущенных пакетов.

2. Теперь отправим пакетное задание. Следующий фрагмент кода Hello использует имя входного файла (input.txt) toopass hello jar и имя класса hello в качестве параметров. Если на компьютере следующие действия на компьютере Windows с помощью входного файла — hello, рекомендованный подход.
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Здравствуйте, параметры в файле hello **input.txt** определяется следующим образом:
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    Вы увидите примерно toohello выходные данные, следующий фрагмент кода:
   
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
   
    Обратите внимание на то, как последняя строка выходных данных hello hello говорит **состояние: запуск**. Кроме того, она включает параметр **id:0** — Здесь **0** — идентификатор пакета hello.

3. Теперь можно извлечь состояние hello этого конкретного пакета, используя идентификатор hello пакета.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Вы увидите примерно toohello выходные данные, следующий фрагмент кода:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hello выходных данных теперь указывается **состояние: успех**, который предлагает hello задания успешно завершена.

4. Если требуется, теперь можно удалить пакет hello.
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Вы увидите примерно toohello выходные данные, следующий фрагмент кода:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Последняя строка Hello hello выходных данных показаны hello пакета успешно удален. Удаление задания, пока она запущена, также разрывает hello задания. При удалении завершенного задания, успешно или нет, она полностью удаляется сведения о задании hello.

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a>Использование Livy Spark в кластерах HDInsight 3.5

Кластер HDInsight 3.5 по умолчанию запрещает использование файлы образцов данных tooaccess пути к локальному файлу или JAR-файлов. Мы рекомендуем вам toouse hello `wasb://` путь вместо tooaccess JAR-файлов и создавать образец данных файлов из кластера hello. Если вы хотите toouse локальный путь, необходимо обновить конфигурации Ambari hello соответствующим образом. toodo так:

1. Откройте портал Ambari toohello для кластера hello. Hello Ambari веб-интерфейса можно найти в кластер HDInsight адресу https://**ИМЯ_КЛАСТЕРА**. azurehdidnsight.net, где ИМЯ_КЛАСТЕРА hello имя кластера.

2. Hello навигации слева, щелкните **Livy**, а затем нажмите кнопку **Configs**.

3. В разделе **по умолчанию livy** добавьте имя свойства hello `livy.file.local-dir-whitelist` и задать его значение слишком**«/»** Если требуется, чтобы система toofile tooallow полный доступ. Если требуется tooallow доступ только tooa конкретного каталога, предоставляют hello путь toothat каталог в качестве значений hello.

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>Отправка задания Livy для кластера в пределах виртуальной сети Azure

При подключении tooan кластер HDInsight Spark из в виртуальной сети Azure, могут напрямую подключаться tooLivy на кластере hello. В этом случае hello URL-адрес конечной точки Livy `http://<IP address of hello headnode>:8998/batches`. Здесь **8998** hello порт, на котором выполняется Livy на головному узлу кластера hello. Дополнительные сведения о доступе к службам через порты, не являющиеся общедоступными, см. в разделе [Порты, используемые службами Hadoop в HDInsight](hdinsight-hadoop-port-settings-for-services.md).

## <a name="troubleshooting"></a>Устранение неполадок

Ниже приведены некоторые проблемы, которые вы можете столкнуться при использовании Livy для удаленного задания отправки tooSpark кластеров.

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a>Использование внешних jar из дополнительного хранилища hello не поддерживается

**Проблема:** при Livy Spark задания ссылается на внешние JAR-файл из учетной записи hello дополнительное хранилище, связанное с кластером hello, hello задание завершается ошибкой.

**Решение:** убедитесь в том, что jar hello toouse доступно в хранилище по умолчанию hello, связанное с кластером HDInsight hello.





## <a name="next-step"></a>Дальнейшие действия

* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)

