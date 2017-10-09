---
title: "aaaGet работы с Python и облачных служб Azure | Документы Microsoft"
description: "Общие сведения об использовании средства Python для Visual Studio toocreate Azure облачных служб, включая веб-ролей и рабочих ролей."
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="33994-103">Использование веб-ролей и рабочих ролей Python с помощью средств Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="33994-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="33994-104">В этой статье представлен обзор способов использования веб-ролей и рабочих ролей Python с помощью [инструментов Python для Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="33994-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="33994-105">Узнайте, как toocreate toouse Visual Studio и развертывать основные облачные службы, использующей Python.</span><span class="sxs-lookup"><span data-stu-id="33994-105">Learn how toouse Visual Studio toocreate and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33994-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="33994-106">Prerequisites</span></span>
* [<span data-ttu-id="33994-107">Visual Studio 2013, 2015 или 2017</span><span class="sxs-lookup"><span data-stu-id="33994-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="33994-108">[Инструменты Python для Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="33994-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="33994-109">[Инструменты пакета SDK для Azure для VS 2013][Azure SDK Tools for VS 2013] или</span><span class="sxs-lookup"><span data-stu-id="33994-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="33994-110">[Инструменты пакета SDK для Azure для VS 2015][Azure SDK Tools for VS 2015] или</span><span class="sxs-lookup"><span data-stu-id="33994-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="33994-111">[Инструменты пакета SDK для Azure для VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="33994-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="33994-112">[Python 2.7 (32-разрядная версия)][Python 2.7 32-bit] или [Python 3.5 (32-разрядная версия)][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="33994-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="33994-113">Что такое веб-роли и рабочие роли Python?</span><span class="sxs-lookup"><span data-stu-id="33994-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="33994-114">Azure предоставляет три вычислительные модели запуска приложений: [веб-приложения в службе приложений Azure][execution model-web sites], [виртуальные машины Azure][execution model-vms] и [облачные службы Azure][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="33994-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="33994-115">Все три модели поддерживают Python.</span><span class="sxs-lookup"><span data-stu-id="33994-115">All three models support Python.</span></span> <span data-ttu-id="33994-116">Облачные службы, которые включают в себя веб-роли и рабочие роли, предоставляют *платформу как службу (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="33994-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="33994-117">В облачной службе веб-роли предоставляет выделенный Internet Information Services (IIS) web server toohost внешнего интерфейса веб-приложений, во время рабочей роли могут выполнять асинхронные, длительные или постоянные задачи зависят от взаимодействия с пользователем или входные данные.</span><span class="sxs-lookup"><span data-stu-id="33994-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="33994-118">Дополнительные сведения см. в разделе [Информация об облачных службах].</span><span class="sxs-lookup"><span data-stu-id="33994-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="33994-119">*Ищете простой веб-сайт toobuild?*</span><span class="sxs-lookup"><span data-stu-id="33994-119">*Looking toobuild a simple website?*</span></span>
> <span data-ttu-id="33994-120">Если ваш сценарий включает в себя только клиентскую часть простого веб-сайта, рассмотрите возможность использования hello простую функцию веб-приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="33994-120">If your scenario involves just a simple website front end, consider using hello lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="33994-121">При расширении веб-сайта, что изменение требований, могут выполнять обновление tooa облачной службы.</span><span class="sxs-lookup"><span data-stu-id="33994-121">You can easily upgrade tooa Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="33994-122">В разделе hello <a href="/develop/python/">центре разработчиков Python</a> для статей, посвященных разработки функции hello веб-приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="33994-122">See hello <a href="/develop/python/">Python Developer Center</a> for articles that cover development of hello Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="33994-123">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="33994-123">Project creation</span></span>
<span data-ttu-id="33994-124">В Visual Studio можно выбрать **облачной службы Azure** в hello **новый проект** диалогового **Python**.</span><span class="sxs-lookup"><span data-stu-id="33994-124">In Visual Studio, you can select **Azure Cloud Service** in hello **New Project** dialog box, under **Python**.</span></span>

![Диалоговое окно "Новый проект"](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="33994-126">В мастере hello облачной службы Azure можно создать новый веб- и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="33994-126">In hello Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Диалоговое окно Облачной службы Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="33994-128">Hello рабочей роли шаблон содержит стандартный код tooconnect tooan учетной записи хранилища Azure или шины обслуживания Azure.</span><span class="sxs-lookup"><span data-stu-id="33994-128">hello worker role template comes with boilerplate code tooconnect tooan Azure storage account or Azure Service Bus.</span></span>

![Решение для Облачной службы](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="33994-130">Можно добавить веб- и рабочих ролей tooan существующей облачной службы в любое время.</span><span class="sxs-lookup"><span data-stu-id="33994-130">You can add web or worker roles tooan existing cloud service at any time.</span></span>  <span data-ttu-id="33994-131">Можно выбрать tooadd существующие проекты в решении или создавать новые.</span><span class="sxs-lookup"><span data-stu-id="33994-131">You can choose tooadd existing projects in your solution, or create new ones.</span></span>

![Команда добавления роли](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="33994-133">В облачной службе могут присутствовать роли, реализованные на различных языках программирования.</span><span class="sxs-lookup"><span data-stu-id="33994-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="33994-134">Например, это может быть веб-роль на Python, реализованная с помощью Django, с рабочими ролями на Python или C#.</span><span class="sxs-lookup"><span data-stu-id="33994-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="33994-135">С помощью очередей служебной шины или очередей хранилища можно легко обмениваться данными между ролями.</span><span class="sxs-lookup"><span data-stu-id="33994-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-hello-cloud-service"></a><span data-ttu-id="33994-136">Установка Python на hello облачной службы</span><span class="sxs-lookup"><span data-stu-id="33994-136">Install Python on hello cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="33994-137">сценарии установки Hello, которые устанавливаются вместе с Visual Studio (во время hello последнего обновления в этой статье) не работают.</span><span class="sxs-lookup"><span data-stu-id="33994-137">hello setup scripts that are installed with Visual Studio (at hello time this article was last updated) do not work.</span></span> <span data-ttu-id="33994-138">В этом разделе описывается обходное решение.</span><span class="sxs-lookup"><span data-stu-id="33994-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="33994-139">Основная проблема Hello сценариев установки hello — что не устанавливать python.</span><span class="sxs-lookup"><span data-stu-id="33994-139">hello main problem with hello setup scripts is that they do not install python.</span></span> <span data-ttu-id="33994-140">Во-первых, определите два [задачи запуска](cloud-services-startup-tasks.md) в hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) файла.</span><span class="sxs-lookup"><span data-stu-id="33994-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="33994-141">Первая задача Hello (**PrepPython.ps1**) загружает и устанавливает среды выполнения Python hello.</span><span class="sxs-lookup"><span data-stu-id="33994-141">hello first task (**PrepPython.ps1**) downloads and installs hello Python runtime.</span></span> <span data-ttu-id="33994-142">Вторая задача Hello (**PipInstaller.ps1**) выполняется tooinstall PIP-адрес может иметь зависимости.</span><span class="sxs-lookup"><span data-stu-id="33994-142">hello second task (**PipInstaller.ps1**) runs pip tooinstall any dependencies you may have.</span></span>

<span data-ttu-id="33994-143">Привет, следующие сценарии были написаны для различных версий Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="33994-143">hello following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="33994-144">Если требуется, чтобы toouse hello версии 2.x Python, набор hello **PYTHON2** переменной файл слишком**на** для hello два запуска задач и задач среды выполнения hello: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="33994-144">If you want toouse hello version 2.x of python, set hello **PYTHON2** variable file too**on** for hello two startup tasks and hello runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

<span data-ttu-id="33994-145">Hello **PYTHON2** и **PYPATH** переменных должны быть добавлены toohello Рабочая задача запуска.</span><span class="sxs-lookup"><span data-stu-id="33994-145">hello **PYTHON2** and **PYPATH** variables must be added toohello worker startup task.</span></span> <span data-ttu-id="33994-146">Hello **PYPATH** переменная используется только в том случае, если hello **PYTHON2** переменной задано слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="33994-146">hello **PYPATH** variable is only used if hello **PYTHON2** variable is set too**on**.</span></span>

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="33994-147">Пример файла ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="33994-147">Sample ServiceDefinition.csdef</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



<span data-ttu-id="33994-148">Создайте hello **PrepPython.ps1** и **PipInstaller.ps1** файлы в hello **. / bin** папке роли.</span><span class="sxs-lookup"><span data-stu-id="33994-148">Next, create hello **PrepPython.ps1** and **PipInstaller.ps1** files in hello **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="33994-149">Файл PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="33994-149">PrepPython.ps1</span></span>
<span data-ttu-id="33994-150">Скрипт в этом файле устанавливает Python.</span><span class="sxs-lookup"><span data-stu-id="33994-150">This script installs python.</span></span> <span data-ttu-id="33994-151">Если hello **PYTHON2** слишком задана переменная среды**на**, то устанавливается Python 2.7, в противном случае устанавливается Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="33994-151">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a><span data-ttu-id="33994-152">Файл PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="33994-152">PipInstaller.ps1</span></span>
<span data-ttu-id="33994-153">Этот скрипт вызывает копирование pip и устанавливает все зависимости hello в hello **requirements.txt** файла.</span><span class="sxs-lookup"><span data-stu-id="33994-153">This script calls up pip and installs all of hello dependencies in hello **requirements.txt** file.</span></span> <span data-ttu-id="33994-154">Если hello **PYTHON2** слишком задана переменная среды**на**, то используется Python 2.7, в противном случае используется Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="33994-154">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="33994-155">Изменение файла LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="33994-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="33994-156">В случае hello **рабочей роли** проекта, **LauncherWorker.ps1** файл является файлом запуска требуется tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="33994-156">In hello case of a **worker role** project, **LauncherWorker.ps1** file is required tooexecute hello startup file.</span></span> <span data-ttu-id="33994-157">В **веб-роли** проекта, hello загрузочный файл вместо этого определяется в свойствах проекта hello.</span><span class="sxs-lookup"><span data-stu-id="33994-157">In a **web role** project, hello startup file is instead defined in hello project properties.</span></span>
> 
> 

<span data-ttu-id="33994-158">Hello **bin\LaunchWorker.ps1** toodo много подготовки работать, но он не работает действительно был создан.</span><span class="sxs-lookup"><span data-stu-id="33994-158">hello **bin\LaunchWorker.ps1** was originally created toodo a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="33994-159">Замените содержимое hello в этом файле hello, выполнив сценарий.</span><span class="sxs-lookup"><span data-stu-id="33994-159">Replace hello contents in that file with hello following script.</span></span>

<span data-ttu-id="33994-160">Этот скрипт вызывает hello **worker.py** файл из проекта python.</span><span class="sxs-lookup"><span data-stu-id="33994-160">This script calls hello **worker.py** file from your python project.</span></span> <span data-ttu-id="33994-161">Если hello **PYTHON2** слишком задана переменная среды**на**, то используется Python 2.7, в противном случае используется Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="33994-161">If hello **PYTHON2** environment variable is set too**on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a><span data-ttu-id="33994-162">Файл ps.cmd</span><span class="sxs-lookup"><span data-stu-id="33994-162">ps.cmd</span></span>
<span data-ttu-id="33994-163">шаблоны Visual Studio Hello должен быть создан **ps.cmd** файла в hello **. / bin** папки.</span><span class="sxs-lookup"><span data-stu-id="33994-163">hello Visual Studio templates should have created a **ps.cmd** file in hello **./bin** folder.</span></span> <span data-ttu-id="33994-164">Этот сценарий вызывает выше сценарии оболочки hello PowerShell и обеспечивает ведение журналов на основе имени hello вызывается оболочки PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="33994-164">This shell script calls out hello PowerShell wrapper scripts above and provides logging based on hello name of hello PowerShell wrapper called.</span></span> <span data-ttu-id="33994-165">Если этот файл не создан, вот данные, которые должны в нем содержаться:</span><span class="sxs-lookup"><span data-stu-id="33994-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="33994-166">Локальный запуск</span><span class="sxs-lookup"><span data-stu-id="33994-166">Run locally</span></span>
<span data-ttu-id="33994-167">Если установить проекта облачной службы как запускаемый проект hello и нажмите клавишу F5, hello облачная служба выполняется в локальный эмулятор Azure hello.</span><span class="sxs-lookup"><span data-stu-id="33994-167">If you set your cloud service project as hello startup project and press F5, hello cloud service runs in hello local Azure emulator.</span></span>

<span data-ttu-id="33994-168">Несмотря на то, что PTVS поддерживает запуск в эмуляторе hello, отладка (например, точки останова) не работает.</span><span class="sxs-lookup"><span data-stu-id="33994-168">Although PTVS supports launching in hello emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="33994-169">toodebug рабочих и веб-роли, можно задать проект роли hello hello запускаемым проектом и отладки, чтобы вместо.</span><span class="sxs-lookup"><span data-stu-id="33994-169">toodebug your web and worker roles, you can set hello role project as hello startup project and debug that instead.</span></span>  <span data-ttu-id="33994-170">В качестве запускаемых при включении можно указать несколько проектов.</span><span class="sxs-lookup"><span data-stu-id="33994-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="33994-171">Щелкните правой кнопкой мыши решение hello, а затем выберите **назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="33994-171">Right-click hello solution and then select **Set StartUp Projects**.</span></span>

![Свойства запускаемого при включении проекта в решении](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a><span data-ttu-id="33994-173">Публикация tooAzure</span><span class="sxs-lookup"><span data-stu-id="33994-173">Publish tooAzure</span></span>
<span data-ttu-id="33994-174">toopublish, щелкните правой кнопкой мыши проект облачной службы hello в решении hello, а затем выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="33994-174">toopublish, right-click hello cloud service project in hello solution and then select **Publish**.</span></span>

![Вход для публикации в Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="33994-176">Выполните мастер hello.</span><span class="sxs-lookup"><span data-stu-id="33994-176">Follow hello wizard.</span></span> <span data-ttu-id="33994-177">При необходимости включите удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="33994-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="33994-178">Удаленный рабочий стол полезно в том случае, если нужно toodebug что-то.</span><span class="sxs-lookup"><span data-stu-id="33994-178">Remote desktop is helpful when you need toodebug something.</span></span>

<span data-ttu-id="33994-179">После завершения настройки параметров щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="33994-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="33994-180">Некоторые ход выполнения отображается в окне вывода hello, то появится окно hello журнал действий Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="33994-180">Some progress appears in hello output window, then you'll see hello Microsoft Azure Activity Log window.</span></span>

![Окно журнала действий Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="33994-182">Развертывание принимает toocomplete несколько минут, затем веб-и/или запуск рабочих ролей в Azure!</span><span class="sxs-lookup"><span data-stu-id="33994-182">Deployment takes several minutes toocomplete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="33994-183">Изучение журналов</span><span class="sxs-lookup"><span data-stu-id="33994-183">Investigate logs</span></span>
<span data-ttu-id="33994-184">После hello облачной службы виртуальная машина запускается и устанавливает Python, можно просмотреть журналы toofind hello наличие сообщений о сбое.</span><span class="sxs-lookup"><span data-stu-id="33994-184">After hello cloud service virtual machine starts up and installs Python, you can look at hello logs toofind any failure messages.</span></span> <span data-ttu-id="33994-185">Эти журналы расположены в hello **C:\Resources\Directory\\\LogFiles {роль}** папки.</span><span class="sxs-lookup"><span data-stu-id="33994-185">These logs are located in hello **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="33994-186">**PrepPython.err.txt** содержит по крайней мере одна ошибка, то из при hello скрипт пытается toodetect, если установлены Python и **PipInstaller.err.txt** может жалуются устаревшей версией PIP-адрес.</span><span class="sxs-lookup"><span data-stu-id="33994-186">**PrepPython.err.txt** has at least one error in it from when hello script tries toodetect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33994-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="33994-187">Next steps</span></span>
<span data-ttu-id="33994-188">Более подробные сведения о работе с веб- и рабочих ролей в средства Python для Visual Studio см. в документации PTVS hello:</span><span class="sxs-lookup"><span data-stu-id="33994-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see hello PTVS documentation:</span></span>

* <span data-ttu-id="33994-189">[Azure Cloud Service Projects for Python][Cloud Service Projects] (Проекты для облачной службы Azure для Python)</span><span class="sxs-lookup"><span data-stu-id="33994-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="33994-190">Дополнительные сведения об использовании служб Azure из рабочих и веб-роли, например с помощью хранилища Azure или Service Bus см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="33994-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see hello following articles:</span></span>

* <span data-ttu-id="33994-191">[Использование хранилища больших двоичных объектов Azure из Python][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="33994-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="33994-192">[Использование табличного хранилища из Python][Table Service]</span><span class="sxs-lookup"><span data-stu-id="33994-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="33994-193">[Использование хранилища очередей из Python][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="33994-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="33994-194">[Как использовать очереди служебной шины][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="33994-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="33994-195">[Как использовать разделы и подписки служебной шины][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="33994-195">[Service Bus Topics][Service Bus Topics]</span></span>

<!--Link references-->

[Информация об облачных службах]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
