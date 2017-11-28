---
title: "aaaBuild Apache Spark машинного самообучения, приложений на Azure HDInsight | Документы Microsoft"
description: "Пошаговые инструкции по как toobuild Apache Spark машинного самообучения, приложения на HDInsight Spark кластеры, использующие книжке Jupyter"
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
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="b2377-103">Создание приложений машинного обучения Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2377-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="b2377-104">Узнайте, как toobuild приложения Apache Spark машины обучения с помощью Spark кластера на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2377-104">Learn how toobuild an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="b2377-105">В этой статье описывается, как toouse hello книжке Jupyter, доступные с toobuild кластера hello и проверки приложения.</span><span class="sxs-lookup"><span data-stu-id="b2377-105">This article shows how toouse hello Jupyter notebook available with hello cluster toobuild and test this application.</span></span> <span data-ttu-id="b2377-106">Hello приложение использует данные HVAC.csv образец hello, которая доступна во всех кластерах по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b2377-106">hello application uses hello sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="b2377-107">**Предварительные требования:**</span><span class="sxs-lookup"><span data-stu-id="b2377-107">**Prerequisites:**</span></span>

<span data-ttu-id="b2377-108">Необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="b2377-108">You must have hello following:</span></span>

* <span data-ttu-id="b2377-109">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2377-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b2377-110">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b2377-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="b2377-111"><a name="data"></a>Понимать hello набора данных</span><span class="sxs-lookup"><span data-stu-id="b2377-111"><a name="data"></a>Understand hello data set</span></span>
<span data-ttu-id="b2377-112">Прежде чем начать создание приложения hello, сообщите нам понять структуру hello hello данных, для которого строится приложение hello и hello тип анализа, который мы выполним hello данных.</span><span class="sxs-lookup"><span data-stu-id="b2377-112">Before we start building hello application, let us understand hello structure of hello data for which we build hello application and hello kind of analysis we will do on hello data.</span></span> 

<span data-ttu-id="b2377-113">В этой статье мы используем образец hello **HVAC.csv** файла данных, доступные в учетной записи хранилища Azure, связанных с кластером HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="b2377-113">In this article, we use hello sample **HVAC.csv** data file that is available in hello Azure Storage account that you associated with hello HDInsight cluster.</span></span> <span data-ttu-id="b2377-114">В учетной записи хранилища hello, находится в файле hello **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="b2377-114">Within hello storage account, hello file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="b2377-115">Загрузите и откройте tooget файл CSV hello hello данные моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="b2377-115">Download and open hello CSV file tooget a snapshot of hello data.</span></span>  

<span data-ttu-id="b2377-116">![Моментальный снимок данных, используемых для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Моментальный снимок данных, используемых для примера машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="b2377-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="b2377-117">Hello данных показаны температуры целевой hello и hello фактическое температуры здания, имеющий Кондиционирования систем.</span><span class="sxs-lookup"><span data-stu-id="b2377-117">hello data shows hello target temperature and hello actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="b2377-118">Предположим, что hello **системы** столбец представляет системный идентификатор hello и hello **SystemAge** столбец представляет hello число лет, система Кондиционирования hello находилось в месте на построение hello.</span><span class="sxs-lookup"><span data-stu-id="b2377-118">Let's assume hello **System** column represents hello system ID and hello **SystemAge** column represents hello number of years hello HVAC system has been in place at hello building.</span></span>

<span data-ttu-id="b2377-119">Мы используем этот toopredict данных здания будут ли еще важнее или colder основываться на целевой температура hello, заданного системой идентификатор и возраст системы.</span><span class="sxs-lookup"><span data-stu-id="b2377-119">We use this data toopredict whether a building will be hotter or colder based on hello target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="b2377-120"><a name="app"></a>Создание приложения машинного обучения Spark с помощью Spark MLlib</span><span class="sxs-lookup"><span data-stu-id="b2377-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="b2377-121">В этом приложении мы используем tooperform конвейера Spark ML классификация документов.</span><span class="sxs-lookup"><span data-stu-id="b2377-121">In this application we use a Spark ML pipeline tooperform a document classification.</span></span> <span data-ttu-id="b2377-122">Конвейера hello мы разбивается на слова hello документа, преобразовать в числовой компонент вектор слова hello и наконец создать модель прогнозирования hello векторов признаков и меток.</span><span class="sxs-lookup"><span data-stu-id="b2377-122">In hello pipeline, we split hello document into words, convert hello words into a numerical feature vector, and finally build a prediction model using hello feature vectors and labels.</span></span> <span data-ttu-id="b2377-123">Выполните следующие шаги toocreate hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b2377-123">Perform hello following steps toocreate hello application.</span></span>

1. <span data-ttu-id="b2377-124">Из hello [портала Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели).</span><span class="sxs-lookup"><span data-stu-id="b2377-124">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="b2377-125">Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b2377-125">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="b2377-126">Из колонки кластера Spark hello, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **книжке Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="b2377-126">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="b2377-127">При появлении запроса введите учетные данные администратора hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="b2377-127">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b2377-128">Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="b2377-128">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="b2377-129">Замените **CLUSTERNAME** с hello имя кластера:</span><span class="sxs-lookup"><span data-stu-id="b2377-129">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="b2377-130">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="b2377-130">Create a new notebook.</span></span> <span data-ttu-id="b2377-131">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="b2377-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="b2377-132">![Создание записной книжки Jupyter для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Создание записной книжки Jupyter для примера машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="b2377-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="b2377-133">Создается и открывается с именем hello Untitled.pynb новый блокнот.</span><span class="sxs-lookup"><span data-stu-id="b2377-133">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="b2377-134">Щелкните имя записной книжки hello вверху hello и введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="b2377-134">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="b2377-135">![Указание имени записной книжки для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Указание имени записной книжки для примера машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="b2377-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="b2377-136">Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом.</span><span class="sxs-lookup"><span data-stu-id="b2377-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="b2377-137">контексты Spark и Hive Hello автоматически создается автоматически при выполнении первой ячейке кода hello.</span><span class="sxs-lookup"><span data-stu-id="b2377-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="b2377-138">Можно запустить, импортировав hello типы, необходимые для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="b2377-138">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="b2377-139">Вставьте следующий фрагмент кода в пустой ячейке hello и нажмите клавишу **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b2377-139">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
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
6. <span data-ttu-id="b2377-140">Теперь необходимо загрузить данные hello (hvac.csv), проанализировать его и использовать его tootrain hello модели.</span><span class="sxs-lookup"><span data-stu-id="b2377-140">You must now load hello data (hvac.csv), parse it, and use it tootrain hello model.</span></span> <span data-ttu-id="b2377-141">Для этого определите функцию, которая проверяет, больше ли фактическое температуры hello построения hello температуры целевой hello.</span><span class="sxs-lookup"><span data-stu-id="b2377-141">For this, you define a function that checks whether hello actual temperature of hello building is greater than hello target temperature.</span></span> <span data-ttu-id="b2377-142">Если больше фактического температуры hello, построение hello активна, обозначаемому значением hello по **1.0**.</span><span class="sxs-lookup"><span data-stu-id="b2377-142">If hello actual temperature is greater, hello building is hot, denoted by hello value **1.0**.</span></span> <span data-ttu-id="b2377-143">Если меньше фактического температуры hello, построение hello холода, обозначаемому значением hello по **0,0**.</span><span class="sxs-lookup"><span data-stu-id="b2377-143">If hello actual temperature is lesser, hello building is cold, denoted by hello value **0.0**.</span></span> 
   
    <span data-ttu-id="b2377-144">Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b2377-144">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="b2377-145">Настройка конвейера hello Spark машинного обучения, который состоит из трех этапов: разметчика, hashingTF и lr.</span><span class="sxs-lookup"><span data-stu-id="b2377-145">Configure hello Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="b2377-146">Дополнительные сведения о возможностях конвейера и о том, как он работает, см. в статье <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Конвейер машинного обучения Spark</a>.</span><span class="sxs-lookup"><span data-stu-id="b2377-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="b2377-147">Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b2377-147">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="b2377-148">Документ обучения toohello соответствия hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="b2377-148">Fit hello pipeline toohello training document.</span></span> <span data-ttu-id="b2377-149">Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b2377-149">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="b2377-150">Проверьте hello обучения документа toocheckpoint хода выполнения с помощью приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b2377-150">Verify hello training document toocheckpoint your progress with hello application.</span></span> <span data-ttu-id="b2377-151">Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b2377-151">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="b2377-152">В конечном итоге будут следующие аналогичные toohello hello выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b2377-152">This should give hello output similar toohello following:</span></span>
   
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

    <span data-ttu-id="b2377-153">Вернуться назад и проверить результаты hello hello необработанные CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="b2377-153">Go back and verify hello output against hello raw CSV file.</span></span> <span data-ttu-id="b2377-154">Например hello первая строка hello CSV-файл содержит эти данные:</span><span class="sxs-lookup"><span data-stu-id="b2377-154">For example, hello first row hello CSV file has this data:</span></span>

    <span data-ttu-id="b2377-155">![Моментальный снимок выходных данных для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Моментальный снимок выходных данных для примера машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="b2377-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="b2377-156">Обратите внимание, как фактический температуры hello, меньше, чем предлагает построение hello температуры целевой hello холодного.</span><span class="sxs-lookup"><span data-stu-id="b2377-156">Notice how hello actual temperature is less than hello target temperature suggesting hello building is cold.</span></span> <span data-ttu-id="b2377-157">Таким образом в выходных данных обучения hello hello значение **метка** в hello — первая строка **0,0**, это означает, что построение hello не активна.</span><span class="sxs-lookup"><span data-stu-id="b2377-157">Hence in hello training output, hello value for **label** in hello first row is **0.0**, which means hello building is not hot.</span></span>

1. <span data-ttu-id="b2377-158">Подготовьте набор данных toorun hello обученной модели по.</span><span class="sxs-lookup"><span data-stu-id="b2377-158">Prepare a data set toorun hello trained model against.</span></span> <span data-ttu-id="b2377-159">toodo таким образом, мы бы передать на системный идентификатор и возраст резервной системы (обозначается как **SystemInfo** в выходных данных обучения hello), и предсказать hello модели, будет ли hello построение с возрастом идентификатор и системы, система может быть еще важнее (обозначается 1.0) или охлаждающего ( обозначается 0,0).</span><span class="sxs-lookup"><span data-stu-id="b2377-159">toodo so, we would pass on a system ID and system age (denoted as **SystemInfo** in hello training output), and hello model would predict whether hello building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="b2377-160">Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b2377-160">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="b2377-161">Наконец выполнение прогнозов по hello тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="b2377-161">Finally, make predictions on hello test data.</span></span> <span data-ttu-id="b2377-162">Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b2377-162">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="b2377-163">Вы должны увидеть следующие выходные данные как toohello.</span><span class="sxs-lookup"><span data-stu-id="b2377-163">You should see an output similar toohello following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="b2377-164">Из первой строки hello в прогнозе hello, можно увидеть, что для системы Отопления с Идентификатором 20 и системы возраст 25 лет hello построение будет горячей (**прогноза = 1,0**).</span><span class="sxs-lookup"><span data-stu-id="b2377-164">From hello first row in hello prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, hello building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="b2377-165">Первое значение Hello DenseVector (0.49999) соответствует toohello прогноза 0,0 а hello второе значение (0.5001) toohello прогноза 1.0.</span><span class="sxs-lookup"><span data-stu-id="b2377-165">hello first value for DenseVector (0.49999) corresponds toohello  prediction 0.0 and hello second value (0.5001) corresponds toohello prediction 1.0.</span></span> <span data-ttu-id="b2377-166">В выходных данных hello, несмотря на то, что второе значение hello только выше, hello модель показывает **прогноза = 1,0**.</span><span class="sxs-lookup"><span data-stu-id="b2377-166">In hello output, even though hello second value is only marginally higher, hello model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="b2377-167">После завершения работы приложения hello, необходимо hello toorelease ресурсы для завершения работы hello ноутбуков.</span><span class="sxs-lookup"><span data-stu-id="b2377-167">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="b2377-168">toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**.</span><span class="sxs-lookup"><span data-stu-id="b2377-168">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="b2377-169">В этом будет завершена и закрыть hello ноутбука.</span><span class="sxs-lookup"><span data-stu-id="b2377-169">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="b2377-170"><a name="anaconda"></a>Использование библиотеки scikit-learn Anaconda для машинного обучения Spark</span><span class="sxs-lookup"><span data-stu-id="b2377-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="b2377-171">Кластеры Apache Spark в HDInsight включают библиотеки Anaconda.</span><span class="sxs-lookup"><span data-stu-id="b2377-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="b2377-172">Это также касается hello **scikit-узнать** библиотеки для машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="b2377-172">This also includes hello **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="b2377-173">Библиотека Hello также содержит различные наборы данных, которые можно использовать образцы приложений toobuild непосредственно из записной книжке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="b2377-173">hello library also includes various data sets that you can use toobuild sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="b2377-174">Для примеров с помощью hello scikit-библиотека Дополнительные сведения см. в разделе [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="b2377-174">For examples on using hello scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="b2377-175"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="b2377-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="b2377-176">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2377-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="b2377-177">Сценарии</span><span class="sxs-lookup"><span data-stu-id="b2377-177">Scenarios</span></span>
* [<span data-ttu-id="b2377-178">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="b2377-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b2377-179">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="b2377-179">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b2377-180">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="b2377-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b2377-181">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2377-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b2377-182">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="b2377-182">Create and run applications</span></span>
* [<span data-ttu-id="b2377-183">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="b2377-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b2377-184">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="b2377-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b2377-185">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="b2377-185">Tools and extensions</span></span>
* [<span data-ttu-id="b2377-186">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala основных приложений</span><span class="sxs-lookup"><span data-stu-id="b2377-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b2377-187">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b2377-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b2377-188">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2377-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b2377-189">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2377-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b2377-190">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="b2377-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b2377-191">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="b2377-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b2377-192">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="b2377-192">Manage resources</span></span>
* [<span data-ttu-id="b2377-193">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2377-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b2377-194">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="b2377-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
