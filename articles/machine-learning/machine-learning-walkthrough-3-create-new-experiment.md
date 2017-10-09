---
title: "Шаг 3. Создание эксперимента машинного обучения | Документация Майкрософт"
description: "Шаг 3 из hello разработка прогнозирующего решения Пошаговое руководство: Создание нового эксперимента обучения в студии машинного обучения Azure."
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
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="db01d-103">Шаг 3. Создание эксперимента машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="db01d-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="db01d-104">Это третий шаг hello hello пошагового руководства, [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="db01d-104">This is hello third step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="db01d-105">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="db01d-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="db01d-106">Отправка существующих данных</span><span class="sxs-lookup"><span data-stu-id="db01d-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="db01d-107">**Создание нового эксперимента**</span><span class="sxs-lookup"><span data-stu-id="db01d-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="db01d-108">Обучать и оценивать модели hello</span><span class="sxs-lookup"><span data-stu-id="db01d-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="db01d-109">Развернуть веб-службу hello</span><span class="sxs-lookup"><span data-stu-id="db01d-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="db01d-110">Доступ к веб-службе hello</span><span class="sxs-lookup"><span data-stu-id="db01d-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="db01d-111">следующим шагом Hello в этом пошаговом руководстве является toocreate эксперимента в студии машинного обучения, использующий hello набор данных, которые мы отправлен.</span><span class="sxs-lookup"><span data-stu-id="db01d-111">hello next step in this walkthrough is toocreate an experiment in Machine Learning Studio that uses hello dataset we uploaded.</span></span>  

1. <span data-ttu-id="db01d-112">В Studio щелкните **+ создать** hello нижней части окна hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-112">In Studio, click **+NEW** at hello bottom of hello window.</span></span>
2. <span data-ttu-id="db01d-113">Выберите **ЭКСПЕРИМЕНТА**, а затем выберите "Пустой эксперимент".</span><span class="sxs-lookup"><span data-stu-id="db01d-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Создание нового эксперимента][0]

2. <span data-ttu-id="db01d-115">По умолчанию выберите hello поэкспериментировать имя hello верхней части холста hello и переименуйте его toosomething смысла.</span><span class="sxs-lookup"><span data-stu-id="db01d-115">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful.</span></span>

    ![Переименование эксперимента][5]
   
   > [!TIP]
   > <span data-ttu-id="db01d-117">Это toofill рекомендаций в **Сводка** и **описание** в эксперименте hello в hello **свойства** области.</span><span class="sxs-lookup"><span data-stu-id="db01d-117">It's a good practice toofill in **Summary** and **Description** for hello experiment in hello **Properties** pane.</span></span> <span data-ttu-id="db01d-118">Эти свойства, присвойте hello эксперимента hello toodocument вероятность того, кто просматривает его позже будет понять цели и методологии.</span><span class="sxs-lookup"><span data-stu-id="db01d-118">These properties give you hello chance toodocument hello experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Свойства эксперимента][6]
   > 
3. <span data-ttu-id="db01d-120">Hello модуля палитры toohello слева холст эксперимента hello, разверните **сохраненные наборы данных**.</span><span class="sxs-lookup"><span data-stu-id="db01d-120">In hello module palette toohello left of hello experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="db01d-121">Созданный в набор данных поиска hello **Мои наборы данных** и перетащите его на холсте hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-121">Find hello dataset you created under **My Datasets** and drag it onto hello canvas.</span></span> <span data-ttu-id="db01d-122">Hello набор данных также можно найти, введя имя hello в hello **поиска** поле над hello палитры.</span><span class="sxs-lookup"><span data-stu-id="db01d-122">You can also find hello dataset by entering hello name in hello **Search** box above hello palette.</span></span>  

    ![Добавить toohello эксперимента hello набора данных][7]

## <a name="prepare-hello-data"></a><span data-ttu-id="db01d-124">Подготовка данных hello</span><span class="sxs-lookup"><span data-stu-id="db01d-124">Prepare hello data</span></span>
<span data-ttu-id="db01d-125">Можно просмотреть hello первые 100 строк данных hello и некоторые статистические данные для всего набора данных hello: щелкните порт вывода hello hello набора данных (hello маленький кружок hello нижней) и выберите **визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="db01d-125">You can view hello first 100 rows of hello data and some statistical information for hello whole dataset: Click hello output port of hello dataset (hello small circle at hello bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="db01d-126">Файл данных hello не поставляются с заголовками столбцов, Studio разработала универсальный заголовки (Col1, Col2 *т. д.*).</span><span class="sxs-lookup"><span data-stu-id="db01d-126">Because hello data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="db01d-127">Хороший заголовки не essential toocreating модели, но они позволяют проще toowork с данными hello в эксперименте hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-127">Good headings aren't essential toocreating a model, but they make it easier toowork with hello data in hello experiment.</span></span> <span data-ttu-id="db01d-128">Кроме того при со временем мы опубликовать эту модель в веб-службе, заголовки hello выяснить hello столбцы toohello пользователем службы hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-128">Also, when we eventually publish this model in a web service, hello headings help identify hello columns toohello user of hello service.</span></span>  

<span data-ttu-id="db01d-129">Можно добавить заголовки столбцов с помощью hello [редактирование метаданных] [ edit-metadata] модуля.</span><span class="sxs-lookup"><span data-stu-id="db01d-129">We can add column headings using hello [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="db01d-130">Использовать hello [редактирование метаданных] [ edit-metadata] toochange метаданных модуля, связанные с набором данных.</span><span class="sxs-lookup"><span data-stu-id="db01d-130">You use hello [Edit Metadata][edit-metadata] module toochange metadata associated with a dataset.</span></span> <span data-ttu-id="db01d-131">В этом случае мы используем его tooprovide более понятные имена для заголовков столбцов.</span><span class="sxs-lookup"><span data-stu-id="db01d-131">In this case, we use it tooprovide more friendly names for column headings.</span></span> 

<span data-ttu-id="db01d-132">toouse [редактирование метаданных][edit-metadata], сначала необходимо указать, какие столбцы toomodify (в этом случае все из них.) Затем укажите действие toobe hello, для этих столбцов (в данном случае изменение заголовков столбцов.)</span><span class="sxs-lookup"><span data-stu-id="db01d-132">toouse [Edit Metadata][edit-metadata], you first specify which columns toomodify (in this case, all of them.) Next, you specify hello action toobe performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="db01d-133">В палитре hello модуль, введите «метаданные» в hello **поиска** поле.</span><span class="sxs-lookup"><span data-stu-id="db01d-133">In hello module palette, type "metadata" in hello **Search** box.</span></span> <span data-ttu-id="db01d-134">Hello [редактирование метаданных] [ edit-metadata] отображается в списке модулей hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-134">hello [Edit Metadata][edit-metadata] appears in hello module list.</span></span>

2. <span data-ttu-id="db01d-135">Щелкните и перетащите hello [редактирование метаданных] [ edit-metadata] модуля на hello холст и разместите его под hello набора данных, мы добавили в более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="db01d-135">Click and drag hello [Edit Metadata][edit-metadata] module onto hello canvas and drop it below hello dataset we added earlier.</span></span>

3. <span data-ttu-id="db01d-136">Подключения hello dataset toohello [редактирование метаданных][edit-metadata]: щелкните порт вывода hello hello набора данных (hello маленький кружок внизу hello hello набора данных), перетащите toohello входному порту [редактирование метаданных ] [ edit-metadata] (hello маленький кружок вверху hello модуля "hello"), затем отпустите кнопку мыши hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-136">Connect hello dataset toohello [Edit Metadata][edit-metadata]: click hello output port of hello dataset (hello small circle at hello bottom of hello dataset), drag toohello input port of [Edit Metadata][edit-metadata] (hello small circle at hello top of hello module), then release hello mouse button.</span></span> <span data-ttu-id="db01d-137">набор данных Hello и модуль оставались подключенными, даже если перемещать либо на холсте hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-137">hello dataset and module remain connected even if you move either around on hello canvas.</span></span>
   
   <span data-ttu-id="db01d-138">Hello эксперимента теперь должна выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db01d-138">hello experiment should now look something like this:</span></span>  
   
   ![Добавление модуля "Изменение метаданных"][1]
   
   <span data-ttu-id="db01d-140">Hello красный восклицательный знак указывает, что мы не задали еще hello свойства для этого модуля.</span><span class="sxs-lookup"><span data-stu-id="db01d-140">hello red exclamation mark indicates that we haven't set hello properties for this module yet.</span></span> <span data-ttu-id="db01d-141">Мы сделаем это позже.</span><span class="sxs-lookup"><span data-stu-id="db01d-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="db01d-142">Можно добавить модуль tooa комментарий, дважды щелкните модуль hello и вводить текст.</span><span class="sxs-lookup"><span data-stu-id="db01d-142">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="db01d-143">Это может помочь быстро выяснить делает какой модуль hello в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="db01d-143">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="db01d-144">В этом случае дважды щелкните hello [редактирование метаданных] [ edit-metadata] модуля и типа hello комментарий «добавить заголовки столбцов».</span><span class="sxs-lookup"><span data-stu-id="db01d-144">In this case, double-click hello [Edit Metadata][edit-metadata] module and type hello comment "Add column headings".</span></span> <span data-ttu-id="db01d-145">Щелкните любой другой hello холст tooclose hello текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="db01d-145">Click anywhere else on hello canvas tooclose hello text box.</span></span> <span data-ttu-id="db01d-146">toodisplay Здравствуйте комментарий, щелкните hello со стрелкой вниз в модуле hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-146">toodisplay hello comment, click hello down-arrow on hello module.</span></span>
   > 
   > ![Модуль Edit Metadata (Изменение метаданных) с добавленными комментариями][8]
   > 
4. <span data-ttu-id="db01d-148">Выберите [редактирование метаданных][edit-metadata]и в hello **свойства** toohello панели справа от холста hello щелкните **запуска средства выбора столбцов**.</span><span class="sxs-lookup"><span data-stu-id="db01d-148">Select [Edit Metadata][edit-metadata], and in hello **Properties** pane toohello right of hello canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="db01d-149">В hello **выберите столбцы** диалоговое окно, выберите все hello строк в **доступные столбцы** и нажмите кнопку > toomove их слишком**выбранные столбцы**.</span><span class="sxs-lookup"><span data-stu-id="db01d-149">In hello **Select columns** dialog, select all hello rows in **Available Columns** and click > toomove them too**Selected Columns**.</span></span>
   <span data-ttu-id="db01d-150">диалоговое окно приветствия должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db01d-150">hello dialog should look like this:</span></span>

   ![Селектор столбцов, где выделены все столбцы][2]

6. <span data-ttu-id="db01d-152">Нажмите кнопку hello **ОК** флажок.</span><span class="sxs-lookup"><span data-stu-id="db01d-152">Click hello **OK** check mark.</span></span>

7. <span data-ttu-id="db01d-153">Вернитесь в hello **свойства** панели найдите hello **новые имена столбцов** параметра.</span><span class="sxs-lookup"><span data-stu-id="db01d-153">Back in hello **Properties** pane, look for hello **New column names** parameter.</span></span> <span data-ttu-id="db01d-154">В этом поле введите список имен для hello 21 столбцов в наборе данных hello, разделенных запятыми и в порядке столбцов.</span><span class="sxs-lookup"><span data-stu-id="db01d-154">In this field, enter a list of names for hello 21 columns in hello dataset, separated by commas and in column order.</span></span> <span data-ttu-id="db01d-155">Имена столбцов hello можно получить из документации hello набора данных на веб-сайте UCI hello, или для удобства можно скопировать и вставить hello после списка:</span><span class="sxs-lookup"><span data-stu-id="db01d-155">You can obtain hello columns names from hello dataset documentation on hello UCI website, or for convenience you can copy and paste hello following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="db01d-156">Панель свойств Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db01d-156">hello Properties pane looks like this:</span></span>
   
   ![Свойства модуля "Изменение метаданных"][3]

> [!TIP]
> <span data-ttu-id="db01d-158">Заголовки столбцов tooverify hello, выполните эксперимент hello (щелкните **ЗАПУСКА** ниже холст эксперимента hello).</span><span class="sxs-lookup"><span data-stu-id="db01d-158">If you want tooverify hello column headings, run hello experiment (click **RUN** below hello experiment canvas).</span></span> <span data-ttu-id="db01d-159">При ее работы (зеленая галочка на [редактирование метаданных][edit-metadata]), щелкните выходной порт hello hello [редактирование метаданных] [ edit-metadata] модуль, а затем выберите **визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="db01d-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click hello output port of hello [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="db01d-160">Можно просмотреть выходные данные hello любого модуля в hello же выполняется hello tooview способом hello данных через эксперимент hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-160">You can view hello output of any module in hello same way tooview hello progress of hello data through hello experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="db01d-161">Создание обучающих и тестовых наборов данных</span><span class="sxs-lookup"><span data-stu-id="db01d-161">Create training and test datasets</span></span>
<span data-ttu-id="db01d-162">Необходимы некоторые tootrain hello модели данных и некоторые tootest его.</span><span class="sxs-lookup"><span data-stu-id="db01d-162">We need some data tootrain hello model and some tootest it.</span></span>
<span data-ttu-id="db01d-163">Поэтому следующий шаг hello hello эксперимента, мы разделить hello набора данных на два отдельных набора данных: один — для изучения нашей модели, а второй для ее проверки.</span><span class="sxs-lookup"><span data-stu-id="db01d-163">So in hello next step of hello experiment, we split hello dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="db01d-164">toodo это, мы используем hello [разбиение данных] [ split] модуля.</span><span class="sxs-lookup"><span data-stu-id="db01d-164">toodo this, we use hello [Split Data][split] module.</span></span>  

1. <span data-ttu-id="db01d-165">Найти hello [разбиение данных] [ split] модуля, перетащите его на холсте hello и подключите его toohello [редактирование метаданных] [ edit-metadata] модуля.</span><span class="sxs-lookup"><span data-stu-id="db01d-165">Find hello [Split Data][split] module, drag it onto hello canvas, and connect it toohello [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="db01d-166">По умолчанию hello пропорции разделения является 0.5 и hello **случайного разбиения** параметр имеет значение.</span><span class="sxs-lookup"><span data-stu-id="db01d-166">By default, hello split ratio is 0.5 and hello **Randomized split** parameter is set.</span></span> <span data-ttu-id="db01d-167">Это означает, что случайные половина данных hello выходных данных через один порт hello [разбиение данных] [ split] модуль и половина через hello других.</span><span class="sxs-lookup"><span data-stu-id="db01d-167">This means that a random half of hello data is output through one port of hello [Split Data][split] module, and half through hello other.</span></span> <span data-ttu-id="db01d-168">Вы можете настроить эти параметры, а также hello **случайное начальное значение** параметр toochange hello разделены на обучающие и проверочные данные.</span><span class="sxs-lookup"><span data-stu-id="db01d-168">You can adjust these parameters, as well as hello **Random seed** parameter, toochange hello split between training and testing data.</span></span> <span data-ttu-id="db01d-169">Для этого примера оставим их как есть.</span><span class="sxs-lookup"><span data-stu-id="db01d-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="db01d-170">Здравствуйте, свойство **часть строк в hello сначала выходной набор данных** определяет, какая часть данных hello выходных данных через hello *левой* порта вывода.</span><span class="sxs-lookup"><span data-stu-id="db01d-170">hello property **Fraction of rows in hello first output dataset** determines how much of hello data is output through hello *left* output port.</span></span> <span data-ttu-id="db01d-171">Для экземпляра Если too0.7 отношение hello, 70% hello данных является выходных данных через hello оставить порт и 30% через порт правой hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-171">For instance, if you set hello ratio too0.7, then 70% of hello data is output through hello left port and 30% through hello right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="db01d-172">Дважды щелкните hello [разбиение данных] [ split] модуля и ввести комментарий hello, «обучение и тестирование данные разделены на 50%».</span><span class="sxs-lookup"><span data-stu-id="db01d-172">Double-click hello [Split Data][split] module and enter hello comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="db01d-173">Мы можем использовать выходные данные hello hello [разбиение данных] [ split] модуль тем не менее мы, например, но позволяет выбрать toouse hello левой выходные данные в виде обучающих данных и правом hello выходные данные как проверочных данных.</span><span class="sxs-lookup"><span data-stu-id="db01d-173">We can use hello outputs of hello [Split Data][split] module however we like, but let's choose toouse hello left output as training data and hello right output as testing data.</span></span>  

<span data-ttu-id="db01d-174">Как упоминалось в hello [ранее](machine-learning-walkthrough-2-upload-data.md), ошибочную высокой кредитного риска в качестве низкая стоимость hello пять раз выше, чем стоимость hello ошибочную низкий кредитного риска в как high.</span><span class="sxs-lookup"><span data-stu-id="db01d-174">As mentioned in hello [previous step](machine-learning-walkthrough-2-upload-data.md), hello cost of misclassifying a high credit risk as low is five times higher than hello cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="db01d-175">tooaccount для этого мы создаем новый набор данных, отражающий эта функция затрат.</span><span class="sxs-lookup"><span data-stu-id="db01d-175">tooaccount for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="db01d-176">В hello новый набор данных в каждом примере высокого риска реплицируются пять раз, пока не реплицируются в каждом примере низким уровнем риска.</span><span class="sxs-lookup"><span data-stu-id="db01d-176">In hello new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="db01d-177">Эту репликацию можно выполнить с помощью кода R:</span><span class="sxs-lookup"><span data-stu-id="db01d-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="db01d-178">Поиск и перетащите hello [выполнение скрипта R] [ execute-r-script] модуля на холст эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-178">Find and drag hello [Execute R Script][execute-r-script] module onto hello experiment canvas.</span></span> 

2. <span data-ttu-id="db01d-179">Подключение hello слева выходной порт hello [разбиение данных] [ split] toohello модуль сначала входному порту («Dataset1») для hello [выполнение скрипта R] [ execute-r-script] модуль.</span><span class="sxs-lookup"><span data-stu-id="db01d-179">Connect hello left output port of hello [Split Data][split] module toohello first input port ("Dataset1") of hello [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="db01d-180">Дважды щелкните hello [выполнение скрипта R] [ execute-r-script] модуля и ввести комментарий hello, «Набор Корректировка себестоимости».</span><span class="sxs-lookup"><span data-stu-id="db01d-180">Double-click hello [Execute R Script][execute-r-script] module and enter hello comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="db01d-181">В hello **свойства** области, удалите текст по умолчанию hello в hello **R-сценарий** параметр и введите этот скрипт:</span><span class="sxs-lookup"><span data-stu-id="db01d-181">In hello **Properties** pane, delete hello default text in hello **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Сценарий R в модуле hello выполнение скрипта R][9]

<span data-ttu-id="db01d-183">Мы должны toodo этой же репликации операции для каждого выхода hello [разбиение данных] [ split] Корректировка себестоимости модуль, так что hello обучающих и проверочных данных имеют hello таким же.</span><span class="sxs-lookup"><span data-stu-id="db01d-183">We need toodo this same replication operation for each output of hello [Split Data][split] module so that hello training and testing data have hello same cost adjustment.</span></span> <span data-ttu-id="db01d-184">Здравствуйте, наиболее простым способом toodo, это путем дублирования hello [выполнение скрипта R] [ execute-r-script] модуля мы только что внесли и подключения его toohello других выходных портом hello [разбиение данных] [ split] модуля.</span><span class="sxs-lookup"><span data-stu-id="db01d-184">hello easiest way toodo this is by duplicating hello [Execute R Script][execute-r-script] module we just made and connecting it toohello other output port of hello [Split Data][split] module.</span></span>

1. <span data-ttu-id="db01d-185">Щелкните правой кнопкой мыши hello [выполнение скрипта R] [ execute-r-script] модуль и выберите **копирования**.</span><span class="sxs-lookup"><span data-stu-id="db01d-185">Right-click hello [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="db01d-186">Щелкните правой кнопкой мыши на холст эксперимента hello и выберите **вставить**.</span><span class="sxs-lookup"><span data-stu-id="db01d-186">Right-click hello experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="db01d-187">Перетащите новый модуль hello в положение, а затем подключите hello правой выходной порт hello [разбиение данных] [ split] toohello модуль сначала входному порту этого нового [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="db01d-187">Drag hello new module into position, and then connect hello right output port of hello [Split Data][split] module toohello first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="db01d-188">Hello нижней части холста hello, нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="db01d-188">At hello bottom of hello canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="db01d-189">Hello копии hello выполнение скрипта R модуля содержит hello же сценариев в hello исходного модуля.</span><span class="sxs-lookup"><span data-stu-id="db01d-189">hello copy of hello Execute R Script module contains hello same script as hello original module.</span></span> <span data-ttu-id="db01d-190">При копировании и вставке модуля на холсте hello, hello копирования сохраняет все свойства hello исходного hello.</span><span class="sxs-lookup"><span data-stu-id="db01d-190">When you copy and paste a module on hello canvas, hello copy retains all hello properties of hello original.</span></span>  
> 
> 

<span data-ttu-id="db01d-191">На эксперимент теперь выглядит приблизительно так:</span><span class="sxs-lookup"><span data-stu-id="db01d-191">Our experiment now looks something like this:</span></span>

![Добавление модуля Разделение и скриптов R][4]

<span data-ttu-id="db01d-193">Подробнее об использовании сценариев R в экспериментах см. в разделе [Расширение возможностей эксперимента с помощью R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="db01d-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="db01d-194">**Далее: [обучения и оценки моделей hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="db01d-194">**Next: [Train and evaluate hello models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

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
