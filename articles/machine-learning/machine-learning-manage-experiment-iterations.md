---
title: "Управление итерациями экспериментов в Студии машинного обучения | Документация Майкрософт"
description: "Как управлять итерациями экспериментов в Студии машинного обучения Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 0e32a02358d1901bb80f356b0289b02b8e98afdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a><span data-ttu-id="99940-103">Управление итерациями экспериментов в Студии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="99940-103">Manage experiment iterations in Azure Machine Learning Studio</span></span>
<span data-ttu-id="99940-104">Разработка модели прогнозной аналитики идет по итерациям — по мере изменения разных функций и параметров экспериментов выполняется сведение результатов, пока не будет получена обученная эффективная модель.</span><span class="sxs-lookup"><span data-stu-id="99940-104">Developing a predictive analysis model is an iterative process - as you modify the various functions and parameters of your experiment, your results converge until you are satisfied that you have a trained, effective model.</span></span> <span data-ttu-id="99940-105">Ключ к этому процессу — отслеживание различных итераций параметров и конфигураций эксперимента.</span><span class="sxs-lookup"><span data-stu-id="99940-105">Key to this process is tracking the various iterations of your experiment parameters and configurations.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="99940-106">В любой момент вы можете просмотреть данные предыдущих выполнений эксперимента, чтобы поставить под вопрос, пересмотреть и, в конечном счете, подтвердить или уточнить предыдущие предположения.</span><span class="sxs-lookup"><span data-stu-id="99940-106">You can review previous runs of your experiments at any time in order to challenge, revisit, and ultimately either confirm or refine previous assumptions.</span></span> <span data-ttu-id="99940-107">При запуске эксперимента Студия машинного обучения ведет журнал выполнения, включая наборы данных, модули, подключения к портам и параметры.</span><span class="sxs-lookup"><span data-stu-id="99940-107">When you run an experiment, Machine Learning Studio keeps a history of the run, including dataset, module, and port connections and parameters.</span></span> <span data-ttu-id="99940-108">В этот журнал также записываются результаты выполнения, данные среды выполнения, в том числе время начала и остановки, сообщения журнала и состояние выполнения.</span><span class="sxs-lookup"><span data-stu-id="99940-108">This history also captures results, runtime information such as start and stop times, log messages, and execution status.</span></span> <span data-ttu-id="99940-109">Вы можете в любое время взглянуть на эти данные, чтобы просмотреть хронологию эксперимента и промежуточные результаты.</span><span class="sxs-lookup"><span data-stu-id="99940-109">You can look back at any of these runs at any time to review the chronology of your experiment and intermediate results.</span></span> <span data-ttu-id="99940-110">Можно даже использовать предыдущий запуск эксперимента, чтобы запустить новый этап исследования и обнаружения на пути к созданию простых, сложных или даже групповых решений моделирования.</span><span class="sxs-lookup"><span data-stu-id="99940-110">You can even use a previous run of your experiment to launch into a new phase of inquiry and discovery on your path to creating simple, complex, or even ensemble modeling solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="99940-111">При просмотре данных предыдущего выполнения эксперимента версия данного эксперимента блокируется и не может быть изменена.</span><span class="sxs-lookup"><span data-stu-id="99940-111">When you view a previous run of an experiment, that version of the experiment is locked and can't be edited.</span></span> <span data-ttu-id="99940-112">Тем не менее, можно сохранить копию, щелкнув **СОХРАНИТ КАК** и указав новое имя для копии.</span><span class="sxs-lookup"><span data-stu-id="99940-112">You can, however, save a copy of it by clicking **SAVE AS** and providing a new name for the copy.</span></span> <span data-ttu-id="99940-113">Новая копия откроется в Студии машинного обучения, и ее можно будет изменять и запускать.</span><span class="sxs-lookup"><span data-stu-id="99940-113">Machine Learning Studio opens the new copy, which you can then edit and run.</span></span> <span data-ttu-id="99940-114">Эта копия вашего эксперимента доступна в списке **ЭКСПЕРИМЕНТЫ** , как и все другие ваши эксперименты.</span><span class="sxs-lookup"><span data-stu-id="99940-114">This copy of your experiment is available in the **EXPERIMENTS** list along with all your other experiments.</span></span>
> 
> 

## <a name="viewing-the-prior-run"></a><span data-ttu-id="99940-115">Просмотр предыдущего выполнения</span><span class="sxs-lookup"><span data-stu-id="99940-115">Viewing the Prior Run</span></span>
<span data-ttu-id="99940-116">Если у вас есть открытый эксперимент, который был выполнен хотя бы один раз, вы можете просмотреть данные предыдущего выполнения, щелкнув **Предыдущее выполнение** на панели свойств.</span><span class="sxs-lookup"><span data-stu-id="99940-116">When you have an experiment open that you have run at least once, you can view the preceding run of the experiment by clicking **Prior Run** in the properties pane.</span></span>

<span data-ttu-id="99940-117">Для примера предположим, что вы создали эксперимент и выполнили его версии в 11:23, 11:42 и 11:55.</span><span class="sxs-lookup"><span data-stu-id="99940-117">For example, suppose you create an experiment and run versions of it at 11:23, 11:42, and 11:55.</span></span> <span data-ttu-id="99940-118">Если вы откроете данные последнего выполнения эксперимента (11:55) и щелкнете **Предыдущее выполнение**, откроется версия, выполненная в 11:42.</span><span class="sxs-lookup"><span data-stu-id="99940-118">If you open the last run of the experiment (11:55) and click **Prior Run**, the version you ran at 11:42 is opened.</span></span>

## <a name="viewing-the-run-history"></a><span data-ttu-id="99940-119">Просмотр журнала выполнения</span><span class="sxs-lookup"><span data-stu-id="99940-119">Viewing the Run History</span></span>
<span data-ttu-id="99940-120">Вы можете просмотреть данные всех предыдущих выполнений эксперимента, щелкнув **Просмотреть журнал выполнения** в открытом эксперименте.</span><span class="sxs-lookup"><span data-stu-id="99940-120">You can view all the previous runs of an experiment by clicking **View Run History** in an open experiment.</span></span>

<span data-ttu-id="99940-121">Для примера предположим, что вы создаете эксперимент с использованием модуля [Линейная регрессия][linear-regression] и хотите просмотреть, как изменение значения **Скорость обучения** влияет на результаты эксперимента.</span><span class="sxs-lookup"><span data-stu-id="99940-121">For example, suppose you create an experiment with the [Linear Regression][linear-regression] module and you want to observe the effect of changing the value of **Learning rate** on your experiment results.</span></span> <span data-ttu-id="99940-122">Вы выполняете эксперимент несколько раз с разными значениями этого параметра, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="99940-122">You run the experiment multiple times with different values for this parameter, as follows:</span></span>

| <span data-ttu-id="99940-123">Значение скорости обучения</span><span class="sxs-lookup"><span data-stu-id="99940-123">Learning Rate value</span></span> | <span data-ttu-id="99940-124">Время начала выполнения</span><span class="sxs-lookup"><span data-stu-id="99940-124">Run start time</span></span> |
| --- | --- |
| <span data-ttu-id="99940-125">0,1</span><span class="sxs-lookup"><span data-stu-id="99940-125">0.1</span></span> |<span data-ttu-id="99940-126">11.9.2014, 16:18:58</span><span class="sxs-lookup"><span data-stu-id="99940-126">9/11/2014 4:18:58 pm</span></span> |
| <span data-ttu-id="99940-127">0,2</span><span class="sxs-lookup"><span data-stu-id="99940-127">0.2</span></span> |<span data-ttu-id="99940-128">11.9.2014, 16:24:33</span><span class="sxs-lookup"><span data-stu-id="99940-128">9/11/2014 4:24:33 pm</span></span> |
| <span data-ttu-id="99940-129">0,4</span><span class="sxs-lookup"><span data-stu-id="99940-129">0.4</span></span> |<span data-ttu-id="99940-130">11.9.2014, 16:28:36</span><span class="sxs-lookup"><span data-stu-id="99940-130">9/11/2014 4:28:36 pm</span></span> |
| <span data-ttu-id="99940-131">0,5</span><span class="sxs-lookup"><span data-stu-id="99940-131">0.5</span></span> |<span data-ttu-id="99940-132">11.9.2014, 16:33:31</span><span class="sxs-lookup"><span data-stu-id="99940-132">9/11/2014 4:33:31 pm</span></span> |

<span data-ttu-id="99940-133">Если щелкнуть **ПРОСМОТРЕТЬ ЖУРНАЛ ВЫПОЛНЕНИЯ**, вы увидите список всех выполнений:</span><span class="sxs-lookup"><span data-stu-id="99940-133">If you click **VIEW RUN HISTORY**, you see a list of all these runs:</span></span>

![Пример журнала выполнения][runhistory]

<span data-ttu-id="99940-135">Щелкните любое из этих выполнений, чтобы просмотреть моментальный снимок эксперимента на момент его выполнения.</span><span class="sxs-lookup"><span data-stu-id="99940-135">Click any of these runs to view a snapshot of the experiment at the time you ran it.</span></span> <span data-ttu-id="99940-136">Сохраняется все — конфигурация, значения параметров, комментарии и результаты, чтобы предоставить вам полную запись выполнения эксперимента.</span><span class="sxs-lookup"><span data-stu-id="99940-136">The configuration, parameter values, comments, and results are all preserved to give you a complete record of that run of your experiment.</span></span>

> [!TIP]
> <span data-ttu-id="99940-137">Чтобы задокументировать итерации эксперимента, можно изменять заголовок при каждом выполнении, можно обновлять **сводку** эксперимента на панели свойств и можно добавлять или обновлять комментарии для отдельных модулей, чтобы записывать вносимые изменения.</span><span class="sxs-lookup"><span data-stu-id="99940-137">To document your iterations of the experiment, you can modify the title each time you run it, you can update the **Summary** of the experiment in the properties pane, and you can add or update comments on individual modules to record your changes.</span></span> <span data-ttu-id="99940-138">Заголовок, сводка и комментарии для модуля сохраняются при каждом выполнении эксперимента.</span><span class="sxs-lookup"><span data-stu-id="99940-138">The title, summary, and module comments are saved with each run of the experiment.</span></span>
> 
> 

<span data-ttu-id="99940-139">В списке экспериментов на вкладке **ЭКСПЕРИМЕНТЫ** в Студии машинного обучения всегда отображается последняя версия эксперимента.</span><span class="sxs-lookup"><span data-stu-id="99940-139">The list of experiments in the **EXPERIMENTS** tab in Machine Learning Studio always displays the latest version of an experiment.</span></span> <span data-ttu-id="99940-140">Если открыть данные предыдущего выполнения эксперимента (используя **Prior Run** (Предыдущее выполнение) или **View run history** (Просмотреть журнал выполнения)), вы сможете вернуться к черновой версии, щелкнув **View run history** (Просмотреть журнал выполнения) и выбрав итерацию, у которой в качестве значения параметра **Состояние** указано **Редактируемый**.</span><span class="sxs-lookup"><span data-stu-id="99940-140">If you open a previous run of the experiment (using **Prior Run** or **VIEW RUN HISTORY**), you can return to the draft version by clicking **VIEW RUN HISTORY** and selecting the iteration that has a **STATE** of **Editable**.</span></span>

## <a name="iterating-on-a-previous-run"></a><span data-ttu-id="99940-141">Перебор итераций предыдущего выполнения</span><span class="sxs-lookup"><span data-stu-id="99940-141">Iterating on a Previous Run</span></span>
<span data-ttu-id="99940-142">Если щелкнуть **Prior Run** (Предыдущее выполнение) или **View run history** (Просмотреть журнал выполнения) и открыть данные предыдущего выполнения, то можно просмотреть завершенный эксперимент в режиме только для чтения.</span><span class="sxs-lookup"><span data-stu-id="99940-142">When you click **Prior Run** or **VIEW RUN HISTORY** and open a previous run, you can view a finished experiment in read-only mode.</span></span>

<span data-ttu-id="99940-143">Если вы хотите начать итерацию своего эксперимента, использовав параметры, настроенные для предыдущего выполнения, это можно сделать, щелкнув **Сохранить как**.</span><span class="sxs-lookup"><span data-stu-id="99940-143">If you want to begin an iteration of your experiment starting with the way you configured it for a previous run, you can do this by opening the run and clicking **SAVE AS**.</span></span> <span data-ttu-id="99940-144">При этом создается новый эксперимент с новым заголовком и пустым журналом выполнения, все компоненты и значения параметров которого взяты из предыдущего выполнения.</span><span class="sxs-lookup"><span data-stu-id="99940-144">This creates a new experiment, with a new title, an empty run history, and all the components and parameter values of the previous run.</span></span> <span data-ttu-id="99940-145">Этот новый эксперимент отображается на вкладке **Эксперименты** на домашней странице Студии машинного обучения. Вы можете изменить и выполнить его, начав новый журнал выполнения для этой итерации своего эксперимента.</span><span class="sxs-lookup"><span data-stu-id="99940-145">This new experiment is listed in the **EXPERIMENTS** tab in the Machine Learning Studio home page, and you can modify and run it, initiating a new run history for this iteration of your experiment.</span></span> 

<span data-ttu-id="99940-146">Для примера предположим, в предыдущем разделе есть журнал выполнения эксперимента.</span><span class="sxs-lookup"><span data-stu-id="99940-146">For example, suppose you have the experiment run history shown in the previous section.</span></span> <span data-ttu-id="99940-147">Вы хотите посмотреть, что происходит, если задать **скорость обучения** 0,4, и опробовать различные значения параметра **Number of training epochs** (Количество эпох обучения).</span><span class="sxs-lookup"><span data-stu-id="99940-147">You want to observe what happens when you set the **Learning rate** parameter to 0.4, and try different values for the **Number of training epochs** parameter.</span></span>

1. <span data-ttu-id="99940-148">Щелкните **ПРОСМОТРЕТЬ ЖУРНАЛ ВЫПОЛНЕНИЯ** и откройте итерацию эксперимента, выполненную в 16:28:36 (в которой вы задали значение параметра равным 0,4).</span><span class="sxs-lookup"><span data-stu-id="99940-148">Click **VIEW RUN HISTORY** and open the iteration of the experiment that you ran at 4:28:36 pm (in which you set the parameter value to 0.4).</span></span>
2. <span data-ttu-id="99940-149">Щелкните **СОХРАНИТЬ КАК**.</span><span class="sxs-lookup"><span data-stu-id="99940-149">Click **SAVE AS**.</span></span>
3. <span data-ttu-id="99940-150">Введите новый заголовок и щелкните флажок **ОК** .</span><span class="sxs-lookup"><span data-stu-id="99940-150">Enter a new title and click the **OK** checkmark.</span></span> <span data-ttu-id="99940-151">Будет создана новая копия эксперимента.</span><span class="sxs-lookup"><span data-stu-id="99940-151">A new copy of the experiment is created.</span></span>
4. <span data-ttu-id="99940-152">Измените значение параметра **Количество эпох обучения** .</span><span class="sxs-lookup"><span data-stu-id="99940-152">Modify the **Number of training epochs** parameter.</span></span>
5. <span data-ttu-id="99940-153">Щелкните **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="99940-153">Click **RUN**.</span></span>

<span data-ttu-id="99940-154">Теперь можно продолжить изменение и выполнение данной версии эксперимента, создавая новый журнал выполнения для записи вашей работы.</span><span class="sxs-lookup"><span data-stu-id="99940-154">You can now continue to modify and run this version of your experiment, building a new run history to record your work.</span></span>

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
