---
title: "aaaA простого эксперимента в студии машинного обучения | Документы Microsoft"
description: "В этом пошаговом руководстве по машинному обучению описано, как создать простой эксперимент по обработке и анализу данных. Мы будем прогнозировать цена hello автомобиля с помощью алгоритма регрессии."
keywords: "эксперимент,линейная регрессия,алгоритмы машинного обучения,руководство по машинному обучению,приемы прогнозного моделирования,эксперимент по обработке и анализу данных"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="1865c-105">Руководство по машинному обучению. Создание первого эксперимента по обработке и анализу данных в Студии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="1865c-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="1865c-106">Если вы еще не использовали **студию машинного обучения Azure**, это руководство предназначено для вас.</span><span class="sxs-lookup"><span data-stu-id="1865c-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="1865c-107">В этом учебнике мы рассмотрим как toouse Studio для hello сначала время toocreate эксперимента машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="1865c-107">In this tutorial, we'll walk through how toouse Studio for hello first time toocreate a machine learning experiment.</span></span> <span data-ttu-id="1865c-108">будет произведена проверка эксперимента Hello аналитической модели, прогнозирующей hello цены на основе разных переменных, таких как создание и технические спецификации автомобилей.</span><span class="sxs-lookup"><span data-stu-id="1865c-108">hello experiment will test an analytical model that predicts hello price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="1865c-109">Этот учебник показывает, основы hello модулей как toodrag перетаскивания в свой эксперимент соединять их запуска эксперимента hello и просмотрите результаты hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-109">This tutorial shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="1865c-110">Мы не будем что toodiscuss hello общий раздел машинного обучения или как tooselect и использование hello 100 + встроенные алгоритмы данных манипуляции модули и включены в Studio.</span><span class="sxs-lookup"><span data-stu-id="1865c-110">We're not going toodiscuss hello general topic of machine learning or how tooselect and use hello 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="1865c-111">Если вы новый обучения toomachine hello серия видеоматериалов [обработки и анализа данных для начинающих](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) может быть toostart лучше всего.</span><span class="sxs-lookup"><span data-stu-id="1865c-111">If you're new toomachine learning, hello video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place toostart.</span></span> <span data-ttu-id="1865c-112">Эта серия видеоматериалов является обучения toomachine значительные введение, с использованием естественного языка и понятий.</span><span class="sxs-lookup"><span data-stu-id="1865c-112">This video series is a great introduction toomachine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="1865c-113">Если вы знакомы с машинного обучения, но вы ищете более общие сведения о студии машинного обучения и hello алгоритмов машинного обучения содержащихся в нем, Вот некоторые хорошо ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1865c-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and hello machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="1865c-114">Что такое Студия машинного обучения?</span><span class="sxs-lookup"><span data-stu-id="1865c-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="1865c-115">Это общий обзор студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="1865c-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="1865c-116">[Машинного обучения основы с примерами алгоритм](machine-learning-basics-infographic-with-algorithm-examples.md) -это инфографикой полезно использовать toolearn Дополнительные сведения о различных типов hello алгоритмов машинного обучения, включенных в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="1865c-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want toolearn more about hello different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="1865c-117">[Машинного обучения руководство](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -в настоящем руководстве описывается hello инфографикой выше, а в интерактивном формате аналогичные сведения.</span><span class="sxs-lookup"><span data-stu-id="1865c-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as hello infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="1865c-118">[Машинного обучения алгоритм памятку](machine-learning-algorithm-cheat-sheet.md) и [как toochoose алгоритмы машинного обучения Microsoft Azure](machine-learning-algorithm-choice.md) — это загружаемый плакат и сопутствующей статье обсуждается алгоритмы Studio hello в глубину.</span><span class="sxs-lookup"><span data-stu-id="1865c-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss hello Studio algorithms in depth.</span></span>
- <span data-ttu-id="1865c-119">[Студии машинного обучения: Алгоритм и модуль справки](https://msdn.microsoft.com/library/azure/dn905974.aspx) -это hello полный справочник для всех модулей студии, включая алгоритмы машинного обучения</span><span class="sxs-lookup"><span data-stu-id="1865c-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is hello complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="1865c-120">Как работает Студия машинного обучения?</span><span class="sxs-lookup"><span data-stu-id="1865c-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="1865c-121">Студия машинного обучения позволяет легко tooset копирование эксперимента с помощью модулей и перетащите запрограммированных ранее с помощью методик прогнозирующего моделирования.</span><span class="sxs-lookup"><span data-stu-id="1865c-121">Machine Learning Studio makes it easy tooset up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="1865c-122">Используя интерактивное визуальное рабочее пространство, вы можете перетаскивать нужные ***наборы данных*** и ***модули анализа*** на интерактивный холст.</span><span class="sxs-lookup"><span data-stu-id="1865c-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="1865c-123">При подключении к вместе tooform ***поэкспериментировать*** работы в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="1865c-123">You connect them together tooform an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="1865c-124">Вы ***создать модель***, ***обучения модели hello***, и ***оценки и тестирования hello модели***.</span><span class="sxs-lookup"><span data-stu-id="1865c-124">You ***create a model***, ***train hello model***, and ***score and test hello model***.</span></span>

<span data-ttu-id="1865c-125">Можно выполнять итерацию по проекту модели редактирования эксперимента hello и запуск до его дает hello результаты, которые вы ищете.</span><span class="sxs-lookup"><span data-stu-id="1865c-125">You can iterate on your model design, editing hello experiment and running it until it gives you hello results you're looking for.</span></span> <span data-ttu-id="1865c-126">Когда модель будет готова, ее можно опубликовать как ***веб-службу***. Это позволит другим пользователям отправлять данные в модель и получать по ним прогнозы.</span><span class="sxs-lookup"><span data-stu-id="1865c-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="1865c-127">Запуск студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="1865c-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="1865c-128">слишком перейти к выполнению Studio tooget[https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="1865c-128">tooget started with Studio, go too[https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="1865c-129">Если вы уже пользовались студией машинного обучения, щелкните **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="1865c-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="1865c-130">Если же нет, сначала щелкните **Sign up here** (Регистрация) и выберите бесплатный или платный вариант использования.</span><span class="sxs-lookup"><span data-stu-id="1865c-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="1865c-131">![Войдите в Studio обучения tooMachine][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="1865c-131">![Sign in tooMachine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="1865c-132">
***Войдите в Studio обучения tooMachine***</span><span class="sxs-lookup"><span data-stu-id="1865c-132">
***Sign in tooMachine Learning Studio***</span></span>

## <a name="five-steps-toocreate-an-experiment"></a><span data-ttu-id="1865c-133">Пять шагов toocreate эксперимента</span><span class="sxs-lookup"><span data-stu-id="1865c-133">Five steps toocreate an experiment</span></span>

<span data-ttu-id="1865c-134">В этом учебнике обучения машины и вы перейдете выполните пять основных шагов toobuild эксперимента в студии машинного обучения toocreate, обучение, оценка модели:</span><span class="sxs-lookup"><span data-stu-id="1865c-134">In this machine learning tutorial, you'll follow five basic steps toobuild an experiment in Machine Learning Studio toocreate, train, and score your model:</span></span>

- <span data-ttu-id="1865c-135">**Создание модели**</span><span class="sxs-lookup"><span data-stu-id="1865c-135">**Create a model**</span></span>
    - <span data-ttu-id="1865c-136">[Шаг 1. Получение данных]</span><span class="sxs-lookup"><span data-stu-id="1865c-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="1865c-137">[Шаг 2: Подготовка данных hello]</span><span class="sxs-lookup"><span data-stu-id="1865c-137">[Step 2: Prepare hello data]</span></span>
    - <span data-ttu-id="1865c-138">[Шаг 3. Определение признаков]</span><span class="sxs-lookup"><span data-stu-id="1865c-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="1865c-139">**Обучение модели hello**</span><span class="sxs-lookup"><span data-stu-id="1865c-139">**Train hello model**</span></span>
    - <span data-ttu-id="1865c-140">[Шаг 4. Выбор и применение алгоритма обучения]</span><span class="sxs-lookup"><span data-stu-id="1865c-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="1865c-141">**Здравствуйте, модель оценки и тестирования**</span><span class="sxs-lookup"><span data-stu-id="1865c-141">**Score and test hello model**</span></span>
    - <span data-ttu-id="1865c-142">[Шаг 5. Прогнозирование цен на новые автомобили]</span><span class="sxs-lookup"><span data-stu-id="1865c-142">[Step 5: Predict new automobile prices]</span></span>

[Шаг 1. Получение данных]: #step-1-get-data
[Шаг 2: Подготовка данных hello]: #step-2-prepare-the-data
[Шаг 3. Определение признаков]: #step-3-define-features
[Шаг 4. Выбор и применение алгоритма обучения]: #step-4-choose-and-apply-a-learning-algorithm
[Шаг 5. Прогнозирование цен на новые автомобили]: #step-5-predict-new-automobile-prices

> [!TIP] 
> <span data-ttu-id="1865c-148">Можно найти рабочую копию hello после эксперимента в hello [коллекции аналитики Cortana](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="1865c-148">You can find a working copy of hello following experiment in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="1865c-149">Go слишком**[первый обработки и анализа данных поэкспериментировать - прогноз цена автомобиль](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  и нажмите кнопку **в Studio** toodownload копию hello эксперимента в вашей машинного обучения Область студии.</span><span class="sxs-lookup"><span data-stu-id="1865c-149">Go too**[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="1865c-150">Шаг 1. Получение данных</span><span class="sxs-lookup"><span data-stu-id="1865c-150">Step 1: Get data</span></span>

<span data-ttu-id="1865c-151">Hello прежде всего необходимо tooperform машинного обучения — данные.</span><span class="sxs-lookup"><span data-stu-id="1865c-151">hello first thing you need tooperform machine learning is data.</span></span>
<span data-ttu-id="1865c-152">В студию машинного обучения входит несколько примеров наборов данных на выбор. Также данные можно импортировать из других источников.</span><span class="sxs-lookup"><span data-stu-id="1865c-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="1865c-153">В этом примере мы будем использовать hello примера набора данных, **автомобиль цена данных (Raw)**, включается в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="1865c-153">For this example, we'll use hello sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="1865c-154">В этом наборе данных содержится информация о разных автомобилях, включая сведения о производителе, модели, технических характеристиках и цене.</span><span class="sxs-lookup"><span data-stu-id="1865c-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="1865c-155">Ниже показано, как tooget hello набора данных в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="1865c-155">Here's how tooget hello dataset into your experiment.</span></span>

1. <span data-ttu-id="1865c-156">Создание нового эксперимента, щелкнув **+ создать** hello нижней части окна hello студии машинного обучения, выберите **ПОЭКСПЕРИМЕНТИРОВАТЬ**и выберите **пустой поэкспериментировать**.</span><span class="sxs-lookup"><span data-stu-id="1865c-156">Create a new experiment by clicking **+NEW** at hello bottom of hello Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="1865c-157">Hello эксперимента присваивается имя по умолчанию, можно увидеть hello верхней части холста hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-157">hello experiment is given a default name that you can see at hello top of hello canvas.</span></span> <span data-ttu-id="1865c-158">Выделите этот текст и переименуйте его в toosomething осмысленное, например, **автомобиль цена прогноза**.</span><span class="sxs-lookup"><span data-stu-id="1865c-158">Select this text and rename it toosomething meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="1865c-159">Имя Hello не toobe уникальным.</span><span class="sxs-lookup"><span data-stu-id="1865c-159">hello name doesn't need toobe unique.</span></span>

    ![Переименование эксперимента hello][rename-experiment]

2. <span data-ttu-id="1865c-161">toohello левой части холст эксперимента hello является палитры наборы данных и модулей.</span><span class="sxs-lookup"><span data-stu-id="1865c-161">toohello left of hello experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="1865c-162">Тип **автомобиль** в поле поиска hello hello верхней части этого палитры toofind hello набора данных с меткой **автомобиль цена данных (Raw)**.</span><span class="sxs-lookup"><span data-stu-id="1865c-162">Type **automobile** in hello Search box at hello top of this palette toofind hello dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="1865c-163">Перетащите этот холст эксперимента toohello набора данных.</span><span class="sxs-lookup"><span data-stu-id="1865c-163">Drag this dataset toohello experiment canvas.</span></span>

    <span data-ttu-id="1865c-164">![Найти автомобиль hello набора данных и перетащите его на холст эксперимента hello][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-164">![Find hello automobile dataset and drag it onto hello experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="1865c-165">***Найти автомобиль hello набора данных и перетащите его на холст эксперимента hello***</span><span class="sxs-lookup"><span data-stu-id="1865c-165">***Find hello automobile dataset and drag it onto hello experiment canvas***</span></span>

<span data-ttu-id="1865c-166">toosee то, что эти данные, как выглядит, щелкните выходной порт hello внизу hello автомобиль hello набора данных, а затем выберите **визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="1865c-166">toosee what this data looks like, click hello output port at hello bottom of hello automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="1865c-167">![Щелкните порт вывода hello и выберите «Визуализация»][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="1865c-167">![Click hello output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="1865c-168">
***Щелкните порт вывода hello и выберите «Визуализация»***</span><span class="sxs-lookup"><span data-stu-id="1865c-168">
***Click hello output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="1865c-169">Наборы данных и модули ввод и порты представленный малые круги - входных портов вверху hello вывод порты внизу hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-169">Datasets and modules have input and output ports represented by small circles - input ports at hello top, output ports at hello bottom.</span></span>
<span data-ttu-id="1865c-170">toocreate потока данных с помощью эксперимента, то необходимо подключить порт вывода одного модуля tooan входного порта другого.</span><span class="sxs-lookup"><span data-stu-id="1865c-170">toocreate a flow of data through your experiment, you'll connect an output port of one module tooan input port of another.</span></span>
<span data-ttu-id="1865c-171">В любое время можно щелкнуть hello выходной порт из набора данных или модуля toosee hello как выглядят данные в этот момент в потоке данных hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-171">At any time, you can click hello output port of a dataset or module toosee what hello data looks like at that point in hello data flow.</span></span>

<span data-ttu-id="1865c-172">В этот образец набора данных каждый экземпляр автомобиль появляется как строка и hello переменные, связанные с каждой автомобиль отображаются в виде столбцов.</span><span class="sxs-lookup"><span data-stu-id="1865c-172">In this sample dataset, each instance of an automobile appears as a row, and hello variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="1865c-173">Заданы переменные hello для конкретных автомобиль, мы будем tootry toopredict hello цена в крайнем правом столбце (столбец 26, под названием «price»).</span><span class="sxs-lookup"><span data-stu-id="1865c-173">Given hello variables for a specific automobile, we're going tootry toopredict hello price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="1865c-174">![Просмотр данных автомобиль hello в окне визуализации данных hello][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="1865c-174">![View hello automobile data in hello data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="1865c-175">
***Просмотр данных автомобиль hello в окне визуализации данных hello***</span><span class="sxs-lookup"><span data-stu-id="1865c-175">
***View hello automobile data in hello data visualization window***</span></span>

<span data-ttu-id="1865c-176">Hello закрыть окно визуализации, щелкнув hello»**x**» в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-176">Close hello visualization window by clicking hello "**x**" in hello upper-right corner.</span></span>

## <a name="step-2-prepare-hello-data"></a><span data-ttu-id="1865c-177">Шаг 2: Подготовка данных hello</span><span class="sxs-lookup"><span data-stu-id="1865c-177">Step 2: Prepare hello data</span></span>

<span data-ttu-id="1865c-178">Перед анализом, как правило, требуется определенная предварительная обработка набора данных.</span><span class="sxs-lookup"><span data-stu-id="1865c-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="1865c-179">Например вы могли заметить hello отсутствующих значений в столбцах hello различных строк.</span><span class="sxs-lookup"><span data-stu-id="1865c-179">For example, you might have noticed hello missing values present in hello columns of various rows.</span></span> <span data-ttu-id="1865c-180">Эти отсутствующие значения должны toobe очищен, hello модель может анализировать данные hello правильно.</span><span class="sxs-lookup"><span data-stu-id="1865c-180">These missing values need toobe cleaned so hello model can analyze hello data correctly.</span></span> <span data-ttu-id="1865c-181">В нашем случае мы удалим все строки, в которых есть недостающие значения.</span><span class="sxs-lookup"><span data-stu-id="1865c-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="1865c-182">Кроме того, hello **нормализованные потери** столбец имеет большую часть отсутствующие значения, поэтому мы исключим этот столбец из модели hello вообще.</span><span class="sxs-lookup"><span data-stu-id="1865c-182">Also, hello **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from hello model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="1865c-183">Чистящая hello отсутствующих значений из входных данных является необходимым условием для использования большинства модулей hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-183">Cleaning hello missing values from input data is a prerequisite for using most of hello modules.</span></span>

<span data-ttu-id="1865c-184">Сначала мы добавляем модуль, который удаляет hello **нормализованные потери** столбца полностью, и мы добавьте другой модуль, который удаляет все строки, отсутствуют данные.</span><span class="sxs-lookup"><span data-stu-id="1865c-184">First we add a module that removes hello **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="1865c-185">Тип **выберите столбцы** в поле поиска hello hello верхней части палитру toofind hello модуля hello [Выбор столбцов в наборе данных] [ select-columns] модуля, перетащите его toohello холст эксперимента .</span><span class="sxs-lookup"><span data-stu-id="1865c-185">Type **select columns** in hello Search box at hello top of hello module palette toofind hello [Select Columns in Dataset][select-columns] module, then drag it toohello experiment canvas.</span></span> <span data-ttu-id="1865c-186">Этот модуль позволяет нам tooselect Здравствуйте, какие столбцы данных, мы должны tooinclude или исключить из модели.</span><span class="sxs-lookup"><span data-stu-id="1865c-186">This module allows us tooselect which columns of data we want tooinclude or exclude in hello model.</span></span>

2. <span data-ttu-id="1865c-187">Подключение hello выходной порт hello **автомобиль цена данных (Raw)** toohello набора данных входному порту hello [Выбор столбцов в наборе данных] [ select-columns] модуля.</span><span class="sxs-lookup"><span data-stu-id="1865c-187">Connect hello output port of hello **Automobile price data (Raw)** dataset toohello input port of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="1865c-188">![Добавьте холст эксперимента toohello модуль «Выберите столбцы в наборе данных» hello и соедините его][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-188">![Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="1865c-189">***Добавьте холст эксперимента toohello модуль «Выберите столбцы в наборе данных» hello и соедините его***</span><span class="sxs-lookup"><span data-stu-id="1865c-189">***Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it***</span></span>

3. <span data-ttu-id="1865c-190">Нажмите кнопку hello [Выбор столбцов в наборе данных] [ select-columns] модуль и выберите команду **запуска средства выбора столбцов** в hello **свойства** области.</span><span class="sxs-lookup"><span data-stu-id="1865c-190">Click hello [Select Columns in Dataset][select-columns] module and click **Launch column selector** in hello **Properties** pane.</span></span>

    - <span data-ttu-id="1865c-191">В левой части экрана приветствия щелкните **с правилами**</span><span class="sxs-lookup"><span data-stu-id="1865c-191">On hello left, click **With rules**</span></span>
    - <span data-ttu-id="1865c-192">В разделе **Begin With** (Начинаются с) нажмите кнопку **All columns** (Все столбцы).</span><span class="sxs-lookup"><span data-stu-id="1865c-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="1865c-193">В данном случае [Выбор столбцов в наборе данных] [ select-columns] toopass через все столбцы hello (за исключением этих столбцов, мы о tooexclude).</span><span class="sxs-lookup"><span data-stu-id="1865c-193">This directs [Select Columns in Dataset][select-columns] toopass through all hello columns (except those columns we're about tooexclude).</span></span>
    - <span data-ttu-id="1865c-194">Hello раскрывающийся список, выберите **исключить** и **имена столбцов**, затем щелкните внутри текстового поля hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-194">From hello drop-downs, select **Exclude** and **column names**, and then click inside hello text box.</span></span> <span data-ttu-id="1865c-195">Отобразится список столбцов.</span><span class="sxs-lookup"><span data-stu-id="1865c-195">A list of columns is displayed.</span></span> <span data-ttu-id="1865c-196">Выберите **нормализованные потери**, и это toohello добавлено текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="1865c-196">Select **normalized-losses**, and it's added toohello text box.</span></span>
    - <span data-ttu-id="1865c-197">Щелкните hello флажок (ОК) кнопку tooclose hello столбец выделения (на hello нижнего правого).</span><span class="sxs-lookup"><span data-stu-id="1865c-197">Click hello check mark (OK) button tooclose hello column selector (on hello lower-right).</span></span>

    <span data-ttu-id="1865c-198">![Запустить селектор столбцов hello и исключить столбец «нормализованные потери» hello][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-198">![Launch hello column selector and exclude hello "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="1865c-199">***Запустить селектор столбцов hello и исключить столбец «нормализованные потери» hello***</span><span class="sxs-lookup"><span data-stu-id="1865c-199">***Launch hello column selector and exclude hello "normalized-losses" column***</span></span>

    <span data-ttu-id="1865c-200">Панель свойств hello сейчас для **Выбор столбцов в наборе данных** указывает, что он будет проходить все столбцы из набора данных hello, за исключением **нормализованные потери**.</span><span class="sxs-lookup"><span data-stu-id="1865c-200">Now hello properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from hello dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="1865c-201">![Панель свойств Hello показывает исключить этот столбец «нормализованные потери» hello][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-201">![hello properties pane shows that hello "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="1865c-202">***Панель свойств Hello показывает исключить этот столбец «нормализованные потери» hello***</span><span class="sxs-lookup"><span data-stu-id="1865c-202">***hello properties pane shows that hello "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="1865c-203">Можно добавить модуль tooa комментарий, дважды щелкните модуль hello и вводить текст.</span><span class="sxs-lookup"><span data-stu-id="1865c-203">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="1865c-204">Это может помочь быстро выяснить делает какой модуль hello в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="1865c-204">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="1865c-205">В этом случае дважды щелкните hello [Выбор столбцов в наборе данных] [ select-columns] модуля и типа hello комментарий «Exclude нормализовать убытки».</span><span class="sxs-lookup"><span data-stu-id="1865c-205">In this case double-click hello [Select Columns in Dataset][select-columns] module and type hello comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="1865c-206">![Дважды щелкните модуль tooadd комментарий][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-206">![Double-click a module tooadd a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="1865c-207">***Дважды щелкните модуль tooadd комментарий***</span><span class="sxs-lookup"><span data-stu-id="1865c-207">***Double-click a module tooadd a comment***</span></span>

3. <span data-ttu-id="1865c-208">Перетащите hello [Очистка недостающих данных] [ clean-missing-data] toohello модуль экспериментов холст и подключите его toohello [Выбор столбцов в наборе данных] [ select-columns] модуля.</span><span class="sxs-lookup"><span data-stu-id="1865c-208">Drag hello [Clean Missing Data][clean-missing-data] module toohello experiment canvas and connect it toohello [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="1865c-209">В hello **свойства** выберите **удалить всю строку** под **Очистка режим**.</span><span class="sxs-lookup"><span data-stu-id="1865c-209">In hello **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="1865c-210">В данном случае [Очистка недостающих данных] [ clean-missing-data] tooclean hello данных путем удаления строк, имеющих отсутствующих значений.</span><span class="sxs-lookup"><span data-stu-id="1865c-210">This directs [Clean Missing Data][clean-missing-data] tooclean hello data by removing rows that have any missing values.</span></span> <span data-ttu-id="1865c-211">Дважды щелкните модуль hello и введите комментарий hello, «Удалить отсутствующие значения строки».</span><span class="sxs-lookup"><span data-stu-id="1865c-211">Double-click hello module and type hello comment "Remove missing value rows."</span></span>

    <span data-ttu-id="1865c-212">![Режим очистки hello набора слишком «удалить всю строку» для модуля «Очистка недостающих данных» hello][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-212">![Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="1865c-213">***Режим очистки hello набора слишком «удалить всю строку» для модуля «Очистка недостающих данных» hello***</span><span class="sxs-lookup"><span data-stu-id="1865c-213">***Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="1865c-214">Запустите эксперимент hello, нажав кнопку **ЗАПУСКА** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="1865c-214">Run hello experiment by clicking **RUN** at hello bottom of hello page.</span></span>

    <span data-ttu-id="1865c-215">Hello эксперимента закончит работу, все модули hello после tooindicate Зеленый флажок, который успешно завершено.</span><span class="sxs-lookup"><span data-stu-id="1865c-215">When hello experiment has finished running, all hello modules have a green check mark tooindicate that they finished successfully.</span></span> <span data-ttu-id="1865c-216">Обратите внимание также hello **по завершении выполнения** состояние в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-216">Notice also hello **Finished running** status in hello upper-right corner.</span></span>

<span data-ttu-id="1865c-217">![После его запуска эксперимента hello должен выглядеть примерно следующим образом][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="1865c-217">![After running it, hello experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="1865c-218">
***После его запуска эксперимента hello должен выглядеть примерно следующим образом***</span><span class="sxs-lookup"><span data-stu-id="1865c-218">
***After running it, hello experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="1865c-219">Почему запустим эксперимента hello сейчас?</span><span class="sxs-lookup"><span data-stu-id="1865c-219">Why did we run hello experiment now?</span></span> <span data-ttu-id="1865c-220">Путем выполнения эксперимента hello, передавать hello определения столбцов данных из hello dataset с помощью hello [Выбор столбцов в наборе данных] [ select-columns] модуля и через hello [Очистка недостающих данных] [ clean-missing-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="1865c-220">By running hello experiment, hello column definitions for our data pass from hello dataset, through hello [Select Columns in Dataset][select-columns] module, and through hello [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="1865c-221">Это означает, что все модули, мы подключаемся слишком[Очистка недостающих данных] [ clean-missing-data] также будет иметь такой же информацией.</span><span class="sxs-lookup"><span data-stu-id="1865c-221">This means that any modules we connect too[Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="1865c-222">Все, которые уже были выполнены в эксперименте hello точку toothis данные чистой hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-222">All we have done in hello experiment up toothis point is clean hello data.</span></span> <span data-ttu-id="1865c-223">Набор данных tooview очищен hello, нажмите кнопку слева выходной порт hello hello [Очистка недостающих данных] [ clean-missing-data] модуль и выберите **визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="1865c-223">If you want tooview hello cleaned dataset, click hello left output port of hello [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="1865c-224">Обратите внимание, что hello **нормализованные потери** столбец больше не используется, и нет отсутствующих значений.</span><span class="sxs-lookup"><span data-stu-id="1865c-224">Notice that hello **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="1865c-225">Теперь, когда данные hello чистой, мы готовы toospecify компонентов, которые мы будем toouse в hello прогнозной модели.</span><span class="sxs-lookup"><span data-stu-id="1865c-225">Now that hello data is clean, we're ready toospecify what features we're going toouse in hello predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="1865c-226">Шаг 3. Определение признаков</span><span class="sxs-lookup"><span data-stu-id="1865c-226">Step 3: Define features</span></span>

<span data-ttu-id="1865c-227">В машинном обучении *признаки* — это отдельные измеримые свойства интересующих объектов.</span><span class="sxs-lookup"><span data-stu-id="1865c-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="1865c-228">В нашем наборе данных каждая строка представляет собой один автомобиль, а каждый столбец — его признак.</span><span class="sxs-lookup"><span data-stu-id="1865c-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="1865c-229">Поиск хороший набор средств для создания прогнозной модели требуется экспериментов и знаний о проблеме hello требуется toosolve.</span><span class="sxs-lookup"><span data-stu-id="1865c-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about hello problem you want toosolve.</span></span> <span data-ttu-id="1865c-230">Некоторые функции лучше подходят для прогнозирования целевого hello, чем другие.</span><span class="sxs-lookup"><span data-stu-id="1865c-230">Some features are better for predicting hello target than others.</span></span> <span data-ttu-id="1865c-231">Кроме того, некоторые свойства совпадают с другими, и часть из них можно удалить.</span><span class="sxs-lookup"><span data-stu-id="1865c-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="1865c-232">Например, Город mpg и магистраль mpg тесно связаны, мы можно хранить один и удалять других hello не сильно влияют hello прогноза.</span><span class="sxs-lookup"><span data-stu-id="1865c-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove hello other without significantly affecting hello prediction.</span></span>

<span data-ttu-id="1865c-233">Нужно построить модель, которая использует подмножество функций hello в наш набор данных.</span><span class="sxs-lookup"><span data-stu-id="1865c-233">Let's build a model that uses a subset of hello features in our dataset.</span></span> <span data-ttu-id="1865c-234">Можно продолжить позже и выбрать различные функции, снова запустите эксперимент hello и проверить, доступны ли более точные результаты.</span><span class="sxs-lookup"><span data-stu-id="1865c-234">You can come back later and select different features, run hello experiment again, and see if you get better results.</span></span> <span data-ttu-id="1865c-235">Но toostart, давайте попробуем hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="1865c-235">But toostart, let's try hello following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="1865c-236">Перетащите еще одно [Выбор столбцов в наборе данных] [ select-columns] toohello модуль поэкспериментировать холста.</span><span class="sxs-lookup"><span data-stu-id="1865c-236">Drag another [Select Columns in Dataset][select-columns] module toohello experiment canvas.</span></span> <span data-ttu-id="1865c-237">Подключение hello слева выходной порт hello [Очистка недостающих данных] [ clean-missing-data] toohello модуля ввода hello [Выбор столбцов в наборе данных] [ select-columns] модуля.</span><span class="sxs-lookup"><span data-stu-id="1865c-237">Connect hello left output port of hello [Clean Missing Data][clean-missing-data] module toohello input of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="1865c-238">![Подключение модуль «Очистка недостающих данных» toohello модуля «Выберите столбцы в наборе данных» hello][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-238">![Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="1865c-239">***Подключение модуль «Очистка недостающих данных» toohello модуля «Выберите столбцы в наборе данных» hello***</span><span class="sxs-lookup"><span data-stu-id="1865c-239">***Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="1865c-240">Дважды щелкните модуль hello и введите «Выберите компоненты для прогнозирования».</span><span class="sxs-lookup"><span data-stu-id="1865c-240">Double-click hello module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="1865c-241">Нажмите кнопку **запуска средства выбора столбцов** в hello **свойства** области.</span><span class="sxs-lookup"><span data-stu-id="1865c-241">Click **Launch column selector** in hello **Properties** pane.</span></span>

3. <span data-ttu-id="1865c-242">Щелкните **With rules**(С правилами).</span><span class="sxs-lookup"><span data-stu-id="1865c-242">Click **With rules**.</span></span>

4. <span data-ttu-id="1865c-243">В разделе **Begin With** (Начальное состояние) нажмите кнопку **No columns** (Нет столбцов).</span><span class="sxs-lookup"><span data-stu-id="1865c-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="1865c-244">В строке приветствия фильтра выберите **Include** и **имена столбцов** и выберите наш список имен столбцов в текстовом поле hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-244">In hello filter row, select **Include** and **column names** and select our list of column names in hello text box.</span></span> <span data-ttu-id="1865c-245">В данном случае hello модуля toonot пропускать любые столбцы (функции), за исключением того, мы указываем hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-245">This directs hello module toonot pass through any columns (features) except hello ones that we specify.</span></span>

5. <span data-ttu-id="1865c-246">Нажмите кнопку hello флажок (ОК).</span><span class="sxs-lookup"><span data-stu-id="1865c-246">Click hello check mark (OK) button.</span></span>

    <span data-ttu-id="1865c-247">![Выберите столбцы (компоненты) tooinclude hello в прогнозе hello][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-247">![Select hello columns (features) tooinclude in hello prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="1865c-248">***Выберите столбцы (компоненты) tooinclude hello в прогнозе hello***</span><span class="sxs-lookup"><span data-stu-id="1865c-248">***Select hello columns (features) tooinclude in hello prediction***</span></span>

<span data-ttu-id="1865c-249">В результате получается отфильтрованный набор данных, содержащий только компонент hello, мы хотим toohello toopass алгоритма, который будет использоваться в следующем шаге hello обучения.</span><span class="sxs-lookup"><span data-stu-id="1865c-249">This produces a filtered dataset containing only hello features we want toopass toohello learning algorithm we'll use in hello next step.</span></span> <span data-ttu-id="1865c-250">Позже вы сможете вернуться назад и заново попробовать выбрать другой набор признаков.</span><span class="sxs-lookup"><span data-stu-id="1865c-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="1865c-251">Шаг 4. Выбор и применение алгоритма обучения</span><span class="sxs-lookup"><span data-stu-id="1865c-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="1865c-252">Теперь все готово, hello данных, создав прогнозной модели состоит из обучения и проверки.</span><span class="sxs-lookup"><span data-stu-id="1865c-252">Now that hello data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="1865c-253">Мы будем использовать tootrain hello модели данных, а затем мы протестируем toosee модели hello насколько это может toopredict цены.</span><span class="sxs-lookup"><span data-stu-id="1865c-253">We'll use our data tootrain hello model, and then we'll test hello model toosee how closely it's able toopredict prices.</span></span>
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

<span data-ttu-id="1865c-254">Есть два типа алгоритмов контролируемого машинного обучения — *классификация* и *регрессия*.</span><span class="sxs-lookup"><span data-stu-id="1865c-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="1865c-255">Классификация используется, чтобы сформировать прогноз по заданному набору категорий, таких как цвет (красный, синий, или зеленый).</span><span class="sxs-lookup"><span data-stu-id="1865c-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="1865c-256">Регрессия является toopredict используется число.</span><span class="sxs-lookup"><span data-stu-id="1865c-256">Regression is used toopredict a number.</span></span>

<span data-ttu-id="1865c-257">Поскольку мы хотим toopredict цена, которая является числом, мы будем использовать алгоритм регрессии.</span><span class="sxs-lookup"><span data-stu-id="1865c-257">Because we want toopredict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="1865c-258">В нашем примере достаточно простой модели *линейной регрессии*.</span><span class="sxs-lookup"><span data-stu-id="1865c-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="1865c-259">Дополнительные сведения о различных алгоритмов машинного обучения toolearn и при toouse их, может просмотреть видео первый hello в hello обработки и анализа данных для ряда начинающих [hello пяти вопросы, ответы обработки и анализа данных](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="1865c-259">If you want toolearn more about different types of machine learning algorithms and when toouse them, you might view hello first video in hello Data Science for Beginners series, [hello five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="1865c-260">Также Обратите внимание на hello инфографикой [машинного обучения основы с примерами алгоритм](machine-learning-basics-infographic-with-algorithm-examples.md), или извлечь hello [машинного обучения алгоритм памятку](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="1865c-260">You might also look at hello infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out hello [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="1865c-261">Мы обучения модели hello, указав его набор данных, содержащих цены hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-261">We train hello model by giving it a set of data that includes hello price.</span></span> <span data-ttu-id="1865c-262">модель Hello сканирует данных hello и поиск корреляции между его цены и автомобиль.</span><span class="sxs-lookup"><span data-stu-id="1865c-262">hello model scans hello data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="1865c-263">Затем мы протестируем hello модели — мы предоставляют набор средств для автомобили, которую мы уже знакомы с и разделе, как близко модель hello поставляется toopredicting hello известных цены.</span><span class="sxs-lookup"><span data-stu-id="1865c-263">Then we'll test hello model - we'll give it a set of features for automobiles we're familiar with and see how close hello model comes toopredicting hello known price.</span></span>

<span data-ttu-id="1865c-264">Мы будем использовать наши данные для обучения модели hello и ее проверки путем разделения hello данных на отдельные обучающий и проверочный наборы данных.</span><span class="sxs-lookup"><span data-stu-id="1865c-264">We'll use our data for both training hello model and testing it by splitting hello data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="1865c-265">Выберите и перетащите hello [разбиение данных] [ split] toohello модуль поэкспериментировать холст и подключите его toohello последнего [Выбор столбцов в наборе данных] [ select-columns] модуль.</span><span class="sxs-lookup"><span data-stu-id="1865c-265">Select and drag hello [Split Data][split] module toohello experiment canvas and connect it toohello last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="1865c-266">Нажмите кнопку hello [разбиение данных] [ split] tooselect модуля его.</span><span class="sxs-lookup"><span data-stu-id="1865c-266">Click hello [Split Data][split] module tooselect it.</span></span> <span data-ttu-id="1865c-267">Найти hello **часть строк в hello сначала выходной набор данных** (в hello **свойства** toohello панели справа от холста hello) и задать для него too0.75.</span><span class="sxs-lookup"><span data-stu-id="1865c-267">Find hello **Fraction of rows in hello first output dataset** (in hello **Properties** pane toohello right of hello canvas) and set it too0.75.</span></span> <span data-ttu-id="1865c-268">В этом случае используется 75 процентов tootrain hello hello данных модели и скрывайте 25% для проверки (более поздней версии, можно поэкспериментировать с помощью различные процентные значения).</span><span class="sxs-lookup"><span data-stu-id="1865c-268">This way, we'll use 75 percent of hello data tootrain hello model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="1865c-269">![Набор hello разделить долю too0.75 модуль «Разбиение данных» hello][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-269">![Set hello split fraction of hello "Split Data" module too0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="1865c-270">***Набор hello разделить долю too0.75 модуль «Разбиение данных» hello***</span><span class="sxs-lookup"><span data-stu-id="1865c-270">***Set hello split fraction of hello "Split Data" module too0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="1865c-271">Изменив hello **случайное начальное значение** параметр, вы можете создавать различные случайных выборок для обучения и проверки.</span><span class="sxs-lookup"><span data-stu-id="1865c-271">By changing hello **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="1865c-272">Этот параметр управляет hello заполнения hello генератора псевдослучайных чисел.</span><span class="sxs-lookup"><span data-stu-id="1865c-272">This parameter controls hello seeding of hello pseudo-random number generator.</span></span>

2. <span data-ttu-id="1865c-273">Запустите эксперимент hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-273">Run hello experiment.</span></span> <span data-ttu-id="1865c-274">При запуске эксперимента hello hello [Выбор столбцов в наборе данных] [ select-columns] и [разбиение данных] [ split] модули передать toohello определения столбца модули, которые мы будем добавлять рядом.</span><span class="sxs-lookup"><span data-stu-id="1865c-274">When hello experiment is run, hello [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions toohello modules we'll be adding next.</span></span>  

3. <span data-ttu-id="1865c-275">hello tooselect обучения алгоритм, разверните hello **машинного обучения** категории в toohello палитры модуля hello слева от hello холст, а затем разверните **модель инициализации**.</span><span class="sxs-lookup"><span data-stu-id="1865c-275">tooselect hello learning algorithm, expand hello **Machine Learning** category in hello module palette toohello left of hello canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="1865c-276">При этом отображаются несколько категорий модули, которые могут быть алгоритмов используется tooinitialize машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="1865c-276">This displays several categories of modules that can be used tooinitialize machine learning algorithms.</span></span> <span data-ttu-id="1865c-277">В этом эксперименте выберите hello [линейной регрессии] [ linear-regression] модуля hello **регрессии** категории и перетащите его toohello холст эксперимента.</span><span class="sxs-lookup"><span data-stu-id="1865c-277">For this experiment, select hello [Linear Regression][linear-regression] module under hello **Regression** category, and drag it toohello experiment canvas.</span></span>
<span data-ttu-id="1865c-278">(Можно также найти модуль hello, введя «Линейная регрессия» в поле поиска палитры hello.)</span><span class="sxs-lookup"><span data-stu-id="1865c-278">(You can also find hello module by typing "linear regression" in hello palette Search box.)</span></span>

4. <span data-ttu-id="1865c-279">Поиск и перетащите hello [Обучение модели] [ train-model] toohello модуль поэкспериментировать холста.</span><span class="sxs-lookup"><span data-stu-id="1865c-279">Find and drag hello [Train Model][train-model] module toohello experiment canvas.</span></span> <span data-ttu-id="1865c-280">Подсоедините hello выход hello [линейной регрессии] [ linear-regression] toohello модуль слева ввода hello [Обучение модели] [ train-model] модуля и подключите hello обучающие данные выходные данные (порт слева) hello [разбиение данных] [ split] модуль toohello правый вход hello [Обучение модели] [ train-model] модуль.</span><span class="sxs-lookup"><span data-stu-id="1865c-280">Connect hello output of hello [Linear Regression][linear-regression] module toohello left input of hello [Train Model][train-model] module, and connect hello training data output (left port) of hello [Split Data][split] module toohello right input of hello [Train Model][train-model] module.</span></span>

    <span data-ttu-id="1865c-281">![Подключение hello «Обучение модели» модуль tooboth hello «Линейная регрессия» и «Разбиение данных» модулей][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-281">![Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="1865c-282">***Подключение hello «Обучение модели» модуль tooboth hello «Линейная регрессия» и «Разбиение данных» модулей***</span><span class="sxs-lookup"><span data-stu-id="1865c-282">***Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="1865c-283">Нажмите кнопку hello [Обучение модели] [ train-model] модуль, щелкните **запуска средства выбора столбцов** в hello **свойства** области, а затем выберите hello **цена** столбца.</span><span class="sxs-lookup"><span data-stu-id="1865c-283">Click hello [Train Model][train-model] module, click **Launch column selector** in hello **Properties** pane, and then select hello **price** column.</span></span> <span data-ttu-id="1865c-284">Это значение hello, что нашей модели является постоянной toopredict.</span><span class="sxs-lookup"><span data-stu-id="1865c-284">This is hello value that our model is going toopredict.</span></span>

    <span data-ttu-id="1865c-285">Выберите hello **цены** столбца в селекторе столбца hello, перемещая его из hello **доступные столбцы** списке toohello **выбранные столбцы** списка.</span><span class="sxs-lookup"><span data-stu-id="1865c-285">You select hello **price** column in hello column selector by moving it from hello **Available columns** list toohello **Selected columns** list.</span></span>

    <span data-ttu-id="1865c-286">![Выберите столбец hello цены для hello модуль «Обучение модели»][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-286">![Select hello price column for hello "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="1865c-287">***Выберите столбец hello цены для hello модуль «Обучение модели»***</span><span class="sxs-lookup"><span data-stu-id="1865c-287">***Select hello price column for hello "Train Model" module***</span></span>

6. <span data-ttu-id="1865c-288">Запустите эксперимент hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-288">Run hello experiment.</span></span>

<span data-ttu-id="1865c-289">Теперь у нас есть обученной регрессионной модели, которая может быть tooscore используется новый автомобиль данных toomake цены прогнозов.</span><span class="sxs-lookup"><span data-stu-id="1865c-289">We now have a trained regression model that can be used tooscore new automobile data toomake price predictions.</span></span>

<span data-ttu-id="1865c-290">![После выполнения команды, hello эксперимента теперь должен выглядеть примерно следующим образом][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="1865c-290">![After running, hello experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="1865c-291">
***После выполнения команды, hello эксперимента теперь должен выглядеть примерно следующим образом***</span><span class="sxs-lookup"><span data-stu-id="1865c-291">
***After running, hello experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="1865c-292">Шаг 5. Прогнозирование цен на новые автомобили</span><span class="sxs-lookup"><span data-stu-id="1865c-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="1865c-293">Теперь, когда обучения модели hello, с помощью 75 процентов данных мы используем его tooscore hello других 25 процентов toosee данных hello насколько нашей функции модели.</span><span class="sxs-lookup"><span data-stu-id="1865c-293">Now that we've trained hello model using 75 percent of our data, we can use it tooscore hello other 25 percent of hello data toosee how well our model functions.</span></span>

1. <span data-ttu-id="1865c-294">Поиск и перетащите hello [модель оценки] [ score-model] toohello модуль поэкспериментировать холста.</span><span class="sxs-lookup"><span data-stu-id="1865c-294">Find and drag hello [Score Model][score-model] module toohello experiment canvas.</span></span> <span data-ttu-id="1865c-295">Подсоедините hello выход hello [Обучение модели] [ train-model] toohello модуль левому входному порту [модель оценки][score-model].</span><span class="sxs-lookup"><span data-stu-id="1865c-295">Connect hello output of hello [Train Model][train-model] module toohello left input port of [Score Model][score-model].</span></span> <span data-ttu-id="1865c-296">Подсоедините hello теста данных выход (правом порт) hello [разбиение данных] [ split] toohello модуль справа входному порту [модель оценки][score-model].</span><span class="sxs-lookup"><span data-stu-id="1865c-296">Connect hello test data output (right port) of hello [Split Data][split] module toohello right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="1865c-297">![Подключение hello «Оценка модели» модуль tooboth hello «Обучение модели» и «Разбиение данных» модули][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-297">![Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="1865c-298">***Подключение hello «Оценка модели» модуль tooboth hello «Обучение модели» и «Разбиение данных» модули***</span><span class="sxs-lookup"><span data-stu-id="1865c-298">***Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="1865c-299">Запустите эксперимент hello и просмотреть вывод hello hello [модель оценки] [ score-model] модуля (щелкните порт вывода hello [модель оценки] [ score-model] и выберите пункт **Визуализировать**).</span><span class="sxs-lookup"><span data-stu-id="1865c-299">Run hello experiment and view hello output from hello [Score Model][score-model] module (click hello output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="1865c-300">Вывод отображает Hello hello прогнозируемые значения по цене и hello известных значений из hello тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="1865c-300">hello output shows hello predicted values for price and hello known values from hello test data.</span></span>  

    <span data-ttu-id="1865c-301">![Выходные данные модуля hello «Оценка модели»][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="1865c-301">![Output of hello "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="1865c-302">***Выходные данные модуля hello «Оценка модели»***</span><span class="sxs-lookup"><span data-stu-id="1865c-302">***Output of hello "Score Model" module***</span></span>

3. <span data-ttu-id="1865c-303">Наконец мы тестируем hello качество результатов hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-303">Finally, we test hello quality of hello results.</span></span> <span data-ttu-id="1865c-304">Выберите и перетащите hello [модель оценки] [ evaluate-model] toohello модуль поэкспериментировать холст и подключите выходные данные hello hello [модель оценки] [ score-model] модуль toohello слева ввода [модель оценки][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="1865c-304">Select and drag hello [Evaluate Model][evaluate-model] module toohello experiment canvas, and connect hello output of hello [Score Model][score-model] module toohello left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="1865c-305">Существует два входных портов на hello [модель оценки] [ evaluate-model] модуль, так как он может быть две модели используется toocompare параллельно.</span><span class="sxs-lookup"><span data-stu-id="1865c-305">There are two input ports on hello [Evaluate Model][evaluate-model] module because it can be used toocompare two models side by side.</span></span> <span data-ttu-id="1865c-306">Позже, можно добавить другой алгоритм toohello эксперимента и использовать [модель оценки] [ evaluate-model] toosee, какой из них обеспечивает лучшие результаты.</span><span class="sxs-lookup"><span data-stu-id="1865c-306">Later, you can add another algorithm toohello experiment and use [Evaluate Model][evaluate-model] toosee which one gives better results.</span></span>

4. <span data-ttu-id="1865c-307">Запустите эксперимент hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-307">Run hello experiment.</span></span>

<span data-ttu-id="1865c-308">Вывод hello hello tooview [модель оценки] [ evaluate-model] модуль, щелкните выходной порт hello, а затем выберите **визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="1865c-308">tooview hello output from hello [Evaluate Model][evaluate-model] module, click hello output port, and then select **Visualize**.</span></span>

<span data-ttu-id="1865c-309">![Результаты оценки в эксперименте hello][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="1865c-309">![Evaluation results for hello experiment][evaluation-results]
</span></span><br/><span data-ttu-id="1865c-310">
***Результаты оценки в эксперименте hello***</span><span class="sxs-lookup"><span data-stu-id="1865c-310">
***Evaluation results for hello experiment***</span></span>

<span data-ttu-id="1865c-311">для нашей модели показаны Hello следующая статистика:</span><span class="sxs-lookup"><span data-stu-id="1865c-311">hello following statistics are shown for our model:</span></span>

- <span data-ttu-id="1865c-312">**Средняя абсолютная погрешность** (MAE): hello среднее абсолютное ошибок ( *ошибка* hello разницы между hello прогнозировать hello фактическое значение и значение).</span><span class="sxs-lookup"><span data-stu-id="1865c-312">**Mean Absolute Error** (MAE): hello average of absolute errors (an *error* is hello difference between hello predicted value and hello actual value).</span></span>
- <span data-ttu-id="1865c-313">**Погрешность означает корневой** (RMSE): hello квадратный корень из среднего hello квадрат ошибок прогноза, выполненных в проверочном наборе данных hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-313">**Root Mean Squared Error** (RMSE): hello square root of hello average of squared errors of predictions made on hello test dataset.</span></span>
- <span data-ttu-id="1865c-314">**Относительная абсолютная погрешность**: hello среднее абсолютный ошибки относительный toohello абсолютное отклонение фактические значения hello среднее всех фактических значений.</span><span class="sxs-lookup"><span data-stu-id="1865c-314">**Relative Absolute Error**: hello average of absolute errors relative toohello absolute difference between actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="1865c-315">**Относительная квадратичная погрешность**: hello среднее toohello относительный квадрат ошибки квадрат различие между фактическими значениями hello и hello среднее всех фактических значений.</span><span class="sxs-lookup"><span data-stu-id="1865c-315">**Relative Squared Error**: hello average of squared errors relative toohello squared difference between hello actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="1865c-316">**Коэффициент детерминации**: hello также называется **R квадрат значение**, это статистический показатель, позволяющее определить, насколько хорошо модель соответствует данным hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-316">**Coefficient of Determination**: Also known as hello **R squared value**, this is a statistical metric indicating how well a model fits hello data.</span></span>

<span data-ttu-id="1865c-317">Для каждой ошибки hello лучше статистики, меньшего размера.</span><span class="sxs-lookup"><span data-stu-id="1865c-317">For each of hello error statistics, smaller is better.</span></span> <span data-ttu-id="1865c-318">Меньшее значение указывает прогнозы hello внимательнее совпадение hello фактические значения.</span><span class="sxs-lookup"><span data-stu-id="1865c-318">A smaller value indicates that hello predictions more closely match hello actual values.</span></span> <span data-ttu-id="1865c-319">Для **коэффициент определения**, hello ближе его значением является tooone (1.0), более точные прогнозы hello hello.</span><span class="sxs-lookup"><span data-stu-id="1865c-319">For **Coefficient of Determination**, hello closer its value is tooone (1.0), hello better hello predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="1865c-320">Итоговый вид эксперимента</span><span class="sxs-lookup"><span data-stu-id="1865c-320">Final experiment</span></span>

<span data-ttu-id="1865c-321">Окончательный эксперимента Hello должен выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1865c-321">hello final experiment should look something like this:</span></span>

<span data-ttu-id="1865c-322">![Окончательный эксперимента Hello][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="1865c-322">![hello final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="1865c-323">
***Окончательный эксперимента Hello***</span><span class="sxs-lookup"><span data-stu-id="1865c-323">
***hello final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="1865c-324">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1865c-324">Next steps</span></span>

<span data-ttu-id="1865c-325">Теперь, после завершения hello первой машине обучения учебника и вы можете настроить эксперимента, можно продолжить tooimprove hello модели и затем развернуть его как прогнозирующей веб-службы.</span><span class="sxs-lookup"><span data-stu-id="1865c-325">Now that you've completed hello first machine learning tutorial and have your experiment set up, you can continue tooimprove hello model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="1865c-326">**Перечисления tootry tooimprove hello модели** -например, можно изменить функции hello, использовать в вашей прогноза.</span><span class="sxs-lookup"><span data-stu-id="1865c-326">**Iterate tootry tooimprove hello model** - For example, you can change hello features you use in your prediction.</span></span> <span data-ttu-id="1865c-327">Или можно изменить свойства hello hello [линейной регрессии] [ linear-regression] алгоритм или используйте другой алгоритм полностью.</span><span class="sxs-lookup"><span data-stu-id="1865c-327">Or you can modify hello properties of hello [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="1865c-328">Можно даже добавить несколько эксперимента машинного обучения алгоритмы tooyour за один раз и сравнить две из них с помощью hello [модель оценки] [ evaluate-model] модуля.</span><span class="sxs-lookup"><span data-stu-id="1865c-328">You can even add multiple machine learning algorithms tooyour experiment at one time and compare two of them by using hello [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="1865c-329">Пример toocompare несколько моделей в одном эксперимент, в статье [сравнение моделей](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) в hello [коллекции аналитики Cortana](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="1865c-329">For an example of how toocompare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="1865c-330">toocopy какая-либо итерация эксперименте используйте hello **SAVE AS** кнопку внизу hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="1865c-330">toocopy any iteration of your experiment, use hello **SAVE AS** button at hello bottom of hello page.</span></span> <span data-ttu-id="1865c-331">Все итерации hello эксперимента можно просмотреть, щелкнув **ПРОСМОТРЕТЬ ЖУРНАЛ ВЫПОЛНЕНИЯ** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="1865c-331">You can see all hello iterations of your experiment by clicking **VIEW RUN HISTORY** at hello bottom of hello page.</span></span> <span data-ttu-id="1865c-332">Дополнительные сведения см. в статье [Управление итерациями экспериментов в Студии машинного обучения Azure][runhistory].</span><span class="sxs-lookup"><span data-stu-id="1865c-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="1865c-333">**Развертывание модели hello как прогнозирующей веб-службы** — Если вы удовлетворены модели, ее можно развернуть как toobe web service используется toopredict ценам автомобилей, используя новые данные.</span><span class="sxs-lookup"><span data-stu-id="1865c-333">**Deploy hello model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service toobe used toopredict automobile prices by using new data.</span></span> <span data-ttu-id="1865c-334">Дополнительные сведения см. в статье [Развертывание веб-службы машинного обучения Azure][publish].</span><span class="sxs-lookup"><span data-stu-id="1865c-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="1865c-335">Требуется более toolearn?</span><span class="sxs-lookup"><span data-stu-id="1865c-335">Want toolearn more?</span></span> <span data-ttu-id="1865c-336">Более широкие и Подробное пошаговое руководство, hello процесса создания, обучения, оценки и развертывания модели, в разделе [разработка прогнозирующего решения с помощью машинного обучения Azure][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="1865c-336">For a more extensive and detailed walkthrough of hello process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
