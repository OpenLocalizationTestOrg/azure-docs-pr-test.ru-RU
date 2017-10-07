---
title: "пользовательские пакеты Maven aaaUse с Jupyter в Spark на Azure HDInsight | Документы Microsoft"
description: "Пошаговые инструкции по как доступные с HDInsight Spark записные книжки Jupyter tooconfigure кластеры toouse пользовательские пакеты Maven."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="33f94-103">Использование внешних пакетов с записными книжками Jupyter в кластерах Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="33f94-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33f94-104">Использование волшебных команд</span><span class="sxs-lookup"><span data-stu-id="33f94-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="33f94-105">Использование действия сценария</span><span class="sxs-lookup"><span data-stu-id="33f94-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="33f94-106">Узнайте, как tooconfigure записной книжке Jupyter в кластере Apache Spark на HDInsight toouse внешних, сообществом **maven** пакетов, которые не включены out of box в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="33f94-106">Learn how tooconfigure a Jupyter notebook in Apache Spark cluster on HDInsight toouse external, community-contributed **maven** packages that are not included out-of-the-box in hello cluster.</span></span> 

<span data-ttu-id="33f94-107">Можно выполнить поиск hello [Maven репозитория](http://search.maven.org/) hello полный список доступных пакетов.</span><span class="sxs-lookup"><span data-stu-id="33f94-107">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="33f94-108">Его также можно получить из других источников.</span><span class="sxs-lookup"><span data-stu-id="33f94-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="33f94-109">Например, полный список предоставленных сообществом пакетов можно найти в разделе [Пакеты Spark](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="33f94-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="33f94-110">В этой статье вы узнаете, как toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) пакет записной книжки Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="33f94-110">In this article, you will learn how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="33f94-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="33f94-111">Prerequisites</span></span>
<span data-ttu-id="33f94-112">Необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="33f94-112">You must have hello following:</span></span>

* <span data-ttu-id="33f94-113">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="33f94-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="33f94-114">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="33f94-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="33f94-115">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="33f94-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="33f94-116">Из hello [портала Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели).</span><span class="sxs-lookup"><span data-stu-id="33f94-116">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="33f94-117">Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="33f94-117">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="33f94-118">Из колонки кластера Spark hello, нажмите кнопку **быстрые ссылки**, а затем из hello **мониторинга кластера** колонке нажмите кнопку **книжке Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="33f94-118">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="33f94-119">При появлении запроса введите учетные данные администратора hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="33f94-119">If prompted, enter hello admin credentials for hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="33f94-120">Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="33f94-120">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="33f94-121">Замените **CLUSTERNAME** с hello имя кластера:</span><span class="sxs-lookup"><span data-stu-id="33f94-121">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="33f94-122">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="33f94-122">Create a new notebook.</span></span> <span data-ttu-id="33f94-123">Щелкните **Создать**, а затем выберите **Spark**.</span><span class="sxs-lookup"><span data-stu-id="33f94-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="33f94-124">![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Создание записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="33f94-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="33f94-125">Создается и открывается с именем hello Untitled.pynb новый блокнот.</span><span class="sxs-lookup"><span data-stu-id="33f94-125">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="33f94-126">Щелкните имя записной книжки hello вверху hello и введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="33f94-126">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="33f94-127">![Введите имя для ноутбука hello](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "укажите имя для ноутбука hello")</span><span class="sxs-lookup"><span data-stu-id="33f94-127">![Provide a name for hello notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="33f94-128">Вы воспользуетесь hello `%%configure` magic tooconfigure hello записной книжки toouse внешнего пакета.</span><span class="sxs-lookup"><span data-stu-id="33f94-128">You will use hello `%%configure` magic tooconfigure hello notebook toouse an external package.</span></span> <span data-ttu-id="33f94-129">Портативные компьютеры, использующие внешние пакеты, убедитесь в вызове hello `%%configure` magic в первую ячейку кода hello.</span><span class="sxs-lookup"><span data-stu-id="33f94-129">In notebooks that use external packages, make sure you call hello `%%configure` magic in hello first code cell.</span></span> <span data-ttu-id="33f94-130">Это гарантирует, что hello ядра — настроенное toouse hello пакета до начала сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="33f94-130">This ensures that hello kernel is configured toouse hello package before hello session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="33f94-131">Если вы забыли ядра tooconfigure hello в первую ячейку hello, можно использовать hello `%%configure` с hello `-f` параметра, но будет перезапустить сеанс hello и ход выполнения всех будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="33f94-131">If you forget tooconfigure hello kernel in hello first cell, you can use hello `%%configure` with hello `-f` parameter, but that will restart hello session and all progress will be lost.</span></span>

    | <span data-ttu-id="33f94-132">Версия HDInsight</span><span class="sxs-lookup"><span data-stu-id="33f94-132">HDInsight version</span></span> | <span data-ttu-id="33f94-133">Команда</span><span class="sxs-lookup"><span data-stu-id="33f94-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="33f94-134">Для HDInsight 3.3 и HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="33f94-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="33f94-135">Для HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="33f94-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="33f94-136">фрагмент кода Hello выше ожидает координаты maven hello для hello внешнего пакета в центральном репозитории Maven.</span><span class="sxs-lookup"><span data-stu-id="33f94-136">hello snippet above expects hello maven coordinates for hello external package in Maven Central Repository.</span></span> <span data-ttu-id="33f94-137">В этом фрагменте кода `com.databricks:spark-csv_2.10:1.4.0` имеет координаты maven hello **spark csv** пакета.</span><span class="sxs-lookup"><span data-stu-id="33f94-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is hello maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="33f94-138">Ниже показано, как построить hello координаты для пакета.</span><span class="sxs-lookup"><span data-stu-id="33f94-138">Here's how you construct hello coordinates for a package.</span></span>
   
    <span data-ttu-id="33f94-139">а.</span><span class="sxs-lookup"><span data-stu-id="33f94-139">a.</span></span> <span data-ttu-id="33f94-140">Найдите пакет hello в hello Maven репозитория.</span><span class="sxs-lookup"><span data-stu-id="33f94-140">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="33f94-141">В этом руководстве мы используем [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="33f94-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="33f94-142">b.</span><span class="sxs-lookup"><span data-stu-id="33f94-142">b.</span></span> <span data-ttu-id="33f94-143">Из репозитория hello сбора значений hello **GroupId**, **ArtifactId**, и **версии**.</span><span class="sxs-lookup"><span data-stu-id="33f94-143">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="33f94-144">Убедитесь, что hello значения, собранные соответствуют кластера.</span><span class="sxs-lookup"><span data-stu-id="33f94-144">Make sure that hello values you gather match your cluster.</span></span> <span data-ttu-id="33f94-145">В этом случае мы используем Scala 2.10 и Spark 1.4.0 пакета, но могут потребоваться различные версии tooselect для версии Scala или Spark соответствующие hello в кластере.</span><span class="sxs-lookup"><span data-stu-id="33f94-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need tooselect different versions for hello appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="33f94-146">Можно узнать версию Scala hello в кластере, запустив `scala.util.Properties.versionString` ядра Spark Jupyter hello или отправить Spark.</span><span class="sxs-lookup"><span data-stu-id="33f94-146">You can find out hello Scala version on your cluster by running `scala.util.Properties.versionString` on hello Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="33f94-147">Можно узнать версию Spark hello в кластере, запустив `sc.version` на записные книжки Jupyter.</span><span class="sxs-lookup"><span data-stu-id="33f94-147">You can find out hello Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="33f94-148">![Использование внешних пакетов с записными книжками Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Использование внешних пакетов с записными книжками Jupyter")</span><span class="sxs-lookup"><span data-stu-id="33f94-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="33f94-149">c.</span><span class="sxs-lookup"><span data-stu-id="33f94-149">c.</span></span> <span data-ttu-id="33f94-150">Объединение hello трех значений, разделенных точкой с запятой (**:**).</span><span class="sxs-lookup"><span data-stu-id="33f94-150">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="33f94-151">Запустите hello кода ячейки с hello `%%configure` магическое значение.</span><span class="sxs-lookup"><span data-stu-id="33f94-151">Run hello code cell with hello `%%configure` magic.</span></span> <span data-ttu-id="33f94-152">Эта операция настроит hello базового Livy сеанса toouse hello пакета, который вы указали.</span><span class="sxs-lookup"><span data-stu-id="33f94-152">This will configure hello underlying Livy session toouse hello package you provided.</span></span> <span data-ttu-id="33f94-153">В последующих ячейках hello в записной книжке hello теперь можно использовать пакет hello, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="33f94-153">In hello subsequent cells in hello notebook, you can now use hello package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="33f94-154">После этого можно выполнить фрагменты кода hello, как показано ниже, tooview hello данные из hello кадр данных был создан в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="33f94-154">You can then run hello snippets, like shown below, tooview hello data from hello dataframe you created in hello previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="33f94-155"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="33f94-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="33f94-156">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="33f94-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="33f94-157">Сценарии</span><span class="sxs-lookup"><span data-stu-id="33f94-157">Scenarios</span></span>
* [<span data-ttu-id="33f94-158">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="33f94-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="33f94-159">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="33f94-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="33f94-160">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="33f94-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="33f94-161">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="33f94-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="33f94-162">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="33f94-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="33f94-163">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="33f94-163">Create and run applications</span></span>
* [<span data-ttu-id="33f94-164">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="33f94-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="33f94-165">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="33f94-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="33f94-166">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="33f94-166">Tools and extensions</span></span>

* [<span data-ttu-id="33f94-167">Использование внешних пакетов Python с элементами Jupyter Notebook в кластерах Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="33f94-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="33f94-168">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений</span><span class="sxs-lookup"><span data-stu-id="33f94-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="33f94-169">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="33f94-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="33f94-170">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="33f94-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="33f94-171">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="33f94-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="33f94-172">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="33f94-172">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="33f94-173">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="33f94-173">Manage resources</span></span>
* [<span data-ttu-id="33f94-174">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="33f94-174">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="33f94-175">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="33f94-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

