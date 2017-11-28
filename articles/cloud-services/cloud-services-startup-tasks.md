---
title: "Выполнение задач запуска в облачных службах Azure | Документация Майкрософт"
description: "Задачи запуска помогают подготовить среду облачной службы для приложения. Вы узнаете, как работают задачи запуска и как их можно создать."
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
ms.openlocfilehash: 1c1b3aa86dc8211de0c07c9fb68da5685c86f551
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="1c2f5-104">Как настроить и выполнить задачи запуска для облачной службы</span><span class="sxs-lookup"><span data-stu-id="1c2f5-104">How to configure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="1c2f5-105">С помощью задач запуска вы можете выполнять различные операции перед запуском роли.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="1c2f5-106">Это может быть установка компонента, регистрация компонентов COM, установка разделов реестра или запуск длительного процесса.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="1c2f5-107">Задачи запуска неприменимы к виртуальным машинам, они подходят только для веб-ролей и рабочих ролей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-107">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="1c2f5-108">Как работают задачи запуска</span><span class="sxs-lookup"><span data-stu-id="1c2f5-108">How startup tasks work</span></span>
<span data-ttu-id="1c2f5-109">Задачи запуска — это действия, выполняемые до запуска роли и определяемые в файле [ServiceDefinition.csdef] с помощью элемента [Task] в элементе [Startup].</span><span class="sxs-lookup"><span data-stu-id="1c2f5-109">Startup tasks are actions that are taken before your roles begin and are defined in the [ServiceDefinition.csdef] file by using the [Task] element within the [Startup] element.</span></span> <span data-ttu-id="1c2f5-110">Часто задачи запуска — это пакетные файлы, но они также могут быть консольными приложениями или пакетными файлами, запускающими сценарии PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="1c2f5-111">Переменные среды передают информацию в задачу запуска, а локальное хранилище можно использовать для передачи информации из задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-111">Environment variables pass information into a startup task, and local storage can be used to pass information out of a startup task.</span></span> <span data-ttu-id="1c2f5-112">Например, в переменной среды можно указать путь к программе, которую вы хотите установить, и файлы могут быть записаны в локальное хранилище, чтобы позже их могла считать роль.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-112">For example, an environment variable can specify the path to a program you want to install, and files can be written to local storage that can then be read later by your roles.</span></span>

<span data-ttu-id="1c2f5-113">Задача запуска может записывать информацию и ошибки в журнал в каталоге, заданном переменной среды **TEMP** .</span><span class="sxs-lookup"><span data-stu-id="1c2f5-113">Your startup task can log information and errors to the directory specified by the **TEMP** environment variable.</span></span> <span data-ttu-id="1c2f5-114">Во время выполнения задачи запуска в облаке переменная среды **TEMP** сопоставляется с каталогом *C:\\Resources\\temp\\[guid].[имя_роли]\\RoleTemp*.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-114">During the startup task, the **TEMP** environment variable resolves to the *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on the cloud.</span></span>

<span data-ttu-id="1c2f5-115">Кроме того, задачи запуска могут выполняться несколько раз между перезагрузками.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="1c2f5-116">Например, задача запуска будет выполняться при каждом перезапуске роли, что не всегда подразумевает перезагрузку.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-116">For example, the startup task will be run each time the role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="1c2f5-117">Задачи запуска следует составлять таким способом, чтобы их можно было без проблем запускать несколько раз.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-117">Startup tasks should be written in a way that allows them to run several times without problems.</span></span>

<span data-ttu-id="1c2f5-118">Задачи запуска должны заканчиваться **errorlevel** (или кодом выхода), равным 0. Тогда процесс запуска будет завершен.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for the startup process to complete.</span></span> <span data-ttu-id="1c2f5-119">Если задача запуска завершается ненулевым **errorlevel**, роль не запускается.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-119">If a startup task ends with a non-zero **errorlevel**, the role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="1c2f5-120">Порядок запуска роли</span><span class="sxs-lookup"><span data-stu-id="1c2f5-120">Role startup order</span></span>
<span data-ttu-id="1c2f5-121">Ниже приведена процедура запуска роли в Azure.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-121">The following lists the role startup procedure in Azure:</span></span>

1. <span data-ttu-id="1c2f5-122">Экземпляр помечается как **Запуск** и не получает трафик.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-122">The instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="1c2f5-123">Все задачи запуска выполняются в соответствии с их атрибутом **taskType** .</span><span class="sxs-lookup"><span data-stu-id="1c2f5-123">All startup tasks are executed according to their **taskType** attribute.</span></span>
   
   * <span data-ttu-id="1c2f5-124">**Простые** задачи (simple) выполняются синхронно, по одной.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-124">The **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="1c2f5-125">**Фоновые** задачи (background) и задачи **переднего плана** (foreground) запускаются асинхронно, параллельно с задачей запуска.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-125">The **background** and **foreground** tasks are started asynchronously, parallel to the startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="1c2f5-126">Службы IIS могут не быть полностью настроены на этапе выполнения задач запуска в процессе запуска, поэтому данные, относящиеся к роли, могут быть недоступны.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-126">IIS may not be fully configured during the startup task stage in the startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="1c2f5-127">Для задач запуска, требующих данные, относящиеся к роли, следует использовать [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c2f5-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="1c2f5-128">Запускается процесс размещения роли и в IIS создается сайт.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-128">The role host process is started and the site is created in IIS.</span></span>
4. <span data-ttu-id="1c2f5-129">Вызывается метод [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1c2f5-129">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="1c2f5-130">Экземпляр помечается как **Готов** , и трафик перенаправляется в него.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-130">The instance is marked as **Ready** and traffic is routed to the instance.</span></span>
6. <span data-ttu-id="1c2f5-131">Вызывается метод [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1c2f5-131">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="1c2f5-132">Пример задачи запуска</span><span class="sxs-lookup"><span data-stu-id="1c2f5-132">Example of a startup task</span></span>
<span data-ttu-id="1c2f5-133">Задачи запуска определяются в файле [ServiceDefinition.csdef], в элементе **Task**.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-133">Startup tasks are defined in the [ServiceDefinition.csdef] file, in the **Task** element.</span></span> <span data-ttu-id="1c2f5-134">Атрибут **commandLine** задает имя и параметры пакетного файла запуска или команды консоли. Атрибут **executionContext** задает уровень привилегий задачи запуска, а атрибут **taskType** указывает, каким образом будет выполняться задача.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-134">The **commandLine** attribute specifies the name and parameters of the startup batch file or console command, the **executionContext** attribute specifies the privilege level of the startup task, and the **taskType** attribute specifies how the task will be executed.</span></span>

<span data-ttu-id="1c2f5-135">В этом примере для задачи запуска создается переменная среды **MyVersionNumber**, которой присваивается значение **1.0.0.0**.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-135">In this example, an environment variable, **MyVersionNumber**, is created for the startup task and set to the value "**1.0.0.0**".</span></span>

<span data-ttu-id="1c2f5-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="1c2f5-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="1c2f5-137">В следующем примере пакетный файл **Startup.cmd** записывает строку «The current version is 1.0.0.0» в файл StartupLog.txt в каталоге, указанном в переменной среды TEMP.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-137">In the following example, the **Startup.cmd** batch file writes the line "The current version is 1.0.0.0" to the StartupLog.txt file in the directory specified by the TEMP environment variable.</span></span> <span data-ttu-id="1c2f5-138">Строка `EXIT /B 0` гарантирует, что задача запуска завершается **errorlevel** , равным 0.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-138">The `EXIT /B 0` line ensures that the startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO The current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="1c2f5-139">В Visual Studio свойству **Копировать в выходной каталог** для пакетного файла запуска должно быть присвоено значение **Всегда копировать**, чтобы пакетный файл запуска был должным образом развернут в проекте Azure (**approot\\bin** для веб-ролей и **approot** для рабочих ролей).</span><span class="sxs-lookup"><span data-stu-id="1c2f5-139">In Visual Studio, the **Copy to Output Directory** property for your startup batch file should be set to **Copy Always** to be sure that your startup batch file is properly deployed to your project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="1c2f5-140">Описание атрибутов задачи</span><span class="sxs-lookup"><span data-stu-id="1c2f5-140">Description of task attributes</span></span>
<span data-ttu-id="1c2f5-141">Ниже описаны атрибуты элемента **Task** в файле [ServiceDefinition.csdef] .</span><span class="sxs-lookup"><span data-stu-id="1c2f5-141">The following describes the attributes of the **Task** element in the [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="1c2f5-142">**commandLine** — задает командную строку для задачи запуска:</span><span class="sxs-lookup"><span data-stu-id="1c2f5-142">**commandLine** - Specifies the command line for the startup task:</span></span>

* <span data-ttu-id="1c2f5-143">Команда с необязательными параметрами командной строки, с которой начинается задача запуска.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-143">The command, with optional command line parameters, which begins the startup task.</span></span>
* <span data-ttu-id="1c2f5-144">Часто это имя пакетного CMD- или BAT-файла.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-144">Frequently this is the filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="1c2f5-145">Задача задается относительно папки AppRoot\\bin развертывания.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-145">The task is relative to the AppRoot\\Bin folder for the deployment.</span></span> <span data-ttu-id="1c2f5-146">Переменные среды не разворачиваются при определении пути и файла задачи.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-146">Environment variables are not expanded in determining the path and file of the task.</span></span> <span data-ttu-id="1c2f5-147">Если требуется расширение среды, можно создать небольшой CMD-файл сценария, который вызывает задачу запуска.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="1c2f5-148">Может быть консольным приложением или пакетным файлом, который запускает [сценарий PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="1c2f5-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="1c2f5-149">**executionContext** — задает уровень привилегий для задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-149">**executionContext** - Specifies the privilege level for the startup task.</span></span> <span data-ttu-id="1c2f5-150">Уровень привилегий может быть ограничен или повышен:</span><span class="sxs-lookup"><span data-stu-id="1c2f5-150">The privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="1c2f5-151">**limited**</span><span class="sxs-lookup"><span data-stu-id="1c2f5-151">**limited**</span></span>  
  <span data-ttu-id="1c2f5-152">Задача запуска выполняется с теми же привилегиями, что и роль.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-152">The startup task runs with the same privileges as the role.</span></span> <span data-ttu-id="1c2f5-153">Если атрибут **executionContext** элемента [Runtime] также имеет значение **limited**, то используются привилегии пользователя.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-153">When the **executionContext** attribute for the [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="1c2f5-154">**elevated**</span><span class="sxs-lookup"><span data-stu-id="1c2f5-154">**elevated**</span></span>  
  <span data-ttu-id="1c2f5-155">Задача запуска выполняется с привилегиями администратора.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-155">The startup task runs with administrator privileges.</span></span> <span data-ttu-id="1c2f5-156">Это позволяет задачам запуска устанавливать программы, вносить изменения в конфигурацию IIS, вносить изменения в реестр и выполнять другие административные задачи без увеличения уровня привилегий самой роли.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-156">This allows startup tasks to install programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing the privilege level of the role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="1c2f5-157">Уровень привилегий задачи запуска не обязательно должен совпадать с уровнем привилегий роли.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-157">The privilege level of a startup task does not need to be the same as the role itself.</span></span>
> 
> 

<span data-ttu-id="1c2f5-158">**taskType** — указывает способ выполнения задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-158">**taskType** - Specifies the way a startup task is executed.</span></span>

* <span data-ttu-id="1c2f5-159">**Простые**</span><span class="sxs-lookup"><span data-stu-id="1c2f5-159">**simple**</span></span>  
  <span data-ttu-id="1c2f5-160">Задачи выполняются синхронно, поочередно и в порядке, указанном в файле [ServiceDefinition.csdef] .</span><span class="sxs-lookup"><span data-stu-id="1c2f5-160">Tasks are executed synchronously, one at a time, in the order specified in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="1c2f5-161">Если одна задача запуска **simple** завершается **errorlevel**, равным нулю, выполняется следующая задача запуска **simple**.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-161">When one **simple** startup task ends with an **errorlevel** of zero, the next **simple** startup task is executed.</span></span> <span data-ttu-id="1c2f5-162">Если больше нет задач запуска **simple** для выполнения, запускается сама роль.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-162">If there are no more **simple** startup tasks to execute, then the role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="1c2f5-163">Если задача **simple** завершается ненулевым **errorlevel**, экземпляр будет заблокирован.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-163">If the **simple** task ends with a non-zero **errorlevel**, the instance will be blocked.</span></span> <span data-ttu-id="1c2f5-164">Последующие задачи запуска **simple** не запустятся, как и сама роль.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-164">Subsequent **simple** startup tasks, and the role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="1c2f5-165">Чтобы убедиться, что пакетный файл завершается нулевым **errorlevel**, выполните команду `EXIT /B 0` в конце обработки пакетного файла.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-165">To ensure that your batch file ends with an **errorlevel** of zero, execute the command `EXIT /B 0` at the end of your batch file process.</span></span>
* <span data-ttu-id="1c2f5-166">**background**</span><span class="sxs-lookup"><span data-stu-id="1c2f5-166">**background**</span></span>  
  <span data-ttu-id="1c2f5-167">Задачи выполняются асинхронно, параллельно с запуском роли.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-167">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span>
* <span data-ttu-id="1c2f5-168">**переднего плана**</span><span class="sxs-lookup"><span data-stu-id="1c2f5-168">**foreground**</span></span>  
  <span data-ttu-id="1c2f5-169">Задачи выполняются асинхронно, параллельно с запуском роли.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-169">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span> <span data-ttu-id="1c2f5-170">Основное различие между задачами **foreground** и **background** состоит в том, что задача **foreground** не разрешает перезапуск или завершение работы роли до завершения задачи.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-170">The key difference between a **foreground** and a **background** task is that a **foreground** task prevents the role from recycling or shutting down until the task has ended.</span></span> <span data-ttu-id="1c2f5-171">Задачи **background** не имеют этого ограничения.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-171">The **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="1c2f5-172">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="1c2f5-172">Environment variables</span></span>
<span data-ttu-id="1c2f5-173">Переменные среды — это способ передачи информации в задачу запуска.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-173">Environment variables are a way to pass information to a startup task.</span></span> <span data-ttu-id="1c2f5-174">Например, можно передать путь к большому двоичному объекту, содержащему программу для установки, или номера портов, которые будет использовать роль, или параметры для управления функциями задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-174">For example, you can put the path to a blob that contains a program to install, or port numbers that your role will use, or settings to control features of your startup task.</span></span>

<span data-ttu-id="1c2f5-175">Существует два типа переменных среды для задачи запуска: статические переменные среды и переменные среды на основе членов класса [RoleEnvironment] .</span><span class="sxs-lookup"><span data-stu-id="1c2f5-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of the [RoleEnvironment] class.</span></span> <span data-ttu-id="1c2f5-176">Оба они находятся в разделе [Environment] файла [ServiceDefinition.csdef] и используют элемент [Variable] и атрибут **name**.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-176">Both are in the [Environment] section of the [ServiceDefinition.csdef] file, and both use the [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="1c2f5-177">Статические переменные среды используют атрибут **value** элемента [Variable] .</span><span class="sxs-lookup"><span data-stu-id="1c2f5-177">Static environment variables uses the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="1c2f5-178">В примере выше создается переменная среды **MyVersionNumber**, которая имеет статическое значение **1.0.0.0**.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-178">The example above creates the environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="1c2f5-179">Другим примером может служить создание переменной среды **StagingOrProduction**, которой можно вручную присвоить значение **staging** или **production**, чтобы выполнять различные действия запуска в зависимости от значения переменной среды **StagingOrProduction**.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-179">Another example would be to create a **StagingOrProduction** environment variable which you can manually set to values of "**staging**" or "**production**" to perform different startup actions based on the value of the **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="1c2f5-180">Переменные среды на основе членов класса RoleEnvironment не используют атрибут **value** элемента [Variable] .</span><span class="sxs-lookup"><span data-stu-id="1c2f5-180">Environment variables based on members of the RoleEnvironment class do not use the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="1c2f5-181">Вместо этого дочерний элемент [RoleInstanceValue] с соответствующим значением атрибута **XPath** используется для создания переменной среды для конкретного члена класса [RoleEnvironment].</span><span class="sxs-lookup"><span data-stu-id="1c2f5-181">Instead, the [RoleInstanceValue] child element, with the appropriate **XPath** attribute value, are used to create an environment variable based on a specific member of the [RoleEnvironment] class.</span></span> <span data-ttu-id="1c2f5-182">Значения атрибута **XPath** для доступа к различным значениям [RoleEnvironment] можно найти [здесь](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="1c2f5-182">Values for the **XPath** attribute to access various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="1c2f5-183">Например, чтобы создать переменную среды, имеющую значение **true** при выполнении в эмуляторе вычислений и **false** — при выполнении в облаке, используйте следующие элементы [Variable] и [RoleInstanceValue]:</span><span class="sxs-lookup"><span data-stu-id="1c2f5-183">For example, to create an environment variable that is "**true**" when the instance is running in the compute emulator, and "**false**" when running in the cloud, use the following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create the environment variable that informs the startup task whether it is running
                in the Compute Emulator or in the cloud. "%ComputeEmulatorRunning%"=="true" when
                running in the Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in the cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="1c2f5-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c2f5-184">Next steps</span></span>
<span data-ttu-id="1c2f5-185">Узнайте, как выполнять некоторые [стандартные задачи запуска](cloud-services-startup-tasks-common.md) с помощью облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-185">Learn how to perform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="1c2f5-186">[Упакуйте](cloud-services-model-and-package.md) облачную службу.</span><span class="sxs-lookup"><span data-stu-id="1c2f5-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

<span data-ttu-id="1c2f5-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="1c2f5-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="1c2f5-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="1c2f5-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
<span data-ttu-id="1c2f5-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span><span class="sxs-lookup"><span data-stu-id="1c2f5-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span></span>
<span data-ttu-id="1c2f5-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span><span class="sxs-lookup"><span data-stu-id="1c2f5-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span></span>
<span data-ttu-id="1c2f5-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="1c2f5-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="1c2f5-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="1c2f5-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="1c2f5-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="1c2f5-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
<span data-ttu-id="1c2f5-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span><span class="sxs-lookup"><span data-stu-id="1c2f5-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span></span>
