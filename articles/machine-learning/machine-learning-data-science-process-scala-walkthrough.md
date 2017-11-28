---
title: "aaaData обработки и анализа с помощью Scala и Spark на Azure | Документы Microsoft"
description: "Как toouse Scala для защищенных машинного обучения задач с помощью hello Spark масштабируемой MLlib Spark ML пакеты и на кластере Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="04e13-103">Обработка и анализ данных с использованием Scala и Spark в Azure</span><span class="sxs-lookup"><span data-stu-id="04e13-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="04e13-104">В этой статье показано, как пакеты toouse Scala для задач защищенных машинного обучения с hello масштабируемой MLlib Spark и Spark ML на кластере Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="04e13-104">This article shows you how toouse Scala for supervised machine learning tasks with hello Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="04e13-105">Он поможет выполнить задачи hello, составляющих hello [процесса обработки и анализа данных](http://aka.ms/datascienceprocess): приема данных и просмотра, визуализации, конструируются, моделирования и модели использования.</span><span class="sxs-lookup"><span data-stu-id="04e13-105">It walks you through hello tasks that constitute hello [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="04e13-106">модели Hello в статье hello включают логистической и линейной регрессии, случайные леса и градиент повышенных деревьев (GBTs), кроме общих tootwo защищено задач машинного обучения:</span><span class="sxs-lookup"><span data-stu-id="04e13-106">hello models in hello article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition tootwo common supervised machine learning tasks:</span></span>

* <span data-ttu-id="04e13-107">Проблемы регрессии: прогноз суммы совет hello ($) для обработки такси</span><span class="sxs-lookup"><span data-stu-id="04e13-107">Regression problem: Prediction of hello tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="04e13-108">двоичная классификация: прогнозирование вероятности оплаты чаевых (1 или 0) за поездку в такси.</span><span class="sxs-lookup"><span data-stu-id="04e13-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="04e13-109">процесс моделирования Hello требует обучения и оценки проверочного набора данных и показатели точности применимо.</span><span class="sxs-lookup"><span data-stu-id="04e13-109">hello modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="04e13-110">В этой статье рассказывается, как toostore этих моделей в хранилище больших двоичных объектов Azure и как tooscore и оценить их прогнозирования производительности.</span><span class="sxs-lookup"><span data-stu-id="04e13-110">In this article, you can learn how toostore these models in Azure Blob storage and how tooscore and evaluate their predictive performance.</span></span> <span data-ttu-id="04e13-111">В этой статье также описывается hello дополнительные разделы, как toooptimize модели с помощью свертки перекрестной проверки и hyper параметра.</span><span class="sxs-lookup"><span data-stu-id="04e13-111">This article also covers hello more advanced topics of how toooptimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="04e13-112">Hello данные, используемые приводится образец hello 2013 NYC такси маршрута и тариф авиакомпании набора данных на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="04e13-112">hello data used is a sample of hello 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="04e13-113">[Scala](http://www.scala-lang.org/), язык, основанный на виртуальной машине Java hello интегрирует концепции объектно ориентированного и функциональный язык.</span><span class="sxs-lookup"><span data-stu-id="04e13-113">[Scala](http://www.scala-lang.org/), a language based on hello Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="04e13-114">Это масштабируемая язык, хорошо подходит toodistributed обработки в облаке hello и выполняется в кластерах Azure Spark.</span><span class="sxs-lookup"><span data-stu-id="04e13-114">It's a scalable language that is well suited toodistributed processing in hello cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="04e13-115">[Spark](http://spark.apache.org/) платформу параллельной обработки открытым исходным кодом, поддерживающий в памяти обрабатывает tooboost hello производительность больших данных аналитики приложений.</span><span class="sxs-lookup"><span data-stu-id="04e13-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing tooboost hello performance of big data analytics applications.</span></span> <span data-ttu-id="04e13-116">Подсистема обработки Spark Hello, созданную для скорости, простоте использования и сложные analytics.</span><span class="sxs-lookup"><span data-stu-id="04e13-116">hello Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="04e13-117">Возможности распределенного вычисления в памяти Spark отлично подходят для итеративных алгоритмов в машинном обучении и графовых вычислениях.</span><span class="sxs-lookup"><span data-stu-id="04e13-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="04e13-118">Hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) пакет предоставляет единый набор API высокого уровня, построена на базе данных кадры, которые помогут вам создать и настроить практические машинного обучения конвейеров.</span><span class="sxs-lookup"><span data-stu-id="04e13-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="04e13-119">[MLlib](http://spark.apache.org/mllib/) — библиотека Spark в масштабируемой машинного обучения, который переводит возможностей моделирования toothis распределенной среде.</span><span class="sxs-lookup"><span data-stu-id="04e13-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities toothis distributed environment.</span></span>

<span data-ttu-id="04e13-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) — предложение размещенной в Azure hello Spark с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="04e13-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="04e13-121">Она также включает поддержку записные книжки Jupyter Scala на кластере Spark hello и может выполнения интерактивных запросов tootransform Spark SQL, фильтрации и отображения данных, хранящихся в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="04e13-121">It also includes support for Jupyter Scala notebooks on hello Spark cluster, and can run Spark SQL interactive queries tootransform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="04e13-122">Hello Scala фрагменты кода в этой статье, предоставляющие решения hello и отображения графики соответствующие hello toovisualize hello данных выполняются в записные книжки Jupyter установлен в кластерах Spark hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-122">hello Scala code snippets in this article that provide hello solutions and show hello relevant plots toovisualize hello data run in Jupyter notebooks installed on hello Spark clusters.</span></span> <span data-ttu-id="04e13-123">шаги моделирования Hello в этих разделах имеется код, показано, как tootrain, вычисления, сохранения и использовать каждый вводе модели.</span><span class="sxs-lookup"><span data-stu-id="04e13-123">hello modeling steps in these topics have code that shows you how tootrain, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="04e13-124">шаги настройки Hello и кода в этой статье предназначены для Azure HDInsight 3.4 Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="04e13-124">hello setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="04e13-125">Однако hello кода в этой статье и в hello [книжке Jupyter Scala](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) , являются универсальными и должен работать на любой кластер Spark.</span><span class="sxs-lookup"><span data-stu-id="04e13-125">However, hello code in this article and in hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="04e13-126">Здравствуйте, настройка кластера и управления действия может быть немного отличается от элементы, отображаемые в этой статье, если вы не используете HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="04e13-126">hello cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="04e13-127">Разделе показано, как Python, а не Scala toocomplete toouse задач для начала до конца процесса обработки и анализа данных. в разделе [обработки и анализа данных с помощью Spark на Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04e13-127">For a topic that shows you how toouse Python rather than Scala toocomplete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="04e13-128">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="04e13-128">Prerequisites</span></span>
* <span data-ttu-id="04e13-129">У вас должна быть подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="04e13-129">You must have an Azure subscription.</span></span> <span data-ttu-id="04e13-130">Если у вас ее нет, [получите бесплатную пробную версию Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="04e13-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="04e13-131">Вы должны hello toocomplete кластера Azure HDInsight 3.4 Spark 1.6 следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="04e13-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster toocomplete hello following procedures.</span></span> <span data-ttu-id="04e13-132">toocreate кластера, см. инструкции hello в [приступить к работе: создание Apache Spark на Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="04e13-132">toocreate a cluster, see hello instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="04e13-133">Задайте тип кластера hello и версии в hello **Выбор типа кластера** меню.</span><span class="sxs-lookup"><span data-stu-id="04e13-133">Set hello cluster type and version on hello **Select Cluster Type** menu.</span></span>

![Настройка типа кластера HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="04e13-135">Описание hello NYC такси обработки данных и инструкции о том, как код tooexecute из записной книжке Jupyter на кластере Spark hello, см. соответствующие разделы hello в [Обзор для обработки и анализа данных с помощью Spark на Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04e13-135">For a description of hello NYC taxi trip data and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster, see hello relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a><span data-ttu-id="04e13-136">Выполнение кода Scala записной книжке Jupyter на кластере Spark hello</span><span class="sxs-lookup"><span data-stu-id="04e13-136">Execute Scala code from a Jupyter notebook on hello Spark cluster</span></span>
<span data-ttu-id="04e13-137">Вы можете запустить записной книжке Jupyter из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="04e13-137">You can launch a Jupyter notebook from hello Azure portal.</span></span> <span data-ttu-id="04e13-138">Найдите кластер Spark приветствия на информационной панели, затем щелкните страницу управления hello tooenter для кластера.</span><span class="sxs-lookup"><span data-stu-id="04e13-138">Find hello Spark cluster on your dashboard, and then click it tooenter hello management page for your cluster.</span></span> <span data-ttu-id="04e13-139">Далее щелкните **панели мониторинга кластера**и нажмите кнопку **книжке Jupyter** tooopen hello ноутбук, связанные с кластера Spark hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** tooopen hello notebook associated with hello Spark cluster.</span></span>

![Панель мониторинга кластера и записные книжки Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="04e13-141">Записные книжки Jupyter также можно просмотреть по адресу https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="04e13-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="04e13-142">Замените *clustername* с hello имя кластера.</span><span class="sxs-lookup"><span data-stu-id="04e13-142">Replace *clustername* with hello name of your cluster.</span></span> <span data-ttu-id="04e13-143">Вам необходим пароль hello вашего администратора учетной записи tooaccess hello Jupyter портативных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="04e13-143">You need hello password for your administrator account tooaccess hello Jupyter notebooks.</span></span>

![Go tooJupyter портативные компьютеры с помощью имени кластера hello](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="04e13-145">Выберите **Scala** toosee каталога, который содержит несколько примеров предварительно пакетированных записных книжек, используйте hello PySpark API.</span><span class="sxs-lookup"><span data-stu-id="04e13-145">Select **Scala** toosee a directory that has a few examples of prepackaged notebooks that use hello PySpark API.</span></span> <span data-ttu-id="04e13-146">Здравствуйте моделирования исследования и счет с помощью Scala.ipynb ноутбук, содержащий hello образцы кода для этого набора разделов Spark доступен на [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="04e13-146">hello Exploration Modeling and Scoring using Scala.ipynb notebook that contains hello code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="04e13-147">Можно передать записной книжки hello непосредственно из GitHub toohello книжке Jupyter сервера на кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="04e13-147">You can upload hello notebook directly from GitHub toohello Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="04e13-148">На домашней странице Jupyter, нажмите кнопку hello **отправить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="04e13-148">On your Jupyter home page, click hello **Upload** button.</span></span> <span data-ttu-id="04e13-149">В проводнике hello, вставьте URL-адрес GitHub (необработанное содержимое) hello портативного компьютера Scala hello и нажмите кнопку **откройте**.</span><span class="sxs-lookup"><span data-stu-id="04e13-149">In hello file explorer, paste hello GitHub (raw content) URL of hello Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="04e13-150">ноутбук Scala Hello доступна на hello URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="04e13-150">hello Scala notebook is available at hello following URL:</span></span>

[<span data-ttu-id="04e13-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="04e13-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="04e13-152">Настройка: предустановленные контексты Spark и Hive, а также магические команды и библиотеки Spark</span><span class="sxs-lookup"><span data-stu-id="04e13-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="04e13-153">Предустановленные контексты Spark и Hive</span><span class="sxs-lookup"><span data-stu-id="04e13-153">Preset Spark and Hive contexts</span></span>
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="04e13-154">Hello Spark ядер, предоставляемых с записные книжки Jupyter имеют предустановленных контекстов.</span><span class="sxs-lookup"><span data-stu-id="04e13-154">hello Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="04e13-155">Не нужно tooexplicitly набор hello Spark или куст контекстов перед началом работы с приложением hello, которое вы разрабатываете.</span><span class="sxs-lookup"><span data-stu-id="04e13-155">You don't need tooexplicitly set hello Spark or Hive contexts before you start working with hello application you are developing.</span></span> <span data-ttu-id="04e13-156">Hello предустановленную контексты — это:</span><span class="sxs-lookup"><span data-stu-id="04e13-156">hello preset contexts are:</span></span>

* <span data-ttu-id="04e13-157">`sc` — для контекста Spark;</span><span class="sxs-lookup"><span data-stu-id="04e13-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="04e13-158">`sqlContext` — для контекста Hive.</span><span class="sxs-lookup"><span data-stu-id="04e13-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="04e13-159">Волшебные команды Spark</span><span class="sxs-lookup"><span data-stu-id="04e13-159">Spark magics</span></span>
<span data-ttu-id="04e13-160">Hello ядра Spark предоставляет некоторые предопределенные «magics», которые являются специальные команды, которые можно вызвать с `%%`.</span><span class="sxs-lookup"><span data-stu-id="04e13-160">hello Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="04e13-161">Два из этих команд используются следующие примеры кода hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-161">Two of these commands are used in hello following code samples.</span></span>

* <span data-ttu-id="04e13-162">`%%local`Указывает, что кода hello в последующих строках выполняется локально.</span><span class="sxs-lookup"><span data-stu-id="04e13-162">`%%local` specifies that hello code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="04e13-163">Hello код должен быть допустимым кодом Scala.</span><span class="sxs-lookup"><span data-stu-id="04e13-163">hello code must be valid Scala code.</span></span>
* <span data-ttu-id="04e13-164">`%%sql -o <variable name>` выполняет запрос Hive к `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="04e13-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="04e13-165">Если hello `-o` передается параметр, результат hello hello запроса сохраняется в hello `%%local` Scala контекста в виде блока данных Spark.</span><span class="sxs-lookup"><span data-stu-id="04e13-165">If hello `-o` parameter is passed, hello result of hello query is persisted in hello `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="04e13-166">Для Дополнительные сведения о ядрах hello записные книжки Jupyter и их стандартных «magics», можно вызвать с `%%` (например, `%%local`), в разделе [кластеров ядер, доступных для записные книжки Jupyter с HDInsight Spark Linux HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="04e13-166">For more information about hello kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="04e13-167">Импорт библиотек</span><span class="sxs-lookup"><span data-stu-id="04e13-167">Import libraries</span></span>
<span data-ttu-id="04e13-168">Импорт hello Spark, MLlib и другие библиотеки вам с помощью hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="04e13-168">Import hello Spark, MLlib, and other libraries you'll need by using hello following code.</span></span>

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a><span data-ttu-id="04e13-169">Прием данных</span><span class="sxs-lookup"><span data-stu-id="04e13-169">Data ingestion</span></span>
<span data-ttu-id="04e13-170">Первым этапом Hello hello процесса обработки и анализа данных является tooingest hello данных, что tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="04e13-170">hello first step in hello Data Science process is tooingest hello data that you want tooanalyze.</span></span> <span data-ttu-id="04e13-171">Переносе hello данных из внешних источников или системами его местоположение в среде моделирования и просмотра данных.</span><span class="sxs-lookup"><span data-stu-id="04e13-171">You bring hello data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="04e13-172">В этой статье вы приема данных hello, соединенных 0,1% пример hello такси маршрута и тариф авиакомпании (хранятся в формате .tsv).</span><span class="sxs-lookup"><span data-stu-id="04e13-172">In this article, hello data you ingest is a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="04e13-173">среда моделирования и просмотра данных Hello — Spark.</span><span class="sxs-lookup"><span data-stu-id="04e13-173">hello data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="04e13-174">Этот раздел содержит hello toocomplete кода hello, следующая последовательность задач:</span><span class="sxs-lookup"><span data-stu-id="04e13-174">This section contains hello code toocomplete hello following series of tasks:</span></span>

1. <span data-ttu-id="04e13-175">Установка пути к каталогам для хранения данных и моделей.</span><span class="sxs-lookup"><span data-stu-id="04e13-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="04e13-176">Чтение в hello (хранятся в формате .tsv) входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="04e13-176">Read in hello input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="04e13-177">Определение схемы для hello и очистить hello данными.</span><span class="sxs-lookup"><span data-stu-id="04e13-177">Define a schema for hello data and clean hello data.</span></span>
4. <span data-ttu-id="04e13-178">Создание очищенного кадра данных и его кэширование в памяти.</span><span class="sxs-lookup"><span data-stu-id="04e13-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="04e13-179">Зарегистрируйте hello данных как временные таблицы в SQLContext.</span><span class="sxs-lookup"><span data-stu-id="04e13-179">Register hello data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="04e13-180">Запросы к таблице hello и Импорт результатов hello в кадре данных.</span><span class="sxs-lookup"><span data-stu-id="04e13-180">Query hello table and import hello results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="04e13-181">Настройка путей каталога к местам хранения в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="04e13-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="04e13-182">Spark может считывать и записывать tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="04e13-182">Spark can read and write tooAzure Blob storage.</span></span> <span data-ttu-id="04e13-183">Используйте Spark tooprocess любой из существующих данных и сохраните результаты hello снова в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="04e13-183">You can use Spark tooprocess any of your existing data, and then store hello results again in Blob storage.</span></span>

<span data-ttu-id="04e13-184">toosave модели или файлов в хранилище больших двоичных объектов, необходимо tooproperly укажите путь hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-184">toosave models or files in Blob storage, you need tooproperly specify hello path.</span></span> <span data-ttu-id="04e13-185">Контейнер по умолчанию hello ссылку присоединенного кластера Spark toohello, используя путь, который начинается с `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="04e13-185">Reference hello default container attached toohello Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="04e13-186">Другие расположения указываются с помощью `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="04e13-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="04e13-187">Hello следующий код задает hello место чтения toobe входных данных hello и hello путь tooBlob хранилища, кластер Spark вложенного toohello сохранения модели hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-187">hello following code sample specifies hello location of hello input data toobe read and hello path tooBlob storage that is attached toohello Spark cluster where hello model will be saved.</span></span>

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a><span data-ttu-id="04e13-188">Импорт данных, создать RDD определить toohello схемы в соответствии с кадра данных.</span><span class="sxs-lookup"><span data-stu-id="04e13-188">Import data, create an RDD, and define a data frame according toohello schema</span></span>
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="04e13-189">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-189">**Output:**</span></span>

<span data-ttu-id="04e13-190">Время toorun hello ячейки: 8 секунд.</span><span class="sxs-lookup"><span data-stu-id="04e13-190">Time toorun hello cell: 8 seconds.</span></span>

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="04e13-191">Запросы к таблице hello и Импорт результатов в кадре данных.</span><span class="sxs-lookup"><span data-stu-id="04e13-191">Query hello table and import results in a data frame</span></span>
<span data-ttu-id="04e13-192">Далее таблица hello запроса тариф авиакомпании, пассажира и подсказки данных. Фильтрация данных поврежден и малые; и напечатайте несколько строк.</span><span class="sxs-lookup"><span data-stu-id="04e13-192">Next, query hello table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="04e13-193">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-193">**Output:**</span></span>

| <span data-ttu-id="04e13-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="04e13-194">fare_amount</span></span> | <span data-ttu-id="04e13-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="04e13-195">passenger_count</span></span> | <span data-ttu-id="04e13-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="04e13-196">tip_amount</span></span> | <span data-ttu-id="04e13-197">tipped</span><span class="sxs-lookup"><span data-stu-id="04e13-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="04e13-198">13,5</span><span class="sxs-lookup"><span data-stu-id="04e13-198">13.5</span></span> |<span data-ttu-id="04e13-199">1.0</span><span class="sxs-lookup"><span data-stu-id="04e13-199">1.0</span></span> |<span data-ttu-id="04e13-200">2,9</span><span class="sxs-lookup"><span data-stu-id="04e13-200">2.9</span></span> |<span data-ttu-id="04e13-201">1.0</span><span class="sxs-lookup"><span data-stu-id="04e13-201">1.0</span></span> |
|        <span data-ttu-id="04e13-202">16,0</span><span class="sxs-lookup"><span data-stu-id="04e13-202">16.0</span></span> |<span data-ttu-id="04e13-203">2,0</span><span class="sxs-lookup"><span data-stu-id="04e13-203">2.0</span></span> |<span data-ttu-id="04e13-204">3.4</span><span class="sxs-lookup"><span data-stu-id="04e13-204">3.4</span></span> |<span data-ttu-id="04e13-205">1.0</span><span class="sxs-lookup"><span data-stu-id="04e13-205">1.0</span></span> |
|        <span data-ttu-id="04e13-206">10,5</span><span class="sxs-lookup"><span data-stu-id="04e13-206">10.5</span></span> |<span data-ttu-id="04e13-207">2,0</span><span class="sxs-lookup"><span data-stu-id="04e13-207">2.0</span></span> |<span data-ttu-id="04e13-208">1.0</span><span class="sxs-lookup"><span data-stu-id="04e13-208">1.0</span></span> |<span data-ttu-id="04e13-209">1.0</span><span class="sxs-lookup"><span data-stu-id="04e13-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="04e13-210">Исследование и визуализация данных</span><span class="sxs-lookup"><span data-stu-id="04e13-210">Data exploration and visualization</span></span>
<span data-ttu-id="04e13-211">После переноса данных hello в Spark, следующим шагом hello в hello процесса обработки и анализа данных является toogain более глубокое представление о данных hello через Просмотр и визуализация.</span><span class="sxs-lookup"><span data-stu-id="04e13-211">After you bring hello data into Spark, hello next step in hello Data Science process is toogain a deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="04e13-212">В этом разделе вы проверяете hello такси данных с помощью SQL-запросов.</span><span class="sxs-lookup"><span data-stu-id="04e13-212">In this section, you examine hello taxi data by using SQL queries.</span></span> <span data-ttu-id="04e13-213">Затем результаты импорта hello в кадр данных tooplot hello целевыми переменными и потенциального функций для визуальной проверки с помощью функции автоматического визуализации hello Jupyter.</span><span class="sxs-lookup"><span data-stu-id="04e13-213">Then, import hello results into a data frame tooplot hello target variables and prospective features for visual inspection by using hello auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-tooplot-data"></a><span data-ttu-id="04e13-214">Использование локальных и magic tooplot данных SQL</span><span class="sxs-lookup"><span data-stu-id="04e13-214">Use local and SQL magic tooplot data</span></span>
<span data-ttu-id="04e13-215">По умолчанию выходные данные hello фрагмента кода, запускаемого из записной книжке Jupyter доступна в контексте hello hello сеанса, в которой сохраняется на hello рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="04e13-215">By default, hello output of any code snippet that you run from a Jupyter notebook is available within hello context of hello session that is persisted on hello worker nodes.</span></span> <span data-ttu-id="04e13-216">Если требуется toosave trip toohello рабочих узлов для каждого вычисления, и если все hello данных, необходимых для вашей вычисление доступен локально на узел сервера Jupyter hello (который hello головного узла), можно использовать hello `%%local` магическая toorun кода hello фрагмент кода на сервере Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-216">If you want toosave a trip toohello worker nodes for every computation, and if all hello data that you need for your computation is available locally on hello Jupyter server node (which is hello head node), you can use hello `%%local` magic toorun hello code snippet on hello Jupyter server.</span></span>

* <span data-ttu-id="04e13-217">**Волшебная команда SQL** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="04e13-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="04e13-218">Hello ядра HDInsight Spark поддерживает запросы HiveQL легко встроенного к SQLContext.</span><span class="sxs-lookup"><span data-stu-id="04e13-218">hello HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="04e13-219">Hello (`-o VARIABLE_NAME`) аргумент hello выходных данных запроса SQL hello сохраняется как Pandas кадр данных на сервере Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-219">hello (`-o VARIABLE_NAME`) argument persists hello output of hello SQL query as a Pandas data frame on hello Jupyter server.</span></span> <span data-ttu-id="04e13-220">Это означает, что она доступна в локальном режиме hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-220">This means it'll be available in hello local mode.</span></span>
* <span data-ttu-id="04e13-221">`%%local` **Волшебная команда**.</span><span class="sxs-lookup"><span data-stu-id="04e13-221">`%%local` **magic**.</span></span> <span data-ttu-id="04e13-222">Hello `%%local` magic работает кода hello локально на сервере Jupyter hello, где hello головного узла кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-222">hello `%%local` magic runs hello code locally on hello Jupyter server, which is hello head node of hello HDInsight cluster.</span></span> <span data-ttu-id="04e13-223">Как правило, используется `%%local` magic вместе с hello `%%sql` magic с hello `-o` параметра.</span><span class="sxs-lookup"><span data-stu-id="04e13-223">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with hello `-o` parameter.</span></span> <span data-ttu-id="04e13-224">Hello `-o` параметр сохранится hello выходных данных запроса SQL hello локально, а затем `%%local` magic приведет к запуску hello следующего набора toorun фрагмент кода локально к выходным данным hello hello запросов SQL, в которой сохраняется локально.</span><span class="sxs-lookup"><span data-stu-id="04e13-224">hello `-o` parameter would persist hello output of hello SQL query locally, and then `%%local` magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally.</span></span>

### <a name="query-hello-data-by-using-sql"></a><span data-ttu-id="04e13-225">Запрос hello данных с помощью SQL</span><span class="sxs-lookup"><span data-stu-id="04e13-225">Query hello data by using SQL</span></span>
<span data-ttu-id="04e13-226">Этот запрос извлекает hello такси приема-передачи, сумма тариф авиакомпании, пассажира количество и сумма подсказки.</span><span class="sxs-lookup"><span data-stu-id="04e13-226">This query retrieves hello taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="04e13-227">В следующих кода hello, hello `%%local` magic создает кадр локальных данных sqlResults.</span><span class="sxs-lookup"><span data-stu-id="04e13-227">In hello following code, hello `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="04e13-228">Можно использовать sqlResults tooplot с помощью matplotlib.</span><span class="sxs-lookup"><span data-stu-id="04e13-228">You can use sqlResults tooplot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="04e13-229">В этой статье магическая команда local используется несколько раз.</span><span class="sxs-lookup"><span data-stu-id="04e13-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="04e13-230">Если набор данных имеет большой размер, проверьте образец toocreate кадра данных, помещающихся в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="04e13-230">If your data set is large, please sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-hello-data"></a><span data-ttu-id="04e13-231">Отобразить данные hello</span><span class="sxs-lookup"><span data-stu-id="04e13-231">Plot hello data</span></span>
<span data-ttu-id="04e13-232">Вы можете отобразить с помощью кода Python в локальном контексте виде блока данных Pandas после hello кадра данных.</span><span class="sxs-lookup"><span data-stu-id="04e13-232">You can plot by using Python code after hello data frame is in local context as a Pandas data frame.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="04e13-233">Hello Spark ядра автоматически визуализирует hello вывод запросов SQL (HiveQL) после выполнения кода hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-233">hello Spark kernel automatically visualizes hello output of SQL (HiveQL) queries after you run hello code.</span></span> <span data-ttu-id="04e13-234">Вы можете выбрать тип визуализации среди нескольких типов:</span><span class="sxs-lookup"><span data-stu-id="04e13-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="04e13-235">Таблица</span><span class="sxs-lookup"><span data-stu-id="04e13-235">Table</span></span>
* <span data-ttu-id="04e13-236">круговая диаграмма;</span><span class="sxs-lookup"><span data-stu-id="04e13-236">Pie</span></span>
* <span data-ttu-id="04e13-237">график;</span><span class="sxs-lookup"><span data-stu-id="04e13-237">Line</span></span>
* <span data-ttu-id="04e13-238">Область</span><span class="sxs-lookup"><span data-stu-id="04e13-238">Area</span></span>
* <span data-ttu-id="04e13-239">линейчатая диаграмма.</span><span class="sxs-lookup"><span data-stu-id="04e13-239">Bar</span></span>

<span data-ttu-id="04e13-240">Вот tooplot hello hello код данных:</span><span class="sxs-lookup"><span data-stu-id="04e13-240">Here's hello code tooplot hello data:</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


<span data-ttu-id="04e13-241">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-241">**Output:**</span></span>

![Гистограмма суммы чаевых](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Сумма чаевых в зависимости от количества пассажиров](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Сумма чаевых в зависимости от тарифа](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="04e13-245">Создание и преобразование признаков, а также последующая подготовка данных для ввода в функции моделирования</span><span class="sxs-lookup"><span data-stu-id="04e13-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="04e13-246">Для функций на основе дерева моделирования из Spark ML и MLlib имеется целевой tooprepare и компонентов с помощью различных методов, таких как группирование, индексирование, горячей один кодировки и векторизации.</span><span class="sxs-lookup"><span data-stu-id="04e13-246">For tree-based modeling functions from Spark ML and MLlib, you have tooprepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="04e13-247">Ниже приведены процедуры toofollow hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="04e13-247">Here are hello procedures toofollow in this section:</span></span>

1. <span data-ttu-id="04e13-248">Создание нового признака путем **группирования** часов в периоды трафика.</span><span class="sxs-lookup"><span data-stu-id="04e13-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="04e13-249">Применить **индексирования и один горячей кодировки** toocategorical функции.</span><span class="sxs-lookup"><span data-stu-id="04e13-249">Apply **indexing and one-hot encoding** toocategorical features.</span></span>
3. <span data-ttu-id="04e13-250">**Выборка и разбиение hello набора данных** в обучающий и проверочный дробей.</span><span class="sxs-lookup"><span data-stu-id="04e13-250">**Sample and split hello data set** into training and test fractions.</span></span>
4. <span data-ttu-id="04e13-251">**Указание переменной обучения и признаков**, а затем создание индексированных или прямо закодированных обучающих и проверочных устойчивых распределенных наборов данных (RDD) или входящих кадров данных с помеченной вершиной.</span><span class="sxs-lookup"><span data-stu-id="04e13-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="04e13-252">Автоматически **классификации и Векторизация функций и целевые объекты** toouse в качестве входных данных для моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="04e13-252">Automatically **categorize and vectorize features and targets** toouse as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="04e13-253">Создание нового признака путем группирования часов в периоды трафика</span><span class="sxs-lookup"><span data-stu-id="04e13-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="04e13-254">Этот код показывает, как toocreate новая функция путем сегментирования часов в момент трафик контейнеров и как toocache hello результирующий кадр данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="04e13-254">This code shows you how toocreate a new feature by binning hours into traffic time buckets and how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="04e13-255">При повторном использовании кадры RDDs и данные кэширование приводит tooimproved времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="04e13-255">Where RDDs and data frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="04e13-256">Соответственно будет кэшировать кадры RDDs и данные на нескольких этапах hello следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="04e13-256">Accordingly, you'll cache RDDs and data frames at several stages in hello following procedures.</span></span>

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="04e13-257">Индексирование и прямое кодирование категориальных признаков</span><span class="sxs-lookup"><span data-stu-id="04e13-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="04e13-258">Здравствуйте моделирования и предполагаете, что функции MLlib требуют возможности с помощью toobe категориальных данных входного индексированных или кодировке предыдущих toouse.</span><span class="sxs-lookup"><span data-stu-id="04e13-258">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="04e13-259">В этом разделе показано, как tooindex или кодирования категориальных признаков для входных данных в моделирования функции hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-259">This section shows you how tooindex or encode categorical features for input into hello modeling functions.</span></span>

<span data-ttu-id="04e13-260">Необходима tooindex или кодирования модели по-разному в зависимости от модели hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-260">You need tooindex or encode your models in different ways, depending on hello model.</span></span> <span data-ttu-id="04e13-261">Например, для моделей логистической и линейной регрессии требуется прямое кодирование.</span><span class="sxs-lookup"><span data-stu-id="04e13-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="04e13-262">Скажем, признак с тремя категориями можно представить в виде трех столбцов признаков.</span><span class="sxs-lookup"><span data-stu-id="04e13-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="04e13-263">Каждый столбец будет содержать 0 или 1 в зависимости от категории hello наблюдения.</span><span class="sxs-lookup"><span data-stu-id="04e13-263">Each column would contain 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="04e13-264">MLlib предоставляет hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) функция горячей один кодирования.</span><span class="sxs-lookup"><span data-stu-id="04e13-264">MLlib provides hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="04e13-265">Этот кодировщик сопоставляет столбец метки столбца tooa индексы двоичных векторов с не более одного значение single.</span><span class="sxs-lookup"><span data-stu-id="04e13-265">This encoder maps a column of label indices tooa column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="04e13-266">С этой кодировкой алгоритмы, которые ожидают числовой табличное значение функции, такие как логистической регрессии может быть применен toocategorical функции.</span><span class="sxs-lookup"><span data-stu-id="04e13-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied toocategorical features.</span></span>

<span data-ttu-id="04e13-267">Здесь можно преобразовать только четыре переменных tooshow примеры, которые являются символьные строки.</span><span class="sxs-lookup"><span data-stu-id="04e13-267">Here you transform only four variables tooshow examples, which are character strings.</span></span> <span data-ttu-id="04e13-268">Вы также можете индексировать другие переменные, такие как день недели, представленные числовыми значениями, в качестве категориальных переменных.</span><span class="sxs-lookup"><span data-stu-id="04e13-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="04e13-269">Для индексирования используйте функцию `StringIndexer()`, а для прямого кодирования — `OneHotEncoder()` из MLlib.</span><span class="sxs-lookup"><span data-stu-id="04e13-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="04e13-270">Ниже приведен код tooindex hello и кодирования категориальных признаков:</span><span class="sxs-lookup"><span data-stu-id="04e13-270">Here is hello code tooindex and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="04e13-271">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-271">**Output:**</span></span>

<span data-ttu-id="04e13-272">Время toorun hello ячейки: 4 секунды.</span><span class="sxs-lookup"><span data-stu-id="04e13-272">Time toorun hello cell: 4 seconds.</span></span>

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a><span data-ttu-id="04e13-273">Выборка и разбиение hello набора данных на обучающие и проверочные дроби</span><span class="sxs-lookup"><span data-stu-id="04e13-273">Sample and split hello data set into training and test fractions</span></span>
<span data-ttu-id="04e13-274">Этот код создает случайной выборки данных hello (25%, в этом примере).</span><span class="sxs-lookup"><span data-stu-id="04e13-274">This code creates a random sampling of hello data (25%, in this example).</span></span> <span data-ttu-id="04e13-275">Несмотря на то, что выборка не является обязательным для этого примера из-за toohello размер набора данных hello, hello статье показано, как можно произвести выборку, чтобы знать, как toouse его для собственных задач, если это требуется.</span><span class="sxs-lookup"><span data-stu-id="04e13-275">Although sampling is not required for this example due toohello size of hello data set, hello article shows you how you can sample so that you know how toouse it for your own problems when needed.</span></span> <span data-ttu-id="04e13-276">Если выборки большие, этот процесс может значительно сэкономить время обучения моделей.</span><span class="sxs-lookup"><span data-stu-id="04e13-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="04e13-277">Затем разделить образец hello в рамках обучения (75%, в этом примере) и проверочные часть toouse (25%, в этом примере) в классификации и регрессии моделирования.</span><span class="sxs-lookup"><span data-stu-id="04e13-277">Next, split hello sample into a training part (75%, in this example) and a testing part (25%, in this example) toouse in classification and regression modeling.</span></span>

<span data-ttu-id="04e13-278">Добавьте строку tooeach случайное число (от 0 до 1) (в столбце «rand»), может быть используется tooselect свертки перекрестной проверки во время обучения.</span><span class="sxs-lookup"><span data-stu-id="04e13-278">Add a random number (between 0 and 1) tooeach row (in a "rand" column) that can be used tooselect cross-validation folds during training.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="04e13-279">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-279">**Output:**</span></span>

<span data-ttu-id="04e13-280">Время toorun hello ячейки: 2 секунды.</span><span class="sxs-lookup"><span data-stu-id="04e13-280">Time toorun hello cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="04e13-281">Указание переменной обучения и признаков, а также последующее создание индексированных или прямо закодированных обучающих и проверочных RDD или входящих кадров данных с помеченной вершиной</span><span class="sxs-lookup"><span data-stu-id="04e13-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="04e13-282">Этот раздел содержит код, который будет показано, как tooindex категориальные текстовых данных, помеченных как выберите тип данных, а его кодирования, поэтому можно использовать алгоритм логистической регрессии MLlib tootrain и тестирования и другие модели классификации.</span><span class="sxs-lookup"><span data-stu-id="04e13-282">This section contains code that shows you how tooindex categorical text data as a labeled point data type, and encode it so you can use it tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="04e13-283">Объекты с помеченной вершиной отформатированы в RDD, которые можно использовать в качестве входных данных для большинства алгоритмов машинного обучения в MLlib.</span><span class="sxs-lookup"><span data-stu-id="04e13-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="04e13-284">Объект [с помеченной вершиной](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) — это разреженный или плотный локальный вектор, связанный с меткой или ответом.</span><span class="sxs-lookup"><span data-stu-id="04e13-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="04e13-285">В этом коде hello целевой (зависимого) переменной и указываются моделей tootrain toouse функции hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-285">In this code, you specify hello target (dependent) variable and hello features toouse tootrain models.</span></span> <span data-ttu-id="04e13-286">Затем вы создаете индексированные или прямо закодированные обучающие и проверочные RDD или входящие кадры данных с помеченной вершиной.</span><span class="sxs-lookup"><span data-stu-id="04e13-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="04e13-287">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-287">**Output:**</span></span>

<span data-ttu-id="04e13-288">Время toorun hello ячейки: 4 секунды.</span><span class="sxs-lookup"><span data-stu-id="04e13-288">Time toorun hello cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a><span data-ttu-id="04e13-289">Автоматически классификации и Векторизация toouse функции и целевых объектов в качестве входных данных для моделей машинного обучения</span><span class="sxs-lookup"><span data-stu-id="04e13-289">Automatically categorize and vectorize features and targets toouse as inputs for machine learning models</span></span>
<span data-ttu-id="04e13-290">Используйте Spark ML toocategorize hello целевой объект и компоненты toouse функций на основе дерева моделирования.</span><span class="sxs-lookup"><span data-stu-id="04e13-290">Use Spark ML toocategorize hello target and features toouse in tree-based modeling functions.</span></span> <span data-ttu-id="04e13-291">Код Hello выполняет две задачи:</span><span class="sxs-lookup"><span data-stu-id="04e13-291">hello code completes two tasks:</span></span>

* <span data-ttu-id="04e13-292">Создает двоичный целевым объектом для классификации, присвоив значение 0 или 1 tooeach точки данных, от 0 до 1 с помощью пороговое значение 0,5.</span><span class="sxs-lookup"><span data-stu-id="04e13-292">Creates a binary target for classification by assigning a value of 0 or 1 tooeach data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="04e13-293">Автоматически категоризирует признаки.</span><span class="sxs-lookup"><span data-stu-id="04e13-293">Automatically categorizes features.</span></span> <span data-ttu-id="04e13-294">Если количество различных числовых значений для любого компонента, hello меньше 32, категория эту функцию.</span><span class="sxs-lookup"><span data-stu-id="04e13-294">If hello number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="04e13-295">Ниже приведен код hello для этих двух задач.</span><span class="sxs-lookup"><span data-stu-id="04e13-295">Here's hello code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="04e13-296">Модель двоичной классификации: прогнозирование вероятности выплаты чаевых за поездку</span><span class="sxs-lookup"><span data-stu-id="04e13-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="04e13-297">В этом разделе создайте три типа ли должно быть уделено совет toopredict модели двоичной классификации:</span><span class="sxs-lookup"><span data-stu-id="04e13-297">In this section, you create three types of binary classification models toopredict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="04e13-298">Объект **модель логистической регрессии** с помощью hello Spark ML `LogisticRegression()` функции</span><span class="sxs-lookup"><span data-stu-id="04e13-298">A **logistic regression model** by using hello Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="04e13-299">Объект **модель классификации случайного леса** с помощью hello Spark ML `RandomForestClassifier()` функции</span><span class="sxs-lookup"><span data-stu-id="04e13-299">A **random forest classification model** by using hello Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="04e13-300">Объект **градиента подъема дерева модели классификации** с помощью hello MLlib `GradientBoostedTrees()` функции</span><span class="sxs-lookup"><span data-stu-id="04e13-300">A **gradient boosting tree classification model** by using hello MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="04e13-301">Создание модели логистической регрессии</span><span class="sxs-lookup"><span data-stu-id="04e13-301">Create a logistic regression model</span></span>
<span data-ttu-id="04e13-302">Создайте модель логистической регрессии с помощью hello Spark ML `LogisticRegression()` функции.</span><span class="sxs-lookup"><span data-stu-id="04e13-302">Next, create a logistic regression model by using hello Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="04e13-303">Здесь создается модель hello, построение кода в последовательность шагов:</span><span class="sxs-lookup"><span data-stu-id="04e13-303">You create hello model building code in a series of steps:</span></span>

1. <span data-ttu-id="04e13-304">**Обучение модели hello** данных с одним набором параметров.</span><span class="sxs-lookup"><span data-stu-id="04e13-304">**Train hello model** data with one parameter set.</span></span>
2. <span data-ttu-id="04e13-305">**Рассмотрение модели hello** на проверочного набора данных с метриками.</span><span class="sxs-lookup"><span data-stu-id="04e13-305">**Evaluate hello model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="04e13-306">**Сохранить модель hello** в хранилище больших двоичных объектов для последующей обработки.</span><span class="sxs-lookup"><span data-stu-id="04e13-306">**Save hello model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="04e13-307">**Модель оценки hello** для тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="04e13-307">**Score hello model** against test data.</span></span>
5. <span data-ttu-id="04e13-308">**Отобразить результаты hello** с получателем операционной кривых характеристика (ROC).</span><span class="sxs-lookup"><span data-stu-id="04e13-308">**Plot hello results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="04e13-309">Ниже приведен код hello для этих процедур.</span><span class="sxs-lookup"><span data-stu-id="04e13-309">Here's hello code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="04e13-310">Загрузки, оценки и сохранить результаты hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-310">Load, score, and save hello results.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="04e13-311">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-311">**Output:**</span></span>

<span data-ttu-id="04e13-312">ROC для тестовых данных — 0,9827381497557599.</span><span class="sxs-lookup"><span data-stu-id="04e13-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="04e13-313">На локальном кривой ROC hello tooplot Pandas данных кадров с помощью Python.</span><span class="sxs-lookup"><span data-stu-id="04e13-313">Use Python on local Pandas data frames tooplot hello ROC curve.</span></span>

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="04e13-314">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-314">**Output:**</span></span>

![Кривая ROC вероятности выплаты чаевых](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="04e13-316">Создание модели классификации случайного леса</span><span class="sxs-lookup"><span data-stu-id="04e13-316">Create a random forest classification model</span></span>
<span data-ttu-id="04e13-317">Создайте модель классификации случайного леса с помощью hello Spark ML `RandomForestClassifier()` функции, а затем проверять hello модели к тестовым данным.</span><span class="sxs-lookup"><span data-stu-id="04e13-317">Next, create a random forest classification model by using hello Spark ML `RandomForestClassifier()` function, and then evaluate hello model on test data.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="04e13-318">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-318">**Output:**</span></span>

<span data-ttu-id="04e13-319">ROC для тестовых данных — 0,9847103571552683.</span><span class="sxs-lookup"><span data-stu-id="04e13-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="04e13-320">Создание модели классификации по методу деревьев с градиентным повышением</span><span class="sxs-lookup"><span data-stu-id="04e13-320">Create a GBT classification model</span></span>
<span data-ttu-id="04e13-321">Создайте модель классификации GBT с помощью элемента MLlib `GradientBoostedTrees()` функции, а затем проверять hello модели к тестовым данным.</span><span class="sxs-lookup"><span data-stu-id="04e13-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate hello model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="04e13-322">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-322">**Output:**</span></span>

<span data-ttu-id="04e13-323">площадь под ROC — 0,9846895479241554.</span><span class="sxs-lookup"><span data-stu-id="04e13-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="04e13-324">Модель регрессии: прогнозирование суммы чаевых</span><span class="sxs-lookup"><span data-stu-id="04e13-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="04e13-325">В этом разделе создайте два вида сумму чаевых hello toopredict моделей регрессии:</span><span class="sxs-lookup"><span data-stu-id="04e13-325">In this section, you create two types of regression models toopredict hello tip amount:</span></span>

* <span data-ttu-id="04e13-326">Объект **модели линейной регрессии, регуляризованной** с помощью hello Spark ML `LinearRegression()` функции.</span><span class="sxs-lookup"><span data-stu-id="04e13-326">A **regularized linear regression model** by using hello Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="04e13-327">Можно сохранить модель hello и рассмотрение hello модели к тестовым данным.</span><span class="sxs-lookup"><span data-stu-id="04e13-327">You'll save hello model and evaluate hello model on test data.</span></span>
* <span data-ttu-id="04e13-328">Объект **повышение приоритета градиента модель дерева регрессии** с помощью hello Spark ML `GBTRegressor()` функции.</span><span class="sxs-lookup"><span data-stu-id="04e13-328">A **gradient-boosting tree regression model** by using hello Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="04e13-329">Создание регуляризованной линейной регрессии</span><span class="sxs-lookup"><span data-stu-id="04e13-329">Create a regularized linear regression model</span></span>
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="04e13-330">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-330">**Output:**</span></span>

<span data-ttu-id="04e13-331">Время toorun hello ячейки: 13 секунд.</span><span class="sxs-lookup"><span data-stu-id="04e13-331">Time toorun hello cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="04e13-332">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-332">**Output:**</span></span>

<span data-ttu-id="04e13-333">R-sqr для тестовых данных — 0,5960320470835743.</span><span class="sxs-lookup"><span data-stu-id="04e13-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="04e13-334">Далее запрос hello результатов тестов как кадра данных и AutoVizWidget и matplotlib toovisualize его.</span><span class="sxs-lookup"><span data-stu-id="04e13-334">Next, query hello test results as a data frame and use AutoVizWidget and matplotlib toovisualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="04e13-335">Код Hello создается фрейм локальных данных из результатов запроса hello и представлены данные hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-335">hello code creates a local data frame from hello query output and plots hello data.</span></span> <span data-ttu-id="04e13-336">Hello `%%local` magic создает кадр локальных данных `sqlResults`, который можно использовать с matplotlib tooplot.</span><span class="sxs-lookup"><span data-stu-id="04e13-336">hello `%%local` magic creates a local data frame, `sqlResults`, which you can use tooplot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="04e13-337">В этой статье данная магическая команда Spark используется несколько раз.</span><span class="sxs-lookup"><span data-stu-id="04e13-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="04e13-338">При больших размерах hello объем данных следует образец toocreate кадра данных, помещающихся в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="04e13-338">If hello amount of data is large, you should sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="04e13-339">Создайте график с помощью "matplotlib" Python.</span><span class="sxs-lookup"><span data-stu-id="04e13-339">Create plots by using Python matplotlib.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="04e13-340">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-340">**Output:**</span></span>

![Сумма чаевых: соотношение фактической и прогнозируемой суммы](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="04e13-342">Создание модели регрессии GBT</span><span class="sxs-lookup"><span data-stu-id="04e13-342">Create a GBT regression model</span></span>
<span data-ttu-id="04e13-343">Создать модель регрессии GBT с помощью hello Spark ML `GBTRegressor()` функции, а затем проверять hello модели к тестовым данным.</span><span class="sxs-lookup"><span data-stu-id="04e13-343">Create a GBT regression model by using hello Spark ML `GBTRegressor()` function, and then evaluate hello model on test data.</span></span>

<span data-ttu-id="04e13-344">[Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="04e13-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="04e13-345">Решение GBTs обучение итеративного дерева toominimize функции потерь.</span><span class="sxs-lookup"><span data-stu-id="04e13-345">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="04e13-346">Деревья с градиентным повышением можно использовать для моделей регрессии и классификации.</span><span class="sxs-lookup"><span data-stu-id="04e13-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="04e13-347">С их помощью можно обрабатывать категориальные признаки, а также определять нелинейные зависимости и взаимодействия признаков. Этот метод не требует масштабирования признаков.</span><span class="sxs-lookup"><span data-stu-id="04e13-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="04e13-348">Кроме того, их можно использовать для создания модели мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="04e13-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="04e13-349">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-349">**Output:**</span></span>

<span data-ttu-id="04e13-350">Test R-sqr — 0,7655383534596654.</span><span class="sxs-lookup"><span data-stu-id="04e13-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="04e13-351">Служебные программы расширенного моделирования для оптимизации</span><span class="sxs-lookup"><span data-stu-id="04e13-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="04e13-352">В этом разделе используются служебные программы машинного обучения, которые часто применяют для оптимизации моделей.</span><span class="sxs-lookup"><span data-stu-id="04e13-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="04e13-353">В частности, есть три разных способа оптимизации моделей машинного обучения с использованием перебора параметров и перекрестной проверки.</span><span class="sxs-lookup"><span data-stu-id="04e13-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="04e13-354">Разбиение данных hello на обучение и проверка наборов, оптимизация hello модели с помощью свертки hyper параметров на основе набора и вычисления в проверочном наборе (Линейная регрессия)</span><span class="sxs-lookup"><span data-stu-id="04e13-354">Split hello data into train and validation sets, optimize hello model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="04e13-355">Оптимизация hello модели с помощью перекрестной проверки и hyper-очистки параметров с помощью функции CrossValidator Spark ML (двоичная классификация)</span><span class="sxs-lookup"><span data-stu-id="04e13-355">Optimize hello model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="04e13-356">Оптимизация hello модели с помощью пользовательского кода перекрестной проверки и выполнить очистку параметров toouse любой машинного обучения набор функций и параметров (Линейная регрессия)</span><span class="sxs-lookup"><span data-stu-id="04e13-356">Optimize hello model by using custom cross-validation and parameter-sweeping code toouse any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="04e13-357">**Перекрестная проверка** — это метод, который оценивает, насколько хорошо модель, обученную на известный набор данных будет generalize функции hello toopredict наборов данных, на которых он еще не прошла обучение.</span><span class="sxs-lookup"><span data-stu-id="04e13-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize toopredict hello features of data sets on which it has not been trained.</span></span> <span data-ttu-id="04e13-358">Hello общие идея этот способ является обучения модели на основе набора данных, известных данных, которое затем hello точности прогнозов его проверяется на основе независимый набор данных.</span><span class="sxs-lookup"><span data-stu-id="04e13-358">hello general idea behind this technique is that a model is trained on a data set of known data, and then hello accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="04e13-359">Типичная реализация — toodivide набора данных в *k*-свертывает, а затем обучения модели hello в циклического перебора всех, кроме одного сверток hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-359">A common implementation is toodivide a data set into *k*-folds, and then train hello model in a round-robin fashion on all but one of hello folds.</span></span>

<span data-ttu-id="04e13-360">**Hyper параметр оптимизации** проблема hello выбрать набор параметров hyper-для алгоритма обучения, обычно с целью hello оптимизация показателем производительности hello алгоритм на независимый набор данных.</span><span class="sxs-lookup"><span data-stu-id="04e13-360">**Hyper-parameter optimization** is hello problem of choosing a set of hyper-parameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="04e13-361">Hyper параметр является значением, которое необходимо указать вне процедуры обучения модели hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-361">A hyper-parameter is a value that you must specify outside hello model training procedure.</span></span> <span data-ttu-id="04e13-362">Предположения о значениях hyper параметров может повлиять на hello гибкость и точность модели hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-362">Assumptions about hyper-parameter values can affect hello flexibility and accuracy of hello model.</span></span> <span data-ttu-id="04e13-363">Деревья принятия решений имеют hyper параметры, например, такие как hello требуемого глубины и количества листьев в дереве hello.</span><span class="sxs-lookup"><span data-stu-id="04e13-363">Decision trees have hyper-parameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="04e13-364">Для метода опорных векторов (SVM) необходимо задать условие штрафа за неправильную классификацию.</span><span class="sxs-lookup"><span data-stu-id="04e13-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="04e13-365">Обычно hyper параметр для оптимизации tooperform способом является toouse поиска сетки, также называемый **очистки параметров**.</span><span class="sxs-lookup"><span data-stu-id="04e13-365">A common way tooperform hyper-parameter optimization is toouse a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="04e13-366">В поиске сетки тщательный поиск выполняется по значениям hello определенному подмножеству hello пространства hyper параметр для алгоритма обучения.</span><span class="sxs-lookup"><span data-stu-id="04e13-366">In a grid search, an exhaustive search is performed through hello values of a specified subset of hello hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="04e13-367">Перекрестная проверка может предоставить toosort метрики производительности out hello оптимальные результаты, найденные с помощью алгоритма поиска hello сетки.</span><span class="sxs-lookup"><span data-stu-id="04e13-367">Cross-validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="04e13-368">При использовании свертки перекрестной проверки hyper параметров, может помочь предел подобных лжевзаимосвязей tootraining модели данных.</span><span class="sxs-lookup"><span data-stu-id="04e13-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model tootraining data.</span></span> <span data-ttu-id="04e13-369">В этом случае модель hello сохраняет hello емкость tooapply toohello общий набор данных, из которой hello обучающие данные были извлечены.</span><span class="sxs-lookup"><span data-stu-id="04e13-369">This way, hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="04e13-370">Оптимизация модели линейной регрессии с помощью перебора гиперпараметров</span><span class="sxs-lookup"><span data-stu-id="04e13-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="04e13-371">Затем разбиение данных на обучение и проверка наборов, используйте hyper-очистки параметров в обучении модели hello toooptimize задано и оценки в проверочном наборе (Линейная регрессия).</span><span class="sxs-lookup"><span data-stu-id="04e13-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set toooptimize hello model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="04e13-372">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-372">**Output:**</span></span>

<span data-ttu-id="04e13-373">Test R-sqr — 0,6226484708501209</span><span class="sxs-lookup"><span data-stu-id="04e13-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="04e13-374">Оптимизировать hello модель двоичной классификации с помощью свертки перекрестной проверки и hyper параметр</span><span class="sxs-lookup"><span data-stu-id="04e13-374">Optimize hello binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="04e13-375">В этом разделе показано, как моделировать toooptimize двоичной классификации с использованием свертки перекрестной проверки и hyper параметр.</span><span class="sxs-lookup"><span data-stu-id="04e13-375">This section shows you how toooptimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="04e13-376">В этом случае используется hello Spark ML `CrossValidator` функции.</span><span class="sxs-lookup"><span data-stu-id="04e13-376">This uses hello Spark ML `CrossValidator` function.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="04e13-377">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-377">**Output:**</span></span>

<span data-ttu-id="04e13-378">Время toorun hello ячейки: 33 секунды.</span><span class="sxs-lookup"><span data-stu-id="04e13-378">Time toorun hello cell: 33 seconds.</span></span>

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="04e13-379">Оптимизация модели линейной регрессии hello с помощью пользовательского кода перекрестной проверки и выполнить очистку параметров</span><span class="sxs-lookup"><span data-stu-id="04e13-379">Optimize hello linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="04e13-380">Затем оптимизация hello модели с помощью пользовательского кода и определить hello оптимальных параметров модели с помощью hello критерию высокой степени точности.</span><span class="sxs-lookup"><span data-stu-id="04e13-380">Next, optimize hello model by using custom code, and identify hello best model parameters by using hello criterion of highest accuracy.</span></span> <span data-ttu-id="04e13-381">Затем создайте окончательной модели hello, оценивать hello модели к тестовым данным и сохранить модель hello в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="04e13-381">Then, create hello final model, evaluate hello model on test data, and save hello model in Blob storage.</span></span> <span data-ttu-id="04e13-382">Наконец загрузить модель hello оценки тестовые данные и оценить точность.</span><span class="sxs-lookup"><span data-stu-id="04e13-382">Finally, load hello model, score test data, and evaluate accuracy.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="04e13-383">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="04e13-383">**Output:**</span></span>

<span data-ttu-id="04e13-384">Время toorun hello ячейки: 61 секунд.</span><span class="sxs-lookup"><span data-stu-id="04e13-384">Time toorun hello cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="04e13-385">Автоматическое использование моделей машинного обучения на основе Spark с кодом Scala</span><span class="sxs-lookup"><span data-stu-id="04e13-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="04e13-386">Обзор разделы с пошаговыми руководствами hello задачами, которые составляют hello процесса обработки и анализа данных в Azure см. в разделе [процесс обработки и анализа данных для команды](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="04e13-386">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="04e13-387">[Пошаговые руководства по процессу для обработки и анализа данных командного](data-science-process-walkthroughs.md) описывает другие руководства начала до конца, демонстрирующие hello шагов в hello командного процесса обработки и анализа данных для конкретных сценариев.</span><span class="sxs-lookup"><span data-stu-id="04e13-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="04e13-388">Пошаговые руководства Hello также показывают, как облачные toocombine и локальных средств и служб в рабочий процесс или конвейера toocreate интеллектуальной приложения.</span><span class="sxs-lookup"><span data-stu-id="04e13-388">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

<span data-ttu-id="04e13-389">[Оценка построения Spark машинного обучения моделей](machine-learning-data-science-spark-model-consumption.md) показано, как код tooautomatically toouse Scala загрузки и оценки новых наборов данных с помощью машинного обучения моделей встроенные Spark и в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="04e13-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how toouse Scala code tooautomatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="04e13-390">Следуйте приведенным инструкциям hello наличие и просто заменить hello кода Python Scala кода в этой статье для автоматических потребления.</span><span class="sxs-lookup"><span data-stu-id="04e13-390">You can follow hello instructions provided there, and simply replace hello Python code with Scala code in this article for automated consumption.</span></span>

