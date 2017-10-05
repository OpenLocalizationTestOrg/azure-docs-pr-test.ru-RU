---
title: "Изучение рабочего процесса PowerShell для службы автоматизации Azure | Документация Майкрософт"
description: "Данная статья предназначена для разработчиков, уже знакомых с PowerShell. В ней рассматриваются различия между PowerShell и рабочим процессом PowerShell, а также понятия, относящиеся к модулям Runbook службы автоматизации."
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
ms.openlocfilehash: 4de812c7f863e42a6ed10c2312d61b8377e06431
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="c37b2-103">Изучение основных понятий рабочего процесса Windows PowerShell для модулей Runbook службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="c37b2-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="c37b2-104">Модули Runbook в службе автоматизации Azure реализованы в виде рабочих процессов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c37b2-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="c37b2-105">Рабочий процесс Windows PowerShell похож на сценарий Windows PowerShell, но имеет ряд существенных отличий, которые могут запутать нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="c37b2-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span></span>  <span data-ttu-id="c37b2-106">Хотя эта статья предназначена помочь вам в написании модулей Runbook с помощью рабочего процесса PowerShell, мы рекомендуем использовать для этого PowerShell, если только вам не требуются контрольные точки.</span><span class="sxs-lookup"><span data-stu-id="c37b2-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="c37b2-107">Существует ряд различий в синтаксисе при разработке модулей runbook рабочего процесса PowerShell, и эти различия требуют немного больше усилий для написания эффективных рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="c37b2-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span></span>  

<span data-ttu-id="c37b2-108">Рабочий процесс представляет собой последовательность запрограммированных взаимосвязанных шагов для выполнения долгосрочных задач или требует координации шагов на множестве устройств или управляемых узлах.</span><span class="sxs-lookup"><span data-stu-id="c37b2-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="c37b2-109">Преимущества рабочего процесса в сравнении с использованием обычного скрипта заключаются в возможности одновременного выполнения действия по отношению ко многим устройствам и в возможности автоматического восстановления при сбоях.</span><span class="sxs-lookup"><span data-stu-id="c37b2-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span></span> <span data-ttu-id="c37b2-110">Рабочий процесс Windows PowerShell представляет собой сценарий Windows PowerShell, использующий Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="c37b2-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="c37b2-111">В то время как рабочий процесс прописан в синтаксисе Windows PowerShell и запускается Windows PowerShell, его обработка выполняется в Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="c37b2-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="c37b2-112">Дополнительные сведения по темам, рассмотренным в этой статье, см. на странице [Общие сведения о рабочем процессе Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="c37b2-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="c37b2-113">Базовая структура рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="c37b2-113">Basic structure of a workflow</span></span>
<span data-ttu-id="c37b2-114">Первый шаг к преобразованию сценария PowerShell в рабочий процесс PowerShell — это добавление ключевого слова **Workflow** .</span><span class="sxs-lookup"><span data-stu-id="c37b2-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span></span>  <span data-ttu-id="c37b2-115">Рабочий процесс начинается с ключевого слова **Workflow** , за которым следует текст сценария, заключенный в фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="c37b2-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span></span> <span data-ttu-id="c37b2-116">Имя рабочего процесса следует за ключевым словом **Workflow**, как это показано в следующем синтаксисе:</span><span class="sxs-lookup"><span data-stu-id="c37b2-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="c37b2-117">Имя рабочего процесса должно соответствовать имени модуля Runbook в службе автоматизации.</span><span class="sxs-lookup"><span data-stu-id="c37b2-117">The name of the workflow must match the name of the Automation runbook.</span></span> <span data-ttu-id="c37b2-118">При импорте модуля runbook имя файла должно соответствовать имени рабочего процесса и заканчиваться на *.ps1*.</span><span class="sxs-lookup"><span data-stu-id="c37b2-118">If the runbook is being imported, then the filename must match the workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="c37b2-119">Чтобы добавить параметры в рабочий процесс, используйте ключевое слово **Param** (как и в случае сценария).</span><span class="sxs-lookup"><span data-stu-id="c37b2-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="c37b2-120">Изменения в коде</span><span class="sxs-lookup"><span data-stu-id="c37b2-120">Code changes</span></span>
<span data-ttu-id="c37b2-121">Код рабочего процесса PowerShell выглядит почти так же, как код сценария PowerShell, но с некоторыми существенными изменениями.</span><span class="sxs-lookup"><span data-stu-id="c37b2-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="c37b2-122">В следующих разделах описываются изменения, которые нужно внести в сценарий PowerShell, чтобы он выполнялся как рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="c37b2-122">The following sections describe changes that you need to make to a PowerShell script for it to run in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="c37b2-123">Действия</span><span class="sxs-lookup"><span data-stu-id="c37b2-123">Activities</span></span>
<span data-ttu-id="c37b2-124">Действие — это конкретная задача в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="c37b2-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="c37b2-125">Так же как скрипт состоит из одной или нескольких команд, рабочий процесс состоит из одного или нескольких действий, которые выполняются в последовательности.</span><span class="sxs-lookup"><span data-stu-id="c37b2-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="c37b2-126">Рабочий процесс Windows PowerShell автоматически преобразует множество командлетов Windows PowerShell в действия при выполнении рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="c37b2-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span></span> <span data-ttu-id="c37b2-127">Если указать один из этих командлетов в модуле runbook, соответствующее действие запускается в Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="c37b2-127">When you specify one of these cmdlets in your runbook, the corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="c37b2-128">Для командлетов, для которых не существует соответствующего действия, рабочий процесс Windows PowerShell автоматически запустит командлет в действии [InlineScript](#inlinescript).</span><span class="sxs-lookup"><span data-stu-id="c37b2-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="c37b2-129">Существует набор командлетов, которые исключаются и не могут использоваться в рабочем процессе, если они явно не включены в блок InlineScript.</span><span class="sxs-lookup"><span data-stu-id="c37b2-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="c37b2-130">Дополнительные сведения об этих понятиях см. в статье [Использование действий в рабочих процессах сценариев](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="c37b2-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="c37b2-131">Действия рабочих процессов совместно используют набор общих параметров для настройки их работы.</span><span class="sxs-lookup"><span data-stu-id="c37b2-131">Workflow activities share a set of common parameters to configure their operation.</span></span> <span data-ttu-id="c37b2-132">Сведения об общих параметрах рабочего процесса см. в статье [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="c37b2-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="c37b2-133">Позиционные параметры</span><span class="sxs-lookup"><span data-stu-id="c37b2-133">Positional parameters</span></span>
<span data-ttu-id="c37b2-134">Позиционные параметры нельзя использовать с действиями и командлетами в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="c37b2-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="c37b2-135">Это означает, что пользоваться необходимо именами параметров.</span><span class="sxs-lookup"><span data-stu-id="c37b2-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="c37b2-136">Рассмотрим, например, следующий код, получающий список всех запущенных служб.</span><span class="sxs-lookup"><span data-stu-id="c37b2-136">For example, consider the following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="c37b2-137">Попытавшись выполнить этот код в рабочем процессе, вы получите сообщение следующего вида: "Невозможно разрешить набор параметров, используя указанные параметры с именами".</span><span class="sxs-lookup"><span data-stu-id="c37b2-137">If you try to run this same code in a workflow, you receive a message like "Parameter set cannot be resolved using the specified named parameters."</span></span>  <span data-ttu-id="c37b2-138">Чтобы устранить эту проблему, достаточно указать имя параметра в представленном ниже формате.</span><span class="sxs-lookup"><span data-stu-id="c37b2-138">To correct this, provide the parameter name as in the following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="c37b2-139">Десериализованные объекты</span><span class="sxs-lookup"><span data-stu-id="c37b2-139">Deserialized objects</span></span>
<span data-ttu-id="c37b2-140">Объекты в рабочих процессах десериализуются.</span><span class="sxs-lookup"><span data-stu-id="c37b2-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="c37b2-141">Это означает, что их свойства по-прежнему доступны, а методы — нет.</span><span class="sxs-lookup"><span data-stu-id="c37b2-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="c37b2-142">Рассмотрим, например, следующий код PowerShell, который останавливает службу с помощью метода Stop объекта Service.</span><span class="sxs-lookup"><span data-stu-id="c37b2-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="c37b2-143">При попытке выполнить этот код в рабочем процессе вы получите сообщение об ошибке "Вызов метода не поддерживается в рабочем процессе Windows PowerShell".</span><span class="sxs-lookup"><span data-stu-id="c37b2-143">If you try to run this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="c37b2-144">Один вариант — перенести эти две строки кода в блок [InlineScript](#inlinescript), в случае чего $Service станет объектом службы в блоке.</span><span class="sxs-lookup"><span data-stu-id="c37b2-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="c37b2-145">Второй путь — использовать другой командлет, который выполняет те же функции, что и метод, если такой командлет существует.</span><span class="sxs-lookup"><span data-stu-id="c37b2-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span></span>  <span data-ttu-id="c37b2-146">В нашем примере командлет Stop-Service выполняет те же функции, что и метод Stop, поэтому для рабочего процесса можно использовать следующий код.</span><span class="sxs-lookup"><span data-stu-id="c37b2-146">In our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="c37b2-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="c37b2-147">InlineScript</span></span>
<span data-ttu-id="c37b2-148">Действие **InlineScript** пригодится, если вам нужно выполнить одну или несколько команд, используя не рабочий процесс, а традиционный сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c37b2-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="c37b2-149">Пока команды в рабочем процессе отправляются в Windows Workflow Foundation для обработки, команды в блоке InlineScript обрабатываются при помощи Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c37b2-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="c37b2-150">InlineScript использует описанный ниже синтаксис.</span><span class="sxs-lookup"><span data-stu-id="c37b2-150">InlineScript uses the following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="c37b2-151">Для получения выходных данных из InlineScript можно присвоить им переменную.</span><span class="sxs-lookup"><span data-stu-id="c37b2-151">You can return output from an InlineScript by assigning the output to a variable.</span></span> <span data-ttu-id="c37b2-152">Код в приведенном ниже примере останавливает службу и выдает ее имя.</span><span class="sxs-lookup"><span data-stu-id="c37b2-152">The following example stops a service and then outputs the service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="c37b2-153">Значения можно передавать в блок InlineScript, но при этом необходимо использовать модификатор области **$Using** .</span><span class="sxs-lookup"><span data-stu-id="c37b2-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="c37b2-154">Приведенный ниже пример идентичен предыдущему за исключением того, что имя службы предоставляется переменной.</span><span class="sxs-lookup"><span data-stu-id="c37b2-154">The following example is identical to the previous example except that the service name is provided by a variable.</span></span>

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


<span data-ttu-id="c37b2-155">В то время как выполнение действий InlineScript может быть критически важно в некоторых рабочих процессах, они не поддерживают конструкции рабочих процессов и должны использоваться тогда, когда это необходимо по следующим причинам.</span><span class="sxs-lookup"><span data-stu-id="c37b2-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span></span>

* <span data-ttu-id="c37b2-156">[Контрольные точки](#checkpoints) в блоке InlineScript не используются.</span><span class="sxs-lookup"><span data-stu-id="c37b2-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="c37b2-157">Если в блоке происходит сбой, его выполнение должно быть возобновлено с начала блока.</span><span class="sxs-lookup"><span data-stu-id="c37b2-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span></span>
* <span data-ttu-id="c37b2-158">[Параллельное выполнение](#parallel-processing) в блоке InlineScript не используется.</span><span class="sxs-lookup"><span data-stu-id="c37b2-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="c37b2-159">InlineScript влияет на масштабируемость рабочего процесса, поскольку содержит сеанс Windows PowerShell для всей продолжительности блока InlineScript.</span><span class="sxs-lookup"><span data-stu-id="c37b2-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span></span>

<span data-ttu-id="c37b2-160">Дополнительные сведения об использовании InlineScript см. в статьях [Выполнение команд Windows PowerShell в рабочем процессе](http://technet.microsoft.com/library/jj574197.aspx) и [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="c37b2-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="c37b2-161">Параллельная обработка</span><span class="sxs-lookup"><span data-stu-id="c37b2-161">Parallel processing</span></span>
<span data-ttu-id="c37b2-162">Одним из преимуществ рабочих процессов Windows PowerShell является возможность выполнять набор команд параллельно, а не последовательно, как это делается в стандартном скрипте.</span><span class="sxs-lookup"><span data-stu-id="c37b2-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="c37b2-163">Можно использовать ключевое слово **Parallel**, чтобы создать блок сценария с несколькими командами, которые выполняются параллельно.</span><span class="sxs-lookup"><span data-stu-id="c37b2-163">You can use the **Parallel** keyword to create a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="c37b2-164">Для этого используется описанный ниже синтаксис.</span><span class="sxs-lookup"><span data-stu-id="c37b2-164">This uses the following syntax shown below.</span></span> <span data-ttu-id="c37b2-165">В этом случае действия Activity1 и Activity2 запускаются одновременно.</span><span class="sxs-lookup"><span data-stu-id="c37b2-165">In this case, Activity1 and Activity2 starts at the same time.</span></span> <span data-ttu-id="c37b2-166">Действие Activity3 запускается только после завершения действий Activity1 и Activity2.</span><span class="sxs-lookup"><span data-stu-id="c37b2-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="c37b2-167">Рассмотрим, например, приведенные ниже команды PowerShell, которые копируют несколько файлов в определенный узел сети.</span><span class="sxs-lookup"><span data-stu-id="c37b2-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span></span>  <span data-ttu-id="c37b2-168">Команды выполняются последовательно, поэтому следующий файл не копируется, пока не закончится копирование предыдущего.</span><span class="sxs-lookup"><span data-stu-id="c37b2-168">These commands are run sequentially so that one file must finish copying before the next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="c37b2-169">Приведенный ниже рабочий процесс выполняет те же команды параллельно, так что все файлы копируются одновременно.</span><span class="sxs-lookup"><span data-stu-id="c37b2-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span></span>  <span data-ttu-id="c37b2-170">При этом сообщение о завершении отображается только после того, как все файлы будут скопированы.</span><span class="sxs-lookup"><span data-stu-id="c37b2-170">Only after they are all copied is the completion message displayed.</span></span>

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


<span data-ttu-id="c37b2-171">Можно использовать конструкцию **ForEach -Parallel** для обработки команд для каждого элемента в коллекции одновременно.</span><span class="sxs-lookup"><span data-stu-id="c37b2-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span></span> <span data-ttu-id="c37b2-172">Элементы в коллекции обрабатываются параллельно, а команды в блоке скрипта выполняются последовательно.</span><span class="sxs-lookup"><span data-stu-id="c37b2-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span></span> <span data-ttu-id="c37b2-173">Для этого используется описанный ниже синтаксис.</span><span class="sxs-lookup"><span data-stu-id="c37b2-173">This uses the following syntax shown below.</span></span> <span data-ttu-id="c37b2-174">В этом случае действие Activity1 запускается одновременно для всех элементов в коллекции.</span><span class="sxs-lookup"><span data-stu-id="c37b2-174">In this case, Activity1 starts at the same time for all items in the collection.</span></span> <span data-ttu-id="c37b2-175">Для каждого элемента действие Activity2 запускается после завершения действия Activity1.</span><span class="sxs-lookup"><span data-stu-id="c37b2-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="c37b2-176">Действие Activity3 запускается только после завершения действий Activity1 и Activity2 для всех элементов.</span><span class="sxs-lookup"><span data-stu-id="c37b2-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="c37b2-177">Приведенный ниже пример аналогичен предыдущему: файлы копируются параллельно.</span><span class="sxs-lookup"><span data-stu-id="c37b2-177">The following example is similar to the previous example copying files in parallel.</span></span>  <span data-ttu-id="c37b2-178">В данном случае после копирования каждого файла отображается отдельное сообщение.</span><span class="sxs-lookup"><span data-stu-id="c37b2-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="c37b2-179">Как только все файлы будут скопированы, отображается итоговое сообщение о завершении.</span><span class="sxs-lookup"><span data-stu-id="c37b2-179">Only after they are all completely copied is the final completion message displayed.</span></span>

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
> <span data-ttu-id="c37b2-180">Не рекомендуется запускать дочерние модули Runbook параллельно, так как обычно этот приводит к недостоверным результатам.</span><span class="sxs-lookup"><span data-stu-id="c37b2-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span></span>  <span data-ttu-id="c37b2-181">Выходные данные дочернего модуля runbook могут не отображаться, а параметры одного дочернего модуля runbook могут влиять на параметры другого.</span><span class="sxs-lookup"><span data-stu-id="c37b2-181">The output from the child runbook sometimes does not show up, and settings in one child runbook can affect the other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="c37b2-182">контрольные точки</span><span class="sxs-lookup"><span data-stu-id="c37b2-182">Checkpoints</span></span>
<span data-ttu-id="c37b2-183">*Контрольная точка* представляет собой моментальный снимок текущего состояния рабочего процесса, который включает текущие значения переменных и любые выходные данные, созданные для этой точки.</span><span class="sxs-lookup"><span data-stu-id="c37b2-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span></span> <span data-ttu-id="c37b2-184">Если рабочий процесс завершается ошибкой или приостанавливается, при следующем запуске он будет выполняться не с начала, а с последней контрольной точки.</span><span class="sxs-lookup"><span data-stu-id="c37b2-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span></span>  <span data-ttu-id="c37b2-185">Можно установить контрольную точку для рабочего процесса при помощи действия **Checkpoint-Workflow** .</span><span class="sxs-lookup"><span data-stu-id="c37b2-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="c37b2-186">В приведенном ниже примере кода действие Activity2 вызывает остановку рабочего процесса, в связи с чем выдается исключение.</span><span class="sxs-lookup"><span data-stu-id="c37b2-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span></span> <span data-ttu-id="c37b2-187">После возобновления рабочий процесс начинается с действия Activity2, поскольку оно идет сразу за последней установленной контрольной точкой.</span><span class="sxs-lookup"><span data-stu-id="c37b2-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="c37b2-188">Контрольные точки в рабочем процессе необходимо устанавливать после действий, которые могут выдавать исключения и которые не должны повторяться при возобновлении рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="c37b2-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span></span> <span data-ttu-id="c37b2-189">Допустим, рабочий процесс создает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="c37b2-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="c37b2-190">Контрольную точку следует создавать как до, так и после команды создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c37b2-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span></span> <span data-ttu-id="c37b2-191">Если создать виртуальную машину не удастся, то при повторном запуске рабочего процесса команды повторятся.</span><span class="sxs-lookup"><span data-stu-id="c37b2-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span></span> <span data-ttu-id="c37b2-192">Если рабочий процесс завершится неудачей после создания виртуальной машины, то при возобновлении он не будет создавать ее заново.</span><span class="sxs-lookup"><span data-stu-id="c37b2-192">If the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span></span>

<span data-ttu-id="c37b2-193">Код в приведенном ниже примере копирует несколько файлов в определенный узел сети и устанавливает контрольную точку после каждого файла.</span><span class="sxs-lookup"><span data-stu-id="c37b2-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="c37b2-194">Если подключение к этому узлу утеряно, рабочий процесс завершатся ошибкой.</span><span class="sxs-lookup"><span data-stu-id="c37b2-194">If the network location is lost, then the workflow ends in error.</span></span>  <span data-ttu-id="c37b2-195">При повторном запуске он начнется с последней контрольной точки, а значит, уже скопированные файлы пропускаются.</span><span class="sxs-lookup"><span data-stu-id="c37b2-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied are skipped.</span></span>

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

<span data-ttu-id="c37b2-196">Учетные данные пользователя не сохраняются после вызова действия [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) или после вызова последней контрольной точки. Поэтому для учетных данных необходимо указать значение null, а затем извлечь их снова из хранилища ресурсов после вызова **Suspend-Workflow** или контрольной точки.</span><span class="sxs-lookup"><span data-stu-id="c37b2-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="c37b2-197">Иначе может появиться следующее сообщение об ошибке: *Невозможно возобновить задание рабочего процесса, поскольку не удалось полностью сохранить постоянные данные или сохраненные постоянные данные повреждены. Необходимо перезапустить рабочий процесс.*</span><span class="sxs-lookup"><span data-stu-id="c37b2-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span></span>

<span data-ttu-id="c37b2-198">Следующий код показывает, как это сделать в модулях Runbook рабочих процессов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c37b2-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first to create the VM (code not shown)

          # Now add the VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="c37b2-199">Это не обязательно делать, если вы проходите проверку подлинности с помощью учетной записи запуска от имени, настроенной с помощью субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="c37b2-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="c37b2-200">Дополнительные сведения о контрольных точках см. в статье [Добавление контрольных точек в рабочий процесс сценария](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="c37b2-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c37b2-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c37b2-201">Next steps</span></span>
* <span data-ttu-id="c37b2-202">Чтобы приступить к работе с модулями Runbook рабочих процессов PowerShell, обратитесь к статье [Мой первый модуль Runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="c37b2-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
