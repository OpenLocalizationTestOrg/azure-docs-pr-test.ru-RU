---
title: "aaaUse Apache Spark tooanalyze данные в хранилище Озера данных Azure | Документы Microsoft"
description: "Запуск заданий Spark tooanalyze данные, хранящиеся в хранилище Озера данных Azure"
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
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a><span data-ttu-id="c1664-103">Использовать данные tooanalyze кластера HDInsight Spark в хранилище Озера данных</span><span class="sxs-lookup"><span data-stu-id="c1664-103">Use HDInsight Spark cluster tooanalyze data in Data Lake Store</span></span>

<span data-ttu-id="c1664-104">В этом учебнике используется книжке Jupyter доступны с кластерами HDInsight Spark toorun задание, которое считывает данные из учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="c1664-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters toorun a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1664-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c1664-105">Prerequisites</span></span>

* <span data-ttu-id="c1664-106">Учетная запись Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c1664-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="c1664-107">Следуйте инструкциям hello в [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c1664-107">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="c1664-108">Кластер Azure HDInsight Spark с Data Lake Store в качестве хранилища.</span><span class="sxs-lookup"><span data-stu-id="c1664-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="c1664-109">Следуйте инструкциям hello в [создать кластер HDInsight в хранилище Озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c1664-109">Follow hello instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-hello-data"></a><span data-ttu-id="c1664-110">Подготовка данных hello</span><span class="sxs-lookup"><span data-stu-id="c1664-110">Prepare hello data</span></span>

> [!NOTE]
> <span data-ttu-id="c1664-111">Необязательно tooperform этот шаг при создании кластера HDInsight hello с хранилища Озера данных в качестве хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c1664-111">You do not need tooperform this step if you have created hello HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="c1664-112">процессы создания кластера Hello добавляет некоторые демонстрационные данные в учетной записи хранилища Озера данных hello, указанным при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="c1664-112">hello cluster creation processes adds some sample data in hello Data Lake Store account that you specify while creating hello cluster.</span></span> <span data-ttu-id="c1664-113">Пропустите раздел toohello [HDInsight Spark использования кластера с хранилища Озера данных](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="c1664-113">Skip toohello section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="c1664-114">При создании кластера HDInsight с хранилища Озера данных как дополнительное хранилище и больших двоичных объектов хранилища Azure хранения по умолчанию, следует скопировать эти некоторых toohello данных образец хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="c1664-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data toohello Data Lake Store account.</span></span> <span data-ttu-id="c1664-115">Можно использовать hello демонстрационных данных из больших двоичных объектов хранилища Azure, связанной с кластером HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="c1664-115">You can use hello sample data from hello Azure Storage Blob associated with hello HDInsight cluster.</span></span> <span data-ttu-id="c1664-116">Можно использовать hello [ADLCopy средство](http://aka.ms/downloadadlcopy) toodo так.</span><span class="sxs-lookup"><span data-stu-id="c1664-116">You can use hello [ADLCopy tool](http://aka.ms/downloadadlcopy) toodo so.</span></span> <span data-ttu-id="c1664-117">Загрузите и установите программу hello ссылке hello.</span><span class="sxs-lookup"><span data-stu-id="c1664-117">Download and install hello tool from hello link.</span></span>

1. <span data-ttu-id="c1664-118">Откройте командную строку и перейдите в каталог toohello AdlCopy установки, обычно `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="c1664-118">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="c1664-119">Запустите hello, следующая команда toocopy конкретного BLOB-объектов из hello исходный контейнер tooa хранилища Озера данных:</span><span class="sxs-lookup"><span data-stu-id="c1664-119">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="c1664-120">Копировать hello **HVAC.csv** файл образца данных **/HdiSamples/HdiSamples/SensorSampleData/кондиционирования/** toohello хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c1664-120">Copy hello **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store account.</span></span> <span data-ttu-id="c1664-121">фрагмент кода Hello должен выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="c1664-121">hello code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="c1664-122">Убедитесь, что hello файла и пути находятся в правильном регистре hello.</span><span class="sxs-lookup"><span data-stu-id="c1664-122">Make sure you hello file and path names are in hello proper case.</span></span>
   >
   >
3. <span data-ttu-id="c1664-123">Появится запрос tooenter hello учетные данные для hello подписки Azure, в котором у вас есть учетная запись хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="c1664-123">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="c1664-124">Вы увидите выходные данные примерно toohello следующие:</span><span class="sxs-lookup"><span data-stu-id="c1664-124">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="c1664-125">файл данных Hello (**HVAC.csv**) будут скопированы в папке **/hvac** в hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="c1664-125">hello data file (**HVAC.csv**) will be copied under a folder **/hvac** in hello Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="c1664-126">Использование кластера HDInsight Spark с Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c1664-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="c1664-127">Из hello [портала Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели).</span><span class="sxs-lookup"><span data-stu-id="c1664-127">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="c1664-128">Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c1664-128">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="c1664-129">Из колонки кластера Spark hello, нажмите кнопку **быстрые ссылки**, а затем из hello **мониторинга кластера** колонке нажмите кнопку **книжке Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="c1664-129">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="c1664-130">При появлении запроса введите учетные данные администратора hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="c1664-130">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c1664-131">Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="c1664-131">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="c1664-132">Замените **CLUSTERNAME** с hello имя кластера:</span><span class="sxs-lookup"><span data-stu-id="c1664-132">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="c1664-133">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="c1664-133">Create a new notebook.</span></span> <span data-ttu-id="c1664-134">Щелкните **Создать**, а затем выберите **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="c1664-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="c1664-135">![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Создание записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c1664-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="c1664-136">Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом.</span><span class="sxs-lookup"><span data-stu-id="c1664-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="c1664-137">контексты Spark и Hive Hello автоматически создается автоматически при выполнении первой ячейке кода hello.</span><span class="sxs-lookup"><span data-stu-id="c1664-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="c1664-138">Можно запустить, импортировав hello типы, необходимые для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="c1664-138">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="c1664-139">toodo таким образом, вставьте следующий фрагмент кода в ячейку и нажать клавишу hello **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="c1664-139">toodo so, paste hello following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="c1664-140">Отображается каждый раз при запуске задания в Jupyter, заголовок окна обозревателя вашей веб **(Busy)** состояния вместе с hello записной книжки заголовка.</span><span class="sxs-lookup"><span data-stu-id="c1664-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="c1664-141">Вы также увидите Далее toohello сплошной кружок **PySpark** текст в верхнем правом углу hello.</span><span class="sxs-lookup"><span data-stu-id="c1664-141">You will also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="c1664-142">После завершения задания hello, это приведет к изменению tooa полый круг.</span><span class="sxs-lookup"><span data-stu-id="c1664-142">After hello job is completed, this will change tooa hollow circle.</span></span>

     <span data-ttu-id="c1664-143">![Состояние задания записной книжки Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Состояние задания записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c1664-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="c1664-144">Загрузить образец данных во временную таблицу с помощью hello **HVAC.csv** файл, скопированный учетной записи хранилища Озера данных toohello.</span><span class="sxs-lookup"><span data-stu-id="c1664-144">Load sample data into a temporary table using hello **HVAC.csv** file you copied toohello Data Lake Store account.</span></span> <span data-ttu-id="c1664-145">Можно получить доступ к hello данные в учетной записи хранилища Озера данных hello, используя следующий шаблон URL-адреса hello.</span><span class="sxs-lookup"><span data-stu-id="c1664-145">You can access hello data in hello Data Lake Store account using hello following URL pattern.</span></span>

    * <span data-ttu-id="c1664-146">Если у вас есть хранилища Озера данных в качестве хранилища по умолчанию, HVAC.csv будет на аналогичные toohello hello путь URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="c1664-146">If you have Data Lake Store as default storage, HVAC.csv will be at hello path similar toohello following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="c1664-147">Или можно также использовать сокращенный формат, например hello следующее:</span><span class="sxs-lookup"><span data-stu-id="c1664-147">Or, you could also use a shortened format such as hello following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="c1664-148">Если у вас есть хранилища Озера данных в виде дополнительное хранилище, HVAC.csv будет в расположении hello, куда был скопирован, такие как:</span><span class="sxs-lookup"><span data-stu-id="c1664-148">If you have Data Lake Store as additional storage, HVAC.csv will be at hello location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="c1664-149">В пустой ячейке, hello вставьте следующий пример кода замените **MYDATALAKESTORE** с помощью имени учетной записи хранилища Озера данных и нажмите клавишу **SHIFT + ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="c1664-149">In an empty cell, paste hello following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="c1664-150">В этом примере кода регистрируется hello данные во временную таблицу с именем **кондиционирования**.</span><span class="sxs-lookup"><span data-stu-id="c1664-150">This code example registers hello data into a temporary table called **hvac**.</span></span>

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="c1664-151">Так как вы используете ядра PySpark, теперь можно напрямую запустить SQL-запрос для временной таблицы hello **кондиционирования** вы только что создали с помощью hello `%%sql` магическое значение.</span><span class="sxs-lookup"><span data-stu-id="c1664-151">Because you are using a PySpark kernel, you can now directly run a SQL query on hello temporary table **hvac** that you just created by using hello `%%sql` magic.</span></span> <span data-ttu-id="c1664-152">Дополнительные сведения о hello `%%sql` magic, а также другие доступные ядра PySpark hello, magics разделе [ядер, доступных на записные книжки Jupyter с кластерами Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="c1664-152">For more information about hello `%%sql` magic, as well as other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="c1664-153">После успешного завершения задания hello hello, следуя табличного вывода отображается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c1664-153">Once hello job is completed successfully, hello following tabular output is displayed by default.</span></span>

      <span data-ttu-id="c1664-154">![Вывод результатов запроса в виде таблицы](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Вывод результатов запроса в виде таблицы")</span><span class="sxs-lookup"><span data-stu-id="c1664-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="c1664-155">Можно также посмотреть результаты hello в другие представления, а также.</span><span class="sxs-lookup"><span data-stu-id="c1664-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="c1664-156">Например график для приветствия такие же выходные данные выглядят hello следующее.</span><span class="sxs-lookup"><span data-stu-id="c1664-156">For example, an area graph for hello same output would look like hello following.</span></span>

     <span data-ttu-id="c1664-157">![Диаграмма с областями, показывающая результат запроса](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Диаграмма с областями, показывающая результат запроса")</span><span class="sxs-lookup"><span data-stu-id="c1664-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="c1664-158">После завершения работы приложения hello, необходимо hello toorelease ресурсы для завершения работы hello ноутбуков.</span><span class="sxs-lookup"><span data-stu-id="c1664-158">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="c1664-159">toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**.</span><span class="sxs-lookup"><span data-stu-id="c1664-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="c1664-160">В этом будет завершена и закрыть hello ноутбука.</span><span class="sxs-lookup"><span data-stu-id="c1664-160">This will shutdown and close hello notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c1664-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1664-161">Next steps</span></span>

* [<span data-ttu-id="c1664-162">Создание автономного Scala приложения toorun кластере Apache Spark</span><span class="sxs-lookup"><span data-stu-id="c1664-162">Create a standalone Scala application toorun on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c1664-163">Используйте средства HDInsight в набор средств Azure для приложений Spark toocreate IntelliJ для кластера HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="c1664-163">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c1664-164">Используйте средства HDInsight в набор средств Azure для Eclipse toocreate Spark приложений для кластера HDInsight Spark Linux</span><span class="sxs-lookup"><span data-stu-id="c1664-164">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
