---
title: "Учебник по aaaQuickstart для языка R для машинного обучения | Документы Microsoft"
description: "Используйте этот программирования учебника tooget работы быстро с помощью языка hello R с toocreate студии машинного обучения Azure прогнозирования решения R."
keywords: "краткое руководство, язык r, язык программирования r, руководство по программированию на языке r"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="bb853-104">Учебник по языку программирования hello R для машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="bb853-104">Quickstart tutorial for hello R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="bb853-105">Введение</span><span class="sxs-lookup"><span data-stu-id="bb853-105">Introduction</span></span>
<span data-ttu-id="bb853-106">Этот учебник помогает быстро запустить расширение машинного обучения Azure, используя язык программирования hello R.</span><span class="sxs-lookup"><span data-stu-id="bb853-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using hello R programming language.</span></span> <span data-ttu-id="bb853-107">Выполните этот программирования учебника toocreate R, тестирования и выполнять код R в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-107">Follow this R programming tutorial toocreate, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="bb853-108">При работе с учебником, вы создадите законченное решение прогнозирования с помощью языка hello R в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-108">As you work through tutorial, you will create a complete forecasting solution by using hello R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="bb853-109">Машинное обучение Microsoft Azure содержит множество эффективных модулей машинного обучения и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="bb853-110">мощный язык R Hello был описан как общепринятый язык глобальной hello аналитики.</span><span class="sxs-lookup"><span data-stu-id="bb853-110">hello powerful R language has been described as hello lingua franca of analytics.</span></span> <span data-ttu-id="bb853-111">К счастью аналитики и данных для работы в машинном обучении Azure можно расширить с помощью R. Это сочетание предоставляет гибкость hello и глубокого анализа R. hello масштабируемость и простота использования машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="bb853-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides hello scalability and ease of deployment of Azure Machine Learning with hello flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a><span data-ttu-id="bb853-112">Прогнозирование и hello набора данных</span><span class="sxs-lookup"><span data-stu-id="bb853-112">Forecasting and hello dataset</span></span>
<span data-ttu-id="bb853-113">Прогнозирование — широко распространенный и чрезвычайно полезный метод аналитики.</span><span class="sxs-lookup"><span data-stu-id="bb853-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="bb853-114">Распространенные варианты в диапазоне от создать прогноз продаж сезонных элементов, определения оптимальной единиц на складе, toopredicting macroeconomic переменных.</span><span class="sxs-lookup"><span data-stu-id="bb853-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, toopredicting macroeconomic variables.</span></span> <span data-ttu-id="bb853-115">Преимущественно при прогнозировании используются модели временных рядов.</span><span class="sxs-lookup"><span data-stu-id="bb853-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="bb853-116">Данные временных рядов является данных, в котором значения hello имеют индекс времени.</span><span class="sxs-lookup"><span data-stu-id="bb853-116">Time series data is data in which hello values have a time index.</span></span> <span data-ttu-id="bb853-117">Индекс Hello времени может быть regular, например ежемесячно или каждую минуту или нерегулярным.</span><span class="sxs-lookup"><span data-stu-id="bb853-117">hello time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="bb853-118">Модель временных рядов основана на данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="bb853-118">A time series model is based on time series data.</span></span> <span data-ttu-id="bb853-119">язык программирования Hello R содержит гибкую среду и расширенная аналитика для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-119">hello R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="bb853-120">В этом руководстве мы будем использовать данные о производстве молочных продуктов в Калифорнии и ценах на них.</span><span class="sxs-lookup"><span data-stu-id="bb853-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="bb853-121">Сюда входят ежемесячные данные по hello производства несколько товаров и цене hello milk файловой системы FAT, товарного тест производительности.</span><span class="sxs-lookup"><span data-stu-id="bb853-121">This data includes monthly information on hello production of several dairy products and hello price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="bb853-122">Hello данные, используемые в этой статье, а также сценарии R, могут быть [загрузить здесь][download].</span><span class="sxs-lookup"><span data-stu-id="bb853-122">hello data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="bb853-123">Эти данные были первоначально полученные из информации, доступной из hello университета Wisconsin на http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="bb853-123">This data was originally synthesized from information available from hello University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="bb853-124">План</span><span class="sxs-lookup"><span data-stu-id="bb853-124">Organization</span></span>
<span data-ttu-id="bb853-125">Будет прохождения несколько шагов вы узнаете, как toocreate, тестирование и выполнять код R обработки аналитических и данных в среде машинного обучения Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-125">We will progress through several steps as you learn how toocreate, test and execute analytics and data manipulation R code in hello Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="bb853-126">Сначала мы рассмотрим hello основы использования языка hello R в студии машинного обучения Azure среде hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-126">First we will explore hello basics of using hello R language in hello Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="bb853-127">Затем мы хода выполнения toodiscussing различные аспекты операций ввода-вывода для данных, код R и графики в среде машинного обучения Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-127">Then we progress toodiscussing various aspects of I/O for data, R code and graphics in hello Azure Machine Learning environment.</span></span>
* <span data-ttu-id="bb853-128">Затем мы формируется hello первую часть наших прогнозирования решение путем создания кода для очистки данных и преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-128">We will then construct hello first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="bb853-129">Наши данные подготовки будет выполнять анализ hello корреляции между несколько переменных hello в наш набор данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-129">With our data prepared we will perform an analysis of hello correlations between several of hello variables in our dataset.</span></span>
* <span data-ttu-id="bb853-130">Наконец, мы создадим прогнозную модель сезонного временного ряда для молочного производства.</span><span class="sxs-lookup"><span data-stu-id="bb853-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="bb853-131"><a id="mlstudio"></a>Работа с языком R в Студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="bb853-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="bb853-132">В этом разделе представлены некоторые основные вопросы взаимодействия и язык программирования hello R в студии машинного обучения среде hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-132">This section takes you through some basics of interacting with hello R programming language in hello Machine Learning Studio environment.</span></span> <span data-ttu-id="bb853-133">язык Hello R предоставляет мощное средство toocreate настроить аналитики и данных манипуляции модулей в среде машинного обучения Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-133">hello R language provides a powerful tool toocreate customized analytics and data manipulation modules within hello Azure Machine Learning environment.</span></span>

<span data-ttu-id="bb853-134">Я использую RStudio toodevelop, тестирования и отладки кода R в небольших масштабах.</span><span class="sxs-lookup"><span data-stu-id="bb853-134">I will use RStudio toodevelop, test and debug R code on a small scale.</span></span> <span data-ttu-id="bb853-135">Этот код, который затем вырезать и вставить в [выполнение скрипта R] [ execute-r-script] модуля в студии машинного обучения готов toorun.</span><span class="sxs-lookup"><span data-stu-id="bb853-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready toorun.</span></span>  

### <a name="hello-execute-r-script-module"></a><span data-ttu-id="bb853-136">Выполнение скрипта R модуля Hello</span><span class="sxs-lookup"><span data-stu-id="bb853-136">hello Execute R Script module</span></span>
<span data-ttu-id="bb853-137">В студии машинного обучения, R-скриптов, выполняются в hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-137">Within Machine Learning Studio, R scripts are run within hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="bb853-138">Пример hello [выполнение скрипта R] [ execute-r-script] модуля в студии машинного обучения, приведенный на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="bb853-138">An example of hello [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![Язык программирования R: hello выполнение скрипта R модуля, выбранного в студии машинного обучения][1]

<span data-ttu-id="bb853-140">*Рисунок 1. Среда студии машинного обучения Hello Отображение выбранного модуля выполнение скрипта R hello.*</span><span class="sxs-lookup"><span data-stu-id="bb853-140">*Figure 1. hello Machine Learning Studio environment showing hello Execute R Script module selected.*</span></span>

<span data-ttu-id="bb853-141">Ссылающаяся tooFigure 1, давайте рассмотрим некоторые основные части hello hello студии машинного обучения среду для работы с hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-141">Referring tooFigure 1, let's look at some of hello key parts of hello Machine Learning Studio environment for working with hello [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="bb853-142">модули Hello в эксперименте hello отображаются в центральной области hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-142">hello modules in hello experiment are shown in hello center pane.</span></span>
* <span data-ttu-id="bb853-143">Hello верхнюю часть hello правая панель содержит tooview окна и редактирования сценариев R.</span><span class="sxs-lookup"><span data-stu-id="bb853-143">hello upper part of hello right pane contains a window tooview and edit your R scripts.</span></span>  
* <span data-ttu-id="bb853-144">Hello нижней части правой панели показаны некоторые свойства hello [выполнение скрипта R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="bb853-144">hello lower part of right pane shows some properties of hello [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="bb853-145">Журналы ошибок и вывода hello можно просмотреть, щелкнув соответствующий участков hello в этой области.</span><span class="sxs-lookup"><span data-stu-id="bb853-145">You can view hello error and output logs by clicking on hello appropriate spots of this pane.</span></span>

<span data-ttu-id="bb853-146">Мы будем Конечно, обсуждать hello [выполнение скрипта R] [ execute-r-script] более подробно в hello остальной части этого документа.</span><span class="sxs-lookup"><span data-stu-id="bb853-146">We will, of course, be discussing hello [Execute R Script][execute-r-script] in greater detail in hello rest of this document.</span></span>

<span data-ttu-id="bb853-147">При работе с более сложными функциями R для изменения, тестирования и отладки кода я рекомендую использовать RStudio.</span><span class="sxs-lookup"><span data-stu-id="bb853-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="bb853-148">Как и в случае разработки любого программного обеспечения, создавайте код пошагово, отдельными фрагментами, и тестируйте его на небольших, простых проверочных примерах.</span><span class="sxs-lookup"><span data-stu-id="bb853-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="bb853-149">Вырежьте и вставьте в окно скрипта hello R hello функций [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-149">Then cut and paste your functions into hello R script window of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="bb853-150">Такой подход позволяет tooharness как hello RStudio интегрированной среды разработки (IDE) и hello power машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-150">This approach allows you tooharness both hello RStudio integrated development environment (IDE) and hello power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="bb853-151">Выполнение кода R</span><span class="sxs-lookup"><span data-stu-id="bb853-151">Execute R code</span></span>
<span data-ttu-id="bb853-152">Любой код R в hello [выполнение скрипта R] [ execute-r-script] модуль будет выполняться при запуске эксперимента hello, щелкнув hello **запуска** кнопки.</span><span class="sxs-lookup"><span data-stu-id="bb853-152">Any R code in hello [Execute R Script][execute-r-script] module will execute when you run hello experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="bb853-153">По завершении выполнения флажок будет отображаться на hello [выполнение скрипта R] [ execute-r-script] значок.</span><span class="sxs-lookup"><span data-stu-id="bb853-153">When execution has completed, a check mark will appear on hello [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="bb853-154">Защищенное программирование на R для Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="bb853-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="bb853-155">При разработке кода на R для, скажем, какой-нибудь веб-службы с помощью Машинного обучения Azure необходимо предусмотреть, как ваш код будет реагировать на непредвиденные входные данные и исключения.</span><span class="sxs-lookup"><span data-stu-id="bb853-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="bb853-156">ясности toomaintain не включены в hello способ проверки и обработки исключений в большинство примеров кода hello показано.</span><span class="sxs-lookup"><span data-stu-id="bb853-156">toomaintain clarity, I have not included much in hello way of checking or exception handling in most of hello code examples shown.</span></span> <span data-ttu-id="bb853-157">Однако далее я приведу несколько примеров функций, использующих возможности языка R для обработки исключений.</span><span class="sxs-lookup"><span data-stu-id="bb853-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="bb853-158">Если требуется более полную обработку R обработки исключений, рекомендуется прочитать hello соответствующих разделах hello книги по Wickham, перечисленных в [приложение B — Дополнительные материалы](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="bb853-158">If you need a more complete treatment of R exception handling, I recommend you read hello applicable sections of hello book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="bb853-159">Отладка и тестирование кода R в Студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="bb853-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="bb853-160">tooreiterate, я рекомендую тестирования и отладки кода R в RStudio небольших масштабах.</span><span class="sxs-lookup"><span data-stu-id="bb853-160">tooreiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="bb853-161">Однако бывают случаи, когда будет необходимо tootrack проблем кода R в hello [выполнение скрипта R] [ execute-r-script] сам.</span><span class="sxs-lookup"><span data-stu-id="bb853-161">However, there are cases where you will need tootrack down R code problems in hello [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="bb853-162">Кроме того, он является хорошей практикой toocheck результатов в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="bb853-162">In addition, it is good practice toocheck your results in Machine Learning Studio.</span></span>

<span data-ttu-id="bb853-163">В основном в файл output.log найдены выходные данные hello выполнения кода R и на платформе hello машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-163">Output from hello execution of your R code and on hello Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="bb853-164">Дополнительная информация отображается в файле error.log.</span><span class="sxs-lookup"><span data-stu-id="bb853-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="bb853-165">Если во время выполнения кода R в студии машинного обучения происходит ошибка, первое действие должно быть toolook на error.log.</span><span class="sxs-lookup"><span data-stu-id="bb853-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be toolook at error.log.</span></span> <span data-ttu-id="bb853-166">Этот файл может содержать полезные ошибки сообщения toohelp понять и исправить ошибки.</span><span class="sxs-lookup"><span data-stu-id="bb853-166">This file can contain useful error messages toohelp you understand and correct your error.</span></span> <span data-ttu-id="bb853-167">error.log tooview, если щелкнуть **Просмотр журнала ошибок** на hello **панели «свойства»** для hello [выполнение скрипта R] [ execute-r-script] hello ошибкой.</span><span class="sxs-lookup"><span data-stu-id="bb853-167">tooview error.log, click on **View error log** on hello **properties pane** for hello [Execute R Script][execute-r-script] containing hello error.</span></span>

<span data-ttu-id="bb853-168">Например, нужно ли устанавливать hello, выполнив кода R, а также не определено y переменной, в [выполнение скрипта R] [ execute-r-script] модуля:</span><span class="sxs-lookup"><span data-stu-id="bb853-168">For example, I ran hello following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="bb853-169">Этот код вызывает ошибку tooexecute, возникающие в случае ошибки.</span><span class="sxs-lookup"><span data-stu-id="bb853-169">This code fails tooexecute, resulting in an error condition.</span></span> <span data-ttu-id="bb853-170">Щелкнув **Просмотр журнала ошибок** на hello **панель свойств** создает hello экран, показанный на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="bb853-170">Clicking on **View error log** on hello **properties pane** produces hello display shown in Figure 2.</span></span>

  ![Всплывающее окно сообщения об ошибке][2]

<span data-ttu-id="bb853-172">*Рис. 2. Всплывающее окно сообщения об ошибке*</span><span class="sxs-lookup"><span data-stu-id="bb853-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="bb853-173">Похоже, мы должны toolook в файл output.log toosee hello R сообщение.</span><span class="sxs-lookup"><span data-stu-id="bb853-173">It looks like we need toolook in output.log toosee hello R error message.</span></span> <span data-ttu-id="bb853-174">Щелкните hello [выполнение скрипта R] [ execute-r-script] и выберите команду hello **просматривать файл output.log** элемент hello **панели «свойства»** toohello справа.</span><span class="sxs-lookup"><span data-stu-id="bb853-174">Click on hello [Execute R Script][execute-r-script] and then click on hello **View output.log** item on hello **properties pane** toohello right.</span></span> <span data-ttu-id="bb853-175">Откроется новое окно браузера, и я вижу следующее hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-175">A new browser window opens, and I see hello following.</span></span>

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="bb853-176">Это сообщение об ошибке содержит исключить неожиданные результаты и четко определяет проблему hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-176">This error message contains no surprises and clearly identifies hello problem.</span></span>

<span data-ttu-id="bb853-177">значение hello tooinspect любого объекта в R, можно напечатать файл файл output.log toohello этих значений.</span><span class="sxs-lookup"><span data-stu-id="bb853-177">tooinspect hello value of any object in R, you can print these values toohello output.log file.</span></span> <span data-ttu-id="bb853-178">Hello правил для проверки объектов, значения в основном являются hello же, как и в интерактивном сеансе R.</span><span class="sxs-lookup"><span data-stu-id="bb853-178">hello rules for examining object values are essentially hello same as in an interactive R session.</span></span> <span data-ttu-id="bb853-179">Например при вводе имени переменной в строке значение hello hello объекта будет напечатан toohello файл output.log файла.</span><span class="sxs-lookup"><span data-stu-id="bb853-179">For example, if you type a variable name on a line, hello value of hello object will be printed toohello output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="bb853-180">Пакеты в Студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="bb853-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="bb853-181">Служба машинного обучения Azure содержит более 350 предустановленных пакетов на языке R.</span><span class="sxs-lookup"><span data-stu-id="bb853-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="bb853-182">Можно использовать следующий код в hello hello [выполнение скрипта R] [ execute-r-script] tooretrieve модуль список hello предустановлен пакетов.</span><span class="sxs-lookup"><span data-stu-id="bb853-182">You can use hello following code in hello [Execute R Script][execute-r-script] module tooretrieve a list of hello preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="bb853-183">Если вы не понимаете hello последняя строка кода в момент hello, читайте дальше.</span><span class="sxs-lookup"><span data-stu-id="bb853-183">If you don't understand hello last line of this code at hello moment, read on.</span></span> <span data-ttu-id="bb853-184">В hello оставшейся части документа мы активно рассмотрим использование R в среде машинного обучения Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-184">In hello rest of this document we will extensively discuss using R in hello Azure Machine Learning environment.</span></span>

### <a name="introduction-toorstudio"></a><span data-ttu-id="bb853-185">Введение tooRStudio</span><span class="sxs-lookup"><span data-stu-id="bb853-185">Introduction tooRStudio</span></span>
<span data-ttu-id="bb853-186">RStudio является широко используемым интегрированной среды разработки для R. Я использую RStudio для редактирования, тестирование и отладка некоторой части кода hello R, используемых в этом кратком руководстве.</span><span class="sxs-lookup"><span data-stu-id="bb853-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of hello R code used in this quick start guide.</span></span> <span data-ttu-id="bb853-187">После тестирования и готов код R, просто копировать и вставлять из редактора RStudio hello в студию машинного обучения [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-187">Once R code is tested and ready, you simply cut and paste from hello RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="bb853-188">Если у вас установлена на настольном компьютере язык программирования hello R, я рекомендую сделать это сейчас.</span><span class="sxs-lookup"><span data-stu-id="bb853-188">If you do not have hello R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="bb853-189">Бесплатные файлы для загрузки языка R с открытым кодом можно найти по адресу hello сети полный архив R (CRAN) в [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="bb853-189">Free downloads of open source R language are available at hello Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="bb853-190">Доступны файлы для скачивания для Windows, Mac OS и Linux или UNIX.</span><span class="sxs-lookup"><span data-stu-id="bb853-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="bb853-191">Выберите близлежащих зеркала и следуйте приведенным инструкциям загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-191">Choose a nearby mirror and follow hello download directions.</span></span> <span data-ttu-id="bb853-192">CRAN также содержит множество полезных пакетов для аналитики и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="bb853-193">Если новый tooRStudio, необходимо загрузить и установить версию для настольного компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-193">If you are new tooRStudio, you should download and install hello desktop version.</span></span> <span data-ttu-id="bb853-194">Можно найти RStudio загружаемые файлы для Windows, Mac OS и Linux и UNIX на http://www.rstudio.com/products/RStudio/ приветствия.</span><span class="sxs-lookup"><span data-stu-id="bb853-194">You can find hello RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="bb853-195">Следуйте приведенным инструкциям hello, предоставляемые tooinstall RStudio на настольном компьютере.</span><span class="sxs-lookup"><span data-stu-id="bb853-195">Follow hello directions provided tooinstall RStudio on your desktop machine.</span></span>  

<span data-ttu-id="bb853-196">Введение в учебник tooRStudio находится в https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="bb853-196">A tutorial introduction tooRStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="bb853-197">Дополнительные сведения по использованию RStudio можно найти в [Приложении А][appendixa].</span><span class="sxs-lookup"><span data-stu-id="bb853-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="bb853-198"><a id="scriptmodule"></a>Получение данных из модуля hello выполнение скрипта R</span><span class="sxs-lookup"><span data-stu-id="bb853-198"><a id="scriptmodule"></a>Get data in and out of hello Execute R Script module</span></span>
<span data-ttu-id="bb853-199">В этом разделе мы рассмотрим, как получить данные в действие и из hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-199">In this section we will discuss how you get data into and out of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="bb853-200">Мы рассмотрим, как toohandle различные типы данных считывать в действие и из hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-200">We will review how toohandle various data types read into and out of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="bb853-201">Hello полный код для этого раздела находится в hello ZIP-файл, загруженный ранее.</span><span class="sxs-lookup"><span data-stu-id="bb853-201">hello complete code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="bb853-202">Загрузка и проверка данных в Студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="bb853-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="bb853-203"><a id="loading"></a>Загрузить набор данных hello</span><span class="sxs-lookup"><span data-stu-id="bb853-203"><a id="loading"></a>Load hello dataset</span></span>
<span data-ttu-id="bb853-204">Начнем с загрузкой hello **csdairydata.csv** файла в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-204">We will start by loading hello **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="bb853-205">Запустите среду Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="bb853-206">Щелкните **+ создать** в hello понизить левой части экрана и выберите **набора данных**.</span><span class="sxs-lookup"><span data-stu-id="bb853-206">Click on **+ NEW** at hello lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="bb853-207">Выберите **из локального файла**, а затем **Обзор** tooselect hello файла.</span><span class="sxs-lookup"><span data-stu-id="bb853-207">Select **From Local File**, and then **Browse** tooselect hello file.</span></span>
* <span data-ttu-id="bb853-208">Убедитесь, что вы выбрали **универсального CSV-файл с заголовком (.csv)** hello тип для набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-208">Make sure you have selected **Generic CSV file with header (.csv)** as hello type for hello dataset.</span></span>
* <span data-ttu-id="bb853-209">Щелкните флажок hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-209">Click hello check mark.</span></span>
* <span data-ttu-id="bb853-210">После передачи hello набора данных вы увидите новый набор данных hello, щелкнув hello **наборы данных** вкладки.</span><span class="sxs-lookup"><span data-stu-id="bb853-210">After hello dataset has been uploaded, you should see hello new dataset by clicking on hello **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="bb853-211">Создание эксперимента</span><span class="sxs-lookup"><span data-stu-id="bb853-211">Create an experiment</span></span>
<span data-ttu-id="bb853-212">Теперь, когда у нас есть некоторые данные в студии машинного обучения, нам нужна toocreate анализ hello toodo эксперимента.</span><span class="sxs-lookup"><span data-stu-id="bb853-212">Now that we have some data in Machine Learning Studio, we need toocreate an experiment toodo hello analysis.</span></span>  

* <span data-ttu-id="bb853-213">Щелкните **+ создать** в списке hello левому нижнему углу и выберите **эксперимента**, затем **пустой эксперимента**.</span><span class="sxs-lookup"><span data-stu-id="bb853-213">Click on **+ NEW** at hello lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="bb853-214">Назовите эксперимента, выбрав и изменение, hello **эксперимента создан на...**  заголовок вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="bb853-214">You can name your experiment by selecting, and modifying, hello **Experiment created on ...** title at hello top of hello page.</span></span> <span data-ttu-id="bb853-215">Например, изменение слишком**ЦС Молоко Analysis**.</span><span class="sxs-lookup"><span data-stu-id="bb853-215">For example, changing it too**CA Dairy Analysis**.</span></span>
* <span data-ttu-id="bb853-216">Слева hello hello эксперимента страницы разверните **сохраненные наборы данных**, а затем **Мои наборы данных**.</span><span class="sxs-lookup"><span data-stu-id="bb853-216">On hello left of hello experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="bb853-217">Вы увидите hello **cadairydata.csv** загруженный ранее.</span><span class="sxs-lookup"><span data-stu-id="bb853-217">You should see hello **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="bb853-218">Перетаскивание hello **csdairydata.csv dataset** на hello эксперимента.</span><span class="sxs-lookup"><span data-stu-id="bb853-218">Drag and drop hello **csdairydata.csv dataset** onto hello experiment.</span></span>
* <span data-ttu-id="bb853-219">В hello **поиска поэкспериментировать элементы** поле в верхней части hello hello левой панели, то тип [выполнение скрипта R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="bb853-219">In hello **Search experiment items** box on hello top of hello left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="bb853-220">Вы увидите, отображаются в списке поиска hello модуля hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-220">You will see hello module appear in hello search list.</span></span>
* <span data-ttu-id="bb853-221">Перетаскивание hello [выполнение скрипта R] [ execute-r-script] модуля на вашей палитра.</span><span class="sxs-lookup"><span data-stu-id="bb853-221">Drag and drop hello [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="bb853-222">Подсоедините hello выход hello **csdairydata.csv dataset** toohello крайний левый вход (**Dataset1**) из hello [выполнение скрипта R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="bb853-222">Connect hello output of hello **csdairydata.csv dataset** toohello leftmost input (**Dataset1**) of hello [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="bb853-223">**Не забывайте tooclick на «Сохранить»**</span><span class="sxs-lookup"><span data-stu-id="bb853-223">**Don't forget tooclick on 'Save'!**</span></span>  

<span data-ttu-id="bb853-224">На этом этапе ваш эксперимент должен выглядеть, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="bb853-224">At this point your experiment should look something like Figure 3.</span></span>

![Hello анализа Молоко ЦС поэкспериментировать с набора данных и выполнение скрипта R модуля][3]

<span data-ttu-id="bb853-226">*Рис. 3. Hello анализа Молоко ЦС поэкспериментировать с набора данных и выполнение скрипта R модуля.*</span><span class="sxs-lookup"><span data-stu-id="bb853-226">*Figure 3. hello CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-hello-data"></a><span data-ttu-id="bb853-227">Проверка данных hello</span><span class="sxs-lookup"><span data-stu-id="bb853-227">Check on hello data</span></span>
<span data-ttu-id="bb853-228">Давайте посмотрим на hello данные, которые мы загрузили в нашем эксперимент.</span><span class="sxs-lookup"><span data-stu-id="bb853-228">Let's have a look at hello data we have loaded into our experiment.</span></span> <span data-ttu-id="bb853-229">В эксперименте hello, щелкните на результате hello hello **cadairydata.csv dataset** и выберите **визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="bb853-229">In hello experiment, click on hello output of hello **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="bb853-230">Вы увидите нечто вроде этого (рис. 4):</span><span class="sxs-lookup"><span data-stu-id="bb853-230">You should see something like Figure 4.</span></span>  

![Сводка по набору данных cadairydata.csv hello][4]

<span data-ttu-id="bb853-232">*Рис. 4. Сводка hello cadairydata.csv dataset.*</span><span class="sxs-lookup"><span data-stu-id="bb853-232">*Figure 4. Summary of hello cadairydata.csv dataset.*</span></span>

<span data-ttu-id="bb853-233">Здесь представлено много полезной информации.</span><span class="sxs-lookup"><span data-stu-id="bb853-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="bb853-234">Мы видим hello первые несколько строк того же набора данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-234">We can see hello first several rows of that dataset.</span></span> <span data-ttu-id="bb853-235">Если выбирается столбец hello раздел статистики показывает Дополнительные сведения о столбце hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-235">If we select a column, hello Statistics section shows more information about hello column.</span></span> <span data-ttu-id="bb853-236">Например строка hello тип компонента показывает, какие типы данных столбца toohello назначенный студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-236">For example, hello Feature Type row shows us what data types Azure Machine Learning Studio assigned toohello column.</span></span> <span data-ttu-id="bb853-237">Наличие быстрого выглядят следующим образом — хороший проверочной, прежде чем начать toodo серьезные несохраненные.</span><span class="sxs-lookup"><span data-stu-id="bb853-237">Having a quick look like this is a good sanity check before we start toodo any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="bb853-238">Первый сценарий R</span><span class="sxs-lookup"><span data-stu-id="bb853-238">First R script</span></span>
<span data-ttu-id="bb853-239">Давайте создадим простой первый tooexperiment R-скрипт с в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-239">Let's create a simple first R script tooexperiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="bb853-240">Я создания и тестирования hello, выполнив скрипт в RStudio.</span><span class="sxs-lookup"><span data-stu-id="bb853-240">I have created and tested hello following script in RStudio.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="bb853-241">Осталось tootransfer этот сценарий tooAzure студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="bb853-241">Now I need tootransfer this script tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="bb853-242">Можно было бы его просто вырезать и вставить.</span><span class="sxs-lookup"><span data-stu-id="bb853-242">I could simply cut and paste.</span></span> <span data-ttu-id="bb853-243">Но в данном случае я перенесу свой скрипт R при помощи ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="bb853-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-toohello-execute-r-script-module"></a><span data-ttu-id="bb853-244">Модуль выполнение скрипта R toohello входных данных</span><span class="sxs-lookup"><span data-stu-id="bb853-244">Data input toohello Execute R Script module</span></span>
<span data-ttu-id="bb853-245">Давайте посмотрим на toohello входов hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-245">Let's have a look at hello inputs toohello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="bb853-246">В этом примере мы будет считываются данные молока Калифорния hello hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-246">In this example we will read hello California dairy data into hello [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="bb853-247">Существует три возможных входных значений для hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-247">There are three possible inputs for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="bb853-248">В зависимости от приложения можно использовать любой из них или все.</span><span class="sxs-lookup"><span data-stu-id="bb853-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="bb853-249">Это вполне разумным toouse R-сценарий, который не принимает входные данные во всех.</span><span class="sxs-lookup"><span data-stu-id="bb853-249">It is also perfectly reasonable toouse an R script that takes no input at all.</span></span>  

<span data-ttu-id="bb853-250">Давайте рассмотрим каждый из входных данных, поступающих из левой tooright.</span><span class="sxs-lookup"><span data-stu-id="bb853-250">Let's look at each of these inputs, going from left tooright.</span></span> <span data-ttu-id="bb853-251">Вы увидите hello имена каждого входа hello, наведя курсор на hello входных данных и чтение hello всплывающей подсказки.</span><span class="sxs-lookup"><span data-stu-id="bb853-251">You can see hello names of each of hello inputs by placing your cursor over hello input and reading hello tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="bb853-252">Пакет скриптов</span><span class="sxs-lookup"><span data-stu-id="bb853-252">Script Bundle</span></span>
<span data-ttu-id="bb853-253">Hello пакет сценария ввода позволяет toopass hello содержимое ZIP-файл в [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-253">hello Script Bundle input allows you toopass hello contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="bb853-254">Используются следующие команды tooread hello содержимое hello ZIP-файл в коде R hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-254">You can use one of hello following commands tooread hello contents of hello zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="bb853-255">Машинное обучение Azure обрабатывает файлы в архив hello, как если бы они находятся в hello src / directory, поэтому требуется tooprefix имена файл с таким именем каталога.</span><span class="sxs-lookup"><span data-stu-id="bb853-255">Azure Machine Learning treats files in hello zip as if they are in hello src/ directory, so you need tooprefix your file names with this directory name.</span></span> <span data-ttu-id="bb853-256">Например, если hello zip содержит файлы hello `yourfile.R` и `yourData.rdata` в корне hello zip hello, можно по адресу их как `src/yourfile.R` и `src/yourData.rdata` при использовании `source` и `load`.</span><span class="sxs-lookup"><span data-stu-id="bb853-256">For example, if hello zip contains hello files `yourfile.R` and `yourData.rdata` in hello root of hello zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="bb853-257">Мы уже рассмотрели Загрузка наборов данных в [загрузке набора данных hello](#loading).</span><span class="sxs-lookup"><span data-stu-id="bb853-257">We already discussed loading datasets in [Loading hello dataset](#loading).</span></span> <span data-ttu-id="bb853-258">После создания и проверки hello R сценарий, показанный в предыдущем разделе hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="bb853-258">Once you have created and tested hello R script shown in hello previous section, do hello following:</span></span>

1. <span data-ttu-id="bb853-259">Сохранить скрипт hello R в. R-файл.</span><span class="sxs-lookup"><span data-stu-id="bb853-259">Save hello R script into a .R file.</span></span> <span data-ttu-id="bb853-260">Я назвал свой файл скрипта "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="bb853-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="bb853-261">Вот содержимое hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-261">Here's hello contents.</span></span>
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="bb853-262">Создайте ZIP-файл и скопируйте в него свой скрипт.</span><span class="sxs-lookup"><span data-stu-id="bb853-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="bb853-263">В Windows, правой кнопкой мыши файл hello и выберите **отправки**, а затем **сжатая папка**.</span><span class="sxs-lookup"><span data-stu-id="bb853-263">On Windows, you can right-click on hello file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="bb853-264">Это создаст новый ZIP-файл, содержащий hello «simpleplot. Файл R».</span><span class="sxs-lookup"><span data-stu-id="bb853-264">This will create a new zip file containing hello "simpleplot.R" file.</span></span>
3. <span data-ttu-id="bb853-265">Добавьте в файл toohello **наборы данных** в студии машинного обучения, указав тип hello как **zip**.</span><span class="sxs-lookup"><span data-stu-id="bb853-265">Add your file toohello **datasets** in Machine Learning Studio, specifying hello type as **zip**.</span></span> <span data-ttu-id="bb853-266">Теперь вы увидите hello ZIP-файл в наборах данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-266">You should now see hello zip file in your datasets.</span></span>
4. <span data-ttu-id="bb853-267">Перетаскивание hello ZIP-файл из **наборы данных** на hello **холст ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="bb853-267">Drag and drop hello zip file from **datasets** onto hello **ML Studio canvas**.</span></span>
5. <span data-ttu-id="bb853-268">Подсоедините hello выход hello **ZIP-архив данных** toohello значок **пакет сценария** вводу hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-268">Connect hello output of hello **zip data** icon toohello **Script Bundle** input of hello [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="bb853-269">Тип hello `source()` функция с именем zip файл в окне кода hello для hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-269">Type hello `source()` function with your zip file name into hello code window for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="bb853-270">В данном случае введено `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="bb853-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="bb853-271">Обязательно щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bb853-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="bb853-272">После выполнения этих действий, hello [выполнение скрипта R] [ execute-r-script] модуль будет выполняться скрипт hello R в ZIP-файле hello при запуске эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-272">Once these steps are complete, hello [Execute R Script][execute-r-script] module will execute hello R script in hello zip file when hello experiment is run.</span></span> <span data-ttu-id="bb853-273">На этом этапе ваш эксперимент должен выглядеть, как изображено на рисунке 5.</span><span class="sxs-lookup"><span data-stu-id="bb853-273">At this point your experiment should look something like Figure 5.</span></span>

![Эксперимент с использованием сценария R, сжатого в ZIP-файл][6]

<span data-ttu-id="bb853-275">*Рис. 5. Эксперимент с использованием сценария R, сжатого в ZIP-файл*</span><span class="sxs-lookup"><span data-stu-id="bb853-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="bb853-276">Набор данных 1</span><span class="sxs-lookup"><span data-stu-id="bb853-276">Dataset1</span></span>
<span data-ttu-id="bb853-277">Прямоугольный таблицу tooyour R код данных можно передавать с помощью ввода hello Dataset1.</span><span class="sxs-lookup"><span data-stu-id="bb853-277">You can pass a rectangular table of data tooyour R code by using hello Dataset1 input.</span></span> <span data-ttu-id="bb853-278">В нашей hello простой сценарий `maml.mapInputPort(1)` функция считывает hello данные из порта 1.</span><span class="sxs-lookup"><span data-stu-id="bb853-278">In our simple script hello `maml.mapInputPort(1)` function reads hello data from port 1.</span></span> <span data-ttu-id="bb853-279">Эти данные затем присваивается имя переменной tooa кадр данных в коде.</span><span class="sxs-lookup"><span data-stu-id="bb853-279">This data is then assigned tooa dataframe variable name in your code.</span></span> <span data-ttu-id="bb853-280">В нашем сценарии простой hello первой строки кода выполняет hello назначения.</span><span class="sxs-lookup"><span data-stu-id="bb853-280">In our simple script hello first line of code performs hello assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="bb853-281">Выполнение эксперимента, щелкнув hello **запуска** кнопки.</span><span class="sxs-lookup"><span data-stu-id="bb853-281">Execute your experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="bb853-282">После завершения выполнения hello, щелкните hello [выполнение скрипта R] [ execute-r-script] модуля, а затем нажмите кнопку **просмотреть выходной журнал** на панели свойств hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-282">When hello execution finishes, click on hello [Execute R Script][execute-r-script] module and then click **View output log** on hello properties pane.</span></span> <span data-ttu-id="bb853-283">Новая страница откроется в браузере, показывающая hello содержимое файла файл output.log hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-283">A new page should appear in your browser showing hello contents of hello output.log file.</span></span> <span data-ttu-id="bb853-284">При прокрутке вы увидите примерно hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="bb853-284">When you scroll down you should see something like hello following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="bb853-285">Дальше вниз hello страница является более подробные сведения о hello столбцы, которые будет выглядеть примерно hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="bb853-285">Farther down hello page is more detailed information on hello columns, which will look something like hello following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="bb853-286">Эти результаты, главным образом, как и ожидалось, с 228 наблюдения и 9 столбцами в кадр данных hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-286">These results are mostly as expected, with 228 observations and 9 columns in hello dataframe.</span></span> <span data-ttu-id="bb853-287">Мы видим hello имена столбцов, тип данных hello R и образец каждого столбца.</span><span class="sxs-lookup"><span data-stu-id="bb853-287">We can see hello column names, hello R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="bb853-288">Этот же вывода на печать удобно доступен из hello выходные данные устройства R hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-288">This same printed output is conveniently available from hello R Device output of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="bb853-289">Мы обсудим hello выходы hello [выполнение скрипта R] [ execute-r-script] модуля в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-289">We will discuss hello outputs of hello [Execute R Script][execute-r-script] module in hello next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="bb853-290">Набор данных 2</span><span class="sxs-lookup"><span data-stu-id="bb853-290">Dataset2</span></span>
<span data-ttu-id="bb853-291">Hello поведение hello Dataset2 входные данные не идентичные toothat Dataset1.</span><span class="sxs-lookup"><span data-stu-id="bb853-291">hello behavior of hello Dataset2 input is identical toothat of Dataset1.</span></span> <span data-ttu-id="bb853-292">С помощью этого порта можно передать еще одну прямоугольную таблицу данных в код на R.</span><span class="sxs-lookup"><span data-stu-id="bb853-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="bb853-293">Здравствуйте, функция `maml.mapInputPort(2)`, с аргументом hello 2, является используется toopass эти данные.</span><span class="sxs-lookup"><span data-stu-id="bb853-293">hello function `maml.mapInputPort(2)`, with hello argument 2, is used toopass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="bb853-294">Порты вывода модуля "Выполнение скрипта R"</span><span class="sxs-lookup"><span data-stu-id="bb853-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="bb853-295">Вывод таблицы данных</span><span class="sxs-lookup"><span data-stu-id="bb853-295">Output a dataframe</span></span>
<span data-ttu-id="bb853-296">Можно вывести содержимое hello кадр данных R как таблицу прямоугольный через порт hello Dataset1 результат с помощью hello `maml.mapOutputPort()` функции.</span><span class="sxs-lookup"><span data-stu-id="bb853-296">You can output hello contents of an R dataframe as a rectangular table through hello Result Dataset1 port by using hello `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="bb853-297">В нашей простой сценарий R это выполняется по следующей строкой hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-297">In our simple R script this is performed by hello following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="bb853-298">После выполнения эксперимента hello, щелкните порт вывода результата Dataset1 hello и выберите команду **визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="bb853-298">After running hello experiment, click on hello Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="bb853-299">Вы увидите нечто вроде этого (рис. 6):</span><span class="sxs-lookup"><span data-stu-id="bb853-299">You should see something like Figure 6.</span></span>

![визуализация Hello hello выходной hello молока данных Калифорния][7]

<span data-ttu-id="bb853-301">*Рис. 6. визуализация Hello hello выходной hello молока данных Калифорнии.*</span><span class="sxs-lookup"><span data-stu-id="bb853-301">*Figure 6. hello visualization of hello output of hello California dairy data.*</span></span>

<span data-ttu-id="bb853-302">Это выходные данные выглядят идентичными toohello данные, точно так, как ожидалось.</span><span class="sxs-lookup"><span data-stu-id="bb853-302">This output looks identical toohello input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="bb853-303">Порт вывода "Устройство R"</span><span class="sxs-lookup"><span data-stu-id="bb853-303">R Device output</span></span>
<span data-ttu-id="bb853-304">Здравствуйте, выходные данные устройства hello [выполнение скрипта R] [ execute-r-script] модуль выходными данными сообщения и графики.</span><span class="sxs-lookup"><span data-stu-id="bb853-304">hello Device output of hello [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="bb853-305">Оба стандартный выход и Стандартная ошибка сообщения из R отправляются toohello устройство R выходной порт.</span><span class="sxs-lookup"><span data-stu-id="bb853-305">Both standard output and standard error messages from R are sent toohello R Device output port.</span></span>  

<span data-ttu-id="bb853-306">hello tooview R вывода на устройство, щелкните на порту hello, а затем на **визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="bb853-306">tooview hello R Device output, click on hello port and then on **Visualize**.</span></span> <span data-ttu-id="bb853-307">Мы видим hello стандартный вывод и стандартную ошибку из сценария hello R на рис. 7.</span><span class="sxs-lookup"><span data-stu-id="bb853-307">We see hello standard output and standard error from hello R script in Figure 7.</span></span>

![Стандартный выход и Стандартная ошибка из hello порт устройства R][8]

<span data-ttu-id="bb853-309">*Рис. 7. Стандартный выход и Стандартная ошибка из hello порт устройство R.*</span><span class="sxs-lookup"><span data-stu-id="bb853-309">*Figure 7. Standard output and standard error from hello R Device port.*</span></span>

<span data-ttu-id="bb853-310">Прокрутка вниз мы вывод hello графики из наших сценария R на рис. 8.</span><span class="sxs-lookup"><span data-stu-id="bb853-310">Scrolling down we see hello graphics output from our R script in Figure 8.</span></span>  

![Вывод графики hello порт устройства R][9]

<span data-ttu-id="bb853-312">*Рис. 8. Выходные данные hello порт устройства R графики.*</span><span class="sxs-lookup"><span data-stu-id="bb853-312">*Figure 8. Graphics output from hello R Device port.*</span></span>  

## <span data-ttu-id="bb853-313"><a id="filtering"></a>Фильтрация и преобразование данных</span><span class="sxs-lookup"><span data-stu-id="bb853-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="bb853-314">В этом разделе мы выполним некоторые операции преобразования hello Калифорния молока данных и фильтрации данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-314">In this section we will perform some basic data filtering and transformation operations on hello California dairy data.</span></span> <span data-ttu-id="bb853-315">Концу hello в этом разделе будет иметь данные в формате, удобном для построения аналитических моделей.</span><span class="sxs-lookup"><span data-stu-id="bb853-315">By hello end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="bb853-316">В частности, в этом разделе мы выполним несколько распространенных задач по очистке и преобразованию данных: преобразование типа данных, фильтрацию кадров данных, добавление новых вычисляемых столбцов и преобразование значений.</span><span class="sxs-lookup"><span data-stu-id="bb853-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="bb853-317">Этот цвет фона поможет вам работать с hello множество вариантов, в реальных проблем.</span><span class="sxs-lookup"><span data-stu-id="bb853-317">This background should help you deal with hello many variations encountered in real-world problems.</span></span>

<span data-ttu-id="bb853-318">Hello полный код R для этого раздела, доступен в hello ZIP-файл, загруженный ранее.</span><span class="sxs-lookup"><span data-stu-id="bb853-318">hello complete R code for this section is available in hello zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="bb853-319">Преобразование типов данных</span><span class="sxs-lookup"><span data-stu-id="bb853-319">Type transformations</span></span>
<span data-ttu-id="bb853-320">Теперь, когда мы могут считывать данные молока Калифорния hello выполнения кода hello R в hello [выполнение скрипта R] [ execute-r-script] модуля, нам нужно tooensure наличие hello данные в столбцах hello hello предназначен тип и формат.</span><span class="sxs-lookup"><span data-stu-id="bb853-320">Now that we can read hello California dairy data into hello R code in hello [Execute R Script][execute-r-script] module, we need tooensure that hello data in hello columns has hello intended type and format.</span></span>  

<span data-ttu-id="bb853-321">R — это динамически типизированный язык, это означает, что типы данных преобразуются из одного tooanother при необходимости.</span><span class="sxs-lookup"><span data-stu-id="bb853-321">R is a dynamically typed language, which means that data types are coerced from one tooanother as required.</span></span> <span data-ttu-id="bb853-322">типы атомарных данных Hello в R: числовые, логические и символ.</span><span class="sxs-lookup"><span data-stu-id="bb853-322">hello atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="bb853-323">Тип Hello фактор — категориальные данные в хранилище используется toocompactly.</span><span class="sxs-lookup"><span data-stu-id="bb853-323">hello factor type is used toocompactly store categorical data.</span></span> <span data-ttu-id="bb853-324">Гораздо Дополнительные сведения о типах данных можно найти в ссылках hello в [приложение B - дальнейшего изучения](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="bb853-324">You can find much more information on data types in hello references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="bb853-325">При считывании табличных данных в R из внешнего источника, всегда является хорошей идеей hello toocheck, возникающие в типы столбцов hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-325">When tabular data is read into R from an external source, it is always a good idea toocheck hello resulting types in hello columns.</span></span> <span data-ttu-id="bb853-326">Зачастую может оказаться, что данные в столбце не символьного типа, как предполагалось, а относятся к типу фактор (или наоборот).</span><span class="sxs-lookup"><span data-stu-id="bb853-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="bb853-327">В других случаях столбец, который должен содержать числовые данные, содержит символьные данные, например «1,23» вместо 1,23 — числа с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="bb853-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="bb853-328">К счастью это просто tooconvert один тип tooanother, при условии, что сопоставление возможно.</span><span class="sxs-lookup"><span data-stu-id="bb853-328">Fortunately, it is easy tooconvert one type tooanother, as long as mapping is possible.</span></span> <span data-ttu-id="bb853-329">Например «Невада» нельзя преобразовать в числовое значение, но ее можно будет преобразовать tooa коэффициент (категориальной переменной).</span><span class="sxs-lookup"><span data-stu-id="bb853-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it tooa factor (categorical variable).</span></span> <span data-ttu-id="bb853-330">Еще один пример. Числовое значение 1 можно преобразовать в символ '1' или в фактор.</span><span class="sxs-lookup"><span data-stu-id="bb853-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="bb853-331">простой синтаксис Hello для любого из этих преобразований: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="bb853-331">hello syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="bb853-332">Эти функции преобразования типов включают следующие hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-332">These type conversion functions include hello following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="bb853-333">Просмотрев hello типы данных столбцов hello, мы входные данные в предыдущем разделе hello: все столбцы имеют тип числовой, за исключением столбца hello с меткой «Месяц», тип символа.</span><span class="sxs-lookup"><span data-stu-id="bb853-333">Looking at hello data types of hello columns we input in hello previous section: all columns are of type numeric, except for hello column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="bb853-334">Давайте преобразовать этот коэффициент tooa и hello результаты теста.</span><span class="sxs-lookup"><span data-stu-id="bb853-334">Let's convert this tooa factor and test hello results.</span></span>  

<span data-ttu-id="bb853-335">Я удалил строку hello, матрица scatterplot hello созданы и добавлены строки, преобразование коэффициент tooa столбец «Month» hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-335">I have deleted hello line that created hello scatterplot matrix and added a line converting hello 'Month' column tooa factor.</span></span> <span data-ttu-id="bb853-336">В моей эксперименте я будет просто вырежьте и вставьте hello R код в окно кода hello hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-336">In my experiment I will just cut and paste hello R code into hello code window of hello [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="bb853-337">Можно также обновить hello ZIP-файл и отправьте его tooAzure студии машинного обучения, но это занимает несколько шагов.</span><span class="sxs-lookup"><span data-stu-id="bb853-337">You could also update hello zip file and upload it tooAzure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="bb853-338">Давайте выполните этот код и посмотрите на hello выходном файле журнала hello R-сценария.</span><span class="sxs-lookup"><span data-stu-id="bb853-338">Let's execute this code and look at hello output log for hello R script.</span></span> <span data-ttu-id="bb853-339">на рис. 9 показан Hello необходимые данные из журнала hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-339">hello relevant data from hello log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="bb853-340">*Рис. 9. Сводка hello кадр данных с переменной коэффициент.*</span><span class="sxs-lookup"><span data-stu-id="bb853-340">*Figure 9. Summary of hello dataframe with a factor variable.*</span></span>

<span data-ttu-id="bb853-341">должно появиться сообщение Hello тип для месяца "**коэффициент с 14 уровней**".</span><span class="sxs-lookup"><span data-stu-id="bb853-341">hello type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="bb853-342">Это проблема, поскольку существуют только в течение 12 месяцев года hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-342">This is a problem since there are only 12 months in hello year.</span></span> <span data-ttu-id="bb853-343">Можно также проверить, hello типа toosee в **визуализировать** hello результирующий набор данных является порт "**категориальная**".</span><span class="sxs-lookup"><span data-stu-id="bb853-343">You can also check toosee that hello type in **Visualize** of hello Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="bb853-344">Hello проблема в том, «Month», столбец не был закодирован систематически hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-344">hello problem is that hello 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="bb853-345">В некоторых случаях месяц назван April, а в других — сокращенно Apr. Эту проблему можно решить путем обрезки символов too3 строку hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming hello string too3 characters.</span></span> <span data-ttu-id="bb853-346">Строка кода Hello теперь выглядит hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bb853-346">hello line of code now looks like hello following:</span></span>

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="bb853-347">Повторно запустите эксперимент hello и просмотреть журнал выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-347">Rerun hello experiment and view hello output log.</span></span> <span data-ttu-id="bb853-348">Hello тесты на ожидаемые результаты показаны на рис. 10.</span><span class="sxs-lookup"><span data-stu-id="bb853-348">hello expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="bb853-349">*Рис. 10. Сводные сведения о кадре данных hello с правильное число уровней коэффициент.*</span><span class="sxs-lookup"><span data-stu-id="bb853-349">*Figure 10. Summary of hello dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="bb853-350">Наш переменной коэффициент теперь имеет hello требуемого 12 уровней.</span><span class="sxs-lookup"><span data-stu-id="bb853-350">Our factor variable now has hello desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="bb853-351">Базовая фильтрация таблицы данных</span><span class="sxs-lookup"><span data-stu-id="bb853-351">Basic data frame filtering</span></span>
<span data-ttu-id="bb853-352">Таблицы данных R поддерживают массу возможностей фильтрации.</span><span class="sxs-lookup"><span data-stu-id="bb853-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="bb853-353">Наборы данных можно разбивать на подмножества, используя логическую фильтрацию по строкам или столбцам.</span><span class="sxs-lookup"><span data-stu-id="bb853-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="bb853-354">Во многих случаях вам потребуются сложные критерии фильтрации.</span><span class="sxs-lookup"><span data-stu-id="bb853-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="bb853-355">ссылки на Hello в [приложение B - дальнейшего изучения](#appendixb) содержат сложные примеры фильтрации блоки данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-355">hello references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="bb853-356">Выполним операцию фильтрации в нашем наборе данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="bb853-357">Если взглянуть на столбцы hello в кадр данных cadairydata hello, вы увидите два ненужных столбцов.</span><span class="sxs-lookup"><span data-stu-id="bb853-357">If you look at hello columns in hello cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="bb853-358">Hello первый столбец содержит только число строк, не очень удобен.</span><span class="sxs-lookup"><span data-stu-id="bb853-358">hello first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="bb853-359">второй столбец Hello, Year.Month, содержит избыточные сведения.</span><span class="sxs-lookup"><span data-stu-id="bb853-359">hello second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="bb853-360">Мы легко можно исключить эти столбцы, используя следующий код R hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-360">We can easily exclude these columns by using hello following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="bb853-361">Из теперь на этот раздел будет просто показано hello дополнительный код, добавленный в hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-361">From now on in this section, I will just show you hello additional code I am adding in hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="bb853-362">Каждой новой строки будут добавлены **перед** hello `str()` функции.</span><span class="sxs-lookup"><span data-stu-id="bb853-362">I will add each new line **before** hello `str()` function.</span></span> <span data-ttu-id="bb853-363">Я использую это функция tooverify результаты в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-363">I use this function tooverify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="bb853-364">Добавить следующие строки кода toomy R в hello hello [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-364">I add hello following line toomy R code in hello [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="bb853-365">Запустите этот код в эксперименте и проверяет результат hello из hello выходные данные журнала.</span><span class="sxs-lookup"><span data-stu-id="bb853-365">Run this code in your experiment and check hello result from hello output log.</span></span> <span data-ttu-id="bb853-366">Результат приведен на рис. 11.</span><span class="sxs-lookup"><span data-stu-id="bb853-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="bb853-367">*Рис. 11. Удалить сводку hello кадр данных с двумя столбцами.*</span><span class="sxs-lookup"><span data-stu-id="bb853-367">*Figure 11. Summary of hello dataframe with two columns removed.*</span></span>

<span data-ttu-id="bb853-368">Отличная новость!</span><span class="sxs-lookup"><span data-stu-id="bb853-368">Good news!</span></span> <span data-ttu-id="bb853-369">Мы получаем hello ожидалось результатов.</span><span class="sxs-lookup"><span data-stu-id="bb853-369">We get hello expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="bb853-370">Добавление нового столбца</span><span class="sxs-lookup"><span data-stu-id="bb853-370">Add a new column</span></span>
<span data-ttu-id="bb853-371">модели временных рядов toocreate будет удобный toohave столбце, содержащем hello месяцев с момента запуска hello hello временных рядов.</span><span class="sxs-lookup"><span data-stu-id="bb853-371">toocreate time series models it will be convenient toohave a column containing hello months since hello start of hello time series.</span></span> <span data-ttu-id="bb853-372">Мы создадим столбец Month.Count (Количество месяцев).</span><span class="sxs-lookup"><span data-stu-id="bb853-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="bb853-373">toohelp организации кода hello, мы создадим нашей первой простая функция `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="bb853-373">toohelp organize hello code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="bb853-374">Затем будет применена toocreate этой функции в новом столбце в кадр данных hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-374">We will then apply this function toocreate a new column in hello dataframe.</span></span> <span data-ttu-id="bb853-375">новый код Hello выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="bb853-375">hello new code is as follows.</span></span>

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="bb853-376">Теперь запустите эксперимент hello обновлены и использовать результаты hello выходные данные журнала tooview hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-376">Now run hello updated experiment and use hello output log tooview hello results.</span></span> <span data-ttu-id="bb853-377">Этот результат приведен на рисунке 12.</span><span class="sxs-lookup"><span data-stu-id="bb853-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="bb853-378">*Рис. 12. Сводка hello кадр данных с hello дополнительного столбца.*</span><span class="sxs-lookup"><span data-stu-id="bb853-378">*Figure 12. Summary of hello dataframe with hello additional column.*</span></span>

<span data-ttu-id="bb853-379">Похоже, все работает.</span><span class="sxs-lookup"><span data-stu-id="bb853-379">It looks like everything is working.</span></span> <span data-ttu-id="bb853-380">У нас есть hello новый столбец с ожидаемыми значениями hello в нашем кадр данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-380">We have hello new column with hello expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="bb853-381">Преобразование значений</span><span class="sxs-lookup"><span data-stu-id="bb853-381">Value transformations</span></span>
<span data-ttu-id="bb853-382">В этом разделе мы выполним некоторых простых преобразований по значениям hello в некоторых столбцах hello из наших кадр данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-382">In this section we will perform some simple transformations on hello values in some of hello columns of our dataframe.</span></span> <span data-ttu-id="bb853-383">язык Hello R поддерживает почти произвольное значение преобразования.</span><span class="sxs-lookup"><span data-stu-id="bb853-383">hello R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="bb853-384">ссылки на Hello в [приложение B — Дополнительные материалы](#appendixb) содержат сложные примеры.</span><span class="sxs-lookup"><span data-stu-id="bb853-384">hello references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="bb853-385">Если взглянуть на значения hello в hello сводки по нашей кадр данных вы увидите нечто нечетное здесь.</span><span class="sxs-lookup"><span data-stu-id="bb853-385">If you look at hello values in hello summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="bb853-386">Неужели мороженого в Калифорнии производят больше, чем молока?</span><span class="sxs-lookup"><span data-stu-id="bb853-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="bb853-387">Нет, конечно не так, как это не имеет никакого смысла, как этот факт жаль, что может быть toosome нас lovers мороженого.</span><span class="sxs-lookup"><span data-stu-id="bb853-387">No, of course not, as this makes no sense, sad as this fact may be toosome of us ice cream lovers.</span></span> <span data-ttu-id="bb853-388">единицы Hello отличаются.</span><span class="sxs-lookup"><span data-stu-id="bb853-388">hello units are different.</span></span> <span data-ttu-id="bb853-389">Цена Hello измеряется в нам фунты milk в единицах 1 млн фунты США, мороженого измеряется в 1000 нам галлоны и cottage Цилиндрическая измеряется в 1000 фунты США.</span><span class="sxs-lookup"><span data-stu-id="bb853-389">hello price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="bb853-390">При условии, что мороженого взвешивается около 6,5 фунты на галлон, мы можем легко hello эти значения, поэтому все они находятся в равных единиц 1000 фунты tooconvert умножения.</span><span class="sxs-lookup"><span data-stu-id="bb853-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do hello multiplication tooconvert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="bb853-391">В нашей модели прогнозирования мы используем мультипликативную модель для корректировки этих данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="bb853-392">Преобразование журнала позволяет нам toouse линейной модели, что упрощает этот процесс.</span><span class="sxs-lookup"><span data-stu-id="bb853-392">A log transformation allows us toouse a linear model, simplifying this process.</span></span> <span data-ttu-id="bb853-393">Можно применить преобразование журнала hello в hello же функции, где применяется множитель hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-393">We can apply hello log transformation in hello same function where hello multiplier is applied.</span></span>

<span data-ttu-id="bb853-394">В hello после кода, определить новую функцию `log.transform()`и примените его toohello строки, содержащие hello числовых значений.</span><span class="sxs-lookup"><span data-stu-id="bb853-394">In hello following code, I define a new function, `log.transform()`, and apply it toohello rows containing hello numerical values.</span></span> <span data-ttu-id="bb853-395">Hello R `Map()` функции — hello используется tooapply `log.transform()` toohello функция выбранные столбцы из hello кадр данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-395">hello R `Map()` function is used tooapply hello `log.transform()` function toohello selected columns of hello dataframe.</span></span> <span data-ttu-id="bb853-396">`Map()`Аналогично слишком`apply()` , но позволяет более одного списка аргументов функции toohello.</span><span class="sxs-lookup"><span data-stu-id="bb853-396">`Map()` is similar too`apply()` but allows for more than one list of arguments toohello function.</span></span> <span data-ttu-id="bb853-397">Обратите внимание, что список множители предоставляет hello второй аргумент toohello `log.transform()` функции.</span><span class="sxs-lookup"><span data-stu-id="bb853-397">Note that a list of multipliers supplies hello second argument toohello `log.transform()` function.</span></span> <span data-ttu-id="bb853-398">Hello `na.omit()` немного tooensure очистки мы нет отсутствующих или неопределенные значения в hello кадр данных используется функция.</span><span class="sxs-lookup"><span data-stu-id="bb853-398">hello `na.omit()` function is used as a bit of cleanup tooensure we do not have missing or undefined values in hello dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="bb853-399">Нет происходит довольно бит в hello `log.transform()` функции.</span><span class="sxs-lookup"><span data-stu-id="bb853-399">There is quite a bit happening in hello `log.transform()` function.</span></span> <span data-ttu-id="bb853-400">Большая часть кода поиск потенциальных проблем с аргументами hello, или работа с исключениями, которые по-прежнему могут возникнуть во время вычисления hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-400">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="bb853-401">Фактически только несколько строк кода hello вычислений.</span><span class="sxs-lookup"><span data-stu-id="bb853-401">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="bb853-402">Задача Hello hello защитного программирования — сбой hello tooprevent одну функцию, которая предотвращает обработку продолжение.</span><span class="sxs-lookup"><span data-stu-id="bb853-402">hello goal of hello defensive programming is tooprevent hello failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="bb853-403">Внезапный сбой продолжительного анализа — вещь довольно неприятная.</span><span class="sxs-lookup"><span data-stu-id="bb853-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="bb853-404">tooavoid, который ограничит этой ситуации возвращаемых значений необходимо выбрать, по умолчанию повредить toodownstream обработки.</span><span class="sxs-lookup"><span data-stu-id="bb853-404">tooavoid this situation, default return values must be chosen that will limit damage toodownstream processing.</span></span> <span data-ttu-id="bb853-405">Сообщение также является произведенных tooalert пользователей, которые пошло так.</span><span class="sxs-lookup"><span data-stu-id="bb853-405">A message is also produced tooalert users that something has gone wrong.</span></span>

<span data-ttu-id="bb853-406">Если вы не используется toodefensive программирование на языке R, этот код может показаться немного невозможной.</span><span class="sxs-lookup"><span data-stu-id="bb853-406">If you are not used toodefensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="bb853-407">Я поможет hello основных шагов:</span><span class="sxs-lookup"><span data-stu-id="bb853-407">I will walk you through hello major steps:</span></span>

1. <span data-ttu-id="bb853-408">Определяется вектор четырех сообщений.</span><span class="sxs-lookup"><span data-stu-id="bb853-408">A vector of four messages is defined.</span></span> <span data-ttu-id="bb853-409">Эти сообщения являются используется toocommunicate сведения о некоторых возможных ошибок hello и исключениях, возникающих с этим кодом.</span><span class="sxs-lookup"><span data-stu-id="bb853-409">These messages are used toocommunicate information about some of hello possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="bb853-410">Во всех этих случаях возвращается значение NA (нет данных).</span><span class="sxs-lookup"><span data-stu-id="bb853-410">I return a value of NA for each case.</span></span> <span data-ttu-id="bb853-411">Есть и другие возможности, у которых может быть меньше побочных эффектов.</span><span class="sxs-lookup"><span data-stu-id="bb853-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="bb853-412">Может возвратить вектор из нулей или исходного вектора входного hello, например.</span><span class="sxs-lookup"><span data-stu-id="bb853-412">I could return a vector of zeroes, or hello original input vector, for example.</span></span>
3. <span data-ttu-id="bb853-413">Проверка выполняется в функции toohello аргументы hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-413">Checks are run on hello arguments toohello function.</span></span> <span data-ttu-id="bb853-414">В каждом случае, если обнаруживается ошибка, возвращается значение по умолчанию и создается сообщение hello `warning()` функции.</span><span class="sxs-lookup"><span data-stu-id="bb853-414">In each case, if an error is detected, a default value is returned and a message is produced by hello `warning()` function.</span></span> <span data-ttu-id="bb853-415">Я использую `warning()` вместо `stop()` как последний hello нарушит выполнения, точно удается tooavoid.</span><span class="sxs-lookup"><span data-stu-id="bb853-415">I am using `warning()` rather than `stop()` as hello latter will terminate execution, exactly what I am trying tooavoid.</span></span> <span data-ttu-id="bb853-416">Обратите внимание, что при написании этого кода я использовал процедуры, поскольку использование функций сделало бы его сложнее и непонятнее.</span><span class="sxs-lookup"><span data-stu-id="bb853-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="bb853-417">Hello журнала вычислений упаковываются в `tryCatch()` , чтобы исключения не приведет к остановке внезапные tooprocessing.</span><span class="sxs-lookup"><span data-stu-id="bb853-417">hello log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt tooprocessing.</span></span> <span data-ttu-id="bb853-418">Без функции `tryCatch()` большинство ошибок, вызванных функциями R, вызывает сигнал остановки, что приводит именно к прерыванию.</span><span class="sxs-lookup"><span data-stu-id="bb853-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="bb853-419">Выполните этот код R в эксперименте и рассмотрим hello напечатанных выходные данные в файле файл output.log hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-419">Execute this R code in your experiment and have a look at hello printed output in hello output.log file.</span></span> <span data-ttu-id="bb853-420">Значения преобразования hello hello журнала четырех столбцов в hello, теперь будут видеть, как показано на рис. 13.</span><span class="sxs-lookup"><span data-stu-id="bb853-420">You will now see hello transformed values of hello four columns in hello log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="bb853-421">*Рис. 13. Сводка hello преобразования значения в кадр данных hello.*</span><span class="sxs-lookup"><span data-stu-id="bb853-421">*Figure 13. Summary of hello transformed values in hello dataframe.*</span></span>

<span data-ttu-id="bb853-422">Мы увидим, что значения hello были преобразованы.</span><span class="sxs-lookup"><span data-stu-id="bb853-422">We see hello values have been transformed.</span></span> <span data-ttu-id="bb853-423">Теперь производство молока значительно превышает по объемам производство остальных молочных продуктов (не забывайте, что мы используем логарифмическую шкалу).</span><span class="sxs-lookup"><span data-stu-id="bb853-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="bb853-424">Теперь все наши данные в порядке и мы можем приступать к моделированию.</span><span class="sxs-lookup"><span data-stu-id="bb853-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="bb853-425">Просмотрев hello визуализации сводки для hello выходных данных результирующего набора данных из наших [выполнение скрипта R] [ execute-r-script] модуля, вы увидите столбец «Month» hello «Категориальная» с уникальными значениями, 12, снова так же, как мы старались .</span><span class="sxs-lookup"><span data-stu-id="bb853-425">Looking at hello visualization summary for hello Result Dataset output of our [Execute R Script][execute-r-script] module, you will see hello 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="bb853-426"><a id="timeseries"></a>Объекты временного ряда и корреляционный анализ</span><span class="sxs-lookup"><span data-stu-id="bb853-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="bb853-427">В этом разделе мы исследовать несколько основных объектов R ряда времени и анализировать hello корреляции между некоторыми hello переменных.</span><span class="sxs-lookup"><span data-stu-id="bb853-427">In this section we will explore a few basic R time series objects and analyze hello correlations between some of hello variables.</span></span> <span data-ttu-id="bb853-428">Наша цель — toooutput кадр данных содержащего hello парные сведений о корреляции в несколько задержки.</span><span class="sxs-lookup"><span data-stu-id="bb853-428">Our goal is toooutput a dataframe containing hello pairwise correlation information at several lags.</span></span>

<span data-ttu-id="bb853-429">Hello полный код R для этого раздела находится в hello ZIP-файл, загруженный ранее.</span><span class="sxs-lookup"><span data-stu-id="bb853-429">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="bb853-430">Объекты временных рядов в языке R</span><span class="sxs-lookup"><span data-stu-id="bb853-430">Time series objects in R</span></span>
<span data-ttu-id="bb853-431">Как уже упоминалось, временные ряды представляют собой ряды значений данных, индексированные по времени.</span><span class="sxs-lookup"><span data-stu-id="bb853-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="bb853-432">R время ряд объектов, используемых toocreate индекса и управления им hello времени.</span><span class="sxs-lookup"><span data-stu-id="bb853-432">R time series objects are used toocreate and manage hello time index.</span></span> <span data-ttu-id="bb853-433">Существует несколько преимуществ toousing время ряда объектов.</span><span class="sxs-lookup"><span data-stu-id="bb853-433">There are several advantages toousing time series objects.</span></span> <span data-ttu-id="bb853-434">Объекты ряда времени освободить вас от hello многие элементы управления hello временных индекс значения, инкапсулированным в hello объекта.</span><span class="sxs-lookup"><span data-stu-id="bb853-434">Time series objects free you from hello many details of managing hello time series index values that are encapsulated in hello object.</span></span> <span data-ttu-id="bb853-435">Кроме того, время ряда объекты позволяют toouse hello много методов ряда времени для отображения на диаграмме, печать, моделирования и т. д.</span><span class="sxs-lookup"><span data-stu-id="bb853-435">In addition, time series objects allow you toouse hello many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="bb853-436">Hello POSIXct времени серии класс обычно используется и относительно проста.</span><span class="sxs-lookup"><span data-stu-id="bb853-436">hello POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="bb853-437">Этот класс ряда времени измеряет время от начала эпохи hello, 1 января 1970 года hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-437">This time series class measures time from hello start of hello epoch, January 1, 1970.</span></span> <span data-ttu-id="bb853-438">В этом примере мы будем использовать объекты временных рядов POSIXct.</span><span class="sxs-lookup"><span data-stu-id="bb853-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="bb853-439">Другие распространенные классы объектов временных рядов включают zoo и xts (расширяемые временные ряды).</span><span class="sxs-lookup"><span data-stu-id="bb853-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="bb853-440">Пример объекта временных рядов</span><span class="sxs-lookup"><span data-stu-id="bb853-440">Time series object example</span></span>
<span data-ttu-id="bb853-441">Приступим к разбору примера.</span><span class="sxs-lookup"><span data-stu-id="bb853-441">Let's get started with our example.</span></span> <span data-ttu-id="bb853-442">Перетащим **новый** модуль [Выполнить сценарий R][execute-r-script] в свой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="bb853-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="bb853-443">Подключения hello Dataset1 результат выходной порт hello существующих [выполнение скрипта R] [ execute-r-script] toohello модуль Dataset1 входному порту hello новый [выполнение скрипта R] [ execute-r-script] модуля.</span><span class="sxs-lookup"><span data-stu-id="bb853-443">Connect hello Result Dataset1 output port of hello existing [Execute R Script][execute-r-script] module toohello Dataset1 input port of hello new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="bb853-444">Как это делалось для первого примеры hello, как мы ход примере hello в некоторые моменты, которые будет показано только hello добавочное дополнительных строк кода R на каждом шаге.</span><span class="sxs-lookup"><span data-stu-id="bb853-444">As I did for hello first examples, as we progress through hello example, at some points I will show only hello incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-hello-dataframe"></a><span data-ttu-id="bb853-445">Чтение кадр данных hello</span><span class="sxs-lookup"><span data-stu-id="bb853-445">Reading hello dataframe</span></span>
<span data-ttu-id="bb853-446">В качестве первого шага давайте чтения в кадр данных и убедитесь, что мы получаем hello ожидалось результатов.</span><span class="sxs-lookup"><span data-stu-id="bb853-446">As a first step, let's read in a dataframe and make sure we get hello expected results.</span></span> <span data-ttu-id="bb853-447">Hello следующий код должен выполнять задания hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-447">hello following code should do hello job.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

<span data-ttu-id="bb853-448">Теперь запустите эксперимент hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-448">Now, run hello experiment.</span></span> <span data-ttu-id="bb853-449">Журнал Hello hello новую фигуру выполнение скрипта R должна выглядеть как на рис. 14.</span><span class="sxs-lookup"><span data-stu-id="bb853-449">hello log of hello new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="bb853-450">*Рис. 14. Сводные сведения о кадре данных hello в модуле выполнение скрипта R hello.*</span><span class="sxs-lookup"><span data-stu-id="bb853-450">*Figure 14. Summary of hello dataframe in hello Execute R Script module.*</span></span>

<span data-ttu-id="bb853-451">Эти данные являются типов ожидается hello и формат.</span><span class="sxs-lookup"><span data-stu-id="bb853-451">This data is of hello expected types and format.</span></span> <span data-ttu-id="bb853-452">Обратите внимание, что столбец «Month» hello имеет коэффициент тип имеет hello требуется число уровней.</span><span class="sxs-lookup"><span data-stu-id="bb853-452">Note that hello 'Month' column is of type factor and has hello expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="bb853-453">Создание объекта временных рядов</span><span class="sxs-lookup"><span data-stu-id="bb853-453">Creating a time series object</span></span>
<span data-ttu-id="bb853-454">Мы должны tooadd время кадр данных tooour рядов объекта.</span><span class="sxs-lookup"><span data-stu-id="bb853-454">We need tooadd a time series object tooour dataframe.</span></span> <span data-ttu-id="bb853-455">Замените текущий код hello hello следующее, что добавляется новый столбец класса POSIXct.</span><span class="sxs-lookup"><span data-stu-id="bb853-455">Replace hello current code with hello following, which adds a new column of class POSIXct.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

<span data-ttu-id="bb853-456">Теперь в журнале hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-456">Now, check hello log.</span></span> <span data-ttu-id="bb853-457">Результат приведен на рисунке 15.</span><span class="sxs-lookup"><span data-stu-id="bb853-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="bb853-458">*Рис. 15. Сводные сведения о кадре данных hello с объектом ряда времени.*</span><span class="sxs-lookup"><span data-stu-id="bb853-458">*Figure 15. Summary of hello dataframe with a time series object.*</span></span>

<span data-ttu-id="bb853-459">Мы увидим из сводки hello hello нового столбца на самом деле относится к классу POSIXct.</span><span class="sxs-lookup"><span data-stu-id="bb853-459">We can see from hello summary that hello new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-hello-data"></a><span data-ttu-id="bb853-460">Исследование и преобразование данных hello</span><span class="sxs-lookup"><span data-stu-id="bb853-460">Exploring and transforming hello data</span></span>
<span data-ttu-id="bb853-461">Рассмотрим некоторые из переменных hello в этом наборе данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-461">Let's explore some of hello variables in this dataset.</span></span> <span data-ttu-id="bb853-462">Матрица scatterplot — хороший способ tooproduce быстрого просмотра.</span><span class="sxs-lookup"><span data-stu-id="bb853-462">A scatterplot matrix is a good way tooproduce a quick look.</span></span> <span data-ttu-id="bb853-463">Я замена hello `str()` функции в предыдущем коде R hello со следующей строкой hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-463">I am replacing hello `str()` function in hello previous R code with hello following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="bb853-464">Выполним этот код и посмотрим на результат.</span><span class="sxs-lookup"><span data-stu-id="bb853-464">Run this code and see what happens.</span></span> <span data-ttu-id="bb853-465">Hello построения, произведенные hello порт устройства R должна выглядеть как на рисунке 16.</span><span class="sxs-lookup"><span data-stu-id="bb853-465">hello plot produced at hello R Device port should look like Figure 16.</span></span>

![Точечная диаграмма выбранных переменных][17]

<span data-ttu-id="bb853-467">*Рис. 16. Матрица точечной диаграммы выбранных переменных*</span><span class="sxs-lookup"><span data-stu-id="bb853-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="bb853-468">Есть некоторые odd-looking структуры в связях hello между этими переменными.</span><span class="sxs-lookup"><span data-stu-id="bb853-468">There is some odd-looking structure in hello relationships between these variables.</span></span> <span data-ttu-id="bb853-469">Возможно это возникает из тренды в данных hello и hello факт, что мы не стандартизованы hello переменных.</span><span class="sxs-lookup"><span data-stu-id="bb853-469">Perhaps this arises from trends in hello data and from hello fact that we have not standardized hello variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="bb853-470">Корреляционный анализ</span><span class="sxs-lookup"><span data-stu-id="bb853-470">Correlation analysis</span></span>
<span data-ttu-id="bb853-471">tooperform analysis корреляции, необходимые tooboth отменяется тенденций и стандартизировать hello переменных.</span><span class="sxs-lookup"><span data-stu-id="bb853-471">tooperform correlation analysis we need tooboth de-trend and standardize hello variables.</span></span> <span data-ttu-id="bb853-472">Можно просто использовать hello R `scale()` функции, которая центров и масштабирует переменных.</span><span class="sxs-lookup"><span data-stu-id="bb853-472">We could simply use hello R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="bb853-473">Возможно, это было бы быстрее.</span><span class="sxs-lookup"><span data-stu-id="bb853-473">This function might well run faster.</span></span> <span data-ttu-id="bb853-474">Тем не менее, я хочу tooshow вы примером защитного программирования в среде R.</span><span class="sxs-lookup"><span data-stu-id="bb853-474">However, I want tooshow you an example of defensive programing in R.</span></span>

<span data-ttu-id="bb853-475">Hello `ts.detrend()` показанную ниже функцию выполняет обе операции.</span><span class="sxs-lookup"><span data-stu-id="bb853-475">hello `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="bb853-476">Hello две следующие строки кода отменяется трендов данных hello и затем стандартизации значений hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-476">hello following two lines of code de-trend hello data and then standardize hello values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="bb853-477">Нет происходит довольно бит в hello `ts.detrend()` функции.</span><span class="sxs-lookup"><span data-stu-id="bb853-477">There is quite a bit happening in hello `ts.detrend()` function.</span></span> <span data-ttu-id="bb853-478">Большая часть кода поиск потенциальных проблем с аргументами hello, или работа с исключениями, которые по-прежнему могут возникнуть во время вычисления hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-478">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="bb853-479">Фактически только несколько строк кода hello вычислений.</span><span class="sxs-lookup"><span data-stu-id="bb853-479">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="bb853-480">Мы уже обсуждали пример защищенного программирования в разделе [Преобразование значений](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="bb853-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="bb853-481">Оба блока вычислений выполняются внутри функции `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="bb853-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="bb853-482">Для некоторых ошибок, это делает смысле tooreturn hello исходного входного вектора, и в других случаях возвратить вектора нули.</span><span class="sxs-lookup"><span data-stu-id="bb853-482">For some errors it makes sense tooreturn hello original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="bb853-483">Обратите внимание, что hello Линейная регрессия используется для отмены сведения о тенденциях Регрессия ряда времени.</span><span class="sxs-lookup"><span data-stu-id="bb853-483">Note that hello linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="bb853-484">Hello прогнозирующих переменных представляет собой объект ряда времени.</span><span class="sxs-lookup"><span data-stu-id="bb853-484">hello predictor variable is a time series object.</span></span>  

<span data-ttu-id="bb853-485">Один раз `ts.detrend()` определяется мы применить переменные toohello интересуют наши кадр данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-485">Once `ts.detrend()` is defined we apply it toohello variables of interest in our dataframe.</span></span> <span data-ttu-id="bb853-486">Мы должны привести hello полученный список созданных `lapply()` toodata кадр данных с помощью `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="bb853-486">We must coerce hello resulting list created by `lapply()` toodata dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="bb853-487">Из-за защитного аспектов `ts.detrend()`, tooprocess сбой одной из переменных hello не помешает исправить обработку hello другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="bb853-487">Because of defensive aspects of `ts.detrend()`, failure tooprocess one of hello variables will not prevent correct processing of hello others.</span></span>  

<span data-ttu-id="bb853-488">Последняя строка кода Hello создает парные scatterplot.</span><span class="sxs-lookup"><span data-stu-id="bb853-488">hello final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="bb853-489">После выполнения кода hello R hello результаты hello scatterplot показаны на рис.</span><span class="sxs-lookup"><span data-stu-id="bb853-489">After running hello R code, hello results of hello scatterplot are shown in Figure 17.</span></span>

![Попарная точечная диаграмма после вычитания тренда и стандартизации временных рядов][18]

<span data-ttu-id="bb853-491">*Рис. 17. Попарная точечная диаграмма после вычитания тренда и стандартизации временных рядов*</span><span class="sxs-lookup"><span data-stu-id="bb853-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="bb853-492">Вы можете сравнить эти toothose результаты, показанные на рис.</span><span class="sxs-lookup"><span data-stu-id="bb853-492">You can compare these results toothose shown in Figure 16.</span></span> <span data-ttu-id="bb853-493">Удалены тренда hello и hello переменные стандартизованы, мы увидим гораздо меньше структуры в hello связи между этими переменными.</span><span class="sxs-lookup"><span data-stu-id="bb853-493">With hello trend removed and hello variables standardized, we see a lot less structure in hello relationships between these variables.</span></span>

<span data-ttu-id="bb853-494">корреляции hello toocompute кода Hello как объекты R ccf выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="bb853-494">hello code toocompute hello correlations as R ccf objects is as follows.</span></span>

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="bb853-495">Выполнение этого кода создает журнал hello показано на рис.</span><span class="sxs-lookup"><span data-stu-id="bb853-495">Running this code produces hello log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="bb853-496">*Рис. 18. Список ccf объектов из анализа парный корреляции hello.*</span><span class="sxs-lookup"><span data-stu-id="bb853-496">*Figure 18. List of ccf objects from hello pairwise correlation analysis.*</span></span>

<span data-ttu-id="bb853-497">Каждой задержке соответствует значение корреляции.</span><span class="sxs-lookup"><span data-stu-id="bb853-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="bb853-498">Ни один из этих значений корреляции не достаточно большой toobe значительные.</span><span class="sxs-lookup"><span data-stu-id="bb853-498">None of these correlation values is large enough toobe significant.</span></span> <span data-ttu-id="bb853-499">Таким образом, можно заключить, что каждую переменную можно моделировать независимо от других.</span><span class="sxs-lookup"><span data-stu-id="bb853-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="bb853-500">Вывод таблицы данных</span><span class="sxs-lookup"><span data-stu-id="bb853-500">Output a dataframe</span></span>
<span data-ttu-id="bb853-501">Как список объектов R ccf, рассчитанное hello парные корреляции.</span><span class="sxs-lookup"><span data-stu-id="bb853-501">We have computed hello pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="bb853-502">Это представляет немного проблемы как hello порт вывода результирующего набора данных, которая требует кадр данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-502">This presents a bit of a problem as hello Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="bb853-503">Кроме того hello объекта ccf является списком, мы хотим только значения hello в первый элемент hello этого списка hello корреляции в hello различные проблемы.</span><span class="sxs-lookup"><span data-stu-id="bb853-503">Further, hello ccf object is itself a list and we want only hello values in hello first element of this list, hello correlations at hello various lags.</span></span>

<span data-ttu-id="bb853-504">Hello следующую hello запаздывания код извлекает значения из списка hello ccf объектов, которые сами являются списками.</span><span class="sxs-lookup"><span data-stu-id="bb853-504">hello following code extracts hello lag values from hello list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="bb853-505">Первая строка кода Hello немного сложнее и объяснения помогут понять его.</span><span class="sxs-lookup"><span data-stu-id="bb853-505">hello first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="bb853-506">Работа с hello вдоль и поперек у нас есть hello следующее:</span><span class="sxs-lookup"><span data-stu-id="bb853-506">Working from hello inside out we have hello following:</span></span>

1. <span data-ttu-id="bb853-507">Hello "**[[**«оператор с аргументом hello»**1**" выбирает hello вектор корреляции в задержка hello из первого элемента списка объектов ccf hello hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-507">hello '**[[**' operator with hello argument '**1**' selects hello vector of correlations at hello lags from hello first element of hello ccf object list.</span></span>
2. <span data-ttu-id="bb853-508">Hello `do.call()` применяется функций hello `rbind()` функции hello элементы списка hello возвращают, `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="bb853-508">hello `do.call()` function applies hello `rbind()` function over hello elements of hello list returns by `lapply()`.</span></span>
3. <span data-ttu-id="bb853-509">Hello `data.frame()` функция относит hello результата, формируемого `do.call()` tooa кадр данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-509">hello `data.frame()` function coerces hello result produced by `do.call()` tooa dataframe.</span></span>

<span data-ttu-id="bb853-510">Обратите внимание, что строка hello имена в столбце hello кадр данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-510">Note that hello row names are in a column of hello dataframe.</span></span> <span data-ttu-id="bb853-511">Это сохраняет имена строку hello, когда они выводятся из hello [выполнение скрипта R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="bb853-511">Doing so preserves hello row names when they are output from hello [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="bb853-512">Выполнение кода hello вывод hello показано на рисунке 19 когда я **визуализировать** hello выходные данные в hello порт результирующего набора данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-512">Running hello code produces hello output shown in Figure 19 when I **Visualize** hello output at hello Result Dataset port.</span></span> <span data-ttu-id="bb853-513">Hello строк, называются в первом столбце hello, как планировалось.</span><span class="sxs-lookup"><span data-stu-id="bb853-513">hello row names are in hello first column, as intended.</span></span>

![Вывод результатов анализа корреляции hello][20]

<span data-ttu-id="bb853-515">*Рис. 19. Результаты вывода analysis корреляции hello.*</span><span class="sxs-lookup"><span data-stu-id="bb853-515">*Figure 19. Results output from hello correlation analysis.*</span></span>

## <span data-ttu-id="bb853-516"><a id="seasonalforecasting"></a>Пример временных рядов: сезонное прогнозирование</span><span class="sxs-lookup"><span data-stu-id="bb853-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="bb853-517">Наши данные теперь находится в форме, подходящей для анализа и обнаружено, что нет не значительные взаимосвязи между переменными hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between hello variables.</span></span> <span data-ttu-id="bb853-518">Пойдем дальше и создадим прогностическую модель временных рядов.</span><span class="sxs-lookup"><span data-stu-id="bb853-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="bb853-519">С помощью этой модели будет спрогнозировать Калифорния milk производства для hello 12 месяцев 2013.</span><span class="sxs-lookup"><span data-stu-id="bb853-519">Using this model we will forecast California milk production for hello 12 months of 2013.</span></span>

<span data-ttu-id="bb853-520">У нашей прогностической модели будет два компонента: тренд и сезонный компонент.</span><span class="sxs-lookup"><span data-stu-id="bb853-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="bb853-521">Полный прогноз Hello — hello совокупность этих двух компонентов.</span><span class="sxs-lookup"><span data-stu-id="bb853-521">hello complete forecast is hello product of these two components.</span></span> <span data-ttu-id="bb853-522">Модели такого типа называются мультипликативными.</span><span class="sxs-lookup"><span data-stu-id="bb853-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="bb853-523">альтернативой Hello представляет собой аддитивный модель.</span><span class="sxs-lookup"><span data-stu-id="bb853-523">hello alternative is an additive model.</span></span> <span data-ttu-id="bb853-524">Мы уже применены переменных toohello преобразования журнала интерес, что делает этот анализ работы со.</span><span class="sxs-lookup"><span data-stu-id="bb853-524">We have already applied a log transformation toohello variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="bb853-525">Hello полный код R для этого раздела находится в hello ZIP-файл, загруженный ранее.</span><span class="sxs-lookup"><span data-stu-id="bb853-525">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="creating-hello-dataframe-for-analysis"></a><span data-ttu-id="bb853-526">Создание hello кадр данных для анализа</span><span class="sxs-lookup"><span data-stu-id="bb853-526">Creating hello dataframe for analysis</span></span>
<span data-ttu-id="bb853-527">Начните с добавления **новый** [выполнение скрипта R] [ execute-r-script] модуль tooyour эксперимента.</span><span class="sxs-lookup"><span data-stu-id="bb853-527">Start by adding a **new** [Execute R Script][execute-r-script] module tooyour experiment.</span></span> <span data-ttu-id="bb853-528">Подключение hello **результирующего набора данных** вывода hello существующих [выполнение скрипта R] [ execute-r-script] toohello модуль **Dataset1** ввода нового модуля hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-528">Connect hello **Result Dataset** output of hello existing [Execute R Script][execute-r-script] module toohello **Dataset1** input of hello new module.</span></span> <span data-ttu-id="bb853-529">Hello результат должен выглядеть примерно как на рис.</span><span class="sxs-lookup"><span data-stu-id="bb853-529">hello result should look something like Figure 20.</span></span>

![Hello поэкспериментировать с hello добавлен новый модуль выполнение скрипта R][21]

<span data-ttu-id="bb853-531">*Рис. 20. Hello поэкспериментировать с hello добавлен новый модуль выполнение R-сценария.*</span><span class="sxs-lookup"><span data-stu-id="bb853-531">*Figure 20. hello experiment with hello new Execute R Script module added.*</span></span>

<span data-ttu-id="bb853-532">Как и для анализа hello корреляции, который мы только что выполнили, мы нужен tooadd столбца с объектом ряда времени POSIXct.</span><span class="sxs-lookup"><span data-stu-id="bb853-532">As with hello correlation analysis we just completed, we need tooadd a column with a POSIXct time series object.</span></span> <span data-ttu-id="bb853-533">просто это необходимо сделать после кода Hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-533">hello following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="bb853-534">Запустите этот код и просмотрите журнал hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-534">Run this code and look at hello log.</span></span> <span data-ttu-id="bb853-535">Рисунок 21 вид Hello результата.</span><span class="sxs-lookup"><span data-stu-id="bb853-535">hello result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="bb853-536">*Рис. 21. Сводка hello кадр данных.*</span><span class="sxs-lookup"><span data-stu-id="bb853-536">*Figure 21. A summary of hello dataframe.*</span></span>

<span data-ttu-id="bb853-537">С данным результатом Приносим toostart готовности в ходе анализа.</span><span class="sxs-lookup"><span data-stu-id="bb853-537">With this result, we are ready toostart our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="bb853-538">Создание набора данных для обучения</span><span class="sxs-lookup"><span data-stu-id="bb853-538">Create a training dataset</span></span>
<span data-ttu-id="bb853-539">Созданный кадр данных hello мы должны toocreate обучающий набор данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-539">With hello dataframe constructed we need toocreate a training dataset.</span></span> <span data-ttu-id="bb853-540">Эти данные будут включены все hello наблюдения за исключением hello последние 12 hello года 2013, являющееся нашей проверочном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-540">This data will include all of hello observations except hello last 12, of hello year 2013, which is our test dataset.</span></span> <span data-ttu-id="bb853-541">Hello ниже программный код кадр данных подмножеств hello и создает графики hello молока производства и цена переменных.</span><span class="sxs-lookup"><span data-stu-id="bb853-541">hello following code subsets hello dataframe and creates plots of hello dairy production and price variables.</span></span> <span data-ttu-id="bb853-542">Затем создать точечное hello четыре переменных производства и ценой.</span><span class="sxs-lookup"><span data-stu-id="bb853-542">I then create plots of hello four production and price variables.</span></span> <span data-ttu-id="bb853-543">Анонимная функция имеет некоторые делается дополнение для построения используется toodefine и затем выполните итерацию через список hello hello двух других аргументов с `Map()`.</span><span class="sxs-lookup"><span data-stu-id="bb853-543">An anonymous function is used toodefine some augments for plot, and then iterate over hello list of hello other two arguments with `Map()`.</span></span> <span data-ttu-id="bb853-544">Если вам кажется, что здесь пригодилась бы структура for ... loop, вы совершенно правы.</span><span class="sxs-lookup"><span data-stu-id="bb853-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="bb853-545">Но поскольку язык R оперирует функциями, я продемонстрирую решение с использованием функций.</span><span class="sxs-lookup"><span data-stu-id="bb853-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="bb853-546">В результате выполнения кода hello возникает ряд временных рядов диаграммы из выходных данных устройство R hello, показаны на рисунке 22 hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-546">Running hello code produces hello series of time series plots from hello R Device output shown in Figure 22.</span></span> <span data-ttu-id="bb853-547">Обратите внимание, что этой оси времени hello измеряется в даты, приятным преимуществом hello время метод построения ряда.</span><span class="sxs-lookup"><span data-stu-id="bb853-547">Note that hello time axis is in units of dates, a nice benefit of hello time series plot method.</span></span>

![Первая диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Вторая диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Третья диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Четвертая диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="bb853-552">*Рис. 22. Диаграммы временных рядов данных по ценам и производству молочных продуктов в Калифорнии*</span><span class="sxs-lookup"><span data-stu-id="bb853-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="bb853-553">Модель тренда</span><span class="sxs-lookup"><span data-stu-id="bb853-553">A trend model</span></span>
<span data-ttu-id="bb853-554">После создания объект ряда времени и только что рассмотрели данных hello, начнем tooconstruct модель тренда для hello Калифорния milk производственных данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-554">Having created a time series object and having had a look at hello data, let's start tooconstruct a trend model for hello California milk production data.</span></span> <span data-ttu-id="bb853-555">Для этого можно использовать регрессию временного ряда.</span><span class="sxs-lookup"><span data-stu-id="bb853-555">We can do this with a time series regression.</span></span> <span data-ttu-id="bb853-556">Тем не менее это видно из диаграммы hello, мы должны более Наклон и пересечение tooaccurately моделировать hello наблюдается тенденция в hello обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-556">However, it is clear from hello plot that we will need more than a slope and intercept tooaccurately model hello observed trend in hello training data.</span></span>

<span data-ttu-id="bb853-557">Имея hello малого масштаба данных hello, я будет построена модель hello для тренда в RStudio и затем вырезать и вставить результирующую модель hello в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-557">Given hello small scale of hello data, I will build hello model for trend in RStudio and then cut and paste hello resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="bb853-558">RStudio предоставляет интерактивную среду для такого рода интерактивного анализа.</span><span class="sxs-lookup"><span data-stu-id="bb853-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="bb853-559">В качестве первой попытки попытается полиномиальная Регрессия с питание too3.</span><span class="sxs-lookup"><span data-stu-id="bb853-559">As a first attempt, I will try a polynomial regression with powers up too3.</span></span> <span data-ttu-id="bb853-560">При создании таких моделей существует высокая вероятность образования лжевзаимосвязей.</span><span class="sxs-lookup"><span data-stu-id="bb853-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="bb853-561">Таким образом это наиболее условия tooavoid высокого порядка.</span><span class="sxs-lookup"><span data-stu-id="bb853-561">Therefore, it is best tooavoid high order terms.</span></span> <span data-ttu-id="bb853-562">Hello `I()` функция подавляет интерпретацию содержимое hello (интерпретирует содержимое hello «как есть») и позволяет toowrite буквально интерпретируемых функции в формуле регрессии.</span><span class="sxs-lookup"><span data-stu-id="bb853-562">hello `I()` function inhibits interpretation of hello contents (interprets hello contents 'as is') and allows you toowrite a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="bb853-563">Этот код создает следующие hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-563">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="bb853-564">На основе значений P (Pr (> | t |)) в этих выходных данных видно, что hello квадрат термин может быть незначительной.</span><span class="sxs-lookup"><span data-stu-id="bb853-564">From P values (Pr(>|t|)) in this output, we can see that hello squared term may not be significant.</span></span> <span data-ttu-id="bb853-565">Я использую hello `update()` функции toomodify этой модели, удаление hello квадрат термин.</span><span class="sxs-lookup"><span data-stu-id="bb853-565">I will use hello `update()` function toomodify this model by dropping hello squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="bb853-566">Этот код создает следующие hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-566">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="bb853-567">Теперь значительно лучше.</span><span class="sxs-lookup"><span data-stu-id="bb853-567">This looks better.</span></span> <span data-ttu-id="bb853-568">Значимыми являются все слова hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-568">All of hello terms are significant.</span></span> <span data-ttu-id="bb853-569">Тем не менее значение 2e 16 hello это значение по умолчанию и не следует принимать слишком серьезно.</span><span class="sxs-lookup"><span data-stu-id="bb853-569">However, hello 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="bb853-570">Для проверки работоспособности сделаем график ряда времени hello Калифорния подсчет рабочих данных показано кривой тренда hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-570">As a sanity test, let's make a time series plot of hello California dairy production data with hello trend curve shown.</span></span> <span data-ttu-id="bb853-571">Я добавил hello, следующий код в hello машинного обучения Azure [выполнение скрипта R] [ execute-r-script] toocreate модели (не RStudio) hello модели и сделать построение.</span><span class="sxs-lookup"><span data-stu-id="bb853-571">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) toocreate hello model and make a plot.</span></span> <span data-ttu-id="bb853-572">Hello результат показан на рисунке 23.</span><span class="sxs-lookup"><span data-stu-id="bb853-572">hello result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Данные молочного производства Калифорнии с моделью тренда](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="bb853-574">*Рис. 23. Данные молочного производства Калифорнии с моделью тренда*</span><span class="sxs-lookup"><span data-stu-id="bb853-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="bb853-575">Похоже, hello тренда модель соответствует данным hello довольно хорошо.</span><span class="sxs-lookup"><span data-stu-id="bb853-575">It looks like hello trend model fits hello data fairly well.</span></span> <span data-ttu-id="bb853-576">Кроме того существует не toobe свидетельство чрезмерное Подгонка, такие как нечетными wiggles кривой hello модели.</span><span class="sxs-lookup"><span data-stu-id="bb853-576">Further, there does not seem toobe evidence of over-fitting, such as odd wiggles in hello model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="bb853-577">Сезонная модель</span><span class="sxs-lookup"><span data-stu-id="bb853-577">Seasonal model</span></span>
<span data-ttu-id="bb853-578">С моделью тренда в наличии нам нужна toopush на и включать сезонных эффектов hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-578">With a trend model in hand, we need toopush on and include hello seasonal effects.</span></span> <span data-ttu-id="bb853-579">Мы будем использовать hello месяц года hello как фиктивный действующему hello Линейная модель toocapture hello по месяцам.</span><span class="sxs-lookup"><span data-stu-id="bb853-579">We will use hello month of hello year as a dummy variable in hello linear model toocapture hello month-by-month effect.</span></span> <span data-ttu-id="bb853-580">Обратите внимание, что при вводе коэффициент переменных в модель отсекаемый отрезок hello не вычисляемые.</span><span class="sxs-lookup"><span data-stu-id="bb853-580">Note that when you introduce factor variables into a model, hello intercept must not be computed.</span></span> <span data-ttu-id="bb853-581">Если этого не сделать, формула hello чрезмерно указанным, а также приведет к удалению R один hello требуемого факторов, но сохранить hello свободный член.</span><span class="sxs-lookup"><span data-stu-id="bb853-581">If you do not do this, hello formula is over-specified and R will drop one of hello desired factors but keep hello intercept term.</span></span>

<span data-ttu-id="bb853-582">Поскольку у нас есть удовлетворительные тренда модели можно использовать hello `update()` функция tooadd hello новые термины toohello существующей модели.</span><span class="sxs-lookup"><span data-stu-id="bb853-582">Since we have a satisfactory trend model we can use hello `update()` function tooadd hello new terms toohello existing model.</span></span> <span data-ttu-id="bb853-583">Hello -1 в формуле hello обновления удаляет hello свободный член.</span><span class="sxs-lookup"><span data-stu-id="bb853-583">hello -1 in hello update formula drops hello intercept term.</span></span> <span data-ttu-id="bb853-584">До момента hello в RStudio:</span><span class="sxs-lookup"><span data-stu-id="bb853-584">Continuing in RStudio for hello moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="bb853-585">Этот код создает следующие hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-585">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="bb853-586">Мы видим, эту модель hello больше не имеет свободный член и имеет 12 факторов значительные месяца.</span><span class="sxs-lookup"><span data-stu-id="bb853-586">We see that hello model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="bb853-587">Это именно то, чего мы старались toosee.</span><span class="sxs-lookup"><span data-stu-id="bb853-587">This is exactly what we wanted toosee.</span></span>

<span data-ttu-id="bb853-588">Создадим другой рисунка ряда времени hello Калифорния молока производственных данных toosee того, насколько хорошо работает hello сезонных модели.</span><span class="sxs-lookup"><span data-stu-id="bb853-588">Let's make another time series plot of hello California dairy production data toosee how well hello seasonal model is working.</span></span> <span data-ttu-id="bb853-589">Я добавил hello, следующий код в hello машинного обучения Azure [выполнение скрипта R] [ execute-r-script] toocreate hello модели и сделать построение.</span><span class="sxs-lookup"><span data-stu-id="bb853-589">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] toocreate hello model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="bb853-590">Этот код запускается в машинном обучении Azure создает построения hello показано на рис.</span><span class="sxs-lookup"><span data-stu-id="bb853-590">Running this code in Azure Machine Learning produces hello plot shown in Figure 24.</span></span>

![Данные молочного производства Калифорнии с моделью, включающей сезонные составляющие](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="bb853-592">*Рис. 24. Данные молочного производства Калифорнии с моделью, включающей сезонные составляющие*</span><span class="sxs-lookup"><span data-stu-id="bb853-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="bb853-593">Hello соответствия toohello данных показано на рис. 24 вместо поощряя.</span><span class="sxs-lookup"><span data-stu-id="bb853-593">hello fit toohello data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="bb853-594">Тренд hello и влияние сезонных hello (ежемесячно вариант) найдите разумного.</span><span class="sxs-lookup"><span data-stu-id="bb853-594">Both hello trend and hello seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="bb853-595">Как проверку еще раз на нашей модели давайте взглянем на остатков hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-595">As another check on our model, let's have a look at hello residuals.</span></span> <span data-ttu-id="bb853-596">Hello следующее выражение вычисляет код hello прогнозируемые значения из наших двух моделей, вычисляет hello остатки для hello сезонных модели, а затем отображает эти остатки для hello обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-596">hello following code computes hello predicted values from our two models, computes hello residuals for hello seasonal model, and then plots these residuals for hello training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="bb853-597">Hello остаточные рисунка показана на рис. 25.</span><span class="sxs-lookup"><span data-stu-id="bb853-597">hello residual plot is shown in Figure 25.</span></span>

![Остатки hello сезонных модели для hello обучающих данных](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="bb853-599">*Рис. 25. Остатки hello сезонных модель для hello обучающих данных.*</span><span class="sxs-lookup"><span data-stu-id="bb853-599">*Figure 25. Residuals of hello seasonal model for hello training data.*</span></span>

<span data-ttu-id="bb853-600">Выглядит вполне логично.</span><span class="sxs-lookup"><span data-stu-id="bb853-600">These residuals look reasonable.</span></span> <span data-ttu-id="bb853-601">Нет нет определенной структуры, за исключением hello эффект recession hello 2008-2009 г., который не учитывает нашей модели особенно хорошо.</span><span class="sxs-lookup"><span data-stu-id="bb853-601">There is no particular structure, except hello effect of hello 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="bb853-602">показано на рис. 25 построения Hello полезно для определения шаблоны, зависящие от времени в остатков hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-602">hello plot shown in Figure 25 is useful for detecting any time-dependent patterns in hello residuals.</span></span> <span data-ttu-id="bb853-603">явный подход Hello вычисление и отображение остатков hello, я использовал помещает остатков hello в порядке времени на диаграмме hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-603">hello explicit approach of computing and plotting hello residuals I used places hello residuals in time order on hello plot.</span></span> <span data-ttu-id="bb853-604">Если на hello другой стороны, я графически в `milk.lm$residuals`, построения hello не было бы в порядке времени.</span><span class="sxs-lookup"><span data-stu-id="bb853-604">If, on hello other hand, I had plotted `milk.lm$residuals`, hello plot would not have been in time order.</span></span>

<span data-ttu-id="bb853-605">Можно также использовать `plot.lm()` tooproduce ряд диагностики графики.</span><span class="sxs-lookup"><span data-stu-id="bb853-605">You can also use `plot.lm()` tooproduce a series of diagnostic plots.</span></span>

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="bb853-606">Пример ряда диагностических диаграмм, созданных с помощью этого кода, приведен на рис. 26.</span><span class="sxs-lookup"><span data-stu-id="bb853-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Первый из диагностики графики для hello сезонных модели](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Второе из диагностики графики для hello сезонных модели](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Третья из диагностики графики для hello сезонных модели](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Четвертая из диагностики графики для hello сезонных модели](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="bb853-611">*Рис. 26. Диагностика которых служат для hello сезонных модели.*</span><span class="sxs-lookup"><span data-stu-id="bb853-611">*Figure 26. Diagnostic plots for hello seasonal model.*</span></span>

<span data-ttu-id="bb853-612">Существует несколько высокой влиятельные точек, указанных в этих графики, но ничего не toocause большую важность.</span><span class="sxs-lookup"><span data-stu-id="bb853-612">There are a few highly influential points identified in these plots, but nothing toocause great concern.</span></span> <span data-ttu-id="bb853-613">Кроме того мы видим из построения обычный Q-Q hello, остатков hello закрыть распределенных, toonormally допущение важные для линейной модели.</span><span class="sxs-lookup"><span data-stu-id="bb853-613">Further, we can see from hello Normal Q-Q plot that hello residuals are close toonormally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="bb853-614">Прогнозирование и оценка моделей</span><span class="sxs-lookup"><span data-stu-id="bb853-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="bb853-615">Имеется только один дополнительные toocomplete toodo самое нашего примера.</span><span class="sxs-lookup"><span data-stu-id="bb853-615">There is just one more thing toodo toocomplete our example.</span></span> <span data-ttu-id="bb853-616">Нам нужна toocompute прогнозов и сравнивать hello ошибки с hello фактические данные.</span><span class="sxs-lookup"><span data-stu-id="bb853-616">We need toocompute forecasts and measure hello error against hello actual data.</span></span> <span data-ttu-id="bb853-617">Наш прогноз будет для hello 12 месяцев 2013.</span><span class="sxs-lookup"><span data-stu-id="bb853-617">Our forecast will be for hello 12 months of 2013.</span></span> <span data-ttu-id="bb853-618">Мы можно вычислить меру ошибки для этого прогноза toohello фактические данные, не является частью нашей обучающий набор данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-618">We can compute an error measure for this forecast toohello actual data that is not part of our training dataset.</span></span> <span data-ttu-id="bb853-619">Кроме того мы можно сравнить производительность на hello 18 лет обучающих данных toohello 12 месяцев тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-619">Additionally, we can compare performance on hello 18 years of training data toohello 12 months of test data.</span></span>  

<span data-ttu-id="bb853-620">Используется несколько метрик производительности hello toomeasure модели временных рядов.</span><span class="sxs-lookup"><span data-stu-id="bb853-620">A number of metrics are used toomeasure hello performance of time series models.</span></span> <span data-ttu-id="bb853-621">В нашем случае мы будем использовать ошибка hello среднеквадратическое (RMS).</span><span class="sxs-lookup"><span data-stu-id="bb853-621">In our case we will use hello root mean square (RMS) error.</span></span> <span data-ttu-id="bb853-622">Hello следующая функция вычисляет погрешность hello RMS между два ряда.</span><span class="sxs-lookup"><span data-stu-id="bb853-622">hello following function computes hello RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="bb853-623">Как и в hello `log.transform()` функция обсуждалось Здравствуйте, «Value преобразования» раздела, много ошибок проверки и исключение код восстановления в этой функции.</span><span class="sxs-lookup"><span data-stu-id="bb853-623">As with hello `log.transform()` function we discussed in hello "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="bb853-624">принципы Hello, применяемых являются hello же.</span><span class="sxs-lookup"><span data-stu-id="bb853-624">hello principles employed are hello same.</span></span> <span data-ttu-id="bb853-625">Hello работа выполняется в двух местах в оболочку `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="bb853-625">hello work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="bb853-626">Во-первых hello временных рядов, exponentiated, так как мы работаем с журналами hello hello значений.</span><span class="sxs-lookup"><span data-stu-id="bb853-626">First, hello time series are exponentiated, since we have been working with hello logs of hello values.</span></span> <span data-ttu-id="bb853-627">Во-вторых обнаруженная ошибка RMS hello является вычисляемым.</span><span class="sxs-lookup"><span data-stu-id="bb853-627">Second, hello actual RMS error is computed.</span></span>  

<span data-ttu-id="bb853-628">Давайте оснащенном hello toomeasure функция ошибки RMS, построения и выходных кадр данных, содержащая ошибки hello RMS.</span><span class="sxs-lookup"><span data-stu-id="bb853-628">Equipped with a function toomeasure hello RMS error, let's build and output a dataframe containing hello RMS errors.</span></span> <span data-ttu-id="bb853-629">Мы будет включать термины hello тренда предназначенный только для модели и hello полную модель с сезонных факторов.</span><span class="sxs-lookup"><span data-stu-id="bb853-629">We will include terms for hello trend model alone and hello complete model with seasonal factors.</span></span> <span data-ttu-id="bb853-630">Hello следующий код hello задания с помощью двух hello линейной модели, мы создания.</span><span class="sxs-lookup"><span data-stu-id="bb853-630">hello following code does hello job by using hello two linear models we have constructed.</span></span>

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="bb853-631">Выполнение этого кода выводятся данные hello, показанный на рисунке 27 в hello порт вывода результирующего набора данных.</span><span class="sxs-lookup"><span data-stu-id="bb853-631">Running this code produces hello output shown in Figure 27 at hello Result Dataset output port.</span></span>

![Сравнение ошибок RMS для моделей hello][26]

<span data-ttu-id="bb853-633">*Рис. 27. Сравнение ошибок RMS для моделей hello.*</span><span class="sxs-lookup"><span data-stu-id="bb853-633">*Figure 27. Comparison of RMS errors for hello models.*</span></span>

<span data-ttu-id="bb853-634">Эти результаты мы увидим, что добавление toohello сезонных факторов hello модель сокращает ошибки RMS hello значительно.</span><span class="sxs-lookup"><span data-stu-id="bb853-634">From these results, we see that adding hello seasonal factors toohello model reduces hello RMS error significantly.</span></span> <span data-ttu-id="bb853-635">Не слишком удивительно, но ошибка hello RMS для обучающих данных hello немного меньше hello прогноза.</span><span class="sxs-lookup"><span data-stu-id="bb853-635">Not too surprisingly, hello RMS error for hello training data is a bit less than for hello forecast.</span></span>

## <span data-ttu-id="bb853-636"><a id="appendixa"></a>ПРИЛОЖЕНИИ a. Руководство по tooRStudio</span><span class="sxs-lookup"><span data-stu-id="bb853-636"><a id="appendixa"></a>APPENDIX A: Guide tooRStudio</span></span>
<span data-ttu-id="bb853-637">RStudio хорошо задокументированы, поэтому в этом приложении я предоставлю некоторые ссылки toohello ключевые разделы документации tooget hello RStudio, которого вы начали.</span><span class="sxs-lookup"><span data-stu-id="bb853-637">RStudio is quite well documented, so in this appendix I will provide some links toohello key sections of hello RStudio documentation tooget you started.</span></span>

1. <span data-ttu-id="bb853-638">Создание проектов</span><span class="sxs-lookup"><span data-stu-id="bb853-638">Creating projects</span></span>
   
   <span data-ttu-id="bb853-639">С помощью RStudio можно организовывать свой код на R в проекты и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="bb853-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="bb853-640">Hello документацию, которая использует проектов можно найти на https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="bb853-640">hello documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="bb853-641">Я рекомендую, выполните следующую инструкцию и создать проект для примеров кода hello R в этом документе.</span><span class="sxs-lookup"><span data-stu-id="bb853-641">I recommend that you follow these directions and create a project for hello R code examples in this document.</span></span>  
2. <span data-ttu-id="bb853-642">Изменение и выполнение кода на R</span><span class="sxs-lookup"><span data-stu-id="bb853-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="bb853-643">RStudio предоставляет интегрированную среду для изменения и выполнения кода на R.</span><span class="sxs-lookup"><span data-stu-id="bb853-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="bb853-644">Документацию можно найти по адресу https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="bb853-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="bb853-645">Отладка</span><span class="sxs-lookup"><span data-stu-id="bb853-645">Debugging</span></span>
   
   <span data-ttu-id="bb853-646">RStudio располагает эффективными возможностями отладки.</span><span class="sxs-lookup"><span data-stu-id="bb853-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="bb853-647">Документацию по этим функциям можно найти по адресу https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="bb853-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="bb853-648">функции устранения неполадок Hello точки останова, задокументированы в https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="bb853-648">hello breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="bb853-649"><a id="appendixb"></a>ПРИЛОЖЕНИЕ Б. Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="bb853-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="bb853-650">Это программирования учебника описаны основы hello R действий требуется toouse hello язык R с студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="bb853-650">This R programming tutorial covers hello basics of what you need toouse hello R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="bb853-651">Если вы еще не знакомы с языком R, на ресурсе CRAN можно найти два вводных курса:</span><span class="sxs-lookup"><span data-stu-id="bb853-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="bb853-652">R для начинающих по Emmanuel Paradis это хорошая toostart на http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="bb853-652">R for Beginners by Emmanuel Paradis is a good place toostart at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="bb853-653">Введение tooR по N. Вт.</span><span class="sxs-lookup"><span data-stu-id="bb853-653">An Introduction tooR by W. N.</span></span> <span data-ttu-id="bb853-654">Венаблес (W. N. Venables)</span><span class="sxs-lookup"><span data-stu-id="bb853-654">Venables et.</span></span> <span data-ttu-id="bb853-655">и др. —</span><span class="sxs-lookup"><span data-stu-id="bb853-655">al.</span></span> <span data-ttu-id="bb853-656">немного более углубленный курс, доступный по адресу http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="bb853-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="bb853-657">По языку R написано много книг, которые могут помочь в его освоении.</span><span class="sxs-lookup"><span data-stu-id="bb853-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="bb853-658">Вот некоторые из них, которые показались мне наиболее полезными:</span><span class="sxs-lookup"><span data-stu-id="bb853-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="bb853-659">Hello Art R программирования: Обзор из статистического программного обеспечения по Norman Matloff является tooprogramming отличным введением в R.</span><span class="sxs-lookup"><span data-stu-id="bb853-659">hello Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction tooprogramming in R.</span></span>  
* <span data-ttu-id="bb853-660">Рецепты R, Пол Teetor предоставляет и решение подход toousing R.</span><span class="sxs-lookup"><span data-stu-id="bb853-660">R Cookbook by Paul Teetor provides a problem and solution approach toousing R.</span></span>  
* <span data-ttu-id="bb853-661">«R в действии» Роберта Кабакова (Robert Kabacoff) — еще одна полезная книга.</span><span class="sxs-lookup"><span data-stu-id="bb853-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="bb853-662">веб-сайт быстрого R дополнительное Hello — полезным ресурсом на http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="bb853-662">hello companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="bb853-663">Является доступны бесплатно на http://www.burns-stat.com/documents/books/the-r-inferno/ Inferno R, Патрик Бернс удивительно пришлите книги, которое отвечает за ряд сложных и трудно разделы, которые могут быть обнаружены при программировании в книге R. hello.</span><span class="sxs-lookup"><span data-stu-id="bb853-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. hello book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="bb853-664">Если требуется глубокое погружение в дополнительные разделы в R, взглянем на книги hello Дополнительно R, Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="bb853-664">If you want a deep dive into advanced topics in R, have a look at hello book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="bb853-665">Hello Интернет-версию эта книга доступна бесплатно в http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="bb853-665">hello online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="bb853-666">Каталог пакетов ряда времени R можно найти в hello CRAN представление задач для анализа временных рядов: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="bb853-666">A catalogue of R time series packages can be found in hello CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="bb853-667">Сведения о пакеты объектов ряда определенное время должен указывать toohello документации для этого пакета.</span><span class="sxs-lookup"><span data-stu-id="bb853-667">For information on specific time series object packages, you should refer toohello documentation for that package.</span></span>

<span data-ttu-id="bb853-668">Книга Hello вводные временных рядов с помощью R, Пол Cowpertwait и Эндрю Metcalfe предоставляет введение toousing R для анализа временных рядов.</span><span class="sxs-lookup"><span data-stu-id="bb853-668">hello book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction toousing R for time series analysis.</span></span> <span data-ttu-id="bb853-669">Множество других теоретических работ содержат примеры на языке R.</span><span class="sxs-lookup"><span data-stu-id="bb853-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="bb853-670">Некоторые полезные ресурсы в Интернете:</span><span class="sxs-lookup"><span data-stu-id="bb853-670">Some great internet resources:</span></span>

* <span data-ttu-id="bb853-671">DataCamp: DataCamp учебные R в удобства hello браузера с видео занятия и кодирования упражнений.</span><span class="sxs-lookup"><span data-stu-id="bb853-671">DataCamp: DataCamp teaches R in hello comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="bb853-672">Нет интерактивной учебники по hello последнюю методы R и пакеты.</span><span class="sxs-lookup"><span data-stu-id="bb853-672">There are interactive tutorials on hello latest R techniques and packages.</span></span> <span data-ttu-id="bb853-673">Время https://www.datacamp.com/courses/introduction-to-r выполнить hello свободного интерактивный учебник по языку R</span><span class="sxs-lookup"><span data-stu-id="bb853-673">Take hello free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="bb853-674">Руководство по началу работы с R из Programiz: https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="bb853-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="bb853-675">Краткое руководство по R от Келли Блэк (Kelly Black) из университета Кларксон по адресу http://www.cyclismo.org/tutorial/R/.</span><span class="sxs-lookup"><span data-stu-id="bb853-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="bb853-676">Ссылки на более чем 60 ресурсов по R: http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html.</span><span class="sxs-lookup"><span data-stu-id="bb853-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
