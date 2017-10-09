---
title: "Пример с MLlib Spark на HDInsight - Azure обучения aaaMachine | Документы Microsoft"
description: "Узнайте, как toocreate Spark MLlib toouse приложение обучения машины, которое анализирует набор данных с помощью классификации через логистической регрессии."
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
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="16c6b-104">Используйте Spark MLlib toobuild машинного обучения приложения и анализ набора данных</span><span class="sxs-lookup"><span data-stu-id="16c6b-104">Use Spark MLlib toobuild a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="16c6b-105">Узнайте, как toouse Spark **MLlib** toocreate a машинного обучения toodo простого прогнозирующего анализ приложения на открытие набора данных.</span><span class="sxs-lookup"><span data-stu-id="16c6b-105">Learn how toouse Spark **MLlib** toocreate a machine learning application toodo simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="16c6b-106">В этом примере используется *классификация* посредством логистической регрессии на основе встроенных библиотек машинного обучения Spark.</span><span class="sxs-lookup"><span data-stu-id="16c6b-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="16c6b-107">Этот пример также доступен в виде записной книжки Jupyter в кластере Spark (на платформе Linux), созданном в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="16c6b-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="16c6b-108">взаимодействие с ноутбука Hello позволяет выполнять фрагменты кода Python hello из записной книжки hello сам.</span><span class="sxs-lookup"><span data-stu-id="16c6b-108">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="16c6b-109">Учебник hello toofollow в записной книжке создайте Spark кластера и запустите записной книжке Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="16c6b-109">toofollow hello tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="16c6b-110">Выполните записной книжки hello **Spark машинного обучения — прогнозирующей аналитики на данные проверки пищевых продуктов с помощью MLlib.ipynb** под hello **Python** папки.</span><span class="sxs-lookup"><span data-stu-id="16c6b-110">Then, run hello notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under hello **Python** folder.</span></span>
>
>

<span data-ttu-id="16c6b-111">MLlib — это основная библиотека Spark, содержащая множество служебных программ, которые подходят для задач машинного обучения, в частности:</span><span class="sxs-lookup"><span data-stu-id="16c6b-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="16c6b-112">классификация;</span><span class="sxs-lookup"><span data-stu-id="16c6b-112">Classification</span></span>
* <span data-ttu-id="16c6b-113">Регрессия</span><span class="sxs-lookup"><span data-stu-id="16c6b-113">Regression</span></span>
* <span data-ttu-id="16c6b-114">Кластеризация</span><span class="sxs-lookup"><span data-stu-id="16c6b-114">Clustering</span></span>
* <span data-ttu-id="16c6b-115">тематического моделирования;</span><span class="sxs-lookup"><span data-stu-id="16c6b-115">Topic modeling</span></span>
* <span data-ttu-id="16c6b-116">сингулярного разложения и анализа по методу главных компонент;</span><span class="sxs-lookup"><span data-stu-id="16c6b-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="16c6b-117">проверки гипотез и статистической выборки.</span><span class="sxs-lookup"><span data-stu-id="16c6b-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="16c6b-118">Сведения о классификации и логистической регрессии</span><span class="sxs-lookup"><span data-stu-id="16c6b-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="16c6b-119">*Классификация*, популярных машинного обучения задач, — процесс hello сортировки входных данных по категориям.</span><span class="sxs-lookup"><span data-stu-id="16c6b-119">*Classification*, a popular machine learning task, is hello process of sorting input data into categories.</span></span> <span data-ttu-id="16c6b-120">Это задание hello объекта toofigure алгоритм классификации, как tooassign «метки» tooinput данные, предоставляемые.</span><span class="sxs-lookup"><span data-stu-id="16c6b-120">It is hello job of a classification algorithm toofigure out how tooassign "labels" tooinput data that you provide.</span></span> <span data-ttu-id="16c6b-121">Например, можно рассмотреть алгоритм машинного обучения, который принимает биржевых данных в качестве входных данных и разделяет hello акций на две категории: следует продавать изменения курса акций и акции, которые должны поддерживать.</span><span class="sxs-lookup"><span data-stu-id="16c6b-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides hello stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="16c6b-122">Логистическая Регрессия является hello алгоритма, который используется для классификации.</span><span class="sxs-lookup"><span data-stu-id="16c6b-122">Logistic regression is hello algorithm that you use for classification.</span></span> <span data-ttu-id="16c6b-123">API Spark для логистической регрессии подходит для задач *двоичной классификации* или разделения входных данных на две группы.</span><span class="sxs-lookup"><span data-stu-id="16c6b-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="16c6b-124">Дополнительные сведения о логистической регрессии см. в статье [Википедии](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="16c6b-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="16c6b-125">Таким образом, процесс hello логистической регрессии производит *логистической функции* , может быть используется toopredict hello вероятности, вектор ввода относится в одну группу или других hello.</span><span class="sxs-lookup"><span data-stu-id="16c6b-125">In summary, hello process of logistic regression produces a *logistic function* that can be used toopredict hello probability that an input vector belongs in one group or hello other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="16c6b-126">Пример прогнозного анализа на основе данных контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="16c6b-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="16c6b-127">В этом примере используется Spark tooperform некоторые прогнозирующей аналитики на данные проверки пищевых продуктов (**Food_Inspections1.csv**), был получен через hello [портал данных Город Чикаго](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="16c6b-127">In this example, you use Spark tooperform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through hello [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="16c6b-128">Этот набор данных содержит сведения о пищевых продуктов установление проверок, которые проводились в Чикаго, включая сведения о каждом установлении, нарушений hello найден (если таковые имеются) и hello результаты проверки hello.</span><span class="sxs-lookup"><span data-stu-id="16c6b-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, hello violations found (if any), and hello results of hello inspection.</span></span> <span data-ttu-id="16c6b-129">уже находится в учетной записи хранилища hello, связанной с кластером hello в CSV-файла Hello **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-129">hello CSV data file is already available in hello storage account associated with hello cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="16c6b-130">В следующие действия hello разработке toosee модели, что требуется toopass или сбой проверки пищевых продуктов.</span><span class="sxs-lookup"><span data-stu-id="16c6b-130">In hello steps below, you develop a model toosee what it takes toopass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="16c6b-131">Начало создания приложения машинного обучения Spark MMLib</span><span class="sxs-lookup"><span data-stu-id="16c6b-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="16c6b-132">Из hello [портал Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели).</span><span class="sxs-lookup"><span data-stu-id="16c6b-132">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="16c6b-133">Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-133">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="16c6b-134">Из колонки кластера Spark hello, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **книжке Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-134">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="16c6b-135">При появлении запроса введите учетные данные администратора hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="16c6b-135">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="16c6b-136">Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="16c6b-136">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="16c6b-137">Замените **CLUSTERNAME** с hello имя кластера:</span><span class="sxs-lookup"><span data-stu-id="16c6b-137">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="16c6b-138">Создайте записную книжку.</span><span class="sxs-lookup"><span data-stu-id="16c6b-138">Create a notebook.</span></span> <span data-ttu-id="16c6b-139">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="16c6b-140">![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Создание записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="16c6b-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="16c6b-141">Создается и открывается с именем hello Untitled.pynb новый блокнот.</span><span class="sxs-lookup"><span data-stu-id="16c6b-141">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="16c6b-142">Щелкните имя записной книжки hello вверху hello и введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="16c6b-142">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="16c6b-143">![Введите имя для ноутбука hello](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "укажите имя для ноутбука hello")</span><span class="sxs-lookup"><span data-stu-id="16c6b-143">![Provide a name for hello notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for hello notebook")</span></span>
1. <span data-ttu-id="16c6b-144">Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом.</span><span class="sxs-lookup"><span data-stu-id="16c6b-144">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="16c6b-145">контексты Spark и Hive Hello автоматически создаются при выполнении первой ячейке кода hello.</span><span class="sxs-lookup"><span data-stu-id="16c6b-145">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="16c6b-146">Можно приступать к созданию машинного обучения приложения путем импорта hello типы, необходимые для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="16c6b-146">You can start building your machine learning application by importing hello types required for this scenario.</span></span> <span data-ttu-id="16c6b-147">toodo таким образом, поместите курсор hello в ячейке hello и нажмите клавишу **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-147">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="16c6b-148">Создание входной таблицы данных</span><span class="sxs-lookup"><span data-stu-id="16c6b-148">Construct an input dataframe</span></span>
<span data-ttu-id="16c6b-149">Мы используем `sqlContext` tooperform преобразования структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="16c6b-149">We can use `sqlContext` tooperform transformations on structured data.</span></span> <span data-ttu-id="16c6b-150">Hello первой задачей является данных образец hello tooload ((**Food_Inspections1.csv**)) в Spark SQL *кадр данных*.</span><span class="sxs-lookup"><span data-stu-id="16c6b-150">hello first task is tooload hello sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="16c6b-151">Поскольку hello необработанные данные в формате CSV, мы должны toouse hello Spark контекста toopull все строки файла hello в память как неструктурированных текстовых; затем используется tooparse библиотеки Python CSV каждую строку отдельно.</span><span class="sxs-lookup"><span data-stu-id="16c6b-151">Because hello raw data is in a CSV format, we need toouse hello Spark context toopull every line of hello file into memory as unstructured text; then, you use Python's CSV library tooparse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="16c6b-152">Теперь у нас есть hello CSV-файл как RDD.</span><span class="sxs-lookup"><span data-stu-id="16c6b-152">We now have hello CSV file as an RDD.</span></span>  <span data-ttu-id="16c6b-153">схемы hello toounderstand данных hello, нам получить одну строку из hello RDD.</span><span class="sxs-lookup"><span data-stu-id="16c6b-153">toounderstand hello schema of hello data, we retrieve one row from hello RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="16c6b-154">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="16c6b-154">You should see an output like hello following:</span></span>

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
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="16c6b-155">Hello выше выходных данных дает представление о схеме hello hello входного файла.</span><span class="sxs-lookup"><span data-stu-id="16c6b-155">hello preceding output gives us an idea of hello schema of hello input file.</span></span> <span data-ttu-id="16c6b-156">Он включает hello имени каждого установление hello введите установление, адрес hello, hello данных проверок hello и расположения hello, среди прочего.</span><span class="sxs-lookup"><span data-stu-id="16c6b-156">It includes hello name of every establishment, hello type of establishment, hello address, hello data of hello inspections, and hello location, among other things.</span></span> <span data-ttu-id="16c6b-157">Позволяет выбрать несколько столбцов, которые полезны для прогнозирующего анализа и сгруппировать результаты hello в кадр данных, который мы затем использовать toocreate временной таблицы.</span><span class="sxs-lookup"><span data-stu-id="16c6b-157">Let's select a few columns that are useful for our predictive analysis and group hello results as a dataframe, which we then use toocreate a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="16c6b-158">Теперь у нас есть *таблица данных*, `df`, на основе которой можно выполнять анализ.</span><span class="sxs-lookup"><span data-stu-id="16c6b-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="16c6b-159">У нас также есть временная таблица **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="16c6b-160">Мы включили нужных в кадр данных hello четырех столбцов: **идентификатор**, **имя**, **результатов**, и **нарушений**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-160">We've included four columns of interest in hello dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="16c6b-161">Давайте небольшую выборку данных hello:</span><span class="sxs-lookup"><span data-stu-id="16c6b-161">Let's get a small sample of hello data:</span></span>

        df.show(5)

    <span data-ttu-id="16c6b-162">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="16c6b-162">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a><span data-ttu-id="16c6b-163">Понимание данных hello</span><span class="sxs-lookup"><span data-stu-id="16c6b-163">Understand hello data</span></span>
1. <span data-ttu-id="16c6b-164">Давайте начнем tooget представление о наш набор данных содержит.</span><span class="sxs-lookup"><span data-stu-id="16c6b-164">Let's start tooget a sense of what our dataset contains.</span></span> <span data-ttu-id="16c6b-165">Например, каковы hello различных значений в hello **результатов** столбца?</span><span class="sxs-lookup"><span data-stu-id="16c6b-165">For example, what are hello different values in hello **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="16c6b-166">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="16c6b-166">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="16c6b-167">Быстрый визуализации можете помочь нам причина о распределении hello этих результатов.</span><span class="sxs-lookup"><span data-stu-id="16c6b-167">A quick visualization can help us reason about hello distribution of these outcomes.</span></span> <span data-ttu-id="16c6b-168">Мы уже имеются данные hello во временной таблице **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-168">We already have hello data in a temporary table **CountResults**.</span></span> <span data-ttu-id="16c6b-169">Можно выполнить следующий SQL-запрос к таблице tooget hello hello лучше понять распределение результатов hello.</span><span class="sxs-lookup"><span data-stu-id="16c6b-169">You can run hello following SQL query against hello table tooget a better understanding of how hello results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="16c6b-170">Hello `%%sql` следуют магическое `-o countResultsdf` гарантирует, что hello выходных данных запроса hello сохраняется локально на сервере Jupyter hello (обычно hello головному узлу кластера hello).</span><span class="sxs-lookup"><span data-stu-id="16c6b-170">hello `%%sql` magic followed by `-o countResultsdf` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="16c6b-171">Hello выходные данные сохраняются в виде [Pandas](http://pandas.pydata.org/) кадр данных с hello указано имя **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-171">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **countResultsdf**.</span></span>

    <span data-ttu-id="16c6b-172">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="16c6b-172">You should see an output like hello following:</span></span>

    <span data-ttu-id="16c6b-173">![Результат SQL-запроса](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Результат SQL-запроса")</span><span class="sxs-lookup"><span data-stu-id="16c6b-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="16c6b-174">Дополнительные сведения о hello `%%sql` magic и другие доступные ядра PySpark hello, magics. в разделе [ядер, доступных на записные книжки Jupyter с кластерами Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="16c6b-174">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="16c6b-175">Можно также использовать Matplotlib, библиотеку используется tooconstruct визуализации данных, toocreate построение.</span><span class="sxs-lookup"><span data-stu-id="16c6b-175">You can also use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="16c6b-176">Так как hello рисунка должны быть созданы из локально hello материализованные **countResultsdf** кадр данных, фрагмент кода hello должно начинаться с hello `%%local` магическое значение.</span><span class="sxs-lookup"><span data-stu-id="16c6b-176">Because hello plot must be created from hello locally persisted **countResultsdf** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="16c6b-177">Это гарантирует, что hello код запускается локально на сервере Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="16c6b-177">This ensures that hello code is run locally on hello Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="16c6b-178">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="16c6b-178">You should see an output like hello following:</span></span>

    <span data-ttu-id="16c6b-179">![Выходные данные приложения машинного обучения Spark — круговая диаграмма с пятью отдельными результатами проверки](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Результаты машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="16c6b-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="16c6b-180">Проверка может дать один из 5 следующих результатов:</span><span class="sxs-lookup"><span data-stu-id="16c6b-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="16c6b-181">Business not located;</span><span class="sxs-lookup"><span data-stu-id="16c6b-181">Business not located</span></span>
   * <span data-ttu-id="16c6b-182">Fail;</span><span class="sxs-lookup"><span data-stu-id="16c6b-182">Fail</span></span>
   * <span data-ttu-id="16c6b-183">Pass;</span><span class="sxs-lookup"><span data-stu-id="16c6b-183">Pass</span></span>
   * <span data-ttu-id="16c6b-184">Pss w/ conditions</span><span class="sxs-lookup"><span data-stu-id="16c6b-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="16c6b-185">Out of Business.</span><span class="sxs-lookup"><span data-stu-id="16c6b-185">Out of Business</span></span>

     <span data-ttu-id="16c6b-186">Сообщите нам Разработайте модели, что можно hello результат проверки пищевых продуктов, нарушений данного hello.</span><span class="sxs-lookup"><span data-stu-id="16c6b-186">Let us develop a model that can guess hello outcome of a food inspection, given hello violations.</span></span> <span data-ttu-id="16c6b-187">Логистическая Регрессия является методом двоичной классификации, он делает toogroup смысле наши данные на две категории: **ошибкой** и **передачи**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-187">Since logistic regression is a binary classification method, it makes sense toogroup our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="16c6b-188">«Передать с условия» по-прежнему передаче, поэтому когда мы обучения модели hello, мы рассмотрим hello двух результатов эквивалент.</span><span class="sxs-lookup"><span data-stu-id="16c6b-188">A "Pass w/ Conditions" is still a Pass, so when we train hello model, we consider hello two results equivalent.</span></span> <span data-ttu-id="16c6b-189">Данные с hello других результатов («Business находятся» или «Out of Business») не используются, их удаление из наших обучающего набора.</span><span class="sxs-lookup"><span data-stu-id="16c6b-189">Data with hello other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="16c6b-190">Это должно быть нормально, поскольку эти две категории составляют очень небольшой процент от hello результаты все равно.</span><span class="sxs-lookup"><span data-stu-id="16c6b-190">This should be okay since these two categories make up a very small percentage of hello results anyway.</span></span>
1. <span data-ttu-id="16c6b-191">Далее нам нужно преобразовать существующую таблицу данных (`df`) в новую таблицу данных, где каждая проверка представлена в виде пары «метка-нарушение».</span><span class="sxs-lookup"><span data-stu-id="16c6b-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="16c6b-192">В нашем случае метка `0.0` представляет неудачу, `1.0` — успех, а `-1.0` — другие результаты, помимо этих двух.</span><span class="sxs-lookup"><span data-stu-id="16c6b-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="16c6b-193">Мы отфильтровать эти другие результаты при вычислении hello нового кадра данных.</span><span class="sxs-lookup"><span data-stu-id="16c6b-193">We filter those other results out when computing hello new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="16c6b-194">какие hello toosee с меткой данных, который выглядит как, давайте получение одной строки.</span><span class="sxs-lookup"><span data-stu-id="16c6b-194">toosee what hello labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="16c6b-195">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="16c6b-195">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a><span data-ttu-id="16c6b-196">Создать модель логистической регрессии из входного hello кадр данных</span><span class="sxs-lookup"><span data-stu-id="16c6b-196">Create a logistic regression model from hello input dataframe</span></span>
<span data-ttu-id="16c6b-197">Наш последняя задача — tooconvert hello, с меткой данных в формате, который можно проанализировать с логистической регрессии.</span><span class="sxs-lookup"><span data-stu-id="16c6b-197">Our final task is tooconvert hello labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="16c6b-198">Алгоритм логистической регрессии Hello ввода tooa должен быть набор *пары вектор функция меток*, где «вектора компонента» hello — вектор чисел, представляющий точку ввода hello.</span><span class="sxs-lookup"><span data-stu-id="16c6b-198">hello input tooa logistic regression algorithm should be a set of *label-feature vector pairs*, where hello "feature vector" is a vector of numbers representing hello input point.</span></span> <span data-ttu-id="16c6b-199">Таким образом мы должны tooconvert нарушений «hello» столбца, который является частично структурированными и содержит количество комментариев в свободной форме, tooan массив действительных чисел, компьютер может с легкостью понять.</span><span class="sxs-lookup"><span data-stu-id="16c6b-199">So, we need tooconvert hello "violations" column, which is semi-structured and contains many comments in free-text, tooan array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="16c6b-200">Один из подходов Стандартная машины обучения для обработки естественного языка — tooassign каждого distinct слово «индекс», а затем передайте вектор toohello алгоритма машинного обучения таким образом, значение каждого индекса содержит hello относительной частоте слова в тексте hello Строка.</span><span class="sxs-lookup"><span data-stu-id="16c6b-200">One standard machine learning approach for processing natural language is tooassign each distinct word an "index", and then pass a vector toohello machine learning algorithm such that each index's value contains hello relative frequency of that word in hello text string.</span></span>

<span data-ttu-id="16c6b-201">MLlib предоставляет простой способ tooperform этой операции.</span><span class="sxs-lookup"><span data-stu-id="16c6b-201">MLlib provides an easy way tooperform this operation.</span></span> <span data-ttu-id="16c6b-202">Во-первых «разметки» каждого нарушений строка tooget hello отдельные слова в каждой строке.</span><span class="sxs-lookup"><span data-stu-id="16c6b-202">First, "tokenize" each violations string tooget hello individual words in each string.</span></span> <span data-ttu-id="16c6b-203">Затем с помощью `HashingTF` tooconvert каждого набора маркеры в вектора компонента, который затем может быть tooconstruct алгоритм логистической регрессии переданный toohello модели.</span><span class="sxs-lookup"><span data-stu-id="16c6b-203">Then, use a `HashingTF` tooconvert each set of tokens into a feature vector that can then be passed toohello logistic regression algorithm tooconstruct a model.</span></span> <span data-ttu-id="16c6b-204">Для выполнения всех этих действий последовательно используем оператор pipeline.</span><span class="sxs-lookup"><span data-stu-id="16c6b-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a><span data-ttu-id="16c6b-205">Оценка модели hello на отдельном проверочный набор данных</span><span class="sxs-lookup"><span data-stu-id="16c6b-205">Evaluate hello model on a separate test dataset</span></span>
<span data-ttu-id="16c6b-206">Мы используем hello модель, созданную ранее слишком*прогнозирования* какие hello будет результаты новых проверок, в зависимости от нарушений hello, которые были обнаружены.</span><span class="sxs-lookup"><span data-stu-id="16c6b-206">We can use hello model we created earlier too*predict* what hello results of new inspections will be, based on hello violations that were observed.</span></span> <span data-ttu-id="16c6b-207">Мы обучения этой модели на наборе данных hello **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-207">We trained this model on hello dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="16c6b-208">Сообщите нам использовать второй набор данных, **Food_Inspections2.csv**, слишком*оценки* hello стойкость эта модель новые данные.</span><span class="sxs-lookup"><span data-stu-id="16c6b-208">Let us use a second dataset, **Food_Inspections2.csv**, too*evaluate* hello strength of this model on new data.</span></span> <span data-ttu-id="16c6b-209">Этот второй набор данных (**Food_Inspections2.csv**) уже должен быть в контейнере хранилища по умолчанию hello, связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="16c6b-209">This second data set (**Food_Inspections2.csv**) should already be in hello default storage container associated with hello cluster.</span></span>

1. <span data-ttu-id="16c6b-210">Hello следующий фрагмент кода создает новый кадр данных, **predictionsDf** , содержащий созданные hello модели прогнозирования hello.</span><span class="sxs-lookup"><span data-stu-id="16c6b-210">hello following snippet creates a new dataframe, **predictionsDf** that contains hello prediction generated by hello model.</span></span> <span data-ttu-id="16c6b-211">фрагмент кода Hello также создает временную таблицу с именем **прогнозов** основании hello кадр данных.</span><span class="sxs-lookup"><span data-stu-id="16c6b-211">hello snippet also creates a temporary table called **Predictions** based on hello dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="16c6b-212">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="16c6b-212">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="16c6b-213">Посмотрите на один hello прогнозов.</span><span class="sxs-lookup"><span data-stu-id="16c6b-213">Look at one of hello predictions.</span></span> <span data-ttu-id="16c6b-214">выполните этот фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="16c6b-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="16c6b-215">Прогноз для hello первой записью в hello проверочного набора данных не существует.</span><span class="sxs-lookup"><span data-stu-id="16c6b-215">There is a prediction for hello first entry in hello test data set.</span></span>
1. <span data-ttu-id="16c6b-216">Hello `model.transform()` метод применим hello же преобразования tooany новых данных с одной схеме hello и моментом прибытия на прогноз результатов как tooclassify hello данных.</span><span class="sxs-lookup"><span data-stu-id="16c6b-216">hello `model.transform()` method applies hello same transformation tooany new data with hello same schema, and arrive at a prediction of how tooclassify hello data.</span></span> <span data-ttu-id="16c6b-217">Мы можем сделать некоторые простые статистики tooget представление о насколько точны прогнозы нашей:</span><span class="sxs-lookup"><span data-stu-id="16c6b-217">We can do some simple statistics tooget a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="16c6b-218">Hello вывод выглядит следующим образом следующие hello.</span><span class="sxs-lookup"><span data-stu-id="16c6b-218">hello output looks like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="16c6b-219">Использование логистической регрессии с Spark дает нам точную модель hello связь между нарушений описания на английском языке и заданного business будет "пройден" или "не пройден проверки пищевых продуктов.</span><span class="sxs-lookup"><span data-stu-id="16c6b-219">Using logistic regression with Spark gives us an accurate model of hello relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-hello-prediction"></a><span data-ttu-id="16c6b-220">Создайте визуальное представление прогноза hello</span><span class="sxs-lookup"><span data-stu-id="16c6b-220">Create a visual representation of hello prediction</span></span>
<span data-ttu-id="16c6b-221">Теперь мы можно создать toohelp окончательного визуализации, которые нам обсуждения hello результатов данного теста.</span><span class="sxs-lookup"><span data-stu-id="16c6b-221">We can now construct a final visualization toohelp us reason about hello results of this test.</span></span>

1. <span data-ttu-id="16c6b-222">Мы начнем путем извлечения различные прогнозы hello и результаты из hello **прогнозов** временной таблицы, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="16c6b-222">We start by extracting hello different predictions and results from hello **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="16c6b-223">Hello следующие запросы разделения hello выходные данные в виде *true_positive*, *false_positive*, *true_negative*, и *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="16c6b-223">hello following queries separate hello output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="16c6b-224">В запросах hello ниже, мы отключить визуализации с помощью `-q` и также сохранить hello выходные данные (с помощью `-o`) как блоки данных, который затем используется с hello `%%local` магическое значение.</span><span class="sxs-lookup"><span data-stu-id="16c6b-224">In hello queries below, we turn off visualization by using `-q` and also save hello output (by using `-o`) as dataframes that can be then used with hello `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="16c6b-225">Наконец, используйте следующий фрагмент toogenerate hello построения использование hello **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-225">Finally, use hello following snippet toogenerate hello plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="16c6b-226">Вы увидите hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="16c6b-226">You should see hello following output:</span></span>

    <span data-ttu-id="16c6b-227">![Выходные данные приложения машинного обучения Spark — круговая диаграмма с процентными значениями для проверок качества пищевых продуктов, которые не были пройдены.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Результаты машинного обучения Spark")</span><span class="sxs-lookup"><span data-stu-id="16c6b-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="16c6b-228">На этой диаграмме «позитивные» результат ссылается toohello сбой проверки пищевых продуктов, а отрицательный результат ссылается переданный проверки tooa.</span><span class="sxs-lookup"><span data-stu-id="16c6b-228">In this chart, a "positive" result refers toohello failed food inspection, while a negative result refers tooa passed inspection.</span></span>

## <a name="shut-down-hello-notebook"></a><span data-ttu-id="16c6b-229">Завершение работы записной книжки hello</span><span class="sxs-lookup"><span data-stu-id="16c6b-229">Shut down hello notebook</span></span>
<span data-ttu-id="16c6b-230">После завершения работы приложения hello, следует закрыть hello записной книжки toorelease hello ресурсы.</span><span class="sxs-lookup"><span data-stu-id="16c6b-230">After you have finished running hello application, you should shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="16c6b-231">toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**.</span><span class="sxs-lookup"><span data-stu-id="16c6b-231">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="16c6b-232">Это завершает работу и закрывает hello ноутбука.</span><span class="sxs-lookup"><span data-stu-id="16c6b-232">This shuts down and closes hello notebook.</span></span>

## <span data-ttu-id="16c6b-233"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="16c6b-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="16c6b-234">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c6b-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="16c6b-235">Сценарии</span><span class="sxs-lookup"><span data-stu-id="16c6b-235">Scenarios</span></span>
* [<span data-ttu-id="16c6b-236">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="16c6b-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="16c6b-237">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="16c6b-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="16c6b-238">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="16c6b-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="16c6b-239">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c6b-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="16c6b-240">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="16c6b-240">Create and run applications</span></span>
* [<span data-ttu-id="16c6b-241">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="16c6b-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="16c6b-242">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="16c6b-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="16c6b-243">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="16c6b-243">Tools and extensions</span></span>
* [<span data-ttu-id="16c6b-244">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений</span><span class="sxs-lookup"><span data-stu-id="16c6b-244">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="16c6b-245">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="16c6b-245">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="16c6b-246">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c6b-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="16c6b-247">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c6b-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="16c6b-248">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="16c6b-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="16c6b-249">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="16c6b-249">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="16c6b-250">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="16c6b-250">Manage resources</span></span>
* [<span data-ttu-id="16c6b-251">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="16c6b-251">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="16c6b-252">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="16c6b-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
