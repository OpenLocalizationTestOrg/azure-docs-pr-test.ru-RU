---
title: "Создание пользовательских R-модулей в Машинном обучении Azure | Документация Майкрософт"
description: "Краткое руководство по созданию пользовательских R-модулей в Машинном обучении Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 964ddb551a475243891abce8a2b835e65569a4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="2492b-103">Создание пользовательских R-модулей в Машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="2492b-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="2492b-104">В этой статье описывается процедура создания и развертывания пользовательского R-модуля в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="2492b-104">This topic describes how to author and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="2492b-105">Здесь поясняется, что такое пользовательский R-модуль, и какие файлы используются для его создания.</span><span class="sxs-lookup"><span data-stu-id="2492b-105">It explains what custom R modules are and what files are used to define them.</span></span> <span data-ttu-id="2492b-106">В этом разделе также описан способ создания файлов, определяющих модуль, и регистрации модуля для его развертывания в рабочей области Машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="2492b-106">It illustrates how to construct the files that define a module and how to register the module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="2492b-107">Затем более подробно описываются элементы и атрибуты, используемые в определении пользовательского модуля.</span><span class="sxs-lookup"><span data-stu-id="2492b-107">The elements and attributes used in the definition of the custom module are then described in more detail.</span></span> <span data-ttu-id="2492b-108">Кроме этого, здесь рассматриваются способы использования дополнительных функций, файлов и нескольких наборов выходных данных.</span><span class="sxs-lookup"><span data-stu-id="2492b-108">How to use auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="2492b-109">Что такое пользовательский R-модуль?</span><span class="sxs-lookup"><span data-stu-id="2492b-109">What is a custom R module?</span></span>
<span data-ttu-id="2492b-110">**Пользовательский модуль** — это определяемый пользователем модуль, который можно передать в свою рабочую область и выполнить в рамках эксперимента Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2492b-110">A **custom module** is a user-defined module that can be uploaded to your workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="2492b-111">**Пользовательский R-модуль** представляет собой настраиваемый модуль, который выполняет определяемую пользователем R-функцию.</span><span class="sxs-lookup"><span data-stu-id="2492b-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="2492b-112">**R** — это язык программирования, предназначенный для статистических вычислений и работы с графикой. Его широко используют специалисты по статистике, а также обработке и анализу данных для реализации алгоритмов.</span><span class="sxs-lookup"><span data-stu-id="2492b-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="2492b-113">В настоящее время R — это единственный язык, поддерживаемый в пользовательских модулях, но в следующих выпусках планируется добавить поддержку и других языков.</span><span class="sxs-lookup"><span data-stu-id="2492b-113">Currently, R is the only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="2492b-114">Пользовательские модули принадлежат к **группе первоклассных модулей** в Машинном обучении Azure в том смысле, что их можно использовать наравне с любым другим модулем.</span><span class="sxs-lookup"><span data-stu-id="2492b-114">Custom modules have **first-class status** in Azure Machine Learning in the sense that they can be used just like any other module.</span></span> <span data-ttu-id="2492b-115">Их можно выполнять с другими модулями, включенными в опубликованный эксперимент или визуализации.</span><span class="sxs-lookup"><span data-stu-id="2492b-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="2492b-116">Вы можете управлять алгоритмом, реализуемым модулем, используемыми портами ввода и вывода, параметрами моделирования и другими параметрами, определяющими поведение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2492b-116">You have control over the algorithm implemented by the module, the input and output ports to be used, the modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="2492b-117">Эксперимент, содержащий пользовательские модули, также можно опубликовать в коллекции Cortana Intelligence, чтобы упростить совместное использование.</span><span class="sxs-lookup"><span data-stu-id="2492b-117">An experiment that contains custom modules can also be published into the Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="2492b-118">Файлы в пользовательском R-модуле</span><span class="sxs-lookup"><span data-stu-id="2492b-118">Files in a custom R module</span></span>
<span data-ttu-id="2492b-119">Пользовательский R-модуль создается на основе ZIP-файла, содержащего как минимум два файла:</span><span class="sxs-lookup"><span data-stu-id="2492b-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="2492b-120">**исходный файл** , который реализует R-функцию, предоставляемую модулем;</span><span class="sxs-lookup"><span data-stu-id="2492b-120">A **source file** that implements the R function exposed by the module</span></span>
* <span data-ttu-id="2492b-121">**XML-файл определения** , описывающий интерфейс пользовательского модуля.</span><span class="sxs-lookup"><span data-stu-id="2492b-121">An **XML definition file** that describes the custom module interface</span></span>

<span data-ttu-id="2492b-122">В ZIP-файл также можно включить дополнительные вспомогательные файлы, обеспечивающие функциональные возможности, доступ к которым можно получить из пользовательского модуля.</span><span class="sxs-lookup"><span data-stu-id="2492b-122">Additional auxiliary files can also be included in the .zip file that provides functionality that can be accessed from the custom module.</span></span> <span data-ttu-id="2492b-123">Эта возможность описана в подразделе **Аргументы** в справочном разделе **Элементы в XML-файле определения** после примера быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="2492b-123">This option is discussed in the **Arguments** part of the reference section **Elements in the XML definition file** following the quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="2492b-124">Пример быстрого запуска: определение, создание пакета и регистрация пользовательского R-модуля</span><span class="sxs-lookup"><span data-stu-id="2492b-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="2492b-125">В этом примере показано, как создать файлы, необходимые для пользовательского R-модуля, упаковать их в ZIP-файл и затем зарегистрировать модуль в рабочей области Машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="2492b-125">This example illustrates how to construct the files required by a custom R module, package them into a zip file, and then register the module in your Machine Learning workspace.</span></span> <span data-ttu-id="2492b-126">Пример ZIP-пакета и файлов можно скачать на странице [скачивания файла CustomAddRows.zip](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="2492b-126">The example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="the-source-file"></a><span data-ttu-id="2492b-127">Исходный файл</span><span class="sxs-lookup"><span data-stu-id="2492b-127">The source file</span></span>
<span data-ttu-id="2492b-128">Рассмотрим пример модуля **Custom Add Rows** (Добавление пользовательских строк), который изменяет стандартную реализацию модуля **Add Rows** (Добавление строк), используемого для объединения строк (наблюдений) из двух наборов данных (кадров данных).</span><span class="sxs-lookup"><span data-stu-id="2492b-128">Consider the example of a **Custom Add Rows** module that modifies the standard implementation of the **Add Rows** module used to concatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="2492b-129">Стандартный модуль **Add Rows** (Добавление строк) добавляет строки второго входного набора данных в конец первого входного набора данных, используя алгоритм `rbind`.</span><span class="sxs-lookup"><span data-stu-id="2492b-129">The standard **Add Rows** module appends the rows of the second input dataset to the end of the first input dataset using the `rbind` algorithm.</span></span> <span data-ttu-id="2492b-130">Настраиваемая функция `CustomAddRows` подобным образом принимает в качестве входных данных два набора данных, а также дополнительный логический параметр переноса значений.</span><span class="sxs-lookup"><span data-stu-id="2492b-130">The customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="2492b-131">Если для параметра переноса задано значение **FALSE**, она возвращает тот же набор данных, что и при стандартной реализации.</span><span class="sxs-lookup"><span data-stu-id="2492b-131">If the swap parameter is set to **FALSE**, it returns the same data set as the standard implementation.</span></span> <span data-ttu-id="2492b-132">Если же для параметра переноса задано значение **TRUE**, функция добавляет строки из первого входного набора данных в конец второго набора данных.</span><span class="sxs-lookup"><span data-stu-id="2492b-132">But if the swap parameter is **TRUE**, the function appends rows of first input dataset to the end of the second dataset instead.</span></span> <span data-ttu-id="2492b-133">Файл CustomAddRows.R, содержащий реализацию функции R `CustomAddRows` , предоставляемой модулем **Добавление пользовательских строк** , содержит следующий код на языке R.</span><span class="sxs-lookup"><span data-stu-id="2492b-133">The CustomAddRows.R file that contains the implementation of the R `CustomAddRows` function exposed by the **Custom Add Rows** module has the following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="the-xml-definition-file"></a><span data-ttu-id="2492b-134">XML-файл определения</span><span class="sxs-lookup"><span data-stu-id="2492b-134">The XML definition file</span></span>
<span data-ttu-id="2492b-135">Чтобы предоставить данную `CustomAddRows` функцию как модуль Машинного обучения Azure, необходимо создать XML-файл определения, чтобы задать вид и поведение модуля **Добавление пользовательских строк** .</span><span class="sxs-lookup"><span data-stu-id="2492b-135">To expose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created to specify how the **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another. Dataset 2 is concatenated to Dataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify the base language, script file and R function to use for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: The values of the id attributes in the Input and Arg elements must match the parameter names in the R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>The combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="2492b-136">Обратите внимание, что значение атрибутов **id** элементов **Input** и **Arg** в XML-файле должно ПОЛНОСТЬЮ совпадать с именами параметров функций кода R в файле CustomAddRows.R (в данном примере это *dataset1*, *dataset2* и *swap*).</span><span class="sxs-lookup"><span data-stu-id="2492b-136">It is critical to note that the value of the **id** attributes of the **Input** and **Arg** elements in the XML file must match the function parameter names of the R code in the CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in the example).</span></span> <span data-ttu-id="2492b-137">Аналогичным образом значение атрибута **entryPoint** элемента **Language** должно ПОЛНОСТЬЮ соответствовать имени функции в R-скрипте (в данном примере это *CustomAddRows*).</span><span class="sxs-lookup"><span data-stu-id="2492b-137">Similarly, the value of the **entryPoint** attribute of the **Language** element must match the name of the function in the R script EXACTLY: (*CustomAddRows* in the example).</span></span> 

<span data-ttu-id="2492b-138">И наоборот, атрибут **id** элемента **Output** не соответствует каким-либо переменным в R-скрипте.</span><span class="sxs-lookup"><span data-stu-id="2492b-138">In contrast, the **id** attribute for the **Output** element does not correspond to any variables in the R script.</span></span> <span data-ttu-id="2492b-139">Если требуется несколько наборов выходных данных, следует просто вернуть список из функции R с результатами, размещенными *в том же порядке* , в котором **выходные данные** заявлены в XML-файле.</span><span class="sxs-lookup"><span data-stu-id="2492b-139">When more than one output is required, simply return a list from the R function with results placed *in the same order* as **Outputs** elements are declared in the XML file.</span></span>

### <a name="package-and-register-the-module"></a><span data-ttu-id="2492b-140">Создание пакета и регистрация модуля</span><span class="sxs-lookup"><span data-stu-id="2492b-140">Package and register the module</span></span>
<span data-ttu-id="2492b-141">Сохраните эти два файла как *CustomAddRows.R* и *CustomAddRows.xml*, а затем поместите их в архивный файл *CustomAddRows.zip*.</span><span class="sxs-lookup"><span data-stu-id="2492b-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip the two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="2492b-142">Чтобы зарегистрировать их в рабочей области машинного обучения, перейдите в свою рабочую область в Студии машинного обучения, нажмите кнопку **+Создать** в нижней части страницы и выберите **Модуль -> From zip package** (Из ZIP-пакета), чтобы передать новый пользовательский модуль **Custom Add Rows** (Добавление пользовательских строк).</span><span class="sxs-lookup"><span data-stu-id="2492b-142">To register them in your Machine Learning workspace, go to your workspace in the Machine Learning Studio, click the **+NEW** button on the bottom and choose **MODULE -> FROM ZIP PACKAGE** to upload the new **Custom Add Rows** module.</span></span>

![Передача ZIP-файла](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="2492b-144">Теперь модуль **Добавление пользовательских строк** доступен из экспериментов Машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="2492b-144">The **Custom Add Rows** module is now ready to be accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-the-xml-definition-file"></a><span data-ttu-id="2492b-145">Элементы в XML-файле определения</span><span class="sxs-lookup"><span data-stu-id="2492b-145">Elements in the XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="2492b-146">Элементы «Модуль»</span><span class="sxs-lookup"><span data-stu-id="2492b-146">Module elements</span></span>
<span data-ttu-id="2492b-147">Элемент **Модуль** используется для определения пользовательского модуля в XML-файле.</span><span class="sxs-lookup"><span data-stu-id="2492b-147">The **Module** element is used to define a custom module in the XML file.</span></span> <span data-ttu-id="2492b-148">С помощью нескольких элементов **модуль** в одном XML-файле можно определить несколько модулей.</span><span class="sxs-lookup"><span data-stu-id="2492b-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="2492b-149">Каждый модуль в рабочей области должен иметь уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="2492b-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="2492b-150">Если зарегистрировать пользовательский модуль с таким же именем, как у имеющегося пользовательского модуля, существующий модуль заменится на новый.</span><span class="sxs-lookup"><span data-stu-id="2492b-150">Register a custom module with the same name as an existing custom module and it replaces the existing module with the new one.</span></span> <span data-ttu-id="2492b-151">При этом пользовательский модуль можно зарегистрировать с таким же именем, как у имеющегося модуля машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2492b-151">Custom modules can, however, be registered with the same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="2492b-152">Он появится в категории **пользовательских** на палитре модулей.</span><span class="sxs-lookup"><span data-stu-id="2492b-152">If so, they appear in the **Custom** category of the module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another...</Description>/> 


<span data-ttu-id="2492b-153">В элементе **Module** можно указать два дополнительных необязательных элемента:</span><span class="sxs-lookup"><span data-stu-id="2492b-153">Within the **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="2492b-154">элемент **Owner** , внедренный в модуль;</span><span class="sxs-lookup"><span data-stu-id="2492b-154">an **Owner** element that is embedded into the module</span></span>  
* <span data-ttu-id="2492b-155">элемент **Description** , содержащий текст, отображающийся в экспресс-справке для модуля и при наведении на модуль в пользовательском интерфейсе машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="2492b-155">a **Description** element that contains text that is displayed in quick help for the module and when you hover over the module in the Machine Learning UI.</span></span>

<span data-ttu-id="2492b-156">Правила по ограничению количества символов в элементах Module:</span><span class="sxs-lookup"><span data-stu-id="2492b-156">Rules for characters limits in the Module elements:</span></span>

* <span data-ttu-id="2492b-157">Значение атрибута **name** в элементе **Module** не должно превышать 64 символа.</span><span class="sxs-lookup"><span data-stu-id="2492b-157">The value of the **name** attribute in the **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="2492b-158">Содержимое элемента **Описание** не должно превышать 128 символов.</span><span class="sxs-lookup"><span data-stu-id="2492b-158">The content of the **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="2492b-159">Содержимое элемента **Владелец** не должно превышать 32 символа.</span><span class="sxs-lookup"><span data-stu-id="2492b-159">The content of the **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="2492b-160">Результаты модуля могут быть детерминированными или недетерминированными.** По умолчанию все модули считаются детерминированными.</span><span class="sxs-lookup"><span data-stu-id="2492b-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered to be deterministic.</span></span> <span data-ttu-id="2492b-161">Другими словами, при прочих равных входных параметрах и данных модуль должен выдать одни и те же результаты при каждом выполнении.</span><span class="sxs-lookup"><span data-stu-id="2492b-161">That is, given an unchanging set of input parameters and data, the module should return the same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="2492b-162">Это означает, что Студия машинного обучения Azure повторяет выполнение только модулей, помеченных как детерминированные, если параметр или входные данные были изменены.</span><span class="sxs-lookup"><span data-stu-id="2492b-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or the input data has changed.</span></span> <span data-ttu-id="2492b-163">При возвращении кэшированных результатов эксперименты можно проводить гораздо быстрее.</span><span class="sxs-lookup"><span data-stu-id="2492b-163">Returning the cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="2492b-164">Существуют недетерминированные функции, например RAND или функция, возвращающая текущую дату и время.</span><span class="sxs-lookup"><span data-stu-id="2492b-164">There are functions that are nondeterministic, such as RAND or a function that returns the current date or time.</span></span> <span data-ttu-id="2492b-165">Если в модуле используется недетерминированная функция, можно указать, что модуль является недетерминированным, установив для необязательного атрибута **isDeterministic** значение **false**.</span><span class="sxs-lookup"><span data-stu-id="2492b-165">If your module uses a nondeterministic function, you can specify that the module is non-deterministic by setting the optional **isDeterministic** attribute to **FALSE**.</span></span> <span data-ttu-id="2492b-166">Таким образом модуль будет выполняться повторно при каждом выполнении эксперимента, даже если входные данные и параметры модуля не менялись.</span><span class="sxs-lookup"><span data-stu-id="2492b-166">This insures that the module is rerun whenever the experiment is run, even if the module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="2492b-167">Определение языка</span><span class="sxs-lookup"><span data-stu-id="2492b-167">Language Definition</span></span>
<span data-ttu-id="2492b-168">Элемент **Language** в XML-файле определения используется для указания языка пользовательского модуля.</span><span class="sxs-lookup"><span data-stu-id="2492b-168">The **Language** element in your XML definition file is used to specify the custom module language.</span></span> <span data-ttu-id="2492b-169">В настоящее время R — единственный поддерживаемый язык.</span><span class="sxs-lookup"><span data-stu-id="2492b-169">Currently, R is the only supported language.</span></span> <span data-ttu-id="2492b-170">Значением атрибута **sourceFile** должно быть имя R-файла, который содержит функции вызова при выполнении модуля.</span><span class="sxs-lookup"><span data-stu-id="2492b-170">The value of the **sourceFile** attribute must be the name of the R file that contains the function to call when the module is run.</span></span> <span data-ttu-id="2492b-171">Этот файл должен быть в составе ZIP-пакета.</span><span class="sxs-lookup"><span data-stu-id="2492b-171">This file must be part of the zip package.</span></span> <span data-ttu-id="2492b-172">Значением атрибута **entryPoint** является имя вызываемой функции. Оно должно совпадать с допустимой функцией, определенной в исходном файле.</span><span class="sxs-lookup"><span data-stu-id="2492b-172">The value of the **entryPoint** attribute is the name of the function being called and must match a valid function defined with in the source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="2492b-173">порты;</span><span class="sxs-lookup"><span data-stu-id="2492b-173">Ports</span></span>
<span data-ttu-id="2492b-174">Входные и выходные порты для пользовательского модуля указываются в дочерних элементах раздела **Порты** в XML-файле определения.</span><span class="sxs-lookup"><span data-stu-id="2492b-174">The input and output ports for a custom module are specified in child elements of the **Ports** section of the XML definition file.</span></span> <span data-ttu-id="2492b-175">От того, в каком порядке заданы эти элементы, зависит структура (UX), которая будет отображаться для пользователей.</span><span class="sxs-lookup"><span data-stu-id="2492b-175">The order of these elements determines the layout experienced (UX) by users.</span></span> <span data-ttu-id="2492b-176">Первым дочерним **входом** или **выходом** в элементе **Ports** XML-файла будет крайний слева порт входа в интерфейсе машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="2492b-176">The first child **input** or **output** listed in the **Ports** element of the XML file becomes the left-most input port in the Machine Learning UX.</span></span>
<span data-ttu-id="2492b-177">Каждый порт входа и выхода может иметь необязательный дочерний элемент **Description** , задающий текст, отображаемый при наведении курсора мыши на порт в пользовательском интерфейсе машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="2492b-177">Each input and output port may have an optional **Description** child element that specifies the text shown when you hover the mouse cursor over the port in the Machine Learning UI.</span></span>

<span data-ttu-id="2492b-178">**Правила портов**:</span><span class="sxs-lookup"><span data-stu-id="2492b-178">**Ports Rules**:</span></span>

* <span data-ttu-id="2492b-179">Максимальное число **портов входа и выхода** — по 8 для каждого.</span><span class="sxs-lookup"><span data-stu-id="2492b-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="2492b-180">Входные элементы</span><span class="sxs-lookup"><span data-stu-id="2492b-180">Input elements</span></span>
<span data-ttu-id="2492b-181">Порты входа позволяют передавать данные в функцию R и в рабочую область.</span><span class="sxs-lookup"><span data-stu-id="2492b-181">Input ports allow you to pass data to your R function and workspace.</span></span> <span data-ttu-id="2492b-182">Ниже приведены **типы данных** , которые поддерживаются для портов входа.</span><span class="sxs-lookup"><span data-stu-id="2492b-182">The **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="2492b-183">**DataTable:** этот тип передается R-функции в формате data.frame.</span><span class="sxs-lookup"><span data-stu-id="2492b-183">**DataTable:** This type is passed to your R function as a data.frame.</span></span> <span data-ttu-id="2492b-184">Фактически все типы (например, CSV-файлы или ARFF-файлы), которые поддерживаются машинным обучением и которые совместимы с **DataTable** , автоматически преобразуются в формат data.frame.</span><span class="sxs-lookup"><span data-stu-id="2492b-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted to a data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="2492b-185">Атрибут **id**, привязанный к каждому порту входа **DataTable**, должен иметь уникальное значение, которое должно совпадать с соответствующим именем параметра в функции R.</span><span class="sxs-lookup"><span data-stu-id="2492b-185">The **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="2492b-186">Необязательные порты **DataTable**, которые не передаются в качестве входных в эксперименте, имеют значение **null**, передаваемое в функцию R, а необязательные ZIP-порты игнорируются, если вход не подключен.</span><span class="sxs-lookup"><span data-stu-id="2492b-186">Optional **DataTable** ports that are not passed as input in an experiment have the value **NULL** passed to the R function and optional zip ports are ignored if the input is not connected.</span></span> <span data-ttu-id="2492b-187">Атрибут **isOptional** необязательный для типов **DataTable** и **Zip**, и для него по умолчанию задано значение *false*.</span><span class="sxs-lookup"><span data-stu-id="2492b-187">The **isOptional** attribute is optional for both the **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="2492b-188">**Zip** — пользовательские модули могут принимать в качестве входных данных ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="2492b-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="2492b-189">Эти входные данные распаковываются в рабочий каталог функции.</span><span class="sxs-lookup"><span data-stu-id="2492b-189">This input is unpacked into the R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files to be extracted to the R working directory.</Description>
           </Input>

<span data-ttu-id="2492b-190">Для пользовательских модулей R идентификатор ZIP-порта не должен соответствовать параметрам функции R.</span><span class="sxs-lookup"><span data-stu-id="2492b-190">For custom R modules, the id for a Zip port does not have to match any parameters of the R function.</span></span> <span data-ttu-id="2492b-191">Это связано с тем, что ZIP-файл автоматически извлекается в рабочий каталог R.</span><span class="sxs-lookup"><span data-stu-id="2492b-191">This is because the zip file is automatically extracted to the R working directory.</span></span>

<span data-ttu-id="2492b-192">**Правила входных данных:**</span><span class="sxs-lookup"><span data-stu-id="2492b-192">**Input Rules:**</span></span>

* <span data-ttu-id="2492b-193">Значением атрибута **id** элемента **Input** должно быть допустимое имя переменной R.</span><span class="sxs-lookup"><span data-stu-id="2492b-193">The value of the **id** attribute of the **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="2492b-194">Значение атрибута **id** элемента **Input** не должно превышать 64 символа.</span><span class="sxs-lookup"><span data-stu-id="2492b-194">The value of the **id** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="2492b-195">Значение атрибута **name** элемента **Input** не должно превышать 64 символа.</span><span class="sxs-lookup"><span data-stu-id="2492b-195">The value of the **name** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="2492b-196">Содержимое элемента **Описание** не должно превышать 128 символов.</span><span class="sxs-lookup"><span data-stu-id="2492b-196">The content of the **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="2492b-197">Значение атрибута **type** элемента **Input** должно быть *Zip* или *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="2492b-197">The value of the **type** attribute of the **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="2492b-198">Значение атрибута **isOptional** элемента **Input** не является обязательным (по умолчанию *false*, если значение не указано). Если значение указано, оно должно быть *true* или *false*.</span><span class="sxs-lookup"><span data-stu-id="2492b-198">The value of the **isOptional** attribute of the **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="2492b-199">Выходные элементы</span><span class="sxs-lookup"><span data-stu-id="2492b-199">Output elements</span></span>
<span data-ttu-id="2492b-200">**Стандартные выходные порты** сопоставляются со значениями, выдаваемыми функцией R, что потом может использоваться последующими модулями.</span><span class="sxs-lookup"><span data-stu-id="2492b-200">**Standard output ports:** Output ports are mapped to the return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="2492b-201">*DataTable* — пока единственный поддерживаемый стандартный выходной порт.</span><span class="sxs-lookup"><span data-stu-id="2492b-201">*DataTable* is the only standard output port type supported currently.</span></span> <span data-ttu-id="2492b-202">(Ожидается поддержка *Learners* и *Transforms*.) Выходной объект *DataTable* определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2492b-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="2492b-203">Что касается выходов в пользовательских модулях R, значение атрибута **id** не обязательно должно соответствовать скрипту R, но оно должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="2492b-203">For outputs in custom R modules, the value of the **id** attribute does not have to correspond with anything in the R script, but it must be unique.</span></span> <span data-ttu-id="2492b-204">Что касается выхода одного модуля, значение, выдаваемое функцией R, должно быть *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="2492b-204">For a single module output, the return value from the R function must be a *data.frame*.</span></span> <span data-ttu-id="2492b-205">Для вывода нескольких объектов поддерживаемого типа данных необходимо указать соответствующие порты в XML-файле определения, а объекты необходимо возвратить в виде списка.</span><span class="sxs-lookup"><span data-stu-id="2492b-205">In order to output more than one object of a supported data type, the appropriate output ports need to be specified in the XML definition file and the objects need to be returned as a list.</span></span> <span data-ttu-id="2492b-206">Выходные объекты назначаются портам вывода слева направо, в том порядке, в котором объекты размещены в возвращенном списке.</span><span class="sxs-lookup"><span data-stu-id="2492b-206">The output objects are assigned to output ports from left to right, reflecting the order in which the objects are placed in the returned list.</span></span>

<span data-ttu-id="2492b-207">Например, если требуется изменить модуль **Custom Add Rows** (Добавление пользовательских строк) для вывода двух оригинальных наборов данных *dataset1* и *dataset2* в дополнение к новым присоединенным наборам данных *dataset* (слева направо: *dataset*, *dataset1*, *dataset2*), то необходимо определить выходные порты в файле CustomAddRows.xml следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2492b-207">For example, if you want to modify the **Custom Add Rows** module to output the original two datasets, *dataset1* and *dataset2*, in addition to the new joined dataset, *dataset*, (in an order, from left to right, as: *dataset*, *dataset1*, *dataset2*), then define the output ports in the CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="2492b-208">Затем возвратите список объектов в виде списка с правильным порядком в файле CustomAddRows.R:</span><span class="sxs-lookup"><span data-stu-id="2492b-208">And return the list of objects in a list in the correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="2492b-209">**Выход визуализации.** Вы можете также указать выходной порт типа *Визуализация*, отображающий выходные данные от графического устройства и консоли выходных данных R.</span><span class="sxs-lookup"><span data-stu-id="2492b-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays the output from the R graphics device and console output.</span></span> <span data-ttu-id="2492b-210">Этот порт не является частью выходных данных функции R и не влияет на порядок других типов выходных портов.</span><span class="sxs-lookup"><span data-stu-id="2492b-210">This port is not part of the R function output and does not interfere with the order of the other output port types.</span></span> <span data-ttu-id="2492b-211">Для добавления порта визуализации в пользовательские модули добавьте элемент **Output** со значением *Visualization* для его атрибута **type**:</span><span class="sxs-lookup"><span data-stu-id="2492b-211">To add a visualization port to the custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View the R console graphics device output.</Description>
    </Output>

<span data-ttu-id="2492b-212">**Правила выходных данных:**</span><span class="sxs-lookup"><span data-stu-id="2492b-212">**Output Rules:**</span></span>

* <span data-ttu-id="2492b-213">Значением атрибута **id** элемента **Output** должно быть допустимое имя переменной R.</span><span class="sxs-lookup"><span data-stu-id="2492b-213">The value of the **id** attribute of the **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="2492b-214">Значение атрибута **id** элемента **Output** не должно превышать 32 символа.</span><span class="sxs-lookup"><span data-stu-id="2492b-214">The value of the **id** attribute of the **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="2492b-215">Значение атрибута **name** элемента **Output** не должно превышать 64 символа.</span><span class="sxs-lookup"><span data-stu-id="2492b-215">The value of the **name** attribute of the **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="2492b-216">Значением атрибута **type** элемента **Output** должно быть *Visualization*.</span><span class="sxs-lookup"><span data-stu-id="2492b-216">The value of the **type** attribute of the **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="2492b-217">Аргументы</span><span class="sxs-lookup"><span data-stu-id="2492b-217">Arguments</span></span>
<span data-ttu-id="2492b-218">Дополнительные данные могут передаваться в функцию R через параметры модуля, которые определяются в элементе **Аргументы**.</span><span class="sxs-lookup"><span data-stu-id="2492b-218">Additional data can be passed to the R function via module parameters which are defined in the **Arguments** element.</span></span> <span data-ttu-id="2492b-219">Эти параметры отображаются в правой части панели свойств в пользовательском интерфейсе машинного обучения при выборе модуля.</span><span class="sxs-lookup"><span data-stu-id="2492b-219">These parameters appear in the rightmost properties pane of the Machine Learning UI when the module is selected.</span></span> <span data-ttu-id="2492b-220">Аргументы могут быть любого поддерживаемого типа. При необходимости можно создать пользовательскую нумерацию.</span><span class="sxs-lookup"><span data-stu-id="2492b-220">Arguments can be any of the supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="2492b-221">Как и элементы **Ports**, элементы **Arguments** могут иметь необязательный элемент **Description**, который задает текст, отображаемый при наведении указателя мыши на имя параметра.</span><span class="sxs-lookup"><span data-stu-id="2492b-221">Similar to the **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies the text that appears when you hover the mouse over the parameter name.</span></span>
<span data-ttu-id="2492b-222">Дополнительные свойства для модуля, например defaultValue, minValue и maxValue, можно добавить к любому аргументу в виде атрибутов для элемента **Properties**.</span><span class="sxs-lookup"><span data-stu-id="2492b-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added to any argument as attributes to a **Properties** element.</span></span> <span data-ttu-id="2492b-223">Допустимые свойства для элемента **Properties** зависят от типа аргумента. Они описаны в следующем разделе, где также приведены типы поддерживаемых аргументов.</span><span class="sxs-lookup"><span data-stu-id="2492b-223">Valid properties for the **Properties** element depend on the argument type and are described with the supported argument types in the next section.</span></span> <span data-ttu-id="2492b-224">Пользователям не нужно вводить значения для аргументов, свойство **isOptional** которых имеет значение **true**.</span><span class="sxs-lookup"><span data-stu-id="2492b-224">Arguments with the **isOptional** property set to **"true"** do not require the user to enter a value.</span></span> <span data-ttu-id="2492b-225">Если для аргумента значение не указано, он не передается в функцию точки входа.</span><span class="sxs-lookup"><span data-stu-id="2492b-225">If a value is not provided to the argument, then the argument is not passed to the entry point function.</span></span> <span data-ttu-id="2492b-226">Аргументы функции точки входа, которые не являются обязательными, необходимо явным образом обрабатывать с помощью функции, например назначать значение по умолчанию null в определении функции точки входа.</span><span class="sxs-lookup"><span data-stu-id="2492b-226">Arguments of the entry point function that are optional need to be explicitly handled by the function, e.g. assigned a default value of NULL in the entry point function definition.</span></span> <span data-ttu-id="2492b-227">Необязательный аргумент будет обеспечивать применение других ограничений аргументов, например min или max, если это значение указано пользователем.</span><span class="sxs-lookup"><span data-stu-id="2492b-227">An optional argument will only enforce the other argument constraints, i.e. min or max, if a value is provided by the user.</span></span>
<span data-ttu-id="2492b-228">Как и в случае с портами ввода и вывода, крайне важно, чтобы с каждым параметром было связано уникальное значение идентификатора.</span><span class="sxs-lookup"><span data-stu-id="2492b-228">As with inputs and outputs, it is critical that each of the parameters have unique id values associated with them.</span></span> <span data-ttu-id="2492b-229">В нашем примере быстрого запуска привязанным идентификатором или параметром был *swap*.</span><span class="sxs-lookup"><span data-stu-id="2492b-229">In our quick start example the associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="2492b-230">Элемент Arg</span><span class="sxs-lookup"><span data-stu-id="2492b-230">Arg element</span></span>
<span data-ttu-id="2492b-231">Параметр модуля определяется с помощью дочернего элемента **Arg** в разделе **Arguments** XML-файла определения.</span><span class="sxs-lookup"><span data-stu-id="2492b-231">A module parameter is defined using the **Arg** child element of the **Arguments** section of the XML definition file.</span></span> <span data-ttu-id="2492b-232">Как и в случае с дочерними элементами в разделе **Ports**, от порядка параметров в разделе **Arguments** зависит схема размещения элементов в UX.</span><span class="sxs-lookup"><span data-stu-id="2492b-232">As with the child elements in the **Ports** section, the ordering of parameters in the **Arguments** section defines the layout encountered in the UX.</span></span> <span data-ttu-id="2492b-233">Параметры отображаются сверху вниз в пользовательском интерфейсе в том же порядке, в котором они определены в XML-файле.</span><span class="sxs-lookup"><span data-stu-id="2492b-233">The parameters appear from top down in the UI in the same order in which they are defined in the XML file.</span></span> <span data-ttu-id="2492b-234">Здесь перечислены типы, поддерживаемые для параметров в машинном обучении.</span><span class="sxs-lookup"><span data-stu-id="2492b-234">The types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="2492b-235">**int** — параметр целочисленного типа (32-разрядная версия).</span><span class="sxs-lookup"><span data-stu-id="2492b-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="2492b-236">*Необязательные свойства*: **min**, **max**, **default** и **isOptional**.</span><span class="sxs-lookup"><span data-stu-id="2492b-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="2492b-237">**double** — параметр типа double.</span><span class="sxs-lookup"><span data-stu-id="2492b-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="2492b-238">*Необязательные свойства*: **min**, **max**, **default** и **isOptional**.</span><span class="sxs-lookup"><span data-stu-id="2492b-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="2492b-239">**bool** — логический параметр, который представлен в UX в виде флажка.</span><span class="sxs-lookup"><span data-stu-id="2492b-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="2492b-240">*Необязательные свойства*: **по умолчанию** — значение false (если не задано).</span><span class="sxs-lookup"><span data-stu-id="2492b-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="2492b-241">**string**— стандартная строка</span><span class="sxs-lookup"><span data-stu-id="2492b-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="2492b-242">*Необязательные свойства*: **default** и **isOptional**.</span><span class="sxs-lookup"><span data-stu-id="2492b-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="2492b-243">**ColumnPicker** — параметр выбора столбца.</span><span class="sxs-lookup"><span data-stu-id="2492b-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="2492b-244">Этот тип воспроизводится в UX в виде средства выбора столбца.</span><span class="sxs-lookup"><span data-stu-id="2492b-244">This type renders in the UX as a column chooser.</span></span> <span data-ttu-id="2492b-245">Элемент **Property** используется для указания идентификатора порта, из которого будут выбираться столбцы. При этом тип порта назначения должен быть *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="2492b-245">The **Property** element is used here to specify the id of the port from which columns are selected, where the target port type must be *DataTable*.</span></span> <span data-ttu-id="2492b-246">Результат выбора столбца передается функции R в виде списка строк, содержащих имена выбранных столбцов.</span><span class="sxs-lookup"><span data-stu-id="2492b-246">The result of the column selection is passed to the R function as a list of strings containing the selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="2492b-247">*Необходимые свойства*: **portId** — совпадает с идентификатором элемента входных данных типа *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="2492b-247">*Required Properties*: **portId** - matches the id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="2492b-248">*Необязательные свойства*:</span><span class="sxs-lookup"><span data-stu-id="2492b-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="2492b-249">**allowedTypes** фильтрует типы столбцов для выбора.</span><span class="sxs-lookup"><span data-stu-id="2492b-249">**allowedTypes** - Filters the column types from which you can pick.</span></span> <span data-ttu-id="2492b-250">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="2492b-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="2492b-251">Числовой</span><span class="sxs-lookup"><span data-stu-id="2492b-251">Numeric</span></span>
    * <span data-ttu-id="2492b-252">Логический</span><span class="sxs-lookup"><span data-stu-id="2492b-252">Boolean</span></span>
    * <span data-ttu-id="2492b-253">категориальные;</span><span class="sxs-lookup"><span data-stu-id="2492b-253">Categorical</span></span>
    * <span data-ttu-id="2492b-254">string</span><span class="sxs-lookup"><span data-stu-id="2492b-254">String</span></span>
    * <span data-ttu-id="2492b-255">Метка</span><span class="sxs-lookup"><span data-stu-id="2492b-255">Label</span></span>
    * <span data-ttu-id="2492b-256">Функция</span><span class="sxs-lookup"><span data-stu-id="2492b-256">Feature</span></span>
    * <span data-ttu-id="2492b-257">Оценка</span><span class="sxs-lookup"><span data-stu-id="2492b-257">Score</span></span>
    * <span data-ttu-id="2492b-258">Все</span><span class="sxs-lookup"><span data-stu-id="2492b-258">All</span></span>
  * <span data-ttu-id="2492b-259">**по умолчанию** — варианты выбора по умолчанию, допустимые для выбора столбца:</span><span class="sxs-lookup"><span data-stu-id="2492b-259">**default** - Valid default selections for the column picker include:</span></span> 
    
    * <span data-ttu-id="2492b-260">None</span><span class="sxs-lookup"><span data-stu-id="2492b-260">None</span></span>
    * <span data-ttu-id="2492b-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="2492b-261">NumericFeature</span></span>
    * <span data-ttu-id="2492b-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="2492b-262">NumericLabel</span></span>
    * <span data-ttu-id="2492b-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="2492b-263">NumericScore</span></span>
    * <span data-ttu-id="2492b-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="2492b-264">NumericAll</span></span>
    * <span data-ttu-id="2492b-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="2492b-265">BooleanFeature</span></span>
    * <span data-ttu-id="2492b-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="2492b-266">BooleanLabel</span></span>
    * <span data-ttu-id="2492b-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="2492b-267">BooleanScore</span></span>
    * <span data-ttu-id="2492b-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="2492b-268">BooleanAll</span></span>
    * <span data-ttu-id="2492b-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="2492b-269">CategoricalFeature</span></span>
    * <span data-ttu-id="2492b-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="2492b-270">CategoricalLabel</span></span>
    * <span data-ttu-id="2492b-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="2492b-271">CategoricalScore</span></span>
    * <span data-ttu-id="2492b-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="2492b-272">CategoricalAll</span></span>
    * <span data-ttu-id="2492b-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="2492b-273">StringFeature</span></span>
    * <span data-ttu-id="2492b-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="2492b-274">StringLabel</span></span>
    * <span data-ttu-id="2492b-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="2492b-275">StringScore</span></span>
    * <span data-ttu-id="2492b-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="2492b-276">StringAll</span></span>
    * <span data-ttu-id="2492b-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="2492b-277">AllLabel</span></span>
    * <span data-ttu-id="2492b-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="2492b-278">AllFeature</span></span>
    * <span data-ttu-id="2492b-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="2492b-279">AllScore</span></span>
    * <span data-ttu-id="2492b-280">Все</span><span class="sxs-lookup"><span data-stu-id="2492b-280">All</span></span>

<span data-ttu-id="2492b-281">**DropDown**— указанный пользователем пронумерованный (раскрывающийся) список.</span><span class="sxs-lookup"><span data-stu-id="2492b-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="2492b-282">Раскрывающийся список элементов, заданных в элементе **Properties** с помощью элемента **Item**.</span><span class="sxs-lookup"><span data-stu-id="2492b-282">The dropdown items are specified within the **Properties** element using an **Item** element.</span></span> <span data-ttu-id="2492b-283">Элемент **id** для каждого параметра **Item** должен быть уникальной и допустимой переменной R.</span><span class="sxs-lookup"><span data-stu-id="2492b-283">The **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="2492b-284">Значение элемента **name** параметра **Item** выступает в качестве отображаемого текста и значения, передаваемого в функцию R.</span><span class="sxs-lookup"><span data-stu-id="2492b-284">The value of the **name** of an **Item** serves as both the text that you see and the value that is passed to the R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="2492b-285">*Необязательные свойства*:</span><span class="sxs-lookup"><span data-stu-id="2492b-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="2492b-286">**default** — значение свойства по умолчанию должно соответствовать значению идентификатора от одного из элементов **Item**.</span><span class="sxs-lookup"><span data-stu-id="2492b-286">**default** - The value for the default property must correspond with an id value from one of the **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="2492b-287">Вспомогательные файлы</span><span class="sxs-lookup"><span data-stu-id="2492b-287">Auxiliary Files</span></span>
<span data-ttu-id="2492b-288">Любой файл, помещенный в ZIP-файл пользовательского модуля, будет доступен для использования во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2492b-288">Any file that is placed in your custom module ZIP file is going to be available for use during execution time.</span></span> <span data-ttu-id="2492b-289">Вся структура каталогов сохраняется.</span><span class="sxs-lookup"><span data-stu-id="2492b-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="2492b-290">Это означает, что вызов файлов работает как локально, так и при выполнении в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="2492b-290">This means that file sourcing works the same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="2492b-291">Обратите внимание, что все файлы извлекаются в каталог src, поэтому все пути должны иметь префикс src/.</span><span class="sxs-lookup"><span data-stu-id="2492b-291">Notice that all files are extracted to ‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="2492b-292">Предположим, например, что из набора данных необходимо удалить все повторяющиеся строки и строки, в которых частично отсутствуют данные, перед выводом в функцию CustomAddRows, и вы уже написали R-функцию, которая выполняет это действие в файле RemoveDupNARows.R:</span><span class="sxs-lookup"><span data-stu-id="2492b-292">For example, say you want to remove any rows with NAs from the dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="2492b-293">Вы можете вызвать вспомогательный файл RemoveDupNARows.R из функции CustomAddRows:</span><span class="sxs-lookup"><span data-stu-id="2492b-293">You can source the auxiliary file RemoveDupNARows.R in the CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="2492b-294">Затем передать ZIP-файл, содержащий CustomAddRows.R, CustomAddRows.xml и RemoveDupNARows.R, в качестве пользовательского R-модуля.</span><span class="sxs-lookup"><span data-stu-id="2492b-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="2492b-295">Среда выполнения</span><span class="sxs-lookup"><span data-stu-id="2492b-295">Execution Environment</span></span>
<span data-ttu-id="2492b-296">В среде выполнения R-скрипта используется та же версия R, что и в модуле **Выполнение R-скрипта** , и могут использоваться те же пакеты по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2492b-296">The execution environment for the R script uses the same version of R as the **Execute R Script** module and can use the same default packages.</span></span> <span data-ttu-id="2492b-297">В пользовательский модуль также можно добавить дополнительные пакеты R, включая их в ZIP-пакет.</span><span class="sxs-lookup"><span data-stu-id="2492b-297">You can also add additional R packages to your custom module by including them in the custom module zip package.</span></span> <span data-ttu-id="2492b-298">Просто загрузите их в R-скрипт так же, как в среду R.</span><span class="sxs-lookup"><span data-stu-id="2492b-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="2492b-299">**Ограничения среды выполнения** включают:</span><span class="sxs-lookup"><span data-stu-id="2492b-299">**Limitations of the execution environment** include:</span></span>

* <span data-ttu-id="2492b-300">Несохраняемая файловая система. Файлы, записанные при выполнении пользовательского модуля, не сохраняются между несколькими запусками одного и того же модуля.</span><span class="sxs-lookup"><span data-stu-id="2492b-300">Non-persistent file system: Files written when the custom module is run are not persisted across multiple runs of the same module.</span></span>
* <span data-ttu-id="2492b-301">Нет доступа к сети</span><span class="sxs-lookup"><span data-stu-id="2492b-301">No network access</span></span>

