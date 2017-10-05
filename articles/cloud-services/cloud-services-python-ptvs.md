---
title: "Начало работы с облачными службами Azure и Python | Документация Майкрософт"
description: "Обзор использования Python Tools в Visual Studio для создания облачных служб Azure, включая веб-роли и рабочие роли."
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
ms.openlocfilehash: 7d2bc89943087323e92cf06981bbacaf4b8ff060
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a><span data-ttu-id="bc3d2-103">Использование веб-ролей и рабочих ролей Python с помощью средств Python для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc3d2-103">Python web and worker roles with Python Tools for Visual Studio</span></span>

<span data-ttu-id="bc3d2-104">В этой статье представлен обзор способов использования веб-ролей и рабочих ролей Python с помощью [инструментов Python для Visual Studio][Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="bc3d2-104">This article provides an overview of using Python web and worker roles using [Python Tools for Visual Studio][Python Tools for Visual Studio].</span></span> <span data-ttu-id="bc3d2-105">Узнайте, как с помощью Visual Studio создать и развернуть базовую облачную службу, которая использует Python.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-105">Learn how to use Visual Studio to create and deploy a basic Cloud Service that uses Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc3d2-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bc3d2-106">Prerequisites</span></span>
* [<span data-ttu-id="bc3d2-107">Visual Studio 2013, 2015 или 2017</span><span class="sxs-lookup"><span data-stu-id="bc3d2-107">Visual Studio 2013, 2015, or 2017</span></span>](https://www.visualstudio.com/)
* <span data-ttu-id="bc3d2-108">[Инструменты Python для Visual Studio][Python Tools for Visual Studio] (PTVS)</span><span class="sxs-lookup"><span data-stu-id="bc3d2-108">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)</span></span>
* <span data-ttu-id="bc3d2-109">[Инструменты пакета SDK для Azure для VS 2013][Azure SDK Tools for VS 2013] или</span><span class="sxs-lookup"><span data-stu-id="bc3d2-109">[Azure SDK Tools for VS 2013][Azure SDK Tools for VS 2013] or</span></span>  
<span data-ttu-id="bc3d2-110">[Инструменты пакета SDK для Azure для VS 2015][Azure SDK Tools for VS 2015] или</span><span class="sxs-lookup"><span data-stu-id="bc3d2-110">[Azure SDK Tools for VS 2015][Azure SDK Tools for VS 2015] or</span></span>  
<span data-ttu-id="bc3d2-111">[Инструменты пакета SDK для Azure для VS 2017][Azure SDK Tools for VS 2017]</span><span class="sxs-lookup"><span data-stu-id="bc3d2-111">[Azure SDK Tools for VS 2017][Azure SDK Tools for VS 2017]</span></span>
* <span data-ttu-id="bc3d2-112">[Python 2.7 (32-разрядная версия)][Python 2.7 32-bit] или [Python 3.5 (32-разрядная версия)][Python 3.5 32-bit]</span><span class="sxs-lookup"><span data-stu-id="bc3d2-112">[Python 2.7 32-bit][Python 2.7 32-bit] or [Python 3.5 32-bit][Python 3.5 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a><span data-ttu-id="bc3d2-113">Что такое веб-роли и рабочие роли Python?</span><span class="sxs-lookup"><span data-stu-id="bc3d2-113">What are Python web and worker roles?</span></span>
<span data-ttu-id="bc3d2-114">Azure предоставляет три вычислительные модели запуска приложений: [веб-приложения в службе приложений Azure][execution model-web sites], [виртуальные машины Azure][execution model-vms] и [облачные службы Azure][execution model-cloud services].</span><span class="sxs-lookup"><span data-stu-id="bc3d2-114">Azure provides three compute models for running applications: [Web Apps feature in Azure App Service][execution model-web sites], [Azure Virtual Machines][execution model-vms], and [Azure Cloud Services][execution model-cloud services].</span></span> <span data-ttu-id="bc3d2-115">Все три модели поддерживают Python.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-115">All three models support Python.</span></span> <span data-ttu-id="bc3d2-116">Облачные службы, которые включают в себя веб-роли и рабочие роли, предоставляют *платформу как службу (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-116">Cloud Services, which include web and worker roles, provide *Platform as a Service (PaaS)*.</span></span> <span data-ttu-id="bc3d2-117">В рамках облачной службы веб-роль предоставляет выделенный веб-сервер IIS для размещения внешних веб-приложений, тогда как рабочая роль может выполнять асинхронные, долгосрочные или постоянные задачи, не зависящие от пользовательских действий и пользовательского ввода.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-117">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front end web applications, while a worker role can run asynchronous, long-running, or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="bc3d2-118">Дополнительные сведения см. в разделе [Информация об облачных службах].</span><span class="sxs-lookup"><span data-stu-id="bc3d2-118">For more information, see [What is a Cloud Service?].</span></span>

> [!NOTE]
> <span data-ttu-id="bc3d2-119">*Требуется создать простой веб-сайт?*</span><span class="sxs-lookup"><span data-stu-id="bc3d2-119">*Looking to build a simple website?*</span></span>
> <span data-ttu-id="bc3d2-120">Если вам необходимо создать сайт с простым внешним интерфейсом, воспользуйтесь упрощенными веб-приложениями в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-120">If your scenario involves just a simple website front end, consider using the lightweight Web Apps feature in Azure App Service.</span></span> <span data-ttu-id="bc3d2-121">По мере роста веб-сайта и изменения требований можно легко выполнить обновление к облачной службе.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-121">You can easily upgrade to a Cloud Service as your website grows and your requirements change.</span></span> <span data-ttu-id="bc3d2-122">В <a href="/develop/python/">Центре разработчиков Python</a> можно найти статьи, посвященные разработке веб-приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-122">See the <a href="/develop/python/">Python Developer Center</a> for articles that cover development of the Web Apps feature in Azure App Service.</span></span>
> <br />
> 
> 

## <a name="project-creation"></a><span data-ttu-id="bc3d2-123">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="bc3d2-123">Project creation</span></span>
<span data-ttu-id="bc3d2-124">В Visual Studio в диалоговом окне **Новый проект** в разделе **Python** выберите **Облачная служба Azure**.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-124">In Visual Studio, you can select **Azure Cloud Service** in the **New Project** dialog box, under **Python**.</span></span>

![Диалоговое окно "Новый проект"](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

<span data-ttu-id="bc3d2-126">В мастере настройки облачной службы Azure можно создать новую веб-роль и рабочие роли.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-126">In the Azure Cloud Service wizard, you can create new web and worker roles.</span></span>

![Диалоговое окно Облачной службы Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

<span data-ttu-id="bc3d2-128">Шаблон рабочей роли входит в состав стандартного кода для подключения к учетной записи хранения Azure или к служебной шине Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-128">The worker role template comes with boilerplate code to connect to an Azure storage account or Azure Service Bus.</span></span>

![Решение для Облачной службы](./media/cloud-services-python-ptvs/worker.png)

<span data-ttu-id="bc3d2-130">Добавить веб-роль или рабочую роль к уже существующей облачной службе можно в любое время.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-130">You can add web or worker roles to an existing cloud service at any time.</span></span>  <span data-ttu-id="bc3d2-131">Также можно добавить к собственному решению существующий проект или создать новые проекты.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-131">You can choose to add existing projects in your solution, or create new ones.</span></span>

![Команда добавления роли](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

<span data-ttu-id="bc3d2-133">В облачной службе могут присутствовать роли, реализованные на различных языках программирования.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-133">Your cloud service can contain roles implemented in different languages.</span></span>  <span data-ttu-id="bc3d2-134">Например, это может быть веб-роль на Python, реализованная с помощью Django, с рабочими ролями на Python или C#.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-134">For example, you can have a Python web role implemented using Django, with Python, or with C# worker roles.</span></span>  <span data-ttu-id="bc3d2-135">С помощью очередей служебной шины или очередей хранилища можно легко обмениваться данными между ролями.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-135">You can easily communicate between your roles using Service Bus queues or storage queues.</span></span>

## <a name="install-python-on-the-cloud-service"></a><span data-ttu-id="bc3d2-136">Установка Python в облачной службе</span><span class="sxs-lookup"><span data-stu-id="bc3d2-136">Install Python on the cloud service</span></span>
> [!WARNING]
> <span data-ttu-id="bc3d2-137">Скрипты установки, которые устанавливаются вместе с Visual Studio (на момент последнего обновления этой статьи), не работают.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-137">The setup scripts that are installed with Visual Studio (at the time this article was last updated) do not work.</span></span> <span data-ttu-id="bc3d2-138">В этом разделе описывается обходное решение.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-138">This section describes a workaround.</span></span>
> 
> 

<span data-ttu-id="bc3d2-139">Основная проблема скриптов установки заключается в том, что они не устанавливают Python.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-139">The main problem with the setup scripts is that they do not install python.</span></span> <span data-ttu-id="bc3d2-140">Сначала определите две [задачи запуска](cloud-services-startup-tasks.md) в файле [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef).</span><span class="sxs-lookup"><span data-stu-id="bc3d2-140">First, define two [startup tasks](cloud-services-startup-tasks.md) in the [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span> <span data-ttu-id="bc3d2-141">Первая задача (**PrepPython.ps1**) скачивает и устанавливает среду выполнения Python.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-141">The first task (**PrepPython.ps1**) downloads and installs the Python runtime.</span></span> <span data-ttu-id="bc3d2-142">Вторая задача (**PipInstaller.ps1**) запускает PIP, чтобы установить зависимости.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-142">The second task (**PipInstaller.ps1**) runs pip to install any dependencies you may have.</span></span>

<span data-ttu-id="bc3d2-143">Приведенные ниже скрипты написаны для Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-143">The following scripts were written targeting Python 3.5.</span></span> <span data-ttu-id="bc3d2-144">Если нужно использовать Python версии 2.x, в файле переменной **PYTHON2** установите значение **on** для двух задач запуска и задачи выполнения: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-144">If you want to use the version 2.x of python, set the **PYTHON2** variable file to **on** for the two startup tasks and the runtime task: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.</span></span>

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

<span data-ttu-id="bc3d2-145">В задачу запуска рабочей роли необходимо добавить переменные **PYTHON2** и **PYPATH**.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-145">The **PYTHON2** and **PYPATH** variables must be added to the worker startup task.</span></span> <span data-ttu-id="bc3d2-146">Переменная **PYPATH** используется, только если для переменной **PYTHON2** установлено значение **on**.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-146">The **PYPATH** variable is only used if the **PYTHON2** variable is set to **on**.</span></span>

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

#### <a name="sample-servicedefinitioncsdef"></a><span data-ttu-id="bc3d2-147">Пример файла ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="bc3d2-147">Sample ServiceDefinition.csdef</span></span>
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



<span data-ttu-id="bc3d2-148">Далее в папке **./bin** своей роли создайте файлы **PrepPython.ps1** и **PipInstaller.ps1**.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-148">Next, create the **PrepPython.ps1** and **PipInstaller.ps1** files in the **./bin** folder of your role.</span></span>

#### <a name="preppythonps1"></a><span data-ttu-id="bc3d2-149">Файл PrepPython.ps1</span><span class="sxs-lookup"><span data-stu-id="bc3d2-149">PrepPython.ps1</span></span>
<span data-ttu-id="bc3d2-150">Скрипт в этом файле устанавливает Python.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-150">This script installs python.</span></span> <span data-ttu-id="bc3d2-151">Если для переменной среды **PYTHON2** задано значение **on**, будет установлена версия Python 2.7. В противном случае будет установлена версия Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-151">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is installed, otherwise Python 3.5 is installed.</span></span>

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

        Write-Output "Not found, downloading $url to $outFile$nl"
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

#### <a name="pipinstallerps1"></a><span data-ttu-id="bc3d2-152">Файл PipInstaller.ps1</span><span class="sxs-lookup"><span data-stu-id="bc3d2-152">PipInstaller.ps1</span></span>
<span data-ttu-id="bc3d2-153">Этот скрипт вызывает PIP и устанавливает все зависимости в файле **requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-153">This script calls up pip and installs all of the dependencies in the **requirements.txt** file.</span></span> <span data-ttu-id="bc3d2-154">Если для переменной среды **PYTHON2** задано значение **on**, будет использоваться Python 2.7. В противном случае будет использоваться Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-154">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

#### <a name="modify-launchworkerps1"></a><span data-ttu-id="bc3d2-155">Изменение файла LaunchWorker.ps1</span><span class="sxs-lookup"><span data-stu-id="bc3d2-155">Modify LaunchWorker.ps1</span></span>
> [!NOTE]
> <span data-ttu-id="bc3d2-156">В проекте **рабочей роли** файл **LauncherWorker.ps1** необходим для выполнения файла запуска.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-156">In the case of a **worker role** project, **LauncherWorker.ps1** file is required to execute the startup file.</span></span> <span data-ttu-id="bc3d2-157">В проекте **веб-роли** файл запуска определяется в свойствах проекта.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-157">In a **web role** project, the startup file is instead defined in the project properties.</span></span>
> 
> 

<span data-ttu-id="bc3d2-158">Изначально файл **bin\LaunchWorker.ps1** создавался для выполнения множества подготовительных задач. Но в действительности он этого не делает.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-158">The **bin\LaunchWorker.ps1** was originally created to do a lot of prep work but it doesn't really work.</span></span> <span data-ttu-id="bc3d2-159">Замените содержимое этого файла на приведенный ниже скрипт.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-159">Replace the contents in that file with the following script.</span></span>

<span data-ttu-id="bc3d2-160">Этот скрипт вызывает файл **worker.py** из проекта Python.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-160">This script calls the **worker.py** file from your python project.</span></span> <span data-ttu-id="bc3d2-161">Если для переменной среды **PYTHON2** задано значение **on**, будет использоваться Python 2.7. В противном случае будет использоваться Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-161">If the **PYTHON2** environment variable is set to **on**, then Python 2.7 is used, otherwise Python 3.5 is used.</span></span>

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

    # Customize to your local dev environment

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

#### <a name="pscmd"></a><span data-ttu-id="bc3d2-162">Файл ps.cmd</span><span class="sxs-lookup"><span data-stu-id="bc3d2-162">ps.cmd</span></span>
<span data-ttu-id="bc3d2-163">При выполнении шаблонов Visual Studio в папке **./bin** должен быть создан файл **ps.cmd**.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-163">The Visual Studio templates should have created a **ps.cmd** file in the **./bin** folder.</span></span> <span data-ttu-id="bc3d2-164">Этот скрипт оболочки вызывает приведенные выше скрипты оболочки PowerShell и обеспечивает ведение журнала на основе имени вызванной оболочки PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-164">This shell script calls out the PowerShell wrapper scripts above and provides logging based on the name of the PowerShell wrapper called.</span></span> <span data-ttu-id="bc3d2-165">Если этот файл не создан, вот данные, которые должны в нем содержаться:</span><span class="sxs-lookup"><span data-stu-id="bc3d2-165">If this file wasn't created, here is what should be in it.</span></span> 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a><span data-ttu-id="bc3d2-166">Локальный запуск</span><span class="sxs-lookup"><span data-stu-id="bc3d2-166">Run locally</span></span>
<span data-ttu-id="bc3d2-167">Если настроить проект облачной службы в качестве запускаемого проекта и нажать клавишу F5, эта облачная служба запустится в локальном эмуляторе Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-167">If you set your cloud service project as the startup project and press F5, the cloud service runs in the local Azure emulator.</span></span>

<span data-ttu-id="bc3d2-168">Хотя PTVS поддерживает возможность запуска в эмуляторе, процедура отладки (например, установка точек останова) в этом режиме не работает.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-168">Although PTVS supports launching in the emulator, debugging (for example, breakpoints) does not work.</span></span>

<span data-ttu-id="bc3d2-169">Чтобы отладить веб-роли и рабочие роли, необходимо установить в настройках проекта роли параметр, определяющий его запуск при включении, и выполнить отладку таким образом.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-169">To debug your web and worker roles, you can set the role project as the startup project and debug that instead.</span></span>  <span data-ttu-id="bc3d2-170">В качестве запускаемых при включении можно указать несколько проектов.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-170">You can also set multiple startup projects.</span></span>  <span data-ttu-id="bc3d2-171">Щелкните решение правой кнопкой мыши и выберите пункт **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-171">Right-click the solution and then select **Set StartUp Projects**.</span></span>

![Свойства запускаемого при включении проекта в решении](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-to-azure"></a><span data-ttu-id="bc3d2-173">Публикация в Azure</span><span class="sxs-lookup"><span data-stu-id="bc3d2-173">Publish to Azure</span></span>
<span data-ttu-id="bc3d2-174">Чтобы опубликовать, щелкните правой кнопкой мыши проект облачной службы в решении и выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-174">To publish, right-click the cloud service project in the solution and then select **Publish**.</span></span>

![Вход для публикации в Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

<span data-ttu-id="bc3d2-176">Следуйте указаниям мастера.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-176">Follow the wizard.</span></span> <span data-ttu-id="bc3d2-177">При необходимости включите удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-177">If you need to, enable remote desktop.</span></span> <span data-ttu-id="bc3d2-178">Его также удобно использовать, когда нужно выполнить отладку.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-178">Remote desktop is helpful when you need to debug something.</span></span>

<span data-ttu-id="bc3d2-179">После завершения настройки параметров щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-179">When you are done configuring settings, click **Publish**.</span></span>

<span data-ttu-id="bc3d2-180">В окне вывода можно наблюдать выполнение некоторых операций, а затем появится окно журнала действий Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-180">Some progress appears in the output window, then you'll see the Microsoft Azure Activity Log window.</span></span>

![Окно журнала действий Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

<span data-ttu-id="bc3d2-182">Для развертывания потребуется несколько минут, после чего веб-роли и рабочие роли будут запущены на платформе Azure.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-182">Deployment takes several minutes to complete, then your web and/or worker roles run on Azure!</span></span>

### <a name="investigate-logs"></a><span data-ttu-id="bc3d2-183">Изучение журналов</span><span class="sxs-lookup"><span data-stu-id="bc3d2-183">Investigate logs</span></span>
<span data-ttu-id="bc3d2-184">После того как виртуальная машина в облачной службе запустится и установит Python, можно просмотреть журналы, чтобы найти сообщения о сбое.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-184">After the cloud service virtual machine starts up and installs Python, you can look at the logs to find any failure messages.</span></span> <span data-ttu-id="bc3d2-185">Эти журналы расположены в папке **C:\Resources\Directory\\{role}\LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-185">These logs are located in the **C:\Resources\Directory\\{role}\LogFiles** folder.</span></span> <span data-ttu-id="bc3d2-186">В файле **PrepPython.err.txt** содержится по крайней мере одна ошибка, которая возникает при попытке скрипта обнаружить, установлен ли язык Python. В файле **PipInstaller.err.txt** может быть сообщение о том, что существующая версия PIP устарела.</span><span class="sxs-lookup"><span data-stu-id="bc3d2-186">**PrepPython.err.txt** has at least one error in it from when the script tries to detect if Python is installed and **PipInstaller.err.txt** may complain about an outdated version of pip.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc3d2-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc3d2-187">Next steps</span></span>
<span data-ttu-id="bc3d2-188">С дополнительной информацией о работе с веб-ролями и рабочими ролями в средствах Python для Visual Studio можно ознакомиться в документации PTVS:</span><span class="sxs-lookup"><span data-stu-id="bc3d2-188">For more detailed information about working with web and worker roles in Python Tools for Visual Studio, see the PTVS documentation:</span></span>

* <span data-ttu-id="bc3d2-189">[Azure Cloud Service Projects for Python][Cloud Service Projects] (Проекты для облачной службы Azure для Python)</span><span class="sxs-lookup"><span data-stu-id="bc3d2-189">[Cloud Service Projects][Cloud Service Projects]</span></span>

<span data-ttu-id="bc3d2-190">Дополнительные сведения об использовании служб Azure из веб-ролей или рабочих ролей, например об использовании хранилища Azure или служебной шины Azure, см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="bc3d2-190">For more details about using Azure services from your web and worker roles, such as using Azure Storage or Service Bus, see the following articles:</span></span>

* <span data-ttu-id="bc3d2-191">[Использование хранилища больших двоичных объектов Azure из Python][Blob Service]</span><span class="sxs-lookup"><span data-stu-id="bc3d2-191">[Blob Service][Blob Service]</span></span>
* <span data-ttu-id="bc3d2-192">[Использование табличного хранилища из Python][Table Service]</span><span class="sxs-lookup"><span data-stu-id="bc3d2-192">[Table Service][Table Service]</span></span>
* <span data-ttu-id="bc3d2-193">[Использование хранилища очередей из Python][Queue Service]</span><span class="sxs-lookup"><span data-stu-id="bc3d2-193">[Queue Service][Queue Service]</span></span>
* <span data-ttu-id="bc3d2-194">[Как использовать очереди служебной шины][Service Bus Queues]</span><span class="sxs-lookup"><span data-stu-id="bc3d2-194">[Service Bus Queues][Service Bus Queues]</span></span>
* <span data-ttu-id="bc3d2-195">[Как использовать разделы и подписки служебной шины][Service Bus Topics]</span><span class="sxs-lookup"><span data-stu-id="bc3d2-195">[Service Bus Topics][Service Bus Topics]</span></span>

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
