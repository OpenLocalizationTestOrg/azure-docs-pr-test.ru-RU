---
title: "aaaTroubleshoot Spark с помощью Azure HDInsight | Документы Microsoft"
description: "Ответы toocommon вопросов о работе с Apache Spark и Azure HDInsight."
keywords: "Azure HDInsight, Spark, часто задаваемые вопросы, руководство по устранению неполадок, распространенные проблемы, конфигурация приложения, Ambari"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a>Устранение неполадок в Spark с помощью Azure HDInsight

Дополнительные сведения о hello основные проблемы и способы их устранения при работе с Apache Spark полезных данных в Apache Ambari.

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a>Как настроить приложение Spark с помощью Ambari в кластерах?

### <a name="resolution-steps"></a>Способы устранения

в HDInsight ранее установленные значения конфигурации Hello для выполнения данной процедуры. . в разделе конфигурации Spark требуются значения в набор и toowhat toobe, toodetermine [в каком случае Spark исключение приложения OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception). 

1. В списке hello кластеров выберите **Spark2**.

    ![Выбор кластера из списка](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. Выберите hello **Configs** вкладки.

    ![Перейдите на вкладку конфигураций hello](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. В списке hello конфигураций, выберите **настраиваемый spark2 значения по умолчанию**.

    ![Выбор конфигурации custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. Найдите параметр необходимы tooadjust, такие как значения hello **spark.executor.memory**. В этом случае hello значение **4608m** слишком велико.

    ![Выберите поле spark.executor.memory hello](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. Набор hello значение toohello рекомендуется. Здравствуйте, значение **2048m** рекомендуется использовать для этого параметра.

    ![Измените значение too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. Сохраните значение hello, а затем сохраните конфигурацию hello. Выберите в панели инструментов hello **Сохранить**.

    ![Сохранить приветствия и конфигурации](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    Если нужно будет пересмотреть какую-либо конфигурацию, вы получите оповещение. Обратите внимание, hello элементов, а затем выберите **продолжить в любом случае**. 

    ![Нажатие кнопки "Proceed Anyway" (Продолжить)](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    Записи об изменениях конфигурации hello заметку, а затем выберите **Сохранить**.

    ![Введите примечание о внесенные изменения hello](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. При каждом сохранении конфигурации появится toorestart hello службы. Нажмите кнопку **Перезапустить**.

    ![Нажатие кнопки "Перезапустить"](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    Подтвердите перезапуск hello.

    ![Нажатие кнопки "Confirm Restart All" (Подтвердить перезапуск всех)](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    Можно просмотреть выполняющиеся процессы hello.

    ![Просмотр запущенных процессов](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. Вы можете добавить конфигурации. В списке hello конфигураций, выберите **настраиваемый spark2 значения по умолчанию**и выберите **добавить свойство**.

    ![Выбор "Добавить свойство"](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. Определите новое свойство. Можно определить одно свойство, используя диалоговое окно для конкретных параметров, таких как тип данных hello. Или вы можете определить несколько свойств с одним определением на строку. 

    В этом примере hello **spark.driver.memory** определяется свойство со значением **4g**.

    ![Определение нового свойства](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. Сохранить конфигурацию hello и затем перезапустите службу hello, как описано в шаге 6 и 7.

Эти изменения распространяются кластера, но может быть переопределен при отправке задания Spark hello.

### <a name="additional-reading"></a>Дополнительные материалы

[Отправка задания Spark в кластерах HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a>Как настроить приложение Spark с помощью Jupyter Notebook в кластерах?

### <a name="resolution-steps"></a>Способы устранения

1. . в разделе конфигурации Spark требуются значения в набор и toowhat toobe, toodetermine [в каком случае Spark исключение приложения OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).

2. В первой ячейке hello записной книжки Jupyter hello после hello **%% Настройка** директивы, задавать конфигурации Spark hello в допустимом формате JSON. При необходимости измените hello фактические значения:

    ![Добавление конфигурации](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a>Дополнительные материалы

[Отправка задания Spark в кластерах HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a>Как настроить приложение Spark с помощью Livy в кластерах?

### <a name="resolution-steps"></a>Способы устранения

1. . в разделе конфигурации Spark требуются значения в набор и toowhat toobe, toodetermine [в каком случае Spark исключение приложения OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception). 

2. Отправка tooLivy приложения hello Spark с помощью клиента REST, например cURL. Используйте следующие команды аналогичные toohello. При необходимости измените hello фактические значения:

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a>Дополнительные материалы

[Отправка задания Spark в кластерах HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a>Как настроить приложение Spark с помощью spark-submit в кластерах?

### <a name="resolution-steps"></a>Способы устранения

1. . в разделе конфигурации Spark требуются значения в набор и toowhat toobe, toodetermine [в каком случае Spark исключение приложения OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Запустите spark оболочки с помощью команды аналогичные toohello следующее. При необходимости измените hello фактическое значение hello конфигураций: 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a>Дополнительные материалы

[Отправка задания Spark в кластерах HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a>Что вызывает в приложении Spark исключение OutOfMemoryError?

### <a name="detailed-description"></a>Подробное описание

Hello Spark приложения завершается с hello следующие типы неперехваченных исключений:

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a>Возможные причины

Hello наиболее вероятной причиной этого исключения — что не хватает памяти в куче выделяется toohello виртуальных машин Java (JVM). Эти JVM запускаются непосредственно в исполнителей и драйверы, или как часть hello Spark приложения. 

### <a name="resolution-steps"></a>Способы устранения

1. Определите максимальный размер hello данных hello Spark приложение обрабатывает hello. Можно сделать прогноз, на основе максимального размера hello hello входных данных, hello промежуточных данных, созданного путем преобразования входных данных hello и hello выходных данных, получаемая при приложения hello дополнительные преобразования hello промежуточные данные. Этот процесс может быть итеративным, если не удается предугадать начальное значение. 

2. Убедитесь, что ты toouse имеет достаточно ресурсов с точки зрения памяти ядра tooaccommodate hello Spark приложения и кластера HDInsight hello. Это можно определить, просмотрев раздел метрики кластера hello hello YARN пользовательского интерфейса для значений hello объекта **используемая память** vs. **Memory Total** (Всего памяти), а также **VCores Used** (Используемые ядра VCore) и **VCores Total** (Всего ядер VCore).

3. Задания после Spark hello конфигураций tooappropriate значения, которые не должно превышать 90% доступной памяти hello и ядер. Hello значения должны быть в пределах требований к памяти hello hello Spark приложения: 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    tooget hello общая память, используемая все исполнители, запустите hello следующую команду: 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    tooget hello использования памяти драйвером hello, запустите hello следующую команду:
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a>Дополнительные материалы

- [Раздел об управлении памятью Spark](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (Отладка приложения Spark в кластере HDInsight)

