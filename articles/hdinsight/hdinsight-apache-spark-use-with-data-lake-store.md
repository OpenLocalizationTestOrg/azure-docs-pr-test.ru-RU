---
title: "Использование Apache Spark для анализа данных в Azure Data Lake Store | Документация Майкрософт"
description: "Выполнение заданий Spark для анализа данных, сохраненных в Azure Data Lake Store"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 66f115c4f348ccaeb8855568ba1ad50faa442173
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="7cdf6-103">Использование кластера HDInsight Spark для анализа данных в Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7cdf6-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="7cdf6-104">В этом руководстве для выполнения задания, которое считывает данные из учетной записи Data Lake Store, используется записная книжка Jupyter, доступная в кластерах HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cdf6-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7cdf6-105">Prerequisites</span></span>

* <span data-ttu-id="7cdf6-106">Учетная запись Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="7cdf6-107">Следуйте инструкциям в разделе [Приступая к работе с хранилищем озера данных Azure на портале Azure](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7cdf6-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="7cdf6-108">Кластер Azure HDInsight Spark с Data Lake Store в качестве хранилища.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="7cdf6-109">Следуйте инструкциям в статье [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7cdf6-109">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="7cdf6-110">Подготовка данных</span><span class="sxs-lookup"><span data-stu-id="7cdf6-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="7cdf6-111">Этот шаг не нужно выполнять, если вы создали кластер HDInsight, использующий Data Lake Store в качестве хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="7cdf6-112">Процессы создания кластера добавляют демонстрационные данные в учетную запись Data Lake Store, указанную при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-112">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="7cdf6-113">Перейдите к разделу [Использование кластера HDInsight Spark с Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="7cdf6-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="7cdf6-114">Если вы создали кластер HDInsight, использующий Data Lake Store в качестве дополнительного хранилища и хранилище BLOB-объектов Azure как хранилище по умолчанию, то в учетную запись Data Lake Store сначала следует скопировать демонстрационные данные.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="7cdf6-115">Вы можете использовать пример данных из хранилища BLOB-объектов Azure, связанного с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="7cdf6-116">Для этого можно использовать [инструмент ADLCopy](http://aka.ms/downloadadlcopy) .</span><span class="sxs-lookup"><span data-stu-id="7cdf6-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="7cdf6-117">Скачайте и установите этот инструмент с помощью следующей ссылки.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="7cdf6-118">Откройте командную строку и перейдите в каталог, в который установлено средство AdlCopy, обычно `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="7cdf6-119">Выполните следующую команду, чтобы скопировать заданный большой двоичный объект из контейнера-источника в хранилище озера данных:</span><span class="sxs-lookup"><span data-stu-id="7cdf6-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="7cdf6-120">Скопируйте пример файла данных **HVAC.csv**, расположенный в папке **/HdiSamples/HdiSamples/SensorSampleData/hvac/**, в учетную запись Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="7cdf6-121">Фрагмент кода должен иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="7cdf6-122">Убедитесь, что имена файлов и пути указаны в правильном регистре.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="7cdf6-123">Вам будет предложено ввести учетные данные для подписки Azure, в которой расположена учетная запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-123">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="7cdf6-124">Вы увидите результат, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="7cdf6-124">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="7cdf6-125">Файл данных (**HVAC.csv**) будет скопирован в папку **/hvac** в учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="7cdf6-126">Использование кластера HDInsight Spark с Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7cdf6-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="7cdf6-127">На начальной панели [портала Azure](https://portal.azure.com/)щелкните элемент кластера Spark (если он закреплен на начальной панели).</span><span class="sxs-lookup"><span data-stu-id="7cdf6-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="7cdf6-128">Кроме того, вы можете перейти к кластеру, последовательно щелкнув **Просмотреть все** > **Кластеры HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="7cdf6-129">В колонке кластера Spark щелкните **Быстрые ссылки**, затем в колонке **Панель мониторинга кластера** выберите **Записная книжка Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="7cdf6-130">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7cdf6-131">Также можно открыть Jupyter Notebook для своего кластера, открыв следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="7cdf6-132">Замените **CLUSTERNAME** именем кластера:</span><span class="sxs-lookup"><span data-stu-id="7cdf6-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="7cdf6-133">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-133">Create a new notebook.</span></span> <span data-ttu-id="7cdf6-134">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="7cdf6-135">![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Создание записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="7cdf6-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="7cdf6-136">Так как записная книжка была создана с помощью ядра PySpark, задавать контексты явно необязательно.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="7cdf6-137">Контексты Spark и Hive будут созданы автоматически при выполнении первой ячейки кода.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="7cdf6-138">Можно начать с импорта различных типов, необходимых для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="7cdf6-139">Для этого вставьте следующий фрагмент кода в ячейку и нажмите сочетание клавиш **SHIFT+ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="7cdf6-140">При каждом запуске задания в Jupyter в заголовке окна веб-браузера будет отображаться состояние **(Занято)** , а также название записной книжки.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="7cdf6-141">Кроме того, рядом с надписью **PySpark** в верхнем правом углу окна будет показан закрашенный кружок.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="7cdf6-142">После завершения задания этот значок изменится на кружок без заливки.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="7cdf6-143">![Состояние задания записной книжки Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Состояние задания записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="7cdf6-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="7cdf6-144">Загрузите пример данных во временную таблицу с помощью файла **HVAC.csv** , скопированного в учетную запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="7cdf6-145">Получить доступ к данным в учетной записи хранилища озера данных можно с помощью следующего шаблона URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="7cdf6-146">Если Data Lake Store используется в качестве хранилища по умолчанию, путь к файлу HVAC.csv будет похож на следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="7cdf6-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="7cdf6-147">Можно также использовать сокращенный формат, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="7cdf6-148">Если Data Lake Store используется в качестве дополнительного хранилища, файл HVAC.csv будет находиться в расположении, куда он был скопирован, например:</span><span class="sxs-lookup"><span data-stu-id="7cdf6-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="7cdf6-149">Вставьте приведенный ниже код в пустую ячейку, замените **MYDATALAKESTORE** именем учетной записи Data Lake Store и нажмите клавиши **SHIFT+ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="7cdf6-150">Этот пример кода регистрирует данные во временной таблице с именем **hvac**.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="7cdf6-151">Так как вы используете ядро PySpark, вы можете отправить SQL-запрос непосредственно к временной таблице **hvac**, которую вы только что создали с помощью магической команды `%%sql`.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="7cdf6-152">Дополнительные сведения о волшебном слове `%%sql` , а также других волшебных словах, доступных в ядре PySpark, приведены в разделе [Ядра, доступные в записных книжках Jupyter с кластерами Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="7cdf6-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="7cdf6-153">После успешного выполнения задания по умолчанию будет показаны следующие табличные данные.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="7cdf6-154">![Вывод результатов запроса в виде таблицы](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Вывод результатов запроса в виде таблицы")</span><span class="sxs-lookup"><span data-stu-id="7cdf6-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="7cdf6-155">Результаты также можно просмотреть и в других визуализациях.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="7cdf6-156">Например, диаграмма областей для тех же выходных данных будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="7cdf6-157">![Диаграмма с областями, показывающая результат запроса](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Диаграмма с областями, показывающая результат запроса")</span><span class="sxs-lookup"><span data-stu-id="7cdf6-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="7cdf6-158">Завершив работу с приложением, следует закрыть записную книжку, чтобы освободить ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="7cdf6-159">Для этого в записной книжке в меню **Файл** выберите пункт **Close and Halt** (Закрыть и остановить).</span><span class="sxs-lookup"><span data-stu-id="7cdf6-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="7cdf6-160">Это завершит работу записной книжки и закроет ее.</span><span class="sxs-lookup"><span data-stu-id="7cdf6-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7cdf6-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7cdf6-161">Next steps</span></span>

* [<span data-ttu-id="7cdf6-162">Создание автономного приложения Scala для работы в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="7cdf6-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="7cdf6-163">Создание приложений Spark для кластера HDInsight Spark на платформе Linux с помощью средств HDInsight в наборе средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7cdf6-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="7cdf6-164">Создание приложений Spark для кластера HDInsight Spark на платформе Linux с помощью средств HDInsight в наборе средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="7cdf6-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
