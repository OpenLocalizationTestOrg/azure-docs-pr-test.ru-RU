---
title: "Выполнение интерактивных запросов в кластере Azure HDInsight Spark | Документация Майкрософт"
description: "Краткое руководство HDInsight Spark по созданию кластера Apache Spark в HDInsight."
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
ms.openlocfilehash: ada1c3d1482c68834dbbf5eabbd045a7e0c01f9f
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="6496d-104">Выполнение интерактивных запросов в кластере HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="6496d-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="6496d-105">В этой статье описано, как с помощью записной книжки Jupyter выполнять интерактивные запросы Spark SQL к кластеру Spark.</span><span class="sxs-lookup"><span data-stu-id="6496d-105">In this article, you use a Jupyter notebook to run interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="6496d-106">Записная книжка Jupyter представляет собой браузерное приложение, которое позволяет использовать интерактивный интерфейс на базе консоли в Интернете.</span><span class="sxs-lookup"><span data-stu-id="6496d-106">Jupyter notebook is a browser-based application that extends the console-based interactive experience to the Web.</span></span> <span data-ttu-id="6496d-107">Дополнительные сведения см. в [документации по записным книжкам Jupyter](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span><span class="sxs-lookup"><span data-stu-id="6496d-107">For more information, see [The Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="6496d-108">В ходе работы с этим руководством вы выполните интерактивный SQL-запрос к Spark с помощью ядра **PySpark** в записной книжке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="6496d-108">For this tutorial, you use the **PySpark** kernel in the Jupyter notebook to run an interactive Spark SQL query.</span></span> <span data-ttu-id="6496d-109">Записные книжки Jupyter в кластерах HDInsight поддерживают еще две версии ядер — **PySpark3** и **Spark**.</span><span class="sxs-lookup"><span data-stu-id="6496d-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="6496d-110">Дополнительные сведения об этих ядрах и о преимуществах **PySpark** см. в статье [Ядра для записной книжки Jupyter в кластерах Spark в Azure HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="6496d-110">For more information about the kernels, and the benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6496d-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6496d-111">Prerequisites</span></span>

* <span data-ttu-id="6496d-112">**Кластер Azure HDInsight Spark**.</span><span class="sxs-lookup"><span data-stu-id="6496d-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="6496d-113">Инструкции см. в статье [Создание кластера Apache Spark в Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="6496d-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-to-run-interactive-queries"></a><span data-ttu-id="6496d-114">Создание записной книжки Jupyter для выполнения интерактивных запросов</span><span class="sxs-lookup"><span data-stu-id="6496d-114">Create a Jupyter notebook to run interactive queries</span></span>

<span data-ttu-id="6496d-115">Чтобы выполнять запросы, мы воспользуемся тестовым набором данных, который по умолчанию всегда доступен в хранилище, связанном с кластером.</span><span class="sxs-lookup"><span data-stu-id="6496d-115">To run queries, we use sample data that is by default available in the storage associated with the cluster.</span></span> <span data-ttu-id="6496d-116">Но эти данные нужно сначала загрузить в Spark в виде кадра данных.</span><span class="sxs-lookup"><span data-stu-id="6496d-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="6496d-117">Когда кадр данных будет готов, вы сможете отправлять запросы к нему с помощью записной книжки Jupyter.</span><span class="sxs-lookup"><span data-stu-id="6496d-117">Once you have the dataframe, you can run queries on it using the Jupyter notebook.</span></span> <span data-ttu-id="6496d-118">Из этого раздела вы узнаете, как выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6496d-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="6496d-119">регистрация тестового набора данных в качестве кадра данных Spark;</span><span class="sxs-lookup"><span data-stu-id="6496d-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="6496d-120">выполнение запросов к кадру данных.</span><span class="sxs-lookup"><span data-stu-id="6496d-120">Run queries on the dataframe.</span></span>

1. <span data-ttu-id="6496d-121">Откройте [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6496d-121">Open the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="6496d-122">Если закрепили кластер на панели мониторинга, щелкните элемент кластера на панели мониторинга, чтобы открыть колонку кластера.</span><span class="sxs-lookup"><span data-stu-id="6496d-122">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="6496d-123">Если вы не закрепили кластер на панели мониторинга, в области слева щелкните **Кластеры HDInsight**, а затем выберите созданный кластер.</span><span class="sxs-lookup"><span data-stu-id="6496d-123">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="6496d-124">В разделе **Быстрые ссылки** щелкните **Панели мониторинга кластера**, а затем — **Записная книжка Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="6496d-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="6496d-125">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="6496d-125">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="6496d-126">![Открытие записной книжки Jupyter для выполнения интерактивного запроса Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Открытие записной книжки Jupyter для выполнения интерактивного запроса Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="6496d-126">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="6496d-127">Также можно открыть записную книжку Jupyter для своего кластера, открыв следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="6496d-127">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="6496d-128">Замените **CLUSTERNAME** именем кластера:</span><span class="sxs-lookup"><span data-stu-id="6496d-128">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="6496d-129">Создайте записную книжку.</span><span class="sxs-lookup"><span data-stu-id="6496d-129">Create a notebook.</span></span> <span data-ttu-id="6496d-130">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="6496d-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="6496d-131">![Создание записной книжки Jupyter для выполнения интерактивного запроса Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Создание записной книжки Jupyter для выполнения интерактивного запроса Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="6496d-131">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="6496d-132">Будет создана и открыта записная книжка с именем Untitled (Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="6496d-132">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="6496d-133">Щелкните имя записной книжки вверху и по желанию введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="6496d-133">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="6496d-134">![Указание имени записной книжки Jupter, из которой будет выполняться интерактивный запрос Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Указание имени записной книжки Jupter, из которой будет выполняться интерактивный запрос Spark")</span><span class="sxs-lookup"><span data-stu-id="6496d-134">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5. <span data-ttu-id="6496d-135">Вставьте указанный ниже код в пустую ячейку и нажмите сочетание клавиш **SHIFT + ВВОД**, чтобы выполнить код.</span><span class="sxs-lookup"><span data-stu-id="6496d-135">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="6496d-136">Код импортирует типы, необходимые для этого сценария:</span><span class="sxs-lookup"><span data-stu-id="6496d-136">The code imports the types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="6496d-137">Так как записная книжка была создана с помощью ядра PySpark, задавать контексты явно необязательно.</span><span class="sxs-lookup"><span data-stu-id="6496d-137">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="6496d-138">Контексты Spark и Hive будут созданы автоматически при выполнении первой ячейки кода.</span><span class="sxs-lookup"><span data-stu-id="6496d-138">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span>

    <span data-ttu-id="6496d-139">![Состояние интерактивного запроса Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Состояние интерактивного запроса Spark SQL")</span><span class="sxs-lookup"><span data-stu-id="6496d-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="6496d-140">При каждом запуске интерактивного запроса в Jupyter в заголовке окна веб-браузера будет отображаться состояние **(Занято)**, а также название записной книжки.</span><span class="sxs-lookup"><span data-stu-id="6496d-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="6496d-141">Кроме того, рядом с надписью **PySpark** в верхнем правом углу окна будет показан закрашенный кружок.</span><span class="sxs-lookup"><span data-stu-id="6496d-141">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="6496d-142">После завершения задания он изменится на кружок без заливки.</span><span class="sxs-lookup"><span data-stu-id="6496d-142">After the job is completed, it changes to a hollow circle.</span></span>

6. <span data-ttu-id="6496d-143">Прежде чем загружать данные в кластер Spark, давайте немного изучим их.</span><span class="sxs-lookup"><span data-stu-id="6496d-143">Before you load the data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="6496d-144">Тестовые данные, используемые в этом руководстве, доступны на всех кластерах HDInsight Spark в виде CSV-файла по адресу **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span><span class="sxs-lookup"><span data-stu-id="6496d-144">The sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="6496d-145">Эти данные демонстрируют колебания температуры в здании.</span><span class="sxs-lookup"><span data-stu-id="6496d-145">The data captures the temperature variations of a building.</span></span> <span data-ttu-id="6496d-146">Ниже вы видите несколько первых строк из этого набора данных.</span><span class="sxs-lookup"><span data-stu-id="6496d-146">Here are the first few rows of the data.</span></span>

    <span data-ttu-id="6496d-147">![Моментальный снимок данных для интерактивных запросов Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span><span class="sxs-lookup"><span data-stu-id="6496d-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="6496d-148">Создайте кадр данных и временную таблицу **hvac**, выполнив следующий код:</span><span class="sxs-lookup"><span data-stu-id="6496d-148">Create a dataframe and a temporary table (**hvac**) by running the following code.</span></span> <span data-ttu-id="6496d-149">Для целей этого руководства нам не нужно создавать во временной таблице все столбцы, присутствующие в необработанных данных в формате CSV.</span><span class="sxs-lookup"><span data-stu-id="6496d-149">For this tutorial, we do not create all the columns in the temporary table as compared to the columns in the raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse the data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer the schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="6496d-150">Когда таблица будет готова, выполните интерактивный запрос к данным с помощью следующего кода.</span><span class="sxs-lookup"><span data-stu-id="6496d-150">Once the table is created, run interactive query on the data, use the following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="6496d-151">Так как вы используете ядро PySpark, вы можете отправить интерактивный SQL-запрос непосредственно к временной таблице **hvac**, которую вы создали с помощью волшебной команды `%%sql`.</span><span class="sxs-lookup"><span data-stu-id="6496d-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on the temporary table **hvac** that you created by using the `%%sql` magic.</span></span> <span data-ttu-id="6496d-152">Дополнительные сведения о магической команде `%%sql`, а также других магических командах, доступных в ядре PySpark, приведены в статье [Ядра для записных книжек Jupyter с кластерами Apache Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="6496d-152">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="6496d-153">По умолчанию выводятся следующие табличные данные.</span><span class="sxs-lookup"><span data-stu-id="6496d-153">The following tabular output is displayed by default.</span></span>

     <span data-ttu-id="6496d-154">![Таблица результатов интерактивного запроса Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Таблица результатов интерактивного запроса Spark")</span><span class="sxs-lookup"><span data-stu-id="6496d-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="6496d-155">Результаты также можно просмотреть и в других визуализациях.</span><span class="sxs-lookup"><span data-stu-id="6496d-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="6496d-156">Например, диаграмма областей для тех же выходных данных будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="6496d-156">For example, an area graph for the same output would look like the following.</span></span>

    <span data-ttu-id="6496d-157">![Диаграмма с областями результата интерактивного запроса Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Диаграмма с областями результата интерактивного запроса Spark")</span><span class="sxs-lookup"><span data-stu-id="6496d-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="6496d-158">Завершив работу с приложением, можно закрыть записную книжку, чтобы освободить ресурсы кластера.</span><span class="sxs-lookup"><span data-stu-id="6496d-158">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="6496d-159">Для этого в записной книжке в меню **Файл** выберите пункт **Close and Halt** (Закрыть и остановить).</span><span class="sxs-lookup"><span data-stu-id="6496d-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="6496d-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6496d-160">Next step</span></span>

<span data-ttu-id="6496d-161">Из этой статьи вы узнали, как выполнять интерактивные запросы в Spark с помощью записной книжки Jupyter.</span><span class="sxs-lookup"><span data-stu-id="6496d-161">In this article you learned how to run interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="6496d-162">Теперь переходите к следующей статье, в которой объясняется, как перенести зарегистрированные в Spark данные в средство бизнес-аналитики, например в Power BI или Tableau.</span><span class="sxs-lookup"><span data-stu-id="6496d-162">Advance to the next article to see how the data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="6496d-163">Использование средств визуализации данных с помощью Apache Spark BI в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6496d-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




