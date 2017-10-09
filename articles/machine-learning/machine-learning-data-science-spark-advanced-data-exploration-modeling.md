---
title: "Просмотр данных aaaAdvanced и моделирования с Spark | Документы Microsoft"
description: "С помощью просмотра данных toodo HDInsight Spark и обучения двоичных моделей классификации и регрессии с помощью перекрестной проверки и hyperparameter оптимизации."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="2aea4-103">Расширенное исследование и моделирование данных с помощью Spark</span><span class="sxs-lookup"><span data-stu-id="2aea4-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="2aea4-104">В этом пошаговом руководстве используется HDInsight Spark toodo данных обучения и просмотра двоичной классификации и перекрестной проверки моделей регрессии и оптимизации hyperparameter образца hello NYC такси маршрута и успешного 2013 набора данных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-104">This walkthrough uses HDInsight Spark toodo data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="2aea4-105">Он поможет выполнить шаги hello hello [процесса обработки и анализа данных](http://aka.ms/datascienceprocess), узел узел, с помощью HDInsight Spark кластера для обработки и модели данных и hello hello toostore больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2aea4-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="2aea4-106">Hello процесс более подробно рассматривается и визуализация данных из большого двоичного объекта хранилища Azure и затем выполняется подготовка данных toobuild hello прогнозных моделей.</span><span class="sxs-lookup"><span data-stu-id="2aea4-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="2aea4-107">Python был используется toocode hello решения и tooshow hello соответствующие графики.</span><span class="sxs-lookup"><span data-stu-id="2aea4-107">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span> <span data-ttu-id="2aea4-108">Эти модели, с помощью hello Spark MLlib toolkit toodo двоичной классификации и регрессии моделирования задачи построения.</span><span class="sxs-lookup"><span data-stu-id="2aea4-108">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="2aea4-109">Hello **двоичной классификации** задача — toopredict ли совет оплачивается поездки hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-109">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="2aea4-110">Hello **регрессии** задача представляет сумму hello toopredict hello подсказки на основе других функций подсказки.</span><span class="sxs-lookup"><span data-stu-id="2aea4-110">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="2aea4-111">Hello моделирования действия также содержат код, показывающий, как tootrain, оценки и сохранение каждого типа модели.</span><span class="sxs-lookup"><span data-stu-id="2aea4-111">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="2aea4-112">Hello разделе освещаются некоторые hello основание таким же, как hello [данных и моделирование с Spark](machine-learning-data-science-spark-data-exploration-modeling.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="2aea4-112">hello topic covers some of hello same ground as hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="2aea4-113">Однако он является более «Дополнительно», так как он использует перекрестной проверки с hyperparameter широкими tootrain оптимально точные классификационных и регрессионных моделей.</span><span class="sxs-lookup"><span data-stu-id="2aea4-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping tootrain optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="2aea4-114">**Перекрестная проверка (CV)** — это метод, который оценивает, насколько хорошо модель, обученную на известный набор данных обобщает возможности hello toopredicting наборов данных, на котором он еще не прошла обучение.</span><span class="sxs-lookup"><span data-stu-id="2aea4-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes toopredicting hello features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="2aea4-115">Здесь используется общая реализация является набор данных на свертки K toodivide и затем обучения модели hello в циклического перебора всех, кроме одного сверток hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-115">A common implementation used here is toodivide a dataset into K folds and then train hello model in a round-robin fashion on all but one of hello folds.</span></span> <span data-ttu-id="2aea4-116">оценивается возможность Hello hello модели tooprediction точно в том случае, когда протестирован hello независимый набор данных в этой модели hello tootrain свертки не используется.</span><span class="sxs-lookup"><span data-stu-id="2aea4-116">hello ability of hello model tooprediction accurately when tested against hello independent dataset in this fold not used tootrain hello model is assessed.</span></span>

<span data-ttu-id="2aea4-117">**Оптимизация Hyperparameter** проблема hello по выбору набор гиперпараметров для алгоритма обучения, обычно с целью hello оптимизация показателем производительности hello алгоритм на независимый набор данных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-117">**Hyperparameter optimization** is hello problem of choosing a set of hyperparameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="2aea4-118">**Гиперпараметров** — это значения, которые должны быть указаны вне процедуры обучения модели hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-118">**Hyperparameters** are values that must be specified outside of hello model training procedure.</span></span> <span data-ttu-id="2aea4-119">Предположения о этих значений может повлиять на гибкость hello и точности моделей hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-119">Assumptions about these values can impact hello flexibility and accuracy of hello models.</span></span> <span data-ttu-id="2aea4-120">Деревья принятия решений имеют гиперпараметров, к примеру, такие как hello требуемого глубины и количества листьев в дереве hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-120">Decision trees have hyperparameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="2aea4-121">Для методов опорных векторов (SVM) необходимо задать условие штрафа за неправильную классификацию.</span><span class="sxs-lookup"><span data-stu-id="2aea4-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="2aea4-122">Обычно способом tooperform hyperparameter для оптимизации используются здесь является поиска в сетке или **очистки параметров**.</span><span class="sxs-lookup"><span data-stu-id="2aea4-122">A common way tooperform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="2aea4-123">Сюда входят выполняет тщательный поиск по значениям hello определенному подмножеству hello hyperparameter пространства для алгоритма обучения.</span><span class="sxs-lookup"><span data-stu-id="2aea4-123">This consists of performing an exhaustive search through hello values a specified subset of hello hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="2aea4-124">Перекрестной проверки можно указать toosort метрики производительности out hello оптимальные результаты, найденные с помощью алгоритма поиска hello сетки.</span><span class="sxs-lookup"><span data-stu-id="2aea4-124">Cross validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="2aea4-125">Используется с широкими подобных ограничение помогает лжевзаимосвязей tootraining модели данных, чтобы hello модель сохраняет hello емкость tooapply toohello общий набор данных, из которой hello обучающие данные были извлечены hyperparameter CV.</span><span class="sxs-lookup"><span data-stu-id="2aea4-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model tootraining data so that hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

<span data-ttu-id="2aea4-126">модели Hello, мы используем включают логистической и линейной регрессии, случайные леса и градиента повышенных деревьев:</span><span class="sxs-lookup"><span data-stu-id="2aea4-126">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="2aea4-127">[Линейная регрессия с SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) модель линейной регрессии, которая использует метод вероятностный градиентный спуск (SGD) и для оптимизации и возможность масштабирования toopredict hello совет суммы оплаты.</span><span class="sxs-lookup"><span data-stu-id="2aea4-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="2aea4-128">[Логистическая Регрессия с LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) и регрессии «logit» представляет собой модель регрессии, который может использоваться при классификации данных категориальные toodo hello зависимой переменной.</span><span class="sxs-lookup"><span data-stu-id="2aea4-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="2aea4-129">LBFGS-это алгоритм оптимизации реализация ньютон, соответствующий алгоритм Бройдена-Флетчера-Гольдфарба-Шанно (BFGS) hello ограниченный объем памяти компьютера с помощью и широко используемый в машинном обучении.</span><span class="sxs-lookup"><span data-stu-id="2aea4-129">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="2aea4-130">[Случайные леса](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="2aea4-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="2aea4-131">Они объединяют многих решений деревьев tooreduce hello риск переобучения.</span><span class="sxs-lookup"><span data-stu-id="2aea4-131">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="2aea4-132">Случайные леса, используются для классификации и регрессии и может обрабатывать категориальных признаков и могут быть расширены параметр toohello мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="2aea4-132">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="2aea4-133">Они не требуется возможность масштабирования и являются может toocapture нелинейности и возможность взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="2aea4-133">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="2aea4-134">Случайные леса принадлежат hello наиболее успешных моделей машинного обучения для классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="2aea4-134">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="2aea4-135">[Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="2aea4-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="2aea4-136">Решение GBTs обучение итеративного дерева toominimize функции потерь.</span><span class="sxs-lookup"><span data-stu-id="2aea4-136">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="2aea4-137">GBTs используются для классификации и регрессии и может обрабатывать категориальных признаков не требуется возможность масштабирования и являются может toocapture нелинейности и возможностей взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="2aea4-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="2aea4-138">Кроме того, его можно использовать для создания модели мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="2aea4-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="2aea4-139">Примеры использования CV и Hyperparameter моделирования Очистка отображаются для проблемы бинарной классификации hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-139">Modeling examples using CV and Hyperparameter sweep are shown for hello binary classification problem.</span></span> <span data-ttu-id="2aea4-140">Более простые примеры (без параметра переходов) перечислены в разделе Основные hello по задачам регрессии.</span><span class="sxs-lookup"><span data-stu-id="2aea4-140">Simpler examples (without parameter sweeps) are presented in hello main topic for regression tasks.</span></span> <span data-ttu-id="2aea4-141">Однако в приложение hello также предоставляются проверку с помощью эластичных net для линейной регрессии и CV с параметром с помощью очистки для регрессии случайного леса.</span><span class="sxs-lookup"><span data-stu-id="2aea4-141">But in hello appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="2aea4-142">Hello **гибкому net** — метод регуляризованной регрессии линейно подгонки линейной регрессии моделей, объединяющее показателей L1 и L2 hello ответственность за hello [лассо](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) и [ребра](https://en.wikipedia.org/wiki/Tikhonov_regularization) методы.</span><span class="sxs-lookup"><span data-stu-id="2aea4-142">hello **elastic net** is a regularized regression method for fitting linear regression models that linearly combines hello L1 and L2 metrics as penalties of hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="2aea4-143">Хотя набор средств Spark MLlib hello спроектированный toowork с большими наборами данных, сравнительно небольшую выборку (с помощью 170 тысяч строк, 0,1% hello исходный набор данных NYC ~ 30 МБ) используется здесь для удобства.</span><span class="sxs-lookup"><span data-stu-id="2aea4-143">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="2aea4-144">Упражнение Hello в данном разделе выполняется эффективно (в течение 10 минут) в кластере HDInsight с 2 рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="2aea4-144">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="2aea4-145">Hello одинаковый код, с небольшими изменениями может быть используется tooprocess более крупных-наборов данных, с соответствующими изменениями для кэширования данных в памяти и изменение размера кластера hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-145">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="2aea4-146">Настройка: кластеры и записные книжки Spark</span><span class="sxs-lookup"><span data-stu-id="2aea4-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="2aea4-147">Действия по настройке и код, указанные в этом пошаговом руководстве, применимы к использованию для HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="2aea4-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="2aea4-148">Но записные книжки Jupyter можно использовать для кластеров HDInsight Spark 1.6 и Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="2aea4-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="2aea4-149">Описание toothem hello записных книжек и ссылки, представлено в hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) для репозитория GitHub hello, содержащий их.</span><span class="sxs-lookup"><span data-stu-id="2aea4-149">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="2aea4-150">Кроме того код hello здесь и в записных книжках hello связаны является универсальным и должен работать на любой кластер Spark.</span><span class="sxs-lookup"><span data-stu-id="2aea4-150">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="2aea4-151">Если вы не используете HDInsight Spark, настройку и управление ими действия hello кластера может быть немного отличается от показанной здесь.</span><span class="sxs-lookup"><span data-stu-id="2aea4-151">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="2aea4-152">Для удобства ниже приведены hello записные книжки Jupyter ссылки toohello Spark 1.6 и toobe 2.0, выполняются в ядро pyspark hello hello server книжке Jupyter.</span><span class="sxs-lookup"><span data-stu-id="2aea4-152">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 and 2.0 toobe run in hello pyspark kernel of hello Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="2aea4-153">Записные книжки для Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="2aea4-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="2aea4-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb). Содержит разделы в записной книжке №1 и варианты моделей с использованием настройки гиперпараметров и перекрестной проверки.</span><span class="sxs-lookup"><span data-stu-id="2aea4-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="2aea4-155">Записные книжки для Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="2aea4-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="2aea4-156">[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): этот файл содержит сведения о как tooperform Просмотр данных, моделирования и оценки в Spark 2.0 кластеров.</span><span class="sxs-lookup"><span data-stu-id="2aea4-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="2aea4-157">Программа установки: hello, библиотеки и расположения хранилища конфигурации Spark контекста</span><span class="sxs-lookup"><span data-stu-id="2aea4-157">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="2aea4-158">Spark — может tooAzure tooread и записи хранилища больших двоичных объектов (также известный как WASB).</span><span class="sxs-lookup"><span data-stu-id="2aea4-158">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="2aea4-159">Поэтому любые существующие данные, хранящиеся в ней могут быть обработаны с помощью Spark и hello результаты хранимых в WASB.</span><span class="sxs-lookup"><span data-stu-id="2aea4-159">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="2aea4-160">toosave модели или файлов в WASB, hello путь должен toobe указано правильно.</span><span class="sxs-lookup"><span data-stu-id="2aea4-160">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="2aea4-161">Hello кластера Spark toohello присоединенного контейнера по умолчанию можно обращаться, используя путь, начиная с: «wasb: / / /».</span><span class="sxs-lookup"><span data-stu-id="2aea4-161">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="2aea4-162">Другие расположения начинаются с wasb://.</span><span class="sxs-lookup"><span data-stu-id="2aea4-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="2aea4-163">Настройка путей каталога к месту хранения в хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="2aea4-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="2aea4-164">Hello следующий код задает hello место чтения toobe данных hello и hello hello модели хранения каталога toowhich hello модели выходных данных будет сохранен:</span><span class="sxs-lookup"><span data-stu-id="2aea4-164">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="2aea4-165">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-165">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="2aea4-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="2aea4-167">Импорт библиотек</span><span class="sxs-lookup"><span data-stu-id="2aea4-167">Import libraries</span></span>
<span data-ttu-id="2aea4-168">Импортируйте необходимые библиотеки с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="2aea4-168">Import necessary libraries with hello following code:</span></span>

    # LOAD PYSPARK LIBRARIES
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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="2aea4-169">Предустановленный контекст Spark и волшебные команды PySpark</span><span class="sxs-lookup"><span data-stu-id="2aea4-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="2aea4-170">Hello PySpark ядер, предоставляемых с записные книжки Jupyter имеют предустановленных контекста.</span><span class="sxs-lookup"><span data-stu-id="2aea4-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="2aea4-171">Поэтому необязательно tooset hello Spark или куст контекстов явно перед началом работы с приложением hello, которое вы разрабатываете.</span><span class="sxs-lookup"><span data-stu-id="2aea4-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="2aea4-172">Эти контексты доступны вам по умолчанию,</span><span class="sxs-lookup"><span data-stu-id="2aea4-172">These contexts are available for you by default.</span></span> <span data-ttu-id="2aea4-173">а именно:</span><span class="sxs-lookup"><span data-stu-id="2aea4-173">These contexts are:</span></span>

* <span data-ttu-id="2aea4-174">sc для Spark;</span><span class="sxs-lookup"><span data-stu-id="2aea4-174">sc - for Spark</span></span> 
* <span data-ttu-id="2aea4-175">sqlContext для Hive.</span><span class="sxs-lookup"><span data-stu-id="2aea4-175">sqlContext - for Hive</span></span>

<span data-ttu-id="2aea4-176">Hello ядра PySpark предоставляет некоторые предопределенные «magics», которые являются специальные команды, которые можно вызвать с %%.</span><span class="sxs-lookup"><span data-stu-id="2aea4-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="2aea4-177">В этих примерах кода используются две подобные команды.</span><span class="sxs-lookup"><span data-stu-id="2aea4-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="2aea4-178">**%% локального** указывает, что код hello в последующих строках toobe выполняются локально.</span><span class="sxs-lookup"><span data-stu-id="2aea4-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="2aea4-179">В качестве кода должен быть указан корректный код Python.</span><span class="sxs-lookup"><span data-stu-id="2aea4-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="2aea4-180">**%% sql -o <variable name>**  выполняет запрос Hive в отношении hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="2aea4-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="2aea4-181">Если передается параметр -o hello, hello результат запроса hello сохраняется в hello %% локального контекста Python как Pandas кадр данных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="2aea4-182">Для Дополнительные сведения о ядра hello записные книжки Jupyter и предопределенные hello «magics», они предоставляют, в разделе [кластеры ядер, доступных для записные книжки Jupyter с HDInsight Spark Linux в HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="2aea4-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="2aea4-183">Прием данных из открытого большого двоичного объекта:</span><span class="sxs-lookup"><span data-stu-id="2aea4-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="2aea4-184">Hello первым шагом в процессе обработки и анализа данных hello является tooingest hello данных toobe анализируются из источников, где она находится в среде моделирования и просмотра данных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="2aea4-185">В нашем пошаговом руководстве — это среда Spark.</span><span class="sxs-lookup"><span data-stu-id="2aea4-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="2aea4-186">Этот раздел содержит toocomplete кода hello последовательности задач:</span><span class="sxs-lookup"><span data-stu-id="2aea4-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="2aea4-187">hello данные примера toobe моделируется приема</span><span class="sxs-lookup"><span data-stu-id="2aea4-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="2aea4-188">чтение во входном наборе данных hello (хранятся в формате .tsv)</span><span class="sxs-lookup"><span data-stu-id="2aea4-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="2aea4-189">Очистить hello данные и формат</span><span class="sxs-lookup"><span data-stu-id="2aea4-189">format and clean hello data</span></span>
* <span data-ttu-id="2aea4-190">создание и кэширование объектов (устойчивых распределенных наборов данных или фреймов данных) в памяти;</span><span class="sxs-lookup"><span data-stu-id="2aea4-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="2aea4-191">регистрация данных в качестве временной таблицы в контексте SQL.</span><span class="sxs-lookup"><span data-stu-id="2aea4-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="2aea4-192">Ниже приведен код hello для приема данных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-192">Here is hello code for data ingestion.</span></span>

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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2aea4-193">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-193">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-194">Время, затраченное tooexecute над ячейкой: 276.62 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-194">Time taken tooexecute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="2aea4-195">Исследование и визуализация данных</span><span class="sxs-lookup"><span data-stu-id="2aea4-195">Data exploration & visualization</span></span>
<span data-ttu-id="2aea4-196">Hello данных была помещена в Spark, hello следующим шагом в процессе обработки и анализа данных hello после toogain глубокого понимания hello данных через Просмотр и визуализация.</span><span class="sxs-lookup"><span data-stu-id="2aea4-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="2aea4-197">В этом разделе рассматриваются hello такси данные с помощью SQL-запросов построения hello целевой переменных и потенциальных возможностей для визуальной проверки.</span><span class="sxs-lookup"><span data-stu-id="2aea4-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="2aea4-198">В частности мы построения hello частоту пассажира счетчиков в такси приема-передачи, частота hello совет сумм и как изменять советы по типам и сумма платежа.</span><span class="sxs-lookup"><span data-stu-id="2aea4-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="2aea4-199">Построить гистограмму для частоты счетчика пассажира в образце hello такси приема-передачи данных</span><span class="sxs-lookup"><span data-stu-id="2aea4-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="2aea4-200">Этот код и последующие фрагменты использовать образец hello magic tooquery SQL и данных локального magic tooplot hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="2aea4-201">**Магическое SQL (`%%sql`)** hello ядра HDInsight PySpark поддерживает встроенные легко HiveQL запросы к hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="2aea4-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="2aea4-202">Hello (-o имя_переменной) аргумент hello выходных данных запроса SQL hello сохраняется как Pandas кадр данных на сервере Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="2aea4-203">Это означает, что он доступен в локальном режиме hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="2aea4-204">Hello  **`%%local` магическое** — использовать код toorun локально на сервере Jupyter hello, где hello головному узлу кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="2aea4-205">Как правило, используется `%%local` magic после hello `%%sql -o` magic — используется toorun запроса.</span><span class="sxs-lookup"><span data-stu-id="2aea4-205">Typically, you use `%%local` magic after hello `%%sql -o` magic is used toorun a query.</span></span> <span data-ttu-id="2aea4-206">параметр -o Hello сохранится hello выходных данных запроса SQL hello локально.</span><span class="sxs-lookup"><span data-stu-id="2aea4-206">hello -o parameter would persist hello output of hello SQL query locally.</span></span> <span data-ttu-id="2aea4-207">Здравствуйте, затем `%%local` magic триггеры hello следующего набора toorun фрагменты кода локально к выходным данным hello hello запросов SQL, в которой сохраняется в локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="2aea4-207">Then hello `%%local` magic triggers hello next set of code snippets toorun locally against hello output of hello SQL queries that has been persisted locally.</span></span> <span data-ttu-id="2aea4-208">выходные данные Hello автоматически визуализируются после выполнения кода hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-208">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="2aea4-209">Этот запрос извлекает hello приема-передачи данных по количеству пассажира.</span><span class="sxs-lookup"><span data-stu-id="2aea4-209">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="2aea4-210">Этот код создает локальный кадров данных из результатов запроса hello и представлены данные hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-210">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="2aea4-211">Hello `%%local` magic создает локальный-кадра данных, `sqlResults`, который может использоваться для отображения на диаграмме с помощью matplotlib.</span><span class="sxs-lookup"><span data-stu-id="2aea4-211">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="2aea4-212">В этом пошаговом руководстве волшебная команда PySpark используется несколько раз.</span><span class="sxs-lookup"><span data-stu-id="2aea4-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="2aea4-213">При больших размерах hello объем данных следует образец toocreate кадра данных, помещающихся в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="2aea4-213">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="2aea4-214">Вот hello кода tooplot hello приема-передачи с пассажира счетчиков</span><span class="sxs-lookup"><span data-stu-id="2aea4-214">Here is hello code tooplot hello trips by passenger counts</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="2aea4-215">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-215">**OUTPUT**</span></span>

![Частота поездок в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="2aea4-217">Можно выбирать различные виды визуализаций (таблицы, круговая, строки, области или панели) с помощью hello **тип** кнопок меню в записной книжке hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="2aea4-218">Здесь показана панель построения Hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-218">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="2aea4-219">Построение гистограммы суммы чаевых и ее зависимости от количества пассажиров и тарифа.</span><span class="sxs-lookup"><span data-stu-id="2aea4-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="2aea4-220">Использовать toosample данных запроса SQL...</span><span class="sxs-lookup"><span data-stu-id="2aea4-220">Use a SQL query toosample data..</span></span>

    # SQL SQUERY
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


<span data-ttu-id="2aea4-221">Эта ячейка код использует данные о hello hello SQL запроса toocreate три графики.</span><span class="sxs-lookup"><span data-stu-id="2aea4-221">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


<span data-ttu-id="2aea4-222">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="2aea4-222">**OUTPUT:**</span></span> 

![Распределение суммы чаевых](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Сумма чаевых в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Сумма чаевых в зависимости от тарифа](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="2aea4-226">Проектирование признаков, преобразование и подготовка данных к моделированию</span><span class="sxs-lookup"><span data-stu-id="2aea4-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="2aea4-227">В этом разделе описывается и предоставляет кода hello для процедур, используемых tooprepare данных для использования в модели машинного Обучения.</span><span class="sxs-lookup"><span data-stu-id="2aea4-227">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="2aea4-228">Здесь показано, как hello toodo следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2aea4-228">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="2aea4-229">Создание нового признака путем секционирования часов в ячейки трафика.</span><span class="sxs-lookup"><span data-stu-id="2aea4-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="2aea4-230">Индексация и прямое кодирование категориальных признаков</span><span class="sxs-lookup"><span data-stu-id="2aea4-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="2aea4-231">Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения</span><span class="sxs-lookup"><span data-stu-id="2aea4-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="2aea4-232">Создание вложенных случайной выборки данных hello и разбейте его на обучающий и проверочный наборы</span><span class="sxs-lookup"><span data-stu-id="2aea4-232">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="2aea4-233">масштабирование признаков;</span><span class="sxs-lookup"><span data-stu-id="2aea4-233">Feature scaling</span></span>
* <span data-ttu-id="2aea4-234">кэширование объектов в памяти.</span><span class="sxs-lookup"><span data-stu-id="2aea4-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="2aea4-235">Создание нового признака путем секционирования часов трафика в ячейки.</span><span class="sxs-lookup"><span data-stu-id="2aea4-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="2aea4-236">Этот код показывает, как toocreate новую функцию с помощью секционирования трафика времени в ячейки, а затем как toocache hello результирующий кадр данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="2aea4-236">This code shows how toocreate a new feature by partitioning traffic times into bins and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="2aea4-237">Кэширование приводит tooimproved времени выполнения, где устойчивым распределенных наборы данных (RDDs) и кадров данных используются несколько раз.</span><span class="sxs-lookup"><span data-stu-id="2aea4-237">Caching leads tooimproved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="2aea4-238">В этом пошаговом руководстве процесс кэширования существующих данных выполняется в несколько этапов.</span><span class="sxs-lookup"><span data-stu-id="2aea4-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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

<span data-ttu-id="2aea4-239">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-239">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-240">126 050.</span><span class="sxs-lookup"><span data-stu-id="2aea4-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="2aea4-241">Индексация и прямое кодирование категориальных признаков</span><span class="sxs-lookup"><span data-stu-id="2aea4-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="2aea4-242">В этом разделе показано, как tooindex или кодирования категориальных признаков для входных данных в моделирования функции hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-242">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="2aea4-243">Здравствуйте, моделирования и прогнозирования функции MLlib требуют возможности с помощью категориальных данных входного быть проиндексированы или кодировке предыдущих toouse.</span><span class="sxs-lookup"><span data-stu-id="2aea4-243">hello modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior toouse.</span></span> 

<span data-ttu-id="2aea4-244">В зависимости от модели hello необходима tooindex или кодировать их по-разному.</span><span class="sxs-lookup"><span data-stu-id="2aea4-244">Depending on hello model, you need tooindex or encode them in different ways.</span></span> <span data-ttu-id="2aea4-245">Например, модели логистической и линейной регрессии требуют горячей один кодировки, где, например, в трех столбцов компонентов, с каждой содержащее 0 или 1 в зависимости от категории hello наблюдения можно развернуть компонент с три категории.</span><span class="sxs-lookup"><span data-stu-id="2aea4-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="2aea4-246">Предоставляет MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) функции toodo горячей один кодировки.</span><span class="sxs-lookup"><span data-stu-id="2aea4-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="2aea4-247">Этот кодировщик сопоставляет столбец метки столбца tooa индексы двоичных векторов, с максимум один значение single.</span><span class="sxs-lookup"><span data-stu-id="2aea4-247">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="2aea4-248">Эта кодировка позволяет алгоритмы, которые ожидают числовой табличное значение функции, такие как логистической регрессии применяется toobe toocategorical функции.</span><span class="sxs-lookup"><span data-stu-id="2aea4-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="2aea4-249">Ниже приведен код tooindex hello и кодирования категориальных признаков:</span><span class="sxs-lookup"><span data-stu-id="2aea4-249">Here is hello code tooindex and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

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


<span data-ttu-id="2aea4-250">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-250">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-251">Время, затраченное tooexecute над ячейкой: 3.14 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-251">Time taken tooexecute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="2aea4-252">Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения</span><span class="sxs-lookup"><span data-stu-id="2aea4-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="2aea4-253">Этот раздел содержит код, который показывает, как тип данных категориальные text tooindex как с меткой точки данных и как tooencode его.</span><span class="sxs-lookup"><span data-stu-id="2aea4-253">This section contains code that shows how tooindex categorical text data as a labeled point data type and how tooencode it.</span></span> <span data-ttu-id="2aea4-254">Это подготавливает toobe используется tootrain и тестирования MLlib логистической регрессии и другие модели классификации.</span><span class="sxs-lookup"><span data-stu-id="2aea4-254">This prepares it toobe used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="2aea4-255">Объекты с помеченной вершиной отформатированы в устойчивые распределенные наборы данных, которые можно использовать в качестве входных для большинства алгоритмов машинного обучения в MLlib.</span><span class="sxs-lookup"><span data-stu-id="2aea4-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="2aea4-256">Объект [с помеченной вершиной](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) — это разреженный или плотный локальный вектор, связанный с меткой или ответом.</span><span class="sxs-lookup"><span data-stu-id="2aea4-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="2aea4-257">Ниже приведен код tooindex hello и кодирования текста функции для двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="2aea4-257">Here is hello code tooindex and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="2aea4-258">Ниже приведен код hello tooencode и индекс категориальные текстовых признаков для анализа линейной регрессии.</span><span class="sxs-lookup"><span data-stu-id="2aea4-258">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="2aea4-259">Создание вложенных случайной выборки данных hello и разбейте его на обучающий и проверочный наборы</span><span class="sxs-lookup"><span data-stu-id="2aea4-259">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="2aea4-260">Этот код создает случайной выборки данных hello (здесь используется 25%).</span><span class="sxs-lookup"><span data-stu-id="2aea4-260">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="2aea4-261">Несмотря на то, что он не является обязательным для этого примера из-за размера toohello hello набора данных, мы демонстрируют, как можно произвести выборку данных hello здесь.</span><span class="sxs-lookup"><span data-stu-id="2aea4-261">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample hello data here.</span></span> <span data-ttu-id="2aea4-262">Затем вы знаете, как toouse его собственные проблемы, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="2aea4-262">Then you know how toouse it for your own problem if needed.</span></span> <span data-ttu-id="2aea4-263">Если выборки большие, этот процесс может значительно сэкономить время обучения моделей.</span><span class="sxs-lookup"><span data-stu-id="2aea4-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="2aea4-264">Далее мы разбить образец hello в рамках обучения (здесь 75%) и тестирования toouse часть (25% здесь) в классификации и регрессии моделирования.</span><span class="sxs-lookup"><span data-stu-id="2aea4-264">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

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

<span data-ttu-id="2aea4-265">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-265">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-266">Время, затраченное tooexecute над ячейкой: 0.31 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-266">Time taken tooexecute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="2aea4-267">масштабирование признаков;</span><span class="sxs-lookup"><span data-stu-id="2aea4-267">Feature scaling</span></span>
<span data-ttu-id="2aea4-268">Масштабирование функции, также известные как нормализация данных гарантирует, что функции широко распределенные значениями не учитывая чрезмерного весить в целевой функции hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="2aea4-269">Hello код для функции масштабирования использует hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello функции toounit дисперсию.</span><span class="sxs-lookup"><span data-stu-id="2aea4-269">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="2aea4-270">MLlib предоставляет функцию StandardScaler для выполнения линейной регрессии с применением метода стохастического градиента (SGD).</span><span class="sxs-lookup"><span data-stu-id="2aea4-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="2aea4-271">Алгоритм SGD широко используется для обучения других моделей машинного обучения (например, регуляризованной регрессии или метода опорных векторов).</span><span class="sxs-lookup"><span data-stu-id="2aea4-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="2aea4-272">Обнаружено алгоритм toobe hello LinearRegressionWithSGD конфиденциальных toofeature масштабирования.</span><span class="sxs-lookup"><span data-stu-id="2aea4-272">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>   
> 
> 

<span data-ttu-id="2aea4-273">Вот переменных tooscale hello кода для использования с регуляризацией hello линейный SGD алгоритм.</span><span class="sxs-lookup"><span data-stu-id="2aea4-273">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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

<span data-ttu-id="2aea4-274">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-274">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-275">Время, затраченное tooexecute над ячейкой: 11.67 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-275">Time taken tooexecute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="2aea4-276">кэширование объектов в памяти.</span><span class="sxs-lookup"><span data-stu-id="2aea4-276">Cache objects in memory</span></span>
<span data-ttu-id="2aea4-277">Hello время, необходимое для обучения и проверки алгоритмов машинного Обучения можно уменьшить путем кэширования hello входные данные кадра объекты используются для классификации, регрессию и возможности масштабирования.</span><span class="sxs-lookup"><span data-stu-id="2aea4-277">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression and, scaled features.</span></span>

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

<span data-ttu-id="2aea4-278">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-278">**OUTPUT**</span></span> 

<span data-ttu-id="2aea4-279">Время, затраченное tooexecute над ячейкой: 0,13 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-279">Time taken tooexecute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="2aea4-280">Прогнозирование вероятности выплаты чаевых за поездку с помощью моделей бинарной классификации</span><span class="sxs-lookup"><span data-stu-id="2aea4-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="2aea4-281">В этом разделе показано, как использование трех моделей для задача двоичной классификации hello прогнозирования, независимо от того, имеется ли для обработки такси оплачивается совет.</span><span class="sxs-lookup"><span data-stu-id="2aea4-281">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="2aea4-282">Hello модели представлены являются:</span><span class="sxs-lookup"><span data-stu-id="2aea4-282">hello models presented are:</span></span>

* <span data-ttu-id="2aea4-283">Логистическая регрессия</span><span class="sxs-lookup"><span data-stu-id="2aea4-283">Logistic regression</span></span> 
* <span data-ttu-id="2aea4-284">Случайный лес</span><span class="sxs-lookup"><span data-stu-id="2aea4-284">Random forest</span></span>
* <span data-ttu-id="2aea4-285">Градиентный бустинг деревьев</span><span class="sxs-lookup"><span data-stu-id="2aea4-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="2aea4-286">Процесс создания модели состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="2aea4-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="2aea4-287">**Обучение модели** с использованием данных с одним набором параметров.</span><span class="sxs-lookup"><span data-stu-id="2aea4-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="2aea4-288">**Оценка модели** на основе набора тестовых данных с метриками.</span><span class="sxs-lookup"><span data-stu-id="2aea4-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="2aea4-289">**Сохранение модели** в большом двоичном объекте для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="2aea4-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="2aea4-290">Далее показано, как toodo перекрестной проверки (CV) с параметром широкими двумя способами:</span><span class="sxs-lookup"><span data-stu-id="2aea4-290">We show how toodo cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="2aea4-291">С помощью **универсального** задает пользовательский код, который может быть применен tooany алгоритма в параметре MLlib и tooany в алгоритме.</span><span class="sxs-lookup"><span data-stu-id="2aea4-291">Using **generic** custom code which can be applied tooany algorithm in MLlib and tooany parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="2aea4-292">С помощью hello **pySpark CrossValidator конвейера функция**.</span><span class="sxs-lookup"><span data-stu-id="2aea4-292">Using hello **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="2aea4-293">Обратите внимание, что CrossValidator имеет несколько ограничений для Spark 1.5.0.</span><span class="sxs-lookup"><span data-stu-id="2aea4-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="2aea4-294">Модели конвейера не могут быть сохранены для последующей обработки.</span><span class="sxs-lookup"><span data-stu-id="2aea4-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="2aea4-295">Не может использоваться для каждого параметра в модели.</span><span class="sxs-lookup"><span data-stu-id="2aea4-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="2aea4-296">Не может использоваться для каждого алгоритма MLlib.</span><span class="sxs-lookup"><span data-stu-id="2aea4-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="2aea4-297">Универсальный перекрестной проверки и hyperparameter свертки, используемые с алгоритмом логистической регрессии hello для двоичной классификации</span><span class="sxs-lookup"><span data-stu-id="2aea4-297">Generic cross validation and hyperparameter sweeping used with hello logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="2aea4-298">Hello кода в этом разделе показано, как tootrain, оценки и сохранить модель логистической регрессии с [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , прогнозирует ли совет получает оплату за маршрут в наборе данных маршрута и тариф авиакомпании такси hello NYC.</span><span class="sxs-lookup"><span data-stu-id="2aea4-298">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="2aea4-299">Hello модель обучается перекрестной проверки (CV) и свертки hyperparameter реализуется с помощью пользовательского кода, который может быть применен tooany обучающие алгоритмы в MLlib hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-299">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied tooany of hello learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="2aea4-300">Этот пользовательский код CV Hello выполнение может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2aea4-300">hello execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="2aea4-301">**Обучение модели логистической регрессии hello, используя CV и hyperparameter свертки**</span><span class="sxs-lookup"><span data-stu-id="2aea4-301">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2aea4-302">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-302">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="2aea4-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="2aea4-304">Intercept: -0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="2aea4-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="2aea4-305">Время, затраченное tooexecute над ячейкой: 14.43 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-305">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="2aea4-306">**Оценка модели двоичной классификации hello со стандартными показателями**</span><span class="sxs-lookup"><span data-stu-id="2aea4-306">**Evaluate hello binary classification model with standard metrics**</span></span>

<span data-ttu-id="2aea4-307">Hello кода в этом разделе показано, как tooevaluate логистической регрессии модели с проверочных данных, включая рисунка hello ROC кривой.</span><span class="sxs-lookup"><span data-stu-id="2aea4-307">hello code in this section shows how tooevaluate a logistic regression model against a test data-set, including a plot of hello ROC curve.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

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

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2aea4-308">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-308">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-309">Area under PR = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="2aea4-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="2aea4-310">Area under ROC = 0.983383274312</span><span class="sxs-lookup"><span data-stu-id="2aea4-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="2aea4-311">Summary Stats</span><span class="sxs-lookup"><span data-stu-id="2aea4-311">Summary Stats</span></span>

<span data-ttu-id="2aea4-312">Precision = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="2aea4-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="2aea4-313">Recall = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="2aea4-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="2aea4-314">F1 Score = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="2aea4-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="2aea4-315">Время, затраченное tooexecute над ячейкой: 2,67 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-315">Time taken tooexecute above cell: 2.67 seconds</span></span>

<span data-ttu-id="2aea4-316">**Отобразите hello ROC кривой.**</span><span class="sxs-lookup"><span data-stu-id="2aea4-316">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="2aea4-317">Hello *predictionAndLabelsDF* регистрируется как таблица, *tmp_results*, в предыдущую ячейку hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-317">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="2aea4-318">*tmp_results* можно использовать toodo запросов и выводить результаты в hello sqlResults-кадра данных для отображения на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="2aea4-318">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="2aea4-319">Ниже приведен код hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-319">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="2aea4-320">Вот прогнозов toomake кода hello и построения hello ROC кривой.</span><span class="sxs-lookup"><span data-stu-id="2aea4-320">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
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


<span data-ttu-id="2aea4-321">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-321">**OUTPUT**</span></span>

![Кривая ROC логистической регрессии для универсального подхода](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="2aea4-323">**Сохранение модели в большом двоичном объекте для последующего использования**</span><span class="sxs-lookup"><span data-stu-id="2aea4-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="2aea4-324">Hello кода в этом разделе показано, как модели логистической регрессии hello toosave для потребления.</span><span class="sxs-lookup"><span data-stu-id="2aea4-324">hello code in this section shows how toosave hello logistic regression model for consumption.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="2aea4-325">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-325">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-326">Время, затраченное tooexecute над ячейкой: 34.57 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-326">Time taken tooexecute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="2aea4-327">Использование функции конвейера MLlib CrossValidator с моделью LogisticRegression (эластичная регрессия)</span><span class="sxs-lookup"><span data-stu-id="2aea4-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="2aea4-328">Hello кода в этом разделе показано, как tootrain, оценки и сохранить модель логистической регрессии с [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , прогнозирует ли совет получает оплату за маршрут в наборе данных маршрута и тариф авиакомпании такси hello NYC.</span><span class="sxs-lookup"><span data-stu-id="2aea4-328">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="2aea4-329">Hello модель обучается перекрестной проверки (CV) и hyperparameter свертки реализованы с hello функция MLlib CrossValidator конвейера для CV с очистку параметров.</span><span class="sxs-lookup"><span data-stu-id="2aea4-329">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with hello MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="2aea4-330">Hello выполнение этого кода MLlib CV может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2aea4-330">hello execution of this MLlib CV code can take several minutes.</span></span>
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="2aea4-331">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-331">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-332">Время, затраченное tooexecute над ячейкой: 107.98 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-332">Time taken tooexecute above cell: 107.98 seconds</span></span>

<span data-ttu-id="2aea4-333">**Отобразите hello ROC кривой.**</span><span class="sxs-lookup"><span data-stu-id="2aea4-333">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="2aea4-334">Hello *predictionAndLabelsDF* регистрируется как таблица, *tmp_results*, в предыдущую ячейку hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-334">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="2aea4-335">*tmp_results* можно использовать toodo запросов и выводить результаты в hello sqlResults-кадра данных для отображения на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="2aea4-335">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="2aea4-336">Ниже приведен код hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-336">Here is hello code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="2aea4-337">Вот hello кода tooplot hello ROC кривой.</span><span class="sxs-lookup"><span data-stu-id="2aea4-337">Here is hello code tooplot hello ROC curve.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
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


<span data-ttu-id="2aea4-338">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-338">**OUTPUT**</span></span>

![Кривая ROC логистической регрессии с использованием MLlib CrossValidator](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="2aea4-340">Классификация случайного леса</span><span class="sxs-lookup"><span data-stu-id="2aea4-340">Random forest classification</span></span>
<span data-ttu-id="2aea4-341">Hello кода в этом разделе показано, как tootrain, оценки и сохранить регрессии случайного леса, которая прогнозирует, оплачивается ли подсказка для обработки в hello NYC такси маршрута и тариф авиакомпании набора данных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-341">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRING TREES
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


<span data-ttu-id="2aea4-342">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-342">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-343">Area under ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="2aea4-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="2aea4-344">Время, затраченное tooexecute над ячейкой: 26.72 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-344">Time taken tooexecute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="2aea4-345">Классификация с применением модели градиентного бустинга деревьев</span><span class="sxs-lookup"><span data-stu-id="2aea4-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="2aea4-346">Hello кода в этом разделе описывается, как tootrain, оценки и сохранить градиента подъема дерева модели, которая прогнозирует, оплачивается ли подсказка для обработки в hello NYC такси маршрута и тариф авиакомпании набора данных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-346">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
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

<span data-ttu-id="2aea4-347">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-347">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-348">Area under ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="2aea4-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="2aea4-349">Время, затраченное tooexecute над ячейкой: 28.13 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-349">Time taken tooexecute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="2aea4-350">Прогнозирование суммы чаевых с помощью моделей регрессии (без использования перекрестной проверки)</span><span class="sxs-lookup"><span data-stu-id="2aea4-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="2aea4-351">В этом разделе показано, как использование трех моделей для регрессии задачу hello: прогнозирования hello совет оплаты такси поездки, на основе других функций подсказки.</span><span class="sxs-lookup"><span data-stu-id="2aea4-351">This section shows how use three models for hello regression task: predict hello tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="2aea4-352">Hello модели представлены являются:</span><span class="sxs-lookup"><span data-stu-id="2aea4-352">hello models presented are:</span></span>

* <span data-ttu-id="2aea4-353">регуляризованная линейная регрессия;</span><span class="sxs-lookup"><span data-stu-id="2aea4-353">Regularized linear regression</span></span>
* <span data-ttu-id="2aea4-354">случайный лес;</span><span class="sxs-lookup"><span data-stu-id="2aea4-354">Random forest</span></span>
* <span data-ttu-id="2aea4-355">градиентный бустинг деревьев.</span><span class="sxs-lookup"><span data-stu-id="2aea4-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="2aea4-356">Эти модели был описан в введение hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-356">These models were described in hello introduction.</span></span> <span data-ttu-id="2aea4-357">Процесс создания модели состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="2aea4-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="2aea4-358">**Обучение модели** с использованием данных с одним набором параметров.</span><span class="sxs-lookup"><span data-stu-id="2aea4-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="2aea4-359">**Оценка модели** на основе набора тестовых данных с метриками.</span><span class="sxs-lookup"><span data-stu-id="2aea4-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="2aea4-360">**Сохранение модели** в большом двоичном объекте для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="2aea4-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="2aea4-361">AZURE Примечание: Перекрестная проверка не используется с hello три модели регрессии в этом разделе, так как это было показано в подробные данные для модели логистической регрессии hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-361">AZURE NOTE: Cross-validation is not used with hello three regression models in this section, since this was shown in detail for hello logistic regression models.</span></span> <span data-ttu-id="2aea4-362">Пример, показывающий, как toouse CV со эластичной Net для линейной регрессии предоставляется в hello приложение этого раздела.</span><span class="sxs-lookup"><span data-stu-id="2aea4-362">An example showing how toouse CV with Elastic Net for linear regression is provided in hello Appendix of this topic.</span></span>
> 
> <span data-ttu-id="2aea4-363">AZURE Примечание: Наш опыт показывает, могут возникать проблемы с последующим согласованием LinearRegressionWithSGD моделей и параметры должны toobe изменен или оптимизированное тщательно для получения модели.</span><span class="sxs-lookup"><span data-stu-id="2aea4-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="2aea4-364">Проблему конвергенции можно решить, выполнив масштабирование переменных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="2aea4-365">Эластичный net регрессии, как показано в разделе toothis приложение hello, можно также использовать вместо LinearRegressionWithSGD.</span><span class="sxs-lookup"><span data-stu-id="2aea4-365">Elastic net regression, shown in hello Appendix toothis topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="2aea4-366">Линейная регрессия с применением SGD</span><span class="sxs-lookup"><span data-stu-id="2aea4-366">Linear regression with SGD</span></span>
<span data-ttu-id="2aea4-367">Hello кода в этом разделе показано, как toouse масштабировать tootrain функции линейной регрессии, который использует вероятностный градиентный спуск (SGD) для оптимизации, и как tooscore, оценки и сохранить модель hello в хранилище больших двоичных объектов Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="2aea4-367">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="2aea4-368">Наш опыт показывает могут возникать проблемы с последующим согласованием hello LinearRegressionWithSGD моделей и параметры должны toobe изменен или оптимизированное тщательно для получения модели.</span><span class="sxs-lookup"><span data-stu-id="2aea4-368">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="2aea4-369">Проблему конвергенции можно решить, выполнив масштабирование переменных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

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

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="2aea4-370">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-370">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span><span class="sxs-lookup"><span data-stu-id="2aea4-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="2aea4-372">Intercept: 0.854507624459</span><span class="sxs-lookup"><span data-stu-id="2aea4-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="2aea4-373">RMSE = 1.23485131376</span><span class="sxs-lookup"><span data-stu-id="2aea4-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="2aea4-374">R-sqr = 0.597963951127</span><span class="sxs-lookup"><span data-stu-id="2aea4-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="2aea4-375">Время, затраченное tooexecute над ячейкой: 38.62 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-375">Time taken tooexecute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="2aea4-376">Регрессия с использованием модели случайного леса</span><span class="sxs-lookup"><span data-stu-id="2aea4-376">Random Forest regression</span></span>
<span data-ttu-id="2aea4-377">Hello кода в этом разделе показано, как tootrain, оценки и сохранить случайного леса модель, прогнозирующая объем подсказки для hello NYC такси обработки данных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-377">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts tip amount for hello NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="2aea4-378">В приложение hello предоставляется перекрестной проверки с параметром широкими с использованием пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="2aea4-378">Cross-validation with parameter sweeping using custom code is provided in hello appendix.</span></span>
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

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

<span data-ttu-id="2aea4-379">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-379">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-380">RMSE = 0.931981967875</span><span class="sxs-lookup"><span data-stu-id="2aea4-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="2aea4-381">R-sqr = 0.733445485802</span><span class="sxs-lookup"><span data-stu-id="2aea4-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="2aea4-382">Время, затраченное tooexecute над ячейкой: 25.98 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-382">Time taken tooexecute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="2aea4-383">Регрессия с применением градиентного бустинга деревьев</span><span class="sxs-lookup"><span data-stu-id="2aea4-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="2aea4-384">Hello кода в этом разделе описывается, как tootrain, оценки и сохранить градиента повышения деревьев модель, прогнозирующая объем подсказки для hello NYC такси обработки данных.</span><span class="sxs-lookup"><span data-stu-id="2aea4-384">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="2aea4-385">**Обучение и анализ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-385">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2aea4-386">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-386">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-387">RMSE = 0.928172197114</span><span class="sxs-lookup"><span data-stu-id="2aea4-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="2aea4-388">R-sqr = 0.732680354389</span><span class="sxs-lookup"><span data-stu-id="2aea4-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="2aea4-389">Время, затраченное tooexecute над ячейкой: 20.9 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-389">Time taken tooexecute above cell: 20.9 seconds</span></span>

<span data-ttu-id="2aea4-390">**Графическое представления**</span><span class="sxs-lookup"><span data-stu-id="2aea4-390">**Plot**</span></span>

<span data-ttu-id="2aea4-391">*tmp_results* регистрируется как таблицу Hive в предыдущую ячейку hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-391">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="2aea4-392">Результаты из таблицы hello выводятся в hello *sqlResults* кадра данных для отображения на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="2aea4-392">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="2aea4-393">Ниже приведен код hello</span><span class="sxs-lookup"><span data-stu-id="2aea4-393">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="2aea4-394">Вот hello tooplot кода hello данных с помощью сервера Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-394">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="2aea4-396">Приложение. Дополнительные задачи регрессии с использованием перекрестной проверки с перебором параметров</span><span class="sxs-lookup"><span data-stu-id="2aea4-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="2aea4-397">Это приложение содержит код отображение как CV toodo с помощью эластичных net для линейной регрессии и как CV toodo с параметром Очистка регрессии случайного леса с помощью пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="2aea4-397">This appendix contains code showing how toodo CV using Elastic net for linear regression and how toodo CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="2aea4-398">Перекрестная проверка с использованием эластичной сети для линейной регрессии</span><span class="sxs-lookup"><span data-stu-id="2aea4-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="2aea4-399">Hello кода в этом разделе показано, как toodo перекрестная проверка, с помощью net гибкому для линейной регрессии и как tooevaluate hello модели с тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="2aea4-399">hello code in this section shows how toodo cross validation using Elastic net for linear regression and how tooevaluate hello model against test data.</span></span>

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2aea4-400">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-400">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-401">Время, затраченное tooexecute над ячейкой: 161.21 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-401">Time taken tooexecute above cell: 161.21  seconds</span></span>

<span data-ttu-id="2aea4-402">**Оценка с помощью метрики R SQR**</span><span class="sxs-lookup"><span data-stu-id="2aea4-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="2aea4-403">*tmp_results* регистрируется как таблицу Hive в предыдущую ячейку hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-403">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="2aea4-404">Результаты из таблицы hello выводятся в hello *sqlResults* кадра данных для отображения на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="2aea4-404">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="2aea4-405">Ниже приведен код hello</span><span class="sxs-lookup"><span data-stu-id="2aea4-405">Here is hello code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="2aea4-406">Ниже приведен код hello toocalculate R sqr.</span><span class="sxs-lookup"><span data-stu-id="2aea4-406">Here is hello code toocalculate R-sqr.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="2aea4-407">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-407">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-408">R-sqr = 0.619184907088</span><span class="sxs-lookup"><span data-stu-id="2aea4-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="2aea4-409">Перекрестная проверка с перебором параметров с использованием пользовательского кода для регрессии случайного леса</span><span class="sxs-lookup"><span data-stu-id="2aea4-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="2aea4-410">Hello кода в этом разделе показано, как toodo перекрестная проверка с помощью очистки параметров с помощью пользовательского кода для регрессии случайного леса и как tooevaluate hello модели с тестовыми данными.</span><span class="sxs-lookup"><span data-stu-id="2aea4-410">hello code in this section shows how toodo cross validation with parameter sweep using custom code for random forest regression and how tooevaluate hello model against test data.</span></span>

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2aea4-411">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-411">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-412">RMSE = 0.906972198262</span><span class="sxs-lookup"><span data-stu-id="2aea4-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="2aea4-413">R-sqr = 0.740751197012</span><span class="sxs-lookup"><span data-stu-id="2aea4-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="2aea4-414">Время, затраченное tooexecute над ячейкой: 69.17 секунд</span><span class="sxs-lookup"><span data-stu-id="2aea4-414">Time taken tooexecute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="2aea4-415">Очистка объектов из памяти и вывод расположений моделей</span><span class="sxs-lookup"><span data-stu-id="2aea4-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="2aea4-416">Используйте `unpersist()` toodelete объектов в кэше в памяти.</span><span class="sxs-lookup"><span data-stu-id="2aea4-416">Use `unpersist()` toodelete objects cached in memory.</span></span>

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

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


<span data-ttu-id="2aea4-417">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-417">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="2aea4-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="2aea4-419">** Распечатки путь toomodel файлов toobe используется в записной книжке потребления hello.</span><span class="sxs-lookup"><span data-stu-id="2aea4-419">**Printout path toomodel files toobe used in hello consumption notebook.</span></span> <span data-ttu-id="2aea4-420">** tooconsume и оценка независимой-набор данных, нужно toocopy и вставьте эти имена файлов в hello «Потребления ноутбук».</span><span class="sxs-lookup"><span data-stu-id="2aea4-420">** tooconsume and score an independent data-set, you need toocopy and paste these file names in hello "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="2aea4-421">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2aea4-421">**OUTPUT**</span></span>

<span data-ttu-id="2aea4-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="2aea4-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="2aea4-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="2aea4-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="2aea4-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="2aea4-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="2aea4-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="2aea4-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="2aea4-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="2aea4-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="2aea4-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="2aea4-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="2aea4-428">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="2aea4-428">What's next?</span></span>
<span data-ttu-id="2aea4-429">Теперь после создания модели регрессии и классификации с hello Spark MlLib, готовы toolearn, как tooscore и оценивать эти модели.</span><span class="sxs-lookup"><span data-stu-id="2aea4-429">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span>

<span data-ttu-id="2aea4-430">**Модели потребления:** toolearn как tooscore и оценить hello классификационных и регрессионных моделей, созданных в этом разделе см. в разделе [оценка и оценки моделей построен Spark машинного обучения](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="2aea4-430">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

