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
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a>Используйте Spark MLlib toobuild машинного обучения приложения и анализ набора данных

Узнайте, как toouse Spark **MLlib** toocreate a машинного обучения toodo простого прогнозирующего анализ приложения на открытие набора данных. В этом примере используется *классификация* посредством логистической регрессии на основе встроенных библиотек машинного обучения Spark. 

> [!TIP]
> Этот пример также доступен в виде записной книжки Jupyter в кластере Spark (на платформе Linux), созданном в HDInsight. взаимодействие с ноутбука Hello позволяет выполнять фрагменты кода Python hello из записной книжки hello сам. Учебник hello toofollow в записной книжке создайте Spark кластера и запустите записной книжке Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`). Выполните записной книжки hello **Spark машинного обучения — прогнозирующей аналитики на данные проверки пищевых продуктов с помощью MLlib.ipynb** под hello **Python** папки.
>
>

MLlib — это основная библиотека Spark, содержащая множество служебных программ, которые подходят для задач машинного обучения, в частности:

* классификация;
* Регрессия
* Кластеризация
* тематического моделирования;
* сингулярного разложения и анализа по методу главных компонент;
* проверки гипотез и статистической выборки.

## <a name="what-are-classification-and-logistic-regression"></a>Сведения о классификации и логистической регрессии
*Классификация*, популярных машинного обучения задач, — процесс hello сортировки входных данных по категориям. Это задание hello объекта toofigure алгоритм классификации, как tooassign «метки» tooinput данные, предоставляемые. Например, можно рассмотреть алгоритм машинного обучения, который принимает биржевых данных в качестве входных данных и разделяет hello акций на две категории: следует продавать изменения курса акций и акции, которые должны поддерживать.

Логистическая Регрессия является hello алгоритма, который используется для классификации. API Spark для логистической регрессии подходит для задач *двоичной классификации* или разделения входных данных на две группы. Дополнительные сведения о логистической регрессии см. в статье [Википедии](https://en.wikipedia.org/wiki/Logistic_regression).

Таким образом, процесс hello логистической регрессии производит *логистической функции* , может быть используется toopredict hello вероятности, вектор ввода относится в одну группу или других hello.  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>Пример прогнозного анализа на основе данных контроля качества пищевых продуктов
В этом примере используется Spark tooperform некоторые прогнозирующей аналитики на данные проверки пищевых продуктов (**Food_Inspections1.csv**), был получен через hello [портал данных Город Чикаго](https://data.cityofchicago.org/). Этот набор данных содержит сведения о пищевых продуктов установление проверок, которые проводились в Чикаго, включая сведения о каждом установлении, нарушений hello найден (если таковые имеются) и hello результаты проверки hello. уже находится в учетной записи хранилища hello, связанной с кластером hello в CSV-файла Hello **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.

В следующие действия hello разработке toosee модели, что требуется toopass или сбой проверки пищевых продуктов.

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>Начало создания приложения машинного обучения Spark MMLib
1. Из hello [портал Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели). Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.   
1. Из колонки кластера Spark hello, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **книжке Jupyter**. При появлении запроса введите учетные данные администратора hello hello кластера.

   > [!NOTE]
   > Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере. Замените **CLUSTERNAME** с hello имя кластера:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. Создайте записную книжку. Щелкните **Создать**, а затем выберите **PySpark**.

    ![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Создание записной книжки Jupyter")
1. Создается и открывается с именем hello Untitled.pynb новый блокнот. Щелкните имя записной книжки hello вверху hello и введите понятное имя.

    ![Введите имя для ноутбука hello](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "укажите имя для ноутбука hello")
1. Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом. контексты Spark и Hive Hello автоматически создаются при выполнении первой ячейке кода hello. Можно приступать к созданию машинного обучения приложения путем импорта hello типы, необходимые для этого сценария. toodo таким образом, поместите курсор hello в ячейке hello и нажмите клавишу **SHIFT + ВВОД**.

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>Создание входной таблицы данных
Мы используем `sqlContext` tooperform преобразования структурированных данных. Hello первой задачей является данных образец hello tooload ((**Food_Inspections1.csv**)) в Spark SQL *кадр данных*.

1. Поскольку hello необработанные данные в формате CSV, мы должны toouse hello Spark контекста toopull все строки файла hello в память как неструктурированных текстовых; затем используется tooparse библиотеки Python CSV каждую строку отдельно.

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. Теперь у нас есть hello CSV-файл как RDD.  схемы hello toounderstand данных hello, нам получить одну строку из hello RDD.

        inspections.take(1)

    Вы должны увидеть результаты hello следующим образом:

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
1. Hello выше выходных данных дает представление о схеме hello hello входного файла. Он включает hello имени каждого установление hello введите установление, адрес hello, hello данных проверок hello и расположения hello, среди прочего. Позволяет выбрать несколько столбцов, которые полезны для прогнозирующего анализа и сгруппировать результаты hello в кадр данных, который мы затем использовать toocreate временной таблицы.

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. Теперь у нас есть *таблица данных*, `df`, на основе которой можно выполнять анализ. У нас также есть временная таблица **CountResults**. Мы включили нужных в кадр данных hello четырех столбцов: **идентификатор**, **имя**, **результатов**, и **нарушений**.

    Давайте небольшую выборку данных hello:

        df.show(5)

    Вы должны увидеть результаты hello следующим образом:

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

## <a name="understand-hello-data"></a>Понимание данных hello
1. Давайте начнем tooget представление о наш набор данных содержит. Например, каковы hello различных значений в hello **результатов** столбца?

        df.select('results').distinct().show()

    Вы должны увидеть результаты hello следующим образом:

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
1. Быстрый визуализации можете помочь нам причина о распределении hello этих результатов. Мы уже имеются данные hello во временной таблице **CountResults**. Можно выполнить следующий SQL-запрос к таблице tooget hello hello лучше понять распределение результатов hello.

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    Hello `%%sql` следуют магическое `-o countResultsdf` гарантирует, что hello выходных данных запроса hello сохраняется локально на сервере Jupyter hello (обычно hello головному узлу кластера hello). Hello выходные данные сохраняются в виде [Pandas](http://pandas.pydata.org/) кадр данных с hello указано имя **countResultsdf**.

    Вы должны увидеть результаты hello следующим образом:

    ![Результат SQL-запроса](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Результат SQL-запроса")

    Дополнительные сведения о hello `%%sql` magic и другие доступные ядра PySpark hello, magics. в разделе [ядер, доступных на записные книжки Jupyter с кластерами Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
1. Можно также использовать Matplotlib, библиотеку используется tooconstruct визуализации данных, toocreate построение. Так как hello рисунка должны быть созданы из локально hello материализованные **countResultsdf** кадр данных, фрагмент кода hello должно начинаться с hello `%%local` магическое значение. Это гарантирует, что hello код запускается локально на сервере Jupyter hello.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Вы должны увидеть результаты hello следующим образом:

    ![Выходные данные приложения машинного обучения Spark — круговая диаграмма с пятью отдельными результатами проверки](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Результаты машинного обучения Spark")
1. Проверка может дать один из 5 следующих результатов:

   * Business not located;
   * Fail;
   * Pass;
   * Pss w/ conditions
   * Out of Business.

     Сообщите нам Разработайте модели, что можно hello результат проверки пищевых продуктов, нарушений данного hello. Логистическая Регрессия является методом двоичной классификации, он делает toogroup смысле наши данные на две категории: **ошибкой** и **передачи**. «Передать с условия» по-прежнему передаче, поэтому когда мы обучения модели hello, мы рассмотрим hello двух результатов эквивалент. Данные с hello других результатов («Business находятся» или «Out of Business») не используются, их удаление из наших обучающего набора. Это должно быть нормально, поскольку эти две категории составляют очень небольшой процент от hello результаты все равно.
1. Далее нам нужно преобразовать существующую таблицу данных (`df`) в новую таблицу данных, где каждая проверка представлена в виде пары «метка-нарушение». В нашем случае метка `0.0` представляет неудачу, `1.0` — успех, а `-1.0` — другие результаты, помимо этих двух. Мы отфильтровать эти другие результаты при вычислении hello нового кадра данных.

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    какие hello toosee с меткой данных, который выглядит как, давайте получение одной строки.

        labeledData.take(1)

    Вы должны увидеть результаты hello следующим образом:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a>Создать модель логистической регрессии из входного hello кадр данных
Наш последняя задача — tooconvert hello, с меткой данных в формате, который можно проанализировать с логистической регрессии. Алгоритм логистической регрессии Hello ввода tooa должен быть набор *пары вектор функция меток*, где «вектора компонента» hello — вектор чисел, представляющий точку ввода hello. Таким образом мы должны tooconvert нарушений «hello» столбца, который является частично структурированными и содержит количество комментариев в свободной форме, tooan массив действительных чисел, компьютер может с легкостью понять.

Один из подходов Стандартная машины обучения для обработки естественного языка — tooassign каждого distinct слово «индекс», а затем передайте вектор toohello алгоритма машинного обучения таким образом, значение каждого индекса содержит hello относительной частоте слова в тексте hello Строка.

MLlib предоставляет простой способ tooperform этой операции. Во-первых «разметки» каждого нарушений строка tooget hello отдельные слова в каждой строке. Затем с помощью `HashingTF` tooconvert каждого набора маркеры в вектора компонента, который затем может быть tooconstruct алгоритм логистической регрессии переданный toohello модели. Для выполнения всех этих действий последовательно используем оператор pipeline.

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a>Оценка модели hello на отдельном проверочный набор данных
Мы используем hello модель, созданную ранее слишком*прогнозирования* какие hello будет результаты новых проверок, в зависимости от нарушений hello, которые были обнаружены. Мы обучения этой модели на наборе данных hello **Food_Inspections1.csv**. Сообщите нам использовать второй набор данных, **Food_Inspections2.csv**, слишком*оценки* hello стойкость эта модель новые данные. Этот второй набор данных (**Food_Inspections2.csv**) уже должен быть в контейнере хранилища по умолчанию hello, связанные с кластером hello.

1. Hello следующий фрагмент кода создает новый кадр данных, **predictionsDf** , содержащий созданные hello модели прогнозирования hello. фрагмент кода Hello также создает временную таблицу с именем **прогнозов** основании hello кадр данных.

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    Вы должны увидеть результаты hello следующим образом:

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
1. Посмотрите на один hello прогнозов. выполните этот фрагмент кода:

        predictionsDf.take(1)

   Прогноз для hello первой записью в hello проверочного набора данных не существует.
1. Hello `model.transform()` метод применим hello же преобразования tooany новых данных с одной схеме hello и моментом прибытия на прогноз результатов как tooclassify hello данных. Мы можем сделать некоторые простые статистики tooget представление о насколько точны прогнозы нашей:

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    Hello вывод выглядит следующим образом следующие hello.

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    Использование логистической регрессии с Spark дает нам точную модель hello связь между нарушений описания на английском языке и заданного business будет "пройден" или "не пройден проверки пищевых продуктов.

## <a name="create-a-visual-representation-of-hello-prediction"></a>Создайте визуальное представление прогноза hello
Теперь мы можно создать toohelp окончательного визуализации, которые нам обсуждения hello результатов данного теста.

1. Мы начнем путем извлечения различные прогнозы hello и результаты из hello **прогнозов** временной таблицы, созданной ранее. Hello следующие запросы разделения hello выходные данные в виде *true_positive*, *false_positive*, *true_negative*, и *false_negative*. В запросах hello ниже, мы отключить визуализации с помощью `-q` и также сохранить hello выходные данные (с помощью `-o`) как блоки данных, который затем используется с hello `%%local` магическое значение.

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. Наконец, используйте следующий фрагмент toogenerate hello построения использование hello **Matplotlib**.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Вы увидите hello следующие выходные данные:

    ![Выходные данные приложения машинного обучения Spark — круговая диаграмма с процентными значениями для проверок качества пищевых продуктов, которые не были пройдены.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Результаты машинного обучения Spark")

    На этой диаграмме «позитивные» результат ссылается toohello сбой проверки пищевых продуктов, а отрицательный результат ссылается переданный проверки tooa.

## <a name="shut-down-hello-notebook"></a>Завершение работы записной книжки hello
После завершения работы приложения hello, следует закрыть hello записной книжки toorelease hello ресурсы. toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**. Это завершает работу и закрывает hello ноутбука.

## <a name="seealso"></a>Дополнительные материалы
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Сценарии
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Создание и запуск приложений
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Средства и расширения
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)
