---
title: "aaaData исследования и моделирования с Spark | Документы Microsoft"
description: "Демонстрирует hello возможности набора средств hello Spark MLlib на Azure моделирования и просмотра данных."
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
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="22246-103">Исследование и моделирование данных с помощью Spark</span><span class="sxs-lookup"><span data-stu-id="22246-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="22246-104">В этом пошаговом руководстве использует просмотр данных toodo HDInsight Spark и двоичной классификации и регрессии задачи моделирования образца hello NYC такси маршрута и успешного 2013 набора данных.</span><span class="sxs-lookup"><span data-stu-id="22246-104">This walkthrough uses HDInsight Spark toodo data exploration and binary classification and regression modeling tasks on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="22246-105">Он поможет выполнить шаги hello hello [процесса обработки и анализа данных](http://aka.ms/datascienceprocess), узел узел, с помощью HDInsight Spark кластера для обработки и модели данных и hello hello toostore больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="22246-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="22246-106">Hello процесс более подробно рассматривается и визуализация данных из большого двоичного объекта хранилища Azure и затем выполняется подготовка данных toobuild hello прогнозных моделей.</span><span class="sxs-lookup"><span data-stu-id="22246-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="22246-107">Эти модели, с помощью hello Spark MLlib toolkit toodo двоичной классификации и регрессии моделирования задачи построения.</span><span class="sxs-lookup"><span data-stu-id="22246-107">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="22246-108">Hello **двоичной классификации** задача — toopredict ли совет оплачивается поездки hello.</span><span class="sxs-lookup"><span data-stu-id="22246-108">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="22246-109">Hello **регрессии** задача представляет сумму hello toopredict hello подсказки на основе других функций подсказки.</span><span class="sxs-lookup"><span data-stu-id="22246-109">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="22246-110">модели Hello, мы используем включают логистической и линейной регрессии, случайные леса и градиента повышенных деревьев:</span><span class="sxs-lookup"><span data-stu-id="22246-110">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="22246-111">[Линейная регрессия с SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) модель линейной регрессии, которая использует метод вероятностный градиентный спуск (SGD) и для оптимизации и возможность масштабирования toopredict hello совет суммы оплаты.</span><span class="sxs-lookup"><span data-stu-id="22246-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="22246-112">[Логистическая Регрессия с LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) и регрессии «logit» представляет собой модель регрессии, который может использоваться при классификации данных категориальные toodo hello зависимой переменной.</span><span class="sxs-lookup"><span data-stu-id="22246-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="22246-113">LBFGS-это алгоритм оптимизации реализация ньютон, соответствующий алгоритм Бройдена-Флетчера-Гольдфарба-Шанно (BFGS) hello ограниченный объем памяти компьютера с помощью и широко используемый в машинном обучении.</span><span class="sxs-lookup"><span data-stu-id="22246-113">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="22246-114">[Случайные леса](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="22246-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="22246-115">Они объединяют многих решений деревьев tooreduce hello риск переобучения.</span><span class="sxs-lookup"><span data-stu-id="22246-115">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="22246-116">Случайные леса, используются для классификации и регрессии и может обрабатывать категориальных признаков и могут быть расширены параметр toohello мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="22246-116">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="22246-117">Они не требуется возможность масштабирования и являются может toocapture нелинейности и возможность взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="22246-117">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="22246-118">Случайные леса принадлежат hello наиболее успешных моделей машинного обучения для классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="22246-118">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="22246-119">[Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="22246-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="22246-120">Решение GBTs обучение итеративного дерева toominimize функции потерь.</span><span class="sxs-lookup"><span data-stu-id="22246-120">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="22246-121">GBTs используются для классификации и регрессии и может обрабатывать категориальных признаков не требуется возможность масштабирования и являются может toocapture нелинейности и возможностей взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="22246-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="22246-122">Кроме того, его можно использовать для создания модели мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="22246-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="22246-123">Hello моделирования действия также содержат код, показывающий, как tootrain, оценки и сохранение каждого типа модели.</span><span class="sxs-lookup"><span data-stu-id="22246-123">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="22246-124">Python был используется toocode hello решения и tooshow hello соответствующие графики.</span><span class="sxs-lookup"><span data-stu-id="22246-124">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="22246-125">Хотя набор средств Spark MLlib hello спроектированный toowork с большими наборами данных, сравнительно небольшую выборку (с помощью 170 тысяч строк, 0,1% hello исходный набор данных NYC ~ 30 МБ) используется здесь для удобства.</span><span class="sxs-lookup"><span data-stu-id="22246-125">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="22246-126">Упражнение Hello в данном разделе выполняется эффективно (в течение 10 минут) в кластере HDInsight с 2 рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="22246-126">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="22246-127">Hello одинаковый код, с небольшими изменениями может быть используется tooprocess более крупных-наборов данных, с соответствующими изменениями для кэширования данных в памяти и изменение размера кластера hello.</span><span class="sxs-lookup"><span data-stu-id="22246-127">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="22246-128">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="22246-128">Prerequisites</span></span>
<span data-ttu-id="22246-129">Вам потребуется учетная запись Azure и Spark 1.6 (или Spark 2.0) кластер HDInsight toocomplete в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="22246-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="22246-130">В разделе hello [Обзор для обработки и анализа данных с помощью Spark на Azure HDInsight](machine-learning-data-science-spark-overview.md) инструкции о том, как toosatisfy эти требования.</span><span class="sxs-lookup"><span data-stu-id="22246-130">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="22246-131">Этот раздел также содержит описание hello такси 2013 NYC данные, используемые здесь и инструкции о том, как код tooexecute из записной книжке Jupyter на кластере Spark hello.</span><span class="sxs-lookup"><span data-stu-id="22246-131">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="22246-132">Кластеры и записные книжки Spark</span><span class="sxs-lookup"><span data-stu-id="22246-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="22246-133">Действия по настройке и код, указанные в этом пошаговом руководстве, применимы к использованию для HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="22246-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="22246-134">Но записные книжки Jupyter можно использовать для кластеров HDInsight Spark 1.6 и Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="22246-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="22246-135">Описание toothem hello записных книжек и ссылки, представлено в hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) для репозитория GitHub hello, содержащий их.</span><span class="sxs-lookup"><span data-stu-id="22246-135">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="22246-136">Кроме того код hello здесь и в записных книжках hello связаны является универсальным и должен работать на любой кластер Spark.</span><span class="sxs-lookup"><span data-stu-id="22246-136">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="22246-137">Если вы не используете HDInsight Spark, настройку и управление ими действия hello кластера может быть немного отличается от показанной здесь.</span><span class="sxs-lookup"><span data-stu-id="22246-137">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="22246-138">Для удобства ниже приведены hello ссылки записные книжки Jupyter toohello для 1.6 Spark (выполняются в ядро pySpark hello hello server книжке Jupyter toobe) и 2.0 Spark (toobe запуска ядра pySpark3 hello объекта hello книжке Jupyter сервера).</span><span class="sxs-lookup"><span data-stu-id="22246-138">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 (toobe run in hello pySpark kernel of hello Jupyter Notebook server) and  Spark 2.0 (toobe run in hello pySpark3 kernel of hello Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="22246-139">Записные книжки для Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="22246-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="22246-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): содержит сведения о том, как просмотр данных tooperform, моделирование и оценка с несколько разных алгоритмов.</span><span class="sxs-lookup"><span data-stu-id="22246-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how tooperform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="22246-141">Записные книжки для Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="22246-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="22246-142">Hello регрессии и классификации задачи, которые реализуются с помощью кластера Spark 2.0 находятся в отдельном записных книжек и записной книжки hello классификации используются различные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="22246-142">hello regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and hello classification notebook uses a different data set:</span></span>

- <span data-ttu-id="22246-143">[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): этот файл содержит сведения о как tooperform Просмотр данных, моделирования и оценки в Spark 2.0 кластеры, использующие hello trip такси NYC и набор данных тариф авиакомпании, описано [здесь](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="22246-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="22246-144">Записной книжки может быть хорошей отправной точкой для быстрого исследования кода hello, предоставленные для Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="22246-144">This notebook may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> <span data-ttu-id="22246-145">Для подробных записной книжки анализирует hello такси NYC данных, см. Далее записной книжки hello в этом списке.</span><span class="sxs-lookup"><span data-stu-id="22246-145">For a more detailed notebook analyzes hello NYC Taxi data, see hello next notebook in this list.</span></span> <span data-ttu-id="22246-146">См. примечания hello ниже, сравнивающие эти портативные компьютеры.</span><span class="sxs-lookup"><span data-stu-id="22246-146">See hello notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="22246-147">[Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): этот файл показывает, как tooperform данные wrangling (Spark SQL и кадр данных операции), просмотр, моделирование и оценка с помощью hello trip такси NYC и тариф авиакомпании набор данных описывается [ Здесь](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="22246-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="22246-148">[Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): этот файл показывает, как tooperform данные wrangling (Spark SQL и кадр данных операции), просмотр, моделирование и оценка с помощью hello хорошо известных авиакомпании на время отправления набор данных на основе 2011 г. и 2012.</span><span class="sxs-lookup"><span data-stu-id="22246-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="22246-149">Мы интегрировать dataset авиакомпании hello hello аэропорта погоды данных (например, windspeed, температуры, высота над уровнем моря т. д.) предыдущих toomodeling, эти функции погоды могут быть включены в модель hello.</span><span class="sxs-lookup"><span data-stu-id="22246-149">We integrated hello airline dataset with hello airport weather data (e.g. windspeed, temperature, altitude etc.) prior toomodeling, so these weather features can be included in hello model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="22246-150">набор данных авиакомпании Hello был добавлен toohello Spark 2.0 записных книжек toobetter иллюстрируют использование hello алгоритмы классификации.</span><span class="sxs-lookup"><span data-stu-id="22246-150">hello airline dataset was added toohello Spark 2.0 notebooks toobetter illustrate hello use of classification algorithms.</span></span> <span data-ttu-id="22246-151">См. следующие ссылки на сведения о набора данных на время отправления авиакомпании и набора данных погоды hello.</span><span class="sxs-lookup"><span data-stu-id="22246-151">See hello following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="22246-152">Данные о расписании вылетов авиакомпании: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="22246-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="22246-153">Данные о погоде в аэропортах: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="22246-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="22246-154">записных книжек Spark 2.0 Hello на такси NYC hello и наборы авиакомпании рейса задержка данных может занять 10 минут или более toorun (в зависимости от размера hello кластер HDI).</span><span class="sxs-lookup"><span data-stu-id="22246-154">hello Spark 2.0 notebooks on hello NYC taxi and airline flight delay data-sets can take 10 mins or more toorun (depending on hello size of your HDI cluster).</span></span> <span data-ttu-id="22246-155">Hello первой записной книжки в hello над списком показаны различные аспекты hello исследования данных, визуализации и машинного Обучения моделей обучения в записной книжке, занимает меньше времени toorun уменьшается NYC набора данных, в которой hello такси и тариф авиакомпании файлы были предварительно присоединены к домену: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) записной книжки принимает более короткое время toofinish (2-3 минуты) и может быть это хорошая отправная точка для быстро анализ кода hello у нас есть обеспечивает Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="22246-155">hello first notebook in hello above list shows many aspects of hello data exploration, visualization and ML model training in a notebook that takes less time toorun with down-sampled NYC data set, in which hello taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time toofinish (2-3 mins) and may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="22246-156">Hello ниже описаны связанные toousing Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="22246-156">hello descriptions below are related toousing Spark 1.6.</span></span> <span data-ttu-id="22246-157">Для версий Spark 2.0 используйте записных книжек hello описаны и ссылки выше.</span><span class="sxs-lookup"><span data-stu-id="22246-157">For Spark 2.0 versions, please use hello notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="22246-158">Программа установки: hello, библиотеки и расположения хранилища конфигурации Spark контекста</span><span class="sxs-lookup"><span data-stu-id="22246-158">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="22246-159">Spark — может tooAzure tooread и записи хранилища больших двоичных объектов (также известный как WASB).</span><span class="sxs-lookup"><span data-stu-id="22246-159">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="22246-160">Поэтому любые существующие данные, хранящиеся в ней могут быть обработаны с помощью Spark и hello результаты хранимых в WASB.</span><span class="sxs-lookup"><span data-stu-id="22246-160">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="22246-161">toosave модели или файлов в WASB, hello путь должен toobe указано правильно.</span><span class="sxs-lookup"><span data-stu-id="22246-161">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="22246-162">Hello кластера Spark toohello присоединенного контейнера по умолчанию можно обращаться, используя путь, начиная с: «wasb: / / /».</span><span class="sxs-lookup"><span data-stu-id="22246-162">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="22246-163">Другие расположения начинаются с wasb://.</span><span class="sxs-lookup"><span data-stu-id="22246-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="22246-164">Настройка путей каталога к месту хранения в хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="22246-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="22246-165">Hello следующий код задает hello место чтения toobe данных hello и hello hello модели хранения каталога toowhich hello модели выходных данных будет сохранен:</span><span class="sxs-lookup"><span data-stu-id="22246-165">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="22246-166">Импорт библиотек</span><span class="sxs-lookup"><span data-stu-id="22246-166">Import libraries</span></span>
<span data-ttu-id="22246-167">Для установки также требуется импорт необходимых библиотек.</span><span class="sxs-lookup"><span data-stu-id="22246-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="22246-168">Задать контекст spark и импортируйте необходимые библиотеки с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="22246-168">Set spark context and import necessary libraries with hello following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="22246-169">Предустановленный контекст Spark и волшебные команды PySpark</span><span class="sxs-lookup"><span data-stu-id="22246-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="22246-170">Hello PySpark ядер, предоставляемых с записные книжки Jupyter имеют предустановленных контекста.</span><span class="sxs-lookup"><span data-stu-id="22246-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="22246-171">Поэтому необязательно tooset hello Spark или куст контекстов явно перед началом работы с приложением hello, которое вы разрабатываете.</span><span class="sxs-lookup"><span data-stu-id="22246-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="22246-172">Эти контексты доступны вам по умолчанию,</span><span class="sxs-lookup"><span data-stu-id="22246-172">These contexts are available for you by default.</span></span> <span data-ttu-id="22246-173">а именно:</span><span class="sxs-lookup"><span data-stu-id="22246-173">These contexts are:</span></span>

* <span data-ttu-id="22246-174">sc для Spark;</span><span class="sxs-lookup"><span data-stu-id="22246-174">sc - for Spark</span></span> 
* <span data-ttu-id="22246-175">sqlContext для Hive.</span><span class="sxs-lookup"><span data-stu-id="22246-175">sqlContext - for Hive</span></span>

<span data-ttu-id="22246-176">Hello ядра PySpark предоставляет некоторые предопределенные «magics», которые являются специальные команды, которые можно вызвать с %%.</span><span class="sxs-lookup"><span data-stu-id="22246-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="22246-177">В этих примерах кода используются две подобные команды.</span><span class="sxs-lookup"><span data-stu-id="22246-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="22246-178">**%% локального** указывает, что код hello в последующих строках toobe выполняются локально.</span><span class="sxs-lookup"><span data-stu-id="22246-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="22246-179">В качестве кода должен быть указан корректный код Python.</span><span class="sxs-lookup"><span data-stu-id="22246-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="22246-180">**%% sql -o <variable name>**  выполняет запрос Hive в отношении hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="22246-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="22246-181">Если передается параметр -o hello, hello результат запроса hello сохраняется в hello %% локального контекста Python как Pandas кадр данных.</span><span class="sxs-lookup"><span data-stu-id="22246-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="22246-182">Для Дополнительные сведения о ядра hello записные книжки Jupyter и предопределенные hello «magics», они предоставляют, в разделе [кластеры ядер, доступных для записные книжки Jupyter с HDInsight Spark Linux в HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="22246-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="22246-183">Прием данных из открытого большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="22246-183">Data ingestion from public blob</span></span>
<span data-ttu-id="22246-184">Первым шагом процесса обработки и анализа данных hello Hello является tooingest hello данных toobe анализируются из источников где — находится в среде моделирования и просмотра данных.</span><span class="sxs-lookup"><span data-stu-id="22246-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="22246-185">Среда Hello — Spark в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="22246-185">hello environment is Spark in this walkthrough.</span></span> <span data-ttu-id="22246-186">Этот раздел содержит toocomplete кода hello последовательности задач:</span><span class="sxs-lookup"><span data-stu-id="22246-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="22246-187">hello данные примера toobe моделируется приема</span><span class="sxs-lookup"><span data-stu-id="22246-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="22246-188">чтение во входном наборе данных hello (хранятся в формате .tsv)</span><span class="sxs-lookup"><span data-stu-id="22246-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="22246-189">Очистить hello данные и формат</span><span class="sxs-lookup"><span data-stu-id="22246-189">format and clean hello data</span></span>
* <span data-ttu-id="22246-190">создание и кэширование объектов (устойчивых распределенных наборов данных или фреймов данных) в памяти;</span><span class="sxs-lookup"><span data-stu-id="22246-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="22246-191">регистрация данных в качестве временной таблицы в контексте SQL.</span><span class="sxs-lookup"><span data-stu-id="22246-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="22246-192">Ниже приведен код hello для приема данных.</span><span class="sxs-lookup"><span data-stu-id="22246-192">Here is hello code for data ingestion.</span></span>

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="22246-193">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-193">**OUTPUT:**</span></span>

<span data-ttu-id="22246-194">Время, затраченное tooexecute над ячейкой: 51.72 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-194">Time taken tooexecute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="22246-195">Исследование и визуализация данных</span><span class="sxs-lookup"><span data-stu-id="22246-195">Data exploration & visualization</span></span>
<span data-ttu-id="22246-196">Hello данных была помещена в Spark, hello следующим шагом в процессе обработки и анализа данных hello после toogain глубокого понимания hello данных через Просмотр и визуализация.</span><span class="sxs-lookup"><span data-stu-id="22246-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="22246-197">В этом разделе рассматриваются hello такси данные с помощью SQL-запросов построения hello целевой переменных и потенциальных возможностей для визуальной проверки.</span><span class="sxs-lookup"><span data-stu-id="22246-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="22246-198">В частности мы построения hello частоту пассажира счетчиков в такси приема-передачи, частота hello совет сумм и как изменять советы по типам и сумма платежа.</span><span class="sxs-lookup"><span data-stu-id="22246-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="22246-199">Построить гистограмму для частоты счетчика пассажира в образце hello такси приема-передачи данных</span><span class="sxs-lookup"><span data-stu-id="22246-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="22246-200">Этот код и последующие фрагменты использовать образец hello magic tooquery SQL и данных локального magic tooplot hello.</span><span class="sxs-lookup"><span data-stu-id="22246-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="22246-201">**Магическое SQL (`%%sql`)** hello ядра HDInsight PySpark поддерживает встроенные легко HiveQL запросы к hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="22246-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="22246-202">Hello (-o имя_переменной) аргумент hello выходных данных запроса SQL hello сохраняется как Pandas кадр данных на сервере Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="22246-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="22246-203">Это означает, что он доступен в локальном режиме hello.</span><span class="sxs-lookup"><span data-stu-id="22246-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="22246-204">Hello  **`%%local` магическое** — использовать код toorun локально на сервере Jupyter hello, где hello головному узлу кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="22246-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="22246-205">Как правило, используется `%%local` magic вместе с hello `%%sql` magic с параметром -o.</span><span class="sxs-lookup"><span data-stu-id="22246-205">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="22246-206">параметр -o Hello сохранится hello выходных данных запроса SQL hello локально и затем %% локального magic приведет к запуску hello следующего набора toorun фрагмент кода локально к выходным данным hello hello запросов SQL, в которой сохраняется локально</span><span class="sxs-lookup"><span data-stu-id="22246-206">hello -o parameter would persist hello output of hello SQL query locally and then %%local magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally</span></span>

<span data-ttu-id="22246-207">выходные данные Hello автоматически визуализируются после выполнения кода hello.</span><span class="sxs-lookup"><span data-stu-id="22246-207">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="22246-208">Этот запрос извлекает hello приема-передачи данных по количеству пассажира.</span><span class="sxs-lookup"><span data-stu-id="22246-208">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="22246-209">Этот код создает локальный кадров данных из результатов запроса hello и представлены данные hello.</span><span class="sxs-lookup"><span data-stu-id="22246-209">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="22246-210">Hello `%%local` magic создает локальный-кадра данных, `sqlResults`, который может использоваться для отображения на диаграмме с помощью matplotlib.</span><span class="sxs-lookup"><span data-stu-id="22246-210">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="22246-211">В этом пошаговом руководстве волшебная команда PySpark используется несколько раз.</span><span class="sxs-lookup"><span data-stu-id="22246-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="22246-212">При больших размерах hello объем данных следует образец toocreate кадра данных, помещающихся в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="22246-212">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="22246-213">Вот hello кода tooplot hello приема-передачи с пассажира счетчиков</span><span class="sxs-lookup"><span data-stu-id="22246-213">Here is hello code tooplot hello trips by passenger counts</span></span>

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

<span data-ttu-id="22246-214">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-214">**OUTPUT:**</span></span>

![Частота поездок в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="22246-216">Можно выбирать различные виды визуализаций (таблицы, круговая, строки, области или панели) с помощью hello **тип** кнопок меню в записной книжке hello.</span><span class="sxs-lookup"><span data-stu-id="22246-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="22246-217">Здесь показана панель построения Hello.</span><span class="sxs-lookup"><span data-stu-id="22246-217">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="22246-218">Построение гистограммы суммы чаевых и ее зависимости от количества пассажиров и тарифа.</span><span class="sxs-lookup"><span data-stu-id="22246-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="22246-219">Используйте toosample данных запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="22246-219">Use a SQL query toosample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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


<span data-ttu-id="22246-220">Эта ячейка код использует данные о hello hello SQL запроса toocreate три графики.</span><span class="sxs-lookup"><span data-stu-id="22246-220">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
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


<span data-ttu-id="22246-221">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-221">**OUTPUT:**</span></span> 

![Распределение суммы чаевых](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Сумма чаевых в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Сумма чаевых в зависимости от тарифа](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="22246-225">Проектирование признаков, преобразование и подготовка данных к моделированию</span><span class="sxs-lookup"><span data-stu-id="22246-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="22246-226">В этом разделе описывается и предоставляет кода hello для процедур, используемых tooprepare данных для использования в модели машинного Обучения.</span><span class="sxs-lookup"><span data-stu-id="22246-226">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="22246-227">Здесь показано, как hello toodo следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="22246-227">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="22246-228">Создание нового признака путем группирования часов в периоды трафика</span><span class="sxs-lookup"><span data-stu-id="22246-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="22246-229">индексация и кодирование категориальных признаков;</span><span class="sxs-lookup"><span data-stu-id="22246-229">Index and encode categorical features</span></span>
* <span data-ttu-id="22246-230">Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения</span><span class="sxs-lookup"><span data-stu-id="22246-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="22246-231">Создание вложенных случайной выборки данных hello и разбейте его на обучающий и проверочный наборы</span><span class="sxs-lookup"><span data-stu-id="22246-231">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="22246-232">масштабирование признаков;</span><span class="sxs-lookup"><span data-stu-id="22246-232">Feature scaling</span></span>
* <span data-ttu-id="22246-233">кэширование объектов в памяти.</span><span class="sxs-lookup"><span data-stu-id="22246-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="22246-234">Создание нового признака путем группирования часов в периоды трафика</span><span class="sxs-lookup"><span data-stu-id="22246-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="22246-235">Этот код показывает, как toocreate новая функция путем сегментирования часов в момент трафик контейнеров, а затем как toocache hello результирующий кадр данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="22246-235">This code shows how toocreate a new feature by binning hours into traffic time buckets and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="22246-236">Где устойчивым распределенных наборы данных (RDDs) и кадров данных используются многократно, кэширование приводит tooimproved времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="22246-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="22246-237">Соответственно, мы RDDs и кэш кадров данных на несколько этапов в пошаговом руководстве hello.</span><span class="sxs-lookup"><span data-stu-id="22246-237">Accordingly, we cache RDDs and data-frames at several stages in hello walkthrough.</span></span> 

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
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="22246-238">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-238">**OUTPUT:**</span></span> 

<span data-ttu-id="22246-239">126 050.</span><span class="sxs-lookup"><span data-stu-id="22246-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="22246-240">Индексация и кодирование категориальных признаков в качестве ввода для функций моделирования</span><span class="sxs-lookup"><span data-stu-id="22246-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="22246-241">В этом разделе показано, как tooindex или кодирования категориальных признаков для входных данных в моделирования функции hello.</span><span class="sxs-lookup"><span data-stu-id="22246-241">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="22246-242">Здравствуйте моделирования и предполагаете, что функции MLlib требуют возможности с помощью toobe категориальных данных входного индексированных или кодировке предыдущих toouse.</span><span class="sxs-lookup"><span data-stu-id="22246-242">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="22246-243">В зависимости от модели hello необходима tooindex или кодировать их по-разному:</span><span class="sxs-lookup"><span data-stu-id="22246-243">Depending on hello model, you need tooindex or encode them in different ways:</span></span>  

* <span data-ttu-id="22246-244">**На основе дерева моделирования** требует toobe категорий, кодируются как числовые значения (например, компонент с три категории могут быть кодированы 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="22246-244">**Tree-based modeling** requires categories toobe encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="22246-245">Для этого можно использовать функцию [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) в MLlib.</span><span class="sxs-lookup"><span data-stu-id="22246-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="22246-246">Эта функция кодирует строковый столбец метки столбца tooa метки индексов, упорядоченных по частот метки.</span><span class="sxs-lookup"><span data-stu-id="22246-246">This function encodes a string column of labels tooa column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="22246-247">Несмотря на то, что индексации с числовыми значениями для ввода и обработки данных, на основе дерева алгоритмы hello может быть указанного tootreat их соответствующим образом как категории.</span><span class="sxs-lookup"><span data-stu-id="22246-247">Although indexed with numerical values for input and data handling, hello tree-based algorithms can be specified tootreat them appropriately as categories.</span></span> 
* <span data-ttu-id="22246-248">**Модели логистической и линейной регрессии** требуют горячей один кодировки, where, например, компонент с трем категориям можно развернуть в трех столбцов компонентов, с каждой содержащее 0 или 1 в зависимости от категории hello наблюдения.</span><span class="sxs-lookup"><span data-stu-id="22246-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="22246-249">Предоставляет MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) функции toodo горячей один кодировки.</span><span class="sxs-lookup"><span data-stu-id="22246-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="22246-250">Этот кодировщик сопоставляет столбец метки столбца tooa индексы двоичных векторов, с максимум один значение single.</span><span class="sxs-lookup"><span data-stu-id="22246-250">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="22246-251">Эта кодировка позволяет алгоритмы, которые ожидают числовой табличное значение функции, такие как логистической регрессии применяется toobe toocategorical функции.</span><span class="sxs-lookup"><span data-stu-id="22246-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="22246-252">Ниже приведен код tooindex hello и кодирования категориальных признаков:</span><span class="sxs-lookup"><span data-stu-id="22246-252">Here is hello code tooindex and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="22246-253">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-253">**OUTPUT:**</span></span>

<span data-ttu-id="22246-254">Время, затраченное tooexecute над ячейкой: 1,28 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-254">Time taken tooexecute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="22246-255">Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения</span><span class="sxs-lookup"><span data-stu-id="22246-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="22246-256">Этот раздел содержит код, который показывает, как тип данных категориальные текст tooindex как с меткой точки данных и зашифровать их, чтобы его можно было использовать tootrain и тестирования MLlib логистической регрессии и других моделей классификации.</span><span class="sxs-lookup"><span data-stu-id="22246-256">This section contains code that shows how tooindex categorical text data as a labeled point data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="22246-257">Объекты с помеченной вершиной отформатированы в устойчивые распределенные наборы данных, которые можно использовать в качестве входных для большинства алгоритмов машинного обучения в MLlib.</span><span class="sxs-lookup"><span data-stu-id="22246-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="22246-258">Объект [с помеченной вершиной](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) — это разреженный или плотный локальный вектор, связанный с меткой или ответом.</span><span class="sxs-lookup"><span data-stu-id="22246-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="22246-259">Этот раздел содержит код, который показывает, как tooindex категориальные текстовых данных как [с меткой точки](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) тип данных, а затем включите ее, чтобы его можно было использовать tootrain и тестирования MLlib логистической регрессии и других моделей классификации.</span><span class="sxs-lookup"><span data-stu-id="22246-259">This section contains code that shows how tooindex categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="22246-260">Объекты с помеченной вершиной — это устойчивые распределенные наборы данных, состоящие из метки (переменной ответа или целевой переменной) и вектора признаков.</span><span class="sxs-lookup"><span data-stu-id="22246-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="22246-261">Данные в таком формате используются в качестве входных для алгоритмов машинного обучения в MLlib.</span><span class="sxs-lookup"><span data-stu-id="22246-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="22246-262">Ниже приведен код tooindex hello и кодирования текста функции для двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="22246-262">Here is hello code tooindex and encode text features for binary classification.</span></span>

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


<span data-ttu-id="22246-263">Ниже приведен код hello tooencode и индекс категориальные текстовых признаков для анализа линейной регрессии.</span><span class="sxs-lookup"><span data-stu-id="22246-263">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="22246-264">Создание вложенных случайной выборки данных hello и разбейте его на обучающий и проверочный наборы</span><span class="sxs-lookup"><span data-stu-id="22246-264">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="22246-265">Этот код создает случайной выборки данных hello (здесь используется 25%).</span><span class="sxs-lookup"><span data-stu-id="22246-265">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="22246-266">Несмотря на то, что он не является обязательным для этого примера из-за размера toohello hello набора данных, мы демонстрируют, как можно произвести выборку здесь, вы знаете, как toouse его собственные проблемы, если это требуется.</span><span class="sxs-lookup"><span data-stu-id="22246-266">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample here so you know how toouse it for your own problem when needed.</span></span> <span data-ttu-id="22246-267">Если выборки большие, этот процесс может значительно сэкономить время обучения моделей.</span><span class="sxs-lookup"><span data-stu-id="22246-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="22246-268">Далее мы разбить образец hello в рамках обучения (здесь 75%) и тестирования toouse часть (25% здесь) в классификации и регрессии моделирования.</span><span class="sxs-lookup"><span data-stu-id="22246-268">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="22246-269">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-269">**OUTPUT:**</span></span>

<span data-ttu-id="22246-270">Время, затраченное tooexecute над ячейкой: 0.24 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-270">Time taken tooexecute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="22246-271">масштабирование признаков;</span><span class="sxs-lookup"><span data-stu-id="22246-271">Feature scaling</span></span>
<span data-ttu-id="22246-272">Масштабирование функции, также известные как нормализация данных гарантирует, что функции широко распределенные значениями не учитывая чрезмерного весить в целевой функции hello.</span><span class="sxs-lookup"><span data-stu-id="22246-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="22246-273">Hello код для функции масштабирования использует hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello функции toounit дисперсию.</span><span class="sxs-lookup"><span data-stu-id="22246-273">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="22246-274">MLlib предоставляет функцию StandardScaler для выполнения линейной регрессии с применением метода стохастического градиента. Этот алгоритм широко используется для обучения других моделей машинного обучения (например, регуляризованной регрессии или метода опорных векторов).</span><span class="sxs-lookup"><span data-stu-id="22246-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="22246-275">Обнаружено алгоритм toobe hello LinearRegressionWithSGD конфиденциальных toofeature масштабирования.</span><span class="sxs-lookup"><span data-stu-id="22246-275">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>
> 
> 

<span data-ttu-id="22246-276">Вот переменных tooscale hello кода для использования с регуляризацией hello линейный SGD алгоритм.</span><span class="sxs-lookup"><span data-stu-id="22246-276">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="22246-277">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-277">**OUTPUT:**</span></span>

<span data-ttu-id="22246-278">Время, затраченное tooexecute над ячейкой: 13.17 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-278">Time taken tooexecute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="22246-279">кэширование объектов в памяти.</span><span class="sxs-lookup"><span data-stu-id="22246-279">Cache objects in memory</span></span>
<span data-ttu-id="22246-280">Hello время, необходимое для обучения и проверки алгоритмов машинного Обучения может быть уменьшена путем кэширования объекты кадра hello входные данные, используемые для классификации, регрессию, и возможности масштабирования.</span><span class="sxs-lookup"><span data-stu-id="22246-280">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression, and scaled features.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="22246-281">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-281">**OUTPUT:**</span></span> 

<span data-ttu-id="22246-282">Время, затраченное tooexecute над ячейкой: 0,15 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-282">Time taken tooexecute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="22246-283">Прогнозирование вероятности выплаты чаевых за поездку с помощью моделей бинарной классификации</span><span class="sxs-lookup"><span data-stu-id="22246-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="22246-284">В этом разделе показано, как использование трех моделей для задача двоичной классификации hello прогнозирования, независимо от того, имеется ли для обработки такси оплачивается совет.</span><span class="sxs-lookup"><span data-stu-id="22246-284">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="22246-285">Hello модели представлены являются:</span><span class="sxs-lookup"><span data-stu-id="22246-285">hello models presented are:</span></span>

* <span data-ttu-id="22246-286">регуляризованная логистическая регрессия;</span><span class="sxs-lookup"><span data-stu-id="22246-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="22246-287">модель случайного леса;</span><span class="sxs-lookup"><span data-stu-id="22246-287">Random forest model</span></span>
* <span data-ttu-id="22246-288">градиентный бустинг деревьев.</span><span class="sxs-lookup"><span data-stu-id="22246-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="22246-289">Процесс создания модели состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="22246-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="22246-290">**Обучение модели** с использованием данных с одним набором параметров.</span><span class="sxs-lookup"><span data-stu-id="22246-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="22246-291">**Оценка модели** на основе набора тестовых данных с метриками.</span><span class="sxs-lookup"><span data-stu-id="22246-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="22246-292">**Сохранение модели** в большом двоичном объекте для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="22246-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="22246-293">Классификация с применением логистической регрессии</span><span class="sxs-lookup"><span data-stu-id="22246-293">Classification using logistic regression</span></span>
<span data-ttu-id="22246-294">Hello кода в этом разделе показано, как tootrain, оценки и сохранить модель логистической регрессии с [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , прогнозирует ли совет получает оплату за маршрут в наборе данных маршрута и тариф авиакомпании такси hello NYC.</span><span class="sxs-lookup"><span data-stu-id="22246-294">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="22246-295">**Обучение модели логистической регрессии hello, используя CV и hyperparameter свертки**</span><span class="sxs-lookup"><span data-stu-id="22246-295">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="22246-296">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-296">**OUTPUT:**</span></span> 

<span data-ttu-id="22246-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="22246-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="22246-298">Intercept: -0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="22246-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="22246-299">Время, затраченное tooexecute над ячейкой: 14.43 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-299">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="22246-300">**Оценка модели двоичной классификации hello со стандартными показателями**</span><span class="sxs-lookup"><span data-stu-id="22246-300">**Evaluate hello binary classification model with standard metrics**</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="22246-301">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-301">**OUTPUT:**</span></span> 

<span data-ttu-id="22246-302">Area under PR = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="22246-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="22246-303">Area under ROC = 0.983714670256</span><span class="sxs-lookup"><span data-stu-id="22246-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="22246-304">Summary Stats</span><span class="sxs-lookup"><span data-stu-id="22246-304">Summary Stats</span></span>

<span data-ttu-id="22246-305">Precision = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="22246-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="22246-306">Recall = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="22246-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="22246-307">F1 Score = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="22246-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="22246-308">Время, затраченное tooexecute над ячейкой: 57.61 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-308">Time taken tooexecute above cell: 57.61 seconds</span></span>

<span data-ttu-id="22246-309">**Отобразите hello ROC кривой.**</span><span class="sxs-lookup"><span data-stu-id="22246-309">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="22246-310">Hello *predictionAndLabelsDF* регистрируется как таблица, *tmp_results*, в предыдущую ячейку hello.</span><span class="sxs-lookup"><span data-stu-id="22246-310">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="22246-311">*tmp_results* можно использовать toodo запросов и выводить результаты в hello sqlResults-кадра данных для отображения на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="22246-311">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="22246-312">Ниже приведен код hello.</span><span class="sxs-lookup"><span data-stu-id="22246-312">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="22246-313">Вот прогнозов toomake кода hello и построения hello ROC кривой.</span><span class="sxs-lookup"><span data-stu-id="22246-313">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="22246-314">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-314">**OUTPUT:**</span></span>

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="22246-316">Классификация случайного леса</span><span class="sxs-lookup"><span data-stu-id="22246-316">Random forest classification</span></span>
<span data-ttu-id="22246-317">Hello кода в этом разделе показано, как tootrain, оценки и сохранить модель случайного леса, которая прогнозирует, оплачивается ли подсказка для обработки в hello NYC такси маршрута и тариф авиакомпании набора данных.</span><span class="sxs-lookup"><span data-stu-id="22246-317">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="22246-318">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-318">**OUTPUT:**</span></span>

<span data-ttu-id="22246-319">Area under ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="22246-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="22246-320">Время, затраченное tooexecute над ячейкой: 31.09 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-320">Time taken tooexecute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="22246-321">Классификация с применением модели градиентного бустинга деревьев</span><span class="sxs-lookup"><span data-stu-id="22246-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="22246-322">Hello кода в этом разделе описывается, как tootrain, оценки и сохранить градиента подъема дерева модели, которая прогнозирует, оплачивается ли подсказка для обработки в hello NYC такси маршрута и тариф авиакомпании набора данных.</span><span class="sxs-lookup"><span data-stu-id="22246-322">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="22246-323">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-323">**OUTPUT:**</span></span>

<span data-ttu-id="22246-324">Area under ROC = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="22246-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="22246-325">Время, затраченное tooexecute над ячейкой: 19.76 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-325">Time taken tooexecute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="22246-326">Прогнозирование суммы чаевых за поездку в такси с помощью моделей регрессии</span><span class="sxs-lookup"><span data-stu-id="22246-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="22246-327">В этом разделе показано, как использование трех моделей для hello регрессии задача прогнозирования hello Сумма оплаты trip такси, на основе других функций совет подсказки hello.</span><span class="sxs-lookup"><span data-stu-id="22246-327">This section shows how use three models for hello regression task of predicting hello amount of hello tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="22246-328">Hello модели представлены являются:</span><span class="sxs-lookup"><span data-stu-id="22246-328">hello models presented are:</span></span>

* <span data-ttu-id="22246-329">регуляризованная линейная регрессия;</span><span class="sxs-lookup"><span data-stu-id="22246-329">Regularized linear regression</span></span>
* <span data-ttu-id="22246-330">случайный лес;</span><span class="sxs-lookup"><span data-stu-id="22246-330">Random forest</span></span>
* <span data-ttu-id="22246-331">градиентный бустинг деревьев.</span><span class="sxs-lookup"><span data-stu-id="22246-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="22246-332">Эти модели был описан в введение hello.</span><span class="sxs-lookup"><span data-stu-id="22246-332">These models were described in hello introduction.</span></span> <span data-ttu-id="22246-333">Процесс создания модели состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="22246-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="22246-334">**Обучение модели** с использованием данных с одним набором параметров.</span><span class="sxs-lookup"><span data-stu-id="22246-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="22246-335">**Оценка модели** на основе набора тестовых данных с метриками.</span><span class="sxs-lookup"><span data-stu-id="22246-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="22246-336">**Сохранение модели** в большом двоичном объекте для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="22246-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="22246-337">Линейная регрессия с применением SGD</span><span class="sxs-lookup"><span data-stu-id="22246-337">Linear regression with SGD</span></span>
<span data-ttu-id="22246-338">Hello кода в этом разделе показано, как toouse масштабировать tootrain функции линейной регрессии, который использует вероятностный градиентный спуск (SGD) для оптимизации, и как tooscore, оценки и сохранить модель hello в хранилище больших двоичных объектов Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="22246-338">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="22246-339">Наш опыт показывает могут возникать проблемы с последующим согласованием hello LinearRegressionWithSGD моделей и параметры должны toobe изменен или оптимизированное тщательно для получения модели.</span><span class="sxs-lookup"><span data-stu-id="22246-339">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="22246-340">Проблему конвергенции можно решить, выполнив масштабирование переменных.</span><span class="sxs-lookup"><span data-stu-id="22246-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="22246-341">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-341">**OUTPUT:**</span></span>

<span data-ttu-id="22246-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="22246-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="22246-343">Intercept: 0.853872718283</span><span class="sxs-lookup"><span data-stu-id="22246-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="22246-344">RMSE = 1.24190115863</span><span class="sxs-lookup"><span data-stu-id="22246-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="22246-345">R-sqr = 0.608017146081</span><span class="sxs-lookup"><span data-stu-id="22246-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="22246-346">Время, затраченное tooexecute над ячейкой: 58,42 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-346">Time taken tooexecute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="22246-347">Регрессия с использованием модели случайного леса</span><span class="sxs-lookup"><span data-stu-id="22246-347">Random Forest regression</span></span>
<span data-ttu-id="22246-348">Hello кода в этом разделе показано, как tootrain, оценки и сохранить регрессии случайного леса, которая прогнозирует сумма подсказки для hello NYC такси обработки данных.</span><span class="sxs-lookup"><span data-stu-id="22246-348">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts tip amount for hello NYC taxi trip data.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRING TREES
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="22246-349">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-349">**OUTPUT:**</span></span>

<span data-ttu-id="22246-350">RMSE = 0.891209218139</span><span class="sxs-lookup"><span data-stu-id="22246-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="22246-351">R-sqr = 0.759661334921</span><span class="sxs-lookup"><span data-stu-id="22246-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="22246-352">Время, затраченное tooexecute над ячейкой: 49.21 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-352">Time taken tooexecute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="22246-353">Регрессия с применением градиентного бустинга деревьев</span><span class="sxs-lookup"><span data-stu-id="22246-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="22246-354">Hello кода в этом разделе описывается, как tootrain, оценки и сохранить градиента повышения деревьев модель, прогнозирующая объем подсказки для hello NYC такси обработки данных.</span><span class="sxs-lookup"><span data-stu-id="22246-354">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="22246-355">**Обучение и анализ**</span><span class="sxs-lookup"><span data-stu-id="22246-355">**Train and evaluate **</span></span>

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

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="22246-356">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-356">**OUTPUT:**</span></span>

<span data-ttu-id="22246-357">RMSE = 0.908473148639</span><span class="sxs-lookup"><span data-stu-id="22246-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="22246-358">R-sqr = 0.753835096681</span><span class="sxs-lookup"><span data-stu-id="22246-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="22246-359">Время, затраченное tooexecute над ячейкой: 34.52 секунд</span><span class="sxs-lookup"><span data-stu-id="22246-359">Time taken tooexecute above cell: 34.52 seconds</span></span>

<span data-ttu-id="22246-360">**Графическое представления**</span><span class="sxs-lookup"><span data-stu-id="22246-360">**Plot**</span></span>

<span data-ttu-id="22246-361">*tmp_results* регистрируется как таблицу Hive в предыдущую ячейку hello.</span><span class="sxs-lookup"><span data-stu-id="22246-361">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="22246-362">Результаты из таблицы hello выводятся в hello *sqlResults* кадра данных для отображения на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="22246-362">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="22246-363">Ниже приведен код hello</span><span class="sxs-lookup"><span data-stu-id="22246-363">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="22246-364">Вот hello tooplot кода hello данных с помощью сервера Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="22246-364">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="22246-365">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="22246-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="22246-367">Очистка объектов из памяти</span><span class="sxs-lookup"><span data-stu-id="22246-367">Clean up objects from memory</span></span>
<span data-ttu-id="22246-368">Используйте `unpersist()` toodelete объектов в кэше в памяти.</span><span class="sxs-lookup"><span data-stu-id="22246-368">Use `unpersist()` toodelete objects cached in memory.</span></span>

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a><span data-ttu-id="22246-369">Запись места хранения для потребления и оценки моделей hello</span><span class="sxs-lookup"><span data-stu-id="22246-369">Record storage locations of hello models for consumption and scoring</span></span>
<span data-ttu-id="22246-370">tooconsume и оценка набор независимых описано в hello [оценка и оценить построение Spark машинного обучения моделей](machine-learning-data-science-spark-model-consumption.md) разделе требуются toocopy и вставки этих файлов имена содержащего hello сохранения моделей, созданных здесь в hello Потребление книжке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="22246-370">tooconsume and score an independent dataset described in hello [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need toocopy and paste these file names containing hello saved models created here into hello Consumption Jupyter notebook.</span></span> <span data-ttu-id="22246-371">Вот tooprint кода hello hello пути toomodel файлы, необходимые существует.</span><span class="sxs-lookup"><span data-stu-id="22246-371">Here is hello code tooprint out hello paths toomodel files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="22246-372">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="22246-372">**OUTPUT**</span></span>

<span data-ttu-id="22246-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="22246-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="22246-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="22246-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="22246-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="22246-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="22246-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="22246-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="22246-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="22246-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="22246-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="22246-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="22246-379">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="22246-379">What's next?</span></span>
<span data-ttu-id="22246-380">Теперь после создания модели регрессии и классификации с hello Spark MlLib, готовы toolearn, как tooscore и оценивать эти модели.</span><span class="sxs-lookup"><span data-stu-id="22246-380">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span> <span data-ttu-id="22246-381">Расширенный просмотр данных и моделирования записной книжки Погружение глубже в том числе перекрестной проверки, hyper параметр приветствия широкими и модели оценки.</span><span class="sxs-lookup"><span data-stu-id="22246-381">hello advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="22246-382">**Модели потребления:** toolearn как tooscore и оценить hello классификационных и регрессионных моделей, созданных в этом разделе см. в разделе [оценка и оценки моделей построен Spark машинного обучения](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="22246-382">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="22246-383">**Перекрестная проверка и перебор гиперпараметров**. Сведения об обучении моделей с помощью перекрестной проверки и перебора гиперпараметров см. в статье [Расширенное исследование и моделирование данных с помощью Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md).</span><span class="sxs-lookup"><span data-stu-id="22246-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

