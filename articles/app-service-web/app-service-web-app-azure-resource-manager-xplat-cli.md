---
title: "Кроссплатформенные средства командной строки на основе Azure Resource Manager для веб-приложений Azure | Документация Майкрософт"
description: "Узнайте, как использовать новые кроссплатформенные средства командной строки на основе Azure Resource Manager для управления веб-приложениями Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="c0977-103">Использование кроссплатформенного интерфейса командной строки на основе Azure Resource Manager для службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="c0977-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0977-104">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="c0977-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="c0977-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0977-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="c0977-106">Версия кроссплатформенного средства командной строки Microsoft Azure 0.10.5 включает новые команды,</span><span class="sxs-lookup"><span data-stu-id="c0977-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="c0977-107">которые позволяют использовать команды PowerShell на основе Azure Resource Manager для управления службой приложений.</span><span class="sxs-lookup"><span data-stu-id="c0977-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span></span>

<span data-ttu-id="c0977-108">Дополнительные сведения об управлении группами ресурсов см. в статье об [управлении ресурсами и группами ресурсов Azure с помощью интерфейса командной строки Azure](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c0977-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="c0977-109">Попробуйте также [Azure CLI 2.0](https://github.com/Azure/azure-cli). Это интерфейс командной строки нового поколения, написанный на языке Python, для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c0977-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="c0977-110">Управление планами службы приложений</span><span class="sxs-lookup"><span data-stu-id="c0977-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="c0977-111">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="c0977-111">Create an App Service Plan</span></span>
<span data-ttu-id="c0977-112">Чтобы создать план службы приложений, используйте команду **azure appserviceplan create**.</span><span class="sxs-lookup"><span data-stu-id="c0977-112">To create an app service plan, use the **azure appserviceplan create** command.</span></span>

<span data-ttu-id="c0977-113">Ниже описаны его параметры.</span><span class="sxs-lookup"><span data-stu-id="c0977-113">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="c0977-114">**--resource-group**: группа ресурсов, в которую входит новый план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c0977-114">**--resource-group**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="c0977-115">**--name**: имя плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c0977-115">**--name**: name of the app service plan.</span></span>
* <span data-ttu-id="c0977-116">**--location**: расположение плана службы.</span><span class="sxs-lookup"><span data-stu-id="c0977-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="c0977-117">**--sku**: ценовая категория (SKU).</span><span class="sxs-lookup"><span data-stu-id="c0977-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span></span> <span data-ttu-id="c0977-118">Варианты: F1 (бесплатный); D1 (общедоступный);</span><span class="sxs-lookup"><span data-stu-id="c0977-118">D1 (Shared).</span></span> <span data-ttu-id="c0977-119">B1 (малый базовый), B2 (средний базовый) и B3 (крупный базовый);</span><span class="sxs-lookup"><span data-stu-id="c0977-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="c0977-120">S1 (малый стандартный), S2 (средний стандартный) и S3 (крупный стандартный);</span><span class="sxs-lookup"><span data-stu-id="c0977-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="c0977-121">P1 (малый премиум), P2 (средний премиум) и P3 (крупный премиум).</span><span class="sxs-lookup"><span data-stu-id="c0977-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="c0977-122">**--instances**: число рабочих служб в плане службы приложений. Значение по умолчанию — 1.</span><span class="sxs-lookup"><span data-stu-id="c0977-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span></span>

<span data-ttu-id="c0977-123">Пример использования этого командлета:</span><span class="sxs-lookup"><span data-stu-id="c0977-123">Example to use this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="c0977-124">Создание плана службы приложений Linux</span><span class="sxs-lookup"><span data-stu-id="c0977-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="c0977-125">Это можно сделать с помощью той же команды **azure appserviceplan create** с дополнительным параметром **--islinux true**.</span><span class="sxs-lookup"><span data-stu-id="c0977-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span></span> <span data-ttu-id="c0977-126">Обратите внимание на ограничения и регионы, описанные в статье [Вводные сведения о службе приложений на платформе Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c0977-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="c0977-127">Получение списка существующих планов службы приложений</span><span class="sxs-lookup"><span data-stu-id="c0977-127">List Existing App Service Plans</span></span>
<span data-ttu-id="c0977-128">Чтобы получить список существующих планов службы приложений, используйте команду **azure appserviceplan list**.</span><span class="sxs-lookup"><span data-stu-id="c0977-128">To list the existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="c0977-129">Чтобы получить список всех планов службы приложений для определенной группы ресурсов, используйте такую команду:</span><span class="sxs-lookup"><span data-stu-id="c0977-129">To list all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="c0977-130">Чтобы получить определенный план службы приложений, используйте команду **azure appserviceplan show**.</span><span class="sxs-lookup"><span data-stu-id="c0977-130">To get a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="c0977-131">Настройка существующего плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="c0977-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="c0977-132">Чтобы изменить параметры существующего плана службы приложений, используйте команду **azure appserviceplan config**.</span><span class="sxs-lookup"><span data-stu-id="c0977-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span></span> <span data-ttu-id="c0977-133">Вы можете изменить SKU и число рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="c0977-133">You can change the sku, and the number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="c0977-134">Масштабирование плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="c0977-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="c0977-135">Чтобы масштабировать существующий план службы приложений, используйте команду:</span><span class="sxs-lookup"><span data-stu-id="c0977-135">To scale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a><span data-ttu-id="c0977-136">Изменение SKU для плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="c0977-136">Changing the SKU of an App Service Plan</span></span>
<span data-ttu-id="c0977-137">Чтобы изменить SKU для существующего плана службы приложений, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c0977-137">To change the sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="c0977-138">Удаление существующего плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="c0977-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="c0977-139">Чтобы удалить существующий план службы приложений, сначала необходимо переместить или удалить все назначенные приложения.</span><span class="sxs-lookup"><span data-stu-id="c0977-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span></span> <span data-ttu-id="c0977-140">Затем с помощью команды **azure webapp delete** можно удалить план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c0977-140">Then using the **azure webapp delete** command you can delete the app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="c0977-141">Управление приложениями службы приложений</span><span class="sxs-lookup"><span data-stu-id="c0977-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="c0977-142">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="c0977-142">Create a web app</span></span>
<span data-ttu-id="c0977-143">Чтобы создать веб-приложение, используйте команду **azure webapp create**.</span><span class="sxs-lookup"><span data-stu-id="c0977-143">To create a web app, use the **azure webapp create** command.</span></span>

<span data-ttu-id="c0977-144">Ниже описаны его параметры.</span><span class="sxs-lookup"><span data-stu-id="c0977-144">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="c0977-145">**--name**: имя нового веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c0977-145">**--name**: name for the web app.</span></span>
* <span data-ttu-id="c0977-146">**--plan**: имя плана службы приложений, в котором будет размещено веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="c0977-146">**--plan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="c0977-147">**--resource-group**: группа ресурсов, в которую входит этот план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c0977-147">**--resource-group**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="c0977-148">**--location**: расположение веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c0977-148">**--location**: the web app location.</span></span>

<span data-ttu-id="c0977-149">Пример использования этого командлета:</span><span class="sxs-lookup"><span data-stu-id="c0977-149">Example to use this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="c0977-150">Удаление существующего приложения</span><span class="sxs-lookup"><span data-stu-id="c0977-150">Delete an existing app</span></span>
<span data-ttu-id="c0977-151">Удалить существующее приложение можно с помощью команды **azure webapp delete**.</span><span class="sxs-lookup"><span data-stu-id="c0977-151">To delete an existing app, you can use the **azure webapp delete** command.</span></span> <span data-ttu-id="c0977-152">Необходимо указать имя приложения и имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c0977-152">You need to specify the name of the app and the resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="c0977-153">Список существующих приложений</span><span class="sxs-lookup"><span data-stu-id="c0977-153">List existing apps</span></span>
<span data-ttu-id="c0977-154">Чтобы получить список существующих приложений, используйте команду **azure webapp list**.</span><span class="sxs-lookup"><span data-stu-id="c0977-154">To list the existing apps, use the **azure webapp list** command.</span></span>

<span data-ttu-id="c0977-155">Чтобы получить список всех приложений в определенной группе ресурсов, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c0977-155">To list all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="c0977-156">Чтобы получить определенное приложение, используйте команду **azure webapp show**.</span><span class="sxs-lookup"><span data-stu-id="c0977-156">To get a specific app, use the **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="c0977-157">Настройка существующего приложения</span><span class="sxs-lookup"><span data-stu-id="c0977-157">Configure an existing app</span></span>
<span data-ttu-id="c0977-158">Чтобы изменить параметры и конфигурацию существующего приложения, используйте команду **azure webapp config set**.</span><span class="sxs-lookup"><span data-stu-id="c0977-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span></span>

<span data-ttu-id="c0977-159">Пример 1. Изменение PHP-версии приложения</span><span class="sxs-lookup"><span data-stu-id="c0977-159">Example (1): change the php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="c0977-160">Пример 2. Добавление или изменение параметров приложения:</span><span class="sxs-lookup"><span data-stu-id="c0977-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="c0977-161">Чтобы узнать, какие еще конфигурации можно изменить, используйте команду **azure webapp config set -h**.</span><span class="sxs-lookup"><span data-stu-id="c0977-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span></span>

### <a name="change-the-state-of-an-existing-app"></a><span data-ttu-id="c0977-162">Изменение состояния существующего приложения</span><span class="sxs-lookup"><span data-stu-id="c0977-162">Change the state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="c0977-163">Перезапуск приложения</span><span class="sxs-lookup"><span data-stu-id="c0977-163">Restart an app</span></span>
<span data-ttu-id="c0977-164">Чтобы перезапустить приложение, укажите имя приложения и его группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c0977-164">To restart an app, you must specify the name and resource group of the app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="c0977-165">Остановка приложения</span><span class="sxs-lookup"><span data-stu-id="c0977-165">Stop an app</span></span>
<span data-ttu-id="c0977-166">Чтобы остановить приложение, укажите имя приложения и его группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c0977-166">To stop an app, you must specify the name and resource group of the app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="c0977-167">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="c0977-167">Start an app</span></span>
<span data-ttu-id="c0977-168">Чтобы запустить приложение, укажите имя приложения и его группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c0977-168">To start an app, you must specify the name and resource group of the app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="c0977-169">Управление профилями публикации приложения</span><span class="sxs-lookup"><span data-stu-id="c0977-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="c0977-170">У каждого приложения есть профиль публикации, который может использоваться для публикации кода.</span><span class="sxs-lookup"><span data-stu-id="c0977-170">Each app has a publishing profile that can be used to publish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="c0977-171">Получение профиля публикации</span><span class="sxs-lookup"><span data-stu-id="c0977-171">Get Publishing Profile</span></span>
<span data-ttu-id="c0977-172">Чтобы получить профиль публикации для приложения, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c0977-172">To get the publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="c0977-173">Эта команда выводит в командной строке имя публикации профиля пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="c0977-173">This command echoes the publishing profile username and password to the command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="c0977-174">Управление именами узлов приложения</span><span class="sxs-lookup"><span data-stu-id="c0977-174">Manage app hostnames</span></span>
<span data-ttu-id="c0977-175">Чтобы управлять привязками имен узлов для приложения, используйте команду **azure webapp config hostnames**.</span><span class="sxs-lookup"><span data-stu-id="c0977-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="c0977-176">Список привязок имен узлов</span><span class="sxs-lookup"><span data-stu-id="c0977-176">List hostname bindings</span></span>
<span data-ttu-id="c0977-177">Чтобы получить текущие привязки имен узлов для приложения, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c0977-177">To get the current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="c0977-178">Добавление привязок имен узлов</span><span class="sxs-lookup"><span data-stu-id="c0977-178">Add hostname bindings</span></span>
<span data-ttu-id="c0977-179">Чтобы добавить привязки имен узлов в приложение, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c0977-179">To add hostname bindings to an app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="c0977-180">Удаление привязок имен узлов</span><span class="sxs-lookup"><span data-stu-id="c0977-180">Delete hostname bindings</span></span>
<span data-ttu-id="c0977-181">Чтобы удалить привязки имен узлов, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c0977-181">To delete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="c0977-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0977-182">Next Steps</span></span>
* <span data-ttu-id="c0977-183">Дополнительные сведения о поддержке интерфейса командной строки в Azure Resource Manager см. в статье об [управлении ресурсами и группами ресурсов Azure с помощью интерфейса командной строки Azure](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c0977-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="c0977-184">Дополнительные сведения об управлении службой приложений с помощью PowerShell см. в статье [Управление веб-приложениями Azure с помощью PowerShell на основе Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c0977-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="c0977-185">Сведения об использовании службы приложений Azure на платформе Linux см. в статье [Вводные сведения о службе приложений на платформе Linux](app-service-linux-intro.md).</span><span class="sxs-lookup"><span data-stu-id="c0977-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>
