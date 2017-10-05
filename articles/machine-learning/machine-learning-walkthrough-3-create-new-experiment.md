---
title: "Шаг 3. Создание эксперимента машинного обучения | Документация Майкрософт"
description: "Третий этап пошагового руководства по разработке прогнозного решения: создание эксперимента обучения в студии машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cd410316910bce76f5c915c06e83b24c034481b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="9db82-103">Шаг 3. Создание эксперимента машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="9db82-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="9db82-104">Это третий этап из пошагового руководства [Разработка решения для прогнозной аналитики в службе машинного обучения Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="9db82-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="9db82-105">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="9db82-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="9db82-106">Отправка существующих данных</span><span class="sxs-lookup"><span data-stu-id="9db82-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="9db82-107">**Создание нового эксперимента**</span><span class="sxs-lookup"><span data-stu-id="9db82-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="9db82-108">Обучение и анализ моделей</span><span class="sxs-lookup"><span data-stu-id="9db82-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="9db82-109">Развертывание веб-службы</span><span class="sxs-lookup"><span data-stu-id="9db82-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="9db82-110">Доступ к веб-службе</span><span class="sxs-lookup"><span data-stu-id="9db82-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="9db82-111">Следующим этапом в этом пошаговом руководстве является создание эксперимента в студии машинного обучения, который использует отправленный набор данных.</span><span class="sxs-lookup"><span data-stu-id="9db82-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span></span>  

1. <span data-ttu-id="9db82-112">В студии машинного обучения щелкните **+СОЗДАТЬ** в нижней части окна.</span><span class="sxs-lookup"><span data-stu-id="9db82-112">In Studio, click **+NEW** at the bottom of the window.</span></span>
2. <span data-ttu-id="9db82-113">Выберите **ЭКСПЕРИМЕНТА**, а затем выберите "Пустой эксперимент".</span><span class="sxs-lookup"><span data-stu-id="9db82-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Создание нового эксперимента][0]

2. <span data-ttu-id="9db82-115">В верхней части холста выберите имя эксперимента по умолчанию и присвойте ему понятное имя.</span><span class="sxs-lookup"><span data-stu-id="9db82-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span></span>

    ![Переименование эксперимента][5]
   
   > [!TIP]
   > <span data-ttu-id="9db82-117">Рекомендуем заполнить поля **Сводка** и **Описание** для эксперимента в области **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="9db82-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span></span> <span data-ttu-id="9db82-118">Эти свойства позволят вам задокументировать эксперимент, чтобы любой, кто откроет его позднее, смог понять ваши цели и методы.</span><span class="sxs-lookup"><span data-stu-id="9db82-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Свойства эксперимента][6]
   > 
3. <span data-ttu-id="9db82-120">На палитре модулей слева от полотна эксперимента разверните **Saved Datasets**(Сохраненные наборы данных).</span><span class="sxs-lookup"><span data-stu-id="9db82-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="9db82-121">Найдите набор данных, созданный в разделе **Мои наборы данных** , и перетащите его на холст.</span><span class="sxs-lookup"><span data-stu-id="9db82-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span></span> <span data-ttu-id="9db82-122">Набор данных можно также отыскать, введя имя в поле **Поиск** над палитрой.</span><span class="sxs-lookup"><span data-stu-id="9db82-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span></span>  

    ![Добавление набора данных в эксперимент][7]

## <a name="prepare-the-data"></a><span data-ttu-id="9db82-124">Подготовка данных</span><span class="sxs-lookup"><span data-stu-id="9db82-124">Prepare the data</span></span>
<span data-ttu-id="9db82-125">Чтобы просмотреть первые 100 строк данных и некоторые статистические сведения для всего набора данных, щелкните выходной порт набора данных (маленький кружок в нижней части) правой кнопкой мыши и выберите команду **Визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="9db82-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="9db82-126">Поскольку файл данных поступил без заголовков столбцов, студия предоставляет универсальные заголовки (Col1, Col2 *и т. д.*).</span><span class="sxs-lookup"><span data-stu-id="9db82-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="9db82-127">Понятные заголовки столбцов не имеют существенного значения для создания модели, однако они облегчат работу с данными в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="9db82-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span></span> <span data-ttu-id="9db82-128">Кроме того, при последующей публикации этой модели в веб-службе заголовки помогают определять столбцы пользователям службы.</span><span class="sxs-lookup"><span data-stu-id="9db82-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span></span>  

<span data-ttu-id="9db82-129">Заголовки столбцов можно добавить с помощью модуля [Edit Metadata][edit-metadata] (Изменение метаданных).</span><span class="sxs-lookup"><span data-stu-id="9db82-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="9db82-130">Модуль [Edit Metadata][edit-metadata] (Изменение метаданных) используется для изменения метаданных, связанных с набором данных.</span><span class="sxs-lookup"><span data-stu-id="9db82-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span></span> <span data-ttu-id="9db82-131">В этом случае мы используем его, чтобы предоставить более понятные имена заголовков столбцов.</span><span class="sxs-lookup"><span data-stu-id="9db82-131">In this case, we use it to provide more friendly names for column headings.</span></span> 

<span data-ttu-id="9db82-132">Для использования модуля [Edit Metadata][edit-metadata] (Изменение метаданных) сначала необходимо указать, какие столбцы будут изменены (в нашем случае все). Далее следует указать действие, которое будет выполнено с этими столбцами (в нашем случае изменение заголовков столбцов).</span><span class="sxs-lookup"><span data-stu-id="9db82-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="9db82-133">В палитре модуля введите "metadata" в поле **Поиск** .</span><span class="sxs-lookup"><span data-stu-id="9db82-133">In the module palette, type "metadata" in the **Search** box.</span></span> <span data-ttu-id="9db82-134">Модуль [Edit Metadata][edit-metadata] (Изменение метаданных) появляется в списке модулей.</span><span class="sxs-lookup"><span data-stu-id="9db82-134">The [Edit Metadata][edit-metadata] appears in the module list.</span></span>

2. <span data-ttu-id="9db82-135">Щелкните и перетащите модуль [Edit Metadata][edit-metadata] (Изменение метаданных) на холст и вставьте его под набором данных, добавленным ранее.</span><span class="sxs-lookup"><span data-stu-id="9db82-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span></span>

3. <span data-ttu-id="9db82-136">Подключите набор данных к модулю [Edit Metadata][edit-metadata] (Изменение метаданных). Щелкните порт вывода набора данных (маленький кружок в нижней части набора данных), перетащите в порт ввода модуля [Edit Metadata][edit-metadata] (Изменение метаданных) (маленький кружок в верхней части модуля) и отпустите кнопку мыши.</span><span class="sxs-lookup"><span data-stu-id="9db82-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span></span> <span data-ttu-id="9db82-137">Набор данных и модуль остаются подключенными даже при их перемещении на холсте.</span><span class="sxs-lookup"><span data-stu-id="9db82-137">The dataset and module remain connected even if you move either around on the canvas.</span></span>
   
   <span data-ttu-id="9db82-138">Теперь наш эксперимент должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9db82-138">The experiment should now look something like this:</span></span>  
   
   ![Добавление модуля "Изменение метаданных"][1]
   
   <span data-ttu-id="9db82-140">Красный восклицательный знак указывает, что для этого модуля свойства еще не заданы.</span><span class="sxs-lookup"><span data-stu-id="9db82-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span></span> <span data-ttu-id="9db82-141">Мы сделаем это позже.</span><span class="sxs-lookup"><span data-stu-id="9db82-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="9db82-142">Дважды щелкните модуль и введите текст, чтобы добавить комментарий.</span><span class="sxs-lookup"><span data-stu-id="9db82-142">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="9db82-143">Это поможет вам увидеть описание модуля и его действие в рамках эксперимента.</span><span class="sxs-lookup"><span data-stu-id="9db82-143">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="9db82-144">В этом случае дважды щелкните модуль [Edit Metadata][edit-metadata] (Изменение метаданных) и введите комментарий "Добавить заголовки столбцов".</span><span class="sxs-lookup"><span data-stu-id="9db82-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span></span> <span data-ttu-id="9db82-145">Щелкните в любом месте холста, чтобы закрыть текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="9db82-145">Click anywhere else on the canvas to close the text box.</span></span> <span data-ttu-id="9db82-146">Чтобы отобразить комментарий, щелкните стрелку вниз в модуле.</span><span class="sxs-lookup"><span data-stu-id="9db82-146">To display the comment, click the down-arrow on the module.</span></span>
   > 
   > ![Модуль Edit Metadata (Изменение метаданных) с добавленными комментариями][8]
   > 
4. <span data-ttu-id="9db82-148">Выберите [Изменить метаданные][edit-metadata], затем в области **Свойства** справа от холста щелкните **Launch column selector** (Запустить средство выбора столбцов).</span><span class="sxs-lookup"><span data-stu-id="9db82-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="9db82-149">В диалоговом окне **Select columns** (Выбор столбцов) выберите все строки в разделе **Available Columns** (Доступные столбцы) и нажмите кнопку ">", чтобы переместить их в раздел **Selected Columns** (Выбранные столбцы).</span><span class="sxs-lookup"><span data-stu-id="9db82-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span></span>
   <span data-ttu-id="9db82-150">Диалоговое окно должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9db82-150">The dialog should look like this:</span></span>

   ![Селектор столбцов, где выделены все столбцы][2]

6. <span data-ttu-id="9db82-152">Нажмите кнопку с флажком **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9db82-152">Click the **OK** check mark.</span></span>

7. <span data-ttu-id="9db82-153">На панели **Свойства** найдите параметр **New column names** (Новые имена столбцов).</span><span class="sxs-lookup"><span data-stu-id="9db82-153">Back in the **Properties** pane, look for the **New column names** parameter.</span></span> <span data-ttu-id="9db82-154">В этом поле введите список имен для 21 столбца набора данных с разделителями-запятыми и в порядке расположения столбцов.</span><span class="sxs-lookup"><span data-stu-id="9db82-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span></span> <span data-ttu-id="9db82-155">Вы можете получить имена столбцов из документации по наборам данных на веб-сайте UCI или скопировать и вставить следующий список.</span><span class="sxs-lookup"><span data-stu-id="9db82-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="9db82-156">Панель свойств выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9db82-156">The Properties pane looks like this:</span></span>
   
   ![Свойства модуля "Изменение метаданных"][3]

> [!TIP]
> <span data-ttu-id="9db82-158">Если вы хотите проверить заголовки столбцов, запустите эксперимент (щелкните **RUN** (Выполнить) под холстом эксперимента).</span><span class="sxs-lookup"><span data-stu-id="9db82-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span></span> <span data-ttu-id="9db82-159">После его завершения (в модуле [Edit Metadata][edit-metadata] (Изменение метаданных) появится зеленая галочка) щелкните порт вывода модуля [Edit Metadata][edit-metadata] (Изменение метаданных), а затем выберите **Визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="9db82-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="9db82-160">Аналогичным образом можно просматривать выход любого модуля, чтобы следить за ходом использования данных в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="9db82-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="9db82-161">Создание обучающих и тестовых наборов данных</span><span class="sxs-lookup"><span data-stu-id="9db82-161">Create training and test datasets</span></span>
<span data-ttu-id="9db82-162">Необходимы данные для обучения модели и данные для ее тестирования.</span><span class="sxs-lookup"><span data-stu-id="9db82-162">We need some data to train the model and some to test it.</span></span>
<span data-ttu-id="9db82-163">Поэтому на следующем шаге эксперимента мы разделяем набор данных на два отдельных набора: один для обучения модели, а другой для ее тестирования.</span><span class="sxs-lookup"><span data-stu-id="9db82-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="9db82-164">Для этого используется модуль [Split Data][split] (Разделение данных).</span><span class="sxs-lookup"><span data-stu-id="9db82-164">To do this, we use the [Split Data][split] module.</span></span>  

1. <span data-ttu-id="9db82-165">Найдите модуль [Split Data][split] (Разделение данных), перетащите его на холст и подключите к модулю [Edit Metadata][edit-metadata] (Изменение метаданных).</span><span class="sxs-lookup"><span data-stu-id="9db82-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="9db82-166">По умолчанию коэффициент разделения равен 0,5 и задан параметр **Randomized split** (Случайное разделение).</span><span class="sxs-lookup"><span data-stu-id="9db82-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span></span> <span data-ttu-id="9db82-167">Это означает, что случайно выбранная половина данных будет выводиться через один порт модуля [Split Data][split] (Разделение данных), а другая половина — через другой.</span><span class="sxs-lookup"><span data-stu-id="9db82-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span></span> <span data-ttu-id="9db82-168">Эти параметры можно отрегулировать, а также использовать параметр **Случайное начальное значение**, чтобы изменить соотношение между данными для обучения и тестирования.</span><span class="sxs-lookup"><span data-stu-id="9db82-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span></span> <span data-ttu-id="9db82-169">Для этого примера оставим их как есть.</span><span class="sxs-lookup"><span data-stu-id="9db82-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="9db82-170">Свойство **Fraction of rows in the first output dataset** (Доля строк в первом выходном наборе данных) определяет, какой объем данных будет выводиться через *левый* порт вывода.</span><span class="sxs-lookup"><span data-stu-id="9db82-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span></span> <span data-ttu-id="9db82-171">Например, если коэффициент установлен на 0,7, то 70% данных выходит через левый порт, а 30% — через правый.</span><span class="sxs-lookup"><span data-stu-id="9db82-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="9db82-172">Дважды щелкните модуль [Split Data][split] (Разделение данных) и введите комментарий "Соотношение данных обучения и тестирования составляет 50 %".</span><span class="sxs-lookup"><span data-stu-id="9db82-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="9db82-173">Выходные данные модуля [Split Data][split] (Разделение данных) можно использовать по своему усмотрению. Однако предлагаем использовать левый выход для обучения данных, а правый — для их оценки.</span><span class="sxs-lookup"><span data-stu-id="9db82-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span></span>  

<span data-ttu-id="9db82-174">Как отмечалось на [предыдущем шаге](machine-learning-walkthrough-2-upload-data.md), стоимость ошибочной классификации высокого кредитного риска как низкого в пять раз выше, чем стоимость ошибочной классификации низкого кредитного риска как высокого.</span><span class="sxs-lookup"><span data-stu-id="9db82-174">As mentioned in the [previous step](machine-learning-walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="9db82-175">Чтобы это учесть, создадим новый набор данных, отражающий эту функцию стоимости.</span><span class="sxs-lookup"><span data-stu-id="9db82-175">To account for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="9db82-176">В новом наборе данных каждый пример высокого риска реплицируется пять раз, а каждый пример низкого риска не реплицируется.</span><span class="sxs-lookup"><span data-stu-id="9db82-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="9db82-177">Эту репликацию можно выполнить с помощью кода R:</span><span class="sxs-lookup"><span data-stu-id="9db82-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="9db82-178">Найдите и перетащите модуль [Выполнить сценарий R][execute-r-script] на холст эксперимента.</span><span class="sxs-lookup"><span data-stu-id="9db82-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span></span> 

2. <span data-ttu-id="9db82-179">Подключите левый порт вывода модуля [Split Data][split] (Разделение данных) к первому порту ввода (Dataset1) модуля[Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="9db82-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="9db82-180">Дважды щелкните модуль [Выполнить сценарий R][execute-r-script] и введите комментарий "Задать корректировку стоимости".</span><span class="sxs-lookup"><span data-stu-id="9db82-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="9db82-181">На панели **Свойства** удалите текст по умолчанию в параметре **R-скрипт** и введите следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="9db82-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Сценарий R в модуле "Выполнить сценарий R"][9]

<span data-ttu-id="9db82-183">Необходимо проделать ту же операцию репликации для каждого выхода модуля [Split Data][split] (Разделение данных), чтобы данные для обучения и тестирования получили одинаковую корректировку стоимости.</span><span class="sxs-lookup"><span data-stu-id="9db82-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span></span> <span data-ttu-id="9db82-184">Проще всего это сделать, скопировав созданный модуль [Execute R Script][execute-r-script] (Выполнение сценария R) и подключив его к другому порту вывода модуля [Split Data][split] (Разделение данных).</span><span class="sxs-lookup"><span data-stu-id="9db82-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span></span>

1. <span data-ttu-id="9db82-185">Щелкните правой кнопкой мыши модуль [Выполнить сценарий R][execute-r-script] и выберите **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="9db82-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="9db82-186">Щелкните правой кнопкой мыши полотно эксперимента и выберите **Вставить**.</span><span class="sxs-lookup"><span data-stu-id="9db82-186">Right-click the experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="9db82-187">Перетащите модуль в позицию и подключите правый порт вывода модуля [Split Data][split] (Разделение данных) к первому порту ввода нового модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="9db82-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="9db82-188">В нижней части холста нажмите кнопку **Run** (Выполнить).</span><span class="sxs-lookup"><span data-stu-id="9db82-188">At the bottom of the canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="9db82-189">Копия модуля "Выполнение скрипта R" содержит тот же скрипт, что и исходный модуль.</span><span class="sxs-lookup"><span data-stu-id="9db82-189">The copy of the Execute R Script module contains the same script as the original module.</span></span> <span data-ttu-id="9db82-190">При копировании и вставке модуля на полотно копия сохраняет все свойства оригинала.</span><span class="sxs-lookup"><span data-stu-id="9db82-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span></span>  
> 
> 

<span data-ttu-id="9db82-191">На эксперимент теперь выглядит приблизительно так:</span><span class="sxs-lookup"><span data-stu-id="9db82-191">Our experiment now looks something like this:</span></span>

![Добавление модуля Разделение и скриптов R][4]

<span data-ttu-id="9db82-193">Подробнее об использовании сценариев R в экспериментах см. в разделе [Расширение возможностей эксперимента с помощью R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="9db82-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="9db82-194">**Дальнейшие действия: [обучение и анализ моделей](machine-learning-walkthrough-4-train-and-evaluate-models.md)**.</span><span class="sxs-lookup"><span data-stu-id="9db82-194">**Next: [Train and evaluate the models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
