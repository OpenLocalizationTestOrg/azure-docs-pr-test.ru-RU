---
title: "aaaRun задачи запуска в облачных службах Azure | Документы Microsoft"
description: "Задачи запуска помогают подготовить среду облачной службы для приложения. Это объясняется, как рабочих задач запуска и как toomake их"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="110b3-104">Выполнение задач запуска tooconfigure и выполнения для облачной службы</span><span class="sxs-lookup"><span data-stu-id="110b3-104">How tooconfigure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="110b3-105">Можно использовать операции tooperform запуска задачи до запуска роли.</span><span class="sxs-lookup"><span data-stu-id="110b3-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="110b3-106">Операции, вы можете tooperform включают установки компонента, регистрация компонентов COM, установка разделов реестра или запуск длительного процесса.</span><span class="sxs-lookup"><span data-stu-id="110b3-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="110b3-107">При запуске задачи не машины tooVirtual применимо, только tooCloud Service Web и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="110b3-107">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="110b3-108">Как работают задачи запуска</span><span class="sxs-lookup"><span data-stu-id="110b3-108">How startup tasks work</span></span>
<span data-ttu-id="110b3-109">Задачи запуска — действия, выполняемые до роли begin и определены в hello [ServiceDefinition.csdef] файла с помощью hello [задачи] элемент в пределах hello [запуска]элемент.</span><span class="sxs-lookup"><span data-stu-id="110b3-109">Startup tasks are actions that are taken before your roles begin and are defined in hello [ServiceDefinition.csdef] file by using hello [Task] element within hello [Startup] element.</span></span> <span data-ttu-id="110b3-110">Часто задачи запуска — это пакетные файлы, но они также могут быть консольными приложениями или пакетными файлами, запускающими сценарии PowerShell.</span><span class="sxs-lookup"><span data-stu-id="110b3-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="110b3-111">Переменные среды передают сведения в задачу запуска, и локальное хранилище можно использовать toopass сведения из задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="110b3-111">Environment variables pass information into a startup task, and local storage can be used toopass information out of a startup task.</span></span> <span data-ttu-id="110b3-112">Например, переменная среды можно указать hello путь tooa программы требуется tooinstall, а файлы могут быть записаны toolocal хранилище, могут считываться позже вашей роли.</span><span class="sxs-lookup"><span data-stu-id="110b3-112">For example, an environment variable can specify hello path tooa program you want tooinstall, and files can be written toolocal storage that can then be read later by your roles.</span></span>

<span data-ttu-id="110b3-113">Задача запуска может записывать сведения и ошибки toohello каталог, заданный параметром hello **TEMP** переменной среды.</span><span class="sxs-lookup"><span data-stu-id="110b3-113">Your startup task can log information and errors toohello directory specified by hello **TEMP** environment variable.</span></span> <span data-ttu-id="110b3-114">Во время выполнения задачи запуска hello, hello **TEMP** переменной среды устраняет toohello *C:\\ресурсов\\temp\\[guid]. [ roleName]\\RoleTemp* каталог при выполнении в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-114">During hello startup task, hello **TEMP** environment variable resolves toohello *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on hello cloud.</span></span>

<span data-ttu-id="110b3-115">Кроме того, задачи запуска могут выполняться несколько раз между перезагрузками.</span><span class="sxs-lookup"><span data-stu-id="110b3-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="110b3-116">Например hello задача запуска будет выполняться при каждом перезапуске роли hello и они могут не всегда связано с перезагрузкой.</span><span class="sxs-lookup"><span data-stu-id="110b3-116">For example, hello startup task will be run each time hello role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="110b3-117">Задачи запуска должен быть написан таким образом, их toorun несколько раз без проблем.</span><span class="sxs-lookup"><span data-stu-id="110b3-117">Startup tasks should be written in a way that allows them toorun several times without problems.</span></span>

<span data-ttu-id="110b3-118">Задачи запуска должны заканчиваться **errorlevel** (или кодом выхода) ноль toocomplete процесс запуска hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for hello startup process toocomplete.</span></span> <span data-ttu-id="110b3-119">Если задача запуска оканчивается ненулевым **errorlevel**, hello роль не запускается.</span><span class="sxs-lookup"><span data-stu-id="110b3-119">If a startup task ends with a non-zero **errorlevel**, hello role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="110b3-120">Порядок запуска роли</span><span class="sxs-lookup"><span data-stu-id="110b3-120">Role startup order</span></span>
<span data-ttu-id="110b3-121">Hello ниже приведена процедура запуска роли hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="110b3-121">hello following lists hello role startup procedure in Azure:</span></span>

1. <span data-ttu-id="110b3-122">Hello экземпляр помечен как **запуск** и не принимает трафика.</span><span class="sxs-lookup"><span data-stu-id="110b3-122">hello instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="110b3-123">Все задачи запуска выполняются в соответствии с tootheir **taskType** атрибута.</span><span class="sxs-lookup"><span data-stu-id="110b3-123">All startup tasks are executed according tootheir **taskType** attribute.</span></span>
   
   * <span data-ttu-id="110b3-124">Hello **простой** задачи выполняются синхронно, по одному.</span><span class="sxs-lookup"><span data-stu-id="110b3-124">hello **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="110b3-125">Hello **фона** и **переднего плана** задачи — задача запуска работает асинхронно, параллельные toohello.</span><span class="sxs-lookup"><span data-stu-id="110b3-125">hello **background** and **foreground** tasks are started asynchronously, parallel toohello startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="110b3-126">Службы IIS могут не полностью настроен во время этапа запуска задач hello в процессе запуска hello, поэтому данные, зависящие от роли могут быть недоступны.</span><span class="sxs-lookup"><span data-stu-id="110b3-126">IIS may not be fully configured during hello startup task stage in hello startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="110b3-127">Для задач запуска, требующих данные, относящиеся к роли, следует использовать [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="110b3-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="110b3-128">запускается процесс размещения роли Hello и в службах IIS создается узел hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-128">hello role host process is started and hello site is created in IIS.</span></span>
4. <span data-ttu-id="110b3-129">Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="110b3-129">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="110b3-130">Hello экземпляр помечен как **готовности** и трафика перенаправленное toohello экземпляра.</span><span class="sxs-lookup"><span data-stu-id="110b3-130">hello instance is marked as **Ready** and traffic is routed toohello instance.</span></span>
6. <span data-ttu-id="110b3-131">Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="110b3-131">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="110b3-132">Пример задачи запуска</span><span class="sxs-lookup"><span data-stu-id="110b3-132">Example of a startup task</span></span>
<span data-ttu-id="110b3-133">Задачи запуска определяются в hello [ServiceDefinition.csdef] файла в hello **задачи** элемента.</span><span class="sxs-lookup"><span data-stu-id="110b3-133">Startup tasks are defined in hello [ServiceDefinition.csdef] file, in hello **Task** element.</span></span> <span data-ttu-id="110b3-134">Hello **commandLine** атрибут указывает имя hello и параметры hello пакетный файл или с помощью консоли команду, hello **executionContext** атрибут задает hello права доступа для запуска hello Задача и hello **taskType** атрибут указывает, каким образом будет выполняться задача hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-134">hello **commandLine** attribute specifies hello name and parameters of hello startup batch file or console command, hello **executionContext** attribute specifies hello privilege level of hello startup task, and hello **taskType** attribute specifies how hello task will be executed.</span></span>

<span data-ttu-id="110b3-135">В этом примере переменной среды **MyVersionNumber**, создается для задачи запуска hello и задать значение toohello "**1.0.0.0**».</span><span class="sxs-lookup"><span data-stu-id="110b3-135">In this example, an environment variable, **MyVersionNumber**, is created for hello startup task and set toohello value "**1.0.0.0**".</span></span>

<span data-ttu-id="110b3-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="110b3-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="110b3-137">В следующем примере hello, hello **Startup.cmd** пакетный файл записывает строку hello «hello текущая версия — 1.0.0.0» файл StartupLog.txt toohello в каталоге hello, указанном в переменной среды TEMP hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-137">In hello following example, hello **Startup.cmd** batch file writes hello line "hello current version is 1.0.0.0" toohello StartupLog.txt file in hello directory specified by hello TEMP environment variable.</span></span> <span data-ttu-id="110b3-138">Hello `EXIT /B 0` строки гарантирует, что hello задача запуска оканчивается **errorlevel** равно нулю.</span><span class="sxs-lookup"><span data-stu-id="110b3-138">hello `EXIT /B 0` line ensures that hello startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="110b3-139">В Visual Studio hello **скопируйте каталог tooOutput** свойства для пакетного файла запуска должно быть установлено слишком**всегда Копировать** toobe, убедитесь, что пакетный файл запуска должным образом развернут tooyour проекта в Azure (**approot\\bin** для веб-ролей и **approot** для рабочих ролей).</span><span class="sxs-lookup"><span data-stu-id="110b3-139">In Visual Studio, hello **Copy tooOutput Directory** property for your startup batch file should be set too**Copy Always** toobe sure that your startup batch file is properly deployed tooyour project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="110b3-140">Описание атрибутов задачи</span><span class="sxs-lookup"><span data-stu-id="110b3-140">Description of task attributes</span></span>
<span data-ttu-id="110b3-141">Hello ниже описываются атрибуты hello hello **задачи** элемент в hello [ServiceDefinition.csdef] файла:</span><span class="sxs-lookup"><span data-stu-id="110b3-141">hello following describes hello attributes of hello **Task** element in hello [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="110b3-142">**Командная строка** -указывает hello командной строки для запуска задачи hello:</span><span class="sxs-lookup"><span data-stu-id="110b3-142">**commandLine** - Specifies hello command line for hello startup task:</span></span>

* <span data-ttu-id="110b3-143">Hello команда с необязательными параметрами командной строки, которая начинает задачу запуска hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-143">hello command, with optional command line parameters, which begins hello startup task.</span></span>
* <span data-ttu-id="110b3-144">Часто это имя файла hello .cmd или .bat пакетный файл.</span><span class="sxs-lookup"><span data-stu-id="110b3-144">Frequently this is hello filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="110b3-145">Задача Hello — относительный toohello AppRoot\\папка Bin для развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-145">hello task is relative toohello AppRoot\\Bin folder for hello deployment.</span></span> <span data-ttu-id="110b3-146">Переменные среды не будут развернуты при определении пути hello и задачи «hello».</span><span class="sxs-lookup"><span data-stu-id="110b3-146">Environment variables are not expanded in determining hello path and file of hello task.</span></span> <span data-ttu-id="110b3-147">Если требуется расширение среды, можно создать небольшой CMD-файл сценария, который вызывает задачу запуска.</span><span class="sxs-lookup"><span data-stu-id="110b3-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="110b3-148">Может быть консольным приложением или пакетным файлом, который запускает [сценарий PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="110b3-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="110b3-149">**executionContext** -указывает hello уровень прав доступа для запуска задачи hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-149">**executionContext** - Specifies hello privilege level for hello startup task.</span></span> <span data-ttu-id="110b3-150">уровень прав доступа Hello можно ограничены или с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="110b3-150">hello privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="110b3-151">**limited**</span><span class="sxs-lookup"><span data-stu-id="110b3-151">**limited**</span></span>  
  <span data-ttu-id="110b3-152">Hello задача запуска выполняется с одинаковыми правами как роль hello hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-152">hello startup task runs with hello same privileges as hello role.</span></span> <span data-ttu-id="110b3-153">Здравствуйте, когда **executionContext** атрибут для hello [среды выполнения] элемент является также **ограниченный**, то используются права доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="110b3-153">When hello **executionContext** attribute for hello [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="110b3-154">**elevated**</span><span class="sxs-lookup"><span data-stu-id="110b3-154">**elevated**</span></span>  
  <span data-ttu-id="110b3-155">Hello задача запуска выполняется с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="110b3-155">hello startup task runs with administrator privileges.</span></span> <span data-ttu-id="110b3-156">Это позволяет задачи запуска программы tooinstall, внести изменения в конфигурацию IIS, выполнять изменения в реестр, а также другие административные задачи без увеличения hello права доступа для самой роли hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-156">This allows startup tasks tooinstall programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing hello privilege level of hello role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="110b3-157">Hello уровень прав доступа задачи запуска не требуется toobe Здравствуйте таким же, как сама роль hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-157">hello privilege level of a startup task does not need toobe hello same as hello role itself.</span></span>
> 
> 

<span data-ttu-id="110b3-158">**Тип задачи** -указывает, выполняется hello, каким образом задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="110b3-158">**taskType** - Specifies hello way a startup task is executed.</span></span>

* <span data-ttu-id="110b3-159">**Простые**</span><span class="sxs-lookup"><span data-stu-id="110b3-159">**simple**</span></span>  
  <span data-ttu-id="110b3-160">Задачи выполняются синхронно, одновременно в порядке hello, указываемой hello [ServiceDefinition.csdef] файла.</span><span class="sxs-lookup"><span data-stu-id="110b3-160">Tasks are executed synchronously, one at a time, in hello order specified in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="110b3-161">Если в одном **простой** задача запуска оканчивается **errorlevel** равна нулю, hello рядом **простой** выполнения задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="110b3-161">When one **simple** startup task ends with an **errorlevel** of zero, hello next **simple** startup task is executed.</span></span> <span data-ttu-id="110b3-162">Если больше нет **простой** задач запуска tooexecute, а затем запускается сама роль hello.</span><span class="sxs-lookup"><span data-stu-id="110b3-162">If there are no more **simple** startup tasks tooexecute, then hello role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="110b3-163">Если hello **простой** задача оканчивается с ненулевым **errorlevel**, hello экземпляр блокируется.</span><span class="sxs-lookup"><span data-stu-id="110b3-163">If hello **simple** task ends with a non-zero **errorlevel**, hello instance will be blocked.</span></span> <span data-ttu-id="110b3-164">Последующие **простой** задачи запуска и сама роль hello не запустится.</span><span class="sxs-lookup"><span data-stu-id="110b3-164">Subsequent **simple** startup tasks, and hello role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="110b3-165">tooensure, которая заканчивается пакетный файл **errorlevel** равна нулю, выполните команду hello `EXIT /B 0` конце hello процесса пакетного файла.</span><span class="sxs-lookup"><span data-stu-id="110b3-165">tooensure that your batch file ends with an **errorlevel** of zero, execute hello command `EXIT /B 0` at hello end of your batch file process.</span></span>
* <span data-ttu-id="110b3-166">**background**</span><span class="sxs-lookup"><span data-stu-id="110b3-166">**background**</span></span>  
  <span data-ttu-id="110b3-167">Задачи выполняются асинхронно, параллельно с запуска hello hello роли.</span><span class="sxs-lookup"><span data-stu-id="110b3-167">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span>
* <span data-ttu-id="110b3-168">**переднего плана**</span><span class="sxs-lookup"><span data-stu-id="110b3-168">**foreground**</span></span>  
  <span data-ttu-id="110b3-169">Задачи выполняются асинхронно, параллельно с запуска hello hello роли.</span><span class="sxs-lookup"><span data-stu-id="110b3-169">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span> <span data-ttu-id="110b3-170">Здравствуйте, основное отличие между **переднего плана** и **фона** том, что **переднего плана** задача позволяет роли hello из перезапуск или завершение работы, пока не получит задачу hello завершено.</span><span class="sxs-lookup"><span data-stu-id="110b3-170">hello key difference between a **foreground** and a **background** task is that a **foreground** task prevents hello role from recycling or shutting down until hello task has ended.</span></span> <span data-ttu-id="110b3-171">Hello **фона** задачи не имеют этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="110b3-171">hello **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="110b3-172">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="110b3-172">Environment variables</span></span>
<span data-ttu-id="110b3-173">Переменные среды — задача запуска tooa способом toopass сведения.</span><span class="sxs-lookup"><span data-stu-id="110b3-173">Environment variables are a way toopass information tooa startup task.</span></span> <span data-ttu-id="110b3-174">Например можно поместить hello путь tooa blob, содержащий tooinstall программы или номера портов, которые будет использовать роль или параметров функций toocontrol задачей запуска.</span><span class="sxs-lookup"><span data-stu-id="110b3-174">For example, you can put hello path tooa blob that contains a program tooinstall, or port numbers that your role will use, or settings toocontrol features of your startup task.</span></span>

<span data-ttu-id="110b3-175">Существует два типа переменных среды для задачи запуска; статические переменные среды и переменные среды на основе членов hello [ RoleEnvironment] класса.</span><span class="sxs-lookup"><span data-stu-id="110b3-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="110b3-176">Обе они находятся в hello [среды] раздел hello [ServiceDefinition.csdef] файл и оба hello используйте [переменных] элемент и **имя** атрибут.</span><span class="sxs-lookup"><span data-stu-id="110b3-176">Both are in hello [Environment] section of hello [ServiceDefinition.csdef] file, and both use hello [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="110b3-177">Hello использует переменные среды статических **значение** атрибут hello [переменных] элемента.</span><span class="sxs-lookup"><span data-stu-id="110b3-177">Static environment variables uses hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="110b3-178">Приведенный выше пример Hello создает переменную среды hello **MyVersionNumber** содержит статическое значение «**1.0.0.0**».</span><span class="sxs-lookup"><span data-stu-id="110b3-178">hello example above creates hello environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="110b3-179">Другим примером может служить toocreate **StagingOrProduction** переменной среды, которую можно установить вручную, toovalues из «**промежуточных**«или»**рабочей**» tooperform различных действий запуска на основе hello значения hello **StagingOrProduction** переменной среды.</span><span class="sxs-lookup"><span data-stu-id="110b3-179">Another example would be toocreate a **StagingOrProduction** environment variable which you can manually set toovalues of "**staging**" or "**production**" tooperform different startup actions based on hello value of hello **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="110b3-180">Не используйте переменные среды на основе членов класса RoleEnvironment hello hello **значение** атрибут hello [переменных] элемента.</span><span class="sxs-lookup"><span data-stu-id="110b3-180">Environment variables based on members of hello RoleEnvironment class do not use hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="110b3-181">Вместо этого hello [RoleInstanceValue] дочерний элемент с hello соответствующие **XPath** значение атрибута, будут использоваться toocreate переменной среды, в зависимости от конкретного члена hello [ RoleEnvironment] класса.</span><span class="sxs-lookup"><span data-stu-id="110b3-181">Instead, hello [RoleInstanceValue] child element, with hello appropriate **XPath** attribute value, are used toocreate an environment variable based on a specific member of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="110b3-182">Значения для hello **XPath** атрибута tooaccess различных [ RoleEnvironment] значения можно найти [здесь](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="110b3-182">Values for hello **XPath** attribute tooaccess various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="110b3-183">К примеру, toocreate переменной среды, "**true**» при запуске hello в эмуляторе вычислений hello, и"**false**» при работе в облаке hello используйте следующие hello [переменных] и [RoleInstanceValue] элементов:</span><span class="sxs-lookup"><span data-stu-id="110b3-183">For example, toocreate an environment variable that is "**true**" when hello instance is running in hello compute emulator, and "**false**" when running in hello cloud, use hello following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="110b3-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="110b3-184">Next steps</span></span>
<span data-ttu-id="110b3-185">Узнайте, как tooperform некоторые [общие задачи запуска](cloud-services-startup-tasks-common.md) с облачной службой.</span><span class="sxs-lookup"><span data-stu-id="110b3-185">Learn how tooperform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="110b3-186">[Упакуйте](cloud-services-model-and-package.md) облачную службу.</span><span class="sxs-lookup"><span data-stu-id="110b3-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[задачи]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[запуска]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[среды выполнения]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[среды]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[переменных]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
