---
title: "aaaCreate конвейера CI или компакт-диска в Azure с помощью Team Services | Документы Microsoft"
description: "Узнайте, как Visual Studio Team Services toocreate конвейера для непрерывной интеграции и доставки, который развертывает tooIIS приложения web на виртуальной Машине Windows"
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
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="55dc1-103">Создание конвейера для непрерывной интеграции с помощью Visual Studio Team Services и IIS</span><span class="sxs-lookup"><span data-stu-id="55dc1-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="55dc1-104">tooautomate hello сборки, тестирования и развертывания этапах разработки приложения, можно использовать непрерывной интеграции и развертывания (CI/CD) конвейера.</span><span class="sxs-lookup"><span data-stu-id="55dc1-104">tooautomate hello build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="55dc1-105">В рамках этого руководства вы создадите конвейер CI/CD с помощью Visual Studio Team Services и виртуальной машины Windows в Azure, где выполняются службы IIS.</span><span class="sxs-lookup"><span data-stu-id="55dc1-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="55dc1-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="55dc1-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="55dc1-107">Публикация проекта Team Services веб-приложения ASP.NET tooa</span><span class="sxs-lookup"><span data-stu-id="55dc1-107">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="55dc1-108">создавать определение сборки, которое активируется фиксациями кода;</span><span class="sxs-lookup"><span data-stu-id="55dc1-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="55dc1-109">устанавливать и настраивать IIS на виртуальной машине в Azure;</span><span class="sxs-lookup"><span data-stu-id="55dc1-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="55dc1-110">Добавить группу развертывания tooa экземпляр IIS hello в Team Services</span><span class="sxs-lookup"><span data-stu-id="55dc1-110">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="55dc1-111">Создание выпуска определения toopublish новый веб-развертывание пакетов tooIIS</span><span class="sxs-lookup"><span data-stu-id="55dc1-111">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="55dc1-112">Тестирование hello CI/CD конвейера</span><span class="sxs-lookup"><span data-stu-id="55dc1-112">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="55dc1-113">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="55dc1-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="55dc1-114">Запустите `Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="55dc1-114">Run `Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="55dc1-115">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="55dc1-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="55dc1-116">Создание проекта в Team Services</span><span class="sxs-lookup"><span data-stu-id="55dc1-116">Create project in Team Services</span></span>
<span data-ttu-id="55dc1-117">Visual Studio Team Services обеспечивает совместную работу и разработку без необходимости обслуживания решения для управления локальным кодом.</span><span class="sxs-lookup"><span data-stu-id="55dc1-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="55dc1-118">Team Services также позволяет выполнять тестирование кода в облака, а также создавать и анализировать приложение.</span><span class="sxs-lookup"><span data-stu-id="55dc1-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="55dc1-119">Вы можете выбрать интегрированную среду разработки и репозиторий системы управления версиями, которые лучше всего подходят для вашего сценария разработки кода.</span><span class="sxs-lookup"><span data-stu-id="55dc1-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="55dc1-120">В этом учебнике можно использовать бесплатную учетную запись toocreate основные веб-приложения ASP.NET и конвейер CI или компакт-диска.</span><span class="sxs-lookup"><span data-stu-id="55dc1-120">For this tutorial, you can use a free account toocreate a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="55dc1-121">Если у вас еще нет учетной записи Team Services, [создайте ее](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="55dc1-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="55dc1-122">процесс фиксации кода hello toomanage, определений сборок и определения выпуска, Создание проекта в Team Services следующим образом:</span><span class="sxs-lookup"><span data-stu-id="55dc1-122">toomanage hello code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="55dc1-123">В браузере откройте панель мониторинга Team Services и выберите **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="55dc1-124">Введите *myWebApp* для hello **имя проекта**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-124">Enter *myWebApp* for hello **Project name**.</span></span> <span data-ttu-id="55dc1-125">Оставьте все другие toouse значения по умолчанию *Git* системы управления версиями и *Agile* процесс рабочего элемента.</span><span class="sxs-lookup"><span data-stu-id="55dc1-125">Leave all other default values toouse *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="55dc1-126">Выберите параметр hello слишком**предоставить** *члены команды*, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-126">Choose hello option too**Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="55dc1-127">После создания проекта, выберите параметр hello слишком**инициализации при помощи README или gitignore**, затем **инициализировать**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-127">Once your project has been created, choose hello option too**Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="55dc1-128">Внутри нового проекта выберите **панелей мониторинга** сверху hello, затем выберите **в среде Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-128">Inside your new project, choose **Dashboards** across hello top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="55dc1-129">Создание веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="55dc1-129">Create ASP.NET web application</span></span>
<span data-ttu-id="55dc1-130">В предыдущем шаге hello создать проект в Team Services.</span><span class="sxs-lookup"><span data-stu-id="55dc1-130">In hello previous step, you created a project in Team Services.</span></span> <span data-ttu-id="55dc1-131">Последний шаг Hello открывает новый проект в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55dc1-131">hello final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="55dc1-132">Управление фиксаций кода в hello **Team Explorer** окна.</span><span class="sxs-lookup"><span data-stu-id="55dc1-132">You manage your code commits in hello **Team Explorer** window.</span></span> <span data-ttu-id="55dc1-133">Создайте локальную копию нового проекта, а затем создайте веб-приложение ASP.NET из шаблона, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="55dc1-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="55dc1-134">Выберите **клон** toocreate репозитории git локального проекта Team Services.</span><span class="sxs-lookup"><span data-stu-id="55dc1-134">Select **Clone** toocreate a local git repo of your Team Services project.</span></span>
    
    ![Клонирование репозитория из проекта Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="55dc1-136">В разделе **Решения** выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-136">Under **Solutions**, select **New**.</span></span>

    ![Создание решения веб-приложения](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="55dc1-138">Выберите **веб** шаблоны, а затем выберите hello **веб-приложение ASP.NET** шаблона.</span><span class="sxs-lookup"><span data-stu-id="55dc1-138">Select **Web** templates, and then choose hello **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="55dc1-139">Введите имя для вашего приложения, такие как *myWebApp*и снимите флажок hello для **создать каталог для решения**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-139">Enter a name for your application, such as *myWebApp*, and uncheck hello box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="55dc1-140">Если параметр hello, снимите флажок hello слишком**tooproject добавить Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-140">If hello option is available, uncheck hello box too**Add Application Insights tooproject**.</span></span> <span data-ttu-id="55dc1-141">Application Insights требуется вы tooauthorize веб-приложения с помощью Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="55dc1-141">Application Insights requires you tooauthorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="55dc1-142">tookeep простым в этом учебнике, пропустите этот процесс.</span><span class="sxs-lookup"><span data-stu-id="55dc1-142">tookeep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="55dc1-143">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-143">Select **OK**.</span></span>
4. <span data-ttu-id="55dc1-144">Выберите **MVC** из списка шаблонов hello.</span><span class="sxs-lookup"><span data-stu-id="55dc1-144">Choose **MVC** from hello template list.</span></span>
    1. <span data-ttu-id="55dc1-145">Выберите **Изменить способ проверки подлинности**, затем — **Нет проверки подлинности** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="55dc1-146">Выберите **ОК** toocreate решения.</span><span class="sxs-lookup"><span data-stu-id="55dc1-146">Select **OK** toocreate your solution.</span></span>
5. <span data-ttu-id="55dc1-147">В hello **Team Explorer** окно, выберите **изменения**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-147">In hello **Team Explorer** window, choose **Changes**.</span></span>

    ![Зафиксировать репозитория git служб tooTeam локальных изменений](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="55dc1-149">В текстовом поле hello фиксации, введите сообщение, таких как *фиксации начального*.</span><span class="sxs-lookup"><span data-stu-id="55dc1-149">In hello commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="55dc1-150">Выберите **зафиксировать все и синхронизировать** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="55dc1-150">Choose **Commit All and Sync** from hello drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="55dc1-151">Создание определения сборки</span><span class="sxs-lookup"><span data-stu-id="55dc1-151">Create build definition</span></span>
<span data-ttu-id="55dc1-152">В Team Services используется toooutline определение сборки, построение приложения.</span><span class="sxs-lookup"><span data-stu-id="55dc1-152">In Team Services, you use a build definition toooutline how your application should be built.</span></span> <span data-ttu-id="55dc1-153">В этом учебнике мы создадим базового определения, принимает наш исходный код сборки hello решения, а затем создается веб развертывание пакета, можно использовать toorun hello веб-приложения на сервере IIS.</span><span class="sxs-lookup"><span data-stu-id="55dc1-153">In this tutorial, we create a basic definition that takes our source code, builds hello solution, then creates web deploy package we can use toorun hello web app on an IIS server.</span></span>

1. <span data-ttu-id="55dc1-154">В проекте Team Services выберите **построения и выпуска** сверху hello, затем выберите **строит**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-154">In your Team Services project, choose **Build & Release** across hello top, then select **Builds**.</span></span>
3. <span data-ttu-id="55dc1-155">Выберите **+ Новое определение**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="55dc1-156">Выберите hello **ASP.NET (Предварительная версия)** шаблона и выберите **применить**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-156">Choose hello **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="55dc1-157">Оставьте все по умолчанию hello значения задачи.</span><span class="sxs-lookup"><span data-stu-id="55dc1-157">Leave all hello default task values.</span></span> <span data-ttu-id="55dc1-158">В разделе **получить исходный**, убедитесь, что hello *myWebApp* репозитория и *master* выбраны ветви.</span><span class="sxs-lookup"><span data-stu-id="55dc1-158">Under **Get sources**, ensure that hello *myWebApp* repository and *master* branch are selected.</span></span>

    ![Создание определения сборки в проекте Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="55dc1-160">На hello **триггеры** вкладки, переместите ползунок hello **включения триггера** слишком*включено*.</span><span class="sxs-lookup"><span data-stu-id="55dc1-160">On hello **Triggers** tab, move hello slider for **Enable this trigger** too*Enabled*.</span></span>
7. <span data-ttu-id="55dc1-161">Сохранить определение сборки hello и очередь новую сборку, выбрав **сохранить & очередь** , затем **сохранить & очередь** еще раз.</span><span class="sxs-lookup"><span data-stu-id="55dc1-161">Save hello build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="55dc1-162">Оставьте значения по умолчанию hello и выделите **очереди**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-162">Leave hello defaults and select **Queue**.</span></span>

<span data-ttu-id="55dc1-163">Контрольное значение hello сборки запланирован на размещенный агент, затем начинают toobuild.</span><span class="sxs-lookup"><span data-stu-id="55dc1-163">Watch as hello build is scheduled on a hosted agent, then begins toobuild.</span></span> <span data-ttu-id="55dc1-164">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="55dc1-164">hello output is similar toohello following example:</span></span>

![Успешная сборка проекта Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="55dc1-166">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="55dc1-166">Create virtual machine</span></span>
<span data-ttu-id="55dc1-167">tooprovide toorun платформы веб-приложения ASP.NET требуется виртуальной машине под управлением служб IIS.</span><span class="sxs-lookup"><span data-stu-id="55dc1-167">tooprovide a platform toorun your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="55dc1-168">Team Services использует toointeract агента с экземпляра IIS hello как фиксация кода и активации сборок.</span><span class="sxs-lookup"><span data-stu-id="55dc1-168">Team Services uses an agent toointeract with hello IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="55dc1-169">Создайте виртуальную машину Windows Server 2016 с помощью [этого примера скрипта](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55dc1-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="55dc1-170">Он занимает несколько минут для сценария toorun hello и создать hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="55dc1-170">It takes a few minutes for hello script toorun and create hello VM.</span></span> <span data-ttu-id="55dc1-171">После создания hello виртуальной Машины откройте порт 80 для веб-трафика с [AzureRmNetworkSecurityRuleConfig добавить](/powershell/module/azurerm.resources/new-azurermresourcegroup) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="55dc1-171">Once hello VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

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

<span data-ttu-id="55dc1-172">tooconnect tooyour виртуальной Машины, получить hello общедоступный IP-адрес с [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="55dc1-172">tooconnect tooyour VM, obtain hello public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="55dc1-173">Создайте сеанс удаленного рабочего стола tooyour виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="55dc1-173">Create a remote desktop session tooyour VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="55dc1-174">Откройте на hello виртуальной Машины, **PowerShell администратора** командной строки.</span><span class="sxs-lookup"><span data-stu-id="55dc1-174">On hello VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="55dc1-175">Установите IIS и необходимые компоненты .NET, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="55dc1-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="55dc1-176">Создание группы развертывания</span><span class="sxs-lookup"><span data-stu-id="55dc1-176">Create deployment group</span></span>
<span data-ttu-id="55dc1-177">toopush out hello web развертывание сервера IIS toohello пакета, определите группу развертывания в Team Services.</span><span class="sxs-lookup"><span data-stu-id="55dc1-177">toopush out hello web deploy package toohello IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="55dc1-178">Эта группа позволяет toospecify, какие серверы являются целью hello новых сборок, зафиксировал tooTeam кода выполняются службы и сборки.</span><span class="sxs-lookup"><span data-stu-id="55dc1-178">This group allows you toospecify which servers are hello target of new builds as you commit code tooTeam Services and builds are completed.</span></span>

1. <span data-ttu-id="55dc1-179">В Team Services выберите **Сборка и выпуск**, а затем — **Группы развертываний**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="55dc1-180">Выберите **Добавить группу развертывания**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="55dc1-181">Например, введите имя для группы hello *myIIS*, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-181">Enter a name for hello group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="55dc1-182">В hello **зарегистрируйте машины** Убедитесь *Windows* выбран, а затем установите флажок "hello" слишком**использовать в скрипте hello личный маркер доступа для проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-182">In hello **Register machines** section, ensure *Windows* is selected, then check hello box too**Use a personal access token in hello script for authentication**.</span></span>
5. <span data-ttu-id="55dc1-183">Выберите **скопируйте сценарий tooclipboard**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-183">Select **Copy script tooclipboard**.</span></span>


### <a name="add-iis-vm-toohello-deployment-group"></a><span data-ttu-id="55dc1-184">Добавить группу развертывания toohello IIS виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="55dc1-184">Add IIS VM toohello deployment group</span></span>
<span data-ttu-id="55dc1-185">Создание группы развертывания hello добавьте каждой группы toohello экземпляр IIS.</span><span class="sxs-lookup"><span data-stu-id="55dc1-185">With hello deployment group created, add each IIS instance toohello group.</span></span> <span data-ttu-id="55dc1-186">Team Services создает скрипт, который загружает и настраивает агент на hello виртуальной Машины, которая получает новый веб-узел развертывания пакетов, а затем применяет их tooIIS.</span><span class="sxs-lookup"><span data-stu-id="55dc1-186">Team Services generates a script that downloads and configures an agent on hello VM that receives new web deploy packages then applies it tooIIS.</span></span>

1. <span data-ttu-id="55dc1-187">Вернитесь в hello **PowerShell администратора** сеанс на ВМ, вставьте и запустите сценарий hello, скопированные из Team Services.</span><span class="sxs-lookup"><span data-stu-id="55dc1-187">Back in hello **Administrator PowerShell** session on your VM, paste and run hello script copied from Team Services.</span></span>
2. <span data-ttu-id="55dc1-188">Когда запрос tooconfigure теги для агента hello, выберите *Y* и введите *web*.</span><span class="sxs-lookup"><span data-stu-id="55dc1-188">When prompted tooconfigure tags for hello agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="55dc1-189">Когда появится сообщение hello учетной записи пользователя, нажмите клавишу *возвращают* tooaccept hello значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="55dc1-189">When prompted for hello user account, press *Return* tooaccept hello defaults.</span></span>
4. <span data-ttu-id="55dc1-190">Дождитесь hello toofinish сценария с сообщением *vstsagent.account.computername служба успешно запущена*.</span><span class="sxs-lookup"><span data-stu-id="55dc1-190">Wait for hello script toofinish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="55dc1-191">В hello **группы развертывания** страница hello **построения и выпуска** меню, откройте hello *myIIS* Группа развертывания.</span><span class="sxs-lookup"><span data-stu-id="55dc1-191">In hello **Deployment groups** page of hello **Build & Release** menu, open hello *myIIS* deployment group.</span></span> <span data-ttu-id="55dc1-192">На hello **машины** убедитесь, что указана ВМ.</span><span class="sxs-lookup"><span data-stu-id="55dc1-192">On hello **Machines** tab, verify that your VM is listed.</span></span>

    ![Виртуальная машина успешно добавлено tooTeam группы развертывания служб](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="55dc1-194">Создание определения выпуска</span><span class="sxs-lookup"><span data-stu-id="55dc1-194">Create release definition</span></span>
<span data-ttu-id="55dc1-195">toopublish сборки, необходимо создать определение выпуска в Team Services.</span><span class="sxs-lookup"><span data-stu-id="55dc1-195">toopublish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="55dc1-196">Это определение запускается автоматически при успешной сборке приложения.</span><span class="sxs-lookup"><span data-stu-id="55dc1-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="55dc1-197">Необходимо выбрать hello развертывания группы toopush веб-развертывания пакета и определить соответствующие параметры IIS hello.</span><span class="sxs-lookup"><span data-stu-id="55dc1-197">You choose hello deployment group toopush your web deploy package to, and define hello appropriate IIS settings.</span></span>

1. <span data-ttu-id="55dc1-198">Выберите **Сборка и выпуск**, а затем — **Сборки**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="55dc1-199">Выберите определение сборки hello на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="55dc1-199">Choose hello build definition created in a previous step.</span></span>
2. <span data-ttu-id="55dc1-200">В разделе **Недавно завершенные**, выберите последнюю сборку hello, а затем выберите **выпуска**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-200">Under **Recently completed**, choose hello most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="55dc1-201">Выберите **Да** toocreate определения выпуска.</span><span class="sxs-lookup"><span data-stu-id="55dc1-201">Choose **Yes** toocreate a release definition.</span></span>
4. <span data-ttu-id="55dc1-202">Выберите hello **пустой** шаблон, затем выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-202">Choose hello **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="55dc1-203">Убедитесь, определение сборки проекта и исходные hello заполнены проекта.</span><span class="sxs-lookup"><span data-stu-id="55dc1-203">Verify hello project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="55dc1-204">Выберите hello **непрерывного развертывания** флажок, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-204">Select hello **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="55dc1-205">Выберите поле со списком hello Далее слишком**+ добавить задачи** и выберите *добавить этап развертывания группы*.</span><span class="sxs-lookup"><span data-stu-id="55dc1-205">Select hello drop-down box next too**+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Добавьте определение toorelease задач в Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="55dc1-207">Выберите **добавить** Далее слишком**IIS Web App Deploy(Preview)**, а затем выберите **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-207">Choose **Add** next too**IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="55dc1-208">Выберите hello **выполнить для развертывания группы** родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="55dc1-208">Select hello **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="55dc1-209">Для **Группа развертывания**, выберите группу hello развертывания, то созданный ранее, такие как *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="55dc1-209">For **Deployment Group**, select hello deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="55dc1-210">В hello **теги машины** выберите **добавить** и выберите hello *web* тег.</span><span class="sxs-lookup"><span data-stu-id="55dc1-210">In hello **Machine tags** box, select **Add** and choose hello *web* tag.</span></span>
    
    ![Задача группы развертывания определения выпуска для IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="55dc1-212">Выберите hello **развертывание: IIS веб-приложения, развертывание** tooconfigure задачи служб IIS экземпляра параметры следующим образом:</span><span class="sxs-lookup"><span data-stu-id="55dc1-212">Select hello **Deploy: IIS Web App Deploy** task tooconfigure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="55dc1-213">Для **имени веб-сайта** введите *Веб-сайт по умолчанию*.</span><span class="sxs-lookup"><span data-stu-id="55dc1-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="55dc1-214">Оставьте все hello другие параметры по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="55dc1-214">Leave all hello other default settings.</span></span>
12. <span data-ttu-id="55dc1-215">Щелкните **Сохранить**, а затем дважды нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="55dc1-216">Создание выпуска и публикация</span><span class="sxs-lookup"><span data-stu-id="55dc1-216">Create a release and publish</span></span>
<span data-ttu-id="55dc1-217">Теперь вы можете отправить пакет веб-развертывания как новый выпуск.</span><span class="sxs-lookup"><span data-stu-id="55dc1-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="55dc1-218">Этот шаг связывается с агентом hello в каждый экземпляр, который является частью группы развертывания hello, помещает hello web развертывание пакета, а затем настраивает IIS toorun hello обновить веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="55dc1-218">This step communicates with hello agent on each instance that is part of hello deployment group, pushes hello web deploy package, then configures IIS toorun hello updated web application.</span></span>

1. <span data-ttu-id="55dc1-219">В определении выпуска выберите **+ Выпуск**, затем выберите **Создать выпуск**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="55dc1-220">Убедитесь, что последняя сборка hello в раскрывающемся списке hello, вместе с **автоматическое развертывание: после создания выпуска**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-220">Verify that hello latest build is selected in hello drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="55dc1-221">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-221">Select **Create**.</span></span>
3. <span data-ttu-id="55dc1-222">Небольшой баннер hello верхней части появляется определение выпуска, такие как *выпуска «версия 1"был создан*.</span><span class="sxs-lookup"><span data-stu-id="55dc1-222">A small banner appears across hello top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="55dc1-223">Выберите hello ссылка выпуска.</span><span class="sxs-lookup"><span data-stu-id="55dc1-223">Select hello release link.</span></span>
4. <span data-ttu-id="55dc1-224">Откройте hello **журналы** вкладке toowatch hello выпуска выполняется.</span><span class="sxs-lookup"><span data-stu-id="55dc1-224">Open hello **Logs** tab toowatch hello release progress.</span></span>
    
    ![Успешное создание выпуска Team Services и отправка пакета веб-развертывания](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="55dc1-226">После выпуска hello откройте веб-браузер и введите hello общедоступный адрес производства вашей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="55dc1-226">After hello release is complete, open a web browser and enter hello public IIP address of your VM.</span></span> <span data-ttu-id="55dc1-227">Вы увидите, что веб-приложение ASP.NET выполняется.</span><span class="sxs-lookup"><span data-stu-id="55dc1-227">Your ASP.NET web application is running.</span></span>

    ![Выполнение веб-приложения ASP.NET на виртуальной машине IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a><span data-ttu-id="55dc1-229">Весь конвейер CI/CD теста hello</span><span class="sxs-lookup"><span data-stu-id="55dc1-229">Test hello whole CI/CD pipeline</span></span>
<span data-ttu-id="55dc1-230">С веб-приложения на сервере IIS попробуйте hello весь конвейер CI или компакт-диска.</span><span class="sxs-lookup"><span data-stu-id="55dc1-230">With your web application running on IIS, now try hello whole CI/CD pipeline.</span></span> <span data-ttu-id="55dc1-231">После внесения изменений в Visual Studio, чтобы зафиксировать, активируется код сборки, что вызывает выпустить обновленную веб-развертывание пакета tooIIS:</span><span class="sxs-lookup"><span data-stu-id="55dc1-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package tooIIS:</span></span>

1. <span data-ttu-id="55dc1-232">В Visual Studio откройте hello **обозревателе решений** окна.</span><span class="sxs-lookup"><span data-stu-id="55dc1-232">In Visual Studio, open hello **Solution Explorer** window.</span></span>
2. <span data-ttu-id="55dc1-233">Переход открытия tooand *myWebApp | Представления | Главная | Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="55dc1-233">Navigate tooand open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="55dc1-234">Изменение tooread строка 6:</span><span class="sxs-lookup"><span data-stu-id="55dc1-234">Edit line 6 tooread:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="55dc1-235">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="55dc1-235">Save hello file.</span></span>
5. <span data-ttu-id="55dc1-236">Откройте hello **Team Explorer** окно, выберите hello *myWebApp* проекта, а затем выберите **изменения**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-236">Open hello **Team Explorer** window, select hello *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="55dc1-237">Введите сообщение фиксации, например *конвейера тестирование CI/CD*, выберите **все фиксации и синхронизации** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="55dc1-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from hello drop-down menu.</span></span>
7. <span data-ttu-id="55dc1-238">В рабочей области Team Services новая сборка запускается из фиксации кода hello.</span><span class="sxs-lookup"><span data-stu-id="55dc1-238">In Team Services workspace, a new build is triggered from hello code commit.</span></span> 
    - <span data-ttu-id="55dc1-239">Выберите **Сборка и выпуск**, а затем — **Сборки**.</span><span class="sxs-lookup"><span data-stu-id="55dc1-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="55dc1-240">Выберите определение сборки, а затем выберите hello **в очереди и выполнения** toowatch сборки как hello построения продвижения.</span><span class="sxs-lookup"><span data-stu-id="55dc1-240">Choose your build definition, then select hello **Queued & running** build toowatch as hello build progresses.</span></span>
9. <span data-ttu-id="55dc1-241">После успешного построения hello, инициируется новый выпуск.</span><span class="sxs-lookup"><span data-stu-id="55dc1-241">Once hello build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="55dc1-242">Выберите **построения и выпуска**, затем **выпуски** пакет, помещается tooyour ВМ IIS веб-hello toosee развертывания.</span><span class="sxs-lookup"><span data-stu-id="55dc1-242">Choose **Build & Release**, then **Releases** toosee hello web deploy package pushed tooyour IIS VM.</span></span> 
    - <span data-ttu-id="55dc1-243">Выберите hello **обновление** значок tooupdate hello состояния.</span><span class="sxs-lookup"><span data-stu-id="55dc1-243">Select hello **Refresh** icon tooupdate hello status.</span></span> <span data-ttu-id="55dc1-244">Здравствуйте, когда *среды* столбце отображается зеленая галочка, hello выпуска успешно развернута tooIIS.</span><span class="sxs-lookup"><span data-stu-id="55dc1-244">When hello *Environments* column shows a green check mark, hello release has successfully deployed tooIIS.</span></span>
11. <span data-ttu-id="55dc1-245">применить изменения, toosee, обновить веб-сайта IIS, в браузере.</span><span class="sxs-lookup"><span data-stu-id="55dc1-245">toosee your changes applied, refresh your IIS website in a browser.</span></span>

    ![Выполнение веб-приложения ASP.NET на виртуальной машине IIS из конвейера CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="55dc1-247">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55dc1-247">Next steps</span></span>

<span data-ttu-id="55dc1-248">В этом учебнике вы создали веб-приложения ASP.NET в Team Services и настроенного построения и выпуска определения toodeploy нового веб-узла развертывания tooIIS пакетов на каждой фиксации кода.</span><span class="sxs-lookup"><span data-stu-id="55dc1-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions toodeploy new web deploy packages tooIIS on each code commit.</span></span> <span data-ttu-id="55dc1-249">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="55dc1-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="55dc1-250">Публикация проекта Team Services веб-приложения ASP.NET tooa</span><span class="sxs-lookup"><span data-stu-id="55dc1-250">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="55dc1-251">создавать определение сборки, которое активируется фиксациями кода;</span><span class="sxs-lookup"><span data-stu-id="55dc1-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="55dc1-252">устанавливать и настраивать IIS на виртуальной машине в Azure;</span><span class="sxs-lookup"><span data-stu-id="55dc1-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="55dc1-253">Добавить группу развертывания tooa экземпляр IIS hello в Team Services</span><span class="sxs-lookup"><span data-stu-id="55dc1-253">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="55dc1-254">Создание выпуска определения toopublish новый веб-развертывание пакетов tooIIS</span><span class="sxs-lookup"><span data-stu-id="55dc1-254">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="55dc1-255">Тестирование hello CI/CD конвейера</span><span class="sxs-lookup"><span data-stu-id="55dc1-255">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="55dc1-256">Как переместить следующий учебник toolearn toohello toosecure веб-сервере с использованием сертификата SSL.</span><span class="sxs-lookup"><span data-stu-id="55dc1-256">Advance toohello next tutorial toolearn how toosecure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="55dc1-257">[Secure a web server with SSL certificates on a Linux virtual machine in Azure](tutorial-secure-web-server.md) (Защита веб-сервера на виртуальной машине Linux в облаке Azure с помощью SSL-сертификата)</span><span class="sxs-lookup"><span data-stu-id="55dc1-257">[Secure web server with SSL](tutorial-secure-web-server.md)</span></span>