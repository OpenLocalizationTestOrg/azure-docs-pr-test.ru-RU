---
title: "aaaLearning рабочий процесс PowerShell для автоматизации Azure | Документы Microsoft"
description: "Эта статья предназначена как краткий обзор для разработчиков знакомы с PowerShell toounderstand hello конкретные различия в PowerShell и рабочий процесс PowerShell и модулей Runbook применимо tooAutomation основные понятия."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="72904-103">Изучение основных понятий рабочего процесса Windows PowerShell для модулей Runbook службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="72904-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="72904-104">Модули Runbook в службе автоматизации Azure реализованы в виде рабочих процессов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72904-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="72904-105">Рабочий процесс Windows PowerShell является аналогичный сценарий Windows PowerShell tooa, но имеет ряд существенных отличий, которые могут быть сложными tooa нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="72904-105">A Windows PowerShell Workflow is similar tooa Windows PowerShell script but has some significant differences that can be confusing tooa new user.</span></span>  <span data-ttu-id="72904-106">В данной статье предполагаемого toohelp записи модулей Runbook с помощью рабочего процесса PowerShell, мы рекомендуем запись модулей Runbook с помощью PowerShell, если не требуется контрольные точки.</span><span class="sxs-lookup"><span data-stu-id="72904-106">While this article is intended toohelp you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="72904-107">Существует несколько различий синтаксис при создании и настройке модулей Runbook рабочего процесса PowerShell, и эти различия требуют немного больше рабочих процессов действующие toowrite.</span><span class="sxs-lookup"><span data-stu-id="72904-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work toowrite effective workflows.</span></span>  

<span data-ttu-id="72904-108">Рабочий процесс — это последовательность связанных операций программируемых, в которых выполняются длительные задачи или требуют координации нескольких действий hello на нескольких устройствах или управляемых узлах.</span><span class="sxs-lookup"><span data-stu-id="72904-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require hello coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="72904-109">Hello преимущества рабочего процесса через обычный сценарий — возможность hello toosimultaneously выполнения действия с несколькими устройствами и tooautomatically hello возможность восстановления после сбоев.</span><span class="sxs-lookup"><span data-stu-id="72904-109">hello benefits of a workflow over a normal script include hello ability toosimultaneously perform an action against multiple devices and hello ability tooautomatically recover from failures.</span></span> <span data-ttu-id="72904-110">Рабочий процесс Windows PowerShell представляет собой сценарий Windows PowerShell, использующий Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="72904-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="72904-111">Хотя рабочий процесс hello написанным с использованием синтаксиса Windows PowerShell и запускается Windows PowerShell, обрабатывается он Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="72904-111">While hello workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="72904-112">Дополнительные сведения по темам hello в этой статье в разделе [Приступая к работе с Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="72904-112">For complete details on hello topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="72904-113">Базовая структура рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="72904-113">Basic structure of a workflow</span></span>
<span data-ttu-id="72904-114">Hello tooconverting первый шаг рабочего процесса PowerShell tooa сценария PowerShell заключать с hello **рабочего процесса** ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="72904-114">hello first step tooconverting a PowerShell script tooa PowerShell workflow is enclosing it with hello **Workflow** keyword.</span></span>  <span data-ttu-id="72904-115">Рабочий процесс начинается с hello **рабочего процесса** ключевое слово и текст hello hello сценария, заключенное в фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="72904-115">A workflow starts with hello **Workflow** keyword followed by hello body of hello script enclosed in braces.</span></span> <span data-ttu-id="72904-116">Имя рабочего процесса hello Hello соответствует hello **рабочего процесса** ключевое слово, как показано в hello, используя синтаксис:</span><span class="sxs-lookup"><span data-stu-id="72904-116">hello name of hello workflow follows hello **Workflow** keyword as shown in hello following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="72904-117">Имя Hello hello рабочего процесса должно соответствовать имени hello hello Runbook службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="72904-117">hello name of hello workflow must match hello name of hello Automation runbook.</span></span> <span data-ttu-id="72904-118">Если импортируется hello runbook, то hello имя файла должно совпадать с именем hello рабочего процесса и должны оканчиваться на *.ps1*.</span><span class="sxs-lookup"><span data-stu-id="72904-118">If hello runbook is being imported, then hello filename must match hello workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="72904-119">tooadd параметры toohello рабочего процесса используйте hello **Param** так же, как сценарий tooa ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="72904-119">tooadd parameters toohello workflow, use hello **Param** keyword just as you would tooa script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="72904-120">Изменения в коде</span><span class="sxs-lookup"><span data-stu-id="72904-120">Code changes</span></span>
<span data-ttu-id="72904-121">Код рабочего процесса PowerShell выглядит код скрипта tooPowerShell почти так же, за исключением несколько значительных изменений.</span><span class="sxs-lookup"><span data-stu-id="72904-121">PowerShell workflow code looks almost identical tooPowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="72904-122">Hello в следующих разделах описываются изменения, что необходимый сценарий PowerShell tooa toomake toorun в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="72904-122">hello following sections describe changes that you need toomake tooa PowerShell script for it toorun in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="72904-123">Действия</span><span class="sxs-lookup"><span data-stu-id="72904-123">Activities</span></span>
<span data-ttu-id="72904-124">Действие — это конкретная задача в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="72904-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="72904-125">Так же как скрипт состоит из одной или нескольких команд, рабочий процесс состоит из одного или нескольких действий, которые выполняются в последовательности.</span><span class="sxs-lookup"><span data-stu-id="72904-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="72904-126">Рабочий процесс Windows PowerShell автоматически преобразует многие hello tooactivities командлеты Windows PowerShell при запуске рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="72904-126">Windows PowerShell Workflow automatically converts many of hello Windows PowerShell cmdlets tooactivities when it runs a workflow.</span></span> <span data-ttu-id="72904-127">При указании одного из этих командлетов в модуле runbook hello соответствующее действие выполняется в Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="72904-127">When you specify one of these cmdlets in your runbook, hello corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="72904-128">Для командлетов без соответствующего действия рабочего процесса Windows PowerShell автоматически запускает командлет hello в [InlineScript](#inlinescript) действия.</span><span class="sxs-lookup"><span data-stu-id="72904-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs hello cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="72904-129">Существует набор командлетов, которые исключаются и не могут использоваться в рабочем процессе, если они явно не включены в блок InlineScript.</span><span class="sxs-lookup"><span data-stu-id="72904-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="72904-130">Дополнительные сведения об этих понятиях см. в статье [Использование действий в рабочих процессах сценариев](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="72904-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="72904-131">Действия рабочих процессов используют набор общих параметров tooconfigure их работу.</span><span class="sxs-lookup"><span data-stu-id="72904-131">Workflow activities share a set of common parameters tooconfigure their operation.</span></span> <span data-ttu-id="72904-132">Дополнительные сведения об общих параметрах hello рабочего процесса см. в разделе [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="72904-132">For details about hello workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="72904-133">Позиционные параметры</span><span class="sxs-lookup"><span data-stu-id="72904-133">Positional parameters</span></span>
<span data-ttu-id="72904-134">Позиционные параметры нельзя использовать с действиями и командлетами в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="72904-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="72904-135">Это означает, что пользоваться необходимо именами параметров.</span><span class="sxs-lookup"><span data-stu-id="72904-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="72904-136">Например рассмотрим следующий код, который получает все службы, работающей hello.</span><span class="sxs-lookup"><span data-stu-id="72904-136">For example, consider hello following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="72904-137">При попытке toorun этот же код в рабочем процессе, появится сообщение, как «Не удается разрешить набор hello указан с помощью параметра именованные параметры.»</span><span class="sxs-lookup"><span data-stu-id="72904-137">If you try toorun this same code in a workflow, you receive a message like "Parameter set cannot be resolved using hello specified named parameters."</span></span>  <span data-ttu-id="72904-138">toocorrect это, укажите имя параметра hello, как показано ниже hello.</span><span class="sxs-lookup"><span data-stu-id="72904-138">toocorrect this, provide hello parameter name as in hello following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="72904-139">Десериализованные объекты</span><span class="sxs-lookup"><span data-stu-id="72904-139">Deserialized objects</span></span>
<span data-ttu-id="72904-140">Объекты в рабочих процессах десериализуются.</span><span class="sxs-lookup"><span data-stu-id="72904-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="72904-141">Это означает, что их свойства по-прежнему доступны, а методы — нет.</span><span class="sxs-lookup"><span data-stu-id="72904-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="72904-142">Например рассмотрим следующий код PowerShell, который останавливает службу, с помощью метода Stop hello объекта службы hello hello.</span><span class="sxs-lookup"><span data-stu-id="72904-142">For example, consider hello following PowerShell code that stops a service using hello Stop method of hello Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="72904-143">Если вы сделаете toorun это в рабочем процессе, появится сообщение об ошибке «вызов метода не поддерживается в рабочем процессе Windows PowerShell».</span><span class="sxs-lookup"><span data-stu-id="72904-143">If you try toorun this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="72904-144">Один из вариантов — toowrap эти две строки кода в [InlineScript](#inlinescript) блока, в этом случае $Service бы внутри блока hello объекта службы.</span><span class="sxs-lookup"><span data-stu-id="72904-144">One option is toowrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within hello block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="72904-145">Другой вариант — toouse другой командлет, который выполняет hello же функциональность, что метод hello, если он доступен.</span><span class="sxs-lookup"><span data-stu-id="72904-145">Another option is toouse another cmdlet that performs hello same functionality as hello method, if one is available.</span></span>  <span data-ttu-id="72904-146">В нашем примере hello Stop-Service предоставляет hello же функциональность, что метод остановки hello и использовать следующие hello для рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="72904-146">In our sample, hello Stop-Service cmdlet provides hello same functionality as hello Stop method, and you could use hello following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="72904-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="72904-147">InlineScript</span></span>
<span data-ttu-id="72904-148">Hello **InlineScript** действия полезно, если требуется toorun одной или нескольких команд как традиционный сценарий PowerShell вместо рабочего процесса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72904-148">hello **InlineScript** activity is useful when you need toorun one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="72904-149">Во время обработки команды в рабочем процессе отправляются tooWindows Workflow Foundation, команды в блоке InlineScript обрабатываются Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72904-149">While commands in a workflow are sent tooWindows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="72904-150">InlineScript использует синтаксис, показанный ниже hello.</span><span class="sxs-lookup"><span data-stu-id="72904-150">InlineScript uses hello following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="72904-151">Может возвращать выходные данные из InlineScript, назначив hello выходной tooa переменной.</span><span class="sxs-lookup"><span data-stu-id="72904-151">You can return output from an InlineScript by assigning hello output tooa variable.</span></span> <span data-ttu-id="72904-152">Hello следующий пример останавливает службу и затем выводит имя службы hello.</span><span class="sxs-lookup"><span data-stu-id="72904-152">hello following example stops a service and then outputs hello service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="72904-153">Значения можно передавать в блок InlineScript, но при этом необходимо использовать модификатор области **$Using** .</span><span class="sxs-lookup"><span data-stu-id="72904-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="72904-154">Hello ниже приведен предыдущий пример идентичные toohello за исключением того, что hello службы предоставляет имя переменной.</span><span class="sxs-lookup"><span data-stu-id="72904-154">hello following example is identical toohello previous example except that hello service name is provided by a variable.</span></span>

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="72904-155">Во время действия InlineScript могут быть критическими в определенных рабочих процессов, они не поддерживают конструкции рабочего процесса и должен использоваться только при необходимости для hello следующих причин:</span><span class="sxs-lookup"><span data-stu-id="72904-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for hello following reasons:</span></span>

* <span data-ttu-id="72904-156">[Контрольные точки](#checkpoints) в блоке InlineScript не используются.</span><span class="sxs-lookup"><span data-stu-id="72904-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="72904-157">В случае сбоя в блоке hello должна быть возобновлена из hello начало блока hello.</span><span class="sxs-lookup"><span data-stu-id="72904-157">If a failure occurs within hello block, it must be resumed from hello beginning of hello block.</span></span>
* <span data-ttu-id="72904-158">[Параллельное выполнение](#parallel-processing) в блоке InlineScript не используется.</span><span class="sxs-lookup"><span data-stu-id="72904-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="72904-159">InlineScript влияет на масштабируемость hello рабочего процесса, поскольку содержит сеанс Windows PowerShell hello для hello всю длину блока InlineScript hello.</span><span class="sxs-lookup"><span data-stu-id="72904-159">InlineScript affects scalability of hello workflow since it holds hello Windows PowerShell session for hello entire length of hello InlineScript block.</span></span>

<span data-ttu-id="72904-160">Дополнительные сведения об использовании InlineScript см. в статьях [Выполнение команд Windows PowerShell в рабочем процессе](http://technet.microsoft.com/library/jj574197.aspx) и [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="72904-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="72904-161">Параллельная обработка</span><span class="sxs-lookup"><span data-stu-id="72904-161">Parallel processing</span></span>
<span data-ttu-id="72904-162">Одно из преимуществ рабочих процессов Windows PowerShell является возможность tooperform hello набор команд параллельно, а не последовательно как и в стандартном сценарии.</span><span class="sxs-lookup"><span data-stu-id="72904-162">One advantage of Windows PowerShell Workflows is hello ability tooperform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="72904-163">Можно использовать hello **параллельных** ключевое слово toocreate блок сценария с несколькими командами, которые выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="72904-163">You can use hello **Parallel** keyword toocreate a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="72904-164">В этом случае используется синтаксис, показанный ниже hello.</span><span class="sxs-lookup"><span data-stu-id="72904-164">This uses hello following syntax shown below.</span></span> <span data-ttu-id="72904-165">В этом случае действия Activity1 и Activity2 начинается hello то же время.</span><span class="sxs-lookup"><span data-stu-id="72904-165">In this case, Activity1 and Activity2 starts at hello same time.</span></span> <span data-ttu-id="72904-166">Действие Activity3 запускается только после завершения действий Activity1 и Activity2.</span><span class="sxs-lookup"><span data-stu-id="72904-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="72904-167">Например рассмотрим следующие команды PowerShell, предназначенных для копирования нескольких файлов tooa сетевым адресом hello.</span><span class="sxs-lookup"><span data-stu-id="72904-167">For example, consider hello following PowerShell commands that copy multiple files tooa network destination.</span></span>  <span data-ttu-id="72904-168">Эти команды выполняются последовательно, поэтому данный файл необходимо завершить копирование до hello после запуска.</span><span class="sxs-lookup"><span data-stu-id="72904-168">These commands are run sequentially so that one file must finish copying before hello next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="72904-169">Hello следующий рабочий процесс запускает эти же параллельный команд, чтобы все они начинается копирование hello же время.</span><span class="sxs-lookup"><span data-stu-id="72904-169">hello following workflow runs these same commands in parallel so that they all start copying at hello same time.</span></span>  <span data-ttu-id="72904-170">Только после того, что все они являются скопировать сообщение о завершении hello отображается.</span><span class="sxs-lookup"><span data-stu-id="72904-170">Only after they are all copied is hello completion message displayed.</span></span>

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


<span data-ttu-id="72904-171">Можно использовать hello **ForEach-Parallel** одновременно составлять команды tooprocess для каждого элемента в коллекции.</span><span class="sxs-lookup"><span data-stu-id="72904-171">You can use hello **ForEach -Parallel** construct tooprocess commands for each item in a collection concurrently.</span></span> <span data-ttu-id="72904-172">Hello элементов в коллекции hello обрабатываются параллельно, а hello команды в блоке сценария hello выполняются последовательно.</span><span class="sxs-lookup"><span data-stu-id="72904-172">hello items in hello collection are processed in parallel while hello commands in hello script block run sequentially.</span></span> <span data-ttu-id="72904-173">В этом случае используется синтаксис, показанный ниже hello.</span><span class="sxs-lookup"><span data-stu-id="72904-173">This uses hello following syntax shown below.</span></span> <span data-ttu-id="72904-174">В этом случае действия Activity1 начинается hello же время для всех элементов в коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="72904-174">In this case, Activity1 starts at hello same time for all items in hello collection.</span></span> <span data-ttu-id="72904-175">Для каждого элемента действие Activity2 запускается после завершения действия Activity1.</span><span class="sxs-lookup"><span data-stu-id="72904-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="72904-176">Действие Activity3 запускается только после завершения действий Activity1 и Activity2 для всех элементов.</span><span class="sxs-lookup"><span data-stu-id="72904-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="72904-177">Следующий пример Hello — аналогично предыдущего примера toohello копирование файлов в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="72904-177">hello following example is similar toohello previous example copying files in parallel.</span></span>  <span data-ttu-id="72904-178">В данном случае после копирования каждого файла отображается отдельное сообщение.</span><span class="sxs-lookup"><span data-stu-id="72904-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="72904-179">Только после того, что все они являются полностью копируются строительства приветственных сообщений отображается.</span><span class="sxs-lookup"><span data-stu-id="72904-179">Only after they are all completely copied is hello final completion message displayed.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> <span data-ttu-id="72904-180">Не рекомендуется параллельно выполняемого дочерние модули Runbook, так как это было показано toogive недостоверным результатам.</span><span class="sxs-lookup"><span data-stu-id="72904-180">We do not recommend running child runbooks in parallel since this has been shown toogive unreliable results.</span></span>  <span data-ttu-id="72904-181">Hello выходные данные дочернего модуля hello иногда не отображаются, и параметры в один дочерний модуль может повлиять на другие параллельные дочерние модули hello</span><span class="sxs-lookup"><span data-stu-id="72904-181">hello output from hello child runbook sometimes does not show up, and settings in one child runbook can affect hello other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="72904-182">Контрольные точки</span><span class="sxs-lookup"><span data-stu-id="72904-182">Checkpoints</span></span>
<span data-ttu-id="72904-183">Объект *контрольной точки* представляет собой моментальный снимок текущего состояния hello hello рабочего процесса, включающего hello текущие значения переменных и любые выходные данные созданного toothat точки.</span><span class="sxs-lookup"><span data-stu-id="72904-183">A *checkpoint* is a snapshot of hello current state of hello workflow that includes hello current value for variables and any output generated toothat point.</span></span> <span data-ttu-id="72904-184">Если рабочий процесс завершается по ошибке или приостановлена, затем hello очередном запуске он будет запущен в последней контрольной точки вместо запуска hello отсечения hello.</span><span class="sxs-lookup"><span data-stu-id="72904-184">If a workflow ends in error or is suspended, then hello next time it is run it will start from its last checkpoint instead of hello start of hello worfklow.</span></span>  <span data-ttu-id="72904-185">Можно установить контрольную точку в рабочем процессе с hello **Checkpoint-Workflow** действия.</span><span class="sxs-lookup"><span data-stu-id="72904-185">You can set a checkpoint in a workflow with hello **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="72904-186">В следующий образец кода hello исключение возникает после вызывает Activity2 hello tooend рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="72904-186">In hello following sample code, an exception occurs after Activity2 causing hello workflow tooend.</span></span> <span data-ttu-id="72904-187">При повторном запуске hello рабочего процесса, оно начинается с запуска Activity2, поскольку это действие было сразу после hello последней заданной контрольной точки.</span><span class="sxs-lookup"><span data-stu-id="72904-187">When hello workflow is run again, it starts by running Activity2 since this was just after hello last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="72904-188">Необходимо задать контрольные точки в рабочий процесс после действия, которые могут быть подвержены tooexception и не должны повторяться при возобновлении рабочего процесса hello.</span><span class="sxs-lookup"><span data-stu-id="72904-188">You should set checkpoints in a workflow after activities that may be prone tooexception and should not be repeated if hello workflow is resumed.</span></span> <span data-ttu-id="72904-189">Допустим, рабочий процесс создает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="72904-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="72904-190">Контрольную точку можно задать до и после hello команды toocreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="72904-190">You could set a checkpoint both before and after hello commands toocreate hello virtual machine.</span></span> <span data-ttu-id="72904-191">Создание hello завершается сбоем, hello команды будет повторяется, если hello рабочий процесс запускается снова.</span><span class="sxs-lookup"><span data-stu-id="72904-191">If hello creation fails, then hello commands would be repeated if hello workflow is started again.</span></span> <span data-ttu-id="72904-192">В случае отсечения hello после успешного создания hello, затем hello виртуальной машины не создается повторно при возобновлении рабочего процесса hello.</span><span class="sxs-lookup"><span data-stu-id="72904-192">If hello worfklow fails after hello creation succeeds, then hello virtual machine will not be created again when hello workflow is resumed.</span></span>

<span data-ttu-id="72904-193">Следующий пример Hello копирует несколько файлов tooa сетевое расположение и устанавливает контрольную точку после каждого файла.</span><span class="sxs-lookup"><span data-stu-id="72904-193">hello following example copies multiple files tooa network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="72904-194">В случае утери hello сетевое расположение hello рабочий процесс завершается по ошибке.</span><span class="sxs-lookup"><span data-stu-id="72904-194">If hello network location is lost, then hello workflow ends in error.</span></span>  <span data-ttu-id="72904-195">Когда запускается снова, она будет возобновлено в hello последней контрольной точки, это означает, что только hello файлы, которые уже были скопированы, пропускаются.</span><span class="sxs-lookup"><span data-stu-id="72904-195">When it is started again, it will resume at hello last checkpoint meaning that only hello files that have already been copied are skipped.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

<span data-ttu-id="72904-196">Поскольку учетные данные пользователя не сохраняются после вызова метода hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) действия или после последней контрольной точки hello должны toonull учетные данные tooset hello, а затем извлечение их снова из хранилища активов hello после  **Suspend-Workflow** или контрольной точки вызывается.</span><span class="sxs-lookup"><span data-stu-id="72904-196">Because username credentials are not persisted after you call hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after hello last checkpoint, you need tooset hello credentials toonull and then retrieve them again from hello asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="72904-197">В противном случае может появиться сообщение об ошибке после hello: *hello задания рабочего процесса нельзя возобновить, либо из-за постоянного хранения данных не удалось сохранить полностью, или сохранить сохраняемости данные повреждены. Необходимо перезапустить рабочий процесс hello.*</span><span class="sxs-lookup"><span data-stu-id="72904-197">Otherwise, you may receive hello following error message: *hello workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart hello workflow.*</span></span>

<span data-ttu-id="72904-198">Hello после того же кода показано, как toohandle это в модулях Runbook рабочего процесса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72904-198">hello following same code demonstrates how toohandle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="72904-199">Это не обязательно делать, если вы проходите проверку подлинности с помощью учетной записи запуска от имени, настроенной с помощью субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="72904-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="72904-200">Дополнительные сведения о контрольных точках см. в разделе [tooa добавление контрольных точек рабочего процесса сценария](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="72904-200">For more information about checkpoints, see [Adding Checkpoints tooa Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72904-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="72904-201">Next steps</span></span>
* <span data-ttu-id="72904-202">tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="72904-202">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
