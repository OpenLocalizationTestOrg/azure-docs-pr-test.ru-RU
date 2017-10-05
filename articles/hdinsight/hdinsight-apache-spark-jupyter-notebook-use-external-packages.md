---
title: "Использование пользовательских пакетов Maven с записной книжкой Jupyter в кластерах Spark в Azure HDInsight | Документация Майкрософт"
description: "Пошаговые инструкции по настройке записных книжек Jupyter, доступных с кластерами HDInsight Spark для использования пользовательских пакетов Maven."
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
ms.openlocfilehash: 0bcfe220e60e34937c667c7b416065d5f3dc8d63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="96de2-103">Использование внешних пакетов с записными книжками Jupyter в кластерах Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="96de2-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96de2-104">Использование волшебных команд</span><span class="sxs-lookup"><span data-stu-id="96de2-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="96de2-105">Использование действия сценария</span><span class="sxs-lookup"><span data-stu-id="96de2-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="96de2-106">Узнайте, как настроить записную книжку Jupyter в кластере Apache Spark в HDInsight для использования внешних, предоставленных сообществом пакетов **Maven**, которые не включены в готовую версию кластера.</span><span class="sxs-lookup"><span data-stu-id="96de2-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span></span> 

<span data-ttu-id="96de2-107">Полный список доступных пакетов можно найти в [репозитории Maven](http://search.maven.org/) .</span><span class="sxs-lookup"><span data-stu-id="96de2-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="96de2-108">Его также можно получить из других источников.</span><span class="sxs-lookup"><span data-stu-id="96de2-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="96de2-109">Например, полный список предоставленных сообществом пакетов можно найти в разделе [Пакеты Spark](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="96de2-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="96de2-110">В этой статье вы узнаете, как использовать пакет [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) с записной книжкой Jupyter.</span><span class="sxs-lookup"><span data-stu-id="96de2-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="96de2-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="96de2-111">Prerequisites</span></span>
<span data-ttu-id="96de2-112">Необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="96de2-112">You must have the following:</span></span>

* <span data-ttu-id="96de2-113">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="96de2-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="96de2-114">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="96de2-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="96de2-115">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="96de2-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="96de2-116">На начальной панели [портала Azure](https://portal.azure.com/)щелкните элемент кластера Spark (если он закреплен на начальной панели).</span><span class="sxs-lookup"><span data-stu-id="96de2-116">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="96de2-117">Кроме того, вы можете перейти к кластеру, последовательно щелкнув **Просмотреть все** > **Кластеры HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="96de2-117">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="96de2-118">В колонке кластера Spark щелкните **Быстрые ссылки**, затем в колонке **Панель мониторинга кластера** выберите **Записная книжка Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="96de2-118">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="96de2-119">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="96de2-119">If prompted, enter the admin credentials for the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="96de2-120">Также можно открыть Jupyter Notebook для своего кластера, открыв следующий URL-адрес в браузере.</span><span class="sxs-lookup"><span data-stu-id="96de2-120">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="96de2-121">Замените **CLUSTERNAME** именем кластера:</span><span class="sxs-lookup"><span data-stu-id="96de2-121">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="96de2-122">Создайте новую записную книжку.</span><span class="sxs-lookup"><span data-stu-id="96de2-122">Create a new notebook.</span></span> <span data-ttu-id="96de2-123">Щелкните **Создать**, а затем выберите **Spark**.</span><span class="sxs-lookup"><span data-stu-id="96de2-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="96de2-124">![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Создание записной книжки Jupyter")</span><span class="sxs-lookup"><span data-stu-id="96de2-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="96de2-125">Будет создана и открыта записная книжка с именем Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="96de2-125">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="96de2-126">Щелкните имя записной книжки в верхней части страницы сверху и введите понятное имя.</span><span class="sxs-lookup"><span data-stu-id="96de2-126">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="96de2-127">![Указание имени для записной книжки](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Указание имени для записной книжки")</span><span class="sxs-lookup"><span data-stu-id="96de2-127">![Provide a name for the notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="96de2-128">Используйте волшебную команду `%%configure` , чтобы настроить записную книжку для использования внешнего пакета.</span><span class="sxs-lookup"><span data-stu-id="96de2-128">You will use the `%%configure` magic to configure the notebook to use an external package.</span></span> <span data-ttu-id="96de2-129">В записных книжках, которые используют внешние пакеты, следует вызывать волшебную команду `%%configure` в первой ячейке кода.</span><span class="sxs-lookup"><span data-stu-id="96de2-129">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span></span> <span data-ttu-id="96de2-130">Она настраивает ядро для использования пакета до начала сеанса.</span><span class="sxs-lookup"><span data-stu-id="96de2-130">This ensures that the kernel is configured to use the package before the session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="96de2-131">Если вы забыли настроить ядро в первой ячейке, можно использовать `%%configure` с параметром `-f`, но при этом сеанс будет перезапущен и все изменения будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="96de2-131">If you forget to configure the kernel in the first cell, you can use the `%%configure` with the `-f` parameter, but that will restart the session and all progress will be lost.</span></span>

    | <span data-ttu-id="96de2-132">Версия HDInsight</span><span class="sxs-lookup"><span data-stu-id="96de2-132">HDInsight version</span></span> | <span data-ttu-id="96de2-133">Команда</span><span class="sxs-lookup"><span data-stu-id="96de2-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="96de2-134">Для HDInsight 3.3 и HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="96de2-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="96de2-135">Для HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="96de2-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="96de2-136">Приведенный выше фрагмент ожидает получить координаты Maven для внешнего пакета в центральном репозитории Maven.</span><span class="sxs-lookup"><span data-stu-id="96de2-136">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span></span> <span data-ttu-id="96de2-137">В этом фрагменте кода `com.databricks:spark-csv_2.10:1.4.0` — координата пакета **spark-csv** в Maven.</span><span class="sxs-lookup"><span data-stu-id="96de2-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="96de2-138">Вот как сформировать координаты для пакета.</span><span class="sxs-lookup"><span data-stu-id="96de2-138">Here's how you construct the coordinates for a package.</span></span>
   
    <span data-ttu-id="96de2-139">а.</span><span class="sxs-lookup"><span data-stu-id="96de2-139">a.</span></span> <span data-ttu-id="96de2-140">Найдите пакет в репозитории Maven.</span><span class="sxs-lookup"><span data-stu-id="96de2-140">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="96de2-141">В этом руководстве мы используем [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="96de2-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="96de2-142">b.</span><span class="sxs-lookup"><span data-stu-id="96de2-142">b.</span></span> <span data-ttu-id="96de2-143">В репозитории найдите значения для параметров **GroupId**, **ArtifactId** и **Version**.</span><span class="sxs-lookup"><span data-stu-id="96de2-143">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="96de2-144">Убедитесь, что полученные значения соответствуют кластеру.</span><span class="sxs-lookup"><span data-stu-id="96de2-144">Make sure that the values you gather match your cluster.</span></span> <span data-ttu-id="96de2-145">В этом случае мы используем Scala 2.10 и пакет Spark 1.4.0, но может потребоваться выбрать другие версии, соответствующие версиям Scala или Spark в вашем кластере.</span><span class="sxs-lookup"><span data-stu-id="96de2-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="96de2-146">Выяснить версию Scala в кластере можно, выполнив `scala.util.Properties.versionString` для ядра Jupyter Spark или при отправке Spark.</span><span class="sxs-lookup"><span data-stu-id="96de2-146">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="96de2-147">Выяснить версию Spark в кластере можно, выполнив `sc.version` для элементов Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="96de2-147">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="96de2-148">![Использование внешних пакетов с записными книжками Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Использование внешних пакетов с записными книжками Jupyter")</span><span class="sxs-lookup"><span data-stu-id="96de2-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="96de2-149">c.</span><span class="sxs-lookup"><span data-stu-id="96de2-149">c.</span></span> <span data-ttu-id="96de2-150">Объедините три значения, разделив их двоеточием (**:**).</span><span class="sxs-lookup"><span data-stu-id="96de2-150">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="96de2-151">Запустите ячейку кода с помощью волшебной команды `%%configure` .</span><span class="sxs-lookup"><span data-stu-id="96de2-151">Run the code cell with the `%%configure` magic.</span></span> <span data-ttu-id="96de2-152">После выполнения этой команды соответствующий сеанс Livy будет использовать указанный вами пакет.</span><span class="sxs-lookup"><span data-stu-id="96de2-152">This will configure the underlying Livy session to use the package you provided.</span></span> <span data-ttu-id="96de2-153">В последующих ячейках записной книжки теперь можно использовать этот пакет, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="96de2-153">In the subsequent cells in the notebook, you can now use the package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="96de2-154">Затем можно запустить фрагменты кода, как показано ниже, чтобы просмотреть данные из таблицы данных, созданной на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="96de2-154">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="96de2-155"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="96de2-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="96de2-156">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="96de2-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="96de2-157">Сценарии</span><span class="sxs-lookup"><span data-stu-id="96de2-157">Scenarios</span></span>
* [<span data-ttu-id="96de2-158">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="96de2-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="96de2-159">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="96de2-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="96de2-160">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="96de2-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="96de2-161">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="96de2-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="96de2-162">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="96de2-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="96de2-163">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="96de2-163">Create and run applications</span></span>
* [<span data-ttu-id="96de2-164">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="96de2-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="96de2-165">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="96de2-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="96de2-166">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="96de2-166">Tools and extensions</span></span>

* [<span data-ttu-id="96de2-167">Использование внешних пакетов Python с элементами Jupyter Notebook в кластерах Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="96de2-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="96de2-168">Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="96de2-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="96de2-169">Удаленная отладка приложений Spark в кластере HDInsight Spark Linux с помощью подключаемого модуля средств HDInsight для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="96de2-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="96de2-170">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="96de2-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="96de2-171">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="96de2-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="96de2-172">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="96de2-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="96de2-173">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="96de2-173">Manage resources</span></span>
* [<span data-ttu-id="96de2-174">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="96de2-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="96de2-175">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="96de2-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

