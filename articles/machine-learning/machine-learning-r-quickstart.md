---
title: "Краткое руководство по языку программирования R для службы машинного обучения | Документация Майкрософт"
description: "Это руководство по языку программирования R поможет быстро создать прогностическое решение, используя язык R в Студии машинного обучения Azure."
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
ms.openlocfilehash: 598f5ce445e520b6cdc347c80f7f3dcbc9c2c9e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="quickstart-tutorial-for-the-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="14529-104">Краткое руководство по языку программирования R для службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="14529-104">Quickstart tutorial for the R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="14529-105">Введение</span><span class="sxs-lookup"><span data-stu-id="14529-105">Introduction</span></span>
<span data-ttu-id="14529-106">Этот учебник поможет быстро расширить возможности службы машинного обучения Azure с помощью языка программирования R.</span><span class="sxs-lookup"><span data-stu-id="14529-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using the R programming language.</span></span> <span data-ttu-id="14529-107">Выполнив приведенные в этом учебнике инструкции, вы научитесь создавать, тестировать и выполнять код R в службе машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-107">Follow this R programming tutorial to create, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="14529-108">Во время работы с руководством вы создадите полноценное прогностическое решение, используя язык R в службе машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-108">As you work through tutorial, you will create a complete forecasting solution by using the R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="14529-109">Машинное обучение Microsoft Azure содержит множество эффективных модулей машинного обучения и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="14529-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="14529-110">Высокоэффективный язык R считается универсальным языком аналитики.</span><span class="sxs-lookup"><span data-stu-id="14529-110">The powerful R language has been described as the lingua franca of analytics.</span></span> <span data-ttu-id="14529-111">К счастью, возможности аналитики и обработки данных, которыми располагает Машинное обучение Azure, можно расширить благодаря использованию языка R. Это сочетание позволяет объединить масштабируемость при развертывании Машинного обучения Azure с гибкостью и глубиной аналитики языка R.</span><span class="sxs-lookup"><span data-stu-id="14529-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides the scalability and ease of deployment of Azure Machine Learning with the flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-the-dataset"></a><span data-ttu-id="14529-112">Прогнозирование и набор данных</span><span class="sxs-lookup"><span data-stu-id="14529-112">Forecasting and the dataset</span></span>
<span data-ttu-id="14529-113">Прогнозирование — широко распространенный и чрезвычайно полезный метод аналитики.</span><span class="sxs-lookup"><span data-stu-id="14529-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="14529-114">Сфера его применения охватывает широкий диапазон: от прогноза объема продаж сезонных товаров, определяющего уровень заполнения склада, до расчета макроэкономических переменных.</span><span class="sxs-lookup"><span data-stu-id="14529-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, to predicting macroeconomic variables.</span></span> <span data-ttu-id="14529-115">Преимущественно при прогнозировании используются модели временных рядов.</span><span class="sxs-lookup"><span data-stu-id="14529-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="14529-116">Данные временных рядов — данные, значения которых имеют индекс времени.</span><span class="sxs-lookup"><span data-stu-id="14529-116">Time series data is data in which the values have a time index.</span></span> <span data-ttu-id="14529-117">Значение индекса времени может быть регулярным (например, помесячным или поминутным), или нерегулярным.</span><span class="sxs-lookup"><span data-stu-id="14529-117">The time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="14529-118">Модель временных рядов основана на данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="14529-118">A time series model is based on time series data.</span></span> <span data-ttu-id="14529-119">Язык программирования R располагает гибкой структурой и широкими аналитическими возможностями для временных данных.</span><span class="sxs-lookup"><span data-stu-id="14529-119">The R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="14529-120">В этом руководстве мы будем использовать данные о производстве молочных продуктов в Калифорнии и ценах на них.</span><span class="sxs-lookup"><span data-stu-id="14529-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="14529-121">Эти данные включают в себя информацию о производстве нескольких молочных продуктов и цену молочного жира — эталонного товара за каждый месяц.</span><span class="sxs-lookup"><span data-stu-id="14529-121">This data includes monthly information on the production of several dairy products and the price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="14529-122">Данные, использующиеся в этой статье, а также сценарии на языке R можно [скачать здесь][download].</span><span class="sxs-lookup"><span data-stu-id="14529-122">The data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="14529-123">Эти данные основаны на информации, собранной университетом Висконсина и доступной по адресу http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="14529-123">This data was originally synthesized from information available from the University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="14529-124">План</span><span class="sxs-lookup"><span data-stu-id="14529-124">Organization</span></span>
<span data-ttu-id="14529-125">Вам потребуется несколько шагов, чтобы научиться создавать, тестировать и выполнять код на R для анализа и обработки данных в среде Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-125">We will progress through several steps as you learn how to create, test and execute analytics and data manipulation R code in the Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="14529-126">Сначала мы изучим основы использования языка R в Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-126">First we will explore the basics of using the R language in the Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="14529-127">Затем рассмотрим различные аспекты ввода и вывода данных, кода на R и графики в среде Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-127">Then we progress to discussing various aspects of I/O for data, R code and graphics in the Azure Machine Learning environment.</span></span>
* <span data-ttu-id="14529-128">После этого мы построим первую часть прогнозного решения, создав код для очистки и преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="14529-128">We will then construct the first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="14529-129">Подготовив данные, мы проанализируем корреляцию нескольких переменных нашего набора данных.</span><span class="sxs-lookup"><span data-stu-id="14529-129">With our data prepared we will perform an analysis of the correlations between several of the variables in our dataset.</span></span>
* <span data-ttu-id="14529-130">Наконец, мы создадим прогнозную модель сезонного временного ряда для молочного производства.</span><span class="sxs-lookup"><span data-stu-id="14529-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="14529-131"><a id="mlstudio"></a>Работа с языком R в Студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="14529-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="14529-132">В этом разделе вы ознакомитесь с основами работы с языком программирования R в Студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="14529-132">This section takes you through some basics of interacting with the R programming language in the Machine Learning Studio environment.</span></span> <span data-ttu-id="14529-133">Язык R — мощный инструмент для создания настраиваемых модулей анализа и обработки данных в среде Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-133">The R language provides a powerful tool to create customized analytics and data manipulation modules within the Azure Machine Learning environment.</span></span>

<span data-ttu-id="14529-134">Для разработки, тестирования и отладки небольших фрагментов кода на языке R мы будем использовать RStudio.</span><span class="sxs-lookup"><span data-stu-id="14529-134">I will use RStudio to develop, test and debug R code on a small scale.</span></span> <span data-ttu-id="14529-135">Впоследствии мы вставим эти готовые фрагменты в модуль [Выполнить сценарий R][execute-r-script] в Студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="14529-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready to run.</span></span>  

### <a name="the-execute-r-script-module"></a><span data-ttu-id="14529-136">Модуль «Выполнение сценария R»</span><span class="sxs-lookup"><span data-stu-id="14529-136">The Execute R Script module</span></span>
<span data-ttu-id="14529-137">В Студии машинного обучения сценарии на языке R выполняются в модуле [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-137">Within Machine Learning Studio, R scripts are run within the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="14529-138">Пример модуля [Выполнить сценарий R][execute-r-script] в Студии машинного обучения показан на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="14529-138">An example of the [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![Язык программирования R: в Студии машинного обучения выбран модуль «Выполнение сценария R»][1]

<span data-ttu-id="14529-140">*Рис. 1. Среда Студии машинного обучения с выбранным модулем «Выполнение сценария R»*</span><span class="sxs-lookup"><span data-stu-id="14529-140">*Figure 1. The Machine Learning Studio environment showing the Execute R Script module selected.*</span></span>

<span data-ttu-id="14529-141">Используя рис. 1, рассмотрим основные элементы среды Студии машинного обучения для работы с модулем [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-141">Referring to Figure 1, let's look at some of the key parts of the Machine Learning Studio environment for working with the [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="14529-142">Модули эксперимента отображаются на центральной панели.</span><span class="sxs-lookup"><span data-stu-id="14529-142">The modules in the experiment are shown in the center pane.</span></span>
* <span data-ttu-id="14529-143">В верхней части правой панели находится окно просмотра и изменения скриптов R.</span><span class="sxs-lookup"><span data-stu-id="14529-143">The upper part of the right pane contains a window to view and edit your R scripts.</span></span>  
* <span data-ttu-id="14529-144">В нижней части правой панели отображаются свойства модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-144">The lower part of right pane shows some properties of the [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="14529-145">Журнал ошибок и журнал выходных данных можно просмотреть, щелкнув соответствующие элементы панели.</span><span class="sxs-lookup"><span data-stu-id="14529-145">You can view the error and output logs by clicking on the appropriate spots of this pane.</span></span>

<span data-ttu-id="14529-146">Разумеется, в оставшейся части этого документа мы рассмотрим модуль [Выполнить сценарий R][execute-r-script] подробнее.</span><span class="sxs-lookup"><span data-stu-id="14529-146">We will, of course, be discussing the [Execute R Script][execute-r-script] in greater detail in the rest of this document.</span></span>

<span data-ttu-id="14529-147">При работе с более сложными функциями R для изменения, тестирования и отладки кода я рекомендую использовать RStudio.</span><span class="sxs-lookup"><span data-stu-id="14529-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="14529-148">Как и в случае разработки любого программного обеспечения, создавайте код пошагово, отдельными фрагментами, и тестируйте его на небольших, простых проверочных примерах.</span><span class="sxs-lookup"><span data-stu-id="14529-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="14529-149">Затем вырезайте и вставляйте готовые функции в окно сценария модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-149">Then cut and paste your functions into the R script window of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="14529-150">Такой подход позволяет в полной мере использовать как интегрированную среду разработки (IDE) RStudio, так и возможности Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-150">This approach allows you to harness both the RStudio integrated development environment (IDE) and the power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="14529-151">Выполнение кода R</span><span class="sxs-lookup"><span data-stu-id="14529-151">Execute R code</span></span>
<span data-ttu-id="14529-152">Любой код на R в модуле [Выполнить сценарий R][execute-r-script] выполняется при запуске эксперимента нажатием кнопки **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="14529-152">Any R code in the [Execute R Script][execute-r-script] module will execute when you run the experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="14529-153">Когда код выполнен, на значке модуля [Выполнить сценарий R][execute-r-script] появляется флажок.</span><span class="sxs-lookup"><span data-stu-id="14529-153">When execution has completed, a check mark will appear on the [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="14529-154">Защищенное программирование на R для Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="14529-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="14529-155">При разработке кода на R для, скажем, какой-нибудь веб-службы с помощью Машинного обучения Azure необходимо предусмотреть, как ваш код будет реагировать на непредвиденные входные данные и исключения.</span><span class="sxs-lookup"><span data-stu-id="14529-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="14529-156">Чтобы не усложнять, я не стал добавлять проверку или обработку исключений во все примеры кода.</span><span class="sxs-lookup"><span data-stu-id="14529-156">To maintain clarity, I have not included much in the way of checking or exception handling in most of the code examples shown.</span></span> <span data-ttu-id="14529-157">Однако далее я приведу несколько примеров функций, использующих возможности языка R для обработки исключений.</span><span class="sxs-lookup"><span data-stu-id="14529-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="14529-158">Если вас интересует более подробная информация об обработке исключений на R, советую прочитать соответствующие разделы книги Викхема (Wickham) из [Приложения Б. Дополнительные материалы](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="14529-158">If you need a more complete treatment of R exception handling, I recommend you read the applicable sections of the book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="14529-159">Отладка и тестирование кода R в Студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="14529-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="14529-160">Повторюсь: я рекомендую использовать RStudio для отладки и тестирования небольших фрагментов кода на R.</span><span class="sxs-lookup"><span data-stu-id="14529-160">To reiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="14529-161">Но бывают случаи, когда необходимо отслеживать проблемы кода непосредственно в модуле [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-161">However, there are cases where you will need to track down R code problems in the [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="14529-162">Кроме того, это неплохая привычка — проверять результаты работы в Студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="14529-162">In addition, it is good practice to check your results in Machine Learning Studio.</span></span>

<span data-ttu-id="14529-163">Большая часть выходных данных при выполнении кода на R на платформе Машинного обучения Azure находится в файле output.log.</span><span class="sxs-lookup"><span data-stu-id="14529-163">Output from the execution of your R code and on the Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="14529-164">Дополнительная информация отображается в файле error.log.</span><span class="sxs-lookup"><span data-stu-id="14529-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="14529-165">Если при выполнении вашего кода в Студии машинного обучения происходит сбой, в первую очередь нужно просмотреть файл error.log.</span><span class="sxs-lookup"><span data-stu-id="14529-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be to look at error.log.</span></span> <span data-ttu-id="14529-166">В этом файле могут быть полезные сообщения об ошибках, которые помогут вам понять и исправить свою ошибку.</span><span class="sxs-lookup"><span data-stu-id="14529-166">This file can contain useful error messages to help you understand and correct your error.</span></span> <span data-ttu-id="14529-167">Чтобы просмотреть файл error.log, щелкните **View error log** (Просмотреть журнал ошибок) на **панели свойств** модуля [Выполнить сценарий R][execute-r-script], содержащего ошибку.</span><span class="sxs-lookup"><span data-stu-id="14529-167">To view error.log, click on **View error log** on the **properties pane** for the [Execute R Script][execute-r-script] containing the error.</span></span>

<span data-ttu-id="14529-168">Например, запустим этот код на R с неопределенной переменной y в модуле [Выполнить сценарий R][execute-r-script]:</span><span class="sxs-lookup"><span data-stu-id="14529-168">For example, I ran the following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="14529-169">Выполнить этот код не удается, возникает условие ошибки.</span><span class="sxs-lookup"><span data-stu-id="14529-169">This code fails to execute, resulting in an error condition.</span></span> <span data-ttu-id="14529-170">Если щелкнуть **View error log** (Просмотреть журнал ошибок) на **панели свойств**, появится всплывающее окно (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="14529-170">Clicking on **View error log** on the **properties pane** produces the display shown in Figure 2.</span></span>

  ![Всплывающее окно сообщения об ошибке][2]

<span data-ttu-id="14529-172">*Рис. 2. Всплывающее окно сообщения об ошибке*</span><span class="sxs-lookup"><span data-stu-id="14529-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="14529-173">Похоже, нужно просмотреть файл output.log, чтобы прочитать сообщение об ошибке в коде на R.</span><span class="sxs-lookup"><span data-stu-id="14529-173">It looks like we need to look in output.log to see the R error message.</span></span> <span data-ttu-id="14529-174">Щелкнем [Выполнить сценарий R][execute-r-script], а затем — **View output log** (Просмотр журнала выходных данных) на **панели свойств** справа.</span><span class="sxs-lookup"><span data-stu-id="14529-174">Click on the [Execute R Script][execute-r-script] and then click on the **View output.log** item on the **properties pane** to the right.</span></span> <span data-ttu-id="14529-175">Откроется новое окно браузера, где мы увидим следующее:</span><span class="sxs-lookup"><span data-stu-id="14529-175">A new browser window opens, and I see the following.</span></span>

    [Critical]     Error: Error 0063: The following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="14529-176">В сообщении об ошибке нет ничего неожиданного: проблема четко определена.</span><span class="sxs-lookup"><span data-stu-id="14529-176">This error message contains no surprises and clearly identifies the problem.</span></span>

<span data-ttu-id="14529-177">Чтобы проверить значение любого объекта в коде на R, можно обеспечить вывод этих значений в файл output.log.</span><span class="sxs-lookup"><span data-stu-id="14529-177">To inspect the value of any object in R, you can print these values to the output.log file.</span></span> <span data-ttu-id="14529-178">Правила проверки значений объектов в принципе те же, что и при интерактивном сеансе работы с R.</span><span class="sxs-lookup"><span data-stu-id="14529-178">The rules for examining object values are essentially the same as in an interactive R session.</span></span> <span data-ttu-id="14529-179">Например, если ввести в строке имя переменной, значение объекта выводится в файл output.log.</span><span class="sxs-lookup"><span data-stu-id="14529-179">For example, if you type a variable name on a line, the value of the object will be printed to the output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="14529-180">Пакеты в Студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="14529-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="14529-181">Служба машинного обучения Azure содержит более 350 предустановленных пакетов на языке R.</span><span class="sxs-lookup"><span data-stu-id="14529-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="14529-182">Чтобы увидеть список предустановленных пакетов, используйте приведенный ниже код в модуле [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-182">You can use the following code in the [Execute R Script][execute-r-script] module to retrieve a list of the preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="14529-183">Если вам пока не понятна последняя строка кода, не останавливайтесь.</span><span class="sxs-lookup"><span data-stu-id="14529-183">If you don't understand the last line of this code at the moment, read on.</span></span> <span data-ttu-id="14529-184">Далее в этом документе мы подробно рассмотрим использование R в среде Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-184">In the rest of this document we will extensively discuss using R in the Azure Machine Learning environment.</span></span>

### <a name="introduction-to-rstudio"></a><span data-ttu-id="14529-185">Основные сведения об RStudio</span><span class="sxs-lookup"><span data-stu-id="14529-185">Introduction to RStudio</span></span>
<span data-ttu-id="14529-186">RStudio — широко распространенная среда IDE для языка R. Я буду использовать RStudio для изменения, тестирования и отладки фрагментов кода на R, используемых в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="14529-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of the R code used in this quick start guide.</span></span> <span data-ttu-id="14529-187">Когда код на R готов и проверен, его можно просто вырезать из редактора RStudio и вставить в модуль [Выполнить сценарий R][execute-r-script] в Студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="14529-187">Once R code is tested and ready, you simply cut and paste from the RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="14529-188">Если на вашем компьютере еще не установлен язык R, советую сделать это сейчас.</span><span class="sxs-lookup"><span data-stu-id="14529-188">If you do not have the R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="14529-189">Вы можете бесплатно загрузить R с открытым исходным кодом на сайте Comprehensive R Archive Network (CRAN) по адресу [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="14529-189">Free downloads of open source R language are available at the Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="14529-190">Доступны файлы для скачивания для Windows, Mac OS и Linux или UNIX.</span><span class="sxs-lookup"><span data-stu-id="14529-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="14529-191">Выберите любое зеркало и следуйте инструкциям по загрузке.</span><span class="sxs-lookup"><span data-stu-id="14529-191">Choose a nearby mirror and follow the download directions.</span></span> <span data-ttu-id="14529-192">CRAN также содержит множество полезных пакетов для аналитики и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="14529-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="14529-193">Если вы еще не знакомы с RStudio, вам лучше загрузить и установить версию для настольного компьютера.</span><span class="sxs-lookup"><span data-stu-id="14529-193">If you are new to RStudio, you should download and install the desktop version.</span></span> <span data-ttu-id="14529-194">Скачать RStudio для Windows, Mac OS и Linux (UNIX) можно по ссылке http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="14529-194">You can find the RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="14529-195">Следуйте инструкциям по установке RStudio на компьютер.</span><span class="sxs-lookup"><span data-stu-id="14529-195">Follow the directions provided to install RStudio on your desktop machine.</span></span>  

<span data-ttu-id="14529-196">Руководство по основам работы с RStudio доступно по адресу https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="14529-196">A tutorial introduction to RStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="14529-197">Дополнительные сведения по использованию RStudio можно найти в [Приложении А][appendixa].</span><span class="sxs-lookup"><span data-stu-id="14529-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="14529-198"><a id="scriptmodule"></a>Добавление данных в модуль «Выполнение сценария R» и их извлечение оттуда</span><span class="sxs-lookup"><span data-stu-id="14529-198"><a id="scriptmodule"></a>Get data in and out of the Execute R Script module</span></span>
<span data-ttu-id="14529-199">В этом разделе мы рассмотрим ввод и вывод данных модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-199">In this section we will discuss how you get data into and out of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="14529-200">Мы ознакомимся с обработкой различных типов данных, передаваемых в модуль [Выполнить сценарий R][execute-r-script] и получаемых из него.</span><span class="sxs-lookup"><span data-stu-id="14529-200">We will review how to handle various data types read into and out of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="14529-201">Полный код для этого раздела есть в ZIP-файле, который вы загрузили ранее.</span><span class="sxs-lookup"><span data-stu-id="14529-201">The complete code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="14529-202">Загрузка и проверка данных в Студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="14529-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="14529-203"><a id="loading"></a>Загрузка набора данных</span><span class="sxs-lookup"><span data-stu-id="14529-203"><a id="loading"></a>Load the dataset</span></span>
<span data-ttu-id="14529-204">Для начала загрузим в Студию машинного обучения Azure файл **csdairydata.csv** .</span><span class="sxs-lookup"><span data-stu-id="14529-204">We will start by loading the **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="14529-205">Запустите среду Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="14529-206">Щелкните **+ NEW** (+ Создать) в нижнем левом углу экрана и выберите **Dataset** (Набор данных).</span><span class="sxs-lookup"><span data-stu-id="14529-206">Click on **+ NEW** at the lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="14529-207">Выберите **From Local File** (Из локального файла) и нажмите кнопку **Browse** (Обзор), чтобы выбрать файл.</span><span class="sxs-lookup"><span data-stu-id="14529-207">Select **From Local File**, and then **Browse** to select the file.</span></span>
* <span data-ttu-id="14529-208">Убедитесь, что в качестве типа набора данных выбран вариант **Универсальный CSV-файл с заголовком** .</span><span class="sxs-lookup"><span data-stu-id="14529-208">Make sure you have selected **Generic CSV file with header (.csv)** as the type for the dataset.</span></span>
* <span data-ttu-id="14529-209">Щелкните значок галочки.</span><span class="sxs-lookup"><span data-stu-id="14529-209">Click the check mark.</span></span>
* <span data-ttu-id="14529-210">После загрузки набора данных он появится на вкладке **Наборы данных** .</span><span class="sxs-lookup"><span data-stu-id="14529-210">After the dataset has been uploaded, you should see the new dataset by clicking on the **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="14529-211">Создание эксперимента</span><span class="sxs-lookup"><span data-stu-id="14529-211">Create an experiment</span></span>
<span data-ttu-id="14529-212">Теперь, когда у нас есть определенные данные в Студии машинного обучения, нужно создать эксперимент, чтобы выполнить анализ.</span><span class="sxs-lookup"><span data-stu-id="14529-212">Now that we have some data in Machine Learning Studio, we need to create an experiment to do the analysis.</span></span>  

* <span data-ttu-id="14529-213">Щелкните **+ NEW** (+ Создать) в левом нижнем углу и выберите **Experiment** (Эксперимент), а затем — **Blank Experiment** (Пустой эксперимент).</span><span class="sxs-lookup"><span data-stu-id="14529-213">Click on **+ NEW** at the lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="14529-214">Чтобы задать для него название, выделите и отредактируйте заголовок **Эксперимент создан...** вверху страницы.</span><span class="sxs-lookup"><span data-stu-id="14529-214">You can name your experiment by selecting, and modifying, the **Experiment created on ...** title at the top of the page.</span></span> <span data-ttu-id="14529-215">Например, можно изменить его на **Анализ молочных продуктов**.</span><span class="sxs-lookup"><span data-stu-id="14529-215">For example, changing it to **CA Dairy Analysis**.</span></span>
* <span data-ttu-id="14529-216">В левой части страницы эксперимента разверните узел **Saved Datasets** (Сохраненные наборы данных), а затем – **My Datasets** (Мои наборы данных).</span><span class="sxs-lookup"><span data-stu-id="14529-216">On the left of the experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="14529-217">Вы должны увидеть загруженный ранее файл **cadairydata.csv** .</span><span class="sxs-lookup"><span data-stu-id="14529-217">You should see the **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="14529-218">Перетащите **набор данных csdairydata.csv** на рабочую область эксперимента.</span><span class="sxs-lookup"><span data-stu-id="14529-218">Drag and drop the **csdairydata.csv dataset** onto the experiment.</span></span>
* <span data-ttu-id="14529-219">В поле **Search experiment items** (Поиск элементов эксперимента) в верхней части левой панели введите текст [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-219">In the **Search experiment items** box on the top of the left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="14529-220">Этот модуль появится в списке результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="14529-220">You will see the module appear in the search list.</span></span>
* <span data-ttu-id="14529-221">Перетащите модуль [Выполнить сценарий R][execute-r-script] на палитру.</span><span class="sxs-lookup"><span data-stu-id="14529-221">Drag and drop the [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="14529-222">Соедините порт вывода **набора данных csdairydata.csv** с крайним левым портом ввода (**Набор данных 1**) модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-222">Connect the output of the **csdairydata.csv dataset** to the leftmost input (**Dataset1**) of the [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="14529-223">**Не забудьте нажать кнопку «Сохранить»!**</span><span class="sxs-lookup"><span data-stu-id="14529-223">**Don't forget to click on 'Save'!**</span></span>  

<span data-ttu-id="14529-224">На этом этапе ваш эксперимент должен выглядеть, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="14529-224">At this point your experiment should look something like Figure 3.</span></span>

![Эксперимент «Анализ молочных продуктов»: набор данных и модуль «Выполнение сценария R»][3]

<span data-ttu-id="14529-226">*Рис. 3. Эксперимент «Анализ молочных продуктов»: набор данных и модуль «Выполнение сценария R»*</span><span class="sxs-lookup"><span data-stu-id="14529-226">*Figure 3. The CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-the-data"></a><span data-ttu-id="14529-227">Проверка данных</span><span class="sxs-lookup"><span data-stu-id="14529-227">Check on the data</span></span>
<span data-ttu-id="14529-228">Рассмотрим данные, загруженные в наш эксперимент.</span><span class="sxs-lookup"><span data-stu-id="14529-228">Let's have a look at the data we have loaded into our experiment.</span></span> <span data-ttu-id="14529-229">В эксперименте щелкните порт вывода **набора данных cadairydata.csv** и выберите **Visualize** (Визуализировать).</span><span class="sxs-lookup"><span data-stu-id="14529-229">In the experiment, click on the output of the **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="14529-230">Вы увидите нечто вроде этого (рис. 4):</span><span class="sxs-lookup"><span data-stu-id="14529-230">You should see something like Figure 4.</span></span>  

![Сводка набора данных cadairydata.csv][4]

<span data-ttu-id="14529-232">*Рис. 4. Сводка набора данных cadairydata.csv*</span><span class="sxs-lookup"><span data-stu-id="14529-232">*Figure 4. Summary of the cadairydata.csv dataset.*</span></span>

<span data-ttu-id="14529-233">Здесь представлено много полезной информации.</span><span class="sxs-lookup"><span data-stu-id="14529-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="14529-234">Также видны первые несколько строк этого набора данных.</span><span class="sxs-lookup"><span data-stu-id="14529-234">We can see the first several rows of that dataset.</span></span> <span data-ttu-id="14529-235">Если выбрать какой-либо столбец, в разделе «Статистика» появится более подробная информация об этом столбце.</span><span class="sxs-lookup"><span data-stu-id="14529-235">If we select a column, the Statistics section shows more information about the column.</span></span> <span data-ttu-id="14529-236">Например, строка «Тип компонента» показывает, какие типы данных присвоены этому в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-236">For example, the Feature Type row shows us what data types Azure Machine Learning Studio assigned to the column.</span></span> <span data-ttu-id="14529-237">Такой беглый просмотр данных — хорошая проверка перед началом серьезной работы.</span><span class="sxs-lookup"><span data-stu-id="14529-237">Having a quick look like this is a good sanity check before we start to do any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="14529-238">Первый сценарий R</span><span class="sxs-lookup"><span data-stu-id="14529-238">First R script</span></span>
<span data-ttu-id="14529-239">Создадим простой первый сценарий на R, с которым и будем работать в Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-239">Let's create a simple first R script to experiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="14529-240">Я создал и протестировал такой сценарий в RStudio:</span><span class="sxs-lookup"><span data-stu-id="14529-240">I have created and tested the following script in RStudio.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="14529-241">Теперь мне нужно перенести его в Студию машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-241">Now I need to transfer this script to Azure Machine Learning Studio.</span></span> <span data-ttu-id="14529-242">Можно было бы его просто вырезать и вставить.</span><span class="sxs-lookup"><span data-stu-id="14529-242">I could simply cut and paste.</span></span> <span data-ttu-id="14529-243">Но в данном случае я перенесу свой скрипт R при помощи ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="14529-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-to-the-execute-r-script-module"></a><span data-ttu-id="14529-244">Ввод данных в модуль "Выполнение скрипта R"</span><span class="sxs-lookup"><span data-stu-id="14529-244">Data input to the Execute R Script module</span></span>
<span data-ttu-id="14529-245">Рассмотрим порты ввода модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-245">Let's have a look at the inputs to the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="14529-246">В этом примере мы считаем данные по молочной продукции Калифорнии в модуль [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-246">In this example we will read the California dairy data into the [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="14529-247">У модуля [Выполнить сценарий R][execute-r-script] может быть три порта ввода.</span><span class="sxs-lookup"><span data-stu-id="14529-247">There are three possible inputs for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="14529-248">В зависимости от приложения можно использовать любой из них или все.</span><span class="sxs-lookup"><span data-stu-id="14529-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="14529-249">Кроме того, иногда целесообразно использовать сценарий R вообще без портов ввода.</span><span class="sxs-lookup"><span data-stu-id="14529-249">It is also perfectly reasonable to use an R script that takes no input at all.</span></span>  

<span data-ttu-id="14529-250">Рассмотрим все порты ввода по порядку слева направо.</span><span class="sxs-lookup"><span data-stu-id="14529-250">Let's look at each of these inputs, going from left to right.</span></span> <span data-ttu-id="14529-251">Наведя курсор на порт, можно увидеть всплывающую подсказку с его именем.</span><span class="sxs-lookup"><span data-stu-id="14529-251">You can see the names of each of the inputs by placing your cursor over the input and reading the tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="14529-252">Пакет скриптов</span><span class="sxs-lookup"><span data-stu-id="14529-252">Script Bundle</span></span>
<span data-ttu-id="14529-253">Порт ввода "Пакет сценариев" позволяет передать содержимое ZIP-файла в модуль [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-253">The Script Bundle input allows you to pass the contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="14529-254">Для считывания содержимого ZIP-файла в код на R можно использовать одну из этих команд.</span><span class="sxs-lookup"><span data-stu-id="14529-254">You can use one of the following commands to read the contents of the zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="14529-255">Машинное обучение Azure обрабатывает файлы ZIP-архива, как если бы они находились в каталоге src/, поэтому необходимо добавлять имя этого каталога в начало имен файлов.</span><span class="sxs-lookup"><span data-stu-id="14529-255">Azure Machine Learning treats files in the zip as if they are in the src/ directory, so you need to prefix your file names with this directory name.</span></span> <span data-ttu-id="14529-256">Например, если ZIP-файл содержит файлы `yourfile.R` и `yourData.rdata` в корне, вы будете рассматривать их как `src/yourfile.R` и `src/yourData.rdata` при использовании `source` и `load`.</span><span class="sxs-lookup"><span data-stu-id="14529-256">For example, if the zip contains the files `yourfile.R` and `yourData.rdata` in the root of the zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="14529-257">Загрузка наборов данных уже рассматривалась в разделе [Загрузка набора данных](#loading).</span><span class="sxs-lookup"><span data-stu-id="14529-257">We already discussed loading datasets in [Loading the dataset](#loading).</span></span> <span data-ttu-id="14529-258">После создания и тестирования сценария R, описанного в предыдущем разделе, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="14529-258">Once you have created and tested the R script shown in the previous section, do the following:</span></span>

1. <span data-ttu-id="14529-259">Сохраните скрипт R в файл с расширением .R.</span><span class="sxs-lookup"><span data-stu-id="14529-259">Save the R script into a .R file.</span></span> <span data-ttu-id="14529-260">Я назвал свой файл скрипта "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="14529-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="14529-261">Вот содержимое.</span><span class="sxs-lookup"><span data-stu-id="14529-261">Here's the contents.</span></span>
   
        ## Only one of the following two lines should be used
        ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
        ## If in RStudio, use the second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## The following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="14529-262">Создайте ZIP-файл и скопируйте в него свой скрипт.</span><span class="sxs-lookup"><span data-stu-id="14529-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="14529-263">В Windows щелкните файл правой кнопкой мыши и выберите **Отправить**, а затем — **Сжатая ZIP-папка**.</span><span class="sxs-lookup"><span data-stu-id="14529-263">On Windows, you can right-click on the file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="14529-264">Будет создан ZIP-файл, содержащий файл "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="14529-264">This will create a new zip file containing the "simpleplot.R" file.</span></span>
3. <span data-ttu-id="14529-265">Добавьте свой файл в **наборы данных** в студии машинного обучения, указав тип файла **ZIP**.</span><span class="sxs-lookup"><span data-stu-id="14529-265">Add your file to the **datasets** in Machine Learning Studio, specifying the type as **zip**.</span></span> <span data-ttu-id="14529-266">Теперь вы увидите ZIP-файл среди своих наборов данных.</span><span class="sxs-lookup"><span data-stu-id="14529-266">You should now see the zip file in your datasets.</span></span>
4. <span data-ttu-id="14529-267">Перетащите ZIP-файл из **наборов данных** на **холст студии машинного обучения**.</span><span class="sxs-lookup"><span data-stu-id="14529-267">Drag and drop the zip file from **datasets** onto the **ML Studio canvas**.</span></span>
5. <span data-ttu-id="14529-268">Соедините порт вывода значка **ZIP-данных** с портом ввода **Пакет сценариев** модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-268">Connect the output of the **zip data** icon to the **Script Bundle** input of the [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="14529-269">В окне кода модуля [Выполнить сценарий R][execute-r-script] введите функцию `source()` с именем вашего ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="14529-269">Type the `source()` function with your zip file name into the code window for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="14529-270">В данном случае введено `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="14529-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="14529-271">Обязательно щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="14529-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="14529-272">После выполнения этих шагов модуль [Выполнить сценарий R][execute-r-script] выполнит сценарий R в ZIP-файле при запуске эксперимента.</span><span class="sxs-lookup"><span data-stu-id="14529-272">Once these steps are complete, the [Execute R Script][execute-r-script] module will execute the R script in the zip file when the experiment is run.</span></span> <span data-ttu-id="14529-273">На этом этапе ваш эксперимент должен выглядеть, как изображено на рисунке 5.</span><span class="sxs-lookup"><span data-stu-id="14529-273">At this point your experiment should look something like Figure 5.</span></span>

![Эксперимент с использованием сценария R, сжатого в ZIP-файл][6]

<span data-ttu-id="14529-275">*Рис. 5. Эксперимент с использованием сценария R, сжатого в ZIP-файл*</span><span class="sxs-lookup"><span data-stu-id="14529-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="14529-276">Набор данных 1</span><span class="sxs-lookup"><span data-stu-id="14529-276">Dataset1</span></span>
<span data-ttu-id="14529-277">С помощью порта ввода «Набор данных 1» можно передать прямоугольную таблицу данных в код на R.</span><span class="sxs-lookup"><span data-stu-id="14529-277">You can pass a rectangular table of data to your R code by using the Dataset1 input.</span></span> <span data-ttu-id="14529-278">В нашем простом сценарии функция `maml.mapInputPort(1)` считывает данные из порта 1.</span><span class="sxs-lookup"><span data-stu-id="14529-278">In our simple script the `maml.mapInputPort(1)` function reads the data from port 1.</span></span> <span data-ttu-id="14529-279">Затем эти данные присваиваются имени переменной в вашем коде, тип которой — таблица данных.</span><span class="sxs-lookup"><span data-stu-id="14529-279">This data is then assigned to a dataframe variable name in your code.</span></span> <span data-ttu-id="14529-280">В нашем примере скрипта присвоение выполняет первая строка кода.</span><span class="sxs-lookup"><span data-stu-id="14529-280">In our simple script the first line of code performs the assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="14529-281">Выполните эксперимент, нажав кнопку **Запуск** .</span><span class="sxs-lookup"><span data-stu-id="14529-281">Execute your experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="14529-282">По завершении выполнения щелкните модуль [Выполнить сценарий R][execute-r-script], а затем — **View output log** (Просмотр журнала выходных данных) на панели свойств.</span><span class="sxs-lookup"><span data-stu-id="14529-282">When the execution finishes, click on the [Execute R Script][execute-r-script] module and then click **View output log** on the properties pane.</span></span> <span data-ttu-id="14529-283">В браузере откроется новая страница с содержимым файла output.log.</span><span class="sxs-lookup"><span data-stu-id="14529-283">A new page should appear in your browser showing the contents of the output.log file.</span></span> <span data-ttu-id="14529-284">Прокрутив ее вниз, вы увидите следующее:</span><span class="sxs-lookup"><span data-stu-id="14529-284">When you scroll down you should see something like the following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="14529-285">Далее в нижней части страницы содержатся более подробные сведения в столбцах, которые будут выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="14529-285">Farther down the page is more detailed information on the columns, which will look something like the following.</span></span>

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

<span data-ttu-id="14529-286">Результаты преимущественно ожидаемые. В таблице данных 228 наблюдений и 9 столбцов.</span><span class="sxs-lookup"><span data-stu-id="14529-286">These results are mostly as expected, with 228 observations and 9 columns in the dataframe.</span></span> <span data-ttu-id="14529-287">Отображаются имена столбцов, тип данных R и пример каждого столбца.</span><span class="sxs-lookup"><span data-stu-id="14529-287">We can see the column names, the R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="14529-288">Эти же результаты можно получить с помощью порта вывода "Устройство R" модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-288">This same printed output is conveniently available from the R Device output of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="14529-289">Порты вывода модуля [Выполнить сценарий R][execute-r-script] мы рассмотрим подробнее в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="14529-289">We will discuss the outputs of the [Execute R Script][execute-r-script] module in the next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="14529-290">Набор данных 2</span><span class="sxs-lookup"><span data-stu-id="14529-290">Dataset2</span></span>
<span data-ttu-id="14529-291">Поведение портов ввода "Набор данных 2" такое же, как у портов "Набор данных 1".</span><span class="sxs-lookup"><span data-stu-id="14529-291">The behavior of the Dataset2 input is identical to that of Dataset1.</span></span> <span data-ttu-id="14529-292">С помощью этого порта можно передать еще одну прямоугольную таблицу данных в код на R.</span><span class="sxs-lookup"><span data-stu-id="14529-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="14529-293">Для передачи этих данных используется функция `maml.mapInputPort(2)`с аргументом 2.</span><span class="sxs-lookup"><span data-stu-id="14529-293">The function `maml.mapInputPort(2)`, with the argument 2, is used to pass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="14529-294">Порты вывода модуля "Выполнение скрипта R"</span><span class="sxs-lookup"><span data-stu-id="14529-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="14529-295">Вывод таблицы данных</span><span class="sxs-lookup"><span data-stu-id="14529-295">Output a dataframe</span></span>
<span data-ttu-id="14529-296">Через порт «Итоговый набор данных 1» можно вывести содержимое таблицы данных на R в виде прямоугольной таблицы с помощью функции `maml.mapOutputPort()` .</span><span class="sxs-lookup"><span data-stu-id="14529-296">You can output the contents of an R dataframe as a rectangular table through the Result Dataset1 port by using the `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="14529-297">В нашем примере простого сценария R это выполняется с помощью такой строки:</span><span class="sxs-lookup"><span data-stu-id="14529-297">In our simple R script this is performed by the following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="14529-298">Выполнив эксперимент, щелкните порт вывода Result Dataset1 (Итоговый набор данных 1), а затем — **Visualize** (Визуализировать).</span><span class="sxs-lookup"><span data-stu-id="14529-298">After running the experiment, click on the Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="14529-299">Вы увидите нечто вроде этого (рис. 6):</span><span class="sxs-lookup"><span data-stu-id="14529-299">You should see something like Figure 6.</span></span>

![Визуализация вывода данных по молочной продукции Калифорнии][7]

<span data-ttu-id="14529-301">*Рис. 6. Визуализация вывода данных по молочной продукции Калифорнии*</span><span class="sxs-lookup"><span data-stu-id="14529-301">*Figure 6. The visualization of the output of the California dairy data.*</span></span>

<span data-ttu-id="14529-302">Выходные данные выглядят в точности так, как и входные — как и предполагалось.</span><span class="sxs-lookup"><span data-stu-id="14529-302">This output looks identical to the input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="14529-303">Порт вывода "Устройство R"</span><span class="sxs-lookup"><span data-stu-id="14529-303">R Device output</span></span>
<span data-ttu-id="14529-304">Порт вывода "Устройство R" модуля [Выполнить сценарий R][execute-r-script] предназначен для вывода сообщений и графики.</span><span class="sxs-lookup"><span data-stu-id="14529-304">The Device output of the [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="14529-305">Как стандартный вывод данных, так и сообщения об ошибках на R направляются в порт вывода "Устройство R".</span><span class="sxs-lookup"><span data-stu-id="14529-305">Both standard output and standard error messages from R are sent to the R Device output port.</span></span>  

<span data-ttu-id="14529-306">Чтобы просмотреть выходные данные порта «Устройство R», щелкните этот порт и выберите **Визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="14529-306">To view the R Device output, click on the port and then on **Visualize**.</span></span> <span data-ttu-id="14529-307">На рисунке 7 показаны стандартный вывод данных и стандартный вывод ошибок.</span><span class="sxs-lookup"><span data-stu-id="14529-307">We see the standard output and standard error from the R script in Figure 7.</span></span>

![Стандартный вывод данных и стандартный вывод ошибок из порта «Устройство R»][8]

<span data-ttu-id="14529-309">*Рис. 7. Стандартный вывод данных и стандартный вывод ошибок из порта «Устройство R»*</span><span class="sxs-lookup"><span data-stu-id="14529-309">*Figure 7. Standard output and standard error from the R Device port.*</span></span>

<span data-ttu-id="14529-310">Прокрутив вниз, увидим графический вывод данных скрипта R (рис. 8).</span><span class="sxs-lookup"><span data-stu-id="14529-310">Scrolling down we see the graphics output from our R script in Figure 8.</span></span>  

![Графический вывод данных из порта «Устройство R»][9]

<span data-ttu-id="14529-312">*Рис. 8. Графический вывод данных из порта «Устройство R»*</span><span class="sxs-lookup"><span data-stu-id="14529-312">*Figure 8. Graphics output from the R Device port.*</span></span>  

## <span data-ttu-id="14529-313"><a id="filtering"></a>Фильтрация и преобразование данных</span><span class="sxs-lookup"><span data-stu-id="14529-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="14529-314">В этом разделе мы выполним простые операции фильтрации и преобразования данных по молочной продукции Калифорнии.</span><span class="sxs-lookup"><span data-stu-id="14529-314">In this section we will perform some basic data filtering and transformation operations on the California dairy data.</span></span> <span data-ttu-id="14529-315">В конце мы получим данные в формате, удобном для построения аналитической модели.</span><span class="sxs-lookup"><span data-stu-id="14529-315">By the end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="14529-316">В частности, в этом разделе мы выполним несколько распространенных задач по очистке и преобразованию данных: преобразование типа данных, фильтрацию кадров данных, добавление новых вычисляемых столбцов и преобразование значений.</span><span class="sxs-lookup"><span data-stu-id="14529-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="14529-317">Эти базовые навыки помогут вам справиться с любыми видами задач при решении практических проблем.</span><span class="sxs-lookup"><span data-stu-id="14529-317">This background should help you deal with the many variations encountered in real-world problems.</span></span>

<span data-ttu-id="14529-318">Полный код на R для этого раздела доступен в ZIP-файле, который вы загрузили ранее.</span><span class="sxs-lookup"><span data-stu-id="14529-318">The complete R code for this section is available in the zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="14529-319">Преобразование типов данных</span><span class="sxs-lookup"><span data-stu-id="14529-319">Type transformations</span></span>
<span data-ttu-id="14529-320">Мы уже можем считать данные по молочной продукции Калифорнии в код на R модуля [Выполнить сценарий R][execute-r-script], но нужно убедиться, что данные в столбцах имеют нужный тип и формат.</span><span class="sxs-lookup"><span data-stu-id="14529-320">Now that we can read the California dairy data into the R code in the [Execute R Script][execute-r-script] module, we need to ensure that the data in the columns has the intended type and format.</span></span>  

<span data-ttu-id="14529-321">R — динамически типизированный язык. Другими словами, при необходимости типы данных преобразуются из одного в другой.</span><span class="sxs-lookup"><span data-stu-id="14529-321">R is a dynamically typed language, which means that data types are coerced from one to another as required.</span></span> <span data-ttu-id="14529-322">Атомарные типы данных в языке R включают числовые, логические и символьные.</span><span class="sxs-lookup"><span data-stu-id="14529-322">The atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="14529-323">Факторы используются для компактного хранения категориальных данных.</span><span class="sxs-lookup"><span data-stu-id="14529-323">The factor type is used to compactly store categorical data.</span></span> <span data-ttu-id="14529-324">Подробные сведения о типах данных можно найти в разделе [Приложение Б. Дополнительные материалы](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="14529-324">You can find much more information on data types in the references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="14529-325">При считывании в R табличных данных из внешних источников рекомендуется всегда проверять в столбцах результирующие типы.</span><span class="sxs-lookup"><span data-stu-id="14529-325">When tabular data is read into R from an external source, it is always a good idea to check the resulting types in the columns.</span></span> <span data-ttu-id="14529-326">Зачастую может оказаться, что данные в столбце не символьного типа, как предполагалось, а относятся к типу фактор (или наоборот).</span><span class="sxs-lookup"><span data-stu-id="14529-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="14529-327">В других случаях столбец, который должен содержать числовые данные, содержит символьные данные, например «1,23» вместо 1,23 — числа с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="14529-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="14529-328">К счастью, можно легко преобразовывать один тип данных в другой, при условии что их сопоставление возможно.</span><span class="sxs-lookup"><span data-stu-id="14529-328">Fortunately, it is easy to convert one type to another, as long as mapping is possible.</span></span> <span data-ttu-id="14529-329">Например, нельзя преобразовать слово "Самара" в числовое значение, но его можно преобразовать в фактор (категориальную переменную).</span><span class="sxs-lookup"><span data-stu-id="14529-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it to a factor (categorical variable).</span></span> <span data-ttu-id="14529-330">Еще один пример. Числовое значение 1 можно преобразовать в символ '1' или в фактор.</span><span class="sxs-lookup"><span data-stu-id="14529-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="14529-331">Синтаксис любого из этих преобразований прост: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="14529-331">The syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="14529-332">Вот функции преобразования типов данных:</span><span class="sxs-lookup"><span data-stu-id="14529-332">These type conversion functions include the following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="14529-333">Рассмотрим типы данных столбцов, которые мы ввели в предыдущем разделе. Тип всех столбцов числовой, кроме столбца Month, тип которого символьный.</span><span class="sxs-lookup"><span data-stu-id="14529-333">Looking at the data types of the columns we input in the previous section: all columns are of type numeric, except for the column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="14529-334">Преобразуем его в фактор и проверим результат.</span><span class="sxs-lookup"><span data-stu-id="14529-334">Let's convert this to a factor and test the results.</span></span>  

<span data-ttu-id="14529-335">Я удалил строку, создававшую матрицу точечной диаграммы, и добавил строку, преобразующую тип столбца Month в фактор.</span><span class="sxs-lookup"><span data-stu-id="14529-335">I have deleted the line that created the scatterplot matrix and added a line converting the 'Month' column to a factor.</span></span> <span data-ttu-id="14529-336">В моем эксперименте я просто вырежу код на R и вставлю его в окно кода модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-336">In my experiment I will just cut and paste the R code into the code window of the [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="14529-337">Также можно обновить ZIP-файл и передать его в Студию машинного обучения Azure, но это будет дольше.</span><span class="sxs-lookup"><span data-stu-id="14529-337">You could also update the zip file and upload it to Azure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check the result
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="14529-338">Выполните этот код и найдите в журнале сценарий R.</span><span class="sxs-lookup"><span data-stu-id="14529-338">Let's execute this code and look at the output log for the R script.</span></span> <span data-ttu-id="14529-339">Соответствующие данные журнала показаны на рис. 9.</span><span class="sxs-lookup"><span data-stu-id="14529-339">The relevant data from the log is shown in Figure 9.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="14529-340">*Рис. 9. Сводка таблицы данных с фактором в качестве переменной*</span><span class="sxs-lookup"><span data-stu-id="14529-340">*Figure 9. Summary of the dataframe with a factor variable.*</span></span>

<span data-ttu-id="14529-341">Тип столбца Month изменился на**Factor w/ 14 levels**.</span><span class="sxs-lookup"><span data-stu-id="14529-341">The type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="14529-342">Такой вариант нас не устраивает, поскольку в году всего 12 месяцев.</span><span class="sxs-lookup"><span data-stu-id="14529-342">This is a problem since there are only 12 months in the year.</span></span> <span data-ttu-id="14529-343">Также можно убедиться, что тип выходных данных — **Categorical** (Категориальный), выбрав **Visualize** (Визуализировать) в меню порта Result Dataset (Итоговый набор данных).</span><span class="sxs-lookup"><span data-stu-id="14529-343">You can also check to see that the type in **Visualize** of the Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="14529-344">Проблема в том, что кодирование столбца "Месяц" было бессистемным.</span><span class="sxs-lookup"><span data-stu-id="14529-344">The problem is that the 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="14529-345">В некоторых случаях месяц назван April, а в других — сокращенно Apr. Эту проблему можно решить, сократив строку до трех символов.</span><span class="sxs-lookup"><span data-stu-id="14529-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming the string to 3 characters.</span></span> <span data-ttu-id="14529-346">Теперь строка кода выглядит так:</span><span class="sxs-lookup"><span data-stu-id="14529-346">The line of code now looks like the following:</span></span>

    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="14529-347">Запустите эксперимент еще раз и проверьте журнал.</span><span class="sxs-lookup"><span data-stu-id="14529-347">Rerun the experiment and view the output log.</span></span> <span data-ttu-id="14529-348">Ожидаемые результаты показаны на рис. 10.</span><span class="sxs-lookup"><span data-stu-id="14529-348">The expected results are shown in Figure 10.</span></span>  

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="14529-349">*Рис. 10. Сводка таблицы данных с правильным количеством уровней фактора*</span><span class="sxs-lookup"><span data-stu-id="14529-349">*Figure 10. Summary of the dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="14529-350">Теперь у нашей переменной — фактора — 12 уровней, как и положено.</span><span class="sxs-lookup"><span data-stu-id="14529-350">Our factor variable now has the desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="14529-351">Базовая фильтрация таблицы данных</span><span class="sxs-lookup"><span data-stu-id="14529-351">Basic data frame filtering</span></span>
<span data-ttu-id="14529-352">Таблицы данных R поддерживают массу возможностей фильтрации.</span><span class="sxs-lookup"><span data-stu-id="14529-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="14529-353">Наборы данных можно разбивать на подмножества, используя логическую фильтрацию по строкам или столбцам.</span><span class="sxs-lookup"><span data-stu-id="14529-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="14529-354">Во многих случаях вам потребуются сложные критерии фильтрации.</span><span class="sxs-lookup"><span data-stu-id="14529-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="14529-355">В материалах из [Приложения Б. Дополнительные материалы](#appendixb) содержится множество примеров фильтрации таблиц данных.</span><span class="sxs-lookup"><span data-stu-id="14529-355">The references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="14529-356">Выполним операцию фильтрации в нашем наборе данных.</span><span class="sxs-lookup"><span data-stu-id="14529-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="14529-357">Если рассмотреть столбцы таблицы данных cadariydata, можно заметить два ненужных столбца.</span><span class="sxs-lookup"><span data-stu-id="14529-357">If you look at the columns in the cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="14529-358">Первый содержит только номер строки — который не так уж и важен.</span><span class="sxs-lookup"><span data-stu-id="14529-358">The first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="14529-359">Второй, Year.Month, содержит избыточную информацию.</span><span class="sxs-lookup"><span data-stu-id="14529-359">The second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="14529-360">С помощью кода на R мы можем легко исключить эти столбцы.</span><span class="sxs-lookup"><span data-stu-id="14529-360">We can easily exclude these columns by using the following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="14529-361">С этого момента я буду показывать только дополнительный код, который добавляется в модуль [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-361">From now on in this section, I will just show you the additional code I am adding in the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="14529-362">Новые строки будут добавляться **перед** функцией `str()`.</span><span class="sxs-lookup"><span data-stu-id="14529-362">I will add each new line **before** the `str()` function.</span></span> <span data-ttu-id="14529-363">Эта функция нужна для проверки результатов в Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-363">I use this function to verify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="14529-364">Добавим следующую строку в код на R в модуле [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-364">I add the following line to my R code in the [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="14529-365">Выполните этот код в своем эксперименте и проверьте результат по журналу.</span><span class="sxs-lookup"><span data-stu-id="14529-365">Run this code in your experiment and check the result from the output log.</span></span> <span data-ttu-id="14529-366">Результат приведен на рис. 11.</span><span class="sxs-lookup"><span data-stu-id="14529-366">These results are shown in Figure 11.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="14529-367">*Рис. 11. Сводка таблицы данных после удаления двух столбцов*</span><span class="sxs-lookup"><span data-stu-id="14529-367">*Figure 11. Summary of the dataframe with two columns removed.*</span></span>

<span data-ttu-id="14529-368">Отличная новость!</span><span class="sxs-lookup"><span data-stu-id="14529-368">Good news!</span></span> <span data-ttu-id="14529-369">Результат оправдал ожидания.</span><span class="sxs-lookup"><span data-stu-id="14529-369">We get the expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="14529-370">Добавление нового столбца</span><span class="sxs-lookup"><span data-stu-id="14529-370">Add a new column</span></span>
<span data-ttu-id="14529-371">При создании модели временных рядов удобно иметь столбец, отсчитывающий месяцы с начала временного ряда.</span><span class="sxs-lookup"><span data-stu-id="14529-371">To create time series models it will be convenient to have a column containing the months since the start of the time series.</span></span> <span data-ttu-id="14529-372">Мы создадим столбец Month.Count (Количество месяцев).</span><span class="sxs-lookup"><span data-stu-id="14529-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="14529-373">Для упрощения кодирования создадим первую простую функцию `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="14529-373">To help organize the code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="14529-374">Затем применим эту функцию для создания столбца в таблице данных.</span><span class="sxs-lookup"><span data-stu-id="14529-374">We will then apply this function to create a new column in the dataframe.</span></span> <span data-ttu-id="14529-375">Вот новый код:</span><span class="sxs-lookup"><span data-stu-id="14529-375">The new code is as follows.</span></span>

    ## Create a new column with the month count
    ## Function to find the number of months from the first
    ## month of the time series
    num.month <- function(Year, Month) {
      ## Find the starting year
      min.year  <- min(Year)

      ## Compute the number of months from the start of the time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute the new column for the dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="14529-376">Теперь выполните обновленный эксперимент и посмотрите результаты в журнале.</span><span class="sxs-lookup"><span data-stu-id="14529-376">Now run the updated experiment and use the output log to view the results.</span></span> <span data-ttu-id="14529-377">Этот результат приведен на рисунке 12.</span><span class="sxs-lookup"><span data-stu-id="14529-377">These results are shown in Figure 12.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="14529-378">*Рис. 12. Сводка таблицы данных с добавленным столбцом*</span><span class="sxs-lookup"><span data-stu-id="14529-378">*Figure 12. Summary of the dataframe with the additional column.*</span></span>

<span data-ttu-id="14529-379">Похоже, все работает.</span><span class="sxs-lookup"><span data-stu-id="14529-379">It looks like everything is working.</span></span> <span data-ttu-id="14529-380">У нас появился новый столбец с заданными значениями.</span><span class="sxs-lookup"><span data-stu-id="14529-380">We have the new column with the expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="14529-381">Преобразование значений</span><span class="sxs-lookup"><span data-stu-id="14529-381">Value transformations</span></span>
<span data-ttu-id="14529-382">В этом разделе мы выполним несколько простых преобразований значений в некоторых столбцах таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="14529-382">In this section we will perform some simple transformations on the values in some of the columns of our dataframe.</span></span> <span data-ttu-id="14529-383">Язык R поддерживает практически любые преобразования значений.</span><span class="sxs-lookup"><span data-stu-id="14529-383">The R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="14529-384">В материалах из [Приложения Б. Дополнительные материалы](#appendixb) содержится множество примеров.</span><span class="sxs-lookup"><span data-stu-id="14529-384">The references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="14529-385">Изучив значения в сводках таблиц данных, можно заметить нечто странное.</span><span class="sxs-lookup"><span data-stu-id="14529-385">If you look at the values in the summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="14529-386">Неужели мороженого в Калифорнии производят больше, чем молока?</span><span class="sxs-lookup"><span data-stu-id="14529-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="14529-387">Разумеется, нет. Это просто не имеет смысла — как это ни печально для всех любителей мороженого.</span><span class="sxs-lookup"><span data-stu-id="14529-387">No, of course not, as this makes no sense, sad as this fact may be to some of us ice cream lovers.</span></span> <span data-ttu-id="14529-388">Просто использованы разные единицы измерения.</span><span class="sxs-lookup"><span data-stu-id="14529-388">The units are different.</span></span> <span data-ttu-id="14529-389">Цена привязана к фунтам веса. Количество молока измеряется в миллионах фунтов, мороженого — в тысячах галлонов, а творога — в тысячах фунтов.</span><span class="sxs-lookup"><span data-stu-id="14529-389">The price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="14529-390">Зная, что вес мороженого составляет около 6,5 фунтов на галлон, мы легко преобразуем все значения, чтобы привести их к одной единице измерения — 1000 фунтов.</span><span class="sxs-lookup"><span data-stu-id="14529-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do the multiplication to convert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="14529-391">В нашей модели прогнозирования мы используем мультипликативную модель для корректировки этих данных.</span><span class="sxs-lookup"><span data-stu-id="14529-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="14529-392">Логарифмическое преобразование позволяет использовать линейную модель, что упрощает этот процесс.</span><span class="sxs-lookup"><span data-stu-id="14529-392">A log transformation allows us to use a linear model, simplifying this process.</span></span> <span data-ttu-id="14529-393">Логарифмическое преобразование можно применить в той же функции, в которой применяется множитель.</span><span class="sxs-lookup"><span data-stu-id="14529-393">We can apply the log transformation in the same function where the multiplier is applied.</span></span>

<span data-ttu-id="14529-394">В следующем примере кода я определил новую функцию `log.transform()`и применил ее к строкам, содержащим числовые значения.</span><span class="sxs-lookup"><span data-stu-id="14529-394">In the following code, I define a new function, `log.transform()`, and apply it to the rows containing the numerical values.</span></span> <span data-ttu-id="14529-395">Функция R `Map()` используется для того, чтобы применить функцию `log.transform()` к выбранным столбцам таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="14529-395">The R `Map()` function is used to apply the `log.transform()` function to the selected columns of the dataframe.</span></span> <span data-ttu-id="14529-396">Функция `Map()` сходна с функцией `apply()`, но позволяет добавлять в функцию несколько списков аргументов.</span><span class="sxs-lookup"><span data-stu-id="14529-396">`Map()` is similar to `apply()` but allows for more than one list of arguments to the function.</span></span> <span data-ttu-id="14529-397">Обратите внимание, что список множителей предоставляет второй аргумент функции `log.transform()` .</span><span class="sxs-lookup"><span data-stu-id="14529-397">Note that a list of multipliers supplies the second argument to the `log.transform()` function.</span></span> <span data-ttu-id="14529-398">Функция `na.omit()` используется для очистки, чтобы убедиться, что в таблице данных нет недостающих или неопределенных значений.</span><span class="sxs-lookup"><span data-stu-id="14529-398">The `na.omit()` function is used as a bit of cleanup to ensure we do not have missing or undefined values in the dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for the transformation, which is the log
      ## of the input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments to function log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier to funcition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check the input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap the multiplication in tryCatch
      ## If there is an exception, print the warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply the transformation function to the 4 columns
    ## of the dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="14529-399">Функция `log.transform()` выполняет большую работу.</span><span class="sxs-lookup"><span data-stu-id="14529-399">There is quite a bit happening in the `log.transform()` function.</span></span> <span data-ttu-id="14529-400">Большая часть кода выполняет поиск потенциальных проблем с использованием аргументов или обрабатывает исключения, которые могут возникать во время вычислений.</span><span class="sxs-lookup"><span data-stu-id="14529-400">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="14529-401">Фактически, только несколько строк кода выполняют вычисления.</span><span class="sxs-lookup"><span data-stu-id="14529-401">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="14529-402">Цель такого защищенного программирования — не допустить, чтобы сбой одной функции привел к нарушению всей работы.</span><span class="sxs-lookup"><span data-stu-id="14529-402">The goal of the defensive programming is to prevent the failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="14529-403">Внезапный сбой продолжительного анализа — вещь довольно неприятная.</span><span class="sxs-lookup"><span data-stu-id="14529-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="14529-404">Чтобы избежать этого, необходимо выбрать значения, возвращаемые по умолчанию, что уменьшит возможные негативные последствия.</span><span class="sxs-lookup"><span data-stu-id="14529-404">To avoid this situation, default return values must be chosen that will limit damage to downstream processing.</span></span> <span data-ttu-id="14529-405">Также выдается сообщение, предупреждающее пользователя о проблеме.</span><span class="sxs-lookup"><span data-stu-id="14529-405">A message is also produced to alert users that something has gone wrong.</span></span>

<span data-ttu-id="14529-406">Если вы не знакомы с защищенным программированием на R, понять этот код может быть трудно.</span><span class="sxs-lookup"><span data-stu-id="14529-406">If you are not used to defensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="14529-407">Поясню основные шаги:</span><span class="sxs-lookup"><span data-stu-id="14529-407">I will walk you through the major steps:</span></span>

1. <span data-ttu-id="14529-408">Определяется вектор четырех сообщений.</span><span class="sxs-lookup"><span data-stu-id="14529-408">A vector of four messages is defined.</span></span> <span data-ttu-id="14529-409">Они используются для передачи информации о некоторых потенциальных ошибках и исключениях, которые могут возникнуть при выполнении кода.</span><span class="sxs-lookup"><span data-stu-id="14529-409">These messages are used to communicate information about some of the possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="14529-410">Во всех этих случаях возвращается значение NA (нет данных).</span><span class="sxs-lookup"><span data-stu-id="14529-410">I return a value of NA for each case.</span></span> <span data-ttu-id="14529-411">Есть и другие возможности, у которых может быть меньше побочных эффектов.</span><span class="sxs-lookup"><span data-stu-id="14529-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="14529-412">Например, можно было бы возвращать вектор нулей или вектор исходного входного объекта.</span><span class="sxs-lookup"><span data-stu-id="14529-412">I could return a vector of zeroes, or the original input vector, for example.</span></span>
3. <span data-ttu-id="14529-413">Выполняются проверки аргументов функций.</span><span class="sxs-lookup"><span data-stu-id="14529-413">Checks are run on the arguments to the function.</span></span> <span data-ttu-id="14529-414">В каждом случае при обнаружении ошибки возвращается значение по умолчанию и создается сообщение с помощью функции `warning()`.</span><span class="sxs-lookup"><span data-stu-id="14529-414">In each case, if an error is detected, a default value is returned and a message is produced by the `warning()` function.</span></span> <span data-ttu-id="14529-415">Я использую `warning()`, а не `stop()`, так как последняя функция прерывает выполнение, а именно этого я и хочу избежать.</span><span class="sxs-lookup"><span data-stu-id="14529-415">I am using `warning()` rather than `stop()` as the latter will terminate execution, exactly what I am trying to avoid.</span></span> <span data-ttu-id="14529-416">Обратите внимание, что при написании этого кода я использовал процедуры, поскольку использование функций сделало бы его сложнее и непонятнее.</span><span class="sxs-lookup"><span data-stu-id="14529-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="14529-417">Вычисления журнала выполняются внутри вызова `tryCatch()` , чтобы исключения не привели к внезапному прерыванию обработки.</span><span class="sxs-lookup"><span data-stu-id="14529-417">The log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt to processing.</span></span> <span data-ttu-id="14529-418">Без функции `tryCatch()` большинство ошибок, вызванных функциями R, вызывает сигнал остановки, что приводит именно к прерыванию.</span><span class="sxs-lookup"><span data-stu-id="14529-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="14529-419">Выполните этот код на R в своем эксперименте и просмотрите вывод данных в файле output.log.</span><span class="sxs-lookup"><span data-stu-id="14529-419">Execute this R code in your experiment and have a look at the printed output in the output.log file.</span></span> <span data-ttu-id="14529-420">Преобразованные значения четырех столбцов появятся в журнале (см. рис. 13).</span><span class="sxs-lookup"><span data-stu-id="14529-420">You will now see the transformed values of the four columns in the log, as shown in Figure 13.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="14529-421">*Рис. 13. Сводка преобразованных значений в таблице данных*</span><span class="sxs-lookup"><span data-stu-id="14529-421">*Figure 13. Summary of the transformed values in the dataframe.*</span></span>

<span data-ttu-id="14529-422">Как мы видим, значения изменились.</span><span class="sxs-lookup"><span data-stu-id="14529-422">We see the values have been transformed.</span></span> <span data-ttu-id="14529-423">Теперь производство молока значительно превышает по объемам производство остальных молочных продуктов (не забывайте, что мы используем логарифмическую шкалу).</span><span class="sxs-lookup"><span data-stu-id="14529-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="14529-424">Теперь все наши данные в порядке и мы можем приступать к моделированию.</span><span class="sxs-lookup"><span data-stu-id="14529-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="14529-425">Просмотрев визуализацию вывода данных через порт "Итоговый набор данных" модуля [Выполнить сценарий R][execute-r-script], вы увидите, что тип столбца Month теперь "Категориальный" с 12 уникальными значениями, как мы и хотели.</span><span class="sxs-lookup"><span data-stu-id="14529-425">Looking at the visualization summary for the Result Dataset output of our [Execute R Script][execute-r-script] module, you will see the 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="14529-426"><a id="timeseries"></a>Объекты временного ряда и корреляционный анализ</span><span class="sxs-lookup"><span data-stu-id="14529-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="14529-427">В этом разделе мы исследуем несколько базовых объектов временных рядов R и проанализируем взаимосвязи некоторых переменных.</span><span class="sxs-lookup"><span data-stu-id="14529-427">In this section we will explore a few basic R time series objects and analyze the correlations between some of the variables.</span></span> <span data-ttu-id="14529-428">Наша задача — вывод таблицы данных, содержащей сведения о попарной корреляции с несколькими задержками.</span><span class="sxs-lookup"><span data-stu-id="14529-428">Our goal is to output a dataframe containing the pairwise correlation information at several lags.</span></span>

<span data-ttu-id="14529-429">Полный код на R для этого раздела доступен в ZIP-файле, который вы загрузили ранее.</span><span class="sxs-lookup"><span data-stu-id="14529-429">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="14529-430">Объекты временных рядов в языке R</span><span class="sxs-lookup"><span data-stu-id="14529-430">Time series objects in R</span></span>
<span data-ttu-id="14529-431">Как уже упоминалось, временные ряды представляют собой ряды значений данных, индексированные по времени.</span><span class="sxs-lookup"><span data-stu-id="14529-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="14529-432">Объекты временных рядов на R используются для создания индексов времени и управления ними.</span><span class="sxs-lookup"><span data-stu-id="14529-432">R time series objects are used to create and manage the time index.</span></span> <span data-ttu-id="14529-433">Использование объектов временных рядов имеет несколько преимуществ.</span><span class="sxs-lookup"><span data-stu-id="14529-433">There are several advantages to using time series objects.</span></span> <span data-ttu-id="14529-434">Оно избавляет от необходимости вникать в подробности управления значениями индексов временных рядов, которые уже включены в объект.</span><span class="sxs-lookup"><span data-stu-id="14529-434">Time series objects free you from the many details of managing the time series index values that are encapsulated in the object.</span></span> <span data-ttu-id="14529-435">Кроме того, использование объектов временных рядов позволяет применять многочисленные методы временных рядов для построения диаграмм, моделирования и много другого.</span><span class="sxs-lookup"><span data-stu-id="14529-435">In addition, time series objects allow you to use the many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="14529-436">Класс временных рядов POSIXct довольно распространен и относительно прост.</span><span class="sxs-lookup"><span data-stu-id="14529-436">The POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="14529-437">Этот класс временных рядов измеряет количество времени, прошедшее с начала эры UNIX — 1 января 1970 г.</span><span class="sxs-lookup"><span data-stu-id="14529-437">This time series class measures time from the start of the epoch, January 1, 1970.</span></span> <span data-ttu-id="14529-438">В этом примере мы будем использовать объекты временных рядов POSIXct.</span><span class="sxs-lookup"><span data-stu-id="14529-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="14529-439">Другие распространенные классы объектов временных рядов включают zoo и xts (расширяемые временные ряды).</span><span class="sxs-lookup"><span data-stu-id="14529-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in the references in Section 5.7. [commenting because this section doesn't exist, even in the original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="14529-440">Пример объекта временных рядов</span><span class="sxs-lookup"><span data-stu-id="14529-440">Time series object example</span></span>
<span data-ttu-id="14529-441">Приступим к разбору примера.</span><span class="sxs-lookup"><span data-stu-id="14529-441">Let's get started with our example.</span></span> <span data-ttu-id="14529-442">Перетащим **новый** модуль [Выполнить сценарий R][execute-r-script] в свой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="14529-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="14529-443">Соединим порт вывода "Итоговый набор данных 1" существующего модуля [Выполнить сценарий R][execute-r-script] с портом ввода "Набор данных 1" нового модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-443">Connect the Result Dataset1 output port of the existing [Execute R Script][execute-r-script] module to the Dataset1 input port of the new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="14529-444">Как и в предыдущих случаях, с определенного момента работы над примером я буду показывать только отдельные фрагменты кода на R, которые добавляются на каждом этапе.</span><span class="sxs-lookup"><span data-stu-id="14529-444">As I did for the first examples, as we progress through the example, at some points I will show only the incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-the-dataframe"></a><span data-ttu-id="14529-445">Чтение таблицы данных</span><span class="sxs-lookup"><span data-stu-id="14529-445">Reading the dataframe</span></span>
<span data-ttu-id="14529-446">Для начала давайте считаем таблицу данных и убедимся, что мы получили тот результат, на который рассчитывали.</span><span class="sxs-lookup"><span data-stu-id="14529-446">As a first step, let's read in a dataframe and make sure we get the expected results.</span></span> <span data-ttu-id="14529-447">Эту работу может выполнить следующий код:</span><span class="sxs-lookup"><span data-stu-id="14529-447">The following code should do the job.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check the results

<span data-ttu-id="14529-448">Теперь выполним эксперимент.</span><span class="sxs-lookup"><span data-stu-id="14529-448">Now, run the experiment.</span></span> <span data-ttu-id="14529-449">Журнал новой формы «Выполнение скрипта R» должен выглядеть как на рис. 14.</span><span class="sxs-lookup"><span data-stu-id="14529-449">The log of the new Execute R Script shape should look like Figure 14.</span></span>

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

<span data-ttu-id="14529-450">*Рис. 14. Сводка таблицы данных в модуле «Выполнение сценария R»*</span><span class="sxs-lookup"><span data-stu-id="14529-450">*Figure 14. Summary of the dataframe in the Execute R Script module.*</span></span>

<span data-ttu-id="14529-451">У этих данных ожидаемый тип и формат.</span><span class="sxs-lookup"><span data-stu-id="14529-451">This data is of the expected types and format.</span></span> <span data-ttu-id="14529-452">Тип данных столбца "Месяц" — фактор с верным количеством уровней.</span><span class="sxs-lookup"><span data-stu-id="14529-452">Note that the 'Month' column is of type factor and has the expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="14529-453">Создание объекта временных рядов</span><span class="sxs-lookup"><span data-stu-id="14529-453">Creating a time series object</span></span>
<span data-ttu-id="14529-454">В нашу таблицу данных нужно добавить объект временного ряда.</span><span class="sxs-lookup"><span data-stu-id="14529-454">We need to add a time series object to our dataframe.</span></span> <span data-ttu-id="14529-455">Замените текущий код следующим, добавляющим новый столбец класса POSIXct:</span><span class="sxs-lookup"><span data-stu-id="14529-455">Replace the current code with the following, which adds a new column of class POSIXct.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check the results

<span data-ttu-id="14529-456">Теперь проверьте журнал.</span><span class="sxs-lookup"><span data-stu-id="14529-456">Now, check the log.</span></span> <span data-ttu-id="14529-457">Результат приведен на рисунке 15.</span><span class="sxs-lookup"><span data-stu-id="14529-457">It should look like Figure 15.</span></span>

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

<span data-ttu-id="14529-458">*Рис. 15. Сводка таблицы данных с объектом временных рядов*</span><span class="sxs-lookup"><span data-stu-id="14529-458">*Figure 15. Summary of the dataframe with a time series object.*</span></span>

<span data-ttu-id="14529-459">Как мы видим, действительно появился новый столбец класса POSIXct.</span><span class="sxs-lookup"><span data-stu-id="14529-459">We can see from the summary that the new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-the-data"></a><span data-ttu-id="14529-460">Исследование и преобразование данных</span><span class="sxs-lookup"><span data-stu-id="14529-460">Exploring and transforming the data</span></span>
<span data-ttu-id="14529-461">Рассмотрим некоторые из переменных в этом наборе данных.</span><span class="sxs-lookup"><span data-stu-id="14529-461">Let's explore some of the variables in this dataset.</span></span> <span data-ttu-id="14529-462">Для этого прекрасно подойдет точечная диаграмма.</span><span class="sxs-lookup"><span data-stu-id="14529-462">A scatterplot matrix is a good way to produce a quick look.</span></span> <span data-ttu-id="14529-463">Заменим функцию `str()` в предыдущем фрагменте кода на R следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="14529-463">I am replacing the `str()` function in the previous R code with the following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="14529-464">Выполним этот код и посмотрим на результат.</span><span class="sxs-lookup"><span data-stu-id="14529-464">Run this code and see what happens.</span></span> <span data-ttu-id="14529-465">Диаграмма, полученная через порт "Устройство R", приведена на рисунке 16.</span><span class="sxs-lookup"><span data-stu-id="14529-465">The plot produced at the R Device port should look like Figure 16.</span></span>

![Точечная диаграмма выбранных переменных][17]

<span data-ttu-id="14529-467">*Рис. 16. Матрица точечной диаграммы выбранных переменных*</span><span class="sxs-lookup"><span data-stu-id="14529-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="14529-468">Во взаимосвязях этих переменных можно заметить необычную структуру.</span><span class="sxs-lookup"><span data-stu-id="14529-468">There is some odd-looking structure in the relationships between these variables.</span></span> <span data-ttu-id="14529-469">Возможно, это результат наличия тренда в данных или вызвано тем, что переменные не стандартизованы.</span><span class="sxs-lookup"><span data-stu-id="14529-469">Perhaps this arises from trends in the data and from the fact that we have not standardized the variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="14529-470">Корреляционный анализ</span><span class="sxs-lookup"><span data-stu-id="14529-470">Correlation analysis</span></span>
<span data-ttu-id="14529-471">Для осуществления корреляционного анализа необходимо произвести как вычитание тренда, так и стандартизацию переменных.</span><span class="sxs-lookup"><span data-stu-id="14529-471">To perform correlation analysis we need to both de-trend and standardize the variables.</span></span> <span data-ttu-id="14529-472">Можно просто использовать функцию R `scale()` , которая масштабирует переменные и размещает их по центру.</span><span class="sxs-lookup"><span data-stu-id="14529-472">We could simply use the R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="14529-473">Возможно, это было бы быстрее.</span><span class="sxs-lookup"><span data-stu-id="14529-473">This function might well run faster.</span></span> <span data-ttu-id="14529-474">Однако я хочу продемонстрировать защищенное программирование на R.</span><span class="sxs-lookup"><span data-stu-id="14529-474">However, I want to show you an example of defensive programing in R.</span></span>

<span data-ttu-id="14529-475">Функция `ts.detrend()` , показанная ниже, выполняет обе эти операции.</span><span class="sxs-lookup"><span data-stu-id="14529-475">The `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="14529-476">Следующие две строки кода вычитают тренд из данных и приводят значения к одному стандарту.</span><span class="sxs-lookup"><span data-stu-id="14529-476">The following two lines of code de-trend the data and then standardize the values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function to de-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time to have the same length',
                    'ERROR: ts.detrend requires argument ts to be of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros to return as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # The input arguments are not of the same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If the ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If the ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that the Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend the time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply the detrend.ts function to the variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot the results to look at the relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="14529-477">Функция `ts.detrend()` выполняет большую работу.</span><span class="sxs-lookup"><span data-stu-id="14529-477">There is quite a bit happening in the `ts.detrend()` function.</span></span> <span data-ttu-id="14529-478">Большая часть кода выполняет поиск потенциальных проблем с использованием аргументов или обрабатывает исключения, которые могут возникать во время вычислений.</span><span class="sxs-lookup"><span data-stu-id="14529-478">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="14529-479">Фактически, только несколько строк кода выполняют вычисления.</span><span class="sxs-lookup"><span data-stu-id="14529-479">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="14529-480">Мы уже обсуждали пример защищенного программирования в разделе [Преобразование значений](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="14529-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="14529-481">Оба блока вычислений выполняются внутри функции `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="14529-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="14529-482">Для некоторых ошибок имеет смысл возвращать вектор исходного входного объекта, а в других случаях я возвращаю вектор нулей.</span><span class="sxs-lookup"><span data-stu-id="14529-482">For some errors it makes sense to return the original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="14529-483">Обратите внимание, что линейная регрессия, использующаяся для вычитания тренда, является регрессией временного ряда.</span><span class="sxs-lookup"><span data-stu-id="14529-483">Note that the linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="14529-484">Прогнозирующая переменная — это объект временного ряда.</span><span class="sxs-lookup"><span data-stu-id="14529-484">The predictor variable is a time series object.</span></span>  

<span data-ttu-id="14529-485">Когда функция `ts.detrend()` определена, применим ее к интересующим нас переменным таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="14529-485">Once `ts.detrend()` is defined we apply it to the variables of interest in our dataframe.</span></span> <span data-ttu-id="14529-486">Нужно привести список, созданный функцией `lapply()`, в соответствие с данными таблицы данных с помощью функции `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="14529-486">We must coerce the resulting list created by `lapply()` to data dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="14529-487">Благодаря защищенности `ts.detrend()`сбой обработки одной переменной не помешает обработке остальных.</span><span class="sxs-lookup"><span data-stu-id="14529-487">Because of defensive aspects of `ts.detrend()`, failure to process one of the variables will not prevent correct processing of the others.</span></span>  

<span data-ttu-id="14529-488">Последняя строка кода создает попарную точечную диаграмму.</span><span class="sxs-lookup"><span data-stu-id="14529-488">The final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="14529-489">Точечная диаграмма, полученная в результате выполнения этого кода на R, приведена на рис. 17.</span><span class="sxs-lookup"><span data-stu-id="14529-489">After running the R code, the results of the scatterplot are shown in Figure 17.</span></span>

![Попарная точечная диаграмма после вычитания тренда и стандартизации временных рядов][18]

<span data-ttu-id="14529-491">*Рис. 17. Попарная точечная диаграмма после вычитания тренда и стандартизации временных рядов*</span><span class="sxs-lookup"><span data-stu-id="14529-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="14529-492">Вы можете сравнить эти результаты с приведенными на рис. 16.</span><span class="sxs-lookup"><span data-stu-id="14529-492">You can compare these results to those shown in Figure 16.</span></span> <span data-ttu-id="14529-493">После удаления тренда и стандартизации переменных мы видим, что взаимосвязи переменных гораздо менее структурированы.</span><span class="sxs-lookup"><span data-stu-id="14529-493">With the trend removed and the variables standardized, we see a lot less structure in the relationships between these variables.</span></span>

<span data-ttu-id="14529-494">Код для вычисления корреляций как объектов взаимнокорреляционной функции (CCF-объектов) R следующий:</span><span class="sxs-lookup"><span data-stu-id="14529-494">The code to compute the correlations as R ccf objects is as follows.</span></span>

    ## A function to compute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of the pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute the list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="14529-495">При выполнении этого кода создается журнал, показанный на рис. 18.</span><span class="sxs-lookup"><span data-stu-id="14529-495">Running this code produces the log shown in Figure 18.</span></span>

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

<span data-ttu-id="14529-496">*Рис. 18. Список CCF-объектов после попарного корреляционного анализа*</span><span class="sxs-lookup"><span data-stu-id="14529-496">*Figure 18. List of ccf objects from the pairwise correlation analysis.*</span></span>

<span data-ttu-id="14529-497">Каждой задержке соответствует значение корреляции.</span><span class="sxs-lookup"><span data-stu-id="14529-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="14529-498">Все эти значения корреляции слишком малы, чтобы быть значимыми.</span><span class="sxs-lookup"><span data-stu-id="14529-498">None of these correlation values is large enough to be significant.</span></span> <span data-ttu-id="14529-499">Таким образом, можно заключить, что каждую переменную можно моделировать независимо от других.</span><span class="sxs-lookup"><span data-stu-id="14529-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="14529-500">Вывод таблицы данных</span><span class="sxs-lookup"><span data-stu-id="14529-500">Output a dataframe</span></span>
<span data-ttu-id="14529-501">Мы рассчитали попарные корреляции в виде списка CCF-объектов.</span><span class="sxs-lookup"><span data-stu-id="14529-501">We have computed the pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="14529-502">Это представляет определенные сложности, поскольку порту вывода "Итоговый набор данных" требуется таблица данных на R.</span><span class="sxs-lookup"><span data-stu-id="14529-502">This presents a bit of a problem as the Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="14529-503">Более того, CCF-объект сам по себе является списком, а нас интересуют только значения первого элемента этого списка, корреляции с различными задержками.</span><span class="sxs-lookup"><span data-stu-id="14529-503">Further, the ccf object is itself a list and we want only the values in the first element of this list, the correlations at the various lags.</span></span>

<span data-ttu-id="14529-504">Следующий код извлекает значения задержек из списка CCF-объектов, которые и сами являются списками.</span><span class="sxs-lookup"><span data-stu-id="14529-504">The following code extracts the lag values from the list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with the row names column and the
    ## correlation data frame and assign the column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## The following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="14529-505">Первая строка кода довольно сложная. Возможно, объяснения помогут понять ее.</span><span class="sxs-lookup"><span data-stu-id="14529-505">The first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="14529-506">Проанализируем по порядку, от вложенных операторов к внешним:</span><span class="sxs-lookup"><span data-stu-id="14529-506">Working from the inside out we have the following:</span></span>

1. <span data-ttu-id="14529-507">Оператор **[[** с аргументом **1** выбирает вектор корреляций с задержками из первого элемента списка CCF-объектов.</span><span class="sxs-lookup"><span data-stu-id="14529-507">The '**[[**' operator with the argument '**1**' selects the vector of correlations at the lags from the first element of the ccf object list.</span></span>
2. <span data-ttu-id="14529-508">Функция `do.call()` применяет функцию `rbind()` к элементам списка возвращаемых значений с помощью `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="14529-508">The `do.call()` function applies the `rbind()` function over the elements of the list returns by `lapply()`.</span></span>
3. <span data-ttu-id="14529-509">Функция `data.frame()` относит результаты, полученные от `do.call()`, к таблице данных.</span><span class="sxs-lookup"><span data-stu-id="14529-509">The `data.frame()` function coerces the result produced by `do.call()` to a dataframe.</span></span>

<span data-ttu-id="14529-510">Обратите внимание, что имена строк находятся в столбце таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="14529-510">Note that the row names are in a column of the dataframe.</span></span> <span data-ttu-id="14529-511">Благодаря этому имена строк сохраняются при выводе из модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-511">Doing so preserves the row names when they are output from the [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="14529-512">Результат выполнения кода после применения **визуализации** вывода из порта Result Dataset (Итоговый набор данных) показан на рис. 19.</span><span class="sxs-lookup"><span data-stu-id="14529-512">Running the code produces the output shown in Figure 19 when I **Visualize** the output at the Result Dataset port.</span></span> <span data-ttu-id="14529-513">Имена строк находятся в первом столбце, как и предполагалось.</span><span class="sxs-lookup"><span data-stu-id="14529-513">The row names are in the first column, as intended.</span></span>

![Вывод результатов корреляционного анализа][20]

<span data-ttu-id="14529-515">*Рис. 19. Вывод результатов корреляционного анализа*</span><span class="sxs-lookup"><span data-stu-id="14529-515">*Figure 19. Results output from the correlation analysis.*</span></span>

## <span data-ttu-id="14529-516"><a id="seasonalforecasting"></a>Пример временных рядов: сезонное прогнозирование</span><span class="sxs-lookup"><span data-stu-id="14529-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="14529-517">Сейчас наши данные приведены к виду, удобному для анализа, и мы установили, что между переменными нет значимых корреляций.</span><span class="sxs-lookup"><span data-stu-id="14529-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between the variables.</span></span> <span data-ttu-id="14529-518">Пойдем дальше и создадим прогностическую модель временных рядов.</span><span class="sxs-lookup"><span data-stu-id="14529-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="14529-519">С помощью этой модели мы спрогнозируем производство молока в Калифорнии на 12 месяцев 2013 г.</span><span class="sxs-lookup"><span data-stu-id="14529-519">Using this model we will forecast California milk production for the 12 months of 2013.</span></span>

<span data-ttu-id="14529-520">У нашей прогностической модели будет два компонента: тренд и сезонный компонент.</span><span class="sxs-lookup"><span data-stu-id="14529-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="14529-521">Окончательный прогноз будет произведением этих двух компонентов.</span><span class="sxs-lookup"><span data-stu-id="14529-521">The complete forecast is the product of these two components.</span></span> <span data-ttu-id="14529-522">Модели такого типа называются мультипликативными.</span><span class="sxs-lookup"><span data-stu-id="14529-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="14529-523">Альтернативой является аддитивная модель.</span><span class="sxs-lookup"><span data-stu-id="14529-523">The alternative is an additive model.</span></span> <span data-ttu-id="14529-524">Мы уже применили логарифмическое преобразование к интересующим нас переменным, благодаря чему будет легко обработать результаты анализа.</span><span class="sxs-lookup"><span data-stu-id="14529-524">We have already applied a log transformation to the variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="14529-525">Полный код на R для этого раздела доступен в ZIP-файле, который вы загрузили ранее.</span><span class="sxs-lookup"><span data-stu-id="14529-525">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="creating-the-dataframe-for-analysis"></a><span data-ttu-id="14529-526">Создание таблицы данных для анализа</span><span class="sxs-lookup"><span data-stu-id="14529-526">Creating the dataframe for analysis</span></span>
<span data-ttu-id="14529-527">В первую очередь добавьте в эксперимент **новый** модуль [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="14529-527">Start by adding a **new** [Execute R Script][execute-r-script] module to your experiment.</span></span> <span data-ttu-id="14529-528">Соедините порт вывода **Итоговый набор данных** существующего модуля [Выполнить сценарий R][execute-r-script] с портом ввода **Набор данных 1** нового модуля.</span><span class="sxs-lookup"><span data-stu-id="14529-528">Connect the **Result Dataset** output of the existing [Execute R Script][execute-r-script] module to the **Dataset1** input of the new module.</span></span> <span data-ttu-id="14529-529">Результат изображен на рисунке 20.</span><span class="sxs-lookup"><span data-stu-id="14529-529">The result should look something like Figure 20.</span></span>

![Эксперимент после добавления нового модуля «Выполнение сценария R»][21]

<span data-ttu-id="14529-531">*Рис. 20. Эксперимент после добавления нового модуля «Выполнение сценария R»*</span><span class="sxs-lookup"><span data-stu-id="14529-531">*Figure 20. The experiment with the new Execute R Script module added.*</span></span>

<span data-ttu-id="14529-532">Как и в случае недавно выполненного корреляционного анализа, нужно добавить столбец с объектом временных рядов POSIXct.</span><span class="sxs-lookup"><span data-stu-id="14529-532">As with the correlation analysis we just completed, we need to add a column with a POSIXct time series object.</span></span> <span data-ttu-id="14529-533">Это может выполнить следующий код.</span><span class="sxs-lookup"><span data-stu-id="14529-533">The following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment the first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="14529-534">Выполните этот код и проверьте журнал.</span><span class="sxs-lookup"><span data-stu-id="14529-534">Run this code and look at the log.</span></span> <span data-ttu-id="14529-535">Результат приведен на рисунке 21.</span><span class="sxs-lookup"><span data-stu-id="14529-535">The result should look like Figure 21.</span></span>

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

<span data-ttu-id="14529-536">*Рис. 21. Сводка таблицы данных*</span><span class="sxs-lookup"><span data-stu-id="14529-536">*Figure 21. A summary of the dataframe.*</span></span>

<span data-ttu-id="14529-537">Получив такой результат, мы можем приступить к анализу.</span><span class="sxs-lookup"><span data-stu-id="14529-537">With this result, we are ready to start our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="14529-538">Создание набора данных для обучения</span><span class="sxs-lookup"><span data-stu-id="14529-538">Create a training dataset</span></span>
<span data-ttu-id="14529-539">Имея готовую таблицу данных, нужно создать учебный набор данных.</span><span class="sxs-lookup"><span data-stu-id="14529-539">With the dataframe constructed we need to create a training dataset.</span></span> <span data-ttu-id="14529-540">Эти данные будут включать все наблюдения за исключением последних 12 (за 2013 год), которые станут тестовым набором данных.</span><span class="sxs-lookup"><span data-stu-id="14529-540">This data will include all of the observations except the last 12, of the year 2013, which is our test dataset.</span></span> <span data-ttu-id="14529-541">Приведенный ниже код разбивает таблицу данных на подмножества и создает диаграммы переменных: цены и производства молочных продуктов.</span><span class="sxs-lookup"><span data-stu-id="14529-541">The following code subsets the dataframe and creates plots of the dairy production and price variables.</span></span> <span data-ttu-id="14529-542">Затем создаем диаграммы четырех переменных: цены и производства молочных продуктов.</span><span class="sxs-lookup"><span data-stu-id="14529-542">I then create plots of the four production and price variables.</span></span> <span data-ttu-id="14529-543">Анонимная функция используется для определения приращений диаграммы и последующей итерации для списка оставшихся двух аргументов с помощью `Map()`.</span><span class="sxs-lookup"><span data-stu-id="14529-543">An anonymous function is used to define some augments for plot, and then iterate over the list of the other two arguments with `Map()`.</span></span> <span data-ttu-id="14529-544">Если вам кажется, что здесь пригодилась бы структура for ... loop, вы совершенно правы.</span><span class="sxs-lookup"><span data-stu-id="14529-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="14529-545">Но поскольку язык R оперирует функциями, я продемонстрирую решение с использованием функций.</span><span class="sxs-lookup"><span data-stu-id="14529-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="14529-546">После выполнения кода получаем серию диаграмм временных рядов через порт вывода "Устройство R" (см. рис. 22).</span><span class="sxs-lookup"><span data-stu-id="14529-546">Running the code produces the series of time series plots from the R Device output shown in Figure 22.</span></span> <span data-ttu-id="14529-547">Заметьте, что по оси времени расположены даты. Это приятный бонус при использовании метода построения диаграмм временных рядов.</span><span class="sxs-lookup"><span data-stu-id="14529-547">Note that the time axis is in units of dates, a nice benefit of the time series plot method.</span></span>

![Первая диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Вторая диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Третья диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Четвертая диаграмма временных рядов данных по ценам и производству молочных продуктов в Калифорнии](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="14529-552">*Рис. 22. Диаграммы временных рядов данных по ценам и производству молочных продуктов в Калифорнии*</span><span class="sxs-lookup"><span data-stu-id="14529-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="14529-553">Модель тренда</span><span class="sxs-lookup"><span data-stu-id="14529-553">A trend model</span></span>
<span data-ttu-id="14529-554">Создав объект временных рядов и просмотрев данные, приступим к созданию модели тренда для данных по производству молочных продуктов в Калифорнии.</span><span class="sxs-lookup"><span data-stu-id="14529-554">Having created a time series object and having had a look at the data, let's start to construct a trend model for the California milk production data.</span></span> <span data-ttu-id="14529-555">Для этого можно использовать регрессию временного ряда.</span><span class="sxs-lookup"><span data-stu-id="14529-555">We can do this with a time series regression.</span></span> <span data-ttu-id="14529-556">Но по диаграмме видно, что для точного моделирования наблюдаемого в данных для обучения тренда недостаточно знать только наклон и смещение.</span><span class="sxs-lookup"><span data-stu-id="14529-556">However, it is clear from the plot that we will need more than a slope and intercept to accurately model the observed trend in the training data.</span></span>

<span data-ttu-id="14529-557">Учитывая небольшой объем данных, создадим модель для тренда в RStudio, а затем вырежем результат и вставим его в Машинное обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-557">Given the small scale of the data, I will build the model for trend in RStudio and then cut and paste the resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="14529-558">RStudio предоставляет интерактивную среду для такого рода интерактивного анализа.</span><span class="sxs-lookup"><span data-stu-id="14529-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="14529-559">Для начала попробуем применить полиномиальную регрессию со степенями до 3.</span><span class="sxs-lookup"><span data-stu-id="14529-559">As a first attempt, I will try a polynomial regression with powers up to 3.</span></span> <span data-ttu-id="14529-560">При создании таких моделей существует высокая вероятность образования лжевзаимосвязей.</span><span class="sxs-lookup"><span data-stu-id="14529-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="14529-561">Поэтому лучше не использовать члены со степенями высокого порядка.</span><span class="sxs-lookup"><span data-stu-id="14529-561">Therefore, it is best to avoid high order terms.</span></span> <span data-ttu-id="14529-562">Функция `I()` запрещает интерпретацию содержимого (интерпретирует содержимое «как есть») и позволяет записать интерпретируемую буквально функцию в уравнение регрессии.</span><span class="sxs-lookup"><span data-stu-id="14529-562">The `I()` function inhibits interpretation of the contents (interprets the contents 'as is') and allows you to write a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="14529-563">Это дает следующий результат:</span><span class="sxs-lookup"><span data-stu-id="14529-563">This generates the following.</span></span>

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

<span data-ttu-id="14529-564">По значениям P (Pr(>|t|)) можно видеть, что значением члена со степенью 2 можно пренебречь.</span><span class="sxs-lookup"><span data-stu-id="14529-564">From P values (Pr(>|t|)) in this output, we can see that the squared term may not be significant.</span></span> <span data-ttu-id="14529-565">С помощью функции `update()` изменим эту модель, опустив член со степенью 2.</span><span class="sxs-lookup"><span data-stu-id="14529-565">I will use the `update()` function to modify this model by dropping the squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="14529-566">Это дает следующий результат:</span><span class="sxs-lookup"><span data-stu-id="14529-566">This generates the following.</span></span>

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

<span data-ttu-id="14529-567">Теперь значительно лучше.</span><span class="sxs-lookup"><span data-stu-id="14529-567">This looks better.</span></span> <span data-ttu-id="14529-568">Остались только значимые члены.</span><span class="sxs-lookup"><span data-stu-id="14529-568">All of the terms are significant.</span></span> <span data-ttu-id="14529-569">Однако значение 2e-16 — значение по умолчанию, и ему не стоит придавать большого значения.</span><span class="sxs-lookup"><span data-stu-id="14529-569">However, the 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="14529-570">Для проверки корректности создадим диаграмму временных рядов данных молочного производства Калифорнии с использованием полученной линии тренда.</span><span class="sxs-lookup"><span data-stu-id="14529-570">As a sanity test, let's make a time series plot of the California dairy production data with the trend curve shown.</span></span> <span data-ttu-id="14529-571">Для создания модели и построения диаграммы я добавил приведенный ниже код в модуль [Выполнить сценарий R][execute-r-script] в Машинном обучении Azure (а не RStudio).</span><span class="sxs-lookup"><span data-stu-id="14529-571">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) to create the model and make a plot.</span></span> <span data-ttu-id="14529-572">Результат показан на рис. 23.</span><span class="sxs-lookup"><span data-stu-id="14529-572">The result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Данные молочного производства Калифорнии с моделью тренда](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="14529-574">*Рис. 23. Данные молочного производства Калифорнии с моделью тренда*</span><span class="sxs-lookup"><span data-stu-id="14529-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="14529-575">Как видим, модель тренда идеально соответствует данным.</span><span class="sxs-lookup"><span data-stu-id="14529-575">It looks like the trend model fits the data fairly well.</span></span> <span data-ttu-id="14529-576">Более того, нет никаких признаков чрезмерной детализации вроде случайных колебаний линии модели.</span><span class="sxs-lookup"><span data-stu-id="14529-576">Further, there does not seem to be evidence of over-fitting, such as odd wiggles in the model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="14529-577">Сезонная модель</span><span class="sxs-lookup"><span data-stu-id="14529-577">Seasonal model</span></span>
<span data-ttu-id="14529-578">Получив модель тренда, можно двигаться дальше и добавить сезонные составляющие.</span><span class="sxs-lookup"><span data-stu-id="14529-578">With a trend model in hand, we need to push on and include the seasonal effects.</span></span> <span data-ttu-id="14529-579">Мы используем месяц года в качестве фиктивной переменной линейной модели, чтобы отследить изменения по месяцам.</span><span class="sxs-lookup"><span data-stu-id="14529-579">We will use the month of the year as a dummy variable in the linear model to capture the month-by-month effect.</span></span> <span data-ttu-id="14529-580">Обратите внимание, что при внесении в модель переменных факторов расчет смещения не выполняют.</span><span class="sxs-lookup"><span data-stu-id="14529-580">Note that when you introduce factor variables into a model, the intercept must not be computed.</span></span> <span data-ttu-id="14529-581">Если это сделать, формула будет слишком детализирована, и R проигнорирует один из требуемых факторов, но сохранит определяющий смещение член.</span><span class="sxs-lookup"><span data-stu-id="14529-581">If you do not do this, the formula is over-specified and R will drop one of the desired factors but keep the intercept term.</span></span>

<span data-ttu-id="14529-582">Так как у нас удовлетворительная модель тренда, можно добавить новые члены в существующую модель с помощью функции `update()` .</span><span class="sxs-lookup"><span data-stu-id="14529-582">Since we have a satisfactory trend model we can use the `update()` function to add the new terms to the existing model.</span></span> <span data-ttu-id="14529-583">-1 в формуле обновления удаляет определяющий смещение член.</span><span class="sxs-lookup"><span data-stu-id="14529-583">The -1 in the update formula drops the intercept term.</span></span> <span data-ttu-id="14529-584">Теперь продолжим в RStudio:</span><span class="sxs-lookup"><span data-stu-id="14529-584">Continuing in RStudio for the moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="14529-585">Это дает следующий результат:</span><span class="sxs-lookup"><span data-stu-id="14529-585">This generates the following.</span></span>

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

<span data-ttu-id="14529-586">Мы видим, что в модели отсутствует определяющий смещение член, но есть 12 значимых факторов месяца.</span><span class="sxs-lookup"><span data-stu-id="14529-586">We see that the model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="14529-587">Именно к этому мы и стремились.</span><span class="sxs-lookup"><span data-stu-id="14529-587">This is exactly what we wanted to see.</span></span>

<span data-ttu-id="14529-588">Построим еще одну диаграмму временного ряда данных по молочному производству Калифорнии, чтобы проверить работу модели.</span><span class="sxs-lookup"><span data-stu-id="14529-588">Let's make another time series plot of the California dairy production data to see how well the seasonal model is working.</span></span> <span data-ttu-id="14529-589">Я добавил следующий код в модуль [Выполнить сценарий R][execute-r-script] Машинного обучения Azure, чтобы создать модель и построить диаграмму.</span><span class="sxs-lookup"><span data-stu-id="14529-589">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] to create the model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="14529-590">Диаграмма, полученная в результате выполнения этого кода в Машинном обучении Azure, приведена на рис. 24.</span><span class="sxs-lookup"><span data-stu-id="14529-590">Running this code in Azure Machine Learning produces the plot shown in Figure 24.</span></span>

![Данные молочного производства Калифорнии с моделью, включающей сезонные составляющие](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="14529-592">*Рис. 24. Данные молочного производства Калифорнии с моделью, включающей сезонные составляющие*</span><span class="sxs-lookup"><span data-stu-id="14529-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="14529-593">Соответствие данных на рисунке 24 довольно обнадеживающее.</span><span class="sxs-lookup"><span data-stu-id="14529-593">The fit to the data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="14529-594">И тренд, и сезонная составляющая (в помесячном варианте) выглядят вполне разумно.</span><span class="sxs-lookup"><span data-stu-id="14529-594">Both the trend and the seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="14529-595">В качестве еще одной проверки нашей модели рассмотрим остатки.</span><span class="sxs-lookup"><span data-stu-id="14529-595">As another check on our model, let's have a look at the residuals.</span></span> <span data-ttu-id="14529-596">Приведенный ниже код вычисляет прогнозируемые значения наших двух моделей, вычисляет остатки для сезонной модели и отображает эти остатки для данных для обучения.</span><span class="sxs-lookup"><span data-stu-id="14529-596">The following code computes the predicted values from our two models, computes the residuals for the seasonal model, and then plots these residuals for the training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot the residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="14529-597">Диаграмма остатков приведена на рисунке 25.</span><span class="sxs-lookup"><span data-stu-id="14529-597">The residual plot is shown in Figure 25.</span></span>

![Остатки сезонной модели для данных для обучения](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="14529-599">*Рис. 25. Остатки сезонной модели для данных для обучения*</span><span class="sxs-lookup"><span data-stu-id="14529-599">*Figure 25. Residuals of the seasonal model for the training data.*</span></span>

<span data-ttu-id="14529-600">Выглядит вполне логично.</span><span class="sxs-lookup"><span data-stu-id="14529-600">These residuals look reasonable.</span></span> <span data-ttu-id="14529-601">Определенная структура отсутствует, за исключением влияния экономического спада 2008–2009 годов, который не слишком хорошо отражен в нашей модели.</span><span class="sxs-lookup"><span data-stu-id="14529-601">There is no particular structure, except the effect of the 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="14529-602">Диаграмма на рис. 25 помогает определить любые связанные со временем закономерности в остатках.</span><span class="sxs-lookup"><span data-stu-id="14529-602">The plot shown in Figure 25 is useful for detecting any time-dependent patterns in the residuals.</span></span> <span data-ttu-id="14529-603">Благодаря использованию эксплицитного подхода к вычислению и визуальному представлению остатков они располагаются на диаграмме во временной последовательности.</span><span class="sxs-lookup"><span data-stu-id="14529-603">The explicit approach of computing and plotting the residuals I used places the residuals in time order on the plot.</span></span> <span data-ttu-id="14529-604">Если бы для построения диаграммы использовалось `milk.lm$residuals`, диаграмма не отражала бы зависимость от времени.</span><span class="sxs-lookup"><span data-stu-id="14529-604">If, on the other hand, I had plotted `milk.lm$residuals`, the plot would not have been in time order.</span></span>

<span data-ttu-id="14529-605">Для построения ряда диагностических диаграмм можно также использовать функцию `plot.lm()`.</span><span class="sxs-lookup"><span data-stu-id="14529-605">You can also use `plot.lm()` to produce a series of diagnostic plots.</span></span>

    ## Show the diagnostic plots for the model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="14529-606">Пример ряда диагностических диаграмм, созданных с помощью этого кода, приведен на рис. 26.</span><span class="sxs-lookup"><span data-stu-id="14529-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Первая диагностическая диаграмма для сезонной модели](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Вторая диагностическая диаграмма для сезонной модели](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Третья диагностическая диаграмма для сезонной модели](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Четвертая диагностическая диаграмма для сезонной модели](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="14529-611">*Рис. 26. Диагностические диаграммы для сезонной модели*</span><span class="sxs-lookup"><span data-stu-id="14529-611">*Figure 26. Diagnostic plots for the seasonal model.*</span></span>

<span data-ttu-id="14529-612">На этих диаграммах можно увидеть несколько точек влияния, но они не дают поводов для серьезного беспокойства.</span><span class="sxs-lookup"><span data-stu-id="14529-612">There are a few highly influential points identified in these plots, but nothing to cause great concern.</span></span> <span data-ttu-id="14529-613">Более того, на графике Q-Q видно, что распределение остатков близко к нормальному, что важно для линейных моделей.</span><span class="sxs-lookup"><span data-stu-id="14529-613">Further, we can see from the Normal Q-Q plot that the residuals are close to normally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="14529-614">Прогнозирование и оценка моделей</span><span class="sxs-lookup"><span data-stu-id="14529-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="14529-615">Остался последний шаг до завершения работы.</span><span class="sxs-lookup"><span data-stu-id="14529-615">There is just one more thing to do to complete our example.</span></span> <span data-ttu-id="14529-616">Необходимо рассчитать прогнозы и измерить их отклонения от фактических данных.</span><span class="sxs-lookup"><span data-stu-id="14529-616">We need to compute forecasts and measure the error against the actual data.</span></span> <span data-ttu-id="14529-617">Составим прогноз на 12 месяцев 2013 года.</span><span class="sxs-lookup"><span data-stu-id="14529-617">Our forecast will be for the 12 months of 2013.</span></span> <span data-ttu-id="14529-618">Можно рассчитать величину отклонений для этого прогноза по отношению к фактическим данным, не входящим в наш набор данных для обучения.</span><span class="sxs-lookup"><span data-stu-id="14529-618">We can compute an error measure for this forecast to the actual data that is not part of our training dataset.</span></span> <span data-ttu-id="14529-619">Кроме того, можно сравнить эффективность, используя учебные данные за 18 лет и тестовые данные за 12 месяцев.</span><span class="sxs-lookup"><span data-stu-id="14529-619">Additionally, we can compare performance on the 18 years of training data to the 12 months of test data.</span></span>  

<span data-ttu-id="14529-620">Для измерения эффективности моделей временных рядов используется несколько показателей.</span><span class="sxs-lookup"><span data-stu-id="14529-620">A number of metrics are used to measure the performance of time series models.</span></span> <span data-ttu-id="14529-621">В нашем случае мы используем среднеквадратическое отклонение.</span><span class="sxs-lookup"><span data-stu-id="14529-621">In our case we will use the root mean square (RMS) error.</span></span> <span data-ttu-id="14529-622">Следующая функция вычисляет среднеквадратическое отклонение между двумя рядами.</span><span class="sxs-lookup"><span data-stu-id="14529-622">The following function computes the RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function to compute the RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments to function RMS.error of wrong type encountered",
                    "ERROR: Input vector to function RMS.error is too short",
                    "ERROR: Input vectors to function RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check the arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate the values, else just copy
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

    ## Compute the RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="14529-623">Как и в случае с функцией `log.transform()` , которую мы рассматривали в разделе «Преобразование значений», значительная часть кода данной функции занимается проверкой и обработкой исключений.</span><span class="sxs-lookup"><span data-stu-id="14529-623">As with the `log.transform()` function we discussed in the "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="14529-624">Задействованы те же принципы.</span><span class="sxs-lookup"><span data-stu-id="14529-624">The principles employed are the same.</span></span> <span data-ttu-id="14529-625">Работа выполняется двумя фрагментами кода внутри функций `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="14529-625">The work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="14529-626">В первом фрагменте временные ряды возводятся в степень, поскольку до этого мы работали с логарифмами значений.</span><span class="sxs-lookup"><span data-stu-id="14529-626">First, the time series are exponentiated, since we have been working with the logs of the values.</span></span> <span data-ttu-id="14529-627">Во втором фрагменте вычисляется фактическое среднеквадратическое отклонение.</span><span class="sxs-lookup"><span data-stu-id="14529-627">Second, the actual RMS error is computed.</span></span>  

<span data-ttu-id="14529-628">Вооружившись функцией для измерения среднеквадратического отклонения, построим и выведем таблицу данных с отклонениями.</span><span class="sxs-lookup"><span data-stu-id="14529-628">Equipped with a function to measure the RMS error, let's build and output a dataframe containing the RMS errors.</span></span> <span data-ttu-id="14529-629">Введем только члены для модели тренда и полную модель с сезонными факторами.</span><span class="sxs-lookup"><span data-stu-id="14529-629">We will include terms for the trend model alone and the complete model with seasonal factors.</span></span> <span data-ttu-id="14529-630">Приведенный ниже код выполнит эту задачу с помощью двух линейных моделей, созданных ранее.</span><span class="sxs-lookup"><span data-stu-id="14529-630">The following code does the job by using the two linear models we have constructed.</span></span>

    ## Compute the RMS error in a dataframe
    ## Include the row names in the first column so they will
    ## appear in the output of the Execute R Script
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

    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="14529-631">Результат выполнения этого кода, выведенный через порт "Итоговый набор данных", приведен на рисунке 27</span><span class="sxs-lookup"><span data-stu-id="14529-631">Running this code produces the output shown in Figure 27 at the Result Dataset output port.</span></span>

![Сравнение среднеквадратического отклонения для моделей][26]

<span data-ttu-id="14529-633">*Рис. 27. Сравнение среднеквадратического отклонения для моделей*</span><span class="sxs-lookup"><span data-stu-id="14529-633">*Figure 27. Comparison of RMS errors for the models.*</span></span>

<span data-ttu-id="14529-634">Как видно по этим результатам, после добавления к модели сезонных факторов среднеквадратическое отклонение значительно уменьшилось.</span><span class="sxs-lookup"><span data-stu-id="14529-634">From these results, we see that adding the seasonal factors to the model reduces the RMS error significantly.</span></span> <span data-ttu-id="14529-635">Вполне ожидаемо, что отклонение для учебных данных чуть меньше, чем для прогноза.</span><span class="sxs-lookup"><span data-stu-id="14529-635">Not too surprisingly, the RMS error for the training data is a bit less than for the forecast.</span></span>

## <span data-ttu-id="14529-636"><a id="appendixa"></a>ПРИЛОЖЕНИЕ А. Руководство по RStudio</span><span class="sxs-lookup"><span data-stu-id="14529-636"><a id="appendixa"></a>APPENDIX A: Guide to RStudio</span></span>
<span data-ttu-id="14529-637">Среда разработки RStudio хорошо описана, поэтому в данном приложении приведены некоторые ссылки на ключевые разделы документации по RStudio, которые помогут вам приступить к работе</span><span class="sxs-lookup"><span data-stu-id="14529-637">RStudio is quite well documented, so in this appendix I will provide some links to the key sections of the RStudio documentation to get you started.</span></span>

1. <span data-ttu-id="14529-638">Создание проектов</span><span class="sxs-lookup"><span data-stu-id="14529-638">Creating projects</span></span>
   
   <span data-ttu-id="14529-639">С помощью RStudio можно организовывать свой код на R в проекты и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="14529-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="14529-640">Документацию по использованию проектов можно найти по адресу https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="14529-640">The documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="14529-641">Рекомендую следовать этим инструкциям и создать проект для примеров кода на R, приведенных в данном документе.</span><span class="sxs-lookup"><span data-stu-id="14529-641">I recommend that you follow these directions and create a project for the R code examples in this document.</span></span>  
2. <span data-ttu-id="14529-642">Изменение и выполнение кода на R</span><span class="sxs-lookup"><span data-stu-id="14529-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="14529-643">RStudio предоставляет интегрированную среду для изменения и выполнения кода на R.</span><span class="sxs-lookup"><span data-stu-id="14529-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="14529-644">Документацию можно найти по адресу https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="14529-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="14529-645">Отладка</span><span class="sxs-lookup"><span data-stu-id="14529-645">Debugging</span></span>
   
   <span data-ttu-id="14529-646">RStudio располагает эффективными возможностями отладки.</span><span class="sxs-lookup"><span data-stu-id="14529-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="14529-647">Документацию по этим функциям можно найти по адресу https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="14529-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="14529-648">Функции устранения ошибок точек останова описаны в документе по адресу https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="14529-648">The breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="14529-649"><a id="appendixb"></a>ПРИЛОЖЕНИЕ Б. Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="14529-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="14529-650">В этом руководстве по программированию на языке R описываются основные компоненты, которые нужны для использования языка R со Студией машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="14529-650">This R programming tutorial covers the basics of what you need to use the R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="14529-651">Если вы еще не знакомы с языком R, на ресурсе CRAN можно найти два вводных курса:</span><span class="sxs-lookup"><span data-stu-id="14529-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="14529-652">"R для начинающих" Эммануэля Паради (Emmanuel Paradis) — замечательный учебник для начала работы, который доступен по адресу http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf;</span><span class="sxs-lookup"><span data-stu-id="14529-652">R for Beginners by Emmanuel Paradis is a good place to start at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="14529-653">"Введение в язык R" В. Н.</span><span class="sxs-lookup"><span data-stu-id="14529-653">An Introduction to R by W. N.</span></span> <span data-ttu-id="14529-654">Венаблес (W. N. Venables)</span><span class="sxs-lookup"><span data-stu-id="14529-654">Venables et.</span></span> <span data-ttu-id="14529-655">и др. —</span><span class="sxs-lookup"><span data-stu-id="14529-655">al.</span></span> <span data-ttu-id="14529-656">немного более углубленный курс, доступный по адресу http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="14529-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="14529-657">По языку R написано много книг, которые могут помочь в его освоении.</span><span class="sxs-lookup"><span data-stu-id="14529-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="14529-658">Вот некоторые из них, которые показались мне наиболее полезными:</span><span class="sxs-lookup"><span data-stu-id="14529-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="14529-659">Книга Нормана Мэтлофа (Norman Matloff) The Art of R Programming: A Tour of Statistical Software Design — хороший пример введения в программирование на R.</span><span class="sxs-lookup"><span data-stu-id="14529-659">The Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction to programming in R.</span></span>  
* <span data-ttu-id="14529-660">Книга Пола Титора (Paul Teetor) R Cookbook содержит проблемы и их решение на R.</span><span class="sxs-lookup"><span data-stu-id="14529-660">R Cookbook by Paul Teetor provides a problem and solution approach to using R.</span></span>  
* <span data-ttu-id="14529-661">«R в действии» Роберта Кабакова (Robert Kabacoff) — еще одна полезная книга.</span><span class="sxs-lookup"><span data-stu-id="14529-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="14529-662">Веб-сайт Quick R — полезный ресурс по адресу http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="14529-662">The companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="14529-663">В книге R Inferno (Адский язык R) Патрика Бернса (Patrick Burns), написанной в неожиданно юмористическом ключе, рассматриваются сложные проблемы, с которыми можно столкнуться при программировании на R. Книгу можно скачать бесплатно по адресу http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="14529-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. The book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="14529-664">Если вы хотите углубиться в сложные темы языка R, почитайте новую книгу Хэдли Викхема (Hadley Wickham) Advanced R.</span><span class="sxs-lookup"><span data-stu-id="14529-664">If you want a deep dive into advanced topics in R, have a look at the book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="14529-665">Электронную версию этой книги можно найти по адресу http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="14529-665">The online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="14529-666">В разделе Task View (Представление задач) ресурса CRAN можно найти каталог пакетов временных рядов на R для анализа временных рядов: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="14529-666">A catalogue of R time series packages can be found in the CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="14529-667">Информацию по определенным пакетам объектов временных рядов см. в документации к этим пакетам.</span><span class="sxs-lookup"><span data-stu-id="14529-667">For information on specific time series object packages, you should refer to the documentation for that package.</span></span>

<span data-ttu-id="14529-668">Книга Introductory Time Series with R Пола Каупертвейта (Paul Cowpertwait) и Эндрю Меткалфа (Andrew Metcalfe) представляет собой введение в использование языка R для анализа временных рядов.</span><span class="sxs-lookup"><span data-stu-id="14529-668">The book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction to using R for time series analysis.</span></span> <span data-ttu-id="14529-669">Множество других теоретических работ содержат примеры на языке R.</span><span class="sxs-lookup"><span data-stu-id="14529-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="14529-670">Некоторые полезные ресурсы в Интернете:</span><span class="sxs-lookup"><span data-stu-id="14529-670">Some great internet resources:</span></span>

* <span data-ttu-id="14529-671">DataCamp — на сайте DataCamp обучение R происходит в вашем браузере с помощью видеозанятий и упражнений по кодированию.</span><span class="sxs-lookup"><span data-stu-id="14529-671">DataCamp: DataCamp teaches R in the comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="14529-672">Здесь представлены интерактивные учебники по последним методам кодирования на R и пакетам R.</span><span class="sxs-lookup"><span data-stu-id="14529-672">There are interactive tutorials on the latest R techniques and packages.</span></span> <span data-ttu-id="14529-673">Пройдите бесплатный интерактивный курс по языку R на странице https://www.datacamp.com/courses/introduction-to-r.</span><span class="sxs-lookup"><span data-stu-id="14529-673">Take the free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="14529-674">Руководство по началу работы с R из Programiz: https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="14529-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="14529-675">Краткое руководство по R от Келли Блэк (Kelly Black) из университета Кларксон по адресу http://www.cyclismo.org/tutorial/R/.</span><span class="sxs-lookup"><span data-stu-id="14529-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="14529-676">Ссылки на более чем 60 ресурсов по R: http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html.</span><span class="sxs-lookup"><span data-stu-id="14529-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

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
