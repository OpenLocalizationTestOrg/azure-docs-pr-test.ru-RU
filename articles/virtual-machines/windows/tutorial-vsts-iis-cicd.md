---
title: "Создание конвейера CI/CD в Azure с помощью служб Team Services | Документация Майкрософт"
description: "Сведения о создании с помощью Visual Studio Team Services конвейера для непрерывной интеграции и доставки, который выполняет развертывание веб-приложения в IIS на виртуальной машине Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a587f58fad2ec74c7633823c4d34f900e7c01f7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="75773-103">Создание конвейера для непрерывной интеграции с помощью Visual Studio Team Services и IIS</span><span class="sxs-lookup"><span data-stu-id="75773-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="75773-104">Чтобы автоматизировать этапы создания, тестирования и развертывания проекта приложения, вы можете использовать конвейер для непрерывной интеграции и развертывания (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="75773-104">To automate the build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="75773-105">В рамках этого руководства вы создадите конвейер CI/CD с помощью Visual Studio Team Services и виртуальной машины Windows в Azure, где выполняются службы IIS.</span><span class="sxs-lookup"><span data-stu-id="75773-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="75773-106">Вы узнаете, как выполнять такие задачи.</span><span class="sxs-lookup"><span data-stu-id="75773-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75773-107">Публикация веб-приложения ASP.NET в проекте Team Services.</span><span class="sxs-lookup"><span data-stu-id="75773-107">Publish an ASP.NET web application to a Team Services project</span></span>
> * <span data-ttu-id="75773-108">создавать определение сборки, которое активируется фиксациями кода;</span><span class="sxs-lookup"><span data-stu-id="75773-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="75773-109">устанавливать и настраивать IIS на виртуальной машине в Azure;</span><span class="sxs-lookup"><span data-stu-id="75773-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="75773-110">добавлять экземпляр IIS в группу развертывания в Team Services;</span><span class="sxs-lookup"><span data-stu-id="75773-110">Add the IIS instance to a deployment group in Team Services</span></span>
> * <span data-ttu-id="75773-111">создавать определение выпуска для публикации новых пакетов веб-развертывания в IIS;</span><span class="sxs-lookup"><span data-stu-id="75773-111">Create a release definition to publish new web deploy packages to IIS</span></span>
> * <span data-ttu-id="75773-112">Тестирование конвейера CI/CD</span><span class="sxs-lookup"><span data-stu-id="75773-112">Test the CI/CD pipeline</span></span>

<span data-ttu-id="75773-113">Для работы с этим руководством требуется модуль Azure PowerShell версии не ниже 3.6.</span><span class="sxs-lookup"><span data-stu-id="75773-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="75773-114">Чтобы узнать версию, выполните команду `Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="75773-114">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="75773-115">Если вам необходимо выполнить обновление, ознакомьтесь со статьей, посвященной [установке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="75773-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="75773-116">Создание проекта в Team Services</span><span class="sxs-lookup"><span data-stu-id="75773-116">Create project in Team Services</span></span>
<span data-ttu-id="75773-117">Visual Studio Team Services обеспечивает совместную работу и разработку без необходимости обслуживания решения для управления локальным кодом.</span><span class="sxs-lookup"><span data-stu-id="75773-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="75773-118">Team Services также позволяет выполнять тестирование кода в облака, а также создавать и анализировать приложение.</span><span class="sxs-lookup"><span data-stu-id="75773-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="75773-119">Вы можете выбрать интегрированную среду разработки и репозиторий системы управления версиями, которые лучше всего подходят для вашего сценария разработки кода.</span><span class="sxs-lookup"><span data-stu-id="75773-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="75773-120">В рамках этого руководства вы можете использовать бесплатную учетную запись, чтобы создать базовое веб-приложение ASP.NET и конвейер CI/CD.</span><span class="sxs-lookup"><span data-stu-id="75773-120">For this tutorial, you can use a free account to create a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="75773-121">Если у вас еще нет учетной записи Team Services, [создайте ее](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="75773-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="75773-122">Чтобы управлять процессом фиксации кода, определениями сборки и выпуска, создайте проект в Team Services следующим образом:</span><span class="sxs-lookup"><span data-stu-id="75773-122">To manage the code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="75773-123">В браузере откройте панель мониторинга Team Services и выберите **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="75773-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="75773-124">Введите *myWebApp* для **имени проекта**.</span><span class="sxs-lookup"><span data-stu-id="75773-124">Enter *myWebApp* for the **Project name**.</span></span> <span data-ttu-id="75773-125">Оставьте все остальные значения по умолчанию, чтобы использовать управление версиями *Git* и процесс рабочих элементов *Agile*.</span><span class="sxs-lookup"><span data-stu-id="75773-125">Leave all other default values to use *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="75773-126">Выберите параметр для **совместного использования** с *участниками команды*, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="75773-126">Choose the option to **Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="75773-127">После создания проекта выберите параметр для **инициализации с файлом сведений или GITIGNORE-файлом**, а затем щелкните **Инициализировать**.</span><span class="sxs-lookup"><span data-stu-id="75773-127">Once your project has been created, choose the option to **Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="75773-128">Внутри нового проекта выберите **Панели мониторинга** в верхней области, а затем — **Открыть в Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="75773-128">Inside your new project, choose **Dashboards** across the top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="75773-129">Создание веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="75773-129">Create ASP.NET web application</span></span>
<span data-ttu-id="75773-130">На предыдущем шаге вы создали проект в Team Services.</span><span class="sxs-lookup"><span data-stu-id="75773-130">In the previous step, you created a project in Team Services.</span></span> <span data-ttu-id="75773-131">На последнем шаге новый проект открывается в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="75773-131">The final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="75773-132">Управление фиксациями кода выполняется в окне **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="75773-132">You manage your code commits in the **Team Explorer** window.</span></span> <span data-ttu-id="75773-133">Создайте локальную копию нового проекта, а затем создайте веб-приложение ASP.NET из шаблона, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="75773-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="75773-134">Нажмите кнопку **Клонировать**, чтобы создать локальный репозиторий Git проекта Team Services.</span><span class="sxs-lookup"><span data-stu-id="75773-134">Select **Clone** to create a local git repo of your Team Services project.</span></span>
    
    ![Клонирование репозитория из проекта Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="75773-136">В разделе **Решения** выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="75773-136">Under **Solutions**, select **New**.</span></span>

    ![Создание решения веб-приложения](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="75773-138">Выберите шаблоны **Веб**, а затем выберите шаблон **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="75773-138">Select **Web** templates, and then choose the **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="75773-139">Введите имя приложения, например *myWebApp*, а затем снимите флажок для параметра **Создать каталог для решения**.</span><span class="sxs-lookup"><span data-stu-id="75773-139">Enter a name for your application, such as *myWebApp*, and uncheck the box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="75773-140">Снимите флажок для параметра **Добавить Application Insights в проект**, если он доступен.</span><span class="sxs-lookup"><span data-stu-id="75773-140">If the option is available, uncheck the box to **Add Application Insights to project**.</span></span> <span data-ttu-id="75773-141">Вам потребуется авторизовать веб-приложение в Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="75773-141">Application Insights requires you to authorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="75773-142">Чтобы упростить работу с этим руководством, пропустите этот процесс.</span><span class="sxs-lookup"><span data-stu-id="75773-142">To keep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="75773-143">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="75773-143">Select **OK**.</span></span>
4. <span data-ttu-id="75773-144">Из списка шаблонов выберите **MVC**.</span><span class="sxs-lookup"><span data-stu-id="75773-144">Choose **MVC** from the template list.</span></span>
    1. <span data-ttu-id="75773-145">Выберите **Изменить способ проверки подлинности**, затем — **Нет проверки подлинности** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="75773-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="75773-146">Нажмите кнопку **ОК**, чтобы создать решение.</span><span class="sxs-lookup"><span data-stu-id="75773-146">Select **OK** to create your solution.</span></span>
5. <span data-ttu-id="75773-147">В окне **Team Explorer** выберите **Изменения**.</span><span class="sxs-lookup"><span data-stu-id="75773-147">In the **Team Explorer** window, choose **Changes**.</span></span>

    ![Фиксация локальных изменений в репозитории Git в Team Services](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="75773-149">В текстовом поле фиксации введите сообщение, например *Начальная фиксация*.</span><span class="sxs-lookup"><span data-stu-id="75773-149">In the commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="75773-150">В раскрывающемся меню выберите **Зафиксировать все и синхронизировать**.</span><span class="sxs-lookup"><span data-stu-id="75773-150">Choose **Commit All and Sync** from the drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="75773-151">Создание определения сборки</span><span class="sxs-lookup"><span data-stu-id="75773-151">Create build definition</span></span>
<span data-ttu-id="75773-152">Вы используете определение сборки в Team Services, чтобы обозначить, как должно быть создано приложение.</span><span class="sxs-lookup"><span data-stu-id="75773-152">In Team Services, you use a build definition to outline how your application should be built.</span></span> <span data-ttu-id="75773-153">В рамках этого руководства мы создадим базовое определение, которое выполняет сборку решения на основе исходного кода, а затем создает пакет веб-развертывания, который мы можем использовать для запуска веб-приложения на сервере IIS.</span><span class="sxs-lookup"><span data-stu-id="75773-153">In this tutorial, we create a basic definition that takes our source code, builds the solution, then creates web deploy package we can use to run the web app on an IIS server.</span></span>

1. <span data-ttu-id="75773-154">В проекте Team Services выберите **Сборка и выпуск** в верхней области, а затем — **Сборки**.</span><span class="sxs-lookup"><span data-stu-id="75773-154">In your Team Services project, choose **Build & Release** across the top, then select **Builds**.</span></span>
3. <span data-ttu-id="75773-155">Выберите **+ Новое определение**.</span><span class="sxs-lookup"><span data-stu-id="75773-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="75773-156">Выберите шаблон **ASP.NET (предварительная версия)**, а затем щелкните **Применить**.</span><span class="sxs-lookup"><span data-stu-id="75773-156">Choose the **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="75773-157">Оставьте все значения задач по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="75773-157">Leave all the default task values.</span></span> <span data-ttu-id="75773-158">В разделе **Получить исходные коды** выберите репозиторий *myWebApp* и *главную* ветвь.</span><span class="sxs-lookup"><span data-stu-id="75773-158">Under **Get sources**, ensure that the *myWebApp* repository and *master* branch are selected.</span></span>

    ![Создание определения сборки в проекте Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="75773-160">На вкладке **Триггеры** переместите ползунок для параметра **включения триггера** в значение *Включено*.</span><span class="sxs-lookup"><span data-stu-id="75773-160">On the **Triggers** tab, move the slider for **Enable this trigger** to *Enabled*.</span></span>
7. <span data-ttu-id="75773-161">Сохраните определение сборки и поместите в очередь новую сборку, выбрав **Сохранить и поместить в очередь**, а затем **снова выберите этот параметр**.</span><span class="sxs-lookup"><span data-stu-id="75773-161">Save the build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="75773-162">Оставьте остальные значения по умолчанию, а затем выберите **Очередь**.</span><span class="sxs-lookup"><span data-stu-id="75773-162">Leave the defaults and select **Queue**.</span></span>

<span data-ttu-id="75773-163">Просмотрите, как планируется выполнение сборки на размещенном агенте и как выполняется сам процесс сборки.</span><span class="sxs-lookup"><span data-stu-id="75773-163">Watch as the build is scheduled on a hosted agent, then begins to build.</span></span> <span data-ttu-id="75773-164">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="75773-164">The output is similar to the following example:</span></span>

![Успешная сборка проекта Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="75773-166">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="75773-166">Create virtual machine</span></span>
<span data-ttu-id="75773-167">Чтобы предоставить платформу для выполнения веб-приложения ASP.NET, вам необходима виртуальная машина Windows, где выполняются службы IIS.</span><span class="sxs-lookup"><span data-stu-id="75773-167">To provide a platform to run your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="75773-168">Team Services использует агент для взаимодействия с экземпляром IIS после фиксации кода и активации сборок.</span><span class="sxs-lookup"><span data-stu-id="75773-168">Team Services uses an agent to interact with the IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="75773-169">Создайте виртуальную машину Windows Server 2016 с помощью [этого примера скрипта](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="75773-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="75773-170">Выполнение скрипта и создание виртуальной машины занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="75773-170">It takes a few minutes for the script to run and create the VM.</span></span> <span data-ttu-id="75773-171">После создания виртуальной машины откройте порт 80 для веб-трафика с помощью команды [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup), как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="75773-171">Once the VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

<span data-ttu-id="75773-172">Чтобы подключиться к виртуальной машине, получите общедоступный IP-адрес с помощью команды [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress), как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="75773-172">To connect to your VM, obtain the public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="75773-173">Создайте сеанс подключения к удаленному рабочему столу виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="75773-173">Create a remote desktop session to your VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="75773-174">На виртуальной машине откройте окно командной строки **PowerShell с правами администратора**.</span><span class="sxs-lookup"><span data-stu-id="75773-174">On the VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="75773-175">Установите IIS и необходимые компоненты .NET, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="75773-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="75773-176">Создание группы развертывания</span><span class="sxs-lookup"><span data-stu-id="75773-176">Create deployment group</span></span>
<span data-ttu-id="75773-177">Чтобы передать пакет веб-развертывания на сервер IIS, вам необходимо определить группу развертывания в Team Services.</span><span class="sxs-lookup"><span data-stu-id="75773-177">To push out the web deploy package to the IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="75773-178">Эта группа позволяет указать, какие серверы являются целевыми серверами новых сборок после фиксации кода в Team Services и завершения сборок.</span><span class="sxs-lookup"><span data-stu-id="75773-178">This group allows you to specify which servers are the target of new builds as you commit code to Team Services and builds are completed.</span></span>

1. <span data-ttu-id="75773-179">В Team Services выберите **Сборка и выпуск**, а затем — **Группы развертываний**.</span><span class="sxs-lookup"><span data-stu-id="75773-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="75773-180">Выберите **Добавить группу развертывания**.</span><span class="sxs-lookup"><span data-stu-id="75773-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="75773-181">Введите имя группы, например *myIIS*, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="75773-181">Enter a name for the group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="75773-182">В разделе **Регистрация компьютеров** выберите *Windows*, а затем установите флажок для параметра **использования личного маркера доступа в скрипте для проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="75773-182">In the **Register machines** section, ensure *Windows* is selected, then check the box to **Use a personal access token in the script for authentication**.</span></span>
5. <span data-ttu-id="75773-183">Выберите параметр **Copy script to clipboard** (Копировать скрипт в буфер обмена).</span><span class="sxs-lookup"><span data-stu-id="75773-183">Select **Copy script to clipboard**.</span></span>


### <a name="add-iis-vm-to-the-deployment-group"></a><span data-ttu-id="75773-184">Добавление виртуальной машины с IIS в группу развертывания</span><span class="sxs-lookup"><span data-stu-id="75773-184">Add IIS VM to the deployment group</span></span>
<span data-ttu-id="75773-185">Добавьте каждый экземпляр IIS в созданную группу развертывания.</span><span class="sxs-lookup"><span data-stu-id="75773-185">With the deployment group created, add each IIS instance to the group.</span></span> <span data-ttu-id="75773-186">Team Services создает скрипт, который загружает и настраивает агент на виртуальной машине, которая получает новые пакеты веб-развертывания, а затем применяет их к IIS.</span><span class="sxs-lookup"><span data-stu-id="75773-186">Team Services generates a script that downloads and configures an agent on the VM that receives new web deploy packages then applies it to IIS.</span></span>

1. <span data-ttu-id="75773-187">Вернитесь в сеанс **PowerShell с правами администратора**, запущенный на виртуальной машине, вставьте и запустите скрипт, скопированный из Team Services.</span><span class="sxs-lookup"><span data-stu-id="75773-187">Back in the **Administrator PowerShell** session on your VM, paste and run the script copied from Team Services.</span></span>
2. <span data-ttu-id="75773-188">При появлении запроса на настройку тегов для агента выберите *Y* и введите *web*.</span><span class="sxs-lookup"><span data-stu-id="75773-188">When prompted to configure tags for the agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="75773-189">При появлении запроса на указание учетной записи пользователя щелкните *Возврат*, чтобы принять значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="75773-189">When prompted for the user account, press *Return* to accept the defaults.</span></span>
4. <span data-ttu-id="75773-190">Ожидайте сообщение о завершении выполнения скрипта — *Служба vstsagent.account.computername успешно запущена*.</span><span class="sxs-lookup"><span data-stu-id="75773-190">Wait for the script to finish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="75773-191">На странице **групп развертывания** меню **сборки и выпуска** откройте группу развертывания *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="75773-191">In the **Deployment groups** page of the **Build & Release** menu, open the *myIIS* deployment group.</span></span> <span data-ttu-id="75773-192">Убедитесь, что ваша виртуальная машина находится в списке на вкладке **Компьютеры**.</span><span class="sxs-lookup"><span data-stu-id="75773-192">On the **Machines** tab, verify that your VM is listed.</span></span>

    ![Виртуальная машина успешно добавлена в группу развертывания Team Services](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="75773-194">Создание определения выпуска</span><span class="sxs-lookup"><span data-stu-id="75773-194">Create release definition</span></span>
<span data-ttu-id="75773-195">Чтобы опубликовать сборки, создайте определение выпуска в Team Services.</span><span class="sxs-lookup"><span data-stu-id="75773-195">To publish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="75773-196">Это определение запускается автоматически при успешной сборке приложения.</span><span class="sxs-lookup"><span data-stu-id="75773-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="75773-197">Вам необходимо выбрать группу развертывания, в которую требуется опубликовать пакет веб-развертывания, а также определить соответствующие параметры IIS.</span><span class="sxs-lookup"><span data-stu-id="75773-197">You choose the deployment group to push your web deploy package to, and define the appropriate IIS settings.</span></span>

1. <span data-ttu-id="75773-198">Выберите **Сборка и выпуск**, а затем — **Сборки**.</span><span class="sxs-lookup"><span data-stu-id="75773-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="75773-199">Выберите определение сборки, созданное на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="75773-199">Choose the build definition created in a previous step.</span></span>
2. <span data-ttu-id="75773-200">В разделе **Недавно завершенные** выберите последнюю сборку, а затем — **Версия**.</span><span class="sxs-lookup"><span data-stu-id="75773-200">Under **Recently completed**, choose the most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="75773-201">Щелкните **Да**, чтобы создать определение выпуска.</span><span class="sxs-lookup"><span data-stu-id="75773-201">Choose **Yes** to create a release definition.</span></span>
4. <span data-ttu-id="75773-202">Выберите шаблон **Пустой**, а затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="75773-202">Choose the **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="75773-203">Параметры проекта и определения сборки источника должны быть заполнены данными вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="75773-203">Verify the project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="75773-204">Установите флажок для параметра **Непрерывное развертывание**, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="75773-204">Select the **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="75773-205">Щелкните раскрывающийся список рядом с параметром **+ Добавить задачи** и выберите *Добавить этап группы развертывания*.</span><span class="sxs-lookup"><span data-stu-id="75773-205">Select the drop-down box next to **+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Добавление задачи в определение выпуска в Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="75773-207">Выберите **Добавить** рядом с **IIS Web App Deploy(Preview)** (Развертывание веб-приложения IIS (предварительная версия)), а затем выберите **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="75773-207">Choose **Add** next to **IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="75773-208">Выберите родительскую задачу **Запуск в группе развертывания**.</span><span class="sxs-lookup"><span data-stu-id="75773-208">Select the **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="75773-209">Для **группы развертывания** выберите ранее созданную группу развертывания, например *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="75773-209">For **Deployment Group**, select the deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="75773-210">В поле **Теги компьютера** выберите **Добавить**, а затем выберите тег *web*.</span><span class="sxs-lookup"><span data-stu-id="75773-210">In the **Machine tags** box, select **Add** and choose the *web* tag.</span></span>
    
    ![Задача группы развертывания определения выпуска для IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="75773-212">Выберите задачу **развертывания веб-приложения IIS**, чтобы настроить параметры экземпляра IIS, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="75773-212">Select the **Deploy: IIS Web App Deploy** task to configure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="75773-213">Для **имени веб-сайта** введите *Веб-сайт по умолчанию*.</span><span class="sxs-lookup"><span data-stu-id="75773-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="75773-214">Оставьте все остальные параметры по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="75773-214">Leave all the other default settings.</span></span>
12. <span data-ttu-id="75773-215">Щелкните **Сохранить**, а затем дважды нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="75773-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="75773-216">Создание выпуска и публикация</span><span class="sxs-lookup"><span data-stu-id="75773-216">Create a release and publish</span></span>
<span data-ttu-id="75773-217">Теперь вы можете отправить пакет веб-развертывания как новый выпуск.</span><span class="sxs-lookup"><span data-stu-id="75773-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="75773-218">На этом шаге выполняется взаимодействие с агентом в каждом экземпляре, который является частью группы развертывания, отправка пакета веб-развертывания, а затем настройка IIS для выполнения обновленного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="75773-218">This step communicates with the agent on each instance that is part of the deployment group, pushes the web deploy package, then configures IIS to run the updated web application.</span></span>

1. <span data-ttu-id="75773-219">В определении выпуска выберите **+ Выпуск**, затем выберите **Создать выпуск**.</span><span class="sxs-lookup"><span data-stu-id="75773-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="75773-220">В раскрывающемся списке выберите последнюю сборку, а также триггер **Автоматическое развертывание: после создания выпуска**.</span><span class="sxs-lookup"><span data-stu-id="75773-220">Verify that the latest build is selected in the drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="75773-221">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="75773-221">Select **Create**.</span></span>
3. <span data-ttu-id="75773-222">В верхней области определения выпуска появится небольшой баннер, например *Создан выпуск 1*.</span><span class="sxs-lookup"><span data-stu-id="75773-222">A small banner appears across the top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="75773-223">Выберите ссылку выпуска.</span><span class="sxs-lookup"><span data-stu-id="75773-223">Select the release link.</span></span>
4. <span data-ttu-id="75773-224">Откройте вкладку **Журналы**, чтобы просмотреть состояние выпуска.</span><span class="sxs-lookup"><span data-stu-id="75773-224">Open the **Logs** tab to watch the release progress.</span></span>
    
    ![Успешное создание выпуска Team Services и отправка пакета веб-развертывания](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="75773-226">После создания выпуска откройте браузер и введите общедоступный IP-адрес виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="75773-226">After the release is complete, open a web browser and enter the public IIP address of your VM.</span></span> <span data-ttu-id="75773-227">Вы увидите, что веб-приложение ASP.NET выполняется.</span><span class="sxs-lookup"><span data-stu-id="75773-227">Your ASP.NET web application is running.</span></span>

    ![Выполнение веб-приложения ASP.NET на виртуальной машине IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-the-whole-cicd-pipeline"></a><span data-ttu-id="75773-229">Тестирование всего конвейера CI/CD</span><span class="sxs-lookup"><span data-stu-id="75773-229">Test the whole CI/CD pipeline</span></span>
<span data-ttu-id="75773-230">Теперь, когда у вас есть веб-приложение, выполняющееся на IIS, запустите конвейер CI/CD.</span><span class="sxs-lookup"><span data-stu-id="75773-230">With your web application running on IIS, now try the whole CI/CD pipeline.</span></span> <span data-ttu-id="75773-231">После внесения изменений в Visual Studio и фиксации кода активируется сборка, которая затем запускает выпуск обновленного пакета веб-развертывания в IIS:</span><span class="sxs-lookup"><span data-stu-id="75773-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package to IIS:</span></span>

1. <span data-ttu-id="75773-232">В Visual Studio откройте окно **обозревателя решений**.</span><span class="sxs-lookup"><span data-stu-id="75773-232">In Visual Studio, open the **Solution Explorer** window.</span></span>
2. <span data-ttu-id="75773-233">Выберите *myWebApp | Views | Home | Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="75773-233">Navigate to and open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="75773-234">Измените строку 6 на следующую:</span><span class="sxs-lookup"><span data-stu-id="75773-234">Edit line 6 to read:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="75773-235">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="75773-235">Save the file.</span></span>
5. <span data-ttu-id="75773-236">Откройте окно **Team Explorer** и выберите проект *myWebApp*, а затем — **Изменения**.</span><span class="sxs-lookup"><span data-stu-id="75773-236">Open the **Team Explorer** window, select the *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="75773-237">Введите сообщение фиксации, например *Тестирование конвейера CI/CD*, а затем в раскрывающемся меню выберите **Зафиксировать все и синхронизировать**.</span><span class="sxs-lookup"><span data-stu-id="75773-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from the drop-down menu.</span></span>
7. <span data-ttu-id="75773-238">В рабочей области Team Services новая сборка активируется из фиксации кода.</span><span class="sxs-lookup"><span data-stu-id="75773-238">In Team Services workspace, a new build is triggered from the code commit.</span></span> 
    - <span data-ttu-id="75773-239">Выберите **Сборка и выпуск**, а затем — **Сборки**.</span><span class="sxs-lookup"><span data-stu-id="75773-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="75773-240">Выберите свое определение сборки, а затем выберите сборку **В очереди и выполняется** для отслеживания процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="75773-240">Choose your build definition, then select the **Queued & running** build to watch as the build progresses.</span></span>
9. <span data-ttu-id="75773-241">После успешного выполнения сборки активируется новый выпуск.</span><span class="sxs-lookup"><span data-stu-id="75773-241">Once the build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="75773-242">Выберите **Сборка и выпуск**, а затем — **Выпуски**, чтобы увидеть пакет веб-развертывания, отправленный на виртуальную машину IIS.</span><span class="sxs-lookup"><span data-stu-id="75773-242">Choose **Build & Release**, then **Releases** to see the web deploy package pushed to your IIS VM.</span></span> 
    - <span data-ttu-id="75773-243">Щелкните значок **обновления**, чтобы обновить состояние.</span><span class="sxs-lookup"><span data-stu-id="75773-243">Select the **Refresh** icon to update the status.</span></span> <span data-ttu-id="75773-244">Появление в столбце *сред* зеленой галочки означает успешное развертывание выпуска в IIS.</span><span class="sxs-lookup"><span data-stu-id="75773-244">When the *Environments* column shows a green check mark, the release has successfully deployed to IIS.</span></span>
11. <span data-ttu-id="75773-245">Чтобы увидеть, что изменения применены, обновите веб-сайт IIS в браузере.</span><span class="sxs-lookup"><span data-stu-id="75773-245">To see your changes applied, refresh your IIS website in a browser.</span></span>

    ![Выполнение веб-приложения ASP.NET на виртуальной машине IIS из конвейера CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="75773-247">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="75773-247">Next steps</span></span>

<span data-ttu-id="75773-248">В рамках этого руководства вы создали веб-приложение ASP.NET в Team Services, а также настроили определения сборки и выпуска для развертывания новых пакетов веб-развертывания в IIS для каждой фиксации кода.</span><span class="sxs-lookup"><span data-stu-id="75773-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions to deploy new web deploy packages to IIS on each code commit.</span></span> <span data-ttu-id="75773-249">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="75773-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75773-250">публиковать веб-приложение ASP.NET в проекте Team Services;</span><span class="sxs-lookup"><span data-stu-id="75773-250">Publish an ASP.NET web application to a Team Services project</span></span>
> * <span data-ttu-id="75773-251">создавать определение сборки, которое активируется фиксациями кода;</span><span class="sxs-lookup"><span data-stu-id="75773-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="75773-252">устанавливать и настраивать IIS на виртуальной машине в Azure;</span><span class="sxs-lookup"><span data-stu-id="75773-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="75773-253">добавлять экземпляр IIS в группу развертывания в Team Services;</span><span class="sxs-lookup"><span data-stu-id="75773-253">Add the IIS instance to a deployment group in Team Services</span></span>
> * <span data-ttu-id="75773-254">создавать определение выпуска для публикации новых пакетов веб-развертывания в IIS;</span><span class="sxs-lookup"><span data-stu-id="75773-254">Create a release definition to publish new web deploy packages to IIS</span></span>
> * <span data-ttu-id="75773-255">Тестирование конвейера CI/CD</span><span class="sxs-lookup"><span data-stu-id="75773-255">Test the CI/CD pipeline</span></span>

<span data-ttu-id="75773-256">Перейдите к следующему руководству, чтобы узнать, как защитить веб-сервер с помощью SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="75773-256">Advance to the next tutorial to learn how to secure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="75773-257">[Secure a web server with SSL certificates on a Linux virtual machine in Azure](tutorial-secure-web-server.md) (Защита веб-сервера на виртуальной машине Linux в облаке Azure с помощью SSL-сертификата)</span><span class="sxs-lookup"><span data-stu-id="75773-257">[Secure web server with SSL](tutorial-secure-web-server.md)</span></span>