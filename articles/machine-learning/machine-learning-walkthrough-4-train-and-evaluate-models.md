---
title: "Шаг 4. Обучение и анализ моделей прогнозирующей аналитики | Документация Майкрософт"
description: "Четвертый этап пошагового руководства по разработке прогнозного решения: обучение и оценка нескольких моделей в студии машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 58d46dd1464ec0a3fc9639f78d4429e0e778c2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-the-predictive-analytic-models"></a><span data-ttu-id="c6d59-103">Шаг 4. Обучение и анализ моделей прогнозирующей аналитики</span><span class="sxs-lookup"><span data-stu-id="c6d59-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span></span>
<span data-ttu-id="c6d59-104">Это четвертая часть пошагового руководства [по разработке решения для прогнозной аналитики в Машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="c6d59-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="c6d59-105">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="c6d59-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="c6d59-106">Отправка существующих данных</span><span class="sxs-lookup"><span data-stu-id="c6d59-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="c6d59-107">Создание нового эксперимента</span><span class="sxs-lookup"><span data-stu-id="c6d59-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="c6d59-108">**Обучение и анализ моделей**</span><span class="sxs-lookup"><span data-stu-id="c6d59-108">**Train and evaluate the models**</span></span>
5. [<span data-ttu-id="c6d59-109">Развертывание веб-службы</span><span class="sxs-lookup"><span data-stu-id="c6d59-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="c6d59-110">Доступ к веб-службе</span><span class="sxs-lookup"><span data-stu-id="c6d59-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="c6d59-111">Одно из преимуществ использования студии машинного обучения Azure для создания моделей машинного обучения заключается в том, что вы можете проверить несколько типов моделей и сравнить их результаты в рамках одного эксперимента.</span><span class="sxs-lookup"><span data-stu-id="c6d59-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span></span> <span data-ttu-id="c6d59-112">Этот тип экспериментов помогает найти наилучшее решение проблемы.</span><span class="sxs-lookup"><span data-stu-id="c6d59-112">This type of experimentation helps you find the best solution for your problem.</span></span>

<span data-ttu-id="c6d59-113">В эксперименте, разрабатываемом в этом пошаговом руководстве, мы создадим два разных типа модели и сравним результаты их оценки, чтобы решить, какой алгоритм мы хотим использовать в нашем финальном эксперименте.</span><span class="sxs-lookup"><span data-stu-id="c6d59-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span></span>  

<span data-ttu-id="c6d59-114">Существует множество моделей, которые можно выбрать.</span><span class="sxs-lookup"><span data-stu-id="c6d59-114">There are various models we could choose from.</span></span> <span data-ttu-id="c6d59-115">Чтобы просмотреть доступные модели, разверните узел **Машинное обучение** в палитре модулей, а затем **Initialize Model** (Инициализация модели) и узлы под ним.</span><span class="sxs-lookup"><span data-stu-id="c6d59-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span></span> <span data-ttu-id="c6d59-116">Для этого эксперимента мы выберем модули [Two-Class Support Vector Machine][two-class-support-vector-machine] (Двухклассовый метод опорных векторов) и [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Двухклассовое увеличивающееся дерево решений).</span><span class="sxs-lookup"><span data-stu-id="c6d59-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="c6d59-117">Чтобы решить, какой алгоритм машинного обучения лучше всего подойдет для решения конкретной задачи, изучите статью [Выбор алгоритмов Машинного обучения Microsoft Azure](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="c6d59-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-the-models"></a><span data-ttu-id="c6d59-118">Обучение моделей</span><span class="sxs-lookup"><span data-stu-id="c6d59-118">Train the models</span></span>

<span data-ttu-id="c6d59-119">В этот эксперимент мы добавим модули [Two-Class Support Vector Machine][two-class-boosted-decision-tree] (Двухклассовый метод опорных векторов) и [Two-Class Boosted Decision Tree][two-class-support-vector-machine] (Двухклассовое увеличивающееся дерево решений).</span><span class="sxs-lookup"><span data-stu-id="c6d59-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="c6d59-120">Двухклассовое увеличивающееся дерево принятия решений;</span><span class="sxs-lookup"><span data-stu-id="c6d59-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="c6d59-121">Сначала давайте настроим модуль увеличивающегося дерева решений.</span><span class="sxs-lookup"><span data-stu-id="c6d59-121">First, let's set up the boosted decision tree model.</span></span>

1. <span data-ttu-id="c6d59-122">Найдите модуль [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Двухклассовое увеличивающееся дерево решений) на палитре модулей и перетащите его на холст.</span><span class="sxs-lookup"><span data-stu-id="c6d59-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="c6d59-123">Найдите модуль [Train Model][train-model] (Обучение модели), перетащите его на холст, а затем подключите точку вывода модуля [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Двухклассовое увеличивающееся дерево решений) к левому порту ввода модуля [Train Model][train-model] (Обучение модели).</span><span class="sxs-lookup"><span data-stu-id="c6d59-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="c6d59-124">Модуль [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Двухклассовое увеличивающееся дерево решений) инициализирует универсальную модель, а модуль [Train Model][train-model] (Обучение модели) использует обучающие данные для обучения модели.</span><span class="sxs-lookup"><span data-stu-id="c6d59-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span></span> 

3. <span data-ttu-id="c6d59-125">Соедините левый выход левого модуля [Execute R Script][execute-r-script] (Выполнение скрипта R) с правым портом ввода модуля [Train Model][train-model] (Обучение модели). Напомним, что на [шаге 3](machine-learning-walkthrough-3-create-new-experiment.md) этого руководства мы решили использовать для обучения данные, поступающие от левой стороны модуля разделения данных.</span><span class="sxs-lookup"><span data-stu-id="c6d59-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c6d59-126">Для этого эксперимента нам не нужны два входа и один выход модуля [Execute R Script][execute-r-script] (Выполнение скрипта R), поэтому мы просто оставим их неподключенными.</span><span class="sxs-lookup"><span data-stu-id="c6d59-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="c6d59-127">Теперь эта часть эксперимента выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c6d59-127">This portion of the experiment now looks something like this:</span></span>  

![Обучение модели][1]

<span data-ttu-id="c6d59-129">Теперь мы сообщим модулю [Train Model][train-model] (Обучение модели), что наша модель должна прогнозировать значения кредитного риска (поле Credit Risk).</span><span class="sxs-lookup"><span data-stu-id="c6d59-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span></span>

1. <span data-ttu-id="c6d59-130">Выберите модуль [Train Model][train-model] (Обучение модели).</span><span class="sxs-lookup"><span data-stu-id="c6d59-130">Select the [Train Model][train-model] module.</span></span> <span data-ttu-id="c6d59-131">В области **Properties** (Свойства) щелкните **Launch column selector** (Запустить средство выбора столбцов).</span><span class="sxs-lookup"><span data-stu-id="c6d59-131">In the **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="c6d59-132">В диалоговом окне **Select a single column** (Выберите один столбец) введите в разделе **Available Columns** (Доступные столбцы) в поле поиска значение "Credit Risk", выберите внизу столбец Credit Risk (Кредитный риск) и нажмите кнопку со стрелкой вправо (**>**), чтобы переместить столбец "Credit Risk" (Кредитный риск) в раздел **Selected Columns** (Выбранные столбцы).</span><span class="sxs-lookup"><span data-stu-id="c6d59-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span></span> 

    ![Выбор столбца "Credit Risk" (Кредитный риск) для модуля "Train Model" (Обучение модели)][0]

3. <span data-ttu-id="c6d59-134">Нажмите кнопку с флажком (**ОК**).</span><span class="sxs-lookup"><span data-stu-id="c6d59-134">Click the **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="c6d59-135">Двухклассовая машина опорных векторов;</span><span class="sxs-lookup"><span data-stu-id="c6d59-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="c6d59-136">Теперь настроим модель SVM.</span><span class="sxs-lookup"><span data-stu-id="c6d59-136">Next, we set up the SVM model.</span></span>  

<span data-ttu-id="c6d59-137">Сначала немного информации о SVM.</span><span class="sxs-lookup"><span data-stu-id="c6d59-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="c6d59-138">"Повышенные" деревья принятия решения хорошо работают с атрибутами любого типа.</span><span class="sxs-lookup"><span data-stu-id="c6d59-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="c6d59-139">Однако поскольку модуль SVM создает линейный классификатор, генерируемая им модель имеет наименьшую ошибку при проверке среди всех атрибутов одного масштаба.</span><span class="sxs-lookup"><span data-stu-id="c6d59-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span></span> <span data-ttu-id="c6d59-140">Чтобы свести все числовые признаки к одному масштабу, мы используем преобразование "Tanh" (с помощью модуля [Normalize Data][normalize-data] (Нормализация данных)).</span><span class="sxs-lookup"><span data-stu-id="c6d59-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="c6d59-141">Этот алгоритм преобразует все числа в значения, лежащие в интервале [0,1].</span><span class="sxs-lookup"><span data-stu-id="c6d59-141">This transforms our numbers into the [0,1] range.</span></span> <span data-ttu-id="c6d59-142">Модуль SVM преобразовывает строковые признаки в категориальные, а затем в бинарные признаки 0/1, поэтому вручную их преобразовывать не нужно.</span><span class="sxs-lookup"><span data-stu-id="c6d59-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span></span> <span data-ttu-id="c6d59-143">Кроме того, мы не хотим преобразовывать столбец кредитного риска (столбец 21) — он числовой, но мы обучаем модель прогнозировать именно его значение, поэтому нам не нужно его трогать.</span><span class="sxs-lookup"><span data-stu-id="c6d59-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span></span>  

<span data-ttu-id="c6d59-144">Чтобы настроить модель SVM, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c6d59-144">To set up the SVM model, do the following:</span></span>

1. <span data-ttu-id="c6d59-145">Найдите модуль [Two-Class Support Vector Machine][two-class-support-vector-machine] (Двухклассовый метод опорных векторов) на палитре модулей и перетащите его на холст.</span><span class="sxs-lookup"><span data-stu-id="c6d59-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="c6d59-146">Щелкните правой кнопкой мыши модуль [Train Model][train-model] (Обучение модели), выберите команду **Copy** (Копировать), а затем щелкните холст правой кнопкой мыши и выберите **Paste** (Вставить).</span><span class="sxs-lookup"><span data-stu-id="c6d59-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span></span> <span data-ttu-id="c6d59-147">Обратите внимание, что копия модуля [Train Model][train-model] (Обучение модели) имеет тот же набор выбранных столбцов, что и оригинал.</span><span class="sxs-lookup"><span data-stu-id="c6d59-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span></span>

3. <span data-ttu-id="c6d59-148">Соедините вывод модуля [Two-Class Support Vector Machine][two-class-support-vector-machine] (Двухклассовый метод опорных векторов) с левым портом ввода второго модуля [Train Model][train-model] (Обучение модели).</span><span class="sxs-lookup"><span data-stu-id="c6d59-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="c6d59-149">Найдите модуль [Normalize Data][normalize-data] (Нормализация данных) и перетащите его на холст.</span><span class="sxs-lookup"><span data-stu-id="c6d59-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span></span>

5. <span data-ttu-id="c6d59-150">Соедините ввод этого модуля с левым портом вывода левого модуля [Execute R Script][execute-r-script] (Выполнение скрипта R). Обратите внимание, что порт вывода любого модуля может быть подключен к нескольким модулям.</span><span class="sxs-lookup"><span data-stu-id="c6d59-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span></span>

6. <span data-ttu-id="c6d59-151">Соедините левый выходной порт модуля [Normalize Data][normalize-data] (Нормализация данных) с правым входным портом второго модуля [Train Model][train-model] (Обучение модели).</span><span class="sxs-lookup"><span data-stu-id="c6d59-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span></span>

<span data-ttu-id="c6d59-152">Теперь эта часть эксперимента должна выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c6d59-152">This portion of our experiment should now look something like this:</span></span>  

![Обучение второй модели][2]  

<span data-ttu-id="c6d59-154">Теперь настройте модуль [Normalize Data][normalize-data] (Нормализация данных).</span><span class="sxs-lookup"><span data-stu-id="c6d59-154">Now configure the [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="c6d59-155">Щелкните модуль [Normalize Data][normalize-data] (Нормализация данных), чтобы выбрать его.</span><span class="sxs-lookup"><span data-stu-id="c6d59-155">Click to select the [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="c6d59-156">На панели **Properties** (Свойства) выберите для параметра **Transformation method** (Метод преобразования) значение **Tanh**.</span><span class="sxs-lookup"><span data-stu-id="c6d59-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span></span>

2. <span data-ttu-id="c6d59-157">Щелкните **Запустить средство выбора столбцов** (Launch column selector), укажите для параметра **Begin With** (Начало с) значение No columns (Без столбцов). В первом раскрывающемся списке выберите пункт **Включение**, во втором — **column type** (тип столбца), а в третьем — **Числовой**.</span><span class="sxs-lookup"><span data-stu-id="c6d59-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span></span> <span data-ttu-id="c6d59-158">Это указывает, что будут преобразованы все числовые столбцы (и только числовые).</span><span class="sxs-lookup"><span data-stu-id="c6d59-158">This specifies that all the numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="c6d59-159">Щелкните знак плюса (+) в правой части этой строки. Это позволит создать строку с раскрывающимися списками.</span><span class="sxs-lookup"><span data-stu-id="c6d59-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="c6d59-160">Выберите в первом раскрывающемся списке значение **Exclude** (Исключить), во втором раскрывающемся списке выберите **column names** (Имена столбцов), затем введите текст "Credit risk" в текстовом поле.</span><span class="sxs-lookup"><span data-stu-id="c6d59-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span></span> <span data-ttu-id="c6d59-161">Так мы сообщим модулю, что столбец "Credit Risk" (Кредитный риск) нужно игнорировать. В противном случае этот столбец будет преобразован, так как является числовым.</span><span class="sxs-lookup"><span data-stu-id="c6d59-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="c6d59-162">Нажмите кнопку с флажком (**ОК**).</span><span class="sxs-lookup"><span data-stu-id="c6d59-162">Click the **OK** check mark.</span></span>  

    ![Выбор столбцов для модуля "Normalize Data" (Нормализация данных)][5]

<span data-ttu-id="c6d59-164">Теперь модуль [Normalize Data][normalize-data] (Нормализация данных) настроен для выполнения преобразования "Tanh" для всех числовых столбцов, за исключением столбца "Credit Risk" (Кредитный риск).</span><span class="sxs-lookup"><span data-stu-id="c6d59-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span></span>  

## <a name="score-and-evaluate-the-models"></a><span data-ttu-id="c6d59-165">Оценка и анализ моделей</span><span class="sxs-lookup"><span data-stu-id="c6d59-165">Score and evaluate the models</span></span>

<span data-ttu-id="c6d59-166">Мы будем использовать для оценки обученных моделей данные тестирования, которые были отделены модулем [Split Data][split] (Разделение данных).</span><span class="sxs-lookup"><span data-stu-id="c6d59-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span></span> <span data-ttu-id="c6d59-167">Затем можно сравнить результаты двух моделей, чтобы увидеть, которая модель создает лучший результат.</span><span class="sxs-lookup"><span data-stu-id="c6d59-167">We can then compare the results of the two models to see which generated better results.</span></span>  

### <a name="add-the-score-model-modules"></a><span data-ttu-id="c6d59-168">Добавление модулей "Score Model" (Оценка модели)</span><span class="sxs-lookup"><span data-stu-id="c6d59-168">Add the Score Model modules</span></span>

1. <span data-ttu-id="c6d59-169">Найдите модуль [Score Model][score-model] (Оценка модели) и перетащите его на холст.</span><span class="sxs-lookup"><span data-stu-id="c6d59-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="c6d59-170">Подключите модуль [Train Model][train-model] (Обучение модели), который подключен к модулю [Two-Class Support Vector Machine][two-class-boosted-decision-tree] (Двухклассовый метод опорных векторов), к левому порту ввода нового модуля [Score Model][score-model] (Оценка модели).</span><span class="sxs-lookup"><span data-stu-id="c6d59-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="c6d59-171">Соедините правый модуль [Execute R Script][execute-r-script] (Выполнение скрипта R), который возвращает данные для тестирования, с правым входным портом модуля [Score Model][score-model] (Оценка модели).</span><span class="sxs-lookup"><span data-stu-id="c6d59-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span></span>

    ![Модуль "Score Model" (Оценка модели) подключен][6]
   
   <span data-ttu-id="c6d59-173">Теперь модуль [Score Model][score-model] (Оценка модели) может получить сведения о кредите из тестовых данных, обработать их с помощью модели и сравнить созданные моделью прогнозы с фактическими данными столбца кредитного риска из тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="c6d59-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span></span>

4. <span data-ttu-id="c6d59-174">Скопируйте и вставьте модуль [Score Model][score-model] (Оценка модели), чтобы создать вторую копию.</span><span class="sxs-lookup"><span data-stu-id="c6d59-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span></span>

5. <span data-ttu-id="c6d59-175">Соедините выход модуля SVM (т. е. порт вывода модуля [Train Model][train-model] (Обучение модели), подключенного к модулю [Two-Class Support Vector Machine][two-class-support-vector-machine] (Двухклассовый метод опорных векторов)) со входным портом второго модуля [Score Model][score-model] (Оценка модели).</span><span class="sxs-lookup"><span data-stu-id="c6d59-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="c6d59-176">Для модели SVM необходимо выполнить то же самое преобразование тестовых данных, которое делалось для обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="c6d59-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span></span> <span data-ttu-id="c6d59-177">Поэтому скопируйте и вставьте модуль [Normalize Data][normalize-data] (Нормализация данных), чтобы создать второй его экземпляр, и подключите его к выходу правого модуля [Execute R Script][execute-r-script] (Выполнение скрипта R).</span><span class="sxs-lookup"><span data-stu-id="c6d59-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="c6d59-178">Соедините левый выход второго модуля [Normalize Data][normalize-data] (Нормализация данных) с правым входным портом второго модуля [Score Model][score-model] (Оценка модели).</span><span class="sxs-lookup"><span data-stu-id="c6d59-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span></span>

    ![Оба модуля "Score Model" (Оценка модели) подключены][7]

### <a name="add-the-evaluate-model-module"></a><span data-ttu-id="c6d59-180">Добавление модуля "Evaluate Model" (Анализ модели)</span><span class="sxs-lookup"><span data-stu-id="c6d59-180">Add the Evaluate Model module</span></span>

<span data-ttu-id="c6d59-181">Чтобы проанализировать и сравнить два результата оценки, мы будем использовать модуль [Evaluate Model ][evaluate-model] (Анализ модели).</span><span class="sxs-lookup"><span data-stu-id="c6d59-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="c6d59-182">Найдите модуль [Evaluate Model][evaluate-model] (Анализ модели) и перетащите его на холст.</span><span class="sxs-lookup"><span data-stu-id="c6d59-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="c6d59-183">Подключите порт вывода модуля [Score Model][score-model] (Оценка модели), связанного с модулем увеличивающегося дерева решений, к левому входному порту модуля [Evaluate Model][evaluate-model] (Анализ модели).</span><span class="sxs-lookup"><span data-stu-id="c6d59-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="c6d59-184">Соедините второй модуль [Score Model][score-model] (Оценка модели) с левым входным портом.</span><span class="sxs-lookup"><span data-stu-id="c6d59-184">Connect the other [Score Model][score-model] module to the right input port.</span></span>  

    ![Модуль "Evaluate Model" (Анализ модели) подключен][8]

### <a name="run-the-experiment-and-check-the-results"></a><span data-ttu-id="c6d59-186">Запуск эксперимента и проверка результатов</span><span class="sxs-lookup"><span data-stu-id="c6d59-186">Run the experiment and check the results</span></span>

<span data-ttu-id="c6d59-187">Нажмите кнопку **ЗАПУСТИТЬ** внизу холста, чтобы запустить эксперимент.</span><span class="sxs-lookup"><span data-stu-id="c6d59-187">To run the experiment, click the **RUN** button below the canvas.</span></span> <span data-ttu-id="c6d59-188">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="c6d59-188">It may take a few minutes.</span></span> <span data-ttu-id="c6d59-189">В каждом модуле будет отображаться вращающийся индикатор, показывающий, что модуль выполняется. Когда модуль завершит работу, появится зеленый флажок.</span><span class="sxs-lookup"><span data-stu-id="c6d59-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span></span> <span data-ttu-id="c6d59-190">Если эта галочка появилась во всех модулях, значит эксперимент завершил выполнение.</span><span class="sxs-lookup"><span data-stu-id="c6d59-190">When all the modules have a check mark, the experiment has finished running.</span></span>

<span data-ttu-id="c6d59-191">Теперь наш эксперимент должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c6d59-191">The experiment should now look something like this:</span></span>  

![Сравнение обеих моделей][3]

<span data-ttu-id="c6d59-193">Чтобы проверить результаты, щелкните правой кнопкой мыши порт вывода модуля [Evaluate Model][evaluate-model] (Анализ модели) и выберите **Visualize** (Визуализировать).</span><span class="sxs-lookup"><span data-stu-id="c6d59-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="c6d59-194">Модуль [Evaluate Model][evaluate-model] (Анализ модели) создает пару кривых и метрики, которые позволяют сравнить результаты двух оцениваемых моделей.</span><span class="sxs-lookup"><span data-stu-id="c6d59-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span></span> <span data-ttu-id="c6d59-195">Результаты можно видеть в виде кривых ROC (рабочих характеристик приемника), кривых точности/полноты или кривых точности прогноза.</span><span class="sxs-lookup"><span data-stu-id="c6d59-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="c6d59-196">Дополнительные отображаемые данные включают матрицу несоответствий, накопительные значения для области под кривой (AUC) и другие метрики.</span><span class="sxs-lookup"><span data-stu-id="c6d59-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span></span> <span data-ttu-id="c6d59-197">Вы можете изменить пороговое значение, перемещая ползунок влево или вправо, чтобы посмотреть, как это влияет на набор метрик.</span><span class="sxs-lookup"><span data-stu-id="c6d59-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span></span>  

<span data-ttu-id="c6d59-198">В правой части графика щелкните **Scored dataset** (Оцененный набор данных) или **Scored dataset to compare** (Оцененный набор данных для сравнения), чтобы выделить соответствующую кривую и отобразить внизу соответствующие метрики.</span><span class="sxs-lookup"><span data-stu-id="c6d59-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span></span> <span data-ttu-id="c6d59-199">В условных обозначениях для кривых "Scored dataset" (Оцененный набор данных) соответствует левому порту ввода модуля [Evaluate Model][evaluate-model] (Оценка модели). В нашем случае это модель увеличивающегося дерева решений.</span><span class="sxs-lookup"><span data-stu-id="c6d59-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span></span> <span data-ttu-id="c6d59-200">"Оцененный набор данных для сравнения" соответствует правому входному порту — в нашем случае это модель SVM.</span><span class="sxs-lookup"><span data-stu-id="c6d59-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span></span> <span data-ttu-id="c6d59-201">Щелкните одну из этих меток, чтобы выделить кривую и отобразить внизу метрики для соответствующей модели, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="c6d59-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span></span>  

![Кривые ROC для моделей][4]

<span data-ttu-id="c6d59-203">Изучив эти значения, можно определить, какая модель обеспечивает более точные результаты.</span><span class="sxs-lookup"><span data-stu-id="c6d59-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span></span> <span data-ttu-id="c6d59-204">Можно вернуться назад и повторить эксперимент, изменяя значения параметров в моделях.</span><span class="sxs-lookup"><span data-stu-id="c6d59-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span></span> 

<span data-ttu-id="c6d59-205">Наука и искусство интерпретации результатов и настройки производительности моделей выходит за рамки этого руководства.</span><span class="sxs-lookup"><span data-stu-id="c6d59-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span></span> <span data-ttu-id="c6d59-206">Для получения дополнительной информации ознакомьтесь со следующими статьями.</span><span class="sxs-lookup"><span data-stu-id="c6d59-206">For additional help, you might read the following articles:</span></span>
- [<span data-ttu-id="c6d59-207">Оценка эффективности модели в машинном обучении Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c6d59-207">How to evaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="c6d59-208">Выбор параметров для оптимизации алгоритмов в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="c6d59-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="c6d59-209">Интерпретация результатов модели в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="c6d59-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="c6d59-210">При каждом выполнении эксперимента запись об этой итерации сохраняется в журнале выполнения.</span><span class="sxs-lookup"><span data-stu-id="c6d59-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span></span> <span data-ttu-id="c6d59-211">Эти итерации можно просмотреть и вернуться к любой из них, нажав кнопку **ПРОСМОТР ЖУРНАЛА ВЫПОЛНЕНИЯ** под холстом.</span><span class="sxs-lookup"><span data-stu-id="c6d59-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span></span> <span data-ttu-id="c6d59-212">Можно также щелкнуть **Prior Run** (Предыдущее выполнение) на панели **Свойства**, чтобы открыть результаты предыдущей попытки сравнения.</span><span class="sxs-lookup"><span data-stu-id="c6d59-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span></span>
> 
> <span data-ttu-id="c6d59-213">Можно сделать копию любой итерации эксперимента, нажав кнопку **SAVE AS** (Сохранить как) под холстом.</span><span class="sxs-lookup"><span data-stu-id="c6d59-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span></span> 
> <span data-ttu-id="c6d59-214">Чтобы отслеживать, какие данные вы сравнивали на каждом этапе выполнения эксперимента, используйте свойства эксперимента **Сводка** и **Описание**.</span><span class="sxs-lookup"><span data-stu-id="c6d59-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="c6d59-215">Дополнительные сведения см. в статье [Управление итерациями экспериментов в Студии машинного обучения Azure](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="c6d59-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="c6d59-216">**Дальнейшие действия: [Развертывание веб-службы](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="c6d59-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
