---
title: "aaaAnalyze данных с помощью машинного обучения Azure | Документы Microsoft"
description: "Используйте машинного обучения Azure toobuild прогнозной модели машинного обучения на основе данных, хранимых в хранилище данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="8528b-103">Анализ данных с помощью машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="8528b-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8528b-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="8528b-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="8528b-105">машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="8528b-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="8528b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8528b-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="8528b-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="8528b-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="8528b-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="8528b-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="8528b-109">В этом учебнике используется машинного обучения Azure toobuild прогнозной модели машинного обучения на основе данных, хранимых в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8528b-109">This tutorial uses Azure Machine Learning toobuild a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8528b-110">В частности для Adventure Works, велосипеда производственный hello и построен целевой маркетинговой кампании, по прогнозирование, если клиент является toobuy скорее всего, велосипед или нет.</span><span class="sxs-lookup"><span data-stu-id="8528b-110">Specifically, this builds a targeted marketing campaign for Adventure Works, hello bike shop, by predicting if a customer is likely toobuy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="8528b-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8528b-111">Prerequisites</span></span>
<span data-ttu-id="8528b-112">toostep изучения этого руководства требуется:</span><span class="sxs-lookup"><span data-stu-id="8528b-112">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="8528b-113">Хранилище данных SQL, в которое предварительно загружены демонстрационные данные AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="8528b-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="8528b-114">tooprovision это, см. в разделе [создать хранилище данных SQL] [ Create a SQL Data Warehouse] и выберите образец hello tooload данных.</span><span class="sxs-lookup"><span data-stu-id="8528b-114">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="8528b-115">Если хранилище данных уже существует, но в нем нет демонстрационных данных, вы можете [загрузить их вручную][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="8528b-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-hello-data"></a><span data-ttu-id="8528b-116">1. Получение данных hello</span><span class="sxs-lookup"><span data-stu-id="8528b-116">1. Get hello data</span></span>
<span data-ttu-id="8528b-117">Hello данные находятся в представлении dbo.vTargetMail hello базы данных AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="8528b-117">hello data is in hello dbo.vTargetMail view in hello AdventureWorksDW database.</span></span> <span data-ttu-id="8528b-118">tooread эти данные:</span><span class="sxs-lookup"><span data-stu-id="8528b-118">tooread this data:</span></span>

1. <span data-ttu-id="8528b-119">Войдите в [Студию машинного обучения Azure][Azure Machine Learning studio] и щелкните My experiments (Мои эксперименты).</span><span class="sxs-lookup"><span data-stu-id="8528b-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="8528b-120">Щелкните **+ Создать** и выберите **Blank Experiment** (Пустой эксперимент).</span><span class="sxs-lookup"><span data-stu-id="8528b-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="8528b-121">Введите для своего эксперимента имя «Целевой маркетинг».</span><span class="sxs-lookup"><span data-stu-id="8528b-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="8528b-122">Перетащите hello **чтения** модуля из области модули hello в hello canvas.</span><span class="sxs-lookup"><span data-stu-id="8528b-122">Drag hello **Reader** module from hello modules pane into hello canvas.</span></span>
5. <span data-ttu-id="8528b-123">Укажите сведения hello базы данных хранилища данных SQL на панели свойств hello.</span><span class="sxs-lookup"><span data-stu-id="8528b-123">Specify hello details of your SQL Data Warehouse database in hello Properties pane.</span></span>
6. <span data-ttu-id="8528b-124">Укажите базу данных hello **запроса** tooread hello данные представляют интерес.</span><span class="sxs-lookup"><span data-stu-id="8528b-124">Specify hello database **query** tooread hello data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="8528b-125">Запустите эксперимент hello, нажав кнопку **запуска** под холст эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="8528b-125">Run hello experiment by clicking **Run** under hello experiment canvas.</span></span>
<span data-ttu-id="8528b-126">![Запустите эксперимент hello][1]</span><span class="sxs-lookup"><span data-stu-id="8528b-126">![Run hello experiment][1]</span></span>

<span data-ttu-id="8528b-127">По завершении успешному выполнению эксперимента hello щелкните порт вывода hello внизу hello модуль считывания hello и выберите **визуализировать** toosee hello импортируемых данных.</span><span class="sxs-lookup"><span data-stu-id="8528b-127">After hello experiment finishes running successfully, click hello output port at hello bottom of hello Reader module and select **Visualize** toosee hello imported data.</span></span>
<span data-ttu-id="8528b-128">![Просмотр импортированных данных][3]</span><span class="sxs-lookup"><span data-stu-id="8528b-128">![View imported data][3]</span></span>

## <a name="2-clean-hello-data"></a><span data-ttu-id="8528b-129">2. Очистить hello данных</span><span class="sxs-lookup"><span data-stu-id="8528b-129">2. Clean hello data</span></span>
<span data-ttu-id="8528b-130">данные tooclean hello, удалите некоторые столбцы, которые не являются значимыми для моделей hello.</span><span class="sxs-lookup"><span data-stu-id="8528b-130">tooclean hello data, drop some columns that are not relevant for hello model.</span></span> <span data-ttu-id="8528b-131">toodo это:</span><span class="sxs-lookup"><span data-stu-id="8528b-131">toodo this:</span></span>

1. <span data-ttu-id="8528b-132">Перетащите hello **столбцы проекта** модуля в hello canvas.</span><span class="sxs-lookup"><span data-stu-id="8528b-132">Drag hello **Project Columns** module into hello canvas.</span></span>
2. <span data-ttu-id="8528b-133">Нажмите кнопку **запуска средства выбора столбцов** в toospecify панели свойств hello, какие столбцы нужно toodrop.</span><span class="sxs-lookup"><span data-stu-id="8528b-133">Click **Launch column selector** in hello Properties pane toospecify which columns you wish toodrop.</span></span>
   <span data-ttu-id="8528b-134">![Столбцы проекта][4]</span><span class="sxs-lookup"><span data-stu-id="8528b-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="8528b-135">Исключите два столбца: CustomerAlternateKey и GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="8528b-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="8528b-136">![Удаление ненужных столбцов][5]</span><span class="sxs-lookup"><span data-stu-id="8528b-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-hello-model"></a><span data-ttu-id="8528b-137">3. Построение модели hello</span><span class="sxs-lookup"><span data-stu-id="8528b-137">3. Build hello model</span></span>
<span data-ttu-id="8528b-138">Разделите данные hello 80-20: 80% tootrain модели машинного обучения и 20% tootest hello модели.</span><span class="sxs-lookup"><span data-stu-id="8528b-138">We will split hello data 80-20: 80% tootrain a machine learning model and 20% tootest hello model.</span></span> <span data-ttu-id="8528b-139">Будет использовать алгоритмы «Два класса» hello данной проблемы двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="8528b-139">We will make use of hello “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="8528b-140">Перетащите hello **разбиение** модуля в hello canvas.</span><span class="sxs-lookup"><span data-stu-id="8528b-140">Drag hello **Split** module into hello canvas.</span></span>
2. <span data-ttu-id="8528b-141">Введите часть строк в hello первый выходной набор данных на панели свойств hello 0,8.</span><span class="sxs-lookup"><span data-stu-id="8528b-141">Enter 0.8 for Fraction of rows in hello first output dataset in hello Properties pane.</span></span>
   <span data-ttu-id="8528b-142">![Разделение данных на обучающую и тестовую выборки][6]</span><span class="sxs-lookup"><span data-stu-id="8528b-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="8528b-143">Перетащите hello **Двухклассового повышенного дерева принятия решений** модуля в hello canvas.</span><span class="sxs-lookup"><span data-stu-id="8528b-143">Drag hello **Two-Class Boosted Decision Tree** module into hello canvas.</span></span>
4. <span data-ttu-id="8528b-144">Перетащите hello **Обучение модели** модуля в hello холст и указания входных данных hello.</span><span class="sxs-lookup"><span data-stu-id="8528b-144">Drag hello **Train Model** module into hello canvas and specify hello inputs.</span></span> <span data-ttu-id="8528b-145">Нажмите кнопку **запуска средства выбора столбцов** hello панели свойств.</span><span class="sxs-lookup"><span data-stu-id="8528b-145">Then, click **Launch column selector** in hello Properties pane.</span></span>
   * <span data-ttu-id="8528b-146">Первый входной набор данных: алгоритм ML.</span><span class="sxs-lookup"><span data-stu-id="8528b-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="8528b-147">Во-вторых входных данных: алгоритм hello tootrain данных на.</span><span class="sxs-lookup"><span data-stu-id="8528b-147">Second input: Data tootrain hello algorithm on.</span></span>
     <span data-ttu-id="8528b-148">![Подключение hello модуль обучения модели][7]</span><span class="sxs-lookup"><span data-stu-id="8528b-148">![Connect hello Train Model module][7]</span></span>
5. <span data-ttu-id="8528b-149">Выберите hello **BikeBuyer** столбец как столбец toopredict hello.</span><span class="sxs-lookup"><span data-stu-id="8528b-149">Select hello **BikeBuyer** column as hello column toopredict.</span></span>
   <span data-ttu-id="8528b-150">![Выберите столбец toopredict][8]</span><span class="sxs-lookup"><span data-stu-id="8528b-150">![Select Column toopredict][8]</span></span>

## <a name="4-score-hello-model"></a><span data-ttu-id="8528b-151">4. Модель оценки hello</span><span class="sxs-lookup"><span data-stu-id="8528b-151">4. Score hello model</span></span>
<span data-ttu-id="8528b-152">Теперь мы проверим, как выполняет hello модели к тестовым данным.</span><span class="sxs-lookup"><span data-stu-id="8528b-152">Now, we will test how hello model performs on test data.</span></span> <span data-ttu-id="8528b-153">Мы сравнит алгоритм hello Выбор с toosee другой алгоритм, который дает более высокую производительность.</span><span class="sxs-lookup"><span data-stu-id="8528b-153">We will compare hello algorithm of our choice with a different algorithm toosee which performs better.</span></span>

1. <span data-ttu-id="8528b-154">Перетащите **модель оценки** модуля в hello canvas.</span><span class="sxs-lookup"><span data-stu-id="8528b-154">Drag **Score Model** module into hello canvas.</span></span>
    <span data-ttu-id="8528b-155">Сначала ввода: обучение модели второй набор входных данных: данные теста ![hello модель оценки][9]</span><span class="sxs-lookup"><span data-stu-id="8528b-155">First input: Trained model Second input: Test data ![Score hello model][9]</span></span>
2. <span data-ttu-id="8528b-156">Перетащите hello **Двухклассовая Байесовская Точечная машина** на холст эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="8528b-156">Drag hello **Two-Class Bayes Point Machine** into hello experiment canvas.</span></span> <span data-ttu-id="8528b-157">Мы сравнит, как работает этот алгоритм в toohello сравнения Двухклассового повышенного дерева принятия решений.</span><span class="sxs-lookup"><span data-stu-id="8528b-157">We will compare how this algorithm performs in comparison toohello Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="8528b-158">Копировать и вставить hello модулей Обучение модели и оценка модели hello холст.</span><span class="sxs-lookup"><span data-stu-id="8528b-158">Copy and Paste hello modules Train Model and Score Model in hello canvas.</span></span>
4. <span data-ttu-id="8528b-159">Перетащите hello **модель оценки** модуля в hello холст toocompare hello двух алгоритмов.</span><span class="sxs-lookup"><span data-stu-id="8528b-159">Drag hello **Evaluate Model** module into hello canvas toocompare hello two algorithms.</span></span>
5. <span data-ttu-id="8528b-160">**Запустите** hello эксперимента.</span><span class="sxs-lookup"><span data-stu-id="8528b-160">**Run** hello experiment.</span></span>
   <span data-ttu-id="8528b-161">![Запустите эксперимент hello][10]</span><span class="sxs-lookup"><span data-stu-id="8528b-161">![Run hello experiment][10]</span></span>
6. <span data-ttu-id="8528b-162">Щелкните порт вывода hello внизу hello hello модель оценки модуль и выберите визуализировать.</span><span class="sxs-lookup"><span data-stu-id="8528b-162">Click hello output port at hello bottom of hello Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="8528b-163">![Отображение результатов классификации][11]</span><span class="sxs-lookup"><span data-stu-id="8528b-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="8528b-164">Hello метрики, предоставляемые являются кривой ROC hello, диаграмма точности отзыв и поднимите кривой.</span><span class="sxs-lookup"><span data-stu-id="8528b-164">hello metrics provided are hello ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="8528b-165">Глядя на эти показатели, мы видим первой модели hello выполняется лучше, чем второй hello.</span><span class="sxs-lookup"><span data-stu-id="8528b-165">Looking at these metrics, we can see that hello first model performed better than hello second one.</span></span> <span data-ttu-id="8528b-166">toolook на hello hello прогнозировать первой модели, щелкните выходной порт hello модель оценки и щелкните визуализировать.</span><span class="sxs-lookup"><span data-stu-id="8528b-166">toolook at hello what hello first model predicted, click on output port of hello Score Model and click Visualize.</span></span>
<span data-ttu-id="8528b-167">![Отображение результатов вычисления][12]</span><span class="sxs-lookup"><span data-stu-id="8528b-167">![Visualize score results][12]</span></span>

<span data-ttu-id="8528b-168">Вы увидите, что tooyour проверочный набор данных добавлено два дополнительных столбца.</span><span class="sxs-lookup"><span data-stu-id="8528b-168">You will see two more columns added tooyour test dataset.</span></span>

* <span data-ttu-id="8528b-169">Оцененных вероятностей: hello вероятность, что пользователь является Покупатель велосипеда.</span><span class="sxs-lookup"><span data-stu-id="8528b-169">Scored Probabilities: hello likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="8528b-170">Оцененный метки: hello классификация выполненную hello модели — «Покупатель велосипеда» (1) или нет (0).</span><span class="sxs-lookup"><span data-stu-id="8528b-170">Scored Labels: hello classification done by hello model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="8528b-171">Этот порог вероятности для пометки задается too50% и могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="8528b-171">This probability threshold for labeling is set too50% and can be adjusted.</span></span>

<span data-ttu-id="8528b-172">Сравнение столбцов hello BikeBuyer (фактические) с hello меток оцененных значений (прогноз), можно увидеть, насколько успешно выполнены hello модели.</span><span class="sxs-lookup"><span data-stu-id="8528b-172">Comparing hello column BikeBuyer (actual) with hello Scored Labels (prediction), you can see how well hello model has performed.</span></span> <span data-ttu-id="8528b-173">Как в этом случае можно использовать toomake этой модели прогнозов для новых клиентов и опубликовать эту модель веб-службы или записать результаты назад tooSQL хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="8528b-173">As next steps, you can use this model toomake predictions for new customers and publish this model as a web service or write results back tooSQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8528b-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8528b-174">Next steps</span></span>
<span data-ttu-id="8528b-175">toolearn Дополнительные сведения о создании прогнозных моделей машинного обучения, см. слишком[tooMachine введение обучения в Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="8528b-175">toolearn more about building predictive machine learning models, refer too[Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
