---
title: "Команды Azure PowerShell на основе Azure Resource Manager для веб-приложений Azure | Документация Майкрософт"
description: "Узнайте, как использовать новые команды PowerShell на основе Azure Resource Manager для управления веб-приложениями Azure."
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
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a><span data-ttu-id="5f80d-103">Управление веб-приложениями Azure с помощью PowerShell на основе Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5f80d-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f80d-104">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="5f80d-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="5f80d-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f80d-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="5f80d-106">В версии Microsoft Azure PowerShell 1.0.0 добавлены новые команды, позволяющие использовать команды PowerShell на основе Azure Resource Manager для управления веб-приложениями.</span><span class="sxs-lookup"><span data-stu-id="5f80d-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span></span>

<span data-ttu-id="5f80d-107">Дополнительные сведения об управлении группами ресурсов см. в статье [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5f80d-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="5f80d-108">Полный список параметров и возможностей командлетов PowerShell на основе Azure Resource Manager для управления веб-приложениями см. [здесь](https://msdn.microsoft.com/library/mt619237.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f80d-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="5f80d-109">Управление планами службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="5f80d-110">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-110">Create an App Service Plan</span></span>
<span data-ttu-id="5f80d-111">Чтобы создать план службы приложений, используйте командлет **New-AzureRmAppServicePlan**.</span><span class="sxs-lookup"><span data-stu-id="5f80d-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="5f80d-112">Ниже описаны его параметры.</span><span class="sxs-lookup"><span data-stu-id="5f80d-112">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="5f80d-113">**Name**: имя плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f80d-113">**Name**: name of the app service plan.</span></span>
* <span data-ttu-id="5f80d-114">**Location**: расположение плана службы.</span><span class="sxs-lookup"><span data-stu-id="5f80d-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="5f80d-115">**ResourceGroupName**: группа ресурсов, в которую входит новый план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f80d-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="5f80d-116">**Tier** — желаемая ценовая категория. По умолчанию используется значение Free. Кроме того, допустимы варианты Shared, Basic, Standard и Premium.</span><span class="sxs-lookup"><span data-stu-id="5f80d-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="5f80d-117">**WorkerSize** — размер рабочих ролей. По умолчанию Small, если для параметра Tier указано значение Basic, Standard или Premium.</span><span class="sxs-lookup"><span data-stu-id="5f80d-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="5f80d-118">По умолчанию Small, если для параметра Tier указано значение Basic, Standard или Premium; также допустимы варианты Medium и Large.</span><span class="sxs-lookup"><span data-stu-id="5f80d-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="5f80d-119">**NumberofWorkers** — число рабочих служб в плане службы приложений. По умолчанию имеет значение 1.</span><span class="sxs-lookup"><span data-stu-id="5f80d-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span></span> 

<span data-ttu-id="5f80d-120">Пример использования этого командлета:</span><span class="sxs-lookup"><span data-stu-id="5f80d-120">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="5f80d-121">Создание плана службы приложений в среде служб приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="5f80d-122">Чтобы создать план службы приложений в среде службы приложений, вы можете использовать уже известную вам команду **New-AzureRmAppServicePlan** с дополнительными параметрами. Эти параметры определяют имя среды службы приложений и имя группы ресурсов, к которой она принадлежит.</span><span class="sxs-lookup"><span data-stu-id="5f80d-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="5f80d-123">Пример использования этого командлета:</span><span class="sxs-lookup"><span data-stu-id="5f80d-123">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="5f80d-124">Дополнительные сведения о среде службы приложений см. в статье [Введение в среду службы приложений](app-service-app-service-environment-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5f80d-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="5f80d-125">Получение списка существующих планов службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-125">List Existing App Service Plans</span></span>
<span data-ttu-id="5f80d-126">Чтобы получить полный список существующих планов службы приложений, используйте командлет **Get-AzureRmAppServicePlan** .</span><span class="sxs-lookup"><span data-stu-id="5f80d-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="5f80d-127">Чтобы получить список всех планов службы приложений в конкретной подписке, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-127">To list all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="5f80d-128">Чтобы получить список всех планов службы приложений для определенной группы ресурсов, используйте такую команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-128">To list all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="5f80d-129">Чтобы получить сведения о конкретном плане службы приложений, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-129">To get a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="5f80d-130">Настройка существующего плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="5f80d-131">Чтобы изменить параметры существующего плана службы приложений, используйте командлет **Set-AzureRmAppServicePlan** .</span><span class="sxs-lookup"><span data-stu-id="5f80d-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="5f80d-132">Вы можете изменить ценовую категорию, размер и количество рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="5f80d-132">You can change the tier, worker size, and the number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="5f80d-133">Масштабирование плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="5f80d-134">Чтобы масштабировать существующий план службы приложений, используйте команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-134">To scale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a><span data-ttu-id="5f80d-135">Изменение размера рабочих ролей для плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-135">Changing the worker size of an App Service Plan</span></span>
<span data-ttu-id="5f80d-136">Чтобы изменить размер рабочих ролей для существующего плана службы приложений, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-136">To change the size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a><span data-ttu-id="5f80d-137">Изменение ценовой категории для плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-137">Changing the Tier of an App Service Plan</span></span>
<span data-ttu-id="5f80d-138">Чтобы изменить ценовую категорию для существующего плана службы приложений, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-138">To change the tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="5f80d-139">Удаление существующего плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="5f80d-140">Чтобы удалить имеющийся план службы приложений, сначала нужно переместить или удалить все назначенные веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5f80d-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span></span> <span data-ttu-id="5f80d-141">Затем с помощью командлета **Remove-AzureRmAppServicePlan** можно удалить план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f80d-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="5f80d-142">Управление веб-приложениями службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="5f80d-143">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5f80d-143">Create a Web App</span></span>
<span data-ttu-id="5f80d-144">Чтобы создать веб-приложение, используйте командлет **New-AzureRmWebApp**.</span><span class="sxs-lookup"><span data-stu-id="5f80d-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="5f80d-145">Ниже описаны его параметры.</span><span class="sxs-lookup"><span data-stu-id="5f80d-145">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="5f80d-146">**Name**: имя нового веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5f80d-146">**Name**: name for the web app.</span></span>
* <span data-ttu-id="5f80d-147">**AppServicePlan**: имя плана службы приложений, в котором будет размещено веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="5f80d-147">**AppServicePlan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="5f80d-148">**ResourceGroupName**: группа ресурсов, в которую входит этот план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f80d-148">**ResourceGroupName**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="5f80d-149">**Location**: расположение веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5f80d-149">**Location**: the web app location.</span></span>

<span data-ttu-id="5f80d-150">Пример использования этого командлета:</span><span class="sxs-lookup"><span data-stu-id="5f80d-150">Example to use this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="5f80d-151">Создание веб-приложения в среде службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="5f80d-152">Чтобы создать веб-приложения в среде службы приложений,</span><span class="sxs-lookup"><span data-stu-id="5f80d-152">To create a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="5f80d-153">вы можете использовать уже известную вам команду **New-AzureRmWebApp** с дополнительными параметрами. Эти параметры определяют имя среды службы приложений и имя группы ресурсов, к которой она принадлежит.</span><span class="sxs-lookup"><span data-stu-id="5f80d-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="5f80d-154">Дополнительные сведения о среде службы приложений см. в статье [Введение в среду службы приложений](app-service-app-service-environment-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5f80d-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="5f80d-155">Удаление существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5f80d-155">Delete an existing Web App</span></span>
<span data-ttu-id="5f80d-156">Чтобы удалить существующее веб-приложение, можно использовать командлет **Remove-AzureRmWebApp** , указав имя веб-приложения и имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5f80d-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="5f80d-157">Список существующих веб-приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-157">List existing Web Apps</span></span>
<span data-ttu-id="5f80d-158">Чтобы получить список существующих веб-приложений, используйте командлет **Get-AzureRmWebApp** .</span><span class="sxs-lookup"><span data-stu-id="5f80d-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="5f80d-159">Чтобы получить список всех веб-приложений в вашей подписке, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-159">To list all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="5f80d-160">Чтобы получить список всех веб-приложений для определенной группы ресурсов, используйте такую команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-160">To list all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="5f80d-161">Чтобы получить сведения о конкретном веб-приложении, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-161">To get a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="5f80d-162">Настройка существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5f80d-162">Configure an existing Web App</span></span>
<span data-ttu-id="5f80d-163">Чтобы изменить параметры и конфигурацию имеющегося веб-приложения, используйте командлет **Set-AzureRmWebApp**.</span><span class="sxs-lookup"><span data-stu-id="5f80d-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="5f80d-164">Полный список параметров см. на [странице описания командлета](https://msdn.microsoft.com/library/mt652487.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f80d-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="5f80d-165">Пример 1. Использование командлета для изменения строк подключения:</span><span class="sxs-lookup"><span data-stu-id="5f80d-165">Example (1): use this cmdlet to change connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="5f80d-166">Пример 2. Добавление или изменение параметров приложения:</span><span class="sxs-lookup"><span data-stu-id="5f80d-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="5f80d-167">Пример 3. Настройка веб-приложения для запуска в 64-разрядном режиме:</span><span class="sxs-lookup"><span data-stu-id="5f80d-167">Example (3):  set the web app to run in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a><span data-ttu-id="5f80d-168">Изменение состояния существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5f80d-168">Change the state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="5f80d-169">Перезапуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5f80d-169">Restart a web app</span></span>
<span data-ttu-id="5f80d-170">Чтобы перезапустить веб-приложение, нужно указать имя веб-приложения и его группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5f80d-170">To restart a web app, you must specify the name and resource group of the web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="5f80d-171">Остановка веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5f80d-171">Stop a web app</span></span>
<span data-ttu-id="5f80d-172">Чтобы остановить веб-приложение, нужно указать имя веб-приложения и его группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5f80d-172">To stop a web app, you must specify the name and resource group of the web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="5f80d-173">Запуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5f80d-173">Start a web app</span></span>
<span data-ttu-id="5f80d-174">Чтобы запустить веб-приложение, нужно указать имя веб-приложения и его группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5f80d-174">To start a web app, you must specify the name and resource group of the web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="5f80d-175">Управление профилями публикации веб-приложений</span><span class="sxs-lookup"><span data-stu-id="5f80d-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="5f80d-176">У каждого веб-приложения есть профиль публикации, который можно использовать для публикации приложений. Эти профили поддерживают несколько операций.</span><span class="sxs-lookup"><span data-stu-id="5f80d-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="5f80d-177">Получение профиля публикации</span><span class="sxs-lookup"><span data-stu-id="5f80d-177">Get Publishing Profile</span></span>
<span data-ttu-id="5f80d-178">Чтобы получить профиль публикации для веб-приложения, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-178">To get the publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="5f80d-179">Эта команда выводит профиль публикации в командную строку и текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="5f80d-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="5f80d-180">Сброс профиля публикации</span><span class="sxs-lookup"><span data-stu-id="5f80d-180">Reset Publishing Profile</span></span>
<span data-ttu-id="5f80d-181">Чтобы сбросить для веб-приложения пароль публикации для FTP и веб-развертывания, используйте такую команду:</span><span class="sxs-lookup"><span data-stu-id="5f80d-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="5f80d-182">Управление сертификатами веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5f80d-182">Manage Web App Certificates</span></span>
<span data-ttu-id="5f80d-183">Дополнительные сведения об управлении сертификатами веб-приложения см. в статье [Привязка SSL-сертификатов с помощью PowerShell](app-service-web-app-powershell-ssl-binding.md).</span><span class="sxs-lookup"><span data-stu-id="5f80d-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="5f80d-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f80d-184">Next Steps</span></span>
* <span data-ttu-id="5f80d-185">Сведения о поддержке PowerShell в Azure Resource Manager см. в статье [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5f80d-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="5f80d-186">Сведения о средах службы приложений см. в статье [Введение в среду службы приложений](app-service-app-service-environment-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5f80d-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="5f80d-187">Сведения об управлении SSL-сертификатами службы приложений с помощью PowerShell см. в статье [Привязка SSL-сертификатов с помощью PowerShell](app-service-web-app-powershell-ssl-binding.md).</span><span class="sxs-lookup"><span data-stu-id="5f80d-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="5f80d-188">Полный список командлетов PowerShell на основе Azure Resource Manager для управления веб-приложениями см. [здесь](https://msdn.microsoft.com/library/mt619237.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f80d-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="5f80d-189">Дополнительные сведения об управлении службой приложений с помощью интерфейса командной строки см. в статье [Using Azure Resource Manager-Based XPlat CLI for Azure Web App](app-service-web-app-azure-resource-manager-xplat-cli.md) (Использование кроссплатформенного интерфейса командной строки на основе Azure Resource Manager для веб-приложения Azure).</span><span class="sxs-lookup"><span data-stu-id="5f80d-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

