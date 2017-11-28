---
title: "Пример машинного обучения с использованием Spark MLlib в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте, как использовать Spark MLlib для создания приложения машинного обучения, которое анализирует набор данных с помощью классификации посредством логистической регрессии."
keywords: "машинное обучение spark, пример машинного обучения spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: e563d4f51c9e27b20df47eca6d3eb00ac79e854f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-spark-mllib-to-build-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="11403-104">Использование Spark MLlib для создания приложения машинного обучения и анализа набора данных</span><span class="sxs-lookup"><span data-stu-id="11403-104">Use Spark MLlib to build a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="11403-105">Узнайте, как использовать Spark **MLlib** для создания приложения машинного обучения с целью проведения простого прогнозного анализа на основе открытого набора данных.</span><span class="sxs-lookup"><span data-stu-id="11403-105">Learn how to use Spark **MLlib** to create a machine learning application to do simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="11403-106">В этом примере используется *классификация* посредством логистической регрессии на основе встроенных библиотек машинного обучения Spark.</span><span class="sxs-lookup"><span data-stu-id="11403-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="11403-107">Этот пример также доступен в виде записной книжки Jupyter в кластере Spark (на платформе Linux), созданном в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11403-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="11403-108">Фрагменты кода Python можно выполнять непосредственно в записной книжке.</span><span class="sxs-lookup"><span data-stu-id="11403-108">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="11403-109">Для прохождения учебника в записной книжке создайте кластер Spark и запустите записную книжку Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="11403-109">To follow the tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="11403-110">Затем запустите записную книжку **Машинное обучение Spark. Прогнозный анализ на основе данных контроля качества пищевых продуктов с использованием MLlib.ipynb** в папке **Python**.</span><span class="sxs-lookup"><span data-stu-id="11403-110">Then, run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under the **Python** folder.</span></span>
>
>

<span data-ttu-id="11403-111">MLlib — это основная библиотека Spark, содержащая множество служебных программ, которые подходят для задач машинного обучения, в частности:</span><span class="sxs-lookup"><span data-stu-id="11403-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="11403-112">классификация;</span><span class="sxs-lookup"><span data-stu-id="11403-112">Classification</span></span>
* <span data-ttu-id="11403-113">Регрессия</span><span class="sxs-lookup"><span data-stu-id="11403-113">Regression</span></span>
* <span data-ttu-id="11403-114">Кластеризация</span><span class="sxs-lookup"><span data-stu-id="11403-114">Clustering</span></span>
* <span data-ttu-id="11403-115">тематического моделирования;</span><span class="sxs-lookup"><span data-stu-id="11403-115">Topic modeling</span></span>
* <span data-ttu-id="11403-116">сингулярного разложения и анализа по методу главных компонент;</span><span class="sxs-lookup"><span data-stu-id="11403-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="11403-117">проверки гипотез и статистической выборки.</span><span class="sxs-lookup"><span data-stu-id="11403-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="11403-118">Сведения о классификации и логистической регрессии</span><span class="sxs-lookup"><span data-stu-id="11403-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="11403-119">*Классификация* — это распространенная задача машинного обучения, которая представляет собой процесс сортировки входных данных по категориям.</span><span class="sxs-lookup"><span data-stu-id="11403-119">*Classification*, a popular machine learning task, is the process of sorting input data into categories.</span></span> <span data-ttu-id="11403-120">Алгоритм классификации определяет принцип назначения «меток» предоставленным входным данных.</span><span class="sxs-lookup"><span data-stu-id="11403-120">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span></span> <span data-ttu-id="11403-121">Например, можно создать алгоритм машинного обучения, который принимает в качестве входных данных информацию об акциях и делит акции на две категории: акции, которые следует продать, и акции, которые стоит оставить.</span><span class="sxs-lookup"><span data-stu-id="11403-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="11403-122">Логистическая регрессия — один из алгоритмов классификации.</span><span class="sxs-lookup"><span data-stu-id="11403-122">Logistic regression is the algorithm that you use for classification.</span></span> <span data-ttu-id="11403-123">API Spark для логистической регрессии подходит для задач *двоичной классификации* или разделения входных данных на две группы.</span><span class="sxs-lookup"><span data-stu-id="11403-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="11403-124">Дополнительные сведения о логистической регрессии см. в статье [Википедии](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="11403-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="11403-125">В общих словах, в основе логистической регрессии лежит некая *логистическая функция* , используемая для прогнозирования вероятности принадлежности вектора входных данных к одной или другой группе.</span><span class="sxs-lookup"><span data-stu-id="11403-125">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="11403-126">Пример прогнозного анализа на основе данных контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="11403-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="11403-127">В этом примере показано использование Spark для прогнозного анализа на основе данных контроля качества пищевых продуктов (**Food_Inspections1.csv**), полученных на [информационном портале Чикаго](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="11403-127">In this example, you use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="11403-128">Этот набор данных содержит сведения о проверках качества пищевых продуктов, проведенных в Чикаго, в частности информацию о каждом предприятии общественного питания, обнаруженных нарушениях (если таковые были) и результатах проверки.</span><span class="sxs-lookup"><span data-stu-id="11403-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, the violations found (if any), and the results of the inspection.</span></span> <span data-ttu-id="11403-129">CSV-файл данных уже доступен в учетной записи хранения, связанной с кластером **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="11403-129">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="11403-130">В следующих разделах описаны шаги по разработке модели, которая позволит узнать, что нужно, чтобы пройти контроль качества пищевых продуктов.</span><span class="sxs-lookup"><span data-stu-id="11403-130">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="11403-131">Начало создания приложения машинного обучения Spark MMLib</span><span class="sxs-lookup"><span data-stu-id="11403-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="11403-132">На начальной панели [портала Azure](https://portal.azure.com/)щелкните плитку кластера Spark (если она закреплена на начальной панели).</span><span class="sxs-lookup"><span data-stu-id="11403-132">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="11403-133">Кроме того, вы можете перейти к кластеру, последовательно щелкнув **Просмотреть все** > **Кластеры HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="11403-133">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="11403-134">В колонке кластера Spark щелкните **Панель мониторинга кластера**, а затем выберите **Записная книжка Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="11403-134">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="11403-135">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="11403-135">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="11403-136">Также можно открыть Jupyter Notebook для своего кластера, открыв следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="11403-136">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="11403-137">Замените **CLUSTERNAME** именем кластера:</span><span class="sxs-lookup"><span data-stu-id="11403-137">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="11403-138">Создайте записную книжку.</span><span class="sxs-lookup"><span data-stu-id="11403-138">Create a notebook.</span></span> <span data-ttu-id="11403-139">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="11403-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="11403-140">![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Создание записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="11403-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="11403-141">Будет создана и открыта записная книжка с именем Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="11403-141">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="11403-142">Щелкните имя записной книжки в верхней части страницы сверху и введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="11403-142">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="11403-143">![Указание имени для записной книжки](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Указание имени для записной книжки")</span><span class="sxs-lookup"><span data-stu-id="11403-143">![Provide a name for the notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for the notebook")</span></span>
1. <span data-ttu-id="11403-144">Так как записная книжка была создана с помощью ядра PySpark, задавать контексты явно необязательно.</span><span class="sxs-lookup"><span data-stu-id="11403-144">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="11403-145">Контексты Spark и Hive будут созданы автоматически при выполнении первой ячейки кода.</span><span class="sxs-lookup"><span data-stu-id="11403-145">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="11403-146">Вы можете приступить к созданию своего приложения машинного обучения, импортировав типы, необходимые для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="11403-146">You can start building your machine learning application by importing the types required for this scenario.</span></span> <span data-ttu-id="11403-147">Для этого наведите курсор на ячейку и нажмите клавиши **SHIFT+ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="11403-147">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="11403-148">Создание входной таблицы данных</span><span class="sxs-lookup"><span data-stu-id="11403-148">Construct an input dataframe</span></span>
<span data-ttu-id="11403-149">Для преобразования структурированных данных можно использовать `sqlContext` .</span><span class="sxs-lookup"><span data-stu-id="11403-149">We can use `sqlContext` to perform transformations on structured data.</span></span> <span data-ttu-id="11403-150">Сначала нужно загрузить пример данных (**Food_Inspections1.csv**) в *таблицу данных* SQL Spark.</span><span class="sxs-lookup"><span data-stu-id="11403-150">The first task is to load the sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="11403-151">Так как изначально данные предоставлены в формате CSV, нужно извлечь каждую строку файла в память как неструктурированный текст с использованием контекста Spark, а затем проанализировать отдельно каждую строку с помощью библиотеки Python в формате CSV.</span><span class="sxs-lookup"><span data-stu-id="11403-151">Because the raw data is in a CSV format, we need to use the Spark context to pull every line of the file into memory as unstructured text; then, you use Python's CSV library to parse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="11403-152">Теперь у нас есть CSV-файл в качестве устойчивого распределенного набора данных (RDD).</span><span class="sxs-lookup"><span data-stu-id="11403-152">We now have the CSV file as an RDD.</span></span>  <span data-ttu-id="11403-153">Чтобы разобраться со схемой данных, извлечем одну строку из RDD.</span><span class="sxs-lookup"><span data-stu-id="11403-153">To understand the schema of the data, we retrieve one row from the RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="11403-154">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="11403-154">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of the plumbing section of the Municipal Code of Chicago and Rules and Regulation of the Board of Health. OBSEVERD THE 3 COMPARTMENT SINK BACKING UP INTO THE 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding to protect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED TO REPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN THE REAR CHILDREN AREA,IN THE KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED TO REPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY THE 15MOS AREA. NEED TO BE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY THE EXPOSED HAND SINK IN THE KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: The floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED TO ELEVATE ALL FOOD ITEMS 6INCH OFF THE FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="11403-155">Приведенные выше выходные данные позволяют нам составить представление о схеме входного файла.</span><span class="sxs-lookup"><span data-stu-id="11403-155">The preceding output gives us an idea of the schema of the input file.</span></span> <span data-ttu-id="11403-156">Помимо прочего, в файле содержатся название, тип и адрес каждого учреждения, а также данные проверки и места проведения проверок.</span><span class="sxs-lookup"><span data-stu-id="11403-156">It includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span></span> <span data-ttu-id="11403-157">Давайте выберем несколько подходящих столбцов для прогнозного анализа и сгруппируем результаты в таблицу данных, которой затем воспользуемся для создания временной таблицы.</span><span class="sxs-lookup"><span data-stu-id="11403-157">Let's select a few columns that are useful for our predictive analysis and group the results as a dataframe, which we then use to create a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="11403-158">Теперь у нас есть *таблица данных*, `df`, на основе которой можно выполнять анализ.</span><span class="sxs-lookup"><span data-stu-id="11403-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="11403-159">У нас также есть временная таблица **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="11403-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="11403-160">Она состоит из 4 столбцов: **id**, **name**, **results** и **violations**.</span><span class="sxs-lookup"><span data-stu-id="11403-160">We've included four columns of interest in the dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="11403-161">Выполните следующую команду, чтобы получить небольшой пример данных:</span><span class="sxs-lookup"><span data-stu-id="11403-161">Let's get a small sample of the data:</span></span>

        df.show(5)

    <span data-ttu-id="11403-162">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="11403-162">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES TO ...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-the-data"></a><span data-ttu-id="11403-163">Используемые данные</span><span class="sxs-lookup"><span data-stu-id="11403-163">Understand the data</span></span>
1. <span data-ttu-id="11403-164">Давайте подробно рассмотрим содержимое набора данных.</span><span class="sxs-lookup"><span data-stu-id="11403-164">Let's start to get a sense of what our dataset contains.</span></span> <span data-ttu-id="11403-165">Например, что представляют собой различные значения в столбце **results** ?</span><span class="sxs-lookup"><span data-stu-id="11403-165">For example, what are the different values in the **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="11403-166">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="11403-166">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. <span data-ttu-id="11403-167">Простой способ понять, каким образом распределены результаты, — применить визуализацию.</span><span class="sxs-lookup"><span data-stu-id="11403-167">A quick visualization can help us reason about the distribution of these outcomes.</span></span> <span data-ttu-id="11403-168">Во временной таблице **CountResults**уже есть данные.</span><span class="sxs-lookup"><span data-stu-id="11403-168">We already have the data in a temporary table **CountResults**.</span></span> <span data-ttu-id="11403-169">Чтобы лучше понять, как распределяются результаты, можно выполнить следующий SQL-запрос к таблице.</span><span class="sxs-lookup"><span data-stu-id="11403-169">You can run the following SQL query against the table to get a better understanding of how the results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="11403-170">Волшебное слово `%%sql`, за которым следует `-o countResultsdf`, гарантирует, что вывод запроса сохраняется локально на сервере Jupyter (обычно это головной узел кластера).</span><span class="sxs-lookup"><span data-stu-id="11403-170">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="11403-171">Выходные данные сохраняются в кадре данных [Pandas](http://pandas.pydata.org/) с именем **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="11403-171">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span></span>

    <span data-ttu-id="11403-172">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="11403-172">You should see an output like the following:</span></span>

    <span data-ttu-id="11403-173">![Результат SQL-запроса](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Результат SQL-запроса")</span><span class="sxs-lookup"><span data-stu-id="11403-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="11403-174">Дополнительные сведения о магической команде `%%sql`, а также других магических командах, доступных в ядре PySpark, приведены в статье [Ядра для записных книжек Jupyter с кластерами Apache Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="11403-174">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="11403-175">Также можно создать диаграмму с помощью Matplotlib, библиотеки, используемой для визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="11403-175">You can also use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="11403-176">Так как диаграмма должна создаваться из локально сохраненного кадра данных **countResultsdf**, фрагмент кода должен начинаться с волшебного слова `%%local`.</span><span class="sxs-lookup"><span data-stu-id="11403-176">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="11403-177">Это гарантирует, что код будет выполняться локально на сервере Jupyter.</span><span class="sxs-lookup"><span data-stu-id="11403-177">This ensures that the code is run locally on the Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="11403-178">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="11403-178">You should see an output like the following:</span></span>

    <span data-ttu-id="11403-179">![Выходные данные приложения машинного обучения Spark — круговая диаграмма с пятью отдельными результатами проверки](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Результаты машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="11403-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="11403-180">Проверка может дать один из 5 следующих результатов:</span><span class="sxs-lookup"><span data-stu-id="11403-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="11403-181">Business not located;</span><span class="sxs-lookup"><span data-stu-id="11403-181">Business not located</span></span>
   * <span data-ttu-id="11403-182">Fail;</span><span class="sxs-lookup"><span data-stu-id="11403-182">Fail</span></span>
   * <span data-ttu-id="11403-183">Pass;</span><span class="sxs-lookup"><span data-stu-id="11403-183">Pass</span></span>
   * <span data-ttu-id="11403-184">Pss w/ conditions</span><span class="sxs-lookup"><span data-stu-id="11403-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="11403-185">Out of Business.</span><span class="sxs-lookup"><span data-stu-id="11403-185">Out of Business</span></span>

     <span data-ttu-id="11403-186">Наша задача — разработать модель, которая может спрогнозировать результат контроля качества пищевых продуктов, исходя из нарушений.</span><span class="sxs-lookup"><span data-stu-id="11403-186">Let us develop a model that can guess the outcome of a food inspection, given the violations.</span></span> <span data-ttu-id="11403-187">Так как логистическая регрессия — это метод двоичной классификации, целесообразно разделить данные на две категории: **Fail** и **Pass**.</span><span class="sxs-lookup"><span data-stu-id="11403-187">Since logistic regression is a binary classification method, it makes sense to group our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="11403-188">Результат "Pass w/ Conditions" также считается проходным, поэтому при обучении модели мы рассматриваем его как эквивалентный Pass.</span><span class="sxs-lookup"><span data-stu-id="11403-188">A "Pass w/ Conditions" is still a Pass, so when we train the model, we consider the two results equivalent.</span></span> <span data-ttu-id="11403-189">Данные с другими результатами ("Business Not Located" или "Out of Business") бесполезны, поэтому мы удалим их из обучающего набора.</span><span class="sxs-lookup"><span data-stu-id="11403-189">Data with the other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="11403-190">Эти никак не должно повлиять на анализ, так как они составляют очень небольшой процент от общего результата.</span><span class="sxs-lookup"><span data-stu-id="11403-190">This should be okay since these two categories make up a very small percentage of the results anyway.</span></span>
1. <span data-ttu-id="11403-191">Далее нам нужно преобразовать существующую таблицу данных (`df`) в новую таблицу данных, где каждая проверка представлена в виде пары «метка-нарушение».</span><span class="sxs-lookup"><span data-stu-id="11403-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="11403-192">В нашем случае метка `0.0` представляет неудачу, `1.0` — успех, а `-1.0` — другие результаты, помимо этих двух.</span><span class="sxs-lookup"><span data-stu-id="11403-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="11403-193">При вычислении новой таблицы данных мы отфильтровываем все второстепенные результаты.</span><span class="sxs-lookup"><span data-stu-id="11403-193">We filter those other results out when computing the new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="11403-194">Чтобы увидеть, как выглядят помеченные данные, давайте извлечем одну строку.</span><span class="sxs-lookup"><span data-stu-id="11403-194">To see what the labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="11403-195">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="11403-195">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a><span data-ttu-id="11403-196">Создание модели логистической регрессии на основе входной таблицы данных</span><span class="sxs-lookup"><span data-stu-id="11403-196">Create a logistic regression model from the input dataframe</span></span>
<span data-ttu-id="11403-197">Наша последняя задача — преобразовать помеченные данные в такой формат, в котором их сможет проанализировать модель логистической регрессии.</span><span class="sxs-lookup"><span data-stu-id="11403-197">Our final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="11403-198">Входные данные для алгоритма логистической регрессии должны представлять собой набор *пар "метка — вектор признаков"*, где "вектор признаков" — это совокупность чисел, представляющая входную точку.</span><span class="sxs-lookup"><span data-stu-id="11403-198">The input to a logistic regression algorithm should be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers representing the input point.</span></span> <span data-ttu-id="11403-199">Таким образом, нам нужно преобразовать столбец violations, содержащий полуструктурированные данные и множество текстовых комментариев в свободной форме, в массив действительных чисел, которые может распознать компьютер.</span><span class="sxs-lookup"><span data-stu-id="11403-199">So, we need to convert the "violations" column, which is semi-structured and contains many comments in free-text, to an array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="11403-200">Стандартный метод обработки естественного языка в машинном обучении — назначить каждому отдельному слову индекс, а затем передать вектор в алгоритм машинного обучения, при этом значение каждого индекса должно содержать относительную частоту использования слова в текстовой строке.</span><span class="sxs-lookup"><span data-stu-id="11403-200">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span></span>

<span data-ttu-id="11403-201">MLlib предоставляет простой способ выполнения этой операции.</span><span class="sxs-lookup"><span data-stu-id="11403-201">MLlib provides an easy way to perform this operation.</span></span> <span data-ttu-id="11403-202">Сначала пометим каждую строку нарушений с помощью маркеров, чтобы определить отдельные слова в каждой строке.</span><span class="sxs-lookup"><span data-stu-id="11403-202">First, "tokenize" each violations string to get the individual words in each string.</span></span> <span data-ttu-id="11403-203">Затем используем `HashingTF`, чтобы преобразовать каждый набор маркеров в вектор признаков, который затем может быть передан в алгоритм логистической регрессии для создания модели.</span><span class="sxs-lookup"><span data-stu-id="11403-203">Then, use a `HashingTF` to convert each set of tokens into a feature vector that can then be passed to the logistic regression algorithm to construct a model.</span></span> <span data-ttu-id="11403-204">Для выполнения всех этих действий последовательно используем оператор pipeline.</span><span class="sxs-lookup"><span data-stu-id="11403-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-the-model-on-a-separate-test-dataset"></a><span data-ttu-id="11403-205">Анализ модели с использованием отдельного тестового набора данных</span><span class="sxs-lookup"><span data-stu-id="11403-205">Evaluate the model on a separate test dataset</span></span>
<span data-ttu-id="11403-206">Созданную ранее модель можно использовать, чтобы *спрогнозировать* результаты новой проверки на основе обнаруженных нарушений.</span><span class="sxs-lookup"><span data-stu-id="11403-206">We can use the model we created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span></span> <span data-ttu-id="11403-207">Мы обучили эту модель по набору данных **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="11403-207">We trained this model on the dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="11403-208">Теперь используем другой набор данных, **Food_Inspections2.csv**, чтобы *оценить* эффективность этой модели на основе новых данных.</span><span class="sxs-lookup"><span data-stu-id="11403-208">Let us use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on new data.</span></span> <span data-ttu-id="11403-209">Другой набор данных (**Food_Inspections2.csv**) должен быть помещен в контейнер хранилища по умолчанию, связанный с кластером.</span><span class="sxs-lookup"><span data-stu-id="11403-209">This second data set (**Food_Inspections2.csv**) should already be in the default storage container associated with the cluster.</span></span>

1. <span data-ttu-id="11403-210">Приведенный ниже фрагмент кода создает кадр данных **predictionsDf**, содержащий сформированный моделью прогноз.</span><span class="sxs-lookup"><span data-stu-id="11403-210">The following snippet creates a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span></span> <span data-ttu-id="11403-211">Фрагмент кода также создает временную таблицу **Predictions** на основе кадра данных.</span><span class="sxs-lookup"><span data-stu-id="11403-211">The snippet also creates a temporary table called **Predictions** based on the dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="11403-212">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="11403-212">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. <span data-ttu-id="11403-213">Чтобы просмотреть пример прогноза,</span><span class="sxs-lookup"><span data-stu-id="11403-213">Look at one of the predictions.</span></span> <span data-ttu-id="11403-214">выполните этот фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="11403-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="11403-215">Вы получите прогноз для первой записи в тестовом наборе данных.</span><span class="sxs-lookup"><span data-stu-id="11403-215">There is a prediction for the first entry in the test data set.</span></span>
1. <span data-ttu-id="11403-216">Метод `model.transform()` таким же образом преобразовывает новые данные и определяет, как их классифицировать.</span><span class="sxs-lookup"><span data-stu-id="11403-216">The `model.transform()` method applies the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span></span> <span data-ttu-id="11403-217">Можно выполнить некоторые статистические расчеты, чтобы увидеть, насколько точны полученные прогнозы:</span><span class="sxs-lookup"><span data-stu-id="11403-217">We can do some simple statistics to get a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="11403-218">Данные результата выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="11403-218">The output looks like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="11403-219">Используя логистическую регрессию Spark, мы создали точную модель, которая прогнозирует вероятность прохождения контроля качества пищевых продуктов для определенного предприятия на основе описаний нарушений на английском языке.</span><span class="sxs-lookup"><span data-stu-id="11403-219">Using logistic regression with Spark gives us an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-the-prediction"></a><span data-ttu-id="11403-220">Создание визуального представления прогноза</span><span class="sxs-lookup"><span data-stu-id="11403-220">Create a visual representation of the prediction</span></span>
<span data-ttu-id="11403-221">Теперь мы можем построить окончательную визуализацию, чтобы наглядно увидеть результаты теста.</span><span class="sxs-lookup"><span data-stu-id="11403-221">We can now construct a final visualization to help us reason about the results of this test.</span></span>

1. <span data-ttu-id="11403-222">Начнем с извлечения различных прогнозов и результатов из временной таблицы **Predictions** , созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="11403-222">We start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="11403-223">Следующие запросы разделяют выходные данные на *true_positive*, *false_positive*, *true_negative* и *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="11403-223">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="11403-224">В приведенных ниже запросах мы отключим визуализацию с помощью `-q`, а также сохраним выходные данные (с помощью `-o`) как кадры данных, которые затем можно будет использовать с волшебным словом `%%local`.</span><span class="sxs-lookup"><span data-stu-id="11403-224">In the queries below, we turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="11403-225">Наконец, используйте следующий фрагмент кода для создания диаграммы с помощью **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="11403-225">Finally, use the following snippet to generate the plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="11403-226">Вы должны увидеть следующий результат.</span><span class="sxs-lookup"><span data-stu-id="11403-226">You should see the following output:</span></span>

    <span data-ttu-id="11403-227">![Выходные данные приложения машинного обучения Spark — круговая диаграмма с процентными значениями для проверок качества пищевых продуктов, которые не были пройдены.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Результаты машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="11403-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="11403-228">На этой диаграмме «положительный» результат представляет собой непройденную проверку, а отрицательный — пройденную.</span><span class="sxs-lookup"><span data-stu-id="11403-228">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span></span>

## <a name="shut-down-the-notebook"></a><span data-ttu-id="11403-229">Завершение работы записной книжки</span><span class="sxs-lookup"><span data-stu-id="11403-229">Shut down the notebook</span></span>
<span data-ttu-id="11403-230">Завершив работу с приложением, следует закрыть записную книжку, чтобы освободить ресурсы.</span><span class="sxs-lookup"><span data-stu-id="11403-230">After you have finished running the application, you should shut down the notebook to release the resources.</span></span> <span data-ttu-id="11403-231">Для этого в записной книжке в меню **Файл** выберите пункт **Close and Halt** (Закрыть и остановить).</span><span class="sxs-lookup"><span data-stu-id="11403-231">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="11403-232">Записная книжка завершит работу и закроется.</span><span class="sxs-lookup"><span data-stu-id="11403-232">This shuts down and closes the notebook.</span></span>

## <span data-ttu-id="11403-233"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="11403-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="11403-234">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="11403-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="11403-235">Сценарии</span><span class="sxs-lookup"><span data-stu-id="11403-235">Scenarios</span></span>
* [<span data-ttu-id="11403-236">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="11403-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="11403-237">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="11403-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="11403-238">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="11403-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="11403-239">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="11403-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="11403-240">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="11403-240">Create and run applications</span></span>
* [<span data-ttu-id="11403-241">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="11403-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="11403-242">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="11403-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="11403-243">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="11403-243">Tools and extensions</span></span>
* [<span data-ttu-id="11403-244">Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="11403-244">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="11403-245">Удаленная отладка приложений Spark в кластере HDInsight Spark Linux с помощью подключаемого модуля средств HDInsight для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="11403-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="11403-246">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="11403-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="11403-247">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="11403-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="11403-248">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="11403-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="11403-249">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="11403-249">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="11403-250">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="11403-250">Manage resources</span></span>
* [<span data-ttu-id="11403-251">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="11403-251">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="11403-252">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="11403-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
