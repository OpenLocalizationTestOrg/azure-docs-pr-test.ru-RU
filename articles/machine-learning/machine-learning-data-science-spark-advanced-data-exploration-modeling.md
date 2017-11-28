---
title: "Расширенное исследование и моделирование данных с помощью Spark | Документация Майкрософт"
description: "Используйте кластер HDInsight Spark для анализа данных, обучения бинарной классификации и моделей регрессии; при этом используются перекрестная проверка и оптимизация гиперпараметров."
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
ms.openlocfilehash: e6bf6bd3c905f077841ef166540337a251b91ad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="2f194-103">Расширенное исследование и моделирование данных с помощью Spark</span><span class="sxs-lookup"><span data-stu-id="2f194-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="2f194-104">В этом пошаговом руководстве рассматривается исследование, обучение бинарной классификации и моделей регрессии; при этом используются перекрестная проверка и оптимизация гиперпараметров для обучения моделей на примере набора данных о поездках в такси по Нью-Йорку и тарифах за 2013 г. с помощью HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="2f194-104">This walkthrough uses HDInsight Spark to do data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of the NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="2f194-105">Здесь также подробно описаны этапы [анализа и обработки данных](http://aka.ms/datascienceprocess) с использованием кластера HDInsight Spark по обработке данных и больших двоичных объектов Azure для хранения данных и моделей.</span><span class="sxs-lookup"><span data-stu-id="2f194-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="2f194-106">В ходе этой процедуры данные из большого двоичного объекта службы хранилища Azure сначала исследуются и визуализируются, а затем подготавливаются для создания прогнозных моделей.</span><span class="sxs-lookup"><span data-stu-id="2f194-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="2f194-107">Чтобы создать код решения и составить соответствующие графики, использовался язык Python.</span><span class="sxs-lookup"><span data-stu-id="2f194-107">Python has been used to code the solution and to show the relevant plots.</span></span> <span data-ttu-id="2f194-108">Эти модели создаются с помощью набора средств Spark MLlib для выполнения задач двоичной классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="2f194-108">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="2f194-109">Задача **двоичной классификации** : спрогнозировать, будут ли выплачены чаевые за поездку.</span><span class="sxs-lookup"><span data-stu-id="2f194-109">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="2f194-110">Задача **регрессии** : спрогнозировать сумму чаевых в зависимости от других признаков.</span><span class="sxs-lookup"><span data-stu-id="2f194-110">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="2f194-111">Здесь также содержатся примеры кода, демонстрирующие процесс обучения, анализа и сохранения модели каждого типа.</span><span class="sxs-lookup"><span data-stu-id="2f194-111">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="2f194-112">В этой статье рассматриваются некоторые из основ, описанные в статье [Исследование и моделирование данных с помощью Spark](machine-learning-data-science-spark-data-exploration-modeling.md).</span><span class="sxs-lookup"><span data-stu-id="2f194-112">The topic covers some of the same ground as the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="2f194-113">Но эта публикация более расширенная, так как в ней также используется перекрестная проверка с перебором гиперпараметров для обучения оптимально точных моделей классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="2f194-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping to train optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="2f194-114">**Перекрестная проверка** — это метод, который оценивает, насколько хорошо модель, обученная на известном наборе данных, обобщается для прогнозирования характеристик наборов данных, на которых она не прошла обучение.</span><span class="sxs-lookup"><span data-stu-id="2f194-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes to predicting the features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="2f194-115">Здесь используется распространенная реализация, разделяющая набор данных на K сверток и затем обучающая модель путем циклического перебора по всем сверткам, кроме одной.</span><span class="sxs-lookup"><span data-stu-id="2f194-115">A common implementation used here is to divide a dataset into K folds and then train the model in a round-robin fashion on all but one of the folds.</span></span> <span data-ttu-id="2f194-116">Оценивается умение модели точно прогнозировать, когда проверенный независимый набор данных в этой свертке не используется для обучения модели.</span><span class="sxs-lookup"><span data-stu-id="2f194-116">The ability of the model to prediction accurately when tested against the independent dataset in this fold not used to train the model is assessed.</span></span>

<span data-ttu-id="2f194-117">**Оптимизация гиперпараметров** — это задача выбора набора гиперпараметров для алгоритма обучения, обычно с целью оптимизации меры производительности алгоритма на независимом наборе данных.</span><span class="sxs-lookup"><span data-stu-id="2f194-117">**Hyperparameter optimization** is the problem of choosing a set of hyperparameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="2f194-118">**Гиперпараметры** — это значения, которые должны быть указаны за пределами процедуры обучения модели.</span><span class="sxs-lookup"><span data-stu-id="2f194-118">**Hyperparameters** are values that must be specified outside of the model training procedure.</span></span> <span data-ttu-id="2f194-119">Предположения относительно этих значений могут повлиять на гибкость и точность моделей.</span><span class="sxs-lookup"><span data-stu-id="2f194-119">Assumptions about these values can impact the flexibility and accuracy of the models.</span></span> <span data-ttu-id="2f194-120">Деревья принятия решений содержат гиперпараметры, такие как требуемая глубина и число листьев в дереве.</span><span class="sxs-lookup"><span data-stu-id="2f194-120">Decision trees have hyperparameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="2f194-121">Для методов опорных векторов (SVM) необходимо задать условие штрафа за неправильную классификацию.</span><span class="sxs-lookup"><span data-stu-id="2f194-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="2f194-122">Распространенный способ выполнения оптимизации гиперпараметров, который используется здесь, — поиск в сетке или **перебор параметров**.</span><span class="sxs-lookup"><span data-stu-id="2f194-122">A common way to perform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="2f194-123">Метод заключается в выполнении тщательного поиска по значениям указанного подмножества пространства гиперпараметров для алгоритма обучения.</span><span class="sxs-lookup"><span data-stu-id="2f194-123">This consists of performing an exhaustive search through the values a specified subset of the hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="2f194-124">Перекрестная проверка может предоставить метрику производительности, чтобы отсортировать оптимальные результаты, выданные алгоритмом поиска в сетке.</span><span class="sxs-lookup"><span data-stu-id="2f194-124">Cross validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="2f194-125">Использование перекрестной проверки с перебором гиперпараметров помогает ограничить такие проблемы, как лжевзаимосвязи модели с обучающими данными, чтобы модель сохраняла возможность применения к общему набору данных, из которого извлекаются данные для обучения.</span><span class="sxs-lookup"><span data-stu-id="2f194-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model to training data so that the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

<span data-ttu-id="2f194-126">Мы использовали такие модели, как логистическая и линейная регрессия, случайные леса и градиентный бустинг деревьев.</span><span class="sxs-lookup"><span data-stu-id="2f194-126">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="2f194-127">[Линейная регрессия с применением SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) — модель линейной регрессии, в которой используется метод стохастического градиента для оптимизации и масштабирование признаков для прогнозирования суммы чаевых.</span><span class="sxs-lookup"><span data-stu-id="2f194-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="2f194-128">[Логистическая регрессия с применением алгоритма LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) (или логит-регрессия) — регрессионная модель, которая используется для классификации данных, если зависимая переменная является категориальной.</span><span class="sxs-lookup"><span data-stu-id="2f194-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="2f194-129">Алгоритм LBFGS — это широко используемый в машинном обучении квазиньютоновский алгоритм оптимизации, который представляет собой модифицированный метод Бройдена — Флетчера — Гольдфарба — Шанно (BFGS) с ограниченным использованием компьютерной памяти.</span><span class="sxs-lookup"><span data-stu-id="2f194-129">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="2f194-130">[Случайные леса](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="2f194-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="2f194-131">Такие совокупности минимизируют необходимость в переобучении.</span><span class="sxs-lookup"><span data-stu-id="2f194-131">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="2f194-132">Случайные леса используются для регрессии и классификации, могут обрабатывать категориальные функции и могут быть расширены до многоклассовой настройки классификации.</span><span class="sxs-lookup"><span data-stu-id="2f194-132">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="2f194-133">С их помощью можно определять нелинейные зависимости и взаимодействия признаков. Этот метод не требует масштабирования признаков.</span><span class="sxs-lookup"><span data-stu-id="2f194-133">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="2f194-134">Случайные леса — одна из самых эффективных моделей машинного обучения для задач классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="2f194-134">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="2f194-135">[Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="2f194-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="2f194-136">Этот метод предусматривает итеративное обучение деревьев принятия решений, что позволяет свести потери к минимуму.</span><span class="sxs-lookup"><span data-stu-id="2f194-136">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="2f194-137">Он применяется для задач классификации и регрессии. С его помощью можно обрабатывать категориальные признаки, а также определять нелинейные зависимости и взаимодействия признаков. Этот метод не требует масштабирования признаков.</span><span class="sxs-lookup"><span data-stu-id="2f194-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="2f194-138">Кроме того, его можно использовать для создания модели мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="2f194-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="2f194-139">Примеры моделирования с использованием перекрестной проверки и перебора гиперпараметров показаны для задачи двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="2f194-139">Modeling examples using CV and Hyperparameter sweep are shown for the binary classification problem.</span></span> <span data-ttu-id="2f194-140">Более простые примеры (без перебора параметров) представлены в основной статье о задачах регрессии.</span><span class="sxs-lookup"><span data-stu-id="2f194-140">Simpler examples (without parameter sweeps) are presented in the main topic for regression tasks.</span></span> <span data-ttu-id="2f194-141">Однако в приложении также представлена проверка с использованием эластичной сети для линейной регрессии и перекрестной проверки с перебором параметров для регрессии случайного леса.</span><span class="sxs-lookup"><span data-stu-id="2f194-141">But in the appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="2f194-142">**Эластичная сеть** — это метод регуляризованной регрессии для подгонки моделей линейной регрессии, которые линейно объединяют метрики L1 и L2 в качестве штрафов методов [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) и [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization).</span><span class="sxs-lookup"><span data-stu-id="2f194-142">The **elastic net** is a regularized regression method for fitting linear regression models that linearly combines the L1 and L2 metrics as penalties of the [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="2f194-143">Несмотря на то что набор средств Spark MLlib предназначен для работы с большими наборами данных, для удобства мы будем использовать относительно небольшую выборку (приблизительно 30 МБ, 170 тыс. строк, примерно 0,1 % исходного набора данных о поездках в такси по Нью-Йорку).</span><span class="sxs-lookup"><span data-stu-id="2f194-143">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="2f194-144">Описанные в этой статье задачи можно эффективно выполнить (примерно за 10 минут) в кластере HDInsight с 2 рабочими узлами.</span><span class="sxs-lookup"><span data-stu-id="2f194-144">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="2f194-145">Тот же код (с незначительными изменениями) можно использовать для обработки больших наборов данных. Необходимо лишь внести соответствующие изменения для кэширования данных в памяти или изменения размера кластера.</span><span class="sxs-lookup"><span data-stu-id="2f194-145">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="2f194-146">Настройка: кластеры и записные книжки Spark</span><span class="sxs-lookup"><span data-stu-id="2f194-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="2f194-147">Действия по настройке и код, указанные в этом пошаговом руководстве, применимы к использованию для HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="2f194-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="2f194-148">Но записные книжки Jupyter можно использовать для кластеров HDInsight Spark 1.6 и Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="2f194-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="2f194-149">Описание записных книжек и ссылки на них вы можете найти в файле [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) для репозитория GitHub с записными книжками.</span><span class="sxs-lookup"><span data-stu-id="2f194-149">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="2f194-150">Более того, код здесь и в связанных записных книжках является универсальным и должен работать в любом кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="2f194-150">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="2f194-151">Действия по настройке кластера и управлению им могут немного отличаться от приведенных здесь, если вы не используете HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="2f194-151">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="2f194-152">Для удобства мы приводим ссылки на записные книжки Jupyter для Spark 1.6 и 2.0, которые можно выполнять в ядре pyspark на сервере Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="2f194-152">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 and 2.0 to be run in the pyspark kernel of the Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="2f194-153">Записные книжки для Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="2f194-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="2f194-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb). Содержит разделы в записной книжке №1 и варианты моделей с использованием настройки гиперпараметров и перекрестной проверки.</span><span class="sxs-lookup"><span data-stu-id="2f194-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="2f194-155">Записные книжки для Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="2f194-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="2f194-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb). Содержит сведения о том, как выполнять просмотр данных, моделирование и оценку в кластерах Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="2f194-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="2f194-157">Настройка места хранения, библиотек и предустановленного контекста Spark</span><span class="sxs-lookup"><span data-stu-id="2f194-157">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="2f194-158">Spark может считывать данные и записывать их в хранилище BLOB-объектов Azure (также известное как WASB).</span><span class="sxs-lookup"><span data-stu-id="2f194-158">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="2f194-159">Таким образом, данные из хранилища можно обрабатывать с помощью Spark и сохранять полученные данные в этом же хранилище.</span><span class="sxs-lookup"><span data-stu-id="2f194-159">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="2f194-160">Чтобы сохранить модели или файлы в хранилище BLOB-объектов, необходимо указать путь соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="2f194-160">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="2f194-161">Контейнер по умолчанию, присоединенный к кластеру Spark, можно указать с помощью пути, который начинается с "wasb:///".</span><span class="sxs-lookup"><span data-stu-id="2f194-161">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="2f194-162">Другие расположения начинаются с wasb://.</span><span class="sxs-lookup"><span data-stu-id="2f194-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="2f194-163">Настройка путей каталога к месту хранения в хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="2f194-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="2f194-164">В следующем примере кода указывается расположение данных, которые необходимо считать, и путь для каталога хранилища модели, где сохраняются выходные данные модели:</span><span class="sxs-lookup"><span data-stu-id="2f194-164">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="2f194-165">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-165">**OUTPUT**</span></span>

<span data-ttu-id="2f194-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="2f194-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="2f194-167">Импорт библиотек</span><span class="sxs-lookup"><span data-stu-id="2f194-167">Import libraries</span></span>
<span data-ttu-id="2f194-168">Импортируйте необходимые библиотеки, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="2f194-168">Import necessary libraries with the following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="2f194-169">Предустановленный контекст Spark и волшебные команды PySpark</span><span class="sxs-lookup"><span data-stu-id="2f194-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="2f194-170">Ядра PySpark, входящие в состав записных книжек Jupyter, имеют предустановленный контекст.</span><span class="sxs-lookup"><span data-stu-id="2f194-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="2f194-171">Поэтому перед началом работы с разрабатываемым приложением вам не нужно явно задавать контексты Spark или Hive.</span><span class="sxs-lookup"><span data-stu-id="2f194-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="2f194-172">Эти контексты доступны вам по умолчанию,</span><span class="sxs-lookup"><span data-stu-id="2f194-172">These contexts are available for you by default.</span></span> <span data-ttu-id="2f194-173">а именно:</span><span class="sxs-lookup"><span data-stu-id="2f194-173">These contexts are:</span></span>

* <span data-ttu-id="2f194-174">sc для Spark;</span><span class="sxs-lookup"><span data-stu-id="2f194-174">sc - for Spark</span></span> 
* <span data-ttu-id="2f194-175">sqlContext для Hive.</span><span class="sxs-lookup"><span data-stu-id="2f194-175">sqlContext - for Hive</span></span>

<span data-ttu-id="2f194-176">Ядро PySpark предоставляет несколько "волшебных команд". Это специальные команды, которые можно вызывать с %%.</span><span class="sxs-lookup"><span data-stu-id="2f194-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="2f194-177">В этих примерах кода используются две подобные команды.</span><span class="sxs-lookup"><span data-stu-id="2f194-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="2f194-178">**%%local** Указывает, что код в последующих строках будет выполнен локально.</span><span class="sxs-lookup"><span data-stu-id="2f194-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="2f194-179">В качестве кода должен быть указан корректный код Python.</span><span class="sxs-lookup"><span data-stu-id="2f194-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="2f194-180">**%%sql -o <variable name>** Выполняет запрос Hive к sqlContext.</span><span class="sxs-lookup"><span data-stu-id="2f194-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="2f194-181">Если передан параметр -o, результат запроса сохраняется в контексте %%local Python в формате Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="2f194-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="2f194-182">Дополнительные сведения о ядрах для записных книжек Jupyter и предустановленных "волшебных командах", которые они предоставляют, см. в статье [Ядра, доступные для использования записными книжками Jupyter с кластерами Apache Spark в HDInsight на платформе Linux](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="2f194-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="2f194-183">Прием данных из открытого большого двоичного объекта:</span><span class="sxs-lookup"><span data-stu-id="2f194-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="2f194-184">Чтобы начать анализ и обработку необходимых данных, требуется переместить их из источников, в которых они находятся, в среду исследования и моделирования данных.</span><span class="sxs-lookup"><span data-stu-id="2f194-184">The first step in the data science process is to ingest the data to be analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="2f194-185">В нашем пошаговом руководстве — это среда Spark.</span><span class="sxs-lookup"><span data-stu-id="2f194-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="2f194-186">Этот раздел содержит код, с помощью которого можно выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2f194-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="2f194-187">прием выборки данных, которые нужно моделировать;</span><span class="sxs-lookup"><span data-stu-id="2f194-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="2f194-188">считывание входного набора данных (TSV-файл);</span><span class="sxs-lookup"><span data-stu-id="2f194-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="2f194-189">форматирование и очистка данных;</span><span class="sxs-lookup"><span data-stu-id="2f194-189">format and clean the data</span></span>
* <span data-ttu-id="2f194-190">создание и кэширование объектов (устойчивых распределенных наборов данных или фреймов данных) в памяти;</span><span class="sxs-lookup"><span data-stu-id="2f194-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="2f194-191">регистрация данных в качестве временной таблицы в контексте SQL.</span><span class="sxs-lookup"><span data-stu-id="2f194-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="2f194-192">Ниже приведен код для приема данных.</span><span class="sxs-lookup"><span data-stu-id="2f194-192">Here is the code for data ingestion.</span></span>

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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES THE DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2f194-193">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-193">**OUTPUT**</span></span>

<span data-ttu-id="2f194-194">Время на выполнение кода выше: 276,62 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-194">Time taken to execute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="2f194-195">Исследование и визуализация данных</span><span class="sxs-lookup"><span data-stu-id="2f194-195">Data exploration & visualization</span></span>
<span data-ttu-id="2f194-196">После помещения данных в Spark необходимо исследовать и визуализировать их, чтобы получить более глубокое представление.</span><span class="sxs-lookup"><span data-stu-id="2f194-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="2f194-197">В этом разделе мы исследуем данные о поездках в такси с помощью SQL-запросов и составим графики целевых переменных и потенциальных признаков для визуального контроля.</span><span class="sxs-lookup"><span data-stu-id="2f194-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="2f194-198">В частности, мы составим график частоты поездок в такси, частоты оставления чаевых и зависимости суммы чаевых от тарифа и типа платежа.</span><span class="sxs-lookup"><span data-stu-id="2f194-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="2f194-199">Построение гистограммы количества пассажиров в выборке данных о поездках на такси</span><span class="sxs-lookup"><span data-stu-id="2f194-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="2f194-200">Этот код и последующие фрагменты используют волшебную команду SQL для запроса примера и локальную волшебную команду для графического представления данных.</span><span class="sxs-lookup"><span data-stu-id="2f194-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="2f194-201">**SQL magic (`%%sql`)** Ядро HDInsight PySpark позволяет легко выполнять встроенные запросы HiveQL к sqlContext.</span><span class="sxs-lookup"><span data-stu-id="2f194-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="2f194-202">Аргумент (-o VARIABLE_NAME) сохраняет выходные данные запроса SQL в формате Pandas DataFrame на сервере Jupyter.</span><span class="sxs-lookup"><span data-stu-id="2f194-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="2f194-203">Это означает, что они доступны в локальном режиме.</span><span class="sxs-lookup"><span data-stu-id="2f194-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="2f194-204">Магическая команда **`%%local`** используется для локального выполнения кода на сервере Jupyter, который представляет собой головной узел кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2f194-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="2f194-205">Как правило, используется команда magic `%%local` после запуска команды magic `%%sql -o` для выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="2f194-205">Typically, you use `%%local` magic after the `%%sql -o` magic is used to run a query.</span></span> <span data-ttu-id="2f194-206">Параметр -o сохранит выходные данные запроса SQL локально.</span><span class="sxs-lookup"><span data-stu-id="2f194-206">The -o parameter would persist the output of the SQL query locally.</span></span> <span data-ttu-id="2f194-207">Затем команда magic `%%local` активирует следующий набор фрагментов кода для локального выполнения в выходных данных запроса SQL, который сохранен локально.</span><span class="sxs-lookup"><span data-stu-id="2f194-207">Then the `%%local` magic triggers the next set of code snippets to run locally against the output of the SQL queries that has been persisted locally.</span></span> <span data-ttu-id="2f194-208">После выполнения кода выходные данные визуализируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="2f194-208">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="2f194-209">Этот запрос извлекает поездки по количеству пассажиров.</span><span class="sxs-lookup"><span data-stu-id="2f194-209">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="2f194-210">Этот код создает локальный фрейм данных из выходных данных запроса и формирует графическое представление данных.</span><span class="sxs-lookup"><span data-stu-id="2f194-210">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="2f194-211">Магическая команда `%%local` создает локальный кадр данных `sqlResults`, который можно использовать для формирования графического представления данных с помощью matplotlib.</span><span class="sxs-lookup"><span data-stu-id="2f194-211">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="2f194-212">В этом пошаговом руководстве волшебная команда PySpark используется несколько раз.</span><span class="sxs-lookup"><span data-stu-id="2f194-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="2f194-213">Если объем данных большой, сделайте выборку, чтобы создать фрейм данных, который можно разместить в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="2f194-213">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="2f194-214">Код для получения графического представления поездок по числу пассажиров</span><span class="sxs-lookup"><span data-stu-id="2f194-214">Here is the code to plot the trips by passenger counts</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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

<span data-ttu-id="2f194-215">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-215">**OUTPUT**</span></span>

![Частота поездок в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="2f194-217">С помощью кнопок в меню **Тип** в записной книжке можно выбрать один из нескольких типов визуализации (таблица либо круговая, линейная, комбинированная или столбчатая диаграмма).</span><span class="sxs-lookup"><span data-stu-id="2f194-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="2f194-218">Здесь показано представление столбчатой диаграммы.</span><span class="sxs-lookup"><span data-stu-id="2f194-218">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="2f194-219">Построение гистограммы суммы чаевых и ее зависимости от количества пассажиров и тарифа.</span><span class="sxs-lookup"><span data-stu-id="2f194-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="2f194-220">Используйте SQL-запрос для выборки данных.</span><span class="sxs-lookup"><span data-stu-id="2f194-220">Use a SQL query to sample data..</span></span>

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


<span data-ttu-id="2f194-221">В этой ячейке кода используется SQL-запрос для формирования трех видов графического представления данных.</span><span class="sxs-lookup"><span data-stu-id="2f194-221">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="2f194-222">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="2f194-222">**OUTPUT:**</span></span> 

![Распределение суммы чаевых](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Сумма чаевых в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Сумма чаевых в зависимости от тарифа](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="2f194-226">Проектирование признаков, преобразование и подготовка данных к моделированию</span><span class="sxs-lookup"><span data-stu-id="2f194-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="2f194-227">В этом разделе приведен пример кода для выполнения процедур по подготовке данных, которые будут использоваться в моделях машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="2f194-227">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="2f194-228">Здесь также показано, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2f194-228">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="2f194-229">Создание нового признака путем секционирования часов в ячейки трафика.</span><span class="sxs-lookup"><span data-stu-id="2f194-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="2f194-230">Индексация и прямое кодирование категориальных признаков</span><span class="sxs-lookup"><span data-stu-id="2f194-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="2f194-231">Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения</span><span class="sxs-lookup"><span data-stu-id="2f194-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="2f194-232">создание случайной вложенной выборки данных и ее разделение на наборы для обучения и тестирования;</span><span class="sxs-lookup"><span data-stu-id="2f194-232">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="2f194-233">масштабирование признаков;</span><span class="sxs-lookup"><span data-stu-id="2f194-233">Feature scaling</span></span>
* <span data-ttu-id="2f194-234">кэширование объектов в памяти.</span><span class="sxs-lookup"><span data-stu-id="2f194-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="2f194-235">Создание нового признака путем секционирования часов трафика в ячейки.</span><span class="sxs-lookup"><span data-stu-id="2f194-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="2f194-236">В следующем коде показано, как создать признак методом секционирования часов в ячейки трафика, а затем кэшировать итоговый фрейм данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="2f194-236">This code shows how to create a new feature by partitioning traffic times into bins and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="2f194-237">Если устойчивые распределенные наборы данных и фреймы данных используются постоянно, на их кэширование необходимо меньше времени.</span><span class="sxs-lookup"><span data-stu-id="2f194-237">Caching leads to improved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="2f194-238">В этом пошаговом руководстве процесс кэширования существующих данных выполняется в несколько этапов.</span><span class="sxs-lookup"><span data-stu-id="2f194-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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

<span data-ttu-id="2f194-239">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-239">**OUTPUT**</span></span>

<span data-ttu-id="2f194-240">126 050.</span><span class="sxs-lookup"><span data-stu-id="2f194-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="2f194-241">Индексация и прямое кодирование категориальных признаков</span><span class="sxs-lookup"><span data-stu-id="2f194-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="2f194-242">В этом разделе показано, как индексировать и кодировать категориальные признаки в качестве ввода для функций моделирования.</span><span class="sxs-lookup"><span data-stu-id="2f194-242">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="2f194-243">Перед использованием в функциях моделирования и прогнозирования MLlib категориальные входные данные сначала необходимо проиндексировать или закодировать.</span><span class="sxs-lookup"><span data-stu-id="2f194-243">The modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior to use.</span></span> 

<span data-ttu-id="2f194-244">В зависимости от модели этот процесс происходит по-разному.</span><span class="sxs-lookup"><span data-stu-id="2f194-244">Depending on the model, you need to index or encode them in different ways.</span></span> <span data-ttu-id="2f194-245">Скажем, для моделей логистической и линейной регрессии требуется прямое кодирование, при котором, например, признак с тремя категориями можно разделить на три столбца признаков, в каждом из которых в зависимости от категории наблюдения содержатся значения 0 или 1.</span><span class="sxs-lookup"><span data-stu-id="2f194-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="2f194-246">Для этого можно использовать функцию [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) в MLlib.</span><span class="sxs-lookup"><span data-stu-id="2f194-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="2f194-247">Этот кодировщик сопоставляет столбец с индексами меток со столбцом двоичных векторов как минимум с одним отдельным значением.</span><span class="sxs-lookup"><span data-stu-id="2f194-247">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="2f194-248">Благодаря этой кодировке алгоритмы, для которых необходимы признаки с числовыми значениями (например, логистическая регрессия), можно применять к категориальным признакам.</span><span class="sxs-lookup"><span data-stu-id="2f194-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="2f194-249">Ниже приведен пример кода, с помощью которого можно проиндексировать и закодировать категориальные признаки.</span><span class="sxs-lookup"><span data-stu-id="2f194-249">Here is the code to index and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

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


<span data-ttu-id="2f194-250">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-250">**OUTPUT**</span></span>

<span data-ttu-id="2f194-251">Время на выполнение кода выше: 3,14 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-251">Time taken to execute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="2f194-252">Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения</span><span class="sxs-lookup"><span data-stu-id="2f194-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="2f194-253">Этот раздел содержит код, который показывает, как индексировать категориальные текстовые данные в виде типа данных с меткой и как их кодировать.</span><span class="sxs-lookup"><span data-stu-id="2f194-253">This section contains code that shows how to index categorical text data as a labeled point data type and how to encode it.</span></span> <span data-ttu-id="2f194-254">Этот код подготавливает данные для обучения и тестирования логистической регрессии MLlib и других моделей классификации.</span><span class="sxs-lookup"><span data-stu-id="2f194-254">This prepares it to be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="2f194-255">Объекты с помеченной вершиной отформатированы в устойчивые распределенные наборы данных, которые можно использовать в качестве входных для большинства алгоритмов машинного обучения в MLlib.</span><span class="sxs-lookup"><span data-stu-id="2f194-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="2f194-256">Объект [с помеченной вершиной](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) — это разреженный или плотный локальный вектор, связанный с меткой или ответом.</span><span class="sxs-lookup"><span data-stu-id="2f194-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="2f194-257">Ниже приведен пример кода, с помощью которого можно проиндексировать и закодировать текстовые характеристики бинарной классификации.</span><span class="sxs-lookup"><span data-stu-id="2f194-257">Here is the code to index and encode text features for binary classification.</span></span>

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


<span data-ttu-id="2f194-258">Ниже приведен пример кода, с помощью которого можно проиндексировать и закодировать категориальные текстовые характеристики для анализа линейной регрессии.</span><span class="sxs-lookup"><span data-stu-id="2f194-258">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="2f194-259">Создание случайной вложенной выборки данных и ее разделение на наборы для обучения и тестирования</span><span class="sxs-lookup"><span data-stu-id="2f194-259">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="2f194-260">С помощью кода в этом разделе создается случайная выборка данных (25 % всех данных).</span><span class="sxs-lookup"><span data-stu-id="2f194-260">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="2f194-261">Хотя из-за небольшого размера используемого набора данных, этот шаг выполнять необязательно, мы все равно покажем, как создавать выборку данных.</span><span class="sxs-lookup"><span data-stu-id="2f194-261">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample the data here.</span></span> <span data-ttu-id="2f194-262">Это поможет вам в случае возникновения проблем.</span><span class="sxs-lookup"><span data-stu-id="2f194-262">Then you know how to use it for your own problem if needed.</span></span> <span data-ttu-id="2f194-263">Если выборки большие, этот процесс может значительно сэкономить время обучения моделей.</span><span class="sxs-lookup"><span data-stu-id="2f194-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="2f194-264">Затем мы разобьем выборку данных на наборы для обучения (75 %) и тестирования (25 %), которые будут использоваться для двоичной классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="2f194-264">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="2f194-265">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-265">**OUTPUT**</span></span>

<span data-ttu-id="2f194-266">Время на выполнение кода выше: 0,31 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-266">Time taken to execute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="2f194-267">масштабирование признаков;</span><span class="sxs-lookup"><span data-stu-id="2f194-267">Feature scaling</span></span>
<span data-ttu-id="2f194-268">Масштабирование признаков (или нормализация данных) гарантирует, что для признаков с широко распределенными значениями не задано высокое значение веса в целевой функции.</span><span class="sxs-lookup"><span data-stu-id="2f194-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="2f194-269">В коде для масштабирования признаков используется функция [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler), которая позволяет масштабировать признаки в зависимости от изменений единицы.</span><span class="sxs-lookup"><span data-stu-id="2f194-269">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="2f194-270">MLlib предоставляет функцию StandardScaler для выполнения линейной регрессии с применением метода стохастического градиента (SGD).</span><span class="sxs-lookup"><span data-stu-id="2f194-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="2f194-271">Алгоритм SGD широко используется для обучения других моделей машинного обучения (например, регуляризованной регрессии или метода опорных векторов).</span><span class="sxs-lookup"><span data-stu-id="2f194-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="2f194-272">Алгоритм LinearRegressionWithSGD чувствителен к масштабированию признаков.</span><span class="sxs-lookup"><span data-stu-id="2f194-272">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>   
> 
> 

<span data-ttu-id="2f194-273">Ниже приведен код для масштабирования переменных, пригодный для использования с регуляризованным линейным алгоритмом с применением стохастического градиента.</span><span class="sxs-lookup"><span data-stu-id="2f194-273">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

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

<span data-ttu-id="2f194-274">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-274">**OUTPUT**</span></span>

<span data-ttu-id="2f194-275">Время на выполнение кода выше: 11,67 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-275">Time taken to execute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="2f194-276">кэширование объектов в памяти.</span><span class="sxs-lookup"><span data-stu-id="2f194-276">Cache objects in memory</span></span>
<span data-ttu-id="2f194-277">Время на обучение и тестирование алгоритмов машинного обучения можно сократить, кэшировав объекты входного фрейма данных, которые использовались в качестве масштабируемых признаков, а также признаков для классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="2f194-277">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression and, scaled features.</span></span>

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

<span data-ttu-id="2f194-278">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-278">**OUTPUT**</span></span> 

<span data-ttu-id="2f194-279">Время на выполнение кода выше: 0,13 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-279">Time taken to execute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="2f194-280">Прогнозирование вероятности выплаты чаевых за поездку с помощью моделей бинарной классификации</span><span class="sxs-lookup"><span data-stu-id="2f194-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="2f194-281">В этом разделе показано, как с помощью трех моделей для выполнения задач двоичной классификации спрогнозировать, будут ли оставлены чаевые за поездку в такси.</span><span class="sxs-lookup"><span data-stu-id="2f194-281">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="2f194-282">Мы используем следующие модели:</span><span class="sxs-lookup"><span data-stu-id="2f194-282">The models presented are:</span></span>

* <span data-ttu-id="2f194-283">Логистическая регрессия</span><span class="sxs-lookup"><span data-stu-id="2f194-283">Logistic regression</span></span> 
* <span data-ttu-id="2f194-284">Случайный лес</span><span class="sxs-lookup"><span data-stu-id="2f194-284">Random forest</span></span>
* <span data-ttu-id="2f194-285">Градиентный бустинг деревьев</span><span class="sxs-lookup"><span data-stu-id="2f194-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="2f194-286">Процесс создания модели состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="2f194-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="2f194-287">**Обучение модели** с использованием данных с одним набором параметров.</span><span class="sxs-lookup"><span data-stu-id="2f194-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="2f194-288">**Оценка модели** на основе набора тестовых данных с метриками.</span><span class="sxs-lookup"><span data-stu-id="2f194-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="2f194-289">**Сохранение модели** в большом двоичном объекте для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="2f194-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="2f194-290">Мы покажем, как выполнить перекрестную проверку с перебором параметров двумя способами:</span><span class="sxs-lookup"><span data-stu-id="2f194-290">We show how to do cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="2f194-291">С использованием **универсального** пользовательского кода, который можно применять к любому алгоритму в MLlib и к любым наборам параметров в алгоритме.</span><span class="sxs-lookup"><span data-stu-id="2f194-291">Using **generic** custom code which can be applied to any algorithm in MLlib and to any parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="2f194-292">С использованием **функции конвейера pySpark CrossValidator**.</span><span class="sxs-lookup"><span data-stu-id="2f194-292">Using the **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="2f194-293">Обратите внимание, что CrossValidator имеет несколько ограничений для Spark 1.5.0.</span><span class="sxs-lookup"><span data-stu-id="2f194-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="2f194-294">Модели конвейера не могут быть сохранены для последующей обработки.</span><span class="sxs-lookup"><span data-stu-id="2f194-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="2f194-295">Не может использоваться для каждого параметра в модели.</span><span class="sxs-lookup"><span data-stu-id="2f194-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="2f194-296">Не может использоваться для каждого алгоритма MLlib.</span><span class="sxs-lookup"><span data-stu-id="2f194-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-the-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="2f194-297">Универсальная перекрестная проверка и перебор гиперпараметров, используемые с алгоритмом логистической регрессии для двоичной классификации</span><span class="sxs-lookup"><span data-stu-id="2f194-297">Generic cross validation and hyperparameter sweeping used with the logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="2f194-298">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения модели логистической регрессии с применением [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , с помощью которой можно спрогнозировать, будут ли выплачены чаевые за поездку в такси по Нью-Йорку, на основе набора данных и тарифов.</span><span class="sxs-lookup"><span data-stu-id="2f194-298">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="2f194-299">Модель обучена с использованием перекрестной проверки и перебора гиперпараметров, реализованных в пользовательском коде, который можно применить к любому из алгоритмов обучения в MLlib.</span><span class="sxs-lookup"><span data-stu-id="2f194-299">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied to any of the learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="2f194-300">Выполнение такого пользовательского кода перекрестной проверки может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2f194-300">The execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="2f194-301">**Обучение модели логистической регрессии с использованием перекрестной проверки и перебора параметров**</span><span class="sxs-lookup"><span data-stu-id="2f194-301">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # SET NUM FOLDS AND NUM PARAMETER SETS TO SWEEP ON
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


    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2f194-302">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-302">**OUTPUT**</span></span>

<span data-ttu-id="2f194-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="2f194-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="2f194-304">Intercept: -0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="2f194-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="2f194-305">Время на выполнение кода выше: 14,43 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-305">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="2f194-306">**Оценка модели бинарной классификации со стандартными метриками**</span><span class="sxs-lookup"><span data-stu-id="2f194-306">**Evaluate the binary classification model with standard metrics**</span></span>

<span data-ttu-id="2f194-307">Код в этом разделе показывает, как оценить модель логистической регрессии по тестовому набору данных, включая построение кривой ROC.</span><span class="sxs-lookup"><span data-stu-id="2f194-307">The code in this section shows how to evaluate a logistic regression model against a test data-set, including a plot of the ROC curve.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2f194-308">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-308">**OUTPUT**</span></span>

<span data-ttu-id="2f194-309">Area under PR = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="2f194-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="2f194-310">Area under ROC = 0.983383274312</span><span class="sxs-lookup"><span data-stu-id="2f194-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="2f194-311">Summary Stats</span><span class="sxs-lookup"><span data-stu-id="2f194-311">Summary Stats</span></span>

<span data-ttu-id="2f194-312">Precision = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="2f194-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="2f194-313">Recall = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="2f194-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="2f194-314">F1 Score = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="2f194-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="2f194-315">Время на выполнение кода выше: 2,67 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-315">Time taken to execute above cell: 2.67 seconds</span></span>

<span data-ttu-id="2f194-316">**Графическое представление кривой ROC.**</span><span class="sxs-lookup"><span data-stu-id="2f194-316">**Plot the ROC curve.**</span></span>

<span data-ttu-id="2f194-317">*predictionAndLabelsDF* регистрируется как таблица (*tmp_results*) в предыдущей ячейке.</span><span class="sxs-lookup"><span data-stu-id="2f194-317">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="2f194-318">*tmp_results* может использоваться для выполнения запросов и вывода результатов во фрейм данных sqlResults для построения диаграммы.</span><span class="sxs-lookup"><span data-stu-id="2f194-318">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="2f194-319">Ниже приведен код:</span><span class="sxs-lookup"><span data-stu-id="2f194-319">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="2f194-320">Ниже приведен код для создания прогнозов и отображения кривой ROC.</span><span class="sxs-lookup"><span data-stu-id="2f194-320">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES                              
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


<span data-ttu-id="2f194-321">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-321">**OUTPUT**</span></span>

![Кривая ROC логистической регрессии для универсального подхода](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="2f194-323">**Сохранение модели в большом двоичном объекте для последующего использования**</span><span class="sxs-lookup"><span data-stu-id="2f194-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="2f194-324">Код в этом разделе показывает, как сохранить модель логистической регрессии для использования.</span><span class="sxs-lookup"><span data-stu-id="2f194-324">The code in this section shows how to save the logistic regression model for consumption.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="2f194-325">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-325">**OUTPUT**</span></span>

<span data-ttu-id="2f194-326">Время на выполнение кода выше: 34,57 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-326">Time taken to execute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="2f194-327">Использование функции конвейера MLlib CrossValidator с моделью LogisticRegression (эластичная регрессия)</span><span class="sxs-lookup"><span data-stu-id="2f194-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="2f194-328">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения модели логистической регрессии с применением [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , с помощью которой можно спрогнозировать, будут ли выплачены чаевые за поездку в такси по Нью-Йорку, на основе набора данных и тарифов.</span><span class="sxs-lookup"><span data-stu-id="2f194-328">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="2f194-329">Модель обучена с использованием перекрестной проверки и перебора гиперпараметров, реализованных с помощью функции конвейера MLlib CrossValidator для перекрестной проверки с перебором гиперпараметров.</span><span class="sxs-lookup"><span data-stu-id="2f194-329">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with the MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="2f194-330">Выполнение такого кода перекрестной проверки MLlib может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2f194-330">The execution of this MLlib CV code can take several minutes.</span></span>
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

    # CONVERT TO DATA-FRAME: THIS DOES NOT RUN ON RDDs
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="2f194-331">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-331">**OUTPUT**</span></span>

<span data-ttu-id="2f194-332">Время на выполнение кода выше: 107,98 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-332">Time taken to execute above cell: 107.98 seconds</span></span>

<span data-ttu-id="2f194-333">**Графическое представление кривой ROC.**</span><span class="sxs-lookup"><span data-stu-id="2f194-333">**Plot the ROC curve.**</span></span>

<span data-ttu-id="2f194-334">*predictionAndLabelsDF* регистрируется как таблица (*tmp_results*) в предыдущей ячейке.</span><span class="sxs-lookup"><span data-stu-id="2f194-334">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="2f194-335">*tmp_results* может использоваться для выполнения запросов и вывода результатов во фрейм данных sqlResults для построения диаграммы.</span><span class="sxs-lookup"><span data-stu-id="2f194-335">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="2f194-336">Ниже приведен код:</span><span class="sxs-lookup"><span data-stu-id="2f194-336">Here is the code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="2f194-337">Ниже приведен код для построения кривых ROC.</span><span class="sxs-lookup"><span data-stu-id="2f194-337">Here is the code to plot the ROC curve.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES 
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


<span data-ttu-id="2f194-338">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-338">**OUTPUT**</span></span>

![Кривая ROC логистической регрессии с использованием MLlib CrossValidator](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="2f194-340">Классификация случайного леса</span><span class="sxs-lookup"><span data-stu-id="2f194-340">Random forest classification</span></span>
<span data-ttu-id="2f194-341">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения регрессии случайного леса, с помощью которой можно спрогнозировать, будут ли выплачены чаевые за поездку в такси по Нью-Йорку, на основе набора данных и тарифов.</span><span class="sxs-lookup"><span data-stu-id="2f194-341">The code in this section shows how to train, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRING TREES
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


<span data-ttu-id="2f194-342">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-342">**OUTPUT**</span></span>

<span data-ttu-id="2f194-343">Area under ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="2f194-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="2f194-344">Время на выполнение кода выше: 26,72 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-344">Time taken to execute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="2f194-345">Классификация с применением модели градиентного бустинга деревьев</span><span class="sxs-lookup"><span data-stu-id="2f194-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="2f194-346">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения модели градиентного бустинга деревьев, с помощью которой можно спрогнозировать, будут ли выплачены чаевые за поездку в такси по Нью-Йорку, на основе набора данных и тарифов.</span><span class="sxs-lookup"><span data-stu-id="2f194-346">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="2f194-347">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-347">**OUTPUT**</span></span>

<span data-ttu-id="2f194-348">Area under ROC = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="2f194-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="2f194-349">Время на выполнение кода выше: 28,13 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-349">Time taken to execute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="2f194-350">Прогнозирование суммы чаевых с помощью моделей регрессии (без использования перекрестной проверки)</span><span class="sxs-lookup"><span data-stu-id="2f194-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="2f194-351">В этом разделе показано, как с помощью трех моделей регрессии спрогнозировать сумму чаевых в зависимости от других признаков.</span><span class="sxs-lookup"><span data-stu-id="2f194-351">This section shows how use three models for the regression task: predict the tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="2f194-352">Мы используем следующие модели:</span><span class="sxs-lookup"><span data-stu-id="2f194-352">The models presented are:</span></span>

* <span data-ttu-id="2f194-353">регуляризованная линейная регрессия;</span><span class="sxs-lookup"><span data-stu-id="2f194-353">Regularized linear regression</span></span>
* <span data-ttu-id="2f194-354">случайный лес;</span><span class="sxs-lookup"><span data-stu-id="2f194-354">Random forest</span></span>
* <span data-ttu-id="2f194-355">градиентный бустинг деревьев.</span><span class="sxs-lookup"><span data-stu-id="2f194-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="2f194-356">Эти модели описаны в начале статьи.</span><span class="sxs-lookup"><span data-stu-id="2f194-356">These models were described in the introduction.</span></span> <span data-ttu-id="2f194-357">Процесс создания модели состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="2f194-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="2f194-358">**Обучение модели** с использованием данных с одним набором параметров.</span><span class="sxs-lookup"><span data-stu-id="2f194-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="2f194-359">**Оценка модели** на основе набора тестовых данных с метриками.</span><span class="sxs-lookup"><span data-stu-id="2f194-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="2f194-360">**Сохранение модели** в большом двоичном объекте для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="2f194-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="2f194-361">ПРИМЕЧАНИЕ AZURE. Перекрестная проверка не используется с тремя моделями регрессии, указанными в этом разделе. Это было подробно описано в отношении моделей логистической регрессии.</span><span class="sxs-lookup"><span data-stu-id="2f194-361">AZURE NOTE: Cross-validation is not used with the three regression models in this section, since this was shown in detail for the logistic regression models.</span></span> <span data-ttu-id="2f194-362">Пример использования перекрестной проверки с эластичной сетью для линейной регрессии показан в приложении к этой статье.</span><span class="sxs-lookup"><span data-stu-id="2f194-362">An example showing how to use CV with Elastic Net for linear regression is provided in the Appendix of this topic.</span></span>
> 
> <span data-ttu-id="2f194-363">ПРИМЕЧАНИЕ AZURE. На практике в моделях LinearRegressionWithSGD часто возникают проблемы с конвергенцией. Чтобы получить допустимую модель, необходимо осторожно изменить или оптимизировать параметры.</span><span class="sxs-lookup"><span data-stu-id="2f194-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="2f194-364">Проблему конвергенции можно решить, выполнив масштабирование переменных.</span><span class="sxs-lookup"><span data-stu-id="2f194-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="2f194-365">Регрессию эластичной сети, показанную в приложении к этой статье, можно также использовать вместо LinearRegressionWithSGD.</span><span class="sxs-lookup"><span data-stu-id="2f194-365">Elastic net regression, shown in the Appendix to this topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="2f194-366">Линейная регрессия с применением метода стохастического градиента</span><span class="sxs-lookup"><span data-stu-id="2f194-366">Linear regression with SGD</span></span>
<span data-ttu-id="2f194-367">С помощью кода, приведенного в этом разделе, на основе масштабируемых признаков можно обучить модель линейной регрессии, в которой для оптимизации используется метод стохастического градиента, а также оценить, проанализировать и сохранить ее в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2f194-367">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="2f194-368">На практике в моделях LinearRegressionWithSGD часто возникают проблемы с конвергенцией. Чтобы получить допустимую модель, необходимо осторожно изменить или оптимизировать параметры.</span><span class="sxs-lookup"><span data-stu-id="2f194-368">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="2f194-369">Проблему конвергенции можно решить, выполнив масштабирование переменных.</span><span class="sxs-lookup"><span data-stu-id="2f194-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="2f194-370">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-370">**OUTPUT**</span></span>

<span data-ttu-id="2f194-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span><span class="sxs-lookup"><span data-stu-id="2f194-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="2f194-372">Intercept: 0.854507624459</span><span class="sxs-lookup"><span data-stu-id="2f194-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="2f194-373">RMSE = 1.23485131376</span><span class="sxs-lookup"><span data-stu-id="2f194-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="2f194-374">R-sqr = 0.597963951127</span><span class="sxs-lookup"><span data-stu-id="2f194-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="2f194-375">Время на выполнение кода выше: 38,62 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-375">Time taken to execute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="2f194-376">Регрессия с использованием модели случайного леса</span><span class="sxs-lookup"><span data-stu-id="2f194-376">Random Forest regression</span></span>
<span data-ttu-id="2f194-377">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения модели случайного леса, с помощью которой можно спрогнозировать суму чаевых за поездку в такси по Нью-Йорку.</span><span class="sxs-lookup"><span data-stu-id="2f194-377">The code in this section shows how to train, evaluate, and save a random forest model that predicts tip amount for the NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="2f194-378">Перекрестная проверка с перебором параметров с использованием пользовательского кода показана в приложении.</span><span class="sxs-lookup"><span data-stu-id="2f194-378">Cross-validation with parameter sweeping using custom code is provided in the appendix.</span></span>
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
    # UN-COMMENT IF YOU WANT TO PRING TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="2f194-379">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-379">**OUTPUT**</span></span>

<span data-ttu-id="2f194-380">RMSE = 0.931981967875</span><span class="sxs-lookup"><span data-stu-id="2f194-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="2f194-381">R-sqr = 0.733445485802</span><span class="sxs-lookup"><span data-stu-id="2f194-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="2f194-382">Время на выполнение кода выше: 25,98 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-382">Time taken to execute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="2f194-383">Регрессия с применением градиентного бустинга деревьев</span><span class="sxs-lookup"><span data-stu-id="2f194-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="2f194-384">Приведенный в этом разделе код предназначен для обучения, анализа и сохранения модели градиентного бустинга деревьев, с помощью которой можно спрогнозировать суму чаевых за поездку в такси по Нью-Йорку.</span><span class="sxs-lookup"><span data-stu-id="2f194-384">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="2f194-385">** Обучать и оценивать **</span><span class="sxs-lookup"><span data-stu-id="2f194-385">**Train and evaluate **</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2f194-386">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-386">**OUTPUT**</span></span>

<span data-ttu-id="2f194-387">RMSE = 0.928172197114</span><span class="sxs-lookup"><span data-stu-id="2f194-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="2f194-388">R-sqr = 0.732680354389</span><span class="sxs-lookup"><span data-stu-id="2f194-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="2f194-389">Время на выполнение кода выше: 20,9 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-389">Time taken to execute above cell: 20.9 seconds</span></span>

<span data-ttu-id="2f194-390">**Графическое представления**</span><span class="sxs-lookup"><span data-stu-id="2f194-390">**Plot**</span></span>

<span data-ttu-id="2f194-391">*tmp_results* регистрируется как таблица Hive в предыдущей ячейке.</span><span class="sxs-lookup"><span data-stu-id="2f194-391">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="2f194-392">Результаты из таблицы передаются во фрейм данных *sqlResults* для формирования графического представления.</span><span class="sxs-lookup"><span data-stu-id="2f194-392">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="2f194-393">Ниже приведен код:</span><span class="sxs-lookup"><span data-stu-id="2f194-393">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="2f194-394">Ниже приведен код для формирования графического представления данных с использованием сервера Jupyter.</span><span class="sxs-lookup"><span data-stu-id="2f194-394">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="2f194-396">Приложение. Дополнительные задачи регрессии с использованием перекрестной проверки с перебором параметров</span><span class="sxs-lookup"><span data-stu-id="2f194-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="2f194-397">В этом приложении содержится код, показывающий, как выполнить перекрестную проверку с использованием эластичной сети для линейной регрессии, а также как выполнить перекрестную проверку с перебором параметров с использованием пользовательского кода для регрессии случайного леса.</span><span class="sxs-lookup"><span data-stu-id="2f194-397">This appendix contains code showing how to do CV using Elastic net for linear regression and how to do CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="2f194-398">Перекрестная проверка с использованием эластичной сети для линейной регрессии</span><span class="sxs-lookup"><span data-stu-id="2f194-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="2f194-399">Код в этом разделе показывает, как выполнить перекрестную проверку с использованием эластичной сети для линейной регрессии и как оценить модель по тестовым данным.</span><span class="sxs-lookup"><span data-stu-id="2f194-399">The code in this section shows how to do cross validation using Elastic net for linear regression and how to evaluate the model against test data.</span></span>

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
    # SIMPLY THE MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT TO DATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses the best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT TO DF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2f194-400">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-400">**OUTPUT**</span></span>

<span data-ttu-id="2f194-401">Время на выполнение приведенного выше кода: 161,21 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-401">Time taken to execute above cell: 161.21  seconds</span></span>

<span data-ttu-id="2f194-402">**Оценка с помощью метрики R SQR**</span><span class="sxs-lookup"><span data-stu-id="2f194-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="2f194-403">*tmp_results* регистрируется как таблица Hive в предыдущей ячейке.</span><span class="sxs-lookup"><span data-stu-id="2f194-403">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="2f194-404">Результаты из таблицы передаются во фрейм данных *sqlResults* для формирования графического представления.</span><span class="sxs-lookup"><span data-stu-id="2f194-404">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="2f194-405">Ниже приведен код:</span><span class="sxs-lookup"><span data-stu-id="2f194-405">Here is the code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="2f194-406">Ниже приведен код для вычисления R-sqr.</span><span class="sxs-lookup"><span data-stu-id="2f194-406">Here is the code to calculate R-sqr.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="2f194-407">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-407">**OUTPUT**</span></span>

<span data-ttu-id="2f194-408">R-sqr = 0.619184907088</span><span class="sxs-lookup"><span data-stu-id="2f194-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="2f194-409">Перекрестная проверка с перебором параметров с использованием пользовательского кода для регрессии случайного леса</span><span class="sxs-lookup"><span data-stu-id="2f194-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="2f194-410">Код в этом разделе показывает, как выполнить перекрестную проверку с перебором параметров с использованием пользовательского кода для регрессии случайного леса и как оценить модель по тестовым данным.</span><span class="sxs-lookup"><span data-stu-id="2f194-410">The code in this section shows how to do cross validation with parameter sweep using custom code for random forest regression and how to evaluate the model against test data.</span></span>

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

    # SPECIFY NUMFOLDS AND ARRAY TO HOLD METRICS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="2f194-411">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-411">**OUTPUT**</span></span>

<span data-ttu-id="2f194-412">RMSE = 0.906972198262</span><span class="sxs-lookup"><span data-stu-id="2f194-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="2f194-413">R-sqr = 0.740751197012</span><span class="sxs-lookup"><span data-stu-id="2f194-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="2f194-414">Время на выполнение кода выше: 69,17 с.</span><span class="sxs-lookup"><span data-stu-id="2f194-414">Time taken to execute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="2f194-415">Очистка объектов из памяти и вывод расположений моделей</span><span class="sxs-lookup"><span data-stu-id="2f194-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="2f194-416">Удалите объекты, кэшированные в памяти, с помощью метода `unpersist()` .</span><span class="sxs-lookup"><span data-stu-id="2f194-416">Use `unpersist()` to delete objects cached in memory.</span></span>

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


<span data-ttu-id="2f194-417">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-417">**OUTPUT**</span></span>

<span data-ttu-id="2f194-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="2f194-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="2f194-419">** Распечатки путь к файлам модели для использования в записной книжке потребления.</span><span class="sxs-lookup"><span data-stu-id="2f194-419">**Printout path to model files to be used in the consumption notebook.</span></span> <span data-ttu-id="2f194-420">** Для использования и оценка независимый набор данных, необходимо скопировать и вставить эти имена файлов в «блокноте потребления».</span><span class="sxs-lookup"><span data-stu-id="2f194-420">** To consume and score an independent data-set, you need to copy and paste these file names in the "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="2f194-421">**ВЫХОДНЫЕ ДАННЫЕ**</span><span class="sxs-lookup"><span data-stu-id="2f194-421">**OUTPUT**</span></span>

<span data-ttu-id="2f194-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="2f194-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="2f194-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="2f194-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="2f194-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="2f194-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="2f194-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="2f194-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="2f194-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="2f194-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="2f194-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="2f194-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="2f194-428">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="2f194-428">What's next?</span></span>
<span data-ttu-id="2f194-429">После создания моделей регрессии и классификации с помощью Spark MlLib необходимо ознакомиться с процессом оценки и анализа этих моделей.</span><span class="sxs-lookup"><span data-stu-id="2f194-429">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span>

<span data-ttu-id="2f194-430">**Использование модели**. Дополнительные сведения об оценке и анализе моделей классификации и регрессии, созданных в этой статье см. в статье [Оценка моделей машинного обучения, созданных с помощью Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="2f194-430">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

