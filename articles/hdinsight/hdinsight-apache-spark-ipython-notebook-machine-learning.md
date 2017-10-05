---
title: "Создание приложений машинного обучения Apache Spark в Azure HDInsight | Документация Майкрософт"
description: "Пошаговые инструкции по созданию приложения машинного обучения Apache Spark в кластерах HDInsight Spark с помощью записной книжки Jupyter"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 158ade4612104020e0231794e7123ea5cad6c459
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="4c2dd-103">Создание приложений машинного обучения Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c2dd-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="4c2dd-104">Узнайте о том, как создать приложение машинного обучения Apache Spark с помощью кластера Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-104">Learn how to build an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="4c2dd-105">В этой статье показано, как использовать записную книжку Jupyter с кластером для создания и тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-105">This article shows how to use the Jupyter notebook available with the cluster to build and test this application.</span></span> <span data-ttu-id="4c2dd-106">Приложение использует данные из примера файла HVAC.csv, который по умолчанию доступен на всех кластерах.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-106">The application uses the sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="4c2dd-107">**Предварительные требования:**</span><span class="sxs-lookup"><span data-stu-id="4c2dd-107">**Prerequisites:**</span></span>

<span data-ttu-id="4c2dd-108">Необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="4c2dd-108">You must have the following:</span></span>

* <span data-ttu-id="4c2dd-109">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="4c2dd-110">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4c2dd-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="4c2dd-111"><a name="data"></a>Общие сведения о наборе данных</span><span class="sxs-lookup"><span data-stu-id="4c2dd-111"><a name="data"></a>Understand the data set</span></span>
<span data-ttu-id="4c2dd-112">Прежде чем приступать к созданию приложения, рассмотрим структуру данных, для которых создается приложение, и тип анализа, который мы будем использовать в отношении данных.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-112">Before we start building the application, let us understand the structure of the data for which we build the application and the kind of analysis we will do on the data.</span></span> 

<span data-ttu-id="4c2dd-113">В этой статье мы используем пример файла данных **HVAC.csv** , доступный в учетной записи хранения Azure, которую вы связали с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-113">In this article, we use the sample **HVAC.csv** data file that is available in the Azure Storage account that you associated with the HDInsight cluster.</span></span> <span data-ttu-id="4c2dd-114">В этой учетной записи хранения файл находится в папке **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-114">Within the storage account, the file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="4c2dd-115">Скачайте и откройте CSV-файл, чтобы получить моментальный снимок данных.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-115">Download and open the CSV file to get a snapshot of the data.</span></span>  

<span data-ttu-id="4c2dd-116">![Моментальный снимок данных, используемых для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Моментальный снимок данных, используемых для примера машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="4c2dd-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="4c2dd-117">Это данные о целевой температуре и фактической температуре здания, в котором установлена система кондиционирования воздуха.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-117">The data shows the target temperature and the actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="4c2dd-118">Предположим, что в столбце **System** указан идентификатор системы, а в столбце **SystemAge** — срок эксплуатации системы кондиционирования в годах.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-118">Let's assume the **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span></span>

<span data-ttu-id="4c2dd-119">Эти сведения используются для прогнозирования того, будет ли температура здания выше или ниже относительно целевой температуры на основе идентификатора системы и ее возраста.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-119">We use this data to predict whether a building will be hotter or colder based on the target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="4c2dd-120"><a name="app"></a>Создание приложения машинного обучения Spark с помощью Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="4c2dd-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="4c2dd-121">В этом приложении мы используем конвейер машинного обучения Spark для выполнения классификации документов.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-121">In this application we use a Spark ML pipeline to perform a document classification.</span></span> <span data-ttu-id="4c2dd-122">В конвейере мы разбиваем документ на слова, преобразуем слова в вектор числовой функции и, наконец, создаем модель прогнозирования с помощью характеристического вектора и меток.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-122">In the pipeline, we split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span></span> <span data-ttu-id="4c2dd-123">Выполните следующие действия, чтобы создать приложение.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-123">Perform the following steps to create the application.</span></span>

1. <span data-ttu-id="4c2dd-124">На начальной панели [портала Azure](https://portal.azure.com/)щелкните элемент кластера Spark (если он закреплен на начальной панели).</span><span class="sxs-lookup"><span data-stu-id="4c2dd-124">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="4c2dd-125">Кроме того, вы можете перейти к кластеру, последовательно щелкнув **Просмотреть все** > **Кластеры HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-125">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="4c2dd-126">В колонке кластера Spark щелкните **Панель мониторинга кластера**, а затем выберите **Записная книжка Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-126">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="4c2dd-127">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-127">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4c2dd-128">Также можно открыть Jupyter Notebook для своего кластера, открыв следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-128">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="4c2dd-129">Замените **CLUSTERNAME** именем кластера:</span><span class="sxs-lookup"><span data-stu-id="4c2dd-129">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="4c2dd-130">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-130">Create a new notebook.</span></span> <span data-ttu-id="4c2dd-131">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="4c2dd-132">![Создание записной книжки Jupyter для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Создание записной книжки Jupyter для примера машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="4c2dd-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="4c2dd-133">Будет создана и открыта записная книжка с именем Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-133">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="4c2dd-134">Щелкните имя записной книжки в верхней части страницы сверху и введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-134">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="4c2dd-135">![Указание имени записной книжки для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Указание имени записной книжки для примера машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="4c2dd-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="4c2dd-136">Так как записная книжка была создана с помощью ядра PySpark, задавать контексты явно необязательно.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="4c2dd-137">Контексты Spark и Hive будут созданы автоматически при выполнении первой ячейки кода.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="4c2dd-138">Можно начать с импорта различных типов, необходимых для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-138">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="4c2dd-139">Вставьте следующий фрагмент кода в пустую ячейку и нажмите клавиши **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-139">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. <span data-ttu-id="4c2dd-140">Теперь необходимо загрузить данные (hvac.csv), проанализировать их и использовать эти данные для обучения модели.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-140">You must now load the data (hvac.csv), parse it, and use it to train the model.</span></span> <span data-ttu-id="4c2dd-141">Для этого необходимо определить функцию, которая проверяет, превышает ли значение фактической температуры здания значение целевой температуры.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-141">For this, you define a function that checks whether the actual temperature of the building is greater than the target temperature.</span></span> <span data-ttu-id="4c2dd-142">Если фактическая температура больше, то здание горячее (значение **1.0**).</span><span class="sxs-lookup"><span data-stu-id="4c2dd-142">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span></span> <span data-ttu-id="4c2dd-143">Если фактическая температура меньше, то здание холодное (значение **0.0**).</span><span class="sxs-lookup"><span data-stu-id="4c2dd-143">If the actual temperature is lesser, the building is cold, denoted by the value **0.0**.</span></span> 
   
    <span data-ttu-id="4c2dd-144">Вставьте следующий фрагмент кода в пустую ячейку и нажмите клавиши **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-144">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List the structure of data for better understanding. Because the data will be
        # loaded as an array, this structure makes it easy to understand what each element
        # in the array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses the raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load the raw HVAC.csv file, parse it using the function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="4c2dd-145">Настройте конвейер машинного обучения Spark, который состоит из трех частей: логического анализатора, hashingTF и lr.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-145">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="4c2dd-146">Дополнительные сведения о возможностях конвейера и о том, как он работает, см. в статье <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Конвейер машинного обучения Spark</a>.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="4c2dd-147">Вставьте следующий фрагмент кода в пустую ячейку и нажмите клавиши **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-147">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="4c2dd-148">Впишите конвейер в документ для обучения.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-148">Fit the pipeline to the training document.</span></span> <span data-ttu-id="4c2dd-149">Вставьте следующий фрагмент кода в пустую ячейку и нажмите клавиши **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-149">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="4c2dd-150">Проверьте, чтобы в документе для обучения имелась контрольная точка хода выполнения для приложения.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-150">Verify the training document to checkpoint your progress with the application.</span></span> <span data-ttu-id="4c2dd-151">Вставьте следующий фрагмент кода в пустую ячейку и нажмите клавиши **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-151">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="4c2dd-152">Результат должен быть аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="4c2dd-152">This should give the output similar to the following:</span></span>
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    <span data-ttu-id="4c2dd-153">Вернитесь и проверьте выходные данные со сведениями в необработанном CSV-файле.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-153">Go back and verify the output against the raw CSV file.</span></span> <span data-ttu-id="4c2dd-154">Например, в первой строке CSV-файла содержатся следующие данные:</span><span class="sxs-lookup"><span data-stu-id="4c2dd-154">For example, the first row the CSV file has this data:</span></span>

    <span data-ttu-id="4c2dd-155">![Моментальный снимок выходных данных для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Моментальный снимок выходных данных для примера машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="4c2dd-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="4c2dd-156">Обратите внимание на то, насколько фактическая температура меньше целевой, что свидетельствует о том, что здание холодное.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-156">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span></span> <span data-ttu-id="4c2dd-157">В выходных данных обучения видно, что значение в первой строке столбца **label** составляет **0,0**. Это означает, что в здании не тепло.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-157">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span></span>

1. <span data-ttu-id="4c2dd-158">Подготовьте набор данных, в отношении которого необходимо выполнить обученную модель.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-158">Prepare a data set to run the trained model against.</span></span> <span data-ttu-id="4c2dd-159">Для этого мы передадим идентификатор системы и ее возраст (значения в столбце **SystemInfo** в выходных данных обучения). После этого модель предскажет, станет ли в здании с этими идентификатором системы и возрастом теплее (значение 1,0) или холоднее (значение 0,0).</span><span class="sxs-lookup"><span data-stu-id="4c2dd-159">To do so, we would pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model would predict whether the building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="4c2dd-160">Вставьте следующий фрагмент кода в пустую ячейку и нажмите клавиши **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-160">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="4c2dd-161">Наконец, создайте прогнозы на основе тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-161">Finally, make predictions on the test data.</span></span> <span data-ttu-id="4c2dd-162">Вставьте следующий фрагмент кода в пустую ячейку и нажмите клавиши **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-162">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="4c2dd-163">Должен отобразиться результат, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="4c2dd-163">You should see an output similar to the following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="4c2dd-164">В первой строке прогноза видно, что при использовании системы кондиционирования с идентификатором 20 и возрастом 25 лет здание будет горячим (**прогноз = 1.0**).</span><span class="sxs-lookup"><span data-stu-id="4c2dd-164">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="4c2dd-165">Первое значение параметра DenseVector (0,49999) соответствует прогнозу 0,0, а второе значение (0,5001) — прогнозу 1,0.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-165">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span></span> <span data-ttu-id="4c2dd-166">В выходных данных видно, что, даже если второе значение лишь незначительно выше, модель показывает **прогноз = 1.0**.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-166">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="4c2dd-167">Завершив работу с приложением, следует закрыть записную книжку, чтобы освободить ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-167">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="4c2dd-168">Для этого в записной книжке в меню **Файл** выберите пункт **Close and Halt** (Закрыть и остановить).</span><span class="sxs-lookup"><span data-stu-id="4c2dd-168">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="4c2dd-169">Это завершит работу записной книжки и закроет ее.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-169">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="4c2dd-170"><a name="anaconda"></a>Использование библиотеки scikit-learn Anaconda для машинного обучения Spark</span><span class="sxs-lookup"><span data-stu-id="4c2dd-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="4c2dd-171">Кластеры Apache Spark в HDInsight включают библиотеки Anaconda.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="4c2dd-172">Они также включают библиотеку **scikit-learn** для машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-172">This also includes the **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="4c2dd-173">Кроме того, библиотека включает различные наборы данных, которые можно использовать для создания примеров приложений прямо в записной книжке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="4c2dd-173">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="4c2dd-174">Примеры использования библиотеки scikit-learn см. на странице: [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="4c2dd-174">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="4c2dd-175"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="4c2dd-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="4c2dd-176">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c2dd-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="4c2dd-177">Сценарии</span><span class="sxs-lookup"><span data-stu-id="4c2dd-177">Scenarios</span></span>
* [<span data-ttu-id="4c2dd-178">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="4c2dd-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="4c2dd-179">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="4c2dd-179">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="4c2dd-180">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="4c2dd-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="4c2dd-181">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c2dd-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="4c2dd-182">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="4c2dd-182">Create and run applications</span></span>
* [<span data-ttu-id="4c2dd-183">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="4c2dd-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="4c2dd-184">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="4c2dd-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="4c2dd-185">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="4c2dd-185">Tools and extensions</span></span>
* [<span data-ttu-id="4c2dd-186">Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="4c2dd-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="4c2dd-187">Удаленная отладка приложений Spark в кластере HDInsight Spark Linux с помощью подключаемого модуля средств HDInsight для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="4c2dd-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="4c2dd-188">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c2dd-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="4c2dd-189">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c2dd-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="4c2dd-190">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="4c2dd-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="4c2dd-191">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="4c2dd-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="4c2dd-192">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="4c2dd-192">Manage resources</span></span>
* [<span data-ttu-id="4c2dd-193">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c2dd-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="4c2dd-194">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="4c2dd-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
