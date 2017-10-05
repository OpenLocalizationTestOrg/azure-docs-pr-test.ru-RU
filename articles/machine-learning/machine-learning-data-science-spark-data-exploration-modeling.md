---
title: "Исследование и моделирование данных с помощью Spark | Документация Майкрософт"
description: "В этой статье показаны возможности исследования и моделирования данных с помощью набора средств Spark MLlib в Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 711407f7dd9e6d442e3f04a23962487f4808e8e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="98910-103">Исследование и моделирование данных с помощью Spark</span><span class="sxs-lookup"><span data-stu-id="98910-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="98910-104">В этом пошаговом руководстве рассматривается исследование и моделирование данных с применением двоичной классификации и регрессии на примере набора данных о поездках в такси по Нью-Йорку и тарифах за 2013 г. с помощью HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="98910-104">This walkthrough uses HDInsight Spark to do data exploration and binary classification and regression modeling tasks on a sample of the NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="98910-105">Здесь также подробно описаны этапы [анализа и обработки данных](http://aka.ms/datascienceprocess) с использованием кластера HDInsight Spark по обработке данных и больших двоичных объектов Azure для хранения данных и моделей.</span><span class="sxs-lookup"><span data-stu-id="98910-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="98910-106">В ходе этой процедуры данные из большого двоичного объекта службы хранилища Azure сначала исследуются и визуализируются, а затем подготавливаются для создания прогнозных моделей.</span><span class="sxs-lookup"><span data-stu-id="98910-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="98910-107">Эти модели создаются с помощью набора средств Spark MLlib для выполнения задач двоичной классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="98910-107">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="98910-108">Задача **двоичной классификации** : спрогнозировать, будут ли выплачены чаевые за поездку.</span><span class="sxs-lookup"><span data-stu-id="98910-108">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="98910-109">Задача **регрессии** : спрогнозировать сумму чаевых в зависимости от других признаков.</span><span class="sxs-lookup"><span data-stu-id="98910-109">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="98910-110">Мы использовали такие модели, как логистическая и линейная регрессия, случайные леса и градиентный бустинг деревьев.</span><span class="sxs-lookup"><span data-stu-id="98910-110">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="98910-111">[Линейная регрессия с применением SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) — модель линейной регрессии, в которой используется метод стохастического градиента для оптимизации и масштабирование признаков для прогнозирования суммы чаевых.</span><span class="sxs-lookup"><span data-stu-id="98910-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="98910-112">[Логистическая регрессия с применением алгоритма LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) (или логит-регрессия) — регрессионная модель, которая используется для классификации данных, если зависимая переменная является категориальной.</span><span class="sxs-lookup"><span data-stu-id="98910-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="98910-113">Алгоритм LBFGS — это широко используемый в машинном обучении квазиньютоновский алгоритм оптимизации, который представляет собой модифицированный метод Бройдена — Флетчера — Гольдфарба — Шанно (BFGS) с ограниченным использованием компьютерной памяти.</span><span class="sxs-lookup"><span data-stu-id="98910-113">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="98910-114">[Случайные леса](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="98910-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="98910-115">Такие совокупности минимизируют необходимость в переобучении.</span><span class="sxs-lookup"><span data-stu-id="98910-115">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="98910-116">Случайные леса используются для регрессии и классификации, могут обрабатывать категориальные функции и могут быть расширены до многоклассовой настройки классификации.</span><span class="sxs-lookup"><span data-stu-id="98910-116">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="98910-117">С их помощью можно определять нелинейные зависимости и взаимодействия признаков. Этот метод не требует масштабирования признаков.</span><span class="sxs-lookup"><span data-stu-id="98910-117">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="98910-118">Случайные леса — одна из самых эффективных моделей машинного обучения для задач классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="98910-118">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="98910-119">[Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="98910-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="98910-120">Этот метод предусматривает итеративное обучение деревьев принятия решений, что позволяет свести потери к минимуму.</span><span class="sxs-lookup"><span data-stu-id="98910-120">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="98910-121">Он применяется для задач классификации и регрессии. С его помощью можно обрабатывать категориальные признаки, а также определять нелинейные зависимости и взаимодействия признаков. Этот метод не требует масштабирования признаков.</span><span class="sxs-lookup"><span data-stu-id="98910-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="98910-122">Кроме того, его можно использовать для создания модели мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="98910-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="98910-123">Здесь также содержатся примеры кода, демонстрирующие процесс обучения, анализа и сохранения модели каждого типа.</span><span class="sxs-lookup"><span data-stu-id="98910-123">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="98910-124">Чтобы создать код решения и составить соответствующие графики, использовался язык Python.</span><span class="sxs-lookup"><span data-stu-id="98910-124">Python has been used to code the solution and to show the relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="98910-125">Несмотря на то что набор средств Spark MLlib предназначен для работы с большими наборами данных, для удобства мы будем использовать относительно небольшую выборку (приблизительно 30 МБ, 170 тыс. строк, примерно 0,1 % исходного набора данных о поездках в такси по Нью-Йорку).</span><span class="sxs-lookup"><span data-stu-id="98910-125">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="98910-126">Описанные в этой статье задачи можно эффективно выполнить (примерно за 10 минут) в кластере HDInsight с 2 рабочими узлами.</span><span class="sxs-lookup"><span data-stu-id="98910-126">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="98910-127">Тот же код (с незначительными изменениями) можно использовать для обработки больших наборов данных. Необходимо лишь внести соответствующие изменения для кэширования данных в памяти или изменения размера кластера.</span><span class="sxs-lookup"><span data-stu-id="98910-127">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="98910-128">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="98910-128">Prerequisites</span></span>
<span data-ttu-id="98910-129">Для работы с этим пошаговым руководством требуется учетная запись Azure и кластер Spark 1.6 или Spark 2.0 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98910-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="98910-130">См. статью [Общие сведения об обработке и анализе данных с помощью платформы Spark в Azure HDInsight](machine-learning-data-science-spark-overview.md) для получения инструкций по выполнению этих требований.</span><span class="sxs-lookup"><span data-stu-id="98910-130">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="98910-131">В этой статье также содержится описание используемых здесь данных о поездках в такси по Нью-Йорку за 2013 г., и инструкции по выполнению кода из записной книжки Jupyter в кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="98910-131">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="98910-132">Кластеры и записные книжки Spark</span><span class="sxs-lookup"><span data-stu-id="98910-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="98910-133">Действия по настройке и код, указанные в этом пошаговом руководстве, применимы к использованию для HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="98910-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="98910-134">Но записные книжки Jupyter можно использовать для кластеров HDInsight Spark 1.6 и Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="98910-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="98910-135">Описание записных книжек и ссылки на них вы можете найти в файле [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) для репозитория GitHub с записными книжками.</span><span class="sxs-lookup"><span data-stu-id="98910-135">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="98910-136">Более того, код здесь и в связанных записных книжках является универсальным и должен работать в любом кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="98910-136">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="98910-137">Действия по настройке кластера и управлению им могут немного отличаться от приведенных здесь, если вы не используете HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="98910-137">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="98910-138">Для удобства мы приводим ссылки на записные книжки Jupyter для Spark 1.6 (выполняемые в ядре PySpark на сервере записной книжки Jupyter) и Spark 2.0 (выполняемые в ядре PySpark3 на сервере записной книжки Jupyter).</span><span class="sxs-lookup"><span data-stu-id="98910-138">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 (to be run in the pySpark kernel of the Jupyter Notebook server) and  Spark 2.0 (to be run in the pySpark3 kernel of the Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="98910-139">Записные книжки для Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="98910-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="98910-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb). Содержит сведения о том, как выполнять просмотр данных, моделирование и оценку с использованием нескольких различных алгоритмов.</span><span class="sxs-lookup"><span data-stu-id="98910-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how to perform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="98910-141">Записные книжки для Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="98910-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="98910-142">Задачи регрессии и классификации, реализованные с помощью кластера Spark 2.0, находятся в отдельных записных книжках и используют другой набор данных:</span><span class="sxs-lookup"><span data-stu-id="98910-142">The regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and the classification notebook uses a different data set:</span></span>

- <span data-ttu-id="98910-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb). Содержит сведения о том, как выполнять просмотр данных, моделирование и оценку в кластерах Spark 2.0 на примере набора данных о расстояниях и ценах на такси в Нью-Йорке, описанного [здесь](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="98910-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="98910-144">Эту записную книжку можно использовать в качестве отправной точки для быстрого изучения кода, предоставленного для Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="98910-144">This notebook may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> <span data-ttu-id="98910-145">В следующей записной книжке списка приведен более детальный анализ данных о поездках в такси по Нью-Йорку</span><span class="sxs-lookup"><span data-stu-id="98910-145">For a more detailed notebook analyzes the NYC Taxi data, see the next notebook in this list.</span></span> <span data-ttu-id="98910-146">(см. примечания после списка сравнения этих записных книжек).</span><span class="sxs-lookup"><span data-stu-id="98910-146">See the notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="98910-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb). Демонстрирует, как можно выполнять структурирование данных (Spark SQL и операции с кадрами данных), просмотр данных, моделирование и оценку на примере набора данных о расстояниях и ценах на такси в Нью-Йорке, который описан [здесь](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="98910-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="98910-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb). Демонстрирует, как можно выполнять структурирование данных (Spark SQL и операции с кадрами данных), просмотр данных, моделирование и оценку на примере известного набора данных о расписании вылетов авиакомпании за 2011 и 2012 гг.</span><span class="sxs-lookup"><span data-stu-id="98910-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="98910-149">До моделирования мы дополнили набор данных об авиарейсах набором данных о погоде в аэропортах (скорость ветра, температура, высота над уровнем моря и т. д.), чтобы включить в модель эту информацию о погоде.</span><span class="sxs-lookup"><span data-stu-id="98910-149">We integrated the airline dataset with the airport weather data (e.g. windspeed, temperature, altitude etc.) prior to modeling, so these weather features can be included in the model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="98910-150">В записные книжки для Spark 2.0 был добавлен набор данных об авиарейсах, который лучше иллюстрирует использование алгоритмов классификации.</span><span class="sxs-lookup"><span data-stu-id="98910-150">The airline dataset was added to the Spark 2.0 notebooks to better illustrate the use of classification algorithms.</span></span> <span data-ttu-id="98910-151">Следующие ссылки помогут получить информацию о наборах данных о расписании вылетов авиакомпании и о погоде.</span><span class="sxs-lookup"><span data-stu-id="98910-151">See the following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="98910-152">Данные о расписании вылетов авиакомпании: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="98910-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="98910-153">Данные о погоде в аэропортах: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="98910-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="98910-154">Выполнение записных книжек Spark 2.0 с наборами данных о поездках в такси по Нью-Йорку и задержке рейсов может занять примерно 10 минут или больше (в зависимости от размера кластера HDI).</span><span class="sxs-lookup"><span data-stu-id="98910-154">The Spark 2.0 notebooks on the NYC taxi and airline flight delay data-sets can take 10 mins or more to run (depending on the size of your HDI cluster).</span></span> <span data-ttu-id="98910-155">В первой записной книжке из приведенного выше списка показаны многие аспекты исследования и визуализации данных, а также обучения модели машинного обучения. За счет уменьшения набора данных о поездках в такси по Нью-Йорку, в котором данные о поездках и тарифах на них объединены в один файл [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb), выполнение и завершение этой записной книжки занимает значительно меньше времени (2–3 минуты), и поэтому ее хорошо использовать в качестве отправной точки для быстрого изучения кода, предоставленного для Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="98910-155">The first notebook in the above list shows many aspects of the data exploration, visualization and ML model training in a notebook that takes less time to run with down-sampled NYC data set, in which the taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time to finish (2-3 mins) and may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="98910-156">Описания, приведенные ниже, относятся к Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="98910-156">The descriptions below are related to using Spark 1.6.</span></span> <span data-ttu-id="98910-157">Для Spark 2.0 используйте записные книжки, описанные выше.</span><span class="sxs-lookup"><span data-stu-id="98910-157">For Spark 2.0 versions, please use the notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="98910-158">Настройка места хранения, библиотек и предустановленного контекста Spark</span><span class="sxs-lookup"><span data-stu-id="98910-158">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="98910-159">Spark может считывать данные и записывать их в хранилище BLOB-объектов Azure (также известное как WASB).</span><span class="sxs-lookup"><span data-stu-id="98910-159">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="98910-160">Таким образом, данные из хранилища можно обрабатывать с помощью Spark и сохранять полученные данные в этом же хранилище.</span><span class="sxs-lookup"><span data-stu-id="98910-160">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="98910-161">Чтобы сохранить модели или файлы в хранилище BLOB-объектов, необходимо указать путь соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="98910-161">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="98910-162">Контейнер по умолчанию, присоединенный к кластеру Spark, можно указать с помощью пути, который начинается с "wasb:///".</span><span class="sxs-lookup"><span data-stu-id="98910-162">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="98910-163">Другие расположения начинаются с wasb://.</span><span class="sxs-lookup"><span data-stu-id="98910-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="98910-164">Настройка путей каталога к месту хранения в хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="98910-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="98910-165">В следующем примере кода указывается расположение данных, которые необходимо считать, и путь для каталога хранилища модели, где сохраняются выходные данные модели:</span><span class="sxs-lookup"><span data-stu-id="98910-165">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="98910-166">Импорт библиотек</span><span class="sxs-lookup"><span data-stu-id="98910-166">Import libraries</span></span>
<span data-ttu-id="98910-167">Для установки также требуется импорт необходимых библиотек.</span><span class="sxs-lookup"><span data-stu-id="98910-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="98910-168">Чтобы импортировать библиотеки и настроить контекст Spark, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="98910-168">Set spark context and import necessary libraries with the following code:</span></span>

    # IMPORT LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="98910-169">Предустановленный контекст Spark и волшебные команды PySpark</span><span class="sxs-lookup"><span data-stu-id="98910-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="98910-170">Ядра PySpark, входящие в состав записных книжек Jupyter, имеют предустановленный контекст.</span><span class="sxs-lookup"><span data-stu-id="98910-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="98910-171">Поэтому перед началом работы с разрабатываемым приложением вам не нужно явно задавать контексты Spark или Hive.</span><span class="sxs-lookup"><span data-stu-id="98910-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="98910-172">Эти контексты доступны вам по умолчанию,</span><span class="sxs-lookup"><span data-stu-id="98910-172">These contexts are available for you by default.</span></span> <span data-ttu-id="98910-173">а именно:</span><span class="sxs-lookup"><span data-stu-id="98910-173">These contexts are:</span></span>

* <span data-ttu-id="98910-174">sc для Spark;</span><span class="sxs-lookup"><span data-stu-id="98910-174">sc - for Spark</span></span> 
* <span data-ttu-id="98910-175">sqlContext для Hive.</span><span class="sxs-lookup"><span data-stu-id="98910-175">sqlContext - for Hive</span></span>

<span data-ttu-id="98910-176">Ядро PySpark предоставляет несколько "волшебных команд". Это специальные команды, которые можно вызывать с %%.</span><span class="sxs-lookup"><span data-stu-id="98910-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="98910-177">В этих примерах кода используются две подобные команды.</span><span class="sxs-lookup"><span data-stu-id="98910-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="98910-178">**%%local** Указывает, что код в последующих строках будет выполнен локально.</span><span class="sxs-lookup"><span data-stu-id="98910-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="98910-179">В качестве кода должен быть указан корректный код Python.</span><span class="sxs-lookup"><span data-stu-id="98910-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="98910-180">**%%sql -o <variable name>** Выполняет запрос Hive к sqlContext.</span><span class="sxs-lookup"><span data-stu-id="98910-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="98910-181">Если передан параметр -o, результат запроса сохраняется в контексте %%local Python в формате Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="98910-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="98910-182">Дополнительные сведения о ядрах для записных книжек Jupyter и предустановленных "волшебных командах", которые они предоставляют, см. в статье [Ядра, доступные для использования записными книжками Jupyter с кластерами Apache Spark в HDInsight на платформе Linux](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="98910-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="98910-183">Прием данных из открытого большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="98910-183">Data ingestion from public blob</span></span>
<span data-ttu-id="98910-184">Чтобы начать анализ и обработку необходимых данных, требуется переместить их из источников, в которых они находятся, в среду исследования и моделирования данных.</span><span class="sxs-lookup"><span data-stu-id="98910-184">The first step in the data science process is to ingest the data to be analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="98910-185">В нашем пошаговом руководстве это среда Spark.</span><span class="sxs-lookup"><span data-stu-id="98910-185">The environment is Spark in this walkthrough.</span></span> <span data-ttu-id="98910-186">Этот раздел содержит код, с помощью которого можно выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="98910-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="98910-187">прием выборки данных, которые нужно моделировать;</span><span class="sxs-lookup"><span data-stu-id="98910-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="98910-188">считывание входного набора данных (TSV-файл);</span><span class="sxs-lookup"><span data-stu-id="98910-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="98910-189">форматирование и очистка данных;</span><span class="sxs-lookup"><span data-stu-id="98910-189">format and clean the data</span></span>
* <span data-ttu-id="98910-190">создание и кэширование объектов (устойчивых распределенных наборов данных или фреймов данных) в памяти;</span><span class="sxs-lookup"><span data-stu-id="98910-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="98910-191">регистрация данных в качестве временной таблицы в контексте SQL.</span><span class="sxs-lookup"><span data-stu-id="98910-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="98910-192">Ниже приведен код для приема данных.</span><span class="sxs-lookup"><span data-stu-id="98910-192">Here is the code for data ingestion.</span></span>

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="98910-193">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-193">**OUTPUT:**</span></span>

<span data-ttu-id="98910-194">Время на выполнение кода выше: 51,72 с.</span><span class="sxs-lookup"><span data-stu-id="98910-194">Time taken to execute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="98910-195">Исследование и визуализация данных</span><span class="sxs-lookup"><span data-stu-id="98910-195">Data exploration & visualization</span></span>
<span data-ttu-id="98910-196">После помещения данных в Spark необходимо исследовать и визуализировать их, чтобы получить более глубокое представление.</span><span class="sxs-lookup"><span data-stu-id="98910-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="98910-197">В этом разделе мы исследуем данные о поездках в такси с помощью SQL-запросов и составим графики целевых переменных и потенциальных признаков для визуального контроля.</span><span class="sxs-lookup"><span data-stu-id="98910-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="98910-198">В частности, мы составим график частоты поездок в такси, частоты оставления чаевых и зависимости суммы чаевых от тарифа и типа платежа.</span><span class="sxs-lookup"><span data-stu-id="98910-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="98910-199">Построение гистограммы количества пассажиров в выборке данных о поездках на такси</span><span class="sxs-lookup"><span data-stu-id="98910-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="98910-200">Этот код и последующие фрагменты используют волшебную команду SQL для запроса примера и локальную волшебную команду для графического представления данных.</span><span class="sxs-lookup"><span data-stu-id="98910-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="98910-201">**SQL magic (`%%sql`)** Ядро HDInsight PySpark позволяет легко выполнять встроенные запросы HiveQL к sqlContext.</span><span class="sxs-lookup"><span data-stu-id="98910-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="98910-202">Аргумент (-o VARIABLE_NAME) сохраняет выходные данные запроса SQL в формате Pandas DataFrame на сервере Jupyter.</span><span class="sxs-lookup"><span data-stu-id="98910-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="98910-203">Это означает, что они доступны в локальном режиме.</span><span class="sxs-lookup"><span data-stu-id="98910-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="98910-204">Магическая команда **`%%local`** используется для локального выполнения кода на сервере Jupyter, который представляет собой головной узел кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98910-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="98910-205">Как правило, магическая команда `%%local` используется в комбинации с командой `%%sql` с параметром -o.</span><span class="sxs-lookup"><span data-stu-id="98910-205">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="98910-206">Параметр -o сохраняет выходные данные запроса SQL локально, после чего волшебная команда %%local активирует следующий набор фрагментов кода, который выполняется локально с выходными данными запросов SQL, сохраненными на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="98910-206">The -o parameter would persist the output of the SQL query locally and then %%local magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally</span></span>

<span data-ttu-id="98910-207">После выполнения кода выходные данные визуализируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="98910-207">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="98910-208">Этот запрос извлекает поездки по количеству пассажиров.</span><span class="sxs-lookup"><span data-stu-id="98910-208">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST THE sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="98910-209">Этот код создает локальный фрейм данных из выходных данных запроса и формирует графическое представление данных.</span><span class="sxs-lookup"><span data-stu-id="98910-209">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="98910-210">Магическая команда `%%local` создает локальный кадр данных `sqlResults`, который можно использовать для формирования графического представления данных с помощью matplotlib.</span><span class="sxs-lookup"><span data-stu-id="98910-210">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="98910-211">В этом пошаговом руководстве волшебная команда PySpark используется несколько раз.</span><span class="sxs-lookup"><span data-stu-id="98910-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="98910-212">Если объем данных большой, сделайте выборку, чтобы создать фрейм данных, который можно разместить в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="98910-212">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="98910-213">Код для получения графического представления поездок по числу пассажиров</span><span class="sxs-lookup"><span data-stu-id="98910-213">Here is the code to plot the trips by passenger counts</span></span>

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="98910-214">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-214">**OUTPUT:**</span></span>

![Частота поездок в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="98910-216">С помощью кнопок в меню **Тип** в записной книжке можно выбрать один из нескольких типов визуализации (таблица либо круговая, линейная, комбинированная или столбчатая диаграмма).</span><span class="sxs-lookup"><span data-stu-id="98910-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="98910-217">Здесь показано представление столбчатой диаграммы.</span><span class="sxs-lookup"><span data-stu-id="98910-217">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="98910-218">Построение гистограммы суммы чаевых и ее зависимости от количества пассажиров и тарифа.</span><span class="sxs-lookup"><span data-stu-id="98910-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="98910-219">Используйте SQL-запрос для выборки данных.</span><span class="sxs-lookup"><span data-stu-id="98910-219">Use a SQL query to sample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST THE sqlContext
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped 
    FROM taxi_train 
    WHERE passenger_count > 0 
    AND passenger_count < 7 
    AND fare_amount > 0 
    AND fare_amount < 200 
    AND payment_type in ('CSH', 'CRD') 
    AND tip_amount > 0 
    AND tip_amount < 25


<span data-ttu-id="98910-220">В этой ячейке кода используется SQL-запрос для формирования трех видов графического представления данных.</span><span class="sxs-lookup"><span data-stu-id="98910-220">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


<span data-ttu-id="98910-221">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-221">**OUTPUT:**</span></span> 

![Распределение суммы чаевых](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Сумма чаевых в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Сумма чаевых в зависимости от тарифа](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="98910-225">Проектирование признаков, преобразование и подготовка данных к моделированию</span><span class="sxs-lookup"><span data-stu-id="98910-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="98910-226">В этом разделе приведен пример кода для выполнения процедур по подготовке данных, которые будут использоваться в моделях машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="98910-226">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="98910-227">Здесь также показано, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="98910-227">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="98910-228">создание нового признака путем группирования часов в периоды трафика;</span><span class="sxs-lookup"><span data-stu-id="98910-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="98910-229">индексация и кодирование категориальных признаков;</span><span class="sxs-lookup"><span data-stu-id="98910-229">Index and encode categorical features</span></span>
* <span data-ttu-id="98910-230">создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения;</span><span class="sxs-lookup"><span data-stu-id="98910-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="98910-231">создание случайной вложенной выборки данных и ее разделение на наборы для обучения и тестирования;</span><span class="sxs-lookup"><span data-stu-id="98910-231">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="98910-232">масштабирование признаков;</span><span class="sxs-lookup"><span data-stu-id="98910-232">Feature scaling</span></span>
* <span data-ttu-id="98910-233">кэширование объектов в памяти.</span><span class="sxs-lookup"><span data-stu-id="98910-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="98910-234">создание нового признака путем группирования часов в периоды трафика;</span><span class="sxs-lookup"><span data-stu-id="98910-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="98910-235">В следующем коде показано, как создать признак путем группирования часов в периоды трафика, а затем кэшировать итоговый фрейм данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="98910-235">This code shows how to create a new feature by binning hours into traffic time buckets and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="98910-236">Если устойчивые распределенные наборы данных и фреймы данных используются постоянно, на их кэширование необходимо меньше времени.</span><span class="sxs-lookup"><span data-stu-id="98910-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="98910-237">В этом пошаговом руководстве процесс кэширования имеющихся данных выполняется в несколько этапов.</span><span class="sxs-lookup"><span data-stu-id="98910-237">Accordingly, we cache RDDs and data-frames at several stages in the walkthrough.</span></span> 

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # THE .COUNT() GOES THROUGH THE ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES THE COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="98910-238">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-238">**OUTPUT:**</span></span> 

<span data-ttu-id="98910-239">126 050.</span><span class="sxs-lookup"><span data-stu-id="98910-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="98910-240">Индексация и кодирование категориальных признаков в качестве ввода для функций моделирования</span><span class="sxs-lookup"><span data-stu-id="98910-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="98910-241">В этом разделе показано, как индексировать и кодировать категориальные признаки в качестве ввода для функций моделирования.</span><span class="sxs-lookup"><span data-stu-id="98910-241">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="98910-242">Перед использованием в функциях моделирования и прогнозирования MLlib категориальные входные данные сначала необходимо проиндексировать или закодировать.</span><span class="sxs-lookup"><span data-stu-id="98910-242">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="98910-243">В зависимости от модели этот процесс происходит по-разному.</span><span class="sxs-lookup"><span data-stu-id="98910-243">Depending on the model, you need to index or encode them in different ways:</span></span>  

* <span data-ttu-id="98910-244">Для **моделирования на основе дерева** необходимо, чтобы категории были закодированы как числовые значения (например, признак с тремя категориями можно закодировать с помощью чисел 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="98910-244">**Tree-based modeling** requires categories to be encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="98910-245">Для этого можно использовать функцию [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) в MLlib.</span><span class="sxs-lookup"><span data-stu-id="98910-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="98910-246">С помощью этой функции столбец меток строкового типа кодируется как столбец с индексами меток, которые упорядочены по частоте меток.</span><span class="sxs-lookup"><span data-stu-id="98910-246">This function encodes a string column of labels to a column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="98910-247">Несмотря на то, что для данных задаются числовые индексы для ввода и дальнейшей обработки, в алгоритмах на основе дерева можно указать, что данные следует рассматривать как категории.</span><span class="sxs-lookup"><span data-stu-id="98910-247">Although indexed with numerical values for input and data handling, the tree-based algorithms can be specified to treat them appropriately as categories.</span></span> 
* <span data-ttu-id="98910-248">Для **моделей логистической и линейной регрессии** требуется прямое кодирование, при котором, например, признак с тремя категориями можно разделить на три столбца признаков, в каждом из которых в зависимости от категории наблюдения содержатся значения 0 или 1.</span><span class="sxs-lookup"><span data-stu-id="98910-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="98910-249">Для этого можно использовать функцию [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) в MLlib.</span><span class="sxs-lookup"><span data-stu-id="98910-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="98910-250">Этот кодировщик сопоставляет столбец с индексами меток со столбцом двоичных векторов как минимум с одним отдельным значением.</span><span class="sxs-lookup"><span data-stu-id="98910-250">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="98910-251">Благодаря этой кодировке алгоритмы, для которых необходимы признаки с числовыми значениями (например, логистическая регрессия), можно применять к категориальным признакам.</span><span class="sxs-lookup"><span data-stu-id="98910-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="98910-252">Ниже приведен пример кода, с помощью которого можно проиндексировать и закодировать категориальные признаки.</span><span class="sxs-lookup"><span data-stu-id="98910-252">Here is the code to index and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is the cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="98910-253">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-253">**OUTPUT:**</span></span>

<span data-ttu-id="98910-254">Время на выполнение кода выше: 1,28 с.</span><span class="sxs-lookup"><span data-stu-id="98910-254">Time taken to execute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="98910-255">Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения</span><span class="sxs-lookup"><span data-stu-id="98910-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="98910-256">В этом разделе содержится код, с помощью которого можно индексировать категориальные текстовые данные в тип данных с помеченной вершиной, а затем закодировать их. После этого данные можно использовать для обучения и проверки модели логистической регрессии MLlib и других моделей классификации.</span><span class="sxs-lookup"><span data-stu-id="98910-256">This section contains code that shows how to index categorical text data as a labeled point data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="98910-257">Объекты с помеченной вершиной отформатированы в устойчивые распределенные наборы данных, которые можно использовать в качестве входных для большинства алгоритмов машинного обучения в MLlib.</span><span class="sxs-lookup"><span data-stu-id="98910-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="98910-258">Объект [с помеченной вершиной](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) — это разреженный или плотный локальный вектор, связанный с меткой или ответом.</span><span class="sxs-lookup"><span data-stu-id="98910-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="98910-259">В этом разделе содержится код, с помощью которого можно индексировать категориальные текстовые данные в тип данных [с помеченной вершиной](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point), а затем закодировать их. После этого данные можно использовать для обучения и проверки модели логистической регрессии MLlib и других моделей классификации.</span><span class="sxs-lookup"><span data-stu-id="98910-259">This section contains code that shows how to index categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="98910-260">Объекты с помеченной вершиной — это устойчивые распределенные наборы данных, состоящие из метки (переменной ответа или целевой переменной) и вектора признаков.</span><span class="sxs-lookup"><span data-stu-id="98910-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="98910-261">Данные в таком формате используются в качестве входных для алгоритмов машинного обучения в MLlib.</span><span class="sxs-lookup"><span data-stu-id="98910-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="98910-262">Ниже приведен пример кода, с помощью которого можно проиндексировать и закодировать текстовые характеристики бинарной классификации.</span><span class="sxs-lookup"><span data-stu-id="98910-262">Here is the code to index and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="98910-263">Ниже приведен пример кода, с помощью которого можно проиндексировать и закодировать категориальные текстовые характеристики для анализа линейной регрессии.</span><span class="sxs-lookup"><span data-stu-id="98910-263">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])

        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="98910-264">Создание случайной вложенной выборки данных и ее разделение на наборы для обучения и тестирования</span><span class="sxs-lookup"><span data-stu-id="98910-264">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="98910-265">С помощью кода в этом разделе создается случайная выборка данных (25 % всех данных).</span><span class="sxs-lookup"><span data-stu-id="98910-265">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="98910-266">Несмотря на то, что из-за небольшого размера используемого набора данных, этот шаг выполнять необязательно, мы все равно покажем, как создавать выборку. Это поможет вам в случае возникновения проблем.</span><span class="sxs-lookup"><span data-stu-id="98910-266">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample here so you know how to use it for your own problem when needed.</span></span> <span data-ttu-id="98910-267">Если выборки большие, этот процесс может значительно сэкономить время обучения моделей.</span><span class="sxs-lookup"><span data-stu-id="98910-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="98910-268">Затем мы разобьем выборку данных на наборы для обучения (75 %) и тестирования (25 %), которые будут использоваться для двоичной классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="98910-268">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="98910-269">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-269">**OUTPUT:**</span></span>

<span data-ttu-id="98910-270">Время на выполнение кода выше: 0,24 с.</span><span class="sxs-lookup"><span data-stu-id="98910-270">Time taken to execute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="98910-271">масштабирование признаков;</span><span class="sxs-lookup"><span data-stu-id="98910-271">Feature scaling</span></span>
<span data-ttu-id="98910-272">Масштабирование признаков (или нормализация данных) гарантирует, что для признаков с широко распределенными значениями не задано высокое значение веса в целевой функции.</span><span class="sxs-lookup"><span data-stu-id="98910-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="98910-273">В коде для масштабирования признаков используется функция [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler), которая позволяет масштабировать признаки в зависимости от изменений единицы.</span><span class="sxs-lookup"><span data-stu-id="98910-273">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="98910-274">MLlib предоставляет функцию StandardScaler для выполнения линейной регрессии с применением метода стохастического градиента. Этот алгоритм широко используется для обучения других моделей машинного обучения (например, регуляризованной регрессии или метода опорных векторов).</span><span class="sxs-lookup"><span data-stu-id="98910-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="98910-275">Алгоритм LinearRegressionWithSGD чувствителен к масштабированию признаков.</span><span class="sxs-lookup"><span data-stu-id="98910-275">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>
> 
> 

<span data-ttu-id="98910-276">Ниже приведен код для масштабирования переменных, пригодный для использования с регуляризованным линейным алгоритмом с применением стохастического градиента.</span><span class="sxs-lookup"><span data-stu-id="98910-276">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

    # FEATURE SCALING

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="98910-277">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-277">**OUTPUT:**</span></span>

<span data-ttu-id="98910-278">Время на выполнение кода выше: 13,17 с.</span><span class="sxs-lookup"><span data-stu-id="98910-278">Time taken to execute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="98910-279">кэширование объектов в памяти.</span><span class="sxs-lookup"><span data-stu-id="98910-279">Cache objects in memory</span></span>
<span data-ttu-id="98910-280">Время на обучение и тестирование алгоритмов машинного обучения можно сократить, кэшировав объекты входного фрейма данных, которые использовались в качестве масштабируемых признаков, а также признаков для классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="98910-280">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression, and scaled features.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="98910-281">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-281">**OUTPUT:**</span></span> 

<span data-ttu-id="98910-282">Время на выполнение кода выше: 0,15 с.</span><span class="sxs-lookup"><span data-stu-id="98910-282">Time taken to execute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="98910-283">Прогнозирование вероятности выплаты чаевых за поездку с помощью моделей бинарной классификации</span><span class="sxs-lookup"><span data-stu-id="98910-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="98910-284">В этом разделе показано, как с помощью трех моделей для выполнения задач двоичной классификации спрогнозировать, будут ли оставлены чаевые за поездку в такси.</span><span class="sxs-lookup"><span data-stu-id="98910-284">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="98910-285">Мы используем следующие модели:</span><span class="sxs-lookup"><span data-stu-id="98910-285">The models presented are:</span></span>

* <span data-ttu-id="98910-286">регуляризованная логистическая регрессия;</span><span class="sxs-lookup"><span data-stu-id="98910-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="98910-287">модель случайного леса;</span><span class="sxs-lookup"><span data-stu-id="98910-287">Random forest model</span></span>
* <span data-ttu-id="98910-288">градиентный бустинг деревьев.</span><span class="sxs-lookup"><span data-stu-id="98910-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="98910-289">Процесс создания модели состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="98910-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="98910-290">**Обучение модели** с использованием данных с одним набором параметров.</span><span class="sxs-lookup"><span data-stu-id="98910-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="98910-291">**Оценка модели** на основе набора тестовых данных с метриками.</span><span class="sxs-lookup"><span data-stu-id="98910-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="98910-292">**Сохранение модели** в большом двоичном объекте для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="98910-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="98910-293">Классификация с применением логистической регрессии</span><span class="sxs-lookup"><span data-stu-id="98910-293">Classification using logistic regression</span></span>
<span data-ttu-id="98910-294">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения модели логистической регрессии с применением [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , с помощью которой можно спрогнозировать, будут ли выплачены чаевые за поездку в такси по Нью-Йорку, на основе набора данных и тарифов.</span><span class="sxs-lookup"><span data-stu-id="98910-294">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="98910-295">**Обучение модели логистической регрессии с использованием перекрестной проверки и перебора параметров**</span><span class="sxs-lookup"><span data-stu-id="98910-295">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="98910-296">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-296">**OUTPUT:**</span></span> 

<span data-ttu-id="98910-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="98910-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="98910-298">Intercept: -0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="98910-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="98910-299">Время на выполнение кода выше: 14,43 с.</span><span class="sxs-lookup"><span data-stu-id="98910-299">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="98910-300">**Оценка модели бинарной классификации со стандартными метриками**</span><span class="sxs-lookup"><span data-stu-id="98910-300">**Evaluate the binary classification model with standard metrics**</span></span>

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="98910-301">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-301">**OUTPUT:**</span></span> 

<span data-ttu-id="98910-302">Area under PR = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="98910-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="98910-303">Area under ROC = 0.983714670256</span><span class="sxs-lookup"><span data-stu-id="98910-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="98910-304">Summary Stats</span><span class="sxs-lookup"><span data-stu-id="98910-304">Summary Stats</span></span>

<span data-ttu-id="98910-305">Precision = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="98910-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="98910-306">Recall = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="98910-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="98910-307">F1 Score = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="98910-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="98910-308">Время на выполнение кода выше: 57,61 с.</span><span class="sxs-lookup"><span data-stu-id="98910-308">Time taken to execute above cell: 57.61 seconds</span></span>

<span data-ttu-id="98910-309">**Графическое представление кривой ROC.**</span><span class="sxs-lookup"><span data-stu-id="98910-309">**Plot the ROC curve.**</span></span>

<span data-ttu-id="98910-310">*predictionAndLabelsDF* регистрируется как таблица (*tmp_results*) в предыдущей ячейке.</span><span class="sxs-lookup"><span data-stu-id="98910-310">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="98910-311">*tmp_results* может использоваться для выполнения запросов и вывода результатов во фрейм данных sqlResults для построения диаграммы.</span><span class="sxs-lookup"><span data-stu-id="98910-311">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="98910-312">Ниже приведен код:</span><span class="sxs-lookup"><span data-stu-id="98910-312">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="98910-313">Ниже приведен код для создания прогнозов и отображения кривой ROC.</span><span class="sxs-lookup"><span data-stu-id="98910-313">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


<span data-ttu-id="98910-314">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-314">**OUTPUT:**</span></span>

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="98910-316">Классификация случайного леса</span><span class="sxs-lookup"><span data-stu-id="98910-316">Random forest classification</span></span>
<span data-ttu-id="98910-317">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения модели случайного леса, с помощью которой на основе набора данных о поездках и тарифах по Нью-Йорку можно спрогнозировать, оставит ли пассажир чаевые за поездку в такси.</span><span class="sxs-lookup"><span data-stu-id="98910-317">The code in this section shows how to train, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT TO PRINT TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="98910-318">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-318">**OUTPUT:**</span></span>

<span data-ttu-id="98910-319">Area under ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="98910-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="98910-320">Время на выполнение кода выше: 31,09 с.</span><span class="sxs-lookup"><span data-stu-id="98910-320">Time taken to execute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="98910-321">Классификация с применением модели градиентного бустинга деревьев</span><span class="sxs-lookup"><span data-stu-id="98910-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="98910-322">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения модели градиентного бустинга деревьев, с помощью которой можно спрогнозировать, будут ли выплачены чаевые за поездку в такси по Нью-Йорку, на основе набора данных и тарифов.</span><span class="sxs-lookup"><span data-stu-id="98910-322">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="98910-323">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-323">**OUTPUT:**</span></span>

<span data-ttu-id="98910-324">Area under ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="98910-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="98910-325">Время на выполнение кода выше: 19,76 с.</span><span class="sxs-lookup"><span data-stu-id="98910-325">Time taken to execute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="98910-326">Прогнозирование суммы чаевых за поездку в такси с помощью моделей регрессии</span><span class="sxs-lookup"><span data-stu-id="98910-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="98910-327">В этом разделе показано, как с помощью трех моделей регрессии спрогнозировать сумму чаевых в зависимости от других признаков.</span><span class="sxs-lookup"><span data-stu-id="98910-327">This section shows how use three models for the regression task of predicting the amount of the tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="98910-328">Мы используем следующие модели:</span><span class="sxs-lookup"><span data-stu-id="98910-328">The models presented are:</span></span>

* <span data-ttu-id="98910-329">регуляризованная линейная регрессия;</span><span class="sxs-lookup"><span data-stu-id="98910-329">Regularized linear regression</span></span>
* <span data-ttu-id="98910-330">случайный лес;</span><span class="sxs-lookup"><span data-stu-id="98910-330">Random forest</span></span>
* <span data-ttu-id="98910-331">градиентный бустинг деревьев.</span><span class="sxs-lookup"><span data-stu-id="98910-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="98910-332">Эти модели описаны в начале статьи.</span><span class="sxs-lookup"><span data-stu-id="98910-332">These models were described in the introduction.</span></span> <span data-ttu-id="98910-333">Процесс создания модели состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="98910-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="98910-334">**Обучение модели** с использованием данных с одним набором параметров.</span><span class="sxs-lookup"><span data-stu-id="98910-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="98910-335">**Оценка модели** на основе набора тестовых данных с метриками.</span><span class="sxs-lookup"><span data-stu-id="98910-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="98910-336">**Сохранение модели** в большом двоичном объекте для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="98910-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="98910-337">Линейная регрессия с применением SGD</span><span class="sxs-lookup"><span data-stu-id="98910-337">Linear regression with SGD</span></span>
<span data-ttu-id="98910-338">С помощью кода, приведенного в этом разделе, на основе масштабируемых признаков можно обучить модель линейной регрессии, в которой для оптимизации используется метод стохастического градиента, а также оценить, проанализировать и сохранить ее в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="98910-338">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="98910-339">На практике в моделях LinearRegressionWithSGD часто возникают проблемы с конвергенцией. Чтобы получить допустимую модель, необходимо осторожно изменить или оптимизировать параметры.</span><span class="sxs-lookup"><span data-stu-id="98910-339">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="98910-340">Проблему конвергенции можно решить, выполнив масштабирование переменных.</span><span class="sxs-lookup"><span data-stu-id="98910-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES TO TRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN THE DEFAULT BLOB FOR THE CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="98910-341">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-341">**OUTPUT:**</span></span>

<span data-ttu-id="98910-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="98910-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="98910-343">Intercept: 0.853872718283</span><span class="sxs-lookup"><span data-stu-id="98910-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="98910-344">RMSE = 1.24190115863</span><span class="sxs-lookup"><span data-stu-id="98910-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="98910-345">R-sqr = 0.608017146081</span><span class="sxs-lookup"><span data-stu-id="98910-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="98910-346">Время на выполнение кода выше: 58,42 с.</span><span class="sxs-lookup"><span data-stu-id="98910-346">Time taken to execute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="98910-347">Регрессия с использованием модели случайного леса</span><span class="sxs-lookup"><span data-stu-id="98910-347">Random Forest regression</span></span>
<span data-ttu-id="98910-348">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения регрессии случайного леса, с помощью которой можно спрогнозировать суму чаевых за поездку в такси по Нью-Йорку.</span><span class="sxs-lookup"><span data-stu-id="98910-348">The code in this section shows how to train, evaluate, and save a random forest regression that predicts tip amount for the NYC taxi trip data.</span></span>

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT TO PRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="98910-349">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-349">**OUTPUT:**</span></span>

<span data-ttu-id="98910-350">RMSE = 0.891209218139</span><span class="sxs-lookup"><span data-stu-id="98910-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="98910-351">R-sqr = 0.759661334921</span><span class="sxs-lookup"><span data-stu-id="98910-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="98910-352">Время на выполнение кода выше: 49,21 с.</span><span class="sxs-lookup"><span data-stu-id="98910-352">Time taken to execute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="98910-353">Регрессия с применением градиентного бустинга деревьев</span><span class="sxs-lookup"><span data-stu-id="98910-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="98910-354">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения модели градиентного бустинга деревьев, с помощью которой можно спрогнозировать суму чаевых за поездку в такси по Нью-Йорку.</span><span class="sxs-lookup"><span data-stu-id="98910-354">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="98910-355">** Обучать и оценивать **</span><span class="sxs-lookup"><span data-stu-id="98910-355">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS TO DF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="98910-356">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-356">**OUTPUT:**</span></span>

<span data-ttu-id="98910-357">RMSE = 0.908473148639</span><span class="sxs-lookup"><span data-stu-id="98910-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="98910-358">R-sqr = 0.753835096681</span><span class="sxs-lookup"><span data-stu-id="98910-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="98910-359">Время на выполнение кода выше: 34,52 с.</span><span class="sxs-lookup"><span data-stu-id="98910-359">Time taken to execute above cell: 34.52 seconds</span></span>

<span data-ttu-id="98910-360">**Графическое представления**</span><span class="sxs-lookup"><span data-stu-id="98910-360">**Plot**</span></span>

<span data-ttu-id="98910-361">*tmp_results* регистрируется как таблица Hive в предыдущей ячейке.</span><span class="sxs-lookup"><span data-stu-id="98910-361">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="98910-362">Результаты из таблицы передаются во фрейм данных *sqlResults* для формирования графического представления.</span><span class="sxs-lookup"><span data-stu-id="98910-362">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="98910-363">Ниже приведен код:</span><span class="sxs-lookup"><span data-stu-id="98910-363">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="98910-364">Ниже приведен код для формирования графического представления данных с использованием сервера Jupyter.</span><span class="sxs-lookup"><span data-stu-id="98910-364">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


<span data-ttu-id="98910-365">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="98910-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="98910-367">Очистка объектов из памяти</span><span class="sxs-lookup"><span data-stu-id="98910-367">Clean up objects from memory</span></span>
<span data-ttu-id="98910-368">Удалите объекты, кэшированные в памяти, с помощью метода `unpersist()` .</span><span class="sxs-lookup"><span data-stu-id="98910-368">Use `unpersist()` to delete objects cached in memory.</span></span>

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


## <a name="record-storage-locations-of-the-models-for-consumption-and-scoring"></a><span data-ttu-id="98910-369">Запись места хранения моделей для дальнейшего использования и оценки</span><span class="sxs-lookup"><span data-stu-id="98910-369">Record storage locations of the models for consumption and scoring</span></span>
<span data-ttu-id="98910-370">Чтобы использовать и оценивать независимые наборы данных, описанные в разделе [Оценка моделей машинного обучения, созданных с помощью Spark](machine-learning-data-science-spark-model-consumption.md), необходимо скопировать и вставить в записную книжку Jupyter Consumption имена файлов с сохраненными моделями, созданными с помощью инструкций из этой статьи.</span><span class="sxs-lookup"><span data-stu-id="98910-370">To consume and score an independent dataset described in the [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need to copy and paste these file names containing the saved models created here into the Consumption Jupyter notebook.</span></span> <span data-ttu-id="98910-371">Ниже приведен код для вывода путей к необходимым файлам моделей.</span><span class="sxs-lookup"><span data-stu-id="98910-371">Here is the code to print out the paths to model files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="98910-372">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="98910-372">**OUTPUT**</span></span>

<span data-ttu-id="98910-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="98910-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="98910-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="98910-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="98910-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="98910-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="98910-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="98910-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="98910-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="98910-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="98910-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="98910-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="98910-379">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="98910-379">What's next?</span></span>
<span data-ttu-id="98910-380">После создания моделей регрессии и классификации с помощью Spark MlLib необходимо ознакомиться с процессом оценки и анализа этих моделей.</span><span class="sxs-lookup"><span data-stu-id="98910-380">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span> <span data-ttu-id="98910-381">С помощью записной книжки по расширенному исследованию и моделированию данных можно более подробно ознакомиться с тем, как использовать перекрестную проверку, очистку гиперпараметров и оценку модели.</span><span class="sxs-lookup"><span data-stu-id="98910-381">The advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="98910-382">**Использование модели**. Дополнительные сведения об оценке и анализе моделей классификации и регрессии, созданных в этой статье см. в статье [Оценка моделей машинного обучения, созданных с помощью Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="98910-382">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="98910-383">**Перекрестная проверка и перебор гиперпараметров**. Сведения об обучении моделей с помощью перекрестной проверки и перебора гиперпараметров см. в статье [Расширенное исследование и моделирование данных с помощью Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md).</span><span class="sxs-lookup"><span data-stu-id="98910-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

