---
title: "Использование средств визуализации данных с помощью Spark BI в Azure HDInsight | Документация Майкрософт"
description: "Используйте средства визуализации данных для аналитики с помощью Apache Spark BI в кластерах HDInsight"
keywords: "apache spark bi, spark bi, визуализация данных spark, бизнес-аналитика spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 49dd161049ac442081fe6d26cf8bd3a56a2e0687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="82d9f-104">Использование средств визуализации данных с помощью Apache Spark BI в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="82d9f-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="82d9f-105">Узнайте, как использовать средства визуализации данных, такие как Power BI и Tableau, для анализа набора необработанных демонстрационных данных с помощью Apache Spark BI в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82d9f-105">Learn how to use data visualization tools such as Power BI and Tableau to analyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="82d9f-106">Возможности подключения к инструментам бизнес-аналитики, описываемые в этой статье, не поддерживаются в Spark 2.1 в Azure HDInsight 3.6 (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="82d9f-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="82d9f-107">Поддерживается только Spark версий 1.6 и 2.0 (HDInsight 3.4 и HDInsight 3.5 соответственно).</span><span class="sxs-lookup"><span data-stu-id="82d9f-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="82d9f-108">Это руководство также доступно в виде записной книжки Jupyter в кластере HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="82d9f-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="82d9f-109">Фрагменты кода Python можно выполнять непосредственно в записной книжке.</span><span class="sxs-lookup"><span data-stu-id="82d9f-109">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="82d9f-110">Чтобы выполнить действия в руководстве из записной книжки, создайте кластер Spark, запустите записную книжку Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), а затем запустите записную книжку **Использование средств бизнес-аналитики с Apache Spark в HDInsight.ipynb** в папке **Python**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-110">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under the **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82d9f-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82d9f-111">Prerequisites</span></span>

* <span data-ttu-id="82d9f-112">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82d9f-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="82d9f-113">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="82d9f-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="82d9f-114"><a name="hivetable"></a>Подготовка данных для визуализации данных Spark</span><span class="sxs-lookup"><span data-stu-id="82d9f-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="82d9f-115">В этом разделе мы используем записную книжку [Jupyter](https://jupyter.org) из кластера HDInsight Spark, для выполнения заданий, которые обрабатывают необработанные демонстрационные данные и сохраняют их в виде таблицы.</span><span class="sxs-lookup"><span data-stu-id="82d9f-115">In this section, we use the [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster to run jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="82d9f-116">В качестве демонстрационных данных выступает CSV-файл (hvac.csv), доступный на всех кластерах по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="82d9f-116">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="82d9f-117">После сохранения данных в виде таблицы можно переходить к следующему разделу, в котором мы используем средства бизнес-аналитики для подключения к таблице и последующей визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="82d9f-117">Once your data is saved as a table, in the next section we use BI tools to connect to the table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="82d9f-118">Если вы выполняете действия, описанные в этой статье, после инструкций из статьи о [выполнении интерактивных запросов в кластере Spark в HDInsight](hdinsight-apache-spark-load-data-run-query.md), можно сразу перейти к шагу 8 ниже.</span><span class="sxs-lookup"><span data-stu-id="82d9f-118">If you are performing the steps in this article after completing the instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip to Step 8 below.</span></span>
>

1. <span data-ttu-id="82d9f-119">На начальной панели [портала Azure](https://portal.azure.com/)щелкните плитку кластера Spark (если она закреплена на начальной панели).</span><span class="sxs-lookup"><span data-stu-id="82d9f-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="82d9f-120">Кроме того, вы можете перейти к кластеру, последовательно щелкнув **Просмотреть все** > **Кластеры HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="82d9f-121">В колонке кластера Spark щелкните **Панель мониторинга кластера**, а затем выберите **Записная книжка Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="82d9f-122">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="82d9f-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82d9f-123">Также можно открыть Jupyter Notebook для своего кластера, открыв следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="82d9f-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="82d9f-124">Замените **CLUSTERNAME** именем кластера:</span><span class="sxs-lookup"><span data-stu-id="82d9f-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="82d9f-125">Создайте записную книжку.</span><span class="sxs-lookup"><span data-stu-id="82d9f-125">Create a notebook.</span></span> <span data-ttu-id="82d9f-126">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="82d9f-127">![Создание записной книжки Jupyter для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Создание записной книжки Jupyter для Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="82d9f-128">Будет создана и открыта записная книжка с именем Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="82d9f-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="82d9f-129">Щелкните имя записной книжки в верхней части страницы сверху и введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="82d9f-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="82d9f-130">![Указание имени записной книжки для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Указание имени записной книжки для Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-130">![Provide a name for the notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for the notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="82d9f-131">Так как записная книжка была создана с помощью ядра PySpark, задавать контексты явно необязательно.</span><span class="sxs-lookup"><span data-stu-id="82d9f-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="82d9f-132">Контексты Spark и Hive будут созданы автоматически при выполнении первой ячейки кода.</span><span class="sxs-lookup"><span data-stu-id="82d9f-132">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="82d9f-133">Можно начать с импорта различных типов, необходимых для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="82d9f-133">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="82d9f-134">Для этого наведите курсор на ячейку и нажмите клавиши **SHIFT+ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-134">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="82d9f-135">Загрузите демонстрационные данные во временную таблицу.</span><span class="sxs-lookup"><span data-stu-id="82d9f-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="82d9f-136">При создании кластера Spark в HDInsight файл с демонстрационными данными **hvac.csv** копируется в связанную учетную запись хранения по следующему пути: **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-136">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="82d9f-137">Вставьте следующий фрагмент кода в пустую ячейку и нажмите клавиши **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-137">In an empty cell, paste the following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="82d9f-138">Этот фрагмент кода регистрирует данные в таблице с именем **hvac**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-138">This snippet registers the data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. <span data-ttu-id="82d9f-139">Убедитесь, что таблица была успешно создана.</span><span class="sxs-lookup"><span data-stu-id="82d9f-139">Verify that the table was successfully created.</span></span> <span data-ttu-id="82d9f-140">Можно использовать волшебное слово `%%sql` для непосредственного выполнения запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="82d9f-140">You can use the `%%sql` magic to run Hive queries directly.</span></span> <span data-ttu-id="82d9f-141">Дополнительные сведения о магической команде `%%sql`, а также других магических командах, доступных в ядре PySpark, приведены в статье [Ядра для записных книжек Jupyter с кластерами Apache Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="82d9f-141">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="82d9f-142">Вы увидите примерно следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="82d9f-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="82d9f-143">Таблицами Hive являются только те таблицы, в которых в столбце **isTemporary** указано значение false. Такие таблицы будут храниться в хранилище метаданных, и к ним могут получать доступ средства бизнес-аналитики.</span><span class="sxs-lookup"><span data-stu-id="82d9f-143">Only the tables that have false under the **isTemporary** column are hive tables that are stored in the metastore and can be accessed from the BI tools.</span></span> <span data-ttu-id="82d9f-144">В этом руководстве мы подключимся к созданной нами таблице **hvac**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-144">In this tutorial, we connect to the **hvac** table we created.</span></span>

8. <span data-ttu-id="82d9f-145">Убедитесь, что таблица содержит нужные данные.</span><span class="sxs-lookup"><span data-stu-id="82d9f-145">Verify that the table contains the intended data.</span></span> <span data-ttu-id="82d9f-146">Вставьте следующий фрагмент кода в пустую ячейку в записной книжке и нажмите **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-146">In an empty cell in the notebook, copy the following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="82d9f-147">Завершите работу записной книжки для освобождения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="82d9f-147">Shut down the notebook to release the resources.</span></span> <span data-ttu-id="82d9f-148">Для этого в записной книжке в меню **Файл** выберите пункт **Close and Halt** (Закрыть и остановить).</span><span class="sxs-lookup"><span data-stu-id="82d9f-148">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="82d9f-149"><a name="powerbi"></a>Использование Power BI для визуализации данных Spark</span><span class="sxs-lookup"><span data-stu-id="82d9f-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="82d9f-150">Этот раздел применим только к Spark 1.6 в HDInsight 3.4 и к Spark 2.0 в HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="82d9f-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="82d9f-151">После сохранения данных в виде таблицы можно воспользоваться Power BI для подключения к данным и визуализировать их для создания отчетов, панелей мониторинга и т. д.</span><span class="sxs-lookup"><span data-stu-id="82d9f-151">Once you have saved the data as a table, you can use Power BI to connect to the data and visualize it to create reports, dashboards, etc.</span></span>

1. <span data-ttu-id="82d9f-152">Убедитесь, что у вас есть доступ к Power BI.</span><span class="sxs-lookup"><span data-stu-id="82d9f-152">Make sure you have access to Power BI.</span></span> <span data-ttu-id="82d9f-153">Вы можете оформить подписку на бесплатную предварительную версию Power BI на сайте [http://www.powerbi.com/](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="82d9f-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="82d9f-154">Войдите в [Power BI](http://www.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="82d9f-154">Sign in to [Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="82d9f-155">В нижней части области слева щелкните **Получить данные**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-155">From the bottom of the left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="82d9f-156">На странице **Получение данных** в разделе **Импорт или подключение к данным** для **Базы данных** нажмите кнопку **Получить**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-156">On the **Get Data** page, under **Import or Connect to Data**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="82d9f-157">![Получение данных в Power BI для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Получение данных в Power BI для Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="82d9f-158">На следующем экране выберите **Spark на Azure HDInsight**, а затем щелкните **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-158">On the next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="82d9f-159">При появлении запроса введите URL-адрес кластера (`mysparkcluster.azurehdinsight.net`) и учетные данные для подключения к кластеру.</span><span class="sxs-lookup"><span data-stu-id="82d9f-159">When prompted, enter the cluster URL (`mysparkcluster.azurehdinsight.net`) and the credentials to connect to the cluster.</span></span>

    <span data-ttu-id="82d9f-160">![Подключение к Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Подключение к Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-160">![Connect to Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect to Apache Spark BI")</span></span>

    <span data-ttu-id="82d9f-161">После установления соединения Power BI начнет импорт данных из кластера Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82d9f-161">After the connection is established, Power BI starts importing data from the Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="82d9f-162">Power BI импортирует данные и добавляет набор данных **Spark** в раздел **Наборы данных**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-162">Power BI imports the data and adds a **Spark** dataset under the **Datasets** heading.</span></span> <span data-ttu-id="82d9f-163">Щелкните по набору данных, при этом откроется новый лист для визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="82d9f-163">Click the data set to open a new worksheet to visualize the data.</span></span> <span data-ttu-id="82d9f-164">Кроме того, вы можете сохранить лист в виде отчета.</span><span class="sxs-lookup"><span data-stu-id="82d9f-164">You can also save the worksheet as a report.</span></span> <span data-ttu-id="82d9f-165">Чтобы сохранить лист, выберите **Сохранить** в меню **Файл**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-165">To save a worksheet, from the **File** menu, click **Save**.</span></span>

    <span data-ttu-id="82d9f-166">![Плитка Apache Spark BI на информационной панели Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Плитка Apache Spark BI на информационной панели Power BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="82d9f-167">Обратите внимание, что в списке **Поля** справа есть таблица **hvac**, которую мы создали ранее.</span><span class="sxs-lookup"><span data-stu-id="82d9f-167">Notice that the **Fields** list on the right lists the **hvac** table you created earlier.</span></span> <span data-ttu-id="82d9f-168">Разверните таблицу, чтобы просмотреть все поля в таблице, как они были определены ранее в записной книжке.</span><span class="sxs-lookup"><span data-stu-id="82d9f-168">Expand the table to see the fields in the table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="82d9f-169">![Список таблиц на панели мониторинга Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Список таблиц на панели мониторинга Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="82d9f-170">Создайте визуализацию для отображения расхождений между целевой температурой и фактической температурой для каждого здания.</span><span class="sxs-lookup"><span data-stu-id="82d9f-170">Build a visualization to show the variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="82d9f-171">Для визуализации данных выберите **Диаграмма с областями** (выделена красным).</span><span class="sxs-lookup"><span data-stu-id="82d9f-171">To visualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="82d9f-172">Чтобы определить оси, перетащите поле **Код здания** в раздел **Ось**, а поля **ActualTemp**(Фактическая температура)/**TargetTemp** (Целевая температура) — в раздел **Значение**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-172">To define the axis, drag-and-drop the **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="82d9f-173">![Создание визуализаций данных Spark с помощью Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Создание визуализаций данных Spark с помощью Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="82d9f-174">По умолчанию представление показывает сумму для **фактической температуры** и **целевой температуры**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-174">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="82d9f-175">Для обоих полей из раскрывающегося списка выберите **Среднее** для получения средней фактической и целевой температуры для обоих зданий.</span><span class="sxs-lookup"><span data-stu-id="82d9f-175">For both the fields, from the drop-down, select **Average** to get an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="82d9f-176">![Создание визуализаций данных Spark с помощью Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Создание визуализаций данных Spark с помощью Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="82d9f-177">Визуализация данных должна соответствовать снимку экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="82d9f-177">Your data visualization should be similar to the one in the screenshot.</span></span> <span data-ttu-id="82d9f-178">Наведите указатель мыши на визуализацию, чтобы отобразить всплывающие подсказки с соответствующими данными.</span><span class="sxs-lookup"><span data-stu-id="82d9f-178">Move your cursor over the visualization to get tool tips with relevant data.</span></span>

    <span data-ttu-id="82d9f-179">![Создание визуализаций данных Spark с помощью Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Создание визуализаций данных Spark с помощью Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="82d9f-180">Щелкните элемент **Save** (Сохранить) в меню в верхней части и введите имя отчета.</span><span class="sxs-lookup"><span data-stu-id="82d9f-180">Click **Save** from the top menu and provide a report name.</span></span> <span data-ttu-id="82d9f-181">Можно также закрепить визуализацию.</span><span class="sxs-lookup"><span data-stu-id="82d9f-181">You can also pin the visual.</span></span> <span data-ttu-id="82d9f-182">При закреплении представление данных будет храниться на панели мониторинга, благодаря чему вы можете мгновенно отслеживать последние изменения.</span><span class="sxs-lookup"><span data-stu-id="82d9f-182">When you pin a visualization, it is stored on your dashboard so you can track the latest value at a glance.</span></span>

   <span data-ttu-id="82d9f-183">Для одного и того же набора данных можно добавить любое количество представлений с визуализацией и закреплять их на панели мониторинга для получения моментального снимка данных.</span><span class="sxs-lookup"><span data-stu-id="82d9f-183">You can add as many visualizations as you want for the same dataset and pin them to the dashboard for a snapshot of your data.</span></span> <span data-ttu-id="82d9f-184">Кроме того, кластеры Spark в HDInsight подключены к Power BI напрямую.</span><span class="sxs-lookup"><span data-stu-id="82d9f-184">Also, Spark clusters on HDInsight are connected to Power BI with direct connect.</span></span> <span data-ttu-id="82d9f-185">Это означает, что Power BI всегда имеет доступ к актуальным данным из кластера, поэтому вам не требуется планировать обновления для набора данных.</span><span class="sxs-lookup"><span data-stu-id="82d9f-185">This ensures that Power BI always has the most up-to-date data from your cluster so you do not need to schedule refreshes for the dataset.</span></span>

## <span data-ttu-id="82d9f-186"><a name="tableau"></a>Использование Tableau Desktop для визуализации данных Spark</span><span class="sxs-lookup"><span data-stu-id="82d9f-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="82d9f-187">Этот раздел применим только для кластеров Spark 1.5.2, созданных в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82d9f-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="82d9f-188">Установите [Tableau Desktop](http://www.tableau.com/products/desktop) на компьютере, на котором вы выполняете действия из этого руководства по Apache Spark BI.</span><span class="sxs-lookup"><span data-stu-id="82d9f-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="82d9f-189">Убедитесь, что на этом компьютере также установлен драйвер ODBC Microsoft Spark.</span><span class="sxs-lookup"><span data-stu-id="82d9f-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="82d9f-190">Вы можете скачать драйвер [здесь](http://go.microsoft.com/fwlink/?LinkId=616229).</span><span class="sxs-lookup"><span data-stu-id="82d9f-190">You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="82d9f-191">Запустите Tableau Desktop.</span><span class="sxs-lookup"><span data-stu-id="82d9f-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="82d9f-192">В левой области в списке сервера для подключения щелкните **Spark SQL**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-192">In the left pane, from the list of server to connect to, click **Spark SQL**.</span></span> <span data-ttu-id="82d9f-193">Если Spark SQL по умолчанию не отображается в левой области, вы можете найти его, щелкнув **Другие серверы**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-193">If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="82d9f-194">В диалоговом окне подключения Spark SQL укажите значения, показанные на снимке экрана ниже, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-194">In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="82d9f-195">![Подключение к кластеру для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Подключение к кластеру для Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-195">![Connect to a cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect to a cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="82d9f-196">Если вы установили на компьютер **драйвер Microsoft ODBC Spark** , в раскрывающемся списке проверки подлинности будет пункт [служба Microsoft Azure HDInsight](http://go.microsoft.com/fwlink/?LinkId=616229) .</span><span class="sxs-lookup"><span data-stu-id="82d9f-196">The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.</span></span>
3. <span data-ttu-id="82d9f-197">В следующем окне в раскрывающемся списке **Схема** щелкните значок **Найти**, а затем щелкните **по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-197">On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="82d9f-198">![Поиск схемы для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Поиск схемы для Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="82d9f-199">Для поля **Таблица** еще раз щелкните значок **Найти**, чтобы вывести список всех таблиц Hive, доступных в кластере.</span><span class="sxs-lookup"><span data-stu-id="82d9f-199">For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster.</span></span> <span data-ttu-id="82d9f-200">Вы должны увидеть таблицу **hvac** , созданную ранее с помощью записной книжки.</span><span class="sxs-lookup"><span data-stu-id="82d9f-200">You should see the **hvac** table you created earlier using the notebook.</span></span>

    <span data-ttu-id="82d9f-201">![Поиск схемы для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Поиск схемы для Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="82d9f-202">Перетащите таблицу в поле в правом верхней части окна.</span><span class="sxs-lookup"><span data-stu-id="82d9f-202">Drag and drop the table to the top box on the right.</span></span> <span data-ttu-id="82d9f-203">Tableau импортирует данные и отображает схему (выделено красным прямоугольником).</span><span class="sxs-lookup"><span data-stu-id="82d9f-203">Tableau imports the data and displays the schema as highlighted by the red box.</span></span>

    <span data-ttu-id="82d9f-204">![Добавление таблиц в Tableau для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Добавление таблиц в Tableau для Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="82d9f-204">![Add tables to Tableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables to Tableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="82d9f-205">Щелкните вкладку **Лист1** слева внизу.</span><span class="sxs-lookup"><span data-stu-id="82d9f-205">Click the **Sheet1** tab at the bottom left.</span></span> <span data-ttu-id="82d9f-206">Создайте визуализацию, на которой представлены средняя целевая температура фактическая температура для всех зданий для каждой даты.</span><span class="sxs-lookup"><span data-stu-id="82d9f-206">Make a visualization that shows the average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="82d9f-207">Перетащите поля **Дата** и **Код здания** в раздел **Столбцы**, а поля **Actual Temp**(Фактическая температура)/**Target Temp** (Целевая температура) — в раздел **Строки**.</span><span class="sxs-lookup"><span data-stu-id="82d9f-207">Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**.</span></span> <span data-ttu-id="82d9f-208">В разделе **Метки** выберите **Область**, которая будет использоваться для визуализации данных Spark.</span><span class="sxs-lookup"><span data-stu-id="82d9f-208">Under **Marks**, select **Area** to use an area map for Spark data visualization.</span></span>

     <span data-ttu-id="82d9f-209">![Добавление полей для визуализации данных Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Добавление полей для визуализации данных Spark")</span><span class="sxs-lookup"><span data-stu-id="82d9f-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="82d9f-210">По умолчанию значения полей температуры отображаются как статистическое выражение.</span><span class="sxs-lookup"><span data-stu-id="82d9f-210">By default, the temperature fields are shown as aggregate.</span></span> <span data-ttu-id="82d9f-211">Если необходимо отобразить среднюю температуру, это можно сделать из раскрывающегося списка, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="82d9f-211">If you want to show the average temperatures instead, you can do so from the drop-down, as shown below.</span></span>

    <span data-ttu-id="82d9f-212">![Получение среднего значения температуры для визуализации данных Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Получение среднего значения температуры для визуализации данных Spark")</span><span class="sxs-lookup"><span data-stu-id="82d9f-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="82d9f-213">Можно также наложить одну карту температуры на другую, чтобы лучше понять разницу между целевой и фактической температурой.</span><span class="sxs-lookup"><span data-stu-id="82d9f-213">You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="82d9f-214">Перемещайте указатель мыши в угол нижней области карты, пока курсор не примет форму красного кружка.</span><span class="sxs-lookup"><span data-stu-id="82d9f-214">Move the mouse to the corner of the lower area map till you see the handle shape highlighted in a red circle.</span></span> <span data-ttu-id="82d9f-215">Перетащите карту на другую карту в верхней части и отпустите кнопку мыши, когда указатель мыши примет форму красного прямоугольника.</span><span class="sxs-lookup"><span data-stu-id="82d9f-215">Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="82d9f-216">![Слияние карт для визуализации данных Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Слияние карт для визуализации данных Spark")</span><span class="sxs-lookup"><span data-stu-id="82d9f-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="82d9f-217">Визуализация данных должна измениться, как показано на снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="82d9f-217">Your data visualization should change as shown in the screenshot:</span></span>

    <span data-ttu-id="82d9f-218">![Выходные данные Tableau для визуализации данных Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Выходные данные Tableau для визуализации данных Spark")</span><span class="sxs-lookup"><span data-stu-id="82d9f-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="82d9f-219">Щелкните **Сохранить** для сохранения рабочего листа.</span><span class="sxs-lookup"><span data-stu-id="82d9f-219">Click **Save** to save the worksheet.</span></span> <span data-ttu-id="82d9f-220">Можно создать панели мониторинга и добавить на них один или несколько листов.</span><span class="sxs-lookup"><span data-stu-id="82d9f-220">You can create dashboards and add one or more sheets to it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82d9f-221">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82d9f-221">Next steps</span></span>

<span data-ttu-id="82d9f-222">Из этой статьи вы узнали, как создать кластер, как создать кадры данных Spark для запроса данных и как получить доступ к этим данным из средств бизнес-аналитики.</span><span class="sxs-lookup"><span data-stu-id="82d9f-222">So far you learned how to create a cluster, create Spark data frames to query data, and then access that data from BI tools.</span></span> <span data-ttu-id="82d9f-223">Теперь вы можете просмотреть инструкции по управлению ресурсами кластера и отладке заданий, запущенных в кластере Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="82d9f-223">You can now look at instructions on how to manage the cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="82d9f-224">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="82d9f-224">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="82d9f-225">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="82d9f-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

