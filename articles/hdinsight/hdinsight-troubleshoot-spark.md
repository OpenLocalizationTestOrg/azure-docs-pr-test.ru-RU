---
title: "Устранение неполадок в Spark с помощью Azure HDInsight | Документация Майкрософт"
description: "Получите ответы на распространенные вопросы о работе с Apache Spark и Azure HDInsight."
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
ms.openlocfilehash: cfed5f0f4f703821e83e3d365810c0e5ad22f035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="230fd-104">Устранение неполадок в Spark с помощью Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="230fd-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="230fd-105">Ознакомьтесь с основными проблемами и их разрешением при работе с полезными данными Apache Spark в Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="230fd-105">Learn about the top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="230fd-106">Как настроить приложение Spark с помощью Ambari в кластерах?</span><span class="sxs-lookup"><span data-stu-id="230fd-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="230fd-107">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="230fd-107">Resolution steps</span></span>

<span data-ttu-id="230fd-108">Значения конфигурации для этой процедуры были предварительно заданы в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="230fd-108">The configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="230fd-109">Чтобы определить, какие конфигурации Spark нужно настроить и с какими значениями, см. раздел [Что вызывает в приложении Spark исключение OutOfMemoryError?](#what-causes-a-spark-application-outofmemoryerror-exception)</span><span class="sxs-lookup"><span data-stu-id="230fd-109">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="230fd-110">В списке кластеров выберите **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="230fd-110">In the list of clusters, select **Spark2**.</span></span>

    ![Выбор кластера из списка](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="230fd-112">Выберите вкладку **Конфигурации** .</span><span class="sxs-lookup"><span data-stu-id="230fd-112">Select the **Configs** tab.</span></span>

    ![Выбор вкладки "Конфигурации"](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="230fd-114">В списке конфигураций выберите **Custom-spark2-defaults**.</span><span class="sxs-lookup"><span data-stu-id="230fd-114">In the list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Выбор конфигурации custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="230fd-116">Найдите параметр значения, который необходимо настроить, например **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="230fd-116">Look for the value setting that you need to adjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="230fd-117">В этом случае значение **4608m** слишком высокое.</span><span class="sxs-lookup"><span data-stu-id="230fd-117">In this case, the value of **4608m** is too high.</span></span>

    ![Выбор поля spark.executor.memory](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="230fd-119">Задайте для этого параметра рекомендуемое значение.</span><span class="sxs-lookup"><span data-stu-id="230fd-119">Set the value to the recommended setting.</span></span> <span data-ttu-id="230fd-120">Рекомендуется использовать значение **2048m**.</span><span class="sxs-lookup"><span data-stu-id="230fd-120">The value **2048m** is recommended for this setting.</span></span>

    ![Изменение значения на 2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="230fd-122">Сохраните это значение, а затем сохраните конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="230fd-122">Save the value, and then save the configuration.</span></span> <span data-ttu-id="230fd-123">На панели инструментов нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="230fd-123">On the toolbar, select **Save**.</span></span>

    ![Сохранение параметра и конфигурации](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="230fd-125">Если нужно будет пересмотреть какую-либо конфигурацию, вы получите оповещение.</span><span class="sxs-lookup"><span data-stu-id="230fd-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="230fd-126">Проверьте элементы, а затем нажмите кнопку **Proceed Anyway** (Продолжить).</span><span class="sxs-lookup"><span data-stu-id="230fd-126">Note the items, and then select **Proceed Anyway**.</span></span> 

    ![Нажатие кнопки "Proceed Anyway" (Продолжить)](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="230fd-128">Запишите примечание об изменениях конфигурации, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="230fd-128">Write a note about the configuration changes, and then select **Save**.</span></span>

    ![Примечание об изменениях](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="230fd-130">При каждом сохранении конфигурации вам будет предложено перезапустить службу.</span><span class="sxs-lookup"><span data-stu-id="230fd-130">Whenever a configuration is saved, you are prompted to restart the service.</span></span> <span data-ttu-id="230fd-131">Нажмите кнопку **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="230fd-131">Select **Restart**.</span></span>

    ![Нажатие кнопки "Перезапустить"](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="230fd-133">Подтвердите перезапуск.</span><span class="sxs-lookup"><span data-stu-id="230fd-133">Confirm the restart.</span></span>

    ![Нажатие кнопки "Confirm Restart All" (Подтвердить перезапуск всех)](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="230fd-135">Вы можете просмотреть запущенные процессы.</span><span class="sxs-lookup"><span data-stu-id="230fd-135">You can review the processes that are running.</span></span>

    ![Просмотр запущенных процессов](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="230fd-137">Вы можете добавить конфигурации.</span><span class="sxs-lookup"><span data-stu-id="230fd-137">You can add configurations.</span></span> <span data-ttu-id="230fd-138">В списке конфигураций выберите **Custom-spark2-defaults**, а затем щелкните **Добавить свойство**.</span><span class="sxs-lookup"><span data-stu-id="230fd-138">In the list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Выбор "Добавить свойство"](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="230fd-140">Определите новое свойство.</span><span class="sxs-lookup"><span data-stu-id="230fd-140">Define a new property.</span></span> <span data-ttu-id="230fd-141">Вы можете определить отдельное свойство с помощью диалогового окна для определенных параметров, например тип данных.</span><span class="sxs-lookup"><span data-stu-id="230fd-141">You can define a single property by using a dialog box for specific settings such as the data type.</span></span> <span data-ttu-id="230fd-142">Или вы можете определить несколько свойств с одним определением на строку.</span><span class="sxs-lookup"><span data-stu-id="230fd-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="230fd-143">В этом примере свойство **spark.driver.memory** определяется со значением **4 ГБ**.</span><span class="sxs-lookup"><span data-stu-id="230fd-143">In this example, the **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Определение нового свойства](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="230fd-145">Сохраните конфигурацию и перезапустите службу, как описано на шагах 6 и 7.</span><span class="sxs-lookup"><span data-stu-id="230fd-145">Save the configuration, and then restart the service as described in steps 6 and 7.</span></span>

<span data-ttu-id="230fd-146">Эти изменения применяются на уровне кластера, но их можно переопределить при отправке задания Spark.</span><span class="sxs-lookup"><span data-stu-id="230fd-146">These changes are cluster-wide but can be overridden when you submit the Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="230fd-147">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="230fd-147">Additional reading</span></span>

[<span data-ttu-id="230fd-148">Отправка задания Spark в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="230fd-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="230fd-149">Как настроить приложение Spark с помощью Jupyter Notebook в кластерах?</span><span class="sxs-lookup"><span data-stu-id="230fd-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="230fd-150">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="230fd-150">Resolution steps</span></span>

1. <span data-ttu-id="230fd-151">Чтобы определить, какие конфигурации Spark нужно настроить и с какими значениями, см. раздел [Что вызывает в приложении Spark исключение OutOfMemoryError?](#what-causes-a-spark-application-outofmemoryerror-exception)</span><span class="sxs-lookup"><span data-stu-id="230fd-151">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="230fd-152">Укажите конфигурации Spark в допустимом формате JSON в первой ячейке Jupyter Notebook после директивы **%%configure**.</span><span class="sxs-lookup"><span data-stu-id="230fd-152">In the first cell of the Jupyter notebook, after the **%%configure** directive, specify the Spark configurations in valid JSON format.</span></span> <span data-ttu-id="230fd-153">При необходимости измените фактические значения:</span><span class="sxs-lookup"><span data-stu-id="230fd-153">Change the actual values as necessary:</span></span>

    ![Добавление конфигурации](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="230fd-155">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="230fd-155">Additional reading</span></span>

[<span data-ttu-id="230fd-156">Отправка задания Spark в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="230fd-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="230fd-157">Как настроить приложение Spark с помощью Livy в кластерах?</span><span class="sxs-lookup"><span data-stu-id="230fd-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="230fd-158">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="230fd-158">Resolution steps</span></span>

1. <span data-ttu-id="230fd-159">Чтобы определить, какие конфигурации Spark нужно настроить и с какими значениями, см. раздел [Что вызывает в приложении Spark исключение OutOfMemoryError?](#what-causes-a-spark-application-outofmemoryerror-exception)</span><span class="sxs-lookup"><span data-stu-id="230fd-159">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="230fd-160">Отправьте приложение Spark в Livy с помощью клиента REST, например cURL.</span><span class="sxs-lookup"><span data-stu-id="230fd-160">Submit the Spark application to Livy by using a REST client like cURL.</span></span> <span data-ttu-id="230fd-161">Используйте команду, аналогичную приведенной ниже.</span><span class="sxs-lookup"><span data-stu-id="230fd-161">Use a command similar to the following.</span></span> <span data-ttu-id="230fd-162">При необходимости измените фактические значения:</span><span class="sxs-lookup"><span data-stu-id="230fd-162">Change the actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="230fd-163">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="230fd-163">Additional reading</span></span>

[<span data-ttu-id="230fd-164">Отправка задания Spark в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="230fd-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="230fd-165">Как настроить приложение Spark с помощью spark-submit в кластерах?</span><span class="sxs-lookup"><span data-stu-id="230fd-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="230fd-166">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="230fd-166">Resolution steps</span></span>

1. <span data-ttu-id="230fd-167">Чтобы определить, какие конфигурации Spark нужно настроить и с какими значениями, см. раздел [Что вызывает в приложении Spark исключение OutOfMemoryError?](#what-causes-a-spark-application-outofmemoryerror-exception)</span><span class="sxs-lookup"><span data-stu-id="230fd-167">To determine which Spark configurations need to be set and to what values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="230fd-168">Запустите оболочку Spark с помощью команды, аналогичной приведенной ниже.</span><span class="sxs-lookup"><span data-stu-id="230fd-168">Launch spark-shell by using a command similar to the following.</span></span> <span data-ttu-id="230fd-169">При необходимости измените фактические значения конфигураций:</span><span class="sxs-lookup"><span data-stu-id="230fd-169">Change the actual value of the configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="230fd-170">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="230fd-170">Additional reading</span></span>

[<span data-ttu-id="230fd-171">Отправка задания Spark в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="230fd-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="230fd-172">Что вызывает в приложении Spark исключение OutOfMemoryError?</span><span class="sxs-lookup"><span data-stu-id="230fd-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="230fd-173">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="230fd-173">Detailed description</span></span>

<span data-ttu-id="230fd-174">Сбой приложения Spark со следующими типами неперехваченных исключений:</span><span class="sxs-lookup"><span data-stu-id="230fd-174">The Spark application fails, with the following types of uncaught exceptions:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="230fd-175">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="230fd-175">Probable cause</span></span>

<span data-ttu-id="230fd-176">Наиболее вероятной причиной этого исключения является нехватка памяти кучи, выделенной для виртуальных машин Java.</span><span class="sxs-lookup"><span data-stu-id="230fd-176">The most likely cause of this exception is that not enough heap memory is allocated to the Java virtual machines (JVMs).</span></span> <span data-ttu-id="230fd-177">Эти виртуальные машины Java запускаются как исполнители или драйверы в рамках приложения Spark.</span><span class="sxs-lookup"><span data-stu-id="230fd-177">These JVMs are launched as executors or drivers as part of the Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="230fd-178">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="230fd-178">Resolution steps</span></span>

1. <span data-ttu-id="230fd-179">Определите максимальный объем данных, которые обрабатывает приложение Spark.</span><span class="sxs-lookup"><span data-stu-id="230fd-179">Determine the maximum size of the data the Spark application handles.</span></span> <span data-ttu-id="230fd-180">Это значение можно предугадать, исходя из максимального размера входных данных, промежуточных данных, создаваемых при преобразовании входных данных, и выходных данных, получаемых при дальнейшем преобразовании промежуточных данных приложением.</span><span class="sxs-lookup"><span data-stu-id="230fd-180">You can make a guess based on the maximum size of the input data, the intermediate data that's produced by transforming the input data, and the output data that's produced when the application is further transforming the intermediate data.</span></span> <span data-ttu-id="230fd-181">Этот процесс может быть итеративным, если не удается предугадать начальное значение.</span><span class="sxs-lookup"><span data-stu-id="230fd-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="230fd-182">Убедитесь, что в кластере HDInsight, который будет использоваться, достаточно ресурсов, таких как память и количество ядер, для работы приложения Spark.</span><span class="sxs-lookup"><span data-stu-id="230fd-182">Make sure that the HDInsight cluster that you're going to use has enough resources in terms of memory and cores to accommodate the Spark application.</span></span> <span data-ttu-id="230fd-183">Это можно определить, просмотрев в разделе Cluster Metrics (Метрики кластера) пользовательского интерфейса YARN такие значения, как **Memory Used** (Используемая память) и **Memory Total** (Всего памяти), а также **VCores Used** (Используемые ядра VCore) и **VCores Total** (Всего ядер VCore).</span><span class="sxs-lookup"><span data-stu-id="230fd-183">You can determine this by viewing the cluster metrics section of the YARN UI for the values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="230fd-184">Задайте для параметров конфигурации Spark соответствующие значения, не превышающие 90 % доступной памяти и количества ядер.</span><span class="sxs-lookup"><span data-stu-id="230fd-184">Set the following Spark configurations to appropriate values, which should not exceed 90% of the available memory and cores.</span></span> <span data-ttu-id="230fd-185">Эти значения должны быть в пределах требований к объему памяти для приложения Spark:</span><span class="sxs-lookup"><span data-stu-id="230fd-185">The values should be well within the memory requirements of the Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="230fd-186">Чтобы получить общий объем памяти, используемый всеми исполнителями, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="230fd-186">To get the total memory used by all executors, run the following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="230fd-187">Чтобы получить общий объем памяти, используемый драйвером, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="230fd-187">To get the total memory used by the driver, run the following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="230fd-188">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="230fd-188">Additional reading</span></span>

- [<span data-ttu-id="230fd-189">Раздел об управлении памятью Spark</span><span class="sxs-lookup"><span data-stu-id="230fd-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- <span data-ttu-id="230fd-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (Отладка приложения Spark в кластере HDInsight)</span><span class="sxs-lookup"><span data-stu-id="230fd-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)</span></span>

