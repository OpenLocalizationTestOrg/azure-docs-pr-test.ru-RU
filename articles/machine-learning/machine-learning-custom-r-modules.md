---
title: "aaaAuthor настраиваемые модули R в машинном обучении Azure | Документы Microsoft"
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
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="d0869-103">Создание пользовательских R-модулей в Машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="d0869-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="d0869-104">В этом разделе описывается способ tooauthor и развернуть пользовательские модули R в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="d0869-104">This topic describes how tooauthor and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="d0869-105">Он описывает сущность пользовательских R-модулей и файлы, используемые toodefine их.</span><span class="sxs-lookup"><span data-stu-id="d0869-105">It explains what custom R modules are and what files are used toodefine them.</span></span> <span data-ttu-id="d0869-106">Он показывает, каким образом tooconstruct hello файлы, определяющие модуль и как tooregister hello модуль для развертывания в рабочей области машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d0869-106">It illustrates how tooconstruct hello files that define a module and how tooregister hello module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="d0869-107">Hello элементы и атрибуты, используемые в определении hello пользовательского модуля hello затем описаны более подробно.</span><span class="sxs-lookup"><span data-stu-id="d0869-107">hello elements and attributes used in hello definition of hello custom module are then described in more detail.</span></span> <span data-ttu-id="d0869-108">Как также описана toouse вспомогательные функции и файлы и несколько выходов.</span><span class="sxs-lookup"><span data-stu-id="d0869-108">How toouse auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="d0869-109">Что такое пользовательский R-модуль?</span><span class="sxs-lookup"><span data-stu-id="d0869-109">What is a custom R module?</span></span>
<span data-ttu-id="d0869-110">Объект **пользовательский модуль** пользовательского модуля, который может быть переданы tooyour рабочей области и выполняется как часть эксперимента машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d0869-110">A **custom module** is a user-defined module that can be uploaded tooyour workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="d0869-111">**Пользовательский R-модуль** представляет собой настраиваемый модуль, который выполняет определяемую пользователем R-функцию.</span><span class="sxs-lookup"><span data-stu-id="d0869-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="d0869-112">**R** — это язык программирования, предназначенный для статистических вычислений и работы с графикой. Его широко используют специалисты по статистике, а также обработке и анализу данных для реализации алгоритмов.</span><span class="sxs-lookup"><span data-stu-id="d0869-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="d0869-113">В настоящее время R — единственный языковой hello поддерживается в пользовательские модули, но поддержка для дополнительных языков запланирована для будущих версий.</span><span class="sxs-lookup"><span data-stu-id="d0869-113">Currently, R is hello only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="d0869-114">Пользовательские модули имеют **состояние первого** в машинном обучении Azure в смысле hello, их можно использовать так же, как и любой другой модуль.</span><span class="sxs-lookup"><span data-stu-id="d0869-114">Custom modules have **first-class status** in Azure Machine Learning in hello sense that they can be used just like any other module.</span></span> <span data-ttu-id="d0869-115">Их можно выполнять с другими модулями, включенными в опубликованный эксперимент или визуализации.</span><span class="sxs-lookup"><span data-stu-id="d0869-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="d0869-116">Контролировать алгоритм hello реализована модулем hello, hello используется toobe портов ввода-вывода, hello параметры моделирования и другие различные характеристики среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="d0869-116">You have control over hello algorithm implemented by hello module, hello input and output ports toobe used, hello modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="d0869-117">Эксперимент, который содержит пользовательские модули могут быть опубликованы в коллекции Cortana аналитики hello упрощает совместное использование.</span><span class="sxs-lookup"><span data-stu-id="d0869-117">An experiment that contains custom modules can also be published into hello Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="d0869-118">Файлы в пользовательском R-модуле</span><span class="sxs-lookup"><span data-stu-id="d0869-118">Files in a custom R module</span></span>
<span data-ttu-id="d0869-119">Пользовательский R-модуль создается на основе ZIP-файла, содержащего как минимум два файла:</span><span class="sxs-lookup"><span data-stu-id="d0869-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="d0869-120">Объект **исходный файл** , реализующий функции hello R, предоставляемыми hello модуля</span><span class="sxs-lookup"><span data-stu-id="d0869-120">A **source file** that implements hello R function exposed by hello module</span></span>
* <span data-ttu-id="d0869-121">**XML-файл определения** , описывающий hello интерфейс пользовательского модуля</span><span class="sxs-lookup"><span data-stu-id="d0869-121">An **XML definition file** that describes hello custom module interface</span></span>

<span data-ttu-id="d0869-122">Также можно включить дополнительные вспомогательные файлы в ZIP-файл hello, предоставляет функции, которые доступны из пользовательского модуля hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-122">Additional auxiliary files can also be included in hello .zip file that provides functionality that can be accessed from hello custom module.</span></span> <span data-ttu-id="d0869-123">Эта возможность описана в hello **аргументы** частью hello справочном разделе **элементов в XML-файл определения hello** следующий пример hello краткое руководство.</span><span class="sxs-lookup"><span data-stu-id="d0869-123">This option is discussed in hello **Arguments** part of hello reference section **Elements in hello XML definition file** following hello quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="d0869-124">Пример быстрого запуска: определение, создание пакета и регистрация пользовательского R-модуля</span><span class="sxs-lookup"><span data-stu-id="d0869-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="d0869-125">В этом примере показано, как tooconstruct hello файлы, необходимые пользовательский модуль R, упаковать их в ZIP-файл, а затем зарегистрировать модуль hello в рабочей области машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d0869-125">This example illustrates how tooconstruct hello files required by a custom R module, package them into a zip file, and then register hello module in your Machine Learning workspace.</span></span> <span data-ttu-id="d0869-126">Hello примере ZIP-пакета и образец файлы можно загрузить из [CustomAddRows.zip, загрузите файл](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d0869-126">hello example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="hello-source-file"></a><span data-ttu-id="d0869-127">исходный файл Hello</span><span class="sxs-lookup"><span data-stu-id="d0869-127">hello source file</span></span>
<span data-ttu-id="d0869-128">Рассмотрим пример hello **Добавление строк настраиваемых** модуль, который изменяет стандартную реализацию hello hello **Добавление строк** модуль использовать tooconcatenate строк (наблюдений) из двух наборов данных (кадры данных).</span><span class="sxs-lookup"><span data-stu-id="d0869-128">Consider hello example of a **Custom Add Rows** module that modifies hello standard implementation of hello **Add Rows** module used tooconcatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="d0869-129">Стандартная Hello **Добавление строк** модуль добавляет строки hello hello второго входного набора данных toohello конца hello первого входного набора данных с помощью hello `rbind` алгоритма.</span><span class="sxs-lookup"><span data-stu-id="d0869-129">hello standard **Add Rows** module appends hello rows of hello second input dataset toohello end of hello first input dataset using hello `rbind` algorithm.</span></span> <span data-ttu-id="d0869-130">настроить Hello `CustomAddRows` функция аналогично принимает два набора данных, а также принимает параметр логическое swap как дополнительный вход.</span><span class="sxs-lookup"><span data-stu-id="d0869-130">hello customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="d0869-131">Если параметр замены hello установлен слишком**FALSE**, он возвращает hello того же набора данных как hello стандартную реализацию.</span><span class="sxs-lookup"><span data-stu-id="d0869-131">If hello swap parameter is set too**FALSE**, it returns hello same data set as hello standard implementation.</span></span> <span data-ttu-id="d0869-132">Но если параметр замены hello **TRUE**, функции hello добавляет строки из первого входного набора данных toohello конец hello второго набора данных, вместо этого.</span><span class="sxs-lookup"><span data-stu-id="d0869-132">But if hello swap parameter is **TRUE**, hello function appends rows of first input dataset toohello end of hello second dataset instead.</span></span> <span data-ttu-id="d0869-133">Hello CustomAddRows.R файл, который содержит реализацию hello hello R `CustomAddRows` из функций hello **Добавление строк настраиваемых** модуль имеет следующий код R hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-133">hello CustomAddRows.R file that contains hello implementation of hello R `CustomAddRows` function exposed by hello **Custom Add Rows** module has hello following R code.</span></span>

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

### <a name="hello-xml-definition-file"></a><span data-ttu-id="d0869-134">XML-файл определения Hello</span><span class="sxs-lookup"><span data-stu-id="d0869-134">hello XML definition file</span></span>
<span data-ttu-id="d0869-135">tooexpose это `CustomAddRows` функции в качестве XML-файла определения модуля машинного обучения Azure, необходимо создать toospecify как hello **Добавление строк настраиваемых** модуля следует выглядят и работают так.</span><span class="sxs-lookup"><span data-stu-id="d0869-135">tooexpose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created toospecify how hello **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="d0869-136">Это критическое toonote, hello значение hello **идентификатор** атрибуты hello **ввода** и **Arg** элементов в XML-файле hello должны совпадать имена параметров функции hello hello R Код файла CustomAddRows.R hello точно: (*dataset1*, *dataset2*, и *swap* в примере hello).</span><span class="sxs-lookup"><span data-stu-id="d0869-136">It is critical toonote that hello value of hello **id** attributes of hello **Input** and **Arg** elements in hello XML file must match hello function parameter names of hello R code in hello CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in hello example).</span></span> <span data-ttu-id="d0869-137">Аналогичным образом hello значение hello **entryPoint** атрибут hello **язык** элемент должен полностью соответствовать hello имя функции hello в скрипте hello R: (*CustomAddRows* в примере hello).</span><span class="sxs-lookup"><span data-stu-id="d0869-137">Similarly, hello value of hello **entryPoint** attribute of hello **Language** element must match hello name of hello function in hello R script EXACTLY: (*CustomAddRows* in hello example).</span></span> 

<span data-ttu-id="d0869-138">Здравствуйте, напротив, **идентификатор** атрибут для hello **вывода** элемента не соответствует tooany переменных в сценарии hello R.</span><span class="sxs-lookup"><span data-stu-id="d0869-138">In contrast, hello **id** attribute for hello **Output** element does not correspond tooany variables in hello R script.</span></span> <span data-ttu-id="d0869-139">Если требуется несколько выходных данных, просто вернуть список из функции hello R с результатами разместить *в hello порядке* как **выходов** элементы, объявленные в XML-файле hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-139">When more than one output is required, simply return a list from hello R function with results placed *in hello same order* as **Outputs** elements are declared in hello XML file.</span></span>

### <a name="package-and-register-hello-module"></a><span data-ttu-id="d0869-140">Пакет и зарегистрировать модуль hello</span><span class="sxs-lookup"><span data-stu-id="d0869-140">Package and register hello module</span></span>
<span data-ttu-id="d0869-141">Сохранить эти файлы как *CustomAddRows.R* и *CustomAddRows.xml* и затем zip вместе hello два файла в *CustomAddRows.zip* файла.</span><span class="sxs-lookup"><span data-stu-id="d0869-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip hello two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="d0869-142">их в рабочей области машинного обучения, рабочей области перейдите tooyour в студии машинного обучения hello щелкните hello tooregister **+ создать** нижней hello и выберите команду **МОДУЛЯ -> из ZIP-ПАКЕТА** tooupload новый Hello **Добавление строк настраиваемых** модуля.</span><span class="sxs-lookup"><span data-stu-id="d0869-142">tooregister them in your Machine Learning workspace, go tooyour workspace in hello Machine Learning Studio, click hello **+NEW** button on hello bottom and choose **MODULE -> FROM ZIP PACKAGE** tooupload hello new **Custom Add Rows** module.</span></span>

![Передача ZIP-файла](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="d0869-144">Hello **Добавление строк настраиваемых** модуль является теперь готовы toobe обращаются эксперименты машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d0869-144">hello **Custom Add Rows** module is now ready toobe accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-hello-xml-definition-file"></a><span data-ttu-id="d0869-145">Элементы в XML-файл определения hello</span><span class="sxs-lookup"><span data-stu-id="d0869-145">Elements in hello XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="d0869-146">Элементы «Модуль»</span><span class="sxs-lookup"><span data-stu-id="d0869-146">Module elements</span></span>
<span data-ttu-id="d0869-147">Hello **модуль** элемент является toodefine используется пользовательский модуль в XML-файле hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-147">hello **Module** element is used toodefine a custom module in hello XML file.</span></span> <span data-ttu-id="d0869-148">С помощью нескольких элементов **модуль** в одном XML-файле можно определить несколько модулей.</span><span class="sxs-lookup"><span data-stu-id="d0869-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="d0869-149">Каждый модуль в рабочей области должен иметь уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="d0869-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="d0869-150">Зарегистрировать пользовательский модуль hello одинаковые имена, как существующий пользовательский модуль, и он заменяет существующий модуль hello hello новый.</span><span class="sxs-lookup"><span data-stu-id="d0869-150">Register a custom module with hello same name as an existing custom module and it replaces hello existing module with hello new one.</span></span> <span data-ttu-id="d0869-151">Пользовательские модули, тем не менее, может быть зарегистрирована hello точно такое же имя в качестве существующего модуля машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d0869-151">Custom modules can, however, be registered with hello same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="d0869-152">Если таким образом, они отображаются в hello **настраиваемый** категории hello модуля палитры.</span><span class="sxs-lookup"><span data-stu-id="d0869-152">If so, they appear in hello **Custom** category of hello module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


<span data-ttu-id="d0869-153">В рамках hello **модуль** элемента, можно указать два дополнительных необязательных элементов:</span><span class="sxs-lookup"><span data-stu-id="d0869-153">Within hello **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="d0869-154">**владельца** элемент, который внедряется в модуль hello</span><span class="sxs-lookup"><span data-stu-id="d0869-154">an **Owner** element that is embedded into hello module</span></span>  
* <span data-ttu-id="d0869-155">**описание** элемент, который содержит текст, отображающийся в экспресс-Справка для модуля "hello" и при наведении на модуль hello в hello интерфейса обучения.</span><span class="sxs-lookup"><span data-stu-id="d0869-155">a **Description** element that contains text that is displayed in quick help for hello module and when you hover over hello module in hello Machine Learning UI.</span></span>

<span data-ttu-id="d0869-156">Правила ограничения символов в элементах hello модуля:</span><span class="sxs-lookup"><span data-stu-id="d0869-156">Rules for characters limits in hello Module elements:</span></span>

* <span data-ttu-id="d0869-157">Здравствуйте, значение hello **имя** атрибута в hello **модуль** элемента не должна превышать 64 символов.</span><span class="sxs-lookup"><span data-stu-id="d0869-157">hello value of hello **name** attribute in hello **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="d0869-158">Здравствуйте, содержимое hello **описание** элемента не должна превышать 128 символов.</span><span class="sxs-lookup"><span data-stu-id="d0869-158">hello content of hello **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="d0869-159">Здравствуйте, содержимое hello **владельца** элемента не должна превышать 32 символов.</span><span class="sxs-lookup"><span data-stu-id="d0869-159">hello content of hello **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="d0869-160">Результаты модуля могут быть детерминированными или nondeterministic.* * по умолчанию, все модули, считаются toobe детерминированной.</span><span class="sxs-lookup"><span data-stu-id="d0869-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered toobe deterministic.</span></span> <span data-ttu-id="d0869-161">Т. е если неизменяемый набор входных параметров и данных, модуль hello должен возвращать hello же результаты, eacRAND или functionh время запуска.</span><span class="sxs-lookup"><span data-stu-id="d0869-161">That is, given an unchanging set of input parameters and data, hello module should return hello same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="d0869-162">Это поведение, студии машинного обучения Azure перезапустит только модули, которые помечены как детерминированную, если параметр или hello входные данные были изменены.</span><span class="sxs-lookup"><span data-stu-id="d0869-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or hello input data has changed.</span></span> <span data-ttu-id="d0869-163">Возврат результатов hello кэширования также предоставляет гораздо более быстрого выполнения экспериментов.</span><span class="sxs-lookup"><span data-stu-id="d0869-163">Returning hello cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="d0869-164">Нет функций, которые являются недетерминированными, таких как RAND или функцию, возвращающую hello текущей даты или времени.</span><span class="sxs-lookup"><span data-stu-id="d0869-164">There are functions that are nondeterministic, such as RAND or a function that returns hello current date or time.</span></span> <span data-ttu-id="d0869-165">Если модуль использует недетерминированную функцию, можно указать модуля hello не является детерминированным, параметр hello необязательно **isDeterministic** атрибут слишком**FALSE**.</span><span class="sxs-lookup"><span data-stu-id="d0869-165">If your module uses a nondeterministic function, you can specify that hello module is non-deterministic by setting hello optional **isDeterministic** attribute too**FALSE**.</span></span> <span data-ttu-id="d0869-166">Это гарантирует, что этот модуль hello запускается повторно при каждом запуске эксперимента hello, даже если hello входных данных модуля и параметры не были изменены.</span><span class="sxs-lookup"><span data-stu-id="d0869-166">This insures that hello module is rerun whenever hello experiment is run, even if hello module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="d0869-167">Определение языка</span><span class="sxs-lookup"><span data-stu-id="d0869-167">Language Definition</span></span>
<span data-ttu-id="d0869-168">Hello **языка** элемент в XML-файл определения — язык пользовательского модуля используется toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-168">hello **Language** element in your XML definition file is used toospecify hello custom module language.</span></span> <span data-ttu-id="d0869-169">В настоящее время R — hello поддерживается только язык.</span><span class="sxs-lookup"><span data-stu-id="d0869-169">Currently, R is hello only supported language.</span></span> <span data-ttu-id="d0869-170">Здравствуйте, значение hello **sourceFile** атрибута должно быть именем hello hello R-файла, который содержит toocall функции hello при запуске модуля hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-170">hello value of hello **sourceFile** attribute must be hello name of hello R file that contains hello function toocall when hello module is run.</span></span> <span data-ttu-id="d0869-171">Этот файл должен быть частью hello ZIP-пакета.</span><span class="sxs-lookup"><span data-stu-id="d0869-171">This file must be part of hello zip package.</span></span> <span data-ttu-id="d0869-172">Здравствуйте, значение hello **entryPoint** атрибут hello имя вызываемой функции hello и должно соответствовать является допустимой функцией, определенные в исходном файле hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-172">hello value of hello **entryPoint** attribute is hello name of hello function being called and must match a valid function defined with in hello source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="d0869-173">порты;</span><span class="sxs-lookup"><span data-stu-id="d0869-173">Ports</span></span>
<span data-ttu-id="d0869-174">Hello портов ввода-вывода для настраиваемого модуля указываются в дочерних элементов hello **порты** раздел XML-файла определения hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-174">hello input and output ports for a custom module are specified in child elements of hello **Ports** section of hello XML definition file.</span></span> <span data-ttu-id="d0869-175">Hello порядок этих элементов разметки hello опытным (UX) пользователями.</span><span class="sxs-lookup"><span data-stu-id="d0869-175">hello order of these elements determines hello layout experienced (UX) by users.</span></span> <span data-ttu-id="d0869-176">первый дочерний элемент Hello **ввода** или **выходные данные** перечисленные в hello **порты** элемент hello XML-файла становится входного порта hello слева в hello UI машины обучения.</span><span class="sxs-lookup"><span data-stu-id="d0869-176">hello first child **input** or **output** listed in hello **Ports** element of hello XML file becomes hello left-most input port in hello Machine Learning UX.</span></span>
<span data-ttu-id="d0869-177">Каждый входной и выходной порт может иметь дополнительный **описание** дочерний элемент, который указывает текст hello, отображаемый при наведении курсора мыши hello порт hello в hello интерфейса обучения.</span><span class="sxs-lookup"><span data-stu-id="d0869-177">Each input and output port may have an optional **Description** child element that specifies hello text shown when you hover hello mouse cursor over hello port in hello Machine Learning UI.</span></span>

<span data-ttu-id="d0869-178">**Правила портов**:</span><span class="sxs-lookup"><span data-stu-id="d0869-178">**Ports Rules**:</span></span>

* <span data-ttu-id="d0869-179">Максимальное число **портов входа и выхода** — по 8 для каждого.</span><span class="sxs-lookup"><span data-stu-id="d0869-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="d0869-180">Входные элементы</span><span class="sxs-lookup"><span data-stu-id="d0869-180">Input elements</span></span>
<span data-ttu-id="d0869-181">Входные порты позволяют функция tooyour R toopass данных и рабочей области.</span><span class="sxs-lookup"><span data-stu-id="d0869-181">Input ports allow you toopass data tooyour R function and workspace.</span></span> <span data-ttu-id="d0869-182">Hello **типы данных** , которые поддерживаются для входных портов, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="d0869-182">hello **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="d0869-183">**DataTable:** этот тип передается функции tooyour R как data.frame.</span><span class="sxs-lookup"><span data-stu-id="d0869-183">**DataTable:** This type is passed tooyour R function as a data.frame.</span></span> <span data-ttu-id="d0869-184">На самом деле, все типы (например, CSV-файлы или файлы ARFF), поддерживаемых машинного обучения, которые совместимы с **DataTable** , преобразованный tooa data.frame автоматически.</span><span class="sxs-lookup"><span data-stu-id="d0869-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted tooa data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="d0869-185">Hello **идентификатор** атрибутов, связанных с каждым **DataTable** входного порта должны иметь уникальное значение, и это значение должно соответствовать соответствующего именованного параметра в функции R.</span><span class="sxs-lookup"><span data-stu-id="d0869-185">hello **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="d0869-186">Необязательный **DataTable** порты, которые не передаются в качестве входных данных в эксперимент имеют значение hello **NULL** функция переданный toohello R и порты необязательный zip учитываются, если входные данные hello не подключен.</span><span class="sxs-lookup"><span data-stu-id="d0869-186">Optional **DataTable** ports that are not passed as input in an experiment have hello value **NULL** passed toohello R function and optional zip ports are ignored if hello input is not connected.</span></span> <span data-ttu-id="d0869-187">Hello **isOptional** атрибут является необязательным для обоих hello **DataTable** и **Zip** типы, а также является *false* по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d0869-187">hello **isOptional** attribute is optional for both hello **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="d0869-188">**Zip** — пользовательские модули могут принимать в качестве входных данных ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="d0869-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="d0869-189">Входные данные, распакованного в рабочий каталог hello R этой функции</span><span class="sxs-lookup"><span data-stu-id="d0869-189">This input is unpacked into hello R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

<span data-ttu-id="d0869-190">Для пользовательских R-модулей идентификатор hello для порта Zip не иметь toomatch параметров функции hello R.</span><span class="sxs-lookup"><span data-stu-id="d0869-190">For custom R modules, hello id for a Zip port does not have toomatch any parameters of hello R function.</span></span> <span data-ttu-id="d0869-191">Это происходит потому hello ZIP-файл является автоматически извлеченные toohello R рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="d0869-191">This is because hello zip file is automatically extracted toohello R working directory.</span></span>

<span data-ttu-id="d0869-192">**Правила входных данных:**</span><span class="sxs-lookup"><span data-stu-id="d0869-192">**Input Rules:**</span></span>

* <span data-ttu-id="d0869-193">Здравствуйте, значение hello **идентификатор** атрибут hello **ввода** элемент должен быть допустимым именем переменной R.</span><span class="sxs-lookup"><span data-stu-id="d0869-193">hello value of hello **id** attribute of hello **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="d0869-194">Здравствуйте, значение hello **идентификатор** атрибут hello **ввода** элемент должен быть не длиннее 64 символов.</span><span class="sxs-lookup"><span data-stu-id="d0869-194">hello value of hello **id** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="d0869-195">Здравствуйте, значение hello **имя** атрибут hello **ввода** элемент должен быть не длиннее 64 символов.</span><span class="sxs-lookup"><span data-stu-id="d0869-195">hello value of hello **name** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="d0869-196">Здравствуйте, содержимое hello **описание** элемент должен быть не длиннее 128 символов</span><span class="sxs-lookup"><span data-stu-id="d0869-196">hello content of hello **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="d0869-197">Здравствуйте, значение hello **тип** атрибут hello **ввода** элемент должен быть *ZIP-* или *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="d0869-197">hello value of hello **type** attribute of hello **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="d0869-198">Hello значение hello **isOptional** атрибут hello **входных данных** элемент не является обязательным (и *false* по умолчанию, если не указан); но если он указан, он должен быть *true* или *false*.</span><span class="sxs-lookup"><span data-stu-id="d0869-198">hello value of hello **isOptional** attribute of hello **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="d0869-199">Выходные элементы</span><span class="sxs-lookup"><span data-stu-id="d0869-199">Output elements</span></span>
<span data-ttu-id="d0869-200">**Стандартного вывода порты:** порты выходные данные, сопоставленные toohello возвращаемые значения функции R, который можно использовать в последующих модулях.</span><span class="sxs-lookup"><span data-stu-id="d0869-200">**Standard output ports:** Output ports are mapped toohello return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="d0869-201">*DataTable* — тип порта hello только стандартные выходные данные, в настоящее время поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d0869-201">*DataTable* is hello only standard output port type supported currently.</span></span> <span data-ttu-id="d0869-202">(Ожидается поддержка *Learners* и *Transforms*.) Выходной объект *DataTable* определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d0869-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="d0869-203">Для выходных данных в пользовательских R-модулей hello значение hello **идентификатор** атрибут не имеет toocorrespond с ничего в скрипте hello R, но он должен быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="d0869-203">For outputs in custom R modules, hello value of hello **id** attribute does not have toocorrespond with anything in hello R script, but it must be unique.</span></span> <span data-ttu-id="d0869-204">Для одного модуля выхода, должен быть hello возвращаемое значение функции hello R *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="d0869-204">For a single module output, hello return value from hello R function must be a *data.frame*.</span></span> <span data-ttu-id="d0869-205">В заказ toooutput более одного объекта поддерживаемый тип данных, порты hello соответствующие выходные данные должны toobe, указанный в XML-файл определения hello и hello объекты должны toobe возвращаются в виде списка.</span><span class="sxs-lookup"><span data-stu-id="d0869-205">In order toooutput more than one object of a supported data type, hello appropriate output ports need toobe specified in hello XML definition file and hello objects need toobe returned as a list.</span></span> <span data-ttu-id="d0869-206">Hello выходных объектов назначаются toooutput порты из левой tooright, отражая hello порядок, в котором hello объекты размещаются в возвращаемый список hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-206">hello output objects are assigned toooutput ports from left tooright, reflecting hello order in which hello objects are placed in hello returned list.</span></span>

<span data-ttu-id="d0869-207">Например, если вы хотите toomodify hello **Добавление строк настраиваемых** toooutput модуль hello исходного двух наборов данных, *dataset1* и *dataset2*, кроме присоединяется новый toohello набор данных, *набора данных*, (по порядку, от левой tooright как: *набора данных*, *dataset1*, *dataset2*), а затем определите hello выходных портов в файле CustomAddRows.xml hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d0869-207">For example, if you want toomodify hello **Custom Add Rows** module toooutput hello original two datasets, *dataset1* and *dataset2*, in addition toohello new joined dataset, *dataset*, (in an order, from left tooright, as: *dataset*, *dataset1*, *dataset2*), then define hello output ports in hello CustomAddRows.xml file as follows:</span></span>

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


<span data-ttu-id="d0869-208">И возвращают список объектов hello в виде списка в правильном порядке hello в «CustomAddRows.R»:</span><span class="sxs-lookup"><span data-stu-id="d0869-208">And return hello list of objects in a list in hello correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="d0869-209">**Выходные данные визуализации:** можно также указать порт вывода типа *визуализации*, отображающего hello hello R графического устройства и консоли вывода.</span><span class="sxs-lookup"><span data-stu-id="d0869-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays hello output from hello R graphics device and console output.</span></span> <span data-ttu-id="d0869-210">Этот порт не является частью выходные данные функции hello R и не влияет на порядок hello hello другие выходные типы портов.</span><span class="sxs-lookup"><span data-stu-id="d0869-210">This port is not part of hello R function output and does not interfere with hello order of hello other output port types.</span></span> <span data-ttu-id="d0869-211">Добавьте визуализации порт toohello пользовательские модули, tooadd **выходные данные** элемент со значением *визуализации* для его **тип** атрибута:</span><span class="sxs-lookup"><span data-stu-id="d0869-211">tooadd a visualization port toohello custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

<span data-ttu-id="d0869-212">**Правила выходных данных:**</span><span class="sxs-lookup"><span data-stu-id="d0869-212">**Output Rules:**</span></span>

* <span data-ttu-id="d0869-213">Здравствуйте, значение hello **идентификатор** атрибут hello **вывода** элемент должен быть допустимым именем переменной R.</span><span class="sxs-lookup"><span data-stu-id="d0869-213">hello value of hello **id** attribute of hello **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="d0869-214">Здравствуйте, значение hello **идентификатор** атрибут hello **выходные данные** элемент должен быть не более 32 символов.</span><span class="sxs-lookup"><span data-stu-id="d0869-214">hello value of hello **id** attribute of hello **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="d0869-215">Здравствуйте, значение hello **имя** атрибут hello **вывода** элемент должен быть не длиннее 64 символов.</span><span class="sxs-lookup"><span data-stu-id="d0869-215">hello value of hello **name** attribute of hello **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="d0869-216">Здравствуйте, значение hello **тип** атрибут hello **вывода** элемент должен быть *визуализации*.</span><span class="sxs-lookup"><span data-stu-id="d0869-216">hello value of hello **type** attribute of hello **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="d0869-217">Аргументы</span><span class="sxs-lookup"><span data-stu-id="d0869-217">Arguments</span></span>
<span data-ttu-id="d0869-218">Дополнительные данные могут передаваться функции toohello R через параметры модуля, которые определены в hello **аргументы** элемента.</span><span class="sxs-lookup"><span data-stu-id="d0869-218">Additional data can be passed toohello R function via module parameters which are defined in hello **Arguments** element.</span></span> <span data-ttu-id="d0869-219">Эти параметры отображаются панели свойств справа hello hello интерфейса обучения при выборе модуля hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-219">These parameters appear in hello rightmost properties pane of hello Machine Learning UI when hello module is selected.</span></span> <span data-ttu-id="d0869-220">Аргументы могут быть любого типа hello поддерживается, или можно создать пользовательские перечисления, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d0869-220">Arguments can be any of hello supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="d0869-221">Аналогичные toohello **порты** элементов, **аргументы** элементов может иметь дополнительный **описание** элемент, который задает hello текст, отображаемый при наведении указателя мыши hello через имя параметра hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-221">Similar toohello **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies hello text that appears when you hover hello mouse over hello parameter name.</span></span>
<span data-ttu-id="d0869-222">Аргумент tooany как атрибуты tooa можно добавить дополнительные свойства для модуля, например defaultValue minValue и maxValue **свойства** элемента.</span><span class="sxs-lookup"><span data-stu-id="d0869-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added tooany argument as attributes tooa **Properties** element.</span></span> <span data-ttu-id="d0869-223">Допустимые свойства для hello **свойства** элемента зависят от типа аргумента hello и описываются с типами аргументов hello поддерживается в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-223">Valid properties for hello **Properties** element depend on hello argument type and are described with hello supported argument types in hello next section.</span></span> <span data-ttu-id="d0869-224">Аргументы, имеющие hello **isOptional** значение свойства слишком**«true»** tooenter пользователя hello значение не требуется.</span><span class="sxs-lookup"><span data-stu-id="d0869-224">Arguments with hello **isOptional** property set too**"true"** do not require hello user tooenter a value.</span></span> <span data-ttu-id="d0869-225">Если значение аргумента toohello не предоставлено, hello аргумент не передается toohello функцию точки входа.</span><span class="sxs-lookup"><span data-stu-id="d0869-225">If a value is not provided toohello argument, then hello argument is not passed toohello entry point function.</span></span> <span data-ttu-id="d0869-226">Аргументы функции точки входа hello, которые являются toobe необязательно должны явным образом обрабатываются функции hello, например назначить значение NULL по умолчанию в определении функции точки входа hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-226">Arguments of hello entry point function that are optional need toobe explicitly handled by hello function, e.g. assigned a default value of NULL in hello entry point function definition.</span></span> <span data-ttu-id="d0869-227">Необязательный аргумент только будет обеспечивать hello ограничения других аргументов, т. е., min или max, если значение указано пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-227">An optional argument will only enforce hello other argument constraints, i.e. min or max, if a value is provided by hello user.</span></span>
<span data-ttu-id="d0869-228">Как и для входных и выходных данных, очень важно, у каждого из параметров hello уникальный идентификатор значения, связанные с ними.</span><span class="sxs-lookup"><span data-stu-id="d0869-228">As with inputs and outputs, it is critical that each of hello parameters have unique id values associated with them.</span></span> <span data-ttu-id="d0869-229">Наши руководства по быстрому запуску был пример hello связанный идентификатор и параметра *swap*.</span><span class="sxs-lookup"><span data-stu-id="d0869-229">In our quick start example hello associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="d0869-230">Элемент Arg</span><span class="sxs-lookup"><span data-stu-id="d0869-230">Arg element</span></span>
<span data-ttu-id="d0869-231">Параметр модуля определяется с помощью hello **Arg** дочерний элемент элемента hello **аргументы** раздел XML-файла определения hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-231">A module parameter is defined using hello **Arg** child element of hello **Arguments** section of hello XML definition file.</span></span> <span data-ttu-id="d0869-232">Как и в случае с дочерними элементами hello в hello **порты** статьи, hello порядок параметров в hello **аргументы** раздел определяет макет hello в hello UI.</span><span class="sxs-lookup"><span data-stu-id="d0869-232">As with hello child elements in hello **Ports** section, hello ordering of parameters in hello **Arguments** section defines hello layout encountered in hello UX.</span></span> <span data-ttu-id="d0869-233">Hello параметры отображаются сверху вниз в hello пользовательского интерфейса в hello же порядок, в котором они определены в XML-файле hello.</span><span class="sxs-lookup"><span data-stu-id="d0869-233">hello parameters appear from top down in hello UI in hello same order in which they are defined in hello XML file.</span></span> <span data-ttu-id="d0869-234">Здесь перечислены Hello, поддерживаемым службами машинного обучения для параметров.</span><span class="sxs-lookup"><span data-stu-id="d0869-234">hello types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="d0869-235">**int** — параметр целочисленного типа (32-разрядная версия).</span><span class="sxs-lookup"><span data-stu-id="d0869-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="d0869-236">*Необязательные свойства*: **min**, **max**, **default** и **isOptional**.</span><span class="sxs-lookup"><span data-stu-id="d0869-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="d0869-237">**double** — параметр типа double.</span><span class="sxs-lookup"><span data-stu-id="d0869-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="d0869-238">*Необязательные свойства*: **min**, **max**, **default** и **isOptional**.</span><span class="sxs-lookup"><span data-stu-id="d0869-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="d0869-239">**bool** — логический параметр, который представлен в UX в виде флажка.</span><span class="sxs-lookup"><span data-stu-id="d0869-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="d0869-240">*Необязательные свойства*: **по умолчанию** — значение false (если не задано).</span><span class="sxs-lookup"><span data-stu-id="d0869-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="d0869-241">**string**— стандартная строка</span><span class="sxs-lookup"><span data-stu-id="d0869-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="d0869-242">*Необязательные свойства*: **default** и **isOptional**.</span><span class="sxs-lookup"><span data-stu-id="d0869-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="d0869-243">**ColumnPicker** — параметр выбора столбца.</span><span class="sxs-lookup"><span data-stu-id="d0869-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="d0869-244">Этот тип готовится к просмотру в hello UX как выбор столбца.</span><span class="sxs-lookup"><span data-stu-id="d0869-244">This type renders in hello UX as a column chooser.</span></span> <span data-ttu-id="d0869-245">Hello **свойство** элемента — идентификатор hello используется здесь toospecify порт hello, из которой выбираются столбцы, где hello целевого типа порта должно быть *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="d0869-245">hello **Property** element is used here toospecify hello id of hello port from which columns are selected, where hello target port type must be *DataTable*.</span></span> <span data-ttu-id="d0869-246">результат Hello выделенный фрагмент столбца hello передается функции toohello R как список строк, содержащих имена hello выбранных столбцов.</span><span class="sxs-lookup"><span data-stu-id="d0869-246">hello result of hello column selection is passed toohello R function as a list of strings containing hello selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="d0869-247">*Требуемые свойства*: **portId** -совпадений hello идентификатор элемента входных данных с типом *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="d0869-247">*Required Properties*: **portId** - matches hello id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="d0869-248">*Необязательные свойства*:</span><span class="sxs-lookup"><span data-stu-id="d0869-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="d0869-249">**allowedTypes** -типы столбцов hello фильтры, из которого можно выбрать.</span><span class="sxs-lookup"><span data-stu-id="d0869-249">**allowedTypes** - Filters hello column types from which you can pick.</span></span> <span data-ttu-id="d0869-250">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="d0869-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="d0869-251">Числовой</span><span class="sxs-lookup"><span data-stu-id="d0869-251">Numeric</span></span>
    * <span data-ttu-id="d0869-252">Логический</span><span class="sxs-lookup"><span data-stu-id="d0869-252">Boolean</span></span>
    * <span data-ttu-id="d0869-253">категориальные;</span><span class="sxs-lookup"><span data-stu-id="d0869-253">Categorical</span></span>
    * <span data-ttu-id="d0869-254">string</span><span class="sxs-lookup"><span data-stu-id="d0869-254">String</span></span>
    * <span data-ttu-id="d0869-255">Метка</span><span class="sxs-lookup"><span data-stu-id="d0869-255">Label</span></span>
    * <span data-ttu-id="d0869-256">Функция</span><span class="sxs-lookup"><span data-stu-id="d0869-256">Feature</span></span>
    * <span data-ttu-id="d0869-257">Оценка</span><span class="sxs-lookup"><span data-stu-id="d0869-257">Score</span></span>
    * <span data-ttu-id="d0869-258">Все</span><span class="sxs-lookup"><span data-stu-id="d0869-258">All</span></span>
  * <span data-ttu-id="d0869-259">**по умолчанию** -варианты выбора по умолчанию для выбора столбцов hello включают:</span><span class="sxs-lookup"><span data-stu-id="d0869-259">**default** - Valid default selections for hello column picker include:</span></span> 
    
    * <span data-ttu-id="d0869-260">None</span><span class="sxs-lookup"><span data-stu-id="d0869-260">None</span></span>
    * <span data-ttu-id="d0869-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="d0869-261">NumericFeature</span></span>
    * <span data-ttu-id="d0869-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="d0869-262">NumericLabel</span></span>
    * <span data-ttu-id="d0869-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="d0869-263">NumericScore</span></span>
    * <span data-ttu-id="d0869-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="d0869-264">NumericAll</span></span>
    * <span data-ttu-id="d0869-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="d0869-265">BooleanFeature</span></span>
    * <span data-ttu-id="d0869-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="d0869-266">BooleanLabel</span></span>
    * <span data-ttu-id="d0869-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="d0869-267">BooleanScore</span></span>
    * <span data-ttu-id="d0869-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="d0869-268">BooleanAll</span></span>
    * <span data-ttu-id="d0869-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="d0869-269">CategoricalFeature</span></span>
    * <span data-ttu-id="d0869-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="d0869-270">CategoricalLabel</span></span>
    * <span data-ttu-id="d0869-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="d0869-271">CategoricalScore</span></span>
    * <span data-ttu-id="d0869-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="d0869-272">CategoricalAll</span></span>
    * <span data-ttu-id="d0869-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="d0869-273">StringFeature</span></span>
    * <span data-ttu-id="d0869-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="d0869-274">StringLabel</span></span>
    * <span data-ttu-id="d0869-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="d0869-275">StringScore</span></span>
    * <span data-ttu-id="d0869-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="d0869-276">StringAll</span></span>
    * <span data-ttu-id="d0869-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="d0869-277">AllLabel</span></span>
    * <span data-ttu-id="d0869-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="d0869-278">AllFeature</span></span>
    * <span data-ttu-id="d0869-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="d0869-279">AllScore</span></span>
    * <span data-ttu-id="d0869-280">Все</span><span class="sxs-lookup"><span data-stu-id="d0869-280">All</span></span>

<span data-ttu-id="d0869-281">**DropDown**— указанный пользователем пронумерованный (раскрывающийся) список.</span><span class="sxs-lookup"><span data-stu-id="d0869-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="d0869-282">Hello раскрывающийся список элементов, заданных в hello **свойства** элемента с помощью **элемента** элемент.</span><span class="sxs-lookup"><span data-stu-id="d0869-282">hello dropdown items are specified within hello **Properties** element using an **Item** element.</span></span> <span data-ttu-id="d0869-283">Hello **идентификатор** для каждого **элемент** должно быть уникальным и является допустимой переменной R.</span><span class="sxs-lookup"><span data-stu-id="d0869-283">hello **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="d0869-284">Здравствуйте, значение hello **имя** из **элемент** служит в качестве текста hello, вы видите и hello значению, переданному функции toohello R.</span><span class="sxs-lookup"><span data-stu-id="d0869-284">hello value of hello **name** of an **Item** serves as both hello text that you see and hello value that is passed toohello R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="d0869-285">*Необязательные свойства*:</span><span class="sxs-lookup"><span data-stu-id="d0869-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="d0869-286">**по умолчанию** - hello значение для свойства по умолчанию hello должен соответствовать со значением идентификатора из какого-либо hello **элемент** элементов.</span><span class="sxs-lookup"><span data-stu-id="d0869-286">**default** - hello value for hello default property must correspond with an id value from one of hello **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="d0869-287">Вспомогательные файлы</span><span class="sxs-lookup"><span data-stu-id="d0869-287">Auxiliary Files</span></span>
<span data-ttu-id="d0869-288">Любой файл, который помещается в ZIP-файл настраиваемого модуля является постоянной toobe доступны для использования во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="d0869-288">Any file that is placed in your custom module ZIP file is going toobe available for use during execution time.</span></span> <span data-ttu-id="d0869-289">Вся структура каталогов сохраняется.</span><span class="sxs-lookup"><span data-stu-id="d0869-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="d0869-290">Это означает, что работает считывания файла hello же локально и в выполнении машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d0869-290">This means that file sourcing works hello same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="d0869-291">Обратите внимание, что все файлы, извлеченные too'src "directory, чтобы все пути должны иметь ' src /" префикс.</span><span class="sxs-lookup"><span data-stu-id="d0869-291">Notice that all files are extracted too‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="d0869-292">Например предположим, требуется tooremove все строки, содержащие NAs из набора данных hello, а также удалить все повторяющиеся строки, перед выводом ее в CustomAddRows и уже написаны функцию R, который делает это в файле RemoveDupNARows.R:</span><span class="sxs-lookup"><span data-stu-id="d0869-292">For example, say you want tooremove any rows with NAs from hello dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="d0869-293">Может получать вспомогательного файла hello RemoveDupNARows.R hello CustomAddRows функции:</span><span class="sxs-lookup"><span data-stu-id="d0869-293">You can source hello auxiliary file RemoveDupNARows.R in hello CustomAddRows function:</span></span>

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

<span data-ttu-id="d0869-294">Затем передать ZIP-файл, содержащий CustomAddRows.R, CustomAddRows.xml и RemoveDupNARows.R, в качестве пользовательского R-модуля.</span><span class="sxs-lookup"><span data-stu-id="d0869-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="d0869-295">Среда выполнения</span><span class="sxs-lookup"><span data-stu-id="d0869-295">Execution Environment</span></span>
<span data-ttu-id="d0869-296">Hello среды выполнения для скрипта hello R использует hello же версии R как hello **выполнение скрипта R** модуля и может использовать hello же пакетов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d0869-296">hello execution environment for hello R script uses hello same version of R as hello **Execute R Script** module and can use hello same default packages.</span></span> <span data-ttu-id="d0869-297">Можно также добавить дополнительные R пакеты tooyour пользовательского модуля, включая их в ZIP-пакет hello пользовательский модуль.</span><span class="sxs-lookup"><span data-stu-id="d0869-297">You can also add additional R packages tooyour custom module by including them in hello custom module zip package.</span></span> <span data-ttu-id="d0869-298">Просто загрузите их в R-скрипт так же, как в среду R.</span><span class="sxs-lookup"><span data-stu-id="d0869-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="d0869-299">**Ограничения для среды выполнения hello** включают:</span><span class="sxs-lookup"><span data-stu-id="d0869-299">**Limitations of hello execution environment** include:</span></span>

* <span data-ttu-id="d0869-300">Временный файловая система: файлы, записанные при выполнении пользовательского модуля hello не сохраняются между несколькими запусками hello одного модуля.</span><span class="sxs-lookup"><span data-stu-id="d0869-300">Non-persistent file system: Files written when hello custom module is run are not persisted across multiple runs of hello same module.</span></span>
* <span data-ttu-id="d0869-301">Нет доступа к сети</span><span class="sxs-lookup"><span data-stu-id="d0869-301">No network access</span></span>

