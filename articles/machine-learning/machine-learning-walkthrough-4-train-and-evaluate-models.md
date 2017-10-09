---
title: "Шаг 4: Обучать и оценивать прогнозных моделей аналитической hello | Документы Microsoft"
description: "Шаг 4 hello разработка прогнозирующего решения Пошаговое руководство: обучение, оценки и оценить несколько моделей в студии машинного обучения Azure."
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
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="6f48f-103">Шаг 4 пошагового руководства: Обучать и оценивать прогнозных моделей аналитической hello</span><span class="sxs-lookup"><span data-stu-id="6f48f-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="6f48f-104">В этом разделе содержатся hello четвертый шаг руководства hello [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="6f48f-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="6f48f-105">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="6f48f-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="6f48f-106">Отправка существующих данных</span><span class="sxs-lookup"><span data-stu-id="6f48f-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="6f48f-107">Создание нового эксперимента</span><span class="sxs-lookup"><span data-stu-id="6f48f-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="6f48f-108">**Обучать и оценивать модели hello**</span><span class="sxs-lookup"><span data-stu-id="6f48f-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="6f48f-109">Развернуть веб-службу hello</span><span class="sxs-lookup"><span data-stu-id="6f48f-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="6f48f-110">Доступ к веб-службе hello</span><span class="sxs-lookup"><span data-stu-id="6f48f-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="6f48f-111">Одно из преимуществ использования студии машинного обучения Azure для создания моделей машинного обучения hello не более чем один тип модели tootry возможность hello одновременно в одном эксперимента, сравнить результаты hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="6f48f-112">Этот тип экспериментов помогает найти hello оптимальное решение для конкретной задачи.</span><span class="sxs-lookup"><span data-stu-id="6f48f-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="6f48f-113">В эксперименте hello мы разрабатываем в этом пошаговом руководстве мы создания двух разных типов моделей и сравнить их оценки результатов toodecide какой алгоритм мы хотим toouse в наших окончательного эксперимента.</span><span class="sxs-lookup"><span data-stu-id="6f48f-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="6f48f-114">Существует множество моделей, которые можно выбрать.</span><span class="sxs-lookup"><span data-stu-id="6f48f-114">There are various models we could choose from.</span></span> <span data-ttu-id="6f48f-115">модели toosee hello, доступные, разверните hello **машинного обучения** узла в палитре модуля hello и разверните **модель инициализации** и hello узлы под ним.</span><span class="sxs-lookup"><span data-stu-id="6f48f-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="6f48f-116">Для целей этого эксперимента hello, мы выберем hello [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] (SVM) и hello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree] модули.</span><span class="sxs-lookup"><span data-stu-id="6f48f-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="6f48f-117">tooget решить, какой алгоритм машинного обучения лучше всего подходит для конкретной проблемы hello вы пытаетесь toosolve см. в разделе [как алгоритмы машинного обучения Microsoft Azure toochoose](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="6f48f-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="6f48f-118">Обучение моделей hello</span><span class="sxs-lookup"><span data-stu-id="6f48f-118">Train hello models</span></span>

<span data-ttu-id="6f48f-119">Мы добавим обе hello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree] модуля и [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] модуля в этом эксперимента.</span><span class="sxs-lookup"><span data-stu-id="6f48f-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="6f48f-120">Двухклассовое увеличивающееся дерево принятия решений;</span><span class="sxs-lookup"><span data-stu-id="6f48f-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="6f48f-121">Во-первых можно перейти к настройке модели дерева принятия решений повышенного hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="6f48f-122">Найти hello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree] модуля в палитре модуля hello и перетащите его на холсте hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="6f48f-123">Найти hello [Обучение модели] [ train-model] модуля, перетащите его на холсте hello, а затем подключите выход hello hello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree]toohello модуль левому входному порту hello [Обучение модели] [ train-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="6f48f-124">Hello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree] модуль инициализирует hello универсальная модель, и [Обучение модели] [ train-model] использует обучающих данных модель tootrain hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="6f48f-125">Подсоедините hello левой выход слева hello [выполнение скрипта R] [ execute-r-script] toohello модуль справа входному порту hello [Обучение модели] [ train-model] модуля (мы решено в [шаг 3](machine-learning-walkthrough-3-create-new-experiment.md) это пошаговое руководство toouse hello данных, поступающих из hello левая сторона модуля hello разбиение данных для обучения).</span><span class="sxs-lookup"><span data-stu-id="6f48f-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="6f48f-126">Нам не нужен два hello входов и один из выходов hello hello [выполнение скрипта R] [ execute-r-script] модуля в этом эксперименте, поэтому можно оставить их неприкрепленные.</span><span class="sxs-lookup"><span data-stu-id="6f48f-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="6f48f-127">Эта часть эксперимента hello теперь выглядит примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6f48f-127">This portion of hello experiment now looks something like this:</span></span>  

![Обучение модели][1]

<span data-ttu-id="6f48f-129">Теперь нам нужно tootell hello [Обучение модели] [ train-model] модуля, что мы хотим значение hello модели toopredict hello кредитного риска.</span><span class="sxs-lookup"><span data-stu-id="6f48f-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="6f48f-130">Выберите hello [Обучение модели] [ train-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="6f48f-131">В hello **свойства** области, нажмите кнопку **запуска средства выбора столбцов**.</span><span class="sxs-lookup"><span data-stu-id="6f48f-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="6f48f-132">В hello **выберите один столбец** диалоговое окно, введите в поле поиска hello в разделе «риск кредита» **доступные столбцы**, выберите «Риск кредита» ниже и нажмите кнопку со стрелкой вправо hello ( **>** ) toomove «Кредита риска» слишком**выбранные столбцы**.</span><span class="sxs-lookup"><span data-stu-id="6f48f-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![Выберите столбец hello кредитного риска для hello модуль обучения модели][0]

3. <span data-ttu-id="6f48f-134">Нажмите кнопку hello **ОК** флажок.</span><span class="sxs-lookup"><span data-stu-id="6f48f-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="6f48f-135">Двухклассовая машина опорных векторов;</span><span class="sxs-lookup"><span data-stu-id="6f48f-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="6f48f-136">Далее мы устанавливаем модель SVM hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="6f48f-137">Сначала немного информации о SVM.</span><span class="sxs-lookup"><span data-stu-id="6f48f-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="6f48f-138">"Повышенные" деревья принятия решения хорошо работают с атрибутами любого типа.</span><span class="sxs-lookup"><span data-stu-id="6f48f-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="6f48f-139">Тем не менее, так как модуль SVM hello создает линейный классификатор, hello модели, который создается, имеет hello наиболее Ошибка теста после всех числовых функций hello же шкале.</span><span class="sxs-lookup"><span data-stu-id="6f48f-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="6f48f-140">tooconvert все числовые функции toohello же масштабирования, мы используем преобразования «Tanh» (с hello [нормализовать данные] [ normalize-data] модуля).</span><span class="sxs-lookup"><span data-stu-id="6f48f-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="6f48f-141">Это преобразует нашей числа в диапазон hello [0,1].</span><span class="sxs-lookup"><span data-stu-id="6f48f-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="6f48f-142">модуль SVM Hello преобразует строки функции toocategorical функций и затем toobinary 0 и 1, поэтому мы не требуется toomanually преобразование строки функции.</span><span class="sxs-lookup"><span data-stu-id="6f48f-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="6f48f-143">Кроме того, мы не хотим tootransform hello кредитного риска в столбце (21) — это числовые, но это значение hello, мы обучения hello toopredict модели, поэтому необходимо tooleave его отдельно.</span><span class="sxs-lookup"><span data-stu-id="6f48f-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="6f48f-144">tooset модель SVM hello, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6f48f-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="6f48f-145">Найти hello [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] модуля в палитре модуля hello и перетащите его на холсте hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="6f48f-146">Щелкните правой кнопкой мыши hello [Обучение модели] [ train-model] модуль, выберите **копирования**, щелкните hello полотна правой кнопкой мыши и выберите **вставить**.</span><span class="sxs-lookup"><span data-stu-id="6f48f-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="6f48f-147">Здравствуйте, копия hello [Обучение модели] [ train-model] модуль имеет hello же Выбор столбцов, как исходный hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="6f48f-148">Подсоедините hello выход hello [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] toohello модуль слева входного порта hello второй [Обучение модели] [ train-model] модуль.</span><span class="sxs-lookup"><span data-stu-id="6f48f-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="6f48f-149">Найти hello [нормализовать данные] [ normalize-data] модуля и перетащите его на холсте hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="6f48f-150">Подсоедините hello левой выход слева hello [выполнение скрипта R] [ execute-r-script] toohello входного модуля этого модуля (Обратите внимание, что hello выходной порт модуля может быть подключенным toomore больше одного модуля).</span><span class="sxs-lookup"><span data-stu-id="6f48f-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="6f48f-151">Подключение hello слева выходной порт hello [нормализовать данные] [ normalize-data] модуль toohello право входному порту hello, во-вторых [Обучение модели] [ train-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="6f48f-152">Теперь эта часть эксперимента должна выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="6f48f-152">This portion of our experiment should now look something like this:</span></span>  

![Второй модели обучения hello][2]  

<span data-ttu-id="6f48f-154">Теперь настройка hello [нормализовать данные] [ normalize-data] модуля:</span><span class="sxs-lookup"><span data-stu-id="6f48f-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="6f48f-155">Нажмите кнопку tooselect hello [нормализовать данные] [ normalize-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="6f48f-156">В hello **свойства** выберите **Tanh** для hello **метод преобразования** параметра.</span><span class="sxs-lookup"><span data-stu-id="6f48f-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="6f48f-157">Нажмите кнопку **запуска средства выбора столбцов**, выберите «Нет столбцов» для **начинаются с**выберите **Include** в первом раскрывающемся списке hello выберите **тип столбца**в hello второго раскрывающегося списка и выберите **числовое** в третьем раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="6f48f-158">Указывает, преобразуются все hello числовых столбцов (и только числовые).</span><span class="sxs-lookup"><span data-stu-id="6f48f-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="6f48f-159">Нажмите кнопку hello toohello знак плюс (+) слева от этой строки — это создает строку из раскрывающихся списков.</span><span class="sxs-lookup"><span data-stu-id="6f48f-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="6f48f-160">Выберите **исключить** в первом раскрывающемся списке hello выберите **имена столбцов** в hello второго раскрывающегося списка и введите «Кредит риск» в поле текста hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="6f48f-161">Это указывает, что следует игнорировать этот столбец кредитного риска hello (требуются toodo это потому, что этот столбец является числовым и поэтому будет преобразовано мы не исключения).</span><span class="sxs-lookup"><span data-stu-id="6f48f-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="6f48f-162">Нажмите кнопку hello **ОК** флажок.</span><span class="sxs-lookup"><span data-stu-id="6f48f-162">Click hello **OK** check mark.</span></span>  

    ![Выберите столбцы для hello нормализовать данные модуля][5]

<span data-ttu-id="6f48f-164">Hello [нормализовать данные] [ normalize-data] модуль теперь является набор tooperform Tanh преобразование для всех числовых столбцов за исключением столбца hello кредитного риска.</span><span class="sxs-lookup"><span data-stu-id="6f48f-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="6f48f-165">Оценка и оценивать модели hello</span><span class="sxs-lookup"><span data-stu-id="6f48f-165">Score and evaluate hello models</span></span>

<span data-ttu-id="6f48f-166">Мы используем hello проверочных данных, который был в зависимости от hello [разбиение данных] [ split] tooscore модуль нашей обученных моделей.</span><span class="sxs-lookup"><span data-stu-id="6f48f-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="6f48f-167">Затем можно сравнить результаты двух моделей toosee hello, создавшего лучшие результаты hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="6f48f-168">Добавить модель оценки модулей hello</span><span class="sxs-lookup"><span data-stu-id="6f48f-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="6f48f-169">Найти hello [модель оценки] [ score-model] модуля и перетащите его на холсте hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="6f48f-170">Подключение hello [Обучение модели] [ train-model] модуль, который был подключен toohello [Двухклассового повышенного дерева принятия решений] [ two-class-boosted-decision-tree] модуль toohello левый вход порт hello [модель оценки] [ score-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="6f48f-171">Подключение правой hello [выполнение скрипта R] [ execute-r-script] toohello модуля (нашей проверочных данных) право входному порту hello [модель оценки] [ score-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![Модуль "Score Model" (Оценка модели) подключен][6]
   
   <span data-ttu-id="6f48f-173">Hello [модель оценки] [ score-model] модуля, теперь могут получить сведения о кредитной hello из hello проверочных данных, запустите его через модель hello, и прогнозы hello сравнения моделей hello создаются с hello фактическое кредит риска столбец в hello проверочных данных.</span><span class="sxs-lookup"><span data-stu-id="6f48f-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="6f48f-174">Скопируйте и вставьте hello [модель оценки] [ score-model] toocreate модуль второй копии.</span><span class="sxs-lookup"><span data-stu-id="6f48f-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="6f48f-175">Подключите выход hello модели SVM hello (то есть hello выходной порт hello [Обучение модели] [ train-model] модуль, который был подключен toohello [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] модуля) toohello входному порту hello второй [модель оценки] [ score-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="6f48f-176">Hello модели опорных Векторов у нас есть toodo hello и те же данные теста toohello преобразования, как это делалось toohello обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="6f48f-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="6f48f-177">Таким образом, скопируйте и вставьте hello [нормализовать данные] [ normalize-data] toocreate модуль второй копии и подключите его вправо toohello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="6f48f-178">Затем подсоедините hello левой выход hello [нормализовать данные] [ normalize-data] toohello модуль справа входному порту hello, во-вторых [модель оценки] [ score-model] модуль.</span><span class="sxs-lookup"><span data-stu-id="6f48f-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![Оба модуля "Score Model" (Оценка модели) подключены][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="6f48f-180">Добавить модуль оценки модели hello</span><span class="sxs-lookup"><span data-stu-id="6f48f-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="6f48f-181">tooevaluate hello двух результатов массовой оценки и сравнить их, мы используем [модель оценки] [ evaluate-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="6f48f-182">Найти hello [модель оценки] [ evaluate-model] модуля и перетащите его на холсте hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="6f48f-183">Подключение hello выходной порт hello [модель оценки] [ score-model] модуль, связанный с hello повышенного дерева модели toohello слева входному порту hello принятия решений [модель оценки] [ evaluate-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="6f48f-184">Подключение hello других [модель оценки] [ score-model] toohello модуль справа входному порту.</span><span class="sxs-lookup"><span data-stu-id="6f48f-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![Модуль "Evaluate Model" (Анализ модели) подключен][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="6f48f-186">Запустите эксперимент hello и проверьте результаты hello</span><span class="sxs-lookup"><span data-stu-id="6f48f-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="6f48f-187">toorun Здравствуйте эксперимент, выберите hello **ЗАПУСКА** кнопки ниже hello холста.</span><span class="sxs-lookup"><span data-stu-id="6f48f-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="6f48f-188">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6f48f-188">It may take a few minutes.</span></span> <span data-ttu-id="6f48f-189">Признак вращающийся для каждого модуля показывает, он работает, и затем зеленая галочка показывает завершении hello модуля.</span><span class="sxs-lookup"><span data-stu-id="6f48f-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="6f48f-190">Если флажок установлен для всех модулей hello, эксперимента hello завершит работу.</span><span class="sxs-lookup"><span data-stu-id="6f48f-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="6f48f-191">Hello эксперимента теперь должна выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6f48f-191">hello experiment should now look something like this:</span></span>  

![Сравнение обеих моделей][3]

<span data-ttu-id="6f48f-193">toocheck hello, щелкните выходной порт hello hello [модель оценки] [ evaluate-model] модуль и выберите **визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="6f48f-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="6f48f-194">Hello [модель оценки] [ evaluate-model] модуль создает пару кривых и метрик, которые позволяют вам toocompare hello результаты двух моделей Оцененный hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="6f48f-195">Можно просмотреть результаты hello как оператор характеристики приемника (ROC) кривых, точности и отзыва кривых или кривых точности прогнозов.</span><span class="sxs-lookup"><span data-stu-id="6f48f-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="6f48f-196">Дополнительные данные, отображаемые включает матрицей, совокупные значения для hello площадь под кривой hello (AUC) и другие показатели.</span><span class="sxs-lookup"><span data-stu-id="6f48f-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="6f48f-197">Можно изменить пороговое значение hello путем перемещения hello ползунок влево или вправо и увидеть, как он влияет hello набор показателей.</span><span class="sxs-lookup"><span data-stu-id="6f48f-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="6f48f-198">Щелкните toohello справа от диаграммы hello **Оцененный набор данных** или **Оцененный набор данных toocompare** toohighlight hello связанного кривых и toodisplay hello связанных метрик ниже.</span><span class="sxs-lookup"><span data-stu-id="6f48f-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="6f48f-199">В условных обозначениях hello кривых hello, «Оцененный набор данных» соответствует toohello левому входному порту hello [модель оценки] [ evaluate-model] модуля — в нашем случае это hello повышенного модели дерева принятия решений.</span><span class="sxs-lookup"><span data-stu-id="6f48f-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="6f48f-200">«Оцененный набор данных toocompare» соответствует toohello правый входной порт - модель SVM hello в нашем случае.</span><span class="sxs-lookup"><span data-stu-id="6f48f-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="6f48f-201">При выборе одного из этих меток, выделяется hello кривой для данной модели, а соответствующие метрики hello отображаются, как показано в следующих график hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![Кривые ROC для моделей][4]

<span data-ttu-id="6f48f-203">Изучив эти значения, можно решить, какую модель является ближайшим toogiving hello результаты, которые вы ищете.</span><span class="sxs-lookup"><span data-stu-id="6f48f-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="6f48f-204">Можно вернуться назад и завершение цикла эксперимента, изменив значения параметров в разных моделях hello.</span><span class="sxs-lookup"><span data-stu-id="6f48f-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="6f48f-205">Научные Hello и искусство интерпретации этих результатов и настройка производительности hello модели используется вне области hello этого пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="6f48f-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="6f48f-206">Для получения дополнительной справки может прочитать hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="6f48f-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="6f48f-207">Как tooevaluate модели производительности в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="6f48f-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="6f48f-208">Выберите параметры toooptimize алгоритмов в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="6f48f-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="6f48f-209">Интерпретация результатов модели в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="6f48f-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="6f48f-210">Каждый раз при выполнении эксперимента hello запись этой итерации сохраняется hello журнал выполнения.</span><span class="sxs-lookup"><span data-stu-id="6f48f-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="6f48f-211">Можно просматривать эти итераций и возвращать tooany из них, щелкнув **ПРОСМОТРЕТЬ ЖУРНАЛ ВЫПОЛНЕНИЯ** ниже hello холста.</span><span class="sxs-lookup"><span data-stu-id="6f48f-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="6f48f-212">Можно также щелкнуть **предыдущего запуска** в hello **свойства** области tooreturn toohello итерации, непосредственно предшествующего hello один было открыто.</span><span class="sxs-lookup"><span data-stu-id="6f48f-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="6f48f-213">Можно сделать копию какой-либо итерации эксперимента, щелкнув **SAVE AS** ниже hello холста.</span><span class="sxs-lookup"><span data-stu-id="6f48f-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="6f48f-214">Используйте hello эксперимента **Сводка** и **описание** tookeep свойства записи были проверены в эксперименте итераций.</span><span class="sxs-lookup"><span data-stu-id="6f48f-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="6f48f-215">Дополнительные сведения см. в статье [Управление итерациями экспериментов в Студии машинного обучения Azure](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="6f48f-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="6f48f-216">**Далее: [развернуть веб-службу hello](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="6f48f-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

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
