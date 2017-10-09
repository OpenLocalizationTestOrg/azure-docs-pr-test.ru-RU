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
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="e2760-104">Устранение неполадок в Spark с помощью Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2760-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="e2760-105">Дополнительные сведения о hello основные проблемы и способы их устранения при работе с Apache Spark полезных данных в Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="e2760-105">Learn about hello top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="e2760-106">Как настроить приложение Spark с помощью Ambari в кластерах?</span><span class="sxs-lookup"><span data-stu-id="e2760-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="e2760-107">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="e2760-107">Resolution steps</span></span>

<span data-ttu-id="e2760-108">в HDInsight ранее установленные значения конфигурации Hello для выполнения данной процедуры.</span><span class="sxs-lookup"><span data-stu-id="e2760-108">hello configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="e2760-109">. в разделе конфигурации Spark требуются значения в набор и toowhat toobe, toodetermine [в каком случае Spark исключение приложения OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="e2760-109">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="e2760-110">В списке hello кластеров выберите **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="e2760-110">In hello list of clusters, select **Spark2**.</span></span>

    ![Выбор кластера из списка](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="e2760-112">Выберите hello **Configs** вкладки.</span><span class="sxs-lookup"><span data-stu-id="e2760-112">Select hello **Configs** tab.</span></span>

    ![Перейдите на вкладку конфигураций hello](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="e2760-114">В списке hello конфигураций, выберите **настраиваемый spark2 значения по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="e2760-114">In hello list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Выбор конфигурации custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="e2760-116">Найдите параметр необходимы tooadjust, такие как значения hello **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="e2760-116">Look for hello value setting that you need tooadjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="e2760-117">В этом случае hello значение **4608m** слишком велико.</span><span class="sxs-lookup"><span data-stu-id="e2760-117">In this case, hello value of **4608m** is too high.</span></span>

    ![Выберите поле spark.executor.memory hello](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="e2760-119">Набор hello значение toohello рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="e2760-119">Set hello value toohello recommended setting.</span></span> <span data-ttu-id="e2760-120">Здравствуйте, значение **2048m** рекомендуется использовать для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="e2760-120">hello value **2048m** is recommended for this setting.</span></span>

    ![Измените значение too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="e2760-122">Сохраните значение hello, а затем сохраните конфигурацию hello.</span><span class="sxs-lookup"><span data-stu-id="e2760-122">Save hello value, and then save hello configuration.</span></span> <span data-ttu-id="e2760-123">Выберите в панели инструментов hello **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e2760-123">On hello toolbar, select **Save**.</span></span>

    ![Сохранить приветствия и конфигурации](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="e2760-125">Если нужно будет пересмотреть какую-либо конфигурацию, вы получите оповещение.</span><span class="sxs-lookup"><span data-stu-id="e2760-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="e2760-126">Обратите внимание, hello элементов, а затем выберите **продолжить в любом случае**.</span><span class="sxs-lookup"><span data-stu-id="e2760-126">Note hello items, and then select **Proceed Anyway**.</span></span> 

    ![Нажатие кнопки "Proceed Anyway" (Продолжить)](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="e2760-128">Записи об изменениях конфигурации hello заметку, а затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e2760-128">Write a note about hello configuration changes, and then select **Save**.</span></span>

    ![Введите примечание о внесенные изменения hello](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="e2760-130">При каждом сохранении конфигурации появится toorestart hello службы.</span><span class="sxs-lookup"><span data-stu-id="e2760-130">Whenever a configuration is saved, you are prompted toorestart hello service.</span></span> <span data-ttu-id="e2760-131">Нажмите кнопку **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="e2760-131">Select **Restart**.</span></span>

    ![Нажатие кнопки "Перезапустить"](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="e2760-133">Подтвердите перезапуск hello.</span><span class="sxs-lookup"><span data-stu-id="e2760-133">Confirm hello restart.</span></span>

    ![Нажатие кнопки "Confirm Restart All" (Подтвердить перезапуск всех)](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="e2760-135">Можно просмотреть выполняющиеся процессы hello.</span><span class="sxs-lookup"><span data-stu-id="e2760-135">You can review hello processes that are running.</span></span>

    ![Просмотр запущенных процессов](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="e2760-137">Вы можете добавить конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e2760-137">You can add configurations.</span></span> <span data-ttu-id="e2760-138">В списке hello конфигураций, выберите **настраиваемый spark2 значения по умолчанию**и выберите **добавить свойство**.</span><span class="sxs-lookup"><span data-stu-id="e2760-138">In hello list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Выбор "Добавить свойство"](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="e2760-140">Определите новое свойство.</span><span class="sxs-lookup"><span data-stu-id="e2760-140">Define a new property.</span></span> <span data-ttu-id="e2760-141">Можно определить одно свойство, используя диалоговое окно для конкретных параметров, таких как тип данных hello.</span><span class="sxs-lookup"><span data-stu-id="e2760-141">You can define a single property by using a dialog box for specific settings such as hello data type.</span></span> <span data-ttu-id="e2760-142">Или вы можете определить несколько свойств с одним определением на строку.</span><span class="sxs-lookup"><span data-stu-id="e2760-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="e2760-143">В этом примере hello **spark.driver.memory** определяется свойство со значением **4g**.</span><span class="sxs-lookup"><span data-stu-id="e2760-143">In this example, hello **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Определение нового свойства](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="e2760-145">Сохранить конфигурацию hello и затем перезапустите службу hello, как описано в шаге 6 и 7.</span><span class="sxs-lookup"><span data-stu-id="e2760-145">Save hello configuration, and then restart hello service as described in steps 6 and 7.</span></span>

<span data-ttu-id="e2760-146">Эти изменения распространяются кластера, но может быть переопределен при отправке задания Spark hello.</span><span class="sxs-lookup"><span data-stu-id="e2760-146">These changes are cluster-wide but can be overridden when you submit hello Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="e2760-147">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="e2760-147">Additional reading</span></span>

[<span data-ttu-id="e2760-148">Отправка задания Spark в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2760-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="e2760-149">Как настроить приложение Spark с помощью Jupyter Notebook в кластерах?</span><span class="sxs-lookup"><span data-stu-id="e2760-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="e2760-150">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="e2760-150">Resolution steps</span></span>

1. <span data-ttu-id="e2760-151">. в разделе конфигурации Spark требуются значения в набор и toowhat toobe, toodetermine [в каком случае Spark исключение приложения OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="e2760-151">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="e2760-152">В первой ячейке hello записной книжки Jupyter hello после hello **%% Настройка** директивы, задавать конфигурации Spark hello в допустимом формате JSON.</span><span class="sxs-lookup"><span data-stu-id="e2760-152">In hello first cell of hello Jupyter notebook, after hello **%%configure** directive, specify hello Spark configurations in valid JSON format.</span></span> <span data-ttu-id="e2760-153">При необходимости измените hello фактические значения:</span><span class="sxs-lookup"><span data-stu-id="e2760-153">Change hello actual values as necessary:</span></span>

    ![Добавление конфигурации](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="e2760-155">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="e2760-155">Additional reading</span></span>

[<span data-ttu-id="e2760-156">Отправка задания Spark в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2760-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="e2760-157">Как настроить приложение Spark с помощью Livy в кластерах?</span><span class="sxs-lookup"><span data-stu-id="e2760-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="e2760-158">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="e2760-158">Resolution steps</span></span>

1. <span data-ttu-id="e2760-159">. в разделе конфигурации Spark требуются значения в набор и toowhat toobe, toodetermine [в каком случае Spark исключение приложения OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="e2760-159">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="e2760-160">Отправка tooLivy приложения hello Spark с помощью клиента REST, например cURL.</span><span class="sxs-lookup"><span data-stu-id="e2760-160">Submit hello Spark application tooLivy by using a REST client like cURL.</span></span> <span data-ttu-id="e2760-161">Используйте следующие команды аналогичные toohello.</span><span class="sxs-lookup"><span data-stu-id="e2760-161">Use a command similar toohello following.</span></span> <span data-ttu-id="e2760-162">При необходимости измените hello фактические значения:</span><span class="sxs-lookup"><span data-stu-id="e2760-162">Change hello actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="e2760-163">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="e2760-163">Additional reading</span></span>

[<span data-ttu-id="e2760-164">Отправка задания Spark в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2760-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="e2760-165">Как настроить приложение Spark с помощью spark-submit в кластерах?</span><span class="sxs-lookup"><span data-stu-id="e2760-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="e2760-166">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="e2760-166">Resolution steps</span></span>

1. <span data-ttu-id="e2760-167">. в разделе конфигурации Spark требуются значения в набор и toowhat toobe, toodetermine [в каком случае Spark исключение приложения OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="e2760-167">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="e2760-168">Запустите spark оболочки с помощью команды аналогичные toohello следующее.</span><span class="sxs-lookup"><span data-stu-id="e2760-168">Launch spark-shell by using a command similar toohello following.</span></span> <span data-ttu-id="e2760-169">При необходимости измените hello фактическое значение hello конфигураций:</span><span class="sxs-lookup"><span data-stu-id="e2760-169">Change hello actual value of hello configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="e2760-170">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="e2760-170">Additional reading</span></span>

[<span data-ttu-id="e2760-171">Отправка задания Spark в кластерах HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2760-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="e2760-172">Что вызывает в приложении Spark исключение OutOfMemoryError?</span><span class="sxs-lookup"><span data-stu-id="e2760-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="e2760-173">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="e2760-173">Detailed description</span></span>

<span data-ttu-id="e2760-174">Hello Spark приложения завершается с hello следующие типы неперехваченных исключений:</span><span class="sxs-lookup"><span data-stu-id="e2760-174">hello Spark application fails, with hello following types of uncaught exceptions:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="e2760-175">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="e2760-175">Probable cause</span></span>

<span data-ttu-id="e2760-176">Hello наиболее вероятной причиной этого исключения — что не хватает памяти в куче выделяется toohello виртуальных машин Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="e2760-176">hello most likely cause of this exception is that not enough heap memory is allocated toohello Java virtual machines (JVMs).</span></span> <span data-ttu-id="e2760-177">Эти JVM запускаются непосредственно в исполнителей и драйверы, или как часть hello Spark приложения.</span><span class="sxs-lookup"><span data-stu-id="e2760-177">These JVMs are launched as executors or drivers as part of hello Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="e2760-178">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="e2760-178">Resolution steps</span></span>

1. <span data-ttu-id="e2760-179">Определите максимальный размер hello данных hello Spark приложение обрабатывает hello.</span><span class="sxs-lookup"><span data-stu-id="e2760-179">Determine hello maximum size of hello data hello Spark application handles.</span></span> <span data-ttu-id="e2760-180">Можно сделать прогноз, на основе максимального размера hello hello входных данных, hello промежуточных данных, созданного путем преобразования входных данных hello и hello выходных данных, получаемая при приложения hello дополнительные преобразования hello промежуточные данные.</span><span class="sxs-lookup"><span data-stu-id="e2760-180">You can make a guess based on hello maximum size of hello input data, hello intermediate data that's produced by transforming hello input data, and hello output data that's produced when hello application is further transforming hello intermediate data.</span></span> <span data-ttu-id="e2760-181">Этот процесс может быть итеративным, если не удается предугадать начальное значение.</span><span class="sxs-lookup"><span data-stu-id="e2760-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="e2760-182">Убедитесь, что ты toouse имеет достаточно ресурсов с точки зрения памяти ядра tooaccommodate hello Spark приложения и кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e2760-182">Make sure that hello HDInsight cluster that you're going toouse has enough resources in terms of memory and cores tooaccommodate hello Spark application.</span></span> <span data-ttu-id="e2760-183">Это можно определить, просмотрев раздел метрики кластера hello hello YARN пользовательского интерфейса для значений hello объекта **используемая память** vs. **Memory Total** (Всего памяти), а также **VCores Used** (Используемые ядра VCore) и **VCores Total** (Всего ядер VCore).</span><span class="sxs-lookup"><span data-stu-id="e2760-183">You can determine this by viewing hello cluster metrics section of hello YARN UI for hello values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="e2760-184">Задания после Spark hello конфигураций tooappropriate значения, которые не должно превышать 90% доступной памяти hello и ядер.</span><span class="sxs-lookup"><span data-stu-id="e2760-184">Set hello following Spark configurations tooappropriate values, which should not exceed 90% of hello available memory and cores.</span></span> <span data-ttu-id="e2760-185">Hello значения должны быть в пределах требований к памяти hello hello Spark приложения:</span><span class="sxs-lookup"><span data-stu-id="e2760-185">hello values should be well within hello memory requirements of hello Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="e2760-186">tooget hello общая память, используемая все исполнители, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e2760-186">tooget hello total memory used by all executors, run hello following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="e2760-187">tooget hello использования памяти драйвером hello, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e2760-187">tooget hello total memory used by hello driver, run hello following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="e2760-188">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="e2760-188">Additional reading</span></span>

- [<span data-ttu-id="e2760-189">Раздел об управлении памятью Spark</span><span class="sxs-lookup"><span data-stu-id="e2760-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- <span data-ttu-id="e2760-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (Отладка приложения Spark в кластере HDInsight)</span><span class="sxs-lookup"><span data-stu-id="e2760-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)</span></span>

