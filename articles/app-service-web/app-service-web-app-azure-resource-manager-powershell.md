---
title: "Диспетчер ресурсов на основе PowerShell aaaAzure команды для веб-приложения Azure | Документы Microsoft"
description: "Узнайте, как toouse hello новый toomanage команды PowerShell на основе диспетчера ресурсов Azure, веб-приложения Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="2db96-103">С помощью веб-приложениях Azure Azure Resource Manager-Based PowerShell tooManage</span><span class="sxs-lookup"><span data-stu-id="2db96-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2db96-104">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="2db96-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="2db96-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2db96-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="2db96-106">С помощью Microsoft Azure PowerShell версии 1.0.0 новые команды будут добавлены, предоставляющее toomanage под управлением диспетчера ресурсов Azure PowerShell команды hello возможность hello пользователя toouse веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="2db96-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="2db96-107">toolearn об управлении группами ресурсов, в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2db96-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="2db96-108">toolearn о hello полный список параметров и параметров для hello командлеты PowerShell в разделе hello [полный Справочник по командлетам командлетов PowerShell на основе диспетчера ресурсов Azure Web App](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="2db96-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="2db96-109">Управление планами службы приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="2db96-110">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-110">Create an App Service Plan</span></span>
<span data-ttu-id="2db96-111">план служб приложений toocreate использовать hello **New AzureRmAppServicePlan** командлета.</span><span class="sxs-lookup"><span data-stu-id="2db96-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="2db96-112">Ниже описаны различные параметры hello:</span><span class="sxs-lookup"><span data-stu-id="2db96-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="2db96-113">**Имя**: имя плана обслуживания приложений hello.</span><span class="sxs-lookup"><span data-stu-id="2db96-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="2db96-114">**Location**: расположение плана службы.</span><span class="sxs-lookup"><span data-stu-id="2db96-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="2db96-115">**ResourceGroupName**: группа ресурсов, содержащая hello только что созданный план обслуживания приложений.</span><span class="sxs-lookup"><span data-stu-id="2db96-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="2db96-116">**Уровень**: hello требуемого ценовой категории (по умолчанию — Free, есть параметры, Shared, Basic, Standard и Premium).</span><span class="sxs-lookup"><span data-stu-id="2db96-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="2db96-117">**WorkerSize**: hello размер работников (по умолчанию — небольшой, если указан параметр hello уровня Basic, Standard или Premium.</span><span class="sxs-lookup"><span data-stu-id="2db96-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="2db96-118">По умолчанию Small, если для параметра Tier указано значение Basic, Standard или Premium; также допустимы варианты Medium и Large.</span><span class="sxs-lookup"><span data-stu-id="2db96-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="2db96-119">**NumberofWorkers**: hello число рабочих процессов в hello плана (значение по умолчанию — 1).</span><span class="sxs-lookup"><span data-stu-id="2db96-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="2db96-120">Пример toouse этого командлета:</span><span class="sxs-lookup"><span data-stu-id="2db96-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="2db96-121">Создание плана службы приложений в среде служб приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="2db96-122">toocreate план служб приложений в среде службы приложений, используйте hello же команда **New AzureRmAppServicePlan** команду с именем hello toospecify лишние параметры ASE и имя группы ресурсов в ASE.</span><span class="sxs-lookup"><span data-stu-id="2db96-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="2db96-123">Пример toouse этого командлета:</span><span class="sxs-lookup"><span data-stu-id="2db96-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="2db96-124">Дополнительные сведения о среде службы приложений, проверка toolearn [tooApp введение среды службы](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="2db96-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="2db96-125">Получение списка существующих планов службы приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-125">List Existing App Service Plans</span></span>
<span data-ttu-id="2db96-126">использовать toolist hello существующих планах службы приложений, **Get AzureRmAppServicePlan** командлета.</span><span class="sxs-lookup"><span data-stu-id="2db96-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="2db96-127">toolist используйте всех планах службы приложений в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="2db96-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="2db96-128">toolist всех планах службы приложений в определенной группе ресурсов, используйте:</span><span class="sxs-lookup"><span data-stu-id="2db96-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="2db96-129">Используйте tooget план обслуживания определенного приложения.</span><span class="sxs-lookup"><span data-stu-id="2db96-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="2db96-130">Настройка существующего плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="2db96-131">Параметры hello toochange существующего плана служб приложений, используйте hello **AzureRmAppServicePlan набор** командлета.</span><span class="sxs-lookup"><span data-stu-id="2db96-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="2db96-132">Можно изменить уровень hello, размер рабочего потока и hello число рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="2db96-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="2db96-133">Масштабирование плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="2db96-134">использовать существующий план служб приложений, tooscale:</span><span class="sxs-lookup"><span data-stu-id="2db96-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="2db96-135">Изменение размера рабочей hello план служб приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="2db96-136">размер hello toochange рабочих процессов в существующий план служб приложений, используйте:</span><span class="sxs-lookup"><span data-stu-id="2db96-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="2db96-137">Изменение hello уровня план служб приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="2db96-138">toochange уровень hello существующий план служб приложений, используйте:</span><span class="sxs-lookup"><span data-stu-id="2db96-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="2db96-139">Удаление существующего плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="2db96-140">toodelete существующего плана служб приложений все назначенные toobe необходимость приложения web перемещен или удален сначала.</span><span class="sxs-lookup"><span data-stu-id="2db96-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="2db96-141">Затем с помощью hello **AzureRmAppServicePlan удаление** командлета можно удалить план служб приложений hello.</span><span class="sxs-lookup"><span data-stu-id="2db96-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="2db96-142">Управление веб-приложениями службы приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="2db96-143">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="2db96-143">Create a Web App</span></span>
<span data-ttu-id="2db96-144">toocreate веб-приложения, используйте hello **New AzureRmWebApp** командлета.</span><span class="sxs-lookup"><span data-stu-id="2db96-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="2db96-145">Ниже описаны различные параметры hello:</span><span class="sxs-lookup"><span data-stu-id="2db96-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="2db96-146">**Имя**: имя для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2db96-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="2db96-147">**AppServicePlan**: имя для плана обслуживания hello используется toohost hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2db96-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="2db96-148">**ResourceGroupName**: группы ресурсов, на котором размещена hello план обслуживания приложений.</span><span class="sxs-lookup"><span data-stu-id="2db96-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="2db96-149">**Расположение**: hello местоположению веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2db96-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="2db96-150">Пример toouse этого командлета:</span><span class="sxs-lookup"><span data-stu-id="2db96-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="2db96-151">Создание веб-приложения в среде службы приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="2db96-152">toocreate веб-приложения в среде службы приложений (ASE).</span><span class="sxs-lookup"><span data-stu-id="2db96-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="2db96-153">Используйте hello же **New AzureRmWebApp** команду с именем hello ASE toospecify лишние параметры и имя группы ресурсов hello, к которой принадлежит hello ASE.</span><span class="sxs-lookup"><span data-stu-id="2db96-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="2db96-154">Дополнительные сведения о среде службы приложений, проверка toolearn [tooApp введение среды службы](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="2db96-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="2db96-155">Удаление существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="2db96-155">Delete an existing Web App</span></span>
<span data-ttu-id="2db96-156">toodelete существующего веб-приложения, можно использовать hello **AzureRmWebApp удаление** командлета, требуется имя веб-приложения hello toospecify hello и имя группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="2db96-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="2db96-157">Список существующих веб-приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-157">List existing Web Apps</span></span>
<span data-ttu-id="2db96-158">toolist hello существующего веб-приложения, используют hello **Get AzureRmWebApp** командлета.</span><span class="sxs-lookup"><span data-stu-id="2db96-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="2db96-159">Используйте для всех веб-приложений в вашей подписке toolist:</span><span class="sxs-lookup"><span data-stu-id="2db96-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="2db96-160">Используйте для всех веб-приложений в определенной группе ресурсов, toolist:</span><span class="sxs-lookup"><span data-stu-id="2db96-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="2db96-161">tooget определенного веб-приложения, используйте:</span><span class="sxs-lookup"><span data-stu-id="2db96-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="2db96-162">Настройка существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="2db96-162">Configure an existing Web App</span></span>
<span data-ttu-id="2db96-163">Параметры toochange hello и конфигурации для существующего веб-приложения используйте hello **AzureRmWebApp набор** командлета.</span><span class="sxs-lookup"><span data-stu-id="2db96-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="2db96-164">Полный список параметров, проверьте hello [перехода по ссылке командлета](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="2db96-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="2db96-165">Пример (1): используйте этот командлет строки подключения с toochange</span><span class="sxs-lookup"><span data-stu-id="2db96-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="2db96-166">Пример 2. Добавление или изменение параметров приложения:</span><span class="sxs-lookup"><span data-stu-id="2db96-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="2db96-167">Пример (3): toorun набор hello веб приложения в 64-разрядном режиме</span><span class="sxs-lookup"><span data-stu-id="2db96-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="2db96-168">Изменить состояние hello существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="2db96-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="2db96-169">Перезапуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="2db96-169">Restart a web app</span></span>
<span data-ttu-id="2db96-170">toorestart веб-приложения, необходимо указать hello имя и группе ресурсов hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2db96-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="2db96-171">Остановка веб-приложения</span><span class="sxs-lookup"><span data-stu-id="2db96-171">Stop a web app</span></span>
<span data-ttu-id="2db96-172">toostop веб-приложения, необходимо указать hello имя и группе ресурсов hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2db96-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="2db96-173">Запуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="2db96-173">Start a web app</span></span>
<span data-ttu-id="2db96-174">toostart веб-приложения, необходимо указать hello имя и группе ресурсов hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2db96-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="2db96-175">Управление профилями публикации веб-приложений</span><span class="sxs-lookup"><span data-stu-id="2db96-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="2db96-176">Каждый веб-приложения имеется профиль публикации, который можно использовать toopublish приложений, несколько операций могут выполняться в профилях публикации.</span><span class="sxs-lookup"><span data-stu-id="2db96-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="2db96-177">Получение профиля публикации</span><span class="sxs-lookup"><span data-stu-id="2db96-177">Get Publishing Profile</span></span>
<span data-ttu-id="2db96-178">tooget hello профиль для веб-приложения, используйте публикации:</span><span class="sxs-lookup"><span data-stu-id="2db96-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="2db96-179">Эта команда отображает hello публикации профиль toohello командной строки также выходных данных hello публикации профиль tooa текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="2db96-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="2db96-180">Сброс профиля публикации</span><span class="sxs-lookup"><span data-stu-id="2db96-180">Reset Publishing Profile</span></span>
<span data-ttu-id="2db96-181">tooreset, оба hello пароль публикации для FTP и веб-развертывания для веб-приложения, используйте:</span><span class="sxs-lookup"><span data-stu-id="2db96-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="2db96-182">Управление сертификатами веб-приложения</span><span class="sxs-lookup"><span data-stu-id="2db96-182">Manage Web App Certificates</span></span>
<span data-ttu-id="2db96-183">toolearn о как toomanage веб-приложения сертификаты, в разделе [привязки SSL-сертификаты с помощью PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="2db96-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="2db96-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2db96-184">Next Steps</span></span>
* <span data-ttu-id="2db96-185">toolearn о поддержке PowerShell диспетчера ресурсов Azure в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="2db96-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="2db96-186">toolearn о средах службы приложений, в разделе [tooApp введение среды службы.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="2db96-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="2db96-187">в разделе toolearn об управлении сертификатами SSL службы приложения с помощью PowerShell, [привязки SSL-сертификаты с помощью PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="2db96-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="2db96-188">toolearn о hello полный список командлетов PowerShell на основе диспетчера ресурсов Azure для веб-приложения Azure в разделе [Справочник по командлетам Azure командлетов PowerShell диспетчера ресурсов Azure приложения Web.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="2db96-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="2db96-189">в разделе toolearn об управлении службы приложений, используя интерфейс командной строки, [XPlat-CLI Using Azure Resource Manager-Based для веб-приложения Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2db96-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

