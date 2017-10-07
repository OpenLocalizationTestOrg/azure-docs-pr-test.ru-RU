---
title: "aaaRun интерактивной обработки запросов на кластере Azure HDInsight Spark | Документы Microsoft"
description: "Примеры использования HDInsight Spark на как кластер toocreate Apache Spark в HDInsight."
keywords: "краткое руководство Spark,интерактивный запрос Spark,интерактивный запрос,Hdinsight Spark,Azure Spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="62eb8-104">Выполнение интерактивных запросов в кластере HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="62eb8-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="62eb8-105">В этой статье используется Jupyter записной книжки toorun интерактивного Spark SQL-запросов к кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="62eb8-105">In this article, you use a Jupyter notebook toorun interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="62eb8-106">Книжке Jupyter является приложением на основе браузера, расширяющий toohello интерактивное взаимодействие с помощью консоли hello Web.</span><span class="sxs-lookup"><span data-stu-id="62eb8-106">Jupyter notebook is a browser-based application that extends hello console-based interactive experience toohello Web.</span></span> <span data-ttu-id="62eb8-107">Дополнительные сведения см. в разделе [книжке Jupyter hello](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="62eb8-107">For more information, see [hello Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="62eb8-108">В этом учебнике используется hello **PySpark** ядра в toorun записной книжки Jupyter hello интерактивный Spark SQL-запроса.</span><span class="sxs-lookup"><span data-stu-id="62eb8-108">For this tutorial, you use hello **PySpark** kernel in hello Jupyter notebook toorun an interactive Spark SQL query.</span></span> <span data-ttu-id="62eb8-109">Записные книжки Jupyter в кластерах HDInsight поддерживают еще две версии ядер — **PySpark3** и **Spark**.</span><span class="sxs-lookup"><span data-stu-id="62eb8-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="62eb8-110">Дополнительные сведения о ядрах hello и преимущества использования hello **PySpark**, в разделе [кластеров ядер записной книжки Jupyter использования с Apache Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="62eb8-110">For more information about hello kernels, and hello benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62eb8-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="62eb8-111">Prerequisites</span></span>

* <span data-ttu-id="62eb8-112">**Кластер Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="62eb8-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="62eb8-113">Инструкции см. в статье [Создание кластера Apache Spark в Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="62eb8-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a><span data-ttu-id="62eb8-114">Создание записной книжке Jupyter toorun интерактивной обработки запросов</span><span class="sxs-lookup"><span data-stu-id="62eb8-114">Create a Jupyter notebook toorun interactive queries</span></span>

<span data-ttu-id="62eb8-115">запросы toorun мы используем образец данных, по умолчанию, доступные в hello хранилище, связанное с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="62eb8-115">toorun queries, we use sample data that is by default available in hello storage associated with hello cluster.</span></span> <span data-ttu-id="62eb8-116">Но эти данные нужно сначала загрузить в Spark в виде кадра данных.</span><span class="sxs-lookup"><span data-stu-id="62eb8-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="62eb8-117">При наличии hello кадр данных можно выполнять запросы на его с помощью книжке Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="62eb8-117">Once you have hello dataframe, you can run queries on it using hello Jupyter notebook.</span></span> <span data-ttu-id="62eb8-118">Из этого раздела вы узнаете, как выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="62eb8-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="62eb8-119">регистрация тестового набора данных в качестве кадра данных Spark;</span><span class="sxs-lookup"><span data-stu-id="62eb8-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="62eb8-120">Выполнять запросы на кадр данных hello.</span><span class="sxs-lookup"><span data-stu-id="62eb8-120">Run queries on hello dataframe.</span></span>

1. <span data-ttu-id="62eb8-121">Откройте hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="62eb8-121">Open hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="62eb8-122">Если вы выбрали мониторинга toohello toopin hello кластера, щелкните плитку кластера hello из hello мониторинга toolaunch hello кластера колонки.</span><span class="sxs-lookup"><span data-stu-id="62eb8-122">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="62eb8-123">Если не закрепить мониторинга toohello кластера hello hello левой панели, нажмите кнопку **кластеров HDInsight**и нажмите кнопку hello кластера, вы создали.</span><span class="sxs-lookup"><span data-stu-id="62eb8-123">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="62eb8-124">В разделе **Быстрые ссылки** щелкните **Панели мониторинга кластера**, а затем — **Записная книжка Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="62eb8-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="62eb8-125">При появлении запроса введите учетные данные администратора hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="62eb8-125">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="62eb8-126">![Откройте Jupyter записной книжки toorun интерактивного Spark SQL-запроса](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "откройте Jupyter записной книжки toorun интерактивного Spark SQL-запроса")</span><span class="sxs-lookup"><span data-stu-id="62eb8-126">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="62eb8-127">Также может обращаться к записной книжки Jupyter hello для кластера, открыв hello следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="62eb8-127">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="62eb8-128">Замените **CLUSTERNAME** с hello имя кластера:</span><span class="sxs-lookup"><span data-stu-id="62eb8-128">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="62eb8-129">Создайте записную книжку.</span><span class="sxs-lookup"><span data-stu-id="62eb8-129">Create a notebook.</span></span> <span data-ttu-id="62eb8-130">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="62eb8-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="62eb8-131">![Создать интерактивный запрос Spark SQL Jupyter записной книжки toorun](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "создания Jupyter записной книжки toorun интерактивного Spark SQL-запроса")</span><span class="sxs-lookup"><span data-stu-id="62eb8-131">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="62eb8-132">Создается и открывается с именем hello Untitled(Untitled.pynb) новый блокнот.</span><span class="sxs-lookup"><span data-stu-id="62eb8-132">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="62eb8-133">Щелкните имя записной книжки hello вверху hello и введите понятное имя, если требуется.</span><span class="sxs-lookup"><span data-stu-id="62eb8-133">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="62eb8-134">![Введите имя для hello Jupter записной книжки toorun интерактивных Spark запросов из](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "укажите имя для hello Jupter записной книжки toorun интерактивных Spark запросов из")</span><span class="sxs-lookup"><span data-stu-id="62eb8-134">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5. <span data-ttu-id="62eb8-135">Ниже hello вставить код в пустой ячейке и нажмите клавишу **SHIFT + ВВОД** toorun кода hello.</span><span class="sxs-lookup"><span data-stu-id="62eb8-135">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="62eb8-136">Код Hello импортирует hello типы, необходимые для этого сценария:</span><span class="sxs-lookup"><span data-stu-id="62eb8-136">hello code imports hello types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="62eb8-137">Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом.</span><span class="sxs-lookup"><span data-stu-id="62eb8-137">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="62eb8-138">контексты Spark и Hive Hello автоматически создаются при выполнении первой ячейке кода hello.</span><span class="sxs-lookup"><span data-stu-id="62eb8-138">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span>

    <span data-ttu-id="62eb8-139">![Состояние интерактивного запроса Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Состояние интерактивного запроса Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="62eb8-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="62eb8-140">Показывает каждый раз при выполнении интерактивных запросов в Jupyter, заголовок окна обозревателя вашей веб **(Busy)** состояния вместе с hello записной книжки заголовка.</span><span class="sxs-lookup"><span data-stu-id="62eb8-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="62eb8-141">Появится следующий toohello сплошной кружок **PySpark** текст в верхнем правом углу hello.</span><span class="sxs-lookup"><span data-stu-id="62eb8-141">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="62eb8-142">По завершении задания hello изменяется tooa полый круг.</span><span class="sxs-lookup"><span data-stu-id="62eb8-142">After hello job is completed, it changes tooa hollow circle.</span></span>

6. <span data-ttu-id="62eb8-143">Перед загрузкой данных hello в кластере Spark, сообщите нам найти моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="62eb8-143">Before you load hello data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="62eb8-144">Hello образцы данных, используемые в этом учебнике доступен в виде CSV-файла на всех кластерах HDInsight Spark на **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="62eb8-144">hello sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="62eb8-145">Hello данных захватывает hello температуры различные виды здания.</span><span class="sxs-lookup"><span data-stu-id="62eb8-145">hello data captures hello temperature variations of a building.</span></span> <span data-ttu-id="62eb8-146">Ниже приведены несколько первых строк данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="62eb8-146">Here are hello first few rows of hello data.</span></span>

    <span data-ttu-id="62eb8-147">![Моментальный снимок данных для интерактивных запросов Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span><span class="sxs-lookup"><span data-stu-id="62eb8-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="62eb8-148">Создайте кадр данных и временную таблицу (**кондиционирования**), выполнив следующий код hello.</span><span class="sxs-lookup"><span data-stu-id="62eb8-148">Create a dataframe and a temporary table (**hvac**) by running hello following code.</span></span> <span data-ttu-id="62eb8-149">В этом учебнике мы не создавайте все столбцы hello в hello временную таблицу сравнения toohello в виде столбцов hello необработанных данных в формате CSV.</span><span class="sxs-lookup"><span data-stu-id="62eb8-149">For this tutorial, we do not create all hello columns in hello temporary table as compared toohello columns in hello raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="62eb8-150">После создания таблицы hello построения интерактивных запросов на основе данных hello, с помощью hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="62eb8-150">Once hello table is created, run interactive query on hello data, use hello following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="62eb8-151">Так как вы используете ядра PySpark, теперь можно напрямую запустить интерактивный SQL-запроса для временной таблицы hello **кондиционирования** , созданного с помощью hello `%%sql` магическое значение.</span><span class="sxs-lookup"><span data-stu-id="62eb8-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on hello temporary table **hvac** that you created by using hello `%%sql` magic.</span></span> <span data-ttu-id="62eb8-152">Дополнительные сведения о hello `%%sql` magic и другие доступные ядра PySpark hello, magics. в разделе [ядер, доступных на записные книжки Jupyter с кластерами Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="62eb8-152">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="62eb8-153">по умолчанию отображаются следующие табличного вывода Hello.</span><span class="sxs-lookup"><span data-stu-id="62eb8-153">hello following tabular output is displayed by default.</span></span>

     <span data-ttu-id="62eb8-154">![Таблица результатов интерактивного запроса Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Таблица результатов интерактивного запроса Spark")</span><span class="sxs-lookup"><span data-stu-id="62eb8-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="62eb8-155">Можно также посмотреть результаты hello в другие представления, а также.</span><span class="sxs-lookup"><span data-stu-id="62eb8-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="62eb8-156">Например график для приветствия такие же выходные данные выглядят hello следующее.</span><span class="sxs-lookup"><span data-stu-id="62eb8-156">For example, an area graph for hello same output would look like hello following.</span></span>

    <span data-ttu-id="62eb8-157">![Диаграмма с областями результата интерактивного запроса Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Диаграмма с областями результата интерактивного запроса Spark")</span><span class="sxs-lookup"><span data-stu-id="62eb8-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="62eb8-158">Завершение работы ресурсов кластера hello toorelease записной книжки hello, после завершения работы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="62eb8-158">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="62eb8-159">toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**.</span><span class="sxs-lookup"><span data-stu-id="62eb8-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="62eb8-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62eb8-160">Next step</span></span>

<span data-ttu-id="62eb8-161">В этой статье вы узнали, каким образом toorun интерактивной обработки запросов в Spark с помощью книжке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="62eb8-161">In this article you learned how toorun interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="62eb8-162">Далее в статье toosee toohello как извлечь данные hello, зарегистрированное в Spark приращения в средство анализа бизнес-Аналитики, таких как Power BI и Tableau.</span><span class="sxs-lookup"><span data-stu-id="62eb8-162">Advance toohello next article toosee how hello data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="62eb8-163">Использование средств визуализации данных с помощью Apache Spark BI в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="62eb8-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




